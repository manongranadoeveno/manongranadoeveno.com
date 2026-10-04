<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Your Name – Portfolio</title>
<style>
:root{--bg:#15181a;--ink:#ece8da;--dim:#8d9189;--rec:#e8352e;--frame:#23282b;
 box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
*,*::before,*::after{box-sizing:inherit}
html,body{height:100%;margin:0}
body{background:var(--bg);color:var(--ink);font-family:"Courier New",ui-monospace,monospace;overflow:hidden}
.cam{position:relative;height:100%;display:flex;flex-direction:column;padding:18px 22px 14px}

/* Top bar: REC indicator, timecode, name */
.hud{display:flex;justify-content:space-between;align-items:center;font-size:14px;letter-spacing:.06em}
.rec{display:flex;align-items:center;gap:8px;color:var(--rec);font-weight:700}
.dot{width:12px;height:12px;border-radius:50%;background:var(--rec);animation:blink 1.2s steps(1) infinite}
.paused .dot{animation:none;background:var(--dim)}
.paused .rec{color:var(--dim)}
@keyframes blink{50%{opacity:0}}

/* Viewfinder */
.stage{position:relative;flex:1;min-height:0;margin:14px 0;display:grid;place-items:center}
.corner{position:absolute;width:34px;height:34px;border:2px solid var(--ink);opacity:.8}
.tl{top:0;left:0;border-right:0;border-bottom:0}
.tr{top:0;right:0;border-left:0;border-bottom:0}
.bl{bottom:0;left:0;border-right:0;border-top:0}
.br{bottom:0;right:0;border-left:0;border-top:0}
.cross{position:absolute;width:26px;height:26px;opacity:.5}
.cross::before,.cross::after{content:"";position:absolute;background:var(--ink)}
.cross::before{left:12px;top:0;width:2px;height:26px}
.cross::after{top:12px;left:0;height:2px;width:26px}
.shot{width:min(100%,760px);aspect-ratio:16/9;max-height:100%;position:relative;overflow:hidden;border:1px solid #3a4044}
.shot .art{position:absolute;inset:0;background-size:cover;background-position:center}
.shot.cut .art{animation:cut .45s}
@keyframes cut{
 0%{filter:brightness(2.4) contrast(1.4);transform:scaleY(.96)}
 100%{filter:none;transform:none}
}
/* scanlines */
.shot::after{content:"";position:absolute;inset:0;pointer-events:none;
 background:repeating-linear-gradient(0deg,rgba(0,0,0,.18) 0 1px,transparent 1px 3px)}
.cap{position:absolute;left:0;right:0;bottom:0;padding:16px 18px;background:linear-gradient(transparent,rgba(0,0,0,.75));z-index:2}
.cap h1{margin:0 0 4px;font-size:clamp(20px,4vw,34px);font-weight:700}
.cap p{margin:0;font-size:14px;line-height:1.5;max-width:56ch;color:#d6d2c4}
.meta{font-size:12px;color:var(--dim);margin-top:8px;letter-spacing:.05em}

/* Film strip selector */
.strip{display:flex;align-items:stretch;background:#0d0f10;padding:16px 0;position:relative;overflow-x:auto;scrollbar-width:none}
.strip::-webkit-scrollbar{display:none}
.strip::before,.strip::after{content:"";position:absolute;left:0;right:0;height:8px;
 background:repeating-linear-gradient(90deg,#2b3033 0 10px,transparent 10px 20px)}
.strip::before{top:4px}
.strip::after{bottom:4px}
.frame{flex:0 0 150px;margin:0 6px;border:2px solid transparent;background:var(--frame);color:var(--ink);
 padding:0;cursor:pointer;font:inherit;text-align:left;position:relative}
.frame .art{height:80px;opacity:.55;transition:opacity .2s;background-size:cover;background-position:center}
.frame span{display:block;font-size:11px;padding:5px 6px;color:var(--dim)}
.frame:hover .art{opacity:.85}
.frame[aria-current="true"]{border-color:var(--rec)}
.frame[aria-current="true"] .art{opacity:1}
.frame[aria-current="true"] span{color:var(--ink)}
.frame[aria-current="true"]::before{content:"● REC";position:absolute;top:5px;left:6px;z-index:2;
 font-size:10px;font-weight:700;color:var(--rec)}
.frame:focus-visible,.btn:focus-visible{outline:2px solid var(--ink);outline-offset:3px}

/* Footer + buttons */
.foot{display:flex;justify-content:space-between;gap:12px;align-items:center;font-size:12px;color:var(--dim);margin-top:10px;flex-wrap:wrap}
.btn{font:inherit;color:var(--ink);background:none;border:1px solid #3a4044;padding:6px 12px;cursor:pointer}
.btn:hover{border-color:var(--ink)}

/* About overlay */
.about{display:none;position:absolute;inset:0;z-index:5;background:rgba(21,24,26,.96);padding:36px 24px;overflow:auto}
.about.on{display:block}
.about div{max-width:60ch;margin:0 auto;line-height:1.65}
.about h2{margin-top:0}

@media (prefers-reduced-motion:reduce){.dot,.shot.cut .art{animation:none}}
@media (max-width:560px){.frame{flex-basis:120px}.frame .art{height:62px}.cam{padding:14px}}
</style>
</head>
<body>
<main class="cam" id="cam">

 <div class="hud">
  <div class="rec"><span class="dot"></span><span id="state">REC</span></div>
  <div id="tc" aria-label="Timecode">00:00:00:00</div>
  <div>YOUR NAME ▮▮▮▯</div>
 </div>

 <section class="stage" aria-live="polite">
  <i class="corner tl"></i><i class="corner tr"></i><i class="corner bl"></i><i class="corner br"></i>
  <i class="cross"></i>
  <div class="shot" id="shot">
   <div class="art" id="art"></div>
   <div class="cap">
    <h1 id="title"></h1>
    <p id="desc"></p>
    <div class="meta" id="meta"></div>
   </div>
  </div>
 </section>

 <nav class="strip" id="strip" aria-label="Projects"></nav>

 <div class="foot">
  <span>← → to change reel · P to pause</span>
  <span>
   <button class="btn" id="pause">Pause</button>
   <button class="btn" id="aboutBtn">About</button>
   <a class="btn" style="text-decoration:none" href="mailto:hello@yourname.com">Contact</a>
  </span>
 </div>

 <div class="about" id="about">
  <div>
   <h2>About</h2>
   <p>Write two or three sentences about who you are, what you make, and who you like to work with.</p>
   <button class="btn" id="closeAbout">Close</button>
  </div>
 </div>

</main>

<script>
// ====== EDIT YOUR WORK HERE ======
// art can be a gradient or an image: 'url("images/harbor.jpg")'
const projects = [
 {title:"Harbor Lights", year:2025, role:"Direction, edit",
  desc:"A short documentary about the last night shift at a ferry terminal.",
  art:"linear-gradient(160deg,#27455a,#d7703a 70%,#f3c97a)"},
 {title:"Paper Birds", year:2025, role:"Illustration, animation",
  desc:"Hand-cut paper animation for a children's book trailer.",
  art:"linear-gradient(200deg,#e6d9b8,#c9553d 60%,#5a2a2a)"},
 {title:"Static Bloom", year:2024, role:"Brand identity",
  desc:"Visual identity for a lo-fi music label, built from VHS artifacts.",
  art:"linear-gradient(120deg,#2a1f4d,#7a3fa0 50%,#47c2a9)"},
 {title:"Room 9", year:2024, role:"Photography",
  desc:"A series on hotel rooms between guests, shot on 35mm.",
  art:"linear-gradient(180deg,#6b7d6a,#33423a 60%,#101612)"},
 {title:"Slow Signal", year:2023, role:"Motion design",
  desc:"Title sequence and graphics for a podcast about radio.",
  art:"linear-gradient(140deg,#101820,#2b6c8f 55%,#e8d86a)"}
];
// =================================

const $ = id => document.getElementById(id);
let cur = 0, paused = false, frames = 0;

// Build the film strip
const strip = $("strip");
projects.forEach((p, i) => {
 const b = document.createElement("button");
 b.className = "frame";
 b.innerHTML = '<div class="art" style="background:' + p.art + '"></div>' +
   '<span>REEL ' + String(i + 1).padStart(2, "0") + ' · ' + p.title + '</span>';
 b.onclick = () => select(i);
 strip.appendChild(b);
});

// Select a project (this is the "REC" selector)
function select(i) {
 cur = (i + projects.length) % projects.length;
 const p = projects[cur];
 $("art").style.background = p.art;
 $("title").textContent = p.title;
 $("desc").textContent = p.desc;
 $("meta").textContent = p.year + " · " + p.role;

 [...strip.children].forEach((el, k) => {
  if (k === cur) {
   el.setAttribute("aria-current", "true");
   el.scrollIntoView({inline: "center", block: "nearest", behavior: "smooth"});
  } else el.removeAttribute("aria-current");
 });

 // Replay the "cut" flash
 const s = $("shot");
 s.classList.remove("cut");
 void s.offsetWidth;
 s.classList.add("cut");
 frames = 0; // timecode restarts on each new reel
}
select(0);

// Timecode at 24 fps (HH:MM:SS:FF)
setInterval(() => {
 if (paused) return;
 frames++;
 const f = frames % 24,
       s = Math.floor(frames / 24) % 60,
       m = Math.floor(frames / 1440) % 60,
       h = Math.floor(frames / 86400);
 $("tc").textContent = [h, m, s, f].map(n => String(n).padStart(2, "0")).join(":");
}, 1000 / 24);

// Pause / resume
function togglePause() {
 paused = !paused;
 $("cam").classList.toggle("paused", paused);
 $("state").textContent = paused ? "PAUSE" : "REC";
 $("pause").textContent = paused ? "Resume" : "Pause";
}
$("pause").onclick = togglePause;
$("aboutBtn").onclick = () => $("about").classList.add("on");
$("closeAbout").onclick = () => $("about").classList.remove("on");

// Keyboard controls
addEventListener("keydown", e => {
 if (e.key === "ArrowRight") select(cur + 1);
 else if (e.key === "ArrowLeft") select(cur - 1);
 else if (e.key.toLowerCase() === "p") togglePause();
 else if (e.key === "Escape") $("about").classList.remove("on");
});
</script>
</body>
</html>
