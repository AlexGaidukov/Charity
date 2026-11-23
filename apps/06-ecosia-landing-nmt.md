# Ecosia (ecosia.org): разбор лендинга по Next Move Theory

Дата снятия: 2026-11-22. Главная https://www.ecosia.org/ и подстраницы, которые новичок видит в первые 1–2 клика (список в конце).
Статусы утверждений: **[факт]** — дословно или напрямую видно на сайте; **[вывод]** — выведено из фактов и канона; **[гипотеза]** — моё предположение, нужна проверка.
Методология: Next Move Theory / Advanced JTBD (канон в `Next-Move-Theory-Canon/`). Термины методологии даны в скобках при первом упоминании.

---

## Резюме на один экран

1. **Главный экран говорит не о деревьях, а о приватности.** Крупный заголовок: «Private by design». Слово «trees» на первом экране есть только во вкладке браузера («Ecosia - the search engine that plants trees») и в счётчиках под строкой поиска, а их на десктопе закрывает cookie-баннер. На телефоне про деревья на первом экране нет ничего. Уникальное отличие Ecosia ушло ниже сгиба страницы. [факт + вывод]
2. **Заголовок про приватность спорит с первым, что видит человек.** Под «Private by design» сразу вылезает баннер: «we and our 5 partners use cookies… Personalised advertising… Google, Marketing». Обещание и первое впечатление расходятся, и это бьёт по доверию. [факт + вывод]
3. **Сильнее всего сделана проба продукта.** Строка поиска стоит на главной, регистрации нет. Попробовать можно за 5 секунд, и после первого запроса в шапке появляется личный счётчик «1» и уровень «Level 1 - Ecocurious». [факт] Из всех разобранных нами лендингов здесь самый короткий путь до первого результата. [вывод]
4. **Прозрачность сделана лучше, чем у всех, кого мы смотрели**: ежемесячный финотчёт с разбивкой до налогов и рекламы, список стран и сумм, B Corp. Но это доказательство того, что *организация* честная. Ответа на вопрос «что меняется от *моих* поисков» нет: сколько запросов дают дерево, на лендинге не найдено. А в справке прямо написано, что личный вклад — это оценка по среднему пользователю. [факт + вывод]
5. **Главный страх не назван: «результаты будут хуже, чем в Google».** На главной об этом ни слова, хотя на странице выдачи видно, что результаты идут от Google (ссылка «Report result» ведёт на support.google.com). Одна строка «Results powered by Google/Bing» сняла бы основное возражение. [факт + вывод]
6. **Цепочка обрывается на самом ценном действии: сделать Ecosia поиском по умолчанию.** На главной это не предлагается. Единственный CTA в шапке, «Download Ecosia Browser», сразу запускает скачивание zip, без объяснения. На мобильном CTA в шапке нет вообще, ссылки на приложения только в футере. Последний блок «Join 20 million people making a difference every day.» стоит без кнопки. [факт]
7. **Мелкие поломки**: /about отдаёт 404; на карточке «How Ecosia works» в выдаче написано «200M trees and counting!», а на главной в тот же момент 258,701,375; на главной доход в евро, в отчёте в долларах. [факт]

**Что взять себе (charity / passive-earning):** пробу результата ставить прямо на первый экран, без регистрации (как строка поиска у Ecosia); финансовую прозрачность делать как у них, ежемесячно и до цента; но, в отличие от них, отвечать на вопрос «что даёт именно моё действие» честной формулой и держать уникальное отличие в главном заголовке, а не под сгибом.

---

## 0. Что было на лендинге (снятие 2026-11-22)

Способ: curl получил 403 (сайт блокирует неброузерные запросы), поэтому всё снято через Playwright (Chromium): accessibility-снимки, извлечение текста, скриншоты десктоп 1200×659 и мобильный 390×844 в `.playwright-mcp/` (`ecosia-home-first-screen.png`, `ecosia-home-mobile.png`, `ecosia-browser-confirmation.png`). Регион поиска определился как «Bulgaria». [факт]

Где у Ecosia «лендинг» [вывод]: отдельной маркетинговой страницы для новичка нет. Главная — это строка поиска плюс маркетинговые блоки под ней. Дальше новичок попадает на /browser (CTA в шапке и в футере), в финотчёт (ссылки с главной, из выдачи и из футера выдачи), на страницу проектов в блоге и на карточку «How Ecosia works» в выдаче после первого запроса. /about отдаёт 404. [факт]

### 0.1 Главная https://www.ecosia.org/: блоки по порядку (тексты дословно)

| # | Блок | Дословный текст |
|---|---|---|
| — | `<title>` / meta | «Ecosia - the search engine that plants trees» / «Ecosia is a search engine and AI that uses 100% of its profits for the planet, supporting tree planting and renewable energy projects.» |
| — | Шапка | логотип ECOSIA · CTA **«Download Ecosia Browser»** (с иконкой Apple на macOS; ведёт на /browser/confirmation, где сразу начинается скачивание `EcosiaInstaller.zip`). На мобильном 390px CTA в шапке нет |
| — | Cookie-баннер (Didomi) | «With your agreement, we and our 5 partners use cookies or similar technologies to store, access, and process personal data like your visit on this website, IP addresses and cookie identifiers. Some partners do not ask for your consent…» / «Analytics, Essential, Google, Marketing, Personalised advertising and content…» · «Manage cookies» · «Reject non-essential» · «Accept all». Закрывает нижнюю треть экрана на десктопе и ~60% на мобильном |
| 1 | Hero (H1) | **«Private by design»** · поле поиска с плейсхолдером «Ask, search, browse...» · кнопки «AI tools», микрофон («Start recording») |
| 2 | Счётчики (под строкой поиска) | «258,701,375 trees planted by Ecosia» (ссылка на blog/tag/where-does-ecosia-plant-trees) · «€106,199,130 dedicated to climate action» (ссылка на финотчёт) |
| 3 | Why choose Ecosia? | H3 «What we stand for». Четыре пункта: «100% of profits for the planet. We use all our profits for climate action, with the majority going into tree-planting projects around the world.» / «Secure and private. We respect your privacy like we respect the planet. We only collect data necessary to deliver a great product, and not a byte more.» / «AI designed for you, not profit. We use small AI models that deliver accurate answers from reliable sources. Your conversations are private and never used to train AI models.» / «We fund renewable energy. Our solar power investments help produce clean energy, pushing fossil fuels off the European energy grid.» |
| 4 | Monthly financial report | «€4,041,907 total income this month» · H3 «We're fully transparent» · «We publish financial reports every month so you can see exactly how much we made and how we spent it. Total transparency, every month.» · CTA «See our reports» |
| 5 | Our tree planting approach | H3 «We restore and protect biodiversity hotspots» · «Instead of monocultures, we grow over 900 different native species where they are needed most. Always shoulder-to-shoulder with local communities.» |
| 6 | Цифры | «258,701,375 Trees planted by the Ecosia community» · «20 million people using Ecosia» · «900+ native species» · «35+ countries involved» · «70+ active projects» · CTA «Discover all projects» |
| 7 | Финальный заголовок | **«Join 20 million people making a difference every day.»** Кнопки под ним нет |
| — | Футер | «B-Corporation Certificate» · What we do: Ecosia Browser / Ecosia Search / Financial reports · About: Help and Legal / Careers / Press / Blog · Legal (вкл. «Transparency information (MStV)», «Empowering Consumers Directive») · Apps: Play store / App store · соцсети |

### 0.2 /browser https://www.ecosia.org/browser

`<title>` «The browser that funds tree planting». [факт]

| # | Блок | Дословный текст |
|---|---|---|
| 1 | Hero | H1 **«The browser that funds tree planting»** · H2 «Be climate active while you browse» · CTA «Download Ecosia Browser» · ссылка «Looking for Ecosia Search?» |
| 2 | Our mission | «100% of our profits are for the planet» / «Ecosia's mission is to create simple ways for everyone to be climate active every day.» / «We dedicate 100% of our profits to the planet. That means you can plant trees, protect endangered animals, and uplift communities around the world simply by browsing.» · «Learn more about Ecosia» · счётчики деревьев и евро |
| 3 | Top features | «The best way to search with Ecosia»: «Ecosia search built in…» / «Track your impact. With your own Ecosia profile, you can see how you're helping people, the planet and animals.» / «AI designed for you. Our AI runs on European servers and uses smaller AI models than most mainstream models.» |
| 4 | Privacy | «Stay safe while browsing. Our privacy panel keeps an eye out and warns you about unsafe sites…» |
| 5 | Performance | «Fast loading. Our browser is optimized for speed, loading pages up to three times faster than most mainstream browsers.» / «Energy saver…» |
| 6 | Customization | обои из проектов посадки · «Import settings. Set things up just how you like them by importing favorites and settings from another browser.» · тема · фичи домашней страницы |
| 7 | Финал | **«Switch to the browser that plants trees — it only takes 60 seconds»** |

/browser/confirmation: H1 «Only a few steps left to get started» · «If your download doesn't begin automatically, click here to download.» · **«Unable to install? Set Ecosia as default search instead.»** · три шага «Open / Install / Launch… import any settings and preferences you wish to bring over from your old browser.» [факт]

### 0.3 Что новичок видит после первого поиска (https://www.ecosia.org/search?q=best+running+shoes)

- Справа карточка: **«How Ecosia works» / «Like other search engines, we make money from ads. We then use 100% of our profits for the planet. The result: 200M trees and counting!»** / «See our financial reports». [факт]
- В шапке личный счётчик «1»; по клику: «Guest user», «Level 1 - Ecocurious», «See your impact grow. Reach new levels and see the climate impact you're having through your own Ecosia account.», «Sign in» / «Create an account»; меню «Use Ecosia: Desktop Browser / Android App / iOS App / Ecosia for Companies». [факт]
- Под каждым результатом «Report result» со ссылкой на support.google.com, то есть результаты в этом запросе шли от Google. [факт] Футер выдачи: «Want to know how we spend our profits? See financial reports» / «Check out the latest updates about our planting projects». [факт]

### 0.4 Финотчёт (ecosia.co/finreportsen → blog.ecosia.org/ecosia-financial-reports-tree-planting-receipts/)

«Let's be clear about the numbers» · October 2026 · «3,459,287 Trees financed this month» (перед числом отрисован символ «$») · «$2,428,476.56 Dedicated to climate action» · разбивка: Trees $1,305,253.59; Other climate impact $1,123,222.97; Building search diversity $170,041.56; «Proudly paying taxes $1,030,425.02… Unlike much of Big Tech, we stay clear of tax evasion schemes.»; «Spreading the word $100,878.28»; Operational costs $1,050,868.05 (с разбивкой до офиса и поездок) · «Total income this month $4,780,689.46» · «Ecosia is a not-for-profit business. We don't pay out dividends and cannot be bought.» · «Please note that it takes six weeks to process the month's payments.» · выплаты по 12 странам · внизу «Get Ecosia for free and plant your first tree! Add Ecosia to Chrome». [факт]

### 0.5 Страница проектов (blog.ecosia.org/tag/where-does-ecosia-plant-trees)

«At Ecosia, we plant trees where they're needed most…» и карточки «Your trees in Argentina / Australia / Brazil / … / the United Kingdom» с одной фразой о смысле проекта (например, Indonesia: «Finding alternatives to palm oil monocultures to fight deforestation and safeguard orangutan habitats.»). CTA «Add Ecosia to Chrome». [факт]

### 0.6 Справка, куда лендинг не ведёт напрямую, но где лежат ответы (для сравнения)

- https://support.ecosia.org/article/1217-eu2024-825 (ссылка есть в футере главной, «Empowering Consumers Directive»): «A tree counts as planted by Ecosia once a second field monitoring, three years after planting, confirms it's alive.» / проекты «are not carbon-offset projects» / «Ecosia profiles show an estimate of impact metrics for an average user at the level of that profile.» / «Ecosia doesn't earn money from searches themselves, we fund tree planting through the profit generated by ads shown alongside search results». [факт]
- https://support.ecosia.org/article/844-seed-counter: «These numbers are based on Ecosia's overall impact and averaged / scaled by level, not an exact, individualised count of "your own" trees.» / «Seeds don't equal money. Seeds do not follow the logic as "one seed = one tree".» / growth points «designed to reward habit and long-term use, not every single search». [факт]

---

## 1. Для кого лендинг и какие работы он предполагает

Уровни (`ajtbd-key-theses.md §9`, `job-structure.md §9`): Big Job — результат уровнем выше, в нём живёт мотивация; Core Job — самая высокая работа, которую продукт выполняет целиком; Small Jobs — работы того же уровня, которые продукт не делает; Micro Jobs — шаги под Core Job.

### 1.1 Работы (гипотеза по тексту лендинга)

**Сегмент S1: «человек, которого тревожит климат, но у которого нет времени и денег что-то делать»** [гипотеза; по title, счётчикам, «making a difference every day»]
- **Core Job, которую выполняет Ecosia** [вывод]: «хочу найти ответ / нужный сайт в интернете». Ecosia выполняет её целиком (поиск, AI-чат, браузер).
- **Big Job** [гипотеза]: «хочу регулярно делать что-то реальное для климата, не тратя дополнительных денег и времени», и рядом эмоциональная работа «чувствовать себя человеком, который не просто переживает, а действует» (опора на identity alignment, `behaviour-change.md §9`).
- **Точка A** [гипотеза]: ищет в Google десятки раз в день по привычке; переживает за климат; донатить регулярно не готов или забывает; не доверяет «зелёным» обещаниям компаний.
- **Точка B** [гипотеза]: ищет так же, как раньше, ничего не потерял в качестве; знает и видит, что его привычное действие финансирует реальные, проверенные посадки.
- **Критерии успеха** [гипотеза; ✔ — отражено на лендинге, ✘ — не найдено]:
  - ✘ **результаты не хуже Google** (направление: качество выдачи; уровень: «нахожу с первого запроса так же, как раньше»). Не найдено на главной.
  - ✘ **переход без усилий** («поставить по умолчанию за минуту»). На главной не найдено; на /browser есть «it only takes 60 seconds» ✔ (только для браузера).
  - ✔ **деньги реально идут на климат, это можно проверить**: «100% of profits», ежемесячный отчёт, B Corp.
  - ✔ **деревья настоящие, не «галочка»**: «900+ native species», «Instead of monocultures», проекты по странам. Самое сильное доказательство, правило «засчитываем дерево, только если оно живо через 3 года», лежит в справке, не на лендинге.
  - ✘ **мой вклад виден и понятен** («сколько моих запросов = дерево»). Не найдено на лендинге; в справке прямо сказано, что личные цифры — оценка по среднему.
- **Small Jobs** (того же уровня, Ecosia их не делает) [вывод]: напрямую донатить на посадку или климат; компенсировать свой углеродный след (Ecosia в справке подчёркивает, что это «not carbon-offset projects»); голосовать кошельком, выбирая «зелёные» товары.
- **Micro Jobs** [вывод]: набрать запрос; поставить Ecosia по умолчанию в браузере или на телефоне; перенести закладки; завести аккаунт, чтобы видеть уровень.

**Сегмент S2: «европеец, который не хочет отдавать данные Big Tech»** [вывод: на него работают H1 «Private by design», «not a byte more», «European servers», в отчёте «European Search Perspective»]
- Core Job та же (поиск), **Big Job**: «пользоваться интернетом и AI, не кормя своими данными американские корпорации». Критерии: не трекают, не обучают AI на моих разговорах, данные в Европе. Конкуренты: DuckDuckGo, Startpage, Qwant, Brave.

**Сегмент S3: «пользователь AI-чатов, которому важна этика»** [гипотеза; блок «AI designed for you, not profit», плейсхолдер «Ask, search, browse...»]. Big Job: «получать ответы от AI, не поддерживая энергозатратные модели Big Tech».

**Сегмент S4: компании и муниципалитеты** [факт: «Ecosia for Companies» в меню выдачи, в справке кейс «How one UK council planted 3,500 trees»]. На главной этот сегмент не адресован. [факт]

### 1.2 Кого лендинг обслуживает на самом деле и кого должен

- **Первый экран обслуживает S2 (приватность)** [вывод]: H1 и плейсхолдер про приватность и AI. **Тело страницы обслуживает S1 (климат)**: счётчики, 100% прибыли, отчёт, посадки. Страница говорит с двумя сегментами по очереди и ни одного не проводит до конца цепочки. [вывод]
- **Должен в первую очередь — S1** [вывод + гипотеза]. Причина в том, что на языке канона называется причинным критерием сегментации (`segmentation.md §7`): у S1 есть свойство, благодаря которому Ecosia может создать ценность, которую не создаёт никто из конкурентов, — «мой привычный поиск сам финансирует посадки». Для S2 Ecosia — одна из многих приватных поисковиков, и здесь ей приходится соревноваться на поле, где DuckDuckGo и Brave сильнее и известнее. [гипотеза: нужна проверка на данных конверсии по сегментам]
- Возможная причина смещения в сторону приватности и формулировки «dedicated to climate action» вместо «your search plants a tree» [гипотеза]: требования директивы ЕС EmpCo к экологическим заявлениям (в футере есть ссылка на объяснение «Communicating in line with the European Directive on Consumer Empowerment»). Это реальное ограничение, но решается оно точной формулировкой, а не уходом от главного отличия (см. §8.2).

---

## 2. Однострочник и базовые сообщения

### 2.1 One-liner (формула канона: что это + какие Core Jobs выполняет + ценность в критериях, `communication.md §5`)

- В `<title>`: **«Ecosia - the search engine that plants trees»** [факт]. Что это (search engine) — да; Core Job (поиск) — да; ценность — «plants trees», это Big Job-уровень без критерия. Для однострочника это неплохо: его легко пересказать. [вывод]
- На видимом экране однострочника нет: H1 «Private by design» не говорит, что это, и не называет работу. Тест канона «может ли человек после одного прочтения повторить, что это, что делает и какая ценность» (`communication.md §5`) первый экран не проходит: пересказ будет «какой-то приватный поиск». [вывод]
- На /browser лучше: «The browser that funds tree planting» + «Switch… it only takes 60 seconds». Есть что это, Big Job и критерий перехода. [вывод]

### 2.2 Ценность: критерии или прилагательные?

| Формулировка | Тип | Комментарий |
|---|---|---|
| «Private by design», «Secure and private», «a great product» | прилагательные [факт] | Канон: «fast», «safe», «reliable» не являются утверждением о ценности, пока не переведены в критерии (`communication.md §3`) [вывод] |
| «We only collect data necessary… and not a byte more» | полукритерий [вывод] | Направление есть, проверяемого уровня нет (что именно не собирается?) |
| «accurate answers from reliable sources» | прилагательные [факт] | Не сказано, по какому критерию accurate |
| «Your conversations are private and never used to train AI models» | критерий [вывод] | Конкретно и проверяемо, лучшая строка блока |
| «100% of profits for the planet» | критерий [вывод] | Конкретно, но «profit» в справке определён как остаток после затрат, инвестиций и налогов; на лендинге этой оговорки нет |
| «258,701,375 trees», «€106,199,130», «€4,041,907 this month», «900+ species», «35+ countries», «70+ projects», «20 million people» | критерии организации [факт] | Числа сильные, но это критерии *Ecosia*, а не критерии пользователя: «что даст мой поиск» и «не хуже ли поиск» они не отвечают [вывод] |
| «loading pages up to three times faster», «only takes 60 seconds» (/browser) | критерии [факт] | Хорошо; «up to three times faster than most mainstream browsers» без источника [вывод] |

**Итог** [вывод]: о себе Ecosia говорит в цифрах, а о пользователе в прилагательных. Две главные пользовательские ценности (поиск не хуже + мой вклад) на лендинге не выражены ни прилагательным, ни критерием.

### 2.3 Фичи как доказательство или как сообщение?

- На главной фичей почти нет. Блок «What we stand for» — это ценности компании, а не работы пользователя. [вывод]
- На /browser фичи идут списком («Ecosia search built in», «Energy saver», «Change up your look», «Choose your top features») и в основном не привязаны к работе и критерию (`communication.md §4`). Исключения, которые работают как доказательство: «Import settings» доказывает «переход без потерь», «60 seconds» доказывает «переход без усилий». [вывод]
- Финотчёт — образцовое доказательство («proof layer») для критерия «деньги правда идут на климат», но с главной он вынесен на отдельную страницу. На самой главной стоит одна цифра дохода без расходов. [вывод]

---

## 3. Лендинг как путь посетителя: блок за блоком

Канон: лендинг — короткая критическая цепочка работ (Critical Chain of Jobs), её точка B — достаточно веры и мотивации, чтобы сделать первый шаг; каноническая последовательность из 9 шагов служит диагностикой (`communication.md §8`).

| # | Блок | Какой вопрос посетителя закрывает | Шаг канона | Разрыв |
|---|---|---|---|---|
| 0 | Вкладка/title | «Что это?» — поисковик, который сажает деревья | 1 One-liner | Видно только во вкладке и в выдаче Google, не на странице [вывод] |
| 1 | H1 «Private by design» + поиск | «Можно попробовать?» — да, сразу | 9 CTA (очень дешёвый) + проба Aha | Пропущены шаги 1–3: не сказано, что это и для кого. Обещание приватности тут же спорит с cookie-баннером [вывод] |
| 2 | Счётчики | «Это серьёзно?» — 258M деревьев, €106M | 4 (масштаб) / доказательство | На первом экране закрыты баннером; не связаны с действием посетителя [факт + вывод] |
| 3 | What we stand for | «Что за компания?» | 5 / 7 частично (приватность) | Работы и критерии пользователя не названы; четыре разные темы (климат, приватность, AI, энергия) делят внимание [вывод] |
| 4 | Финотчёт | «Не гринвошинг ли это?» | 7 Снятие страха | Хорошо. Но на главной одна цифра дохода, нет «куда ушло» [вывод] |
| 5 | Подход к посадке | «Деревья настоящие?» | 7 Снятие страха | Хорошо («Instead of monocultures»). Нет правила выживаемости через 3 года [вывод] |
| 6 | Цифры + «Discover all projects» | «Много ли нас?» | соцдоказательство | Ведёт в блог, а не к действию [вывод] |
| 7 | «Join 20 million people…» | «Что мне сделать?» | 8 State B + 9 CTA | **Кнопки нет.** Финальный призыв без действия [факт] |
| — | Нет блока | «А поиск не хуже Google?» | 6 Проблемы текущего решения / 7 страх | **Главный разрыв**: не найдено на лендинге [факт + вывод] |
| — | Нет блока | «Сколько даёт мой поиск?» | 4 Ценность в критериях | Не найдено [факт] |
| — | Нет блока | «Как сделать Ecosia поиском по умолчанию?» | 9 Первый шаг для привычки | Только как запасной вариант на странице после скачивания браузера («Unable to install? Set Ecosia as default search instead.») [факт] |
| — | Нет блока | «Чем плох Google?» | 5 компонент CA: «уволить» конкурента | Есть только в финотчёте: «Unlike much of Big Tech, we stay clear of tax evasion schemes» [факт] |

**Где рвётся цепочка** [вывод]: у главной два разных первых шага — «попробуй поиск сейчас» (сделан идеально) и «смени привычку» (не сделан). Первый даёт однократный запрос, но деньги Ecosia приходят только от регулярных поисков через неё (справка: «more searches through Ecosia means more ad-supported searches»). Значит, настоящая точка B лендинга — «Ecosia стала поиском по умолчанию», и до неё страница посетителя не доводит.

---

## 4. Пять компонентов Consideration Activators (знание, которое двигает выбор)

Канон (`consideration-activators.md §1`): 1 — знание нового графа работ (Job Graph) для Big Job; 2 — конкретная дельта ценности по критериям; 3 — названный продукт и первый шаг; 4 — снятые конкретные страхи о новом пути; 5 — конкурирующий путь «уволен», то есть показан конкретно худшим. 1–3 — минимум, 4–5 сильно поднимают конверсию.

| # | Компонент | Есть на лендинге? | Что именно |
|---|---|---|---|
| 1 | Новый способ выполнить Big Job | **Частично** [вывод] | Мысль «ищешь как обычно, а прибыль от рекламы идёт на деревья» на главной не сформулирована. Механика («we make money from ads») появляется только в карточке в выдаче, *после* первого поиска. На главной есть только итог («trees planted by Ecosia») |
| 2 | Дельта ценности по критериям | **Нет для пользователя** [вывод] | Цифры масштаба организации есть; «твой год поисков ≈ X деревьев» или хотя бы «в среднем активный пользователь…» не найдено на лендинге |
| 3 | Названный продукт + первый шаг | **Да для пробы, нет для привычки** [вывод] | Строка поиска — идеальный первый шаг. Поставить по умолчанию на главной не предлагается; браузер скачивается без объяснения; на мобильном CTA в шапке нет [факт] |
| 4 | Снятые страхи | **Частично** [вывод] | Гринвошинг: снят хорошо (отчёт, B Corp, нативные виды). «Поиск хуже»: не снят. «Слежка»: заявлен, но подорван баннером. «Мой вклад ничтожен»: не снят |
| 5 | «Уволить» конкурента | **Почти нет** [вывод] | Google, Chrome, «просто задонатить», углеродные офсеты на главной не названы. Сильные аргументы (налоги, не офсеты, AI не обучается на разговорах) разбросаны по отчёту и справке |

Вывод [вывод]: из минимальной тройки на главной полностью есть только компонент 3, и только для однократной пробы. По канону (`consideration-activators.md §1`) без 1 и 2 человек не двинется дальше пробы, и это совпадает с наблюдаемым разрывом между «попробовал» и «сменил по умолчанию». [гипотеза: нужна проверка конверсии «первый поиск → поиск по умолчанию»]

---

## 5. Семь допущений покупки

Канон (`communication.md §2`): покупка (здесь — смена поиска по умолчанию) происходит, только если вдоль цепочки выполняются семь допущений.

| # | Допущение | Статус на лендинге | Комментарий |
|---|---|---|---|
| 1 | Посетитель из целевого сегмента, у него есть нужный Big Job | **Не управляется** [вывод] | Первый экран зовёт S2 (приватность), тело страницы — S1 (климат). Трафик смешанный, отбора нет |
| 2 | Продукт создаёт ценность выше прогноза и текущего решения | **Не показано** [вывод] | Для Core Job (поиск) — нет сравнения с Google. Для Big Job (климат) — масштаб есть, личной ценности нет |
| 3 | Посетитель понимает ценность | **Слабо** [вывод] | Механика «реклама → прибыль → деревья» на главной не объяснена; видна только после поиска |
| 4 | Реальные условия цепочки выполнены | **Частично** [вывод] | Поиск работает без условий. Браузер: zip-установка на macOS; Chrome-расширение на главной не предлагается (только в блоге); корпоративные устройства с запретом менять поиск не обсуждаются [факт + гипотеза] |
| 5 | Конкретные страхи сняты | **Частично** [вывод] | см. §6.1 |
| 6 | Путь к ценности достаточно короткий | **Да для пробы** [факт + вывод] | Поиск без регистрации; счётчик «1» сразу. Для привычки: путь не показан |
| 7 | Цепочка не ломается по дороге | **Есть трещины** [факт] | Cookie-баннер закрывает счётчики и пол-экрана на мобильном; /about 404; «200M trees» в выдаче против 258M на главной; € на главной и $ в отчёте; CTA шапки сразу запускает скачивание без страницы о продукте |

---

## 6. Барьеры, страхи, ожидания и проба Aha

### 6.1 Барьеры (реальные факты, мешающие начать) и страхи (прогнозы)

Канон: барьер — объективный факт, его убирают изменением реальности; страх — прогноз поломки, его снимают коммуникацией, только если поломка неправда (`barrier-removal.md §1, §3, §4`).

**Барьеры** [вывод + гипотеза]
- **Смена поиска по умолчанию в браузере** — главный барьер. На лендинге нет пошаговой инструкции или кнопки «Set as default» для Chrome/Safari/Edge/мобильных. Сам Ecosia этот барьер решает браузером («Import settings», «60 seconds») — это механика «сменить входной путь» (`barrier-removal.md §6`), но предлагается она только тем, кто готов сменить весь браузер.
- **Корпоративные и школьные устройства**, где менять поиск или ставить браузер нельзя [гипотеза]. На лендинге не найдено.
- **Регионы, где Ecosia не монетизируется** [факт из справки: «While we are not yet able to monetize all markets…»]. Это реальный барьер для Big Job (поиск в таком регионе не финансирует посадки напрямую). Справка решает это усреднением; на лендинге не упомянуто.

**Страхи** (что посетитель прогнозирует) [гипотеза по сегменту; статус на лендинге — факт]

| Страх | На лендинге | Как можно снять честно |
|---|---|---|
| «Результаты будут хуже, чем в Google» | **Не найдено** | Факт есть: в выдаче источник Google (ссылка «Report result»), в футере «Transparency information (MStV)» про Bing/Google/EUSP. Сказать на главной, показать пример выдачи |
| «Это гринвошинг, деревья нарисованы» | **Хорошо снят**: отчёт, B Corp, «Instead of monocultures», проекты | Добавить правило из справки: «A tree counts as planted… once a second field monitoring, three years after planting, confirms it's alive.» Это самый сильный аргумент, и он не на лендинге |
| «Мои поиски ничего не меняют» | **Не найдено** | Честная формула оценки (есть в справке) коротко на главной |
| «Это ещё одна компания, которая следит» | **Заявлено и подорвано**: «Private by design» + баннер «Personalised advertising… Google, Marketing… 5 partners»; на /browser в тексте настроек cookies — Microsoft Clarity «captures how you interact with our website» [факт] | Объяснить, почему реклама и Google в баннере (это источник денег на деревья), и сделать дефолтом «Reject non-essential» визуально равнозначным |
| «Будет больше рекламы» | **Не найдено** | В справке: «The advertisements on Ecosia are clearly labeled as Ads and are text links». Можно показать |
| «Компанию купят, и всё изменится» | **В отчёте, не на главной**: «We don't pay out dividends and cannot be bought.» | Вынести на главную (steward-ownership) |

### 6.2 Управление ожиданиями

Канон: коммуникация задаёт прогноз, который продукт потом должен превзойти; завышенное обещание делает разочарование неизбежным (`communication.md §9`).

- **Риск завышения** [вывод]: title «the search engine that plants trees» и «Join 20 million people making a difference» подталкивают к ожиданию «каждый мой поиск = дерево / я увижу *свои* деревья». Реальность по справке: «not an exact, individualised count of "your own" trees», «Seeds do not follow the logic as "one seed = one tree"». Человек, который заведёт аккаунт ради «своих деревьев», рискует получить отрицательную ошибку прогноза (Problem, `behaviour-change.md §7`).
- **Риск занижения** [вывод]: о личной ценности на главной не сказано ничего, поэтому у части посетителей прогноз ценности слишком мал, чтобы менять привычку.
- **Позитив** [вывод]: Ecosia честна в деталях (определение «profit», правило 3 лет, «estimate»), просто эта честность спрятана в справке. Перенос одной строки на главную снял бы оба риска сразу.

### 6.3 Проба Aha на лендинге

Канон: момент Aha нужно ставить как можно левее в цепочке; каждый шаг до него — внимание «в долг» (`customers-attention-management.md §6`).

- **Проба поиска — лучшая в нашей выборке** [вывод]: Aha по Core Job («нашёл, что искал») доступен в первые секунды, без регистрации. Сам лендинг и есть продукт.
- **Aha по Big Job не срабатывает** [вывод]: после первого поиска счётчик показывает «1» и «Level 1 - Ecocurious», но что значит «1», не объяснено; карточка «How Ecosia works» рассказывает про 200M деревьев всех пользователей, не про вклад этого поиска. Канон: Aha — это превышение прогноза по критериям, с которыми человек пришёл (`job-structure.md §8`); критерий «вижу свой вклад» здесь не превышен, а размыт.

---

## 7. Силы за и против перехода, конкуренты

Канон: силы изменения поведения (`behaviour-change.md §9`); привычку почти нельзя ослабить, её нужно переиспользовать (`ajtbd-key-theses.md §20`); класс изменения определяется знакомостью Core Job (`behaviour-change.md §10`).

**Класс изменения** [вывод]: Core Job «искать в интернете» знакома всем, значит это класс 1: коммуникация должна вести с критериев Core Job («такие же результаты»), а главные страхи — про качество исполнения, а не про смысл категории. Лендинг Ecosia ведёт с Big Job и ценностей компании, а страх по качеству Core Job не трогает. Это несовпадение класса и коммуникации. [вывод]

**Силы «за»** [вывод]
- Идентичность: «я человек, который действует ради климата» — лендинг частично её задевает («making a difference every day», «climate active»).
- Любопытство: живой счётчик деревьев — хороший крючок.
- Знание более выгодного способа выполнить Big Job (компоненты 1–2) — слабое, см. §4.

**Силы «против»** [вывод]
- **Привычка к Google** — главная. Google — эталон «захвата через привязку к триггеру» («first place I go when I have a question», `customers-attention-management.md §10`). Ecosia не сможет её «победить», но может переиспользовать: стать тем же самым местом по тому же триггеру (поиск по умолчанию, адресная строка). Браузер с «Import settings» и «Ecosia search built in» — правильное переиспользование, но предложено слишком тяжёлым шагом (новый браузер вместо смены одной настройки).
- Страх ухудшения поиска (не снят).
- Неявная конкурирующая работа [гипотеза]: «не выглядеть наивным, который верит в "деревья за клики"» — снимается прозрачностью, которая у Ecosia есть, но не на виду.

**Конкуренты, которых лендинг должен «уволить»** (показать конкретно худшими по критериям Big Job, `consideration-activators.md §1`, компонент 5)

| Конкурент | Что сделать | Есть ли на лендинге |
|---|---|---|
| Google Search / Chrome (привычка) | «Те же результаты, но прибыль идёт на деревья, а не акционерам; мы платим налоги» | Нет (налоги — только в отчёте) [факт] |
| DuckDuckGo / Brave / Startpage (для S2) | «Приватно *и* финансирует посадки» | Нет [факт] |
| ChatGPT и другие AI (для S3) | «Small AI models», «never used to train» | Частично, блок «AI designed for you, not profit» [факт] |
| «Задонатить напрямую» / «купить офсеты» | «Без денег из кармана; не офсеты, а проверенные через 3 года деревья» | Нет (только справка) [факт] |
| «Ничего не делать» | Цена бездействия по критерию Big Job | Нет [факт] |

---

## 8. Итог

### 8.1 Топ-риски лендинга

1. **Уникальное отличие (деревья) ушло с первого экрана** в пользу приватности, где Ecosia одна из многих. [вывод]
2. **Нет моста от пробы к привычке**: строка поиска даёт один запрос, но «поставить по умолчанию» на главной не предлагается; финальный призыв без кнопки; на мобильном нет CTA. [факт + вывод]
3. **Главный страх класса 1 («поиск хуже Google») не снят**, хотя факт для снятия есть. [факт + вывод]
4. **Обещание приватности против cookie-баннера** с «Personalised advertising» и «Google» на первом экране. [факт + вывод]
5. **Нет ответа «что даёт мой поиск»**: ожидание «каждый поиск = дерево» остаётся неуправляемым, а справка его потом опровергает. [вывод]
6. **Мелкие поломки доверия**: 404 на /about, «200M» против 258M, € против $. [факт]

### 8.2 Точки роста: конкретные правки (формулировки — черновики; всё, что не подтверждено на сайте, помечено `[VERIFY]`)

1. **Вернуть однострочник в H1** (что это + работа + ценность):
   «Search like you always do. Our ad profits plant trees — 258 million so far.»
   или ближе к EmpCo-формулировкам самого Ecosia: «The search engine that funds tree planting with 100% of its profits.» «Private by design» оставить подзаголовком.
2. **Одна строка под поиском против главного страха**: «Results powered by Google and Bing [VERIFY — какие провайдеры по регионам, см. MStV]. Same answers, different purpose.»
3. **Блок «How it works» на главной в 3 шага** (сейчас есть только в выдаче): «You search → we earn from ads, like any search engine → 100% of profits go to climate action. We publish every euro monthly.»
4. **Честная личная формула** (снимает и завышение, и занижение): «An average active user helps fund about X trees a year [VERIFY — посчитать по методике из справки, обновление августа 2026]. It's an estimate — here's how we calculate it.»
5. **Главный CTA после блока доверия и в финале**: «Make Ecosia your default search — takes 30 seconds [VERIFY]» с определением браузера и пошаговой подсказкой; «Download Ecosia Browser» оставить вторым вариантом. Под «Join 20 million people…» поставить кнопку.
6. **Мобильный CTA**: на телефоне показывать «Get the app» / «Add to Safari as default» в шапке, а не только в футере.
7. **Вынести на главную два лучших аргумента из справки и отчёта**: «A tree only counts once it's still alive 3 years after planting.» и «We can't be sold and don't pay dividends.»
8. **«Уволить» Google одной фразой с фактом из отчёта**: «Unlike much of Big Tech, we pay our taxes — €… last month [VERIFY — из текущего отчёта].»
9. **Объяснить баннер**: рядом с cookie-баннером одна строка «Ads are how we fund trees. We never sell your data [VERIFY — сверить с privacy policy].»
10. **Поправить поломки**: /about → редирект на страницу о компании; актуальное число в карточке «How Ecosia works»; одна валюта на главной и в отчёте.
11. **Объяснить личный счётчик при первом появлении**: «1 search today. Searches like yours funded 3,459,287 trees last month.» (число — из отчёта, обновлять ежемесячно).

### 8.3 Рискованные допущения лендинга (RAT) и как их проверить дёшево

| # | Допущение | Насколько смертельно, если неверно | Дешёвая проверка |
|---|---|---|---|
| 1 | Деревья, а не приватность, — главный мотив новых пользователей | высоко: выбор H1 и сегмента | A/B первого экрана «деревья» против «приватности» по метрике «поиск по умолчанию через 7 дней» |
| 2 | Главный барьер к привычке — страх «поиск хуже», а не сложность смены настройки | высоко | Опрос ушедших после 1–3 поисков: «Что помешало оставить Ecosia?» (вопрос из `barrier-removal.md §7`); A/B строки «Results powered by…» |
| 3 | Честная личная формула повышает, а не снижает конверсию | среднее | A/B блока с оценкой «X деревьев в год» против без него |
| 4 | Финотчёт в 1 клик действительно снимает страх гринвошинга у новичков | среднее | Клик-карта: сколько новичков открывают отчёт; интервью «Что убедило / что смутило?» |
| 5 | Браузер — лучший путь к привычке, чем инструкция по смене поиска | высоко для экономики | A/B главного CTA «Make default» против «Download Browser» по удержанию на 30 день |
| 6 | Cookie-баннер с «Personalised advertising» не подрывает обещание приватности | среднее | Интервью с S2 на первом экране; доля «Reject non-essential» |

### 8.4 Что из этого взять нашему charity / passive-earning продукту

1. **Проба результата прямо на первом экране, без регистрации.** У Ecosia лендинг и есть продукт. Нам нужна похожая «строка поиска»: действие, которое даёт первый результат за секунды (например, симуляция «сколько даст мой день» или первый реальный вклад без аккаунта). [вывод]
2. **Прозрачность как у Ecosia, но на главной.** Ежемесячный отчёт до цента, налоги, реклама, выплаты по получателям — лучший снятый страх «куда идут деньги» из всей выборки. Мы должны показывать не одну цифру, а разбивку прямо на лендинге. [вывод]
3. **Отвечать на «что даёт именно моё действие» честной формулой.** Ошибка Ecosia в том, что честный ответ («это оценка по среднему пользователю») спрятан в справке, а лендинг подталкивает к ожиданию «каждый поиск = дерево». Нам нужна видимая формула вклада с оговоркой рядом. [вывод]
4. **Правило подсчёта, которое снимает гринвошинг**: у Ecosia это «дерево засчитано, только если живо через 3 года». Нам нужен такой же проверяемый критерий «засчитано, когда…» для нашего результата. [вывод]
5. **Мост от пробы к привычке — отдельный главный CTA.** Пассивная модель зарабатывает на регулярности, а не на первом действии; лендинг должен вести именно к «поставил по умолчанию / включил в фоне», с объяснением в 1–3 шага и кнопкой в финале. [вывод]
6. **Не прятать уникальное отличие ради модной темы.** Приватность, AI — «гигиена»; держать в H1 то, чего нет у конкурентов. [вывод]
7. **Учесть регулирование заранее** [гипотеза]: если мы работаем в ЕС, директива EmpCo ограничивает экологические заявления. Формулировки вроде «funds», «estimate», «dedicated to» и ссылка на методику подсчёта нужны с первого дня.

---

## Источники (сняты 2026-11-22, Playwright/Chromium, регион поиска Bulgaria)

- https://www.ecosia.org/ (главная, десктоп 1200×659 и мобильный 390×844)
- https://www.ecosia.org/browser
- https://www.ecosia.org/browser/confirmation (при открытии автоматически начинается скачивание `EcosiaInstaller.zip`; файл удалён)
- https://www.ecosia.org/search?q=best+running+shoes (страница выдачи, карточка «How Ecosia works», личный счётчик)
- https://ecosia.co/finreportsen → https://blog.ecosia.org/ecosia-financial-reports-tree-planting-receipts/ (отчёт за October 2026)
- https://blog.ecosia.org/tag/where-does-ecosia-plant-trees/
- https://www.ecosia.org/about (404)
- https://support.ecosia.org/article/1217-eu2024-825
- https://support.ecosia.org/article/844-seed-counter
- https://support.ecosia.org/search?query=how+many+searches+tree (поиск по справке; статьи о числе запросов на дерево не найдено)
- https://www.bcorporation.net/find-a-b-corp/company/ecosia-gmbh/ (ссылка из футера, не открывалась)
- Скриншоты: `/Users/alexgaidukov/Projects/Charity/.playwright-mcp/ecosia-home-first-screen.png`, `ecosia-home-mobile.png`, `ecosia-browser-confirmation.png`
- Канон: `Next-Move-Theory-Canon/Advanced-Jobs-To-Be-Done/` — communication.md (§2, §3, §4, §5, §8, §9), consideration-activators.md (§1, §4, §10), barrier-removal.md (§1, §3, §4, §6, §7), customers-attention-management.md (§2, §6, §10, §11), job-structure.md (§8, §9), segmentation.md (§7, §9), behaviour-change.md (§7, §9, §10), ajtbd-key-theses.md (§9, §20, §24); `.claude/skills/nmt-craft-go-to-market/` (SKILL.md, references/glossary.md); `.claude/skills/nmt-diagnose/SKILL.md`.
