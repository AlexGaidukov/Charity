# Grass / Wynd Network

## Суть / модель
<!-- что делает, как зарабатывает, куда идут деньги/ресурсы -->
- Пользователю платят за неиспользуемый интернет-канал — поток денег идёт к пользователю.

## Платформы и онбординг

## Функционал

## Интерфейс (экран за экраном)
- **Главный экран (гость, Android 3.6.1)** — снято на эмуляторе:
  - Хедер: лого grass™, переключатель тёмной темы, аватар-маскот (зелёная капля).
  - Ярко-салатовая плашка «Sign up to save your progress» + SIGN UP / SIGN IN.
  - Плашка «Grow Your Earnings» + кнопка SHARE WITH FRIENDS (рефералка вынесена на главный).
  - Блок «🔒 Sign Up to Save your Points»: карточки **Epoch Network Earnings** (иконка 💎) и **Epoch Uptime Earnings** (иконка листа) + счётчик Uptime (дни/часы/мин). Поинты копятся даже у гостя, но «заблокированы» до регистрации.
  - Блок подключения: иконка Wi-Fi (красная = не подключено), кнопка CONNECT, статус «Waiting for you to sign in.» + технический код `awaiting_login`.
  - Таб-бар: дашборд (грид), подарок (rewards), кубик (вероятно wallet/устройства).
- **Sign Up (WebView)**: GOOGLE / email, «Have a referral code?», 2 чекбокса (T&C обязательный, маркетинг опциональный), CONTINUE. Continue неактивна, пока не пройдёт невидимая reCAPTCHA. Внизу 5 юр. документов (Privacy, General T&C, Wallet T&C, Rewards T&C, Cookie).

## Мотивация и геймификация

## Плюсы / минусы / наблюдения

## Сырые заметки

- Идея: тебе платят за интернет, который ты не используешь (неиспользуемый трафик/канал). Деньги все платят тебе.

---

## С сайта (ресёрч, 2026-11-22)
Источники: grass.io (бывш. getgrass.io), /download, /learn, /privacy-policy, /network-use-policy. wynd.network → wyndlabs.ai (только слоган «Internet-scale data for Business Intelligence»).

### Модель
- Пользователь делится неиспользуемым каналом → получает **Grass Points** → они конвертируются в **GRASS (токен, Solana) или USDC** в распределениях.
- Платят верифицированные бизнесы: через узлы пользователей идёт сбор публичных веб-данных. Главный покупатель — **AI-лаборатории** (данные для обучения; далее поиск / live web).
- Разрешённые сценарии: AI/ML-данные, мониторинг цен, SEO, верификация рекламы, индексирование, академ. исследования. Запрещено: хакинг, DDoS, фишинг, scalping и т.п. Каждый клиент проходит проверку.
- Юрлица: Grass Foundation, Grass OpCo Ltd (приложение), Grass RetailCo Ltd (железо).

### Продукты / платформы
- Desktop: Windows, macOS (Apple Silicon / Intel), Linux (Ubuntu).
- Android (Google Play / APK, Android 9+). iOS на странице загрузки нет.
- Расширение Chrome (на главной упоминается, на /download не перечислено).
- **GRASSHOPPER** — аппаратное устройство (стабильнее подключение).
- Веб-дашборд app.grass.io.
- Встроенный кошелёк (non-custodial, Solana, passkey).
- B2B: **Grass Contents API** (URL → чистый HTML/Markdown/текст для AI-агентов).

### Механика наград (с Epoch 11, окт 2025)
- **Uptime Points** — за время онлайн; за аптайм активных рефералов; за милстоуны/бонусы. Ставка зависит от **Network Quality Score** (качество IP, не скорость; VPN = 0%).
- **Network Points** — фиксированный пул **1 000 000 в день**, делится пропорционально реально использованному трафику. Нет трафика — нет Network Points. Влияют регион, стабильность, история.
- Эпохи; Stage 2 = Epochs 1–19 (14.10.2024–08.06.2026).
- Tiers и milestones в Rewards Dashboard; реферальная ссылка с кодом.
- Покупка устройства/установка не гарантирует Network Points.

### Онбординг
1. Скачать приложение / расширение.
2. Подтвердить согласие на sharing — подключение стартует сразу (пауза/выключение в любой момент).
3. Аккаунт по email или Google.
4. Кошелёк создаётся автоматически (passkey).
- KYC для пользователей не упоминается; санкционные регионы могут не получать токены.

### Дашборд
- Главная: статус подключения, аптайм, поинты, пауза/отключение.
- Rewards: tiers, milestones, рефералы, разбивка Uptime / Referral, история эпох, Network Points.
- Network Quality (оценка IP).
- Wallet: депозит (MoonPay: карта, Venmo, крипта), swap без SOL на газ (Jupiter), стейкинг GRASS, вывод.

### Приватность
- Собирают: email, username, адрес кошелька, IP, данные устройства/OS, crash-логи.
- Заявляют: не читают файлы, историю браузера, личные данные; персональные данные не продают. AppEsteem certified, член AMTSO.
- Важно: **IP пользователя виден сайтам**, куда идёт трафик.
- Подрядчики: Turnkey (ключи кошелька), MoonPay, Jupiter.

### Цифры
- 8,5 млн+ пользователей.
- Суммы выплат и объём трафика не раскрыты.

### Не изучено
Rewards T&C (grassfoundation.io), документация (gitbook), Wallet T&C, полные статьи про Stage 2, кошелёк, Network Quality.

## Android-билд (v3.6.1, APK с files.grass.io)
- Package `io.getgrass.www`, versionCode 3006001, target SDK 36. Подпись: O=Grass, Toronto.
- Запрашиваемые разрешения: INTERNET, ACCESS_NETWORK_STATE, ACCESS_LOCAL_NETWORK, FOREGROUND_SERVICE (+ REMOTE_MESSAGING), WAKE_LOCK, RECEIVE_BOOT_COMPLETED (автозапуск), REQUEST_IGNORE_BATTERY_OPTIMIZATIONS, POST_NOTIFICATIONS, SYSTEM_ALERT_WINDOW (поверх других окон), REQUEST_INSTALL_PACKAGES (самообновление APK в обход Play), AD_ID, Install Referrer (атрибуция рефералов/рекламы).
- Вывод: работает как постоянный фоновый сервис, стартует при загрузке, просит исключить из оптимизации батареи.

- Регистрация 2026-11-22 не прошла: OTP на email не приходит, Google OAuth → api.grass.io/auth/google отдаёт Cloudflare 504. Разбор онбординга по скриншотам: [01-grass-onboarding.md](01-grass-onboarding.md)
- Разбор APK (архитектура, прокси-протокол, трекинг, фичи из фронтенда): [01-grass-apk-analysis.md](01-grass-apk-analysis.md)
