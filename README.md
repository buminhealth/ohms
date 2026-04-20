<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>부민병원 보건관리시스템 (OHMS)</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css">
<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
<style>
/* ============================================================
   부민병원 보건관리시스템 (OHMS) - Phase 1
   디자인 컨셉: 병원 업무 - 신뢰감·가독성·밀도
============================================================ */
:root {
  --bg: #f7f8fa;
  --surface: #ffffff;
  --surface-2: #f1f3f5;
  --border: #e5e7eb;
  --border-strong: #d1d5db;
  --text: #111827;
  --text-2: #4b5563;
  --text-3: #9ca3af;
  
  --primary: #0f4c75;
  --primary-dark: #0a3a5c;
  --primary-light: #e3edf6;
  --accent: #10b981;
  --accent-dark: #059669;
  
  --warn: #f59e0b;
  --warn-bg: #fef3c7;
  --danger: #dc2626;
  --danger-bg: #fee2e2;
  --info: #3b82f6;
  --info-bg: #dbeafe;
  
  --radius: 8px;
  --radius-sm: 5px;
  --radius-lg: 12px;
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.04);
  --shadow: 0 2px 8px rgba(0,0,0,0.06);
  --shadow-lg: 0 10px 30px rgba(0,0,0,0.12);
  
  --font: 'Pretendard Variable', Pretendard, -apple-system, BlinkMacSystemFont, sans-serif;
}

* { box-sizing: border-box; }
html, body { margin: 0; padding: 0; }
body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--text);
  font-size: 14px;
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}
button, input, select, textarea { font-family: inherit; font-size: inherit; color: inherit; }
button { cursor: pointer; border: none; background: none; }
input, select, textarea {
  width: 100%;
  padding: 8px 10px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-sm);
  background: #fff;
  outline: none;
  transition: border-color 0.15s, box-shadow 0.15s;
}
input:focus, select:focus, textarea:focus {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px var(--primary-light);
}
label { display: block; font-size: 12px; color: var(--text-2); margin-bottom: 4px; font-weight: 500; }
table { width: 100%; border-collapse: collapse; }

/* ---------- 로그인 ---------- */
#loginView {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #0f4c75 0%, #0a3a5c 100%);
}
.login-card {
  background: #fff;
  padding: 40px;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  width: 100%;
  max-width: 400px;
}
.login-card h1 {
  margin: 0 0 8px;
  font-size: 24px;
  color: var(--primary);
  letter-spacing: -0.5px;
}
.login-card .subtitle { color: var(--text-3); font-size: 13px; margin-bottom: 28px; }
.login-card .logo-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: var(--primary-light);
  color: var(--primary);
  padding: 6px 12px;
  border-radius: 100px;
  font-size: 11px;
  font-weight: 600;
  margin-bottom: 16px;
  letter-spacing: 0.5px;
}
.login-card .field { margin-bottom: 14px; }
.login-card button[type="submit"] {
  width: 100%;
  padding: 12px;
  background: var(--primary);
  color: #fff;
  border-radius: var(--radius-sm);
  font-weight: 600;
  margin-top: 12px;
  font-size: 15px;
  transition: background 0.15s;
}
.login-card button[type="submit"]:hover { background: var(--primary-dark); }
.login-error { color: var(--danger); font-size: 13px; margin-top: 10px; min-height: 18px; }
.login-hint {
  margin-top: 24px;
  padding-top: 20px;
  border-top: 1px solid var(--border);
  font-size: 12px;
  color: var(--text-3);
  line-height: 1.7;
}

/* ---------- 앱 레이아웃 ---------- */
#appView { display: none; }
.app-shell { display: grid; grid-template-columns: 220px 1fr; min-height: 100vh; }

/* 사이드바 */
.sidebar {
  background: #0f172a;
  color: #e5e7eb;
  padding: 20px 12px;
  display: flex;
  flex-direction: column;
}
.sidebar-brand {
  padding: 8px 12px 20px;
  border-bottom: 1px solid rgba(255,255,255,0.1);
  margin-bottom: 16px;
}
.sidebar-brand .name {
  font-size: 16px;
  font-weight: 700;
  color: #fff;
  letter-spacing: -0.3px;
}
.sidebar-brand .tag {
  font-size: 10px;
  color: #64748b;
  letter-spacing: 1px;
  margin-top: 3px;
  font-weight: 600;
}
.nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 12px;
  border-radius: var(--radius-sm);
  color: #cbd5e1;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
  margin-bottom: 2px;
}
.nav-item:hover { background: rgba(255,255,255,0.06); color: #fff; }
.nav-item.active { background: var(--primary); color: #fff; }
.nav-item .icon { width: 18px; text-align: center; }
.nav-footer {
  margin-top: auto;
  padding-top: 16px;
  border-top: 1px solid rgba(255,255,255,0.1);
  font-size: 11px;
  color: #64748b;
}
.nav-user {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 12px;
  margin-bottom: 6px;
}
.nav-user .avatar {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 13px;
}
.nav-user .info { flex: 1; overflow: hidden; }
.nav-user .email { color: #fff; font-size: 12px; text-overflow: ellipsis; overflow: hidden; white-space: nowrap; }
.nav-user .role { color: #64748b; font-size: 10px; }

/* 메인 */
.main {
  padding: 28px 32px;
  max-width: 1400px;
}
.page-header {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  margin-bottom: 24px;
  gap: 16px;
  flex-wrap: wrap;
}
.page-title {
  margin: 0;
  font-size: 22px;
  font-weight: 700;
  color: var(--text);
  letter-spacing: -0.4px;
}
.page-subtitle {
  font-size: 13px;
  color: var(--text-3);
  margin-top: 4px;
}
.page-actions { display: flex; gap: 8px; flex-wrap: wrap; }

/* 버튼 */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 14px;
  border-radius: var(--radius-sm);
  font-weight: 600;
  font-size: 13px;
  transition: all 0.15s;
  border: 1px solid transparent;
  white-space: nowrap;
}
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:hover { background: var(--primary-dark); }
.btn-accent { background: var(--accent); color: #fff; }
.btn-accent:hover { background: var(--accent-dark); }
.btn-outline { background: #fff; border-color: var(--border-strong); color: var(--text); }
.btn-outline:hover { background: var(--surface-2); border-color: var(--text-3); }
.btn-danger { background: #fff; border-color: #fecaca; color: var(--danger); }
.btn-danger:hover { background: var(--danger-bg); }
.btn-sm { padding: 4px 10px; font-size: 12px; }
.btn-icon { padding: 6px; }
.btn:disabled { opacity: 0.5; cursor: not-allowed; }

/* 카드 */
.card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  box-shadow: var(--shadow-sm);
  overflow: hidden;
}
.card-header {
  padding: 14px 18px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: var(--surface-2);
}
.card-header .title { font-weight: 700; font-size: 14px; }
.card-body { padding: 18px; }

/* 통계 카드 */
.stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 12px; margin-bottom: 20px; }
.stat {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 14px 16px;
}
.stat .label { font-size: 11px; color: var(--text-3); font-weight: 600; letter-spacing: 0.5px; text-transform: uppercase; }
.stat .value { font-size: 22px; font-weight: 700; margin-top: 4px; color: var(--text); }
.stat .delta { font-size: 11px; color: var(--text-2); margin-top: 2px; }
.stat.accent .value { color: var(--primary); }
.stat.warn .value { color: var(--warn); }

/* 테이블 */
.data-table {
  width: 100%;
  font-size: 13px;
}
.data-table thead th {
  text-align: left;
  padding: 10px 12px;
  background: var(--surface-2);
  color: var(--text-2);
  font-weight: 600;
  font-size: 12px;
  border-bottom: 1px solid var(--border-strong);
  white-space: nowrap;
}
.data-table tbody td {
  padding: 10px 12px;
  border-bottom: 1px solid var(--border);
  vertical-align: middle;
}
.data-table tbody tr { transition: background 0.1s; }
.data-table tbody tr:hover { background: var(--primary-light); cursor: pointer; }
.data-table tbody tr.selected { background: var(--primary-light); }

/* 배지 */
.badge {
  display: inline-flex;
  align-items: center;
  padding: 2px 8px;
  border-radius: 100px;
  font-size: 11px;
  font-weight: 600;
  border: 1px solid transparent;
}
.badge.active { background: #dcfce7; color: #166534; }
.badge.resigned { background: #fee2e2; color: #991b1b; }
.badge.office { background: #e0e7ff; color: #3730a3; }
.badge.field { background: #fef3c7; color: #92400e; }
.badge.gray { background: #f3f4f6; color: #374151; }
.badge.gender-m { background: #dbeafe; color: #1e40af; }
.badge.gender-f { background: #fce7f3; color: #9d174d; }

/* 검색 툴바 */
.toolbar {
  display: flex;
  gap: 8px;
  margin-bottom: 14px;
  flex-wrap: wrap;
  align-items: center;
}
.toolbar .search {
  flex: 1;
  min-width: 240px;
  position: relative;
}
.toolbar .search input { padding-left: 34px; }
.toolbar .search::before {
  content: '🔍';
  position: absolute;
  left: 10px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 13px;
  opacity: 0.5;
}
.toolbar select { max-width: 150px; }

/* 모달 */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.45);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 20px;
  animation: fadeIn 0.15s ease;
}
.modal {
  background: #fff;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  max-width: 600px;
  width: 100%;
  max-height: 85vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  animation: slideUp 0.2s ease;
}
.modal.wide { max-width: 900px; }
.modal-header {
  padding: 18px 22px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.modal-header h3 { margin: 0; font-size: 16px; font-weight: 700; }
.modal-body { padding: 22px; overflow-y: auto; flex: 1; }
.modal-footer {
  padding: 14px 22px;
  border-top: 1px solid var(--border);
  display: flex;
  justify-content: flex-end;
  gap: 8px;
  background: var(--surface-2);
}
.close-btn {
  width: 32px;
  height: 32px;
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  color: var(--text-3);
}
.close-btn:hover { background: var(--surface-2); color: var(--text); }

/* 폼 그리드 */
.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px 16px; }
.form-grid .full { grid-column: 1 / -1; }
.field { margin-bottom: 0; }

/* 토스트 */
.toast {
  position: fixed;
  bottom: 24px;
  right: 24px;
  background: var(--text);
  color: #fff;
  padding: 12px 18px;
  border-radius: var(--radius);
  font-size: 13px;
  box-shadow: var(--shadow-lg);
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.25s;
  z-index: 2000;
  max-width: 360px;
}
.toast.show { opacity: 1; transform: translateY(0); }
.toast.toast-success { background: var(--accent-dark); }
.toast.toast-error { background: var(--danger); }
.toast.toast-warn { background: var(--warn); }

/* 로딩 */
.loading-overlay {
  position: fixed;
  inset: 0;
  background: rgba(255,255,255,0.85);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 3000;
  gap: 12px;
}
.spinner {
  width: 36px;
  height: 36px;
  border: 3px solid var(--border);
  border-top-color: var(--primary);
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
.loading-text { font-size: 13px; color: var(--text-2); font-weight: 500; }

/* 빈 상태 */
.empty-state {
  text-align: center;
  padding: 60px 20px;
  color: var(--text-3);
}
.empty-state .icon { font-size: 40px; margin-bottom: 12px; opacity: 0.4; }
.empty-state .title { font-size: 15px; font-weight: 600; color: var(--text-2); margin-bottom: 4px; }
.empty-state .desc { font-size: 12px; }

/* 파일 드롭 */
.file-drop {
  border: 2px dashed var(--border-strong);
  border-radius: var(--radius);
  padding: 40px;
  text-align: center;
  cursor: pointer;
  transition: all 0.15s;
  background: var(--surface-2);
}
.file-drop:hover, .file-drop.dragover {
  border-color: var(--primary);
  background: var(--primary-light);
}
.file-drop .big-icon { font-size: 36px; margin-bottom: 8px; opacity: 0.6; }
.file-drop .hint { font-size: 13px; color: var(--text-2); }
.file-drop .sub { font-size: 11px; color: var(--text-3); margin-top: 4px; }

/* 매핑 박스 */
.mapping-summary {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 8px;
  margin-top: 12px;
}
.mapping-item {
  padding: 8px 12px;
  background: var(--surface-2);
  border-radius: var(--radius-sm);
  font-size: 12px;
  border-left: 3px solid var(--accent);
}
.mapping-item.unmapped { border-left-color: var(--text-3); opacity: 0.7; }
.mapping-item .src { color: var(--text-3); font-size: 10px; }
.mapping-item .dst { font-weight: 600; color: var(--text); }

.result-banner {
  padding: 12px 16px;
  border-radius: var(--radius);
  margin-bottom: 14px;
  font-size: 13px;
  border: 1px solid;
}
.result-banner.success { background: #dcfce7; border-color: #bbf7d0; color: #166534; }
.result-banner.warn { background: var(--warn-bg); border-color: #fde68a; color: #92400e; }
.result-banner.error { background: var(--danger-bg); border-color: #fecaca; color: #991b1b; }
.result-banner .count { font-weight: 700; font-size: 15px; }

/* 페이지네이션 */
.pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  border-top: 1px solid var(--border);
  background: var(--surface-2);
  font-size: 12px;
}
.pagination .info { color: var(--text-2); }
.pagination .pages { display: flex; gap: 4px; }
.pagination button {
  padding: 4px 10px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-sm);
  background: #fff;
  font-size: 12px;
}
.pagination button:hover:not(:disabled) { border-color: var(--primary); color: var(--primary); }
.pagination button.active { background: var(--primary); color: #fff; border-color: var(--primary); }
.pagination button:disabled { opacity: 0.4; cursor: not-allowed; }

/* 상세 뷰 */
.detail-grid { display: grid; grid-template-columns: 120px 1fr; gap: 8px 16px; font-size: 13px; }
.detail-grid dt { color: var(--text-3); font-weight: 500; }
.detail-grid dd { margin: 0; color: var(--text); font-weight: 500; }

/* 애니메이션 */
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes spin { to { transform: rotate(360deg); } }

.view { display: none; }
.view.active { display: block; }

/* 반응형 */
@media (max-width: 768px) {
  .app-shell { grid-template-columns: 1fr; }
  .sidebar { display: none; }
  .main { padding: 16px; }
  .form-grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>

<!-- ======================================================
     로그인 뷰
====================================================== -->
<div id="loginView">
  <div class="login-card">
    <div class="logo-badge">🏥 BUMIN HOSPITAL · OHMS</div>
    <h1>보건관리시스템</h1>
    <div class="subtitle">산업안전보건법 보건관리자 전용</div>
    
    <form id="loginForm">
      <div class="field">
        <label>이메일</label>
        <input type="email" id="loginEmail" required autocomplete="username" placeholder="clover8477@bumin.co.kr">
      </div>
      <div class="field">
        <label>비밀번호</label>
        <input type="password" id="loginPassword" required autocomplete="current-password" placeholder="••••••••">
      </div>
      <div class="login-error" id="loginError"></div>
      <button type="submit">로그인</button>
    </form>
    
    <div class="login-hint">
      💡 <strong>최초 사용 시:</strong> 관리자 계정이 없으면 아래 '관리자 계정 생성' 클릭<br>
      <button id="showSignupBtn" style="color:var(--primary);font-weight:600;font-size:12px;margin-top:8px;">➕ 관리자 계정 생성</button>
    </div>
  </div>
</div>

<!-- ======================================================
     앱 메인 뷰
====================================================== -->
<div id="appView">
  <div class="app-shell">
    <!-- 사이드바 -->
    <aside class="sidebar">
      <div class="sidebar-brand">
        <div class="name">OHMS</div>
        <div class="tag">부민병원 · 보건관리</div>
      </div>
      
      <div class="nav-item active" data-view="employees">
        <span class="icon">👥</span>
        <span>직원 관리</span>
      </div>
      <div class="nav-item" data-view="import">
        <span class="icon">📥</span>
        <span>엑셀 일괄 업로드</span>
      </div>
      <div class="nav-item" data-view="migrate">
        <span class="icon">🔄</span>
        <span>기존 데이터 이관</span>
      </div>
      <div class="nav-item" data-view="settings">
        <span class="icon">⚙️</span>
        <span>설정</span>
      </div>
      
      <div class="nav-footer">
        <div class="nav-user">
          <div class="avatar" id="userAvatar">–</div>
          <div class="info">
            <div class="email" id="userEmail">—</div>
            <div class="role">관리자</div>
          </div>
        </div>
        <button class="nav-item" id="logoutBtn" style="width:100%">
          <span class="icon">🚪</span>
          <span>로그아웃</span>
        </button>
        <div style="text-align:center;margin-top:10px;">Phase 1 v1.0</div>
      </div>
    </aside>

    <!-- 메인 콘텐츠 -->
    <main class="main">
      
      <!-- 직원 관리 뷰 -->
      <section class="view active" id="view-employees">
        <div class="page-header">
          <div>
            <h1 class="page-title">직원 관리</h1>
            <div class="page-subtitle">부민병원 임직원 인사정보 및 검진 대상자 관리</div>
          </div>
          <div class="page-actions">
            <button class="btn btn-outline" id="btnRefresh">🔄 새로고침</button>
            <button class="btn btn-outline" id="btnExportExcel">📤 엑셀 내보내기</button>
            <button class="btn btn-primary" id="btnAddEmp">➕ 신규 등록</button>
          </div>
        </div>

        <div class="stats" id="employeeStats"></div>

        <div class="card">
          <div class="card-header">
            <div class="title">직원 목록</div>
            <span class="badge gray" id="listCountBadge">0명</span>
          </div>
          <div class="card-body">
            <div class="toolbar">
              <div class="search">
                <input type="text" id="searchInput" placeholder="이름·사번·부서·직무로 검색…">
              </div>
              <select id="filterStatus">
                <option value="active">재직자</option>
                <option value="resigned">퇴사자</option>
                <option value="leave">휴직자</option>
                <option value="all">전체</option>
              </select>
              <select id="filterDept">
                <option value="">전체 부서</option>
              </select>
            </div>
            
            <div style="overflow-x:auto">
              <table class="data-table">
                <thead>
                  <tr>
                    <th>사번</th>
                    <th>이름</th>
                    <th>부서</th>
                    <th>직무</th>
                    <th>생년월일</th>
                    <th>성별</th>
                    <th>입사일</th>
                    <th>상태</th>
                    <th></th>
                  </tr>
                </thead>
                <tbody id="empTableBody"></tbody>
              </table>
              <div id="emptyState" class="empty-state" style="display:none">
                <div class="icon">📋</div>
                <div class="title">등록된 직원이 없습니다</div>
                <div class="desc">'기존 데이터 이관' 메뉴에서 엑셀 파일을 업로드해 시작하세요</div>
              </div>
            </div>
          </div>
          
          <div class="pagination" id="paginationBar" style="display:none">
            <div class="info" id="pageInfo"></div>
            <div class="pages" id="pageButtons"></div>
          </div>
        </div>
      </section>

      <!-- 엑셀 일괄 업로드 뷰 -->
      <section class="view" id="view-import">
        <div class="page-header">
          <div>
            <h1 class="page-title">엑셀 일괄 업로드</h1>
            <div class="page-subtitle">검진기관별 상이한 포맷도 사번 기준으로 자동 매칭됩니다</div>
          </div>
        </div>

        <div class="card" style="margin-bottom:16px">
          <div class="card-header">
            <div class="title">① 파일 업로드</div>
          </div>
          <div class="card-body">
            <input type="file" id="fileInput" accept=".xlsx,.xls,.csv" style="display:none">
            <div class="file-drop" id="fileDrop">
              <div class="big-icon">📊</div>
              <div class="hint"><strong>엑셀 파일을 드래그</strong>하거나 <strong>클릭</strong>해서 선택</div>
              <div class="sub">xlsx, xls, csv 지원 · 사번 컬럼이 있는 파일만 가능</div>
            </div>
            <div id="fileInfo" style="margin-top:12px"></div>
          </div>
        </div>

        <div class="card" id="mappingCard" style="display:none;margin-bottom:16px">
          <div class="card-header">
            <div class="title">② 컬럼 자동 인식 결과</div>
          </div>
          <div class="card-body">
            <div id="mappingInfo"></div>
          </div>
        </div>

        <div class="card" id="previewCard" style="display:none;margin-bottom:16px">
          <div class="card-header">
            <div class="title">③ 데이터 미리보기 (최대 5행)</div>
          </div>
          <div class="card-body" style="overflow-x:auto;padding:0">
            <table class="data-table" id="previewTable"></table>
          </div>
        </div>

        <div id="importActions" style="display:none;text-align:right">
          <button class="btn btn-outline" id="btnCancelImport">취소</button>
          <button class="btn btn-accent" id="btnConfirmImport">✓ 데이터베이스에 저장</button>
        </div>
      </section>

      <!-- 기존 데이터 이관 뷰 -->
      <section class="view" id="view-migrate">
        <div class="page-header">
          <div>
            <h1 class="page-title">기존 데이터 이관</h1>
            <div class="page-subtitle">기존 부민 건강검진 현황판 엑셀을 한번에 Firebase로 업로드합니다</div>
          </div>
        </div>

        <div class="card">
          <div class="card-body">
            <div class="result-banner warn">
              <strong>⚠️ 최초 1회만 실행하세요</strong><br>
              이미 이관된 상태에서 다시 실행하면 기존 데이터가 덮어써집니다. (업데이트 시점 기준)
            </div>
            
            <p style="font-size:13px;color:var(--text-2);margin:16px 0">
              업로드된 <strong>1__부민_건강검진_현황판_업로드.xlsx</strong> 형식을 자동 파싱해 1,543명의 인사정보를 Firebase에 저장합니다.
              검진 기록은 Phase 2에서 이관합니다.
            </p>

            <input type="file" id="migrateFileInput" accept=".xlsx,.xls" style="display:none">
            <div class="file-drop" id="migrateDrop">
              <div class="big-icon">🏥</div>
              <div class="hint"><strong>부민 건강검진 현황판 엑셀</strong>을 업로드하세요</div>
              <div class="sub">3개 시트(채용검진/일반검진/특수건강검진)가 모두 있어야 합니다</div>
            </div>
            
            <div id="migrateResult" style="margin-top:16px"></div>
          </div>
        </div>
      </section>

      <!-- 설정 뷰 -->
      <section class="view" id="view-settings">
        <div class="page-header">
          <div>
            <h1 class="page-title">설정</h1>
            <div class="page-subtitle">시스템 연결 상태 및 환경 설정</div>
          </div>
        </div>

        <div class="card" style="margin-bottom:14px">
          <div class="card-header"><div class="title">🔥 Firebase 연결</div></div>
          <div class="card-body">
            <dl class="detail-grid">
              <dt>프로젝트 ID</dt><dd>bumin-ohms</dd>
              <dt>데이터베이스</dt><dd id="dbStatus">확인 중…</dd>
              <dt>리전</dt><dd>asia-northeast3 (Seoul)</dd>
              <dt>플랜</dt><dd>Spark (무료)</dd>
            </dl>
          </div>
        </div>

        <div class="card" style="margin-bottom:14px">
          <div class="card-header"><div class="title">📊 현재 데이터 규모</div></div>
          <div class="card-body">
            <div class="stats" id="dbStats"></div>
            <button class="btn btn-outline btn-sm" id="btnRefreshStats">🔄 통계 갱신</button>
          </div>
        </div>

        <div class="card" style="margin-bottom:14px">
          <div class="card-header"><div class="title">🛡️ 보안 규칙 (Firestore Rules)</div></div>
          <div class="card-body">
            <p style="font-size:13px;color:var(--text-2);margin-bottom:12px">
              Firebase Console → Firestore → Rules 탭에 아래 규칙을 붙여넣어주세요. 
              <strong style="color:var(--danger)">현재는 테스트 모드(30일 후 차단)</strong>입니다.
            </p>
<pre style="background:#1e293b;color:#e2e8f0;padding:14px;border-radius:var(--radius-sm);font-size:12px;overflow-x:auto;line-height:1.6"><code>rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // 로그인한 사용자만 모든 문서 읽기/쓰기 가능
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}</code></pre>
          </div>
        </div>

        <div class="card" style="margin-bottom:14px">
          <div class="card-header"><div class="title">🔧 날짜 형식 일괄 정정</div></div>
          <div class="card-body">
            <p style="font-size:13px;color:var(--text-2);margin-bottom:12px">
              <strong>입사일/생년월일이 "4/7/25"처럼 표시</strong>되는 경우 클릭하세요. 
              전체 직원의 날짜 필드를 YYYY-MM-DD 형식으로 자동 변환합니다.
            </p>
            <button class="btn btn-primary" id="btnFixDates">📅 날짜 일괄 정정 실행</button>
            <div id="dateFixResult" style="margin-top:12px"></div>
          </div>
        </div>

        <div class="card">
          <div class="card-header"><div class="title">🚨 데이터베이스 초기화</div></div>
          <div class="card-body">
            <p style="font-size:13px;color:var(--text-2);margin-bottom:12px">
              <strong style="color:var(--danger)">주의:</strong> 모든 직원 데이터가 영구 삭제됩니다. 되돌릴 수 없습니다.
            </p>
            <button class="btn btn-danger" id="btnResetDB">🗑️ 전체 직원 데이터 삭제</button>
          </div>
        </div>
      </section>
      
    </main>
  </div>
</div>

<!-- ======================================================
     공통 UI: 로딩 오버레이, 토스트
====================================================== -->
<div class="loading-overlay" id="loadingOverlay" style="display:none">
  <div class="spinner"></div>
  <div class="loading-text" id="loadingText">처리 중…</div>
</div>


<!-- ======================================================
     JavaScript - 모듈 네임스페이스 구조
====================================================== -->
<script type="module">

// ============================================================
// 1. Firebase 초기화
// ============================================================
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import {
  getFirestore, collection, doc, getDoc, getDocs, setDoc, addDoc, updateDoc, deleteDoc,
  query, where, orderBy, limit, writeBatch, serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
import {
  getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged, createUserWithEmailAndPassword
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

const firebaseConfig = {
  apiKey: "AIzaSyAyZRwTV5JXPAKvcH9M2ZYJ3NSjph8PabU",
  authDomain: "bumin-ohms.firebaseapp.com",
  projectId: "bumin-ohms",
  storageBucket: "bumin-ohms.firebasestorage.app",
  messagingSenderId: "269372452715",
  appId: "1:269372452715:web:c99e4f46163d48d434e62e"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);


// ============================================================
// 2. 유틸리티
// ============================================================
const $ = (s, el = document) => el.querySelector(s);
const $$ = (s, el = document) => el.querySelectorAll(s);
const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));

function formatDate(date) {
  if (!date) return '';
  // Date 객체면 바로 포맷
  if (date instanceof Date) {
    if (isNaN(date)) return '';
    return `${date.getFullYear()}-${String(date.getMonth()+1).padStart(2,'0')}-${String(date.getDate()).padStart(2,'0')}`;
  }
  if (typeof date === 'string') {
    // 이미 YYYY-MM-DD 형식이면 앞 10자만 잘라 반환
    if (/^\d{4}-\d{2}-\d{2}/.test(date)) return date.substring(0, 10);
    // 나머지 문자열은 parseExcelDate로 정규화 시도
    const parsed = parseExcelDate(date);
    if (parsed) return parsed;
    return '';
  }
  if (date.toDate) date = date.toDate(); // Firestore Timestamp
  const d = new Date(date);
  if (isNaN(d)) return '';
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
}

function parseExcelDate(value) {
  if (value == null || value === '') return null;
  
  // Date 객체
  if (value instanceof Date) {
    if (isNaN(value)) return null;
    return `${value.getFullYear()}-${String(value.getMonth()+1).padStart(2,'0')}-${String(value.getDate()).padStart(2,'0')}`;
  }
  
  const s = String(value).trim();
  if (!s) return null;
  
  // 20260213 형태 (8자리 숫자)
  if (/^\d{8}$/.test(s)) {
    const y = parseInt(s.substring(0, 4));
    const m = parseInt(s.substring(4, 6));
    const d = parseInt(s.substring(6, 8));
    if (y >= 1900 && y <= 2100 && m >= 1 && m <= 12 && d >= 1 && d <= 31) {
      return `${s.substring(0,4)}-${s.substring(4,6)}-${s.substring(6,8)}`;
    }
  }
  
  // YYYY-MM-DD 또는 YYYY/MM/DD (4자리 연도가 앞)
  let m = s.match(/^(\d{4})[-/.](\d{1,2})[-/.](\d{1,2})/);
  if (m) {
    return `${m[1]}-${String(m[2]).padStart(2,'0')}-${String(m[3]).padStart(2,'0')}`;
  }
  
  // M/D/YY or M/D/YYYY (미국식, 2자리 연도 주의)
  m = s.match(/^(\d{1,2})\/(\d{1,2})\/(\d{2,4})$/);
  if (m) {
    let month = parseInt(m[1]);
    let day = parseInt(m[2]);
    let year = parseInt(m[3]);
    // 2자리 연도 해석: 0~49 → 2000~2049, 50~99 → 1950~1999
    if (year < 100) {
      year = year < 50 ? 2000 + year : 1900 + year;
    }
    // 한국 기업이라 MM/DD 형식일 수도 있고 DD/MM일 수도 있음
    // 입사일/생년월일은 MM/DD 가정 (첫 숫자가 12보다 크면 DD/MM)
    if (month > 12 && day <= 12) {
      [month, day] = [day, month];
    }
    if (year >= 1900 && year <= 2100 && month >= 1 && month <= 12 && day >= 1 && day <= 31) {
      return `${year}-${String(month).padStart(2,'0')}-${String(day).padStart(2,'0')}`;
    }
  }
  
  // YYYY.MM.DD 형태
  m = s.match(/^(\d{4})\.(\d{1,2})\.(\d{1,2})/);
  if (m) {
    return `${m[1]}-${String(m[2]).padStart(2,'0')}-${String(m[3]).padStart(2,'0')}`;
  }
  
  // 엑셀 serial number (1900-01-01 기준)
  const n = Number(s);
  if (!isNaN(n) && n > 25569 && n < 60000) {
    const ms = (n - 25569) * 86400 * 1000;
    const d = new Date(ms);
    return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
  }
  
  // 마지막 시도: new Date()로 파싱
  try {
    const d = new Date(s);
    if (!isNaN(d) && d.getFullYear() >= 1900 && d.getFullYear() <= 2100) {
      return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
    }
  } catch (e) {}
  
  return null;
}

function normalize(s) { return String(s||'').replace(/\s+/g,'').toLowerCase(); }

function isOfficeJob(jobTitle) {
  const officeKeywords = ['사무', '행정', '콜센터', '기획', '경영', '재무', '인사', '총무', '심사', '의료정보', '구매', '법인', '전략', '원무'];
  return officeKeywords.some(k => String(jobTitle||'').includes(k));
}

function toast(msg, type='info', duration=3000) {
  const el = document.createElement('div');
  el.className = `toast toast-${type}`;
  el.textContent = msg;
  document.body.appendChild(el);
  requestAnimationFrame(() => el.classList.add('show'));
  setTimeout(() => {
    el.classList.remove('show');
    setTimeout(() => el.remove(), 300);
  }, duration);
}

function showLoading(text='처리 중…') {
  $('#loadingText').textContent = text;
  $('#loadingOverlay').style.display = 'flex';
}
function hideLoading() { $('#loadingOverlay').style.display = 'none'; }


// ============================================================
// 3. 인증 (Auth) 네임스페이스
// ============================================================
const Auth = {
  async login(email, password) {
    const cred = await signInWithEmailAndPassword(auth, email, password);
    return cred.user;
  },
  
  async signup(email, password) {
    const cred = await createUserWithEmailAndPassword(auth, email, password);
    return cred.user;
  },
  
  async logout() {
    await signOut(auth);
  },
  
  onChange(callback) {
    return onAuthStateChanged(auth, callback);
  }
};


// ============================================================
// 4. DB 접근 (DB) 네임스페이스
// ============================================================
const COL = {
  EMPLOYEES: 'employees',
  EXAMS: 'exams',
  COUNSELING: 'counseling',
  SETTINGS: 'settings'
};

const DB = {
  // --- 직원 ---
  async getEmployee(empCode) {
    if (!empCode) return null;
    const ref = doc(db, COL.EMPLOYEES, String(empCode));
    const snap = await getDoc(ref);
    return snap.exists() ? { id: snap.id, ...snap.data() } : null;
  },
  
  async getAllEmployees() {
    const snap = await getDocs(collection(db, COL.EMPLOYEES));
    return snap.docs.map(d => ({ id: d.id, ...d.data() }));
  },
  
  async saveEmployee(emp) {
    if (!emp.empCode) throw new Error('사번 필수');
    const ref = doc(db, COL.EMPLOYEES, String(emp.empCode));
    // undefined는 Firestore에서 에러 발생하므로 제거
    const clean = {};
    Object.keys(emp).forEach(k => {
      if (emp[k] !== undefined && emp[k] !== '') clean[k] = emp[k];
    });
    await setDoc(ref, { ...clean, updatedAt: serverTimestamp() }, { merge: true });
    return emp.empCode;
  },
  
  async bulkSaveEmployees(employees, onProgress) {
    const results = { success: 0, fail: 0, errors: [] };
    const chunks = [];
    for (let i = 0; i < employees.length; i += 400) chunks.push(employees.slice(i, i + 400));
    
    let done = 0;
    for (const chunk of chunks) {
      const batch = writeBatch(db);
      for (const emp of chunk) {
        if (!emp.empCode) { results.fail++; results.errors.push({emp, reason:'사번 없음'}); continue; }
        const clean = {};
        Object.keys(emp).forEach(k => {
          if (emp[k] !== undefined && emp[k] !== '' && emp[k] !== null) clean[k] = emp[k];
        });
        const ref = doc(db, COL.EMPLOYEES, String(emp.empCode));
        batch.set(ref, { ...clean, updatedAt: serverTimestamp() }, { merge: true });
        results.success++;
      }
      try {
        await batch.commit();
      } catch (e) {
        results.fail += chunk.length;
        results.success -= chunk.length;
        results.errors.push({ reason: e.message, chunk: chunk.length });
      }
      done += chunk.length;
      if (onProgress) onProgress(done, employees.length);
    }
    return results;
  },
  
  async deleteEmployee(empCode) {
    await deleteDoc(doc(db, COL.EMPLOYEES, String(empCode)));
  },
  
  async deleteAllEmployees() {
    const snap = await getDocs(collection(db, COL.EMPLOYEES));
    const chunks = [];
    const docs = snap.docs;
    for (let i = 0; i < docs.length; i += 400) chunks.push(docs.slice(i, i + 400));
    
    let count = 0;
    for (const chunk of chunks) {
      const batch = writeBatch(db);
      chunk.forEach(d => batch.delete(d.ref));
      await batch.commit();
      count += chunk.length;
    }
    return count;
  },
  
  async countCollection(colName) {
    const snap = await getDocs(collection(db, colName));
    return snap.size;
  },
  
  /**
   * 전체 직원의 날짜 필드를 YYYY-MM-DD 형식으로 일괄 정규화
   */
  async fixAllDates(onProgress) {
    const snap = await getDocs(collection(db, COL.EMPLOYEES));
    const dateFields = ['hireDate', 'birthDate', 'resignDate', 'transferDate'];
    const stats = { total: snap.size, fixed: 0, skipped: 0, samples: [] };
    
    const chunks = [];
    const docs = snap.docs;
    for (let i = 0; i < docs.length; i += 400) chunks.push(docs.slice(i, i + 400));
    
    let done = 0;
    for (const chunk of chunks) {
      const batch = writeBatch(db);
      for (const d of chunk) {
        const data = d.data();
        const updates = {};
        let hasChange = false;
        
        for (const f of dateFields) {
          const v = data[f];
          if (!v) continue;
          
          // 이미 YYYY-MM-DD 형식이면 스킵
          if (typeof v === 'string' && /^\d{4}-\d{2}-\d{2}$/.test(v)) continue;
          // 9999-12-31은 퇴사일 불명이므로 스킵
          if (v === '9999-12-31') continue;
          
          const fixed = parseExcelDate(v);
          if (fixed && fixed !== v) {
            updates[f] = fixed;
            hasChange = true;
            if (stats.samples.length < 5) {
              stats.samples.push({ name: data.name, field: f, before: String(v), after: fixed });
            }
          }
        }
        
        if (hasChange) {
          batch.update(d.ref, updates);
          stats.fixed++;
        } else {
          stats.skipped++;
        }
      }
      await batch.commit();
      done += chunk.length;
      if (onProgress) onProgress(done, snap.size);
    }
    return stats;
  }
};


// ============================================================
// 5. 지능형 엑셀 파서 (Import) 네임스페이스
// ============================================================
const FIELD_SYNONYMS = {
  empCode: ['사번','사원코드','사원번호','직원번호','직원코드','사원ID','ID','empno','emp_code','employee_id','번호'],
  name: ['이름','성명','사원명','직원명','대상자','name'],
  department: ['부서','부서명','소속','소속부서','근무부서','department','dept'],
  jobTitle: ['직무','직무명','직종','직책','직위','job','position'],
  hireDate: ['입사일','입사일자','채용일','임용일','hireDate'],
  resignDate: ['퇴사일','퇴사일자','퇴직일','퇴직일자','resignDate'],
  transferDate: ['전입일','현직전입일','배치일','배치일자','전보일'],
  gender: ['성별','gender','sex'],
  email: ['이메일','EMAIL','email','메일','E-mail'],
  phone: ['연락처','전화번호','휴대폰','핸드폰','phone','mobile','HP'],
  birthDate: ['생년월일','생일','birthdate','DOB'],
  hazard: ['유해인자','유해요인','노출인자','대상유해인자'],
};

const Import = {
  matchHeader(header) {
    if (!header) return null;
    const h = normalize(header);
    for (const [field, syns] of Object.entries(FIELD_SYNONYMS)) {
      if (syns.some(s => normalize(s) === h)) return field;
    }
    for (const [field, syns] of Object.entries(FIELD_SYNONYMS)) {
      if (syns.some(s => h.includes(normalize(s)) || (normalize(s).length >= 3 && normalize(s).includes(h)))) return field;
    }
    return null;
  },
  
  async parseFile(file) {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        try {
          const data = new Uint8Array(e.target.result);
          const wb = XLSX.read(data, { type: 'array', cellDates: true });
          const sheets = {};
          for (const name of wb.SheetNames) {
            sheets[name] = XLSX.utils.sheet_to_json(wb.Sheets[name], {
              header: 1, defval: null, raw: false
            });
          }
          resolve(sheets);
        } catch (err) { reject(err); }
      };
      reader.onerror = () => reject(reader.error);
      reader.readAsArrayBuffer(file);
    });
  },
  
  detectHeaderRow(rows) {
    let best = { idx: 0, score: 0, headers: rows[0] || [] };
    const maxScan = Math.min(10, rows.length);
    for (let i = 0; i < maxScan; i++) {
      const row = rows[i] || [];
      let score = 0;
      for (const cell of row) if (this.matchHeader(cell)) score++;
      if (score > best.score) best = { idx: i, score, headers: row };
    }
    return best;
  },
  
  analyzeSheet(rows) {
    const hd = this.detectHeaderRow(rows);
    const headers = hd.headers.map(h => String(h ?? '').trim());
    const mapping = {};
    const unmapped = [];
    headers.forEach((h, i) => {
      if (!h) return;
      const f = this.matchHeader(h);
      if (f) mapping[i] = f;
      else unmapped.push({ index: i, name: h });
    });
    const dataRows = rows.slice(hd.idx + 1).filter(r => r && r.some(c => c != null && c !== ''));
    return { headerRowIndex: hd.idx, headers, mapping, unmapped, dataRows };
  },
  
  applyMapping(dataRows, mapping, extraData = {}) {
    const records = [];
    const errors = [];
    for (let i = 0; i < dataRows.length; i++) {
      const row = dataRows[i];
      const rec = { ...extraData };
      for (let col = 0; col < row.length; col++) {
        const cell = row[col];
        if (cell == null || cell === '') continue;
        const field = mapping[col];
        if (field) rec[field] = cell;
      }
      // 날짜 변환
      ['examDate','hireDate','resignDate','transferDate','birthDate'].forEach(f => {
        if (rec[f]) { const p = parseExcelDate(rec[f]); if (p) rec[f] = p; }
      });
      // 사번 정규화
      if (rec.empCode) rec.empCode = String(rec.empCode).trim();
      if (!rec.empCode) {
        errors.push({ row: i + 2, reason: '사번 없음' });
        continue;
      }
      records.push(rec);
    }
    return { records, errors };
  }
};


// ============================================================
// 6. 직원 관리 (Employees) 네임스페이스
// ============================================================
const Employees = {
  list: [],
  filteredList: [],
  currentPage: 1,
  pageSize: 50,
  
  async loadAll() {
    showLoading('직원 목록 불러오는 중…');
    try {
      this.list = await DB.getAllEmployees();
      this.list.sort((a, b) => {
        // 재직자 우선, 그 다음 이름순
        if (!!a.resignDate !== !!b.resignDate) return a.resignDate ? 1 : -1;
        return (a.name || '').localeCompare(b.name || '', 'ko');
      });
      this.applyFilters();
      this.renderStats();
      this.renderDepartmentFilter();
    } catch (e) {
      console.error(e);
      toast('직원 목록 조회 실패: ' + e.message, 'error');
    } finally {
      hideLoading();
    }
  },
  
  applyFilters() {
    const q = normalize($('#searchInput').value);
    const status = $('#filterStatus').value;
    const dept = $('#filterDept').value;
    
    this.filteredList = this.list.filter(e => {
      const isResigned = !!e.resignDate;
      const isLeave = e.status === 'leave';
      
      // 상태 필터
      if (status === 'active' && (isResigned || isLeave)) return false;
      if (status === 'resigned' && !isResigned) return false;
      if (status === 'leave' && !isLeave) return false;
      // 'all'은 전체 통과
      
      // 부서 필터
      if (dept && e.department !== dept) return false;
      
      // 검색어 필터
      if (q) {
        const hay = normalize(`${e.empCode} ${e.name} ${e.department} ${e.jobTitle}`);
        if (!hay.includes(q)) return false;
      }
      return true;
    });
    
    this.currentPage = 1;
    this.renderTable();
  },
  
  renderTable() {
    const start = (this.currentPage - 1) * this.pageSize;
    const end = start + this.pageSize;
    const pageData = this.filteredList.slice(start, end);
    
    $('#listCountBadge').textContent = `${this.filteredList.length}명`;
    
    if (this.filteredList.length === 0) {
      $('#empTableBody').innerHTML = '';
      $('#emptyState').style.display = 'block';
      $('#paginationBar').style.display = 'none';
      return;
    }
    $('#emptyState').style.display = 'none';
    
    const html = pageData.map(e => {
      const isResigned = !!e.resignDate;
      const isUnknownResign = e.resignDate === '9999-12-31';
      const isLeave = e.status === 'leave';
      
      let statusBadge;
      if (isLeave) {
        statusBadge = '<span class="badge gray">휴직</span>';
      } else if (isResigned && isUnknownResign) {
        statusBadge = `<span class="badge resigned">퇴사 (일자불명)</span>`;
      } else if (isResigned) {
        statusBadge = `<span class="badge resigned">퇴사 ${formatDate(e.resignDate)}</span>`;
      } else {
        statusBadge = '<span class="badge active">재직</span>';
      }
      
      // 사무/현업 배지는 표시하지 않음 (상태 컬럼에 재직정보 있음)
      
      const genderBadge = e.gender === '남'
        ? '<span class="badge gender-m">남</span>'
        : e.gender === '여'
        ? '<span class="badge gender-f">여</span>'
        : '<span style="color:var(--text-3)">-</span>';
      
      return `
        <tr data-emp="${esc(e.empCode)}">
          <td style="font-family:monospace;font-size:12px">${esc(e.empCode)}</td>
          <td><strong>${esc(e.name || '-')}</strong></td>
          <td>${esc(e.department || '-')}</td>
          <td>${esc(e.jobTitle || '-')}</td>
          <td style="font-family:monospace;font-size:12px">${formatDate(e.birthDate) || '-'}</td>
          <td>${genderBadge}</td>
          <td style="font-family:monospace;font-size:12px">${formatDate(e.hireDate) || '-'}</td>
          <td>${statusBadge}</td>
          <td style="text-align:right">
            <button class="btn btn-outline btn-sm" data-action="edit" data-emp="${esc(e.empCode)}">수정</button>
          </td>
        </tr>
      `;
    }).join('');
    
    $('#empTableBody').innerHTML = html;
    
    // 페이지네이션
    this.renderPagination();
    
    // 행 클릭 핸들러
    $$('#empTableBody tr').forEach(tr => {
      tr.addEventListener('click', (ev) => {
        if (ev.target.closest('button')) return;
        Employees.showDetail(tr.dataset.emp);
      });
    });
    $$('#empTableBody button[data-action="edit"]').forEach(btn => {
      btn.addEventListener('click', (ev) => {
        ev.stopPropagation();
        Employees.showEditModal(btn.dataset.emp);
      });
    });
  },
  
  renderPagination() {
    const total = this.filteredList.length;
    const totalPages = Math.ceil(total / this.pageSize);
    const bar = $('#paginationBar');
    
    if (totalPages <= 1) {
      bar.style.display = 'none';
      return;
    }
    bar.style.display = 'flex';
    
    const start = (this.currentPage - 1) * this.pageSize + 1;
    const end = Math.min(start + this.pageSize - 1, total);
    $('#pageInfo').textContent = `${start.toLocaleString()}–${end.toLocaleString()} / ${total.toLocaleString()}명`;
    
    const btns = [];
    btns.push(`<button data-page="${this.currentPage - 1}" ${this.currentPage === 1 ? 'disabled' : ''}>‹</button>`);
    
    const maxShow = 7;
    let startP = Math.max(1, this.currentPage - Math.floor(maxShow / 2));
    let endP = Math.min(totalPages, startP + maxShow - 1);
    startP = Math.max(1, endP - maxShow + 1);
    
    if (startP > 1) {
      btns.push(`<button data-page="1">1</button>`);
      if (startP > 2) btns.push(`<span style="padding:4px">…</span>`);
    }
    for (let p = startP; p <= endP; p++) {
      btns.push(`<button data-page="${p}" class="${p === this.currentPage ? 'active' : ''}">${p}</button>`);
    }
    if (endP < totalPages) {
      if (endP < totalPages - 1) btns.push(`<span style="padding:4px">…</span>`);
      btns.push(`<button data-page="${totalPages}">${totalPages}</button>`);
    }
    
    btns.push(`<button data-page="${this.currentPage + 1}" ${this.currentPage === totalPages ? 'disabled' : ''}>›</button>`);
    
    $('#pageButtons').innerHTML = btns.join('');
    $$('#pageButtons button[data-page]').forEach(b => {
      b.addEventListener('click', () => {
        const p = parseInt(b.dataset.page);
        if (p >= 1 && p <= totalPages) {
          this.currentPage = p;
          this.renderTable();
          window.scrollTo({ top: 0, behavior: 'smooth' });
        }
      });
    });
  },
  
  renderStats() {
    const total = this.list.length;
    const active = this.list.filter(e => !e.resignDate && e.status !== 'leave').length;
    const resigned = this.list.filter(e => !!e.resignDate).length;
    const leave = this.list.filter(e => e.status === 'leave').length;
    const male = this.list.filter(e => !e.resignDate && e.status !== 'leave' && e.gender === '남').length;
    const female = this.list.filter(e => !e.resignDate && e.status !== 'leave' && e.gender === '여').length;
    const office = this.list.filter(e => !e.resignDate && e.status !== 'leave' && isOfficeJob(e.jobTitle)).length;
    
    $('#employeeStats').innerHTML = `
      <div class="stat accent">
        <div class="label">전체 등록</div>
        <div class="value">${total.toLocaleString()}</div>
        <div class="delta">직원 전체</div>
      </div>
      <div class="stat">
        <div class="label">재직자</div>
        <div class="value">${active.toLocaleString()}</div>
        <div class="delta">일반검진 대상</div>
      </div>
      <div class="stat warn">
        <div class="label">퇴사자</div>
        <div class="value">${resigned.toLocaleString()}</div>
        <div class="delta">이력 보존 중</div>
      </div>
      ${leave > 0 ? `<div class="stat">
        <div class="label">휴직자</div>
        <div class="value">${leave.toLocaleString()}</div>
        <div class="delta">복직 시 재분류</div>
      </div>` : ''}
      <div class="stat">
        <div class="label">성별 (재직)</div>
        <div class="value" style="font-size:18px">남 ${male.toLocaleString()} / 여 ${female.toLocaleString()}</div>
        <div class="delta">사무직 ${office.toLocaleString()}명 포함</div>
      </div>
    `;
  },
  
  renderDepartmentFilter() {
    const depts = [...new Set(this.list.map(e => e.department).filter(Boolean))].sort();
    const select = $('#filterDept');
    const current = select.value;
    select.innerHTML = '<option value="">전체 부서</option>' + 
      depts.map(d => `<option value="${esc(d)}">${esc(d)}</option>`).join('');
    if (current) select.value = current;
  },
  
  showDetail(empCode) {
    const emp = this.list.find(e => String(e.empCode) === String(empCode));
    if (!emp) return;
    
    const isUnknownResign = emp.resignDate === '9999-12-31';
    let statusHtml;
    if (emp.status === 'leave') {
      statusHtml = '<span class="badge gray">휴직</span>' + (emp.resignNote ? ` <small>(${esc(emp.resignNote)})</small>` : '');
    } else if (emp.resignDate && isUnknownResign) {
      statusHtml = `<span class="badge resigned">퇴사 (일자불명)</span>` + (emp.resignNote ? ` <small>(${esc(emp.resignNote)})</small>` : '');
    } else if (emp.resignDate) {
      statusHtml = `<span class="badge resigned">${formatDate(emp.resignDate)}</span>`;
    } else {
      statusHtml = '<span class="badge active">재직중</span>';
    }
    
    Modal.open({
      title: `${emp.name} (${emp.empCode})`,
      body: `
        <dl class="detail-grid">
          <dt>사번</dt><dd style="font-family:monospace">${esc(emp.empCode)}</dd>
          <dt>이름</dt><dd>${esc(emp.name || '-')}</dd>
          <dt>성별</dt><dd>${esc(emp.gender || '-')}</dd>
          <dt>생년월일</dt><dd>${formatDate(emp.birthDate) || '-'}</dd>
          <dt>부서</dt><dd>${esc(emp.department || '-')}</dd>
          <dt>직무</dt><dd>${esc(emp.jobTitle || '-')}</dd>
          <dt>입사일</dt><dd>${formatDate(emp.hireDate) || '-'}</dd>
          <dt>현직전입일</dt><dd>${formatDate(emp.transferDate) || '-'}</dd>
          <dt>퇴사일</dt><dd>${statusHtml}</dd>
          <dt>유해인자</dt><dd>${esc(emp.hazard || '-')}</dd>
          <dt>이메일</dt><dd>${esc(emp.email || '-')}</dd>
          <dt>연락처</dt><dd>${esc(emp.phone || '-')}</dd>
        </dl>
      `,
      actions: [
        { text: '수정', variant: 'primary', handler: () => { Modal.close(); this.showEditModal(empCode); } },
        { text: '닫기', variant: 'outline', handler: () => Modal.close() },
      ]
    });
  },
  
  showEditModal(empCode) {
    const emp = empCode ? this.list.find(e => String(e.empCode) === String(empCode)) : {};
    const isNew = !empCode;
    
    Modal.open({
      title: isNew ? '신규 직원 등록' : `직원 정보 수정 - ${emp.name}`,
      body: `
        <form id="empForm">
          <div class="form-grid">
            <div class="field">
              <label>사번 *</label>
              <input name="empCode" required value="${esc(emp.empCode || '')}" ${isNew ? '' : 'readonly'}>
            </div>
            <div class="field">
              <label>이름 *</label>
              <input name="name" required value="${esc(emp.name || '')}">
            </div>
            <div class="field">
              <label>성별</label>
              <select name="gender">
                <option value="">-</option>
                <option value="남" ${emp.gender==='남'?'selected':''}>남</option>
                <option value="여" ${emp.gender==='여'?'selected':''}>여</option>
              </select>
            </div>
            <div class="field">
              <label>생년월일</label>
              <input type="date" name="birthDate" value="${formatDate(emp.birthDate)}">
            </div>
            <div class="field">
              <label>부서</label>
              <input name="department" value="${esc(emp.department || '')}">
            </div>
            <div class="field">
              <label>직무</label>
              <input name="jobTitle" value="${esc(emp.jobTitle || '')}">
            </div>
            <div class="field">
              <label>입사일</label>
              <input type="date" name="hireDate" value="${formatDate(emp.hireDate)}">
            </div>
            <div class="field">
              <label>현직전입일</label>
              <input type="date" name="transferDate" value="${formatDate(emp.transferDate)}">
            </div>
            <div class="field">
              <label>퇴사일</label>
              <input type="date" name="resignDate" value="${formatDate(emp.resignDate)}">
            </div>
            <div class="field">
              <label>이메일</label>
              <input type="email" name="email" value="${esc(emp.email || '')}">
            </div>
            <div class="field">
              <label>연락처</label>
              <input name="phone" value="${esc(emp.phone || '')}">
            </div>
            <div class="field full">
              <label>유해인자 (특수검진 대상)</label>
              <input name="hazard" value="${esc(emp.hazard || '')}" placeholder="예: 방사선, 포름알데히드, 야간">
            </div>
          </div>
        </form>
      `,
      actions: [
        ...(isNew ? [] : [{ 
          text: '🗑 삭제', variant: 'danger',
          handler: async () => {
            if (!confirm(`${emp.name} (${emp.empCode}) 정보를 영구 삭제합니다. 계속하시겠습니까?`)) return;
            showLoading('삭제 중…');
            try {
              await DB.deleteEmployee(emp.empCode);
              toast('삭제 완료', 'success');
              Modal.close();
              this.loadAll();
            } catch (e) { toast('삭제 실패: ' + e.message, 'error'); }
            finally { hideLoading(); }
          }
        }]),
        { text: '취소', variant: 'outline', handler: () => Modal.close() },
        {
          text: '저장', variant: 'accent',
          handler: async () => {
            const form = $('#empForm');
            if (!form.checkValidity()) { form.reportValidity(); return; }
            const fd = new FormData(form);
            const data = Object.fromEntries(fd.entries());
            // 빈 값은 제거
            Object.keys(data).forEach(k => { if (!data[k]) delete data[k]; });
            
            showLoading('저장 중…');
            try {
              await DB.saveEmployee(data);
              toast('저장 완료', 'success');
              Modal.close();
              this.loadAll();
            } catch (e) {
              toast('저장 실패: ' + e.message, 'error');
            } finally { hideLoading(); }
          }
        }
      ]
    });
  },
  
  exportToExcel() {
    if (this.filteredList.length === 0) {
      toast('내보낼 데이터가 없습니다', 'warn');
      return;
    }
    const data = this.filteredList.map(e => {
      const isUnknownResign = e.resignDate === '9999-12-31';
      let statusText = '재직';
      if (e.status === 'leave') statusText = '휴직';
      else if (e.resignDate && isUnknownResign) statusText = `퇴사 (${e.resignNote || '일자불명'})`;
      else if (e.resignDate) statusText = '퇴사';
      
      return {
        '사번': e.empCode,
        '이름': e.name,
        '성별': e.gender || '',
        '생년월일': formatDate(e.birthDate),
        '부서': e.department || '',
        '직무': e.jobTitle || '',
        '입사일': formatDate(e.hireDate),
        '현직전입일': formatDate(e.transferDate),
        '재직상태': statusText,
        '퇴사일': isUnknownResign ? '' : formatDate(e.resignDate),
        '비고': e.resignNote || '',
        '유해인자': e.hazard || '',
        '이메일': e.email || '',
        '연락처': e.phone || ''
      };
    });
    const ws = XLSX.utils.json_to_sheet(data);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, '직원목록');
    const today = formatDate(new Date());
    XLSX.writeFile(wb, `부민_직원목록_${today}.xlsx`);
    toast('엑셀 파일 다운로드 완료', 'success');
  }
};


// ============================================================
// 7. 엑셀 업로드 (Upload) 네임스페이스
// ============================================================
const Upload = {
  parsedData: null, // { file, analysis, extraData }
  
  setupDropZone(dropEl, inputEl, handler) {
    dropEl.addEventListener('click', () => inputEl.click());
    dropEl.addEventListener('dragover', e => { e.preventDefault(); dropEl.classList.add('dragover'); });
    dropEl.addEventListener('dragleave', () => dropEl.classList.remove('dragover'));
    dropEl.addEventListener('drop', e => {
      e.preventDefault();
      dropEl.classList.remove('dragover');
      if (e.dataTransfer.files.length) handler(e.dataTransfer.files[0]);
    });
    inputEl.addEventListener('change', e => {
      if (e.target.files.length) handler(e.target.files[0]);
    });
  },
  
  async handleFile(file) {
    showLoading('엑셀 파일 분석 중…');
    try {
      const sheets = await Import.parseFile(file);
      const sheetNames = Object.keys(sheets);
      
      // 첫 번째 시트 또는 가장 많은 데이터가 있는 시트 선택
      let targetSheet = sheetNames[0];
      let maxRows = 0;
      for (const name of sheetNames) {
        if (sheets[name].length > maxRows) {
          maxRows = sheets[name].length;
          targetSheet = name;
        }
      }
      
      const analysis = Import.analyzeSheet(sheets[targetSheet]);
      this.parsedData = { file, analysis, sheetName: targetSheet, allSheets: sheets };
      
      $('#fileInfo').innerHTML = `
        <div class="result-banner success">
          <strong>✓ ${esc(file.name)}</strong> (${(file.size/1024).toFixed(1)} KB)<br>
          시트: <strong>${esc(targetSheet)}</strong> · 데이터 행 ${analysis.dataRows.length.toLocaleString()}개 · 
          인식된 컬럼 ${Object.keys(analysis.mapping).length}개
        </div>
      `;
      
      this.renderMapping(analysis);
      this.renderPreview(analysis);
      $('#importActions').style.display = 'block';
    } catch (e) {
      console.error(e);
      toast('파일 분석 실패: ' + e.message, 'error');
    } finally { hideLoading(); }
  },
  
  renderMapping(analysis) {
    const items = [];
    analysis.headers.forEach((h, i) => {
      if (!h) return;
      const field = analysis.mapping[i];
      if (field) {
        items.push(`
          <div class="mapping-item">
            <div class="src">${esc(h)}</div>
            <div class="dst">→ ${fieldLabel(field)}</div>
          </div>
        `);
      } else {
        items.push(`
          <div class="mapping-item unmapped">
            <div class="src">${esc(h)}</div>
            <div class="dst" style="color:var(--text-3)">(인식 안 됨, 무시)</div>
          </div>
        `);
      }
    });
    
    const hasEmpCode = Object.values(analysis.mapping).includes('empCode');
    const warning = hasEmpCode ? '' : `
      <div class="result-banner error" style="margin-bottom:12px">
        <strong>⚠️ 사번 컬럼을 찾을 수 없습니다!</strong><br>
        헤더에 '사번', '사원코드', '사원번호' 중 하나가 포함되어야 업로드 가능합니다.
      </div>
    `;
    
    $('#mappingInfo').innerHTML = warning + `
      <div class="mapping-summary">${items.join('')}</div>
    `;
    $('#mappingCard').style.display = 'block';
    
    // 사번 없으면 저장 버튼 비활성화
    $('#btnConfirmImport').disabled = !hasEmpCode;
  },
  
  renderPreview(analysis) {
    const headers = analysis.headers.map(h => esc(h || ''));
    const rows = analysis.dataRows.slice(0, 5);
    
    let html = '<thead><tr>';
    headers.forEach(h => html += `<th>${h}</th>`);
    html += '</tr></thead><tbody>';
    rows.forEach(row => {
      html += '<tr>';
      for (let i = 0; i < headers.length; i++) {
        const cell = row[i];
        html += `<td>${esc(cell == null ? '' : String(cell))}</td>`;
      }
      html += '</tr>';
    });
    html += '</tbody>';
    
    $('#previewTable').innerHTML = html;
    $('#previewCard').style.display = 'block';
  },
  
  async confirmImport() {
    if (!this.parsedData) return;
    const { analysis } = this.parsedData;
    
    const { records, errors } = Import.applyMapping(analysis.dataRows, analysis.mapping);
    
    if (records.length === 0) {
      toast('저장할 데이터가 없습니다', 'warn');
      return;
    }
    
    if (!confirm(`${records.length.toLocaleString()}명의 인사정보를 데이터베이스에 저장합니다.\n계속하시겠습니까?`)) return;
    
    showLoading(`저장 중… (0/${records.length})`);
    try {
      const result = await DB.bulkSaveEmployees(records, (done, total) => {
        $('#loadingText').textContent = `저장 중… (${done.toLocaleString()}/${total.toLocaleString()})`;
      });
      
      $('#fileInfo').innerHTML = `
        <div class="result-banner success">
          <div class="count">✓ 저장 완료</div>
          성공: <strong>${result.success.toLocaleString()}건</strong> · 실패: ${result.fail}건
          ${errors.length ? ` · 사번 누락: ${errors.length}건` : ''}
        </div>
      `;
      toast(`${result.success.toLocaleString()}건 저장 완료`, 'success');
      this.reset();
      await Employees.loadAll();
    } catch (e) {
      console.error(e);
      toast('저장 실패: ' + e.message, 'error');
    } finally { hideLoading(); }
  },
  
  reset() {
    this.parsedData = null;
    $('#fileInput').value = '';
    $('#mappingCard').style.display = 'none';
    $('#previewCard').style.display = 'none';
    $('#importActions').style.display = 'none';
  }
};

function fieldLabel(field) {
  const labels = {
    empCode: '사번', name: '이름', department: '부서', jobTitle: '직무',
    hireDate: '입사일', resignDate: '퇴사일', transferDate: '현직전입일',
    gender: '성별', email: '이메일', phone: '연락처', birthDate: '생년월일',
    hazard: '유해인자'
  };
  return labels[field] || field;
}


// ============================================================
// 8. 기존 데이터 마이그레이션 (Migrate) 네임스페이스
// ============================================================

/**
 * 퇴사 상태 자동 감지
 * - 퇴사일 필드 or 유해인자에 "퇴사/퇴사예정" 있으면 퇴사자 처리
 * - 날짜면 그대로 저장, 문자열이면 "퇴사일 불명"으로 표시
 * @returns { resignDate: 실제 저장할 퇴사일, status: 'active'|'resigned'|'leave', note: 비고 }
 */
function detectResignStatus(resignRaw, hazardRaw) {
  let resignDate = null;
  let status = 'active';
  let note = '';
  
  const resignStr = String(resignRaw ?? '').trim();
  const hazardStr = String(hazardRaw ?? '').trim();
  
  // 1) 퇴사일 필드 분석
  if (resignStr) {
    const asDate = parseExcelDate(resignStr);
    if (asDate) {
      // 명확한 날짜 → 퇴사자
      resignDate = asDate;
      status = 'resigned';
    } else if (/퇴사|퇴직/.test(resignStr)) {
      // "퇴사", "퇴사예정" 문자열
      status = 'resigned';
      resignDate = '9999-12-31'; // 퇴사일 불명 표시용 (재직 필터에서 제외)
      if (/예정/.test(resignStr)) note = '퇴사예정';
      else note = '퇴사(일자 불명)';
    } else if (/휴직/.test(resignStr)) {
      status = 'leave';
      note = '휴직';
    }
  }
  
  // 2) 유해인자 필드에서 퇴사 메모 감지
  if (status === 'active' && hazardStr) {
    if (/퇴사|퇴직/.test(hazardStr)) {
      status = 'resigned';
      resignDate = resignDate || '9999-12-31';
      if (/예정/.test(hazardStr)) note = note || '퇴사예정';
      else note = note || '퇴사(일자 불명)';
    } else if (/휴직/.test(hazardStr) && !/^미/.test(hazardStr)) {
      status = 'leave';
      note = note || '휴직';
    }
  }
  
  return { resignDate, status, note };
}

/**
 * 유해인자 필드 정제 - 메모·주석·상태정보 완전 제거
 * 실제 유해인자로 인정할 키워드만 필터링
 */
function cleanHazard(raw) {
  if (!raw) return null;
  let s = String(raw).trim();
  
  // 전체가 상태/메모성 텍스트만 있는 경우 → null
  const onlyStatus = /^(퇴사|퇴직|휴직|미수검|미대상|미해당|해당없음|N\/A|-)$/i;
  if (onlyStatus.test(s)) return null;
  if (s.length < 3) return null; // 너무 짧은 건 무시
  
  // 알려진 유해인자 목록 (산업안전보건법 시행규칙 별표 22)
  const KNOWN_HAZARDS = [
    '방사선', '포름알데히드', '야간', '소음', '분진',
    '벤젠', '톨루엔', '크실렌', '메틸알콜', '메틸렌', '메탄올', 
    '에틸벤젠', '에틸렌', '아세톤', '페놀', '염산', '염화수소',
    '크롬', '납', '수은', '망간', '니켈', '카드뮴',
    '산화에틸렌', '2-부톡시에탄올', 'Isobutanol', 'Isobutnol',
    '알루미늄', '탄산칼슘', '규산염', '규산', '활석', '석영', '실리카',
    '시클로헥사논', '디이소시아네이트', '에틸렌글리콜',
    '용접흄', '산화철', '자외선', '석면', '디메틸',
    '방사선관계종사자'
  ];
  
  // 쉼표·줄바꿈으로 분할
  const parts = s.split(/[,\n]/).map(p => p.trim()).filter(Boolean);
  
  const validParts = parts.filter(p => {
    // 1) 메모·주석 패턴 제거
    if (/수선생님|회신|메시지|보냄|알림|확인|예정|추가하기|추가$|\d{1,2}[./월]\s*\d{1,2}|^\d{4}년.*추가|대상자|검진시|TOP|년\s*정기/.test(p)) {
      // "포름알데히드 추가하기" 같은 경우 → 유해인자만 추출
      const cleaned = p.replace(/추가하기|추가$|검진시.*$|\d{4}년.*?(?=[가-힣]|$)/g, '').trim();
      if (cleaned && cleaned.length >= 2 && KNOWN_HAZARDS.some(h => cleaned.includes(h))) {
        p = cleaned; // 메모만 제거하고 유해인자는 살림
      } else {
        return false;
      }
    }
    // 2) 상태/퇴사 관련 제거
    if (/^(퇴사|퇴직|휴직|미수검|미대상|미해당|해당없음|N\/A|-|\s*)$/i.test(p)) {
      return false;
    }
    // 3) 알려진 유해인자를 포함하거나, 최소한 한글/영문으로 3자 이상인 경우만 인정
    const isKnownHazard = KNOWN_HAZARDS.some(h => p.includes(h));
    if (isKnownHazard) return true;
    // 너무 짧거나 숫자만 있으면 제외
    if (p.length < 2 || /^\d+$/.test(p)) return false;
    return true; // 나머지는 보존 (Isobutnol 오타 등)
  }).map(p => {
    // 4) 개별 파트도 메모 제거
    return p.replace(/\s*(추가하기|추가$|검진시.*$)/g, '').trim();
  }).filter(p => p && p.length >= 2);
  
  if (validParts.length === 0) return null;
  return validParts.join(', ');
}

const Migrate = {
  async handleFile(file) {
    showLoading('부민 현황판 파싱 중…');
    try {
      const sheets = await Import.parseFile(file);
      const required = ['2026년 채용검진', '2026년 일반검진', '2026년 특수건강검진'];
      const missing = required.filter(r => !sheets[r]);
      
      if (missing.length > 0) {
        const banner = $('#migrateResult');
        banner.innerHTML = `
          <div class="result-banner error">
            <strong>⚠️ 필수 시트를 찾을 수 없습니다</strong><br>
            누락: ${missing.join(', ')}<br>
            발견된 시트: ${Object.keys(sheets).join(', ')}
          </div>
        `;
        hideLoading();
        return;
      }
      
      // 3개 시트에서 사번을 key로 정보 통합
      const employeeMap = new Map();    // 사번 있는 직원
      const noCodeByName = new Map();   // 사번 없는 직원 (이름 기준)
      
      for (const sheetName of required) {
        const rows = sheets[sheetName];
        const analysis = Import.analyzeSheet(rows);
        
        // ⚠️ applyMapping을 거치지 않고 직접 처리 (사번 없는 행도 활용)
        for (let i = 0; i < analysis.dataRows.length; i++) {
          const row = analysis.dataRows[i];
          const rec = {};
          for (let col = 0; col < row.length; col++) {
            const cell = row[col];
            if (cell == null || cell === '') continue;
            const field = analysis.mapping[col];
            if (field) rec[field] = cell;
          }
          // 날짜 변환
          ['examDate','hireDate','resignDate','transferDate','birthDate'].forEach(f => {
            if (rec[f]) { const p = parseExcelDate(rec[f]); if (p) rec[f] = p; }
          });
          if (rec.empCode) rec.empCode = String(rec.empCode).trim();
          if (rec.name) rec.name = String(rec.name).trim();
          
          // 완전히 빈 행은 스킵
          if (!rec.empCode && !rec.name) continue;
          
          if (rec.empCode) {
            // 사번 있는 직원
            if (!employeeMap.has(rec.empCode)) {
              employeeMap.set(rec.empCode, { empCode: rec.empCode });
            }
            const emp = employeeMap.get(rec.empCode);
            this._mergeRecord(emp, rec, sheetName);
          } else if (rec.name) {
            // 사번 없는 직원 → 이름 기준으로 통합 (퇴사자 처리)
            const key = `${rec.name}|${rec.hireDate || ''}|${rec.department || ''}`;
            if (!noCodeByName.has(key)) {
              noCodeByName.set(key, { name: rec.name, _noEmpCode: true });
            }
            const emp = noCodeByName.get(key);
            this._mergeRecord(emp, rec, sheetName);
          }
        }
      }
      
      // 🆕 사번 없는 직원에게 임시 사번 부여
      let tmpCounter = 1;
      for (const emp of noCodeByName.values()) {
        const tmpCode = `X-${String(tmpCounter).padStart(4, '0')}`;
        tmpCounter++;
        emp.empCode = tmpCode;
        employeeMap.set(tmpCode, emp);
      }
      
      // 🆕 퇴사 상태 자동 분류 + 유해인자 정제
      const stats = { active: 0, resigned: 0, resignedUnknown: 0, leave: 0, tmpCode: 0 };
      const employees = [];
      
      for (const emp of employeeMap.values()) {
        if (!emp.empCode) continue;
        
        let { resignDate, status, note } = detectResignStatus(emp._rawResign, emp._rawHazard);
        const cleanedHazard = cleanHazard(emp._rawHazard);
        
        // 🆕 사번 없는 직원은 무조건 퇴사자 처리
        if (emp._noEmpCode) {
          status = 'resigned';
          if (!resignDate) resignDate = '9999-12-31';
          note = note ? `${note} / 사번없음(임시부여)` : '사번없음(임시부여)';
          stats.tmpCode++;
        }
        
        const finalEmp = {
          empCode: emp.empCode,
          name: emp.name,
          department: emp.department,
          jobTitle: emp.jobTitle,
          hireDate: emp.hireDate,
          gender: emp.gender,
          email: emp.email,
          transferDate: emp.transferDate,
        };
        
        if (cleanedHazard) finalEmp.hazard = cleanedHazard;
        if (resignDate) finalEmp.resignDate = resignDate;
        if (note) finalEmp.resignNote = note;
        if (status) finalEmp.status = status;
        
        // undefined/null/빈 문자열 제거
        Object.keys(finalEmp).forEach(k => {
          if (finalEmp[k] === undefined || finalEmp[k] === null || finalEmp[k] === '') {
            delete finalEmp[k];
          }
        });
        
        employees.push(finalEmp);
        
        if (status === 'resigned') {
          stats.resigned++;
          if (resignDate === '9999-12-31') stats.resignedUnknown++;
        } else if (status === 'leave') {
          stats.leave++;
        } else {
          stats.active++;
        }
      }
      
      // 확인
      if (!confirm(`3개 시트에서 통합된 ${employees.length.toLocaleString()}명의 인사정보를 Firebase에 저장합니다.\n\n기존 데이터가 있다면 최신 정보로 덮어써집니다.\n\n계속하시겠습니까?`)) {
        hideLoading();
        return;
      }
      
      $('#loadingText').textContent = `저장 중… (0/${employees.length})`;
      const result = await DB.bulkSaveEmployees(employees, (done, total) => {
        $('#loadingText').textContent = `저장 중… (${done.toLocaleString()}/${total.toLocaleString()})`;
      });
      
      $('#migrateResult').innerHTML = `
        <div class="result-banner success">
          <div class="count">✓ 이관 완료</div>
          통합된 인원: <strong>${employees.length.toLocaleString()}명</strong><br>
          저장 성공: <strong>${result.success.toLocaleString()}건</strong> · 실패: ${result.fail}건
          <div style="margin-top:12px;padding-top:10px;border-top:1px solid rgba(0,0,0,0.1);font-size:12px;line-height:1.8">
            📊 <strong>자동 분류 결과:</strong><br>
            ㆍ 재직자: <strong>${stats.active.toLocaleString()}명</strong><br>
            ㆍ 퇴사자: <strong>${stats.resigned.toLocaleString()}명</strong> 
              ${stats.resignedUnknown ? `(그중 퇴사일 불명 ${stats.resignedUnknown}명은 '9999-12-31'로 표시)` : ''}<br>
            ㆍ 휴직자: <strong>${stats.leave.toLocaleString()}명</strong>
            ${stats.tmpCode ? `<br>ㆍ 임시사번 부여 (사번없음→퇴사처리): <strong>${stats.tmpCode}명</strong> <span style="color:var(--text-3)">(X-0001 ~ X-${String(stats.tmpCode).padStart(4,'0')})</span>` : ''}
          </div>
          <div style="margin-top:10px;font-size:12px">
            📌 '직원 관리' 메뉴에서 데이터를 확인하세요.<br>
            📌 임시사번(X-xxxx) 직원은 필터 '퇴사자'에서 확인 가능합니다.<br>
            📌 Phase 2에서 검진 기록도 이관 예정입니다.
          </div>
        </div>
      `;
      toast(`${result.success.toLocaleString()}명 이관 완료`, 'success', 5000);
      await Employees.loadAll();
    } catch (e) {
      console.error(e);
      $('#migrateResult').innerHTML = `
        <div class="result-banner error">
          <strong>오류 발생:</strong> ${esc(e.message)}
        </div>
      `;
    } finally { hideLoading(); }
  },
  
  /** 여러 시트의 동일 직원 데이터를 하나로 병합 */
  _mergeRecord(emp, rec, sheetName) {
    // 기본 인적사항 (먼저 들어온 값 우선)
    ['name','department','jobTitle','hireDate','gender','email','transferDate','birthDate','phone'].forEach(f => {
      if (rec[f] && !emp[f]) emp[f] = rec[f];
    });
    // 퇴사일은 원본 그대로 임시 보존 (나중에 detectResignStatus에서 정제)
    if (rec.resignDate != null && !emp._rawResign) {
      emp._rawResign = rec.resignDate;
    }
    // 특수검진 시트의 유해인자 우선
    if (sheetName === '2026년 특수건강검진' && rec.hazard) {
      emp._rawHazard = rec.hazard;
    } else if (rec.hazard && !emp._rawHazard) {
      emp._rawHazard = rec.hazard;
    }
  }
};


// ============================================================
// 9. 모달 (Modal) 네임스페이스
// ============================================================
const Modal = {
  open({ title, body, actions = [], wide = false }) {
    const existing = $('.modal-backdrop');
    if (existing) existing.remove();
    
    const actionsHtml = actions.map((a, i) => 
      `<button class="btn btn-${a.variant || 'outline'}" data-idx="${i}">${esc(a.text)}</button>`
    ).join('');
    
    const html = `
      <div class="modal-backdrop">
        <div class="modal ${wide ? 'wide' : ''}">
          <div class="modal-header">
            <h3>${esc(title)}</h3>
            <button class="close-btn" data-close>×</button>
          </div>
          <div class="modal-body">${body}</div>
          ${actions.length ? `<div class="modal-footer">${actionsHtml}</div>` : ''}
        </div>
      </div>
    `;
    document.body.insertAdjacentHTML('beforeend', html);
    const backdrop = $('.modal-backdrop');
    
    // 액션 핸들러
    backdrop.querySelectorAll('button[data-idx]').forEach(btn => {
      btn.addEventListener('click', () => {
        const idx = parseInt(btn.dataset.idx);
        actions[idx].handler && actions[idx].handler();
      });
    });
    backdrop.querySelector('[data-close]').addEventListener('click', () => this.close());
    backdrop.addEventListener('click', e => {
      if (e.target === backdrop) this.close();
    });
  },
  
  close() {
    const m = $('.modal-backdrop');
    if (m) m.remove();
  }
};


// ============================================================
// 10. 화면 라우팅 (Router)
// ============================================================
const Router = {
  async show(viewName) {
    $$('.nav-item').forEach(n => n.classList.toggle('active', n.dataset.view === viewName));
    $$('.view').forEach(v => v.classList.toggle('active', v.id === `view-${viewName}`));
    
    if (viewName === 'settings') {
      await Settings.refresh();
    }
  }
};


// ============================================================
// 11. 설정 (Settings) 네임스페이스
// ============================================================
const Settings = {
  async refresh() {
    try {
      // 연결 확인
      $('#dbStatus').textContent = '연결됨 ✓';
      $('#dbStatus').style.color = 'var(--accent-dark)';
      
      const [empCount] = await Promise.all([DB.countCollection(COL.EMPLOYEES)]);
      $('#dbStats').innerHTML = `
        <div class="stat accent">
          <div class="label">직원</div>
          <div class="value">${empCount.toLocaleString()}</div>
          <div class="delta">Firestore: employees</div>
        </div>
        <div class="stat">
          <div class="label">검진 기록</div>
          <div class="value">0</div>
          <div class="delta">Phase 2 예정</div>
        </div>
        <div class="stat">
          <div class="label">상담일지</div>
          <div class="value">0</div>
          <div class="delta">Phase 3 예정</div>
        </div>
      `;
    } catch (e) {
      $('#dbStatus').textContent = '오류: ' + e.message;
      $('#dbStatus').style.color = 'var(--danger)';
    }
  }
};


// ============================================================
// 12. 앱 초기화 및 이벤트 바인딩
// ============================================================
function initApp() {
  // 인증 상태 감시
  Auth.onChange(async (user) => {
    if (user) {
      $('#loginView').style.display = 'none';
      $('#appView').style.display = 'block';
      $('#userEmail').textContent = user.email;
      $('#userAvatar').textContent = (user.email[0] || 'A').toUpperCase();
      await Employees.loadAll();
    } else {
      $('#loginView').style.display = 'flex';
      $('#appView').style.display = 'none';
    }
  });
  
  // 로그인
  $('#loginForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    $('#loginError').textContent = '';
    const email = $('#loginEmail').value;
    const password = $('#loginPassword').value;
    try {
      showLoading('로그인 중…');
      await Auth.login(email, password);
    } catch (err) {
      $('#loginError').textContent = authErrorMessage(err.code);
    } finally { hideLoading(); }
  });
  
  // 관리자 생성
  $('#showSignupBtn').addEventListener('click', async () => {
    const email = prompt('관리자 이메일을 입력하세요:\n(예: clover8477@bumin.co.kr)');
    if (!email) return;
    const password = prompt('비밀번호를 입력하세요 (6자 이상):');
    if (!password || password.length < 6) {
      toast('비밀번호는 6자 이상이어야 합니다', 'error');
      return;
    }
    try {
      showLoading('계정 생성 중…');
      await Auth.signup(email, password);
      toast('관리자 계정이 생성되었습니다', 'success');
    } catch (err) {
      $('#loginError').textContent = authErrorMessage(err.code);
    } finally { hideLoading(); }
  });
  
  // 로그아웃
  $('#logoutBtn').addEventListener('click', async () => {
    if (!confirm('로그아웃 하시겠습니까?')) return;
    await Auth.logout();
    toast('로그아웃 되었습니다', 'info');
  });
  
  // 네비게이션
  $$('.nav-item[data-view]').forEach(item => {
    item.addEventListener('click', () => Router.show(item.dataset.view));
  });
  
  // 직원 관리 검색/필터
  $('#searchInput').addEventListener('input', debounce(() => Employees.applyFilters(), 200));
  $('#filterStatus').addEventListener('change', () => Employees.applyFilters());
  $('#filterDept').addEventListener('change', () => Employees.applyFilters());
  
  // 직원 관리 버튼
  $('#btnRefresh').addEventListener('click', () => Employees.loadAll());
  $('#btnAddEmp').addEventListener('click', () => Employees.showEditModal(null));
  $('#btnExportExcel').addEventListener('click', () => Employees.exportToExcel());
  
  // 엑셀 업로드
  Upload.setupDropZone($('#fileDrop'), $('#fileInput'), f => Upload.handleFile(f));
  $('#btnCancelImport').addEventListener('click', () => Upload.reset());
  $('#btnConfirmImport').addEventListener('click', () => Upload.confirmImport());
  
  // 마이그레이션
  Upload.setupDropZone($('#migrateDrop'), $('#migrateFileInput'), f => Migrate.handleFile(f));
  
  // 설정
  $('#btnRefreshStats').addEventListener('click', () => Settings.refresh());
  
  // 날짜 일괄 정정
  $('#btnFixDates').addEventListener('click', async () => {
    if (!confirm('전체 직원의 날짜 필드(입사일/생년월일/퇴사일/전입일)를 YYYY-MM-DD 형식으로 정규화합니다.\n계속하시겠습니까?')) return;
    
    showLoading('날짜 정정 중…');
    try {
      const stats = await DB.fixAllDates((done, total) => {
        $('#loadingText').textContent = `정정 중… (${done}/${total})`;
      });
      
      const samplesHtml = stats.samples.map(s => 
        `<div style="font-family:monospace;font-size:11px;padding:3px 0">
          ${esc(s.name)} · ${s.field}: <span style="color:var(--danger)">${esc(s.before)}</span> → <span style="color:var(--accent-dark)">${esc(s.after)}</span>
        </div>`
      ).join('');
      
      $('#dateFixResult').innerHTML = `
        <div class="result-banner success">
          <div class="count">✓ 정정 완료</div>
          전체 ${stats.total.toLocaleString()}건 · 수정 <strong>${stats.fixed.toLocaleString()}건</strong> · 변경 없음 ${stats.skipped.toLocaleString()}건
          ${stats.samples.length ? `<div style="margin-top:10px;padding-top:8px;border-top:1px solid rgba(0,0,0,0.1)">
            <strong style="font-size:12px">변경 샘플:</strong>
            ${samplesHtml}
          </div>` : ''}
        </div>
      `;
      toast(`${stats.fixed.toLocaleString()}건 정정 완료`, 'success');
      await Employees.loadAll();
    } catch (e) {
      console.error(e);
      $('#dateFixResult').innerHTML = `
        <div class="result-banner error">
          <strong>오류:</strong> ${esc(e.message)}
        </div>
      `;
    } finally { hideLoading(); }
  });
  
  $('#btnResetDB').addEventListener('click', async () => {
    const confirm1 = prompt('모든 직원 데이터를 삭제합니다.\n계속하려면 "전체삭제"를 입력하세요:');
    if (confirm1 !== '전체삭제') return;
    showLoading('삭제 중…');
    try {
      const count = await DB.deleteAllEmployees();
      toast(`${count.toLocaleString()}건 삭제 완료`, 'success');
      await Employees.loadAll();
      await Settings.refresh();
    } catch (e) {
      toast('삭제 실패: ' + e.message, 'error');
    } finally { hideLoading(); }
  });
}

function authErrorMessage(code) {
  const map = {
    'auth/invalid-email': '이메일 형식이 올바르지 않습니다',
    'auth/user-not-found': '등록되지 않은 계정입니다',
    'auth/wrong-password': '비밀번호가 일치하지 않습니다',
    'auth/invalid-credential': '이메일 또는 비밀번호가 올바르지 않습니다',
    'auth/email-already-in-use': '이미 사용 중인 이메일입니다',
    'auth/weak-password': '비밀번호는 6자 이상이어야 합니다',
    'auth/network-request-failed': '네트워크 연결을 확인해주세요',
    'auth/too-many-requests': '잠시 후 다시 시도해주세요',
    'auth/operation-not-allowed': 'Firebase Console에서 이메일/비밀번호 로그인을 활성화해주세요'
  };
  return map[code] || '오류: ' + code;
}

function debounce(fn, ms) {
  let t;
  return (...args) => {
    clearTimeout(t);
    t = setTimeout(() => fn(...args), ms);
  };
}

// 시작!
initApp();

</script>
</body>
</html>
