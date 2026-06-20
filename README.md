<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Запоминаем препараты по патологии</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            padding: 30px;
            max-width: 900px;
            width: 100%;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 25px 50px rgba(0,0,0,0.5);
        }
        h1 {
            text-align: center;
            color: #fff;
            font-size: 2em;
            margin-bottom: 10px;
            text-shadow: 0 0 20px rgba(100, 100, 255, 0.5);
        }
        .subtitle {
            text-align: center;
            color: #aaa;
            margin-bottom: 25px;
            font-size: 0.95em;
        }
        .stats {
            display: flex;
            justify-content: space-between;
            background: rgba(255,255,255,0.08);
            border-radius: 15px;
            padding: 12px 20px;
            margin-bottom: 20px;
            color: #fff;
            font-size: 0.95em;
        }
        .stats span {
            color: #8af;
        }
        .card-area {
            background: rgba(0,0,0,0.4);
            border-radius: 20px;
            padding: 30px 20px;
            margin-bottom: 20px;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }
        .card-area:hover {
            border-color: rgba(100, 150, 255, 0.4);
        }
        .card-number {
            color: #88aaff;
            font-size: 0.85em;
            margin-bottom: 10px;
            letter-spacing: 2px;
        }
        .card-name {
            color: #fff;
            font-size: 1.8em;
            font-weight: 600;
            text-align: center;
            line-height: 1.3;
            margin-bottom: 5px;
        }
        .card-desc {
            color: #9ab;
            font-size: 0.95em;
            text-align: center;
            max-width: 600px;
            line-height: 1.5;
            margin-top: 10px;
        }
        .card-hint {
            color: #ffcc66;
            font-size: 0.85em;
            margin-top: 15px;
            font-style: italic;
        }
        .flip-hint {
            color: #667;
            font-size: 0.8em;
            margin-top: 8px;
        }
        .mode-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 20px;
        }
        .mode-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.9em;
            font-weight: 500;
            transition: all 0.3s;
            background: rgba(255,255,255,0.1);
            color: #ccc;
        }
        .mode-btn:hover {
            background: rgba(255,255,255,0.2);
            transform: translateY(-2px);
        }
        .mode-btn.active {
            background: #4a7aff;
            color: #fff;
            box-shadow: 0 4px 15px rgba(74, 122, 255, 0.4);
        }
        .controls {
            display: flex;
          justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-top: 5px;
        }
        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 500;
            transition: all 0.3s;
        }
        .btn-primary {
            background: linear-gradient(135deg, #4a7aff, #6c5ce7);
            color: #fff;
            box-shadow: 0 4px 15px rgba(74, 122, 255, 0.3);
        }
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 122, 255, 0.5);
        }
        .btn-secondary {
            background: rgba(255,255,255,0.1);
            color: #ddd;
            border: 1px solid rgba(255,255,255,0.15);
        }
        .btn-secondary:hover {
            background: rgba(255,255,255,0.2);
            transform: translateY(-2px);
        }
        .btn-success {
            background: linear-gradient(135deg, #00b894, #00cec9);
            color: #fff;
        }
        .btn-success:hover {
            transform: translateY(-2px);
        }
        .btn-danger {
            background: linear-gradient(135deg, #e17055, #d63031);
            color: #fff;
        }
        .btn-danger:hover {
            transform: translateY(-2px);
        }
        .progress-bar {
            width: 100%;
            height: 6px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 20px;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4a7aff, #6c5ce7);
            border-radius: 10px;
            transition: width 0.4s ease;
            width: 0%;
        }
        .input-group {
            display: flex;
            gap: 10px;
            width: 100%;
            max-width: 500px;
            margin: 10px auto;
        }
        .input-group input {
            flex: 1;
            padding: 12px 15px;
            border-radius: 12px;
            border: 1px solid rgba(255,255,255,0.2);
            background: rgba(255,255,255,0.08);
            color: #fff;
            font-size: 1em;
            outline: none;
        }
        .input-group input:focus {
            border-color: #4a7aff;
        }
        .input-group input::placeholder {
            color: #667;
        }
        .result-msg {
            text-align: center;
            font-size: 1.1em;
            margin-top: 8px;
            min-height: 30px;
        }
        .correct { color: #00b894; }
        .wrong { color: #e17055; }
        .hidden { display: none; }
        .finish-screen {
            text-align: center;
            color: #fff;
            padding: 30px;
        }
        .finish-screen h2 {
            font-size: 2em;
            margin-bottom: 10px;
        }
        .finish-screen .score {
            font-size: 3em;
            font-weight: bold;
            color: #ffcc66;
            margin: 15px 0;
        }
        @media (max-width: 600px) {
            .container { padding: 15px; }
            .card-name { font-size: 1.3em; }
            .stats { flex-direction: column; gap: 5px; }
        }
    </style>
</head>
<body>
<div class="container" id="app">
    <h1>🧬 Патология: запоминаем препараты</h1>
    <p class="subtitle">Нажимайте на карточку, чтобы перевернуть её. Проверьте себя!</p>

    <div class="stats">
        <div>📊 Изучено: <span id="studied">0</span>/<span id="total">0</span></div>
        <div>✅ Правильно: <span id="correct">0</span></div>
        <div>❌ Неправильно: <span id="wrong">0</span></div>
        <div>🔥 Серия: <span id="streak">0</span></div>
    </div>

    <div class="progress-bar">
        <div class="progress-fill" id="progressFill"></div>
    </div>
    <div class="mode-buttons">
        <button class="mode-btn active" data-mode="study" onclick="setMode('study')">📖 Изучение</button>
        <button class="mode-btn" data-mode="quiz" onclick="setMode('quiz')">✍️ Проверка</button>
        <button class="mode-btn" data-mode="mix" onclick="setMode('mix')">🔀 Вперемешку</button>
    </div>

    <div class="card-area" id="cardArea" onclick="handleCardClick()">
        <div class="card-number" id="cardNumber">№ --</div>
        <div class="card-name" id="cardName">Нажмите "Начать"</div>
        <div class="card-desc hidden" id="cardDesc"></div>
        <div class="card-hint hidden" id="cardHint">🔄 Нажмите, чтобы перевернуть</div>
        <div class="flip-hint" id="flipHint"></div>
    </div>

    <div id="quizSection" class="hidden">
        <div class="input-group">
            <input type="text" id="answerInput" placeholder="Введите название препарата..." onkeydown="if(event.key==='Enter') checkAnswer()">
            <button class="btn btn-success" onclick="checkAnswer()">✓ Ответ</button>
        </div>
        <div class="result-msg" id="resultMsg"></div>
    </div>

    <div class="controls">
        <button class="btn btn-primary" id="startBtn" onclick="startGame()">▶ Начать</button>
        <button class="btn btn-secondary" id="nextBtn" onclick="nextCard()">➡ Следующий</button>
        <button class="btn btn-secondary" id="shuffleBtn" onclick="shuffleCards()">🔀 Перемешать</button>
        <button class="btn btn-danger" id="resetBtn" onclick="resetGame()">🔄 Сброс</button>
    </div>
</div>

<script>
    // Все препараты из файла
    const ALL_CARDS = [
        { id: 1, name: "Амилоидоз печени", desc: "Отложение амилоида между стенкой синусоидного капилляра и гепатоцитами. Метахромазия." },
        { id: 2, name: "Амилоидоз почки", desc: "Отложение амилоида в сосудистом клубочке, склероз стромы, отложение в стенках канальцев." },
        { id: 3, name: "Бурая индурация легких", desc: "На фоне хронического венозного полнокровия — кровоизлияния, гемосидерин (сидерофаги)." },
        { id: 4, name: "Гиалиноз стенки артерий", desc: "Гладкомышечная стенка замещена плотным белковым веществом, просвет сужен." },
        { id: 5, name: "Гиперкератоз", desc: "Избыточное ороговение (утолщение рогового слоя), чешуйки." },
        { id: 6, name: "Гиалиноз клубочков почки", desc: "Белковые зерна в гепатоцитах, напоминают гиалиновый хрящ. Необратим." },
        { id: 7, name: "Лейкоплакия", desc: "Ороговение неороговевающего многослойного плоского эпителия." },
        { id: 8, name: "Лейкоплакия языка", desc: "Ороговение эпителия языка — белое пятно." },
        { id: 9, name: "Меланоз кожи", desc: "Накопление зерен меланина в клетках базального слоя эпителия." },
        { id: 10, name: "Гемохроматоз", desc: "Отложение пигмента в коже и слизистых оболочках." },
        { id: 11, name: "Подагра", desc: "Отложение солей мочевой кислоты в области мелких суставов и сухожилий." },
        { id: 12, name: "Гидропическая дистрофия печени", desc: "Вакуольная дистрофия — разрушение органелл, крупная вакуоль." },
        { id: 13, name: "Жировая дистрофия печени", desc: "Жировые включения в гепатоцитах (мелкокапельное и крупнокапельное ожирение)." },
        { id: 14, name: "Липидоз аорты", desc: "Пропитывание стенки аорты липопротеидами низкой плотности (атеросклероз)." },
        { id: 15, name: "Ложная гипертрофия мышцы", desc: "Мышца увеличена за счет разрастания жировой ткани в строме." },
        { id: 16, name: "Аденовирусная пневмония", desc: "Альвеолоциты увеличены, с крупным гиперхромным ядром (ДНК-вирус)." },
        { id: 17, name: "Бронхиальная астма", desc: "Гипертрофия и спазм мышечной стенки бронхиолы, густая слизь." },
        { id: 18, name: "Бронхоэктаз", desc: "Истончение и растяжение стенки бронха, деформация, слизь и экссудат." },
[21/06/2026 01:32] Жад: { id: 19, name: "Бронхопневмония", desc: "Гнойный экссудат в просвете бронхов, полнокровие." },
        { id: 20, name: "Эмфизема легкого", desc: "Значительное расширение альвеол, разрушение перегородок." },
        { id: 21, name: "Гриппозная пневмония", desc: "Жидкость с белком в альвеоле, атипичные клетки, кровоизлияния." },
        { id: 22, name: "Слизистая гиперплазия стенки бронха", desc: "Много слизистых желез и бокаловидных клеток (хронический бронхит)." },
        { id: 23, name: "Карнификация легкого", desc: "Фибрин заменяется соединительной тканью (организация)." },
        { id: 24, name: "Крупозная пневмония (стадия серого опеченения)", desc: "Истонченные межальвеолярные перегородки, гнойный экссудат." },
        { id: 25, name: "Крупозная (долевая) пневмония", desc: "Поражение верхней доли правого легкого, белые разрастания." },
        { id: 26, name: "Туберкулезная гранулема в легком", desc: "Некроз в центре, эпителиоидные клетки, гигантские клетки Лангханса." },
        { id: 27, name: "Казеозная пневмония", desc: "Обширный очаг некроза с воспалительной инфильтрацией." },
        { id: 28, name: "Первичный туберкулезный комплекс", desc: "Субплевральный очаг + лимфаденит + лимфангит." },
        { id: 29, name: "Кавернозный туберкулез", desc: "Каверна (полость некроза) с дренирующим бронхом." },
        { id: 30, name: "Туберкулезный менингит", desc: "Специфическое воспаление с некрозом и гигантскими клетками." },
        { id: 31, name: "Туберкулезный спондилит", desc: "Поражение тел позвонков, специфическое воспаление с некрозом." },
        { id: 32, name: "Флегмонозный аппендицит", desc: "Гнойная инфильтрация всех слоев червеобразного отростка." },
        { id: 33, name: "Аппендицит с перфорацией", desc: "Дефект стенки отростка, фибринозные наложения (перитонит)." },
        { id: 34, name: "Мозговидное набухание пейеровой бляшки", desc: "Лимфоидная ткань с макрофагами (брюшной тиф)." },
        { id: 35, name: "Билиарный цирроз печени", desc: "Застой желчи, портальный цирроз, широкие прослойки соединительной ткани." },
        { id: 36, name: "Смешанный (крупно-мелкоузловой) цирроз печени", desc: "Сморщенная печень, узловая перестройка." },
        { id: 37, name: "Дифтеритический колит (дизентерия)", desc: "Фибринозное воспаление, некроз слизистой, фибрин на поверхности." },
        { id: 38, name: "Эксикоз", desc: "Обезвоживание организма, сухость кожи, снижение тургора." },
        { id: 39, name: "Эрозия желудка", desc: "Дефект (некроз) не выходит за пределы слизистой оболочки." },
        { id: 40, name: "Вирусный гепатит", desc: "Некротическая форма (HBV), обширные некрозы, лимфо-макрофагальная инфильтрация." },
        { id: 41, name: "Камни желчного пузыря", desc: "Камни, пролежни, закупорка общего желчного протока." },
        { id: 42, name: "Кандидоз кишечника", desc: "Разрастание мицелия грибов Candida в слизистой оболочке." },
        { id: 43, name: "\"Голова медузы\"", desc: "Симптом портальной гипертензии (цирроз печени)." },
        { id: 44, name: "Язва желудка", desc: "Некроз, фиброз в стенке и дне язвы." },
        { id: 45, name: "Акцидентальная инволюция тимуса", desc: "Уменьшение дольки, снижение лимфоцитов, широкие прослойки соединительной ткани." },
        { id: 46, name: "Первичный иммунодефицит", desc: "Дольки уменьшены, неправильной формы, тельца отсутствуют." },
        { id: 47, name: "Дифтерия гортани", desc: "Фибринозная пленка, полнокровие, воспалительная инфильтрация." },
        { id: 48, name: "\"Тигровое\" сердце", desc: "Токсическая дистрофия миокарда при дифтерии (жир в виде полос)." },
        { id: 49, name: "Герпетические пузырьки", desc: "Вирусное поражение кожи при герпесе, баллонная дистрофия." },
        { id: 50, name: "Гумма печени", desc: "Сифилитическая гранулема: зона некроза, вал из эпителиоидных клеток." },
        { id: 51, name: "Септический очаг в миокарде", desc: "Гнойный экссудат, колонии микробов (септикопиемия)." },
        { id: 52, name: "Тканевая эмболия", desc: "Комплекс опухолевых клеток в просвете сосудов." },
        { id: 53, name: "Жировая эмболия сосудов легкого", desc: "Капли жира закупоривают мелкие сосуды (окраска судан III)." },
        { id: 54, name: "Воздушная эмболия", desc: "Пузырьки воздуха в сосудах." },
        { id: 55, name: "Инфаркт легкого", desc: "Зона геморрагического инфаркта, перифокальное воспаление." },
        { id: 56, name: "Кровоизлияние в мозг", desc: "Геморрагическое пропитывание ткани (гематома)." },
        { id: 57, name: "\"Мускатная\" печень", desc: "Выраженное полнокровие центральных вен (хронический венозный застой)." },
        { id: 58, name: "Слоновость", desc: "Разрастание соединительной ткани на фоне хронического лимфостаза." },
        { id: 59, name: "Стаз крови", desc: "Остановка кровотока в капилляре, эритроциты склеены." },
        { id: 60, name: "Тромбоз в артерии", desc: "Организация тромба, реканализация." },
        { id: 61, name: "Тромбоэмболия легочной артерии", desc: "Тромб в легочной артерии." },
        { id: 62, name: "Гангрена кишечника", desc: "Тромбоз брыжеечной артерии, некроз участка кишки." },
        { id: 63, name: "Казеозный некроз с эпителиоидными клетками", desc: "Коагуляционный некроз, эпителиоидные и гигантские клетки." },
        { id: 64, name: "Колликвационный некроз", desc: "Размягчение ткани (гнойное расплавление)." },
        { id: 65, name: "Остеомиелит кости", desc: "Гнойное воспаление в кости и мягких тканях, секвестр." },
        { id: 66, name: "Гнойный менингит", desc: "Диффузное гнойное воспаление в мягкой мозговой оболочке." },
        { id: 67, name: "Менингококкемия", desc: "Гнойное воспаление, кровоизлияния в надпочечники." },
        { id: 68, name: "Полиомиелит", desc: "Воспаление серого вещества спинного мозга, лимфоцитарная инфильтрация." },
        { id: 69, name: "Аденома простаты", desc: "Доброкачественная опухоль из железистой ткани, гипертрофия стенки мочевого пузыря." },
        { id: 70, name: "Папиллома", desc: "Доброкачественная опухоль из многослойного плоского эпителия." },
        { id: 71, name: "Carcinoma in situ (рак на месте)", desc: "Злокачественная опухоль без инвазии." },
        { id: 72, name: "Фиброма", desc: "Доброкачественная опухоль из соединительной ткани." },
        { id: 73, name: "Фиброаденома молочной железы", desc: "Сложная опухоль из соединительной ткани и секреторных отделов." },
        { id: 74, name: "Капиллярная гемангиома", desc: "Доброкачественная опухоль из мелких кровеносных сосудов." },
        { id: 75, name: "Гемангиома", desc: "Доброкачественная опухоль из кровеносных сосудов (капиллярная/кавернозная)." },
        { id: 76, name: "Ганглионеврома", desc: "Доброкачественная опухоль из нейронов нервного сплетения." },
        { id: 77, name: "Мезентериальная липосаркома", desc: "Злокачественная опухоль из жировой ткани брыжейки." },
        { id: 78, name: "Лимфогранулематоз", desc: "Лакунарная клетка (Рид-Штернберга) в лимфоузле." },
        { id: 79, name: "Лейкоз", desc: "Опухоль кроветворной ткани, бластные клетки в сосудах." },
        { id: 80, name: "Меланома", desc: "Злокачественная опухоль из меланоцитов, много пигмента." },
        { id: 81, name: "Метастаз аденокарциномы в лимфоузел", desc: "Ткань лимфоузла замещена опухолевым эпителием." },
        { id: 82, name: "Острый мегакариобластный лейкоз", desc: "Злокачественная опухоль из мегакариобластов." },
        { id: 83, name: "Аденома надпочечника", desc: "Доброкачественная гормонально-активная опухоль." },
        { id: 84, name: "Неврофиброма \"Конского хвоста\"", desc: "Сложная опухоль из фибромы и оболочек спинно-мозговых нервов." },
        { id: 85, name: "Гепатоцеллюлярный рак печени", desc: "Злокачественная опухоль из гепатоцитов." },
        { id: 86, name: "Перстневидноклеточный (слизистый) рак", desc: "Клетки с вакуолью слизи, ядро на периферии." },
        { id: 87, name: "Плоскоклеточный рак с ороговением", desc: "Злокачественная опухоль из эпителия с \"жемчужинами\"." },
        { id: 88, name: "Тератома", desc: "Опухоль из эмбриональных тканей." },
        { id: 89, name: "Опухоль Крукенберга", desc: "Метастаз в яичник (перстневидные клетки)." },
        { id: 90, name: "Острая почечная недостаточность", desc: "Некротический нефроз (некроз канальцев)." },
        { id: 91, name: "Инфаркт почки", desc: "Ишемический инфаркт, клиновидная зона некроза." },
        { id: 92, name: "Постстрептококковый гломерулонефрит", desc: "Инфекционно-аллергическое заболевание, \"горбы\"." },
        { id: 93, name: "Пиелонефрит", desc: "Инфекционное заболевание, гной в канальцах, воспаление стромы." },
        { id: 94, name: "Аневризма левого желудочка", desc: "Выпячивание стенки сердца с разрывом." },
        { id: 95, name: "Атеросклероз аорты", desc: "Липоидоз, липосклероз, атероматоз, атерокальциноз." },
        { id: 96, name: "Инфаркт миокарда", desc: "Разрушенные кардиомиоциты, макрофаги." },
        { id: 97, name: "Постинфарктный кардиосклероз", desc: "Рубцовая ткань вместо некроза, гипертрофия миокарда." },
        { id: 98, name: "Бородавчатый эндокардит", desc: "Тромботические наложения на эндокарде (ревматизм)." },
        { id: 99, name: "Межуточный экссудативный миокардит", desc: "Отек и лимфоцитарная инфильтрация, дистрофия кардиомиоцитов." },
        { id: 100, name: "Гранулематозный миокардит (ревматический)", desc: "Гранулемы в соединительной ткани (ревматизм)." }
    ];

    let cards = [];
    let currentIndex = 0;
    let isFlipped = false;
    let mode = 'study';
    let studied = new Set();
    let correctCount = 0;
    let wrongCount = 0;
    let streak = 0;
    let isGameStarted = false;

    const $ = id => document.getElementById(id);

    function shuffle(arr) {
        for (let i = arr.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        return arr;
    }

    function shuffleCards() {
        if (!isGameStarted) return;
        shuffle(cards);
        currentIndex = 0;
        isFlipped = false;
        updateDisplay();
    }

    function startGame() {
        cards = [...ALL_CARDS];
        shuffle(cards);
        currentIndex = 0;
        isFlipped = false;
        isGameStarted = true;
        $('startBtn').textContent = '▶ Игра начата';
        $('startBtn').style.opacity = '0.6';
        updateDisplay();
        updateStats();
        $('flipHint').textContent = '👆 Нажмите на карточку, чтобы увидеть описание';
    }

    function setMode(newMode) {
        mode = newMode;
        document.querySelectorAll('.mode-btn').forEach(b => b.classList.remove('active'));
        document.querySelector([data-mode="${newMode}"]).classList.add('active');
        
        if (newMode === 'quiz') {
            $('quizSection').classList.remove('hidden');
            $('cardHint').classList.remove('hidden');
            $('cardHint').textContent = '✍️ Вспомните название и введите его в поле';
        } else {
            $('quizSection').classList.add('hidden');
            $('cardHint').classList.add('hidden');
        }
        
        if (isGameStarted) updateDisplay();
    }

    function handleCardClick() {
        if (!isGameStarted) {
            startGame();
            return;
        }
        if (!isFlipped) {
            isFlipped = true;
            if (mode !== 'quiz') {
                $('cardHint').classList.remove('hidden');
                $('cardHint').textContent = 📝 ${cards[currentIndex].desc};
            }
            updateDisplay();
            if (mode === 'study') {
                studied.add(cards[currentIndex].id);
                updateStats();
            }
        }
    }
[21/06/2026 01:32] Жад: function nextCard() {
        if (!isGameStarted || cards.length === 0) return;
        if (mode === 'mix') {
            // Берём случайную карточку
            currentIndex = Math.floor(Math.random() * cards.length);
        } else {
            currentIndex = (currentIndex + 1) % cards.length;
        }
        isFlipped = false;
        $('resultMsg').textContent = '';
        $('answerInput').value = '';
        $('cardHint').classList.add('hidden');
        updateDisplay();
    }

    function checkAnswer() {
        if (mode !== 'quiz' || !isGameStarted) return;
        const input = $('answerInput').value.trim().toLowerCase();
        const currentName = cards[currentIndex].name.toLowerCase();
        
        if (!input) {
            $('resultMsg').innerHTML = '✏️ Введите название!';
            $('resultMsg').className = 'result-msg wrong';
            return;
        }

        // Проверка: точное совпадение или частичное
        const isCorrect = input === currentName || 
                          currentName.includes(input) || 
                          input.includes(currentName) ||
