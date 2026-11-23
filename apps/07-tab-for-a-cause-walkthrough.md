# Tab for a Cause: интерфейс вживую (экран за экраном)

Снято 2026-11-23 в Playwright (Chromium, десктоп 1440×900, регион BG). Аккаунт новый, зарегистрирован пользователем вручную через email: шаги verify-email и set-username он прошёл сам, их скриншотов нет. Расширение не ставили; открывали `tab.gladly.io/newtab/first-tab/`, как это делает расширение после установки.
Скриншоты: [`screenshots/tab-for-a-cause/`](../screenshots/tab-for-a-cause/). На `14-account.png` и `33-classic-account.png` виден email тестового аккаунта.
Код и архитектура: [07-tab-for-a-cause-decompile.md](07-tab-for-a-cause-decompile.md).

## Главное
1. **Новичок попадает в v4 («Tab for <cause>»), а не в Classic.** Hearts там нет вообще. Вместо них один счётчик «сколько собрало всё сообщество» и недельные лиги на «Impact Points». Classic (legacy с Hearts и выбором из 10 фондов) включается только вручную: Account → «Switch to Classic».
2. **Вкладки в v4 не дают Hearts.** После 5 вкладок в v4 и перехода в Classic баланс равен 1 ♥, а в Stats написано «5 tabs all time». Так и в коде бэкенда: `addVc` только при `!isV4`.
3. **Первый экран после регистрации — реклама собственного продукта.** Полноэкранное промо Shop for a Cause («Your cart. More heart.», UTM `bf26-shop-fullpage`) открывается поверх тура для новичка: две модалки одна на другой.
4. **Реклама включается на второй-третьей вкладке**, 3-дневная пауза здесь не действует. Она есть только на странице входа v5 (`tabLoginFirstVisit`). На первой вкладке AdThrive не загружен, на второй уже грузятся Prebid и GPT, на третьей заполнены все 3 слота. Креативы, которые мы увидели: **букмекер Winbet** (с предупреждением о зависимости от азартных игр), **«GPS Locator App for Couples»** (слежка за партнёром), NetEase Games. Для благотворительного продукта это заметный риск для бренда.
5. **Продукт стал хабом для перекрёстных продаж**: Shop for a Cause (промо-модалка, Shop Earnings в настройках), Search for a Cause (первый пункт в выборе поисковика, иконка с бейджем «Inactive», промо «up to 4x more»), Games for a Cause (каталог Google GameSnacks), Pause for a Cause (новый продукт, упомянут в лидерборде).

## Путь нового пользователя
| # | Экран | Что видно | Скриншот |
|---|---|---|---|
| 1 | `/v5/login?app=tab` | Логотип, 4 кнопки: Google · **Facebook** (кнопка осталась, хотя в коде вход через FB объявлен прекращённым) · email · Apple. Больше ничего: ни слова о том, зачем входить. В консоли: «Ads will show in approximately 67 hours», «Meta Pixel — Invalid PixelID: an empty string» | `01-login.png` |
| 2 | verify-email → повторный вход → set-username | прошёл пользователь, скриншотов нет | — |
| 3 | `/v5/select-cause` | «Choose a cause to support», 14 карточек. У **каждой** приписка «Still in beta: some features like widgets are missing, but you can always switch back». Global Health выбрана заранее | `02-select-cause*.png` |
| 4 | `/v5/referral-capture` | «Processing referral data…», затем редирект на `/newtab/` | `03-referral-capture.png` |
| 5 | `/newtab/` — промо | Полноэкранный iframe `/v5/notifications?slot=modal-center`: «Your cart. More heart. Before the holiday shopping starts, get Shop for a Cause…» | `04-newtab-first.png` |
| 6 | Тур v4, шаг 1 | «Your tabs are doing great things. Now, every tab you open helps train and support community healthcare workers to provide at-home visits.» | `05-tour-step1.png` |
| 7 | Тур v4, шаг 2 | «It doesn't cost you a thing. Ads on the new tab page raise money that we give to nonprofits. Most ads aren't good—but these ones are :)» | `06-tour-step2.png` |
| 8 | Вкладка v4 | Фото дня, логотип, чип «Supporting: Global Health», поиск «Search Google». В шапке: пригласить · инфо · видео · игры · лидерборд · **$2,107,666** (растёт на глазах) · настройки | `07-tour-step3.png` |

Тур занимает всего 2 шага, про сам интерфейс в нём ничего нет.

## Вкладка v4: элементы
| Элемент | Что делает | Скриншот |
|---|---|---|
| Пригласить | Модалка «Get a friend on board»: вкладка Email (кому, имя, сообщение) и Social media (ссылка `tab.gladly.io/global-health/?u=<username>`). Награда не упоминается | `08-invite-popover.png`, `09-invite-social.png` |
| Лидерборд | iframe v5: «weekly leaderboard», 5 лиг (звезда → … → бриллиант), выше зелёной линии — повышение, ниже красной — вылет. **Impact Points**: 40 за видео, 40 за ролик Pause for a Cause, за вкладки, покупки, «20x more» за поиск, за минуты в играх. У новичка таблица пустая | `10-leaderboard.png` |
| Видео | iframe `/v5/iframe/opt-in-video`: «Watch a video, raise money for charity! No videos available right now… the button will become green» | `11-video-ad.png` |
| Игры | `/v5/games/global-health` — встроенный **Google GameSnacks** (около 100 HTML5-игр по жанрам) под красной плашкой «Games for a Cause: Make every game count – for Global Health!» | `12-games.png` |
| Счётчик $ | Подсказка «We've raised this together — This is the total our community has raised for nonprofits all over the world». Личного вклада не показывает | `18-money-raised-popover.png` |
| Чип каузы / ⓘ | → «About the Cause»: таблица исходов («Provide 1 home visit from a community health worker», «prenatal care for 1 woman», «1 infant care package»), фонд Partners In Health. Сколько стоит один исход, не сказано | `13-about-cause.png` |
| Выбор поисковика | **Search for a Cause «Earn More Impact ❤️»** первым пунктом, затем Google (по умолчанию), Ecosia, DuckDuckGo, Bing, Yahoo. «Only updates search preferences for the new tab page» | `20-search-engine-select.png` |
| Иконка поиска с бейджем | Появляется позже. «Search for a Cause — Inactive. Searching raises up to 4x more… 0 Searches Today» + GET IT NOW | `35-sfac-search-promo.png` |
| Реклама | Липкий футер 728×90 и 300×250 справа, который сдвигает содержимое вверх. Ссылка «Update Privacy Preferences» (CMP Raptive) | `18-…`, `19-cause-chip-with-ads.png` |
| CMP | На второй вкладке: «Manage Your Privacy… our **141 partners**», кнопки Reject All / Manage / Accept All. Мы нажали Reject All | `17-newtab-second-open.png` |

## Настройки v4 (собраны из двух фронтендов)
- **Account** (`/newtab/account`, Next.js): Switch Cause (14 вариантов «Tab for ___»), Shortcuts (вкл/выкл), username, email, «Data privacy choices», «Leave Tab for Global Health → **Switch to Classic**» с предупреждением. — `14-account.png`
- **Background** (`/v5/account/background`, Laravel): фото дня · выбрать фото · своё фото · сплошной цвет. — `15-background.png`
- **Shop Earnings** (`/v5/account/earnings`): «Raise Money While You Shop… 10,000+ Stores · Free to Use · **100% to Charity**», кнопка «Get Started with Shop for a Cause». — `16-shop-earnings.png`
- **About the Cause**, Help, Our Financials, Feedback (Google Form).

## Classic (legacy, после «Switch to Classic»)
| Экран | Что видно | Скриншот |
|---|---|---|
| Тур, шаг 1 | «Your tabs are changing the world! …(The money comes from showing ads in the corner of the page.)» Одновременно справа промо «Make a bigger impact — Search for a Cause… up to 4x more than tabs alone» | `21-classic-newtab.png` |
| Тур, шаги 2–4 | Hearts («You'll earn a Heart with every tab… Donate your Hearts to your favorite charity to tell us where to give money»), настройки, виджеты (подсказка **уезжает за левый край экрана**) | `22…24-classic-tour-*.png` |
| Тур, шаг 5 | «We're thrilled to have you!», ссылка `tab.gladly.io/?u=<username>`, «you'll get 350 Hearts for every person who joins!» | `25-classic-tour-5.png` |
| Вкладка | Только фон и шапка: $ · видео · лидерборд · игры · **1 ♥** · меню. Поиска нет, виджетов по умолчанию не видно | `26-classic-dashboard.png` |
| Меню Hearts | «Level 1 — 4 ♥ until next level», «0 ♥ donated» + DONATE HEARTS, «0 friends recruited» + INVITE A FRIEND, легенда: Open a tab 1 ♥ · Recruit a friend 350 ♥ (+100 ♥ за видео в легенде нет) | `27-classic-hearts-dropdown.png` |
| Donate Hearts | «When you donate Hearts, you're telling us to give more of the money we raise to that charity.» 10 фондов (Action Against Hunger, Save the Children, GiveDirectly, Water.org, Educate!, Foundation to Decrease Worldsuck, Room to Read, Human Rights Watch, Conservation International, The Bail Project) с кнопкой «DONATE 1 HEART» и 14 карточек «TRY TAB FOR ___ (Beta)», которые переводят обратно в v4 | `28-classic-donate-hearts.png` |
| Your Stats | «0 days as a Tabber · 5 tabs all time · 5 max tabs in one day · level 1 · 0 recruited · 0 Hearts donated» | `29-classic-stats.png` |
| Widgets / Background / Invite / Account | Переключатели виджетов (закладки, часы, заметки, поиск, todo), выбор фона, реферальная ссылка, аккаунт | `30…33-classic-*.png` |

После обхода аккаунт возвращён в v4 через «Try Tab for Global Health» (`34-back-to-v4.png`).

## Наблюдения для сравнения
- **Обратная связь о вкладе почти нулевая.** В v4 нет ни личного счётчика, ни Hearts: есть только общий счётчик на $2,1 млн и пустой лидерборд. Ощущение «я помог» держится на тексте тура и фотографиях.
- **Две модели мотивации конкурируют внутри одного продукта**: Hearts и голосование за фонд (Classic) против одной каузы и лиг на Impact Points (v4). Пользователь видит обе, связь между ними не объяснена, а прогресс между версиями не переносится.
- **Регистрация до первой ценности:** 4–5 экранов (вход, письмо, повторный вход, username, кауза), а затем сразу промо другого продукта.
- **Подбор рекламы противоречит миссии**: ставки и слежка за партнёром на «благотворительной» вкладке. Фильтровать категории может Raptive, но для региона BG этого, судя по всему, не сделано.
- **Монетизация вне вкладки сильнее, чем на ней**: поиск «до 4x», шопинг «100% to charity», игры, видео. Вкладка работает как точка входа в экосистему Gladly.
- Мелкие баги: кнопка Facebook на экране входа, пустой ID Meta Pixel, наложение модалок, подсказка тура за краем экрана, приписка «Still in beta» у всех 14 кауз.
