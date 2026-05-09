<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FAME MMA Fan Page</title>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;700&family=Roboto:wght@300;400&display=swap" rel="stylesheet">
    <style>
        :root {
            --fame-red: #ff0000;
            --fame-gold: #ffcc00;
            --dark-bg: #0a0a0a;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background-color: var(--dark-bg);
            color: white;
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://images.unsplash.com/photo-1595079676339-1534801ad6cf?auto=format&fit=crop&q=80&w=1000') center/cover;
            height: 40vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            border-bottom: 4px solid var(--fame-red);
        }

        h1 {
            font-family: 'Oswald', sans-serif;
            font-size: 3.5rem;
            margin: 0;
            color: #fff;
            text-shadow: 2px 2px 10px rgba(255,0,0,0.8);
        }

        .highlight { color: var(--fame-gold); }

        .container {
            padding: 20px;
            max-width: 600px;
            margin: auto;
        }

        /* Styl karty walki */
        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 25px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .main-fight {
            text-align: center;
            border-left: 5px solid var(--fame-red);
        }

        .vs-grid {
            display: grid;
            grid-template-columns: 1fr auto 1fr;
            align-items: center;
            gap: 10px;
            margin: 20px 0;
        }

        .fighter-name {
            font-family: 'Oswald', sans-serif;
            font-size: 1.4rem;
            text-transform: uppercase;
        }

        .vs-badge {
            background: var(--fame-red);
            padding: 5px 12px;
            border-radius: 5px;
            font-weight: bold;
            font-style: italic;
        }

        /* Przyciski dopasowane do kciuka na telefonie */
        .btn {
            display: block;
            background: var(--fame-red);
            color: white;
            text-decoration: none;
            padding: 18px;
            border-radius: 12px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: 0.3s;
            margin: 10px 0;
            font-size: 1.1rem;
        }

        .btn-gold {
            background: transparent;
            border: 2px solid var(--fame-gold);
            color: var(--fame-gold);
        }

        footer {
            text-align: center;
            padding: 40px;
            font-size: 0.7rem;
            opacity: 0.5;
        }
    </style>
</head>
<body>

    <header>
        <h1>FAME <span class="highlight">MMA</span></h1>
        <p style="font-family: 'Oswald';">FAN PAGE / NOWY SEZON</p>
    </header>

    <div class="container">
        
        <div class="card main-fight">
            <p style="color: var(--fame-gold); margin: 0; font-weight: bold;">WALKA WIECZORU</p>
            <div class="vs-grid">
                <div class="fighter-name">Don Kasjo</div>
                <div class="vs-badge">VS</div>
                <div class="fighter-name">Boxdel</div>
            </div>
            <p style="font-size: 0.9rem; margin-bottom: 0;">Lokalizacja: Tauron Arena, Kraków</p>
        </div>

        <div class="card">
            <h3 style="margin-top: 0;">Moje typy:</h3>
            <p>🥊 Walka 1: <b>Kasjo przez decyzję</b></p>
            <p>🥊 Walka 2: <b>Pasternak przez KO</b></p>
        </div>

        <a href="#" class="btn">Kup PPV teraz</a>
        <a href="#" class="btn btn-gold">Zobacz trailer karty</a>

    </div>

    <footer>
        DESIGNED FOR MOBILE BY GEMINI AI &copy; 2026
    </footer>

</body>
</html>
