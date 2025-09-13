<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Invitation for Ara</title>
  <style>
    body {
      background: linear-gradient(to bottom right, #fdfbfb, #ebedee); /* soft eye-friendly */
      color: #333;
      text-align: center;
      font-family: "Segoe UI", Tahoma, sans-serif;
      overflow: hidden;
    }
    h1 {
      margin-top: 20px;
      color: #b23a48;
      text-shadow: 1px 1px 3px #fff;
    }
    #stitch {
      width: 160px;
      margin: 15px;
    }
    button {
      font-size: 16px;
      font-weight: 600;
      padding: 10px 22px;
      margin: 15px;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      box-shadow: 2px 2px 6px rgba(0,0,0,0.15);
      transition: transform 0.2s;
    }
    button:hover {
      transform: scale(1.08);
    }
    #yesBtn {
      background-color: #ff9eb5;
      color: white;
    }
    #noBtn {
      background-color: #f46a6a;
      color: white;
    }
    #message {
      margin-top: 12px;
      font-size: 15px;
      color: #555;
      font-style: italic;
      min-height: 24px;
    }
    #finalScene {
      display: none;
      margin-top: 30px;
    }
    #finalScene img {
      width: 200px;
      margin-bottom: 15px;
    }
    #finalScene p {
      font-size: 18px;
      font-weight: bold;
      color: #b23a48;
    }
    .heart, .sticker {
      position: absolute;
      animation: floatUp 6s linear infinite;
      user-select: none;
    }
    .heart {
      font-size: 22px;
      color: #e57373;
    }
    .sticker {
      width: 60px;
    }
    @keyframes floatUp {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(-650px); opacity: 0; }
    }
  </style>
</head>
<body>

  <h1>Ara, will you go on a date with me?</h1>
  <img id="stitch" src="stitch.png" alt="Stitch">

  <div id="buttons">
    <button id="yesBtn">Yes</button>
    <button id="noBtn">No</button>
  </div>

  <p id="message"></p>

  <!-- Final scene after Yes -->
  <div id="finalScene">
    <img src="stitch_flowers.png" alt="Stitch with flowers">
    <p>"Let all that you do be done in love." – 1 Corinthians 16:14</p>
  </div>

  <audio id="music" src="https://ia801603.us.archive.org/3/items/AmazingGrace_201303/AmazingGrace.mp3"></audio>

  <script>
    const yesBtn = document.getElementById("yesBtn");
    const noBtn = document.getElementById("noBtn");
    const buttons = document.getElementById("buttons");
    const music = document.getElementById("music");
    const message = document.getElementById("message");
    const finalScene = document.getElementById("finalScene");

    const noMessages = [
      "Think carefully, Ara. A yes could make this memorable.",
      "Opportunities like this don’t knock twice.",
      "I promise, it will be worth your time.",
      "Even Stitch agrees that yes is the better choice.",
      "You may laugh now, but you’ll enjoy it later.",
      "It seems only Yes remains."
    ];
    let noClickCount = 0;

    // YES button click
    yesBtn.addEventListener("click", () => {
      document.querySelector("h1").innerText = "Thank you, Ara.";
      message.innerText = "";
      buttons.style.display = "none"; // hide buttons
      finalScene.style.display = "block"; // show final scene
      music.play();

      // hearts and stickers
      for (let i = 0; i < 20; i++) {
        setTimeout(createHeart, i * 300);
        if (i % 4 === 0) setTimeout(createSticker, i * 400);
      }
    });

    // NO button click
    noBtn.addEventListener("click", () => {
      if (noClickCount < noMessages.length) {
        message.innerText = noMessages[noClickCount];
        noClickCount++;
      } 
      if (noClickCount >= noMessages.length) {
        noBtn.remove(); // disappears after last message
      }
    });

    // floating hearts
    function createHeart() {
      const heart = document.createElement("div");
      heart.classList.add("heart");
      heart.innerText = "♥";
      document.body.appendChild(heart);
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.top = window.innerHeight + "px";
      setTimeout(() => heart.remove(), 6000);
    }

    // floating Stitch stickers
    function createSticker() {
      const sticker = document.createElement("img");
      sticker.src = "sticker.png"; // use another Stitch sticker image
      sticker.classList.add("sticker");
      document.body.appendChild(sticker);
      sticker.style.left = Math.random() * window.innerWidth + "px";
      sticker.style.top = window.innerHeight + "px";
      setTimeout(() => sticker.remove(), 6000);
    }
  </script>
</body>
</html>
