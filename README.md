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

.scene{
  display:none;
  min-height:100vh;
  padding:30px 20px;
  max-width:900px;
  margin:auto;
  animation:fade 1s ease;
}
.active{display:block;}

@keyframes fade{
  from{opacity:0; transform:translateY(20px)}
  to{opacity:1; transform:translateY(0)}
}

button{
  padding:14px 22px;
  border:none;
  border-radius:30px;
  background:#ff4da6;
  color:white;
  font-size:16px;
  margin:10px;
  cursor:pointer;
}

.card{
  background:rgba(255,255,255,.08);
  padding:20px;
  border-radius:18px;
}

.letter{
  background:#f5e6c8;
  color:#3b2a1a;
  font-family:'Great Vibes',cursive;
  font-size:28px;
  line-height:1.7;
  padding:28px;
  border-radius:12px;
  text-align:left;
}

.gallery img{
  width:100%;
  border-radius:12px;
  margin-top:12px;
}

.story{
  margin:40px 0;
  padding:20px;
  border-radius:18px;
  background:rgba(255,255,255,.07);
}

/* chat */

.chatbox{max-width:520px;margin:30px auto;text-align:left;}
.bubble{
  padding:12px 16px;
  border-radius:18px;
  margin:8px 0;
  width:fit-content;
  max-width:80%;
  animation:fade .4s ease;
}
.me{background:#ff4da6;margin-left:auto;}
.her{background:#2b2b3c;}
.typing{opacity:.7;font-style:italic;}

/* cinematic ending */

.cine-title{
  font-size:42px;
  font-weight:600;
  background:linear-gradient(45deg,#ff7ac6,#ffd6f0);
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
  animation:glow 2s ease-in-out infinite alternate;
}
@keyframes glow{
  from{filter:drop-shadow(0 0 4px #ff4da6);}
  to{filter:drop-shadow(0 0 18px #ff4da6);}
}

.fade-line{
  opacity:0;
  transform:translateY(20px);
  transition:all 1s ease;
}
.fade-line.show{
  opacity:1;
  transform:translateY(0);
}

input{
  padding:12px;
  border-radius:12px;
  border:none;
  width:220px;
}
</style>
</head>

<body>

<audio id="music"></audio>

<!-- LOCK -->
<div id="lock" class="scene active">
  <h1>Private Love Movie 🎬</h1>
  <input id="pw" type="password" placeholder="Password">
  <br>
  <button onclick="unlock()">Enter</button>
</div>

<!-- HOME -->
<div id="home" class="scene">
  <h1>Hi My Favorite Person 💗</h1>
  <div class="card">Every click reveals a piece of my heart.</div>

  <button onclick="playList('intro')">Play Music 🎵</button>
  <button onclick="go('letter')">Open Letter 💌</button>
  <button onclick="go('story')">Story Mode 📖</button>
  <button onclick="go('chat')">Unsent Chats 💬</button>
  <button onclick="go('quiz1')">Love Quiz 💞</button>
  <button onclick="go('gallery')">Memories 📸</button>
</div>

<!-- LETTER -->
<div id="letter" class="scene">
  <h2>My Letter To You</h2>
  <button onclick="playList('letter')">Letter Music 🎶</button>
  <div class="letter" id="typeText"></div>
  <button onclick="burst()">Feel This</button>
  <button onclick="go('home')">Back</button>
</div>

<!-- STORY -->
<div id="story" class="scene">
  <h2>Our Story 🌙</h2>
  <div class="story">Chapter 1 — How it started ✨<br>WRITE HERE</div>
  <div class="story">Chapter 2 — When you became special 💗<br>WRITE HERE</div>
  <div class="story">Chapter 3 — What you mean t
