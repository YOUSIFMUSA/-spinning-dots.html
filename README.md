
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Spinning Dots with Name</title>
  <style>
    body {
      margin: 0;
      background: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <canvas id="dotsCanvas"></canvas>

  <script>
    const canvas = document.getElementById('dotsCanvas');
    const ctx = canvas.getContext('2d');

    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const dots = [];
    const numDots = 400;
    const radius = 150;

    for (let i = 0; i < numDots; i++) {
      const theta = Math.random() * 2 * Math.PI;
      const phi = Math.acos(2 * Math.random() - 1);
      const x = radius * Math.sin(phi) * Math.cos(theta);
      const y = radius * Math.sin(phi) * Math.sin(theta);
      const z = radius * Math.cos(phi);

      dots.push({x, y, z});
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      const time = Date.now() * 0.001;

      for (let i = 0; i < dots.length; i++) {
        let {x, y, z} = dots[i];

        // دوران حول محور Y
        let angle = time;
        let dx = x * Math.cos(angle) - z * Math.sin(angle);
        let dz = x * Math.sin(angle) + z * Math.cos(angle);

        let scale = 500 / (500 + dz);
        let screenX = dx * scale + canvas.width / 2;
        let screenY = y * scale + canvas.height / 2;

        ctx.beginPath();
        ctx.arc(screenX, screenY, 2, 0, 2 * Math.PI);
        ctx.fillStyle = '#00ffff';
        ctx.fill();
      }

      // رسم الاسم "Yousif" في الوسط
      ctx.fillStyle = '#00ffff';
      ctx.font = 'bold 40px Arial';
      ctx.textAlign = 'center';
      ctx.fillText('Yousif', canvas.width / 2, canvas.height / 2 + 15);

      requestAnimationFrame(draw);
    }

    draw();
  </script>
</body>
</html>
