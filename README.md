<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Terminal Intro</title>
<style>
  /* background */
  body {
    margin: 0;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle at 10% 10%, #0b1020 0%, #020306 60%);
    font-family: ui-monospace, SFMono-Regular, Menlo, "Roboto Mono", "Courier New", monospace;
    color: #cfd8dc;
  }

  /* terminal window */
  .term {
    width: min(900px, 90vw);
    max-width: 900px;
    background: linear-gradient(180deg, rgba(20,25,33,0.95), rgba(10,12,15,0.95));
    border-radius: 8px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
    padding: 18px;
    border: 1px solid rgba(255,255,255,0.03);
  }

  .term .bar {
    height: 12px;
    display:flex;
    gap:8px;
    align-items:center;
    margin-bottom:10px;
  }
  .dot {
    width:12px;height:12px;border-radius:50%;
    box-shadow: inset 0 1px rgba(255,255,255,0.15);
  }
  .dot.red{ background:#ff5f56; }
  .dot.yellow{ background:#ffbd2e; }
  .dot.green{ background:#27c93f; }

  .screen {
    background: linear-gradient(180deg, rgba(0,0,0,0.6), rgba(0,0,0,0.35));
    padding: 18px;
    border-radius: 6px;
    min-height: 140px;
    color: #bfe8ff;
    font-size: 20px;
    line-height: 1.4;
    overflow: hidden;
  }

  .line {
    white-space: pre-wrap;
    font-weight: 500;
  }

  .prompt {
    color: #7ef2b6;
    margin-right: 8px;
    display:inline;
  }

  /* cursor */
  .cursor {
    display:inline-block;
    width:10px;
    height:22px;
    background:#bfe8ff;
    margin-left:3px;
    vertical-align:bottom;
    animation: blink 700ms steps(1) infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }

  /* small fade in for whole terminal */
  .term { opacity:0; transform: translateY(8px) scale(0.998); animation: showTerm 300ms ease-out forwards; }
  @keyframes showTerm { to { opacity:1; transform:none; } }

  /* monospace styling for the typed span */
  .typed { color: #e6f7ff; font-weight:700; }

  /* optional: dim older lines */
  .line.old { color: rgba(190,232,255,0.35); font-weight:500; font-size:18px; }
</style>
</head>
<body>

<div class="term" role="region" aria-label="Terminal">
  <div class="bar">
    <div class="dot red"></div>
    <div class="dot yellow"></div>
    <div class="dot green"></div>
  </div>

  <div class="screen" id="screen" aria-live="polite">
    <div class="line old">Last login: just now</div>
    <div class="line"><span class="prompt">➜</span><span id="typed" class="typed"></span><span class="cursor" id="cursor"></span></div>
  </div>
</div>

<script>
/*
  Simple typing effect.
  - edit `message` to whatever you want.
  - `typeSpeed` controls typing speed (ms per char).
  - `postDelay` is how long before writing next line / finishing (ms).
*/

const message = "HI! I'm devops >_<";
const typeSpeed = 70;      // ms per character (lower -> faster)
const postDelay = 800;     // pause after typing
const screen = document.getElementById('screen');
const typedEl = document.getElementById('typed');
const cursor = document.getElementById('cursor');

function sleep(ms){ return new Promise(resolve=>setTimeout(resolve,ms)); }

async function typeText(text){
  typedEl.textContent = "";
  cursor.style.display = "inline-block";
  for(let i=0;i<text.length;i++){
    typedEl.textContent += text[i];
    // subtle random variation to feel human
    const jitter = Math.random()*0.6 - 0.3;
    await sleep(typeSpeed + typeSpeed*jitter);
  }
  // keep cursor blinking a bit then hide
  await sleep(postDelay);
  cursor.style.display = "none";
}

(async function main(){
  // small initial pause, then type
  await sleep(350);
  await typeText(message);

  // optional: after finishing, append a new line with details
  await sleep(300);
  const details = [
    {prompt: "➜", text: "role: devops engineer"},
    {prompt: "➜", text: "skills: terraform · k8s · ci/cd · monitoring"},
  ];

  // make previous typed line "old"
  const firstLine = typedEl.parentElement;
  firstLine.classList.add('old');

  for(const item of details){
    const line = document.createElement('div');
    line.className = 'line';
    line.innerHTML = `<span class="prompt">${item.prompt}</span><span class="typed">`;
    screen.appendChild(line);
    // scroll into view (in case of overflow)
    screen.scrollTop = screen.scrollHeight;
    // typing simulation for this line
    const typedSpan = document.createElement('span');
    typedSpan.className = 'typed';
    line.appendChild(typedSpan);
    const cur = document.createElement('span');
    cur.className = 'cursor';
    line.appendChild(cur);

    await (async ()=>{
      for(let i=0;i<item.text.length;i++){
        typedSpan.textContent += item.text[i];
        await sleep(typeSpeed * 0.9 + Math.random()*typeSpeed*0.6);
      }
      await sleep(400);
      cur.remove();
    })();
  }
})();
</script>

</body>
</html>

<!---
evokerking1/evokerking1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes. hi
--->
[![GitHub WidgetBox](https://github-widgetbox.vercel.app/api/profile?username=Mytai20100&data=followers,repositories,stars,commits&theme=nautilus)](https://github.com/Jurredr/github-widgetbox)
# Languages
![GitHub WidgetBox](https://github-widgetbox.vercel.app/api/skills?languages=c,js,java,python,lua,go,docker,bash&includeNames=true
)

# Frameworks
[![GitHub WidgetBox](https://github-widgetbox.vercel.app/api/skills?frameworks=react,nodejs&includeNames=true
)](https://github.com/Jurredr/github-widgetbox)

# Github stats
[![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=Mytai20100&theme=ambient_gradient)](https://github.com/anuraghazra/github-readme-stats)
[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Mytai20100&layout=pie)](https://github.com/anuraghazra/github-readme-stats)
[![](https://visitcount.itsvg.in/api?id=Mytai20100&label=Profile%20Views&color=0&icon=3&pretty=false)](https://visitcount.itsvg.in)

