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
        font-family:
          -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          "Helvetica Neue", Arial, sans-serif;
        background: linear-gradient(
          135deg,
          var(--bg-900),
          var(--bg-800),
          var(--bg-900)
        );
        color: var(--text-primary);
        -webkit-font-smoothing: antialiased;
      }
      /* ==============================================
         HEADER
         ============================================== */
      header {
        background: linear-gradient(
          180deg,
          rgba(11, 18, 32, 0.7),
          rgba(11, 18, 32, 0.6)
        );
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
        background: linear-gradient(
          180deg,
          rgba(255, 255, 255, 0.02),
          rgba(0, 0, 0, 0.03)
        );
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
      /* Export Buttons Container */
      .export-buttons-container {
        margin-top: 12px;
        padding-top: 12px;
        border-top: 1px solid var(--border);
      }
      .export-buttons-container label {
        display: block;
        font-size: 0.75rem;
        font-weight: 600;
        color: var(--text-secondary);
        margin-bottom: 8px;
      }
      .export-buttons {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
        gap: 8px;
      }
      .btn-export {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 6px;
        padding: 8px 12px;
        font-size: 0.8rem;
        font-weight: 500;
        background: linear-gradient(
          135deg,
          rgba(37, 99, 235, 0.1),
          rgba(37, 99, 235, 0.05)
        );
        border: 1px solid rgba(37, 99, 235, 0.3);
        border-radius: var(--radius);
        color: var(--primary);
        cursor: pointer;
        transition: all 0.2s ease;
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
      }
      .btn-export:hover:not(:disabled) {
        background: linear-gradient(
          135deg,
          rgba(37, 99, 235, 0.2),
          rgba(37, 99, 235, 0.12)
        );
        border-color: var(--primary);
        box-shadow: 0 4px 12px rgba(37, 99, 235, 0.15);
        transform: translateY(-2px);
      }
      .btn-export:active {
        transform: translateY(0);
      }
      .btn-export svg {
        width: 16px;
        height: 16px;
        flex-shrink: 0;
      }
      @media (max-width: 640px) {
        .export-buttons {
          grid-template-columns: repeat(2, 1fr);
        }
      }
      @media (max-width: 420px) {
        .export-buttons {
          grid-template-columns: 1fr;
        }
        .btn-export {
          font-size: 0.75rem;
          padding: 6px 10px;
        }
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
        background: linear-gradient(
          180deg,
          rgba(255, 255, 255, 0.02),
          rgba(0, 0, 0, 0.03)
        );
        border: 1px solid var(--border);
        border-radius: var(--radius);
        padding: 16px;
        transition: all 0.2s;
      }
      .person-card:hover {
        border-color: var(--primary);
        background: linear-gradient(
          180deg,
          rgba(37, 99, 235, 0.05),
          rgba(37, 99, 235, 0.02)
        );
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
        background: linear-gradient(
          135deg,
          var(--primary),
          var(--color-purple)
        );
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
        background: linear-gradient(
          135deg,
          var(--primary),
          var(--color-purple)
        );
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
      /* ==============================================
         INTERNAL OBSERVATIONS
         ============================================== */
      .internal-observations-section {
        margin-top: 32px;
        padding: 20px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
      }
      .observations-title {
        font-size: 1.125rem;
        font-weight: 700;
        color: var(--text-primary);
        margin-bottom: 16px;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .observations-container {
        display: grid;
        grid-template-columns: 1fr;
        gap: 16px;
      }
      .agent-observation {
        padding: 12px;
        background: var(--surface-2);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        display: grid;
        grid-template-columns: 200px 1fr auto;
        gap: 12px;
        align-items: stretch;
      }
      .agent-observation-select {
        display: flex;
        flex-direction: column;
      }
      .agent-observation-select label {
        font-size: 0.75rem;
        font-weight: 600;
        color: var(--text-secondary);
        margin-bottom: 6px;
        text-transform: uppercase;
      }
      .agent-observation-select select {
        flex: 1;
        padding: 8px 12px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        color: var(--text-primary);
        font-size: 0.95rem;
      }
      .agent-observation-textarea {
        display: flex;
        flex-direction: column;
      }
      .agent-observation-textarea label {
        font-size: 0.75rem;
        font-weight: 600;
        color: var(--text-secondary);
        margin-bottom: 6px;
        text-transform: uppercase;
      }
      .agent-observation-textarea textarea {
        flex: 1;
        padding: 8px 12px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        color: var(--text-primary);
        font-size: 0.95rem;
        font-family: inherit;
        resize: none;
      }
      .agent-observation-actions {
        display: flex;
        gap: 8px;
        align-items: flex-end;
      }
      .agent-observation-actions button {
        padding: 8px 12px;
        font-size: 0.85rem;
      }
      .btn-add-observation {
        margin-top: 16px;
        padding: 10px 16px;
        background: var(--primary);
        border: 1px solid var(--primary);
        color: white;
        font-weight: 600;
        border-radius: var(--radius);
        cursor: pointer;
      }
      .btn-add-observation:hover {
        background: var(--primary-strong);
        border-color: var(--primary-strong);
      }
      /* ==============================================
         WEEKEND SCHEDULE
         ============================================== */
      .weekend-schedule-section {
        margin-top: 32px;
        padding: 20px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
      }
      .schedule-title {
        font-size: 1.125rem;
        font-weight: 700;
        color: var(--text-primary);
        margin-bottom: 20px;
      }
      .schedule-day-title {
        font-size: 1rem;
        font-weight: 700;
        color: var(--text-primary);
        margin: 20px 0 12px 0;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .schedule-day-title::before {
        content: "📅";
        font-size: 1.25rem;
      }
      .schedule-table {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 24px;
        background: var(--surface-2);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        overflow: hidden;
      }
      .schedule-table thead {
        background: var(--primary);
        color: white;
      }
      .schedule-table th {
        padding: 12px;
        text-align: center;
        font-weight: 600;
        font-size: 0.9rem;
        border-right: 1px solid var(--border);
      }
      .schedule-table th:last-child {
        border-right: none;
      }
      .schedule-table td {
        padding: 12px;
        border: 1px solid var(--border);
        text-align: center;
        font-size: 0.95rem;
      }
      .schedule-table tbody tr {
        background: var(--surface);
      }
      .schedule-table tbody tr:nth-child(odd) {
        background: var(--surface-2);
      }
      .schedule-time {
        font-weight: 600;
        color: var(--text-primary);
        min-width: 80px;
        background: rgba(37, 99, 235, 0.1);
      }
      .schedule-agent-select {
        padding: 6px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: 4px;
        color: var(--text-primary);
        font-size: 0.9rem;
        min-width: 140px;
      }
      .schedule-agent-select:focus {
        outline: none;
        border-color: var(--primary);
        box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.12);
      }
      .schedule-label {
        font-size: 0.8rem;
        color: var(--text-secondary);
        font-weight: 600;
        margin-bottom: 4px;
        display: block;
      }
      /* ==============================================
         OFF / DAY OFF / VACATION SECTION
         ============================================== */
      .off-schedule-section {
        margin-top: 32px;
        padding: 20px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
      }
      .off-schedule-title {
        font-size: 1.125rem;
        font-weight: 700;
        color: var(--text-primary);
        margin-bottom: 16px;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      /* Improved: Table-like layout for compact display */
      .off-schedule-grid {
        display: flex;
        flex-direction: column;
        gap: 8px;
      }
      .off-agent-card {
        padding: 10px 12px;
        background: var(--surface-2);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        display: grid;
        grid-template-columns: 200px 1fr;
        gap: 12px;
        align-items: center;
      }
      .off-agent-name {
        font-weight: 600;
        color: var(--text-primary);
        font-size: 0.95rem;
        word-break: break-word;
      }
      .off-agent-status {
        display: flex;
        gap: 6px;
        flex-wrap: nowrap;
        justify-content: flex-start;
      }
      .off-status-btn {
        flex: 0 1 auto;
        min-width: auto;
        padding: 6px 12px;
        font-size: 0.8rem;
        font-weight: 600;
        border: 1px solid var(--border);
        border-radius: 4px;
        background: var(--surface);
        color: var(--text-primary);
        cursor: pointer;
        transition: all 0.2s;
        white-space: nowrap;
      }
      .off-status-btn:hover {
        border-color: var(--primary);
        background: rgba(37, 99, 235, 0.08);
      }
      .off-status-btn.active {
        background: var(--primary);
        border-color: var(--primary);
        color: white;
      }
      .off-status-btn.folga.active {
        background: var(--warning);
        border-color: var(--warning);
      }
      .off-status-btn.vacation.active {
        background: var(--danger);
        border-color: var(--danger);
      }
      .off-empty-state {
        grid-column: 1 / -1;
        padding: 32px;
        text-align: center;
        color: var(--text-secondary);
        font-size: 0.95rem;
      }
      /* ==============================================
         MONTH WEEKENDS SCHEDULES (2x2 Layout)
         ============================================== */
      .month-weekends-section {
        margin-top: 32px;
        padding: 20px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: var(--radius);
      }
      .month-weekends-title {
        font-size: 1.25rem;
        font-weight: 700;
        color: var(--text-primary);
        margin-bottom: 20px;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .month-weekends-header {
        display: flex;
        gap: 12px;
        margin-bottom: 20px;
        flex-wrap: wrap;
      }
      .btn-generate-schedules {
        padding: 10px 16px;
        background: var(--primary);
        border: 1px solid var(--primary);
        color: white;
        font-weight: 600;
        border-radius: var(--radius);
        cursor: pointer;
        transition: all 0.2s;
      }
      .btn-generate-schedules:hover {
        background: var(--primary-strong);
        border-color: var(--primary-strong);
      }
      /* Grid layout 2x2 para as 4 agendas de fim de semana */
      .month-weekends-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
        gap: 20px;
        margin-bottom: 20px;
      }
      /* Em telas pequenas, ajusta para 1 coluna */
      @media (max-width: 1200px) {
        .month-weekends-grid {
          grid-template-columns: 1fr;
        }
      }
      .weekend-panel {
        background: var(--surface-2);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        overflow: hidden;
      }
      .weekend-panel-header {
        background: linear-gradient(135deg, var(--primary), var(--primary-strong));
        color: white;
        padding: 14px 16px;
        font-weight: 700;
        font-size: 1rem;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .weekend-panel-content {
        padding: 16px;
        max-height: 600px;
        overflow-y: auto;
      }
      .weekend-day-section {
        margin-bottom: 16px;
      }
      .weekend-day-section:last-child {
        margin-bottom: 0;
      }
      .weekend-day-label {
        font-weight: 700;
        color: var(--text-primary);
        font-size: 0.95rem;
        margin-bottom: 10px;
        padding-bottom: 8px;
        border-bottom: 1px solid var(--border);
      }
      .weekend-shift-row {
        display: flex;
        gap: 10px;
        margin-bottom: 10px;
        align-items: center;
        font-size: 0.9rem;
      }
      .weekend-shift-row:last-child {
        margin-bottom: 0;
      }
      .weekend-shift-label {
        min-width: 70px;
        color: var(--text-secondary);
        font-size: 0.85rem;
        font-weight: 500;
      }
      .weekend-agent-select {
        flex: 1;
        padding: 6px 8px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: 4px;
        color: var(--text-primary);
        font-size: 0.9rem;
        cursor: pointer;
      }
      .weekend-agent-select:focus {
        outline: none;
        border-color: var(--primary);
        box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.12);
      }
      /* CSS para tabelas dentro dos painéis de agenda automática */
      .month-schedule-day-section {
        margin-bottom: 16px;
      }
      .month-schedule-day-section:last-child {
        margin-bottom: 0;
      }
      .month-schedule-day-title {
        font-size: 0.95rem;
        font-weight: 700;
        color: var(--text-primary);
        margin: 0 0 12px 0;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .month-schedule-day-title::before {
        content: "📅";
        font-size: 1rem;
      }
      /* Tabelas dentro dos painéis herdam estilos de .schedule-table */
      .month-schedule-day-section .schedule-table {
        width: 100%;
        border-collapse: collapse;
        background: var(--surface-2);
        border: 1px solid var(--border);
        border-radius: var(--radius);
        overflow: hidden;
        margin: 0;
      }
      .month-schedule-day-section .schedule-table thead {
        background: var(--primary);
        color: white;
      }
      .month-schedule-day-section .schedule-table th {
        padding: 10px 8px;
        text-align: center;
        font-weight: 600;
        font-size: 0.85rem;
        border-right: 1px solid var(--border);
      }
      .month-schedule-day-section .schedule-table th:last-child {
        border-right: none;
      }
      .month-schedule-day-section .schedule-table td {
        padding: 10px 8px;
        border: 1px solid var(--border);
        text-align: center;
        font-size: 0.9rem;
      }
      .month-schedule-day-section .schedule-table tbody tr {
        background: var(--surface);
      }
      .month-schedule-day-section .schedule-table tbody tr:nth-child(odd) {
        background: var(--surface-2);
      }
      .month-schedule-day-section .schedule-table .schedule-time {
        font-weight: 600;
        color: var(--text-primary);
        min-width: 70px;
        background: rgba(37, 99, 235, 0.1);
      }
      /* Dropdown de agentes nas tabelas automáticas */
      .month-schedule-agent-select {
        padding: 6px 8px;
        background: var(--surface);
        border: 1px solid var(--border);
        border-radius: 4px;
        color: var(--text-primary);
        font-size: 0.9rem;
        cursor: pointer;
        min-width: 120px;
        width: 100%;
      }
      .month-schedule-agent-select:focus {
        outline: none;
        border-color: var(--primary);
        box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.12);
      }
      .weekend-agent-select:focus {
        outline: none;
        border-color: var(--primary);
        box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.12);
      }
      .month-off-schedule {
        margin-top: 20px;
        padding-top: 20px;
        border-top: 2px solid var(--border);
      }
      .month-off-schedule-title {
        font-size: 1rem;
        font-weight: 700;
        color: var(--text-primary);
        margin-bottom: 16px;
        display: flex;
        align-items: center;
        gap: 8px;
      }
      .month-off-schedule-grid {
        display: flex;
        flex-direction: column;
        gap: 8px;
      }
      /* ==============================================
         THEME IMPROVEMENTS
         ============================================== */
      .theme-toggle-btn {
        padding: 8px 12px;
        border-radius: var(--radius);
        border: 1px solid var(--border);
        background: transparent;
        color: var(--text-primary);
        cursor: pointer;
        font-weight: 600;
        transition: all 0.2s;
        display: inline-flex;
        align-items: center;
        gap: 6px;
      }
      .theme-toggle-btn:hover {
        border-color: var(--primary);
        background: rgba(37, 99, 235, 0.08);
      }
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
        .agent-observation {
          grid-template-columns: 1fr;
        }
        .schedule-table {
          font-size: 0.85rem;
        }
        .schedule-table th,
        .schedule-table td {
          padding: 8px;
        }
        .schedule-agent-select {
          width: 100%;
          min-width: auto;
        }
        .off-agent-card {
          grid-template-columns: 1fr;
          gap: 8px;
        }
        .off-agent-status {
          flex-wrap: wrap;
        }
        .off-status-btn {
          flex: 1 1 auto;
          min-width: 60px;
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
          <!-- Export Buttons -->
          <div id="exportButtonsContainer" class="export-buttons-container">
            <label>Exportar por Demanda</label>
            <div id="exportButtons" class="export-buttons"></div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <main>
      <div
        id="peopleGrid"
        class="people-grid"
        aria-live="polite"
        aria-label="Grade de agentes"
      ></div>
      <!-- Internal Observations Section -->
      <div class="internal-observations-section" id="observationsSection">
        <div class="observations-title">📝 Observações Internas</div>
        <div class="observations-container" id="observationsContainer"></div>
        <button class="btn-add-observation" id="addObservationBtn">
          + Adicionar Observação
        </button>
      </div>
      <!-- Weekend Schedule Section -->
      <div class="weekend-schedule-section" id="scheduleSection">
        <div class="schedule-title">🗓️ Agenda de Fins de Semana</div>
        <!-- Saturday -->
        <div class="schedule-day-title">SÁBADO</div>
        <table class="schedule-table">
          <thead>
            <tr>
              <th>Turno</th>
              <th>Entrada 01</th>
              <th>Saída 01</th>
              <th>Entrada 02</th>
              <th>Saída 02</th>
              <th>Agente</th>
            </tr>
          </thead>
          <tbody id="saturdaySchedule"></tbody>
        </table>
        <!-- Sunday -->
        <div class="schedule-day-title" style="margin-top: 32px">DOMINGO</div>
        <table class="schedule-table">
          <thead>
            <tr>
              <th>Turno</th>
              <th>Entrada 01</th>
              <th>Saída 01</th>
              <th>Entrada 02</th>
              <th>Saída 02</th>
              <th>Agente</th>
            </tr>
          </thead>
          <tbody id="sundaySchedule"></tbody>
        </table>
        <!-- OFF / DAY OFF / VACATION Section -->
        <div class="off-schedule-section" id="offSection">
          <div class="off-schedule-title">🌗 Folga / Day Off / Férias</div>
          <div class="off-schedule-grid" id="offScheduleGrid"></div>
        </div>
        <!-- MONTH WEEKENDS SCHEDULES Section -->
        <div class="month-weekends-section" id="monthWeekendsSection">
          <div class="month-weekends-title">📅 Agendas de 4 Fins de Semana do Mês</div>
          <div class="month-weekends-header">
            <button class="btn-generate-schedules" id="generateSchedulesBtn">
              🎲 Gerar Agendas Automaticamente
            </button>
          </div>
          <!-- Grid 2x2 para as 4 agendas -->
          <div class="month-weekends-grid" id="monthWeekendsGrid"></div>
          <!-- OFF / DAY OFF para as agendas de mês -->
          <div class="month-off-schedule" id="monthOffScheduleSection">
            <div class="month-off-schedule-title">🌗 Agentes Fora das Agendas</div>
            <div class="month-off-schedule-grid" id="monthOffScheduleGrid"></div>
          </div>
        </div>
      </div>
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
        <div
          id="currentAssignments"
          class="modal-section"
          style="display: none"
        >
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
      /* eslint-disable no-undef */
      // ==============================================
      // CONSTANTES
      // ==============================================
      const STORAGE_KEY = "ghost_people_v1";
      const THEME_KEY = "ghost_theme";
      const OBSERVATIONS_KEY = "ghost_observations_v1";
      const WEEKEND_SCHEDULE_KEY = "ghost_weekend_schedule_v1";
      const OFF_SCHEDULE_KEY = "ghost_off_schedule_v1";
      const MONTH_WEEKENDS_SCHEDULE_KEY = "ghost_month_weekends_v1";
      const OFF_STATUS_OPTIONS = {
        folga: { label: "Folga", color: "#f59e0b" },
        dayoff: { label: "Day Off", color: "#3b82f6" },
        vacation: { label: "Férias", color: "#ef4444" },
      };
      const WEEKEND_SHIFTS = {
        saturday: [
          {
            shift: "Turno 1",
            entry1: "07:30",
            exit1: "11:30",
            entry2: "12:30",
            exit2: "15:50",
          },
          {
            shift: "Turno 2",
            entry1: "08:00",
            exit1: "12:30",
            entry2: "13:30",
            exit2: "16:20",
          },
          {
            shift: "Turno 3",
            entry1: "09:00",
            exit1: "13:30",
            entry2: "14:30",
            exit2: "17:20",
          },
          {
            shift: "Turno 4",
            entry1: "10:00",
            exit1: "14:00",
            entry2: "15:00",
            exit2: "18:20",
          },
          {
            shift: "Turno 5",
            entry1: "12:00",
            exit1: "15:00",
            entry2: "16:00",
            exit2: "20:20",
          },
          {
            shift: "Turno 6",
            entry1: "12:00",
            exit1: "16:00",
            entry2: "17:00",
            exit2: "21:20",
          },
        ],
        sunday: [
          {
            shift: "Turno 1",
            entry1: "08:00",
            exit1: "12:00",
            entry2: "13:00",
            exit2: "16:20",
          },
          {
            shift: "Turno 2",
            entry1: "08:00",
            exit1: "12:30",
            entry2: "13:30",
            exit2: "16:20",
          },
          {
            shift: "Turno 3",
            entry1: "12:00",
            exit1: "14:00",
            entry2: "15:00",
            exit2: "20:20",
          },
          {
            shift: "Turno 4",
            entry1: "12:00",
            exit1: "15:00",
            entry2: "16:00",
            exit2: "20:20",
          },
        ],
      };
      // ==============================================
      // CONSTANTES PARA AGENDAS DE 4 FINS DE SEMANA
      // ==============================================
      const MONTH_WEEKENDS_CONFIG = {
        week1: { label: "Semana 1", weekend: "1º Fim de Semana" },
        week2: { label: "Semana 2", weekend: "2º Fim de Semana" },
        week3: { label: "Semana 3", weekend: "3º Fim de Semana" },
        week4: { label: "Semana 4", weekend: "4º Fim de Semana" },
      };
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
        {
          id: "cancelamentos",
          name: "Análises Cancelamentos",
          color: "bg-cyan",
        },
      ];
      // ==============================================
      // STATE
      // ==============================================
      let people = [];
      let selectedPerson = null;
      let searchTerm = "";
      let filterDemand = "";
      let searchDebounceTimer = null;
      let internalObservations = {};
      let weekendSchedule = {};
      let offSchedule = {};
      let monthWeekendSchedules = {}; // Armazena as 4 agendas de fim de semana do mês
      let observationForms = [];
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
      // INTERNAL OBSERVATIONS STORAGE
      // ==============================================
      function loadObservations() {
        try {
          const stored = localStorage.getItem(OBSERVATIONS_KEY);
          return stored ? JSON.parse(stored) : {};
        } catch (e) {
          console.error("Erro ao carregar observações:", e);
          return {};
        }
      }
      function saveObservations() {
        try {
          localStorage.setItem(
            OBSERVATIONS_KEY,
            JSON.stringify(internalObservations),
          );
          return true;
        } catch (e) {
          console.error("Erro ao salvar observações:", e);
          showToast("Erro ao salvar observações.", "error");
          return false;
        }
      }
      // ==============================================
      // WEEKEND SCHEDULE STORAGE
      // ==============================================
      function loadWeekendSchedule() {
        try {
          const stored = localStorage.getItem(WEEKEND_SCHEDULE_KEY);
          return stored ? JSON.parse(stored) : { saturday: {}, sunday: {} };
        } catch (e) {
          console.error("Erro ao carregar agenda:", e);
          return { saturday: {}, sunday: {} };
        }
      }
      function saveWeekendSchedule() {
        try {
          localStorage.setItem(
            WEEKEND_SCHEDULE_KEY,
            JSON.stringify(weekendSchedule),
          );
          return true;
        } catch (e) {
          console.error("Erro ao salvar agenda:", e);
          showToast("Erro ao salvar agenda.", "error");
          return false;
        }
      }
      // ==============================================
      // OFF SCHEDULE STORAGE
      // ==============================================
      function loadOffSchedule() {
        try {
          const stored = localStorage.getItem(OFF_SCHEDULE_KEY);
          return stored ? JSON.parse(stored) : {};
        } catch (e) {
          console.error("Erro ao carregar folgas:", e);
          return {};
        }
      }
      function saveOffSchedule() {
        try {
          localStorage.setItem(OFF_SCHEDULE_KEY, JSON.stringify(offSchedule));
          return true;
        } catch (e) {
          console.error("Erro ao salvar folgas:", e);
          showToast("Erro ao salvar folgas.", "error");
          return false;
        }
      }
      // ==============================================
      // MONTH WEEKENDS SCHEDULES STORAGE
      // ==============================================
      function loadMonthWeekendSchedules() {
        try {
          const stored = localStorage.getItem(MONTH_WEEKENDS_SCHEDULE_KEY);
          return stored
            ? JSON.parse(stored)
            : { week1: {}, week2: {}, week3: {}, week4: {} };
        } catch (e) {
          console.error("Erro ao carregar agendas do mês:", e);
          return { week1: {}, week2: {}, week3: {}, week4: {} };
        }
      }
      function saveMonthWeekendSchedules() {
        try {
          localStorage.setItem(
            MONTH_WEEKENDS_SCHEDULE_KEY,
            JSON.stringify(monthWeekendSchedules),
          );
          return true;
        } catch (e) {
          console.error("Erro ao salvar agendas do mês:", e);
          showToast("Erro ao salvar agendas do mês.", "error");
          return false;
        }
      }
      /**
       * Gera 4 agendas de fim de semana aleatórias para o mês
       * Cada agente é atribuído a apenas um turno em toda a semana gerada
       * Agentes não atribuídos aparecem na seção "Off/Day Off"
       */
      function generateMonthWeekendSchedules() {
        if (!people || people.length === 0) {
          showToast("Nenhum agente disponível para gerar agendas.", "warning");
          return;
        }
        // Reseta as agendas
        monthWeekendSchedules = {
          week1: { saturday: {}, sunday: {} },
          week2: { saturday: {}, sunday: {} },
          week3: { saturday: {}, sunday: {} },
          week4: { saturday: {}, sunday: {} },
        };
        const weeks = ["week1", "week2", "week3", "week4"];
        const agentIds = people.map((p) => p.id);
        let agentIndex = 0;
        // Para cada semana, gera sábado e domingo
        weeks.forEach((week) => {
          const shifts = ["saturday", "sunday"];
          shifts.forEach((day) => {
            const shiftsForDay =
              day === "saturday" ? WEEKEND_SHIFTS.saturday : WEEKEND_SHIFTS.sunday;
            // Atribui agentes aleatoriamente aos turnos do dia
            shiftsForDay.forEach((shift, shiftIndex) => {
              // Circula entre os agentes disponíveis
              const randomAgentId = agentIds[agentIndex % agentIds.length];
              monthWeekendSchedules[week][day][shiftIndex] = randomAgentId;
              agentIndex++;
            });
          });
        });
        // Salva no localStorage
        if (saveMonthWeekendSchedules()) {
          showToast(
            "✓ Agendas geradas com sucesso! Todos os 4 fins de semana foram criados.",
            "success",
          );
          renderMonthWeekendSchedules();
          renderMonthOffSchedule();
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
        const prefersDark =
          window.matchMedia &&
          window.matchMedia("(prefers-color-scheme: dark)").matches;
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
          (d) => !people.some((p) => p.demands.includes(d.id)),
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
      // EXPORTAÇÃO PARA EXCEL
      // ==============================================
      function getExportDataForDemand(demandId) {
        const demand = DEMANDS.find((d) => d.id === demandId);
        if (!demand) return [];
        const data = [];
        people.forEach((person) => {
          if (person.demands.includes(demandId)) {
            // Escala de fim de semana
            if (weekendSchedule && weekendSchedule.saturday) {
              weekendSchedule.saturday.forEach((slot) => {
                if (slot.agents && slot.agents.includes(person.id)) {
                  data.push({
                    Função: demand.name,
                    Agente: person.name,
                    Data: "Sábado",
                    Turno: slot.time || "Não informado",
                    Status: slot.status || "-",
                    Observações: slot.observations || "-",
                  });
                }
              });
            }
            if (weekendSchedule && weekendSchedule.sunday) {
              weekendSchedule.sunday.forEach((slot) => {
                if (slot.agents && slot.agents.includes(person.id)) {
                  data.push({
                    Função: demand.name,
                    Agente: person.name,
                    Data: "Domingo",
                    Turno: slot.time || "Não informado",
                    Status: slot.status || "-",
                    Observações: slot.observations || "-",
                  });
                }
              });
            }
            // Off-schedule
            if (offSchedule && offSchedule[person.id]) {
              const offItems = offSchedule[person.id];
              Object.values(offItems).forEach((item) => {
                if (item && item.dates && Array.isArray(item.dates)) {
                  item.dates.forEach((date) => {
                    data.push({
                      Função: demand.name,
                      Agente: person.name,
                      Data: date,
                      Turno: item.type || "Não informado",
                      Status: item.type || "-",
                      Observações: "-",
                    });
                  });
                }
              });
            }
          }
        });
        return data;
      }
      function exportDemandToExcel(demandId) {
        const demand = DEMANDS.find((d) => d.id === demandId);
        if (!demand) {
          showToast("Demanda não encontrada", "error");
          return;
        }
        const data = getExportDataForDemand(demandId);
        if (data.length === 0) {
          showToast("Nenhum dado para exportar nesta demanda", "warning");
          return;
        }
        // Criar planilha
        const ws = XLSX.utils.json_to_sheet(data);
        // Ajustar largura das colunas
        const colWidths = [
          { wch: 25 }, // Função
          { wch: 20 }, // Agente
          { wch: 15 }, // Data
          { wch: 15 }, // Turno
          { wch: 15 }, // Status
          { wch: 30 }, // Observações
        ];
        ws["!cols"] = colWidths;
        // Estilizar cabeçalho
        const headerStyle = {
          fill: { fgColor: { rgb: "FF2563EB" } },
          font: { bold: true, color: { rgb: "FFFFFFFF" } },
          alignment: { horizontal: "center", vertical: "center" },
        };
        for (let i = 0; i < data[0] ? Object.keys(data[0]).length : 0; i++) {
          const cellRef = XLSX.utils.encode_col(i) + "1";
          if (ws[cellRef]) {
            ws[cellRef].s = headerStyle;
          }
        }
        // Criar workbook e exportar
        const wb = XLSX.utils.book_new();
        XLSX.utils.book_append_sheet(wb, ws, demand.name);
        const today = new Date().toISOString().split("T")[0];
        const fileName = `Escala_${demand.name.replace(/\s+/g, "_")}_${today}.xlsx`;
        XLSX.writeFile(wb, fileName);
        showToast(`Exportado: ${fileName}`, "success");
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
        `,
          )
          .join("");
      }
      function renderDemandFilter() {
        const select = document.getElementById("demandFilter");
        select.innerHTML =
          '<option value="">Todas as demandas</option>' +
          DEMANDS.map(
            (d) => `<option value="${d.id}">${escapeHtml(d.name)}</option>`,
          ).join("");
      }
      function renderExportButtons() {
        const container = document.getElementById("exportButtons");
        if (!container) return;
        container.innerHTML = DEMANDS.map((demand) => {
          return `
            <button
              class="btn-export"
              data-demand-id="${demand.id}"
              title="Exportar ${escapeHtml(demand.name)}"
              aria-label="Exportar ${escapeHtml(demand.name)} para Excel"
            >
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/>
                <polyline points="17 21 17 13 7 13 7 21"/>
                <polyline points="7 5 7 13 17 13"/>
              </svg>
              ${escapeHtml(demand.name)}
            </button>
          `;
        }).join("");
        // Adicionar event listeners
        container.querySelectorAll(".btn-export").forEach((btn) => {
          btn.addEventListener("click", () => {
            const demandId = btn.dataset.demandId;
            exportDemandToExcel(demandId);
          });
        });
      }
      function renderStatistics() {
        const stats = getStatistics();
        document.getElementById("statTotal").textContent = stats.total;
        document.getElementById("statActive").textContent = stats.active;
        document.getElementById("statAssignments").textContent =
          stats.assignments;
        document.getElementById("statUnassigned").textContent =
          stats.unassigned.length;
      }
      function render() {
        renderPeopleGrid();
        renderStatistics();
        renderObservationsAndSchedule();
        renderExportButtons();
      }
      // ==============================================
      // MODAL
      // ==============================================
      let lastFocused = null;
      function openModal(personId) {
        selectedPerson = people.find((p) => p.id === personId);
        if (!selectedPerson) return;
        document.getElementById("modalAvatar").textContent = escapeHtml(
          selectedPerson.name.charAt(0),
        );
        document.getElementById("modalName").textContent = escapeHtml(
          selectedPerson.name,
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
          },
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
      // RENDER FUNCTIONS
      // ==============================================
      function renderObservations() {
        const container = document.getElementById("observationsContainer");
        observationForms = [];
        if (people.length === 0) {
          container.innerHTML =
            '<p style="color: var(--text-secondary); font-size: 0.95rem;">Nenhum agente registrado.</p>';
          return;
        }
        container.innerHTML = people
          .map((person, _index) => {
            const obs = internalObservations[person.id] || {
              agent: person.id,
              note: "",
            };
            const formId = `obs-${person.id}`;
            observationForms.push(formId);
            return `
          <div class="agent-observation">
            <div class="agent-observation-select">
              <label>Agente</label>
              <select disabled style="background: rgba(255, 255, 255, 0.05);">
                <option>${escapeHtml(person.name)}</option>
              </select>
            </div>
            <div class="agent-observation-textarea">
              <label for="${formId}">Observação Interna</label>
              <textarea id="${formId}" placeholder="Adicione notas internas sobre este agente..." data-person-id="${person.id}">${escapeHtml(obs.note)}</textarea>
            </div>
            <div class="agent-observation-actions">
              <button class="btn-save-observation" data-person-id="${person.id}" style="padding: 8px 12px; font-size: 0.85rem; background: var(--success); border: 1px solid var(--success); color: white; border-radius: var(--radius); cursor: pointer;">Salvar</button>
            </div>
          </div>
        `;
          })
          .join("");
        // Event listeners para botões de salvar
        document.querySelectorAll(".btn-save-observation").forEach((btn) => {
          btn.addEventListener("click", function () {
            const personId = this.dataset.personId;
            const textarea = document.getElementById(`obs-${personId}`);
            const note = textarea.value;
            internalObservations[personId] = {
              agent: personId,
              note: note,
              lastUpdated: new Date().toISOString(),
            };
            saveObservations();
            showToast("Observação salva com sucesso!", "success");
          });
        });
      }
      // Helper: Get agents already selected in other fields for the same day
      function getSelectedAgentsForDay(day, excludeShiftIndex = null) {
        const selectedIds = new Set();
        document
          .querySelectorAll(".schedule-agent-select")
          .forEach((select) => {
            const key = select.dataset.scheduleKey;
            const [selectDay, selectShiftIndex] = key.split("-");
            // Only count if same day and different field
            if (
              selectDay === day &&
              selectShiftIndex !== String(excludeShiftIndex) &&
              select.value
            ) {
              selectedIds.add(select.value);
            }
          });
        return selectedIds;
      }
      function renderWeekendSchedule() {
        const saturdayBody = document.getElementById("saturdaySchedule");
        const sundayBody = document.getElementById("sundaySchedule");
        // Saturday - Fixed structure (same as Sunday)
        saturdayBody.innerHTML = WEEKEND_SHIFTS.saturday
          .map((shift, index) => {
            const scheduleKey = `saturday-${index}`;
            const agentId = weekendSchedule.saturday?.[index] || "";
            const selectedAgents = getSelectedAgentsForDay("saturday", index);
            return `
          <tr>
            <td class="schedule-time">${shift.shift}</td>
            <td>${shift.entry1}</td>
            <td>${shift.exit1}</td>
            <td>${shift.entry2}</td>
            <td>${shift.exit2}</td>
            <td>
              <select class="schedule-agent-select" data-schedule-key="${scheduleKey}">
                <option value="">Selecionar agente</option>
                ${people
                  .map((p) => {
                    const isSelected = agentId === p.id;
                    const isOtherSelected =
                      !isSelected && selectedAgents.has(p.id);
                    return `<option value="${p.id}" ${isSelected ? "selected" : ""}${isOtherSelected ? " disabled" : ""}>${escapeHtml(p.name)}${isOtherSelected ? " (alocado)" : ""}</option>`;
                  })
                  .join("")}
              </select>
            </td>
          </tr>
        `;
          })
          .join("");
        // Sunday - Standard structure
        sundayBody.innerHTML = WEEKEND_SHIFTS.sunday
          .map((shift, index) => {
            const scheduleKey = `sunday-${index}`;
            const agentId = weekendSchedule.sunday?.[index] || "";
            const selectedAgents = getSelectedAgentsForDay("sunday", index);
            return `
          <tr>
            <td class="schedule-time">${shift.shift}</td>
            <td>${shift.entry1}</td>
            <td>${shift.exit1}</td>
            <td>${shift.entry2}</td>
            <td>${shift.exit2}</td>
            <td>
              <select class="schedule-agent-select" data-schedule-key="${scheduleKey}">
                <option value="">Selecionar agente</option>
                ${people
                  .map((p) => {
                    const isSelected = agentId === p.id;
                    const isOtherSelected =
                      !isSelected && selectedAgents.has(p.id);
                    return `<option value="${p.id}" ${isSelected ? "selected" : ""}${isOtherSelected ? " disabled" : ""}>${escapeHtml(p.name)}${isOtherSelected ? " (alocado)" : ""}</option>`;
                  })
                  .join("")}
              </select>
            </td>
          </tr>
        `;
          })
          .join("");
        // Event listeners para mudanças de agente
        document
          .querySelectorAll(".schedule-agent-select")
          .forEach((select) => {
            select.addEventListener("change", function () {
              const key = this.dataset.scheduleKey;
              const [day, shiftIndex] = key.split("-");
              const agentId = this.value;
              if (!weekendSchedule[day]) {
                weekendSchedule[day] = {};
              }
              weekendSchedule[day][shiftIndex] = agentId;
              saveWeekendSchedule();
              // Re-render to update available agents in other selects
              renderWeekendSchedule();
              renderOffSchedule();
              showToast("Agenda atualizada!", "success");
            });
          });
      }
      function renderOffSchedule() {
        const container = document.getElementById("offScheduleGrid");
        // Get all agents that are NOT allocated to any shift
        const allocatedAgentIds = new Set();
        const agentAllocationMap = new Map(); // Track which day each agent is allocated
        // Add Saturday allocated agents
        Object.values(weekendSchedule.saturday || {}).forEach((agentId) => {
          if (agentId) {
            allocatedAgentIds.add(agentId);
            agentAllocationMap.set(agentId, "Sábado");
          }
        });
        // Add Sunday allocated agents
        Object.values(weekendSchedule.sunday || {}).forEach((agentId) => {
          if (agentId) {
            allocatedAgentIds.add(agentId);
            agentAllocationMap.set(agentId, "Domingo");
          }
        });
        // Get unallocated agents
        const unallocatedAgents = people.filter(
          (p) => !allocatedAgentIds.has(p.id),
        );
        if (unallocatedAgents.length === 0) {
          container.innerHTML =
            '<div class="off-empty-state">✅ Todos os agentes foram alocados à agenda de fim de semana.</div>';
          return;
        }
        container.innerHTML = unallocatedAgents
          .map((agent) => {
            const status = offSchedule[agent.id] || null;
            return `
          <div class="off-agent-card">
            <div class="off-agent-name" title="Disponível">${escapeHtml(agent.name)}</div>
            <div class="off-agent-status">
              <button class="off-status-btn folga" data-agent-id="${agent.id}" data-status="folga" title="Marcar como Folga" ${status === "folga" ? "aria-pressed='true'" : ""}>
                Folga
              </button>
              <button class="off-status-btn" data-agent-id="${agent.id}" data-status="dayoff" title="Marcar como Day Off">
                Day Off
              </button>
              <button class="off-status-btn vacation" data-agent-id="${agent.id}" data-status="vacation" title="Marcar como Férias">
                Férias
              </button>
            </div>
          </div>
        `;
          })
          .join("");
        // Apply active states
        document.querySelectorAll(".off-status-btn").forEach((btn) => {
          const agentId = btn.dataset.agentId;
          const btnStatus = btn.dataset.status;
          const currentStatus = offSchedule[agentId];
          if (btnStatus === currentStatus) {
            btn.classList.add("active");
            btn.setAttribute("aria-pressed", "true");
          }
          btn.addEventListener("click", function () {
            const agent = people.find((p) => p.id === agentId);
            if (!agent) return;
            // Remove previous status if exists
            const previousBtn = container.querySelector(
              `.off-status-btn[data-agent-id="${agentId}"].active`,
            );
            if (previousBtn) {
              previousBtn.classList.remove("active");
              previousBtn.setAttribute("aria-pressed", "false");
            }
            // Set new status
            if (offSchedule[agentId] === btnStatus) {
              // Toggle off
              delete offSchedule[agentId];
              this.classList.remove("active");
              this.setAttribute("aria-pressed", "false");
            } else {
              // Set new status
              offSchedule[agentId] = btnStatus;
              this.classList.add("active");
              this.setAttribute("aria-pressed", "true");
            }
            saveOffSchedule();
            showToast(
              `${agent.name} marcado como ${OFF_STATUS_OPTIONS[btnStatus].label}`,
              "success",
            );
          });
        });
      }
      /**
       * Renderiza as 4 agendas de fim de semana do mês usando tabelas HTML
       * Utiliza a mesma estrutura e layout do "Weekend Agenda" para garantir consistência
       * Cada painel contém sábado e domingo com seus respectivos turnos
       */
      function renderMonthWeekendSchedules() {
        const container = document.getElementById("monthWeekendsGrid");
        if (
          !monthWeekendSchedules ||
          Object.keys(monthWeekendSchedules).length === 0
        ) {
          container.innerHTML =
            '<div style="grid-column: 1/-1; text-align: center; padding: 40px; color: var(--text-secondary);">Clique em "Gerar Agendas Automaticamente" para criar as 4 agendas de fim de semana.</div>';
          return;
        }
        const weeks = ["week1", "week2", "week3", "week4"];
        const weekConfigs = MONTH_WEEKENDS_CONFIG;
        container.innerHTML = weeks
          .map((week) => {
            const config = weekConfigs[week];
            const scheduleData = monthWeekendSchedules[week] || {
              saturday: {},
              sunday: {},
            };
            // Renderiza os dias da semana (sábado e domingo) usando tabelas
            const daysHtml = ["saturday", "sunday"]
              .map((day) => {
                const dayTitle =
                  day === "saturday" ? "SÁBADO" : "DOMINGO";
                const shifts =
                  day === "saturday"
                    ? WEEKEND_SHIFTS.saturday
                    : WEEKEND_SHIFTS.sunday;
                // Renderiza a tabela para o dia
                const tableRows = shifts
                  .map((shift, index) => {
                    const agentId = scheduleData[day]?.[index] || "";
                    const uniqueKey = `${week}-${day}-${index}`;
                    return `
                  <tr>
                    <td class="schedule-time">${escapeHtml(shift.shift)}</td>
                    <td>${shift.entry1}</td>
                    <td>${shift.exit1}</td>
                    <td>${shift.entry2}</td>
                    <td>${shift.exit2}</td>
                    <td>
                      <select class="month-schedule-agent-select" data-month-key="${uniqueKey}" data-week="${week}" data-day="${day}" data-shift-index="${index}">
                        <option value="">Selecionar agente</option>
                        ${people
                          .map((p) => {
                            const isSelected = agentId === p.id;
                            return `<option value="${p.id}" ${isSelected ? "selected" : ""}>${escapeHtml(p.name)}</option>`;
                          })
                          .join("")}
                      </select>
                    </td>
                  </tr>
                `;
                  })
                  .join("");
                return `
                <div class="month-schedule-day-section">
                  <div class="month-schedule-day-title">${dayTitle}</div>
                  <table class="schedule-table">
                    <thead>
                      <tr>
                        <th>Turno</th>
                        <th>Entrada 01</th>
                        <th>Saída 01</th>
                        <th>Entrada 02</th>
                        <th>Saída 02</th>
                        <th>Agente</th>
                      </tr>
                    </thead>
                    <tbody>
                      ${tableRows}
                    </tbody>
                  </table>
                </div>
              `;
              })
              .join("");
            return `
              <div class="weekend-panel">
                <div class="weekend-panel-header">
                  <span>${escapeHtml(config.label)} - ${escapeHtml(config.weekend)}</span>
                </div>
                <div class="weekend-panel-content">
                  ${daysHtml}
                </div>
              </div>
            `;
          })
          .join("");
        // Adiciona event listeners para editabilidade
        document.querySelectorAll(".month-schedule-agent-select").forEach((select) => {
          select.addEventListener("change", function () {
            const week = this.dataset.week;
            const day = this.dataset.day;
            const shiftIndex = this.dataset.shiftIndex;
            const agentId = this.value;
            if (!monthWeekendSchedules[week]) {
              monthWeekendSchedules[week] = { saturday: {}, sunday: {} };
            }
            monthWeekendSchedules[week][day][shiftIndex] = agentId;
            saveMonthWeekendSchedules();
            renderMonthOffSchedule();
            showToast("Agenda atualizada!", "success");
          });
        });
      }
      /**
       * Renderiza a seção de agentes que não foram alocados
       * Mostra apenas agentes não alocados em NENHUM dos 4 fins de semana
       */
      function renderMonthOffSchedule() {
        const container = document.getElementById("monthOffScheduleGrid");
        // Coleta todos os agentes alocados em qualquer uma das 4 semanas
        const allocatedAgentIds = new Set();
        Object.values(monthWeekendSchedules).forEach((week) => {
          ["saturday", "sunday"].forEach((day) => {
            Object.values(week[day] || {}).forEach((agentId) => {
              if (agentId) {
                allocatedAgentIds.add(agentId);
              }
            });
          });
        });
        // Encontra agentes não alocados
        const unallocatedAgents = people.filter(
          (p) => !allocatedAgentIds.has(p.id),
        );
        if (unallocatedAgents.length === 0) {
          container.innerHTML =
            '<div style="padding: 20px; text-align: center; color: var(--text-secondary);">✅ Todos os agentes foram alocados aos 4 fins de semana.</div>';
          return;
        }
        container.innerHTML = unallocatedAgents
          .map((agent) => {
            return `
          <div class="off-agent-card">
            <div class="off-agent-name">${escapeHtml(agent.name)}</div>
            <div class="off-agent-status">
              <span style="color: var(--text-secondary); font-size: 0.9rem;">Não alocado neste ciclo</span>
            </div>
          </div>
        `;
          })
          .join("");
      }
      function renderObservationsAndSchedule() {
        renderObservations();
        renderWeekendSchedule();
        renderOffSchedule();
        renderMonthWeekendSchedules();
        renderMonthOffSchedule();
      }
      // ==============================================
      // EVENT LISTENERS
      // ==============================================
      document.addEventListener("click", function (e) {
        if (e.target.closest('[data-action="open-modal"]')) {
          const personId = e.target.closest('[data-action="open-modal"]')
            .dataset.person;
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
      document
        .getElementById("toggleFilters")
        .addEventListener("click", function () {
          const filters = document.getElementById("filtersSection");
          const isActive = filters.classList.toggle("active");
          this.setAttribute("aria-expanded", String(isActive));
        });
      document
        .getElementById("clearAll")
        .addEventListener("click", clearAllAssignments);
      document
        .getElementById("searchInput")
        .addEventListener("input", function (e) {
          searchTerm = e.target.value;
          clearTimeout(searchDebounceTimer);
          searchDebounceTimer = setTimeout(() => {
            render();
          }, 200);
        });
      document
        .getElementById("demandFilter")
        .addEventListener("change", function (e) {
          filterDemand = e.target.value;
          render();
        });
      document
        .getElementById("closeModal")
        .addEventListener("click", closeModal);
      document
        .getElementById("closeModalBtn")
        .addEventListener("click", closeModal);
      document
        .getElementById("modalOverlay")
        .addEventListener("click", function (e) {
          if (e.target === this) {
            closeModal();
          }
        });
      document
        .getElementById("themeToggle")
        .addEventListener("click", function () {
          const isLight =
            document.documentElement.classList.contains("light-mode");
          applyTheme(isLight ? "dark" : "light");
          this.textContent = isLight ? "🌙 Tema" : "☀️ Tema";
        });
      document
        .getElementById("addObservationBtn")
        .addEventListener("click", function () {
          showToast(
            "Use o campo de observações para adicionar notas sobre cada agente.",
            "success",
          );
        });
      document
        .getElementById("generateSchedulesBtn")
        .addEventListener("click", function () {
          generateMonthWeekendSchedules();
        });
      // ==============================================
      // INITIALIZATION
      // ==============================================
      function init() {
        try {
          people = loadFromStorage();
          internalObservations = loadObservations();
          weekendSchedule = loadWeekendSchedule();
          offSchedule = loadOffSchedule();
          monthWeekendSchedules = loadMonthWeekendSchedules();
          initTheme();
          renderDemandFilter();
          renderExportButtons();
          render();
          renderObservationsAndSchedule();
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
    <!-- SheetJS para exportação Excel -->
    <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
  </body>
</html>
