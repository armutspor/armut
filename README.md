<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Armut Spor</title>

<style>
body {
  margin: 0;
  background: #000;
  color: #fff;
  font-family: Arial, sans-serif;
}

/* HEADER */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 15px;
  border-bottom: 1px solid #2ecc71;
}

header h1 {
  color: #2ecc71;
  font-size: 20px;
  margin: 0;
}

header button {
  background: #2ecc71;
  border: none;
  padding: 6px 10px;
  cursor: pointer;
  font-weight: bold;
}

/* LAYOUT */
.container {
  display: flex;
  height: calc(100vh - 100px);
}

/* LEFT */
.left {
  width: 220px;
  border-right: 1px solid #2ecc71;
  padding: 10px;
}

.league {
  color: #2ecc71;
  cursor: pointer;
  margin-bottom: 5px;
}

.teams {
  display: none;
  font-size: 13px;
  margin-left: 10px;
}

/* CENTER */
.center {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
}

.transfer {
  border-bottom: 1px solid #333;
  padding: 8px 0;
}

/* RIGHT */
.right {
  width: 260px;
  border-left: 1px solid #2ecc71;
  padding: 10px;
}

.box {
  border: 1px solid #2ecc71;
  padding: 8px;
  margin-bottom: 10px;
  font-size: 13px;
}

.player {
  color: #2ecc71;
  cursor: pointer;
}

/* TICKER */
.ticker {
  border-top: 1px solid #2ecc71;
  padding: 8px;
  white-space: nowrap;
  overflow: hidden;
  color: #2ecc71;
}

.ticker span {
  display: inline-block;
  padding-left: 100%;
  animation: scroll 20s linear infinite;
}

@keyframes scroll {
  from { transform: translateX(0); }
  to { transform: translateX(-100%); }
}
</style>
</head>

<body>

<header>
  <h1>Armut Spor | Futbol Haberleri</h1>
  <div>
    <span id="clock"></span>
    <button>Uygulamayı Yükle</button>
  </div>
</header>

<div class="container">

  <div class="left">
    <div class="league" onclick="toggle(this)">
      🇹🇷 Türkiye
      <div class="teams">
        Galatasaray – 24P – 12M<br>
        Fenerbahçe – 22P – 12M<br>
        Beşiktaş – 20P – 12M
      </div>
    </div>

    <div class="league" onclick="toggle(this)">
      🇬🇧 Premier League
      <div class="teams">
        Arsenal – 30P – 13M<br>
        Man City – 28P – 13M
      </div>
    </div>
  </div>

  <div class="center">
    <div class="transfer">
      Emir | GS ➜ FB | €8M | 2028
    </div>
    <div class="transfer">
      İlber | Ajax ➜ ArmutSpor | Bedelsiz | 2027
    </div>
  </div>

  <div class="right">
    <div class="box">
      <b>Günün Maçları</b><br>
      20:00 GS – FB 📺<br>
      22:00 Arsenal – City 📺
    </div>

    <div class="box">
      <b>Kariyer Yolculuğu</b><br>
      <div class="player" onclick="alert('GS → Ajax → ArmutSpor')">Emir</div>
      <div class="player" onclick="alert('BJK → PSV → Ajax')">İlber</div>
    </div>
  </div>

</div>

<div class="ticker">
  <span>CANLI: GS 1-0 FB | Arsenal 2-2 City | Milan 0-1 Inter</span>
</div>

<script>
function toggle(el) {
  const t = el.querySelector(".teams");
  t.style.display = t.style.display === "block" ? "none" : "block";
}

function updateClock() {
  const d = new Date();
  document.getElementById("clock").innerText =
    d.toLocaleTimeString() + " " + d.toLocaleDateString();
}
setInterval(updateClock, 1000);
updateClock();
</script>

</body>
</html>
