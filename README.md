<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Will you be my Valentine?</title>
<style>
body{
  margin:0;
  height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  background: linear-gradient(135deg, #ffb3c1, #fff0f3);
  font-family:-apple-system,BlinkMacSystemFont,Arial,sans-serif;
  overflow:hidden;
  padding:1rem;
  transition: background 0.8s ease;
}
#box{
  background:#fff;
  padding:2rem 1.5rem;
  border-radius:24px;
  box-shadow:0 12px 30px rgba(255,77,109,.2);
  text-align:center;
  width:100%;
  max-width:360px;
  z-index:2;
  transition: all 0.5s ease;
}
h1{color:#ff4d6d;font-size:1.7rem}
button{
  margin:10px;
  padding:14px 28px;
  font-size:1.1rem;
  border:0;
  border-radius:40px;
  font-weight:bold;
  cursor:pointer;
  transition: transform 0.2s ease;
}
#yes{background:#ff4d6d;color:#fff}
#no{background:#ffb3c1;color:#fff}
.heart{
  position:absolute;
  bottom:-40px;
  animation:up 4s linear forwards;
  pointer-events:none;
}
@keyframes up{
  to{transform:translateY(-110vh);opacity:0}
}
</style>
</head>

<body>
<div id="box">
  <div style="font-size:3rem">🌹</div>
  <h1 id="q">Will you be my Valentine?</h1>
  <button id="yes">YES</button>
  <button id="no">NO</button>
</div>

<!-- Soft click sound -->
<audio id="clickSound" src="https://assets.codepen.io/3/click.mp3"></audio>

<!-- YouTube background audio embed (hidden) -->
<iframe width="0" height="0" src="https://www.youtube.com/embed/9xRH7aOP_yM?autoplay=1&loop=1&playlist=9xRH7aOP_yM" frameborder="0" allow="autoplay" style="display:none;"></iframe>

<script>
const y = document.getElementById("yes"),
      n = document.getElementById("no"),
      b = document.getElementById("box"),
      clickSound = document.getElementById("clickSound");

const msgs = [
  "Baby, did you just press no?🤨",
  "Again? 🥺",
  "Why would you do that..☹️",
  "Anla naman, nag no ulit.. 💔",
  "Aray...",
  "Please say yes... 🤍"
];

let i = 0, s = 1.1;

function heart(){
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤️";
  h.style.left = Math.random()*100+"vw";
  h.style.fontSize = 12+Math.random()*18+"px";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),4000);
}

setInterval(heart,900);

function playSound(){
  clickSound.currentTime = 0;
  clickSound.play();
}

function vibrate(pattern=100){
  if(navigator.vibrate) navigator.vibrate(pattern);
}

// NO button behavior
n.onclick = () => {
  playSound();
  vibrate([50,50,50]);
  n.textContent = msgs[Math.min(i++,msgs.length-1)];
  s += 0.25;
  y.style.fontSize = s+"rem";
};

// YES button behavior
y.onclick = () => {
  playSound();
  vibrate([100,50,100]);
  y.disabled = true;
  n.disabled = true;

  // Show instant "Wow... that's fast!"
  const tempMsg = document.createElement("h1");
  tempMsg.textContent = "Wow... that's fast! Crush mo siguro ako";
  tempMsg.style.color = "#ff4d6d";
  tempMsg.style.fontSize = "1.5rem";
  b.innerHTML = "";
  b.appendChild(tempMsg);

  setTimeout(() => {
    vibrate([200,100,200]);
    b.innerHTML = `
      <div style="font-size:4rem">💖✨</div>
      <h1>YAAYY! I love you, Baby!</h1>
      <p style="color:#ff4d6d">
        It’s a bit late, but I hope you appreciated the site I made for you baby. 💗
      </p>`;
    for(let j=0;j<40;j++) setTimeout(heart,j*40);

    // Change background to pink-bright yellow gradient
    document.body.style.background = "linear-gradient(135deg, #ffb3c1, #ffeab3)";
  }, 1000);
};
</script>
</body>
</html>
