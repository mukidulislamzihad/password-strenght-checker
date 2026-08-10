<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Password Vault Analyzer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0a0f1a;
    --bg-grid: rgba(200,155,60,0.055);
    --panel:#111a2c;
    --panel-alt:#16213a;
    --edge: rgba(200,155,60,0.22);
    --brass:#c99a45;
    --brass-bright:#e6bb63;
    --teal:#4fb0a0;
    --red:#e0574f;
    --amber:#e0a458;
    --text:#e9e6dc;
    --text-dim:#8b93a7;
    --text-faint:#5b647a;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      linear-gradient(var(--bg-grid) 1px, transparent 1px) 0 0/42px 42px,
      linear-gradient(90deg, var(--bg-grid) 1px, transparent 1px) 0 0/42px 42px,
      var(--bg);
    color:var(--text);
    font-family:'IBM Plex Mono',monospace;
    min-height:100vh;
    padding:36px 18px 60px;
  }
  .wrap{max-width:880px;margin:0 auto;}

  /* header */
  .header{
    display:flex; justify-content:space-between; align-items:flex-end;
    border-bottom:1px solid var(--edge);
    padding-bottom:16px; margin-bottom:26px;
    flex-wrap:wrap; gap:10px;
  }
  .brand{display:flex; align-items:center; gap:12px;}
  .brand-mark{
    width:34px;height:34px; border:1.5px solid var(--brass);
    border-radius:50%; position:relative; flex-shrink:0;
  }
  .brand-mark::before{
    content:"";position:absolute; inset:7px; border:1.5px solid var(--brass);
    border-radius:50%;
  }
  .brand-mark::after{
    content:"";position:absolute; top:50%; left:50%; width:2px; height:9px;
    background:var(--brass-bright); transform:translate(-50%,-100%) rotate(35deg);
    transform-origin:bottom center;
  }
  h1{
    font-family:'Space Grotesk',sans-serif; font-size:19px; font-weight:600;
    letter-spacing:0.02em; margin:0; color:var(--text);
  }
  .subtitle{font-size:11.5px; color:var(--text-dim); font-family:'IBM Plex Mono',monospace; letter-spacing:0.03em; margin-top:2px;}
  .case-id{font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--text-faint); text-align:right; line-height:1.6;}
  .case-id span{color:var(--brass);}

  /* input panel */
  .vault-input{
    background:var(--panel); border:1px solid var(--edge); border-radius:6px;
    padding:22px; margin-bottom:22px; position:relative;
  }
  .corner{position:absolute; width:12px; height:12px; border:1.5px solid var(--brass); opacity:0.6;}
  .corner.tl{top:-1px;left:-1px;border-right:none;border-bottom:none;}
  .corner.tr{top:-1px;right:-1px;border-left:none;border-bottom:none;}
  .corner.bl{bottom:-1px;left:-1px;border-right:none;border-top:none;}
  .corner.br{bottom:-1px;right:-1px;border-left:none;border-top:none;}

  .label-row{
    display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;
  }
  .field-label{
    font-size:11px; text-transform:uppercase; letter-spacing:0.12em; color:var(--brass);
    font-family:'IBM Plex Mono',monospace;
  }
  .gen-btn{
    background:transparent; border:1px solid var(--edge); color:var(--text-dim);
    font-family:'IBM Plex Mono',monospace; font-size:11px; padding:6px 10px;
    border-radius:4px; cursor:pointer; transition:all .15s ease; letter-spacing:0.02em;
  }
  .gen-btn:hover{border-color:var(--brass); color:var(--brass-bright);}

  .input-row{display:flex; gap:8px;}
  #pwd{
    flex:1; background:var(--panel-alt); border:1px solid var(--edge); color:var(--text);
    font-family:'IBM Plex Mono',monospace; font-size:16px; padding:13px 14px;
    border-radius:4px; letter-spacing:0.03em; outline:none; transition:border-color .15s ease;
  }
  #pwd:focus{border-color:var(--brass);}
  .icon-btn{
    background:var(--panel-alt); border:1px solid var(--edge); color:var(--text-dim);
    width:44px; border-radius:4px; cursor:pointer; font-size:15px;
    transition:all .15s ease;
  }
  .icon-btn:hover{color:var(--brass-bright); border-color:var(--brass);}

  .hint{font-size:11px; color:var(--text-faint); margin-top:9px; font-family:'IBM Plex Mono',monospace;}

  /* gauge + verdict */
  .gauge-section{
    display:grid; grid-template-columns:200px 1fr; gap:24px;
    background:var(--panel); border:1px solid var(--edge); border-radius:6px;
    padding:24px; margin-bottom:18px; align-items:center;
  }
  .gauge-wrap{display:flex; flex-direction:column; align-items:center;}
  .score-num{
    font-family:'Space Grotesk',sans-serif; font-size:13px; color:var(--text-dim);
    margin-top:2px; letter-spacing:0.05em;
  }
  .score-num b{color:var(--brass-bright); font-size:16px;}

  .verdict-label{
    font-family:'Space Grotesk',sans-serif; font-weight:700; font-size:26px;
    letter-spacing:0.01em; margin-bottom:6px;
  }
  .verdict-sub{font-size:13px; color:var(--text-dim); margin-bottom:14px; line-height:1.6;}
  .entropy-bar-track{
    height:6px; background:var(--panel-alt); border-radius:3px; overflow:hidden; margin-bottom:6px;
    border:1px solid var(--edge);
  }
  .entropy-bar-fill{height:100%; width:0%; border-radius:3px; transition:width .4s ease, background .4s ease;}
  .entropy-caption{font-size:10.5px; color:var(--text-faint); font-family:'IBM Plex Mono',monospace; display:flex; justify-content:space-between;}

  /* stat grid */
  .grid-3{display:grid; grid-template-columns:repeat(3,1fr); gap:12px; margin-bottom:18px;}
  @media (max-width:640px){.grid-3{grid-template-columns:1fr;} .gauge-section{grid-template-columns:1fr; justify-items:center; text-align:center;}}
  .stat-card{
    background:var(--panel); border:1px solid var(--edge); border-radius:6px; padding:15px 16px;
  }
  .stat-title{
    font-size:10px; text-transform:uppercase; letter-spacing:0.1em; color:var(--brass);
    font-family:'IBM Plex Mono',monospace; margin-bottom:10px; display:flex; align-items:center; gap:6px;
  }
  .stat-title::before{content:"";width:5px;height:5px;background:var(--brass);border-radius:1px;transform:rotate(45deg);}
  .crack-row{
    display:flex; justify-content:space-between; font-family:'IBM Plex Mono',monospace;
    font-size:12px; padding:6px 0; border-bottom:1px dashed rgba(200,155,60,0.14);
  }
  .crack-row:last-child{border-bottom:none;}
  .crack-row .who{color:var(--text-dim);}
  .crack-row .val{color:var(--text); font-weight:500;}

  .comp-item{
    display:flex; justify-content:space-between; align-items:center; padding:5px 0; font-size:12.5px;
  }
  .comp-check{
    width:16px;height:16px; border-radius:3px; display:flex; align-items:center; justify-content:center;
    font-size:10px; flex-shrink:0; font-family:'IBM Plex Mono',monospace; font-weight:700;
  }
  .comp-check.yes{background:rgba(79,176,160,0.16); color:var(--teal); border:1px solid rgba(79,176,160,0.4);}
  .comp-check.no{background:rgba(224,87,79,0.12); color:var(--red); border:1px solid rgba(224,87,79,0.35);}
  .comp-item span{flex:1; margin-right:8px; color:var(--text-dim);}
  .comp-item.active span{color:var(--text);}

  .pool-line{font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--text-dim); padding:4px 0; display:flex; justify-content:space-between;}
  .pool-line b{color:var(--text);}

  /* pattern warnings */
  .warn-panel{
    background:var(--panel); border:1px solid var(--edge); border-radius:6px; padding:16px 18px; margin-bottom:18px;
  }
  .warn-item{
    display:flex; gap:10px; align-items:flex-start; padding:8px 0;
    border-bottom:1px dashed rgba(200,155,60,0.14); font-size:13px; line-height:1.55;
  }
  .warn-item:last-child{border-bottom:none;}
  .warn-tag{
    font-family:'IBM Plex Mono',monospace; font-size:9.5px; padding:2px 6px; border-radius:3px;
    text-transform:uppercase; letter-spacing:0.06em; flex-shrink:0; margin-top:2px; font-weight:600;
  }
  .warn-tag.high{background:rgba(224,87,79,0.16); color:var(--red); border:1px solid rgba(224,87,79,0.4);}
  .warn-tag.mid{background:rgba(224,164,88,0.14); color:var(--amber); border:1px solid rgba(224,164,88,0.35);}
  .warn-empty{color:var(--text-faint); font-size:12.5px; font-family:'IBM Plex Mono',monospace; padding:6px 0;}

  .footer-note{
    text-align:center; font-size:11px; color:var(--text-faint); font-family:'IBM Plex Mono',monospace;
    margin-top:26px; line-height:1.7;
  }
  .footer-note b{color:var(--brass);}
</style>
</head>
<body>
<div class="wrap">

  <div class="header">
    <div class="brand">
      <div class="brand-mark"></div>
      <div>
        <h1>PASSWORD VAULT ANALYZER</h1>
        <div class="subtitle">ADVANCED STRENGTH &amp; ENTROPY AUDIT</div>
      </div>
    </div>
    <div class="case-id">Local analysis only · no data ever leaves your browser<br>REF <span id="refid">—</span></div>
  </div>

  <div class="vault-input">
    <div class="corner tl"></div><div class="corner tr"></div><div class="corner bl"></div><div class="corner br"></div>
    <div class="label-row">
      <div class="field-label">Test Password</div>
      <button class="gen-btn" id="genBtn">↻ Generate Strong Password</button>
    </div>
    <div class="input-row">
      <input type="password" id="pwd" placeholder="Type a password here..." autocomplete="off" spellcheck="false">
      <button class="icon-btn" id="toggleBtn" title="Show/hide">👁</button>
      <button class="icon-btn" id="copyBtn" title="Copy">⧉</button>
    </div>
    <div class="hint">This tool runs entirely in your browser — no password is ever sent anywhere.</div>
  </div>

  <div class="gauge-section">
    <div class="gauge-wrap">
      <svg viewBox="0 0 200 130" width="190" id="gaugeSvg">
        <!-- tick marks -->
        <g id="ticks"></g>
        <path id="track" d="" fill="none" stroke="#1e2a42" stroke-width="14" stroke-linecap="round"/>
        <path id="arc" d="" fill="none" stroke="var(--brass)" stroke-width="14" stroke-linecap="round"/>
        <line id="needle" x1="100" y1="100" x2="100" y2="35" stroke="var(--brass-bright)" stroke-width="3" stroke-linecap="round"/>
        <circle cx="100" cy="100" r="7" fill="#0a0f1a" stroke="var(--brass-bright)" stroke-width="2"/>
      </svg>
      <div class="score-num">SCORE <b id="scoreText">0</b>/100</div>
    </div>
    <div>
      <div class="verdict-label" id="verdictLabel" style="color:var(--text-faint)">Awaiting input...</div>
      <div class="verdict-sub" id="verdictSub">Type a password above to begin the analysis.</div>
      <div class="entropy-bar-track"><div class="entropy-bar-fill" id="entropyFill"></div></div>
      <div class="entropy-caption"><span>Weak</span><span id="entropyBits">0 bits of entropy</span><span>Strong</span></div>
    </div>
  </div>

  <div class="grid-3">
    <div class="stat-card">
      <div class="stat-title">Crack Time Estimate</div>
      <div class="crack-row"><span class="who">Online (throttled)</span><span class="val" id="ct1">—</span></div>
      <div class="crack-row"><span class="who">Offline (bcrypt)</span><span class="val" id="ct2">—</span></div>
      <div class="crack-row"><span class="who">Offline (GPU rig)</span><span class="val" id="ct3">—</span></div>
    </div>
    <div class="stat-card">
      <div class="stat-title">Character Composition</div>
      <div class="comp-item" id="c-len"><div class="comp-check no">×</div><span>Length ≥ 12</span></div>
      <div class="comp-item" id="c-low"><div class="comp-check no">×</div><span>Lowercase (a-z)</span></div>
      <div class="comp-item" id="c-up"><div class="comp-check no">×</div><span>Uppercase (A-Z)</span></div>
      <div class="comp-item" id="c-num"><div class="comp-check no">×</div><span>Digits (0-9)</span></div>
      <div class="comp-item" id="c-sym"><div class="comp-check no">×</div><span>Symbols (!@#...)</span></div>
    </div>
    <div class="stat-card">
      <div class="stat-title">Raw Data</div>
      <div class="pool-line"><span>Length</span><b id="rawLen">0</b></div>
      <div class="pool-line"><span>Character pool</span><b id="rawPool">0</b></div>
      <div class="pool-line"><span>Theoretical combinations</span><b id="rawCombo">0</b></div>
      <div class="pool-line"><span>Unique characters</span><b id="rawUniq">0</b></div>
    </div>
  </div>

  <div class="warn-panel">
    <div class="stat-title" style="margin-bottom:12px;">Pattern &amp; Weakness Detection</div>
    <div id="warnList"><div class="warn-empty">No analysis yet.</div></div>
  </div>

  <div class="footer-note">All calculations happen right here in your browser — <b>nothing is ever sent over the network.</b> Use a password manager for real credentials.</div>

</div>

<script>
document.getElementById('refid').textContent = 'PVA-' + Math.random().toString(36).slice(2,8).toUpperCase();

const commonPasswords = new Set(["password","123456","123456789","12345678","12345","1234567","qwerty","abc123","password1","admin","welcome","letmein","monkey","football","iloveyou","000000","111111","123123","dragon","master","sunshine","princess","qwerty123","1q2w3e4r","passw0rd","trustno1","superman","hello","charlie","aa123456","1234","google","access","shadow","michael","jennifer","2000","696969","batman","donald","666666","7777777","121212","freedom","whatever","ninja","azerty","liverpool","asdfgh"]);

const keyboardRows = ["qwertyuiop","asdfghjkl","zxcvbnm","1234567890"];
const sequences = ["abcdefghijklmnopqrstuvwxyz","0123456789"];

function hasSequential(s){
  const low = s.toLowerCase();
  for(const seq of sequences){
    for(let i=0;i<=seq.length-3;i++){
      const fwd = seq.slice(i,i+3);
      const rev = fwd.split('').reverse().join('');
      if(low.includes(fwd) || low.includes(rev)) return true;
    }
  }
  return false;
}
function hasKeyboardWalk(s){
  const low = s.toLowerCase();
  for(const row of keyboardRows){
    for(let i=0;i<=row.length-3;i++){
      const fwd = row.slice(i,i+3);
      const rev = fwd.split('').reverse().join('');
      if(low.includes(fwd) || low.includes(rev)) return true;
    }
  }
  return false;
}
function hasRepeats(s){
  return /(.)\1\1/.test(s);
}
function hasDateLike(s){
  return /(19|20)\d{2}/.test(s) || /\b\d{1,2}[\/\-]\d{1,2}\b/.test(s);
}
function countUnique(s){
  return new Set(s.split('')).size;
}

function formatTime(seconds){
  if(seconds < 1) return "instantly";
  if(seconds < 60) return Math.ceil(seconds)+" seconds";
  let mins = seconds/60; if(mins<60) return Math.ceil(mins)+" minutes";
  let hrs = mins/60; if(hrs<24) return Math.ceil(hrs)+" hours";
  let days = hrs/24; if(days<30) return Math.ceil(days)+" days";
  let months = days/30; if(months<12) return Math.ceil(months)+" months";
  let years = days/365;
  if(years < 100) return Math.ceil(years)+" years";
  if(years < 1000) return Math.ceil(years/100)+" centuries";
  if(years < 1e6) return Math.ceil(years/1000)+" thousand years";
  if(years < 1e9) return (years/1e6).toFixed(1)+" million years";
  return "longer than the age of the universe";
}

function polar(cx,cy,r,angleDeg){
  const a = (angleDeg-180)*Math.PI/180;
  return {x: cx + r*Math.cos(a), y: cy + r*Math.sin(a)};
}
function describeArc(cx,cy,r,startAngle,endAngle){
  const s = polar(cx,cy,r,endAngle);
  const e = polar(cx,cy,r,startAngle);
  const largeArc = endAngle-startAngle <= 180 ? 0 : 1;
  return `M ${s.x} ${s.y} A ${r} ${r} 0 ${largeArc} 0 ${e.x} ${e.y}`;
}

// draw static track + ticks once
const track = document.getElementById('track');
track.setAttribute('d', describeArc(100,100,80,0,180));
const ticksG = document.getElementById('ticks');
for(let i=0;i<=10;i++){
  const ang = i*18;
  const p1 = polar(100,100,70,ang);
  const p2 = polar(100,100,80,ang);
  const line = document.createElementNS("http://www.w3.org/2000/svg","line");
  line.setAttribute('x1',p1.x); line.setAttribute('y1',p1.y);
  line.setAttribute('x2',p2.x); line.setAttribute('y2',p2.y);
  line.setAttribute('stroke','#2a3652'); line.setAttribute('stroke-width','2');
  ticksG.appendChild(line);
}

function updateGauge(score){
  const arc = document.getElementById('arc');
  const angle = score*1.8; // 0-180
  let color = '#e0574f';
  if(score>=75) color = '#4fb0a0';
  else if(score>=50) color = '#c99a45';
  else if(score>=25) color = '#e0a458';
  arc.setAttribute('stroke', color);
  arc.setAttribute('d', score>0 ? describeArc(100,100,80,0,Math.max(angle,0.01)) : '');
  const needle = document.getElementById('needle');
  const tip = polar(100,100,65,angle);
  needle.setAttribute('x2', tip.x); needle.setAttribute('y2', tip.y);
  needle.setAttribute('stroke', color);
  document.getElementById('scoreText').textContent = Math.round(score);
}

function analyze(pwd){
  const warnList = document.getElementById('warnList');
  const len = pwd.length;

  if(len===0){
    updateGauge(0);
    document.getElementById('verdictLabel').textContent = 'Awaiting input...';
    document.getElementById('verdictLabel').style.color = 'var(--text-faint)';
    document.getElementById('verdictSub').textContent = 'Type a password above to begin the analysis.';
    document.getElementById('entropyFill').style.width = '0%';
    document.getElementById('entropyBits').textContent = '0 bits of entropy';
    document.getElementById('ct1').textContent='—'; document.getElementById('ct2').textContent='—'; document.getElementById('ct3').textContent='—';
    document.getElementById('rawLen').textContent='0'; document.getElementById('rawPool').textContent='0';
    document.getElementById('rawCombo').textContent='0'; document.getElementById('rawUniq').textContent='0';
    ['c-len','c-low','c-up','c-num','c-sym'].forEach(id=>{
      const el = document.getElementById(id);
      el.classList.remove('active');
      el.querySelector('.comp-check').className='comp-check no';
      el.querySelector('.comp-check').textContent='×';
    });
    warnList.innerHTML = '<div class="warn-empty">No analysis yet.</div>';
    return;
  }

  const hasLower = /[a-z]/.test(pwd);
  const hasUpper = /[A-Z]/.test(pwd);
  const hasNum = /[0-9]/.test(pwd);
  const hasSym = /[^a-zA-Z0-9]/.test(pwd);
  const isLong = len>=12;

  let pool = 0;
  if(hasLower) pool+=26;
  if(hasUpper) pool+=26;
  if(hasNum) pool+=10;
  if(hasSym) pool+=32;
  if(pool===0) pool=1;

  let entropy = len * Math.log2(pool);

  // penalties
  const warnings = [];
  const lowerPwd = pwd.toLowerCase();
  if(commonPasswords.has(lowerPwd)){
    warnings.push({tag:'high', text:'This is a well-known common password — appears near the top of breach dictionaries.'});
    entropy = Math.min(entropy, 10);
  }
  if(hasSequential(pwd)){
    warnings.push({tag:'high', text:'Sequential character pattern found (e.g. "abc" or "123").'});
    entropy *= 0.6;
  }
  if(hasKeyboardWalk(pwd)){
    warnings.push({tag:'high', text:'Keyboard-walk pattern found (e.g. "qwerty" or "asdf").'});
    entropy *= 0.6;
  }
  if(hasRepeats(pwd)){
    warnings.push({tag:'mid', text:'The same character repeats 3 or more times in a row.'});
    entropy *= 0.8;
  }
  if(hasDateLike(pwd)){
    warnings.push({tag:'mid', text:'Looks like it contains a year or date pattern — these are easy to guess.'});
    entropy *= 0.9;
  }
  if(len < 8){
    warnings.push({tag:'high', text:'Length is under 8 characters — can be brute-forced very quickly.'});
  } else if(len < 12){
    warnings.push({tag:'mid', text:'Length is under 12 characters — consider making it longer for better security.'});
  }
  const uniq = countUnique(pwd);
  if(uniq < len*0.6 && len>=6){
    warnings.push({tag:'mid', text:'Low ratio of unique characters — more variety would raise the entropy.'});
  }
  if(!hasSym){
    warnings.push({tag:'mid', text:'No symbols or special characters used (!@#$% etc.).'});
  }
  if(!hasUpper || !hasLower){
    warnings.push({tag:'mid', text:'Only one letter case is used — mix uppercase and lowercase.'});
  }

  entropy = Math.max(0, entropy);
  const score = Math.min(100, Math.round((entropy/90)*100));

  updateGauge(score);

  let label, color, sub;
  if(score < 25){ label='VERY WEAK'; color='var(--red)'; sub='This password can be guessed within seconds. Do not use it.'; }
  else if(score < 50){ label='WEAK'; color='var(--amber)'; sub='Not secure enough for any important account.'; }
  else if(score < 75){ label='FAIR'; color='var(--brass-bright)'; sub='Usable, but it can be made considerably stronger.'; }
  else if(score < 90){ label='STRONG'; color='var(--teal)'; sub='A good password — able to withstand most attacks.'; }
  else { label='VERY STRONG'; color='var(--teal)'; sub='Excellent — high entropy and no common patterns detected.'; }

  const vl = document.getElementById('verdictLabel');
  vl.textContent = label; vl.style.color = color;
  document.getElementById('verdictSub').textContent = sub;
  document.getElementById('entropyFill').style.width = score+'%';
  document.getElementById('entropyFill').style.background = color;
  document.getElementById('entropyBits').textContent = entropy.toFixed(1)+' bits of entropy';

  // crack times: guesses ~ 2^entropy, average = half of keyspace
  const guesses = Math.pow(2, entropy) / 2;
  document.getElementById('ct1').textContent = formatTime(guesses / (100/3600)); // 100 guesses/hour
  document.getElementById('ct2').textContent = formatTime(guesses / 10000); // 10k/sec bcrypt
  document.getElementById('ct3').textContent = formatTime(guesses / 1e10); // 10 billion/sec GPU rig

  document.getElementById('rawLen').textContent = len;
  document.getElementById('rawPool').textContent = pool;
  document.getElementById('rawCombo').textContent = 'pool^length';
  document.getElementById('rawUniq').textContent = uniq + ' / ' + len;

  const comps = [
    ['c-len', isLong], ['c-low', hasLower], ['c-up', hasUpper], ['c-num', hasNum], ['c-sym', hasSym]
  ];
  comps.forEach(([id,ok])=>{
    const el = document.getElementById(id);
    el.classList.toggle('active', ok);
    const chk = el.querySelector('.comp-check');
    chk.className = 'comp-check ' + (ok?'yes':'no');
    chk.textContent = ok ? '✓' : '×';
  });

  if(warnings.length===0){
    warnList.innerHTML = '<div class="warn-item"><span class="warn-tag" style="background:rgba(79,176,160,0.16);color:var(--teal);border:1px solid rgba(79,176,160,0.4);">OK</span><span>No common weak patterns detected.</span></div>';
  } else {
    warnList.innerHTML = warnings.map(w=>
      `<div class="warn-item"><span class="warn-tag ${w.tag}">${w.tag==='high'?'RISK':'WARNING'}</span><span>${w.text}</span></div>`
    ).join('');
  }
}

const pwdInput = document.getElementById('pwd');
pwdInput.addEventListener('input', ()=>analyze(pwdInput.value));

document.getElementById('toggleBtn').addEventListener('click', ()=>{
  pwdInput.type = pwdInput.type==='password' ? 'text' : 'password';
});

document.getElementById('copyBtn').addEventListener('click', ()=>{
  if(!pwdInput.value) return;
  navigator.clipboard.writeText(pwdInput.value).then(()=>{
    const btn = document.getElementById('copyBtn');
    const old = btn.textContent;
    btn.textContent = '✓';
    setTimeout(()=>btn.textContent=old, 1000);
  });
});

document.getElementById('genBtn').addEventListener('click', ()=>{
  const lower='abcdefghijklmnopqrstuvwxyz', upper='ABCDEFGHIJKLMNOPQRSTUVWXYZ', nums='0123456789', syms='!@#$%^&*()-_=+[]{}';
  const all = lower+upper+nums+syms;
  let pass = '';
  const required = [lower,upper,nums,syms];
  required.forEach(set=>{ pass += set[Math.floor(Math.random()*set.length)]; });
  for(let i=pass.length;i<16;i++){
    pass += all[Math.floor(Math.random()*all.length)];
  }
  pass = pass.split('').sort(()=>Math.random()-0.5).join('');
  pwdInput.type = 'text';
  pwdInput.value = pass;
  analyze(pass);
});

analyze('');
</script>
</body>
</html>
