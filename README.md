<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>You’ve Got Mail 💌</title>

<style>
body {
  margin: 0;
  height: 100vh;
  background: linear-gradient(135deg, #ffb6d9, #ff69b4);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Tahoma","Verdana",sans-serif;
  overflow: hidden;
}

/* ===== ENVELOPE SCREEN ===== */
.envelope-screen {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.mail-title {
  color: white;
  font-weight: bold;
  font-size: 18px;
  margin-bottom: 20px;
  text-shadow: 2px 2px #ff69b4;
}

.envelope {
  width: 220px;
  height: 140px;
  background: #fff;
  border: 4px solid #ffb6d9;
  position: relative;
  cursor: pointer;
  box-shadow: 8px 8px 0 #ff69b4;
  animation: float 3s ease-in-out infinite;
}

.envelope::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  border-left: 110px solid transparent;
  border-right: 110px solid transparent;
  border-top: 70px solid #ffe6f2;
  transform-origin: top;
  transition: transform 1s ease;
}

.envelope.open::before { transform: rotateX(180deg); }

.heart-stamp {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
}

.open-text {
  margin-top: 15px;
  color: white;
  font-weight: bold;
  animation: blink 1.2s infinite;
}

@keyframes float { 50% { transform: translateY(-10px); } }
@keyframes blink { 50% { opacity: 0; } }

/* ===== POPUP ===== */
.popup {
  width: 360px;
  background: #ffe6f2;
  border: 3px solid #ff69b4;
  box-shadow: 8px 8px 0 #ff1493;
  display: none;
  animation: popIn 1.3s cubic-bezier(.2,1.5,.5,1);
}

.title-bar {
  background: #ff69b4;
  color: white;
  padding: 6px 10px;
  font-weight: bold;
}

.content {
  padding: 20px;
  color: #d1006f;
  min-height: 120px;
}

.buttons {
  display: flex;
  justify-content: space-around;
  padding-bottom: 15px;
}

button {
  background: #ff69b4;
  border: 2px solid #ff1493;
  color: white;
  font-weight: bold;
  padding: 6px 14px;
  cursor: pointer;
}

@keyframes popIn {
  0% { transform: scale(0) translateY(300px); }
  70% { transform: scale(1.15) translateY(-10px); }
  100% { transform: scale(1); }
}

/* ===== HEART STORM ===== */
.heart {
  position: absolute;
  font-size: 32px;
  animation: floatUp 6s linear forwards;
  pointer-events: none;
}

@keyframes floatUp {
  to {
    transform: translateY(-120vh) rotate(360deg);
    opacity: 0;
  }
}

/* ===== FINAL TEXT ===== */
.final-text {
  position: absolute;
  font-size: 64px;
  color: white;
  font-weight: bold;
  text-shadow: 0 0 15px #ff69b4, 4px 4px #ff1493;
  opacity: 0;
  animation: fluffIn 3s ease forwards;
}

@keyframes fluffIn {
  from { transform: scale(0.5); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}
</style>
</head>

<body>

<div class="envelope-screen" id="envelopeScreen">
  <div class="mail-title">💌 YOU’VE GOT MAIL!</div>
  <div class="envelope" id="envelope" onclick="openEnvelope()">
    <div class="heart-stamp">💗</div>
  </div>
  <div class="open-text">OPEN ME</div>
</div>

<div class="popup" id="popup">
  <div class="title-bar">💌 YOU’VE GOT MAIL!</div>
  <div class="content" id="text"></div>
  <div class="buttons">
    <button onclick="accept()">💖 YES</button>
    <button onclick="accept()">😭 ABSOLUTELY YES</button>
  </div>
</div>

<script>
const message = [
  "Hey Sia 💕",
  "",
  "This message has been delivered with love from Rome...",
  "",
  "Will you be my Valentine? 💘"
];

let i = 0;
const textEl = document.getElementById("text");

function openEnvelope() {
  document.getElementById("envelope").classList.add("open");
  setTimeout(() => {
    document.getElementById("envelopeScreen").style.display = "none";
    document.getElementById("popup").style.display = "block";
    typeText();
  }, 1200);
}

function typeText() {
  if (i < message.length) {
    textEl.innerHTML += message[i] + "<br>";
    i++;
    setTimeout(typeText, 650);
  }
}

function accept() {
  document.getElementById("popup").style.display = "none";

  for (let j = 0; j < 250; j++) {
    setTimeout(createHeart, j * 40);
  }

  setTimeout(showFinalText, 4000);
}

function createHeart() {
  const el = document.createElement("div");
  el.className = "heart";
  el.textContent = Math.random() > 0.5 ? "💖" : "💋";
  el.style.left = Math.random() * window.innerWidth + "px";
  el.style.bottom = "-40px";
  el.style.fontSize = (24 + Math.random() * 40) + "px";
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 6000);
}

function showFinalText() {
  const text = document.createElement("div");
  text.className = "final-text";
  text.textContent = "I LOVE YOU SIA 💕";
  document.body.appendChild(text);
}
</script>

</body>
</html>
