<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Ultimate Case Opener & Upgrade</title>
    <style>
        :root {
            --gold: #ffcc00;
            --red: #ff4444;
            --green: #00c851;
            --dark-bg: #0f0f0f;
            --card-bg: #1a1a1a;
        }

        body {
            background-color: var(--dark-bg);
            color: white;
            font-family: 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding-bottom: 50px;
        }

        nav {
            background: #151515;
            padding: 20px 10%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--gold);
            position: sticky;
            top: 0; z-index: 1000;
        }

        .balance-box {
            font-size: 1.2rem;
            background: #252525;
            padding: 10px 20px;
            border-radius: 8px;
            border: 1px solid var(--gold);
        }

        #balance { color: var(--gold); font-weight: bold; }

        .section-title { text-align: center; margin-top: 40px; color: var(--gold); text-transform: uppercase; }

        .container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            padding: 20px 10%;
        }

        .case-card {
            background: var(--card-bg);
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            border: 1px solid #333;
            transition: 0.3s;
        }

        .case-card:hover { border-color: var(--gold); transform: translateY(-5px); }

        .case-img { width: 100%; border-radius: 5px; margin-bottom: 10px; }

        .btn-open {
            background: var(--gold);
            border: none;
            width: 100%;
            padding: 10px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 5px;
        }

        /* --- UPGRADER SECTION --- */
        .upgrader-section {
            background: #151515;
            margin: 50px 10%;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            border: 2px dashed #444;
        }

        .upgrade-controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            align-items: center;
            margin-top: 20px;
        }

        input[type="number"] {
            background: #222;
            border: 1px solid var(--gold);
            color: white;
            padding: 10px;
            border-radius: 5px;
            width: 100px;
        }

        .btn-upgrade {
            background: var(--green);
            color: white;
            border: none;
            padding: 10px 30px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 5px;
        }

        .status-msg { margin-top: 15px; font-weight: bold; min-height: 20px; }
    </style>
</head>
<body>

<nav>
    <div style="font-size: 1.5rem; letter-spacing: 2px;">GOLD<span style="color:var(--gold)">DROP</span></div>
    <div class="balance-box">SALDO: <span id="balance">1000.00</span> PLN</div>
</nav>

<h2 class="section-title">Dostępne Skrzynie</h2>
<div class="container" id="cases">
    <!-- Skrzynie zostaną wygenerowane przez JS -->
</div>

<div class="upgrader-section">
    <h2 style="color: var(--green)">TRYB 50/50 (DOUBLE OR NOTHING)</h2>
    <p>Wpisz kwotę, którą chcesz zaryzykować. Wygrana to 2x stawka!</p>
    <div class="upgrade-controls">
        <input type="number" id="betAmount" value="10" min="1">
        <button class="btn-upgrade" onclick="play5050()">GRAJ O PODWOJENIE</button>
    </div>
    <div id="status" class="status-msg"></div>
</div>

<script>
    let balance = 1000.00;

    const casesData = [
        { name: "MILITARY", price: 5, img: "https://community.cloudflare.steamstatic.com/economy/image/-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXU5A1PIYQNqhpOSV-fRPasw8rsUFJ5KBFZs6eyfRcl7HBiTz5H74y1xtTcz6SmazuIzz0Iu8Ypj-qS892s2Vaxq0VkZ232I9Scc1M6aV_Q_1O-l7C70Z_vup7AnXFis3E8pSGKNoE6_m0" },
        { name: "CHROMA", price: 25, img: "https://community.cloudflare.steamstatic.com/economy/image/-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXU5A1PIYQNqhpOSV-fRPasw8rsUFJ5KBFZs6eyfRcl7HBiTz5Ic9uzq4yKh9-la7rXlD5X7p8oie-S99_03Vbg_RA9MT_2IYScc1A3NVvR-Ffvl7C70Me-6p7AnHFis3E8pSGLeyuNtg" },
        { name: "SPECTRUM", price: 75, img: "https://community.cloudflare.steamstatic.com/economy/image/-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXU5A1PIYQNqhpOSV-fRPasw8rsUFJ5KBFZs6eyfRcl7HBiTz5H74y3xtTcz6SmazuIzz0Iu8Ypj-qS892s2Vaxq0VkZ232I9Scc1M6aV_Q_1O-l7C70Z_vup7AnXFis3E8pSGKNoE6_m0" },
        { name: "COBALT", price: 150, img: "https://community.cloudflare.steamstatic.com/economy/image/-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXU5A1PIYQNqhpOSV-fRPasw8rsUFJ5KBFZs6eyfRcl7HBiTz5H74y1xtTcz6SmazuIzz0Iu8Ypj-qS892s2Vaxq0VkZ232I9Scc1M6aV_Q_1O-l7C70Z_vup7AnXFis3E8pSGKNoE6_m0" },
        { name: "DRAGON", price: 500, img: "https://community.cloudflare.steamstatic.com/economy/image/-9a81dlWLwJ2UUGcVs_nsVtzdOEdtWwKGZZLQHTxDZ7I56KU0Zwwo4NUX4oFJZEHLbXU5A1PIYQNqhpOSV-fRPasw8rsUFJ5KBFZs6eyfRcl7HBiTz5H74y1xtTcz6SmazuIzz0Iu8Ypj-qS892s2Vaxq0VkZ232I9Scc1M6aV_Q_1O-l7C70Z_vup7AnXFis3E8pSGKNoE6_m0" }
    ];

    function init() {
        const container = document.getElementById('cases');
        casesData.forEach(c => {
            container.innerHTML += `
                <div class="case-card">
                    <img src="${c.img}" class="case-img">
                    <h3>${c.name}</h3>
                    <p style="color:var(--gold)">${c.price.toFixed(2)} PLN</p>
                    <button class="btn-open" onclick="openCase(${c.price})">OTWÓRZ</button>
                </div>
            `;
        });
    }

    function updateDisplay() {
        document.getElementById('balance').innerText = balance.toFixed(2);
    }

    function openCase(price) {
        if (balance >= price) {
            balance -= price;
            updateDisplay();
            alert("Skrzynka otwarta! (Tu w przyszłości dodasz animację dropu)");
        } else {
            alert("Brak środków!");
        }
    }

    function play5050() {
        const bet = parseFloat(document.getElementById('betAmount').value);
        const status = document.getElementById('status');

        if (isNaN(bet) || bet <= 0) {
            status.innerText = "Wpisz poprawną kwotę!";
            return;
        }

        if (balance < bet) {
            status.style.color = "var(--red)";
            status.innerText = "Nie masz tyle pieniędzy!";
            return;
        }

        // Odebranie stawki
        balance -= bet;
        updateDisplay();

        status.style.color = "white";
        status.innerText = "Losowanie...";

        setTimeout(() => {
            const win = Math.random() > 0.5; // Mechanizm 50/50

            if (win) {
                const winAmount = bet * 2;
                balance += winAmount;
                status.style.color = var(--green);
                status.innerText = `WYGRANA! +${winAmount.toFixed(2)} PLN`;
            } else {
                status.style.color = var(--red);
                status.innerText = "PRZEGRANA. Spróbuj ponownie!";
            }
            updateDisplay();
        }, 800);
    }

    init();
</script>

</body>
</html>
