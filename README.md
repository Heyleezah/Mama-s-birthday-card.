<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Birthday Card</title>
<style>
  body {
    margin:0;
    height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    background: linear-gradient(135deg,#ff7ac8,#9d4edd);
    font-family: 'Segoe UI', Tahoma, sans-serif;
    overflow:hidden;
  }canvas{position:fixed;top:0;left:0;pointer-events:none;}

.heart { position:absolute; color:#ff4d8d; animation: floatUp 6s linear infinite; font-size:20px; opacity:0.7; } @keyframes floatUp { from { transform: translateY(100vh); opacity:1; } to { transform: translateY(-10vh); opacity:0; } }

.card { width:340px; height:460px; perspective:1000px; z-index:2; } .inner { width:100%; height:100%; transition: transform 1s; transform-style: preserve-3d; position: relative; cursor:pointer; } .card:hover .inner { transform: rotateY(180deg); } .side { position:absolute; width:100%; height:100%; backface-visibility:hidden; border-radius:20px; box-shadow:0 10px 25px rgba(0,0,0,0.25); display:flex; align-items:center; justify-content:center; text-align:center; padding:20px; } .front { background:white; flex-direction:column; } .front h1 { font-size:1.8em; color:#ff4d8d; } .cake { font-size:60px; }

.photo { width:120px; height:120px; border-radius:50%; object-fit:cover; border:4px solid #ff7ac8; margin:10px 0; }

.back { background:#fff0fb; transform: rotateY(180deg); } .back h2 { color:#9d4edd; } .back p { color:#444; font-size:1.1em; }

button { margin-top:15px; padding:10px 18px; border:none; border-radius:20px; background:linear-gradient(90deg,#ff4d8d,#9d4edd); color:white; font-size:14px; cursor:pointer; } </style>

</head>
<body><canvas id="confetti"></canvas>

<div class="heart" style="left:10%; animation-delay:0s">❤</div>
<div class="heart" style="left:30%; animation-delay:2s">❤</div>
<div class="heart" style="left:50%; animation-delay:4s">❤</div>
<div class="heart" style="left:70%; animation-delay:1s">❤</div>
<div class="heart" style="left:85%; animation-delay:3s">❤</div><audio id="music">
  <source src="https://cdn.pixabay.com/audio/2022/03/15/audio_5b8b8a1b3b.mp3" type="audio/mp3">
</audio><div class="card">
  <div class="inner">
    <div class="side front">
        <h1>Happy Birthday Mommy ❤️</h1>
        <!-- Replace the image below with her photo -->
        <img src="https://i.imgur.com/4M34hi2.png" class="photo">
        <div class="cake">🎂</div>
        <p>Hover to open your card</p>
    </div><div class="side back">
  <div>
    <h2>My Special Wish 💕</h2>
    <p>I wish you long life and prosperity with all the good things of life. Love you lots! &lt;3</p>
    <button onclick="startCelebration()">Play Birthday Song 🎵</button>
  </div>
</div>

  </div>
</div><script>
function startCelebration(){
  document.getElementById('music').play();
  startConfetti();
}

// Confetti animation
const canvas = document.getElementById('confetti');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
let pieces = [];
for(let i=0;i<120;i++){
  pieces.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,r:Math.random()*6+4,d:Math.random()*50});
}
function startConfetti(){
  setInterval(draw,20);
}
function draw(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle='rgba(255,255,255,0.9)';
  ctx.beginPath();
  for(let i=0;i<pieces.length;i++){
    let p=pieces[i];
    ctx.moveTo(p.x,p.y);
    ctx.arc(p.x,p.y,p.r,0,Math.PI*2,true);
  }
  ctx.fill();
  update();
}
function update(){
  for(let i=0;i<pieces.length;i++){
    let p=pieces[i];
    p.y+=Math.cos(p.d)+2+p.r/2;
    if(p.y>canvas.height){p.y=0;}
  }
}
</script></body>
</html>
