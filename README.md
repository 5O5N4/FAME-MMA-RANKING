/* Podstawowe style */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    line-height: 1.6;
    color: #333;
    background-color: #fffaf0; /* Delikatny kremowy kolor */
}

/* Nawigacja */
header {
    background: #fff;
    padding: 1rem 5%;
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 1000;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: #d2691e; /* Kolor karmelowy */
}

nav ul {
    display: flex;
    list-style: none;
}

nav ul li a {
    text-decoration: none;
    color: #333;
    margin-left: 20px;
    transition: 0.3s;
}

nav ul li a:hover {
    color: #d2691e;
}

/* Hero Section */
.hero {
    height: 80vh;
    background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), 
                url('https://images.unsplash.com/photo-1578985545062-69928b1d9587?auto=format&fit=crop&w=1200&q=80'); /* Przykładowe zdjęcie */
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    color: white;
    margin-top: 60px;
}

.btn {
    display: inline-block;
    padding: 10px 25px;
    background: #d2691e;
    color: white;
    text-decoration: none;
    border-radius: 25px;
    margin-top: 20px;
    transition: 0.3s;
}

.btn:hover {
    background: #a0522d;
}

/* Galeria */
.gallery {
    padding: 50px 5%;
    text-align: center;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin-top: 30px;
}

.card {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.05);
}

.img-placeholder {
    font-size: 50px;
    background: #fdf5e6;
    height: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    margin-bottom: 15px;
}

/* Stopka */
footer {
    background: #333;
    color: white;
    text-align: center;
    padding: 40px 0;
}

