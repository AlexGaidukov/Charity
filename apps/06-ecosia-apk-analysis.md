# Ecosia: разбор APK (Android 154.0.8037.126.54)

Файлы: XAPK с APKPure (`com.ecosia.android.apk` 274 МБ + split-модули `chrome.apk` 8 МБ и `on_demand.apk` 0,7 МБ), для сверки базовый APK 156.0.8078.74.57 с Uptodown. Package `com.ecosia.android`, только arm64, Chromium 154.
Подлинность: все файлы подписаны одним сертификатом **Ecosia GmbH** (CN=ecosia.org, Wittenberg, DE; SHA-256 `f522d5df…ec765c`). Сборки с двух независимых зеркал совпадают по подписи, у APK 156 есть Source Stamp Google Play.
Метод: распаковка, манифест (aapt2), ресурсы и строки UI (aapt2 dump resources), байткод (dexdump -d), строки `libchrome.so`. Чужой код не запускали, сторонние декомпиляторы не использовали. Снято 2026-11-23.
Пометки: **[факт]** — прямо видно в коде/строках; **[вывод]** — следует из фактов, но код целиком не читали.

---

## Резюме на один экран

1. **Это не своё приложение, а перебрендированный Chromium** (как Chrome, только с логотипом Ecosia), сделанный на white-label-платформе. Собственный код Ecosia — тонкий слой модулей `wl.android.modules.brand.ecosia.*`: новая вкладка с деревьями, профиль с семенами и уровнями, рефералка, AI-режим, онбординг. Всё остальное, около 99% кода, — стоковый Chromium. [факт + вывод]
2. **Деньги — с поиска.** Поиск по умолчанию идёт на `ecosia.org/search`. Установка помечается партнёрским typetag из install referrer, а запросы с Ecosia-доменов уходят с заголовком `X-Ecosia-App`. Так Ecosia отличает поиск из приложения и атрибутирует выручку. [факт]
3. **Блокировщик рекламы eyeo (Adblock Plus) встроен и по умолчанию включает «Acceptable Ads»**: часть рекламы пропускается. У eyeo это платная программа для рекламодателей. [факт; что Ecosia получает долю, — гипотеза]
4. **Геймификация двухуровневая**:
   - гость видит на новой вкладке счётчик поисков («Searches in Ecosia plant trees!») и глобальный счётчик деревьев;
   - с аккаунтом появляются **семена** («Collect seeds every day you use Ecosia»), **growth points** и **20 уровней** с эко-названиями (Ecocurious → Rainforest reviver). [факт]
5. **Маркетинговый стек тяжёлый**: Singular (атрибуция установок), Braze (push, in-app, карточки на новой вкладке), Snowplow (свои события, `sp.ecosia.org`), Unleash (фичефлаги), Auth0 (вход), Firebase Messaging. Целевые конверсии для рекламы: **onboarding_start, onboarding_complete, 1-й, 5-й и 10-й поиск**. [факт]
6. **Google-сервисы Chromium проксируются через свои домены** `*.ecosia-browser.net` (обновление компонентов, перевод, проверка утечек паролей, краш-репорты, проверка связи). Декларация «приватность» подкреплена инфраструктурно. [факт]

---

## 1. Архитектура

| Слой | Что это | Где |
|---|---|---|
| Движок | **Chromium 154** (`org.chromium.chrome.*`), весь браузер нативный, C++ | `libchrome.so` (182 МБ) |
| White-label-слой | Пути сборки `third_party/white_label/chromium/...`, Java-пакеты `wl.android.modules.core.*` (quick delete), `wl.components.experiments`, `wl.components.extra_headers_bridge`. Это платформа для брендированных браузеров; вендор в строках не назван [вывод] | `libchrome.so`, `classes.dex` |
| Бренд Ecosia | `wl.android.modules.brand.ecosia.*`: `auth` (ImpactApiService), `ntp_header` (шапка новой вкладки с impact), `ntp_first_search`, `referrals`, `ai_mode_provider`, `singular`, `network`; `brand.common.onboarding.OnboardingActivity`. UI на Jetpack Compose + View | `classes.dex` (обфусцирован R8) |
| Блокировщик рекламы | **eyeo Chromium SDK** (`components/adblock/*`): EasyList, региональные списки, `exceptionrules.txt` (Acceptable Ads), телеметрия на `ecosia.telemetry.eyeo.com` | `libchrome.so` |
| Split-модули | `chrome` и `on_demand` обязательны (`requiredSplitTypes`): без них установка падает с `INSTALL_FAILED_MISSING_SPLIT`. Поэтому одиночный APK с Uptodown не ставится | `chrome.apk`, `on_demand.apk` |

Прочее в манифесте: ARCore (`libarcore_sdk_c.so`), Credential Manager / passkeys, NFC, Bluetooth, камера и микрофон. Это стандартный набор разрешений Chrome, а не особенности Ecosia. Ecosia добавляет собственные `com.ecosia.android.TOS_ACKED` и `READ_WRITE_BOOKMARK_FOLDERS`. Видеоролик онбординга вшит в APK (`res/6V.mp4`). [факт]

## 2. Как приложение зарабатывает и считает «вклад»

```
Установка ──install referrer──► typetag (tt) сохраняется ──► поиск ecosia.org/search?q=…&tt=…
                                                             + заголовок X-Ecosia-App
Поиск на ecosia.org ──► кука ECFG (в т.ч. счётчик поисков) ──► приложение читает её
                                                              и показывает «N searches» на новой вкладке
Вход в аккаунт (Auth0) ──► POST api.ecosia.org/api/v2/accounts/impact/visits
                          ◄── seeds (balance, lastVisitAt), growthPoints, level (номер, очки до следующего)
```

- **Поисковики** (`TemplateURL`): `www.ecosia.org/search?q=`, `/images`, `/news`, `/videos`, подсказки `ac.ecosia.org/autocomplete`. Есть экран выбора поисковика по закону (DMA: «Based on a law in your region, you need to choose your browser and search engine»). [факт]
- **Typetag**: «Stored typetag from install referrer», «Failed to parse install referrer for typetag». В нативном коде есть `chrome_dse_attribution=1&tt=0387qhzr` — метка трафика из браузера по умолчанию. [факт] Typetag — механизм партнёрской атрибуции поисковой выручки у Ecosia. [вывод]
- **Кука ECFG** — «ECFG cookie stored - search count: …». Счётчик поисков гостя живёт в куке сайта, приложение синхронизирует её со своими настройками. **ECCC** хранит согласие на аналитику («ECCC cookie stored - analytics allowed»). [факт] Отсюда: личный счётчик гостя локальный и пропадёт при очистке данных. [вывод]
- **Глобальный счётчик на новой вкладке**: `ImpactData(treeCount, treeRate, treeLastUpdate, investmentAmount, investmentRate, investmentLastUpdate)` и строка «Investments amount per second». Сервер отдаёт значение и скорость прироста, а клиент **досчитывает «тикающий» счётчик сам** между обновлениями. [факт + вывод]
- **Персональный impact** (`ImpactVisitResponse`): `Seeds(balanceAmount, isModified, lastVisitAt, updatedAt)`, `GrowthPoints(balanceAmount)`, `Level(number, growthPointsToUnlockNextLevel, growthPointsEarnedTowardsNextLevel)`. Эндпоинт называется `impact/visits`, то есть семена начисляются **за дневной визит, а не за поиск** («Collect seeds every day you use Ecosia»). [факт + вывод]

## 3. Функционал по экранам (из строк UI и ключей настроек)

### Онбординг
- Видео-фон, заголовок **«Real change at your fingertips»**, подзаголовок «Join 20 million people making a difference every day», кнопка **Get started** (подтверждено на эмуляторе, [`screenshots/ecosia/01-first-launch.png`](../screenshots/ecosia/01-first-launch.png)).
- Дальше экран «Welcome to [Ecosia]» с **Sign in / Maybe later**. Флаг `ecosia_onboarding_pending_welcome_sign_in` говорит, что предложение войти может всплыть позже, если его отложили. [факт + вывод]
- События: `welcome_screen` · `next` / `skip` / `close`; конверсии в Singular `onboarding_start` → `onboarding_complete`. [факт]
- Промо «браузер по умолчанию»: «Make all your browsing support climate action / People who set Ecosia as their default browser help us plant more trees.» · «Did you know? You can use Ecosia any time you tap links…» · Make default in settings / Maybe later. [факт]

### Новая вкладка (NTP), главный экран
- **Шапка с ротацией заголовков** (`rotating_title`, конфиг с `cdn.ecosia.org/rotating-titles/v1`, поля `version, rotation, order, titles`, категории). Заголовки меняются удалённо, без релиза. [факт]
- **Карточка первого поиска** (`first_search_card`, `FirstSearchComposeView`) до первого запроса; после него `ecosia_ntp_first_search_done`. [факт]
- **Impact-карточка**: «Searches in %s plant trees!» / «Plant trees with every search.», глобальный счётчик деревьев, сумма инвестиций, ссылка на финотчёты (`ecosia_impact_card_financial_reports`). Тултип и хинты («seeds hint», «explore hint») закрываются по одному разу. [факт]
- **Нудж на вход** (`account_nudge_card`), флаг Unleash `mob_android_ntp_login_button`. [факт]
- **Карточки Braze** (`NtpBrazeCard`) — маркетинг может подсовывать карточки на новую вкладку удалённо (флаг `mob_android_braze_integration`). [факт]
- Top sites, Discover-лента статей (из Chromium), кастомные темы и цвета Ecosia, кнопка AI. [факт]

### Профиль: семена и уровни
- «Your Ecosia» / «Your profile» / «Find your impact and personal information inside your profile». Гость отображается как «Guest user». [факт]
- **Seeds**: «Seeds symbolize your own impact», «Collect seeds every day you use Ecosia and see the climate impact you're having.», «Learn more about seeds» (support.ecosia.org/article/844-seed-counter). [факт]
- **20 уровней** «Level N - Название» (в ресурсах подряд; порядок в ресурсах может не совпадать с порядком уровней): Ecocurious, Planet protector, Carbon neutralizer, Seeker of sustainability, Branch builder, Eco enthusiast, Carbon cutter, Seed sower, Emission eliminator, Sustainability sage, Earth advocate, Green explorer, Seed superstar, Planet pal, Seedling supporter, Biodiversity bestie, Forest friend, Wildlife protector, Eco explorer, Rainforest reviver. Уровень 1 — Ecocurious (так же на сайте: «Level 1 - Ecocurious»). На эмуляторе после регистрации был **Level 2 — Green explorer**, то есть порядок в ресурсах не совпадает с порядком уровней. [факт, см. [онбординг](06-ecosia-onboarding.md)]
- Вход через Auth0 (`login.ecosia.org`, `auth0.api.ecosia.org`): Sign up / Sign in / Sign out. [факт]

### Рефералка («Growing together»)
- «Increase your positive impact on the planet by inviting your friends to join Ecosia.» · Share your link / Copy / More sharing methods · «Your invites» · счётчик «X friends invited» на новой вкладке. [факт]
- How it works: 1) друг открывает ссылку (**iOS only**), 2) скачивает приложение из App Store / Google Play, 3) открывает вторую ссылку из сообщения. Текст шаринга: «Check this out: Ecosia plants trees when you search the web! 🌳». API `v1/referrals/referral/`, `v1/referrals/claim/`; на Android реферал засчитывается через install referrer. [факт] Механика неуклюжая: на Android нужно открыть вторую ссылку уже после установки. [вывод]
- Награды за приглашение в строках нет: ни денег, ни бонусных семян, только «impact». [факт по строкам]
- На эмуляторе входа в рефералку не нашлось даже с аккаунтом, справка называется `refer-a-friend-ios-only`. На Android код есть, но экран не показывается. [факт + вывод, см. [онбординг](06-ecosia-onboarding.md)]

### AI
- AI Mode / AI chat (`/ai-chat`, «Ask, search, browse…», «Ask Ecosia anything»). Режимы: Standard AI Chat · Think longer · Learning · Display sources · Generate images (флаг `mob_android_ai_mode_image_generation`). Загрузка файлов `api.ecosia.org/v2/conversations/files/upload`. [факт]
- **Для AI-инструментов нужен аккаунт**: «To use this feature you need to be signed in to an Ecosia account.» / «Sign in for more AI features». AI служит главным поводом зарегистрироваться. [факт + вывод]
- Опт-аут истории чатов (`ecosia.org/chat_threads_opt_out`). Строки Gemini / Glic остались от Chromium; включены ли они, по коду не видно. [факт + вывод]

### Приватность и инструменты
- **Блокировщик рекламы** с иконкой-щитом в тулбаре («N ads blocked on this page», пауза/возобновление по сайту, свои списки фильтров). **Acceptable Ads включены по умолчанию**: «This feature is turned on by default, but you can turn it off at any time.» [факт]
- **Quick delete** — кнопка в адресной строке, стирает данные, есть исключения для сайтов. [факт]
- Тумблер «Help improve Ecosia» (`wl_settings_enable_analytics`) — согласие на аналитику, хранится в куке ECCC. [факт]
- Rate app («Like Ecosia? Show us some love»), feedback по email. [факт]

## 4. Трекинг и маркетинг

| SDK / сервис | Что делает | Детали |
|---|---|---|
| **Singular** (через бэкенд Ecosia `v2/attribution/launch`, `/event`) | атрибуция установок для платной рекламы | события `onboarding_start`, `onboarding_complete`, `first_search`, `fifth_search`, `tenth_search`; Meta install referrer; отправка сессий не чаще заданного интервала |
| **Snowplow** (`sp.ecosia.org`) | продуктовая аналитика | свои схемы `org.ecosia/inapp_search_event`, `android_install_event`, `app_user_state_context`, `abtest_context`, `eccc_context` (согласие). Категории событий: `welcome_screen`, `first_search_card`, `account_nudge_card`, `ai_search_cta`, `default_browser_promo`, `invite_screen`, `link_copying`, `impact`, `profile`, `menu`, `top_sites`, `widget`, `sign_in`, `sign_up` |
| **Braze** | push, in-app, content cards, гео-триггеры | эндпоинт `sondheim.braze.com`; карточки на новой вкладке; Firebase Cloud Messaging для доставки |
| **Unleash** (`api.ecosia.org/v2/toggles`) | фичефлаги и A/B | кеш по версии приложения и региону; видимые флаги `mob_android_ntp_login_button`, `mob_android_braze_integration`, `mob_android_ai_mode_image_generation` |
| **eyeo telemetry** | активные пинги блокировщика | `ecosia.telemetry.eyeo.com`, `eyeochromium_activeping` |
| **Firebase** | push-токены, datatransport | проект `mobile-browser-app` |

Вывод: конверсии «1-й / 5-й / 10-й поиск» для поисковика — то же, что у Grass «100 ч аптайма». Это события, ради которых закупается реклама: выручка начинается с регулярного поиска. [вывод]

## 5. Свои домены вместо Google
`gclient.ecosia-browser.net` (обновления компонентов, время), `translate.ecosia-browser.net`, `pwlookup.ecosia-browser.net` (проверка утечек паролей), `clients.ecosia-browser.net` (краш-репорты, `generate_204`). Стоковый Chromium ходит в эти места на серверы Google. [факт]

## 6. Что это значит для нашего разбора
- **Вклад пользователя пассивный и почти незаметный:** он просто ищет, как раньше. Ecosia компенсирует это визуализацией: тикающий глобальный счётчик, личный счётчик поисков, семена за ежедневный визит, уровни. Сравнить с Grass: там «заработок» в поинтах, здесь «импакт» в деревьях и семенах.
- **Привычку держат ежедневным визитом, а не объёмом:** семена и growth points за каждый день использования. В коде приложения стрика нет, но на веб-странице профиля он есть («Current streak / Longest streak»), как у WCG. Там же коллекция из 22 предметов и метрики, открывающиеся по уровням (см. [онбординг](06-ecosia-onboarding.md)).
- **Регистрацию продают через AI**, а не через импакт: гостю доступно почти всё, кроме AI-инструментов и профиля с семенами.
- **Удалённое управление контентом**: ротация заголовков, карточки Braze, фичефлаги Unleash. Новую вкладку можно перестраивать без релиза. Стоит взять себе.
- **Слабые места:** гостевой счётчик хранится в куке и теряется при очистке; рефералка на Android требует второй ссылки; Acceptable Ads включены по умолчанию в «приватном» браузере.

## Артефакты
Распакованные APK, дампы ресурсов и dexdump лежат во временной папке сессии (`scratchpad/ecosia-unpacked`, `ecosia-xapk`), в репозиторий не кладём. Чтобы повторить: `aapt2 dump xmltree/resources/badging`, `dexdump -d classes.dex` (все три модуля), `strings` по `libchrome.so`, `apksigner verify --print-certs`.
