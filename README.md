<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8" />
  <title>İyi ki Doğdun Ablam! 🎂</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #000;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #f8bbd0;
      user-select: none;
    }

    h1 {
      font-size: 3rem;
      color: #fce4ec;
      text-shadow: 0 0 10px #ff4081;
      margin: 0.5rem 0;
      animation: fadeIn 2s ease forwards;
    }

    p {
      max-width: 600px;
      font-size: 1.3rem;
      color: #f8bbd0;
      margin: 1rem auto;
      opacity: 0;
      text-shadow: 1px 1px 3px rgba(255, 255, 255, 0.3);
      animation: fadeIn 3s ease forwards 2s;
    }

    .heart {
      color: #f06292;
      font-size: 2rem;
      margin: 1rem 0;
      animation: pulse 1.5s infinite;
      text-shadow: 0 0 6px #ff80ab;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
      pointer-events: none;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }

    @keyframes pulse {
      0% {transform: scale(1);}
      50% {transform: scale(1.2);}
      100% {transform: scale(1);}
    }
  </style>
</head>
<body>
  <canvas id="confetti"></canvas>
  <h1>🎉 İyi ki Doğdun Ablam! 🎂</h1>
  <div class="heart">❤️</div>
  <p>
    Hayatımın en güzel ışıklarından birisin.<br />
    Ne zaman yolumu kaybetsem, sen yıldız oldun.<br />
    Bu küçük sürpriz, seni gülümsetmek için.<br />
    Nice mutlu yaşlara, nice umut dolu günlere! 🌟<br />
    Seni çok seviyorum...
  </p>

  <script>
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d');
    let W = window.innerWidth;
    let H = window.innerHeight;
    canvas.width = W;
    canvas.height = H;

    class Confetti {
      constructor() {
        this.x = Math.random() * W;
        this.y = Math.random() * -H; // start above screen
        this.size = Math.random() * 8 + 4;
        this.speedY = Math.random() * 3 + 2;
        this.speedX = (Math.random() - 0.5) * 1.5;
        this.color = `hsl(${Math.random() * 360}, 100%, 70%)`;
        this.tilt = Math.random() * 10 - 10;
        this.tiltAngle = 0;
        this.tiltAngleSpeed = Math.random() * 0.1 + 0.05;
      }
      update() {
        this.tiltAngle += this.tiltAngleSpeed;
        this.y += this.speedY;
        this.x += this.speedX;
        this.tilt = Math.sin(this.tiltAngle) * 15;

        if (this.y > H) {
          this.y = Math.random() * -20;
          this.x = Math.random() * W;
        }
        if (this.x > W) this.x = 0;
        else if (this.x < 0) this.x = W;
      }
      draw() {
        ctx.beginPath();
        ctx.lineWidth = this.size / 2;
        ctx.strokeStyle = this.color;
        ctx.moveTo(this.x + this.tilt + this.size / 2, this.y);
        ctx.lineTo(this.x + this.tilt, this.y + this.tilt + this.size);
        ctx.stroke();
      }
    }

    let confettis = [];
    for (let i = 0; i < 150; i++) {
      confettis.push(new Confetti());
    }

    function animate() {
      ctx.clearRect(0, 0, W, H);
      confettis.forEach(c => {
        c.update();
        c.draw();
      });
      requestAnimationFrame(animate);
    }

    window.addEventListener('resize', () => {
      W = window.innerWidth;
      H = window.innerHeight;
      canvas.width = W;
      canvas.height = H;
    });

    window.onload = () => {
      animate();
    };
  </script>
</body>
</html>

