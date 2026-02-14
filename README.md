<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Our Love Movie 🎬</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&family=Great+Vibes&display=swap" rel="stylesheet">

<style>
body{
 margin:0;
 font-family:Poppins;
 color:white;
 text-align:center;
 background:radial-gradient(circle at 30% 20%, #2a1639, #07060d 60%);
 overflow-x:hidden;
}

/* star sky */
body::before{
content:"";
position:fixed;
inset:0;
background:
radial-gradient(2px 2px at 20% 30%, #fff, transparent),
radial-gradient(1px 1px at 70% 60%, #fff, transparent),
radial-gradient(2px 2px at 40% 80%, #fff, transparent),
radial-gradient(1px 1px at 90% 20%, #fff, transparent);
opacity:.35;
animation:starsMove 90s linear infinite;
pointer-events:none;
}
@keyframes starsMove{
from{transform:translateY(0)}
to{transform:translateY(-800px)}
}

.scene{
 display:none;
 min-height:100vh;
 padding:28px 16px;
 max-width:900px;
 margin:auto;
 opacity:0;
 transition:opacity .6s ease;
}
.active{display:block;opacity:1;}

button{
 padding:14px 22px;
 border:none;
 border-radius:28px;
 background:#ff4da6;
 color:white;
 margin:10px;
 font-size:16px;
 cursor:pointer;
}

.card{
 background:rgba(255,255,255,.08);
 padding:20px;
 border-radius:18px;
 margin:14px 0;
}

input{
 padding:12px;
 border-radius:12px;
 border:none;
 width:220px;
 font-size:16px;
}

.letter{
 background:#f5e6c8;
 color:#3b2a1a;
 font-family:'Great Vibes',cursive;
 font-size:26px;
 line-height:1.7;
 padding:26px;
 border-radius:12px;
 text-align:left;
}

img{width:100%;border-radius:12px;margin-top:12px}

/* floating hearts */
#floatHearts{position:fixed;inset:0;pointer-events:none}
.heart{position:absolute;font-size:18px;opacity:.6;animation:floatUp linear forwards}
@keyframes floatUp{
from{transform:translateY(100vh) scale(.6)}
to{transform:translateY(-10vh) scale(1.4);opacity:0}
}
</style>
</head>

<body>

<audio id="music"></audio>
<div id="floatHearts"></div>

<!-- LOCK -->
<div id="lock" class="scene active">
<h1>Private Love Movie 🎬</h1>
<input id="pwInput" type="password">
<br>
<button id="unlockBtn">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
<h1>Hi My Favorite Person 💗</h1>
<div class="card">Every click reveals a piece of my heart.</div>
<button onclick="show('letter')">Love Letter</button>
<button onclick="show('chat')">Unsent Chats</button>
<button onclick="show('quiz')">Love Quiz</button>
<button onclick="show('gallery')">Memories</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
<h2>My Letter</h2>
<div id="letterBox" class="letter"></div>
<button onclick="typeLetter()">Reveal</button>
<button onclick="emojiBurst()">Feel</button>
<button onclick="show('home')">Back</button>
</div>

<!-- CHAT -->
<div id="chat" class="scene">
<h2>Things I Never Sent</h2>
<div id="chatbox"></div>
<button onclick="startChat()">Play</button>
<button onclick="show('home')">Back</button>
</div>

<!-- QUIZ -->
<div id="quiz" class="scene">
<h2>Deepest Word?</h2>
<input id="deepInput">
<br>
<button onclick="checkDeep()">Unlock</button>
</div>

<!-- GALLERY -->
<div id="gallery" class="scene">
<h2>Memories</h2>
<img src="her.jpg">
<img src="us.jpg">
<button onclick="show('home')">Back</button>
</div>

<!-- FINAL -->
<div id="final" class="scene">
<h1>I choose you. Always.</h1>
<button onclick="emojiBurst()">Forever ❤️</button>
</div>

<script>
const PASS="lovemovie";

/* unlock */
document.getElementById("unlockBtn").onclick=()=>{
 if(document.getElementById("pwInput").value.trim()===PASS)
   show("home");
 else alert("Wrong password 😳");
};

/* cinematic navigation */
function show(id){
 const current=document.querySelector(".scene.active");
 if(current){
  current.style.opacity=0;
  setTimeout(()=>{
   current.classList.remove("active");
   const next=document.getElementById(id);
   next.classList.add("active");
   setTimeout(()=>next.style.opacity=1,40);
  },300);
 }else document.getElementById(id).classList.add("active");
}

/* floating hearts */
setInterval(()=>{
 const h=document.createElement("div");
 h.className="heart";
 h.innerHTML=["💗","💞","💕","💖","❤️"][Math.floor(Math.random()*5)];
 h.style.left=Math.random()*100+"vw";
 h.style.animationDuration=4+Math.random()*5+"s";
 document.getElementById("floatHearts").appendChild(h);
 setTimeout(()=>h.remove(),9000);
},700);

/* sparkles */
document.addEventListener("mousemove",e=>{
 const s=document.createElement("div");
 s.innerHTML="✨";
 s.style.position="fixed";
 s.style.left=e.clientX+"px";
 s.style.top=e.clientY+"px";
 s.style.pointerEvents="none";
 s.style.transition="1s";
 document.body.appendChild(s);
 setTimeout(()=>{s.style.transform="translateY(-20px)";s.style.opacity=0},20);
 setTimeout(()=>s.remove(),1000);
});

/* emoji burst */
function emojiBurst(){
 for(let i=0;i<28;i++){
  const e=document.createElement("div");
  e.innerHTML=["😳","❤️","✨","💞"][Math.floor(Math.random()*4)];
  e.style.position="fixed";
  e.style.left=Math.random()*100+"vw";
  e.style.top="-20px";
  e.style.fontSize="28px";
  e.style.transition="2s linear";
  document.body.appendChild(e);
  setTimeout(()=>{e.style.transform="translateY(110vh) rotate(360deg)";e.style.opacity=0},50);
  setTimeout(()=>e.remove(),2000);
 }
}

/* letter typing */
const text=`Write your real love message here`;
function typeLetter(){
 let i=0,box=document.getElementById("letterBox");
 box.innerHTML="";
 (function t(){if(i<text.length){box.innerHTML+=text[i++];setTimeout(t,25)}})();
}

/* chat */
function startChat(){
 const msgs=["act normal","she's adorable","yeah I'm in love"];
 const box=document.getElementById("chatbox");
 box.innerHTML="";
 msgs.forEach((m,i)=>setTimeout(()=>{
  const b=document.createElement("div");
  b.className="card";
  b.innerText=m;
  box.appendChild(b);
 },i*900));
}

/* quiz */
function checkDeep(){
 if(document.getElementById("deepInput").value.toLowerCase().includes("love")){
   show("final"); emojiBurst();
 }else alert("hint: starts with L");
}
</script>

</body>
</html>
