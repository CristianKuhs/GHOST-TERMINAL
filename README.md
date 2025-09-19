
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tela Hacker — Funcional</title>
  <style>
    :root{--bg:#07121a;--panel:rgba(255,255,255,0.02);--accent:#00ff99;--accent-2:#66ffcc;--muted:rgba(255,255,255,0.35);--glass:rgba(255,255,255,0.03);--font-mono:ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", monospace}
    [data-theme="light"]{--bg:#f6faf9;--panel:rgba(0,0,0,0.03);--accent:#0a6b3a;--accent-2:#1f8f56;--muted:rgba(0,0,0,0.6);--glass:rgba(255,255,255,0.6)}
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:var(--font-mono);background:var(--bg);color:var(--accent)}
    canvas#matrix{position:fixed;inset:0;z-index:0;pointer-events:none}
    .app{display:grid;grid-template-columns:1fr 420px;gap:18px;padding:18px;height:100vh}
    @media(max-width:980px){.app{grid-template-columns:1fr;grid-auto-rows:auto;height:auto;padding:12px}}
    .panel{position:relative;z-index:2;background:linear-gradient(180deg,var(--panel),transparent);border-radius:12px;padding:14px;border:1px solid rgba(0,255,150,0.04);backdrop-filter:blur(6px);box-shadow:0 8px 30px rgba(0,0,0,0.6)}
    .terminal{display:flex;flex-direction:column;height:calc(100vh - 36px);overflow:hidden}
    .term-head{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
    .title{font-weight:800;color:var(--accent-2);letter-spacing:0.6px}
    .controls{display:flex;gap:8px;align-items:center}
    .btn{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:6px 8px;border-radius:8px;cursor:pointer;font-size:13px}
    .btn.primary{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#001;border:none}
    .term-body{flex:1;overflow:auto;background:linear-gradient(180deg,rgba(0,0,0,0.18),rgba(0,0,0,0.06));padding:12px;border-radius:8px;font-size:13px;line-height:1.45}
    .term-line{white-space:pre-wrap}
    .term-footer{display:flex;align-items:center;justify-content:space-between;margin-top:10px;color:var(--muted);font-size:13px}
    .sidebar{display:flex;flex-direction:column;gap:12px;height:calc(100vh - 36px);overflow:auto}
    .card{padding:12px;border-radius:10px;background:var(--glass);border:1px solid rgba(0,255,150,0.04)}
    .user-big{font-size:28px;font-weight:800;color:var(--accent-2)}
    .label{font-size:12px;color:var(--muted);margin-top:6px}
    .bars{display:flex;gap:8px;align-items:end;height:90px}
    .bar{flex:1;background:rgba(0,0,0,0.18);border-radius:8px;padding:6px;display:flex;flex-direction:column-reverse}
    .bar-fill{height:8px;border-radius:6px;background:linear-gradient(90deg,var(--accent),var(--accent-2));}
    .hex-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;font-size:12px}
    .hex{padding:10px;background:rgba(0,0,0,0.18);border-radius:8px}
    #waveCanvas{width:100%;height:90px;border-radius:8px;background:linear-gradient(180deg, rgba(0,0,0,0.06), rgba(0,0,0,0.02));}
    .config{display:flex;flex-direction:column;gap:8px}
    .row{display:flex;gap:8px;align-items:center}
    .input, .select, .range{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:8px;border-radius:8px;color:inherit}
    .muted{color:var(--muted);font-size:13px}
    #seedInputVisible{width:100%}
  </style>
</head>
<body data-theme="dark">
  <canvas id="matrix" aria-hidden="true"></canvas>
  <div class="app">
    <div class="panel terminal" role="main" aria-label="Terminal simulado">
      <div class="term-head">
        <div class="title">H4CK-SIM • Funcional</div>
        <div class="controls">
          <button class="btn" id="toggleTheme">Tema</button>
          <button class="btn" id="clearBtn">Limpar</button>
          <button class="btn primary" id="presetBtn">Preset</button>
        </div>
      </div>
      <div class="term-body" id="terminal" tabindex="0" aria-live="polite"></div>
      <div class="term-footer">
        <div class="muted">Clique e digite — tudo muda conforme o texto</div>
        <div style="display:flex;gap:8px;align-items:center">
          <div class="muted small">Seed: <span id="seedDisplay">—</span></div>
          <button class="btn" id="seedCopy">copiar</button>
        </div>
      </div>
    </div>
    <div class="sidebar">
      <div class="card">
        <div class="label">Usuário</div>
        <div class="user-big" id="userName">guest_000</div>
        <div class="label">Status</div>
        <div id="status">ACTIVE</div>
        <div class="label">Relógio</div>
        <div id="clock" class="muted">--:--:--</div>
      </div>
      <div class="card">
        <div class="label">CPUs / Load</div>
        <div class="bars" id="cpuBars"></div>
        <div class="label">Rede (Mbps)</div>
        <div id="netSpeed" style="font-weight:800">0 Mbps</div>
      </div>
      <div class="card">
        <div class="label">Hex Dump</div>
        <div class="hex-grid" id="hexGrid"></div>
      </div
      <div class="card">
        <div class="label">Waveform</div>
        <canvas id="waveCanvas"></canvas>
      </div>
      <div class="card config">
        <div class="label">Controles</div>
        <div class="row"><input id="seedInputVisible" class="input" placeholder="digite aqui" aria-label="campo de seed visível"/></div>
        <div class="row"><label class="muted">Velocidade</label><input id="speed" type="range" min="50" max="2000" value="400" class="range"/></div>
        <div class="row"><label class="muted">Tema</label><select id="themeSelect" class="select"><option value="dark">Escuro</option><option value="light">Claro</option></select></div>
        <div class="row"><label class="muted">Sons</label><input id="soundToggle" type="checkbox"/></div>
        <div class="row"><button class="btn" id="exportPNG">Exportar PNG</button><button class="btn" id="exportSeedTxt">Salvar Seed</button></div>
        <div class="row"><label class="muted">Presets</label><select id="presetList" class="select"><option value="random">Random</option><option value="matrix">Matrix</option><option value="breach">Breach</option><option value="stealth">Stealth</option></select></div>
      </div>
    </div>
  </div>

  <script>
    // Helpers
    function hashStringToInt(s){ let h = 2166136261 >>> 0; for(let i=0;i<s.length;i++){ h ^= s.charCodeAt(i); h = Math.imul(h,16777619) >>> 0; } return h >>> 0; }
    function makeRng(seed){ let x = seed || 123456789; return function(){ x ^= x << 13; x >>>= 0; x ^= x >>> 17; x ^= x << 5; x >>>= 0; return (x >>> 0) / 4294967295; } }

    // DOM
    const terminal = document.getElementById('terminal');
    const userName = document.getElementById('userName');
    const status = document.getElementById('status');
    const clock = document.getElementById('clock');
    const cpuBars = document.getElementById('cpuBars');
    const netSpeed = document.getElementById('netSpeed');
    const hexGrid = document.getElementById('hexGrid');
    const seedDisplay = document.getElementById('seedDisplay');
    const seedInputVisible = document.getElementById('seedInputVisible');
    const seedCopy = document.getElementById('seedCopy');
    const speedRange = document.getElementById('speed');
    const themeSelect = document.getElementById('themeSelect');
    const soundToggle = document.getElementById('soundToggle');
    const matrixCanvas = document.getElementById('matrix');
    const mctx = matrixCanvas.getContext('2d');
    const waveCanvas = document.getElementById('waveCanvas');
    const waveCtx = waveCanvas.getContext('2d');

    // state
    let currentSeed = '';
    let scheduled = null;
    let soundsOn = false;

    // canvas resize utility
    function resizeCanvases(){
      const dpr = window.devicePixelRatio || 1;
      // matrix
      matrixCanvas.width = Math.floor(window.innerWidth * dpr);
      matrixCanvas.height = Math.floor(window.innerHeight * dpr);
      matrixCanvas.style.width = window.innerWidth + 'px';
      matrixCanvas.style.height = window.innerHeight + 'px';
      mctx.setTransform(dpr,0,0,dpr,0,0);
      // waveform
      const w = Math.max(300, waveCanvas.clientWidth);
      waveCanvas.width = Math.floor(w * dpr);
      waveCanvas.height = Math.floor(90 * dpr);
      waveCanvas.style.width = w + 'px';
      waveCanvas.style.height = '90px';
      waveCtx.setTransform(dpr,0,0,dpr,0,0);
    }
    window.addEventListener('resize', resizeCanvases);
    resizeCanvases();

    // matrix variables
    let cols = Math.floor(window.innerWidth / 14);
    let drops = Array(cols).fill(1);
    function resetMatrix(){ cols = Math.floor(window.innerWidth / 14); drops = new Array(cols).fill(1); }
    window.addEventListener('resize', resetMatrix);

    function drawMatrix(){
      // fade
      mctx.fillStyle = 'rgba(0,0,0,0.06)';
      mctx.fillRect(0,0, matrixCanvas.width / (window.devicePixelRatio || 1), matrixCanvas.height / (window.devicePixelRatio || 1));
      mctx.font = '13px monospace';
      for(let i=0;i<cols;i++){
        const text = String.fromCharCode(0x30A0 + Math.random() * 96);
        mctx.fillStyle = i%2 ? 'rgba(0,255,160,0.12)' : 'rgba(0,255,160,0.06)';
        mctx.fillText(text, i*14, drops[i]*14);
        if(drops[i]*14 > (matrixCanvas.height / (window.devicePixelRatio || 1)) && Math.random() > 0.975) drops[i]=0;
        drops[i]++;
      }
      requestAnimationFrame(drawMatrix);
    }
    drawMatrix();

    // UI update from seed
    function updateFromSeed(text){
      currentSeed = String(text || '');
      const seedInt = hashStringToInt(currentSeed || 'init');
      const rng = makeRng(seedInt || 1);
      seedDisplay.textContent = '0x' + seedInt.toString(16).padStart(8,'0');

      // username and status
      const names = ['root','guest','neo','tr0jan','shadow','script','daemon','sys'];
      userName.textContent = names[Math.floor(rng()*names.length)] + '_' + Math.floor(rng()*9999).toString().padStart(4,'0');
      status.textContent = rng() > 0.8 ? 'SUSPECT' : (rng() > 0.35 ? 'ACTIVE' : 'IDLE');

      // terminal lines
      const templates = [
        `${userName.textContent}@192.168.${Math.floor(rng()*255)}.${Math.floor(rng()*255)}:~$ ssh ${userName.textContent}@198.51.100.${Math.floor(rng()*255)}`,
        `auth: ${rng()>0.5? 'OK':'FAIL'} token:${Math.floor(rng()*1e9).toString(16)}`,
        `proc[${Math.floor(rng()*9999)}]: alloc ${Math.floor(rng()*1e6)} bytes`,
        `net.iface: eth${Math.floor(rng()*8)} tx:${Math.floor(rng()*999)}MB rx:${Math.floor(rng()*999)}MB`,
        `grep -i \"${(currentSeed||'query').slice(0,8)}\" /var/log/syslog | tail -n ${Math.floor(rng()*20)}`,
        `scan:${Math.floor(rng()*100)}% crc:${Math.floor(rng()*65535).toString(16)}`
      ];

      const lines = 12 + Math.floor(rng()*48);
      terminal.innerHTML = '';
      for(let i=0;i<lines;i++){
        const t = templates[Math.floor(rng()*templates.length)];
        const extra = rng()>0.72 ? ('  > ' + Math.random().toString(36).slice(2, 10)) : '';
        const node = document.createElement('div'); node.className = 'term-line';
        node.textContent = '[' + new Date(Date.now() - Math.floor(rng()*1e7)).toISOString().replace('T',' ').slice(0,19) + '] ' + t + extra;
        terminal.appendChild(node);
      }
      terminal.scrollTop = terminal.scrollHeight;

      // cpus
      cpuBars.innerHTML = '';
      const cpus = 2 + Math.floor(rng()*8);
      for(let i=0;i<cpus;i++){
        const fill = Math.floor(rng()*100);
        const b = document.createElement('div'); b.className='bar'; const f = document.createElement('div'); f.className='bar-fill'; f.style.height = Math.max(6, fill/1.8) + '%'; b.appendChild(f); cpuBars.appendChild(b);
      }

      // net speed
      netSpeed.textContent = Math.floor(10 + rng()*990) + ' Mbps';

      // hex grid
      hexGrid.innerHTML = '';
      for(let i=0;i<9;i++){ const h = Math.floor(rng()*0xffffffff).toString(16).padStart(8,'0'); const div = document.createElement('div'); div.className='hex'; div.textContent = h; hexGrid.appendChild(div); }

      // waveform
      drawWave(rng);

      // sound
      if(soundsOn) playBeep(200 + (seedInt % 800));
    }

    // waveform drawing
    function drawWave(rng){
      const w = Math.max(300, waveCanvas.clientWidth);
      const h = 90;
      waveCtx.clearRect(0,0,waveCanvas.width,waveCanvas.height);
      waveCtx.beginPath(); waveCtx.lineWidth = 1.6; waveCtx.strokeStyle = 'rgba(0,255,150,0.95)';
      waveCtx.moveTo(0,h/2);
      for(let x=0;x<w;x+=2){ const y = h/2 + Math.sin((x/6) + rng()*10) * (12 + rng()*28); waveCtx.lineTo(x,y); }
      waveCtx.stroke();
    }

    // clock
    const clockEl = document.getElementById('clock');
    function refreshClock(){ const d = new Date(); clockEl.textContent = d.toLocaleTimeString(); }
    setInterval(refreshClock,1000); refreshClock();

    // scheduling updates
    const speedEl = document.getElementById('speed');
    function scheduleUpdate(val){ if(scheduled) clearTimeout(scheduled); const d = Math.max(50, parseInt(speedEl.value || 400)); scheduled = setTimeout(()=>{ updateFromSeed(val); scheduled = null; }, d); }

    // input behaviour
    seedInputVisible.addEventListener('input', ()=> scheduleUpdate(seedInputVisible.value));
    // capture keyboard even if input not focused
    let ignoreNextKey = false; // to avoid double when typing into input
    seedInputVisible.addEventListener('keydown', ()=>{ ignoreNextKey = true; setTimeout(()=>ignoreNextKey=false,30); });
    document.addEventListener('keydown', (ev)=>{
      if(ignoreNextKey) return; // user is typing in visible input
      if(ev.key.length === 1){ seedInputVisible.value += ev.key; scheduleUpdate(seedInputVisible.value); }
      else if(ev.key === 'Backspace'){ seedInputVisible.value = seedInputVisible.value.slice(0,-1); scheduleUpdate(seedInputVisible.value); }
      else if(ev.key === 'Enter'){ seedInputVisible.value += '
'; scheduleUpdate(seedInputVisible.value); }
    });

    // theme controls
    document.getElementById('toggleTheme').addEventListener('click', ()=>{ document.body.dataset.theme = document.body.dataset.theme === 'dark' ? 'light' : 'dark'; themeSelect.value = document.body.dataset.theme; });
    themeSelect.addEventListener('change', (e)=>{ document.body.dataset.theme = e.target.value; });

    // other controls
    document.getElementById('clearBtn').addEventListener('click', ()=>{ terminal.innerHTML = ''; });
    document.getElementById('presetBtn').addEventListener('click', ()=> applyPreset(document.getElementById('presetList').value));
    document.getElementById('presetList').addEventListener('change',(e)=> applyPreset(e.target.value));
    soundToggle.addEventListener('change',(e)=>{ soundsOn = e.target.checked; if(soundsOn) { try{ audioCtx.resume(); }catch(e){} } });
    seedCopy.addEventListener('click', async ()=>{ try{ await navigator.clipboard.writeText(seedInputVisible.value || ''); seedCopy.textContent = 'copiado'; setTimeout(()=>seedCopy.textContent='copiar',800); }catch(e){ seedCopy.textContent='erro' } });
    document.getElementById('exportSeedTxt').addEventListener('click', ()=> downloadText(seedInputVisible.value || '', 'seed.txt'));
    document.getElementById('exportPNG').addEventListener('click', exportPNG);

    // presets
    function applyPreset(key){ const map = { random: ()=>{ seedInputVisible.value = 'rnd-'+Math.random().toString(36).slice(2,12); scheduleUpdate(seedInputVisible.value); }, matrix: ()=>{ seedInputVisible.value = 'matrix:green-stream'; scheduleUpdate(seedInputVisible.value); }, breach: ()=>{ seedInputVisible.value = 'BREACH-9000'; scheduleUpdate(seedInputVisible.value); }, stealth: ()=>{ seedInputVisible.value = 'stealth-mode:alpha'; scheduleUpdate(seedInputVisible.value); } }; (map[key]||map.random)(); }

    // export PNG
    function exportPNG(){ try{
      const dpr = window.devicePixelRatio || 1;
      const w = Math.min(window.innerWidth, 1400);
      const h = Math.min(window.innerHeight, 900);
      const c = document.createElement('canvas'); c.width = w * dpr; c.height = h * dpr; const ctx = c.getContext('2d'); ctx.scale(dpr,dpr);
      // bg
      ctx.fillStyle = '#001'; ctx.fillRect(0,0,w,h);
      ctx.font = '12px monospace'; ctx.fillStyle = 'rgba(0,255,150,0.95)';
      const lines = Array.from(terminal.querySelectorAll('.term-line')).slice(-40).map(n=>n.textContent);
      for(let i=0;i<lines.length;i++){ ctx.fillText(lines[i].slice(0,120), 12, 30 + i*16); }
      const url = c.toDataURL('image/png'); const a = document.createElement('a'); a.href = url; a.download = 'tela-hacker.png'; a.click();
    }catch(e){ console.error(e); alert('erro ao exportar: ' + e.message);} }

    function downloadText(txt,name){ const blob = new Blob([txt],{type:'text/plain'}); const url = URL.createObjectURL(blob); const a = document.createElement('a'); a.href = url; a.download = name; a.click(); URL.revokeObjectURL(url); }

    // audio
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    function playBeep(freq=440,dur=0.08){ if(!soundsOn) return; const o = audioCtx.createOscillator(); const g = audioCtx.createGain(); o.type = 'sine'; o.frequency.value = freq; g.gain.value = 0.02; o.connect(g); g.connect(audioCtx.destination); o.start(); o.stop(audioCtx.currentTime + dur); }

    // init
    function init(){ resizeCanvases(); resetMatrix(); seedInputVisible.value = 'init-' + Math.random().toString(36).slice(2,10); scheduleUpdate(seedInputVisible.value); }
    init();

    // copy line on click
    terminal.addEventListener('click',(ev)=>{ if(ev.target && ev.target.classList.contains('term-line')){ navigator.clipboard?.writeText(ev.target.textContent || ''); } });

    // ensure terminal is focusable
    terminal.addEventListener('focus', ()=> seedInputVisible.focus());
  </script>
</body>
</html>
