<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title> 𝗥𝗔𝗝𝗔 𝗜𝗦 𝗕𝗥𝗔𝗡𝗗• SIM DATABASE</title>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@300;400;600;700&family=Italiana&display=swap" rel="stylesheet">

<style>
:root{
  --glass:rgba(255,255,255,.08);
  --border:rgba(255,255,255,.25);
  --shine:rgba(255,255,255,.35);
  --text:#f3f6f8;
  --muted:#b6c3cc;
}

*{box-sizing:border-box}

body{
  margin:0;
  min-height:100vh;
  font-family:'Manrope',system-ui;
  color:var(--text);
  display:flex;
  justify-content:center;
  padding:24px;

  /* CODE BACKGROUND */
  background:
    linear-gradient(rgba(5,6,8,.85), rgba(5,6,8,.95)),
    url("https://www.transparenttextures.com/patterns/cubes.png"),
    radial-gradient(circle at top, #1a1f25, #050608 70%);
}

/* APP */
.app{
  width:100%;
  max-width:420px;
}

/* MIRROR PANEL */
.mirror{
  position:relative;
  background:linear-gradient(
    135deg,
    rgba(255,255,255,.14),
    rgba(255,255,255,.04),
    rgba(255,255,255,.1)
  );
  backdrop-filter: blur(20px) saturate(150%);
  -webkit-backdrop-filter: blur(20px) saturate(150%);
  border:1px solid var(--border);
  border-radius:22px;
  padding:22px;
  margin-bottom:20px;
  overflow:hidden;
}

/* mirror shine */
.mirror::before{
  content:'';
  position:absolute;
  inset:-70%;
  background:linear-gradient(
    120deg,
    transparent 40%,
    rgba(255,255,255,.18),
    transparent 60%
  );
  transform:rotate(25deg);
  pointer-events:none;
}

/* HEADER */
.brand{
  text-align:center;
}
.brand h1{
  margin:0;
  font-family:'Italiana',serif;
  font-size:1.4rem;
  letter-spacing:3px;
}
.brand span{
  display:block;
  margin-top:6px;
  font-size:.7rem;
  letter-spacing:4px;
  color:var(--muted);
}

/* INPUT */
input{
  width:100%;
  padding:16px;
  border-radius:16px;
  background:rgba(0,0,0,.35);
  border:1px solid var(--border);
  color:var(--text);
  font-size:.95rem;
  outline:none;
}
input::placeholder{color:#9aa7b1}

/* BUTTON */
button{
  width:100%;
  margin-top:14px;
  padding:15px;
  border-radius:16px;
  background:rgba(255,255,255,.14);
  border:1px solid var(--border);
  color:var(--text);
  font-weight:600;
  letter-spacing:1px;
  cursor:pointer;
  transition:.3s;
}
button:hover{
  background:rgba(255,255,255,.22);
}

/* TERMINAL */
.terminal{
  display:none;
  background:rgba(0,0,0,.45);
  border-radius:16px;
  padding:14px;
  border:1px solid var(--border);
  font-size:.75rem;
  line-height:1.6;
  color:var(--muted);
}

/* RESULTS */
.results{display:none}
.result{
  background:rgba(0,0,0,.35);
  border-radius:16px;
  padding:14px;
  border:1px solid var(--border);
  margin-bottom:10px;
}
.row{
  font-size:.78rem;
  margin-bottom:6px;
}
.row b{
  font-weight:600;
  color:#ffffff;
}

/* CHANNEL LINK */
.channel{
  text-align:center;
  margin-top:18px;
}
.channel a{
  font-size:.75rem;
  letter-spacing:2px;
  text-decoration:none;
  color:#d7eaff;
  opacity:.85;
}
.channel a:hover{opacity:1}

/* FOOTER */
.footer{
  text-align:center;
  font-size:.6rem;
  letter-spacing:2px;
  color:#8b98a3;
  margin-top:14px;
}
</style>
</head>

<body>
<div class="app">

  <!-- HEADER -->
  <div class="mirror brand">
    <h1>𝘙𝘈𝘑𝘈 𝘐𝘚 𝘉𝘙𝘈𝘕𝘋</h1>
    <span>SIM DATABASE</span>
  </div>

  <!-- SEARCH -->
  <div class="mirror">
    <input id="target" placeholder="03XXXXXXXXX" maxlength="11">
    <button onclick="searchSIM()">SCAN</button>
  </div>

  <!-- TERMINAL -->
  <div id="terminal" class="terminal mirror"></div>

  <!-- RESULTS -->
  <div id="results" class="results"></div>

  <!-- CHANNEL LINK -->
  <div class="channel">
    <a href="https://chat.whatsapp.com/L5ifBu6PjJiDCKV5ekBuz1?mode=hqrt2" target="_blank">
      JOIN OUR WHATSAPP CHANNEL
    </a>
  </div>

  <!-- FOOTER -->
  <div class="footer">© 2025 𝐑𝐀𝐉𝐀 𝐈𝐒 𝐁𝐑𝐀𝐍𝐃</div>

</div>

<script>
const API = 'https://sim.f-a-k.workers.dev/?q=';
const terminal = document.getElementById('terminal');
const results = document.getElementById('results');

function log(msg){
  terminal.style.display='block';
  terminal.innerHTML += '> ' + msg + '<br>';
}

async function searchSIM(){
  const q = document.getElementById('target').value.replace(/\D/g,'');

  terminal.innerHTML='';
  results.innerHTML='';
  results.style.display='none';

  if(q.length !== 11){
    alert('Enter valid 11 digit number');
    return;
  }

  log('Mirror interface active...');
  log('Reading data through glass layer...');

  try{
    const r = await fetch(API + q);
    const j = await r.json();

    if(j.status !== 'success') throw 'No record';

    terminal.style.display='none';
    results.style.display='block';

    const arr = Array.isArray(j.data)?j.data:[j.data];
    arr.forEach(o=>{
      let html='<div class="result">';
      for(const k in o){
        html+=`<div class="row"><b>${k}</b>: ${o[k]}</div>`;
      }
      html+='</div>';
      results.innerHTML+=html;
    });

  }catch(e){
    log('Reflection unstable. Database unreachable.');
  }
}
</script>

</body>
</html>
