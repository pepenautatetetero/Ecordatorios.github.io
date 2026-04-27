<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Reciclatorios</title>

<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<style>
body{
    margin: 0;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    background-color: #3f6b3f;
}

#map{
    height: 400px;
}

.header-top{
    background-color: #a8c3a0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 30px;
}

.menu{
    background-color: #6c8f5e;
    display: flex;
    justify-content: center;
    gap: 40px;
    padding: 15px;
}

.menu a{
    text-decoration: none;
    color: black;
    font-weight: bold;
}

section{
    padding: 40px;
    color: white;
}
</style>
</head>

<body>

<!-- MAPA -->
<div id="map"></div>

<!-- HEADER -->
<div class="header-top">
    <h1>RECICLATORIOS</h1>
</div>

<!-- MENU -->
<div class="menu">
    <a href="#aprende">Aprende</a>
    <a href="#donde">Dónde reciclar</a>
    <a href="#juegos">Juegos</a>
</div>

<!-- JUEGO QUIZ -->
<section id="juegos">
<h2>Quiz ♻️</h2>
<p id="pregunta"></p>
<div id="opciones"></div>
<p id="resultado"></p>
<button onclick="siguientePregunta()">Siguiente</button>
</section>

<!-- OTRAS SECCIONES -->
<section id="aprende">
<h2>Aprende a reciclar</h2>
<p>Información básica sobre reciclaje.</p>
</section>

<section id="donde">
<h2>Dónde reciclar</h2>
<p>Lugares de reciclaje.</p>
</section>

<script>
// MAPA
var map = L.map('map').setView([25.78, -100.18], 13);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);

L.marker([25.78, -100.18]).addTo(map)
  .bindPopup('Aquí estás 🚩')
  .openPopup();

// QUIZ
const preguntas = [
{
    pregunta: "¿Qué significan las 3R?",
    opciones: ["Reciclar, Reducir, Reutilizar", "Reubicar, Reducir, Reciclar", "Reutilizar, Rapidez, Reubicar"],
    correcta: 0
},
{
    pregunta: "¿Qué es el PET?",
    opciones: ["Polímero de Energía Térmica", "Polietileno Tereftalato", "Plástico transparente"],
    correcta: 1
}
];

let indice = 0;

function cargarPregunta(){
    const p = document.getElementById("pregunta");
    const op = document.getElementById("opciones");
    op.innerHTML = "";

    p.textContent = preguntas[indice].pregunta;

    preguntas[indice].opciones.forEach((o,i)=>{
        const btn = document.createElement("button");
        btn.textContent = o;
        btn.onclick = ()=>verificar(i);
        op.appendChild(btn);
    });
}

function verificar(i){
    const r = document.getElementById("resultado");
    if(i===preguntas[indice].correcta){
        r.textContent = "Correcto ✅";
    } else {
        r.textContent = "Incorrecto ❌";
    }
}

function siguientePregunta(){
    indice++;
    if(indice < preguntas.length){
        cargarPregunta();
    } else {
        document.getElementById("juegos").innerHTML = "<h2>Terminaste 🎉</h2>";
    }
}

cargarPregunta();
</script>

</body>
</html>
