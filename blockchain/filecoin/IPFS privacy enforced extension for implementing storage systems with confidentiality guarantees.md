
<center>Стрєльніков М. Д.; Ковальчук Л.В., д. т. н., проф. </center>
<center>Національний технічний університет України "Київський</center>
<center>Політехнічний Інститут ім. Ігоря Сікорського"</center>
<center>НН Фізико-технічний інститут</center>
<center>strielnikovmd-ipt@lll.kpi.ua; </center>

---
**Анотація**
У роботі проаналізовано засоби реалізації анонімності і криптографічної безпеки вмісту файлів в розподіленій децентралізованій файловій системі IPFS. Запропоновано та розглянуто засоби підсилення властивості анонімності та шифрування контенту у файловій системі  IPFS з можливістю коректного пошуку зашифрованого вмісту, використання кінцевого шифрування, а також можливості гарантованого і швидкого видалення.

Ключові слова: Proof-of-spacetime, proof-of-replication, filecoin, IPFS, доведення без розголошення, розподілена геш-таблиця, ациклічний граф Меркла.

---
##### Вступ
На сьогоднішній день, проблема збереження конфіденціальності особистих данних вкрай актуальна. Використовуючи переважну більшість додатків та сервісів, користувач не має  гарантії того, що його особисті конфіденційні данні зберігаються зашифрованними. Інша проблема - стабільна та безперебійна доступність централізованих сервісів в умовах стибкоподібного збільшення зростаючих запитів, що можуть спричинити тимчасову недоступність сервісів. У роботі запропоновано використовувати протокол файлової системи IPFS для реалізації децентралізованого конфіденційного сховища данних з гарантованим "скрізним шифруванням". Вирішення цієї задачі надасть можливість створити системи, у яких конфіденційні данні користувача можуть зберігатись, а у подальшому й опрацьовуватись, із наданням карантій конфіденційності. Зберження особистих данних в безпеці є критичними для систем які обробляють конфіденційні данні такі як: менеджери паролів, месенджери, особисті данні пацієнтів медичних установ, данні криптогаманців, сховища конфіденційних файлів та документів, державні реєстри та ін.
##### 1. Вимоги до конфіденційного сховища данних
Розглянемо деяку розподілену систему, яка виступає сховищем чутливих
користувацьких данних. У більшості випадків, користувач не має надійного засобу
перевірки наступних умов:
1. Чутливі данні, що зберігаються у розподіленому сховищі дійсно
зашифровані і провайдер послуг не має доступу до відкритих данних та
зберігає їх зашифрованими (гарантія шифрування);
2. Ключі шифрування згенеровані користувачем, є унікальними, шифрують
лише данні цього користувача і не використовуються системою повторно
чи для шифрування інших данних (гарантія унікальності ключів
шифрування);
3. Без прямої згоди користувача та надання ним системі приватного ключа
(або його приватної частини) неможливо поновоти ключ розшифрування,
таємно скопіювати його під час доступу до системи, а також виключено
існування інших частин загального секрета, що дозволять поновти секрет
(гарантія неможливості розшифровки даних провайдером послуги).

На стогодні існує декілька комерційних аналогів, що за заявленням розробників реалізує наведені вимоги - парольний менеджер NordPass [1], 1password [2], passpack [3], keeper [4] , та BitWarden (також лише у платній версі) [5]. Всі наведені рішення мають централізовану мережеву архітектуру та повністю закритий стандарт реалізації, що унеможливлює легальні спроби аудиту рішення.
##### 2. IPFS: огляд основних принципів та вирішуваних задач
IPFS _(англ. Interplanetary File System)_ – набір протоколів, що забезпечують маршрутизацію у одноранговій мережі (англ. _peer-to-peer_), контенто-орієнтований пошук та зберігання данних[6]. Деякі сучасні WEB3-додатки використовують IPFS замість традиційного стеку мережевих протоколів прикладного рівня (за моделлю OSI) -  HTTP/HTTPS. 
IPFS вирішує наступні проблеми [7]:
1. Розподіл і доступність данних через їх реплікацію у одноранговій мережі, що робить систему на основі IPFS високодоступною та надлишковою: файли розбиваються блоки, що зберігаються на різних вузлах однорангової мережі та у деякій кількості копій (реплікація).
2. Неможливість цензури всередині мережі, через відсутність ценьрального серверу.
3. Можливість версіонування файлів та контенту, що міститься у IPFS.
4. Перевірка цілісності кожного файла, завдяки використанню дерева Меркла для, де кожний листок відповідає деякому блоку файла, а вузол деякому файлу чи группі файлів.
Проте IPFS не має вбудованого функціоналу, що реалізує:
1. Кінцеве шифрування.
2. Шифрування контенту.
3. Розподілу доступу.
4. Авторизації при доступі до контенту.
##### 3. IPFS: огляд підсистем та допоміжних протоколів
Прооведемо огляд основних складових IPFS [8], визначемо їх роль та проаналізуємо властивості тих компонентів, що буде становити інтерес у данній роботі.
1. Content Identifiers (CIDs) - унікальний ідентифікатор блоку файлу, що залежить від його вмісту. Може бути отриманий, як результат геш-функції над блоком. За замовченням використовується SHA-256, проте може бути використано SHA-1, KECCAK, SHAKE, X11, BLAKE, MD5 та ін.[10]
2. Bitswap – протокол, що реалізує, відправку і отримання блоків файлів одноранговою мережею у вигляді повідомлень.[11]
3. Distributed Hash Tables (DHT) – розподілена структура данних, що представляє собою зв'язний список із пари ключа та значення. Дозволяє співвідносити СID певного блоку файлу із ідентифікатором вузлу IPFS-мережі (peerID).[12, 13, 14]
4. DNSLink – протокл, який співвідносить FQDN _(англ. Fully Qualified Domain Name)_ традиційної інтернет-адресси із ідентифікатором об'єкту (СID) у файловій системі IPFS наступним чином: під час DNS-запиту FQDN-адреси файлу, повертається DNS-відповідь, що містить шлях до контенту у просторі IPFS (СID контенту). Використання цього підходу, надає доступ до об'єктів, що зберігаються у IPFS через звичайний браузер, який може отримувати контент лише за FQDN.[15, 16]
5. IPFS Gateway – надає сервіс, що дозволяє IPFS-несумісним браузерам переглядати файли в просторі IPFS. Являє собою проміжкове програмне забезпечення _(англ. Middleware)_ для proxy-серверів, які виступають у ролі посередників між браузером та IPFS-мережею. IPFS Gateway (proxy-сервер) отримує HTTP(S)-запит з браузера клієнта і повертає контент зсередини IPFS-мережі також у вигляді HTTP-відповіді.[17]
6. IPLD _(англ. Inter-Planetary Linked Data)_ - набір форматів та способів представлення данних, а також методи конверсії, серіалізація та десеріалізації данних між різними протоколами стеку IPLD.[18, 19]
7. IPNS _(англ. Inter-Planetary Name System)_ – дозволяє створювати змінювані назви _(англ. Alias)_ та вказівники _(англ. Mutable Pointers)_, що співставлені із СID певного контенту у форматі зручному для сприйняття людиною. Спрощує користування всередині екосистеми протоколів IPFS - дозволяє легко знаходити контент використовуючи зручний для сприйняття формат, оскільки користувач скоріш за все не знає СID (чи геш-значення) контенту, який він шукає [20]. Записи IPNS також містять цифрові підписи, що однозначно співвідносять автора із зробленими ним змінами у контенті по вказаній назві IPNS (авторизація). З цієї точки зору, на IPNS можна дивитись, як на одноранговий PKI _(Public Key Infrastructure, укр. Інфраструктура Відкритих Ключів)_, що реалізує підхід web-of-trust[21].
8. libp2p – фреймвор для розробки Р2Р *(peer-to-peer)* додатків, що включає інструментарій для побудови додатків, що використовують IPFS.
9. Merkle Directed Acyclic Graphs (MDAGs) – одна з ключових ідей протоколу IPFS [22]. Merkle DAGs використовуються для: розбиття файлу на блоки, відновлення файлу по блоках, розподіл реплік файлу по однорангових вузлах IPFS, перевірка та верифікація цілісності та автентичності блоків та файлів, версіонування файлів, організовує усі СID у дерево, використовується для пошуку контенту [23, 7]. 
##### 4. Аналіз концепції контентоорієнтованого пошуку


##### 5. Filecoin
Іншою пов’язаною розробкою є криптовалюта Filecoin [24]. Filecoin – є сховищем файлів, що використовує блокчейн для зберігання файлів. Згідно задуму криптовалюти,
користувачі отримують винагороду токен filecoin за надання та оренду апаратного сховища для збереження та реплікації даних або файлів. Filecoin побудовано, як рівень абстракції над IPFS. Він вирішує задачу поширення використання IPFS, шляхом введення винагород за предоставлення вузлами простору для зберігання данних протягом часу або реплікації. Винагороди розподілюються шляхом встановлення консенсусу у блокчейні за допмогою специфічних алгоритмів:
1. Proof-of-replication (PoRep) – доказ, що використовує zkSNARKs для формування нових листків у MDAG із виділенням відповідного місця на жорсткому диску [29. 30].
2. Proof-of-spacetime (PoST) – дозволяє отримати доказ того, що вузли дійсно зберігають певні файли, які займають певне місце на жосткому диску протягом певного проміжку часу. Вимагає виконання певних криптографічних алгоритмів на цих файлах [31].

Також блокчейн filecoin підтримує власну віртуальну машину FVM, що дозволяє виконувати смартконтракти [32].
##### 6. Розробка розширень конфіденційності IPFS

##### 6.1 Еnd-to-end шифрування контенту
Кінцеве шифрування _(англ. Еnd-to-end)_ - практична реалізація криптографічних протоколів таким чином, що інформація зберігається на кінцевих пристроях чи передається із одного пристроя на інший через незахищенний телекомунікаційний канал лише у зашифрованому вигляді
##### 6.1.1 Протокол створення репліки зашифрованних данних із використанням кінцевого шифрування
Уявімо, що користувач Alice є вузлом мережі IPFS та криптграфічного гаманця Filecoin. Вона прагне зберігати свої власні данні локально на персональному комп'ютері, проте прагне зробити зашифровану копію данних у IPFS сховищі.

Вхід: Приватний ключ від гаманця Filecoin - $SeedPhrase$, файл $m$ (у вигляді відкритого тексту), назва файлу $n_{m}$.
Вихід: Успішно створено репліку поданних данних
1. Користувач Alice виконує автентифікацію у IPFS мережі шляхом авторизації у гаманці Filecoin із власним $SeedPhrase$ (приватний ключ криптогаманця).
2. Alice створює структуру данних $M'$, що складається з:
	Вхід: $SeedPhrase$,  $m$, $n_{m}$ .
	Вихід: контейнер зашифрованих даних $M'$.
	1. Alice генерує випадковий симетричний ключ: $k = rand()$
	2. Alice виконує симетричне шифрування пари $\{n_{m}, m\}$ із використанням ключа $k$: $Enc(\{n_{m}, m\}^k)=M$
	3. Alice формує структуру данних $M'$, що містить $M$ та симетрично зашифрований інший симетричний ключ $k$: $Enc(\{M, k\}^{SeedPhrase})=M'$
	4. Повернути $M'$
3. Alice виконує цифровий підпис $M'$, отримуючи симетрично зашифрований і асиметрично підписаний контейнер $\bar{M}$:
	Вхід: $M'$
	Вихід: $\bar{M}$.
	1. Alice генерує випадковий приватний ключ: $sk = rand()$.
	2. Alice генерує відповідний відкритий ключ $psk$.
	3. Alice виконує цифровий підпис пари публічного ключа $psk$ із контейнером $\bar{M}$, використовуючи $sk$: $\bar{M} = Sign(\{M', psk\}^{sk})$.
	4. Alice знищує приватний ключ $sk$.
	5. Повернути $\bar{M}$
4. Відправлення копії контейнеру $\bar{M}$ із зашифрованними і підписанними данними іншому довільному вузлу Bob мережі IPFS:
	1. Alice вимірює розмір у байтах для $\bar{M}$: $l=sizeof(\bar{M})$.
	2. Alice робить пошук довільного вузлу мережі Bob, що має достатньо місця $c$ для збереження $\bar{M}$: $c > l$.
	3. Відправляє вузлу мережі Bob зашифрований і підписаний контейнер $\bar{M}$.
5. Bob використовує Proof-of-replication протокол для додання нових листків у МDAG, що відповідає збереженню блоків файлу, відповідно реплікації данних $\bar{M}$ серед деяких інших вже авторизованих вузлів.

Аналіз протоколу вище:
1. Bob є автентифікованим користувачем за замовченням, оскільки кожний користувач filecoin володіє криптогаманцем і виконує авторизацію у мережі на початку роботи із використанням особистої $SeedPhrase$.
2. Alice шифрує данні файлу асиметрично, оскільки Alice не буде зберігати ключ рошифрування у відкритому вигляді.
3. Alice також шифрує назву данних або файлу $n_{m}$ щоб не надавати Bob інформації про природу данних, що зберігаються.
4. Alice шифрує контейнер із зашифрованними данними $M'$ та ключем $pk$, щоб приватний ключ $pk$ міг зберігатись у безпеці, як на локальному комп'ютері Alice, так і віддалено.
5. Alice підписує контейнер і отримує $\bar{M}$, щоб мати змогу підтвердити своє авторство над $\bar{M}$ та $M'$ відповідно.
6. Alice знижчує приватний ключ підпису $sk$, оскілки він більше небуде використовуватись і становитиме загрозу крадіжки. Ключ $sk$ є разовим.
7. Нема необхідності у асиметричному обміні ключів, оскільки данні, що відправляються на вузол да Bob зашифровані симетричним ключем Alice заздалегіть. Цифрового підписа достатньо для запобігання спотворення вмісту повідомлення.
8. Ключі шифрування генеруються користувачем локально, а віддаленні вузли не мають ключу розшифрування $SeedPhrase$, виконуючи умови наведенні у постановці задачі п. 1.
9. Безпека протоколу зводиться до безпеки зберігання $SeedPhrase$ (як у більшості криптовалют), та у некомпроментованітсть й криптографічну надійність криптографічного генератора псевдовипадкових чисел $rand()$.

##### 6.1.2 Протокол відновлення зашифрованних данних із репліки, використовуючи кінцеву шифрування
Уявімо, що користувач Alice є вузлом мережі IPFS та криптграфічного гаманця Filecoin. Проте в данний момент часу, Alice не має доступу до свого особистого ком'ютера із копією особистих данних. Alice прагне запитати репліку своїх данних у Bob, що э одним із зберігачів реплік данних Alice.

Вхід: Приватний ключ від гаманця Filecoin - $SeedPhrase$.
Вихід: дешифровані данні $\{m, n_m\}$.
1. Користувач Alice виконує автентифікацію у IPFS мережі шляхом авторизації у гаманці Filecoin із власним $SeedPhrase$ (приватний ключ криптогаманця)
2. Alice запитує у Bob репліку особистих данних $\bar{M}$.
3. Bob здійснює перевірку належності данних $\bar{M}$ до Alice, шляхом перевірки підпису: $Verif(\{\bar{M}, Allice\}^{psk}) = Verif(\{{\{M', psk\}}, Allice\}^{psk}) \in \{ true, false\}$.
4. Якщо Alice є валідним користувачем, то Bob відправляє $\bar{M}$ до Alice.
5. Alice виконує дешифрування: $M' = Enc^{-1}((\bar{M})^{SeedPhrase}) = \{M, k\}$
6. Alice виконує дешифрування: $M = Enc^{-1}((M')^{k}) = \{m, n_m\}$
7. Повернути $\{m, n_m\}$

Аналіз протоколу вище:
1. Безпека протоколу зводиться до забезпечення безпеки зберігання $SeedPhrase$ (як у більшості криптовалют).
2. Усі данні на всії етапах передаються та зберігаються у зашифрованному вигляді.
3. Нема необхідності у асиметричному обміні ключів, оскільки данні, що зберігає вузол Bob, вже зашифровані ключем Alice заздалегіть.

##### 6.1.3 Оптимізація пошуку у MDAG серед зашифрованих данних



##### Висновки
Розроблено протокол, що відповідає вимогам задачі, наведеним у п. 1. Наведено протокол, що дозволяє реалізувати сховизе данних із гарантованим шифруванням, конфіденціністю та високою доступністю. Реалізація запропонованих протоколів може бути виконано, з використанням можливостей смартконтрактів.
##### Джерела
1. NordPass. (n.d.). Features: Zero-Knowledge Architecture. Retrieved \[15 jan 2024\], from [https://nordpass.com/features/zero-knowledge-architecture/](https://nordpass.com/features/zero-knowledge-architecture/)
2. 1Password. (n.d.). Zero-Knowledge Encryption. Retrieved \[16 jan 2024\], from [https://1password.com/features/zero-knowledge-encryption/](https://1password.com/features/zero-knowledge-encryption/)
3. Passpack. (n.d.). Zero-Knowledge Password Manager. Retrieved \[16 jan 2024\], from [https://passpack.com/zero-knowledge-password-manager/](https://passpack.com/zero-knowledge-password-manager/)
4. Keeper Security. (n.d.). Zero-Knowledge for Ultimate Password Security. Retrieved \[16 jan 2024\], from [https://www.keepersecurity.com/resources/zero-knowledge-for-ultimate-password-security.html](https://www.keepersecurity.com/resources/zero-knowledge-for-ultimate-password-security.html)
5. Bitwarden. (n.d.). Zero-Knowledge Encryption White Paper. Retrieved \[16 jan 2024\], from [https://bitwarden.com/resources/zero-knowledge-encryption-white-paper/](https://bitwarden.com/resources/zero-knowledge-encryption-white-paper/)
6. IPFS. (n.d.). IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/](https://docs.ipfs.tech/)
7. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 2). Kharkiv: PROMART. (pp. 56-64). IPFS
8. IPFS. (n.d.). File Systems. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/file-systems/](https://docs.ipfs.tech/concepts/file-systems/)
9. IPFS. (n.d.). Concepts. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/](https://docs.ipfs.tech/concepts/)
10. IPFS. (n.d.). Content Addressing. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/content-addressing/](https://docs.ipfs.tech/concepts/content-addressing/)
11. IPFS. (n.d.). Bitswap. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/bitswap/](https://docs.ipfs.tech/concepts/bitswap/)
12. Wikipedia contributors. (n. d.). Distributed Hash Table. In Wikipedia, The Free Encyclopedia. Retrieved \[15 jan 2024\], from [https://en.wikipedia.org/wiki/Distributed_hash_table](https://en.wikipedia.org/wiki/Distributed_hash_table)
13. IPFS. (n.d.). DHT (Distributed Hash Table). In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/dht/](https://docs.ipfs.tech/concepts/dht/)
14. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 2). Kharkiv: PROMART. (pp. 26-31). DHT
15. IPFS. (n.d.). DNSLink. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/dnslink/](https://docs.ipfs.tech/concepts/dnslink/)
16. IETF. (2013). DNS-Based Service Discovery. RFC 6763. Retrieved \[15 jan 2024\] from [https://www.ietf.org/rfc/rfc6763.txt](https://www.ietf.org/rfc/rfc6763.txt)
17. IPFS. (n.d.). IPFS Gateway. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/ipfs-gateway/](https://docs.ipfs.tech/concepts/ipfs-gateway/)
18. IPLD. (n.d.). Retrieved \[15 jan 2024\], from [https://ipld.io/](https://ipld.io/)
19. IPLD. (n.d.). Primer. In IPLD Documentation. Retrieved \[15 jan 2024\], from [https://ipld.io/docs/intro/primer/](https://ipld.io/docs/intro/primer/)
20. IPFS. (n.d.). IPNS (InterPlanetary Name System). In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/ipns/](https://docs.ipfs.tech/concepts/ipns/)
21. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 2). Kharkiv: PROMART. (pp. 33-44). Web of trust
22. IPFS. (n.d.). MerkleDag. In IPFS Documentation. Retrieved \[15 jan 2024\], from [https://docs.ipfs.tech/concepts/merkle-dag/](https://docs.ipfs.tech/concepts/merkle-dag/
23. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 2). Kharkiv: PROMART. (pp. 83-89). Merkle Tree
24. Protocol Labs. (2017). Filecoin: A Decentralized Storage Network. Retrieved from [https://filecoin.io/filecoin.pdf](https://filecoin.io/filecoin.pdf)
25. Filecoin Project. (n.d.). Algorithms: Proof-of-Space. In Filecoin Specification. Retrieved \[15 jan 2024\], from [https://spec.filecoin.io/#section-algorithms.pos](https://spec.filecoin.io/#section-algorithms.pos)
26. Filecoin Project. (n.d.). How Storage Works. In Filecoin Documentation. Retrieved \[15 jan 2024\], from [https://docs.filecoin.io/basics/how-storage-works](https://docs.filecoin.io/basics/how-storage-works)
27. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 1). Kharkiv: PROMART. (pp. 270-280). Merkle Tree
28. Filecoin Project. (n.d.). Proof-of-Space (PoS) Algorithm. In Filecoin Specification. Retrieved \[15 jan 2024\], from [https://spec.filecoin.io/algorithms/pos/](https://spec.filecoin.io/algorithms/pos/)
29. Filecoin Project. (n.d.). Proof-of-Space-Time (PoST) Algorithm. In Filecoin Specification. Retrieved \[15 jan 2024\], from [https://spec.filecoin.io/algorithms/pos/post/](https://spec.filecoin.io/algorithms/pos/post/)
30. Kravchenko, P., Skriabin, B., Kurbatov, O., Dubinina, O. (2019). Blockchain and decentralized systems: In three volumes (Vol. 2). Kharkiv: PROMART. (pp. 323-335). zkSNARKs
31. Filecoin Project. (n.d.). Proof-of-Replication (PoRep) Algorithm. In Filecoin Specification. Retrieved \[15 jan 2024\], from [https://spec.filecoin.io/algorithms/pos/porep/](https://spec.filecoin.io/algorithms/pos/porep/)
32. Filecoin Project. (n.d.). Filecoin VM (FVM). Retrieved \[15 jan 2024\], from [https://fvm.filecoin.io/](https://fvm.filecoin.io/)
