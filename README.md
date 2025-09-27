<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>💖 Para Ti 💖</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: black;
      font-family: "Segoe Script", cursive;
      color: white;
    }

    h1 {
      position: absolute;
      top: 20px;
      width: 100%;
      text-align: center;
      font-size: 2.5em;
      color: #ff4da6;
      text-shadow: 0 0 15px #ff99cc, 0 0 30px #ff3385;
      animation: brillo 2s infinite alternate;
      z-index: 10;
    }

    .mensaje {
      position: absolute;
      bottom: 40px;
      width: 100%;
      text-align: center;
      font-size: 2em;
      color: #ffcccc;
      text-shadow: 0 0 10px #ff4da6, 0 0 20px #ff1a66;
      animation: flotar 5s infinite alternate ease-in-out;
      z-index: 10;
    }

    @keyframes brillo {
      from { text-shadow: 0 0 10px #ff99cc; }
      to { text-shadow: 0 0 30px #ff3385, 0 0 50px #ff004c; }
    }

    @keyframes flotar {
      0% { transform: translateY(0px) scale(1); }
      100% { transform: translateY(-15px) scale(1.1); }
    }

    canvas {
      display: block;
    }

    /* ---- Carrusel 3D ---- */
    .carrusel {
      position: absolute;
      top: 50%;
      left: 50%;
      transform-style: preserve-3d;
      transform: translate(-50%, -50%) rotateY(0deg);
      width: 400px;
      height: 400px;
      animation: girar 20s infinite linear;
      z-index: 5;
    }

    .carrusel img {
      position: absolute;
      width: 120px;
      height: 120px;
      object-fit: cover;
      border-radius: 20px;
      box-shadow: 0 0 20px #ff4da6, 0 0 40px #ff1a66;
      transition: transform 0.5s;
    }

    .carrusel img:hover {
      transform: scale(1.3);
      z-index: 100;
    }

    @keyframes girar {
      from { transform: translate(-50%, -50%) rotateY(0deg); }
      to { transform: translate(-50%, -50%) rotateY(360deg); }
    }
  </style>
</head>
<body>
  <h1>💖 Para Ti 💖</h1>
  <div class="mensaje" id="mensaje">Te quiero</div>
  <canvas id="corazon"></canvas>

  <!-- Carrusel de fotos -->
  <div class="carrusel" id="carrusel">
    <img src="imagen/img1.jpg">
    <img src="imagen/img2.jpg">
    <img src="imagen/img3.jpg">
    <img src="imagen/img4.jpg">
    <img src="imagen/img5.jpg">
    <img src="imagen/img6.jpg">
    <img src="imagen/img7.jpg">
    <img src="imagen/img8.jpg">
    <img src="imagen/img9.jpg">
    <img src="imagen/img10.jpg">
    <img src="imagen/img11.jpg">
  </div>

  <script>
    const canvas = document.getElementById("corazon");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const hearts = [];
    const particles = [];

    // Lluvia de corazones
    for (let i = 0; i < 100; i++) {
      hearts.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: Math.random() * 20 + 10,
        speed: Math.random() * 2 + 1
      });
    }

    // Corazón gigante con partículas
    function crearCorazon() {
      const centerX = canvas.width / 2;
      const centerY = canvas.height / 2;
      const scale = 15;
      for (let i = 0; i < 2500; i++) {
        const t = Math.random() * Math.PI * 2;
        const x = scale * 16 * Math.pow(Math.sin(t), 3);
        const y = -scale * (13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
        particles.push({
          x: centerX + x,
          y: centerY + y,
          size: Math.random() * 2 + 1,
          alpha: Math.random()
        });
      }
    }
    crearCorazon();

    function dibujar() {
      ctx.fillStyle = "rgba(0,0,0,0.2)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      // Lluvia
      ctx.fillStyle = "#ff4da6";
      ctx.font = "20px Arial";
      hearts.forEach(h => {
        ctx.fillText("💖", h.x, h.y);
        h.y += h.speed;
        if (h.y > canvas.height) {
          h.y = -20;
          h.x = Math.random() * canvas.width;
        }
      });

      // Corazón de partículas
      particles.forEach(p => {
        ctx.beginPath();
        ctx.fillStyle = `rgba(255,77,166,${p.alpha})`;
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fill();
      });
    }
    setInterval(dibujar, 30);

    // ----------- TEXTOS -----------
    const mensajes = [
      "Te quiero ❤️",
      "Eres especial 💕",
      "Mi persona favorita 🌸",
      "Me haces feliz 😍"
    ];
    let index = 0;
    const mensajeEl = document.getElementById("mensaje");

    setInterval(() => {
      index = (index + 1) % mensajes.length;
      mensajeEl.textContent = mensajes[index];
    }, 3000);

    // ----------- Carrusel 3D posiciones -----------
    const carrusel = document.getElementById("carrusel");
    const imgs = carrusel.querySelectorAll("img");
    const total = imgs.length;
    const angle = 360 / total;

    imgs.forEach((img, i) => {
      img.style.transform = `rotateY(${i * angle}deg) translateZ(500px)`;
    });

    window.addEventListener("resize", () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
