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
}

.scene{
 display:none;
 min-height:100vh;
 padding:28px 16px;
 max-width:900px;
 margin:auto;
}

.active{display:block;}

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

.chatbox{max-width:520px;margin:auto;text-align:left}
.bubble{padding:12px 16px;border-radius:18px;margin:8px 0;max-width:80%}
.me{background:#ff4da6;margin-left:auto}
.her{background:#2b2b3c}
.typing{opacity:.7;font-style:italic}

img{width:100%;border-radius:12px;margin-top:12px}

.fade{opacity:0;transform:translateY(20px);transition:1s}
.fade.show{opacity:1;transform:none}
</style>
</head>

<body>

<audio id="music"></audio>

<!-- LOCK -->
<div id="lock" class="scene active">
<h1>Private Love Movie 🎬</h1>
<input id="pwInput" type="password" placeholder="Password">
<br>
<button id="unlockBtn">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
<h1>Hi My Favorite Person 💗</h1>
<div class="card">Every click reveals a piece of my heart.</div>

<button onclick="playList('intro')">Play Music 🎵</button>
<button onclick="show('letter')">Love Letter 💌</button>
<button onclick="show('story')">Story Mode 📖</button>
<button onclick="show('chat')">Unsent Chats 💬</button>
<button onclick="show('quiz')">Love Quiz 💞</button>
<button onclick="show('gallery')">Memories 📸</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
<h2>My Letter To You</h2>
<button onclick="playList('letter')">Letter Music</button>
<div id="letterBox" class="letter"></div>
<button onclick="typeLetter()">Reveal Letter</button>
<button onclick="emojiBurst()">Feel This</button>
<button onclick="show('home')">Back</button>
</div>

<!-- STORY -->
<div id="story" class="scene">
<h2>Our Story 🌙</h2>
<div class="card">Chapter 1 — write your beginning</div>
<div class="card">Chapter 2 — when she became special</div>
<div class="card">Chapter 3 — what she means to you</div>
<button onclick="show('quiz')">Continue →</button>
</div>

<!-- CHAT -->
<div id="chat" class="scene">
<h2>Things I Never Sent 💬</h2>
<div id="chatbox" class="chatbox"></div>
<button onclick="startChat()">Play Chat</button>
<button onclick="show('home')">Back</button>
</div>

<!-- QUIZ -->
<div id="quiz" class="scene">
<h2>Deepest Word?</h2>
<input id="deepInput">
<br>
<button onclick="checkDeep()">Unlock Ending</button>
</div>

<!-- GALLERY -->
<div id="gallery" class="scene">
<h2>Our Memories 📸</h2>
<button onclick="playList('memory')">Memory Music</button>
<img src="her.jpg">
<img src="us.jpg">
<img src="ss1.jpg">
<img src="ss2.jpg">
<button onclick="show('home')">Back</button>
</div>

<!-- FINAL -->
<div id="final" class="scene">
<h1>Final Scene 🎬</h1>
<div class="card">
<div class="fade">Out of everyone…</div>
<div class="fade">I still choose you.</div>
<div class="fade">Every day.</div>
<div class="fade">Every version of life.</div>
</div>
<button onclick="playEnding()">Play Ending</button>
<button onclick="emojiBurst()">Forever ❤️</button>
</div>

<script>
/* ---------- PASSWORD ---------- */

const PASS = "lovemovie";

document.getElementById("unlockBtn").addEventListener("click", () => {
  const v = document.getElementById("pwInput").value.trim();
  if(v === PASS){
    show("home");
  } else {
    alert("Wrong password 😳");
  }
});

/* ---------- NAV ---------- */

function show(id){
 document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
}

/* ---------- MUSIC ---------- */

const tracks={
 intro:["intro1.mp3","intro2.mp3"],
 letter:["letter1.mp3"],
 memory:["memory1.mp3"]
};

let playlist=[],ti=0;

function playList(name){
 playlist = tracks[name] || [];
 if(!playlist.length) return;
 ti=0;
 music.src = playlist[0];
 music.play();
}

music.onended = ()=>{
 if(!playlist.length) return;
 ti = (ti+1)%playlist.length;
 music.src = playlist[ti];
 music.play();
};

/* ---------- EMOJI BURST ---------- */

const emojis=["😳","❤️","✨","💞","🥺"];

function emojiBurst(){
 for(let i=0;i<28;i++){
  const e=document.createElement("div");
  e.innerHTML=emojis[Math.floor(Math.random()*emojis.length)];
  e.style.position="fixed";
  e.style.left=Math.random()*100+"vw";
  e.style.top="-20px";
  e.style.fontSize="28px";
  e.style.transition="2s linear";
  document.body.appendChild(e);
  setTimeout(()=>{
    e.style.transform="translateY(110vh) rotate(360deg)";
    e.style.opacity=0;
  },50);
  setTimeout(()=>e.remove(),2000);
 }
}

/* ---------- LETTER ---------- */

const letterText = `
WRITE YOUR FULL DEEP LOVE LETTER HERE.
MULTILINE WORKS.
MAKE IT PERSONAL.
`;

function typeLetter(){
 const box=document.getElementById("letterBox");
 box.innerHTML="";
 let i=0;
 function step(){
  if(i<letterText.length){
    box.innerHTML += letterText[i++];
    setTimeout(step,28);
  }
 }
 step();
}

/* ---------- CHAT ---------- */

function startChat(){
 const msgs=[
  "okay act normal…",
  "don’t fall too fast…",
  "why is she this adorable",
  "yeah… I’m in love."
 ];
 const box=document.getElementById("chatbox");
 box.innerHTML="";
 msgs.forEach((t,i)=>{
  setTimeout(()=>{
    const b=document.createElement("div");
    b.className="bubble me";
    b.innerText=t;
    box.appendChild(b);
  }, i*900);
 });
}

/* ---------- QUIZ ---------- */

function checkDeep(){
 const v=document.getElementById("deepInput").value.toLowerCase();
 if(v.includes("love")){
   show("final");
   emojiBurst();
 } else {
   alert("Hint: it starts with L");
 }
}

/* ---------- ENDING ---------- */

function playEnding(){
 document.querySelectorAll(".fade").forEach((e,i)=>{
  setTimeout(()=>e.classList.add("show"), i*900);
 });
}
</script>

</body>
</html>
