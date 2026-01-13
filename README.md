<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Sistema de Gestão de Pessoas e Demandas">
  <title>Sistema de Gestão - Pessoas e Demandas</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    :root {
      --slate-950: #020617;
      --slate-900: #0f172a;
      --slate-800: #1e293b;
      --slate-700: #334155;
      --slate-600: #475569;
      --slate-500: #64748b;
      --slate-400: #94a3b8;
      --slate-100: #f1f5f9;
      --blue-600: #2563eb;
      --blue-500: #3b82f6;
      --blue-400: #60a5fa;
      --purple-600: #9333ea;
      --purple-500: #a855f7;
      --green-400: #4ade80;
      --yellow-400: #facc15;
      --yellow-600: #ca8a04;
      --red-600: #dc2626;
      --red-400: #f87171;
      --red-500: #ef4444;
      --pink-500: #ec4899;
      --indigo-500: #6366f1;
      --orange-500: #f97316;
      --teal-500: #14b8a6;
      --cyan-500: #06b6d4;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
      background: linear-gradient(135deg, var(--slate-950), var(--slate-900), var(--slate-950));
      color: var(--slate-100);
      min-height: 100vh;
      -webkit-font-smoothing: antialiased;
    }
    /* Header Styles */
    header {
      background: rgba(15, 23, 42, 0.8);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--slate-800);
      position: sticky;
      top: 0;
      z-index: 40;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
    }
    .header-container {
      max-width: 1800px;
      margin: 0 auto;
      padding: 12px 16px;
    }
    .header-top {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
      flex-wrap: wrap;
    }
    .header-title {
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .header-icon {
      padding: 6px;
      background: rgba(37, 99, 235, 0.2);
      border-radius: 8px;
    }
    .header-icon svg {
      width: 20px;
      height: 20px;
      color: var(--blue-400);
    }
    h1 {
      font-size: 1.125rem;
      font-weight: 700;
    }
    .header-subtitle {
      font-size: 0.75rem;
      color: var(--slate-500);
    }
    .header-actions {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    button {
      padding: 6px 12px;
      border-radius: 8px;
      border: 1px solid;
      font-size: 0.75rem;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.2s;
      display: inline-flex;
      align-items: center;
      gap: 8px;
    }
    .btn-filter {
      background: var(--slate-800);
      color: var(--slate-400);
      border-color: var(--slate-700);
    }
    .btn-filter:hover {
      background: var(--slate-700);
    }
    .btn-filter.active {
      background: rgba(37, 99, 235, 0.2);
      color: var(--blue-400);
      border-color: rgba(37, 99, 235, 0.3);
    }
    .btn-clear {
      background: rgba(220, 38, 38, 0.1);
      color: var(--red-400);
      border-color: rgba(220, 38, 38, 0.2);
    }
    .btn-clear:hover {
      background: rgba(220, 38, 38, 0.2);
    }
    /* Statistics Grid */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 8px;
      margin-top: 12px;
    }
    .stat-card {
      background: rgba(30, 41, 59, 0.4);
      border: 1px solid rgba(51, 65, 85, 0.5);
      border-radius: 8px;
      padding: 8px;
    }
    .stat-label {
      font-size: 10px;
      text-transform: uppercase;
      color: var(--slate-500);
      font-weight: 500;
      margin-bottom: 2px;
    }
    .stat-value {
      font-size: 1.25rem;
      font-weight: 700;
    }
    .stat-value.blue { color: var(--blue-400); }
    .stat-value.green { color: var(--green-400); }
    .stat-value.purple { color: var(--purple-500); }
    .stat-value.yellow { color: var(--yellow-400); }
    /* Filter Section */
    .filters {
      margin-top: 12px;
      background: rgba(30, 41, 59, 0.4);
      border: 1px solid rgba(51, 65, 85, 0.5);
      border-radius: 8px;
      padding: 12px;
      display: none;
    }
    .filters.active {
      display: block;
    }
    .filter-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 12px;
    }
    .filter-group label {
      display: block;
      font-size: 0.75rem;
      font-weight: 500;
      color: var(--slate-400);
      margin-bottom: 6px;
    }
    input, select {
      width: 100%;
      padding: 6px 12px;
      font-size: 0.875rem;
      background: rgba(15, 23, 42, 0.5);
      border: 1px solid var(--slate-600);
      border-radius: 8px;
      color: var(--slate-100);
      transition: all 0.2s;
    }
    input:focus, select:focus {
      outline: none;
      border-color: var(--blue-500);
      box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.2);
    }
    .clear-filters {
      margin-top: 8px;
      background: none;
      border: none;
      color: var(--blue-400);
      text-decoration: underline;
      font-size: 0.75rem;
      cursor: pointer;
      padding: 0;
    }
    .clear-filters:hover {
      color: var(--blue-500);
    }
    /* Main Container */
    main {
      max-width: 1800px;
      margin: 0 auto;
      padding: 16px;
    }
    /* People Grid */
    .people-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
    }
    @media (min-width: 640px) {
      .people-grid { grid-template-columns: repeat(3, 1fr); }
    }
    @media (min-width: 768px) {
      .people-grid { grid-template-columns: repeat(4, 1fr); }
    }
    @media (min-width: 1024px) {
      .people-grid { grid-template-columns: repeat(5, 1fr); }
    }
    @media (min-width: 1280px) {
      .people-grid { grid-template-columns: repeat(6, 1fr); }
    }
    @media (min-width: 1536px) {
      .people-grid { grid-template-columns: repeat(7, 1fr); }
    }
    /* Person Card */
    .person-card {
      background: rgba(15, 23, 42, 0.6);
      backdrop-filter: blur(4px);
      border: 1px solid var(--slate-800);
      border-radius: 12px;
      padding: 12px;
      transition: all 0.2s;
    }
    .person-card:hover {
      border-color: rgba(37, 99, 235, 0.5);
      box-shadow: 0 8px 24px rgba(37, 99, 235, 0.1);
    }
    .person-header {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 10px;
    }
    .person-avatar {
      width: 32px;
      height: 32px;
      background: linear-gradient(135deg, var(--blue-600), var(--purple-600));
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.875rem;
      font-weight: 700;
      flex-shrink: 0;
    }
    .person-info {
      min-width: 0;
      flex: 1;
    }
    .person-name {
      font-weight: 600;
      font-size: 0.875rem;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .person-role {
      font-size: 10px;
      color: var(--slate-500);
    }
    /* Demands List */
    .demands-list {
      min-height: 60px;
      max-height: 120px;
      overflow-y: auto;
      margin-bottom: 10px;
    }
    .demands-list::-webkit-scrollbar {
      width: 4px;
    }
    .demands-list::-webkit-scrollbar-track {
      background: var(--slate-900);
      border-radius: 2px;
    }
    .demands-list::-webkit-scrollbar-thumb {
      background: var(--slate-700);
      border-radius: 2px;
    }
    .demand-item {
      background: rgba(2, 6, 23, 0.5);
      border-radius: 6px;
      padding: 6px;
      margin-bottom: 4px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      transition: all 0.2s;
    }
    .demand-item:hover {
      background: rgba(2, 6, 23, 0.7);
    }
    .demand-info {
      display: flex;
      align-items: center;
      gap: 6px;
      min-width: 0;
      flex: 1;
    }
    .demand-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      flex-shrink: 0;
    }
    .demand-name {
      font-size: 0.75rem;
      font-weight: 500;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .demand-remove {
      opacity: 0;
      padding: 2px;
      background: none;
      border: none;
      cursor: pointer;
      transition: all 0.2s;
      border-radius: 4px;
      flex-shrink: 0;
    }
    .demand-item:hover .demand-remove {
      opacity: 1;
    }
    .demand-remove:hover {
      background: rgba(239, 68, 68, 0.2);
    }
    .demand-remove svg {
      width: 12px;
      height: 12px;
      color: var(--red-400);
    }
    .empty-demands {
      text-align: center;
      padding: 12px;
      color: var(--slate-600);
      font-size: 0.75rem;
    }
    /* Assign Button */
    .btn-assign {
      width: 100%;
      padding: 6px 8px;
      background: rgba(37, 99, 235, 0.1);
      color: var(--blue-400);
      border: 1px solid rgba(37, 99, 235, 0.2);
      border-radius: 8px;
      font-size: 0.75rem;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }
    .btn-assign:hover {
      background: rgba(37, 99, 235, 0.2);
      border-color: rgba(37, 99, 235, 0.4);
    }
    .btn-assign svg {
      width: 12px;
      height: 12px;
    }
    /* Unassigned Section */
    .unassigned-section {
      margin-top: 16px;
      background: rgba(202, 138, 4, 0.05);
      border: 1px solid rgba(202, 138, 4, 0.2);
      border-radius: 8px;
      padding: 12px;
    }
    .unassigned-title {
      font-size: 0.75rem;
      font-weight: 600;
      color: var(--yellow-400);
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .unassigned-title svg {
      width: 14px;
      height: 14px;
    }
    .unassigned-list {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }
    .unassigned-item {
      padding: 4px 8px;
      background: rgba(15, 23, 42, 0.5);
      border: 1px solid var(--slate-700);
      border-radius: 6px;
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 0.75rem;
    }
    /* Modal */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(4px);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 50;
      padding: 16px;
    }
    .modal-overlay.active {
      display: flex;
    }
    .modal {
      background: var(--slate-900);
      border: 1px solid var(--slate-700);
      border-radius: 16px;
      padding: 20px;
      max-width: 600px;
      width: 100%;
      max-height: 85vh;
      overflow-y: auto;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
    }
    .modal-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
    }
    .modal-person {
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .modal-avatar {
      width: 40px;
      height: 40px;
      background: linear-gradient(135deg, var(--blue-600), var(--purple-600));
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1rem;
      font-weight: 700;
    }
    .modal-name {
      font-size: 1.25rem;
      font-weight: 700;
    }
    .modal-count {
      font-size: 0.75rem;
      color: var(--slate-500);
    }
    .modal-close {
      padding: 8px;
      background: none;
      border: none;
      cursor: pointer;
      border-radius: 8px;
      transition: all 0.2s;
    }
    .modal-close:hover {
      background: var(--slate-800);
    }
    .modal-close svg {
      width: 20px;
      height: 20px;
    }
    .modal-section {
      margin-bottom: 20px;
    }
    .modal-section-title {
      font-size: 0.875rem;
      font-weight: 600;
      color: var(--slate-400);
      margin-bottom: 8px;
    }
    .modal-demand-item {
      background: rgba(2, 6, 23, 0.5);
      border-radius: 8px;
      padding: 10px;
      margin-bottom: 6px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .modal-demand-info {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .modal-demand-dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
    }
    .modal-demand-name {
      font-weight: 500;
      font-size: 0.875rem;
    }
    .btn-remove {
      padding: 4px 10px;
      background: rgba(220, 38, 38, 0.1);
      color: var(--red-400);
      border: 1px solid rgba(220, 38, 38, 0.2);
      font-size: 0.75rem;
      border-radius: 6px;
      cursor: pointer;
      transition: all 0.2s;
    }
    .btn-remove:hover {
      background: rgba(220, 38, 38, 0.2);
    }
    .available-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 8px;
    }
    .available-item {
      background: rgba(2, 6, 23, 0.5);
      border: 1px solid var(--slate-800);
      border-radius: 8px;
      padding: 10px;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      align-items: center;
      gap: 10px;
      text-align: left;
    }
    .available-item:hover:not(:disabled) {
      background: rgba(2, 6, 23, 0.7);
      border-color: rgba(37, 99, 235, 0.5);
    }
    .available-item:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
    .available-item .modal-demand-name {
      flex: 1;
    }
    .assigned-badge {
      font-size: 10px;
      color: var(--green-400);
      font-weight: 600;
    }
    .btn-close-modal {
      width: 100%;
      padding: 10px 16px;
      background: var(--blue-600);
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 0.875rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
      margin-top: 20px;
    }
    .btn-close-modal:hover {
      background: var(--blue-500);
    }
    /* Toast Notification */
    .toast {
      position: fixed;
      bottom: 20px;
      right: 20px;
      padding: 12px 16px;
      background: var(--slate-800);
      border: 1px solid var(--slate-700);
      border-radius: 8px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
      color: white;
      font-size: 0.875rem;
      z-index: 100;
      animation: slideIn 0.3s ease;
      max-width: 300px;
    }
    .toast.success {
      background: rgba(16, 185, 129, 0.1);
      border-color: rgba(16, 185, 129, 0.3);
      color: var(--green-400);
    }
    .toast.warning {
      background: rgba(245, 158, 11, 0.1);
      border-color: rgba(245, 158, 11, 0.3);
      color: var(--yellow-400);
    }
    @keyframes slideIn {
      from {
        transform: translateX(400px);
        opacity: 0;
      }
      to {
        transform: translateX(0);
        opacity: 1;
      }
    }
    /* Empty State */
    .empty-state {
      background: rgba(15, 23, 42, 0.5);
      border: 1px solid var(--slate-800);
      border-radius: 8px;
      padding: 32px;
      text-align: center;
    }
    .empty-state svg {
      width: 40px;
      height: 40px;
      color: var(--slate-700);
      margin: 0 auto 8px;
    }
    .empty-state p {
      color: var(--slate-500);
      font-size: 0.875rem;
    }
    /* Color Classes */
    .bg-blue { background-color: var(--blue-500); }
    .bg-purple { background-color: var(--purple-500); }
    .bg-yellow { background-color: var(--yellow-400); }
    .bg-green { background-color: #22c55e; }
    .bg-pink { background-color: var(--pink-500); }
    .bg-indigo { background-color: var(--indigo-500); }
    .bg-orange { background-color: var(--orange-500); }
    .bg-red { background-color: var(--red-500); }
    .bg-teal { background-color: var(--teal-500); }
    .bg-cyan { background-color: var(--cyan-500); }
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="header-container">
      <div class="header-top">
        <div class="header-title">
          <div class="header-icon">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" />
            </svg>
          </div>
          <div>
            <h1>Sistema de Gestão</h1>
            <p class="header-subtitle">Pessoas e Demandas</p>
          </div>
        </div>
        <div class="header-actions">
          <button id="toggleFilters" class="btn-filter">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" style="width:14px;height:14px">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z" />
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
      <div id="filtersSection" class="filters">
        <div class="filter-grid">
          <div class="filter-group">
            <label for="searchInput">Buscar Agente</label>
            <input type="text" id="searchInput" placeholder="Digite o nome...">
          </div>
          <div class="filter-group">
            <label for="demandFilter">Filtrar por Demanda</label>
            <select id="demandFilter">
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
    <div id="peopleGrid" class="people-grid"></div>
    <div id="unassignedSection" class="unassigned-section" style="display:none">
      <div class="unassigned-title">
        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
        </svg>
        Demandas Não Atribuídas (<span id="unassignedCount">0</span>)
      </div>
      <div id="unassignedList" class="unassigned-list"></div>
    </div>
  </main>

  <!-- Modal -->
  <div id="modalOverlay" class="modal-overlay">
    <div class="modal">
      <div class="modal-header">
        <div class="modal-person">
          <div class="modal-avatar" id="modalAvatar"></div>
          <div>
            <div class="modal-name" id="modalName"></div>
            <div class="modal-count" id="modalCount"></div>
          </div>
        </div>
        <button class="modal-close" id="closeModal">
          <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
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
    // 🎯 Data Configuration
    const INITIAL_PEOPLE = [
      { id: '1', name: 'Cristian', role: 'Agente', demands: [] },
      { id: '2', name: 'Eduardo', role: 'Agente', demands: [] },
      { id: '3', name: 'Emanuela', role: 'Agente', demands: [] },
      { id: '4', name: 'Emilly', role: 'Agente', demands: [] },
      { id: '5', name: 'Felipe', role: 'Agente', demands: [] },
      { id: '6', name: 'Cristian', role: 'Agente', demands: [] },
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
    // 🔄 State Management
    let people = [];
    let selectedPerson = null;
    let searchTerm = '';
    let filterDemand = '';
    // 💾 Storage
    const STORAGE_KEY = 'people_demands_v1';
    function loadFromStorage() {
      try {
        const stored = localStorage.getItem(STORAGE_KEY);
        return stored ? JSON.parse(stored) : INITIAL_PEOPLE;
      } catch {
        return INITIAL_PEOPLE;
      }
    }
    function saveToStorage() {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(people));
      } catch (error) {
        console.error('Storage error:', error);
      }
    }
    // 🎨 Toast Notifications
    function showToast(message, type = 'success') {
      const toast = document.createElement('div');
      toast.className = `toast ${type}`;
      toast.textContent = message;
      document.body.appendChild(toast);
      setTimeout(() => {
        toast.style.animation = 'slideIn 0.3s ease reverse';
        setTimeout(() => toast.remove(), 300);
      }, 2500);
    }
    // 🎯 Assignment Logic
    function assignDemand(personId, demandId) {
      const person = people.find(p => p.id === personId);
      if (!person) return;
      if (person.demands.includes(demandId)) {
        showToast('Demanda já atribuída a este agente', 'warning');
        return;
      }
      person.demands.push(demandId);
      saveToStorage();
      render();
      showToast(`Demanda atribuída a ${person.name}`);
    }
    function removeDemand(personId, demandId) {
      const person = people.find(p => p.id === personId);
      if (!person) return;
      const demand = DEMANDS.find(d => d.id === demandId);
      person.demands = person.demands.filter(d => d !== demandId);
      saveToStorage();
      render();
      showToast(`${demand.name} removida de ${person.name}`);
    }
    function clearAllAssignments() {
      if (!confirm('Deseja realmente limpar todas as atribuições?')) return;
      people.forEach(person => person.demands = []);
      saveToStorage();
      render();
      showToast('Todas as atribuições foram limpas');
    }
    // 📊 Statistics
    function getStatistics() {
      const total = people.length;
      const active = people.filter(p => p.demands.length > 0).length;
      const assignments = people.reduce((sum, p) => sum + p.demands.length, 0);
      const unassigned = DEMANDS.filter(d => !people.some(p => p.demands.includes(d.id)));
      return { total, active, assignments, unassigned };
    }
    // 🔍 Filtering
    function getFilteredPeople() {
      return people.filter(person => {
        const matchesSearch = person.name.toLowerCase().includes(searchTerm.toLowerCase());
        const matchesDemand = filterDemand ? person.demands.includes(filterDemand) : true;
        return matchesSearch && matchesDemand;
      });
    }
    // 🎨 Render Functions
    function renderPeopleGrid() {
      const grid = document.getElementById('peopleGrid');
      const filtered = getFilteredPeople();
      if (filtered.length === 0) {
        grid.innerHTML = `
          <div class="empty-state" style="grid-column: 1 / -1;">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" />
            </svg>
            <p>Nenhum agente encontrado</p>
          </div>
        `;
        return;
      }
      grid.innerHTML = filtered.map(person => `
        <div class="person-card">
          <div class="person-header">
            <div class="person-avatar">${person.name.charAt(0)}</div>
            <div class="person-info">
              <div class="person-name">${person.name}</div>
              <div class="person-role">${person.role}</div>
            </div>
          </div>
          <div class="demands-list">
            ${person.demands.length === 0 ? 
              '<div class="empty-demands">Sem demandas</div>' :
              person.demands.map(demandId => {
                const demand = DEMANDS.find(d => d.id === demandId);
                if (!demand) return '';
                return `
                  <div class="demand-item">
                    <div class="demand-info">
                      <div class="demand-dot ${demand.color}"></div>
                      <span class="demand-name">${demand.name}</span>
                    </div>
                    <button class="demand-remove" onclick="removeDemand('${person.id}', '${demandId}')">
                      <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                      </svg>
                    </button>
                  </div>
                `;
              }).join('')
            }
          </div>
          <button class="btn-assign" onclick="openModal('${person.id}')">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
            </svg>
            Atribuir
          </button>
        </div>
      `).join('');
    }
    function renderStatistics() {
      const stats = getStatistics();
      document.getElementById('statTotal').textContent = stats.total;
      document.getElementById('statActive').textContent = stats.active;
      document.getElementById('statAssignments').textContent = stats.assignments;
      document.getElementById('statUnassigned').textContent = stats.unassigned.length;
      // Unassigned demands section
      const section = document.getElementById('unassignedSection');
      if (stats.unassigned.length > 0) {
        section.style.display = 'block';
        document.getElementById('unassignedCount').textContent = stats.unassigned.length;
        document.getElementById('unassignedList').innerHTML = stats.unassigned.map(demand => `
          <div class="unassigned-item">
            <div class="demand-dot ${demand.color}"></div>
            <span>${demand.name}</span>
          </div>
        `).join('');
      } else {
        section.style.display = 'none';
      }
    }
    function renderDemandFilter() {
      const select = document.getElementById('demandFilter');
      select.innerHTML = '<option value="">Todas as demandas</option>' +
        DEMANDS.map(d => `<option value="${d.id}">${d.name}</option>`).join('');
    }
    function render() {
      renderPeopleGrid();
      renderStatistics();
    }
    // 🎯 Modal Functions
    function openModal(personId) {
      selectedPerson = people.find(p => p.id === personId);
      if (!selectedPerson) return;
      document.getElementById('modalAvatar').textContent = selectedPerson.name.charAt(0);
      document.getElementById('modalName').textContent = selectedPerson.name;
      document.getElementById('modalCount').textContent = 
        `${selectedPerson.demands.length} demanda(s) atribuída(s)`;
      // Current assignments
      const currentSection = document.getElementById('currentAssignments');
      if (selectedPerson.demands.length > 0) {
        currentSection.style.display = 'block';
        document.getElementById('currentList').innerHTML = selectedPerson.demands.map(demandId => {
          const demand = DEMANDS.find(d => d.id === demandId);
          if (!demand) return '';
          return `
            <div class="modal-demand-item">
              <div class="modal-demand-info">
                <div class="modal-demand-dot ${demand.color}"></div>
                <span class="modal-demand-name">${demand.name}</span>
              </div>
              <button class="btn-remove" onclick="removeDemand('${selectedPerson.id}', '${demandId}'); closeModal();">
                Remover
              </button>
            </div>
          `;
        }).join('');
      } else {
        currentSection.style.display = 'none';
      }
      // Available demands
      document.getElementById('availableList').innerHTML = DEMANDS.map(demand => {
        const isAssigned = selectedPerson.demands.includes(demand.id);
        return `
          <button 
            class="available-item" 
            ${isAssigned ? 'disabled' : ''}
            onclick="${isAssigned ? '' : `assignDemand('${selectedPerson.id}', '${demand.id}')`}"
          >
            <div class="modal-demand-dot ${demand.color}"></div>
            <span class="modal-demand-name">${demand.name}</span>
            ${isAssigned ? '<span class="assigned-badge">✓ Atribuída</span>' : ''}
          </button>
        `;
      }).join('');
      document.getElementById('modalOverlay').classList.add('active');
    }
    function closeModal() {
      document.getElementById('modalOverlay').classList.remove('active');
      selectedPerson = null;
    }
    // 🎮 Event Listeners
    document.getElementById('toggleFilters').addEventListener('click', function() {
      const filters = document.getElementById('filtersSection');
      const isActive = filters.classList.toggle('active');
      this.classList.toggle('active', isActive);
    });
    document.getElementById('clearAll').addEventListener('click', clearAllAssignments);
    document.getElementById('searchInput').addEventListener('input', function(e) {
      searchTerm = e.target.value;
      render();
      updateClearFiltersButton();
    });
    document.getElementById('demandFilter').addEventListener('change', function(e) {
      filterDemand = e.target.value;
      render();
      updateClearFiltersButton();
    });
    document.getElementById('clearFilters').addEventListener('click', function() {
      searchTerm = '';
      filterDemand = '';
      document.getElementById('searchInput').value = '';
      document.getElementById('demandFilter').value = '';
      render();
      updateClearFiltersButton();
    });
    document.getElementById('closeModal').addEventListener('click', closeModal);
    document.getElementById('closeModalBtn').addEventListener('click', closeModal);
    document.getElementById('modalOverlay').addEventListener('click', function(e) {
      if (e.target === this) closeModal();
    });
    function updateClearFiltersButton() {
      const btn = document.getElementById('clearFilters');
      btn.style.display = (searchTerm || filterDemand) ? 'block' : 'none';
    }
    // 🚀 Initialize
    people = loadFromStorage();
    renderDemandFilter();
    render();
  </script>
</body>
</html>
