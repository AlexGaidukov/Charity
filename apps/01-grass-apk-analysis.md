# Grass: разбор APK (Android 3.6.1)

Файл: `Grass-v3.6.1.apk` (files.grass.io), SHA-256 `dfee7b1c…5db05`, package `io.getgrass.www`.
Метод: распаковка APK, манифест (aapt2), Java/Kotlin-байткод (dexdump), строки нативных библиотек, извлечение вшитого веб-фронтенда из `libapp_lib.so` (таблица ассетов Tauri, распаковка brotli). Без запуска чужого кода и без сторонних декомпиляторов.

---

## 1. Архитектура

| Слой | Что это | Где |
|---|---|---|
| Оболочка | **Tauri 2** (Rust + системный WebView). Тот же код, что у desktop-версии (в конфиге есть сборки под Windows, macOS, Linux, iOS). | `libapp_lib.so` (56 МБ) |
| Интерфейс | **React + Chakra UI + react-router 7, Vite**, бандл 4 МБ вшит в нативную библиотеку. Весь UI — веб, нативные только разрешения и уведомления. | `assets/index-*.js` |
| Прокси-узел | Отдельная Rust-библиотека **`librust_wynd_proxy.so`**. Имя Wynd сохранилось в коде. Построена на фреймворке прокси **rama** и внутреннем репозитории `proxy-stack` (модули `edge`, `tunnels/h2`, `common`). | 12 МБ |
| Java-обёртка | `io.getgrass.plugin.ForegroundService` (сервис узла), `io.grass.sdk.*` (**Grass SDK** — встраиваемый модуль). | `classes.dex` |

Поддержка Android TV: в манифесте есть `leanback` и `LEANBACK_LAUNCHER`, приложение ставится и на телевизоры/приставки.

## 2. Как работает узел (главное)

```
Телефон ──(1) POST director.grass.io/devices/checkin──► Director
         ◄──── адрес edge-сервера, статус устройства ────
Телефон ══(2) исходящий HTTP/2-туннель (TLS)═════════► Edge-сервер Grass
         ◄══ (3) сервер открывает потоки ВНУТРИ туннеля ══  «сходи на URL X»
Телефон ──(4) HTTP/1.1/2 запрос с IP пользователя ───► целевой сайт
         ──(5) ответ обратно по туннелю ─────────────► клиент Grass (AI-компания)
```

- **Reverse tunnel**: телефон сам подключается к серверу (`tunnels/src/h2/reversed_connector.rs`), поэтому входящих портов и проброса на роутере не нужно. Сервер шлёт запросы обратно через туннель, узел выполняет их как **forward-proxy** (`rama-net/proxy/forward.rs`, поддержка `CONNECT`) и возвращает ответ.
- **Слой `remove_headers`** удаляет служебные заголовки, чтобы целевой сайт видел обычный запрос с домашнего IP.
- **Идентичность устройства**: при первом запуске генерируется ключ **Ed25519** (`grass_device.key`, `grass_device.id`, «seed», «seed_dek» — ключ шифрования сида). Устройство регистрируется (`/devices/register`) и подписывает check-in. `resetDeviceIdentity` стирает ключ и регистрирует устройство заново.
- **Статусы от Director**: `OPEN`, `CONNECTING`, `CLOSED`, `FAILED`, `REVOKED` (устройство забанено → «wiping identity and re-registering»), `DEVICE_UNKNOWN` (повтор check-in), `UPGRADE_REQUIRED` (узел останавливается до обновления), `device_quota_exceeded` (лимит устройств на аккаунт), а также ошибка «часы устройства слишком расходятся».
- **JNI-функции узла**: `initialize`, `grassStart`, `startNode`, `startH2Extension` / `stopH2Extension`, `resetDeviceIdentity`.
- В коде **не нашлось** собственного фильтра адресов назначения (запрет локальной сети, 25-го порта и т.п.). Видимо, решать, куда ходить, доверено серверу Grass. Это вывод по строкам, не по коду, поэтому не окончательный.

### Сервис и экономия ресурсов
- Foreground service типа `remoteMessaging` с постоянным уведомлением («Foreground Service Channel»). WakeLock `grass:wakeLock` — без него «sharing may pause when the device dozes».
- Автостарт на `BOOT_COMPLETED`, `LOCKED_BOOT_COMPLETED` (до разблокировки), `QUICKBOOT_POWERON`.
- **Мобильные данные**: `isCellularAllowed`, `isCellularUsageLimited`, `cellularAllowedLimit`, `cellularUsage`. Есть лимит трафика: при превышении узел останавливается (`CELLULAR_LIMIT_EXCEEDED`). Метрики `metered` / `unmetered` учитываются.
- «the foreground service hit its daily time limit and was stopped» — реакция на суточный лимит Android 15+ для foreground-сервисов.
- Периодическая проверка «Checking if node should be running»: учётные данные, сеть, лимит сотовой связи.

## 3. Grass SDK и партнёры
- Пакет `io.grass.sdk.android` / `io.grass.sdk.tauri`, эндпоинт **`/partner/login`** с `appId`, `apiKey`, `projectId`; ошибка `partner_refused` — «The partner app could not sign in to the Grass Network».
- Значит, у Grass есть **SDK для встраивания узла в чужие приложения** (B2B2C-канал: партнёрское приложение монетизирует трафик своих пользователей через Grass). Само приложение Grass использует тот же SDK.

## 4. Самообновление в обход Google Play
- Rust проверяет `files.grass.io/.../mobile-updater-latest.json`, качает `www-getgrass-io-update.apk` через `DownloadManager` и запускает установку (`REQUEST_INSTALL_PACKAGES`).
- Тосты: «An update is available — The app will automatically download the update». Без последней версии «not eligible for Network Points», при `UPGRADE_REQUIRED` узел выключается.

## 5. Трекинг и аналитика
| SDK | Что уходит |
|---|---|
| **AppsFlyer** (атрибуция установок) | `COMPLETE_REGISTRATION` (Google / email), `LOGIN` (Google / email / password), `FIRST_CONNECT` (тип устройства), `REACHED_100H_UPTIME`, `REACHED_100H_NETWORK_POINTS`, `REACHED_500H_NETWORK_POINTS`; customer user id = userId Grass |
| **Facebook SDK** | `setUserData(email)`; события `COMPLETED_REGISTRATION`, `SHARE_REFERRAL_LINK`, `REACHED_5000_UPTIME` с параметром `em` = **email пользователя** (хешируется ли он в параметрах событий, не проверено) |
| **Firebase Crashlytics** | краши, userId |
| Прочее | Google Advertising ID, Install Referrer, видимость пакетов Facebook / Instagram / FB Lite (`<queries>`), `android_id`, brand / manufacturer / model |

Вывод: Grass закупает пользователей платной рекламой в Meta и через AppsFlyer, а события «100 ч аптайма» / «500 ч» — их целевые конверсии для оптимизации рекламы.

## 6. Функционал по фронтенду (роуты и API)

**Экраны** (`/dashboard/...`): главная · `networks` · `statistics` · `rewards`, `rewards/epochs` · `allocation` · `airdrop` · `referral-program` (+ `leaderboard`, `rewards`) · `wallet` (+ `transaction-history`, FAQ) · `store` (+ item; ссылка на shop.grass.io) · `download` · `profile/settings` (app, security, change-email / username, email-preferences, advanced → **pause-sharing**).

**API api.grass.io** (основное): auth (`login`, `loginPasskey`, `register`, `registerGuestProcedure`, `sendOtp` / `verifyOtp`, `verifyReCaptcha`, `refreshToken`) · заработок (`epochEarnings`, `dailyEarnings`, `ipEarnings`, `epochStages`, `ranks`, `claimReward`) · устройства (`devices`, `activeDevices`, `activeIps`, `ipCheck`, `updateDeviceName`, `attachGrasshopperDevice`) · рефералы (`userReferrals`) · airdrop (`airdropStats`, `airdropOverallStats`, `airdropFees`) · кошелёк (`getWalletInfo`, `getUserTokens`, `getSwapQuote`, `sendTransaction`, `getStakingPools`, `getUserStaking`, `listNfts`, `setWhitelist`, MoonPay buy / sell) · `pauseConnection`, `updateTourStatus`, `maintenance`, `deleteUser`.
Кошелёк построен на **Turnkey** (`/public/v1/...`): ключи в защищённом анклаве, вход по passkey или OTP.

**Механики из текстов UI:**
- **Тиры** (картинки бейджей): Iron → Bronze → Silver → Gold → Platinum → Emerald → Diamond → Titan → Vanguard → Conqueror → Grass Max. «Rank Up — Unlock bonus Uptime Points each time you reach a new tier».
- **Рефералка многоуровневая**: «Earn commissions on your referral tree, **up to 3 levels deep**». Реферал «квалифицирован» после **100 ч аптайма** (Pending / Qualified Referrals). Есть лидерборд.
- **Android-бонус**: «Stay Active on Android — Earn **up to 3x** more with constant uptime» (множитель Device Type 3.00X на главном экране).
- **Daily earnings**: оценка с 00:00 UTC, финализация до 12 часов; разбивка по network activity, uptime, bonuses, referrals.
- **Стейкинг GRASS** в пулы «Router operators» с комиссией и APY; claim от 1 GRASS; минимальная сумма анстейка.
- **Dashboard Tour**: 9 шагов (эпоха, сегодня, статус соединения, разбивка по дням, устройства, тир, источники, рефералы, история эпох).
- Иконка `data-labeling` подгружается, но экрана в роутинге не нашлось — возможно, будущая функция (разметка данных за поинты).
- Капча на вебе — reCAPTCHA (`verifyReCaptcha`), в бандле есть и hCaptcha.

## 7. Что это значит для нашего разбора
- Grass — по сути **резидентная прокси-сеть**, упакованная в геймифицированное «приложение заработка»: тиры, эпохи, 3-уровневая рефералка, токен, стейкинг.
- **Мобильный трафик ценится выше** (×3) — отсюда включённая по умолчанию сотовая связь и упор на Android, включая TV-приставки.
- Удержание построено на аптайме: автостарт, foreground-сервис, отключение экономии батареи, конверсии «100 ч» / «500 ч».
- Есть SDK для встраивания в чужие приложения — второй канал роста помимо собственного приложения.

## Артефакты
Временные файлы (распакованный APK, извлечённый фронтенд, дампы) удалены после анализа. Чтобы повторить: распаковать APK, `aapt2 dump xmltree`, `dexdump -d classes.dex`, `strings` по `.so`. Фронтенд Tauri лежит в `.data.rel.ro` `libapp_lib.so` парами (ptr, len) «имя → brotli-блоб» и распаковывается `brotli -d`.
