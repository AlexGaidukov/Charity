# Tab for a Cause / Gladly: декомпиляция и разбор кода

Дата: 2026-11-23. Что разобрано:
- **Chrome-расширение** v6.1 (CRX из Chrome Web Store, id `gibkoahgjfhphbmeiphbcnhehbfdlcgo`);
- **веб-приложение новой вкладки** `tab.gladly.io/newtab/` (legacy React). Исходники восстановлены из публичных source map: 2086 файлов, около 200 своих модулей;
- **v5** (`/v5/login`, серверный рендер): HTML и инлайн-скрипты;
- **мобильное приложение «App for a Cause»** (`io.gladly.appforacause`) и **Safari-расширение Shop for a Cause**: открытый репозиторий `gladly-team/app-for-a-cause`, v1.0.16 от 21.10.2026;
- **бэкенд** GraphQL: открытый репозиторий `gladly-team/tab`, последний коммит 20.04.2026.

Чужой код не запускали, только читали. Вживую новую вкладку под аккаунтом не проходили: браузер Playwright был занят, и без входа v5 отдаёт только страницу логина. Safari-версия (Mac App Store id1579749108) не скачивалась: нужна учётка App Store.

---

## 1. Главное

1. **Расширения как такового почти нет.** CRX весит 10 КБ, в нём три файла, а `permissions: []`. Новая вкладка просто делает редирект на `http://tab.gladly.io/newtab/` (обычный http, CloudFront отвечает 301 на https). Вся логика, реклама и аккаунт живут на сайте. Поэтому утверждение «расширение не может читать ваши данные» технически верно: читать ему нечем.
2. **Продукт живёт в трёх поколениях одновременно**:

   | Версия | Стек | Кто видит |
   |---|---|---|
   | legacy (v3) | React 16 + Relay/GraphQL, Material UI v0 и v1, CRA. Бэкенд AWS Lambda + DynamoDB | старые пользователи (`<body class="legacy">`, `tfac_app_version: legacy`) |
   | v4 | Next.js (`tab-web`), включается cookie `tabV4OptIn` | бета, в коде есть «Switch to V4» |
   | **v5** | **Laravel/Livewire на Laravel Vapor** (Lambda за Cloudflare), Tailwind, сессия `gladly_session` | вход, онбординг, часть настроек, лидерборд, игры, уведомления и мобильное приложение |

   **Поправка после живого прохода** ([walkthrough](07-tab-for-a-cause-walkthrough.md)): новый пользователь после онбординга на v5 получает **v4** («Tab for <cause>», `body.v4`) прямо на `/newtab/`. Legacy называется «Classic» и включается вручную. v4 — гибрид: часть экранов отдаёт Next.js, часть v5 (iframe и ссылки).

   В legacy-коде вход ведёт на `/v5/login`, лидерборд и игры открываются iframe'ами `/v5/leaderboard` и `/v5/games`. Репозитория v5 на GitHub нет: судя по всему, это первая закрытая часть стека.
3. **Обязательная регистрация до первой ценности.** Путь новичка: установка → `onInstalled` открывает `/newtab/first-tab/` → сохраняется install id и время → `/newtab/` → пользователя нет → `/v5/login`. Анонимный режим в коде есть, но выключен: `isAnonymousUserSignInEnabled = () => false`. Вход возможен через Google, Apple или email; Facebook отключён, для старых аккаунтов есть отдельная модалка миграции.
4. **3 дня без рекламы — только на странице входа v5.** При первом визите в `localStorage.tabLoginFirstVisit` пишется время, и пока не прошло 72 часа, `window.shouldShowAds = false`. Обход: `?forceAds=true`. На самой вкладке v4 пауза не действует: вживую реклама появилась уже на 2–3-й вкладке (см. walkthrough).
5. **Монетизация с 2023 года отдана Raptive (бывший AdThrive)**. На вкладке три слота: `raptive-content-ad-1/2` по 300 px справа внизу и `raptive-content-ad-3` шириной 728 px. Собственная библиотека `tab-ads` (Prebid + GAM, обновлялась до 12.2023) в коде закомментирована. Видеореклама true[X] за Hearts ещё подключена (`showVideoAds = () => true`).

## 2. Расширение (CRX v6.1, MV3, сборка 12.10.2022)

| Файл | Что делает |
|---|---|
| `manifest.json` | `chrome_url_overrides.newtab`, пустые `permissions`, `action: {}` |
| `newtab.html/js` | тёмный фон `#121212`, затем `chrome.tabs.update(tab.id, {url: 'http://tab.gladly.io/newtab/'})` (фолбэк через `location.href`) |
| `ext-background.js` | при установке открывает `/newtab/first-tab/`, по клику на иконку открывает новую вкладку, при удалении ставит `setUninstallURL('/newtab/uninstalled/')`, откуда идёт редирект на Google Form с опросом |

Следствия: адресная строка новой вкладки показывает `tab.gladly.io/newtab/`, а не пустое поле. Курсор не встаёт в омнибокс, и поиск Chrome по умолчанию не перехватывается (поиск идёт через виджет, см. ниже). Последнее обновление расширения вышло в октябре 2022, и с тех пор менять его не нужно: всё обновляется на сервере.

## 3. Новая вкладка (legacy), что внутри

**Роуты:** `/newtab/` (дашборд) · `/newtab/settings/widgets|background/` · `/newtab/profile/stats|donate|invite/` · `/newtab/account/` · `/newtab/auth/*` (verify-email, username, missing-email, welcome) · `/newtab/first-tab/` · `/newtab/uninstalled/` · `/newtab/shop`.
Переходы между основными экранами нарочно сделаны полной перезагрузкой страницы, «для загрузки рекламы» (`goTo` в navigation.js): каждый экран заново тянет показы.

**Виджеты:** закладки, часы, заметки, todo, поиск (Bing/Yahoo/CodeFuel, `search.gladly.io`). Фон: цвет, фото, «фото дня» или своя картинка.

**Hearts (виртуальная валюта, в коде `vc`)** — правила на бэкенде:
| Действие | Hearts | Ограничение |
|---|---|---|
| Открыть вкладку | +1 | не чаще раза в 2 с, **не больше 150 за день** (`MAX_DAILY_HEARTS_FROM_TABS`) |
| Посмотреть видеорекламу (true[X], в мобильном AdMob rewarded) | **+100** | не больше 3 роликов в сутки (`isVideoAdEligible`) |
| Приглашённый друг зарегистрировался | **+350** | — |
| Поиск | 0 (начисление закомментировано) | rate-limit: 5/мин, 12/5 мин, 40/день |

Hearts раздаются фондам (`DonateVcMutation`), и квартальный рекламный доход делится пропорционально отданным Hearts. От числа Hearts зависят уровни (`UserLevels`, порог `hearts` на уровень). Сколько денег засчитать за вкладку, сервер берёт из env `EST_MONEY_RAISED_PER_TAB` и прибавляет к счётчику кампании. Это оценка, а не фактический доход.

**Механики вовлечения в коде:** тур для новичка (react-joyride) · уведомления с сервера (`user.notifications`, вариации) · кампании с обратным отсчётом (`MillionRaisedCampaign`, «$1M», «$1.5M», «$2M») · лидерборд (iframe v5) · **Missions / Squads**: групповые цели по вкладкам со стриками (`calculateTabStreak`) · Group Impact, отключён в 04.2026 (`Disable Upstash-backed Group Impact`) · реферальная ссылка, 5 вариантов текста в A/B-тесте («Earn more hearts!», «Double your charitable impact!»…).

**Кросс-продажа своих продуктов прямо в новой вкладке:** Search for a Cause (поиск за пожертвования, Chrome и Firefox), Shop for a Cause (кэшбэк-расширение, сезонные промо Black Friday / Prime Day / Mother's Day, полноэкранные iframe-промо `tab.gladly.io/promos/*`), промо bookshop.org.

**Каузы (ID зашиты в constants):** кошки (Jackson Galaxy Project), собаки, животные, моря, деревья, Black equity, глобальное здоровье, голод, Украина, репродуктивное здоровье, LGBTQ, бедность, демократия, помощь при катастрофах. Каждая кауза доступна отдельным лендингом «Tab for ___».

**B2B-след:** если у пользователя есть `campaignId` и одна из двух каузы (`dYr9lq7`, `WerUli7`), каждая вкладка публикуется в AWS SNS-топик **«Brandfluence»**. Похоже на брендовые кампании, где спонсор платит за вкладки, открытые его аудиторией.

## 4. Трекинг и согласия

| Что | Где |
|---|---|
| Google Analytics 4 `G-LDFLQCKVHG` | legacy |
| Facebook Pixel `1813501258922708` | legacy и v5; на v5 `fbq('init', '')` вызывается **с пустым ID**, срабатывает только noscript-пиксель (баг). Клики по кнопкам входа шлются как `Lead` |
| Reddit Pixel `t2_9btvy` | legacy |
| geoip-js.com (MaxMind) | определение страны / EU |
| Quantcast Choice CMP (свой форк `tab-cmp`) + Google Funding Choices | TCF v2 / USP. Заглушка отвечает рекламным партнёрам **сохранённым** в localStorage согласием, а сам CMP инициализируется через 1,5 с, чтобы не тормозить аукцион |
| Sentry | ошибки |
| feasible.lol | на v5, неизвестный скрипт аналитики |
| PostHog (us.i.posthog.com) | в Safari-расширении Shop for a Cause |
| OneSignal, Branch.io, AdMob, Facebook SDK | мобильное приложение |

## 5. Мобильное приложение «App for a Cause» (Ionic + Capacitor 7)

- **Тонкая оболочка.** Почти каждый экран — iframe на `tab.gladly.io/v5/mobile/*`: `login`, `select-cause`, `set-username`, `verify-email`, `dashboard`, `games`, `leaderboard`, `leaderboard-learn-levels`, `desktop-email`. Нативная часть отвечает только за вход через Firebase (Google/Apple), пуши OneSignal (разрешение запрашивается сразу при старте), Branch (атрибуция рефералов) и рекламу.
- **Монетизация: AdMob rewarded video.** Веб-страница присылает `mobile-screen-reward-ad`, приложение показывает ролик и отправляет `POST /v5/mobile/video-ad-rewarded` (+100 Hearts, лимит 3 в сутки).
- **Мост postMessage:** `mobile-screen-games|leaderboard|change-cause|settings|get-tab-desktop|shop-extension|logout`, `account-delete`, `mobile-open-page`, `mobile-open-external-url`. Проверка origin закомментирована (`// if (event.origin !== ...)`), а Firebase-токен передаётся в URL iframe как `?access_token=` [факт; оценка рисков не входила в задачу].
- **Экран «get-tab-desktop» / `desktop-email`.** Приложение просит email, чтобы прислать ссылку на десктопное расширение. Это ровно то, чего не хватает мобильному лендингу (см. [разбор лендинга](07-tab-for-a-cause-landing-nmt.md), п. 5).
- **iOS: встроенное Safari-расширение Shop for a Cause.** Content scripts на `<all_urls>`, `checkout.js` во всех фреймах, `externally_connectable` для `wild.link` / `wildlinkme`. Это **кэшбэк через партнёрские ссылки Wildlink плюс автоподстановка купонов** на чекауте (Kohl's, JCPenney, Saks, Lands' End, Belk…), то есть модель Honey с отчислением на благотворительность.

## 6. Что это значит для сравнения
- Tab for a Cause — **рекламная площадка**, где благотворительность служит мотивацией. Ресурс пользователя — внимание: показы рекламы на новой вкладке, видео за Hearts, поиск и покупки. Это не ресурс устройства, как у Grass, Salad или BOINC.
- **Hearts — валюта для голосования, а не для денег.** Пользователь не выбирает, сколько отдать: он распределяет, кому достанется общий котёл. Потолки (150 вкладок в день, 3 видео) защищают от накрутки и одновременно ограничивают геймификацию.
- **Воронка рвётся сразу после установки:** обязательная регистрация с верификацией email и username до первой вкладки, а затем 3 дня без рекламы, то есть без реального вклада. Пользователь копит Hearts, которые в эти дни ничем не обеспечены.
- **Рост идёт через кросс-продажу собственных продуктов** (Search, Shop, мобильное приложение, игры) и через B2B-кампании (Brandfluence), а не через само расширение.
- Технический долг заметен: три поколения фронтенда, два UI-фреймворка, полная перезагрузка страницы «ради рекламы», пустой ID Facebook Pixel на v5.

## Воспроизведение
1. CRX: `https://clients2.google.com/service/update2/crx?response=redirect&prodversion=131.0&acceptformat=crx2,crx3&x=id%3Dgibkoahgjfhphbmeiphbcnhehbfdlcgo%26uc`. Отрезать заголовок CRX3 (12 байт + длина), остаток распаковать как zip.
2. Исходники legacy: в `/newtab/` найти чанки `static/js/*.chunk.js`, к каждому дописать `.map`, развернуть `sourcesContent` по путям из `sources`.
3. Репозитории `gladly-team/tab`, `tab-web`, `tab-extensions`, `app-for-a-cause` открыты на GitHub.

Временные файлы лежат в scratchpad сессии и в проект не копировались.
