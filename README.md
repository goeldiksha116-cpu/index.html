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
 background:#07060d;
 overflow-x:hidden;
}

/* stars */
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
@keyframes starsMove{from{transform:translateY(0)}to{transform:translateY(-800px)}}

/* aurora */
body::after{
content:"";
position:fixed;
inset:-50%;
background:
radial-gradient(circle at 20% 40%, rgba(255,0,120,.25), transparent 60%),
radial-gradient(circle at 80% 30%, rgba(120,0,255,.25), transparent 60%),
radial-gradient(circle at 50% 80%, rgba(0,200,255,.20), transparent 60%);
filter:blur(80px);
animation:auroraMove 18s ease-in-out infinite alternate;
pointer-events:none;
z-index:-1;
}
@keyframes auroraMove{
0%{transform:translate(-10%,-5%) scale(1)}
50%{transform:translate(5%,10%) scale(1.2)}
100%{transform:translate(-5%,15%) scale(1)}
}

.scene{display:none;min-height:100vh;padding:28px 16px;max-width:900px;margin:auto;opacity:0;transition:.6s}
.active{display:block;opacity:1;}

button{padding:14px 22px;border:none;border-radius:28px;background:#ff4da6;color:white;margin:10px;font-size:16px;cursor:pointer}
.card{background:rgba(255,255,255,.08);padding:20px;border-radius:18px;margin:14px 0}
input{padding:12px;border-radius:12px;border:none;width:220px;font-size:16px}

.letter{background:#f5e6c8;color:#3b2a1a;font-family:'Great Vibes',cursive;font-size:26px;line-height:1.7;padding:26px;border-radius:12px;text-align:left}

#floatHearts{position:fixed;inset:0;pointer-events:none}
.heart{position:absolute;font-size:18px;opacity:.6;animation:floatUp linear forwards}
@keyframes floatUp{from{transform:translateY(100vh)}to{transform:translateY(-10vh);opacity:0}}

.chatbox{max-width:420px;margin:auto;text-align:left}
.msg{padding:12px 16px;border-radius:18px;margin:8px 0;max-width:80%}
.you{background:#ff4da6;margin-left:auto}

.fadeLine{opacity:0;transition:2s;margin:12px}
.fadeLine.show{opacity:1}
</style>
</head>

<body>

<audio id="music" preload="auto"></audio>
<div id="floatHearts"></div>

<div id="lock" class="scene active">
<h1>Private Love Movie 🎬</h1>
<input id="pwInput" type="password"><br>
<button onclick="unlock()">Enter</button>
</div>

<div id="home" class="scene">
<h1>Hi My Favorite Person 💗</h1>
<div class="card">Every click reveals a piece of my heart.</div>
<button onclick="show('letter')">Love Letter</button>
<button onclick="show('quiz')">Love Quiz</button>
<button onclick="startHunt()">Find My Hidden Thoughts</button>
</div>

<div id="letter" class="scene">
<h2>My Letter</h2>
<div id="letterBox" class="letter"></div>
<button onclick="typeLetter()">Reveal</button>
<button onclick="emojiBurst()">Feel</button>
<button onclick="show('home')">Back</button>
</div>

<div id="quiz" class="scene">
<h2>Deepest Word?</h2>
<input id="deepInput"><br>
<button onclick="checkDeep()">Unlock</button>
</div>

<div id="hunt" class="scene">
<h2>Some feelings are hidden… find them 🥺</h2>
<div id="huntArea" style="height:70vh;position:relative;"></div>
<div id="huntText" class="card"></div>
</div>

<div id="herchat" class="scene">
<h2>Your Phone 📱</h2>
<div id="herBox" class="chatbox"></div>
<button onclick="playHerChat()">Open Messages</button>
</div>

<div id="cinematic" class="scene">
<div style="margin-top:40vh;font-size:28px;line-height:1.8">
<div class="fadeLine">in every version of my life</div>
<div class="fadeLine">in every timeline</div>
<div class="fadeLine">in every possible world</div>
<div class="fadeLine">I still find you</div>
<div class="fadeLine">and I still choose you</div>
</div><br>
<button onclick="emojiBurst()">❤️</button>
</div>

<script>
const PASS="lovemovie";
const music=document.getElementById("music");

/* music per scene */
const tracks={
home:"home.mp3",
letter:"letter.mp3",
hunt:"mystery.mp3",
herchat:"chat.mp3",
cinematic:"ending.mp3"
};

function playMusic(scene){
 if(tracks[scene]){
  music.src=tracks[scene];
  music.volume=.7;
  music.play().catch(()=>{});
 }
}

function unlock(){
 if(document.getElementById("pwInput").value.trim()===PASS) show("home");
 else alert("Wrong password 😳");
}

function show(id){
 document.querySelectorAll(".scene").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
 playMusic(id);
}

/* hearts */
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

/* emoji */
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
  setTimeout(()=>{e.style.transform="translateY(110vh)";e.style.opacity=0},50);
  setTimeout(()=>e.remove(),2000);
 }
}

/* letter */
const text=`Write your real love message here`;
function typeLetter(){
 let i=0,box=document.getElementById("letterBox");
 box.innerHTML="";
 (function t(){if(i<text.length){box.innerHTML+=text[i++];setTimeout(t,25)}})();
}

/* quiz */
function checkDeep(){
 if(document.getElementById("deepInput").value.toLowerCase().includes("love")) startHunt();
 else alert("hint: starts with L");
}

/* hunt */
const memories=[
"this is when I realized I wait for you",
"you became part of my routine",
"I smile at my phone because of you",
"I was scared to admit it",
"I think I fell in love here"
];
function startHunt(){
 show("hunt");
 const area=document.getElementById("huntArea");
 area.innerHTML="";
 memories.forEach(m=>{
  const dot=document.createElement("div");
  dot.style.position="absolute";
  dot.style.left=Math.random()*90+"%";
  dot.style.top=Math.random()*80+"%";
  dot.style.width="26px";
  dot.style.height="26px";
  dot.style.borderRadius="50%";
  dot.style.background="rgba(255,255,255,.08)";
  dot.onclick=()=>{
    document.getElementById("huntText").innerText=m;
    dot.remove();
    if(area.children.length===0)setTimeout(()=>show("herchat"),1200);
  };
  area.appendChild(dot);
 });
}

/* chat */
function playHerChat(){
 const texts=["hey","I wanted to tell you something","you matter to me more than I planned","and honestly...","I think I love you"];
 const box=document.getElementById("herBox");
 box.innerHTML="";
 texts.forEach((t,i)=>{
  setTimeout(()=>{
   const b=document.createElement("div");
   b.className="msg you";
   b.innerText=t;
   box.appendChild(b);
   if(i===texts.length-1)setTimeout(()=>show("cinematic"),1500);
  },i*1200);
 });
}

/* cinematic text */
const observer=new MutationObserver(()=>{
 if(document.getElementById("cinematic").classList.contains("active")){
   document.querySelectorAll(".fadeLine").forEach((l,i)=>setTimeout(()=>l.classList.add("show"),i*1800));
 }
});
observer.observe(document.body,{attributes:true,subtree:true});
</script>

</body>
</html>
