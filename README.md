<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Магазин Telegram Stars</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      font-family: "Segoe UI", sans-serif;
      height: 100%;
      overflow: hidden;
      background: #000;
      color: #fff;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 30px 20px;
      height: 100vh;
      text-align: center;
    }

    .box {
      background: rgba(0, 0, 0, 0.65);
      border-radius: 20px;
      padding: 30px;
      max-width: 480px;
      width: 100%;
      box-shadow: 0 0 30px rgba(255, 255, 255, 0.1);
      animation: fadeIn 1.2s ease;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }

    h1 {
      font-size: 28px;
      margin-bottom: 10px;
    }

    .highlight {
      color: #ffd700;
    }

    p {
      font-size: 16px;
      margin: 10px 0;
    }

    ul {
      list-style: none;
      padding: 0;
      margin: 20px 0;
      text-align: left;
    }

    li {
      margin-bottom: 12px;
      padding-left: 28px;
      position: relative;
      font-size: 15px;
    }

    li::before {
      content: "✨";
      position: absolute;
      left: 0;
    }

    .btn {
      background: linear-gradient(to right, #ffd700, #fff200);
      color: #000;
      border: none;
      padding: 16px 30px;
      border-radius: 50px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      text-decoration: none;
      display: inline-block;
      margin-top: 20px;
      transition: all 0.3s ease;
      box-shadow: 0 6px 20px rgba(255, 255, 0, 0.4);
    }

    .btn:hover {
      transform: scale(1.05);
      box-shadow: 0 8px 30px rgba(255, 255, 0, 0.6);
    }

    .note {
      font-size: 13px;
      margin-top: 15px;
      color: #ccc;
    }

    .timer {
      font-size: 20px;
      margin-top: 15px;
      font-weight: bold;
      color: #ffda00;
    }
  </style>
</head>
<body>

<canvas id="stars"></canvas>

<div class="container">
  <div class="box">
    <h1>💫 <span class="highlight">Telegram Stars</span> со скидкой!</h1>
    <p>Покупай у нас — быстро, дёшево, мгновенно!</p>

    <ul>
      <li>Дарите подарки друзьям прямо в Telegram 🎁</li>
      <li>Открывайте VIP и фишки в ботах 🔓</li>
      <li>Цены ниже, чем у Telegram 🌍</li>
      <li>Stars моментально приходят на аккаунт 💨</li>
      <li>Оплата за 10 секунд ⏱️</li>
    </ul>

    <div class="timer">
      Акция закончится через: <span id="countdown">--:--:--</span>
    </div>

    <a href="https://t.me/BitStarRobot?start=BITmint" class="btn">🔥 Купить Stars сейчас</a>
    <p class="note">Доступны любые объёмы: от 100 до 1 000 000+</p>
  </div>
</div>

<script>
  // Анимация звёзд
  const canvas = document.getElementById('stars');
  const ctx = canvas.getContext('2d');
  let w, h;
  let stars = [];

  function resize() {
    w = canvas.width = window.innerWidth;
    h = canvas.height = window.innerHeight;
    stars = Array.from({length: 100}, () => ({
      x: Math.random() * w,
      y: Math.random() * h,
      radius: Math.random() * 1.5 + 0.5,
      dx: Math.random() * 0.5 - 0.25,
      dy: Math.random() * 0.5 - 0.25,
    }));
  }

  function animate() {
    ctx.clearRect(0, 0, w, h);
    ctx.fillStyle = '#fff';
    stars.forEach(star => {
      ctx.beginPath();
      ctx.arc(star.x, star.y, star.radius, 0, 2 * Math.PI);
      ctx.fill();
      star.x += star.dx;
      star.y += star.dy;

      if (star.x < 0 || star.x > w) star.dx *= -1;
      if (star.y < 0 || star.y > h) star.dy *= -1;
    });
    requestAnimationFrame(animate);
  }

  window.addEventListener('resize', resize);
  resize();
  animate();

  // Таймер до конца акции (например, через 2 часа)
  const countdown = document.getElementById("countdown");
  const endTime = new Date().getTime() + 2 * 60 * 60 * 1000; // 2 часа

  function updateCountdown() {
    const now = new Date().getTime();
    const distance = endTime - now;

    if (distance < 0) {
      countdown.innerText = "00:00:00";
      return;
    }

    const hours = Math.floor((distance / (1000 * 60 * 60)));
    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((distance % (1000 * 60)) / 1000);

    countdown.innerText =
      (hours < 10 ? "0" + hours : hours) + ":" +
      (minutes < 10 ? "0" + minutes : minutes) + ":" +
      (seconds < 10 ? "0" + seconds : seconds);
  }

  setInterval(updateCountdown, 1000);
</script>

</body>
</html>


