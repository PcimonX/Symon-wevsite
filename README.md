<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Love Game 💘</title>
  <style>
    body {
      text-align: center;
      background: pink;
      font-family: "Comic Sans MS", cursive;
      padding-top: 100px;
    }
    .question {
      font-size: 24px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      font-size: 18px;
      border: none;
      border-radius: 10px;
      margin: 10px;
      cursor: pointer;
      transition: 0.3s;
    }
    #yesButton {
      background-color: #ff66b2;
      color: white;
    }
    #noButton {
      background-color: #ff9999;
      color: white;
    }
    .gif {
      width: 200px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div id="valentine">
    <div class="question">Do you love me? 😘</div>
    <button id="yesButton" onclick="acceptLove()">Yes 💖</button>
    <button id="noButton" onclick="rejectLove()">No 😢</button>
  </div>

  <script>
    let noCount = 0;
    const message = [
      "Are you sure?",
      "Really sure?",
      "Please don’t say no 😢",
      "Last chance! 💔"
    ];

    const messageText = document.querySelector(".question");
    const noButton = document.getElementById("noButton");
    const yesButton = document.getElementById("yesButton");

    function rejectLove() {
      if (noCount < message.length) {
        messageText.innerText = message[noCount];
        noCount++;
        noButton.style.transform = `scale(${1 - noCount * 0.1})`;
        yesButton.style.transform = `scale(${1 + noCount * 0.1})`;
      }
      if (noCount === message.length) {
        noButton.style.display = "none";
      }
    }

    function acceptLove() {
      document.getElementById("valentine").innerHTML = `
        <img src="https://media.tenor.com/aEWN44S02ckAAAAC/kiss-kisses.gif" class="gif">
        <div class="question">YAYAYYAYAYAYAY I LOVE YOU SO MUCH AYYY SHEEEESH LITTLE KITTEN ♥</div>
      `;
      launchConfetti();
      startHeartRain();
    }

    // Optional: Fun effects when YES is clicked
    function launchConfetti() {
      const duration = 2000;
      const end = Date.now() + duration;
      (function frame() {
        confetti({
          particleCount: 3,
          angle: 60,
          spread: 55,
          origin: { x: 0 },
        });
        confetti({
          particleCount: 3,
          angle: 120,
          spread: 55,
          origin: { x: 1 },
        });
        if (Date.now() < end) {
          requestAnimationFrame(frame);
        }
      })();
    }

    function startHeartRain() {
      for (let i = 0; i < 20; i++) {
        const heart = document.createElement("div");
        heart.innerHTML = "💖";
        heart.style.position = "fixed";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.top = "-10px";
        heart.style.fontSize = Math.random() * 20 + 20 + "px";
        heart.style.animation = `fall ${2 + Math.random() * 3}s linear`;
        document.body.appendChild(heart);

        heart.addEventListener("animationend", () => heart.remove());
      }
    }

    const style = document.createElement("style");
    style.innerHTML = `
      @keyframes fall {
        to {
          transform: translateY(100vh);
          opacity: 0;
        }
      }
    `;
    document.head.appendChild(style);
  </script>

  <!-- Confetti library -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>
</body>
</html>
