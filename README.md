<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lluvia de Amor</title>
  <style>
    body {
      margin: 0;
      background: #000;
      overflow: hidden;
    }
    canvas {
      display: block;
    }
    h1 {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      color: #ff69b4;
      font-family: sans-serif;
      font-size: 2em;
      text-shadow: 2px 2px 4px #000;
    }
  </style>
</head>
<body>
  <canvas id="canvas"></canvas>
  <h1>¿Quieres salir conmigo?</h1>
  <script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');

    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const hearts = [];
    for (let i = 0; i < 100; i++) {
      hearts.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: Math.random() * 20 + 10,
        speed: Math.random() * 3 + 1
      });
    }

    function drawHeart(x, y, size) {
      ctx.save();
      ctx.translate(x, y);
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.bezierCurveTo(0, -size / 2, -size, -size / 2, -size, 0);
      ctx.bezierCurveTo(-size, size, 0, size * 1.5, 0, size * 2);
      ctx.bezierCurveTo(0, size * 1.5, size, size, size, 0);
      ctx.bezierCurveTo(size, -size / 2, 0, -size / 2, 0, 0);
      ctx.closePath();
      ctx.fillStyle = 'pink';
      ctx.fill();
      ctx.restore();
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let heart of hearts) {
        drawHeart(heart.x, heart.y, heart.size);
        heart.y += heart.speed;
        if (heart.y > canvas.height) {
          heart.y = -heart.size * 2;
          heart.x = Math.random() * canvas.width;
        }
      }
      requestAnimationFrame(animate);
    }

    animate();
  </script>
</body>
</html>
