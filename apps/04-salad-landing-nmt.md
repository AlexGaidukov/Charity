# Salad (salad.com): разбор лендинга по Next Move Theory

Дата снятия: 2026-11-22. Главная https://salad.com/, лендинг для пользователей https://salad.com/download/ и подстраницы (полный список в конце).
Статусы утверждений: **[факт]** — дословно или напрямую видно на сайте; **[вывод]** — выведено из фактов и канона; **[гипотеза]** — моё предположение, нужна проверка.
Методология: Next Move Theory / Advanced JTBD (канон в `Next-Move-Theory-Canon/`). Термины методологии даны в скобках при первом упоминании.

---

## Резюме на один экран

1. **Сайт Salad продаёт облако, а не заработок.** На главной salad.com весь первый экран, меню, кейсы и FAQ сделаны для компаний, которые покупают дешёвые GPU. Тот, кто хочет зарабатывать, видит одну зелёную кнопку в шапке «Chefs: earn with your PC» и один вопрос в FAQ. Настоящий лендинг для пользователей вынесен на /download/. [факт]
2. **Лендинг для пользователей (/download/) — самый честный про деньги из всех, что мы разбирали.** На нём есть реальные заработки по каждой видеокарте за прошлую неделю (диапазон «у большинства машин»), калькулятор «заработок минус электричество» по стране, прямой ответ «Is this real money?» и список требований к ПК до скачивания. Посетитель может прикинуть свою сумму до установки. [факт + вывод]
3. **Но крупная цифра — это цифра лучшего 1%.** Виджет по умолчанию открывается на RTX 4090 (вторая по доходности карта) и крупно показывает «$0.476 per hour, top chefs». Типичный диапазон «$0.230 – $0.286 /hr» написан мельче. У большинства посетителей карта слабее: например, у RTX 3060 типичный диапазон «$0.023 – $0.038» в час. Получается, ожидание завышается теми же данными, которые задумывались как честные. [факт + вывод]
4. **Деньги «грязные» в двух местах, и лендинг их не показывает.** (а) Майнинг криптовалюты включён по умолчанию: это сказано одной строкой в блоке безопасности. (б) Вывод стоит дороже номинала: в магазине PayPal на $5 стоит $5.99 баланса, Visa на $100 — $115. На лендинге об этой разнице ни слова. [факт]
5. **Лучшие части — контроль и «запечатанная коробка».** «Real work, in a sealed box»: задачи идут в изолированной Linux-VM, не видят файлов Windows, пауза мгновенная. Это прямой ответ на главный страх «что чужое делает на моём ПК». [факт + вывод]
6. **Для нашего charity-продукта:** у Salad пожертвование — мелкая опция в магазине («St Jude… $0.10 Donation»), на лендинге одно слово «charity». Им честные цифры дохода нужны, чтобы продавать, а нам нужны честные цифры пользы (сколько добра даёт час работы), и подавать их стоит по типичному пользователю, а не по лучшему. [факт + вывод]

---

## 0. Что было на сайте (снятие 2026-11-22)

### 0.1 Главная https://salad.com/ (B2B, для покупателей GPU)

| # | Блок | Дословный текст |
|---|---|---|
| — | `<title>` | «Salad — Orchestration for distributed infrastructure and the world's idle GPUs» |
| — | Шапка | Products · Use Cases · Pricing · Developers · Company · «Talk to sales» · **«Chefs: earn with your PC»** (зелёная кнопка → /download/) · «Customer sign in». Над hero плашка «Salad Dedicated is coming: RTX PRO 6000 Blackwell, bare metal and VMs on contract.» |
| 1 | Hero | «The orchestration cloud» / H1 **«Salad orchestrates the world's idle GPUs.»** / «One orchestration layer for containers, tokens, and GPUs, running across 16,000+ daily active GPUs in 190+ countries, or privately inside your own organization. Up to 90% less than hyperscaler pricing.» CTA «Explore the platform», «Deploy on SaladCloud». «No contracts, no minimums, per-second billing…» |
| 2 | Бенчмарки | «Every modality, tuned for the network.» «Published benchmarks, not promises.» (напр. «5,243 Flux.1-Schnell images per dollar», «95.1% accuracy on CommonVoice… from $0.16 per audio hour») |
| 3 | Кейсы | «Teams ship on Salad.» Civitai, Blend, Klyne.ai |
| 4 | Блог | «How to build on Salad.» |
| 5 | FAQ «Straight answers.» | 6 вопросов для покупателей; один про пользователей: **«Why do people share their GPUs with Salad?» — «They earn. Salad Chefs run our desktop app when their PC is idle and redeem Salad Balance for PayPal, games, gift cards, and more. Since 2018, more than 450,000 GPUs have contributed compute to the network. Learn about becoming a Chef.»** Ещё один про безопасность — с точки зрения покупателя: «How does security work on a network of other people's computers?» |
| 6 | Финальный CTA | «Explore Salad today.» «Deploy on SaladCloud» · «Talk to sales» · «Chefs: download Salad» |
| — | Футер | отдельная колонка «Chefs»: Download Salad, Store, What's New, Help Portal, Chef app status, Discord. «SOC 2 Type I» |

Скриншот первого экрана: `.playwright-mcp/salad-home-hero.png`.

### 0.2 Лендинг для пользователей https://salad.com/download/ (блоки по порядку)

| # | Блок | Дословный текст |
|---|---|---|
| — | `<title>` / meta | «Download Salad — Earn rewards from your idle PC» / «Salad turns your idle PC into rewards. Contribute GPU compute, CPU compute, or bandwidth and redeem for PayPal, crypto, prepaid cards, gift cards, and more.» |
| — | Шапка (отдельная, «salad CHEFS») | Download · Earning rates · Store · What's New · Help · Discord · SaladCloud · Log in · «Download Salad» |
| 1 | Hero | «Salad for Chefs» / H1 **«The easiest way to earn from your PC.»** / «Your PC has compute and bandwidth that often sit unused. Salad connects eligible capacity to real customer workloads while you're away and rewards you for contributing it. Redeem your balance for PayPal cash, RENDER and other crypto rewards, prepaid cards, gift cards, games, and more.» CTA **«Download for NVIDIA»** / **«Download for AMD»** (прямые ссылки на .exe 1.9.29 на GitHub). Для не-Windows: «Salad runs on Windows PCs. Send yourself the download link, then open it on your computer.» «Send yourself the link» / «Or email it to yourself». Справа видео «Welcome to Salad» (YouTube) |
| 2 | Требования | «What you'll need» — «A Windows 10 or 11 PC, 64-bit. Salad doesn't run on Mac, Linux, or Chromebook.» / «For the best earnings: an NVIDIA RTX 3060 or newer, a 4-core CPU, and 12 GB of RAM. Other NVIDIA and AMD GPUs may still qualify.» |
| 3 | Цифры | «190+ countries of Chefs» · «450,000+ GPUs have earned on Salad» · **«$7M+ paid out to Chefs»** · «45,000+ Chefs on Discord» |
| 4 | How it works | H2 «Leave the keyboard. Start chopping.» — «Install Salad» («…You control when Salad runs and can pause it anytime.») / «Share when you're away» («Choose when Salad runs: manually, or automatically when your PC is idle…») / «Earn Salad Balance» («Your PC may contribute GPU compute, CPU compute, or bandwidth, depending on your hardware, settings, location, and current demand.») / «Redeem» («…PayPal, RENDER and other crypto rewards, prepaid cards, Amazon and other gift cards, games, subscriptions, and charity donations.») |
| 5 | Виджет заработка | «What your GPU earns · Nov 15–21, 2026». По умолчанию **RTX 4090**: крупно **«$0.476 per hour, top chefs»** («What the top 1% of machines earned per hour chopping, including hours with no job»); мельче «Average $0.262 /hr», «Most machines earn $0.230 – $0.286 /hr», «Has a job running 97% of the time». «Based on machines that averaged four hours a day or more… Includes container jobs, bandwidth sharing and mining.» Ссылка «See every GPU class, and how we measure» |
| 6 | Калькулятор | H2 «GPU Electricity Profit Calculator»: «01 Your PC» (ватты в простое / под нагрузкой, «Use our estimate instead», «Measure your own →»), «02 Where you live» (глобус, цена кВт·ч, по умолчанию $0.134 — «EIA average residential price, June 2026. Your bill may differ.»), 8 часов в день. Результат по умолчанию: **«Your Earnings: $1.84 to $2.29 · Electricity Cost: $0.51 · Estimated Profit: $1.34 to $1.79»** (в день) + строка «Top 1% of RTX 4090 Chefs earned $0.476 per hour chopping: about $3.30 a day after electricity at your rate.» Аккордеоны: «What these earnings include», «How earnings are calculated», **«Is this real money?»** — «…your PC is not creating or accruing actual currency. Instead, you earn Salad Balance, which lets you redeem rewards from our curated Storefront…», «How to measure your electricity usage» (розетка-ваттметр «$15 to $35») |
| 7 | Rewards | H2 «Choose how you redeem.» PayPal / RENDER & crypto / Prepaid cards / Gift cards & more («…games, subscriptions, and charity options»). CTA «See the Storefront» |
| 8 | Отзывы | H2 «From the Kitchen.» 3 цитаты с именем и профессией (Kyle LePrevost · Cybersecurity architect; Netanel Takuni · Logistics specialist; Brandon Coin · BC-PC.com) — про простоту, паузу, «stopped letting my computer sit idle, wasting electricity», переход с майнинга |
| 9 | Безопасность | H2 **«Real work, in a sealed box.»** «Customer compute workloads run inside an isolated virtual machine, separate from Windows and your personal files. Salad shows when a workload is active, but does not reveal the customer, workload type, or workload contents.» Пункты: «Compute workloads run in an isolated Linux VM…», «Customer workloads cannot browse your Windows files», «You choose when Salad runs and can pause instantly», **«Crypto mining is presented during signup, enabled by default, and can be disabled in settings»** |
| 10 | Совместимость | H2 «What earns best?» OS / GPU («NVIDIA RTX 3060 or later currently has the best access to high-earning GPU workloads») / CPU / RAM / Connection («Stable broadband; your PC awake and online»). «Eligibility and earnings vary by workload, demand, and region.» |
| 11 | Сообщество | H2 «Nearly 200 countries, one Kitchen.» «Ask 45,000+ real Chefs why they use Salad…» Discord, r/SaladChefs, Community blog |
| 12 | Финальный CTA | H2 «Ready to start chopping?» «Download Salad» · «Send yourself the link» · «What's new in the app» |
| — | Футер | слоган «Share your idle PC. Earn real rewards. Power the world's distributed cloud.»; колонки Chefs / Support / Company («SaladCloud for businesses») / Legal («Chef terms») |

Скриншот первого экрана: `.playwright-mcp/salad-download-hero.png`. Отдельной FAQ-страницы нет: /faq перенаправляет на /download/, /rewards — 404. [факт]

### 0.3 /earning-rates/ (вторая страница пользовательского лендинга)

- H1 «What your GPU really earns on Salad.» «Measured from machines that ran a real week on Salad, including the hours nobody had work for them.» [факт]
- Таблица по 50+ классам GPU за 15–21 ноября 2026, например [факт]:

| GPU | Average /hr | Most machines | Top chefs |
|---|---|---|---|
| RTX 5090 | $0.355 | $0.308 – $0.387 | $0.586 |
| RTX 4090 | $0.262 | $0.230 – $0.286 | $0.476 |
| RTX 4070 | $0.065 | $0.056 – $0.070 | $0.159 |
| RTX 3060 | $0.032 | $0.023 – $0.038 | $0.072 |
| RTX 2060 | $0.029 | $0.023 – $0.031 | $0.072 |

- Блок «Honest numbers, on purpose.»: «Nothing here is a projection.» / «Every hour counts» / «Machines that actually ran» (≥4 ч/день) / «All your earnings count» («Container jobs, bandwidth sharing and mining are all in»). Объяснение, почему среднее выше типичного: «A few machines earn a lot, which pulls the average above what a typical machine sees.» Для новичка: «Most machines… If you are new, expect to start here.» [факт]
- Финал: «Your GPU is already good enough. Put it to work.» «Install Salad, pick what to earn, and let it chop while you sleep.» [факт]

### 0.4 Что лендинг отдал на второй-третий клик

- **/store** (магазин, открыт без логина) [факт]: «PayPal Balance – $5.00 (USD) $5.99», «– $20.00 $22.50», «– $100.00 $110.50», «– $1,000.00 $1090.00»; «Prepaid VISA - $100 $115.00»; «Venmo - $10 Balance $11.50». Блок «Donate Your Balance / See All Charities»: «POW! Protect Our Winters - $0.50 Donation», «St Jude Children's Research Hospital - $0.10 Donation», «K9s for Warriors - $0.10», «Extralife $0.10 Donation».
- **/terms/chefs/** [факт]: «Reward Points have no cash value»; баллы появляются в балансе «within five (5) business days»; при 12 месяцах без начислений баллы «may expire»; возраст 18+; санкционные страны исключены; «You are responsible for the cost of the electricity and internet service…»; налоги на пользователе; отказ от ответственности за повреждение оборудования.

---

## 1. Для кого лендинг и какие работы он предполагает

Уровни работ (по канону, `job-structure.md §9`, `glossary.md`): **Big Job** — результат уровнем выше, там живёт мотивация; **Core Job** — самая крупная работа, которую продукт выполняет целиком; **Small Jobs** — работы того же уровня, которые продукт не делает; **Micro Jobs** — шаги под Core Job.

### 1.1 Сегменты и работы (гипотеза по тексту лендинга)

**S1 «Геймер / владелец мощного ПК, который хочет, чтобы железо окупалось»** — на него написан лендинг [вывод: язык «chopping», Discord, отзывы, магазин с Steam/Valorant/Nitro].
- **Big Job** [гипотеза]: «хочу, чтобы мой дорогой ПК отбивал часть своей стоимости / оплачивал мои игры и подписки, не мешая мне играть».
- **Core Job, которую выполняет Salad** [вывод]: «хочу монетизировать простой видеокарты и процессора, пока меня нет за компьютером».
- **Точка A** [гипотеза]: ПК за $1000+ большую часть суток простаивает; ощущение «зря жрёт электричество» (отзыв: «stopped letting my computer sit idle, wasting electricity» [факт]); подписки и игры — регулярная трата.
- **Точка B** [гипотеза]: ПК работает ночью/днём в отсутствие, баланс растёт, раз в N недель — Nitro/Steam/PayPal; игре не мешает.
- **Критерии успеха** [гипотеза; ✔ — отражено на лендинге]:
  - ✔ сумма в час/день по моей карте — есть (виджет, таблица) [факт];
  - ✔ прибыль после электричества — есть (калькулятор) [факт];
  - ✔ пауза в любой момент, не мешает играм — есть («pause it anytime», «pause instantly») [факт];
  - ✔ безопасность личных файлов — есть («sealed box») [факт];
  - ✘ **сколько времени до первой награды** (когда накопится на $5 PayPal или Nitro за $2.99) — не найдено на лендинге;
  - ✘ **реальный курс вывода** (баланс → деньги) — не найдено на лендинге, только в магазине;
  - ✘ **износ железа и шум/температура** — не найдено на лендинге.
- **Small Jobs** [вывод]: решить, на что потратить баланс (магазин — есть); проверить, что не скам (Discord, Reddit — есть); оплатить электричество (калькулятор — есть); заплатить налоги (только в terms).
- **Micro Jobs** [факт]: скачать .exe под свою карту → установить → создать аккаунт Chef → выбрать, чем делиться (и решить по поводу майнинга) → поставить режим «при простое».

**S2 «Бывший майнер»** [гипотеза; есть отзыв «a significant shift from traditional crypto mining» [факт]]: Big Job «вернуть доход с фермы/карты после конца GPU-майнинга»; Core Job для него **знаком**; критерии — $/час, $/кВт·ч, крипто-вывод (RENDER). Таблица и калькулятор по сути написаны на его языке.

**S3 «Обычный человек с офисным/игровым ноутбуком, хочет пассивный доход»** [гипотеза]: приходит по объявлениям «earn from your PC». Для него Core Job **незнаком**, а реальная сумма по слабой карте — центы в час.

**S4 «Хочу помочь, а не заработать»** [гипотеза]: на лендинге обслуживается одним словом «charity donations» в списке наград. [факт]

**B2B-сторона (SaladCloud)** [факт + вывод]: покупатели GPU для инференса. Big Job «снизить стоимость AI-инференса без потери масштаба», критерии на главной даны цифрами («Up to 90% less than hyperscaler pricing», «per dollar»). Эта сторона на главной выполнена по канону заметно лучше, чем пользовательская: критерии, кейсы с названием компании, раздел «What workloads are not a fit?» (честное управление ожиданиями).

### 1.2 Кого лендинг обслуживает на самом деле и кого должен

- **Главная salad.com обслуживает только B2B** [факт]. Для пользователя она — точка входа с одним выходом (кнопка в шапке). Это осознанное разделение: у пользователей своя шапка, свой бренд «salad CHEFS», свой путь. [вывод] Но тот, кто пришёл по запросу «salad earn», сначала видит «orchestrates the world's idle GPUs» и «Up to 90% less than hyperscaler pricing». Это может читаться двояко: с одной стороны, видно, что есть реальные платящие клиенты (подтверждение, что деньги откуда-то берутся), с другой — «ваше железо продают за 10% от цены облака». [гипотеза]
- **/download/ обслуживает S1 и S2** [вывод]: требования к железу, $/час, ватты, крипто — всё это критерии людей, которые разбираются в «железе». Для них Core Job знаком или наполовину знаком, это изменение поведения первого класса (`behaviour-change.md §10`): вести коммуникацию через Core Job и его критерии уместно — так лендинг и делает.
- **S3 обслуживается плохо** [вывод]: калькулятор и таблица заставляют сначала узнать модель своей карты («Not sure which card you have? Open Salad and check the Performance tab» [факт] — то есть сначала установи). Для него это второй класс: нужен Big Job и снятие страха «разумно ли это вообще».
- **Должен** [гипотеза]: явно выбрать S1 (владелец RTX 3060+) как цель — данные это поддерживают: у слабых карт доход в 5–10 раз ниже. И квалифицировать лид до скачивания: модель карты — это признак сегмента, от которого напрямую зависит ценность (`segmentation.md §7–8`: признак, который меняет решение о ценности, становится вопросом квалификации). Салат это уже наполовину делает (блок требований, таблица) — это сильная сторона.

---

## 2. One-liner и базовые сообщения

### 2.1 One-liner (`communication.md §5`: что это + Core Jobs + ценность в критериях)

Главная (B2B): «Salad orchestrates the world's idle GPUs.» + «…Up to 90% less than hyperscaler pricing.» — формула выполнена: что это, работа, ценность цифрой. [факт + вывод]

/download/:

| Элемент | На лендинге | Оценка |
|---|---|---|
| Что это | «Salad for Chefs» + «the Windows app» (в how it works). Категория «приложение для заработка на простое ПК» читается | ✔ [факт + вывод] |
| Core Job | «earn from your PC», «connects eligible capacity to real customer workloads while you're away» | ✔ [факт] |
| Ценность в критериях | «The easiest way» — прилагательное без уровня. Цифры в hero нет; они начинаются с блока 5 | ✘ в hero [факт + вывод] |

### 2.2 Ценность: критерии или прилагательные?

| Формулировка | Тип | Статус |
|---|---|---|
| «The easiest way to earn from your PC» | превосходная степень без проверяемого уровня | [факт + вывод] |
| «Most machines earn $0.230 – $0.286 /hr» | **настоящий критерий** (направление + уровень, по сроку и выборке) | [факт] |
| «Estimated Profit: $1.34 to $1.79» (день) | **критерий после затрат** — редкость в категории | [факт + вывод] |
| «$7M+ paid out to Chefs» | доказательство, что выплаты реальны (не ценность на человека) | [факт + вывод] |
| «pause instantly», «Customer workloads cannot browse your Windows files» | конкретные критерии по контролю и безопасности | [факт] |
| «Earn real rewards» (футер) | «real» без уровня; при этом «Reward Points have no cash value» в terms | [факт + вывод] |
| «Your GPU is already good enough» (/earning-rates/) | обещание без уровня; для RTX 2060 это ≈ $0.03/ч | [факт + вывод] |

Вывод: на уровне данных ценность выражена критериями лучше, чем у кого-либо в нашей выборке; на уровне заголовков — прилагательными. [вывод]

### 2.3 Фичи как доказательство или как сообщение?

- Hero и How it works ведут через результат («earn», «redeem»), а не через фичи. ✔ [вывод]
- «Isolated Linux VM» подан как доказательство под конкретный страх («cannot browse your Windows files») — образцовая привязка фичи к критерию (`communication.md §4`). [факт + вывод]
- Калькулятор электричества — фича, которая сама по себе является доказательством ценности (проба результата). [вывод]
- Слабое место: «chopping», «Salad Balance», «Kitchen», «Storefront» — внутренний язык бренда. Посетитель должен его перевести (`customers-attention-management.md §11`: неоплаченная работа внимания). «Chopping» встречается в H2 раньше, чем объяснено. [факт + вывод]

---

## 3. Лендинг как путь посетителя: блок за блоком

Канон: лендинг — короткая Critical Chain of Jobs (цепочка шагов клиента), результат которой — достаточно веры и мотивации для первого шага (`communication.md §8`).

| # блока /download/ | Вопрос посетителя | Канонический блок | Закрыт? |
|---|---|---|---|
| (главная) | «Я туда попал?» | — | **Разрыв №0** для тех, кто пришёл на salad.com: путь к заработку — одна кнопка в шапке. Для пришедших по рекламе прямо на /download/ — разрыва нет [факт + вывод] |
| 1 Hero | «Что это?» | 1. One-liner | Да, кроме ценности в критериях [вывод] |
| 1 Hero (видео) | «Покажите» | 5 / 8 | Не оценено (видео не смотрелось). Визуала State B (итог: «купил игру на баланс») на первом экране нет — справа плеер [факт] |
| 2 What you'll need | «Мне подходит?» | Реальные условия (допущение №4) | **Да, сильно**: Windows only, RTX 3060+ — до скачивания [факт] |
| 3 Цифры | «Это работает, платят?» | Доказательство | «$7M+ paid out» — да [факт] |
| 4 How it works | «Как именно, сколько усилий?» | 5. Как выполняется работа | Да [вывод] |
| — | «Это про мою ситуацию? Почему сейчас?» | 3. Контекст / триггер | Частично: «sit unused» есть, триггера нет (новая карта, счёт за свет, конец майнинга) [вывод] |
| 5 Виджет | «Сколько получу я?» | 4. Ценность в критериях | Да по факту, **но якорь — top 1%** на одной из самых дорогих карт [факт + вывод] |
| 6 Калькулятор | «А после электричества?» | 4 + снятие страха «уйду в минус» | Да — сильнейший блок [вывод] |
| 6 «Is this real money?» | «Это деньги?» | 7. Страхи | Да, честно, но спрятано в аккордеон [факт] |
| 7 Rewards | «На что потрачу?» | 8. State B | Список категорий, без курса вывода [факт] |
| 8 Отзывы | «Кто такие же, как я?» | Истории | Есть имена и профессии, нет сумм и сроков [факт] |
| 9 Sealed box | «Что делают на моём ПК?» | 7. Страхи | Да, сильно. Майнинг по умолчанию — честно назван, но одной строкой [факт] |
| — | «Чем плохо то, что я делаю сейчас?» | 6. Проблемы текущего способа | Только в отзыве («wasting electricity», «traditional crypto mining»). Блока нет [факт] |
| — | «Не испортится ли карта? Будет ли шуметь?» | 7. Страхи | **Разрыв**: не найдено на лендинге [факт] |
| — | «Когда первая награда?» | 4 / Aha | **Разрыв**: не найдено на лендинге [факт] |
| 10 What earns best | «Моя карта хорошая?» | Реальные условия | Да (повтор блока 2) [факт] |
| 11 Community | «Есть ли живые люди?» | Доказательство | Да, 45k в Discord [факт] |
| 12 CTA | «Делаю» | 9. CTA | «Download Salad» + «Send yourself the link» для тех, кто не за ПК — хорошая ступенька [факт + вывод] |

---

## 4. Пять компонентов Consideration Activators (знание, которое двигает выбор)

Канон: `consideration-activators.md §1`; компоненты 1–3 — минимум для активации, 4–5 сильно поднимают конверсию.

| # | Компонент | Что есть | Чего нет | Оценка |
|---|---|---|---|---|
| 1 | Новый способ выполнить Big Job (Job Graph) | «Your PC has compute and bandwidth that often sit unused… rewards you for contributing it» | Связка с Big Job («ПК окупает себя / оплачивает игры») словами — нет; есть косвенно через магазин | Частично [вывод] |
| 2 | Конкретная разница в ценности по критериям | $/час по карте, прибыль после электричества, по неделе, по выборке | Сравнение с альтернативой («ничего не делать», майнинг, NiceHash); время до первой награды; потери при выводе | **Есть, сильно**, но с завышенным якорем [факт + вывод] |
| 3 | Названный продукт + первый шаг | «Download for NVIDIA / AMD», «Send yourself the link» | — | Есть [факт] |
| 4 | Снятие конкретных страхов | sealed box, пауза, VM, «Is this real money?», требования к ПК, «$7M+ paid out» | Износ/температура/шум; майнинг по умолчанию подан как факт, а не как снятый страх; комиссия на выводе; срок появления баллов (5 рабочих дней — только в terms) | Частично, выше среднего [вывод] |
| 5 | «Увольнение» текущего способа | Отзыв про майнинг и «wasting electricity» | Явного блока «почему не простой / не NiceHash / не просто майнить» нет | **Почти нет** [факт] |

---

## 5. Семь допущений покупки (`communication.md §2`)

| # | Допущение | Статус для Salad | Основание |
|---|---|---|---|
| 1 | Лид из целевого сегмента, с нужными Big Jobs | **Частично.** Лендинг сам фильтрует (требования к ПК). Риск: трафик S3 с ноутбуками | [факт + гипотеза] |
| 2 | Ценность выше прогноза и текущего способа | **Под вопросом для слабых карт**: RTX 3060 × 8 ч ≈ $0.18–0.30 в день до электричества (расчёт по таблице). Для 4090 — ≈ $40–54/мес прибыли по калькулятору (по умолчанию). Прогноз завышается крупной цифрой top 1% | [факт + вывод] |
| 3 | Лид понимает ценность | **Да**, если доскроллит до блока 5; hero ценность не называет | [вывод] |
| 4 | Нужные условия в реальности выполнены | **Честно раскрыто**: Windows 10/11 64-bit, не Mac/Linux, лучшее — RTX 3060+, 18+, не санкционные страны (последнее — только в terms) | [факт] |
| 5 | Конкретные страхи снижены | **Частично**: безопасность и контроль да; железо, «грязные» деньги (майнинг, наценка вывода) нет | [вывод] |
| 6 | Путь до ценности достаточно короткий | **Не раскрыт**: «within five (5) business days» и минимальный вывод (самый дешёвый PayPal $5 за $5.99 баланса) на лендинге не показаны. Для RTX 3060 это ≈ 3–5 недель по 8 ч до первого PayPal ($5.99 баланса ÷ $0.18–0.30 в день; расчёт) | [факт + вывод] |
| 7 | Цепочка не ломается | Прямые .exe с GitHub (без промежуточной страницы); «Send yourself the link» для мобильных — хорошо. Магазин при первом открытии показывает «Fetching (a few) ingredients from the pantry...» и грузится несколько секунд; в консоли ошибки. Cookie-баннер не обнаружен | [факт] |

---

## 6. Барьеры, страхи, ожидания и проба Aha

### 6.1 Барьеры (факты) vs страхи (прогнозы)

Канон: барьер — объективный факт, снимается изменением реальности; страх — прогноз, снимается коммуникацией, только если поломка не реальна (`barrier-removal.md §1, §3, §4`).

**Барьеры** [факт]:
- Только Windows (класс «неподдерживаемый контекст», `barrier-removal.md §5`) — назван честно, до CTA. ✔
- Слабое железо → центы в час (это не запрет, но ценность ниже порога) — раскрыто через таблицу. ✔
- Электричество платит пользователь; в дорогих регионах прибыль может уйти в ноль — раскрыто калькулятором. ✔ Это образцовое превращение барьера в инструмент: человек сам видит, проходит ли он.
- 18+, санкции — только в terms. ✘
- Сгорание баллов после 12 месяцев без начислений — только в terms. ✘

**Страхи** [вывод]:
| Страх | На лендинге |
|---|---|
| «Чужой код залезет в мои файлы / это вирус» | Снят: «sealed box», VM, «cannot browse your Windows files» ✔ |
| «Будет мешать играть» | Снят: «pause instantly», «automatically when your PC is idle» ✔ |
| «Мне не заплатят / это не деньги» | Частично: «$7M+ paid out», «Is this real money?» (честно, но ответ «нет, это баланс» звучит тревожно без курса вывода) |
| «Уйду в минус по электричеству» | Снят калькулятором ✔ |
| «Карта износится / перегреется / будет шуметь» | Не найдено на лендинге ✘ |
| «Меня втянут в майнинг / моим IP будут пользоваться» | Названо, но не снято: «Crypto mining… enabled by default»; bandwidth sharing — ссылка на help-статью ✘ |
| «Потеряю на выводе» | Не найдено на лендинге; в магазине наценка ≈ 10–20% ✘ |

### 6.2 Управление ожиданиями (`communication.md §9`)

- **Плюс** [факт + вывод]: данные «Honest numbers, on purpose», «Nothing here is a projection», «If you are new, expect to start here» — это ровно то, что канон называет честным прогнозом, который продукт может превзойти.
- **Минус** [факт + вывод]: интерфейс подрывает собственную честность. Крупная цифра — «top chefs», по умолчанию — RTX 4090, в калькуляторе дополнительная строка «Top 1%… about $3.30 a day». Посетитель с RTX 3060 запоминает «$0.47 в час» и получает $0.03. Канон: завышенное ожидание даёт разочарование даже при объективно хорошем результате (`value-creation`, `communication.md §9`). [гипотеза о поведении посетителя]
- **Минус**: «Salad Balance» в USD создаёт ожидание «$1 = $1», а в магазине $5 PayPal = $5.99 баланса. Первое реальное столкновение с ценностью (вывод) — с отрицательной ошибкой прогноза. [факт + вывод]

### 6.3 Проба Aha на лендинге

- Калькулятор — настоящая проба результата до установки: «сколько я, с моей картой, в моей стране, получу чистыми». Это перенос Aha максимально влево (`customers-attention-management.md §6`). [вывод]
- Но настоящий Aha — первая полученная награда (PayPal/Nitro) — во времени не обозначен. [вывод]
- В приложении есть Performance tab для определения карты — на лендинге его роль «сначала установи, потом узнаешь свою цифру»; автоопределения карты в браузере нет. [факт + гипотеза о том, что это возможно]

---

## 7. Силы за и против перехода, конкуренты

По `behaviour-change.md §9`.

**Драйверы** [вывод]:
- Знание более выгодного способа (компоненты 1–2) — сильное, через данные.
- Идентичность: «Chef», «Kitchen», Discord на 45k — принадлежность к сообществу геймеров/энтузиастов железа.
- Любопытство: таблица по картам — «а сколько моя?»

**Блокеры** [вывод]:
- Цена сейчас vs выгода потом: установка, настройка, электричество — сразу; первая награда — через недели.
- Страхи (железо, майнинг, IP) — частично открыты.
- Будущая отрицательная ошибка прогноза: якорь top 1% и наценка вывода.
- Объективный барьер: не Windows / слабая карта.

**Конкуренты, которых лендинг должен «уволить»** (`consideration-activators.md §1`, компонент 5) [гипотеза — по названиям, на лендинге не упоминаются]:
1. **«Ничего не делать»** — главный конкурент. Аргумент есть только в отзыве («wasting electricity»). Канон: мы не можем создать проблемы текущего способа, только показать реальные (`behaviour-change.md §9`).
2. **Самостоятельный майнинг / NiceHash** — для S2. На лендинге только отзыв.
3. **Другие сервисы «заработай на ПК»** (Grass, Honeygain — bandwidth; другие GPU-сети) — не упоминаются. Сильный аргумент Salad, который можно было бы использовать: заработок по картам публикуется за каждую неделю.
4. **Продать/не покупать мощную карту** — для S1 (неявная альтернатива Big Job «окупить ПК»).

---

## 8. Итог

### 8.1 Топ-риски лендинга

1. **Якорь на top 1% и RTX 4090** завышает ожидание большинства → разочарование в первые недели, негатив в Reddit/Discord. [факт + гипотеза о последствиях]
2. **Наценка вывода и «no cash value» не показаны на лендинге** → отрицательная ошибка прогноза в самый важный момент (первый вывод). [факт + вывод]
3. **Майнинг по умолчанию — одной строкой** → риск, что человек почувствует, что его «втянули», и потеряет доверие ко всему продукту. [факт + гипотеза]
4. **Время до первой награды не названо** → длинная серия шагов до Aha, на ней теряется внимание (`customers-attention-management.md §6, §8`). [вывод]
5. **Вход через B2B-главную** → человек, который хочет заработать, видит «90% дешевле облаков» и может прочитать это как «моё железо продают за копейки». [гипотеза]

### 8.2 Точки роста: конкретные правки

Формулировки — **черновики-гипотезы** на языке оригинала. `[VERIFY]` — нельзя публиковать без данных Salad.

1. **Hero с критерием вместо «easiest».**
   Сейчас: «The easiest way to earn from your PC.»
   Вариант: «*Your gaming PC earns while you're away — most RTX 4070 owners make $0.06–0.07 an hour, paid out in PayPal, Steam or Nitro.*» (цифры из таблицы за 15–21.11.2026; брать текущую неделю и выбрать популярную карту `[VERIFY — какая карта самая частая у новичков]`).
2. **Крупная цифра — «Most machines», мелкая — top 1%.** «*Most RTX 4090s earned $0.23–0.29/hr last week. Top 1%: $0.48.*» По умолчанию — самая частая карта, а не 4090. Ещё лучше — определять GPU в браузере (WebGL renderer) `[VERIFY — техническая точность]`.
3. **«Сколько до первой награды»** в калькуляторе: «*At 8 hrs/day, an RTX 3060 reaches its first $5 PayPal reward in about 3–5 weeks.*» (расчёт по таблице и цене в магазине; `[VERIFY]`). Плюс дешёвая первая награда («Discord Nitro Basic $2.99» в магазине) как ранний Aha.
4. **Курс вывода — на лендинге, рядом с «Is this real money?»**: «*Salad Balance is shown in USD. Rewards cost slightly more than face value — e.g. a $20 PayPal reward is $22.50 of balance.*» (факт из магазина). Честность здесь дешевле, чем разочарование при первом выводе.
5. **Майнинг — как выбор, а не как сноска**: «*Mining is on by default because it fills the hours when no customer job is available. Turn it off anytime in Settings — you'll earn less.*» `[VERIFY — причина по умолчанию и влияние на доход]`.
6. **Закрыть страх за железо**: «*Will Salad wear out my GPU?*» + данные о температурах/лимитах мощности, если есть `[VERIFY]`.
7. **Блок «увольнения» простоя**: «*Your PC already draws 100 W sitting idle. Put the same hours to work.*» (102 W — оценка калькулятора для простоя по умолчанию `[VERIFY — формулировка]`).
8. **Истории с цифрами**: к трём отзывам добавить «карта / часы в день / сколько месяцев / на что потратил» `[VERIFY — реальные пользователи с согласием]`.
9. **Вход с главной**: вторая строка под B2B-hero для пользователей — «*Have a gaming PC? Earn from it →*», чтобы не терять тех, кто пришёл на корень домена.
10. **Сократить внутренний жаргон** («chopping», «Kitchen») до момента, когда он объяснён, или дать расшифровку при первом упоминании.

### 8.3 Рискованные допущения лендинга (RAT) и как их проверить дёшево

Ранжировано по «насколько смертельно, если неверно» × «насколько дёшево проверить». [гипотеза — все пункты]

| # | Допущение | Если неверно | Дешёвая проверка |
|---|---|---|---|
| 1 | Крупная цифра top 1% повышает установки и не роняет удержание | Отток в первые 2–4 недели и негатив | A/B: якорь «Most machines» vs «Top chefs»; метрика — удержание на 30-й день и доля дошедших до первого вывода |
| 2 | Наценка вывода не бьёт по доверию | Отзывы «обман» после первого вывода | Анализ r/SaladChefs и тикетов поддержки по словам «fee», «markup», «$5.99» |
| 3 | Майнинг по умолчанию не отталкивает | Удаления сразу после онбординга | Доля отключивших майнинг × удержание; 10 интервью с удалившими (`barrier-removal.md §7`) |
| 4 | Посетители знают модель своей карты | Отвал на виджете, «не знаю, что выбрать» | Аналитика взаимодействия с селектором; тест автоопределения GPU |
| 5 | Главный сегмент — владельцы RTX 3060+ | Трафик ноутбуков/слабых ПК, низкая ценность | Распределение GPU у новых установок × доход в первый месяц |

### 8.4 Что из этого взять нашему charity / passive-earning продукту

1. **Публиковать реальные цифры пользы по неделе, с методикой.** «Honest numbers, on purpose. Nothing here is a projection» — сильнейший ход Salad. Для нас: «за прошлую неделю час работы приложения = X обедов / Y минут вычислений для исследования», с выборкой и датой. [вывод]
2. **Якорь — типичный пользователь, а не лучший.** Ошибка Salad — показывать top 1% крупно. Нам первой показывать медиану, лучшее — мелко. [вывод]
3. **Калькулятор «польза минус затраты»** — перенести один в один: «твоё устройство × часы × страна → вклад в месяц и стоимость электричества». Он одновременно даёт попробовать результат и снимает страх «уйду в минус». [вывод]
4. **«Запечатанная коробка» как блок доверия**: что именно выполняется, что не видит наши файлы, пауза одной кнопкой. Для charity добавить «куда идут деньги/ресурсы» с проверяемым доказательством. [вывод]
5. **Не прятать «грязные» детали** (майнинг по умолчанию, комиссии, курс): у Salad они есть, но в сноске и в магазине. Для charity-продукта доверие — главная ценность; любая скрытая деталь опаснее, чем низкая сумма. [вывод]
6. **Пожертвование как главный сценарий, а не опция в магазине.** У Salad «St Jude… $0.10 Donation» — пункт в конце витрины. Это подтверждает, что инфраструктура для микропожертвований возможна, но позиционирование «помочь» у них отсутствует — место в категории свободно. [факт + гипотеза]
7. **Квалифицировать до установки**: блок «What you'll need» до кнопки экономит обеим сторонам разочарование. [вывод]
8. **Отделить B2B от пользователя**: у Salad это сделано (отдельная шапка, бренд Chefs), но вход с корня домена слабый. Если у нас будет двусторонняя модель — у пользователя должна быть своя главная. [вывод]

---

## Источники (сняты 2026-11-22)

- https://salad.com/ — главная (B2B; curl + Playwright, скриншот первого экрана `.playwright-mcp/salad-home-hero.png`)
- https://salad.com/download/ — лендинг для пользователей (curl + Playwright для виджета и калькулятора, скриншот `.playwright-mcp/salad-download-hero.png`)
- https://salad.com/earning-rates/ — таблица заработков по GPU за 15–21.11.2026 (Playwright)
- https://salad.com/store — магазин наград (Playwright, без логина)
- https://salad.com/terms/chefs/ — условия для Chefs
- https://salad.com/faq — перенаправляет на /download/; https://salad.com/rewards — 404
- Внутренний контекст: `apps/04-salad.md` (на момент разбора — пустой шаблон, заметок нет)

Методология (канон): `Next-Move-Theory-Canon/Advanced-Jobs-To-Be-Done/` — communication.md (§2–§9), consideration-activators.md (§1–§6, §10), barrier-removal.md (§1–§7), customers-attention-management.md (§6, §8, §11), behaviour-change.md (§9–§10), job-structure.md (§8–§9), segmentation.md (§2, §7–§8), ajtbd-key-theses.md (§24); `.claude/skills/nmt-craft-go-to-market/` (SKILL.md, references/glossary.md); `.claude/skills/nmt-diagnose/SKILL.md`.

Не снималось: содержание YouTube-видео «Welcome to Salad»; приложение после установки (онбординг, экран выбора майнинга); help-портал (support.salad.com) кроме ссылок; A/B-варианты страниц (видна одна версия).
