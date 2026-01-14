<html lang="pt-BR">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta
      name="description"
      content="Sistema de Gestão de Pessoas e Demandas - Corporativo"
    />
    <title>Sistema de Gestão - Pessoas e Demandas</title>
    <style>
      /* ==============================================
         RESET E VARIÁVEIS
         ============================================== */
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }
      :root {
        /* Cores - Tema Escuro (padrão) */
        --bg-900: #020617;
        --bg-800: #0b1220;
        --surface: #0f172a;
        --surface-2: #1e293b;
        --text-primary: #e6eef8;
        --text-secondary: #9aa6b3;
        --border: #22303f;
        --primary: #2563eb;
        --primary-strong: #1e40af;
        --success: #16a34a;
        --warning: #f59e0b;
        --danger: #ef4444;
        --radius: 8px;
        /* Cores de demandas */
        --color-blue: #2563eb;
        --color-purple: #a855f7;
        --color-yellow: #facc15;
        --color-green: #22c55e;
        --color-pink: #ec4899;
        --color-indigo: #6366f1;
        --color-orange: #f97316;
        --color-red: #ef4444;
        --color-teal: #14b8a6;
        --color-cyan: #06b6d4;
      }
      /* Tema claro */
      html.light-mode {
        --bg-900: #f8fafc;
        --bg-800: #f1f5f9;
        --surface: #ffffff;
        --surface-2: #e2e8f0;
        --text-primary: #1e293b;
        --text-secondary: #475569;
        --border: #cbd5e1;
      }
      /* ==============================================
         LAYOUT BASE
         ============================================== */
      html,
      body {
        height: 100%;
      }
      body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          "Helvetica Neue", Arial, sans-serif;
        background: linear-gradient(135deg, var(--bg-900), var(--bg-800),
          var(--bg-900));
        color: var(--text-primary);
        -webkit-font-smoothing: antialiased;
      }
      /* ==============================================
         HEADER
         ============================================== */
      header {
        background: linear-gradient(180deg, rgba(11, 18, 32, 0.7), rgba(11, 18, 32, 0.6));
        backdrop-filter: blur(8px);
        border-bottom: 1px solid var(--border);
        position: sticky;
        top: 0;
        z-index: 40;
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
        margin-bottom: 12px;
      }
      .header-title {
        display: flex;
        align-items: center;
        gap: 12px;
      }
      .header-icon {
        padding: 6px;
        background: rgba(37, 99, 235, 0.12);
        border-radius: var(--radius);
      }
      .header-icon svg {
        width: 20px;
        height: 20px;
        color: var(--primary);
        display: block;
      }
      h1 {
        font-size: 1.125rem;
        font-weight: 700;
        color: var(--text-primary);
      }
      .header-subtitle {
        font-size: 0.75rem;
        color: var(--text-secondary);
      }
      .header-actions {
        display: flex;
        gap: 8px;
        align-items: center;
      }
      /* Buttons */
      button {
        padding: 6px 12px;
        border-radius: var(--radius);
        border: 1px solid var(--border);
        font-size: 0.875rem;
        font-weight: 500;
        cursor: pointer;
        transition: all 0.16s;
        display: inline-flex;
        align-items: center;
        gap: 6px;
        background: transparent;
        color: var(--text-primary);
      }
      button:hover:not(:disabled) {
        border-color: var(--primary);
        background: rgba(37, 99, 235, 0.08);
      }
      button:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12);
      }
      button:disabled {
        opacity: 0.5;
        cursor: not-allowed;
      }
      button svg {
        width: 14px;
        height: 14px;
        display: block;
      }
      /* Stats Grid */
      .stats-grid {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 8px;
        margin-top: 12px;
      }
      .stat-card {
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.02),
          rgba(0, 0, 0, 0.03));
        border: 1px solid rgba(255, 255, 255, 0.02);
        border-radius: var(--radius);
        padding: 12px;
      }
      .stat-label {
        font-size: 10px;
        text-transform: uppercase;
        color: var(--text-secondary);
        font-weight: 600;
        margin-bottom: 6px;
      }
      .stat-value {
        font-size: 1.25rem;
        font-weight: 700;
        color: var(--text-primary);
      }
      .stat-value.blue {
        color: var(--primary);
      }
      .stat-value.green {
        color: var(--success);
      }
      .stat-value.purple {
        color: var(--color-purple);
      }
      .stat-value.yellow {
        color: var(--color-yellow);
      }
      /* Filters */
      .filters {
        margin-top: 12px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
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
        font-weight: 600;
        color: var(--text-secondary);
        margin-bottom: 6px;
      }
      input,
      select {
        width: 100%;
        padding: 8px 12px;
        font-size: 0.95rem;
        background: transparent;
        border: 1px solid rgba(255, 255, 255, 0.04);
        border-radius: var(--radius);
        color: var(--text-primary);
      }
      input::placeholder {
        color: var(--text-secondary);
      }
      input:focus,
      select:focus {
        outline: none;
        border-color: var(--primary);
        box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12);
      }
      /* ==============================================
         MAIN CONTENT
         ============================================== */
      main {
        max-width: 1800px;
        margin: 0 auto;
        padding: 16px;
        min-height: calc(100vh - 200px);
      }
      /* People Grid */
      .people-grid {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 12px;
      }
      @media (min-width: 640px) {
        .people-grid {
          grid-template-columns: repeat(3, 1fr);
        }
      }
      @media (min-width: 768px) {
        .people-grid {
          grid-template-columns: repeat(4, 1fr);
        }
      }
      @media (min-width: 1024px) {
        .people-grid {
          grid-template-columns: repeat(5, 1fr);
        }
      }
      .person-card {
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.02),
          rgba(0, 0, 0, 0.03));
        border: 1px solid var(--border);
        border-radius: var(--radius);
        padding: 16px;
        transition: all 0.2s;
      }
      .person-card:hover {
        border-color: var(--primary);
        background: linear-gradient(180deg, rgba(37, 99, 235, 0.05),
          rgba(37, 99, 235, 0.02));
      }
      .person-header {
        display: flex;
        gap: 12px;
        margin-bottom: 12px;
      }
      .person-avatar {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background: linear-gradient(135deg, var(--primary), var(--color-purple));
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: 700;
        color: white;
        flex-shrink: 0;
      }
      .person-info h3 {
        font-size: 1rem;
        font-weight: 600;
        color: var(--text-primary);
        margin-bottom: 2px;
      }
      .person-info p {
        font-size: 0.75rem;
        color: var(--text-secondary);
      }
      .demands-section {
        margin-top: 12px;
      }
      .demands-title {
        font-size: 0.75rem;
        color: var(--text-secondary);
        font-weight: 600;
        margin-bottom: 6px;
      }
      .demands-list {
        display: flex;
        flex-direction: column;
        gap: 4px;
        margin-bottom: 12px;
      }
      .demand-item {
        display: flex;
        align-items: center;
        gap: 6px;
        font-size: 0.85rem;
        padding: 4px 0;
      }
      .demand-dot {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        flex-shrink: 0;
      }
      .btn-assign {
        width: 100%;
        padding: 8px;
        background: rgba(37, 99, 235, 0.1);
        color: var(--primary);
        border: 1px solid rgba(37, 99, 235, 0.2);
        border-radius: var(--radius);
        font-size: 0.85rem;
        cursor: pointer;
        transition: all 0.2s;
      }
      .btn-assign:hover {
        background: rgba(37, 99, 235, 0.15);
        border-color: var(--primary);
      }
      /* Empty State */
      .empty-state {
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        padding: 32px;
        text-align: center;
        grid-column: 1 / -1;
      }
      .empty-state svg {
        width: 40px;
        height: 40px;
        color: var(--text-secondary);
        margin: 0 auto 8px;
        display: block;
      }
      .empty-state p {
        color: var(--text-secondary);
        font-size: 0.95rem;
      }
      /* ==============================================
         MODAL
         ============================================== */
      .modal-overlay {
        position: fixed;
        inset: 0;
        background: rgba(0, 0, 0, 0.5);
        display: none;
        align-items: center;
        justify-content: center;
        z-index: 90;
        padding: 20px;
      }
      .modal-overlay.active {
        display: flex;
      }
      .modal {
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        width: 100%;
        max-width: 500px;
        max-height: calc(100vh - 40px);
        overflow-y: auto;
        box-shadow: 0 20px 25px rgba(0, 0, 0, 0.3);
      }
      .modal-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 16px;
        border-bottom: 1px solid var(--border);
        position: sticky;
        top: 0;
        background: var(--surface);
      }
      .modal-person {
        display: flex;
        gap: 12px;
        align-items: center;
      }
      .modal-avatar {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background: linear-gradient(135deg, var(--primary), var(--color-purple));
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: 700;
        color: white;
      }
      .modal-name {
        font-weight: 600;
        color: var(--text-primary);
      }
      .modal-count {
        font-size: 0.85rem;
        color: var(--text-secondary);
      }
      .modal-close {
        width: 32px;
        height: 32px;
        padding: 0;
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .modal-section {
        padding: 16px;
      }
      .modal-section-title {
        font-size: 0.85rem;
        font-weight: 600;
        color: var(--text-secondary);
        text-transform: uppercase;
        margin-bottom: 12px;
      }
      .available-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
        gap: 8px;
        margin-bottom: 8px;
      }
      .available-item {
        background: rgba(255, 255, 255, 0.02);
        border: 1px solid var(--border);
        border-radius: 6px;
        padding: 10px;
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 8px;
        transition: all 0.14s;
        font-size: 0.9rem;
      }
      .available-item:hover:not(:disabled) {
        background: rgba(255, 255, 255, 0.04);
        border-color: rgba(37, 99, 235, 0.3);
      }
      .available-item:disabled {
        opacity: 0.5;
        cursor: not-allowed;
      }
      .assigned-badge {
        font-size: 11px;
        color: var(--success);
        font-weight: 700;
        margin-left: auto;
      }
      .btn-close-modal {
        width: 100%;
        padding: 10px 16px;
        background: var(--primary);
        color: white;
        border: none;
        border-radius: var(--radius);
        font-size: 0.95rem;
        font-weight: 600;
        cursor: pointer;
        margin-top: 16px;
      }
      .btn-close-modal:hover {
        background: var(--primary-strong);
      }
      /* Demand Colors */
      .bg-blue {
        background-color: var(--color-blue);
      }
      .bg-purple {
        background-color: var(--color-purple);
      }
      .bg-yellow {
        background-color: var(--color-yellow);
      }
      .bg-green {
        background-color: var(--color-green);
      }
      .bg-pink {
        background-color: var(--color-pink);
      }
      .bg-indigo {
        background-color: var(--color-indigo);
      }
      .bg-orange {
        background-color: var(--color-orange);
      }
      .bg-red {
        background-color: var(--color-red);
      }
      .bg-teal {
        background-color: var(--color-teal);
      }
      .bg-cyan {
        background-color: var(--color-cyan);
      }
      /* ==============================================
         TOAST NOTIFICATIONS
         ============================================== */
      .toast {
        position: fixed;
        bottom: 20px;
        right: 20px;
        padding: 12px 16px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        color: var(--text-primary);
        font-size: 0.95rem;
        z-index: 100;
        animation: slideIn 0.3s ease;
        max-width: 300px;
      }
      .toast.success {
        border-color: rgba(22, 163, 74, 0.3);
        background: rgba(22, 163, 74, 0.08);
        color: var(--success);
      }
      .toast.error {
        border-color: rgba(239, 68, 68, 0.3);
        background: rgba(239, 68, 68, 0.08);
        color: var(--danger);
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
      /* ==============================================
         RESPONSIVE
         ============================================== */
      @media (max-width: 420px) {
        h1 {
          font-size: 1rem;
        }
        .stat-value {
          font-size: 1.05rem;
        }
        .stats-grid {
          grid-template-columns: repeat(2, 1fr);
        }
        .header-top {
          flex-direction: column;
          align-items: flex-start;
        }
      }
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
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"
                />
              </svg>
            </div>
            <div>
              <h1>Sistema de Gestão</h1>
              <p class="header-subtitle">Pessoas e Demandas</p>
            </div>
          </div>
          <div class="header-actions">
            <button id="toggleFilters" aria-expanded="false">
              <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z"
                />
              </svg>
              Filtros
            </button>
            <button id="clearAll">Limpar Tudo</button>
            <button id="themeToggle">🌙 Tema</button>
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
              <input
                type="text"
                id="searchInput"
                placeholder="Digite o nome..."
                aria-label="Buscar agente"
              />
            </div>
            <div class="filter-group">
              <label for="demandFilter">Filtrar por Demanda</label>
              <select id="demandFilter" aria-label="Filtrar por demanda">
                <option value="">Todas as demandas</option>
              </select>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <main>
      <div id="peopleGrid" class="people-grid" aria-live="polite" aria-label="Grade de agentes"></div>
    </main>
    <!-- Modal -->
    <div
      id="modalOverlay"
      class="modal-overlay"
      role="dialog"
      aria-modal="true"
      aria-hidden="true"
    >
      <div class="modal" role="document">
        <div class="modal-header">
          <div class="modal-person">
            <div class="modal-avatar" id="modalAvatar"></div>
            <div>
              <div class="modal-name" id="modalName"></div>
              <div class="modal-count" id="modalCount"></div>
            </div>
          </div>
          <button class="modal-close" id="closeModal" aria-label="Fechar modal">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div id="currentAssignments" class="modal-section" style="display: none">
          <div class="modal-section-title">Demandas Atribuídas</div>
          <div id="currentList"></div>
        </div>
        <div class="modal-section">
          <div class="modal-section-title">Demandas Disponíveis</div>
          <div id="availableList" class="available-grid"></div>
        </div>
        <div style="padding: 16px">
          <button class="btn-close-modal" id="closeModalBtn">Concluir</button>
        </div>
      </div>
    </div>
    <!-- Main Script -->
    <script>
      // ==============================================
      // CONSTANTES
      // ==============================================
      const STORAGE_KEY = "ghost_people_v1";
      const THEME_KEY = "ghost_theme";
      const INITIAL_PEOPLE = [
        { id: "1", name: "Cristian", role: "Agente", demands: [] },
        { id: "2", name: "Eduardo", role: "Agente", demands: [] },
        { id: "3", name: "Emanuela", role: "Agente", demands: [] },
        { id: "4", name: "Emilly", role: "Agente", demands: [] },
        { id: "5", name: "Felipe", role: "Agente", demands: [] },
        { id: "6", name: "João", role: "Agente", demands: [] },
        { id: "7", name: "Kaua", role: "Agente", demands: [] },
        { id: "8", name: "Kauane", role: "Agente", demands: [] },
        { id: "9", name: "Luiz", role: "Agente", demands: [] },
        { id: "10", name: "Pamela", role: "Agente", demands: [] },
        { id: "11", name: "Patrick", role: "Agente", demands: [] },
        { id: "12", name: "Pedro", role: "Agente", demands: [] },
        { id: "13", name: "Richard", role: "Agente", demands: [] },
        { id: "14", name: "Thais", role: "Agente", demands: [] },
        { id: "15", name: "Vitória", role: "Agente", demands: [] },
      ];
      const DEMANDS = [
        { id: "nivel2", name: "Nível II", color: "bg-blue" },
        { id: "matrix", name: "Matrix", color: "bg-purple" },
        { id: "vip", name: "Tratamento VIP", color: "bg-yellow" },
        { id: "voz", name: "Voz", color: "bg-green" },
        { id: "emails", name: "Emails", color: "bg-pink" },
        { id: "helpdesk", name: "Help Desk", color: "bg-indigo" },
        { id: "batimento", name: "Batimento", color: "bg-orange" },
        { id: "massivas", name: "Massivas", color: "bg-red" },
        { id: "reincidentes", name: "Análises Reincidentes", color: "bg-teal" },
        { id: "cancelamentos", name: "Análises Cancelamentos", color: "bg-cyan" },
      ];
      // ==============================================
      // STATE
      // ==============================================
      let people = [];
      let selectedPerson = null;
      let searchTerm = "";
      let filterDemand = "";
      let searchDebounceTimer = null;
      // ==============================================
      // UTILITIES
      // ==============================================
      function escapeHtml(str) {
        const div = document.createElement("div");
        div.textContent = str;
        return div.innerHTML;
      }
      function showToast(message, type = "success") {
        const toast = document.createElement("div");
        toast.className = `toast ${type}`;
        toast.textContent = message;
        document.body.appendChild(toast);
        setTimeout(() => {
          toast.style.animation = "slideIn 0.3s ease reverse";
          setTimeout(() => toast.remove(), 300);
        }, 2500);
      }
      // ==============================================
      // STORAGE
      // ==============================================
      function loadFromStorage() {
        try {
          const stored = localStorage.getItem(STORAGE_KEY);
          if (!stored) {
            return JSON.parse(JSON.stringify(INITIAL_PEOPLE));
          }
          const parsed = JSON.parse(stored);
          if (!Array.isArray(parsed) || parsed.length === 0) {
            return JSON.parse(JSON.stringify(INITIAL_PEOPLE));
          }
          return parsed;
        } catch (e) {
          console.error("Erro ao carregar storage:", e);
          return JSON.parse(JSON.stringify(INITIAL_PEOPLE));
        }
      }
      function saveToStorage() {
        try {
          localStorage.setItem(STORAGE_KEY, JSON.stringify(people));
          return true;
        } catch (e) {
          console.error("Erro ao salvar storage:", e);
          showToast("Erro ao salvar dados.", "error");
          return false;
        }
      }
      // ==============================================
      // THEME
      // ==============================================
      function applyTheme(theme) {
        const root = document.documentElement;
        if (theme === "light") {
          root.classList.add("light-mode");
          localStorage.setItem(THEME_KEY, "light");
        } else {
          root.classList.remove("light-mode");
          localStorage.setItem(THEME_KEY, "dark");
        }
      }
      function initTheme() {
        const saved = localStorage.getItem(THEME_KEY);
        const prefersDark = window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches;
        const theme = saved || (prefersDark ? "dark" : "light");
        applyTheme(theme);
      }
      // ==============================================
      // BUSINESS LOGIC
      // ==============================================
      function getStatistics() {
        const total = people.length;
        const active = people.filter((p) => p.demands.length > 0).length;
        const assignments = people.reduce((s, p) => s + p.demands.length, 0);
        const unassigned = DEMANDS.filter(
          (d) => !people.some((p) => p.demands.includes(d.id))
        );
        return { total, active, assignments, unassigned };
      }
      function getFilteredPeople() {
        return people.filter((person) => {
          const matchesSearch = person.name
            .toLowerCase()
            .includes(searchTerm.toLowerCase());
          const matchesDemand = filterDemand
            ? person.demands.includes(filterDemand)
            : true;
          return matchesSearch && matchesDemand;
        });
      }
      function assignDemand(personId, demandId) {
        const person = people.find((p) => p.id === personId);
        if (!person) return;
        if (person.demands.includes(demandId)) {
          showToast("Demanda já atribuída", "error");
          return;
        }
        person.demands.push(demandId);
        if (!saveToStorage()) {
          person.demands.pop();
          return;
        }
        const demand = DEMANDS.find((d) => d.id === demandId);
        showToast(`${demand.name} atribuída a ${person.name}`);
        render();
        openModal(personId);
      }
      function removeDemand(personId, demandId) {
        const person = people.find((p) => p.id === personId);
        if (!person) return;
        person.demands = person.demands.filter((d) => d !== demandId);
        if (!saveToStorage()) {
          person.demands.push(demandId);
          return;
        }
        const demand = DEMANDS.find((d) => d.id === demandId);
        showToast(`${demand.name} removida`);
        render();
        openModal(personId);
      }
      function clearAllAssignments() {
        if (!confirm("Deseja realmente limpar todas as atribuições?")) return;
        const backup = JSON.parse(JSON.stringify(people));
        people.forEach((p) => (p.demands = []));
        if (!saveToStorage()) {
          people = backup;
          showToast("Erro ao salvar", "error");
          return;
        }
        showToast("Todas as atribuições foram limpas");
        render();
      }
      // ==============================================
      // RENDERING
      // ==============================================
      function renderPeopleGrid() {
        const grid = document.getElementById("peopleGrid");
        const filtered = getFilteredPeople();
        if (filtered.length === 0) {
          grid.innerHTML = `
            <div class="empty-state">
              <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
              </svg>
              <p>Nenhum agente encontrado</p>
            </div>
          `;
          return;
        }
        grid.innerHTML = filtered
          .map(
            (person) => `
          <div class="person-card">
            <div class="person-header">
              <div class="person-avatar">${escapeHtml(person.name.charAt(0))}</div>
              <div class="person-info">
                <h3>${escapeHtml(person.name)}</h3>
                <p>${escapeHtml(person.role)}</p>
              </div>
            </div>
            ${
              person.demands.length > 0
                ? `
              <div class="demands-section">
                <div class="demands-title">Demandas (${person.demands.length})</div>
                <div class="demands-list">
                  ${person.demands
                    .map((demandId) => {
                      const demand = DEMANDS.find((d) => d.id === demandId);
                      if (!demand) return "";
                      return `
                    <div class="demand-item">
                      <div class="demand-dot ${demand.color}"></div>
                      <span>${escapeHtml(demand.name)}</span>
                    </div>
                  `;
                    })
                    .join("")}
                </div>
              </div>
            `
                : `<div class="demands-section" style="text-align: center; color: var(--text-secondary); font-size: 0.85rem;">Sem demandas</div>`
            }
            <button class="btn-assign" data-action="open-modal" data-person="${person.id}">
              + Atribuir
            </button>
          </div>
        `
          )
          .join("");
      }
      function renderDemandFilter() {
        const select = document.getElementById("demandFilter");
        select.innerHTML =
          '<option value="">Todas as demandas</option>' +
          DEMANDS.map(
            (d) => `<option value="${d.id}">${escapeHtml(d.name)}</option>`
          ).join("");
      }
      function renderStatistics() {
        const stats = getStatistics();
        document.getElementById("statTotal").textContent = stats.total;
        document.getElementById("statActive").textContent = stats.active;
        document.getElementById("statAssignments").textContent = stats.assignments;
        document.getElementById("statUnassigned").textContent = stats.unassigned.length;
      }
      function render() {
        renderPeopleGrid();
        renderStatistics();
      }
      // ==============================================
      // MODAL
      // ==============================================
      let lastFocused = null;
      function openModal(personId) {
        selectedPerson = people.find((p) => p.id === personId);
        if (!selectedPerson) return;
        document.getElementById("modalAvatar").textContent = escapeHtml(
          selectedPerson.name.charAt(0)
        );
        document.getElementById("modalName").textContent = escapeHtml(
          selectedPerson.name
        );
        document.getElementById("modalCount").textContent =
          `${selectedPerson.demands.length} demanda(s)`;
        // Seção de demandas atribuídas
        const currentSection = document.getElementById("currentAssignments");
        if (selectedPerson.demands.length > 0) {
          currentSection.style.display = "block";
          document.getElementById("currentList").innerHTML =
            selectedPerson.demands
              .map((demandId) => {
                const demand = DEMANDS.find((d) => d.id === demandId);
                if (!demand) return "";
                return `
              <div style="display: flex; align-items: center; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid var(--border);">
                <div style="display: flex; align-items: center; gap: 8px;">
                  <div class="demand-dot ${demand.color}"></div>
                  <span>${escapeHtml(demand.name)}</span>
                </div>
                <button data-action="remove-demand" data-person="${selectedPerson.id}" data-demand="${demand.id}" style="padding: 4px 8px; font-size: 0.8rem; background: rgba(239, 68, 68, 0.1); color: var(--danger); border: 1px solid rgba(239, 68, 68, 0.2); border-radius: var(--radius); cursor: pointer;">Remover</button>
              </div>
            `;
              })
              .join("");
        } else {
          currentSection.style.display = "none";
        }
        // Seção de demandas disponíveis
        document.getElementById("availableList").innerHTML = DEMANDS.map(
          (demand) => {
            const isAssigned = selectedPerson.demands.includes(demand.id);
            return `
          <button class="available-item" data-action="assign-demand" data-person="${selectedPerson.id}" data-demand="${demand.id}" ${isAssigned ? "disabled" : ""}>
            <div class="demand-dot ${demand.color}"></div>
            <span>${escapeHtml(demand.name)}</span>
            ${isAssigned ? '<span class="assigned-badge">✓ Atribuída</span>' : ""}
          </button>
        `;
          }
        ).join("");
        const overlay = document.getElementById("modalOverlay");
        overlay.classList.add("active");
        overlay.setAttribute("aria-hidden", "false");
        lastFocused = document.activeElement;
      }
      function closeModal() {
        const overlay = document.getElementById("modalOverlay");
        overlay.classList.remove("active");
        overlay.setAttribute("aria-hidden", "true");
        selectedPerson = null;
        if (lastFocused && typeof lastFocused.focus === "function") {
          lastFocused.focus();
        }
      }
      // ==============================================
      // EVENT LISTENERS
      // ==============================================
      document.addEventListener("click", function (e) {
        if (e.target.closest('[data-action="open-modal"]')) {
          const personId = e.target.closest('[data-action="open-modal"]').dataset.person;
          openModal(personId);
          return;
        }
        if (e.target.closest('[data-action="assign-demand"]')) {
          const btn = e.target.closest('[data-action="assign-demand"]');
          assignDemand(btn.dataset.person, btn.dataset.demand);
          return;
        }
        if (e.target.closest('[data-action="remove-demand"]')) {
          const btn = e.target.closest('[data-action="remove-demand"]');
          removeDemand(btn.dataset.person, btn.dataset.demand);
          return;
        }
      });
      document.getElementById("toggleFilters").addEventListener("click", function () {
        const filters = document.getElementById("filtersSection");
        const isActive = filters.classList.toggle("active");
        this.setAttribute("aria-expanded", String(isActive));
      });
      document.getElementById("clearAll").addEventListener("click", clearAllAssignments);
      document.getElementById("searchInput").addEventListener("input", function (e) {
        searchTerm = e.target.value;
        clearTimeout(searchDebounceTimer);
        searchDebounceTimer = setTimeout(() => {
          render();
        }, 200);
      });
      document.getElementById("demandFilter").addEventListener("change", function (e) {
        filterDemand = e.target.value;
        render();
      });
      document.getElementById("closeModal").addEventListener("click", closeModal);
      document.getElementById("closeModalBtn").addEventListener("click", closeModal);
      document.getElementById("modalOverlay").addEventListener("click", function (e) {
        if (e.target === this) {
          closeModal();
        }
      });
      document.getElementById("themeToggle").addEventListener("click", function () {
        const isLight = document.documentElement.classList.contains("light-mode");
        applyTheme(isLight ? "dark" : "light");
        this.textContent = isLight ? "🌙 Tema" : "☀️ Tema";
      });
      // ==============================================
      // INITIALIZATION
      // ==============================================
      function init() {
        try {
          people = loadFromStorage();
          initTheme();
          renderDemandFilter();
          render();
          console.log("✓ Sistema inicializado com sucesso");
        } catch (e) {
          console.error("Erro durante inicialização:", e);
          showToast("Erro ao inicializar sistema", "error");
        }
      }
      if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", init);
      } else {
        init();
      }
    </script>
  </body>
</html>
