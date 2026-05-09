<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAME GAME - Staty & Drops</title>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root { --fame-red: #ff0000; --fame-gold: #ffcc00; --dark-bg: #050505; --card-bg: #121212; }
        body { font-family: 'Roboto', sans-serif; background-color: var(--dark-bg); color: white; margin: 0; padding-bottom: 80px; text-align: center; }
        header { background: #000; padding: 15px; border-bottom: 2px solid var(--fame-red); position: sticky; top: 0; z-index: 100; }
        h1 { font-family: 'Oswald', sans-serif; margin: 0; font-size: 1.5rem; }
        
        .wallet { background: #222; padding: 10px; border-radius: 10px; margin: 10px; display: inline-block; font-weight: bold; color: var(--fame-gold); border: 1px solid var(--fame-gold); }

        nav { position: fixed; bottom: 0; width: 100%; background: #111; display: flex; justify-content: space-around; padding: 10px 0; border-top: 1px solid #333; z-index: 1000; }
        .nav-item { color: #888; background: none; border: none; font-family: 'Oswald', sans-serif; font-size: 0.9rem; cursor: pointer; }
        .nav-item.active { color: var(--fame-red); }

        .section { display: none; padding: 20px; animation: fadeIn 0.3s; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* SKRZYNKI */
        .case-container { background: var(--card-bg); border-radius: 20px; padding: 20px; border: 2px dashed #333; }
        .btn-open { background: var(--fame-gold); color: black; border: none; padding: 15px 30px; border-radius: 10px; font-family: 'Oswald'; font-size: 1.1rem; width: 100%; margin-top: 10px; }
        
        /* EKWIPUNEK */
        .inv-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .item-card { background: var(--card-bg); padding: 10px; border-radius: 10px; border: 1px solid #333; text-align: center; }
        .sell-btn { background: #cc0000; color: white; border: none; padding: 5px 10px; border-radius: 5px; margin-top: 5px; font-size: 0.8rem; }

        /* RANKING I GALA (uproszczone) */
        .list-item { background: var(--card-bg); padding: 10px; margin-bottom: 5px; border-radius: 5px; display: flex; justify-content: space-between; }
    </style>
</head>
<body>

<header>
    <h1>FAME <span style="color:var(--fame-gold)">PORTAL</span></h1>
    <div class="wallet">💰 MONETY: <span id="balance">0</span></div>
</header>

<!-- GALA -->
<div id="gala" class="section active">
    <h2 style="font-family: 'Oswald';">NADCHODZĄCA GALA</h2>
    <div class="list-item"><span>ADRIAN POLAK</span> <b>VS</b> <span>FERRARI</span></div>
    <div class="list-item"><span>DON KASJO</span> <b>VS</b> <span>TAŃCULA</span></div>
</div>

<!-- RANKING -->
<div id="ranking" class="section">
    <h2 style="font-family: 'Oswald';">RANKING</h2>
    <div class="list-item"><span>1. DON KASJO</span> <span style="color:var(--fame-gold)">8-2</span></div>
    <div class="list-item"><span>2. ADRIAN POLAK</span> <span>7-3</span></div>
</div>

<!-- SKRZYNKI -->
<div id="drops" class="section">
    <h2 style="font-family: 'Oswald';">DROP (KOSZT: 50 💰)</h2>
    <div class="case-container">
        <div id="case-status" style="font-size: 3rem;">📦</div>
        <div id="drop-result" style="margin: 10px 0; font-weight: bold;">Spróbuj szczęścia!</div>
        <button class="btn-open" onclick="buyCase()">OTWÓRZ SKRZYNIĘ</button>
    </div>
    <button onclick="addMoney(100)" style="margin-top: 20px; background: none; border: 1px solid #444; color: #888; padding: 5px;">+ DARMOWE MONETY (TEST)</button>
</div>

<!-- EKWIPUNEK -->
<div id="inventory" class="section">
    <h2 style="font-family: 'Oswald';">TWÓJ EKWIPUNEK</h2>
    <div id="inv-list" class="inv-grid">
        <!-- Przedmioty pojawią się tutaj -->
    </div>
</div>

<nav>
    <button class="nav-item active" onclick="openSection(event, 'gala')">GALA</button>
    <button class="nav-item" onclick="openSection(event, 'ranking')">RANKING</button>
    <button class="nav-item" onclick="openSection(event, 'drops')">DROP</button>
    <button class="nav-item" onclick="openSection(event, 'inventory')">EQ</button>
</nav>

<script>
    // BAZA PRZEDMIOTÓW
    const itemsData = [
        { name: "Karta Kasjo", price: 150, icon: "🃏", rarity: "GOLD" },
        { name: "Rękawice FAME", price: 40, icon: "🥊", rarity: "NORMAL" },
        { name: "Bilet VIP", price: 300, icon: "🎟️", rarity: "EPIC" },
        { name: "Woda FAME", price: 10, icon: "💧", rarity: "NORMAL" },
        { name: "Złoty Puchar", price: 500, icon: "🏆", rarity: "LEGEND" }
    ];

    let coins = parseInt(localStorage.getItem('fame_coins')) || 100;
    let inventory = JSON.parse(localStorage.getItem('fame_inv')) || [];

    function updateUI() {
        document.getElementById('balance').innerText = coins;
        localStorage.setItem('fame_coins', coins);
        localStorage.setItem('fame_inv', JSON.stringify(inventory));
        renderInventory();
    }

    function openSection(evt, name) {
        document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        document.getElementById(name).classList.add('active');
        evt.currentTarget.classList.add('active');
    }

    function addMoney(amt) {
        coins += amt;
        updateUI();
    }

    function buyCase() {
        if (coins < 50) {
            alert("Nie masz wystarczająco monet!");
            return;
        }
        coins -= 50;
        const result = itemsData[Math.floor(Math.random() * itemsData.length)];
        inventory.push(result);
        document.getElementById('drop-result').innerText = "Wylosowano: " + result.name;
        updateUI();
    }

    function renderInventory() {
        const list = document.getElementById('inv-list');
        list.innerHTML = "";
        inventory.forEach((item, index) => {
            list.innerHTML += `
                <div class="item-card">
                    <div style="font-size: 2rem;">${item.icon}</div>
                    <div style="font-size: 0.8rem; font-weight: bold;">${item.name}</div>
                    <div style="color:var(--fame-gold)">${item.price} 💰</div>
                    <button class="sell-btn" onclick="sellItem(${index})">SPRZEDAJ</button>
                </div>
            `;
        });
        if(inventory.length === 0) list.innerHTML = "<p style='grid-column: 1/3'>Ekwipunek jest pusty.</p>";
    }

    function sellItem(index) {
        coins += inventory[index].price;
        inventory.splice(index, 1);
        updateUI();
    }

    // Start
    updateUI();
</script>

</body>
</html>
