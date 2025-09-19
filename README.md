<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tela Hacker — Simulador</title>
  <style>
    :root{
      --bg:#02060a;
      --panel-bg:rgba(0,0,0,0.4);
      --accent:#00ff99;
      --accent-2:#66ffcc;
      --muted:rgba(255,255,255,0.06);
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", monospace;
    }
    html,body{height:100%;margin:0;background:radial-gradient(1000px 600px at 10% 20%, rgba(0,80,60,0.04), transparent), var(--bg);color:var(--accent);}
    *{box-sizing:border-box}
    .wrap{display:grid;grid-template-columns: 1fr 420px;gap:18px;padding:18px;height:100vh}
    /* Matrix background */
    .matrix{position:fixed;inset:0;z-index:0;pointer-events:none;}
    .panel{position:relative;z-index:2;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border:1px solid rgba(0,255,150,0.04);backdrop-filter: blur(6px);padding:18px;border-radius:10px;box-shadow:0 6px 30px rgba(0,0,0,0.6)}
    /* left (terminal) */
    .terminal{height:calc(100vh - 36px);overflow:hidden;display:flex;flex-direction:column}
    .term-title{font-weight:700;margin-bottom:8px;color:var(--accent-2)}
    .term-body{flex:1;background:linear-gradient(180deg, rgba(0,0,0,0.25), rgba(0,0,0,0.15));padding:12px;border-radius:8px;overflow:auto;line-height:1.4;font-size:14px}
    .term-line{white-space:pre-wrap}
    /* right column */
    .right{display:flex;flex-direction:column;gap:12px;height:calc(100vh - 36px)}
    .card{padding:12px;border-radius:8px;border:1px solid rgba(0,255,150,0.04);background:var(--panel-bg)}
    .big-number{font-size:36px;font-weight:800;color:var(--accent-2)}
    .label{font-size:12px;color:rgba(255,255,255,0.5);margin-top:6px}
    .bars{display:flex;gap:8px;align-items:end;height:80px}
    .bar{flex:1;background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(0,0,0,0.2));border-radius:6px;padding:6px;display:flex;flex-direction:column-reverse}
    .bar-fill{height:10px;border-radius:4px;background:linear-gradient(90deg,var(--accent),var(--accent-2));}
    .hex-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;font-size:12px}
    .hex{padding:8px;background:rgba(0,0,0,0.25);border-radius:6px}
    .footer{display:flex;gap:8px;align-items:center;justify-content:space-between;margin-top:10px;color:rgba(255,255,255,0.45)}
    /* hidden input fills whole page but invisible */
    #seedInput{position:fixed;left:0;top:0;width:100%;height:100%;opacity:0;z-index:9}
    /* small helpers */
    .muted{color:rgba(255,255,255,0.35);font-size:12px}
    .button{padding:6px 10px;border-radius:6px;background:rgba(0,255,150,0.06);border:1px solid rgba(0,255,150,0.06);cursor:pointer}
    @media(max-width:900px){.wrap{grid-template-columns:1fr;grid-auto-rows:auto;height:auto}.right{flex-direction:row;overflow:auto;height:auto}.terminal{height:420px}.panel{margin-bottom:12px}}
  </style>
</head>
<body>
  <!-- matrix backdrop -->
  <canvas class="matrix" id="matrixCanvas"></canvas>
  <div class="wrap">
    <div class="panel terminal" id="leftPanel">
      <div class="term-title">TERMINAL · H4CK-SIM</div>
      <div class="term-body" id="terminal">
        <!-- linhas serão preenchidas via JS -->
      </div>
      <div class="footer">
        <div class="muted">digite qualquer coisa (teclado) — a tela muda conforme o texto</div>
        <div style="display:flex;gap:8px">
          <div class="button" id="copySeed">Copiar seed</div>
          <div class="button" id="randomize">Random</div>
        </div>
      </div>
    </div>
    <div class="right">
      <div class="panel card" style="flex:0 0 220px">
        <div class="label">Usuário</div>
        <div class="big-number" id="userName">guest_000</div>
        <div class="label">Status</div>
        <div id="status">ACTIVE</div>
        <div class="label">Relógio</div>
        <div id="clock" class="muted">--:--:--</div>
      </div>
      <div class="panel card" style="flex:1">
        <div class="label">CPUs / Load</div>
        <div class="bars" id="cpuBars"></div>
        <div class="label">Rede ( Mbps )</div>
        <div id="netSpeed" class="big-number">0</div>
      </div>
      <div class="panel card" style="flex:0 0 220px">
        <div class="label">Hex Dump</div>
        <div class="hex-grid" id="hexGrid"></div>
      </div>
      <div class="panel card" style="flex:1;display:flex;flex-direction:column">
        <div class="label">Waveform</div>
        <canvas id="waveCanvas" height="80"></canvas>
        <div class="label">Random Seeds</div>
        <div id="seedDisplay" class="muted">seed</div>
      </div>
    </div>
  </div>
  <!-- invisible input to capture typed text (focus on click) -->
  <input id="seedInput" spellcheck="false" autocomplete="off" autocapitalize="off" placeholder="digite aqui" />
  <script>
    // === Utility: simple string hash to integer ===
    function hashStringToInt(str){
      let h=2166136261 >>> 0;
      for(let i=0;i<str.length;i++){
        h ^= str.charCodeAt(i);
        h = Math.imul(h,16777619) >>> 0;
      }
      return h >>> 0;
    }
    // === PRNG (xorshift32) seeded from hash ===
    function makeRng(seed){
      let x = seed || 123456789;
      return function(){
        x ^= x << 13; x >>>= 0;
        x ^= x >>> 17;
        x ^= x << 5; x >>>= 0;
        return (x >>> 0) / 4294967295;
      }
    }
    // DOM refs
    const terminal = document.getElementById('terminal');
    const userName = document.getElementById('userName');
    const status = document.getElementById('status');
    const clock = document.getElementById('clock');
    const cpuBars = document.getElementById('cpuBars');
    const netSpeed = document.getElementById('netSpeed');
    const hexGrid = document.getElementById('hexGrid');
    const seedDisplay = document.getElementById('seedDisplay');
    const seedInput = document.getElementById('seedInput');
    const copySeed = document.getElementById('copySeed');
    const randomize = document.getElementById('randomize');
    const waveCanvas = document.getElementById('waveCanvas');
    const waveCtx = waveCanvas.getContext('2d');
    // matrix canvas
    const matrixCanvas = document.getElementById('matrixCanvas');
    const mctx = matrixCanvas.getContext('2d');
    function resizeCanvases(){
      matrixCanvas.width = innerWidth; matrixCanvas.height = innerHeight;
      waveCanvas.width = waveCanvas.clientWidth * devicePixelRatio; waveCanvas.height = 80 * devicePixelRatio;
      waveCtx.scale(devicePixelRatio, devicePixelRatio);
    }
    addEventListener('resize', resizeCanvases);
    resizeCanvases();
    // matrix effect
    const cols = Math.floor(innerWidth/14);
    const drops = new Array(cols).fill(1);
    function drawMatrix(){
      mctx.fillStyle = 'rgba(0,0,0,0.06)';
      mctx.fillRect(0,0,matrixCanvas.width,matrixCanvas.height);
      mctx.font = '13px monospace';
      for(let i=0;i<cols;i++){
        const text = String.fromCharCode(0x30A0 + Math.random()*96);
        mctx.fillStyle = i%2? 'rgba(0,255,160,0.12)' : 'rgba(0,255,160,0.06)';
        mctx.fillText(text, i*14, drops[i]*14);
        if(drops[i]*14 > matrixCanvas.height && Math.random()>0.975) drops[i]=0;
        drops[i]++;
      }
      requestAnimationFrame(drawMatrix);
    }
    drawMatrix();
    // generate UI from seed
    let currentSeed = '';
    function updateFromSeed(text){
      currentSeed = text;
      const seedInt = hashStringToInt(text || '');
      const rng = makeRng(seedInt || 1);
      seedDisplay.textContent = '0x' + seedInt.toString(16).padStart(8,'0');
      // user
      const u = 'usr_' + Math.floor(rng()*9999).toString().padStart(4,'0');
      userName.textContent = u;
      status.textContent = (rng()>0.2)? (rng()>0.6? 'ACTIVE':'IDLE') : 'SUSPECT';
      // terminal lines
      terminal.innerHTML = '';
      const lineTemplates = [
        `ssh ${u}@198.51.100.${Math.floor(rng()*255)}`,
        `auth: ${rng()>0.5? 'OK':'FAIL'}  token:${Math.floor(rng()*1e9).toString(16)}`,
        `proc[${Math.floor(rng()*9999)}]: alloc ${Math.floor(rng()*1e6)} bytes`,
        `net.iface: eth${Math.floor(rng()*8)}  tx:${Math.floor(rng()*999)}MB rx:${Math.floor(rng()*999)}MB`,
        `grep -i "${text.slice(0,6) || 'query'}" /var/log/syslog | tail -n ${Math.floor(rng()*20)}`,
        `§ ${Math.random()>0.5? 'OK':'ERR'}  scan:${Math.floor(rng()*100)}%  —  crc:${Math.floor(rng()*65535).toString(16)}`
      ];
      // make more lines
      const lines = Math.floor(12 + rng()*40);
      for(let i=0;i<lines;i++){
        const t = lineTemplates[Math.floor(rng()*lineTemplates.length)];
        const extra = rng()>0.7? ('  > ' + Math.random().toString(36).slice(2, 10)) : '';
        const node = document.createElement('div'); node.className='term-line';
        node.textContent = '[' + new Date(Date.now() - Math.floor(rng()*1e7)).toISOString().replace('T',' ').slice(0,19) + '] ' + t + extra;
        terminal.appendChild(node);
      }
      terminal.scrollTop = terminal.scrollHeight;
      // cpus
      cpuBars.innerHTML='';
      const cpus = 4 + Math.floor(rng()*6);
      for(let i=0;i<cpus;i++){
        const fill = Math.floor(rng()*100);
        const b = document.createElement('div'); b.className='bar';
        const f = document.createElement('div'); f.className='bar-fill'; f.style.height = (Math.max(4, fill/1.8))+'%';
        b.appendChild(f); cpuBars.appendChild(b);
      }
      // net
      netSpeed.textContent = Math.floor(10 + rng()*990) + ' Mbps';
      // hex grid
      hexGrid.innerHTML='';
      for(let i=0;i<9;i++){
        const h = Math.floor(rng()*0xffffffff).toString(16).padStart(8,'0');
        const div = document.createElement('div'); div.className='hex'; div.textContent = h;
        hexGrid.appendChild(div);
      }
      // waveform
      drawWave(rng);
    }
    // waveform drawing
    function drawWave(rng){
      const w = waveCanvas.clientWidth; const h = 80;
      waveCtx.clearRect(0,0,waveCanvas.width,waveCanvas.height);
      // draw baseline
      waveCtx.beginPath();
      waveCtx.moveTo(0,h/2);
      for(let x=0;x<w;x+=2){
        const y = h/2 + Math.sin((x/4) + rng()*10) * (15 + rng()*20);
        waveCtx.lineTo(x,y);
      }
      waveCtx.lineWidth = 1.5; waveCtx.strokeStyle = 'rgba(0,255,150,0.9)'; waveCtx.stroke();
    }
    // clock
    function refreshClock(){
      const d = new Date();
      clock.textContent = d.toLocaleTimeString();
    }
    setInterval(refreshClock, 1000); refreshClock();
    // seed interactions
    function setSeedTextFromInput(){
      const t = seedInput.value;
      updateFromSeed(t);
    }
    // focus input when clicking anywhere on body so typing affects screen
    document.body.addEventListener('click', ()=>{ seedInput.focus(); });
    seedInput.addEventListener('input', ()=>{ setSeedTextFromInput(); });
    // also listen to keydown to quickly append printable characters (works even if input not focused)
    document.addEventListener('keydown', (ev)=>{
      if(ev.key.length===1){ // printable
        seedInput.value += ev.key;
        setSeedTextFromInput();
      } else if(ev.key==='Backspace'){
        seedInput.value = seedInput.value.slice(0,-1); setSeedTextFromInput();
      } else if(ev.key==='Enter'){
        seedInput.value += '\n'; setSeedTextFromInput();
      }
    });
    // copy seed
    copySeed.addEventListener('click', async ()=>{
      try{ await navigator.clipboard.writeText(currentSeed || ''); copySeed.textContent='copiado'; setTimeout(()=>copySeed.textContent='Copiar seed',900); }catch(e){ copySeed.textContent='erro' }
    });
    randomize.addEventListener('click', ()=>{ seedInput.value = Math.random().toString(36).slice(2,12); setSeedTextFromInput(); });
    // start with a random seed
    seedInput.value = 'init-' + Math.random().toString(36).slice(2,10);
    updateFromSeed(seedInput.value);
    // make initial cpu bars container
    // draw matrix will run via animation frame
    // prevent accidental text selection while typing invisibly
    document.addEventListener('selectstart', (e)=>{ if(e.target===document.body) e.preventDefault(); });
    // small touch: allow clicking a line in terminal to copy
    terminal.addEventListener('click', (ev)=>{
      const t = ev.target && ev.target.textContent; if(t){ navigator.clipboard?.writeText(t); }
    });
  </script>
</body>
</html>
