<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Armut Spor</title>

<style>
:root{
  --green:#2ecc71;
  --dark:#000000;
  --white:#ffffff;
}

*{box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}

body{
  margin:0;
  background:var(--dark);
  color:var(--white);
}

/* HEADER */
header{
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding:10px 20px;
  border-bottom:1px solid var(--green);
}

header .left{
  display:flex;
  align-items:center;
  gap:10px;
}

header img{
  width:40px;
  height:40px;
}

header h1{
  font-size:20px;
  color:var(--green);
}

header .right{
  display:flex;
  align-items:center;
  gap:15px;
}

button{
  background:var(--green);
  border:none;
  padding:6px 10px;
  cursor:pointer;
  font-weight:bold;
}

/* MAIN LAYOUT */
main{
  display:grid;
  grid-template-columns:220px 1fr 260px;
  height:calc(100vh - 100px);
}

/* LEFT – LIGLER */
#leagues{
  border-right:1px solid var(--green);
  padding:10px;
  overflow-y:auto;
}

.league{
  cursor:pointer;
  margin-bottom:8px;
  color:var(--green);
}

.teams{
  margin-left:10px;
  font-size:13px;
  display:none;
}

/* CENTER – TRANSFER AKIŞI */
#center{
  padding:10px;
  overflow-y:auto;
}

.transfer{
  display:flex;
  align-items:center;
  gap:10px;
  border-bottom:1px solid #333;
  padding:8px 0;
}

.transfer img{
  width:40px;
  height:40px;
  border-radius:50%;
  background:#333;
}

/* RIGHT */
#right{
  border-left:1px solid var(--green);
  padding:10px;
}

.box{
  border:1px solid var(--green);
  padding:8px;
  margin-bottom:10px;
  font-size:13px;
}

.player{
  cursor:pointer;
  color:var(--green);
  margin-bottom:5px;
}

/* LIVE TICKER */
#ticker{
  white-space:nowrap;
  overflow:hidden;
  border-top:1px solid var(--green);
  padding:8px;
  color:var(--green);
}

#ticker span{
  display:inline-block;
  padding-left:100%;
  animation:scroll 20s linear infinite;
}

@keyframes scroll{
  0%{transform:translateX(0)}
  100%{transform:translateX(-100%)}
}
</style>
</head>

<body>

<header>
  <div class="left">
    <!-- LOGO -->
    <img src="logo.png" alt="Armut Spor">
    <h1>Futbol Haberleri</h1>
  </div>

  <div class="right">
    <div id="clock"></div>
    <button>Uygulamayı Yükle</button>
  </div>
</header>

<main>

  <!-- SOL -->
  <div id="leagues">
    <div class="league" onclick="toggleTeams(this)">
      🇹🇷 Türkiye
      <div class="teams">
        Galatasaray – 24P – 12M<br>
        Fenerbahçe – 22P – 12M<br>
        Beşiktaş – 20P – 12M
      </div>
    </div>

    <div class="league" onclick="toggleTeams(this)">
      🇬🇧 Premier League
      <div class="teams">
        Arsenal – 30P – 13M<br>
        City – 28P – 13M
      </div>
    </div>
  </div>

  <!-- ORTA -->
  <div id="center">
    <div class="transfer">
      <img>
      <div>
        <b>Emir</b><br>
        GS ➜ FB | €8M | 2028
      </div>
    </div>

    <div class="transfer">
      <img>
      <div>
        <b>İlber</b><br>
        Ajax ➜ ArmutSpor | Bedelsiz | 2027
      </div>
    </div>
  </div>

  <!-- SAĞ -->
  <div id="right">
    <div class="box">
      <b>Günün Maçları</b><br>
      20:00 GS – FB 🟢📺<br>
      22:00 Arsenal – City 🔵📺
    </div>

    <div class="box">
      <b>Kariyer Yolculuğu</b><br>
      <div class="player" onclick="alert('GS → Ajax → ArmutSpor')">Emir</div>
      <div class="player" onclick="alert('BJK → PSV → Ajax')">İlber</div>
    </div>
  </div>

</main>

<div id="ticker">
  <span>CANLI: GS 1-0 FB | Arsenal 2-2 City | Milan 0-1 Inter</span>
</div>

<script>
function toggleTeams(el){
  const t = el.querySelector('.teams');
  t.style.display = t.style.display === 'block' ? 'none' : 'block';
}

function updateClock(){
  const d = new Date();
  document.getElementById("clock").innerText =
    d.toLocaleTimeString() + " " + d.toLocaleDateString();
}
setInterval(updateClock,1000);
updateClock();
</script>

</body>
</html>
