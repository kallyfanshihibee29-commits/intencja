<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dyskretna Intencja</title>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            box-sizing: border-box;
        }
        
        :root {
            --bg: #9fc6e2;
            --bg2: #cfe8f8;
            --navy: #1e3a8a;
            --quote-grad-start: #3b5998;
            --quote-grad-end: #5a8dee;
            --point-blue: #2b7bd6;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            height: 100%;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(180deg, var(--bg) 0%, var(--bg2) 100%);
            min-height: 100%;
            padding: 20px;
            color: var(--navy);
            overflow-x: hidden;
        }

        .back-arrow {
            position: fixed;
            top: 30px;
            left: 30px;
            z-index: 1000;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 50%;
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px rgba(6,21,52,0.15);
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            animation: slideInLeft 0.8s ease-out;
        }

        .back-arrow:hover {
            transform: scale(1.1);
            box-shadow: 0 6px 16px rgba(6,21,52,0.25);
        }

        .back-arrow svg {
            width: 24px;
            height: 24px;
            fill: var(--navy);
        }

        @keyframes slideInLeft {
            from {
                transform: translateX(-100px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        @keyframes slideInRight {
            from {
                transform: translateX(100px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        .container {
            max-width: 500px;
            margin: 0 auto;
            padding: 0 20px;
            animation: slideInRight 1s ease-out;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .title {
            font-family: 'Pacifico', cursive;
            font-size: 2.5rem;
            color: var(--navy);
            margin-bottom: 10px;
            text-shadow: 0 2px 4px rgba(6,21,52,0.12);
        }

        .subtitle {
            font-size: 1rem;
            color: var(--navy);
            opacity: 0.8;
            font-weight: 400;
        }

        .card {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 16px;
            padding: 30px;
            margin-bottom: 25px;
            box-shadow: 
                0 4px 12px rgba(6,21,52,0.12),
                0 2px 6px rgba(59,89,152,0.12);
            backdrop-filter: blur(10px);
        }

        .status-section {
            text-align: center;
            margin-bottom: 30px;
        }

        .status-title {
            font-weight: 700;
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: var(--navy);
        }

        .countdown {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--point-blue);
            margin-bottom: 20px;
        }

        .streak-section {
            margin-bottom: 20px;
        }

        .streak-message {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--point-blue);
            background: rgba(43, 123, 214, 0.1);
            padding: 12px 20px;
            border-radius: 8px;
            border: 2px solid rgba(43, 123, 214, 0.2);
            text-align: center;
            animation: streakGlow 2s ease-in-out infinite alternate;
            transition: all 0.3s ease;
        }

        .streak-message.title-border {
            border: 3px solid var(--title-color);
            box-shadow: 0 0 15px var(--title-glow);
            background: var(--title-bg);
        }

        @keyframes streakGlow {
            from {
                box-shadow: 0 0 5px rgba(43, 123, 214, 0.3);
            }
            to {
                box-shadow: 0 0 15px rgba(43, 123, 214, 0.5);
            }
        }

        .current-title {
            font-size: 1.3rem;
            font-weight: 700;
            text-align: center;
            margin-top: 15px;
            padding: 10px 20px;
            border-radius: 8px;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .draw-button {
            background: linear-gradient(135deg, var(--quote-grad-start) 0%, var(--quote-grad-end) 100%);
            color: white;
            border: 3px solid transparent;
            padding: 15px 30px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 12px rgba(59,89,152,0.3);
            font-family: 'Roboto', sans-serif;
        }

        .draw-button.title-border {
            border: 3px solid var(--title-color);
            box-shadow: 0 4px 12px rgba(59,89,152,0.3), 0 0 15px var(--title-glow);
        }

        .draw-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(59,89,152,0.4);
        }

        .draw-button.title-border:hover {
            box-shadow: 0 6px 16px rgba(59,89,152,0.4), 0 0 20px var(--title-glow);
        }

        .draw-button:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .titles-button {
            background: linear-gradient(135deg, var(--quote-grad-start) 0%, var(--quote-grad-end) 100%);
            color: white;
            border: 3px solid transparent;
            padding: 15px 30px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 12px rgba(59,89,152,0.3);
            font-family: 'Roboto', sans-serif;
            width: 100%;
            text-align: center;
        }

        .titles-button.title-border {
            border: 3px solid var(--title-color);
            box-shadow: 0 4px 12px rgba(59,89,152,0.3), 0 0 15px var(--title-glow);
        }

        .titles-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(59,89,152,0.4);
        }

        .titles-button.title-border:hover {
            box-shadow: 0 6px 16px rgba(59,89,152,0.4), 0 0 20px var(--title-glow);
        }

        .result-section {
            margin-top: 30px;
        }

        .result-card {
            background: linear-gradient(135deg, var(--quote-grad-start) 0%, var(--quote-grad-end) 100%);
            color: white;
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 20px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(59,89,152,0.3);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.5s ease;
            border: 3px solid transparent;
        }



        .result-card.show {
            opacity: 1;
            transform: translateY(0);
        }

        .result-title {
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .result-content {
            font-size: 1.2rem;
            line-height: 1.4;
            font-weight: 400;
        }

        .drawing-animation {
            background: linear-gradient(135deg, var(--quote-grad-start) 0%, var(--quote-grad-end) 100%);
            color: white;
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 20px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(59,89,152,0.3);
        }

        .drawing-text {
            font-size: 1.2rem;
            font-weight: 700;
            animation: pulse 0.5s infinite alternate;
        }

        @keyframes pulse {
            from { opacity: 0.7; }
            to { opacity: 1; }
        }

        .icon {
            width: 24px;
            height: 24px;
            background: var(--point-blue);
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: 700;
            font-size: 14px;
        }

        .history-section {
            margin-top: 30px;
        }

        .history-title {
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: var(--navy);
        }

        .history-item {
            background: rgba(255, 255, 255, 0.7);
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 10px;
            border-left: 4px solid var(--point-blue);
        }

        .history-date {
            font-size: 0.9rem;
            color: var(--navy);
            opacity: 0.7;
            margin-bottom: 5px;
        }

        .history-content {
            font-size: 0.95rem;
            line-height: 1.3;
        }

        .titles-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 10000;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }

        .titles-modal.show {
            opacity: 1;
            visibility: visible;
        }

        .titles-content {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 16px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            max-height: 80%;
            overflow-y: auto;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            transform: scale(0.8);
            transition: transform 0.3s ease;
        }

        .titles-modal.show .titles-content {
            transform: scale(1);
        }

        .titles-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .titles-header h2 {
            font-family: 'Pacifico', cursive;
            font-size: 2rem;
            color: var(--navy);
            margin-bottom: 10px;
        }

        .titles-subtitle {
            color: var(--navy);
            opacity: 0.8;
        }

        .title-card {
            background: rgba(255, 255, 255, 0.8);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 15px;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .title-card.unlocked {
            border: 2px solid rgba(34, 197, 94, 0.5);
            box-shadow: 0 4px 12px rgba(34, 197, 94, 0.2);
        }

        .title-card.locked {
            opacity: 0.6;
        }

        .title-name {
            font-weight: 700;
            font-size: 1.2rem;
            margin-bottom: 8px;
            background: var(--gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .title-icon {
            width: 32px;
            height: 32px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }

        .title-icon img {
            width: 24px;
            height: 24px;
            object-fit: cover;
            border-radius: 3px;
        }

        .title-requirement {
            font-size: 0.9rem;
            color: var(--navy);
            opacity: 0.7;
            margin-bottom: 10px;
        }

        .title-progress {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            height: 8px;
            overflow: hidden;
            margin-bottom: 10px;
        }

        .title-progress-bar {
            height: 100%;
            background: var(--gradient);
            transition: width 0.3s ease;
            border-radius: 8px;
        }

        .title-status {
            font-weight: 700;
            font-size: 0.9rem;
        }

        .title-status.unlocked {
            color: #22c55e;
        }

        .title-status.locked {
            color: #6b7280;
        }

        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--navy);
            opacity: 0.7;
            transition: opacity 0.3s ease;
        }

        .close-modal:hover {
            opacity: 1;
        }



        @keyframes titlePop {
            0% {
                transform: translate(-50%, -50%) scale(0.5);
                opacity: 0;
            }
            20% {
                transform: translate(-50%, -50%) scale(1.1);
                opacity: 1;
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 0;
            }
        }

        @keyframes confettiFall {
            0% {
                transform: translateY(-10px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }

        @media (max-width: 480px) {
            .title {
                font-size: 2rem;
            }
            
            .card {
                padding: 20px;
            }
            
            .container {
                padding: 0 10px;
            }

            .titles-content {
                padding: 20px;
                width: 95%;
            }

            .titles-header h2 {
                font-size: 1.5rem;
            }


        }
    </style>
</head>
<body>
    <div class="back-arrow" onclick="window.open('https://blogwpg.my.canva.site/', '_blank')">
        <svg viewBox="0 0 24 24">
            <path d="M20 11H7.83l5.59-5.59L12 4l-8 8 8 8 1.41-1.41L7.83 13H20v-2z"/>
        </svg>
    </div>
    
    <div class="container">
        <div class="header">
            <h1 class="title">Dyskretna Intencja</h1>
            <p class="subtitle">Codzienna modlitwa i intencja o północy</p>
        </div>

        <div class="card">
            <div class="status-section">
                <div id="streakSection" class="streak-section" style="display: none;">
                    <div class="streak-message" id="streakMessage"></div>
                    <div class="current-title" id="currentTitle" style="display: none;"></div>
                </div>
                <div id="countdownSection" class="countdown-section" style="display: none;">
                    <div class="status-title">Następne losowanie za:</div>
                    <div class="countdown" id="countdown">Ładowanie...</div>
                </div>
                <button class="draw-button" id="drawButton" onclick="startDrawing()">
                    Losuj intencję i modlitwę
                </button>
            </div>

            <div id="drawingArea"></div>
            <div id="resultsArea"></div>
        </div>

        <div class="card">
            <button class="titles-button" id="titlesButton" onclick="showTitlesModal()">
                🏆 Tytuły Dyskretniaka
            </button>
        </div>

        <div class="card history-section">
            <div class="history-title">Historia losowań</div>
            <div id="historyArea">
                <div class="history-item">
                    <div class="history-date">Brak wcześniejszych losowań</div>
                    <div class="history-content">Rozpocznij swoje pierwsze losowanie!</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal tytułów -->
    <div class="titles-modal" id="titlesModal">
        <div class="titles-content">
            <button class="close-modal" onclick="hideTitlesModal()">×</button>
            <div class="titles-header">
                <h2>🏆 Tytuły Dyskretniaka</h2>
                <p class="titles-subtitle">Zdobywaj tytuły poprzez codzienną passę modlitwy!</p>
            </div>
            <div id="titlesContainer"></div>
        </div>
    </div>

    <script>
        const prayers = [
            "Zdrowaś Maryjo, łaski pełna, Pan z Tobą, błogosławiona jesteś między niewiastami i błogosławiony owoc żywota Twojego, Jezus. Święta Maryjo, Matko Boża, módl się za nami grzesznymi teraz i w godzinę śmierci naszej. Amen.",
            "Ojcze nasz, któryś jest w niebiesiech, święć się imię Twoje, przyjdź królestwo Twoje, bądź wola Twoja jako w niebie tak i na ziemi. Chleba naszego powszedniego daj nam dzisiaj i odpuść nam nasze winy, jako i my odpuszczamy naszym winowajcom, i nie wódź nas na pokuszenie, ale nas zbaw ode złego. Amen.",
            "Wierzę w Boga, Ojca wszechmogącego, Stworzyciela nieba i ziemi. I w Jezusa Chrystusa, Syna Jego jedynego, Pana naszego, który się począł z Ducha Świętego, narodził się z Maryi Panny, umęczony pod Ponckim Piłatem, ukrzyżowany, umarł i pogrzebany, zstąpił do piekieł, trzeciego dnia zmartwychwstał, wstąpił na niebiosa, siedzi po prawicy Boga Ojca wszechmogącego, stamtąd przyjdzie sądzić żywych i umarłych. Wierzę w Ducha Świętego, święty Kościół powszechny, świętych obcowanie, grzechów odpuszczenie, ciała zmartwychwstanie, żywot wieczny. Amen.",
            "Chwała Ojcu i Synowi, i Duchowi Świętemu, jako była na początku, teraz i zawsze, i na wieki wieków. Amen.",
            "Pod Twoją obronę uciekamy się, święta Boża Rodzicielko, naszymi prośbami nie gardź w potrzebach naszych, ale od wszelkich złych przygód wiecznie nas wybawiaj, Panno chwalebna i błogosławiona.",
            "Witaj, Królowo, Matko miłosierdzia, życie, słodyczy i nadziejo nasza, witaj! Do Ciebie wołamy, wygnańcy, synowie Ewy, do Ciebie wzdychamy, jęcząc i płacząc na tym łez padole.",
            "Pamiętaj, o najmiłosierniejsza Panno Maryjo, że nie słyszano od wieków, aby ktoś, do Twej świętej opieki się uciekający, Twojej pomocy się dopraszający, o Twoją przyczynę się błagający, był od Ciebie opuszczony.",
            "Aniele Boży, stróżu mój, ty zawsze przy mnie stój, rano, wieczór, we dnie, w nocy, bądź mi zawsze ku pomocy!",
            "Wieczne odpoczywanie racz im dać, Panie, a światłość wiekuista niechaj im świeci. Niech odpoczywają w pokoju. Amen.",
            "Jezu, ufam Tobie!",
            "Jezu miłosierny, miej litość nad nami i nad całym światem!",
            "Najświętsze Serce Jezusa, zmiłuj się nad nami!",
            "Niepokalane Serce Maryi, módl się za nami!",
            "Duchu Święty, przyjdź!",
            "Święty Józefie, módl się za nami!",
            "Królowo Polski, módl się za nami!",
            "Święty Boże, Święty mocny, Święty nieśmiertelny, zmiłuj się nad nami!",
            "Boże, bądź miłościw mnie grzesznemu!",
            "Panie Jezu Chryste, Synu Boga żywego, zmiłuj się nade mną grzesznym!",
            "Błogosławiony niech będzie Bóg w darach swoich!",
            "Błogosławiona niech będzie Najświętsza Maryja Panna!",
            "Magnificat: Wielbi dusza moja Pana i raduje się duch mój w Bogu, Zbawicielu moim.",
            "Anioł Pański zwiastował Pannie Maryi i poczęła z Ducha Świętego.",
            "Oto ja służebnica Pańska, niech mi się stanie według słowa Twego.",
            "A Słowo Ciałem się stało i mieszkało między nami.",
            "Kłaniamy Ci się, Panie Jezu Chryste, i błogosławimy Ciebie, żeś przez święty krzyż Twój świat odkupił.",
            "Ciebie, Boże, chwalimy, Ciebie, Panie, wyznajemy.",
            "Przyjdź, Stworzycielu Duchu, nasze umysły nawiedź, łaską napełnij serca, które sam stworzyłeś.",
            "Serce Jezusa, Syna Ojca Przedwiecznego, zmiłuj się nad nami!",
            "Za Jego bolesną mękę, miej miłosierdzie nad nami i nad całym światem!"
        ];

        const intentions = [
            "Za księdza proboszcza i wszystkich księży z naszej parafii",
            "Za losową osobę korzystającą z aplikacji Dyskretna Intencja",
            "Za dusze cierpiące w Czyśćcu",
            "Za pokój na świecie i w naszych sercach",
            "Za chorych i cierpiących w naszej wspólnocie",
            "Za jedność rodzin i małżeństw",
            "Za młodzież i ich przyszłość",
            "Za osoby samotne i opuszczone",
            "Za nawrócenie grzeszników",
            "Za kapłanów i osoby konsekrowane",
            "Za rodziców i dzieci",
            "Za bezrobotnych i potrzebujących",
            "Za pokój w rodzinach",
            "Za osoby w depresji i smutku",
            "Za misjonarzy na całym świecie",
            "Za papieża i hierarchię Kościoła",
            "Za osoby uzależnione i ich rodziny",
            "Za dzieci nienarodzonych",
            "Za osoby starsze i samotne",
            "Za jedność chrześcijan",
            "Za prześladowanych za wiarę",
            "Za osoby poszukujące Boga",
            "Za nauczycieli i wychowawców",
            "Za lekarzy i służbę zdrowia",
            "Za pokój między narodami",
            "Za ochronę środowiska naturalnego",
            "Za osoby w żałobie",
            "Za więźniów i ich rodziny",
            "Za osoby bezdomne",
            "Za wszystkich wiernych zmarłych"
        ];

        // Funkcja bezpiecznego ładowania danych z localStorage
        function loadData() {
            try {
                lastDrawDate = localStorage.getItem('lastDrawDate');
                todaysPrayer = localStorage.getItem('todaysPrayer');
                todaysIntention = localStorage.getItem('todaysIntention');
                const historyData = localStorage.getItem('drawHistory');
                drawHistory = historyData ? JSON.parse(historyData) : [];
                
                // Załaduj passę
                currentStreak = parseInt(localStorage.getItem('currentStreak') || '0');
                lastStreakDate = localStorage.getItem('lastStreakDate');
                
                // Załaduj zdobyte tytuły
                const unlockedTitlesData = localStorage.getItem('unlockedTitles');
                unlockedTitles = unlockedTitlesData ? JSON.parse(unlockedTitlesData) : [];
                
                // Sprawdź czy passa się nie zerwała (ale tylko jeśli minęło więcej niż 2 dni)
                checkStreakContinuity();
                
                console.log('Załadowane dane:', {
                    lastDrawDate,
                    todaysPrayer: todaysPrayer ? 'tak' : 'nie',
                    todaysIntention: todaysIntention ? 'tak' : 'nie',
                    historyLength: drawHistory.length,
                    currentStreak,
                    unlockedTitles: unlockedTitles.length
                });
            } catch (e) {
                console.log('Błąd ładowania danych:', e);
                drawHistory = [];
                currentStreak = 0;
                unlockedTitles = [];
            }
        }

        let lastDrawDate, todaysPrayer, todaysIntention, drawHistory, currentStreak, lastStreakDate, unlockedTitles;
        
        // Załaduj dane przy starcie
        loadData();

        function checkStreakContinuity() {
            if (!lastStreakDate) return;
            
            const today = new Date();
            const lastDate = new Date(lastStreakDate);
            const diffTime = Math.abs(today - lastDate);
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            
            // Jeśli minęło więcej niż 2 dni, zresetuj passę (dajemy 1 dzień tolerancji)
            if (diffDays > 2) {
                currentStreak = 0;
                console.log('Passa zresetowana - minęło więcej niż 48h');
            }
        }

        const titles = [
            { days: 5, name: "Nowicjusz", gradient: "linear-gradient(135deg, #22c55e, #16a34a)", borderColor: "#22c55e", glowColor: "rgba(34, 197, 94, 0.3)", icon: "zdjęcie_1.png", unlocked: false },
            { days: 10, name: "Uczeń Wytrwałości", gradient: "linear-gradient(135deg, #3b82f6, #1d4ed8)", borderColor: "#3b82f6", glowColor: "rgba(59, 130, 246, 0.3)", icon: "zdjęcie_2.png", unlocked: false },
            { days: 15, name: "Wytrwały Praktykant", gradient: "linear-gradient(135deg, #ec4899, #be185d)", borderColor: "#ec4899", glowColor: "rgba(236, 72, 153, 0.3)", icon: "zdjęcie_3.png", unlocked: false },
            { days: 20, name: "Ogarnięty Dyskretniak", gradient: "linear-gradient(135deg, #f97316, #ea580c)", borderColor: "#f97316", glowColor: "rgba(249, 115, 22, 0.3)", icon: "zdjęcie_4.png", unlocked: false },
            { days: 30, name: "Mistrz Rutyny", gradient: "linear-gradient(135deg, #8b5cf6, #7c3aed)", borderColor: "#8b5cf6", glowColor: "rgba(139, 92, 246, 0.3)", icon: "zdjęcie_5.png", unlocked: false },
            { days: 45, name: "Niepokonany", gradient: "linear-gradient(135deg, #ef4444, #dc2626)", borderColor: "#ef4444", glowColor: "rgba(239, 68, 68, 0.3)", icon: "zdjęcie_6.png", unlocked: false },
            { days: 60, name: "Legendarny Passy Dyskretniaka", gradient: "linear-gradient(135deg, #fbbf24, #f59e0b)", borderColor: "#fbbf24", glowColor: "rgba(251, 191, 36, 0.3)", icon: "zdjęcie_7.png", unlocked: false }
        ];

        function updateStreak() {
            const today = new Date().toDateString();
            const yesterday = new Date();
            yesterday.setDate(yesterday.getDate() - 1);
            const yesterdayStr = yesterday.toDateString();
            
            // Jeśli to pierwsze losowanie lub losowanie następnego dnia po poprzednim
            if (!lastStreakDate || lastStreakDate === yesterdayStr) {
                currentStreak++;
            } else if (lastStreakDate !== today) {
                // Jeśli była przerwa, zresetuj passę
                currentStreak = 1;
            }
            
            lastStreakDate = today;
            
            // Sprawdź czy odblokowano nowe tytuły
            checkNewTitles();
        }

        function checkNewTitles() {
            titles.forEach(title => {
                if (currentStreak >= title.days && !unlockedTitles.includes(title.name)) {
                    unlockedTitles.push(title.name);
                    showTitleUnlocked(title);
                }
            });
            
            // Aktualizuj wygląd przycisków po zdobyciu nowych tytułów
            updateDrawButton();
            updateTitlesButton();
            showStreak();
        }

        function showTitleUnlocked(title) {
            // Uruchom confetti w kolorze tytułu
            createConfetti(title.borderColor);
            
            // Pokaż powiadomienie o nowym tytule
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                background: ${title.gradient};
                color: white;
                padding: 20px 30px;
                border-radius: 12px;
                font-weight: 700;
                font-size: 1.2rem;
                z-index: 10000;
                box-shadow: 0 8px 32px rgba(0,0,0,0.3);
                animation: titlePop 3s ease-out forwards;
            `;
            notification.innerHTML = `🏆 Nowy tytuł odblokowany!<br>"${title.name}"`;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }

        function createConfetti(color) {
            const confettiCount = 50;
            const colors = [color, '#ffffff', '#ffd700']; // Główny kolor + biały + złoty
            
            for (let i = 0; i < confettiCount; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    const randomColor = colors[Math.floor(Math.random() * colors.length)];
                    
                    confetti.style.cssText = `
                        position: fixed;
                        width: 10px;
                        height: 10px;
                        background: ${randomColor};
                        top: -10px;
                        left: ${Math.random() * 100}%;
                        z-index: 9999;
                        border-radius: ${Math.random() > 0.5 ? '50%' : '0'};
                        animation: confettiFall ${2 + Math.random() * 3}s linear forwards;
                        transform: rotate(${Math.random() * 360}deg);
                    `;
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        confetti.remove();
                    }, 5000);
                }, i * 50);
            }
        }

        function getStreakMessage() {
            if (currentStreak === 0) return '';
            if (currentStreak === 1) return '🔥 Pierwszy dzień modlitwy!';
            if (currentStreak < 7) return `🔥 Passa: ${currentStreak} dni z rzędu!`;
            if (currentStreak < 30) return `🔥🔥 Świetna passa: ${currentStreak} dni!`;
            if (currentStreak < 100) return `🔥🔥🔥 Niesamowita passa: ${currentStreak} dni!`;
            return `🔥🔥🔥🔥 Legendarna passa: ${currentStreak} dni!`;
        }

        function updateCountdown() {
            const now = new Date();
            const tomorrow = new Date(now);
            tomorrow.setDate(tomorrow.getDate() + 1);
            tomorrow.setHours(0, 0, 0, 0);
            
            const timeLeft = tomorrow - now;
            
            const hours = Math.floor(timeLeft / (1000 * 60 * 60));
            const minutes = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((timeLeft % (1000 * 60)) / 1000);
            
            document.getElementById('countdown').textContent = 
                `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        function canDrawToday() {
            const today = new Date().toDateString();
            return lastDrawDate !== today;
        }

        function updateDrawButton() {
            const button = document.getElementById('drawButton');
            const highestTitle = getHighestUnlockedTitle();
            
            if (canDrawToday()) {
                button.disabled = false;
                button.textContent = 'Losuj intencję i modlitwę';
            } else {
                button.disabled = true;
                button.textContent = 'Już losowałeś dzisiaj';
            }
            
            if (highestTitle) {
                button.className = 'draw-button title-border';
                button.style.setProperty('--title-color', highestTitle.borderColor);
                button.style.setProperty('--title-glow', highestTitle.glowColor);
            } else {
                button.className = 'draw-button';
            }
        }

        function getHighestUnlockedTitle() {
            let highestTitle = null;
            titles.forEach(title => {
                if (unlockedTitles.includes(title.name)) {
                    if (!highestTitle || title.days > highestTitle.days) {
                        highestTitle = title;
                    }
                }
            });
            return highestTitle;
        }

        function showTodaysResults() {
            const today = new Date().toDateString();
            if (lastDrawDate === today && todaysPrayer && todaysIntention) {
                const resultsArea = document.getElementById('resultsArea');
                const highestTitle = getHighestUnlockedTitle();
                
                resultsArea.innerHTML = `
                    <div class="result-card show">
                        <div class="result-title">
                            <div class="icon">💝</div>
                            Dzisiejsza intencja
                        </div>
                        <div class="result-content">${todaysIntention}</div>
                    </div>
                    <div class="result-card show">
                        <div class="result-title">
                            <div class="icon">🙏</div>
                            Dzisiejsza modlitwa
                        </div>
                        <div class="result-content">${todaysPrayer}</div>
                    </div>
                `;
                showCountdown();
                showStreak();
            }
        }

        function showStreak() {
            const streakMessage = getStreakMessage();
            if (streakMessage) {
                const streakElement = document.getElementById('streakMessage');
                const titleElement = document.getElementById('currentTitle');
                const highestTitle = getHighestUnlockedTitle();
                
                document.getElementById('streakSection').style.display = 'block';
                streakElement.textContent = streakMessage;
                
                if (highestTitle) {
                    streakElement.className = 'streak-message title-border';
                    streakElement.style.setProperty('--title-color', highestTitle.borderColor);
                    streakElement.style.setProperty('--title-glow', highestTitle.glowColor);
                    streakElement.style.setProperty('--title-bg', highestTitle.borderColor + '15');
                    
                    // Pokaż aktualny tytuł
                    titleElement.textContent = highestTitle.name;
                    titleElement.style.background = highestTitle.gradient;
                    titleElement.style.webkitBackgroundClip = 'text';
                    titleElement.style.webkitTextFillColor = 'transparent';
                    titleElement.style.backgroundClip = 'text';
                    titleElement.style.display = 'block';
                } else {
                    streakElement.className = 'streak-message';
                    titleElement.style.display = 'none';
                }
            }
        }

        function showCountdown() {
            document.getElementById('countdownSection').style.display = 'block';
        }

        function startDrawing() {
            if (!canDrawToday()) {
                return;
            }

            const drawingArea = document.getElementById('drawingArea');
            const resultsArea = document.getElementById('resultsArea');
            
            resultsArea.innerHTML = '';
            
            // Najpierw losowanie intencji
            drawingArea.innerHTML = `
                <div class="drawing-animation">
                    <div class="drawing-text" id="drawingText">Losuję intencję...</div>
                </div>
            `;

            const intentionOptions = [...intentions];
            let intentionIndex = 0;
            const intentionInterval = setInterval(() => {
                document.getElementById('drawingText').textContent = intentionOptions[intentionIndex % intentionOptions.length];
                intentionIndex++;
            }, 100);

            setTimeout(() => {
                clearInterval(intentionInterval);
                const selectedIntention = intentions[Math.floor(Math.random() * intentions.length)];
                
                // Potem losowanie modlitwy
                drawingArea.innerHTML = `
                    <div class="drawing-animation">
                        <div class="drawing-text" id="drawingText2">Losuję modlitwę...</div>
                    </div>
                `;

                const prayerOptions = [...prayers];
                let prayerIndex = 0;
                const prayerInterval = setInterval(() => {
                    document.getElementById('drawingText2').textContent = prayerOptions[prayerIndex % prayerOptions.length];
                    prayerIndex++;
                }, 100);

                setTimeout(() => {
                    clearInterval(prayerInterval);
                    const selectedPrayer = prayers[Math.floor(Math.random() * prayers.length)];
                    
                    drawingArea.innerHTML = '';
                    
                    // Zapisz wyniki
                    const today = new Date().toDateString();
                    lastDrawDate = today;
                    todaysPrayer = selectedPrayer;
                    todaysIntention = selectedIntention;
                    
                    // Aktualizuj passę
                    updateStreak();
                    
                    // Dodaj do historii
                    drawHistory.unshift({
                        date: today,
                        prayer: selectedPrayer,
                        intention: selectedIntention,
                        streak: currentStreak
                    });
                    
                    if (drawHistory.length > 10) {
                        drawHistory = drawHistory.slice(0, 10);
                    }
                    
                    // Zapisz wszystko do localStorage
                    saveAllData();
                    
                    // Pokaż wyniki - najpierw intencja, potem modlitwa
                    const highestTitle = getHighestUnlockedTitle();
                    
                    resultsArea.innerHTML = `
                        <div class="result-card">
                            <div class="result-title">
                                <div class="icon">💝</div>
                                Twoja dzisiejsza intencja
                            </div>
                            <div class="result-content">${selectedIntention}</div>
                        </div>
                        <div class="result-card">
                            <div class="result-title">
                                <div class="icon">🙏</div>
                                Twoja dzisiejsza modlitwa
                            </div>
                            <div class="result-content">${selectedPrayer}</div>
                        </div>
                    `;
                    
                    setTimeout(() => {
                        document.querySelectorAll('.result-card').forEach(card => {
                            card.classList.add('show');
                        });
                    }, 100);
                    
                    updateDrawButton();
                    updateHistory();
                    showCountdown();
                    showStreak();
                }, 3000);
            }, 3000);
        }

        function updateHistory() {
            const historyArea = document.getElementById('historyArea');
            
            if (drawHistory.length === 0) {
                historyArea.innerHTML = `
                    <div class="history-item">
                        <div class="history-date">Brak wcześniejszych losowań</div>
                        <div class="history-content">Rozpocznij swoje pierwsze losowanie!</div>
                    </div>
                `;
                return;
            }
            
            historyArea.innerHTML = drawHistory.map(item => `
                <div class="history-item">
                    <div class="history-date">${new Date(item.date).toLocaleDateString('pl-PL')} ${item.streak ? `🔥 Passa: ${item.streak} dni` : ''}</div>
                    <div class="history-content">
                        <strong>Intencja:</strong> ${item.intention}<br>
                        <strong>Modlitwa:</strong> ${item.prayer.substring(0, 50)}...
                    </div>
                </div>
            `).join('');
        }

        // Inicjalizacja - załaduj dane ponownie i wyświetl
        window.addEventListener('load', function() {
            loadData();
            updateDrawButton();
            updateTitlesButton();
            showTodaysResults();
            updateHistory();
        });
        
        // Uruchom inicjalizację od razu
        updateDrawButton();
        updateTitlesButton();
        showTodaysResults();
        updateHistory();
        showStreak();
        
        setInterval(updateCountdown, 1000);
        
        // Sprawdź o północy czy można losować i zapisuj dane regularnie
        setInterval(() => {
            const now = new Date();
            if (now.getHours() === 0 && now.getMinutes() === 0) {
                updateDrawButton();
            }
            // Zapisuj dane co minutę dla pewności
            saveAllData();
        }, 60000);

        function updateTitlesButton() {
            const button = document.getElementById('titlesButton');
            const highestTitle = getHighestUnlockedTitle();
            
            if (highestTitle) {
                button.className = 'titles-button title-border';
                button.style.setProperty('--title-color', highestTitle.borderColor);
                button.style.setProperty('--title-glow', highestTitle.glowColor);
            } else {
                button.className = 'titles-button';
            }
        }

        function showTitlesModal() {
            updateTitlesDisplay();
            document.getElementById('titlesModal').classList.add('show');
        }

        function hideTitlesModal() {
            document.getElementById('titlesModal').classList.remove('show');
        }

        function updateTitlesDisplay() {
            const container = document.getElementById('titlesContainer');
            
            container.innerHTML = titles.map(title => {
                const isUnlocked = unlockedTitles.includes(title.name);
                const progress = Math.min((currentStreak / title.days) * 100, 100);
                
                return `
                    <div class="title-card ${isUnlocked ? 'unlocked' : 'locked'}" style="--gradient: ${title.gradient}">
                        <div class="title-name" style="background: ${title.gradient}; -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;">
                            <div class="title-icon">
                                <img src="${title.icon}" alt="${title.name}" onerror="this.style.display='none';">
                            </div>
                            ${title.name}
                        </div>
                        <div class="title-requirement">
                            Wymagane: ${title.days} dni passy
                        </div>
                        <div class="title-progress">
                            <div class="title-progress-bar" style="width: ${progress}%; background: ${title.gradient}"></div>
                        </div>
                        <div class="title-status ${isUnlocked ? 'unlocked' : 'locked'}">
                            ${isUnlocked ? '✅ Odblokowany!' : `${currentStreak}/${title.days} dni`}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Zamknij modal po kliknięciu w tło
        document.getElementById('titlesModal').addEventListener('click', function(e) {
            if (e.target === this) {
                hideTitlesModal();
            }
        });

        // Zapisuj dane przy każdej zmianie
        function saveAllData() {
            try {
                localStorage.setItem('lastDrawDate', lastDrawDate || '');
                localStorage.setItem('todaysPrayer', todaysPrayer || '');
                localStorage.setItem('todaysIntention', todaysIntention || '');
                localStorage.setItem('drawHistory', JSON.stringify(drawHistory || []));
                localStorage.setItem('currentStreak', currentStreak.toString());
                localStorage.setItem('lastStreakDate', lastStreakDate || '');
                localStorage.setItem('unlockedTitles', JSON.stringify(unlockedTitles || []));
                
                console.log('Zapisano dane:', {
                    lastDrawDate,
                    todaysPrayer: todaysPrayer ? 'tak' : 'nie',
                    todaysIntention: todaysIntention ? 'tak' : 'nie',
                    historyLength: drawHistory ? drawHistory.length : 0,
                    currentStreak,
                    lastStreakDate,
                    unlockedTitles: unlockedTitles.length
                });
            } catch (e) {
                console.log('Błąd zapisywania danych:', e);
            }
        }

        // Zapisuj dane przed zamknięciem strony
        window.addEventListener('beforeunload', saveAllData);
        window.addEventListener('pagehide', saveAllData);
        
        // Zapisuj dane przy każdej aktywności użytkownika
        document.addEventListener('click', saveAllData);
        document.addEventListener('keydown', saveAllData);


    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'990630d38367512f',t:'MTc2MDc3MTE2Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
