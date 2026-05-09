<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fame MMA - Fan Page</title>
    <style>
        /* Stylistyka Dark Mode */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0f0f0f;
            color: white;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        header {
            background: linear-gradient(180deg, #ed1c24 0%, #000 100%);
            padding: 50px 20px;
        }

        h1 {
            font-size: 3rem;
            margin: 0;
            text-transform: uppercase;
            letter-spacing: 5px;
            color: #fff;
        }

        .highlight {
            color: #ffd700; /* Złoty kolor Fame */
        }

        .container {
            padding: 20px;
        }

        .next-event {
            background: #1a1a1a;
            border: 2px solid #ffd700;
            border-radius: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 500px;
        }

        .vs-box {
            display: flex;
            justify-content: space-around;
            align-items: center;
            font-weight: bold;
            font-size: 1.5rem;
        }

        .fighter {
            flex: 1;
        }

        .vs-circle {
            background: #ed1c24;
            width: 50px;
            height: 50px;
            line-height: 50px;
            border-radius: 50%;
            margin: 0 10px;
        }

        .btn {
            display: inline-block;
            background: #ed1c24;
            color: white;
            text-decoration: none;
            padding: 15px 30px;
            border-radius: 30px;
            font-weight: bold;
            margin-top: 20px;
            transition: 0.3s;
        }

        .btn:hover {
            transform: scale(1.1);
            background: #ff3131;
        }

        footer {
            margin-top: 50px;
            font-size: 0.8rem;
            color: #555;
            padding-bottom: 20px;
        }
    </style>
</head>
<body>

    <header>
        <h1>FAME <span class="highlight">MMA</span></h1>
        <p>Największa federacja freak-fight w Europie</p>
    </header>

    <div class="container">
        <div class="next-event">
            <h2 class="highlight">NAJBLIŻSZA WALKA</h2>
            <div class="vs-box">
                <div class="fighter">ZAWODNIK A</div>
                <div class="vs-circle">VS</div>
                <div class="fighter">ZAWODNIK B</div>
            </div>
            <p>Data: Już wkrótce...</p>
        </div>

        <h3>Moje typy na galę:</h3>
        <ul style="list-style: none; padding: 0;">
            <li>✅ Zawodnik A przez KO</li>
            <li>❌ Zawodnik C przez poddanie</li>
        </ul>

        <a href="#" class="btn">KUP PPV (DEMO)</a>
    </div>

    <footer>
        <p>&copy; 2026 Fan Page Stworzony na telefonie</p>
    </footer>

</body>
</html>
