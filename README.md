<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta name="description" content="Sistema de Gestão de Pessoas e Demandas - refatorado para acessibilidade de cores">
  <title>Sistema de Gestão - Pessoas e Demandas</title>
  <style>
    /* RESET */
    *{margin:0;padding:0;box-sizing:border-box}
    /*
      Sistema de cores semântico (variáveis) para manter contraste e facilitar theming.
      - Variáveis principais: background / surface / text / border / primary / status
      - Comentários indicam motivo das escolhas (contraste / legibilidade)
      - As classes coloridas usadas por JS (`bg-...`) continuam existindo, mas agora
        usam as variáveis semânticas garantindo contraste do texto interno.
    */
    :root{
      /* Base (dark) palette */
      --bg-900:#020617; /* muito escuro - usado no gradiente de fundo */
      --bg-800:#0b1220; /* superfícies profundas */
      --surface:#0f172a; /* superfície principal (cards, modais) */
      --surface-1:#111827; /* variante */
      --surface-2:#1e293b; /* cards leves/bordas internas */
      /* Textos */
      --text-primary:#E6EEF8; /* alto contraste sobre superfícies escuras */
      --text-secondary:#9aa6b3; /* leitura secundária */
      --muted:#64748b; /* para rótulos, placeholders */
      /* Bordas / dividers */
      --border:#22303f; /* com contraste sutil sobre surface */
      /* Primary (ação) */
      --primary:#2563eb; /* azul principal (mantido) */
      --primary-strong:#1e40af; /* para hover/estados */
      --primary-contrast:#ffffff; /* cor do texto sobre primary */
      /* Status */
      --success:#16a34a; /* verde para sucesso — suficiente contraste */
      --warning:#f59e0b; /* amarelo (usar com cuidado sobre superfícies claras) */
      --danger:#ef4444; /* vermelho para erros */
      /* semântica para pontos coloridos (mantemos nomes compatíveis) */
      --blue-500:var(--primary);
      --purple-500:#a855f7;
      --yellow-400:#facc15;
      --green-400:#22c55e;
      --pink-500:#ec4899;
      --indigo-500:#6366f1;
      --orange-500:#f97316;
      --red-500:#ef4444;
      --teal-500:#14b8a6;
      --cyan-500:#06b6d4;
      /* Accessibility helpers */
      --dot-border:rgba(255,255,255,0.08);
      /* sizes */
      --radius:8px;
      --radius-lg:12px;
    }
    /* Base layout */
    html,body{height:100%}
    body{
      font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;
      background:linear-gradient(135deg,var(--bg-900),var(--bg-800),var(--bg-900));
      color:var(--text-primary);
      -webkit-font-smoothing:antialiased;
      min-height:100vh;
    }
    /* Header */
    header{
      background:linear-gradient(180deg, rgba(11,18,32,0.7), rgba(11,18,32,0.6));
      backdrop-filter:blur(8px);
      border-bottom:1px solid var(--border);
      position:sticky;top:0;z-index:40;
      box-shadow:0 8px 30px rgba(0,0,0,0.35);
    }
    .header-container{max-width:1800px;margin:0 auto;padding:12px 16px}
    .header-top{display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap}
    .header-title{display:flex;align-items:center;gap:12px}
    .header-icon{padding:6px;background:rgba(37,99,235,0.12);border-radius:var(--radius)}
    .header-icon svg{width:20px;height:20px;color:var(--primary)}
    h1{font-size:1.125rem;font-weight:700;color:var(--text-primary)}
    .header-subtitle{font-size:0.75rem;color:var(--text-secondary)}
    /* Buttons */
    button{padding:6px 12px;border-radius:var(--radius);border:1px solid var(--border);font-size:0.875rem;font-weight:500;cursor:pointer;transition:all .16s;display:inline-flex;align-items:center;gap:8px;background:transparent;color:var(--text-primary)}
    /* Filter button variants */
    .btn-filter{background:var(--surface-2);color:var(--text-secondary);border-color:var(--border)}
    .btn-filter:hover{background:var(--surface)}
    .btn-filter.active{background:rgba(37,99,235,0.14);color:var(--primary)}
    .btn-clear{background:rgba(239,68,68,0.08);color:var(--danger);border-color:rgba(239,68,68,0.12)}
    .btn-clear:hover{background:rgba(239,68,68,0.14)}
    /* Stats Grid */
    .stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-top:12px}
    .stat-card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.03));border:1px solid rgba(255,255,255,0.02);border-radius:var(--radius);padding:12px}
    .stat-label{font-size:10px;text-transform:uppercase;color:var(--text-secondary);font-weight:600;margin-bottom:6px}
    .stat-value{font-size:1.25rem;font-weight:700;color:var(--text-primary)}
    .stat-value.blue{color:var(--primary)}
    .stat-value.green{color:var(--green-400)}
    .stat-value.purple{color:var(--purple-500)}
    .stat-value.yellow{color:var(--yellow-400)}
    /* Filters */
    .filters{margin-top:12px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:12px;display:none}
    .filters.active{display:block}
    .filter-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px}
    .filter-group label{display:block;font-size:0.75rem;font-weight:600;color:var(--text-secondary);margin-bottom:6px}
    input,select{width:100%;padding:8px 12px;font-size:0.95rem;background:transparent;border:1px solid rgba(255,255,255,0.04);border-radius:var(--radius);color:var(--text-primary)}
    input::placeholder{color:var(--text-secondary)}
    input:focus,select:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 3px rgba(37,99,235,0.12)}
    .clear-filters{margin-top:8px;background:none;border:none;color:var(--primary);text-decoration:underline;font-size:0.875rem;cursor:pointer;padding:0}
    .clear-filters:hover{color:var(--primary-strong)}
    /* Main */
    main{max-width:1800px;margin:0 auto;padding:16px}
    /* People grid responsive */
    .people-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
    @media(min-width:640px){.people-grid{grid-template-columns:repeat(3,1fr)}}
    @media(min-width:768px){.people-grid{grid-template-columns:repeat(4,1fr)}}
    @media(min-width:1024px){.people-grid{grid-template-columns:repeat(5,1fr)}}
    @media(min-width:1280px){.people-grid{grid-template-columns:repeat(6,1fr)}}
    @media(min-width:1536px){.people-grid{grid-template-columns:repeat(7,1fr)}}
    /* Person card */
    .person-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:12px;transition:all .18s}
    .person-card:hover{border-color:rgba(37,99,235,0.24);box-shadow:0 10px 30px rgba(37,99,235,0.06)}
    .person-header{display:flex;align-items:center;gap:8px;margin-bottom:10px}
    .person-avatar{width:36px;height:36px;background:linear-gradient(135deg,var(--primary),var(--purple-500));border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:0.9rem;font-weight:700;color:var(--primary-contrast);flex-shrink:0}
    .person-name{font-weight:600;font-size:0.95rem;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color:var(--text-primary)}
    .person-role{font-size:0.75rem;color:var(--text-secondary)}
    /* Demands list */
    .demands-list{min-height:60px;max-height:120px;overflow-y:auto;margin-bottom:10px}
    .demands-list::-webkit-scrollbar{width:6px}
    .demands-list::-webkit-scrollbar-track{background:transparent}
    .demands-list::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.04);border-radius:6px}
    .demand-item{background:rgba(255,255,255,0.02);border-radius:6px;padding:8px;margin-bottom:6px;display:flex;align-items:center;justify-content:space-between}
    .demand-item:hover{background:rgba(255,255,255,0.03)}
    .demand-info{display:flex;align-items:center;gap:8px;min-width:0;flex:1}
    /* demand-dot agora tem borda discreta para manter contraste sobre fundos escuros */
    .demand-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0;border:1px solid var(--dot-border)}
    .demand-name{font-size:0.875rem;font-weight:500;color:var(--text-primary);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
    .demand-remove{opacity:0;padding:4px;background:none;border:none;cursor:pointer;transition:all .12s;border-radius:6px}
    .demand-item:hover .demand-remove{opacity:1}
    .demand-remove:hover{background:rgba(239,68,68,0.12)}
    .demand-remove svg{width:14px;height:14px;color:var(--danger)}
    .empty-demands{text-align:center;padding:12px;color:var(--text-secondary);font-size:0.875rem}
    /* Assign button */
    .btn-assign{width:100%;padding:8px 10px;background:rgba(37,99,235,0.08);color:var(--primary);border:1px solid rgba(37,99,235,0.12);border-radius:var(--radius);font-size:0.9rem;font-weight:600;display:flex;align-items:center;justify-content:center;gap:8px}
    .btn-assign:hover{background:rgba(37,99,235,0.14);border-color:rgba(37,99,235,0.24)}
    .btn-assign svg{width:14px;height:14px}
    /* Unassigned section */
    .unassigned-section{margin-top:16px;background:linear-gradient(180deg, rgba(250,243,205,0.03), rgba(0,0,0,0.02));border:1px solid rgba(250,205,21,0.06);border-radius:var(--radius);padding:12px}
    .unassigned-title{font-size:0.875rem;font-weight:700;color:var(--warning);display:flex;align-items:center;gap:8px;margin-bottom:8px}
    .unassigned-title svg{width:16px;height:16px}
    .unassigned-list{display:flex;flex-wrap:wrap;gap:6px}
    .unassigned-item{padding:6px 8px;background:var(--surface-2);border:1px solid var(--border);border-radius:6px;display:flex;align-items:center;gap:8px;font-size:0.9rem;color:var(--text-primary)}
    /* Modal */
    .modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.6);backdrop-filter:blur(4px);display:none;align-items:center;justify-content:center;z-index:50;padding:16px}
    .modal-overlay.active{display:flex}
    .modal{background:var(--surface);border:1px solid var(--border);border-radius:16px;padding:20px;max-width:720px;width:100%;max-height:85vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,0.5)}
    .modal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px}
    .modal-avatar{width:44px;height:44px;background:linear-gradient(135deg,var(--primary),var(--purple-500));border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1rem;font-weight:700;color:var(--primary-contrast)}
    .modal-name{font-size:1.1rem;font-weight:700;color:var(--text-primary)}
    .modal-count{font-size:0.9rem;color:var(--text-secondary)}
    .modal-close{padding:8px;background:none;border:none;cursor:pointer;border-radius:8px}
    .modal-close:hover{background:rgba(255,255,255,0.02)}
    .modal-section-title{font-size:0.95rem;font-weight:700;color:var(--text-secondary);margin-bottom:8px}
    .modal-demand-item{background:rgba(255,255,255,0.02);border-radius:8px;padding:10px;margin-bottom:8px;display:flex;align-items:center;justify-content:space-between}
    .modal-demand-dot{width:12px;height:12px;border-radius:50%;border:1px solid var(--dot-border)}
    .modal-demand-name{font-weight:600;font-size:0.95rem;color:var(--text-primary)}
    .btn-remove{padding:6px 10px;background:rgba(239,68,68,0.08);color:var(--danger);border:1px solid rgba(239,68,68,0.12);font-size:0.9rem;border-radius:8px;cursor:pointer}
    .btn-remove:hover{background:rgba(239,68,68,0.14)}
    .available-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:8px}
    .available-item{background:rgba(255,255,255,0.02);border:1px solid var(--border);border-radius:8px;padding:10px;cursor:pointer;display:flex;align-items:center;gap:10px;transition:all .14s}
    .available-item:hover:not(:disabled){background:rgba(255,255,255,0.03);border-color:rgba(37,99,235,0.12)}
    .available-item:disabled{opacity:0.5;cursor:not-allowed}
    .assigned-badge{font-size:11px;color:var(--success);font-weight:700}
    .btn-close-modal{width:100%;padding:10px 16px;background:var(--primary);color:var(--primary-contrast);border:none;border-radius:8px;font-size:0.95rem;font-weight:700;cursor:pointer;margin-top:20px}
    .btn-close-modal:hover{background:var(--primary-strong)}
    /* Toast */
    .toast{position:fixed;bottom:20px;right:20px;padding:12px 16px;background:var(--surface);border:1px solid var(--border);border-radius:8px;box-shadow:0 10px 30px rgba(0,0,0,0.5);color:var(--text-primary);font-size:0.95rem;z-index:100;animation:slideIn .3s ease;max-width:320px}
    .toast.success{background:rgba(34,197,94,0.08);border-color:rgba(34,197,94,0.12);color:var(--success)}
    .toast.warning{background:rgba(245,158,11,0.06);border-color:rgba(245,158,11,0.12);color:var(--warning)}
    @keyframes slideIn{from{transform:translateX(200px);opacity:0}to{transform:translateX(0);opacity:1}}
    /* Empty state */
    .empty-state{background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:32px;text-align:center}
    .empty-state svg{width:40px;height:40px;color:var(--text-secondary);margin:0 auto 8px}
    .empty-state p{color:var(--text-secondary);font-size:0.95rem}
    /* Color utility classes kept for JS mapping. Ensure text color contrasts when applied. */
    .bg-blue{background-color:var(--blue-500);color:var(--primary-contrast)}
    .bg-purple{background-color:var(--purple-500);color:var(--primary-contrast)}
    .bg-yellow{background-color:var(--yellow-400);color:var(--bg-900)}
    .bg-green{background-color:var(--green-400);color:var(--bg-900)}
    .bg-pink{background-color:var(--pink-500);color:var(--primary-contrast)}
    .bg-indigo{background-color:var(--indigo-500);color:var(--primary-contrast)}
    .bg-orange{background-color:var(--orange-500);color:var(--primary-contrast)}
    .bg-red{background-color:var(--red-500);color:var(--primary-contrast)}
    .bg-teal{background-color:var(--teal-500);color:var(--primary-contrast)}
    .bg-cyan{background-color:var(--cyan-500);color:var(--bg-900)}
    /* small accessibility helper: ensure SVG icons inherit color from parent */
    svg{display:block}
    /* small responsive tweaks */
    @media(max-width:420px){h1{font-size:1rem}.stat-value{font-size:1.05rem}}
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="header-container">
      <div class="header-top">
        <div class="header-title">
          <div class="header-icon" aria-hidden>
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden>
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"/>
            </svg>
          </div>
          <div>
            <h1>Sistema de Gestão</h1>
            <p class="header-subtitle">Pessoas e Demandas</p>
          </div>
        </div>
        <div class="header-actions">
          <button id="toggleFilters" class="btn-filter" aria-expanded="false">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" style="width:14px;height:14px" aria-hidden>
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z"/>
            </svg>
            Filtros
          </button>
          <button id="clearAll" class="btn-clear">Limpar Tudo</button>
        </div>
      </div>
      <!-- Statistics -->
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-label">Agentes</div>
          <div class="stat-value blue" id="statTotal">0</div>
        </div>
        <div class="stat-card">
          <div class="stat-label">Ativos</div>
          <div class="stat-value green" id="statActive">0</div>
        </div>
        <div class="stat-card">
          <div class="stat-label">Atribuições</div>
          <div class="stat-value purple" id="statAssignments">0</div>
        </div>
        <div class="stat-card">
          <div class="stat-label">Livres</div>
          <div class="stat-value yellow" id="statUnassigned">0</div>
        </div>
      </div>
      <!-- Filters -->
      <div id="filtersSection" class="filters" aria-hidden="true">
        <div class="filter-grid">
          <div class="filter-group">
            <label for="searchInput">Buscar Agente</label>
            <input type="text" id="searchInput" placeholder="Digite o nome..." aria-label="Buscar agente">
          </div>
          <div class="filter-group">
            <label for="demandFilter">Filtrar por Demanda</label>
            <select id="demandFilter" aria-label="Filtrar por demanda">
              <option value="">Todas as demandas</option>
            </select>
          </div>
        </div>
        <button id="clearFilters" class="clear-filters" style="display:none">Limpar filtros</button>
      </div>
    </div>
  </header>
  <!-- Main Content -->
  <main>
    <div id="peopleGrid" class="people-grid" aria-live="polite"></div>
    <div id="unassignedSection" class="unassigned-section" style="display:none" aria-hidden="true">
      <div class="unassigned-title">
        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden>
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
        </svg>
        Demandas Não Atribuídas (<span id="unassignedCount">0</span>)
      </div>
      <div id="unassignedList" class="unassigned-list"></div>
    </div>
  </main>

  <!-- Modal -->
  <div id="modalOverlay" class="modal-overlay" role="dialog" aria-modal="true" aria-hidden="true">
    <div class="modal" role="document">
      <div class="modal-header">
        <div class="modal-person">
          <div class="modal-avatar" id="modalAvatar"></div>
          <div>
            <div class="modal-name" id="modalName"></div>
            <div class="modal-count" id="modalCount"></div>
          </div>
        </div>
        <button class="modal-close" id="closeModal" aria-label="Fechar">
          <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden>
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
          </svg>
        </button>
      </div>
      <div id="currentAssignments" class="modal-section" style="display:none">
        <div class="modal-section-title">Demandas Atribuídas</div>
        <div id="currentList"></div>
      </div>
      <div class="modal-section">
        <div class="modal-section-title">Demandas Disponíveis</div>
        <div id="availableList" class="available-grid"></div>
      </div>
      <button class="btn-close-modal" id="closeModalBtn">Concluir</button>
    </div>
  </div>
  <script>
    /*
      Melhorias aplicadas nesta versão:
      - Removidos event handlers inline gerados via template strings.
      - Sanitização de texto antes de inserção em innerHTML (`escapeHtml`).
      - Delegação de eventos para reduzir ligação de listeners e evitar XSS indireto.
      - Gerenciamento de foco no modal (trap focus básico) e tecla Escape para fechar.
      - Correções de estabilidade e clareza no fluxo de render.
    */
    // Dados iniciais
    const INITIAL_PEOPLE = [
      { id: '1', name: 'Cristian', role: 'Agente', demands: [] },
      { id: '2', name: 'Eduardo', role: 'Agente', demands: [] },
      { id: '3', name: 'Emanuela', role: 'Agente', demands: [] },
      { id: '4', name: 'Emilly', role: 'Agente', demands: [] },
      { id: '5', name: 'Felipe', role: 'Agente', demands: [] },
      { id: '6', name: 'João', role: 'Agente', demands: [] },
      { id: '7', name: 'Kaua', role: 'Agente', demands: [] },
      { id: '8', name: 'Kauane', role: 'Agente', demands: [] },
      { id: '9', name: 'Luiz', role: 'Agente', demands: [] },
      { id: '10', name: 'Pamela', role: 'Agente', demands: [] },
      { id: '11', name: 'Patrick', role: 'Agente', demands: [] },
      { id: '12', name: 'Pedro', role: 'Agente', demands: [] },
      { id: '13', name: 'Richard', role: 'Agente', demands: [] },
      { id: '14', name: 'Thais', role: 'Agente', demands: [] },
      { id: '15', name: 'Vitória', role: 'Agente', demands: [] }
    ];
    const DEMANDS = [
      { id: 'nivel2', name: 'Nível II', color: 'bg-blue' },
      { id: 'matrix', name: 'Matrix', color: 'bg-purple' },
      { id: 'vip', name: 'Tratamento VIP', color: 'bg-yellow' },
      { id: 'voz', name: 'Voz', color: 'bg-green' },
      { id: 'emails', name: 'Emails', color: 'bg-pink' },
      { id: 'helpdesk', name: 'Help Desk', color: 'bg-indigo' },
      { id: 'batimento', name: 'Batimento', color: 'bg-orange' },
      { id: 'massivas', name: 'Massivas', color: 'bg-red' },
      { id: 'reincidentes', name: 'Análises Reincidentes', color: 'bg-teal' },
      { id: 'cancelamentos', name: 'Análises Cancelamentos', color: 'bg-cyan' }
    ];
    let people = [];
    let people = [];
    let selectedPerson = null;
    let searchTerm = '';
    let filterDemand = '';
    const STORAGE_KEY = 'people_demands_v1';
    function loadFromStorage(){
      try{const stored = localStorage.getItem(STORAGE_KEY);return stored?JSON.parse(stored):JSON.parse(JSON.stringify(INITIAL_PEOPLE))}catch{return JSON.parse(JSON.stringify(INITIAL_PEOPLE))}
    }
    function saveToStorage(){try{localStorage.setItem(STORAGE_KEY,JSON.stringify(people))}catch(e){console.error('Storage error',e)}}
    function showToast(message,type='success'){
      const toast=document.createElement('div');toast.className=`toast ${type}`;toast.textContent=message;document.body.appendChild(toast);
      setTimeout(()=>{toast.style.animation='slideIn .3s ease reverse';setTimeout(()=>toast.remove(),300)},2500);
    }
    function escapeHtml(str){
      return String(str)
        .replace(/&/g,'&amp;')
        .replace(/</g,'&lt;')
        .replace(/>/g,'&gt;')
        .replace(/"/g,'&quot;')
        .replace(/'/g,'&#39;');
    }
    function assignDemand(personId,demandId){
      const person=people.find(p=>p.id===personId);if(!person)return; if(person.demands.includes(demandId)){showToast('Demanda já atribuída a este agente','warning');return}
      person.demands.push(demandId);saveToStorage();render();showToast(`Demanda atribuída a ${person.name}`);
    }
    function removeDemand(personId,demandId){
      const person=people.find(p=>p.id===personId);if(!person)return;const demand=DEMANDS.find(d=>d.id===demandId);person.demands=person.demands.filter(d=>d!==demandId);saveToStorage();render();showToast(`${demand.name} removida de ${person.name}`);
    }
    function clearAllAssignments(){if(!confirm('Deseja realmente limpar todas as atribuições?'))return;people.forEach(p=>p.demands=[]);saveToStorage();render();showToast('Todas as atribuições foram limpas')}
    function getStatistics(){const total=people.length;const active=people.filter(p=>p.demands.length>0).length;const assignments=people.reduce((s,p)=>s+p.demands.length,0);const unassigned=DEMANDS.filter(d=>!people.some(p=>p.demands.includes(d.id)));return{total,active,assignments,unassigned}}
    function getFilteredPeople(){return people.filter(person=>{const matchesSearch=person.name.toLowerCase().includes(searchTerm.toLowerCase());const matchesDemand=filterDemand?person.demands.includes(filterDemand):true;return matchesSearch&&matchesDemand})}
    function renderPeopleGrid(){
      const grid=document.getElementById('peopleGrid');const filtered=getFilteredPeople();
      if(filtered.length===0){grid.innerHTML=`<div class="empty-state" style="grid-column:1/-1;"><svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"/></svg><p>Nenhum agente encontrado</p></div>`;return}
      grid.innerHTML=filtered.map(person=>{
        const nameEsc = escapeHtml(person.name);
        const roleEsc = escapeHtml(person.role);
        const avatar = escapeHtml(person.name.charAt(0));
        return `
        <div class="person-card" data-person-id="${person.id}">
          <div class="person-header">
            <div class="person-avatar">${avatar}</div>
            <div class="person-info">
              <div class="person-name">${nameEsc}</div>
              <div class="person-role">${roleEsc}</div>
            </div>
          </div>
          <div class="demands-list">
            ${person.demands.length===0?'<div class="empty-demands">Sem demandas</div>':person.demands.map(demandId=>{const demand=DEMANDS.find(d=>d.id===demandId);if(!demand)return'';const dName=escapeHtml(demand.name);return `
                  <div class="demand-item" data-person-id="${person.id}" data-demand-id="${demand.id}">
                    <div class="demand-info">
                      <div class="demand-dot ${demand.color}" aria-hidden></div>
                      <span class="demand-name">${dName}</span>
                    </div>
                    <button class="demand-remove" type="button" data-action="remove-demand" data-person="${person.id}" data-demand="${demand.id}" aria-label="Remover ${dName}">
                      <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
                    </button>
                  </div>
                `}).join('')}
          </div>
          <button class="btn-assign" type="button" data-action="open-modal" data-person="${person.id}">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
            Atribuir
          </button>
        </div>
      `}).join('')
    }
    function renderStatistics(){
      const stats=getStatistics();document.getElementById('statTotal').textContent=stats.total;document.getElementById('statActive').textContent=stats.active;document.getElementById('statAssignments').textContent=stats.assignments;document.getElementById('statUnassigned').textContent=stats.unassigned.length;
      const section=document.getElementById('unassignedSection');
      if(stats.unassigned.length>0){section.style.display='block';document.getElementById('unassignedCount').textContent=stats.unassigned.length;document.getElementById('unassignedList').innerHTML=stats.unassigned.map(d=>`<div class="unassigned-item"><div class="demand-dot ${d.color}" aria-hidden></div><span>${escapeHtml(d.name)}</span></div>`).join('')}else{section.style.display='none'}
    }
    function renderDemandFilter(){const select=document.getElementById('demandFilter');select.innerHTML='<option value="">Todas as demandas</option>'+DEMANDS.map(d=>`<option value="${d.id}">${escapeHtml(d.name)}</option>`).join('')}
    function render(){renderPeopleGrid();renderStatistics()}
    // Modal focus management
    let lastFocused = null;
    function openModal(personId){
      selectedPerson = people.find(p=>p.id===personId);if(!selectedPerson)return;
      document.getElementById('modalAvatar').textContent = escapeHtml(selectedPerson.name.charAt(0));
      document.getElementById('modalName').textContent = escapeHtml(selectedPerson.name);
      document.getElementById('modalCount').textContent = `${selectedPerson.demands.length} demanda(s) atribuída(s)`;
      const currentSection = document.getElementById('currentAssignments');
      if(selectedPerson.demands.length>0){
        currentSection.style.display='block';
        document.getElementById('currentList').innerHTML = selectedPerson.demands.map(demandId=>{const demand=DEMANDS.find(d=>d.id===demandId);if(!demand)return'';const dn=escapeHtml(demand.name);return `
            <div class="modal-demand-item" data-demand-id="${demand.id}">
              <div class="modal-demand-info">
                <div class="modal-demand-dot ${demand.color}" aria-hidden></div>
                <span class="modal-demand-name">${dn}</span>
              </div>
              <button class="btn-remove" type="button" data-action="remove-demand" data-person="${selectedPerson.id}" data-demand="${demand.id}">Remover</button>
            </div>
          `}).join('')
      } else {
        currentSection.style.display='none';
        document.getElementById('currentList').innerHTML='';
      }
      document.getElementById('availableList').innerHTML = DEMANDS.map(demand=>{const isAssigned=selectedPerson.demands.includes(demand.id);const dn=escapeHtml(demand.name);return `
        <button class="available-item" type="button" ${isAssigned?'disabled':''} data-action="assign-demand" data-person="${selectedPerson.id}" data-demand="${demand.id}">
          <div class="modal-demand-dot ${demand.color}" aria-hidden></div>
          <span class="modal-demand-name">${dn}</span>
          ${isAssigned?'<span class="assigned-badge">✓ Atribuída</span>':''}
        </button>
      `}).join('');
      const overlay = document.getElementById('modalOverlay');overlay.classList.add('active');overlay.setAttribute('aria-hidden','false');
      lastFocused = document.activeElement;
      const focusable = overlay.querySelector('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
      if(focusable) focusable.focus();
      document.addEventListener('keydown', handleModalKeydown);
    }
    function closeModal(){
      const overlay=document.getElementById('modalOverlay');overlay.classList.remove('active');overlay.setAttribute('aria-hidden','true');selectedPerson=null;document.removeEventListener('keydown', handleModalKeydown);
      if(lastFocused && typeof lastFocused.focus === 'function') lastFocused.focus();
    }
    function handleModalKeydown(e){
      if(e.key === 'Escape') { closeModal(); return }
      if(e.key === 'Tab') {
        const overlay = document.getElementById('modalOverlay');
        const focusable = Array.from(overlay.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])')).filter(el=>!el.disabled);
        if(focusable.length===0) { e.preventDefault(); return }
        const idx = focusable.indexOf(document.activeElement);
        if(e.shiftKey){
          if(idx === 0){ focusable[focusable.length-1].focus(); e.preventDefault(); }
        } else {
          if(idx === focusable.length-1){ focusable[0].focus(); e.preventDefault(); }
        }
      }
    }
    // Event delegation for dynamic elements
    document.addEventListener('click', function(e){
      const removeBtn = e.target.closest('[data-action="remove-demand"]');
      if(removeBtn){
        const personId = removeBtn.dataset.person; const demandId = removeBtn.dataset.demand; removeDemand(personId,demandId); return;
      }
      const openBtn = e.target.closest('[data-action="open-modal"]');
      if(openBtn){ openModal(openBtn.dataset.person); return; }
      const assignBtn = e.target.closest('[data-action="assign-demand"]');
      if(assignBtn){ const personId = assignBtn.dataset.person; const demandId = assignBtn.dataset.demand; assignDemand(personId,demandId); return; }
    });
    // Other listeners (static elements)
    const toggleFiltersBtn = document.getElementById('toggleFilters');
    toggleFiltersBtn.addEventListener('click', function(){
      const filters = document.getElementById('filtersSection');
      const isActive = filters.classList.toggle('active');
      this.classList.toggle('active', isActive);
      this.setAttribute('aria-expanded', String(isActive));
      filters.setAttribute('aria-hidden', String(!isActive));
    });
    document.getElementById('clearAll').addEventListener('click', clearAllAssignments);
    document.getElementById('searchInput').addEventListener('input', function(e){ searchTerm = e.target.value; render(); updateClearFiltersButton(); });
    document.getElementById('demandFilter').addEventListener('change', function(e){ filterDemand = e.target.value; render(); updateClearFiltersButton(); });
    document.getElementById('clearFilters').addEventListener('click', function(){ searchTerm=''; filterDemand=''; document.getElementById('searchInput').value=''; document.getElementById('demandFilter').value=''; render(); updateClearFiltersButton(); });
    document.getElementById('closeModal').addEventListener('click', closeModal);
    document.getElementById('closeModalBtn').addEventListener('click', closeModal);
    document.getElementById('modalOverlay').addEventListener('click', function(e){ if(e.target === this) closeModal(); });
    function updateClearFiltersButton(){ const btn=document.getElementById('clearFilters'); btn.style.display=(searchTerm||filterDemand)?'block':'none' }
    // Inicialização
    people = loadFromStorage(); renderDemandFilter(); render();
  </script>
