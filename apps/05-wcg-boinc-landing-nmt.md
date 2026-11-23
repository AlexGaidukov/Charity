# World Community Grid (worldcommunitygrid.org) + BOINC (boinc.berkeley.edu): разбор лендингов по Next Move Theory

Дата снятия: 2026-11-22. Главный фокус: лендинг World Community Grid (WCG) https://www.worldcommunitygrid.org/ и его подстраницы. BOINC https://boinc.berkeley.edu/ разобран короче, как платформа, на которой WCG работает (полный список источников в конце).
Статусы утверждений: **[факт]** — факт с сайта: дословно или напрямую видно; **[вывод]** — выведено из фактов и канона; **[гипотеза]** — моё предположение, нужна проверка.
Методология: Next Move Theory / Advanced JTBD (канон в `Next-Move-Theory-Canon/`). Термины методологии даны в скобках при первом упоминании.

---

## Резюме на один экран

1. **Из всех разобранных лендингов у WCG лучший блок про страхи.** На главной четыре коротких ответа: «It won't slow you down», «It won't drain your battery», «It's safe and secure», «It won't waste your data plan». Каждый ответ держится на конкретном механизме («only runs when you're connected to power», «only… when you're connected to a wireless network»). У Charity Engine такие ответы спрятаны в вики, у WCG они стоят перед финальной кнопкой. [факт + вывод]
2. **Первый экран тратится на юбилей, а не на объяснение.** Заголовок «Celebrating 20 years of World Community Grid» (проект начался в 2004-м, то есть юбилей был в 2024-м, а сейчас конец 2026-го), подзаголовок «Enabling seemingly impossible scientific research to come to life», кнопка «Learn more». Что это и что от меня нужно, сказано только в третьем блоке. Лучшая формулировка вообще лежит в meta description, которую посетитель не видит. [факт + вывод]
3. **Видно, что делает сеть. Не видно, что сделаю я.** «822k volunteers», «7.7M devices», «2.7M years of computing». Сколько даёт один компьютер, на лендинге не сказано, хотя в справке есть готовая единица: «An average computer… returns about 2 results per day». Вклад человека невидим, ровно как у Charity Engine. [факт + вывод]
4. **Доказательства результата расплывчатые и старые.** «Identified new drugs in the fight against neuroblastoma», «Discovered… clean water», «…solar power» без дат и цифр. Свежие новости выходят примерно раз в полгода (июль 2025, октябрь 2025, июнь 2026). На странице About по-прежнему написано «in less than a decade», на странице Donations «Across 18 years… Over the past year, the WCG has been transferred». Проект выглядит менее живым, чем он есть. [факт + вывод]
5. **Кнопка «Join» ведёт в регистрацию, а не к загрузке. Ссылка «Download» для гостя открывает страницу входа.** Путь такой: аккаунт (email, пароль, EULA) → выбор проектов → установка BOINC. Список платформ на главной не назван. Форма лёгкая (2 поля против 8 действий у Charity Engine), но до первого результата всё равно далеко. [факт]
6. **Из привлечённых когда-то людей остался примерно каждый девятый.** На странице статистики 822 820 участников за всё время, а в блоке «Current members by region» в сумме около 93 тыс. Скорее всего, лендинг привлекает, а продукт не даёт поводов остаться: вклад не виден, новости редкие. [факт + гипотеза]
7. **BOINC: страница для энтузиастов, а не для новичка.** Хороший короткий one-liner («Compute for Science… runs them invisibly in the background. It's easy and safe»), доверие через UC Berkeley и NSF, загрузка без регистрации. Но дальше главная занята сырыми новостями проектов (латинские квадраты, «CPU app requires 3.5 GB RAM»), а выбор проекта перекладывается на пользователя. [факт + вывод]

**Что взять себе (charity / passive-earning):** блок страхов как у WCG (каждый страх закрыт механизмом, а не прилагательным); на первом экране one-liner вместо юбилея; личный вклад в понятных единицах («твой ноутбук = ~2 задачи в день = N часов для исследования рака»); регулярный поток маленьких результатов, чтобы человек не забывал о продукте; загрузка до регистрации, как у BOINC; следить, чтобы даты на сайте не выглядели заброшенными.

---

## 0. Что было на лендингах (снятие 2026-11-22)

Способ: WCG — одностраничное React-приложение (статический HTML пустой: «You need to enable JavaScript…»), поэтому снимался через Playwright: извлечение текста + полный скриншот `/.playwright-mcp/wcg-home-2026-11-22.png`. Справка WCG (`/help/topic.s?...`) и все страницы BOINC отдаются сервером и снимались curl. Cookie-баннера на WCG не было. [факт]

### 0.1 WCG, главная https://www.worldcommunitygrid.org/ (блоки по порядку)

`<title>`: «Home | World Community Grid». Meta description: «World Community Grid enables anyone with a computer or Android device to donate their unused computing power to advance cutting-edge scientific research on topics related to health and sustainability.» [факт]

| # | Блок | Дословный текст | CTA |
|---|---|---|---|
| — | Шапка | меню «Research» · «About» · «News» · «Community» · «My contribution» · «Links»; справа «Download» · «Donations» · «Join» · «Log in» | «Join» (→ /join) |
| 1 | Hero | H: **«Celebrating 20 years of World Community Grid»** · «Enabling seemingly impossible scientific research to come to life». Иллюстрация: учёная с пипеткой и спираль ДНК | «Learn more» |
| 2 | Updates | «Discover the latest from World Community Grid» · три карточки: «2026-06-23 Research Update from the MCM Team (June 2026) — SLC5A1 (solute carrier family 5 member 1) top-scoring gene in predictive MCM1 signatures…» · «2025-10-28 … (October 2025) — PDE8B, a gene that is involved in hormone synthesis…» · «2025-07-08 Research Update from the ARP Team (July 2025) — …back up and running since Fall 2024.» | «Show all news →» |
| 3 | How it works | H2 **«Donate your device's spare computing power to help scientists solve the world's biggest problems.»** · «Scientists need your help — They're searching for answers to the world's biggest problems, but it's hard to know where to start. That's why many use computer simulations to point them in the right direction.» · «Your device makes a difference — As a World Community Grid volunteer, your device does research calculations when it has spare power. With your help, scientists can identify the most important results to study in the lab, bringing them one step closer to discoveries that save lives and address global problems.» | «Learn more →» |
| 4 | You can help researchers | вкладки «Help scientists provide more accurate rainfall forecasts for farmers in sub-Saharan Africa.» / «Help search for molecular markers that could lead to improved cancer detection and treatment.» · H3 «Crucial data, better crops.» · «95% of agriculture in Africa depends on rainfall. This project uses massive computing power, data from The Weather Company, and other data to provide more accurate rainfall forecasts, which will help farmers more successfully raise crops.» · H3 «Help improve the odds for cancer patients» · «Mapping Cancer Markers is analyzing millions of data points…» | «Join» в каждой вкладке · «See all projects →» |
| 5 | Results | «With your help, World Community Grid researchers have…» · «Identified new drugs in the fight against neuroblastoma - a childhood cancer.» · «Discovered how nanotechnology could help provide clean water to millions.» · «Discovered new compounds for harnessing solar power.» (ссылки на старые статьи `viewNewsArticle.do?articleId=342/436/450`, дат на карточках нет) | → статьи |
| 6 | By the numbers | «822k — Volunteers have donated their spare computing power towards research initiatives.» · «7.7M — Computers and Android devices have contributed…» · «2.7M — Years of computing power has been contributed to date.» | «See the data →» |
| 7 | Features | «It won't slow you down — Our software monitors your device's performance, so whatever you are doing on your device, it stays out of the way.» · «It won't drain your battery — By default, World Community Grid only runs when you're connected to power.» · «It's safe and secure — Your personal information will never be shared. The software cannot access your personal files. Security experts constantly test the system for vulnerabilities to the latest threats.» · «It won't waste your data plan — …only downloads research tasks and uploads results when you're connected to a wireless network.» | — |
| 8 | Researchers say… | «Without World Community Grid, we wouldn't have even contemplated this project.» — Rob Knight, PhD, …Co-Principal Investigator, Microbiome Immunity Project | — |
| 9 | Looks who's talking | логотипы CTV News Toronto, Fast Company, Forbes (без цитат и дат) | — |
| 10 | Финальный CTA | **«Your spare computing power makes a difference»** · «Join now and start helping today.» Фото улыбающейся девушки | «Join» |
| — | Футер | логотипы Krembil и Jurisica Lab · «World Community Grid is powered by BOINC» · Privacy statement · Terms of use | — |

**Не найдено на главной WCG** [факт]: список платформ (Windows / Mac / Linux / Android / Raspberry Pi назван только на /about/how.s; iOS нет нигде); вклад одного устройства; что будет после нажатия «Join» (шаги); кто управляет проектом сейчас (только логотипы Krembil и Jurisica Lab в футере без подписи); электричество; нагрев и шум; судьба результатов (open data); живой счётчик «сейчас»; истории волонтёров; новый проект Mapping Arthritis Markers («Just Launched» на странице проектов) — на главной его нет.

### 0.2 WCG, путь к установке

- **/join → /join/signup**: шаги «Create account» → «Select projects» → «Install software»; H «Create Account»; поля «Email address», «Password», чекбокс «Accept end user license agreement»; кнопка «Sign Up». [факт]
- **/download** без входа перенаправляет на **/login**. [факт]
- Справка «Registration»: «Register… Select which of our research projects you wish to contribute to… If you do not already have BOINC installed, download and install the software». Кто уже пользуется BOINC, может подключиться по URL. [факт]
- Шаги 2–3 без регистрации не видны и не снимались. [факт]

### 0.3 WCG, подстраницы (то, что нужно для решения, лежит на втором-третьем клике)

- **/about/how.s (How it works)**: «World Community Grid enables anyone with a computer, Android or Raspberry Pi device to support scientific research on health and sustainability.» · YouTube-видео «How WCG Works» · FAQ из трёх вопросов («How do I sign up…?», «What are the recommended minimum system specifications?», «What is BOINC?»). Ответы в тексте страницы не раскрыты, ссылки ведут на эту же страницу (возможно, это аккордеон; кликом не проверялось). [факт]
- **/research/projects.s**: «Active research (3)»: Mapping Arthritis Markers («Just Launched»), Africa Rainfall Project («In Progress»), Mapping Cancer Markers («In Progress»). [факт]
- **/about/security.s**: хостинг в «SHARCNET facility at University of Waterloo»; «source code is tested and reviewed by security experts»; «research applications are cryptographically signed… The software client… will reject and delete any research application that cannot be verified»; шифрование на всех участках; «Our software is not capable of accessing any volunteer files». [факт]
- **/about/about.s**: «supported 31 research projects to date», «published over 35 peer-reviewed papers», «millions of CPU-years of computation in less than a decade», «the biggest volunteer computing initiative devoted to humanitarian science»; история: с 2004 года программа IBM, «In 2021, IBM transferred the World Community Grid assets to Krembil Research Institute, part of the University Health Network (UHN)». Награды Computerworld, BITC, Asian CSR. [факт]
- **/donations**: «The WCG was funded and run by IBM… until February 2022» · «As an academic group, we face a significant financial challenge» · «Across 18 years of life, over 800,000 volunteers…» · «we still need funding for software development and maintaining the infrastructure» · «Click here to donate directly… via UHN Foundation». [факт]
- **/stat/viewGlobal.do** (обновлено «11/22/26 12:06:02 UTC»): Members 822,820 · Devices 7,756,054 · Total run time 2,755,863 years · Results returned 8,006,298,622 · «Run time per calendar day» в среднем 340 лет, «Yesterday» 259 лет · «Current members by region» в сумме 93 293 (28 193 + 20 763 + 8 951 + 487 + 187 + 375 + 2 138 + 1 834 + 30 365). Активных проектов 3, завершённых 28. [факт; сумма — мой подсчёт]
- **Справка, Costs**: «you may see a slight increase in your electricity costs… In most cases, the impact will be the equivalent of an additional low wattage light bulb»; по умолчанию 60% процессора. [факт]
- **Справка, CPU Usage**: «we changed the default setting to only run at 60% of the unused processor time»; есть раздел «Could running the software cause my computer to overheat?». [факт]
- **Справка, System Requirements**: у каждого проекта свои требования (Africa Rainfall Project — 1 GB памяти, 1.5 GB диска, без Android; Mapping Cancer Markers — 400 MB / 500 MB, есть Android); «An average computer contributing to World Community Grid returns about 2 results per day»; Africa Rainfall — 100 MB на загрузку и 60 MB на отправку за одну задачу. [факт]
- **Справка, Android**: «only active when your device is plugged into a power source… and your battery is charged 90% or more»; «only transfers data… when your device is connected to a WiFi network»; «Android 4.1 and higher» (в таблице требований — 4.4); «900 million as of May 2013». [факт]
- **Справка, Installing the Software**: «The software itself will take less than 50 MB»; совет про Internet Explorer; инструкция по массовой установке на много машин. [факт]
- **Справка, Points**: очки и статистика обновляются «twice a day… 00:00 and 12:00 UTC»; очки начисляются после проверки (validation). [факт]

### 0.4 BOINC, главная https://boinc.berkeley.edu/ (блоки по порядку)

| # | Блок | Дословный текст | CTA |
|---|---|---|---|
| 1 | Hero | H **«Compute for Science»** · «BOINC lets you help cutting-edge science research using your computer. The BOINC app, running on your computer, downloads scientific computing jobs and runs them invisibly in the background. It's easy and safe.» · «About 30 science projects use BOINC. They investigate diseases, study climate change, discover pulsars, and do many other types of scientific research.» · «The BOINC and Science United projects are located at the University of California, Berkeley and are supported by the National Science Foundation.» + печати UC Berkeley и NSF | — |
| 2 | START COMPUTING! | «To contribute to science areas (biomedicine, physics, astronomy, and so on) use Science United. Your computer will help current and future projects in the areas you choose.» · «Or download BOINC and choose specific projects. This will let you participate in competitions and systems like Gridcoin.» | «Join Science United» · «Download BOINC» |
| 3 | Правая колонка | «Learn / Communicate / Help» (Science projects, publications, User manual, Message boards, Translate, Test, Publicize) · «Computing power · Certificate · Poll · Teams» · «Scientists: Create and maintain a BOINC project. Run Docker and Autodock jobs with BOINC Central.» · «Programmers: Visit the BOINC github repo» | ссылки |
| 4 | News from BOINC Projects | сырые новости проектов: RakeSearch (матрица латинского квадрата 12×12, «25104 diagonal transversals»), Amicable Numbers («CPU app requires 3.5 GB RAM… No Android support»), Gerasim@Home | «View article» |
| 5 | News | «New space and astronomy projects» (15 Nov 2026) · «Server outage — The server that hosts the BOINC web site, Science United, and BOINC Central, was offline from 3 Sept until today…» (10 Sep 2026) · «BOINC Dashboard available for Linux» | «Discuss» |

- **/download.php**: «BOINC is a program that lets you donate your idle computer time to science projects like Climateprediction.net, Rosetta@home, GPUGrid…» · таблица версий: Windows 64-bit 8.2.11 (16.99 MB), Mac 8.2.11, Android 8.2.11 и старые версии · «When you first run BOINC, you will be asked to choose a project.» · загрузка **без регистрации**. [факт]
- **/projects.php**: «Choosing BOINC projects» — критерии выбора («Does the project clearly describe its goals?… Has the project published results in peer-reviewed journals?… Do you trust the project to use proper security practices?… Who owns the results…?») и таблица из 28 проектов, в том числе World Community Grid. [факт]
- **scienceunited.org**: «Do science research on your computer, tablet, or phone» · «BOINC is secure and will not affect your normal use of the computer» · «non-profit». Форма **/su_join.php**: screen name, email, password, «Science areas you most want to support» (7 областей), «Use of your computer: Low power / Standard / Maximum computing». [факт]

---

## 1. Для кого лендинг WCG и какие работы он предполагает

Уровни работ по канону (`job-structure.md §9`, glossary): **Big Job** — результат уровнем выше, в нём живёт мотивация; **Core Job** — максимальная работа, которую продукт выполняет целиком; **Small Jobs** — работы того же уровня, которые продукт не делает; **Micro Jobs** — шаги под Core Job. У каждой работы есть точка A, точка B и критерии успеха с направлением и уровнем (`job-structure.md §8`).

### 1.1 Сегменты и работы (гипотезы по тексту лендинга и сайта)

**S1. «Хочу реально помочь борьбе с болезнями и бедностью, не тратя денег»** — на него написана главная [вывод]
- **Big Job** [гипотеза]: «хочу чувствовать, что вношу реальный вклад в борьбу с раком и глобальными проблемами, без денег и усилий», а на уровне идентичности — «быть человеком, который помогает науке».
- **Core Job WCG** [вывод]: «хочу отдавать простаивающие вычисления своего устройства исследованиям здоровья и устойчивого развития» («Donate your device's spare computing power…»).
- **Точка A** [гипотеза]: компьютер или телефон часто простаивает; хочется помогать, но жертвовать деньги не хочется или нечего; подозрение к незнакомым программам.
- **Точка B** [гипотеза]: программа тихо работает, устройство не тормозит и не разряжается, я понимаю, какому исследованию и чем помог, и регулярно вижу, что из этого вышло.
- **Критерии успеха** [гипотеза; ✔ — закрыто на главной]:
  - ✔ не мешает работе («stays out of the way»);
  - ✔ не сажает батарею (работает только от сети);
  - ✔ не тратит мобильный трафик (только Wi-Fi);
  - ✔ безопасно (нет доступа к файлам);
  - ✔ помогаю реальным исследованиям с понятной пользой (рак, урожай в Африке);
  - ✘ **вижу свой вклад** («мой компьютер сделал X»): на главной не найдено;
  - ✘ **вижу результат** (что открыли с моей помощью, недавно): только расплывчато и без дат;
  - ✘ не стоит мне денег (электричество): только в справке («low wattage light bulb»).
- **Small Jobs** [вывод]: выбрать, какому исследованию помогать (в регистрации есть выбор проектов, на лендинге его не видно); рассказать друзьям («Spread the word» в меню); пожертвовать деньги («Donations» в шапке — WCG сам выполняет эту работу).
- **Micro Jobs** [факт]: Join → email + пароль + EULA → выбрать проекты → скачать и установить BOINC → первая задача → очки после проверки (обновление дважды в сутки).

**S2. «Кранчер»: энтузиаст распределённых вычислений** — на него работает меню и вся статистика [вывод]
- **Big Job** [гипотеза]: «хочу вкладывать мощность своего железа в науку и видеть свой вклад в цифрах, командах и рейтингах».
- **Core Job** [вывод]: «хочу запускать задачи WCG в BOINC и копить очки и бейджи». На лендинге этого нет, но в меню есть «Teams», «Members», «Milestones», «Beta testing», «Results».
- **Критерии** [гипотеза]: стабильный поток задач; честные очки; поддержка GPU, Linux, ARM; командные соревнования.
- На главной S2 ничего не обещается, но, судя по статистике, именно он держит текущий объём [гипотеза].

**S3. Организации** (массовая установка на много машин, «Become a Partner», наследие IBM CSR) [факт: инструкция по mass install и ссылка в футере]. Отдельной коммуникации на лендинге нет.

**Другая сторона платформы — учёные** («Submit a proposal») и **доноры** («Donations»). Обе стороны висят в той же навигации и спорят с CTA «Join» за внимание волонтёра. [факт + вывод]

### 1.2 Кого лендинг обслуживает на самом деле и кого должен

- **Обслуживает**: S1, и для S1 он заметно сильнее Charity Engine: конкретные получатели пользы (фермеры Африки, онкобольные), ответы на страхи, мнение учёного. [вывод]
- **Для S1 это незнакомая Core Job**: обычный человек раньше не отдавал вычисления своего компьютера науке. По канону это второй класс изменения поведения (`behaviour-change.md §10`): вести через Big Job, до первого контакта загрузить все пять компонентов Consideration Activators (`customers-attention-management.md §4`), а главный страх — о разумности самого действия. Блок Features закрывает его лучше всего на странице. [вывод]
- **Для S2 Core Job знакома** (первый класс): ему нужна разница с другими проектами BOINC. На лендинге этого нет. Его вход — статистика и форумы. [вывод]
- **Должен** [гипотеза]: оставить S1 целью главной, но поднять на первый экран то, что сейчас лежит в третьем блоке, и добавить личный вклад. Донаты и предложения учёных убрать из шапки ниже или в футер (`segmentation.md §9`: фокус — это вычитание).
- **Признак сегмента для квалификации** (`segmentation.md §7–8`) [гипотеза]: «устройство много часов включено в сеть». Именно от этого зависит вклад, а значит, и ценность. Есть и обратный признак: у владельца только iPhone продукт вообще недоступен, а на странице About написано «smartphone or tablet».

---

## 2. One-liner и базовые сообщения

### 2.1 One-liner

Формула канона (`communication.md §5`): **[что это] + [Core Jobs] + [ценность по критериям]**.

| Где | Текст | Что это | Core Job | Ценность в критериях |
|---|---|---|---|---|
| Hero | «Celebrating 20 years… Enabling seemingly impossible scientific research to come to life» | ✘ | ✘ | ✘ (юбилей + прилагательное) [факт + вывод] |
| Блок 3 | «Donate your device's spare computing power to help scientists solve the world's biggest problems.» | косвенно | ✔ | ✘ («world's biggest problems») [вывод] |
| Meta description | «…enables anyone with a computer or Android device to donate their unused computing power to advance cutting-edge scientific research on topics related to health and sustainability.» | ✔ (для кого и на чём) | ✔ | частично: направление (здоровье, устойчивость), уровня нет [вывод] |
| BOINC hero | «Compute for Science… downloads scientific computing jobs and runs them invisibly in the background. It's easy and safe.» | ✔ | ✔ | частично: «invisibly in the background» близко к критерию, «easy and safe» — прилагательные [вывод] |

Тест канона «повторить, что это, что делает, какую ценность даёт» [вывод]: после первого экрана WCG посетитель повторит «какой-то научный проект, которому 20 лет». Ответ «программа, которая отдаёт простой моего компьютера исследованиям рака» появится только после прокрутки до блока 3. У BOINC one-liner проходит тест лучше, хотя ценности в критериях нет и там.

### 2.2 Ценность: критерии или прилагательные?

Канон: ценность выражается в критериях с направлением и уровнем (`communication.md §3`, `job-structure.md §8`).

| Формулировка | Тип | Статус |
|---|---|---|
| «seemingly impossible scientific research», «world's biggest problems», «cutting-edge» | прилагательные | [факт] |
| «95% of agriculture in Africa depends on rainfall… more accurate rainfall forecasts» | контекст с числом, но эффект без уровня (насколько точнее?) | [факт + вывод] |
| «Help improve the odds for cancer patients», «could lead to improved cancer detection» | направление без уровня; честно, без обещания лекарства | [факт + вывод] |
| «822k», «7.7M», «2.7M years» | уровень есть, но про сеть, а не про меня | [факт] |
| «only runs when you're connected to power», «only… on a wireless network» | **настоящие критерии**: условие названо, проверить легко | [факт] |
| «stays out of the way», «safe and secure» | направление; механизм назван («monitors your device's performance», «cannot access your personal files»), уровня нет | [факт] |
| Справка: «about 2 results per day», «60% of the unused processor time», «low wattage light bulb» | **критерии уровня, но спрятаны в справке** | [факт] |

Вывод: самые сильные критерии WCG касаются цены участия (батарея, трафик, процессор, электричество), и часть из них на главной. Критериев выигрыша, то есть что даёт мой вклад и что уже получилось, на главной нет. По канону ценность — это отношение результата к затратам (`ajtbd-key-theses.md §6`): затраты WCG показал хорошо, а результат человек видит только в масштабе всей сети. [вывод]

### 2.3 Фичи как доказательство или как сообщение?

Канон: фича — это доказательство, привязанное к работе и критерию, а не сообщение само по себе (`communication.md §4`).
- Блок, который на сайте называется «Features», на деле — ответы на страхи с фичей-механизмом внутри («monitors your device's performance», «only runs when… connected to power»). Это ровно то, что канон называет фичей как доказательством. Лучший блок страницы. [факт + вывод]
- Подпись криптографией, хостинг в SHARCNET, проверка кода экспертами (/about/security.s) — сильное доказательство для «It's safe and secure», но с главной до него ведёт только меню. Одна фраза «Every research app is cryptographically signed; your device rejects anything else» усилила бы блок. [факт + вывод]
- Выбор проектов при регистрации — фича, которая выполняет работу «помогать тому, что важно мне». На лендинге она не упомянута. [факт + вывод]

---

## 3. Лендинг WCG как короткая цепочка шагов: блок за блоком

Канон: лендинг — короткая цепочка шагов посетителя (Critical Chain of Jobs), конечное состояние которой — достаточно веры и мотивации для первого шага. Канонический порядок из 9 блоков и диагностика разрыва — `communication.md §8`.

| Блок | Вопрос посетителя | Канонический блок | Закрыт? |
|---|---|---|---|
| 1 Hero | «Что это и что мне делать?» | 1. One-liner | **Разрыв №1.** Юбилей вместо one-liner; CTA «Learn more», а не первый шаг [факт + вывод] |
| 2 Updates | «Это живое?» | — (до one-liner) | Отвечает на вопрос «живое ли», но слишком рано и языком учёных («SLC5A1… MCM1 signatures»). Последняя новость пятимесячной давности [факт + вывод] |
| 3 How it works | «Как это работает? Это про меня?» | 2–3, 5. Focus Jobs, контекст, механизм | Да: «your device does research calculations when it has spare power». Триггера («почему сейчас») нет [вывод] |
| 4 You can help | «Кому конкретно я помогу?» | 2 / 8. Big Job, State B | Хорошо: конкретные получатели и CTA «Join» в контексте [вывод] |
| 5 Results | «Это вообще работает?» | 4. Ценность / доказательство | Частично: три результата без дат и цифр, и на странице не видно, свежие ли они [факт + вывод] |
| 6 By the numbers | «Много ли людей так делает?» | соцдоказательство | Да для масштаба сети. Нет для «что даст мой компьютер» — **разрыв №2** [вывод] |
| — | «Чем плохо то, что я делаю сейчас?» | 6. Проблемы текущего способа | **Разрыв №3.** Нет [факт] |
| 7 Features | «Чем я рискую?» | 7. Снятие страхов | **Да, сильно**: четыре страха закрыты механизмами. Не хватает электричества, нагрева и вопроса «кто за этим стоит» [факт + вывод] |
| 8 Researchers say | «Учёным это правда нужно?» | доказательство | Да, но цитата про завершённый проект [факт] |
| 9 Press logos | «Это известная штука?» | соцдоказательство | Слабо: логотипы без цитат и дат [факт + вывод] |
| 10 Final CTA | «Действую» | 8–9. State B + CTA | Повторный CTA есть (лучше, чем у Charity Engine). Но «Join» ведёт в регистрацию, шаги и платформы не названы [факт + вывод] |

**Где рвётся цепочка** [вывод]. По диагностике канона: (1) нет one-liner на первом экране, и посетитель, который не стал прокручивать, уходит, не узнав, что это; (2) ценность для себя не конкретна; (3) текущий способ не «уволен»; (4) первый шаг дороже, чем выглядит: аккаунт → выбор проектов → установка, и «Download» без входа закрыт. Страхи как раз закрыты — это лучшее место страницы.

---

## 4. Пять компонентов Consideration Activators (знание, которое двигает выбор)

Канон (`consideration-activators.md §1`): компоненты 1–3 обязательны для активации, 4–5 сильно поднимают конверсию; для незнакомой категории нужны все пять (`customers-attention-management.md §4`).

| # | Компонент | WCG: что есть | WCG: чего нет | BOINC |
|---|---|---|---|---|
| 1 | Новый способ выполнить Big Job | «Donate your device's spare computing power to help scientists…» + конкретные проекты | Не на первом экране | «help cutting-edge science research using your computer» — сразу в hero [факт] |
| 2 | Разница в ценности по критериям | Масштаб сети, три результата | Вклад одного устройства; свежий результат с цифрой; сравнение с «пожертвовать $10» | Нет [факт + вывод] |
| 3 | Названный продукт + первый шаг | «World Community Grid» + «Join» (дважды) | Платформы; шаги после Join; загрузка без аккаунта | «Join Science United» / «Download BOINC» (без регистрации); платформы на /download.php [факт] |
| 4 | Снятие конкретных страхов | **Блок Features: тормоза, батарея, безопасность, трафик** | Электричество; нагрев и шум; «кто управляет после IBM»; результаты открыты? | «It's easy and safe» — прилагательные; доверие через UC Berkeley и NSF [факт + вывод] |
| 5 | «Увольнение» текущего способа | — | Почему не просто жертвовать, не ставить другой проект BOINC, не оставить компьютер простаивать | Нет; наоборот, BOINC предлагает выбирать среди 28 проектов [факт] |

Конкретные истории (самый плотный формат, `consideration-activators.md §6`): на главной есть только цитата учёного. Материал для истории волонтёра на сайте есть: статистика, команды, «Milestones». Историю «вот что сделал мой ноутбук за год» найти не удалось. [факт + вывод]

---

## 5. Семь допущений покупки (здесь «покупка» = установка и работа программы)

Канон (`communication.md §2`): если установки нет, сначала найти сломанное допущение и только потом переписывать текст.

| # | Допущение | Статус для WCG | Основание |
|---|---|---|---|
| 1 | Лид из целевого сегмента, с нужными Big Jobs | **Под вопросом.** Шапка обслуживает сразу волонтёров, доноров, учёных и кранчеров. Откуда идёт трафик, не видно | [факт + гипотеза] |
| 2 | Ценность выше прогноза и текущего способа | **Не проверяемо с лендинга.** Соотношение 93 тыс. текущих к 822 тыс. за всё время говорит, что у многих ценность не превзошла ожидание | [факт + гипотеза] |
| 3 | Лид понимает ценность | **Частично**: польза для науки понятна, своя доля — нет | [вывод] |
| 4 | Нужные условия в реальности выполнены | **Частично.** Нужен Windows / Mac / Linux / Android / Raspberry Pi; iOS не поддерживается, а About пишет «smartphone or tablet». У проектов разные требования (Africa Rainfall — 1 GB RAM, 1.5 GB диска, 100 MB на задачу, без Android). Активных проектов всего 3 | [факт] |
| 5 | Конкретные страхи снижены | **В основном да** (4 из ~7 вероятных страхов на главной) | [факт + вывод] |
| 6 | Путь до ценности достаточно короткий | **Слабо.** Аккаунт → проекты → установка BOINC → задача → проверка → очки (обновление дважды в сутки). В конце видны очки, а не польза | [факт + вывод] |
| 7 | Цепочка не ломается по дороге | **Мелкие поломки и следы запустения**: /download для гостя → login; FAQ на How it works без видимых ответов; «Celebrating 20 years» в 2026-м; «in less than a decade», «18 years», «Over the past year… transferred» (текст ~2022); Android 4.1 и 4.4 в разных местах; «900 million as of May 2013»; советы про Internet Explorer; у BOINC сервер не работал с 3 по 10 сентября 2026 | [факт] |

---

## 6. Барьеры, страхи, ожидания и проба Aha

### 6.1 Барьеры (реальные факты) vs страхи (прогнозы)

Канон: барьер снимается изменением реальности, страх — коммуникацией, и только если он не сбывается (`barrier-removal.md §3–4`).

**Барьеры** [факт, кроме отмеченного]:
- нет iPhone / iPad-версии, то есть для владельцев только iOS-устройств путь закрыт (тип «unsupported context», `barrier-removal.md §5`);
- аккаунт до загрузки: «Download» гостю недоступен;
- требования проектов к памяти и диску; на Android доступна только часть проектов;
- мало работы: 3 активных проекта; у BOINC-проектов бывают периоды без задач (Amicable Numbers: «don't expect 24/7 availability of tasks») [гипотеза для WCG: перебои с задачами на сайте WCG не упоминаются, но «No Task Executing» есть в справке].

**Страхи** [состав — гипотеза; статус на лендинге — факт]:

| Страх | Реален ли (по сайту) | На главной WCG |
|---|---|---|
| «Будет тормозить» | не сбывается: приоритет у других задач, 60% процессора по умолчанию | ✔ «It won't slow you down» |
| «Сядет батарея» | не сбывается: только от сети (Android — от 90% заряда) | ✔ |
| «Вирус, доступ к файлам» | не сбывается: подпись приложений, проверка кода, нет доступа к файлам | ✔ (без деталей про подпись) |
| «Съест мобильный трафик» | не сбывается: только Wi-Fi. На проводном интернете — до 100 MB на задачу у Africa Rainfall | ✔ |
| «Вырастет счёт за электричество» | **частично реален**: «slight increase… equivalent of an additional low wattage light bulb» | ✘ только в справке |
| «Перегреется, будет шуметь» | частично: раздел про перегрев есть в справке, 60% по умолчанию | ✘ |
| «Проект заброшен / кто за ним стоит» | IBM ушла в 2022, теперь академическая группа с «significant financial challenge» | ✘ только логотипы Krembil в футере |
| «Мои вычисления пойдут фарме, а не людям» | на /donations: «open-source and open-data research» | ✘ |

Вывод: WCG сделал главное, что Charity Engine не сделал: закрыл страхи на самой странице. Оставшиеся страхи дешёвые: ответы уже написаны в справке. Самый неприятный — «проект заброшен», и его подпитывает сам сайт (юбилей двухлетней давности, старые тексты). [вывод]

### 6.2 Управление ожиданиями

Канон: коммуникация задаёт прогноз, который продукт должен превзойти (`communication.md §9`).
- **Сильная сторона**: WCG обещает честно. «bringing them one step closer to discoveries», «could lead to improved cancer detection» — это Core Job («помогаю считать»), а не Big Job («победим рак»). Канон прямо предостерегает от обещания Big Job, которую продукт выполняет не целиком (`communication.md §3`). [факт + вывод]
- **Слабая сторона**: обещание «Your device makes a difference» в продукте превращается в очки и счётчик результатов. Обратная связь о пользе приходит раз в полгода (Research Update). Ожидание «я помогаю» быстро встречается с невидимостью вклада. Канон: устойчивое изменение поведения требует потока Aha (`behaviour-change.md §11`). [вывод]
- Масштабные числа («2.7M years») задают прогноз «моя доля незаметна», то есть работают против личной ценности. [гипотеза]

### 6.3 Проба Aha на лендинге

Канон: Aha (момент, когда продукт оказался лучше ожиданий) ставится как можно левее; каждый шаг до него — внимание в долг (`customers-attention-management.md §6`).
- Настоящий Aha продукта [гипотеза]: «вижу, что мой компьютер вернул первые результаты для проекта по раку, и знаю, что это значит». Для S2 — «очки и место в команде растут».
- На лендинге пробы нет: нет примера экрана «My contribution», нет живого «сейчас считают N устройств», хотя статистика обновляется каждые 12 часов («Statistics last updated… 4 hour(s) ago»). [факт + вывод]
- До Aha [факт]: регистрация → выбор проектов → загрузка и установка BOINC → задача (в среднем 3 часа на результат: «Run time per result 0:000:03:00:55») → проверка → обновление очков в 00:00 или 12:00 UTC. То есть первый видимый вклад приходит через часы, а то и на следующий день.

---

## 7. Силы за и против перехода, конкуренты

Канон: силы изменения поведения (`behaviour-change.md §9`).

**Двигатели** [вывод]:
- идентичность («я волонтёр науки»): лендинг её трогает — «As a World Community Grid volunteer»;
- конкретность получателя пользы (фермеры, онкобольные) делает Big Job осязаемой;
- доверие института: IBM в прошлом, теперь университетская больница (UHN) — но это почти не видно на главной;
- «бесплатно для меня» плюс снятые страхи.

**Тормоза** [вывод]:
- асимметрия цены: установка сейчас, польза потом и невидимая;
- признаки запустения подрывают доверие в категории «пусти программу на свой компьютер»;
- **после установки нет повода помнить о продукте** (он работает невидимо, а это одновременно ценность и проблема: нет потока Aha) [гипотеза];
- главный конкурент — **«ничего не делать»** (`ajtbd-key-theses.md §17`).

**Конкуренты, которых лендинг должен «уволить»** [гипотеза: на сайте WCG ни один не назван]:
1. **«Ничего не делать»**: компьютер просто простаивает. Лендинг бьётся с ним фразой «when it has spare power», но не говорит, чего человек лишается.
2. **Обычное пожертвование** на рак или голод. Ирония: в шапке WCG сам просит донаты. Нужна связка «время компьютера бесплатно + деньги, если можешь», а не два CTA рядом.
3. **Другие проекты на BOINC и Science United** (Rosetta@home, Einstein@home и др.) и Folding@home вне BOINC. Для S2 это главный выбор, и BOINC сам выставляет WCG одним из 28 вариантов. Чем WCG лучше (гуманитарная направленность, «the biggest volunteer computing initiative devoted to humanitarian science», открытые данные), на главной не сказано.
4. **Charity Engine**: тот же BOINC, но с деньгами фондам и розыгрышем. Форма регистрации Charity Engine прямо спрашивает про аккаунт WCG.
5. **Приложения, которые платят за простаивающее железо или трафик** (Salad, Grass и т. п.) и **Gridcoin**, который BOINC сам предлагает на главной («participate in competitions and systems like Gridcoin»). Для части аудитории выбор стоит между «деньги себе» и «наука другим».

---

## 8. BOINC как платформа: коротко и в сравнении с WCG

| Параметр | WCG | BOINC |
|---|---|---|
| Для кого страница | S1 — альтруист-новичок (плюс шапка для всех остальных) | Энтузиаст + учёные + программисты на одном экране [вывод] |
| One-liner на первом экране | ✘ (юбилей) | ✔ «Compute for Science» + описание механизма [факт] |
| Ценность в критериях | только цена участия | «invisibly in the background», в остальном прилагательные [факт] |
| Конкретные получатели пользы | ✔ фермеры, онкобольные | ✘ «diseases, climate change, pulsars» — категории [факт] |
| Снятие страхов | ✔ 4 блока с механизмами | «easy and safe», «will not affect your normal use» — без механизмов [факт] |
| Доверие | цитата учёного, логотипы прессы | UC Berkeley + NSF (сильно и коротко) [факт] |
| Первый шаг | аккаунт до загрузки | загрузка без аккаунта; Science United — аккаунт с выбором областей и режима нагрузки [факт] |
| Выбор, чему помогать | при регистрации (на лендинге не виден) | развилка «области» (Science United) / «конкретные проекты» (BOINC) [факт] |
| Признаки жизни | новости раз в полгода, устаревшие тексты | свежие новости проектов (вчерашние), но сырые и технические; признание отключения сервера на неделю [факт] |

Выводы по BOINC [вывод]:
- BOINC продаёт механизм («платформа для науки»), а не Big Job. Для энтузиаста (первый класс, Core Job знакома) этого хватает. Для новичка (второй класс) страница сразу перекладывает на него работу по выбору (Orientation Job): «When you first run BOINC, you will be asked to choose a project», плюс критерии выбора на /projects.php. Это внимание в долг до Aha (`customers-attention-management.md §6`).
- Science United — правильный ответ на эту проблему: выбор «областей» вместо 28 проектов и выбор режима нагрузки (Low power / Standard / Maximum) прямо в регистрации. Это управление ожиданием и снятие страха «будет тормозить» в одной фиче. Но на главной BOINC Science United подан как один из двух равных вариантов, без объяснения, что он для новичка.
- WCG по отношению к BOINC — «упакованный продукт поверх платформы»: одна тема (гуманитарная наука), понятные получатели пользы, страхи сняты. Это именно то, чего BOINC не хватает для массового сегмента. Но WCG теряет главное преимущество BOINC — загрузку без регистрации.

---

## 9. Итог

### 9.1 Топ-риски лендинга WCG

1. **Первый экран не объясняет продукт** (юбилей + «Learn more»): посетитель, который не прокрутил, уходит без понимания. [факт + вывод]
2. **Личный вклад невидим** ни на лендинге, ни, судя по справке, в первые часы после установки: ценность для S1 не выражена, есть риск разочарования и тихого ухода. Из 822 тыс. участников за всё время текущих около 93 тыс. [факт + гипотеза]
3. **Признаки запустения**: «20 years» в 2026-м, тексты 2022 года, старые результаты без дат, новости раз в полгода. Для категории, где доверие — главный критерий, это подрывает блок страхов. [факт + вывод]
4. **Дорогой первый шаг**: аккаунт до загрузки, «Download» закрыт для гостя, платформы и шаги не названы. [факт]
5. **Конкурирующие CTA и аудитории в шапке** (Download, Donations, Join, Submit a proposal, статистика). [факт + вывод]
6. **Финансовая хрупкость, не названная на главной** («significant financial challenge»): это риск продукта, а не только лендинга. Если проект встанет, волонтёры увидят Problem против всего продукта. [факт + гипотеза]

### 9.2 Точки роста: конкретные правки

Формулировки — черновики-гипотезы для англоязычного лендинга. Пометка `[VERIFY]` — нельзя публиковать без подтверждения данными WCG.

1. **One-liner на первый экран** вместо юбилея. Взять текст meta description и добавить механизм:
   «*Turn your computer's idle time into cancer and climate research. World Community Grid runs science tasks in the background — only when you're not using the power, never touching your files.*» CTA: «*Start helping — free*». Юбилей перенести в бейдж («Since 2004»).
2. **Личный вклад в понятных единицах** (компонент 2): «*An average computer returns about 2 research results a day — roughly 6 hours of science computing, every day you leave it on.*» (2 результата в день и 3 часа на результат — факты справки и статистики; «6 hours» — арифметика, `[VERIFY]` на текущих проектах.)
3. **Свежий результат с датой и цифрой вместо трёх старых**: «*June 2026: Mapping Cancer Markers found SLC5A1 as a top-scoring gene in predictive signatures — computed on volunteers' devices.*» Переписать научный язык новости простыми словами `[VERIFY]` вместе с командой MCM. Даты у трёх старых карточек показать или заменить их.
4. **Дополнить блок страхов тем, что уже есть в справке** (компонент 4):
   - «*Electricity?* About as much as one extra low-wattage bulb. Uses 60% of spare CPU by default — you can lower it.» (справка Costs и CPU Usage)
   - «*Who runs it?* Since 2022, Krembil Research Institute at Toronto's University Health Network — after 18 years at IBM.» (About и Donations)
   - «*Every research app is cryptographically signed — your device rejects anything else.*» (Security)
   - «*Results are open data.*» `[VERIFY для каждого проекта]`.
5. **«Уволить» альтернативы** (компонент 5): «*Your computer is on anyway. Right now its spare power does nothing. Here it searches for cancer markers — at zero cost to you.*» Для S2: «*Already run BOINC? Add World Community Grid in one step — humanitarian research only.*»
6. **Дешёвый первый шаг**: открыть /download без аккаунта (как у BOINC), аккаунт — после установки; рядом с кнопкой показать платформы («Windows · Mac · Linux · Android · Raspberry Pi») и честно «not available on iPhone». Под «Join» показать три шага.
7. **Проба Aha на странице**: живой счётчик со страницы статистики («*Yesterday volunteers returned 1.2M results — 259 years of computing in one day*») и пример экрана «My contribution». `[VERIFY — как этот экран выглядит в продукте]`.
8. **Почистить шапку**: «Donations» и «Submit a proposal» перенести в футер или во вторичное меню, на главной оставить один CTA.
9. **Убрать устаревшее**: «20 years», «in less than a decade», «Over the past year», Android 4.1 / 4.4, «900 million as of May 2013», советы про Internet Explorer.

### 9.3 Рискованные допущения лендинга (RAT) и как их дёшево проверить

Ранжировано по «насколько смертельно, если неверно» × «насколько дёшево проверить». [гипотеза — все пункты]

| # | Допущение, на котором стоит лендинг и продукт | Если неверно | Дешёвая проверка |
|---|---|---|---|
| 1 | Волонтёрам достаточно знать, что сеть большая; личный вклад показывать не нужно | Ставят и забывают, потом удаляют; соотношение текущих к общим остаётся около 11% | Когортный анализ «активен через 30 / 90 дней»; A/B: письмо или уведомление «твой компьютер за неделю сделал N задач для MCM» vs без него |
| 2 | Посетитель прокручивает до блока 3, чтобы понять, что это | Высокий отказ с первого экрана | Карта скролла; A/B hero «юбилей» vs one-liner; метрика — клик по «Join» |
| 3 | Регистрация до загрузки не убивает конверсию | Отвал на шаге «Create account» и «Select projects» | Воронка Join → Sign Up → Select projects → первый результат; тест «Download first» |
| 4 | Блок страхов закрывает главные страхи | Остаются невидимые (электричество, «кто за этим стоит») | 10–15 интервью с теми, кто был на сайте и не установил (`barrier-removal.md §7`: «Was there anything you saw or heard… that made you not even try it?») |
| 5 | Признаки старости сайта не вредят доверию | Новички считают проект заброшенным | Пятисекундный тест первого экрана: «как думаете, проект ещё работает?» |

### 9.4 Чему научиться нашему charity / passive-earning продукту

1. **Скопировать структуру блока страхов WCG.** Каждый страх назван простыми словами («It won't drain your battery»), и сразу под ним механизм («only runs when you're connected to power»). Это лучший готовый образец из всех разобранных лендингов. У нас должны быть свои версии: батарея, трафик, электричество, безопасность, что продаётся из моего ресурса. [вывод]
2. **Первый экран объясняет продукт.** Юбилей, миссия и «Learn more» на первом экране съедают самое дорогое внимание. One-liner по формуле «что + работа + ценность» и CTA первого шага. [вывод]
3. **Личный вклад важнее масштаба сети.** «822k volunteers» говорит «ты капля в море». Нужна единица, в которой человек видит себя: «твой телефон = N задач / обедов / деревьев в неделю», честным диапазоном. [вывод]
4. **Невидимая работа требует видимой обратной связи.** Ценность «работает незаметно» одновременно убивает удержание: человек забывает, что помогает. Нужен регулярный поток маленьких Aha (еженедельный отчёт, «твоя задача пригодилась»), а не обновление раз в полгода. Соотношение 93 тыс. к 822 тыс. — предупреждение. [вывод / гипотеза]
5. **Сначала результат, потом аккаунт.** BOINC даёт скачать без регистрации, WCG — нет. Мы откладываем регистрацию до первого показанного вклада. [вывод]
6. **Обещать Core Job, а не Big Job.** WCG честно говорит «one step closer to discoveries», а не «вылечим рак». Это защищает от разочарования. Нам — «твоё устройство даёт N для фонда X», а не «спасаешь планету». [вывод]
7. **Снять работу по выбору с новичка.** BOINC вываливает 28 проектов, Science United предлагает выбрать область и режим нагрузки. Для нас: 2–3 понятные цели и режим «бережный / обычный / максимум» прямо при старте. [вывод]
8. **Сайт должен выглядеть живым.** Свежие даты, свежие результаты, никаких «20 years» через два года после юбилея. Для продукта, которому доверяют своё устройство, запустение читается как риск. [вывод]
9. **Не ставить рядом CTA «отдай ресурс» и «дай денег».** У WCG «Download», «Donations» и «Join» стоят в шапке рядом. Если нужны оба, сначала бесплатное участие и Aha, потом предложение доплатить. [вывод / гипотеза]

---

## Источники (сняты 2026-11-22)

World Community Grid:
- https://www.worldcommunitygrid.org/ — главная (Playwright: извлечение текста + полный скриншот `/Users/alexgaidukov/Projects/Charity/.playwright-mcp/wcg-home-2026-11-22.png`)
- https://www.worldcommunitygrid.org/join → /join/signup — форма регистрации
- https://www.worldcommunitygrid.org/download → перенаправляет на /login
- https://www.worldcommunitygrid.org/about_us/viewGridComputingBasics.do → /about/how.s — How it works (видео «How WCG Works», https://www.youtube.com/watch?v=P5QU_99oF5k)
- https://www.worldcommunitygrid.org/research/projects.s
- https://www.worldcommunitygrid.org/about/security.s
- https://www.worldcommunitygrid.org/about/about.s
- https://www.worldcommunitygrid.org/donations
- https://www.worldcommunitygrid.org/stat/viewGlobal.do
- https://www.worldcommunitygrid.org/help/viewHelp.do → /help/help.s
- Справка (curl): https://www.worldcommunitygrid.org/help/topic.s?shortName= costs, install, minimumreq, cpuuse, reg, android, points

BOINC:
- https://boinc.berkeley.edu/ — главная (curl + скриншот первого экрана `/Users/alexgaidukov/Projects/Charity/.playwright-mcp/boinc-home-2026-11-22.png`)
- https://boinc.berkeley.edu/download.php
- https://boinc.berkeley.edu/projects.php
- https://boinc.berkeley.edu/computing.php (суммарные цифры подгружаются скриптом, не сняты)
- https://scienceunited.org/ и https://scienceunited.org/su_join.php

Внутренний контекст: `apps/05-wcg-boinc.md` (шаблон, заметок пока нет); для структуры — `apps/02-charity-engine-landing-nmt.md`.

Методология (канон): `Next-Move-Theory-Canon/Advanced-Jobs-To-Be-Done/` — communication.md (§2–§9), consideration-activators.md (§1, §4, §6, §10), barrier-removal.md (§1–§7), customers-attention-management.md (§4–§6), behaviour-change.md (§9–§11), job-structure.md (§8–§9), segmentation.md (§7–§9), ajtbd-key-theses.md (§6, §17, §24); `.claude/skills/nmt-craft-go-to-market/` (SKILL.md, references/glossary.md); `.claude/skills/nmt-diagnose/SKILL.md`.

Не снималось: шаги 2–3 регистрации WCG и сам клиент (нужен аккаунт); экран «My contribution»; содержимое видео «How WCG Works»; раскрытие FAQ на /about/how.s по клику; Terms of use и Privacy statement WCG целиком. Что именно считается «Current members» в статистике WCG (активные или с непустым профилем), на сайте не указано, поэтому оценка «около 11% остаются» — гипотеза.
