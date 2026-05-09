<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAME TYCOON - Drops & Skins</title>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root { --fame-red: #ff0000; --fame-gold: #ffcc00; --dark-bg: #050505; --card-bg: #121212; --blue-rarity: #007bff; }
        body { font-family: 'Roboto', sans-serif; background-color: var(--dark-bg); color: white; margin: 0; padding-bottom: 90px; text-align: center; }
        header { background: #000; padding: 15px; border-bottom: 2px solid var(--fame-red); position: sticky; top: 0; z-index: 100; }
        h1 { font-family: 'Oswald', sans-serif; margin: 0; font-size: 1.5rem; }
        
        .wallet { background: #1a1a1a; padding: 8px 15px; border-radius: 20px; margin-top: 10px; display: inline-block; font-weight: bold; color: var(--fame-gold); border: 1px solid #333; }

        nav { position: fixed; bottom: 0; width: 100%; background: #111; display: flex; justify-content: space-around; padding: 12px 0; border-top: 1px solid #333; z-index: 1000; }
        .nav-item { color: #888; background: none; border: none; font-family: 'Oswald', sans-serif; font-size: 0.85rem; cursor: pointer; transition: 0.2s; }
        .nav-item.active { color: var(--fame-red); transform: scale(1.1); }

        .section { display: none; padding: 15px; animation: fadeIn 0.3s; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* SKRZYNKI */
        .case-selector { display: grid; grid-template-columns: 1fr; gap: 15px; margin-top: 10px; }
        .case-box { background: var(--card-bg); border-radius: 15px; padding: 15px; border: 1px solid #333; transition: 0.3s; }
        .case-box:active { transform: scale(0.98); }
        .btn-buy { width: 100%; padding: 12px; border-radius: 8px; border: none; font-family: 'Oswald'; font-size: 1rem; margin-top: 10px; cursor: pointer; }
        
        .bronze { border-left: 5px solid #cd7f32; } .bronze-btn { background: #cd7f32; color: white; }
        .silver { border-left: 5px solid #c0c0c0; } .silver-btn { background: #c0c0c0; color: black; }
        .gold-case { border-left: 5px solid var(--fame-gold); } .gold-btn { background: var(--fame-gold); color: black; }

        /* EKWIPUNEK */
        .inv-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
        .sell-all-btn { background: #ed1c24; color: white; border: none; padding: 8px 15px; border-radius: 5px; font-family: 'Oswald'; font-size: 0.8rem; }
        .inv-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .item-card { background: var(--card-bg); padding: 12px; border-radius: 12px; border: 1px solid #222; position: relative; }
        .sell-btn { background: #333; color: #ff5555; border: none; padding: 5px; border-radius: 4px; width: 100%; margin-top: 8px; font-size: 0.75rem; border: 1px solid #444; }

        .list-item { background: var(--card-bg); padding: 12px; margin-bottom: 8px; border-radius: 8px; display: flex; justify-content: space-between; align-items: center; }
    </style>
</head>
<body>

<header>
    <h1>FAME <span style="color:var(--fame-gold)">TYCOON</span></h1>
    <div class="wallet">💰 <span id="balance">0</span></div>
</header>

<!-- GALA -->
<div id="gala" class="section active">
    <h2 style="font-family: 'Oswald';">NADCHODZĄCA GALA</h2>
    <div class="list-item"><span>ADRIAN POLAK</span> <b style="color:red">VS</b> <span>FERRARI</span></div>
    <div class="list-item"><span>DON KASJO</span> <b style="color:red">VS</b> <span>TAŃCULA</span></div>
</div>

<!-- RANKING -->
<div id="ranking" class="section">
    <h2 style="font-family: 'Oswald';">TOP ZAWODNICY</h2>
    <div class="list-item"><span>1. DON KASJO</span> <span style="color:var(--fame-gold)">1.45 KD</span></div>
    <div class="list-item"><span>2. ADRIAN POLAK</span> <span>0.95 KD</span></div>
</div>

<!-- SKRZYNKI -->
<div id="drops" class="section">
    <h2 style="font-family: 'Oswald';">WYBIERZ SKRZYNIĘ</h2>
    <div id="last-drop" style="color: var(--fame-gold); height: 20px; margin-bottom: 10px; font-weight: bold;"></div>
    
    <div class="case-selector">
        <div class="case-box bronze">
            <span style="font-size: 2.5rem;">📦</span>
            <h3>SKRZYNIA BRĄZOWA</h3>
            <p>Koszt: 20 💰</p>
            <button class="btn-buy bronze-btn" onclick="buyCase('bronze')">OTWÓRZ</button>
        </div>
        <div class="case-box silver">
            <span style="font-size: 2.5rem;">🔘</span>
            <h3>SKRZYNIA SREBRNA</h3>
            <p>Koszt: 100 💰</p>
            <button class="btn-buy silver-btn" onclick="buyCase('silver')">OTWÓRZ</button>
        </div>
        <div class="case-box gold-case">
            <span style="font-size: 2.5rem;">✨</span>
            <h3>SKRZYNIA ZŁOTA</h3>
            <p>Koszt: 500 💰</p>
            <button class="btn-buy gold-btn" onclick="buyCase('gold')">OTWÓRZ</button>
        </div>
    </div>
    <button onclick="addMoney(500)" style="margin-top: 20px; background: none; border: 1px solid #333; color: #555; padding: 10px; border-radius: 10px;">DODAJ +500 (Dla testów)</button>
</div>

<!-- EKWIPUNEK -->
<div id="inventory" class="section">
    <div class="inv-header">
        <h2 style="font-family: 'Oswald'; margin: 0;">TWOJE EQ</h2>
        <button id="sell-all" class="sell-all-btn" onclick="sellAllItems()">SPRZEDAJ WSZYSTKO</button>
    </div>
    <div id="inv-list" class="inv-grid"></div>
</div>

<nav>
    <button class="nav-item active" onclick="openSection(event, 'gala')">GALA</button>
    <button class="nav-item" onclick="openSection(event, 'ranking')">RANKING</button>
    <button class="nav-item" onclick="openSection(event, 'drops')">DROPS</button>
    <button class="nav-item" onclick="openSection(event, 'inventory')">EQ</button>
</nav>

<script>
    // System przedmiotów
    const database = {
        bronze: [
            { name: "Woda FAME", price: 10, icon: "💧" },
            { name: "Plakat", price: 15, icon: "📜" },
            { name: "Smycz", price: 25, icon: "📿" }
        ],
        silver: [
            { name: "Rękawice", price: 80, icon: "🥊" },
            { name: "Koszulka", price: 120, icon: "👕" },
            { name: "Karta Ferrari", price: 200, icon: "🃏" }
        ],
        gold: [
            { name: "Karta Kasjo", price: 800, icon: "👑" },
            { name: "Bilet VIP", price: 1500, icon: "🎟️" },
            { name: "Pas Mistrza", price: 5000, icon: "🏆" }
        ]
    };

    let coins = parseInt(localStorage.getItem('f_coins')) || 200;
    let inventory = JSON.parse(localStorage.getItem('f_inv')) || [];

    function updateUI() {
        document.getElementById('balance').innerText = coins;
        localStorage.setItem('f_coins', coins);
        localStorage.setItem('f_inv', JSON.stringify(inventory));
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

    function buyCase(type) {
        const prices = { bronze: 20, silver: 100, gold: 500 };
        if (coins < prices[type]) {
            alert("Brak monet!");
            return;
        }
        coins -= prices[type];
        const pool = database[type];
        const win = pool[Math.floor(Math.random() * pool.length)];
        inventory.push(win);
        document.getElementById('last-drop').innerText = "DROP: " + win.name + "!";
        updateUI();
    }

    function renderInventory() {
        const list = document.getElementById('inv-list');
        list.innerHTML = "";
        inventory.forEach((item, index) => {
            list.innerHTML += `
                <div class="item-card">
                    <div style="font-size: 1.8rem;">${item.icon}</div>
                    <div style="font-size: 0.75rem; font-weight: bold; margin: 5px 0;">${item.name}</div>
                    <div style="color:var(--fame-gold); font-size: 0.9rem;">${item.price} 💰</div>
                    <button class="sell-btn" onclick="sellItem(${index})">SPRZEDAJ</button>
                </div>
            `;
        });
        document.getElementById('sell-all').style.display = inventory.length > 1 ? "block" : "none";
    }

    function sellItem(index) {
        coins += inventory[index].price;
        inventory.splice(index, 1);
        updateUI();
    }

    function sellAllItems() {
        if (inventory.length === 0) return;
        const total = inventory.reduce((sum, item) => sum + item.price, 0);
        coins += total;
        inventory = [];
        updateUI();
        alert("Sprzedano wszystko za: " + total + " 💰");
    }

    updateUI();
</script>

</body>
</html>
