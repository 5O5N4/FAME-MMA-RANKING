<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAME MMA - Portal</title>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --fame-red: #ff0000;
            --fame-gold: #ffcc00;
            --dark-bg: #050505;
            --card-bg: #121212;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background-color: var(--dark-bg);
            color: white;
            margin: 0;
            padding-bottom: 80px; /* Miejsce na dolne menu */
        }

        /* Nagłówek */
        header {
            background: #000;
            text-align: center;
            padding: 20px 0;
            border-bottom: 2px solid var(--fame-red);
        }

        h1 { font-family: 'Oswald', sans-serif; margin: 0; font-size: 2rem; }
        .gold { color: var(--fame-gold); }

        /* Nawigacja Dolna */
        nav {
            position: fixed;
            bottom: 0;
            width: 100%;
            background: #111;
            display: flex;
            justify-content: space-around;
            padding: 15px 0;
            border-top: 1px solid #333;
            z-index: 1000;
        }

        .nav-item {
            color: #888;
            text-decoration: none;
            font-family: 'Oswald', sans-serif;
            font-size: 1.2rem;
            background: none;
            border: none;
            cursor: pointer;
        }

        .nav-item.active {
            color: var(--fame-red);
        }

        /* Sekcje */
        .section { display: none; padding: 20px; animation: fadeIn 0.3s; }
        .section.active { display: block; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Karta Walki */
        .fight-card {
            background: var(--card-bg);
            border-radius: 15px;
            margin-bottom: 15px;
            padding: 15px;
            display: grid;
            grid-template-columns: 1fr auto 1fr;
            align-items: center;
            text-align: center;
            border-left: 4px solid var(--fame-red);
        }

        .fighter { font-family: 'Oswald', sans-serif; font-size: 1.1rem; }
        .vs { background: var(--fame-red); padding: 4px 8px; border-radius: 4px; font-weight: bold; font-size: 0.8rem; }

        /* Tabela Rankingu */
        table {
            width: 100%;
            border-collapse: collapse;
            background: var(--card-bg);
            border-radius: 10px;
            overflow: hidden;
        }

        th { background: #222; color: var(--fame-gold); padding: 12px; text-align: left; font-family: 'Oswald'; }
        td { padding: 12px; border-bottom: 1px solid #222; }
        .win { color: #00ff00; font-weight: bold; }
    </style>
</head>
<body>

<header>
    <h1>FAME <span class="gold">STATY</span></h1>
</header>

<!-- SEKTCJA GALA -->
<div id="gala" class="section active">
    <h2 style="font-family: 'Oswald';">AKTUALNA KARTA WALK</h2>
    
    <div class="fight-card">
        <div class="fighter">ADRIAN POLAK</div>
        <div class="vs">VS</div>
        <div class="fighter">FERRARI</div>
    </div>

    <div class="fight-card">
        <div class="fighter">DON KASJO</div>
        <div class="vs">VS</div>
        <div class="fighter">TAŃCULA</div>
    </div>

    <div class="fight-card" style="border-left-color: var(--fame-gold);">
        <div class="fighter">PASZUT</div>
        <div class="vs">VS</div>
        <div class="fighter">NARKUN</div>
    </div>
</div>

<!-- SEKCJA RANKING -->
<div id="ranking" class="section">
    <h2 style="font-family: 'Oswald';">RANKING WYGRANYCH</h2>
    <table>
        <thead>
            <tr>
                <th>ZAWODNIK</th>
                <th>BILANS</th>
                <th>KD</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Don Kasjo</td>
                <td class="win">8-2</td>
                <td>1.25</td>
            </tr>
            <tr>
                <td>Adrian Polak</td>
                <td class="win">7-3</td>
                <td>0.95</td>
            </tr>
            <tr>
                <td>Boxdel</td>
                <td class="win">3-2</td>
                <td>0.80</td>
            </tr>
        </tbody>
    </table>
</div>

<!-- DOLNE MENU -->
<nav>
    <button class="nav-item active" onclick="openSection(event, 'gala')">GALA</button>
    <button class="nav-item" onclick="openSection(event, 'ranking')">RANKING</button>
</nav>

<script>
    function openSection(evt, sectionName) {
        // Ukryj wszystkie sekcje
        var sections = document.getElementsByClassName("section");
        for (var i = 0; i < sections.length; i++) {
            sections[i].classList.remove("active");
        }

        // Usuń klasę active z przycisków
        var navItems = document.getElementsByClassName("nav-item");
        for (var i = 0; i < navItems.length; i++) {
            navItems[i].classList.remove("active");
        }

        // Pokaż wybraną sekcję i dodaj klasę active do przycisku
        document.getElementById(sectionName).classList.add("active");
        evt.currentTarget.classList.add("active");
    }
</script>

</body>
</html>
