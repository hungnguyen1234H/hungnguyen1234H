<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <title>Câu hỏi tình yêu</title>
  <style>
    body {
      text-align: center;
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #ffe6f0, #ffe9cc);
      overflow: hidden;
    }

    .wrapper {
      position: relative;
      display: inline-block;
      margin-top: 100px;
      border: 1px solid #ddd;
      padding: 20px;
      border-radius: 8px;
      background-color: #fff0f5;
      box-shadow: 0 0 15px rgba(255, 105, 180, 0.3);
    }

    .question {
      margin: 0 0 10px 0;
      font-size: 24px;
    }

    .bouncing-text {
      display: inline-block;
      animation: bounce 1s infinite, colorchange 3s infinite;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }

    @keyframes colorchange {
      0%   { color: #ff69b4; }
      25%  { color: #ff1493; }
      50%  { color: #ff6ec7; }
      75%  { color: #d87093; }
      100% { color: #ff69b4; }
    }

    .question-prompt {
      margin: 0 0 20px 0;
      color: #555;
    }

    .button-container {
      position: relative;
      width: 300px;
      height: 50px;
      margin: 0 auto 20px auto;
    }

    .yes-btn,
    .no-btn {
      position: absolute;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      user-select: none;
      border: none;
      border-radius: 5px;
      background-color: #ffb6c1;
      transition: background 0.3s;
    }

    .yes-btn:hover,
    .no-btn:hover {
      background-color: #ff69b4;
      color: white;
    }

    .yes-btn {
      left: 0;
      top: 0;
    }

    .no-btn {
      left: 200px;
      top: 0;
    }

    .gif {
      display: none;
      width: 300px;
      height: auto;
      margin: 20px auto 0 auto;
    }

    /* Trái tim rơi */
    .heart {
      position: fixed;
      top: -50px;
      font-size: 30px;
      animation: fall linear infinite;
      color: red;
      opacity: 0.8;
    }

    @keyframes fall {
      0% {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translateY(100vh) rotate(360deg);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <!-- Nhạc nền dễ thương -->
  <audio id="bgMusic" autoplay loop hidden>
    <source src="https://www.bensound.com/bensound-music/bensound-sunny.mp3" type="audio/mpeg" />
  </audio>

  <!-- Tiếng khóc nhõng nhẽo -->
  <audio id="crySound" hidden>
    <source src="https://cdn.pixabay.com/audio/2023/05/20/audio_232be9ef91.mp3" type="audio/mpeg" />
  </audio>

  <!-- WRAPPER -->
  <div class="wrapper">
    <h2 class="question">
      <span class="bouncing-text">Hương Giang có yêu anh hông?</span>
    </h2>
    <p class="question-prompt">Trả lời thật lòng đi nè 😳</p>

    <div class="button-container">
      <button class="yes-btn">Có 🥰</button>
      <button class="no-btn">Không 😤</button>
    </div>
  </div>

  <!-- GIF KHÓC -->
  <img class="gif" src="" alt="GIF khóc" />

  <script>
    const question = document.querySelector(".question");
    const gif = document.querySelector(".gif");
    const yesBtn = document.querySelector(".yes-btn");
    const noBtn = document.querySelector(".no-btn");
    const questionPrompt = document.querySelector(".question-prompt");
    const buttonContainer = document.querySelector(".button-container");

    const bgMusic = document.getElementById("bgMusic");
    const crySound = document.getElementById("crySound");

    // “Có” nhảy lung tung
    yesBtn.addEventListener("mouseover", () => {
      const containerRect = buttonContainer.getBoundingClientRect();
      const btnRect = yesBtn.getBoundingClientRect();

      const maxX = containerRect.width - btnRect.width;
      const maxY = containerRect.height - btnRect.height;

      const randomX = Math.floor(Math.random() * maxX);
      const randomY = Math.floor(Math.random() * maxY);

      yesBtn.style.left = randomX + "px";
      yesBtn.style.top = randomY + "px";
    });

    // “Không” hiện gif và tiếng khóc
    noBtn.addEventListener("click", () => {
      question.innerHTML = "Em hết yêu anh rồi, em hết thương anh rồi😭😭💔";
      gif.src = "https://media.giphy.com/media/vvc1dJPLEU2QOw9cXy/giphy.gif";
      gif.style.display = "block";

      yesBtn.style.display = "none";
      noBtn.style.display = "none";
      questionPrompt.style.display = "none";

      bgMusic.pause();
      crySound.play();
    });

    // Trái tim rơi
    setInterval(() => {
      const heart = document.createElement("div");
      heart.classList.add("heart");
      heart.innerHTML = "❤️";
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.animationDuration = 2 + Math.random() * 3 + "s";
      document.body.appendChild(heart);

      setTimeout(() => {
        heart.remove();
      }, 5000);
    }, 300);
  </script>
</body>
</html>
