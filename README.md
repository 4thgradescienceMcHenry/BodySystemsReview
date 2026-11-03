<title>Body Systems Quest</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bungee&family=Lexend:wght@400;600;700&display=swap">
<style>
/* Layout: one arcade cabinet column — header, the game screen, touch pad, then teacher notes. Single dark look by design. */
:root{
  --bg:#170a14;          /* deep tissue maroon */
  --panel:#24121f;
  --ink:#fbeef3;
  --muted:#d2b6c4;
  --accent:#ffb43a;      /* fact-block amber */
  --teal:#3ad6c4;        /* hero suit */
  --line:#4a2a3e;
  --display:'Bungee', 'Arial Black', Impact, sans-serif;
  --body:'Lexend', 'Trebuchet MS', system-ui, sans-serif;
  color-scheme:dark;
}
*{box-sizing:border-box}
html,body{background:var(--bg);color:var(--ink)}
body{font-family:var(--body);font-size:16px;line-height:1.55;
  padding-left:max(16px, env(safe-area-inset-left, 0px));
  padding-right:max(16px, env(safe-area-inset-right, 0px));
  padding-block:20px 40px}
.wrap{max-width:980px;margin:0 auto;display:flex;flex-direction:column;gap:18px}
header{display:flex;flex-wrap:wrap;align-items:flex-end;justify-content:space-between;gap:8px 20px}
h1{font-family:var(--display);font-weight:400;font-size:clamp(28px,5vw,46px);line-height:1;margin:0;letter-spacing:.01em;text-wrap:balance}
h1 span{color:var(--accent)}
.tag{font-size:14px;color:var(--muted);margin:0}
.screen{position:relative;width:100%;aspect-ratio:16/9;max-width:100%;border-radius:14px;overflow:hidden;border:3px solid var(--line);background:#000;box-shadow:0 0 0 6px #0c050a}
canvas{display:block;width:100%;height:100%;image-rendering:auto}
.overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;padding:16px;background:rgba(12,4,10,.72)}
.card{max-width:560px;width:100%;max-height:100%;overflow:auto;background:var(--panel);border:3px solid var(--accent);border-radius:14px;padding:clamp(14px,3vw,26px);display:flex;flex-direction:column;gap:12px}
.card .eyebrow{font-size:12px;letter-spacing:.12em;text-transform:uppercase;color:var(--accent);font-weight:700;margin:0}
.card h2{font-family:var(--display);font-weight:400;font-size:clamp(20px,3.4vw,30px);line-height:1.1;margin:0;text-wrap:balance}
.card p{margin:0;font-size:clamp(14px,2.2vw,17px)}
.opts{display:flex;flex-direction:column;gap:8px}
.btn{font:700 16px/1.2 var(--body);color:#1b0a14;background:var(--accent);border:none;border-radius:10px;padding:12px 16px;cursor:pointer;text-align:left;min-height:44px}
.btn.alt{background:#3a2233;color:var(--ink);border:2px solid var(--line)}
.btn.alt:hover:not(:disabled){border-color:var(--accent)}
.btn:disabled{opacity:.45;cursor:default;text-decoration:line-through}
.btn.go{align-self:flex-start;text-align:center;font-family:var(--display);font-weight:400;letter-spacing:.04em}
.btn:focus-visible{outline:3px solid var(--teal);outline-offset:2px}
.feedback{font-weight:600}
.feedback.good{color:#8ff0a4}.feedback.bad{color:#ff9e9e}
.code{display:flex;gap:8px;flex-wrap:wrap}
.code b{font-family:var(--display);font-weight:400;font-size:clamp(26px,6vw,44px);width:1.5em;height:1.6em;display:flex;align-items:center;justify-content:center;background:#0f070c;border:3px solid var(--teal);border-radius:10px;color:var(--teal)}
.pad{display:none;justify-content:space-between;gap:12px;user-select:none;-webkit-user-select:none}
.pad .grp{display:flex;gap:12px}
.pad button{font:400 20px var(--display);color:var(--ink);background:var(--panel);border:3px solid var(--line);border-radius:14px;width:76px;height:64px;touch-action:none}
.pad button.jump{width:120px;background:var(--accent);color:#1b0a14;border-color:var(--accent)}
.pad button.on{filter:brightness(1.3)}
@media (pointer:coarse), (max-width:760px){.pad{display:flex}}
.keys{font-size:14px;color:var(--muted);margin:0}
kbd{font-family:var(--body);font-size:13px;background:var(--panel);border:1px solid var(--line);border-radius:5px;padding:1px 6px;color:var(--ink)}
.notes{border-top:2px solid var(--line);padding-top:16px;display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:16px 28px}
.notes h3{font-family:var(--display);font-weight:400;font-size:18px;margin:0 0 6px;color:var(--accent)}
.notes p,.notes li{font-size:15px;color:var(--muted);margin:0}
.notes ol{margin:0;padding-left:20px;display:flex;flex-direction:column;gap:2px}
.notes div{min-width:0}
@media (prefers-reduced-motion: reduce){*{scroll-behavior:auto}}
</style>

<div class="wrap">
  <header>
    <h1>Body Systems <span>Quest</span></h1>
    <p class="tag">A 6-zone journey for 4th grade science · LSSS 4-LS1-1 and 4-LS1-2</p>
  </header>

  <div class="screen" id="screen">
    <canvas id="game" width="960" height="540" aria-label="Body Systems Quest game screen"></canvas>
    <div class="overlay" id="overlay"></div>
  </div>

  <div class="pad" id="pad" aria-label="Touch controls">
    <div class="grp">
      <button id="bl" aria-label="Move left">&#9664;</button>
      <button id="br" aria-label="Move right">&#9654;</button>
    </div>
    <button id="bj" class="jump" aria-label="Jump">JUMP</button>
  </div>
  <p class="keys">Move with <kbd>&larr;</kbd> <kbd>&rarr;</kbd> or <kbd>A</kbd> <kbd>D</kbd>. Jump with <kbd>Space</kbd>, <kbd>&uarr;</kbd> or <kbd>W</kbd>. Bump the glowing <b>i</b> blocks from below to learn facts. Jump on germs to clear them. Answer the question at each exit gate to earn a letter of the secret code.</p>

  <section class="notes" aria-label="Teacher notes">
    <div>
      <h3>The six zones</h3>
      <ol>
        <li>Digestive system</li>
        <li>Respiratory system</li>
        <li>Circulatory system</li>
        <li>Skeletal system</li>
        <li>Muscular system</li>
        <li>Nervous system and senses</li>
      </ol>
    </div>
    <div>
      <h3>Standards</h3>
      <p><b>4-LS1-1:</b> animals have internal and external structures that support survival, growth, behavior and reproduction. Every zone pairs a body structure with its job.</p>
      <p style="margin-top:8px"><b>4-LS1-2:</b> animals receive information through their senses, process it in the brain and respond. Zone 6 covers this.</p>
    </div>
    <div>
      <h3>Secret code</h3>
      <p>Students earn one letter per zone. The finished code is <b>SYSTEM</b>. Ask students to write it on an exit ticket or tell you when they finish.</p>
    </div>
  </section>
</div>

<script>
(function(){
const SECRET = "SYSTEM";

const ZONES = [
 { name:"Digestive System", place:"Mouth, stomach and small intestine", std:"4-LS1-1",
   sky:["#2b0a18","#6e1f33"], ground:"#b8475d", top:"#f29aac", plat:"#d9667c", deco:"#8c2c44",
   item:"food", itemName:"food bits", germ:"#7fdc8a",
   goal:"Ride the food from the mouth down to the small intestine.",
   facts:[
    "Your teeth are structures that cut, tear and grind food into small pieces.",
    "Your stomach squeezes food and mixes it with acid to break it down.",
    "The small intestine absorbs nutrients from food into your blood."],
   q:{text:"Which structure absorbs nutrients from food into your blood?",
      opts:["The stomach","The small intestine","The esophagus"], a:1,
      hint:"Think about the long, twisty tube after the stomach.",
      why:"The small intestine is lined with tiny folds that pull nutrients into the blood."}},
 { name:"Respiratory System", place:"Windpipe and lungs", std:"4-LS1-1",
   sky:["#0c1a33","#25507a"], ground:"#d9849a", top:"#ffc3d0", plat:"#e89aae", deco:"#3b6c99",
   item:"o2", itemName:"oxygen bubbles", germ:"#c2e36a",
   goal:"Float through the airways and reach the air sacs in the lungs.",
   facts:[
    "Your lungs take in oxygen when you breathe in and let out carbon dioxide when you breathe out.",
    "The diaphragm is a muscle under your lungs. It moves down to pull air in.",
    "Tiny air sacs in your lungs pass oxygen into your blood."],
   q:{text:"Which gas do your lungs bring into your body for your cells to use?",
      opts:["Carbon dioxide","Oxygen","Helium"], a:1,
      hint:"You collected bubbles of it in this zone.",
      why:"Your lungs take in oxygen, and your blood carries it to every cell."}},
 { name:"Circulatory System", place:"Heart and blood vessels", std:"4-LS1-1",
   sky:["#2a0508","#7a1016"], ground:"#9e2730", top:"#ff6f6f", plat:"#c43c45", deco:"#5a0c12",
   item:"rbc", itemName:"red blood cells", germ:"#9be07a",
   goal:"Race through the blood vessels to the heart.",
   facts:[
    "Your heart is a muscle about the size of your fist. It pumps blood all day and night.",
    "Arteries carry blood away from the heart. Veins carry blood back to it.",
    "Red blood cells carry oxygen from your lungs to the rest of your body."],
   q:{text:"What is the main job of the heart?",
      opts:["To pump blood through the body","To digest food","To help you see"], a:0,
      hint:"It beats about 100 times a minute in kids.",
      why:"The heart pumps blood so oxygen and nutrients reach every part of your body."}},
 { name:"Skeletal System", place:"Skull, ribs and spine", std:"4-LS1-1",
   sky:["#14161f","#3c4152"], ground:"#d8cfb8", top:"#fff6de", plat:"#e9e0c8", deco:"#2a2e3b",
   item:"calcium", itemName:"calcium crystals", germ:"#ff8fd2",
   goal:"Climb along the bones from the ribs up to the skull.",
   facts:[
    "An adult skeleton has 206 bones. Bones give your body its shape and support.",
    "Your skull is a hard structure that protects your brain.",
    "Your ribs form a cage that protects your heart and lungs."],
   q:{text:"Which bones protect your heart and lungs?",
      opts:["The skull","The ribs","The finger bones"], a:1,
      hint:"They curve around your chest like a cage.",
      why:"The ribs make a strong cage around the heart and lungs."}},
 { name:"Muscular System", place:"Arm and leg muscles", std:"4-LS1-1",
   sky:["#2b0d0d","#7a2a1e"], ground:"#c0473a", top:"#ff8a6b", plat:"#d9604f", deco:"#5e1c14",
   item:"energy", itemName:"energy sparks", germ:"#a5e8ff",
   goal:"Bounce across the muscles that move your bones.",
   facts:[
    "Muscles move your bones by contracting, which means getting shorter and pulling.",
    "Muscles work in pairs. When your biceps pulls, your triceps relaxes.",
    "Some muscles work without you thinking, like your heart and stomach muscles."],
   q:{text:"How do muscles move your bones?",
      opts:["They push the bones away","They contract and pull on the bones","They turn into bone"], a:1,
      hint:"Muscles can only do one thing: get shorter.",
      why:"Muscles contract and pull. That is why they work in pairs, one for each direction."}},
 { name:"Nervous System", place:"Nerves, senses and brain", std:"4-LS1-2",
   sky:["#120a2e","#3d2a7a"], ground:"#c97bd6", top:"#f3c2ff", plat:"#d995e6", deco:"#2a1c5c",
   item:"signal", itemName:"nerve signals", germ:"#ffd36a",
   goal:"Follow a nerve signal all the way to the brain.",
   facts:[
    "Your eyes, ears, nose, tongue and skin are sense organs. They collect information.",
    "Nerves carry messages from your senses to your brain very fast.",
    "Your brain processes the information and tells your body how to respond."],
   q:{text:"You touch a hot pan and pull your hand away. What carried the message to your brain?",
      opts:["Blood vessels","Bones","Nerves"], a:2,
      hint:"You followed them through this whole zone.",
      why:"Nerves carry signals from your skin to your brain, and the brain sends a message back to your muscles."}}
];

const T=40, VW=960, VH=540, ROWS=13, G=2000, JUMP=760, MAXV=270;
const cvs=document.getElementById('game'), ctx=cvs.getContext('2d');
const ov=document.getElementById('overlay');

let state='title', zi=0, letters=[], score=0, hearts=3, t=0;
let L=null, P=null, cam=0, parts=[];
const keys={left:false,right:false,jump:false};
let jumpHeld=false;

function rng(s){return function(){s|=0;s=s+0x6D2B79F5|0;let x=Math.imul(s^s>>>15,1|s);x=x+Math.imul(x^x>>>7,61|x)^x;return((x^x>>>14)>>>0)/4294967296;}}

function build(z){
  const r=rng(1234+z*97), W=96+z*6;
  const map=[]; for(let y=0;y<ROWS;y++) map.push(new Uint8Array(W));
  for(let x=0;x<W;x++){map[11][x]=1;map[12][x]=1;}
  const fx=[16,Math.floor(W*.45),Math.floor(W*.72)];
  const safe=x=>x<9||x>W-17||fx.some(f=>Math.abs(f-x)<4);
  const gaps=[];
  let x=11;
  while(x<W-18){
    x+=6+Math.floor(r()*7);
    const gw=2+(r()<.2+z*.07?1:0);
    let ok=true; for(let k=-1;k<=gw;k++) if(safe(x+k)) ok=false;
    if(ok){for(let k=0;k<gw;k++){map[11][x+k]=0;map[12][x+k]=0;} gaps.push([x,gw]);}
    x+=gw;
  }
  const items=[];
  gaps.forEach(([gx,gw])=>{
    if(r()<.55){ for(let k=-1;k<=gw;k++) map[8][gx+k]=2; for(let k=0;k<gw;k++) items.push({x:(gx+k)*T+20,y:7*T+20,got:false}); }
    else items.push({x:(gx+gw/2)*T,y:8*T,got:false});
  });
  for(let i=0;i<4+z;i++){
    const px=12+Math.floor(r()*(W-34)), w=3+Math.floor(r()*2), row=r()<.5?7:8;
    let clear=true; for(let k=-1;k<=w;k++){ if(fx.some(f=>Math.abs(f-(px+k))<3)) clear=false; for(let rr=6;rr<=9;rr++) if(map[rr][px+k]) clear=false; }
    if(!clear) continue;
    for(let k=0;k<w;k++){ map[row][px+k]=2; items.push({x:(px+k)*T+20,y:(row-1)*T+20,got:false}); }
  }
  fx.forEach(f=>{map[7][f]=3;});
  for(let gx=6;gx<W-17;gx+=3){ if(map[11][gx]&&r()<.55&&!map[9][gx]&&!map[10][gx]) items.push({x:gx*T+20,y:9*T+20,got:false}); }
  const sx=W-15;
  for(let i=0;i<4;i++) for(let h=0;h<=i;h++) map[10-h][sx+i]=5;
  for(let h=0;h<4;h++) map[10-h][sx+4]=5;
  const enemies=[]; let tries=0;
  while(enemies.length<3+z && tries<200){
    tries++;
    const ex=14+Math.floor(r()*(W-34));
    if(!map[11][ex]||!map[11][ex+1]||!map[11][ex-1]) continue;
    if(map[10][ex]||map[9][ex]) continue;
    if(enemies.some(e=>Math.abs(e.x/T-ex)<6)) continue;
    enemies.push({x:ex*T+5,y:11*T-28,w:30,h:28,vx:-(55+z*9),alive:true,dead:0,ph:r()*6});
  }
  const deco=[]; for(let i=0;i<40;i++) deco.push({x:r()*W*T,y:20+r()*360,r:12+r()*46,d:.2+r()*.5});
  return {W,map,items,enemies,deco,gateX:(W-6)*T,total:items.length,got:0};
}

function solid(c,r){ if(c<0||c>=L.W) return true; if(r<0||r>=ROWS) return false; return L.map[r][c]>0; }

function newPlayer(){ return {x:2*T,y:11*T-38,w:26,h:38,vx:0,vy:0,on:false,coy:0,face:1,inv:0,safe:{x:2*T,y:11*T-38},anim:0}; }

function startZone(){ L=build(zi); P=newPlayer(); cam=0; hearts=3; parts=[]; }

function hitX(e){
  const top=Math.floor(e.y/T), bot=Math.floor((e.y+e.h-1)/T);
  if(e.vx>0){ const c=Math.floor((e.x+e.w)/T); for(let r=top;r<=bot;r++) if(solid(c,r)){ e.x=c*T-e.w-.01; return true; } }
  else if(e.vx<0){ const c=Math.floor(e.x/T); for(let r=top;r<=bot;r++) if(solid(c,r)){ e.x=(c+1)*T+.01; return true; } }
  return false;
}
function hitY(e){
  e.on=false;
  const l=Math.floor(e.x/T), rr=Math.floor((e.x+e.w-1)/T);
  if(e.vy>0){ const r=Math.floor((e.y+e.h)/T); for(let c=l;c<=rr;c++) if(solid(c,r)){ e.y=r*T-e.h; e.vy=0; e.on=true; return null; } }
  else if(e.vy<0){ const r=Math.floor(e.y/T); let hit=null;
    for(let c=l;c<=rr;c++) if(solid(c,r)){ if(!hit||L.map[r]&&L.map[r][c]===3) hit={c,r}; }
    if(hit){ e.y=(hit.r+1)*T; e.vy=0; return hit; } }
  return null;
}

function burst(x,y,col,n){ for(let i=0;i<n;i++) parts.push({x,y,vx:(Math.random()-.5)*300,vy:-Math.random()*320,life:.6+Math.random()*.4,col}); }

function hurt(fell){
  if(!fell && P.inv>0) return;
  hearts--;
  if(hearts<=0){ state='panel'; panel({eyebrow:ZONES[zi].name, title:"Out of hearts!", body:"The germs got you this time. Start the zone again. Your code letters are safe.", go:"Try again", onGo:()=>{startZone(); state='play';}}); return; }
  P.inv=1.6;
  if(fell){ P.x=P.safe.x; P.y=P.safe.y; P.vx=0; P.vy=0; }
  else { P.vy=-380; P.vx=-P.face*200; }
}

function update(dt){
  t+=dt;
  if(state!=='play'){ parts=parts.filter(p=>(p.life-=dt)>0); return; }
  const z=ZONES[zi];
  const acc=P.on?1900:1200;
  if(keys.left&&!keys.right){ P.vx=Math.max(P.vx-acc*dt,-MAXV); P.face=-1; }
  else if(keys.right&&!keys.left){ P.vx=Math.min(P.vx+acc*dt,MAXV); P.face=1; }
  else P.vx*=Math.pow(P.on?.0008:.2,dt);
  if(P.on) P.coy=.1; else P.coy-=dt;
  if(keys.jump&&!jumpHeld&&P.coy>0){ P.vy=-JUMP; P.coy=0; jumpHeld=true; }
  if(!keys.jump){ jumpHeld=false; if(P.vy<-330) P.vy=-330; }
  P.vy=Math.min(P.vy+G*dt,950);
  P.x+=P.vx*dt; if(hitX(P)) P.vx=0;
  P.y+=P.vy*dt;
  const bump=hitY(P);
  if(bump && L.map[bump.r][bump.c]===3){
    L.map[bump.r][bump.c]=4; score+=50;
    burst(bump.c*T+20,bump.r*T,'#ffb43a',14);
    const idx=[...Array(L.W).keys()].filter(c=>L.map[7][c]===4||L.map[7][c]===3).indexOf(bump.c);
    const fact=z.facts[Math.max(0,Math.min(2,idx))];
    keys.jump=false;
    state='panel';
    panel({eyebrow:"Science fact",title:z.name,body:fact,go:"Keep going",onGo:()=>{state='play';}});
  }
  if(P.on){ const c=Math.floor((P.x+P.w/2)/T); if(solid(c-1,11)&&solid(c,11)&&solid(c+1,11)||P.y<10*T-40) P.safe={x:P.x,y:P.y}; }
  if(P.x<0) P.x=0;
  if(P.y>VH+80){ hurt(true); }
  if(P.inv>0) P.inv-=dt;
  P.anim+=Math.abs(P.vx)*dt;

  L.items.forEach(it=>{ if(!it.got && Math.abs(P.x+P.w/2-it.x)<26 && Math.abs(P.y+P.h/2-it.y)<30){ it.got=true; L.got++; score+=10; burst(it.x,it.y,'#ffffff',6);} });

  L.enemies.forEach(e=>{
    if(!e.alive){ e.dead+=dt; return; }
    e.ph+=dt*6;
    e.x+=e.vx*dt;
    if(hitX(e)) e.vx=-e.vx;
    const ahead=e.vx>0?Math.floor((e.x+e.w+2)/T):Math.floor((e.x-2)/T);
    if(!solid(ahead,Math.floor((e.y+e.h+2)/T))) e.vx=-e.vx;
    if(P.x<e.x+e.w&&P.x+P.w>e.x&&P.y<e.y+e.h&&P.y+P.h>e.y){
      if(P.vy>0 && P.y+P.h-e.y<20){ e.alive=false; P.vy=-440; score+=100; burst(e.x+15,e.y+10,z.germ,16); }
      else hurt(false);
    }
  });

  parts=parts.filter(p=>{p.vy+=900*dt;p.x+=p.vx*dt;p.y+=p.vy*dt;return (p.life-=dt)>0;});
  cam+=((P.x-VW*.38)-cam)*Math.min(1,dt*8);
  cam=Math.max(0,Math.min(cam,L.W*T-VW));

  if(P.x>L.gateX+10){ state='quiz'; quiz(); }
}

/* ---------- drawing ---------- */
function rr(x,y,w,h,r){ctx.beginPath();ctx.moveTo(x+r,y);ctx.arcTo(x+w,y,x+w,y+h,r);ctx.arcTo(x+w,y+h,x,y+h,r);ctx.arcTo(x,y+h,x,y,r);ctx.arcTo(x,y,x+w,y,r);ctx.closePath();}

function drawBG(z){
  const g=ctx.createLinearGradient(0,0,0,VH); g.addColorStop(0,z.sky[0]); g.addColorStop(1,z.sky[1]);
  ctx.fillStyle=g; ctx.fillRect(0,0,VW,VH);
  ctx.fillStyle=z.deco;
  L.deco.forEach(d=>{ const x=((d.x-cam*d.d)%(L.W*T)); if(x<-80||x>VW+80) return; ctx.globalAlpha=.35+d.d*.4; ctx.beginPath(); ctx.arc(x,d.y+Math.sin(t+d.x)*6,d.r,0,7); ctx.fill(); });
  ctx.globalAlpha=1;
}

function drawTiles(z){
  const c0=Math.floor(cam/T)-1, c1=c0+Math.ceil(VW/T)+2;
  for(let r=0;r<ROWS;r++) for(let c=c0;c<=c1;c++){
    if(c<0||c>=L.W) continue;
    const v=L.map[r][c]; if(!v) continue;
    const x=c*T-cam, y=r*T;
    if(v===1||v===5){
      ctx.fillStyle=z.ground; ctx.fillRect(x,y,T+.5,T+.5);
      if(r===0||!L.map[r-1][c]){ ctx.fillStyle=z.top; ctx.fillRect(x,y,T+.5,9); for(let k=0;k<3;k++){ctx.beginPath();ctx.arc(x+7+k*13,y+9,6,0,Math.PI);ctx.fill();} }
      ctx.fillStyle='rgba(0,0,0,.12)'; ctx.beginPath(); ctx.arc(x+(c*7%23)+8,y+26,4,0,7); ctx.fill();
    } else if(v===2){
      ctx.fillStyle=z.plat; rr(x+1,y+2,T-2,T-6,10); ctx.fill();
      ctx.fillStyle='rgba(255,255,255,.25)'; rr(x+5,y+5,T-10,7,4); ctx.fill();
    } else if(v===3||v===4){
      const on=v===3, bob=on?Math.sin(t*4+c)*2:0;
      ctx.fillStyle=on?'#ffb43a':'#6b4e5f'; rr(x+2,y+2+bob,T-4,T-4,8); ctx.fill();
      ctx.strokeStyle='#2a1020'; ctx.lineWidth=3; rr(x+2,y+2+bob,T-4,T-4,8); ctx.stroke();
      if(on){ ctx.shadowColor='#ffb43a'; ctx.shadowBlur=16; }
      ctx.fillStyle=on?'#2a1020':'#9a8090'; ctx.font='26px Bungee, Arial Black, sans-serif'; ctx.textAlign='center'; ctx.textBaseline='middle';
      ctx.fillText('i',x+T/2,y+T/2+2+bob); ctx.shadowBlur=0;
    }
  }
}

function drawGate(z){
  const x=L.gateX-cam; if(x<-120||x>VW+120) return;
  const y=11*T;
  ctx.fillStyle='#1b0a14'; rr(x-6,y-150,92,150,40); ctx.fill();
  const g=ctx.createLinearGradient(0,y-140,0,y); g.addColorStop(0,'#3ad6c4'); g.addColorStop(1,'#1a6f66');
  ctx.fillStyle=g; ctx.globalAlpha=.55+Math.sin(t*3)*.2; rr(x+6,y-138,68,138,30); ctx.fill(); ctx.globalAlpha=1;
  ctx.strokeStyle=z.top; ctx.lineWidth=6; rr(x-6,y-150,92,150,40); ctx.stroke();
  ctx.fillStyle='#fbeef3'; ctx.font='16px Bungee, Arial Black, sans-serif'; ctx.textAlign='center'; ctx.textBaseline='alphabetic';
  ctx.fillText('EXIT',x+40,y-160);
}

function drawItem(z,it){
  const x=it.x-cam, y=it.y+Math.sin(t*3+it.x)*4;
  if(x<-30||x>VW+30) return;
  ctx.save(); ctx.translate(x,y);
  switch(z.item){
    case 'food': ctx.fillStyle='#ffa94d'; ctx.beginPath(); ctx.arc(0,0,10,0,7); ctx.fill(); ctx.fillStyle='#ffd8a8'; ctx.beginPath(); ctx.arc(-3,-3,3.5,0,7); ctx.fill(); break;
    case 'o2': ctx.strokeStyle='#bfe9ff'; ctx.lineWidth=2.5; ctx.fillStyle='rgba(160,220,255,.25)'; ctx.beginPath(); ctx.arc(0,0,12,0,7); ctx.fill(); ctx.stroke(); ctx.fillStyle='#e6f7ff'; ctx.font='600 10px Lexend, sans-serif'; ctx.textAlign='center'; ctx.textBaseline='middle'; ctx.fillText('O2',0,1); break;
    case 'rbc': ctx.fillStyle='#ff3b3b'; ctx.beginPath(); ctx.ellipse(0,0,13,10,0,0,7); ctx.fill(); ctx.fillStyle='#b81d24'; ctx.beginPath(); ctx.ellipse(0,0,6,4,0,0,7); ctx.fill(); break;
    case 'calcium': ctx.rotate(t); ctx.fillStyle='#ffffff'; ctx.beginPath(); ctx.moveTo(0,-12); ctx.lineTo(9,0); ctx.lineTo(0,12); ctx.lineTo(-9,0); ctx.closePath(); ctx.fill(); ctx.strokeStyle='#9fd3ff'; ctx.lineWidth=2; ctx.stroke(); break;
    case 'energy': ctx.fillStyle='#ffe14d'; ctx.beginPath(); ctx.moveTo(3,-13); ctx.lineTo(-8,2); ctx.lineTo(-1,2); ctx.lineTo(-4,13); ctx.lineTo(8,-3); ctx.lineTo(1,-3); ctx.closePath(); ctx.fill(); break;
    case 'signal': ctx.rotate(t*1.5); ctx.fillStyle='#ffe9ff'; ctx.shadowColor='#e38cff'; ctx.shadowBlur=12; ctx.beginPath(); for(let k=0;k<10;k++){ const rad=k%2?5:12, a=k*Math.PI/5; ctx.lineTo(Math.cos(a)*rad,Math.sin(a)*rad);} ctx.closePath(); ctx.fill(); ctx.shadowBlur=0; break;
  }
  ctx.restore();
}

function drawGerm(z,e){
  const x=e.x-cam, y=e.y; if(x<-50||x>VW+50) return;
  if(!e.alive){ if(e.dead>.4) return; ctx.globalAlpha=1-e.dead/.4; ctx.fillStyle=z.germ; ctx.beginPath(); ctx.ellipse(x+15,y+24,18,5,0,0,7); ctx.fill(); ctx.globalAlpha=1; return; }
  const cx=x+15, cy=y+15, w=Math.sin(e.ph)*1.5;
  ctx.fillStyle=z.germ;
  for(let k=0;k<8;k++){ const a=k*Math.PI/4+e.ph*.2; ctx.beginPath(); ctx.arc(cx+Math.cos(a)*16,cy+Math.sin(a)*15,3.5,0,7); ctx.fill(); }
  ctx.beginPath(); ctx.ellipse(cx,cy,14+w,13-w,0,0,7); ctx.fill();
  ctx.fillStyle='#ffffff'; ctx.beginPath(); ctx.arc(cx-5,cy-3,4.5,0,7); ctx.arc(cx+5,cy-3,4.5,0,7); ctx.fill();
  ctx.fillStyle='#1b0a14'; const lk=e.vx>0?1.5:-1.5; ctx.beginPath(); ctx.arc(cx-5+lk,cy-2,2.2,0,7); ctx.arc(cx+5+lk,cy-2,2.2,0,7); ctx.fill();
  ctx.strokeStyle='#1b0a14'; ctx.lineWidth=2; ctx.beginPath(); ctx.moveTo(cx-9,cy-9); ctx.lineTo(cx-2,cy-7); ctx.moveTo(cx+9,cy-9); ctx.lineTo(cx+2,cy-7); ctx.stroke();
  ctx.beginPath(); ctx.arc(cx,cy+6,4,Math.PI*1.1,Math.PI*1.9); ctx.stroke();
}

function drawPlayer(){
  if(P.inv>0 && Math.floor(t*14)%2) return;
  const x=P.x-cam, y=P.y, f=P.face, step=P.on?Math.sin(P.anim/9)*5:0;
  ctx.save(); ctx.translate(x+P.w/2,y); ctx.scale(f,1);
  ctx.fillStyle='#145a52';
  ctx.fillRect(-9+step*.6,28,7,10); ctx.fillRect(2-step*.6,28,7,10);
  ctx.fillStyle='#3ad6c4'; rr(-11,14,22,18,7); ctx.fill();
  ctx.fillStyle='#ffb43a'; ctx.fillRect(-11,22,22,3);
  ctx.fillStyle='#2a8f84'; rr(-16,15,6,12,3); ctx.fill();
  ctx.fillStyle='rgba(200,245,255,.35)'; ctx.strokeStyle='#e6fffb'; ctx.lineWidth=2;
  ctx.beginPath(); ctx.arc(1,6,12,0,7); ctx.fill(); ctx.stroke();
  ctx.fillStyle='#8a5a3c'; ctx.beginPath(); ctx.arc(2,7,8,0,7); ctx.fill();
  ctx.fillStyle='#2b1a10'; ctx.beginPath(); ctx.arc(0,2,8,Math.PI,0); ctx.fill();
  ctx.fillStyle='#ffffff'; ctx.beginPath(); ctx.arc(5,7,2.6,0,7); ctx.fill();
  ctx.fillStyle='#4a2c17'; ctx.beginPath(); ctx.arc(5.6,7.3,1.6,0,7); ctx.fill();
  ctx.strokeStyle='#2b1a10'; ctx.lineWidth=1.5; ctx.beginPath(); ctx.arc(4,10,3,.2,Math.PI-.4); ctx.stroke();
  ctx.strokeStyle='#e6fffb'; ctx.lineWidth=2; ctx.beginPath(); ctx.moveTo(-4,-5); ctx.lineTo(-7,-12); ctx.stroke();
  ctx.fillStyle=Math.sin(t*6)>0?'#ffb43a':'#fff3c4'; ctx.beginPath(); ctx.arc(-7,-13,3,0,7); ctx.fill();
  ctx.restore();
}

function drawHUD(z){
  ctx.fillStyle='rgba(12,4,10,.6)'; ctx.fillRect(0,0,VW,46);
  ctx.textBaseline='middle'; ctx.textAlign='left';
  ctx.fillStyle='#ffb43a'; ctx.font='16px Bungee, Arial Black, sans-serif'; ctx.fillText('ZONE '+(zi+1)+'  '+z.name.toUpperCase(),16,24);
  for(let i=0;i<3;i++){ const hx=470+i*28; ctx.fillStyle=i<hearts?'#ff5a6e':'#4a2a3e'; ctx.beginPath(); ctx.moveTo(hx,30); ctx.bezierCurveTo(hx-14,20,hx-8,8,hx,15); ctx.bezierCurveTo(hx+8,8,hx+14,20,hx,30); ctx.fill(); }
  ctx.fillStyle='#fbeef3'; ctx.font='600 15px Lexend, sans-serif';
  ctx.fillText(L.got+'/'+L.total+' '+z.itemName,570,24);
  ctx.textAlign='right'; ctx.fillText('Score '+score,VW-190,24);
  for(let i=0;i<SECRET.length;i++){ const bx=VW-176+i*27; ctx.strokeStyle='#3ad6c4'; ctx.lineWidth=2; rr(bx,10,23,26,5); ctx.stroke();
    ctx.fillStyle='#3ad6c4'; ctx.textAlign='center'; ctx.font='14px Bungee, Arial Black, sans-serif'; ctx.fillText(letters[i]||'',bx+11.5,24); }
}

function draw(){
  const z=ZONES[zi]; if(!L) return;
  drawBG(z); drawTiles(z); drawGate(z);
  L.items.forEach(it=>{ if(!it.got) drawItem(z,it); });
  L.enemies.forEach(e=>drawGerm(z,e));
  if(state!=='win') drawPlayer();
  parts.forEach(p=>{ ctx.globalAlpha=Math.max(0,p.life); ctx.fillStyle=p.col; ctx.fillRect(p.x-cam-3,p.y-3,6,6); }); ctx.globalAlpha=1;
  drawHUD(z);
}

/* ---------- panels ---------- */
let primary=null;
function esc(s){return String(s).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));}
function panel(o){
  ov.hidden=false;
  ov.innerHTML='<div class="card" role="dialog" aria-live="polite">'+(o.eyebrow?'<p class="eyebrow">'+esc(o.eyebrow)+'</p>':'')+'<h2>'+esc(o.title)+'</h2>'+(o.html||('<p>'+esc(o.body)+'</p>'))+'<button class="btn go" id="goBtn">'+esc(o.go)+'</button></div>';
  const b=document.getElementById('goBtn'); primary=()=>{ ov.hidden=true; primary=null; o.onGo(); };
  b.onclick=primary; b.focus({preventScroll:true});
}

function intro(){
  const z=ZONES[zi];
  state='panel'; startZone();
  panel({eyebrow:'Zone '+(zi+1)+' of 6 · '+z.std, title:z.name,
    html:'<p><b>'+esc(z.place)+'.</b> '+esc(z.goal)+'</p><p>Collect '+esc(z.itemName)+', bump the 3 glowing <b>i</b> blocks for facts, and reach the exit gate.</p>',
    go:'Start zone', onGo:()=>{state='play';}});
}

function quiz(){
  const z=ZONES[zi], q=z.q;
  ov.hidden=false; primary=null;
  ov.innerHTML='<div class="card" role="dialog"><p class="eyebrow">Exit gate question · Zone '+(zi+1)+'</p><h2>'+esc(q.text)+'</h2><div class="opts">'+
    q.opts.map((o,i)=>'<button class="btn alt" data-i="'+i+'">'+String.fromCharCode(65+i)+'. '+esc(o)+'</button>').join('')+
    '</div><p class="feedback" id="fb" aria-live="polite"></p></div>';
  const fb=document.getElementById('fb');
  ov.querySelectorAll('[data-i]').forEach(b=>b.onclick=()=>{
    const i=+b.dataset.i;
    if(i===q.a){
      letters[zi]=SECRET[zi]; score+=200;
      const last=zi===ZONES.length-1;
      panel({eyebrow:'Correct!', title:'Code letter: '+SECRET[zi],
        html:'<p>'+esc(q.why)+'</p><div class="code">'+SECRET.split('').map((c,k)=>'<b>'+(letters[k]||'')+'</b>').join('')+'</div>',
        go:last?'See the secret code':'Next zone', onGo:()=>{ if(last) win(); else { zi++; intro(); } }});
    } else { b.disabled=true; fb.className='feedback bad'; fb.textContent='Not quite. Hint: '+q.hint; }
  });
  ov.querySelector('[data-i]').focus({preventScroll:true});
}

function win(){
  state='win';
  panel({eyebrow:'Journey complete · Score '+score, title:'You explored all six body systems!',
    html:'<p>Your body systems work together to keep you alive and growing. Here is your secret code:</p><div class="code">'+SECRET.split('').map(c=>'<b>'+c+'</b>').join('')+'</div><p>Write the code <b>'+SECRET+'</b> on your exit ticket and show your teacher.</p>',
    go:'Play again', onGo:()=>{ zi=0; letters=[]; score=0; intro(); }});
}

function title(){
  state='panel'; zi=0; startZone();
  panel({eyebrow:'4th grade science adventure', title:'Shrink down and explore the human body',
    html:'<p>You are <b>Nova</b>, a tiny explorer. Travel through six body systems, from your stomach all the way to your brain.</p><p>Answer the question at each exit gate to earn one letter. Collect all six letters to unlock the secret code.</p>',
    go:'Start the journey', onGo:()=>intro()});
}

/* ---------- input ---------- */
const KEYMAP={ArrowLeft:'left',a:'left',A:'left',ArrowRight:'right',d:'right',D:'right',ArrowUp:'jump',w:'jump',W:'jump',' ':'jump'};
addEventListener('keydown',e=>{
  if(e.key==='Enter'&&primary&&document.activeElement&&document.activeElement.id!=='goBtn'){ e.preventDefault(); primary(); return; }
  const k=KEYMAP[e.key]; if(!k) return;
  if(state==='play'){ e.preventDefault(); keys[k]=true; }
});
addEventListener('keyup',e=>{ const k=KEYMAP[e.key]; if(k) keys[k]=false; });
addEventListener('blur',()=>{keys.left=keys.right=keys.jump=false;});
function hold(id,k){
  const b=document.getElementById(id);
  const on=e=>{e.preventDefault(); keys[k]=true; b.classList.add('on');};
  const off=e=>{e.preventDefault(); keys[k]=false; b.classList.remove('on');};
  b.addEventListener('pointerdown',on); b.addEventListener('pointerup',off); b.addEventListener('pointercancel',off); b.addEventListener('pointerleave',off);
  b.addEventListener('contextmenu',e=>e.preventDefault());
}
hold('bl','left'); hold('br','right'); hold('bj','jump');

/* ---------- loop ---------- */
let last=performance.now(), accT=0;
function frame(now){
  accT+=Math.min(.1,(now-last)/1000); last=now;
  const step=1/60;
  while(accT>=step){ update(step); accT-=step; }
  draw();
  requestAnimationFrame(frame);
}

function boot(d){
  d=d||{};
  if(Array.isArray(d.letters)&&typeof d.zi==='number'&&d.zi<ZONES.length){
    zi=d.zi; letters=d.letters; score=d.score||0; intro();
  } else title();
  requestAnimationFrame(frame);
}
try{ window.claude?.hot?.snapshot?.(()=>({zi,letters,score})); }catch(e){}
const H=window.claude?.hot;
if(H&&H.ready) H.ready(boot); else boot(H&&H.data?H.data:{});
})();
</script>
