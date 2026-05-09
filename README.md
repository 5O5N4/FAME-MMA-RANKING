<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAME PORTAL & DROPS</title>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --fame-red: #ff0000;
            --fame-gold: #ffcc00;
            --dark-bg: #050505;
            --card-bg: #121212;
        }

        body { font-family: 'Roboto', sans-serif; background-color: var(--dark-bg); color: white; margin: 0; padding-bottom: 80px; text-align: center; }
        header { background: #000; padding: 15px 0; border-bottom: 2px solid var(--fame-red); position: sticky; top: 0; z-index: 100; }
        h1 { font-family: 'Oswald', sans-serif; margin: 0; font-size: 1.8rem; }
        .gold { color: var(--fame-gold); }

        /* Nawigacja */
        nav { position: fixed; bottom: 0; width: 100%; background: #111; display: flex; justify-content: space-around; padding: 10px 0; border-top: 1px solid #333; z-index: 1000; }
        .nav-item { color: #888; background: none; border: none; font-family: 'Oswald', sans-serif; font-size: 1rem; cursor: pointer; padding: 10px; }
        .nav-item.active { color: var(--fame-red); }

        .section { display: none; padding: 20px; animation: fadeIn 0.3s; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Gra / Skrzynki */
        .case-container { background: var(--card-bg); border-radius: 20px; padding: 30px; margin-top: 20px; border: 2px dashed #333; }
        .case-visual { font-size: 5rem; margin: 20px 0; display: block; filter: drop-shadow(0 0 10px var(--fame-gold)); }
        .btn-open { background: var(--fame-gold); color: black; border: none; padding: 15px 40px; border-radius: 10px; font-family: 'Oswald'; font-size: 1.2rem; cursor: pointer; box-shadow: 0 5px 15px rgba(255, 204, 0, 0.4); }
        .btn-open:active { transform: scale(0.95); }
        
        #result { margin-top: 20px; font-size: 1.2rem; font-weight: bold; min-height: 1.5em; color: var(--fame-gold); }

        /* Tabele i Karty (z poprzednich kroków) */
        .fight-card { background: var(--card-bg); border-radius: 10px; padding: 15px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; border-left: 4px solid var(--fame-red); }
        table { width: 100%; border-collapse: collapse; background: var(--card-bg); }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #222; }
    </style>
</head>
<body>

<header>
    <h1>FAME <span class="gold">STATY & DROPS</span></h1>
</header>

<!-- SEKCJA GALA -->
<div id="gala" class="section active">
    <h2 style="font-family: 'Oswald';">KARTA WALK</h2>
    <div class="fight-card"><span>ADRIAN POLAK</span> <b style="color:red">VS</b> <span>FERRARI</span></div>
    <div class="fight-card"><span>DON KASJO</span> <b style="color:red">VS</b> <span>TAŃCULA</span></div>
</div>

<!-- SEKCJA RANKING -->
<div id="ranking" class="section">
    <h2 style="font-family: 'Oswald';">RANKING</h2>
    <table>
        <tr><th>ZAWODNIK</th><th>W-P</th></tr>
        <tr><td>★ DON KASJO</td><td style="color:#0f0">8 - 2</td></tr>
        <tr><td>FERRARI</td><td style="color:#0f0">6 - 6</td></tr>
    </table>
</div>

<!-- SEKCJA SKRZYNKI (GRA) -->
<div id="drops" class="section">
    <h2 style="font-family: 'Oswald';">DARMOWA SKRZYNIA FAME</h2>
    <div class="case-container">
        <span id="case-icon" class="case-visual">📦</span>
        <div id="result">Kliknij, aby otworzyć!</div>
        <button class="btn-open" onclick="openCase()">OTWÓRZ ZA DARMO</button>
    </div>
    <p style="color: #666; font-size: 0.8rem; margin-top: 20px;">To jest tylko symulator. Wszystkie nagrody są wirtualne.</p>
</div>

<nav>
    <button class="nav-item active" onclick="openSection(event, 'gala')">GALA</button>
    <button class="nav-item" onclick="openSection(event, 'ranking')">RANKING</button>
    <button class="nav-item" onclick="openSection(event, 'drops')">SKRZYNIE</button>
</nav>

<script>
    function openSection(evt, sectionName) {
        var sections = document.getElementsByClassName("section");
        for (var i = 0; i < sections.length; i++) sections[i].classList.remove("active");
        var navItems = document.getElementsByClassName("nav-item");
        for (var i = 0; i < navItems.length; i++) navItems[i].classList.remove("active");
        document.getElementById(sectionName).classList.add("active");
        evt.currentTarget.classList.add("active");
    }

    function openCase() {
        const results = [
            "Bilet na FAME 21! 🎟️",
            "Karta Don Kasjo (Legendarna) 🃏",
            "Koszulka FAME MMA 👕",
            "Uścisk dłoni Boxdela 🤝",
            "Zniżka na PPV -10% 💸",
            "Nic! Spróbuj ponownie ❌",
            "Karta Ferrari (Epicka) 🏎️"
        ];
        
        const btn = document.querySelector('.btn-open');
        const resDiv = document.getElementById('result');
        const icon = document.getElementById('case-icon');

        btn.disabled = true;
        resDiv.innerText = "Losowanie...";
        icon.style.animation = "shake 0.5s infinite";

        // Symulacja "otwierania"
        setTimeout(() => {
            const random = Math.floor(Math.random() * results.length);
            resDiv.innerText = results[random];
            icon.style.animation = "none";
            btn.disabled = false;
        }, 1500);
    }
</script>

<style>
    @keyframes shake {
        0% { transform: rotate(0deg); }
        25% { transform: rotate(5deg); }
        50% { transform: rotate(-5deg); }
        75% { transform: rotate(5deg); }
        100% { transform: rotate(0deg); }
    }
</style>

</body>
</html>
