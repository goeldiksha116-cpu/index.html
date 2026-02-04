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

.scene{display:none;min-height:100vh;padding:30px 16px;max-width:900px;margin:auto}
.active{display:block}

button{
 padding:14px 22px;
 border:none;
 border-radius:30px;
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
}

input{
 padding:12px;
 border-radius:12px;
 border:none;
 width:220px;
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

.fade-line{opacity:0;transform:translateY(20px);transition:1s}
.fade-line.show{opacity:1;transform:none}

img{width:100%;border-radius:12px;margin-top:12px}
</style>
</head>

<body>

<audio id="music"></audio>

<!-- LOCK -->
<div id="lock" class="scene active">
<h1>Private Love Movie 🎬</h1>
<input id="pwInput" type="password" placeholder="Password"><br>
<button onclick="unlock()">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
<h1>Hi My Favorite Person 💗</h1>
<div class="card">Every click reveals a piece of my heart.</div>

<button onclick="go('letter')">Letter 💌</button>
<button onclick="go('story')">Story 📖</button>
<button onclick="go('chat')">Chats 💬</button>
<button onclick="go('quiz')">Quiz 💞</button>
<button onclick="go('gallery')">Memories 📸</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
<h2>My Letter</h2>
<div class="letter" id="letterBox"></div>
<button onclick="typeLetter()">Reveal Letter</button>
<button onclick="burst()">Feel This</button>
<button onclick="go('home')">Back</button>
</div>

<!-- STORY -->
<div id="story" class="scene">
<h2>Our Story 🌙</h2>
<div class="card">Chapter 1 — write here</div>
<div class="card">Chapter 2 — write here</div>
<div class="card">Chapter 3 — write here</div>
<button onclick="go('quiz')">Continue</button>
</div>

<!-- CHAT -->
<div id="chat" class="scene">
<h2>Unsent Chats 💬</h2>
<div id="chatbox" class="chatbox"></div>
<button onclick="startChat()">Play Chat</button>
<button onclick="go('home')">Back</button>
</div>

<!-- QUIZ -->
<div id="quiz" class="scene">
<h2>Deepest Word?</h2>
<input id="deepInput">
<button onclick="checkDeep()">Unlock Ending</button>
</div>

<!-- GALLERY -->
<div id="gallery" class="scene">
<h2>Memories 📸</h2>
<img src="her.jpg">
<img src="us.jpg">
<img src="ss1.jpg">
<button onclick="go('home')">Back</button>
</div>

<!-- FINAL -->
<div id="final" class="scene">
<h2>Final Scene 🎬</h2>
<div id="endLines">
<div class="fade-line">Out of everyone…</div>
<div class="fade-line">I choose you.</div>
<div class="fade-line">Every day.</div>
</div>
<button onclick="playEnding()">Play Ending</button>
<button onclick="burst()">Forever</button>
</div>

<script>
const PASS="lovemovie";

/* NAV */
function go(id){
 document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
}

/* ✅ FIXED UNLOCK */
function unlock(){
 const v=document.getElementById("pwInput").value.trim();
 if(v===PASS){
   go("home");
 } else {
   alert("Wrong password 😳");
 }
}

/* EMOJI BURST */
const emojis=["😳","❤️","✨","💞","🥺"];
function burst(){
 for(let i=0;i<25;i++){
  let e=document.createElement("div");
  e.innerHTML=emojis[Math.floor(Math.random()*emojis.length)];
  e.style.position="fixed";
  e.style.left=Math.random()*100+"vw";
  e.style.top="-20px";
  e.style.fontSize="28px";
  e.style.transition="2s linear";
  document.body.appendChild(e);
  setTimeout(()=>{e.style.transform="translateY(110vh)";e.style.opacity=0;},50);
  setTimeout(()=>e.remove(),2000);
 }
}

/* LETTER */
const letterText=`WRITE YOUR LOVE LETTER HERE`;
function typeLetter(){
 let box=document.getElementById("letterBox");
 box.innerHTML="";
 let i=0;
 function step(){
  if(i<letterText.length){
    box.innerHTML+=letterText[i++];
    setTimeout(step,30);
  }
 }
 step();
}

/* CHAT */
function startChat(){
 const flow=["okay act normal…","don’t fall too fast…","why is she this adorable","yeah I’m in love"];
 const box=document.getElementById("chatbox");
 box.innerHTML="";
 flow.forEach((t,i)=>{
  setTimeout(()=>{
    let b=document.createElement("div");
    b.className="bubble me";
    b.innerText=t;
    box.appendChild(b);
  },i*900);
 });
}

/* QUIZ */
function checkDeep(){
 const v=document.getElementById("deepInput").value.toLowerCase();
 if(v.includes("love")){
   go("final");
   burst();
 } else alert("Hint: love");
}

/* ENDING */
function playEnding(){
 document.querySelectorAll(".fade-line").forEach((e,i)=>{
  setTimeout(()=>e.classList.add("show"),i*900);
 });
}
</script>

</body>
</html>
