<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aurex Corporation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: black;
            color: white;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: red;
            text-align: center;
            padding: 20px;
            position: relative;
        }
        header h1 {
            color: black;
            margin: 0;
        }
        header .home-btn {
            position: absolute;
            left: 20px;
            top: 20px;
            background-color: black;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            border-radius: 50%;
        }
        .container {
            text-align: center;
            margin-top: 20px;
        }
        .button {
            background-color: red;
            color: black;
            border: none;
            padding: 15px 25px;
            font-size: 18px;
            cursor: pointer;
            margin: 10px;
        }
        .button:hover {
            background-color: darkred;
        }
        .hidden {
            display: none;
        }
        .form-container {
            margin-top: 20px;
            padding: 20px;
            background-color: #222;
            border-radius: 10px;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
        }
        .form-container input, .form-container textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            background-color: #333;
            border: 1px solid #444;
            color: white;
        }
        footer {
            text-align: center;
            margin-top: 50px;
            color: gray;
        }
    </style>
</head>
<body>

<header>
    <button class="home-btn hidden" id="homeButton">🏠</button>
    <h1 id="mainTitle">Aurex Corporation</h1>
</header>

<div class="container" id="mainMenu">
    <button class="button" id="btnFormula1">Formula 1</button>
    <button class="button" id="btnAurexEnergy">Aurex Energy</button>
</div>

<div id="formula1Section" class="hidden">
    <button class="button" id="btnRegistrarEquipo">Registrar Equipo</button>
    <button class="button" id="btnRegistrarPiloto">Registrar Piloto</button>
</div>

<div id="aurexEnergySection" class="hidden">
    <button class="button" id="btnTropicalMango">Tropical Mango (Original)</button>
    <button class="button" id="btnPurplePulse">Purple Pulse (Uva)</button>
</div>

<!-- Formulario Registrar Equipo -->
<div id="formRegistrarEquipo" class="form-container hidden">
    <h2>Registrar Equipo</h2>
    <form id="formEquipo">
        <input type="text" name="nombre" placeholder="Nombre del Equipo" required>
        <input type="text" name="dueno" placeholder="Dueño (con @)" required>
        <input type="text" name="miembros" placeholder="Miembros" required>
        <input type="text" name="color" placeholder="Color" required>
        <input type="file" name="logo" required>
        <button type="submit" class="button">Enviar</button>
    </form>
</div>

<!-- Formulario Registrar Piloto -->
<div id="formRegistrarPiloto" class="form-container hidden">
    <h2>Registrar Piloto</h2>
    <form id="formPiloto">
        <input type="text" name="nombre" placeholder="Nombre IC" required>
        <input type="number" name="edad" placeholder="Edad IC" required>
        <input type="text" name="user" placeholder="User" required>
        <input type="number" name="numero" placeholder="Número de Piloto" required>
        <input type="file" name="foto" required>
        <button type="submit" class="button">Enviar</button>
    </form>
</div>

<!-- Formulario Hacer Pedido -->
<div id="formPedido" class="form-container hidden">
    <h2>Hacer Pedido</h2>
    <form id="formPedidoData">
        <input type="text" name="nombre" placeholder="Nombre IC" required>
        <input type="text" name="domicilio" placeholder="Domicilio" required>
        <button type="submit" class="button">Enviar Pedido</button>
    </form>
</div>

<footer>
    <p>Desarrollado por: jj26m</p>
</footer>

<script>
    const homeButton = document.getElementById("homeButton");
    const mainMenu = document.getElementById("mainMenu");
    const mainTitle = document.getElementById("mainTitle");

    const formula1Section = document.getElementById("formula1Section");
    const aurexEnergySection = document.getElementById("aurexEnergySection");

    const showSection = (title, section) => {
        console.log(`Mostrando la sección de: ${title}`);
        // Ocultar el menú principal y mostrar la sección correspondiente
        mainMenu.classList.add("hidden");
        mainTitle.textContent = title;
        section.classList.remove("hidden");
        homeButton.classList.remove("hidden");
    };

    const resetToHome = () => {
        console.log("Regresando al inicio...");
        // Volver al menú principal y ocultar todas las secciones
        mainMenu.classList.remove("hidden");
        mainTitle.textContent = "Aurex Corporation";
        formula1Section.classList.add("hidden");
        aurexEnergySection.classList.add("hidden");
        document.querySelectorAll(".form-container").forEach(form => form.classList.add("hidden"));
        homeButton.classList.add("hidden");
    };

    // Botones principales
    document.getElementById("btnFormula1").onclick = function() {
        console.log("Botón Formula 1 presionado");
        showSection("Formula 1", formula1Section);
    };

    document.getElementById("btnAurexEnergy").onclick = function() {
        console.log("Botón Aurex Energy presionado");
        showSection("Aurex Energy", aurexEnergySection);
    };

    // Botón de regresar
    homeButton.onclick = resetToHome;

    // Mostrar formulario para registrar equipo
    document.getElementById("btnRegistrarEquipo").onclick = () => {
        console.log("Formulario de registrar equipo mostrado");
        document.getElementById("formRegistrarEquipo").classList.remove("hidden");
        document.getElementById("formRegistrarPiloto").classList.add("hidden");
    };

    // Mostrar formulario para registrar piloto
    document.getElementById("btnRegistrarPiloto").onclick = () => {
        console.log("Formulario de registrar piloto mostrado");
        document.getElementById("formRegistrarPiloto").classList.remove("hidden");
        document.getElementById("formRegistrarEquipo").classList.add("hidden");
    };

    // Formularios de envío
    document.getElementById("formEquipo").onsubmit = async function(e) {
        e.preventDefault();
        const formData = new FormData(e.target);
        console.log("Formulario de equipo enviado:", formData);
        await fetch("https://discord.com/api/webhooks/1311859474004312064/FsFuWn6JBkIbK8bDkdr0ZQugA6LoRqvr0FYJQqa3x7V-I8YGz2QMhn-hrCSNxo19iS3G", {
            method: "POST",
            body: JSON.stringify({
                content: `**Nombre de Equipo:** ${formData.get("nombre")}\n**Dueño:** ${formData.get("dueno")}\n**Miembros:** ${formData.get("miembros")}\n**Color:** ${formData.get("color")}`
            }),
            headers: { "Content-Type": "application/json" }
        });
        resetToHome();
    };

    document.getElementById("formPiloto").onsubmit = async function(e) {
        e.preventDefault();
       
