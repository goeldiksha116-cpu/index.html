<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Our Love Movie 🎬</title>

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
body{
 margin:0;
 font-family:Poppins;
 color:white;
 text-align:center;
 background:radial-gradient(circle at 30% 20%, #2a1639, #07060d 60%);
}

.scene{display:none;min-height:100vh;padding:30px 16px;max-width:900px;margin:auto}
.active{display:block;animation:fade 0.8s}

@keyframes fade{from{opacity:0;transform:translateY(20px)}}

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

/* chat */
.chatbox{max-width:520px;margin:auto;text-align:left}
.bubble{padding:12px 16px;border-radius:18px;margin:8px 0;max-width:80%}
.me{background:#ff4da6;margin-left:auto}
.her{background:#2b2b3c}
.typing{opacity:.7;font-style:italic}

/* ending */
.cine{
 font-size:38px;
 background:linear-gradient(45deg,#ff7ac6,#ffd6f0);
 -webkit-background-clip:text;
 -webkit-text-fill-color:transparent;
}

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
<input id="pw" type="password" placeholder="Password"><br>
<button onclick="unlock()">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
<h1>Hi My Favorite Person 💗</h1>
<div class="card">Every click reveals a piece of my heart.</div>

<button onclick="playList('intro')">Music 🎵</button>
<button onclick="go('letter')">Letter 💌</button>
<button onclick="go('story')">Story 📖</button>
<button onclick="go('chat')">Chats 💬</button>
<button onclick="go('quiz1')">Quiz 💞</button>
<button onclick="go('gallery')">Memories 📸</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
<h2>My Letter</h2>
<button onclick="playList('letter')">Letter Music</button>
<div class="letter" id="letterBox"></div>
<button onclick="burst()">Feel This</button>
<button onclick="go('home')">Back</button>
</div>

<!-- STORY -->
<div id="story" class="scene">
<h2>Our Story 🌙</h2>
<div class="card">Chapter 1 — WRITE HERE</div>
<div class="card">Chapter 2 — WRITE HERE</div>
<div class="card">Chapter 3 — WRITE HERE</div>
<button onclick="go('clue')">Continue →</button>
</div>

<!-- CHAT -->
<div id="chat" class="scene">
<h2>Unsent Chats 💬</h2>
<div class="chatbox" id="chatbox"></div>
<button onclick="startChat()">Play Chat</button>
<button onclick="go('quiz1')">Continue →</button>
</div>

<!-- QUIZ -->
<div id="quiz1" class="scene">
<h2>Love Quiz</h2>
<p>Who owns my smile?</p>
<button onclick="go('quiz2')">You</button>
<button onclick="go('quiz2')">Still You</button>
</div>

<div id="quiz2" class="scene">
<p>Type what I feel:</p>
<input id="loveAns">
<button onclick="checkLove()">Submit</button>
</div>

<!-- CLUE -->
<div id="clue" class="scene">
<p>Type the deepest word:</p>
<input id="deep">
<button onclick="unlockFinal()">Unlock</button>
</div>

<!-- GALLERY -->
<div id="gallery" class="scene">
<h2>Memories 📸</h2>
<button onclick="playList('memory')">Memory Music</button>
<img src="her.jpg">
<img src="us.jpg">
<img src="ss1.jpg">
<img src="ss2.jpg">
<button onclick="go('home')">Back</button>
</div>

<!-- FINAL -->
<div id="final" class="scene">
<div class="cine">Final Scene 🎬</div>
<div class="card" id="endLines">
<div class="fade-line">Out of everyone…</div>
<div class="fade-line">I still choose you.</div>
<div class="fade-line">Every timeline.</div>
<div class="fade-line">Every day.</div>
</div>
<button onclick="playEnding()">Play Ending</button>
<button onclick="burst()">Forever</button>
</div>

<script>
/* PASSWORD */
const PASS="lovemovie";

/* NAV */
function go(id){
 document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
}

function unlock(){
 if(pw.value===PASS) go("home");
 else alert("Wrong password 😳");
}

/* MUSIC */
const tracks={
 intro:["intro1.mp3"],
 letter:["letter1.mp3"],
 memory:["memory1.mp3"]
};

let list=[],i=0;
function playList(name){
 list=tracks[name]||[];
 if(!list.length) return;
 i=0; music.src=list[0]; music.play();
}

/* EMOJI BURST */
const emojis=["😳","❤️","✨","💞","🥺"];
function burst(){
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

/* LETTER TYPEWRITER */
const msg=`WRITE YOUR DEEP LOVE LETTER HERE`;
let done=false;
letter.onclick=()=>{
 if(done) return; done=true;
 let t=0;
 function step(){
  if(t<msg.length){
   letterBox.innerHTML+=msg[t++];
   setTimeout(step,30);
  }
 }
 step();
};

/* CHAT */
const chat=[
 {t:"me",x:"okay act normal…"},
 {t:"me",x:"don’t fall too fast…"},
 {t:"typing"},
 {t:"her",x:"why are you smiling?"},
 {t:"me",x:"because it’s you."}
];

function startChat(){
 chatbox.innerHTML="";
 let k=0;
 function step(){
  if(k>=chat.length) return;
  let m=chat[k++];
  if(m.t==="typing"){
    let d=document.createElement("div");
    d.className="bubble her typing";
    d.innerText="typing…";
    chatbox.appendChild(d);
    setTimeout(()=>{d.remove();step();},1200);
    return;
  }
  let b=document.createElement("div");
  b.className="bubble "+m.t;
  b.innerText=m.x;
  chatbox.appendChild(b);
  setTimeout(step,900);
 }
 step();
}

/* QUIZ */
function checkLove(){
 if(loveAns.value.toLowerCase().includes("love")){
  burst(); go("story");
 } else alert("Hint: starts with L");
}

function unlockFinal(){
 if(deep.value.toLowerCase().includes("love")){
  go("final"); burst();
 }
}

/* ENDING */
function playEnding(){
 document.querySelectorAll(".fade-line").forEach((e,i)=>{
  setTimeout(()=>e.classList.add("show"), i*900);
 });
}
</script>

</body>
</html>
