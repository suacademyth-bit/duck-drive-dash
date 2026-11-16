<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Duck Dive Dash</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Nunito:wght@700;900&family=Kanit:wght@400;600&display=swap');
:root{--bg:#dfe4ff;--panel:#fff6cf;--inner:#fff;--bd:#1b1c34;--acc:#a06a00;--text:#1d2340;--muted:#556;--chip:#e8ebff;--sky:#0b7bc4;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0f1020;--panel:#2b2d5c;--inner:#181938;--bd:#f3d94e;--acc:#f3d94e;--text:#f4f5ff;--muted:#b4b8e0;--chip:#3a3d78;--sky:#38bdf8}}
:root[data-theme="dark"]{--bg:#0f1020;--panel:#2b2d5c;--inner:#181938;--bd:#f3d94e;--acc:#f3d94e;--text:#f4f5ff;--muted:#b4b8e0;--chip:#3a3d78;--sky:#38bdf8}
*{box-sizing:border-box;-webkit-user-select:none;user-select:none}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;background:var(--bg);color:var(--text);font-family:'Nunito','Kanit',sans-serif;font-weight:700;touch-action:manipulation}
.app{max-width:860px;margin:0 auto;padding:12px;min-height:100vh;display:flex;flex-direction:column;align-items:center}
.px{font-family:'Press Start 2P','Kanit',monospace}
header{text-align:center;margin:10px 0}
h1{font-size:1.5rem;margin:0;color:var(--acc);text-shadow:3px 3px 0 var(--bd);line-height:1.3}
@media (prefers-color-scheme:dark){h1{text-shadow:3px 3px 0 #000}}
.sub{font-size:.78rem;color:var(--sky);margin-top:6px}
.screen{display:none;width:100%;flex-direction:column;gap:14px;background:var(--panel);border:4px solid var(--bd);border-radius:12px;box-shadow:6px 6px 0 rgba(0,0,0,.45);padding:16px}
.screen.on{display:flex}
.inner{background:var(--inner);border:2px solid var(--sky);border-radius:10px;padding:12px}
.btn{font-family:'Press Start 2P','Kanit',monospace;font-size:.7rem;line-height:1.4;color:#fff;background:#3b82f6;border:3px solid #1e3a8a;border-radius:8px;padding:14px 16px;cursor:pointer;box-shadow:0 4px 0 #1e3a8a;text-transform:uppercase}
.btn:active{transform:translateY(3px);box-shadow:0 1px 0 #1e3a8a}
.btn:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
.green{background:#22c55e;border-color:#14532d;box-shadow:0 4px 0 #14532d}.green:active{box-shadow:0 1px 0 #14532d}
.purple{background:#a855f7;border-color:#581c87;box-shadow:0 4px 0 #581c87}.purple:active{box-shadow:0 1px 0 #581c87}
.red{background:#e11d48;border-color:#881337;box-shadow:0 4px 0 #881337}.red:active{box-shadow:0 1px 0 #881337}
.sm{padding:9px 11px;font-size:.6rem}
.menu{display:flex;flex-direction:column;gap:14px;width:100%;max-width:360px;margin:0 auto}
.mascot{display:flex;align-items:center;gap:14px;max-width:440px;width:100%;margin:0 auto}
canvas{image-rendering:pixelated;image-rendering:crisp-edges}
#hero{width:96px;height:64px;flex:none}
.top{display:flex;justify-content:space-between;align-items:center;gap:8px;border-bottom:2px solid var(--sky);padding-bottom:10px}
.top h2{margin:0;font-size:.85rem;color:var(--acc);line-height:1.4}
#plist{display:grid;grid-template-columns:1fr;gap:10px;max-height:62vh;overflow-y:auto}
@media (min-width:640px){#plist{grid-template-columns:1fr 1fr}}
.pc{display:flex;justify-content:space-between;align-items:center;gap:8px}
.pc .py{font-family:'Press Start 2P',monospace;font-size:.85rem;color:var(--acc)}
.pc .hz{font-size:1.4rem;margin-left:8px}
.small{font-size:.78rem;color:var(--muted);line-height:1.5}
ul{margin:4px 0 0;padding-left:20px;font-size:.85rem;line-height:1.6}
.hud{display:flex;justify-content:space-between;align-items:center;background:var(--inner);border:2px solid var(--sky);border-radius:10px;padding:8px 10px}
.score{font-family:'Press Start 2P',monospace;font-size:.7rem;color:var(--acc)}
.prompt{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:10px}
.pw{font-family:'Press Start 2P',monospace;font-size:1.6rem;color:var(--acc)}
.hz2{font-size:2rem;margin-left:8px}
.pill{display:inline-flex;align-items:center;gap:8px;background:var(--chip);border:2px solid var(--sky);border-radius:99px;padding:6px 14px;font-size:.8rem}
.dot{width:12px;height:12px;border-radius:50%;background:#f87171}
.dot.on{background:#4ade80;animation:pulse 1.2s infinite}
@keyframes pulse{50%{opacity:.3;transform:scale(1.2)}}
@media (prefers-reduced-motion:reduce){.dot.on{animation:none}}
.fb{font-size:.85rem;min-height:1.4em;text-align:center;margin-top:6px}
.ok{color:#16a34a}.bad{color:#e11d48}
.pool{position:relative;border:4px solid #0b4f8f;border-radius:8px;overflow:hidden;background:#3aa7ff}
.pool canvas{display:block;width:100%;height:auto}
.ov{position:absolute;top:6px;background:rgba(35,38,52,.85);color:#fff;border-radius:6px;padding:6px 8px;font-family:'Press Start 2P',monospace;font-size:.6rem}
#tm{left:8px}#hearts{right:8px;letter-spacing:2px}
.modal{position:fixed;inset:0;background:rgba(0,0,0,.8);z-index:9;display:none;align-items:center;justify-content:center;padding:16px}
.modal.on{display:flex}
.modal .screen{display:flex;max-width:420px;text-align:center}
#log{min-height:60px;text-align:left;font-size:.85rem}
#log div{padding:5px 0;border-bottom:1px solid var(--chip)}
</style>
</head>
<body>
<div class="app">
<header>
  <h1 class="px">DUCK DIVE DASH</h1>
  <div class="sub">SU Academy • Pinyin Racing Adventure</div>
</header>

<div id="s-home" class="screen on" style="align-items:center">
  <div class="inner mascot">
    <canvas id="hero" width="48" height="32" aria-hidden="true"></canvas>
    <div><div class="px" style="font-size:.7rem;color:var(--acc)">Pinyin Duck</div>
    <div class="small">Speak clearly into your mic and race to victory!</div></div>
  </div>
  <div class="menu">
    <button class="btn green" onclick="startGame()">🎮 Start Game</button>
    <button class="btn purple" onclick="showScreen('s-practice')">📚 Practice Mode</button>
    <button class="btn" onclick="showScreen('s-howto')">❓ How to Play</button>
    <button class="btn" style="background:#0ea5e9;border-color:#075985;box-shadow:0 4px 0 #075985" onclick="startMicTest()">🎤 Test Mic</button>
  </div>
</div>

<div id="s-practice" class="screen">
  <div class="top"><h2 class="px">📚 Practice &amp; Phonetics</h2><button class="btn red sm" onclick="showScreen('s-home')">🏠 Home</button></div>
  <p class="small" style="margin:0">Learn how each pinyin sound is built, with audio, English and Thai (ฟังเสียง พร้อมคำแปลไทยและอังกฤษ).</p>
  <div id="plist"></div>
</div>

<div id="s-howto" class="screen">
  <div class="top"><h2 class="px">❓ How to Play / วิธีการเล่น</h2><button class="btn red sm" onclick="showScreen('s-home')">🏠 Home</button></div>
  <div class="inner">
    <b style="color:var(--acc)">🇬🇧 English</b>
    <ul>
      <li>Race your yellow pixel duck against 2 computer ducks in the pool.</li>
      <li>Read the pinyin on screen <b>out loud</b>. If auto-listening doesn't start, tap the <b>"🎤 Tap to turn on mic"</b> button.</li>
      <li>About 20% accuracy or more passes, your duck dashes ahead, and a new random word appears.</li>
      <li>You have 3 hearts and 2 minutes per word. First to the finish line wins!</li>
    </ul>
    <hr style="border:0;border-top:2px solid var(--chip);margin:12px 0">
    <b style="color:var(--acc)">🇹🇭 ภาษาไทย</b>
    <ul>
      <li>แข่งเป็ดน้อยว่ายน้ำพิกเซลอาร์ตกับคอมพิวเตอร์ 2 ตัวในสระ</li>
      <li>พูดออกเสียงพินอินบนจอ หากไมค์ไม่จับเสียงอัตโนมัติ ให้กดปุ่ม <b>"🎤 แตะเพื่อเปิดไมค์"</b> ที่ปรากฏขึ้น</li>
      <li>ออกเสียงถูกประมาณ 20% ขึ้นไป เป็ดจะพุ่งไปข้างหน้า</li>
      <li>มีหัวใจ 3 ดวง และเวลาคำละ 2 นาที ใครถึงเส้นชัยก่อนชนะ</li>
    </ul>
  </div>
  <button class="btn green" onclick="showScreen('s-home')">Got it! / เข้าใจแล้ว</button>
</div>

<div id="s-game" class="screen" style="padding:12px">
  <div class="hud">
    <button class="btn red sm" onclick="exitGame()" aria-label="Home">🏠 Home</button>
    <div class="score">SCORE <span id="score">0</span></div>
  </div>
  <div class="inner prompt">
    <div>
      <div class="small">SAY THIS PINYIN</div>
      <div><span class="pw" id="pw"></span><span class="hz2" id="hz"></span></div>
      <div class="small" id="mean"></div>
    </div>
    <div style="text-align:center">
      <button class="btn sm" style="background:#0ea5e9;border-color:#075985;box-shadow:0 4px 0 #075985" onclick="guide()">🔊 Guide</button>
      <div style="margin-top:8px"><span class="pill"><span class="dot" id="dot"></span><span id="mt">Starting…</span></span></div>
      <button class="btn sm purple" id="micbtn" style="display:inline-block;margin-top:8px" onclick="enableMic()">🎤 Tap to turn on mic</button>
    </div>
  </div>
  <div class="fb" id="fb" aria-live="polite"></div>
  <div class="pool">
    <canvas id="pool" width="128" height="84"></canvas>
    <div class="ov" id="tm">2:00</div>
    <div class="ov" id="hearts" aria-label="Lives">LIFE ♥♥♥</div>
  </div>
</div>

<div id="s-mic" class="screen">
  <div class="top"><h2 class="px">🎤 Mic Test</h2><button class="btn red sm" onclick="showScreen('s-home')">🏠 Home</button></div>
  <p class="small" id="mi" style="margin:0"></p>
  <div class="inner" style="text-align:center">
    <div class="pw" id="mw" style="font-size:1.3rem"></div>
    <div style="margin-top:10px"><button class="btn sm" onclick="mtGuide()">🔊 Guide</button> <button class="btn sm green" onclick="mtListen()">🎤 Listen</button> <button class="btn sm purple" onclick="mtNext()">Next ▶</button></div>
    <div class="fb" id="ms">Tap Listen, then say the word.</div>
  </div>
  <div class="inner" id="log"></div>
</div>

<div id="m-over" class="modal"><div class="screen">
  <h2 class="px" id="ot" style="font-size:1.1rem;color:var(--acc)"></h2>
  <p id="od" style="margin:0;font-size:.9rem"></p>
  <div class="inner small">Final score: <b id="fs">0</b> · Words mastered: <b id="fw">0</b></div>
  <div style="display:flex;gap:10px;justify-content:center;flex-wrap:wrap">
    <button class="btn green sm" onclick="startGame()">Play Again</button>
    <button class="btn sm" onclick="showScreen('s-home')">Home</button>
  </div>
</div></div>
</div>

<script>
const $=id=>document.getElementById(id);
const WORDS=[
 {py:"bēi",hz:"杯",tone:"1st tone: high, flat",bd:"b + ēi = bēi",en:"Cup / Glass",th:"แก้วน้ำ",acc:[["杯","背","悲","碑","北"]],lat:"bei"},
 {py:"jiàn",hz:"见",tone:"4th tone: falling",bd:"j + iàn = jiàn",en:"To see / Meet",th:"พบ / เห็น",acc:[["见","建","件","健","键","剑","间","渐"]],lat:"jian"},
 {py:"yuè",hz:"月",tone:"4th tone: falling",bd:"y + uè = yuè",en:"Moon / Month",th:"พระจันทร์ / เดือน",acc:[["月","越","乐","约","阅","跃","悦"]],lat:"yue"},
 {py:"jī",hz:"鸡",tone:"1st tone: high, flat",bd:"j + ī = jī",en:"Chicken",th:"ไก่",acc:[["鸡","机","击","基","几","吉","积","级","急"]],lat:"ji"},
 {py:"zuó",hz:"昨",tone:"2nd tone: rising",bd:"z + uó = zuó",en:"Yesterday",th:"เมื่อวาน",acc:[["昨","左","作","做","坐"]],lat:"zuo"},
 {py:"zhuōzi",hz:"桌子",tone:"1st tone + light tone",bd:"zh + uō = zhuō , z + i = zi",en:"Table / Desk",th:"โต๊ะ",acc:[["桌","捉","卓","拙"],["子","字","自","紫"]],lat:"zhuozi"},
 {py:"shuō",hz:"说",tone:"1st tone: high, flat",bd:"sh + uō = shuō",en:"To speak / Say",th:"พูด / กล่าว",acc:[["说","朔","硕","烁"]],lat:"shuo"}
];
const PASS=.2,FIN=1,MAXM=3,ROUND=120;
let cur=null,deck=[],pos=[0,0,0],score=0,mastered=0,streak=0,mistakes=0,secs=ROUND,slowUntil=0;
let running=false,locked=true,timer=null,rec=null,ttsBusy=false,micOK=true,raf=null,last=0,pending=null,mi=0,t=0;
const SR=window.SpeechRecognition||window.webkitSpeechRecognition;

function showScreen(id){stopGame();document.querySelectorAll('.screen').forEach(s=>{if(!s.closest('.modal'))s.classList.remove('on')});$('m-over').classList.remove('on');$(id).classList.add('on')}
function stopGame(){running=false;locked=true;clearInterval(timer);clearTimeout(pending);cancelAnimationFrame(raf);stopRec();if('speechSynthesis' in window)speechSynthesis.cancel();ttsBusy=false}
function exitGame(){if(confirm('Back to Home? Race progress will be lost.'))showScreen('s-home')}
function shuffle(a){a=a.slice();for(let i=a.length-1;i>0;i--){const j=Math.random()*(i+1)|0;[a[i],a[j]]=[a[j],a[i]]}return a}
function speak(text,rate,done){
  if(!('speechSynthesis' in window)){done&&done();return}
  speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(text);u.lang='zh-CN';u.rate=rate;
  const v=speechSynthesis.getVoices().find(v=>/^zh/i.test(v.lang));if(v)u.voice=v;
  ttsBusy=true;u.onend=u.onerror=()=>{ttsBusy=false;done&&done()};
  speechSynthesis.speak(u);
}

/* practice list */
$('plist').innerHTML=WORDS.map((w,i)=>`<div class="inner pc"><div><div><span class="py">${w.py}</span><span class="hz">${w.hz}</span></div>
 <div class="small" style="color:var(--sky)">${w.bd}</div><div class="small">EN: ${w.en} | TH: ${w.th}</div></div>
 <button class="btn sm" onclick="speak('${w.hz}',.7)">🔊 Play</button></div>`).join('');

/* game */
function startGame(){
  showScreen('s-game');
  pos=[0,0,0];score=0;mastered=0;streak=0;mistakes=0;deck=[];slowUntil=0;running=true;micOK=true;
  $('score').innerText=0;hearts();
  $('micbtn').style.display='inline-block';
  last=performance.now();raf=requestAnimationFrame(loop);
  nextWord();
}
function nextWord(){
  if(!running)return;
  if(!deck.length)deck=shuffle(WORDS);
  cur=deck.pop();locked=false;secs=ROUND;
  $('pw').innerText=cur.py;$('hz').innerText=cur.hz;
  $('mean').innerText=`${cur.en} (${cur.th}) · ${cur.tone}`;
  feedback('Tap the mic button and speak clearly!','');
  setMic(SR?'paused':'none');
  clock();clearInterval(timer);timer=setInterval(tick,1000);
}
function guide(){if(!cur)return;stopRec();speak(cur.hz,.75,()=>{if(running&&!locked)startRec()})}
function clock(){$('tm').innerText=`${(secs/60)|0}:${String(secs%60).padStart(2,'0')}`}
function tick(){if(!running||locked)return;secs--;clock();if(secs<=0)miss('⏰ Time’s up! Next word.')}
function feedback(m,c){const f=$('fb');f.innerText=m;f.className='fb '+c}
function setMic(k){
  const d=$('dot'),m=$('mt');d.className='dot'+(k==='listen'?' on':'');
  m.innerText=k==='listen'?'Listening… speak now':k==='paused'?'Ready (Tap mic to speak)':k==='blocked'?'Mic is off':'Voice not supported here';
  if(k==='blocked')feedback('Allow microphone access in browser settings, then tap the button.','bad');
  if(k==='none')feedback('This browser does not support voice input. Use Safari (iOS) or Chrome.','bad');
}

/* recognition */
function startRec(){
  if(!SR||!running||locked||ttsBusy||rec||!micOK)return;
  const r=new SR();r.lang='zh-CN';r.interimResults=false;r.maxAlternatives=6;r.continuous=false;
  r.onresult=handleResult;
  r.onstart=()=>{r._s=1;setMic('listen')};
  r.onerror=e=>{if(e.error==='not-allowed'||e.error==='service-not-allowed'){micOK=false;setMic('blocked')}};
  r.onend=()=>{rec=null;if(running&&!locked&&!ttsBusy&&micOK)setMic('paused')};
  rec=r;try{r.start()}catch(e){rec=null;}
}
function stopRec(){if(rec){const r=rec;rec=null;try{r.abort()}catch(e){}}}
function enableMic(){
  micOK=true;ttsBusy=false;
  if('speechSynthesis' in window)speechSynthesis.cancel();
  stopRec();
  if(running&&!locked)startRec();
}
function lev(a,b){const d=Array.from({length:a.length+1},(_,i)=>[i]);for(let j=1;j<=b.length;j++)d[0][j]=j;
  for(let i=1;i<=a.length;i++)for(let j=1;j<=b.length;j++)d[i][j]=Math.min(d[i-1][j]+1,d[i][j-1]+1,d[i-1][j-1]+(a[i-1]===b[j-1]?0:1));return d[a.length][b.length]}
function scoreAlt(text,rank){
  const s=text.toLowerCase();let f=0;
  if(/[a-z]/.test(s)){const n=s.normalize('NFD').replace(/[\u0300-\u036f\s]/g,'');f=1-lev(n,cur.lat)/Math.max(n.length,cur.lat.length)}
  else{let h=0;cur.acc.forEach(set=>{if(set.some(c=>text.includes(c)))h++});f=h/cur.acc.length}
  return f*(1-rank*.08);
}
function handleResult(e){
  if(!running||locked)return;
  const alts=[...e.results[0]];let best=0;alts.forEach((a,i)=>best=Math.max(best,scoreAlt(a.transcript,i)));
  const pct=Math.round(best*100),heard=alts[0]?alts[0].transcript:'';
  if(best>=PASS)success(pct,heard);else miss(`I heard “${heard}” (${pct}%). Try again!`,true);
}
function success(pct,heard){
  locked=true;stopRec();clearInterval(timer);
  streak++;mastered++;score+=100*Math.min(streak,5);$('score').innerText=score;
  pos[0]=Math.min(FIN,pos[0]+.07);
  feedback(`🎉 Great! “${heard}” matched ${pct}%${streak>1?` · streak x${streak}`:''}`,'ok');
  if(pos[0]<FIN)pending=setTimeout(nextWord,1300);
}
function miss(msg,retry){
  streak=0;mistakes++;hearts();slowUntil=performance.now()+4500;feedback('❌ '+msg,'bad');
  if(mistakes>=MAXM){locked=true;stopRec();clearInterval(timer);pending=setTimeout(()=>end(false,'lives'),1100);return}
  if(!retry){locked=true;stopRec();pending=setTimeout(nextWord,1400)}
}
function hearts(){$('hearts').innerText='LIFE '+'♥'.repeat(MAXM-mistakes)+'♡'.repeat(mistakes)}
function end(win,why){
  const place=1+pos.slice(1).filter(p=>p>pos[0]).length;
  stopGame();
  $('ot').innerText=win?'🎉 VICTORY!':(why==='lives'?'💔 GAME OVER':`🏁 ${place===2?'2nd':'3rd'} place`);
  $('od').innerText=win?'You swam past both opponents and finished first!':(why==='lives'?'Out of hearts. Try again!':'A computer duck reached the finish first. Try again!');
  $('fs').innerText=score;$('fw').innerText=mastered;$('m-over').classList.add('on');
}

/* mic test */
function hasZh(){return 'speechSynthesis' in window&&speechSynthesis.getVoices().some(v=>/^zh/i.test(v.lang))}
function startMicTest(){showScreen('s-mic');mi=0;drawMT();$('log').innerHTML='';
  $('mi').innerText=(SR?'Voice input: supported ✅':'Voice input: NOT supported ❌ (use Safari or Chrome)')+'  ·  Chinese voice: '+(hasZh()?'found ✅':'not found ⚠️')}
function drawMT(){cur=WORDS[mi];$('mw').innerText=cur.py+'  '+cur.hz}
function mtNext(){mi=(mi+1)%WORDS.length;drawMT()}
function mtGuide(){speak(WORDS[mi].hz,.75)}
function mtLog(m){const d=document.createElement('div');d.textContent=m;$('log').prepend(d)}
function mtListen(){
  if(!SR){mtLog('Voice input is not supported in this browser.');return}
  if('speechSynthesis' in window)speechSynthesis.cancel();
  const r=new SR();r.lang='zh-CN';r.maxAlternatives=6;r.interimResults=false;
  $('ms').innerText='🎤 Listening… say it now';
  r.onresult=e=>{const alts=[...e.results[0]];let best=0;alts.forEach((a,i)=>best=Math.max(best,scoreAlt(a.transcript,i)));const p=Math.round(best*100);
    mtLog('Heard: '+alts.map(a=>'“'+a.transcript+'”').join(' / ')+' → '+p+'% '+(p>=20?'✅ pass':'❌ below 20%'))};
  r.onerror=e=>mtLog('Error: '+e.error+(e.error==='not-allowed'?' (mic blocked)':e.error==='no-speech'?' (nothing heard, try again)':''));
  r.onend=()=>{$('ms').innerText='Tap Listen, then say the word.'};
  try{r.start()}catch(err){mtLog('Could not start: '+err.message)}
}

/* pixel art */
const PAL={Y:'#ffd93b',D:'#e8a800',O:'#ff7a1a',K:'#16213a',W:'#ffffff'};
const DUCK=[
"..........CCC...",
".........CCCCC..",
".........YYKYYOO",
".........YYYYYOO",
"..........YYYY..",
"....YYYYYYYYY...",
"...YYYYYYYYYYY..",
"..YYWWYYYYYYYYY.",
".YYYWWYYYYYYYDD.",
"YYYYYYYYYYYYDDD.",
".YYYYYYYYYYDDD..",
"..DDDDDDDDDDD..."];
const CAPS=['#ff3b3b','#2f6bff','#27b060'];
function drawDuck(c,x,y,cap,tt){
  DUCK.forEach((row,j)=>{for(let i=0;i<16;i++){const ch=row[i];if(ch==='.')continue;c.fillStyle=ch==='C'?cap:PAL[ch];c.fillRect(x+i,y+j,1,1)}});
  c.fillStyle='#fff';const w=(tt*6|0)%2;c.fillRect(x-3,y+11+w,2,1);c.fillRect(x-6,y+12-w,2,1);
}
function drawPool(c,tt){
  const W=128,H=84;
  c.fillStyle='#3aa7ff';c.fillRect(0,0,W,H);
  c.fillStyle='#d9c9a0';c.fillRect(0,0,W,6);
  for(let x=0;x<W;x+=8){c.fillStyle='#c4b182';c.fillRect(x,5,4,1)}
  c.fillStyle='#16213a';c.fillRect(0,6,W,1);
  c.fillStyle='#5cbcff';
  for(let y=7;y<H;y+=3)for(let x=0;x<W;x++){if(((x*5+y*3+(tt*5|0))%13)===0)c.fillRect(x,y,2,1)}
  for(let i=0;i<=3;i++){const y=7+i*25;for(let x=0;x<W;x+=2){c.fillStyle=(x/2)%2?'#ff5a5f':'#fff';c.fillRect(x,y,2,2)}}
  for(let y=7;y<H;y+=2){c.fillStyle=(y/2|0)%2?'#fff':'#16213a';c.fillRect(112,y,2,2);c.fillStyle=(y/2|0)%2?'#16213a':'#fff';c.fillRect(114,y,2,2)}
  c.fillStyle='#16213a';c.fillRect(0,6,2,H);
  pos.forEach((p,i)=>{const x=4+Math.min(p,FIN)*94,bob=Math.round(Math.sin(tt*5+i*2));drawDuck(c,Math.round(x),9+i*25+bob,CAPS[i],tt)});
  const px=Math.round(4+Math.min(pos[0],FIN)*94),b=(tt*4|0)%2;
  c.fillStyle='#ff3b3b';c.fillRect(px+6,6+b,4,1);c.fillRect(px+7,7+b,2,1);
}
function loop(now){
  const dt=Math.min(.1,(now-last)/1000);last=now;t=now/1000;
  if(running){
    const slow=now<slowUntil;
    const sp=[(.0035+Math.min(streak,5)*.0016)*(slow?.25:1),.0098+Math.sin(now/2300)*.001,.0087+Math.sin(now/1900+2)*.001];
    for(let i=0;i<3;i++)pos[i]=Math.min(FIN,pos[i]+sp[i]*dt);
    if(pos[0]>=FIN||pos[1]>=FIN||pos[2]>=FIN){
      const win=pos[0]>=FIN;running=false;locked=true;clearInterval(timer);clearTimeout(pending);stopRec();
      pending=setTimeout(()=>end(win,'cpu'),700);
    }
  }
  drawPool($('pool').getContext('2d'),t);
  raf=requestAnimationFrame(loop);
}
(function(){const c=$('hero').getContext('2d');c.fillStyle='#3aa7ff';c.fillRect(0,0,48,32);
 c.fillStyle='#5cbcff';for(let x=0;x<48;x+=6)c.fillRect(x,26+(x%12?0:2),3,1);drawDuck(c,16,8,'#ff3b3b',0)})();
if('speechSynthesis' in window)speechSynthesis.getVoices();
</script>
</body>
</html>
  