<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stick Hero - Jared Ramirez</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Stick Hero Game</h1>
    <p>by Your Name</p>
  </header>

  <main>
    <section class="game-section">
      <canvas id="gameCanvas" width="400" height="400"></canvas>
    </section>

  </main>

  <footer>
    <p>&copy; 2025 Jared Ramirez| Stick Hero Project</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>





style.css
body {
  font-family: Arial, sans-serif;
  background: linear-gradient(to bottom, #a8edea, #fed6e3);
  margin: 0;
  padding: 0;
  text-align: center;
}

header {
  background-color: #333;
  color: white;
  padding: 20px 0;
}

h1 {
  font-size: 2em;
  margin: 0;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 20px;
}

.game-section {
  background: white;
  border: 3px solid #333;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0,0,0,0.2);
  padding: 10px;
  margin-bottom: 20px;
}

canvas {
  background-image: url('background.jpg');
  background-size: cover;
  border-radius: 8px;
}

.reflection {
  max-width: 600px;
  background-color: #fff;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 0 8px rgba(0,0,0,0.2);
}

footer {
  background-color: #333;
  color: white;
  padding: 10px 0;
  margin-top: 30px;
}

/* Responsive */
@media (max-width: 600px) {
  canvas {
    width: 300px;
    height: 300px;
  }
}


script.js
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

let stickLength = 0;
let growing = false;
let baseX = 80;
let baseY = 350;

function drawBase() {
  ctx.fillStyle = "#333";
  ctx.fillRect(baseX - 50, baseY, 100, 20);
}

function drawStick() {
  ctx.strokeStyle = "black";
  ctx.lineWidth = 5;
  ctx.beginPath();
  ctx.moveTo(baseX, baseY);
  ctx.lineTo(baseX, baseY - stickLength);
  ctx.stroke();
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drawBase();
  drawStick();
  requestAnimationFrame(draw);
}

canvas.addEventListener("mousedown", () => { growing = true; });
canvas.addEventListener("mouseup", () => { growing = false; });

function update() {
  if (growing && stickLength < 300) stickLength += 2;
  requestAnimationFrame(update);
}

draw();
update();
