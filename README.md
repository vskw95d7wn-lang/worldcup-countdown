
<!DOCTYPE html>
<html lang="en">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>World Cup Countdown</title>
<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  min-height: 100vh;
  font-family: Arial, sans-serif;
  color: white;
  background: linear-gradient(145deg,#071b12,#020806);
  text-align: center;
  padding: 25px 18px;
}

.container {
  max-width: 550px;
  margin: auto;
}

h1 {
  font-size: 30px;
  margin-top: 35px;
}

.subtitle { color: #a5c5ae; }

.card {
  margin-top: 25px;
  padding: 28px 15px;
  border-radius: 18px;
  border: 1px solid #ffffff30;
  background: #ffffff10;
  cursor: pointer;
}

.card:active { transform: scale(.97); }

.emoji { font-size: 55px; }

.card h2 { margin-bottom: 8px; }

.card p { color: #a5c5ae; }

button {
  background: #1b8145;
  color: white;
  border: none;
  padding: 13px 25px;
  border-radius: 10px;
  font-size: 15px;
  margin-top: 15px;
  cursor: pointer;
}

#countdown {
  display: none;
}

.days {
  font-size: clamp(85px,24vw,145px);
  font-weight: bold;
  margin-top: 35px;
}

.remaining {
  color: #9de5b0;
  letter-spacing: 4px;
}

.timer {
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 10px;
  margin-top: 30px;
}

.unit {
  background: #ffffff12;
  border: 1px solid #ffffff22;
  border-radius: 13px;
  padding: 18px 5px;
}

.number {
  font-size: 26px;
  font-weight: bold;
}

small { color: #a5c5ae; }

footer {
  margin-top: 45px;
  color: #789684;
  font-size: 11px;
  letter-spacing: 2px;
}

.back {
  background: #303c34;
  margin-top: 30px;
}
</style>
</head>

<body>
<div class="container">

<div id="home">
  <h1>WORLD CUP COUNTDOWN</h1>
  <p class="subtitle">Choose your tournament</p>

  <div class="card" onclick="openCup('fifa')">
    <div class="emoji">⚽</div>
    <h2>FIFA WORLD CUP</h2>
    <p>2030 • FOOTBALL</p>
    <button>VIEW COUNTDOWN</button>
  </div>

  <div class="card" onclick="openCup('cricket')">
    <div class="emoji">🏏</div>
    <h2>CRICKET WORLD CUP</h2>
    <p>2027 • CRICKET</p>
    <button>VIEW COUNTDOWN</button>
  </div>
</div>

<div id="countdown">
  <h1 id="cupTitle"></h1>
  <p class="subtitle" id="cupSubtitle"></p>

  <div class="days" id="days">---</div>
  <div class="remaining">DAYS REMAINING</div>

  <div class="timer">
    <div class="unit">
      <div class="number" id="hours">00</div>
      <small>HOURS</small>
    </div>
    <div class="unit">
      <div class="number" id="minutes">00</div>
      <small>MINUTES</small>
    </div>
    <div class="unit">
      <div class="number" id="seconds">00</div>
      <small>SECONDS</small>
    </div>
  </div>

  <button class="back" onclick="goHome()">← BACK TO HOME</button>
</div>

<footer>FOOTBALL & CRICKET • ONE WORLD</footer>
</div>

<script>
let targetDate;

function openCup(type) {
  document.getElementById("home").style.display = "none";
  document.getElementById("countdown").style.display = "block";

  if(type === "fifa") {
    document.getElementById("cupTitle").textContent =
      "FIFA WORLD CUP 2030";
    document.getElementById("cupSubtitle").textContent =
      "THE WORLD'S BIGGEST FOOTBALL EVENT";
    targetDate = new Date("2030-06-13T00:00:00+05:30").getTime();
    document.body.style.background =
      "linear-gradient(145deg,#071b12,#020806)";
  } else {
    document.getElementById("cupTitle").textContent =
      "CRICKET WORLD CUP 2027";
    document.getElementById("cupSubtitle").textContent =
      "THE WORLD'S BIGGEST ODI CRICKET EVENT";
    targetDate = new Date("2027-10-02T00:00:00+05:30").getTime();
    document.body.style.background =
      "linear-gradient(145deg,#102449,#020817)";
  }

  updateCountdown();
}

function goHome() {
  document.getElementById("home").style.display = "block";
  document.getElementById("countdown").style.display = "none";
}

function updateCountdown() {
  if(!targetDate) return;

  const diff = targetDate - Date.now();

  if(diff <= 0) {
    document.getElementById("days").textContent = "0";
    document.getElementById("hours").textContent = "00";
    document.getElementById("minutes").textContent = "00";
    document.getElementById("seconds").textContent = "00";
    return;
  }

  document.getElementById("days").textContent =
    Math.floor(diff / 86400000);

  document.getElementById("hours").textContent =
    String(Math.floor(diff / 3600000) % 24).padStart(2,"0");

  document.getElementById("minutes").textContent =
    String(Math.floor(diff / 60000) % 60).padStart(2,"0");

  document.getElementById("seconds").textContent =
    String(Math.floor(diff / 1000) % 60).padStart(2,"0");
}

setInterval(updateCountdown,1000);
</script>
</body>
</html>
