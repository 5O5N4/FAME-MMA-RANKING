<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Strona typu Key-Drop - Projekt</title>
    <style>
        body {
            background-color: #1a1a1a;
            color: white;
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .case-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            width: 80%;
        }

        .case-card {
            background: linear-gradient(145deg, #232323, #2b2b2b);
            border: 1px solid #3d3d3d;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
        }

        .case-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 20px rgba(255, 204, 0, 0.2);
            border-color: #ffcc00;
        }

        .case-img {
            width: 150px;
            height: auto;
            margin-bottom: 15px;
        }

        .price {
            color: #ffcc00;
            font-weight: bold;
            font-size: 1.2em;
        }

        button {
            background-color: #ffcc00;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="case-container">
        <!-- Przykładowa skrzynka -->
        <div class="case-card">
            <img src="https://via.placeholder.com/150" alt="Skrzynka" class="case-img">
            <h3>MILITARY BOX</h3>
            <p class="price">19.99 PLN</p>
            <button>OTWÓRZ</button>
        </div>

        <div class="case-card">
            <img src="https://via.placeholder.com/150" alt="Skrzynka" class="case-img">
            <h3>GOLDEN CASE</h3>
            <p class="price">49.00 PLN</p>
            <button>OTWÓRZ</button>
        </div>
    </div>

</body>
</html>
