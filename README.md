[index.html](https://github.com/user-attachments/files/26933832/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="에디핏">
<meta name="mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#0B0D11">
<link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoi7JeQ65SU7ZWPIOuLqOqwgCIsInNob3J0X25hbWUiOiLsl5DrlpTtlYMiLCJzdGFydF91cmwiOiIuIiwiZGlzcGxheSI6InN0YW5kYWxvbmUiLCJiYWNrZ3JvdW5kX2NvbG9yIjoiIzBCMEQxMSIsInRoZW1lX2NvbG9yIjoiIzBCMEQxMSJ9">
<title>에디핏 통합 단가 시스템</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;600;700&display=swap');
  *{margin:0;padding:0;box-sizing:border-box}
  body{font-family:'Noto Sans KR',sans-serif;background:#0B0D11;color:#E8E6E1;min-height:100vh}
  #lockScreen{position:fixed;top:0;left:0;width:100%;height:100%;background:#0B0D11;display:flex;align-items:center;justify-content:center;z-index:99999;flex-direction:column}
  #lockScreen .lock-box{background:#141825;border:1px solid #252A3A;border-radius:16px;padding:40px;text-align:center;max-width:360px;width:90%}
  #lockScreen .lock-dot{width:14px;height:14px;border-radius:50%;background:#22D3EE;box-shadow:0 0 12px #22D3EE66;margin:0 auto 16px}
  #lockScreen h2{font-size:20px;color:#F1F5F9;margin-bottom:6px}
  #lockScreen p{font-size:12px;color:#64748B;margin-bottom:20px}
  #lockScreen input{width:100%;padding:12px 16px;border:1px solid #334155;border-radius:8px;background:#0B0D11;color:#E2E8F0;font-size:14px;outline:none;margin-bottom:12px;font-family:inherit}
  #lockScreen input:focus{border-color:#22D3EE}
  #lockScreen button{width:100%;padding:12px;border:none;border-radius:8px;background:linear-gradient(135deg,#0891B2,#22D3EE);color:#0B0D11;font-weight:700;font-size:14px;cursor:pointer;font-family:inherit}
  #lockScreen .err{color:#F87171;font-size:11px;margin-top:8px;display:none}
  #appContent{display:none}
  .header{background:linear-gradient(135deg,#141825,#0B0D11);border-bottom:1px solid #252A3A;padding:18px 24px}
  .header-inner{max-width:1080px;margin:0 auto}
  .dot{display:inline-block;width:9px;height:9px;border-radius:50%;background:#22D3EE;box-shadow:0 0 8px #22D3EE66;vertical-align:middle;margin-right:8px}
  .header-label{font-size:10px;color:#6B7280;letter-spacing:.14em;text-transform:uppercase}
  .header h1{font-size:22px;font-weight:700;margin:4px 0 0;color:#F1F5F9}
  .header p{font-size:12px;color:#64748B;margin:2px 0 0}

  .tabs{max-width:1080px;margin:0 auto;padding:14px 24px 0;display:flex;gap:3px;overflow-x:auto}
  .tab{padding:9px 16px;border-radius:7px 7px 0 0;border:1px solid #252A3A;border-bottom:none;background:transparent;color:#64748B;font-size:13px;font-weight:500;font-family:inherit;cursor:pointer;white-space:nowrap;transition:.2s}
  .tab.active{background:#131720;color:#E2E8F0;border-color:#3B82F6}
  .tab:hover:not(.active){background:#1A1F2E}

  .container{max-width:1080px;margin:0 auto;padding:0 24px 80px}
  .tc{display:none}.tc.active{display:block}

  .card{background:#131720;border:1px solid #252A3A;border-radius:10px;padding:20px;margin-bottom:16px}
  .card h3{font-size:14px;font-weight:600;color:#CBD5E1;margin:0 0 14px}
  .card h3 .badge{font-size:10px;padding:2px 8px;border-radius:10px;margin-left:8px;font-weight:500}

  label{font-size:11px;color:#64748B;display:block;margin-bottom:5px}
  select,input[type="number"],input[type="text"]{width:100%;padding:8px 10px;background:#1A1F2E;border:1px solid #252A3A;border-radius:6px;color:#E2E8F0;font-size:13px;font-family:inherit;outline:none}
  select:focus,input:focus{border-color:#3B82F6}
  input[type="range"]{width:100%;accent-color:#22D3EE}

  .g2{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px}
  .g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:12px}
  .g4{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:12px;margin-bottom:12px}
  .g5{display:grid;grid-template-columns:1fr 1fr 1fr 1fr 1fr;gap:12px;margin-bottom:12px}
  @media(max-width:700px){.g3,.g4,.g5{grid-template-columns:1fr 1fr}.mode-cards{grid-template-columns:1fr!important}}

  .btn{padding:9px 20px;border:none;border-radius:7px;font-size:13px;font-weight:600;font-family:inherit;cursor:pointer;transition:.15s}
  .btn-primary{background:linear-gradient(135deg,#2563EB,#1D4ED8);color:#FFF}
  .btn-green{background:linear-gradient(135deg,#059669,#047857);color:#FFF}
  .btn-cyan{background:linear-gradient(135deg,#0891B2,#0E7490);color:#FFF}
  .btn:hover{transform:translateY(-1px);filter:brightness(1.1)}
  .btn-sm{padding:5px 12px;font-size:11px}
  .btn-outline{background:transparent;border:1px solid #252A3A;color:#94A3B8;padding:7px 14px;border-radius:6px;font-size:12px;font-family:inherit;cursor:pointer}
  .btn-outline:hover{background:#1E293B}

  table{width:100%;border-collapse:collapse;font-size:12px}
  th{padding:7px 8px;color:#64748B;font-weight:500;border-bottom:1px solid #252A3A;white-space:nowrap}
  td{padding:7px 8px;border-bottom:1px solid #1E2330}
  .tr{text-align:right}.tl{text-align:left}.tc2{text-align:center}

  .tag{display:inline-block;padding:2px 7px;border-radius:3px;font-size:10px;font-weight:600}
  .tag-blue{background:rgba(96,165,250,.15);color:#60A5FA}
  .tag-green{background:rgba(74,222,128,.15);color:#4ADE80}
  .tag-cyan{background:rgba(34,211,238,.15);color:#22D3EE}
  .tag-yellow{background:rgba(250,204,21,.15);color:#FACC15}
  .tag-pink{background:rgba(244,114,182,.15);color:#F472B6}
  .tag-red{background:rgba(248,113,113,.15);color:#F87171}
  .tag-orange{background:rgba(251,146,60,.15);color:#FB923C}

  .remove-btn{background:transparent;border:none;color:#F87171;cursor:pointer;font-size:13px}
  .hidden{display:none}

  .mode-cards{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:16px}
  .mode-card{padding:14px;border-radius:8px;border:2px solid #252A3A;cursor:pointer;transition:.2s;text-align:center}
  .mode-card:hover{border-color:#475569}
  .mode-card.active-blue{border-color:#3B82F6;background:rgba(59,130,246,.08)}
  .mode-card.active-green{border-color:#10B981;background:rgba(16,185,129,.08)}
  .mode-card.active-cyan{border-color:#06B6D4;background:rgba(6,182,212,.08)}
  .mode-card .icon{font-size:28px;margin-bottom:6px}
  .mode-card .title{font-size:13px;font-weight:600;color:#E2E8F0}
  .mode-card .desc{font-size:11px;color:#64748B;margin-top:3px}

  .cost-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-top:14px}
  .cost-box{text-align:center;padding:12px 6px;background:#0B0D11;border-radius:8px;border:1px solid #1E2330}
  .cost-box .lb{font-size:10px;color:#64748B;margin-bottom:3px}
  .cost-box .val{font-size:17px;font-weight:700}

  .chip{display:inline-block;padding:5px 12px;border-radius:16px;border:1px solid #252A3A;background:transparent;color:#94A3B8;font-size:12px;font-family:inherit;cursor:pointer;margin:2px;transition:.15s}
  .chip.active{border-color:#22D3EE;background:rgba(34,211,238,.1);color:#22D3EE}

  .divider{border:none;border-top:1px solid #252A3A;margin:14px 0}
  .note{font-size:11px;color:#64748B;line-height:1.6}
  .note b{color:#CBD5E1}

  .compare-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
  .compare-col{background:#0B0D11;border-radius:8px;padding:16px;border:1px solid #1E2330}
  .compare-col h4{font-size:13px;font-weight:600;margin-bottom:10px;text-align:center}

  .cutting-sheets{display:flex;flex-wrap:wrap;gap:20px;justify-content:center}
  .sheet-wrap{position:relative}
  .sheet-label{font-size:12px;color:#CBD5E1;font-weight:600;margin-bottom:6px;text-align:center}
  .sheet-box{position:relative;background:#1A1F2E;border:2px solid #334155;border-radius:4px;overflow:hidden}
  .cut-part{position:absolute;border:1px solid rgba(255,255,255,.25);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:500;color:#FFF;text-shadow:0 1px 2px rgba(0,0,0,.6);overflow:hidden;transition:.2s}
  .cut-part:hover{z-index:10;outline:2px solid #FFF;filter:brightness(1.3)}
  .cut-part .part-info{text-align:center;line-height:1.3;pointer-events:none}
  .cut-waste{position:absolute;background:repeating-linear-gradient(45deg,transparent,transparent 4px,rgba(100,116,139,.15) 4px,rgba(100,116,139,.15) 8px)}
  .sheet-stats{font-size:11px;color:#94A3B8;text-align:center;margin-top:6px}
  .sheet-stats b{color:#E2E8F0}
  .legend-row{display:flex;gap:16px;justify-content:center;flex-wrap:wrap;margin-bottom:14px}
  .legend-item{display:flex;align-items:center;gap:5px;font-size:11px;color:#94A3B8}
  .legend-dot{width:14px;height:14px;border-radius:3px;border:1px solid rgba(255,255,255,.2)}
</style>
</head>
<body>

<!-- 비밀번호 잠금 화면 -->
<div id="lockScreen">
  <div class="lock-box">
    <div class="lock-dot"></div>
    <h2>에디핏</h2>
    <p>통합 단가 시스템</p>
    <input type="password" id="lockPw" placeholder="비밀번호 입력" onkeydown="if(event.key==='Enter')unlock()" autofocus>
    <button onclick="unlock()">로그인</button>
    <div class="err" id="lockErr">비밀번호가 틀렸습니다</div>
  </div>
</div>

<div id="appContent">
<div class="header">
  <div class="header-inner">
    <div><span class="dot"></span><span class="header-label">에디핏 통합 원가 관리 시스템</span></div>
    <h1>가구 원가·단가 통합 계산기</h1>
    <p>에디핏 자체생산 + 홈그린 · 성우산업 · 일흥건영 · 목산 외주 통합 비교</p>
  </div>
</div>

<div class="tabs">
  <button class="tab active" onclick="switchTab('cabinet')">🗄️ 장짜기 (9모드 비교)</button>
  <button class="tab" onclick="switchTab('cutguide')">✂️ 재단가이드</button>
  <button class="tab" onclick="switchTab('order')">📋 합판주문</button>
  <button class="tab" onclick="switchTab('mkquote')">🧾 목산견적</button>
  <button class="tab" onclick="switchTab('munique')">🚪 무니끄</button>
  <button class="tab" onclick="switchTab('single')">📐 개별 부재 단가</button>
  <button class="tab" onclick="switchTab('matdb')">📦 자재 단가 DB</button>
  <button class="tab" onclick="switchTab('settings')">⚙️ 설정</button>
</div>

<div class="container">

<!-- ===================== TAB: 장짜기 ===================== -->
<div class="tc active" id="tab-cabinet">

  <!-- 자재/치수 입력 -->
  <div class="card" style="border-top-left-radius:0">
    <h3>📏 장 외형 & 자재 선택</h3>

    <div class="g3">
      <div>
        <label>도어재 선택</label>
        <select id="cab_doorMat" onchange="cab_updateDoorInfo()">
          <optgroup label="── ⛔ 도어재 없음 ──">
            <option value="NONE" data-price="0" data-w="0" data-h="0">사용안함 (몸통재만 사용)</option>
          </optgroup>
          <optgroup label="── 🔄 몸통재와 동일 ──">
            <option value="SAME_AS_BODY" data-price="0" data-w="0" data-h="0">→ 몸통재와 동일하게 사용</option>
          </optgroup>
          <optgroup label="── 영앤썬 아르모니아 ──">
            <option value="arm_std" data-price="85800" data-w="1220" data-h="2745" data-edge="350" data-edgem="m" selected>아르모니아 스탠다드 (BM1112 등) 85,800원</option>
            <option value="arm_prm" data-price="97900" data-w="1220" data-h="2745" data-edge="350" data-edgem="m">아르모니아 프리미엄 (BM1201 등) 97,900원</option>
            <option value="arm_1323" data-price="79200" data-w="1220" data-h="2440" data-edge="350" data-edgem="m">아르모니아 BM1323/1325 79,200원</option>
          </optgroup>
          <optgroup label="── 시온텍 ──">
            <option value="sion_hp" data-price="64900" data-w="1220" data-h="2745" data-edge="40500" data-edgem="roll">HP샌드그레이(스페셜) 64,900원</option>
            <option value="sion_pican" data-price="79200" data-w="1220" data-h="2745" data-edge="22000" data-edgem="roll">피칸웜그레이우드 79,200원</option>
          </optgroup>
          <optgroup label="── 가공보드 ──">
            <option value="gb_hansol" data-price="99000" data-w="1220" data-h="2745" data-edge="350" data-edgem="m">한솔프리미엄 4*9 99,000원</option>
            <option value="gb_hansol30" data-price="157300" data-w="1220" data-h="2745" data-edge="36000" data-edgem="roll">한솔패트 30T 157,300원</option>
          </optgroup>
          <optgroup label="── 예림 ──">
            <option value="yerim_rosi" data-price="60500" data-w="1220" data-h="2440" data-edge="20000" data-edgem="roll">로지핑크 60,500원</option>
            <option value="yerim_satin" data-price="74800" data-w="1220" data-h="2440" data-edge="44000" data-edgem="roll">새틴얼그레이 74,800원</option>
            <option value="yerim_cera" data-price="67100" data-w="1220" data-h="2440" data-edge="24000" data-edgem="roll">세라믹문 퍼시픽 67,100원</option>
            <option value="yerim_pet" data-price="50600" data-w="1220" data-h="2440" data-edge="20000" data-edgem="roll">저가pet 도어 50,600원</option>
          </optgroup>
          <optgroup label="── 메라톤 ──">
            <option value="mera_low" data-price="121000" data-w="1220" data-h="2440" data-edge="100000" data-edgem="200m">8835BS 저가형 121,000원</option>
            <option value="mera_high" data-price="150700" data-w="1220" data-h="2440" data-edge="100000" data-edgem="200m">8835BS 고급형 150,700원</option>
          </optgroup>
        </select>
      </div>
      <div>
        <label>몸통재 선택</label>
        <select id="cab_bodyMat">
          <optgroup label="── 🔄 도어재와 동일 (오픈장) ──">
            <option value="SAME_AS_DOOR" data-price="0" data-w="0" data-h="0">→ 도어재와 동일하게 사용</option>
          </optgroup>
          <optgroup label="── 예림 ──">
            <option value="yerim_18" data-price="30800" data-w="1220" data-h="2440" data-edge="9000" data-edgem="roll18" selected>예림 18T 몸통합판 30,800원</option>
            <option value="yerim_15" data-price="27500" data-w="1220" data-h="2440" data-edge="9000" data-edgem="roll18">예림 15T 몸통합판 27,500원</option>
            <option value="yerim_anti" data-price="31900" data-w="1220" data-h="2440" data-edge="9000" data-edgem="roll18">예림 항균 18T 31,900원</option>
          </optgroup>
          <optgroup label="── P&R(남태옥) ──">
            <option value="pr_18" data-price="24640" data-w="1220" data-h="2440" data-edge="14000" data-edgem="roll">효산 LPM N202 18T 24,640원</option>
            <option value="pr_15" data-price="22220" data-w="1220" data-h="2440" data-edge="14000" data-edgem="roll">효산 LPM N202 15T 22,220원</option>
          </optgroup>
          <optgroup label="── 신길합판 ──">
            <option value="singil_18" data-price="38500" data-w="1220" data-h="2440" data-edge="27000" data-edgem="roll">신길 우드 N653 18T 38,500원</option>
          </optgroup>
          <optgroup label="── 시온텍 (wpc방수보드) ──">
            <option value="sion_body" data-price="99000" data-w="1220" data-h="2440" data-edge="9000" data-edgem="roll18">시온텍 wpc방수보드 양면pp 18T 99,000원</option>
          </optgroup>
        </select>
      </div>
      <div>
        <label>우라판 선택</label>
        <select id="cab_uraMat">
          <option value="SAME_AS_DOOR" data-price="0">🔄 도어재와 동일 (오픈장)</option>
          <option value="SAME_AS_BODY" data-price="0">🔄 몸통재와 동일</option>
          <option value="yerim_ura" data-price="15950" selected>예림 모시화이트 3T 15,950원</option>
          <option value="pr_ura" data-price="14080">효산 LPM N202 4.5T 14,080원</option>
          <option value="sion_ura" data-price="49500">시온텍 wpc방수보드 5T 49,500원</option>
          <option value="singil_ura" data-price="33000">신길 우라 N653 3T 33,000원</option>
        </select>
      </div>
    </div>

    <div class="g2" style="margin-bottom:14px">
      <div>
        <label>🏭 성우산업 자재등급 (10% DC 적용)</label>
        <select id="cab_swGrade">
          <option value="standard">한솔계열 (안도크림, 포그그레이, 크림화 등)</option>
          <option value="premium">프리미엄 (클레이크림, 바이브실버)</option>
        </select>
      </div>
      <div>
        <label>🏭 홈그린 자재등급</label>
        <select id="cab_hgGrade">
          <option value="BM1112">BM1112 스탠다드</option>
          <option value="BM1201">BM1201 프리미엄</option>
          <option value="BM1323">BM1323</option>
        </select>
      </div>
    </div>
    <div class="g2" style="margin-bottom:14px">
      <div>
        <label>🏭 일흥건영 자재 (사비올라/포렐스)</label>
        <select id="cab_jhGrade">
          <option value="EC811">포렐스 EC811 (85,800원/장) — 가성비</option>
          <option value="P33">사비올라 P33 (233,000원/장) — 프리미엄</option>
          <option value="P59">사비올라 P59 (233,000원/장) — 프리미엄</option>
        </select>
      </div>
      <div>
        <label>🏭 목산 도어공장 자재 (자재+가공 포함)</label>
        <select id="cab_mkGrade">
          <option value="PET">PET 화이트/아이보리 — 저가</option>
          <option value="PET2">PET2 SMR — 중저가</option>
          <option value="DAISY">데이지 솔리드크림 — 중저가</option>
          <option value="WET3000">3000 습식무늬목 — 중가</option>
          <option value="URBAN">어반 화이트오크 — 중고가</option>
          <option value="ASH">건식애쉬 내추럴 — 고가</option>
          <option value="5000">5000평판 무광 — 고가</option>
          <option value="OAKN">건식오크 내추럴 — 프리미엄</option>
          <option value="MANHATTAN">맨하탄/5000NC — 프리미엄</option>
          <option value="SMOKE">훈증무늬목 — 최고급</option>
          <option value="DYE">염색무늬목 — 최고급</option>
        </select>
      </div>
    </div>

    <div class="g5">
      <div><label>전체 가로 (mm)</label><input type="number" id="cab_w" value="900"></div>
      <div><label>전체 높이 (mm)</label><input type="number" id="cab_h" value="2100"></div>
      <div><label>깊이 (mm)</label><input type="number" id="cab_d" value="580"></div>
      <div><label>도어 수</label><input type="number" id="cab_doors" value="2" min="0" max="8"></div>
      <div><label>선반 수</label><input type="number" id="cab_shelves" value="2" min="0" max="10"></div>
    </div>
    <div class="g5">
      <div><label>서랍 수</label><input type="number" id="cab_drawers" value="0" min="0" max="6"></div>
      <div><label>서랍높이 (mm)</label><input type="number" id="cab_drawerH" value="200"></div>
      <div><label>걸레받이 높이</label><input type="number" id="cab_toeH" value="100"></div>
      <div>
        <label>공장가 배율 <b id="cab_factoryLabel" style="color:#22D3EE">×2.3</b></label>
        <input type="range" id="cab_factoryRate" min="15" max="35" value="23" oninput="document.getElementById('cab_factoryLabel').textContent='×'+(this.value/10).toFixed(1)">
      </div>
      <div>
        <label>영업마진 <b id="cab_marginLabel" style="color:#4ADE80">30%</b></label>
        <input type="range" id="cab_marginRate" min="10" max="50" value="30" oninput="document.getElementById('cab_marginLabel').textContent=this.value+'%'">
      </div>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">제작 모드</label>
      <span class="chip" id="ch_open" onclick="toggleOpenMode(this)" style="border-color:#F59E0B">📦 오픈장 (도어재로 전체제작)</span>
      <span style="font-size:10px;color:#64748B;margin-left:8px" id="openModeDesc"></span>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">옵션</label>
      <span class="chip active" id="ch_back" onclick="this.classList.toggle('active')">뒷판(우라)</span>
      <span class="chip active" id="ch_toe" onclick="this.classList.toggle('active')">걸레받이</span>
      <span class="chip" id="ch_nofloor" onclick="this.classList.toggle('active')">바닥없음</span>
      <span class="chip" id="ch_edge4" onclick="this.classList.toggle('active')">4면 엣지</span>
      <span class="chip" id="ch_light" onclick="this.classList.toggle('active')">조명홈가공</span>
    </div>

    <div style="text-align:center;margin-top:6px;display:flex;gap:10px;justify-content:center">
      <button class="btn" onclick="cab_addToList()" style="padding:10px 30px;font-size:14px;background:#1E3A5F;border:1px solid #3B82F6;color:#60A5FA">
        ➕ 장 추가
      </button>
      <button class="btn btn-cyan" onclick="cab_runAll()" style="padding:10px 40px;font-size:14px">
        🔨 9모드 비교 계산
      </button>
    </div>
  </div>

  <!-- 추가된 장 목록 -->
  <div class="card" id="cab_listCard" style="display:none">
    <h3>📦 입력된 장 목록 <span class="badge tag-cyan" id="cab_listCount">0개</span>
      <button class="btn" onclick="cab_clearList()" style="float:right;padding:3px 10px;font-size:10px;background:#7F1D1D;border:1px solid #991B1B">전체삭제</button>
    </h3>
    <div style="overflow-x:auto"><table style="font-size:11px">
      <thead><tr>
        <th class="tl">No</th><th class="tr">가로</th><th class="tr">높이</th><th class="tr">깊이</th>
        <th class="tr">도어</th><th class="tr">선반</th><th class="tr">서랍</th><th class="tl">모드</th><th class="tl">옵션</th><th></th>
      </tr></thead>
      <tbody id="cab_listBody"></tbody>
    </table></div>
  </div>

  <!-- 결과 영역 -->
  <div class="hidden" id="cab_resultArea">

    <!-- 부재 분해 -->
    <div class="card">
      <h3>📋 부재 자동 분해 <span class="badge tag-cyan" id="cab_partCount">0개</span></h3>
      <div style="overflow-x:auto"><table>
        <thead><tr>
          <th class="tl">부재명</th><th class="tl">품목</th><th class="tl">재료</th>
          <th class="tr">가로</th><th class="tr">세로</th><th class="tr">수량</th><th class="tr">면적(mm²)</th>
        </tr></thead>
        <tbody id="cab_partsBody"></tbody>
      </table></div>
    </div>

    <!-- 3모드 비교 -->
    <div class="card">
      <h3>💰 9모드 비교 (에디핏 vs 홈그린 vs 성우 vs 일흥 vs 목산)</h3>
      <div class="compare-grid" id="cab_compareGrid"></div>
    </div>

    <!-- 원장 재단 가이드 -->
    <div class="card">
      <h3>✂️ 원장 재단 배치도 <span class="badge tag-yellow" id="cut_sheetCount">0장</span>
        <button class="btn" onclick="printCutGuide()" style="float:right;padding:4px 14px;font-size:11px;background:#334155;border:1px solid #475569">🖨️ 재단가이드 출력</button>
      </h3>
      <p class="note" style="margin:-8px 0 12px">부재를 원장(합판)에 어떻게 배치하는지 시각적으로 보여줍니다. 도어재·몸통재 별도 원장.</p>
      <div class="legend-row" id="cut_legend"></div>
      <div id="cut_doorSection"></div>
      <div id="cut_bodySection"></div>
      <div id="cut_uraSection"></div>
      <div style="margin-top:14px" id="cut_summaryArea"></div>
    </div>

    <!-- 상세 내역 -->
    <div class="card">
      <h3>📑 모드별 상세 내역</h3>
      <div id="cab_detailArea"></div>
    </div>
  </div>
</div>

<!-- ===================== TAB: 재단가이드 ===================== -->
<div class="tc" id="tab-cutguide">
  <div class="card" style="border-top-left-radius:0">
    <h3>✂️ 합판 재단가이드 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 조립구조·엣지보정 반영</span></h3>

    <div class="g5" style="margin-bottom:10px">
      <div><label>전체 가로 (mm)</label><input type="number" id="cg_w" value="900"></div>
      <div><label>전체 높이 (mm)</label><input type="number" id="cg_h" value="2100"></div>
      <div><label>깊이 (mm)</label><input type="number" id="cg_d" value="580"></div>
      <div><label>도어 수</label><input type="number" id="cg_doors" value="2" min="0" max="8"></div>
      <div><label>선반 수</label><input type="number" id="cg_shelves" value="2" min="0" max="10"></div>
    </div>
    <div class="g5" style="margin-bottom:10px">
      <div><label>서랍 수</label><input type="number" id="cg_drawers" value="0" min="0" max="6"></div>
      <div><label>서랍높이 (mm)</label><input type="number" id="cg_drawerH" value="200"></div>
      <div><label>걸레받이 높이</label><input type="number" id="cg_toeH" value="100"></div>
      <div><label>갭 (mm)</label><input type="number" id="cg_gap" value="3" min="0" max="10"></div>
      <div><label>현장명 (메모)</label><input type="text" id="cg_siteName" value="" placeholder="예: 한남하이페리온"></div>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">📐 측판 두께</label>
      <div class="g2">
        <div style="display:flex;gap:8px;align-items:center">
          <span style="font-size:11px;color:#94A3B8;width:60px">좌측판:</span>
          <select id="cg_leftT" style="flex:1">
            <option value="18" selected>18T (18mm)</option>
            <option value="15">15T (15mm)</option>
            <option value="24">24T (24mm)</option>
          </select>
        </div>
        <div style="display:flex;gap:8px;align-items:center">
          <span style="font-size:11px;color:#94A3B8;width:60px">우측판:</span>
          <select id="cg_rightT" style="flex:1">
            <option value="18" selected>18T (18mm)</option>
            <option value="15">15T (15mm)</option>
            <option value="24">24T (24mm)</option>
          </select>
        </div>
      </div>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">🔧 조립구조</label>
      <div class="g2">
        <div>
          <select id="cg_structure" style="width:100%" onchange="cg_structureChanged()">
            <option value="gawa">가와덮음 — 측판이 상하판을 덮음 (기본)</option>
            <option value="chunji">천지판덮음 — 상하판이 측판을 덮음</option>
          </select>
        </div>
        <div>
          <div class="note" id="cg_structureDesc" style="padding:6px 10px;font-size:10px">
            측판 = 전체높이 / 상하판 = 가로 - 좌T - 우T
          </div>
        </div>
      </div>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">옵션</label>
      <span class="chip active" id="cg_back" onclick="this.classList.toggle('active')">뒷판</span>
      <span class="chip active" id="cg_toe" onclick="this.classList.toggle('active')">걸레받이</span>
      <span class="chip" id="cg_nofloor" onclick="this.classList.toggle('active')">바닥없음</span>
      <span class="chip" id="cg_openMode" onclick="this.classList.toggle('active')" style="border-color:#F59E0B">📦 오픈장</span>
    </div>

    <div style="margin-bottom:14px">
      <label style="margin-bottom:6px">📏 엣지 보정 (면당 +1mm)</label>
      <div class="note" style="padding:8px 12px;font-size:10px;margin-bottom:8px">
        엣지테이프 부착 시 판넬 치수가 면당 1mm 증가합니다.<br>
        아래에서 각 부재별 엣지 면을 설정하면 <b>제단치수 = 설계치수 + 엣지보정</b>으로 자동 산출됩니다.
      </div>
      <div class="g3" style="font-size:10px">
        <div>
          <label style="font-size:10px">측판 엣지</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_side_front" checked> 전면</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_side_top"> 상단</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_side_bottom"> 하단</label>
        </div>
        <div>
          <label style="font-size:10px">상하판 엣지</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_tb_front" checked> 전면</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_tb_left"> 좌측</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_tb_right"> 우측</label>
        </div>
        <div>
          <label style="font-size:10px">선반 엣지</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_shelf_front" checked> 전면</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_shelf_left"> 좌측</label>
          <label style="font-size:9px;color:#64748B"><input type="checkbox" id="cg_e_shelf_right"> 우측</label>
        </div>
      </div>
    </div>

    <div style="text-align:center;margin-top:6px;display:flex;gap:10px;justify-content:center">
      <button class="btn" onclick="cg_addToList()" style="padding:10px 30px;font-size:14px;background:#1E3A5F;border:1px solid #3B82F6;color:#60A5FA">
        ➕ 장 추가
      </button>
      <button class="btn btn-cyan" onclick="cg_runAll()" style="padding:10px 40px;font-size:14px">
        ✂️ 재단가이드 생성
      </button>
    </div>
  </div>

  <!-- 장 목록 -->
  <div class="card" id="cg_listCard" style="display:none">
    <h3>📦 입력된 장 목록 <span class="badge tag-cyan" id="cg_listCount">0개</span>
      <button class="btn" onclick="cg_clearList()" style="float:right;padding:3px 10px;font-size:10px;background:#7F1D1D;border:1px solid #991B1B">전체삭제</button>
    </h3>
    <div style="overflow-x:auto"><table style="font-size:11px">
      <thead><tr>
        <th class="tl">No</th><th class="tr">가로</th><th class="tr">높이</th><th class="tr">깊이</th>
        <th class="tr">도어</th><th class="tr">선반</th><th class="tr">구조</th><th class="tl">모드</th><th class="tl">옵션</th><th></th>
      </tr></thead>
      <tbody id="cg_listBody"></tbody>
    </table></div>
  </div>

  <div class="hidden" id="cg_resultArea">
    <!-- 조립 구조도 -->
    <div class="card">
      <h3>🏗️ 조립 구조도</h3>
      <div id="cg_structureDiagram" style="text-align:center"></div>
    </div>

    <!-- 재단 목록 -->
    <div class="card">
      <h3>📋 재단 목록 <span class="badge tag-cyan" id="cg_partCount">0개</span>
        <button class="btn" onclick="cg_print()" style="float:right;padding:4px 14px;font-size:11px;background:#334155;border:1px solid #475569">🖨️ 재단가이드 인쇄</button>
      </h3>
      <div style="overflow-x:auto"><table style="font-size:11px">
        <thead><tr>
          <th class="tl">부재명</th><th class="tr">설계치수(mm)</th><th class="tr">엣지</th>
          <th class="tr" style="color:#F59E0B">✂️ 제단치수(mm)</th><th class="tr">수량</th><th class="tl">비고</th>
        </tr></thead>
        <tbody id="cg_partsBody"></tbody>
      </table></div>
      <div id="cg_edgeSummary" style="margin-top:10px"></div>
    </div>

    <!-- 원장 배치도 -->
    <div class="card">
      <h3>📐 원장 배치도 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 소재별 원장 소요량</span></h3>
      <div id="cg_layoutArea"></div>
    </div>

    <!-- 추가 부재 입력 -->
    <div class="card">
      <h3>➕ 추가 부재</h3>
      <div class="g5" style="margin-bottom:8px">
        <div><label>부재명</label><input type="text" id="cg_addName" value="" placeholder="가와"></div>
        <div><label>가로 (mm)</label><input type="number" id="cg_addW" value=""></div>
        <div><label>세로 (mm)</label><input type="number" id="cg_addH" value=""></div>
        <div><label>수량</label><input type="number" id="cg_addQty" value="1" min="1"></div>
        <div style="display:flex;align-items:flex-end"><button class="btn btn-cyan" onclick="cg_addPart()" style="width:100%">추가</button></div>
      </div>
      <div class="note" style="font-size:10px">추가 부재에도 엣지보정이 필요하면 전면 체크 후 재생성하세요.</div>
    </div>
  </div>
</div>

<!-- ===================== TAB: 합판주문 ===================== -->
<div class="tc" id="tab-order">
  <div class="card" style="border-top-left-radius:0">
    <h3>📋 합판 주문량 계산 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 부재 입력 → 원장 소요량 자동산출</span></h3>

    <div style="margin-bottom:14px;background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px">
      <label style="font-size:12px;color:#E2E8F0;margin-bottom:8px;display:block">📐 원장 정보</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end;margin-bottom:10px">
        <div><label style="font-size:10px">합판 이름</label><input type="text" id="ord_sheetName" value="" style="width:180px" placeholder="예: 아르모니아 스탠다드" oninput="ord_updateInfo()"></div>
        <div><label style="font-size:10px">가로(mm)</label><input type="number" id="ord_sW" value="1220" style="width:85px" oninput="ord_updateInfo()"></div>
        <div><label style="font-size:10px">세로(mm)</label><input type="number" id="ord_sH" value="2745" style="width:85px" oninput="ord_updateInfo()"></div>
        <div><label style="font-size:10px">단가(원)</label><input type="number" id="ord_sP" value="78000" style="width:100px" oninput="ord_updateInfo()"></div>
      </div>
      <div style="margin-bottom:8px">
        <label style="font-size:10px;color:#64748B">빠른 선택</label>
        <select id="ord_sheet" onchange="ord_quickSelect()" style="width:100%">
          <option value="">— 직접 입력 중 —</option>
          <optgroup label="── 도어재 ──">
            <option value="1220,2745,85800,아르모니아 스탠다드">아르모니아 스탠다드 85,800원 (1220×2745)</option>
            <option value="1220,2745,97900,아르모니아 프리미엄">아르모니아 프리미엄 97,900원 (1220×2745)</option>
            <option value="1220,2440,79200,아르모니아 BM1323">아르모니아 BM1323 79,200원 (1220×2440)</option>
            <option value="1220,2745,64900,HP샌드그레이">시온텍 HP샌드그레이 64,900원 (1220×2745)</option>
            <option value="1220,2745,79200,피칸웜그레이우드">시온텍 피칸웜그레이 79,200원 (1220×2745)</option>
            <option value="1220,2745,99000,한솔프리미엄 4×9">한솔프리미엄 4×9 99,000원 (1220×2745)</option>
            <option value="1220,2440,60500,예림 로지핑크">예림 로지핑크 60,500원 (1220×2440)</option>
            <option value="1220,2440,67100,예림 세라믹문">예림 세라믹문 67,100원 (1220×2440)</option>
            <option value="1220,2440,50600,예림 저가PET">예림 저가PET 50,600원 (1220×2440)</option>
            <option value="2100,2800,253000,사비올라 P33/P59">사비올라 P33/P59 233,000원 (2100×2800)</option>
            <option value="1220,2740,85800,포렐스 EC811">포렐스 EC811 85,800원 (1220×2740)</option>
          </optgroup>
          <optgroup label="── 몸통재 ──">
            <option value="1220,2440,30800,예림 18T 몸통">예림 18T 몸통 30,800원 (1220×2440)</option>
            <option value="1220,2440,27500,예림 15T 몸통">예림 15T 몸통 27,500원 (1220×2440)</option>
            <option value="1220,2440,24600,효산 LPM 18T">효산 LPM 18T 24,640원 (1220×2440)</option>
            <option value="1220,2440,22200,효산 LPM 15T">효산 LPM 15T 22,220원 (1220×2440)</option>
            <option value="1220,2440,38500,신길 우드 18T">신길 우드 18T 38,500원 (1220×2440)</option>
            <option value="1220,2440,99000,시온텍 PS보드 18T">시온텍 PS보드 18T 99,000원 (1220×2440)</option>
          </optgroup>
          <optgroup label="── 우라판 ──">
            <option value="1220,2440,16000,예림 우라 3T">예림 우라 3T 15,950원 (1220×2440)</option>
            <option value="1220,2440,14100,효산 우라 4.5T">효산 우라 4.5T 14,080원 (1220×2440)</option>
            <option value="1220,2440,49500,시온텍 우라 5T">시온텍 우라 5T 49,500원 (1220×2440)</option>
          </optgroup>
        </select>
      </div>
      <div id="ord_sheetInfo" class="note" style="padding:6px 10px;font-size:11px"></div>
    </div>

    <!-- 부재 입력 -->
    <div style="margin-bottom:14px">
      <label style="margin-bottom:6px">➕ 부재 추가</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div><label style="font-size:10px">부재명</label><input type="text" id="ord_name" value="도어" style="width:100px" placeholder="도어"></div>
        <div><label style="font-size:10px">가로(mm)</label><input type="number" id="ord_pw" value="" style="width:90px" placeholder="596"></div>
        <div><label style="font-size:10px">세로(mm)</label><input type="number" id="ord_ph" value="" style="width:90px" placeholder="2100"></div>
        <div><label style="font-size:10px">수량</label><input type="number" id="ord_pq" value="1" min="1" style="width:60px"></div>
        <div><label style="font-size:10px">현장/메모</label><input type="text" id="ord_memo" value="" style="width:120px" placeholder="한남1차"></div>
        <button class="btn btn-cyan" onclick="ord_add()" style="padding:8px 20px">추가</button>
      </div>
    </div>

    <div style="margin-bottom:8px">
      <label style="font-size:10px;color:#94A3B8;margin-bottom:4px;display:block">개별 부재 프리셋</label>
      <div style="display:flex;gap:6px;flex-wrap:wrap">
        <button class="btn" onclick="ord_addPreset('하부도어',496,645)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">하부도어 496×645</button>
        <button class="btn" onclick="ord_addPreset('상부도어',496,795)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">상부도어 496×795</button>
        <button class="btn" onclick="ord_addPreset('키큰장도어',596,2200)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">키큰장 596×2200</button>
        <button class="btn" onclick="ord_addPreset('측판',580,2100)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">측판 580×2100</button>
        <button class="btn" onclick="ord_addPreset('상하판',864,580)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">상하판 864×580</button>
        <button class="btn" onclick="ord_addPreset('선반',864,560)" style="padding:3px 8px;font-size:10px;background:#1E2330;border:1px solid #334155">선반 864×560</button>
      </div>
    </div>

    <!-- 오픈장 일괄 추가 -->
    <div style="margin-bottom:14px;background:#1A1D28;border:1px solid #F59E0B44;border-radius:8px;padding:12px">
      <label style="font-size:11px;color:#F59E0B;margin-bottom:8px;display:block">📦 오픈장 일괄 추가 <span style="font-size:9px;color:#94A3B8">(천판+지판+좌측판+우측판+후면판)</span></label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div><label style="font-size:10px">가로(mm)</label><input type="number" id="ord_opW" value="900" style="width:80px"></div>
        <div><label style="font-size:10px">높이(mm)</label><input type="number" id="ord_opH" value="350" style="width:80px"></div>
        <div><label style="font-size:10px">깊이(mm)</label><input type="number" id="ord_opD" value="580" style="width:80px"></div>
        <div><label style="font-size:10px">측판T</label>
          <select id="ord_opT" style="width:65px">
            <option value="18" selected>18T</option>
            <option value="15">15T</option>
            <option value="24">24T</option>
          </select>
        </div>
        <div><label style="font-size:10px">수량</label><input type="number" id="ord_opQty" value="1" min="1" style="width:50px"></div>
        <div><label style="font-size:10px">메모</label><input type="text" id="ord_opMemo" value="" style="width:100px" placeholder="현장명"></div>
        <button class="btn" onclick="ord_addOpen()" style="padding:8px 16px;background:#78350F;border:1px solid #F59E0B;color:#F59E0B">📦 오픈장 추가</button>
      </div>
    </div>

    <!-- 수납장 일괄 추가 -->
    <div style="margin-bottom:14px;background:#1A1D28;border:1px solid #3B82F644;border-radius:8px;padding:12px">
      <label style="font-size:11px;color:#60A5FA;margin-bottom:8px;display:block">🗄️ 수납장 일괄 추가 <span style="font-size:9px;color:#94A3B8">(치수 입력 → 전체 부재 자동분해)</span></label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end;margin-bottom:8px">
        <div><label style="font-size:10px">가로(mm)</label><input type="number" id="ord_cbW" value="900" style="width:75px"></div>
        <div><label style="font-size:10px">높이(mm)</label><input type="number" id="ord_cbH" value="2100" style="width:75px"></div>
        <div><label style="font-size:10px">깊이(mm)</label><input type="number" id="ord_cbD" value="580" style="width:75px"></div>
        <div><label style="font-size:10px">측판T</label>
          <select id="ord_cbT" style="width:60px">
            <option value="18" selected>18T</option>
            <option value="15">15T</option>
            <option value="24">24T</option>
          </select>
        </div>
        <div><label style="font-size:10px">도어</label><input type="number" id="ord_cbDoors" value="2" min="0" style="width:45px"></div>
        <div><label style="font-size:10px">선반</label><input type="number" id="ord_cbShelves" value="2" min="0" style="width:45px"></div>
        <div><label style="font-size:10px">서랍</label><input type="number" id="ord_cbDrawers" value="0" min="0" style="width:45px"></div>
        <div><label style="font-size:10px">서랍H</label><input type="number" id="ord_cbDrwH" value="200" style="width:55px"></div>
      </div>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div><label style="font-size:10px">걸레받이H</label><input type="number" id="ord_cbToeH" value="100" style="width:60px"></div>
        <div style="display:flex;gap:10px;align-items:center;font-size:10px;color:#94A3B8">
          <label><input type="checkbox" id="ord_cbBack" checked> 뒷판</label>
          <label><input type="checkbox" id="ord_cbToe" checked> 걸레받이</label>
          <label><input type="checkbox" id="ord_cbNoFloor"> 바닥없음</label>
        </div>
        <div><label style="font-size:10px">수량</label><input type="number" id="ord_cbQty" value="1" min="1" style="width:45px"></div>
        <div><label style="font-size:10px">메모</label><input type="text" id="ord_cbMemo" value="" style="width:100px" placeholder="현장명"></div>
        <button class="btn" onclick="ord_addCabinet()" style="padding:8px 16px;background:#1E3A5F;border:1px solid #3B82F6;color:#60A5FA">🗄️ 수납장 추가</button>
      </div>
    </div>
  </div>

  <!-- 부재 목록 -->
  <div class="card">
    <h3>📦 입력된 부재 <span class="badge tag-cyan" id="ord_totalParts">0개</span>
      <span style="float:right;display:flex;gap:6px">
        <button class="btn" onclick="ord_save()" style="padding:3px 10px;font-size:10px;background:#1E3A5F;border:1px solid #3B82F6;color:#60A5FA">💾 저장</button>
        <label class="btn" style="padding:3px 10px;font-size:10px;background:#1E3A3F;border:1px solid #10B981;color:#34D399;cursor:pointer;margin:0">
          📂 불러오기<input type="file" accept=".json" onchange="ord_load(event)" style="display:none">
        </label>
        <button class="btn" onclick="ord_clear()" style="padding:3px 10px;font-size:10px;background:#7F1D1D;border:1px solid #991B1B">전체삭제</button>
      </span>
    </h3>
    <div style="overflow-x:auto"><table style="font-size:11px">
      <thead><tr>
        <th class="tl">부재명</th><th class="tr">가로</th><th class="tr">세로</th>
        <th class="tr">면적</th><th class="tr">수량</th><th class="tl">메모</th><th></th>
      </tr></thead>
      <tbody id="ord_listBody"></tbody>
    </table></div>
    <div id="ord_totalArea" class="note" style="margin-top:8px"></div>
  </div>

  <!-- 배치 결과 -->
  <div class="card">
    <h3>📊 원장 배치 결과 <span class="badge tag-yellow" id="ord_sheetCount">0장</span>
      <button class="btn" onclick="ord_print()" style="float:right;padding:4px 14px;font-size:11px;background:#334155;border:1px solid #475569">🖨️ 주문서 출력</button>
    </h3>
    <div id="ord_resultArea"></div>
    <div id="ord_summaryArea" style="margin-top:12px"></div>
  </div>
</div>

<!-- ===================== TAB: 목산견적 ===================== -->
<div class="tc" id="tab-mkquote">
  <div class="card" style="border-top-left-radius:0">
    <h3>🧾 목산 도어 가견적 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 2024 단가표 기반</span></h3>

    <div class="g3" style="margin-bottom:12px">
      <div>
        <label>자재 등급</label>
        <select id="mq_grade" onchange="mq_gradeChanged()">
          <option value="BALANCE" selected>밸런스 / 스마트 무광</option>
          <option value="MANHATTAN">맨하탄 / 5000NC 무광</option>
          <option value="5000P">5000평판 파우더</option>
          <option value="5000">5000평판 무광 (조색비 포함)</option>
          <option value="URBAN">어반</option>
          <option value="PET">PET 화이트/아이보리</option>
          <option value="PET2">PET2 SMR</option>
        </select>
      </div>
      <div>
        <label>마진율 <b id="mq_marginLabel" style="color:#4ADE80">30%</b> <span style="font-size:9px;color:#64748B">(판매가 기준)</span></label>
        <input type="range" id="mq_margin" min="10" max="50" value="30" oninput="document.getElementById('mq_marginLabel').textContent=this.value+'%';mq_recalc()">
      </div>
      <div>
        <label>현장명</label>
        <input type="text" id="mq_site" placeholder="예: 역삼 롯데캐슬" style="width:100%">
      </div>
    </div>

    <div style="margin-bottom:12px">
      <label style="margin-bottom:6px">➕ 품목 추가</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div>
          <label style="font-size:10px">품목</label>
          <select id="mq_cat" onchange="mq_catChanged()" style="width:130px">
            <option value="하부도어">하부도어 (×645)</option>
            <option value="상부도어">상부도어 (×795)</option>
            <option value="마이다">마이다</option>
            <option value="낮은키큰장">낮은키큰장</option>
            <option value="키큰장도어">키큰장도어</option>
            <option value="붙박이도어">붙박이도어 (×2200)</option>
            <option value="몰딩">몰딩류</option>
            <option value="측판">측판 18T</option>
            <option value="걸레받이">걸레받이 (170)</option>
            <option value="멍기둥">멍기둥</option>
            <option value="직접입력">✏️ 직접입력</option>
          </select>
        </div>
        <div>
          <label style="font-size:10px">규격</label>
          <select id="mq_size" style="width:170px"><option>품목 선택</option></select>
        </div>
        <div><label style="font-size:10px">수량</label><input type="number" id="mq_qty" value="1" min="1" style="width:55px"></div>
        <div><label style="font-size:10px">비고</label><input type="text" id="mq_note" value="" style="width:110px" placeholder="무보링, 보링 등"></div>
        <button class="btn btn-cyan" onclick="mq_add()" style="padding:8px 18px">추가</button>
      </div>
      <div id="mq_customRow" style="display:none;margin-top:8px;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div><label style="font-size:10px">품명</label><input type="text" id="mq_cName" style="width:100px" placeholder="도어"></div>
        <div><label style="font-size:10px">가로</label><input type="number" id="mq_cW" style="width:75px" placeholder="mm"></div>
        <div><label style="font-size:10px">세로</label><input type="number" id="mq_cH" style="width:75px" placeholder="mm"></div>
        <div><label style="font-size:10px">매입단가</label><input type="number" id="mq_cP" style="width:90px" placeholder="원"></div>
      </div>
    </div>
  </div>

  <!-- 견적 목록 -->
  <div class="card">
    <h3>📋 견적 내역 <span class="badge tag-cyan" id="mq_count">0건</span>
      <span style="float:right;display:flex;gap:6px">
        <button class="btn" onclick="mq_print()" style="padding:3px 12px;font-size:10px;background:#334155;border:1px solid #475569">🖨️ 견적서 출력</button>
        <button class="btn" onclick="mq_clear()" style="padding:3px 10px;font-size:10px;background:#7F1D1D;border:1px solid #991B1B">전체삭제</button>
      </span>
    </h3>
    <div style="overflow-x:auto"><table style="font-size:11px">
      <thead><tr>
        <th class="tl">품목</th><th class="tr">규격</th><th class="tr">수량</th>
        <th class="tr">매입단가</th><th class="tr" style="color:#4ADE80">판매단가</th>
        <th class="tr">매입합계</th><th class="tr" style="color:#4ADE80">판매합계</th>
        <th class="tl">비고</th><th></th>
      </tr></thead>
      <tbody id="mq_body"></tbody>
      <tfoot id="mq_foot"></tfoot>
    </table></div>
  </div>

  <!-- 요약 -->
  <div id="mq_summary"></div>
</div>

<!-- ===================== TAB: 무니끄 ===================== -->
<div class="tc" id="tab-munique">
  <div class="card" style="border-top-left-radius:0">
    <h3>🚪 무니끄 도어 가견적 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 원장 배치 + 가공비 + 마진</span></h3>

    <div class="g2" style="margin-bottom:12px">
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E2E8F0;margin-bottom:6px;display:block">📐 원장 정보</label>
        <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
          <div><label style="font-size:10px">가로</label><input type="number" id="mn_sheetW" value="1220" style="width:75px"></div>
          <div><label style="font-size:10px">세로</label><input type="number" id="mn_sheetH" value="2420" style="width:75px"></div>
          <div><label style="font-size:10px">원장단가</label><input type="number" id="mn_sheetP" value="450000" style="width:100px"></div>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E2E8F0;margin-bottom:6px;display:block">🔧 가공비 & 마진</label>
        <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
          <div><label style="font-size:10px">큰도어 가공비</label><input type="number" id="mn_bigFee" value="200000" style="width:95px"></div>
          <div><label style="font-size:10px">작은도어 가공비</label><input type="number" id="mn_smallFee" value="100000" style="width:95px"></div>
          <div><label style="font-size:10px">기준세로(mm)</label><input type="number" id="mn_sizeThreshold" value="1200" style="width:75px"></div>
        </div>
        <div class="note" style="margin-top:6px;font-size:9px">세로 ≥ 기준 → 큰도어 / 세로 < 기준 → 작은도어</div>
        <div style="margin-top:8px">
          <label style="font-size:10px">마진율 <b id="mn_marginLabel" style="color:#4ADE80">30%</b></label>
          <input type="range" id="mn_margin" min="10" max="50" value="30" oninput="document.getElementById('mn_marginLabel').textContent=this.value+'%'" style="width:100%">
        </div>
      </div>
    </div>

    <div style="margin-bottom:10px">
      <label style="font-size:10px">현장명</label>
      <input type="text" id="mn_site" placeholder="예: 잠실르엘 103동" style="width:100%">
    </div>

    <!-- 도어 입력 -->
    <div style="margin-bottom:14px">
      <label style="margin-bottom:6px">➕ 도어 추가</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end">
        <div><label style="font-size:10px">구역/위치</label><input type="text" id="mn_zone" value="" style="width:120px" placeholder="주방 하부"></div>
        <div><label style="font-size:10px">가로(mm)</label><input type="number" id="mn_dw" value="" style="width:85px" placeholder="596"></div>
        <div><label style="font-size:10px">세로(mm)</label><input type="number" id="mn_dh" value="" style="width:85px" placeholder="645"></div>
        <div><label style="font-size:10px">수량</label><input type="number" id="mn_dq" value="1" min="1" style="width:55px"></div>
        <button class="btn btn-cyan" onclick="mn_add()" style="padding:8px 20px">추가</button>
      </div>
    </div>
  </div>

  <!-- 도어 목록 -->
  <div class="card">
    <h3>📋 도어 목록 <span class="badge tag-cyan" id="mn_count">0개</span>
      <span style="float:right;display:flex;gap:6px">
        <button class="btn" onclick="mn_print()" style="padding:3px 12px;font-size:10px;background:#334155;border:1px solid #475569">🖨️ 견적서 출력</button>
        <button class="btn" onclick="mn_clear()" style="padding:3px 10px;font-size:10px;background:#7F1D1D;border:1px solid #991B1B">전체삭제</button>
      </span>
    </h3>
    <div style="overflow-x:auto"><table style="font-size:11px">
      <thead><tr>
        <th class="tl">구역</th><th class="tr">가로</th><th class="tr">세로</th>
        <th class="tr">면적</th><th class="tr">수량</th><th class="tr">구분</th><th class="tr">가공비/개</th><th></th>
      </tr></thead>
      <tbody id="mn_body"></tbody>
    </table></div>
  </div>

  <!-- 배치 & 결과 -->
  <div class="card">
    <h3>📊 원장 배치 <span class="badge tag-yellow" id="mn_sheetCount">0장</span></h3>
    <div id="mn_layoutArea"></div>
  </div>

  <!-- 요약 -->
  <div id="mn_summary"></div>
</div>

<!-- ===================== TAB: 개별 부재 ===================== -->
<div class="tc" id="tab-single">
  <div class="card" style="border-top-left-radius:0">
    <h3>📐 개별 부재 단가 계산</h3>
    <div class="g3">
      <div>
        <label>생산 방식</label>
        <select id="s_mode" onchange="s_modeChange()">
          <option value="edifit">에디핏 자체생산</option>
          <option value="homgreen">홈그린 외주</option>
          <option value="sungwoo">성우산업 외주 (10% DC)</option>
          <option value="ilheung">일흥건영 외주 (사비올라/포렐스)</option>
          <option value="moksan">목산 도어공장 (자재+가공)</option>
        </select>
      </div>
      <div>
        <label>자재 선택</label>
        <select id="s_mat" onchange="s_calc()"></select>
      </div>
      <div>
        <label>품목</label>
        <select id="s_cat" onchange="s_calc()"></select>
      </div>
    </div>
    <div class="g5">
      <div><label>가로 (mm)</label><input type="number" id="s_w" placeholder="595" oninput="s_calc()"></div>
      <div><label>세로 (mm)</label><input type="number" id="s_h" placeholder="2100" oninput="s_calc()"></div>
      <div><label>수량</label><input type="number" id="s_qty" value="1" min="1" oninput="s_calc()"></div>
      <div>
        <label>공장배율 <b id="s_factLabel" style="color:#22D3EE">×2.3</b></label>
        <input type="range" id="s_factRate" min="15" max="35" value="23" oninput="document.getElementById('s_factLabel').textContent='×'+(this.value/10).toFixed(1);s_calc()" style="margin-top:6px">
      </div>
      <div>
        <label>영업마진 <b id="s_margLabel" style="color:#4ADE80">30%</b></label>
        <input type="range" id="s_margRate" min="10" max="50" value="30" oninput="document.getElementById('s_margLabel').textContent=this.value+'%';s_calc()" style="margin-top:6px">
      </div>
    </div>

    <div class="hidden" id="s_result">
      <hr class="divider">
      <div class="cost-row">
        <div class="cost-box"><div class="lb">원자재비</div><div class="val" style="color:#94A3B8" id="sr_mat">-</div></div>
        <div class="cost-box"><div class="lb" id="sr_factLabel">공장가 (×2.3)</div><div class="val" style="color:#22D3EE" id="sr_fact">-</div></div>
        <div class="cost-box"><div class="lb" id="sr_sellLabel">판매가 (마진30%)</div><div class="val" style="color:#4ADE80" id="sr_sell">-</div></div>
        <div class="cost-box"><div class="lb">마진액</div><div class="val" style="color:#FACC15" id="sr_margin">-</div></div>
      </div>
      <div style="text-align:center;margin-top:12px">
        <button class="btn btn-primary btn-sm" onclick="s_addItem()">+ 견적에 추가</button>
      </div>
    </div>
  </div>

  <div class="card hidden" id="s_itemsCard">
    <h3 id="s_itemsTitle">📋 견적 항목</h3>
    <div style="overflow-x:auto"><table>
      <thead><tr>
        <th class="tl">품목</th><th class="tl">자재</th><th class="tl">사이즈</th><th class="tl">방식</th>
        <th class="tr">수량</th><th class="tr">공장가/매입가</th><th class="tr">판매가</th><th class="tr">합계</th><th></th>
      </tr></thead>
      <tbody id="s_itemsBody"></tbody>
    </table></div>
    <div class="cost-row" id="s_summary"></div>
  </div>
</div>

<!-- ===================== TAB: 자재 DB ===================== -->
<div class="tc" id="tab-matdb">
  <div class="card" style="border-top-left-radius:0">
    <h3>📦 자재 단가 DB (원소스)</h3>
    <p class="note" style="margin:-8px 0 14px">에디핏 원자재 매입 단가 현황. 합판자재원가정리 원본 데이터 기준.</p>
    <div style="overflow-x:auto"><table>
      <thead><tr>
        <th class="tl">공급처</th><th class="tl">종류</th><th class="tl">두께</th>
        <th class="tl">이름</th><th class="tr">단가(원)</th><th class="tl">비고</th>
      </tr></thead>
      <tbody id="db_body"></tbody>
    </table></div>
  </div>

  <div class="card">
    <h3>🎨 영앤썬 아르모니아 (홈그린 도어재)</h3>
    <table>
      <thead><tr><th class="tl">등급</th><th class="tl">색상</th><th class="tl">사이즈</th><th class="tr">공급가</th></tr></thead>
      <tbody>
        <tr><td><span class="tag tag-blue">Standard</span></td><td>BM1323, 1325</td><td>1220×2440×18</td><td class="tr" style="font-weight:600">79,200원</td></tr>
        <tr><td><span class="tag tag-blue">Standard</span></td><td>BM1050~1251, 1112</td><td>1220×2745×18</td><td class="tr" style="font-weight:600">85,800원</td></tr>
        <tr><td><span class="tag tag-pink">Premium</span></td><td>BM1180~1206, BMP</td><td>1220×2745×18</td><td class="tr" style="font-weight:600">97,900원</td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- ===================== TAB: 설정 ===================== -->
<div class="tc" id="tab-settings">
  <!-- m당 단가 공식 -->
  <div class="card" style="border-top-left-radius:0">
    <h3>📏 m당 단가 공식</h3>
    <div class="g3" style="margin-bottom:12px">
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#60A5FA;margin-bottom:6px;display:block">📦 몸통재</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pm_bodyP" value="35000" style="width:90px" oninput="pm_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pm_bodyQ" value="4" style="width:50px" oninput="pm_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pm_bodyTotal" style="font-weight:600;color:#60A5FA">140,000</span>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#4ADE80;margin-bottom:6px;display:block">🪵 우라판</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pm_uraP" value="20000" style="width:90px" oninput="pm_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pm_uraQ" value="2" style="width:50px" oninput="pm_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pm_uraTotal" style="font-weight:600;color:#4ADE80">40,000</span>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E879F9;margin-bottom:6px;display:block">🎨 도어재</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pm_doorP" value="100000" style="width:90px" oninput="pm_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pm_doorQ" value="2" style="width:50px" oninput="pm_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pm_doorTotal" style="font-weight:600;color:#E879F9">200,000</span>
        </div>
      </div>
    </div>
    <div class="g3" style="margin-bottom:12px">
      <div>
        <label style="font-size:10px">나누기 m수</label>
        <input type="number" id="pm_meter" value="4.8" step="0.1" style="width:100%" oninput="pm_calc()">
      </div>
      <div>
        <label style="font-size:10px">공장가 배율</label>
        <input type="number" id="pm_factRate" value="2.5" step="0.1" style="width:100%" oninput="pm_calc()">
      </div>
      <div>
        <label style="font-size:10px">마진율 (%)</label>
        <input type="number" id="pm_margin" value="30" min="0" max="50" style="width:100%" oninput="pm_calc()">
      </div>
    </div>
    <div id="pm_result"></div>
  </div>

  <!-- 자당가 공식 -->
  <div class="card">
    <h3>🗄️ 자당가 공식 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 4자 기준 원가 → 공장도가 → 영업금액</span></h3>
    <div class="g3" style="margin-bottom:12px">
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#60A5FA;margin-bottom:6px;display:block">📦 몸통재</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pc_bodyP" value="35000" style="width:90px" oninput="pc_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pc_bodyQ" value="4" style="width:50px" oninput="pc_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pc_bodyTotal" style="font-weight:600;color:#60A5FA">140,000</span>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#4ADE80;margin-bottom:6px;display:block">🪵 우라판</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pc_uraP" value="20000" style="width:90px" oninput="pc_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pc_uraQ" value="1" style="width:50px" oninput="pc_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pc_uraTotal" style="font-weight:600;color:#4ADE80">20,000</span>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E879F9;margin-bottom:6px;display:block">🎨 도어재</label>
        <div style="display:flex;gap:8px;align-items:center">
          <div><label style="font-size:10px">장당 단가</label><input type="number" id="pc_doorP" value="100000" style="width:90px" oninput="pc_calc()"></div>
          <span style="color:#64748B">×</span>
          <div><label style="font-size:10px">장수</label><input type="number" id="pc_doorQ" value="1" style="width:50px" oninput="pc_calc()"></div>
          <span style="color:#64748B">=</span>
          <span id="pc_doorTotal" style="font-weight:600;color:#E879F9">100,000</span>
        </div>
      </div>
    </div>
    <div class="g3" style="margin-bottom:12px">
      <div>
        <label style="font-size:10px">기준 (자)</label>
        <input type="number" id="pc_unit" value="4" step="1" style="width:100%" oninput="pc_calc()">
      </div>
      <div>
        <label style="font-size:10px">공장가 배율</label>
        <input type="number" id="pc_factRate" value="2" step="0.1" style="width:100%" oninput="pc_calc()">
      </div>
      <div>
        <label style="font-size:10px">마진율 (%)</label>
        <input type="number" id="pc_margin" value="30" min="0" max="50" style="width:100%" oninput="pc_calc()">
      </div>
    </div>
    <div id="pc_result"></div>
  </div>

  <!-- 자재 소요량 계산기 -->
  <div class="card">
    <h3>📊 자재 소요량 계산 <span style="font-size:11px;color:#94A3B8;font-weight:400">— 장 치수 → 합판 몇장?</span></h3>

    <div class="g3" style="margin-bottom:10px">
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E2E8F0;margin-bottom:6px;display:block">📐 장 치수</label>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <div><label style="font-size:10px">가로(mm)</label><input type="number" id="su_w" value="900" style="width:80px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">높이(mm)</label><input type="number" id="su_h" value="2100" style="width:80px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">깊이(mm)</label><input type="number" id="su_d" value="580" style="width:80px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">측판T</label>
            <select id="su_t" style="width:60px" onchange="su_calc()">
              <option value="18" selected>18T</option>
              <option value="15">15T</option>
              <option value="24">24T</option>
            </select>
          </div>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E2E8F0;margin-bottom:6px;display:block">🚪 구성</label>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <div><label style="font-size:10px">도어</label><input type="number" id="su_doors" value="2" min="0" style="width:50px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">선반</label><input type="number" id="su_shelves" value="2" min="0" style="width:50px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">서랍</label><input type="number" id="su_drawers" value="0" min="0" style="width:50px" oninput="su_calc()"></div>
          <div><label style="font-size:10px">걸레받이H</label><input type="number" id="su_toeH" value="100" style="width:60px" oninput="su_calc()"></div>
        </div>
      </div>
      <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:12px">
        <label style="font-size:11px;color:#E2E8F0;margin-bottom:6px;display:block">⚙️ 옵션</label>
        <div style="display:flex;flex-direction:column;gap:6px;font-size:11px">
          <label style="color:#94A3B8"><input type="checkbox" id="su_back" checked onchange="su_calc()"> 뒷판</label>
          <label style="color:#94A3B8"><input type="checkbox" id="su_toe" checked onchange="su_calc()"> 걸레받이</label>
          <label style="color:#94A3B8"><input type="checkbox" id="su_nofloor" onchange="su_calc()"> 바닥없음</label>
          <select id="su_mode" style="font-size:10px" onchange="su_calc()">
            <option value="normal">일반 (몸통+도어+우라)</option>
            <option value="allDoor">전부 도어재 (오픈장)</option>
            <option value="noUra">뒷판도 몸통재</option>
          </select>
        </div>
      </div>
    </div>

    <div class="g3" style="margin-bottom:10px">
      <div>
        <label style="font-size:10px">도어재 원장 (mm × mm × 원)</label>
        <div style="display:flex;gap:4px">
          <input type="number" id="su_doorShW" value="1220" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_doorShH" value="2745" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_doorShP" value="85800" style="width:85px" oninput="su_calc()">
        </div>
      </div>
      <div>
        <label style="font-size:10px">몸통재 원장 (mm × mm × 원)</label>
        <div style="display:flex;gap:4px">
          <input type="number" id="su_bodyShW" value="1220" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_bodyShH" value="2440" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_bodyShP" value="30800" style="width:85px" oninput="su_calc()">
        </div>
      </div>
      <div>
        <label style="font-size:10px">우라판 원장 (mm × mm × 원)</label>
        <div style="display:flex;gap:4px">
          <input type="number" id="su_uraShW" value="1220" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_uraShH" value="2440" style="width:70px" oninput="su_calc()">
          <input type="number" id="su_uraShP" value="15950" style="width:85px" oninput="su_calc()">
        </div>
      </div>
    </div>

    <div id="su_result"></div>
  </div>

  <div class="card">
    <h3>⚙️ 외주 가공업체 설정</h3>
    <p class="note" style="margin:-8px 0 14px">업체별 단가율을 설정합니다. 홈그린은 명세서 기반 역산 데이터가 입력되어 있습니다.</p>

    <h4 style="font-size:13px;color:#60A5FA;margin:14px 0 8px">🏭 홈그린 (데이터 입력됨)</h4>
    <table>
      <thead><tr><th class="tl">품목</th><th class="tr">BM1112 (원/1000mm²)</th><th class="tr">BM1201 (원/1000mm²)</th></tr></thead>
      <tbody id="set_hgBody"></tbody>
    </table>

    <hr class="divider">
    <h4 style="font-size:13px;color:#FB923C;margin:0 0 8px">🏭 성우산업 (데이터 입력됨 · 10% DC 적용)</h4>
    <p class="note" style="margin-bottom:8px">동탄한화프레스티지, 영통포레파크, 도곡렉슬 명세서 기반 역산. 매출 10% DC 적용 후 단가.</p>
    <table>
      <thead><tr><th class="tl">품목</th><th class="tr">한솔계열 (원/1000mm²)</th><th class="tr">프리미엄 (원/1000mm²)</th></tr></thead>
      <tbody id="set_swBody"></tbody>
    </table>

    <hr class="divider">
    <h4 style="font-size:13px;color:#34D399;margin:0 0 8px">🏭 일흥건영 (데이터 입력됨 · 자재+가공 포함가)</h4>
    <p class="note" style="margin-bottom:8px">사비올라 P33/P59, 포렐스 EC811 견적서 기반. 한남하이페리온, 도곡레미안 등 실데이터 역산.</p>
    <table>
      <thead><tr><th class="tl">품목</th><th class="tr">포렐스 EC811</th><th class="tr">사비올라 P33</th><th class="tr">사비올라 P59</th></tr></thead>
      <tbody id="set_jhBody"></tbody>
    </table>
    <div class="note" style="margin-top:8px">
      <b>원판 공급가:</b> 포렐스 EC811 85,800원 (1220×2740×18T) · 사비올라 P23 233,000원 (2100×2800×19T)<br>
      <b>엣지:</b> 포렐스 400원/m
    </div>

    <hr class="divider">
    <h4 style="font-size:13px;color:#F59E0B;margin:0 0 8px">🏭 목산 도어공장 (데이터 입력됨 · 자재+가공 포함)</h4>
    <p class="note" style="margin-bottom:8px">2024 단가표 기반. 사이즈별 고정가를 면적비례 단가율로 환산 (496mm 기준). 12개 자재등급.</p>
    <div style="overflow-x:auto"><table style="font-size:10px">
      <thead><tr><th class="tl">품목</th><th class="tr">PET</th><th class="tr">PET2</th><th class="tr">데이지</th><th class="tr">3000습식</th><th class="tr">어반</th><th class="tr">건식애쉬</th><th class="tr">5000무광</th><th class="tr">건식오크</th><th class="tr">맨하탄</th></tr></thead>
      <tbody id="set_mkBody"></tbody>
    </table></div>
    <div class="note" style="margin-top:8px">
      <b>참고:</b> 목산은 사이즈별 고정가 방식이므로, 위 단가율은 근사치입니다. 정확한 가격은 원본 단가표를 참고하세요.<br>
      추가 고급자재: 5000파우더, 훈증무늬목, 염색무늬목도 계산기에서 선택 가능합니다.
    </div>
  </div>

  <div class="card">
    <h3>💡 계산 로직 설명</h3>
    <div class="note">
      <b>에디핏 자체생산:</b><br>
      원자재비 (합판원가 면적비례) → 공장가 = 원자재비 × 배율(2.0~3.5) → 판매가 = 공장가 ÷ (1-마진율)<br><br>
      <b>외주 가공 (홈그린 등):</b><br>
      외주 매입가 (면적×품목별 단가율) → 판매가 = 매입가 ÷ (1-마진율)<br><br>
      <b>혼합 (도어만 외주):</b><br>
      몸통 = 에디핏 공장가 / 도어 = 외주 매입가 → 합산 → 판매가 = 합산 ÷ (1-마진율)<br><br>
      <b>영업마진 계산:</b> 판매가의 30% = 공장가 ÷ 0.7 (금액에서 30% 추가가 아님)
    </div>
  </div>
</div>

</div>

<script>
// ===== CONSTANTS =====
const fmt = v => Math.round(v).toLocaleString('ko-KR');
const CATS = ['도어','EP','서랍도어','폴딩도어','걸레받이','목찬넬','선반','쫄대'];
const HG_RATES = {
  BM1112:{도어:83,EP:80,서랍도어:102,폴딩도어:90,걸레받이:120,목찬넬:135,선반:116,쫄대:95},
  BM1201:{도어:92,EP:80,서랍도어:108,폴딩도어:95,걸레받이:130,목찬넬:140,선반:125,쫄대:100},
  BM1323:{도어:85,EP:82,서랍도어:104,폴딩도어:92,걸레받이:122,목찬넬:137,선반:118,쫄대:97},
};
// 성우산업 단가율 (원/1000mm²) - 명세서 역산, 10% DC 적용 후
// 자재: 한솔계열(안도크림,콘크리트화,포그그레이,크림화), 프리미엄(클레이크림,바이브실버)
const SW_RATES = {
  standard:{도어:52,EP:43,서랍도어:56,폴딩도어:52,걸레받이:90,목찬넬:100,선반:55,쫄대:75,
    label:'한솔계열 (안도크림,포그그레이 등)', dc:0.9},
  premium:{도어:61,EP:47,서랍도어:65,폴딩도어:58,걸레받이:100,목찬넬:110,선반:62,쫄대:82,
    label:'프리미엄 (클레이크림,바이브실버)', dc:0.9},
};
const MIN_SW = 7100; // 성우 최소단가 (10%DC 적용후)

// 일흥건영 단가율 (원/1000mm²) - 사비올라/포렐스 명세서 역산 (자재+가공 포함가)
const JH_RATES = {
  'P33':{ // 사비올라 P33
    도어:105,EP:95,서랍도어:108,폴딩도어:130,걸레받이:130,목찬넬:200,선반:110,쫄대:105,
    label:'사비올라 P33', sheetW:2100, sheetH:2800, sheetT:'19T', sheetPrice:253000
  },
  'P59':{ // 사비올라 P59 (가장 많은 데이터)
    도어:102,EP:97,서랍도어:100,폴딩도어:120,걸레받이:134,목찬넬:200,선반:146,쫄대:140,
    label:'사비올라 P59', sheetW:2100, sheetH:2800, sheetT:'19T', sheetPrice:253000
  },
  'EC811':{ // 포렐스 EC811
    도어:68,EP:60,서랍도어:72,폴딩도어:120,걸레받이:75,목찬넬:150,선반:70,쫄대:75,
    label:'포렐스 EC811', sheetW:1220, sheetH:2740, sheetT:'18T', sheetPrice:85800
  },
};
const MIN_JH = 22000; // 일흥건영 최소단가
const FORELES_EDGE = 440; // 포렐스 엣지 원/m

// 목산 도어공장 단가율 (원/1000mm²) - 2024 단가표 역산, 자재+가공 포함
// 사이즈별 고정가를 면적비례 단가율로 환산 (중간사이즈 496mm 기준)
const MK_RATES = {
  'PET':{도어:53,EP:47,서랍도어:56,폴딩도어:53,걸레받이:49,목찬넬:80,선반:50,쫄대:50,
    label:'PET 화이트/아이보리',tier:'저가'},
  'PET2':{도어:60,EP:52,서랍도어:63,폴딩도어:60,걸레받이:55,목찬넬:85,선반:55,쫄대:55,
    label:'PET2 SMR PET',tier:'중저가'},
  'DAISY':{도어:92,EP:50,서랍도어:95,폴딩도어:92,걸레받이:47,목찬넬:58,선반:52,쫄대:50,
    label:'데이지 솔리드크림/우드화이트',tier:'중저가'},
  'URBAN':{도어:115,EP:103,서랍도어:118,폴딩도어:115,걸레받이:88,목찬넬:120,선반:108,쫄대:105,
    label:'어반 화이트오크/내추럴/다크오크',tier:'중고가'},
  '5000':{도어:150,EP:117,서랍도어:155,폴딩도어:150,걸레받이:96,목찬넬:130,선반:120,쫄대:115,
    label:'5000평판 무광 (조색비 포함)',tier:'고가'},
  '5000P':{도어:167,EP:130,서랍도어:170,폴딩도어:167,걸레받이:105,목찬넬:145,선반:133,쫄대:128,
    label:'5000평판 파우더',tier:'고가'},
  'MANHATTAN':{도어:185,EP:140,서랍도어:190,폴딩도어:185,걸레받이:96,목찬넬:130,선반:140,쫄대:130,
    label:'맨하탄/5000NC 무광',tier:'프리미엄'},
  'ASH':{도어:130,EP:106,서랍도어:135,폴딩도어:130,걸레받이:100,목찬넬:140,선반:115,쫄대:110,
    label:'건식애쉬 내추럴(수성)',tier:'고가'},
  'OAKN':{도어:148,EP:120,서랍도어:152,폴딩도어:148,걸레받이:120,목찬넬:160,선반:130,쫄대:125,
    label:'건식오크 내추럴',tier:'프리미엄'},
  'WET3000':{도어:85,EP:65,서랍도어:88,폴딩도어:85,걸레받이:68,목찬넬:90,선반:70,쫄대:68,
    label:'3000 습식무늬목',tier:'중가'},
  'SMOKE':{도어:200,EP:160,서랍도어:205,폴딩도어:200,걸레받이:120,목찬넬:160,선반:170,쫄대:155,
    label:'훈증무늬목',tier:'최고급'},
  'DYE':{도어:220,EP:176,서랍도어:225,폴딩도어:220,걸레받이:132,목찬넬:176,선반:187,쫄대:170,
    label:'염색무늬목',tier:'최고급'},
};
const MIN_MK = 9000; // 목산 최소단가

// 재단가이드 출력용 글로벌 데이터
let CUT_GUIDE_DATA = null;
const MIN_HG = 8500;

// 자재DB
const MAT_DB = [
  {sup:'P&R(남태옥)',type:'몸통재PB',t:'18T',name:'효산 LPM N202 18T',price:24600,note:'운임적불'},
  {sup:'P&R(남태옥)',type:'몸통재PB',t:'15T',name:'효산 LPM N202 15T',price:22200,note:''},
  {sup:'P&R(남태옥)',type:'우라판',t:'4.5T',name:'효산 LPM N202 우라',price:14100,note:''},
  {sup:'P&R(남태옥)',type:'엣지',t:'',name:'효산 LPM 엣지',price:15400,note:''},
  {sup:'P&R(남태옥)',type:'운송비',t:'',name:'운임비',price:93500,note:''},
  {sup:'배병선',type:'스티커',t:'18파이',name:'스티커 14,000개 18파이',price:92400,note:''},
  {sup:'신길합판',type:'몸통재PB',t:'18T',name:'신길 우드 N653 18T',price:38500,note:'운임적불'},
  {sup:'신길합판',type:'몸통재PB',t:'3T',name:'신길 우라 N653 6T',price:33000,note:''},
  {sup:'신길합판',type:'엣지',t:'',name:'신길 N653 엣지',price:29700,note:''},
  {sup:'신길합판',type:'스티커',t:'',name:'신길 N653 스티커',price:2750,note:''},
  {sup:'시온텍',type:'몸통재',t:'18T',name:'wpc방수보드 양면pp 18T',price:99000,note:'몸통재'},
  {sup:'시온텍',type:'도어재',t:'18T',name:'wpc방수보드 양면PET 도어',price:145200,note:'도어재'},
  {sup:'시온텍',type:'우라판',t:'5T',name:'wpc방수보드 양면pp 우라',price:49500,note:'우라'},
  {sup:'시온텍',type:'도어재',t:'18T',name:'HP샌드그레이(스페셜)',price:64900,note:''},
  {sup:'시온텍',type:'엣지',t:'22m',name:'HP샌드그레이(스페셜) 엣지',price:44600,note:''},
  {sup:'시온텍',type:'도어재',t:'18T',name:'피칸웜그레이우드',price:79200,note:''},
  {sup:'시온텍',type:'엣지',t:'',name:'피칸웜그레이우드 엣지',price:24200,note:''},
  {sup:'시온텍',type:'도어재',t:'lpm,mdf',name:'후면 LPM 도어재',price:42900,note:''},
  {sup:'가공보드',type:'도어재',t:'18T',name:'4*9합판,한솔프리미엄',price:99000,note:''},
  {sup:'가공보드',type:'도어재',t:'18T',name:'한솔패트 30T',price:157300,note:''},
  {sup:'가공보드',type:'도어재',t:'18T',name:'양면패트 한솔',price:121000,note:''},
  {sup:'가공보드',type:'엣지',t:'100m',name:'30T 패트용 100m',price:39600,note:''},
  {sup:'예림',type:'도어재',t:'18T',name:'로지핑크 도어재',price:60500,note:'합판미수500까지'},
  {sup:'예림',type:'엣지',t:'100m',name:'로지핑크엣지',price:22000,note:''},
  {sup:'예림',type:'도어재',t:'18T',name:'새틴얼그레이 도어재',price:74800,note:''},
  {sup:'예림',type:'엣지',t:'100m',name:'새틴얼그레이 엣지',price:48400,note:''},
  {sup:'예림',type:'도어재',t:'18T',name:'세라믹 문 퍼시픽 도어재',price:67100,note:''},
  {sup:'예림',type:'엣지',t:'100m',name:'세라믹 문 퍼시픽 엣지',price:26400,note:''},
  {sup:'예림',type:'도어재',t:'18T',name:'저가pet 도어',price:50600,note:''},
  {sup:'예림',type:'엣지',t:'100m',name:'저가pet 엣지',price:22000,note:''},
  {sup:'예림',type:'몸통재PB',t:'15T',name:'15T 몸통합판 예림',price:27500,note:''},
  {sup:'예림',type:'몸통재PB',t:'18T',name:'18T 몸통합판 예림',price:30800,note:''},
  {sup:'예림',type:'몸통재PB',t:'향균',name:'18T 향균 몸통합판 예림',price:31900,note:''},
  {sup:'예림',type:'엣지',t:'18mm',name:'18mm엣지 예림',price:9900,note:''},
  {sup:'예림',type:'엣지',t:'21mm',name:'21mm엣지 예림',price:11600,note:''},
  {sup:'예림',type:'우라판',t:'2.7T',name:'예림모시화이트 3T 우라',price:16000,note:''},
  {sup:'메라톤',type:'도어재',t:'4*8',name:'8835BS 저가형 도어재',price:121000,note:''},
  {sup:'메라톤',type:'도어재',t:'4*8',name:'8835BS 고급형 도어재',price:150700,note:''},
  {sup:'메라톤',type:'엣지',t:'200m',name:'200m 1롤',price:110000,note:''},
  {sup:'사비올라',type:'도어재',t:'19T',name:'사비올라 P23 (2100×2800)',price:253000,note:'일흥건영 취급'},
  {sup:'사비올라',type:'도어재',t:'19T',name:'사비올라 P33 (2100×2800)',price:253000,note:'일흥건영 취급'},
  {sup:'사비올라',type:'도어재',t:'19T',name:'사비올라 P59 (2100×2800)',price:253000,note:'일흥건영 취급'},
  {sup:'포렐스',type:'도어재',t:'18T',name:'포렐스 EC811 (1220×2740)',price:85800,note:'일흥건영 취급'},
  {sup:'포렐스',type:'엣지',t:'m',name:'포렐스 엣지',price:440,note:'원/m'},
];

// ===== TABS =====
function switchTab(id){
  document.querySelectorAll('.tab').forEach((t,i)=>{
    const ids=['cabinet','cutguide','order','mkquote','munique','single','matdb','settings'];
    t.classList.toggle('active',ids[i]===id);
  });
  document.querySelectorAll('.tc').forEach(c=>c.classList.remove('active'));
  document.getElementById('tab-'+id).classList.add('active');
}

// ===== MATERIAL DB TAB =====
function renderDB(){
  const body=document.getElementById('db_body');
  let lastSup='';
  MAT_DB.forEach(r=>{
    const tr=document.createElement('tr');
    const supCell=r.sup!==lastSup?r.sup:'';
    lastSup=r.sup;
    const typeTag=r.type.includes('도어')?'tag-pink':r.type.includes('몸통')?'tag-blue':r.type.includes('엣지')?'tag-yellow':r.type.includes('우라')?'tag-green':'tag-cyan';
    tr.innerHTML=`<td style="font-weight:${supCell?600:400};color:${supCell?'#E2E8F0':'#64748B'}">${supCell}</td>
      <td><span class="tag ${typeTag}">${r.type}</span></td><td>${r.t}</td>
      <td>${r.name}</td><td class="tr" style="font-weight:600">${fmt(r.price)}원</td><td style="color:#64748B">${r.note}</td>`;
    body.appendChild(tr);
  });
}

// ===== SETTINGS TAB =====
// ===== 목산 견적 TAB =====
const MK_PRICE = {
  BALANCE:{label:'밸런스/스마트 무광',
    하부도어:{645:{296:49000,346:56000,396:60000,446:66000,496:76000,546:81000,596:85000}},
    상부도어:{795:{296:57000,346:63000,396:71000,446:77000,496:83000,546:86000,596:96000}},
    마이다:{213:{396:36000,496:38000,596:40000},321:{396:41000,446:43000,496:45000,596:49000}},
    낮은키큰장:{895:{296:64000,396:76000,496:93000,596:110000},995:{296:68000,396:82000,496:102000,596:121000}},
    키큰장도어:{1195:{296:76000,396:99000,496:121000,596:140000},1495:{396:117000,496:147000,596:170000},1795:{396:130000,496:160000,596:189000}},
    붙박이도어:{2200:{296:136000,346:148000,396:160000,446:172000,496:184000,546:197000,596:209000}},
    몰딩:{써라운딩70:32000,써라운딩100:36000,써라운딩150:52000},걸레받이:39000,멍기둥:19000,
    측판:{2400:{610:171000,650:188000,710:204000},800:{400:51000},900:{600:80000}}
  },
  MANHATTAN:{label:'맨하탄/5000NC 무광',
    하부도어:{645:{296:49000,346:56000,396:60000,446:66000,496:76000,546:81000,596:85000}},
    상부도어:{795:{296:57000,346:63000,396:71000,446:77000,496:83000,546:86000,596:96000}},
    마이다:{213:{396:36000,496:38000,596:40000},321:{396:41000,446:43000,496:45000,596:49000}},
    낮은키큰장:{895:{296:64000,396:76000,496:93000,596:110000},995:{296:68000,396:82000,496:102000,596:121000}},
    키큰장도어:{1195:{296:76000,396:99000,496:121000,596:140000},1495:{396:117000,496:136000,596:157000},1795:{396:130000,496:160000,596:189000}},
    붙박이도어:{2200:{296:136000,346:148000,396:160000,446:172000,496:184000,546:197000,596:209000}},
    몰딩:{써라운딩70:32000,써라운딩100:36000,써라운딩150:52000},걸레받이:39000,멍기둥:19000,
    측판:{2400:{610:171000,650:188000,710:204000},800:{400:51000},900:{600:80000}}
  },
  '5000P':{label:'5000평판 파우더',
    하부도어:{645:{296:38000,346:46000,396:50000,446:57000,496:62000,546:68000,596:72000}},
    상부도어:{795:{296:44000,346:50000,396:57000,446:62000,496:69000,546:72000,596:83000}},
    마이다:{213:{396:26000,496:28000,596:30000},321:{396:30000,446:32000,496:35000,596:38000}},
    낮은키큰장:{895:{296:49000,396:62000,496:75000,596:88000},995:{296:53000,396:69000,496:85000,596:101000}},
    키큰장도어:{1195:{296:62000,396:82000,496:101000,596:121000},1495:{396:94000,496:117000,596:140000},1795:{396:113000,496:140000,596:167000}},
    붙박이도어:{2200:{296:117000,346:130000,396:143000,446:157000,496:170000,546:184000,596:189000}},
    몰딩:{써라운딩70:36000,써라운딩100:40000,써라운딩150:58000},걸레받이:43000,멍기둥:21000,
    측판:{2400:{610:189000,650:207000,710:225000},800:{400:57000},900:{600:88000}}
  },
  '5000':{label:'5000평판 무광 (조색비 포함)',
    하부도어:{645:{296:34000,346:41000,396:45000,446:51000,496:56000,546:61000,596:65000}},
    상부도어:{795:{296:40000,346:45000,396:51000,446:56000,496:62000,546:65000,596:75000}},
    마이다:{213:{396:23000,496:25000,596:27000},321:{396:27000,446:29000,496:31000,596:34000}},
    낮은키큰장:{895:{296:44000,396:56000,496:68000,596:80000},995:{296:48000,396:62000,496:77000,596:91000}},
    키큰장도어:{1195:{296:56000,396:74000,496:91000,596:110000},1495:{396:85000,496:106000,596:127000},1795:{396:102000,496:127000,596:151000}},
    붙박이도어:{2200:{296:106000,346:118000,396:130000,446:142000,496:154000,546:167000,596:171000}},
    몰딩:{써라운딩70:32000,써라운딩100:36000,써라운딩150:52000},걸레받이:39000,멍기둥:19000,
    측판:{2400:{610:171000,650:188000,710:204000},800:{400:51000},900:{600:80000}}
  },
  URBAN:{label:'어반',
    하부도어:{645:{296:27000,346:30000,396:34000,446:37000,496:40000,546:43000,596:46000}},
    상부도어:{795:{296:30000,346:33000,396:36000,446:40000,496:43000,546:46000,596:50000}},
    마이다:{213:{396:16000,496:18000,596:20000},321:{396:20000,446:22000,496:25000,596:27000}},
    낮은키큰장:{895:{296:32000,396:40000,496:49000,596:59000},995:{296:35000,396:44000,496:54000,596:65000}},
    키큰장도어:{1195:{296:41000,396:53000,496:65000,596:77000},1495:{396:65000,496:81000,596:96000},1795:{396:77000,496:96000,596:116000}},
    붙박이도어:{2200:{296:71000,346:83000,396:94000,446:106000,496:118000,546:130000,596:141000}},
    몰딩:{써라운딩70:29000,써라운딩100:31000,써라운딩150:42000},걸레받이:36000,멍기둥:13000,
    측판:{2400:{610:141000,650:164000,710:184000},800:{400:36000},900:{600:59000}}
  },
  PET:{label:'PET 화이트/아이보리',
    하부도어:{645:{296:12000,346:13000,396:15000,446:16000,496:17000,546:18000,596:19000}},
    상부도어:{795:{296:14000,346:15000,396:16000,446:18000,496:19000,546:21000,596:23000}},
    마이다:{213:{396:9000,496:10000,596:11000},321:{396:10000,446:11000,496:12000,596:12000}},
    낮은키큰장:{895:{296:16000,396:19000,496:22000,596:26000},995:{296:18000,396:22000,496:25000,596:29000}},
    키큰장도어:{1195:{296:20000,396:26000,496:31000,596:36000},1495:{396:33000,496:40000,596:46000},1795:{396:44000,496:53000,596:60000}},
    붙박이도어:{2200:{296:42000,346:46000,396:50000,446:54000,496:59000,546:63000,596:69000}},
    몰딩:{써라운딩70:12000,써라운딩100:16000,써라운딩150:21000},걸레받이:20000,멍기둥:9000,
    측판:{2400:{610:69000,650:75000,710:79000},800:{400:16000},900:{600:26000}}
  },
  PET2:{label:'PET2 SMR',
    하부도어:{645:{296:14000,346:15000,396:17000,446:18000,496:19000,546:20000,596:21000}},
    상부도어:{795:{296:16000,346:17000,396:18000,446:20000,496:21000,546:24000,596:26000}},
    마이다:{213:{396:10000,496:11000,596:13000},321:{396:11000,446:13000,496:14000,596:14000}},
    낮은키큰장:{895:{296:18000,396:21000,496:25000,596:29000},995:{296:20000,396:25000,496:28000,596:32000}},
    키큰장도어:{1195:{296:22000,396:29000,496:35000,596:40000},1495:{396:37000,496:44000,596:51000},1795:{396:49000,496:59000,596:66000}},
    붙박이도어:{2200:{296:47000,346:51000,396:55000,446:60000,496:65000,546:70000,596:76000}},
    몰딩:{써라운딩70:13000,써라운딩100:18000,써라운딩150:24000},걸레받이:22000,멍기둥:10000,
    측판:{2400:{610:76000,650:83000,710:87000},800:{400:18000},900:{600:29000}}
  }
};

let MQ_ITEMS = [];

function mq_getSizes(grade, cat){
  const g=MK_PRICE[grade];if(!g) return [];
  const sizes=[];
  if(cat==='몰딩'){
    Object.keys(g.몰딩).forEach(k=>sizes.push({label:k,price:g.몰딩[k],spec:k}));
  } else if(cat==='걸레받이'){
    sizes.push({label:'걸레받이 (170) 2400',price:g.걸레받이,spec:'170×2400'});
  } else if(cat==='멍기둥'){
    sizes.push({label:'멍기둥',price:g.멍기둥,spec:'멍기둥'});
  } else if(g[cat]){
    const catData=g[cat];
    Object.keys(catData).forEach(h=>{
      const hNum=parseInt(h);
      Object.keys(catData[h]).forEach(w=>{
        const wNum=parseInt(w);
        const price=catData[h][w];
        sizes.push({label:`${wNum} × ${hNum}`,price,spec:`${wNum}×${hNum}`,w:wNum,h:hNum});
      });
    });
  }
  return sizes;
}

function mq_gradeChanged(){ mq_catChanged(); }

function mq_catChanged(){
  const grade=document.getElementById('mq_grade').value;
  const cat=document.getElementById('mq_cat').value;
  const sizeSel=document.getElementById('mq_size');
  const customRow=document.getElementById('mq_customRow');
  sizeSel.innerHTML='';

  if(cat==='직접입력'){
    customRow.style.display='flex';
    sizeSel.innerHTML='<option>직접입력</option>';
    return;
  }
  customRow.style.display='none';

  const sizes=mq_getSizes(grade, cat);
  sizes.forEach(s=>{
    const opt=document.createElement('option');
    opt.value=JSON.stringify(s);
    opt.textContent=`${s.label} — ${fmt(s.price)}원`;
    sizeSel.appendChild(opt);
  });
}

function mq_add(){
  const grade=document.getElementById('mq_grade').value;
  const gradeLabel=MK_PRICE[grade]?.label||grade;
  const cat=document.getElementById('mq_cat').value;
  const qty=parseInt(document.getElementById('mq_qty').value)||1;
  const note=document.getElementById('mq_note').value||'';

  let name, spec, cost;
  if(cat==='직접입력'){
    name=document.getElementById('mq_cName').value||'직접입력';
    const w=document.getElementById('mq_cW').value;
    const h=document.getElementById('mq_cH').value;
    cost=parseInt(document.getElementById('mq_cP').value)||0;
    spec=w&&h?`${w}×${h}`:'';
    if(!cost){alert('매입단가를 입력하세요');return;}
  } else {
    const sizeVal=document.getElementById('mq_size').value;
    if(!sizeVal||sizeVal==='품목 선택'){alert('규격을 선택하세요');return;}
    const s=JSON.parse(sizeVal);
    name=cat;
    spec=s.spec;
    cost=s.price;
  }

  MQ_ITEMS.push({name,spec,cost,qty,note,grade:gradeLabel,id:Date.now()});
  mq_recalc();
}

function mq_del(id){ MQ_ITEMS=MQ_ITEMS.filter(i=>i.id!==id); mq_recalc(); }
function mq_clear(){ if(MQ_ITEMS.length&&!confirm('전체 삭제?')) return; MQ_ITEMS=[]; mq_recalc(); }

function mq_recalc(){
  const marg=(parseInt(document.getElementById('mq_margin').value)||30)/100;
  const tbody=document.getElementById('mq_body');
  const tfoot=document.getElementById('mq_foot');
  tbody.innerHTML='';tfoot.innerHTML='';

  let totalCost=0, totalSell=0, totalQty=0;

  MQ_ITEMS.forEach(item=>{
    const sell=Math.round(item.cost/(1-marg));
    const costTotal=item.cost*item.qty;
    const sellTotal=sell*item.qty;
    totalCost+=costTotal; totalSell+=sellTotal; totalQty+=item.qty;

    const tr=document.createElement('tr');
    tr.innerHTML=`<td style="font-weight:500">${item.name}</td>
      <td class="tr" style="font-size:10px">${item.spec}</td>
      <td class="tr">${item.qty}</td>
      <td class="tr" style="color:#94A3B8">${fmt(item.cost)}</td>
      <td class="tr" style="color:#4ADE80;font-weight:600">${fmt(sell)}</td>
      <td class="tr" style="color:#94A3B8">${fmt(costTotal)}</td>
      <td class="tr" style="color:#4ADE80;font-weight:600">${fmt(sellTotal)}</td>
      <td style="font-size:9px;color:#64748B">${item.note}</td>
      <td style="text-align:center"><span onclick="mq_del(${item.id})" style="cursor:pointer;color:#F87171;font-size:12px">✕</span></td>`;
    tbody.appendChild(tr);
  });

  document.getElementById('mq_count').textContent=MQ_ITEMS.length+'건';
  const totalMargin=totalSell-totalCost;

  tfoot.innerHTML=MQ_ITEMS.length?`
    <tr style="background:#0F172A;font-weight:600">
      <td colspan="2">합계</td><td class="tr">${totalQty}</td>
      <td class="tr" style="color:#94A3B8">${fmt(totalCost)}</td><td></td>
      <td class="tr" style="color:#94A3B8">${fmt(totalCost)}</td>
      <td class="tr" style="color:#4ADE80;font-size:14px">${fmt(totalSell)}</td>
      <td colspan="2"></td>
    </tr>`:'';

  document.getElementById('mq_summary').innerHTML=MQ_ITEMS.length?`
    <div class="card" style="margin-top:0">
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center">
        <div>
          <div style="font-size:10px;color:#64748B">매입 합계</div>
          <div style="font-size:18px;font-weight:600;color:#E2E8F0">${fmt(totalCost)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">판매 합계</div>
          <div style="font-size:24px;font-weight:700;color:#4ADE80">${fmt(totalSell)}원</div>
          <div style="font-size:10px;color:#64748B">부가세별도</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">마진액</div>
          <div style="font-size:18px;font-weight:600;color:#FACC15">${fmt(totalMargin)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">마진율</div>
          <div style="font-size:18px;font-weight:600;color:#FACC15">${Math.round(marg*100)}%</div>
          <div style="font-size:10px;color:#64748B">VAT별도 ${fmt(Math.round(totalSell*1.1))}원</div>
        </div>
      </div>
    </div>`:'';
}

function mq_print(){
  if(!MQ_ITEMS.length){alert('견적 품목을 추가하세요');return;}
  const marg=(parseInt(document.getElementById('mq_margin').value)||30)/100;
  const site=document.getElementById('mq_site').value||'';
  const grade=MK_PRICE[document.getElementById('mq_grade').value]?.label||'';
  const today=new Date();
  const ds=today.getFullYear()+'.'+(today.getMonth()+1).toString().padStart(2,'0')+'.'+today.getDate().toString().padStart(2,'0');
  let totalSell=0;

  const rows=MQ_ITEMS.map((item,i)=>{
    const sell=Math.round(item.cost/(1-marg));
    const sellTotal=sell*item.qty;
    totalSell+=sellTotal;
    return `<tr><td class="r">${i+1}</td><td><b>${item.name}</b></td><td class="r">${item.spec}</td><td class="r">${item.qty}</td><td class="r">${fmt(sell)}</td><td class="r"><b>${fmt(sellTotal)}</b></td><td style="font-size:9px">${item.note}</td></tr>`;
  }).join('');

  const win=window.open('','_blank');
  win.document.write(`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>가견적서 - ${site||ds}</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Malgun Gothic',sans-serif;font-size:11px;color:#222;padding:30px;line-height:1.6}
h1{font-size:22px;text-align:center;margin-bottom:4px}
.sub{text-align:center;font-size:12px;color:#666;margin-bottom:20px}
.info{border:2px solid #333;padding:14px;margin-bottom:16px;display:grid;grid-template-columns:1fr 1fr;gap:6px}
.info b{color:#333}
table{width:100%;border-collapse:collapse;margin-bottom:16px}
th,td{border:1px solid #999;padding:5px 8px}
th{background:#2c3e50;color:#fff;font-weight:600;text-align:center;font-size:11px}
td.r{text-align:right}
.total-row{font-weight:700;background:#e8f5e9;font-size:13px}
.amount-box{border:3px solid #333;padding:16px;text-align:center;margin-bottom:16px;border-radius:4px}
.amount-box .big{font-size:32px;font-weight:700;color:#2c3e50}
.footer{text-align:center;margin-top:20px;font-size:9px;color:#999;border-top:1px solid #ddd;padding-top:8px}
.stamp{margin-top:30px;display:flex;justify-content:space-between}
.stamp div{width:200px;text-align:center;border-top:1px solid #333;padding-top:4px;font-size:10px}
@media print{body{padding:15px}.no-print{display:none}}
</style></head><body>
<div class="no-print" style="text-align:center;margin-bottom:16px">
  <button onclick="window.print()" style="padding:8px 30px;font-size:14px;background:#2c3e50;color:#fff;border:none;border-radius:4px;cursor:pointer">🖨️ 인쇄</button>
  <button onclick="window.close()" style="padding:8px 20px;font-size:14px;background:#999;color:#fff;border:none;border-radius:4px;cursor:pointer;margin-left:8px">닫기</button>
</div>
<h1>가 견 적 서</h1>
<div class="sub">에디피카 · ${ds}</div>
<div class="info">
  <div><b>현장명:</b> ${site||'-'}</div>
  <div><b>견적일:</b> ${ds}</div>
  <div><b>도어자재:</b> ${grade} (목산 도어공장)</div>
  <div><b>비고:</b> 부가세 별도</div>
</div>
<table>
  <thead><tr><th>No</th><th>품목</th><th>규격</th><th>수량</th><th>단가</th><th>금액</th><th>비고</th></tr></thead>
  <tbody>${rows}
    <tr class="total-row"><td colspan="5" style="text-align:center">합 계</td><td class="r">${fmt(totalSell)}원</td><td></td></tr>
  </tbody>
</table>
<div class="amount-box">
  <div style="font-size:12px;margin-bottom:4px">총 견적금액 (부가세별도)</div>
  <div class="big">${fmt(totalSell)}원</div>
  <div style="font-size:11px;color:#666;margin-top:4px">부가세포함: ${fmt(Math.round(totalSell*1.1))}원</div>
</div>
<div style="font-size:10px;color:#555;margin-bottom:20px">
  ※ 본 견적은 가견적이며, 실제 시공 시 현장 상황에 따라 변동될 수 있습니다.<br>
  ※ 견적 유효기간: 발행일로부터 30일
</div>
<div class="stamp"><div>공급자 (인)</div><div>수요자 (인)</div></div>
<div class="footer">에디피카 가견적서 · 목산 도어공장 ${grade} · ${ds}</div>
</body></html>`);
  win.document.close();
}

// init
document.addEventListener('DOMContentLoaded',function(){mq_catChanged();});

// ===== 무니끄 TAB =====
let MN_DOORS = [];

function mn_add(){
  const zone=document.getElementById('mn_zone').value||'';
  const w=parseInt(document.getElementById('mn_dw').value)||0;
  const h=parseInt(document.getElementById('mn_dh').value)||0;
  const qty=parseInt(document.getElementById('mn_dq').value)||1;
  if(!w||!h){alert('가로/세로를 입력하세요');return;}
  MN_DOORS.push({zone,w,h,qty,id:Date.now()+Math.random()});
  document.getElementById('mn_dw').value='';
  document.getElementById('mn_dh').value='';
  document.getElementById('mn_zone').focus();
  mn_recalc();
}

function mn_del(id){ MN_DOORS=MN_DOORS.filter(d=>d.id!==id); mn_recalc(); }
function mn_clear(){ if(MN_DOORS.length&&!confirm('전체 삭제?')) return; MN_DOORS=[]; mn_recalc(); }

function mn_recalc(){
  const sheetW=parseInt(document.getElementById('mn_sheetW').value)||1220;
  const sheetH=parseInt(document.getElementById('mn_sheetH').value)||2420;
  const sheetPrice=parseInt(document.getElementById('mn_sheetP').value)||450000;
  const bigFee=parseInt(document.getElementById('mn_bigFee').value)||200000;
  const smallFee=parseInt(document.getElementById('mn_smallFee').value)||100000;
  const threshold=parseInt(document.getElementById('mn_sizeThreshold').value)||1200;
  const margRate=(parseInt(document.getElementById('mn_margin').value)||30)/100;

  // 목록 렌더
  const tbody=document.getElementById('mn_body');
  tbody.innerHTML='';
  let totalQty=0, totalBig=0, totalSmall=0, totalProcessFee=0;

  MN_DOORS.forEach(d=>{
    totalQty+=d.qty;
    const isBig=d.h>=threshold;
    const fee=isBig?bigFee:smallFee;
    if(isBig) totalBig+=d.qty; else totalSmall+=d.qty;
    totalProcessFee+=fee*d.qty;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td style="font-weight:500">${d.zone}</td>
      <td class="tr">${d.w}</td><td class="tr">${d.h}</td>
      <td class="tr" style="color:#94A3B8">${fmt(d.w*d.h)}</td>
      <td class="tr">${d.qty}</td>
      <td class="tr"><span class="tag ${isBig?'tag-pink':'tag-cyan'}">${isBig?'큰도어':'작은도어'}</span></td>
      <td class="tr">${fmt(fee)}</td>
      <td style="text-align:center"><span onclick="mn_del(${d.id})" style="cursor:pointer;color:#F87171;font-size:12px">✕</span></td>`;
    tbody.appendChild(tr);
  });
  document.getElementById('mn_count').textContent=totalQty+'개';

  if(!totalQty){
    document.getElementById('mn_sheetCount').textContent='0장';
    document.getElementById('mn_layoutArea').innerHTML='<div style="text-align:center;color:#475569;padding:20px">도어를 추가하면 원장 배치를 계산합니다</div>';
    document.getElementById('mn_summary').innerHTML='';
    return;
  }

  // 개별 피스 전개
  const pieces=[];
  MN_DOORS.forEach(d=>{
    for(let i=0;i<d.qty;i++){
      pieces.push({name:d.zone+(d.qty>1?' #'+(i+1):''),w:d.w,h:d.h});
    }
  });

  // bin-pack (결방향 고정, 회전 없음)
  const KERF=5;
  const sorted=[...pieces].sort((a,b)=>(Math.max(b.w,b.h)-Math.max(a.w,a.h))||(b.w*b.h-a.w*a.h));
  const sheets=[];
  sorted.forEach(piece=>{
    let placed=false;
    for(let si=0;si<sheets.length;si++){
      const pw=piece.w, ph=piece.h;
      if(pw>sheetW||ph>sheetH) continue;
      const pos=mn_findPos(sheets[si],pw,ph,sheetW,sheetH,KERF);
      if(pos){ sheets[si].push({...piece,x:pos.x,y:pos.y,w:pw,h:ph}); placed=true; break; }
    }
    if(!placed){
      const newSheet=[];
      const pw=piece.w, ph=piece.h;
      if(pw<=sheetW&&ph<=sheetH){
        newSheet.push({...piece,x:0,y:0,w:pw,h:ph});
      } else {
        newSheet.push({...piece,x:0,y:0,w:pw,h:ph}); // oversized
      }
      sheets.push(newSheet);
    }
  });

  const nSheets=sheets.length;
  document.getElementById('mn_sheetCount').textContent=nSheets+'장';

  // 배치 시각화
  const layoutArea=document.getElementById('mn_layoutArea');
  layoutArea.innerHTML='';
  const sheetArea=sheetW*sheetH;
  const colors=['#E11D48','#F59E0B','#3B82F6','#10B981','#8B5CF6','#EC4899','#06B6D4','#84CC16','#F97316','#6366F1'];

  sheets.forEach((s,si)=>{
    const used=s.reduce((a,p)=>a+p.w*p.h,0);
    const pct=(used/sheetArea*100).toFixed(1);
    const scale=Math.min(400/sheetW, 260/sheetH);
    const sw=Math.round(sheetW*scale), sh=Math.round(sheetH*scale);

    let html=`<div style="display:inline-block;vertical-align:top;margin:0 14px 14px 0">`;
    html+=`<div style="font-size:11px;font-weight:600;color:#E2E8F0;margin-bottom:4px">${si+1}번 원장 <span style="color:#94A3B8;font-weight:400">${pct}%</span></div>`;
    html+=`<div class="sheet-box" style="width:${sw}px;height:${sh}px">`;
    html+=`<div class="cut-waste" style="left:0;top:0;width:${sw}px;height:${sh}px;z-index:0"></div>`;
    s.forEach((p,pi)=>{
      const x=Math.round(p.x*scale),y=Math.round(p.y*scale);
      const pw=Math.round(p.w*scale),ph=Math.round(p.h*scale);
      const c=colors[pi%colors.length];
      html+=`<div class="cut-part" style="left:${x}px;top:${y}px;width:${pw}px;height:${ph}px;background:${c}55;border-color:${c}" title="${p.name} ${p.w}×${p.h}">`;
      if(pw>25&&ph>10) html+=`<div class="part-info"><div style="font-size:${Math.min(10,pw/7)}px">${p.name}</div>`;
      if(pw>45&&ph>22) html+=`<div style="font-size:${Math.min(8,pw/9)}px;opacity:.7">${p.w}×${p.h}</div>`;
      if(pw>25&&ph>10) html+=`</div>`;
      html+=`</div>`;
    });
    html+=`</div>`;
    html+=`<div style="font-size:9px;color:#64748B;margin-top:2px">${s.map(p=>p.name).join(', ')}</div></div>`;
    layoutArea.innerHTML+=html;
  });

  // 요약
  const matCost=nSheets*sheetPrice;
  const totalCost=matCost+totalProcessFee;
  const sellPrice=Math.round(totalCost/(1-margRate));
  const margin=sellPrice-totalCost;

  document.getElementById('mn_summary').innerHTML=`
    <div class="card" style="margin-top:0">
      <div style="display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:14px">
        <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px">
          <div style="font-size:10px;color:#64748B;margin-bottom:8px">📦 원자재</div>
          <div style="display:flex;justify-content:space-between;margin-bottom:4px"><span>원장 ${nSheets}장 × ${fmt(sheetPrice)}원</span><span style="font-weight:600">${fmt(matCost)}원</span></div>
        </div>
        <div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px">
          <div style="font-size:10px;color:#64748B;margin-bottom:8px">🔧 가공비</div>
          ${totalBig?`<div style="display:flex;justify-content:space-between;margin-bottom:2px"><span>큰도어 ${totalBig}개 × ${fmt(bigFee)}</span><span>${fmt(totalBig*bigFee)}원</span></div>`:''}
          ${totalSmall?`<div style="display:flex;justify-content:space-between;margin-bottom:2px"><span>작은도어 ${totalSmall}개 × ${fmt(smallFee)}</span><span>${fmt(totalSmall*smallFee)}원</span></div>`:''}
          <div style="display:flex;justify-content:space-between;font-weight:600;border-top:1px solid #334155;padding-top:4px;margin-top:4px"><span>가공비 합계</span><span>${fmt(totalProcessFee)}원</span></div>
        </div>
      </div>
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center">
        <div>
          <div style="font-size:10px;color:#64748B">원가 합계</div>
          <div style="font-size:10px;color:#64748B">(원장+가공비)</div>
          <div style="font-size:20px;font-weight:700;color:#E2E8F0">${fmt(totalCost)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">판매가</div>
          <div style="font-size:10px;color:#64748B">(÷${(1-margRate).toFixed(1)})</div>
          <div style="font-size:24px;font-weight:700;color:#4ADE80">${fmt(sellPrice)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">마진</div>
          <div style="font-size:10px;color:#64748B">&nbsp;</div>
          <div style="font-size:18px;font-weight:600;color:#FACC15">${fmt(margin)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">도어 1개당 평균</div>
          <div style="font-size:10px;color:#64748B">&nbsp;</div>
          <div style="font-size:18px;font-weight:600;color:#A78BFA">${fmt(Math.round(sellPrice/totalQty))}원</div>
        </div>
      </div>
      <div class="note" style="margin-top:10px;font-size:10px">
        <b>도어:</b> ${totalQty}개 (큰도어 ${totalBig} + 작은도어 ${totalSmall}) · <b>원장:</b> ${nSheets}장 · <b>부가세별도:</b> ${fmt(Math.round(sellPrice*1.1))}원
      </div>
    </div>`;
}

function mn_findPos(placed,pw,ph,sW,sH,kerf){
  const candidates=[{x:0,y:0}];
  placed.forEach(p=>{
    candidates.push({x:p.x+p.w+kerf,y:p.y});
    candidates.push({x:p.x,y:p.y+p.h+kerf});
  });
  candidates.sort((a,b)=>a.y-b.y||a.x-b.x);
  for(const c of candidates){
    if(c.x+pw>sW||c.y+ph>sH) continue;
    let ok=true;
    for(const p of placed){
      if(c.x<p.x+p.w+kerf&&c.x+pw>p.x-kerf&&c.y<p.y+p.h+kerf&&c.y+ph>p.y-kerf){ok=false;break;}
    }
    if(ok) return c;
  }
  return null;
}

function mn_print(){
  if(!MN_DOORS.length){alert('도어를 추가하세요');return;}
  const sheetW=parseInt(document.getElementById('mn_sheetW').value)||1220;
  const sheetH=parseInt(document.getElementById('mn_sheetH').value)||2420;
  const sheetPrice=parseInt(document.getElementById('mn_sheetP').value)||450000;
  const bigFee=parseInt(document.getElementById('mn_bigFee').value)||200000;
  const smallFee=parseInt(document.getElementById('mn_smallFee').value)||100000;
  const threshold=parseInt(document.getElementById('mn_sizeThreshold').value)||1200;
  const margRate=(parseInt(document.getElementById('mn_margin').value)||30)/100;
  const site=document.getElementById('mn_site').value||'';
  const today=new Date();
  const ds=today.getFullYear()+'.'+(today.getMonth()+1).toString().padStart(2,'0')+'.'+today.getDate().toString().padStart(2,'0');

  let totalQty=0,totalBig=0,totalSmall=0,totalProcessFee=0;
  const rows=MN_DOORS.map((d,i)=>{
    totalQty+=d.qty;
    const isBig=d.h>=threshold;
    const fee=isBig?bigFee:smallFee;
    if(isBig) totalBig+=d.qty; else totalSmall+=d.qty;
    totalProcessFee+=fee*d.qty;
    return `<tr><td class="r">${i+1}</td><td>${d.zone}</td><td class="r">${d.w}</td><td class="r">${d.h}</td><td class="r">${d.qty}</td><td>${isBig?'큰도어':'작은도어'}</td><td class="r">${fmt(fee)}</td><td class="r">${fmt(fee*d.qty)}</td></tr>`;
  }).join('');

  // bin-pack count
  const pieces=[];
  MN_DOORS.forEach(d=>{for(let i=0;i<d.qty;i++) pieces.push({name:d.zone,w:d.w,h:d.h});});
  const sorted=[...pieces].sort((a,b)=>(Math.max(b.w,b.h)-Math.max(a.w,a.h)));
  const sheets=[];const KERF=5;
  sorted.forEach(piece=>{
    let placed=false;
    for(let si=0;si<sheets.length;si++){
      const pos=mn_findPos(sheets[si],piece.w,piece.h,sheetW,sheetH,KERF);
      if(pos){sheets[si].push({...piece,x:pos.x,y:pos.y});placed=true;break;}
    }
    if(!placed) sheets.push([{...piece,x:0,y:0}]);
  });
  const nSheets=sheets.length;
  const matCost=nSheets*sheetPrice;
  const totalCost=matCost+totalProcessFee;
  const sellPrice=Math.round(totalCost/(1-margRate));

  const win=window.open('','_blank');
  win.document.write(`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>무니끄 견적 - ${site||ds}</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Malgun Gothic',sans-serif;font-size:11px;color:#222;padding:30px;line-height:1.6}
h1{font-size:22px;text-align:center;margin-bottom:4px}
.sub{text-align:center;font-size:12px;color:#666;margin-bottom:20px}
.info{border:2px solid #333;padding:14px;margin-bottom:16px;display:grid;grid-template-columns:1fr 1fr;gap:6px}
table{width:100%;border-collapse:collapse;margin-bottom:16px}
th,td{border:1px solid #999;padding:4px 8px}
th{background:#2c3e50;color:#fff;font-weight:600;text-align:center;font-size:11px}
td.r{text-align:right}
.total-row{font-weight:700;background:#e8f5e9;font-size:12px}
.amount-box{border:3px solid #333;padding:16px;text-align:center;margin-bottom:16px;border-radius:4px}
.amount-box .big{font-size:32px;font-weight:700;color:#2c3e50}
.cost-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px}
.cost-box{border:1px solid #999;padding:12px;border-radius:4px}
.cost-box h4{font-size:12px;margin-bottom:8px;color:#333}
.footer{text-align:center;margin-top:20px;font-size:9px;color:#999;border-top:1px solid #ddd;padding-top:8px}
.stamp{margin-top:30px;display:flex;justify-content:space-between}
.stamp div{width:200px;text-align:center;border-top:1px solid #333;padding-top:4px;font-size:10px}
@media print{body{padding:15px}.no-print{display:none}}
</style></head><body>
<div class="no-print" style="text-align:center;margin-bottom:16px">
  <button onclick="window.print()" style="padding:8px 30px;font-size:14px;background:#2c3e50;color:#fff;border:none;border-radius:4px;cursor:pointer">🖨️ 인쇄</button>
  <button onclick="window.close()" style="padding:8px 20px;font-size:14px;background:#999;color:#fff;border:none;border-radius:4px;cursor:pointer;margin-left:8px">닫기</button>
</div>
<h1>🚪 무니끄 도어 가견적서</h1>
<div class="sub">에디피카 · ${ds}</div>
<div class="info">
  <div><b>현장명:</b> ${site||'-'}</div>
  <div><b>견적일:</b> ${ds}</div>
  <div><b>원장:</b> 무니끄 ${sheetW}×${sheetH}mm · ${fmt(sheetPrice)}원/장</div>
  <div><b>마진율:</b> ${Math.round(margRate*100)}% (판매가 기준)</div>
</div>
<table>
  <thead><tr><th>No</th><th>구역</th><th>가로</th><th>세로</th><th>수량</th><th>구분</th><th>가공단가</th><th>가공비</th></tr></thead>
  <tbody>${rows}
    <tr class="total-row"><td colspan="4">합계</td><td class="r">${totalQty}</td><td>큰${totalBig}/작${totalSmall}</td><td></td><td class="r">${fmt(totalProcessFee)}</td></tr>
  </tbody>
</table>
<div class="cost-grid">
  <div class="cost-box">
    <h4>📦 원자재비</h4>
    <div>원장 ${nSheets}장 × ${fmt(sheetPrice)}원 = <b>${fmt(matCost)}원</b></div>
  </div>
  <div class="cost-box">
    <h4>🔧 가공비</h4>
    ${totalBig?`<div>큰도어 ${totalBig}개 × ${fmt(bigFee)}원 = ${fmt(totalBig*bigFee)}원</div>`:''}
    ${totalSmall?`<div>작은도어 ${totalSmall}개 × ${fmt(smallFee)}원 = ${fmt(totalSmall*smallFee)}원</div>`:''}
    <div><b>합계: ${fmt(totalProcessFee)}원</b></div>
  </div>
</div>
<div class="amount-box">
  <div style="font-size:12px">원가 = 원장${fmt(matCost)} + 가공${fmt(totalProcessFee)} = <b>${fmt(totalCost)}</b></div>
  <div style="font-size:12px;margin:4px 0">판매가 = ${fmt(totalCost)} ÷ ${(1-margRate).toFixed(1)}</div>
  <div class="big">${fmt(sellPrice)}원</div>
  <div style="font-size:11px;color:#666;margin-top:4px">부가세포함: ${fmt(Math.round(sellPrice*1.1))}원 · 도어1개당 평균 ${fmt(Math.round(sellPrice/totalQty))}원</div>
</div>
<div style="font-size:10px;color:#555;margin-bottom:20px">
  ※ 본 견적은 가견적이며, 실제 시공 시 현장 상황에 따라 변동될 수 있습니다.<br>
  ※ 견적 유효기간: 발행일로부터 30일
</div>
<div class="stamp"><div>공급자 (인)</div><div>수요자 (인)</div></div>
<div class="footer">에디피카 · 무니끄 도어 가견적서 · ${ds}</div>
</body></html>`);
  win.document.close();
}

// ===== ORDER TAB =====
let ORD_PARTS = [];
let ORD_SHEET = {w:1220,h:2745,price:85800,label:'아르모니아 스탠다드 1220×2745'};

function ord_quickSelect(){
  const sel=document.getElementById('ord_sheet');
  const v=sel.value;
  if(!v) return; // "직접 입력 중"
  const p=v.split(',');
  document.getElementById('ord_sW').value=p[0];
  document.getElementById('ord_sH').value=p[1];
  document.getElementById('ord_sP').value=p[2];
  document.getElementById('ord_sheetName').value=p[3]||'';
  ord_updateInfo();
  ord_recalc();
}

function ord_updateInfo(){
  const w=parseInt(document.getElementById('ord_sW').value)||0;
  const h=parseInt(document.getElementById('ord_sH').value)||0;
  const price=parseInt(document.getElementById('ord_sP').value)||0;
  const name=document.getElementById('ord_sheetName').value.trim()||`${w}×${h}`;
  ORD_SHEET={w,h,price,label:name};
  document.getElementById('ord_sheetInfo').innerHTML=w&&h?
    `<b>원장:</b> ${name} — ${w}×${h}mm · <b>${fmt(price)}원</b>/장 · 면적 ${fmt(w*h)}mm²`:'원장 사이즈를 입력하세요';
  // 드롭다운을 "직접 입력 중"으로
  document.getElementById('ord_sheet').selectedIndex=0;
}

function ord_getSheet(){
  // 항상 input 필드에서 읽음
  const w=parseInt(document.getElementById('ord_sW').value)||1220;
  const h=parseInt(document.getElementById('ord_sH').value)||2745;
  const price=parseInt(document.getElementById('ord_sP').value)||0;
  const name=document.getElementById('ord_sheetName').value.trim()||`${w}×${h}`;
  ORD_SHEET={w,h,price,label:name};
  document.getElementById('ord_sheetInfo').innerHTML=
    `<b>원장:</b> ${name} — ${w}×${h}mm · <b>${fmt(price)}원</b>/장 · 면적 ${fmt(w*h)}mm²`;
}

function ord_applyCustom(){ord_updateInfo();ord_recalc();}

function ord_addOpen(){
  const W=parseInt(document.getElementById('ord_opW').value)||900;
  const H=parseInt(document.getElementById('ord_opH').value)||350;
  const D=parseInt(document.getElementById('ord_opD').value)||580;
  const T=parseInt(document.getElementById('ord_opT').value)||18;
  const qty=parseInt(document.getElementById('ord_opQty').value)||1;
  const memo=document.getElementById('ord_opMemo').value||'오픈장';
  const innerW=W-T*2;
  const tag=`${memo} ${W}×${H}×${D}`;

  for(let i=0;i<qty;i++){
    const suffix=qty>1?` #${i+1}`:'';
    ORD_PARTS.push({name:`천판${suffix}`,w:innerW,h:D,qty:1,memo:tag,id:Date.now()+Math.random()});
    ORD_PARTS.push({name:`지판${suffix}`,w:innerW,h:D,qty:1,memo:tag,id:Date.now()+Math.random()});
    ORD_PARTS.push({name:`좌측판${suffix}`,w:D,h:H,qty:1,memo:tag,id:Date.now()+Math.random()});
    ORD_PARTS.push({name:`우측판${suffix}`,w:D,h:H,qty:1,memo:tag,id:Date.now()+Math.random()});
    ORD_PARTS.push({name:`후면판${suffix}`,w:innerW,h:H-T*2,qty:1,memo:tag,id:Date.now()+Math.random()});
  }
  ord_recalc();
}

function ord_addCabinet(){
  const W=parseInt(document.getElementById('ord_cbW').value)||900;
  const H=parseInt(document.getElementById('ord_cbH').value)||2100;
  const D=parseInt(document.getElementById('ord_cbD').value)||580;
  const T=parseInt(document.getElementById('ord_cbT').value)||18;
  const nDoors=parseInt(document.getElementById('ord_cbDoors').value)||0;
  const nShelves=parseInt(document.getElementById('ord_cbShelves').value)||0;
  const nDrawers=parseInt(document.getElementById('ord_cbDrawers').value)||0;
  const drwH=parseInt(document.getElementById('ord_cbDrwH').value)||200;
  const toeH=parseInt(document.getElementById('ord_cbToeH').value)||100;
  const hasBack=document.getElementById('ord_cbBack').checked;
  const hasToe=document.getElementById('ord_cbToe').checked;
  const noFloor=document.getElementById('ord_cbNoFloor').checked;
  const qty=parseInt(document.getElementById('ord_cbQty').value)||1;
  const memo=document.getElementById('ord_cbMemo').value||'수납장';
  const gap=3;
  const innerW=W-T*2;
  const tag=`${memo} ${W}×${H}×${D}`;

  for(let i=0;i<qty;i++){
    const sf=qty>1?` #${i+1}`:'';
    // 측판
    ORD_PARTS.push({name:`좌측판${sf}`,w:D,h:H,qty:1,memo:tag,id:Date.now()+Math.random()});
    ORD_PARTS.push({name:`우측판${sf}`,w:D,h:H,qty:1,memo:tag,id:Date.now()+Math.random()});
    // 상판
    ORD_PARTS.push({name:`상판${sf}`,w:innerW,h:D,qty:1,memo:tag,id:Date.now()+Math.random()});
    // 하판
    if(!noFloor) ORD_PARTS.push({name:`하판${sf}`,w:innerW,h:D,qty:1,memo:tag,id:Date.now()+Math.random()});
    // 선반
    for(let s=0;s<nShelves;s++){
      ORD_PARTS.push({name:`선반${sf}${nShelves>1?' '+(s+1):''}`,w:innerW,h:D-20,qty:1,memo:tag,id:Date.now()+Math.random()});
    }
    // 도어
    if(nDoors>0){
      const doorW=Math.floor((W-gap*(nDoors-1))/nDoors);
      let doorH=H;
      if(hasToe) doorH-=(toeH+gap);
      if(nDrawers>0) doorH-=(drwH+gap)*nDrawers;
      for(let d=0;d<nDoors;d++){
        ORD_PARTS.push({name:`도어${sf}${nDoors>1?' '+(d+1):''}`,w:doorW,h:doorH,qty:1,memo:tag,id:Date.now()+Math.random()});
      }
    }
    // 서랍도어
    if(nDrawers>0){
      const drwW=nDoors>1?Math.floor(W/nDoors)-gap:W;
      for(let d=0;d<nDrawers;d++){
        ORD_PARTS.push({name:`서랍도어${sf}${nDrawers>1?' '+(d+1):''}`,w:drwW,h:drwH,qty:1,memo:tag,id:Date.now()+Math.random()});
      }
    }
    // 걸레받이
    if(hasToe) ORD_PARTS.push({name:`걸레받이${sf}`,w:innerW,h:toeH,qty:1,memo:tag,id:Date.now()+Math.random()});
    // 뒷판
    if(hasBack) ORD_PARTS.push({name:`뒷판${sf}`,w:innerW,h:H-T*2,qty:1,memo:tag,id:Date.now()+Math.random()});
  }
  ord_recalc();
}

function ord_save(){
  if(!ORD_PARTS.length){alert('저장할 부재가 없습니다');return;}
  const data={
    version:2,
    savedAt:new Date().toISOString(),
    sheet:{
      name:document.getElementById('ord_sheetName').value||'',
      w:parseInt(document.getElementById('ord_sW').value)||1220,
      h:parseInt(document.getElementById('ord_sH').value)||2745,
      price:parseInt(document.getElementById('ord_sP').value)||0
    },
    parts:ORD_PARTS.map(p=>({name:p.name,w:p.w,h:p.h,qty:p.qty,memo:p.memo}))
  };
  const json=JSON.stringify(data,null,2);
  const blob=new Blob([json],{type:'application/json'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');
  const today=new Date();
  const ds=today.getFullYear()+''+(today.getMonth()+1).toString().padStart(2,'0')+today.getDate().toString().padStart(2,'0');
  const fname=data.sheet.name?`합판주문_${data.sheet.name}_${ds}.json`:`합판주문_${ds}.json`;
  a.href=url; a.download=fname; a.click();
  URL.revokeObjectURL(url);
}

function ord_load(e){
  const file=e.target.files[0];
  if(!file) return;
  const reader=new FileReader();
  reader.onload=function(ev){
    try{
      const data=JSON.parse(ev.target.result);
      if(!data.parts||!data.parts.length){alert('유효한 데이터가 없습니다');return;}
      // 원장 설정 복원
      if(data.sheet){
        document.getElementById('ord_sheetName').value=data.sheet.name||'';
        document.getElementById('ord_sW').value=data.sheet.w||1220;
        document.getElementById('ord_sH').value=data.sheet.h||2745;
        document.getElementById('ord_sP').value=data.sheet.price||0;
      } else if(data.sheetName){
        // v1 호환
        document.getElementById('ord_sheetName').value=data.sheetName;
      }
      // 부재 복원
      ORD_PARTS=data.parts.map(p=>({...p,id:Date.now()+Math.random()}));
      ord_recalc();
      alert(`${data.parts.length}개 부재를 불러왔습니다.${data.savedAt?' (저장: '+data.savedAt.split('T')[0]+')':''}`);
    }catch(err){alert('파일을 읽을 수 없습니다: '+err.message);}
  };
  reader.readAsText(file);
  e.target.value=''; // reset for same file
}

function ord_addPreset(name,w,h){
  document.getElementById('ord_name').value=name;
  document.getElementById('ord_pw').value=w;
  document.getElementById('ord_ph').value=h;
  document.getElementById('ord_pq').value=1;
}

function ord_add(){
  const name=document.getElementById('ord_name').value||'부재';
  const w=parseInt(document.getElementById('ord_pw').value)||0;
  const h=parseInt(document.getElementById('ord_ph').value)||0;
  const qty=parseInt(document.getElementById('ord_pq').value)||1;
  const memo=document.getElementById('ord_memo').value||'';
  if(!w||!h){alert('가로/세로를 입력하세요');return;}
  if(w>ORD_SHEET.w&&w>ORD_SHEET.h || h>ORD_SHEET.w&&h>ORD_SHEET.h){
    if(!confirm(`부재(${w}×${h})가 원장(${ORD_SHEET.w}×${ORD_SHEET.h})보다 큽니다. 그래도 추가하시겠습니까?`)) return;
  }
  ORD_PARTS.push({name,w,h,qty,memo,id:Date.now()});
  document.getElementById('ord_pw').value='';
  document.getElementById('ord_ph').value='';
  document.getElementById('ord_name').focus();
  ord_recalc();
}

function ord_del(id){
  ORD_PARTS=ORD_PARTS.filter(p=>p.id!==id);
  ord_recalc();
}

function ord_clear(){
  if(ORD_PARTS.length&&!confirm('전체 삭제하시겠습니까?')) return;
  ORD_PARTS=[];
  ord_recalc();
}

function ord_recalc(){
  ord_getSheet();
  // 목록 렌더
  const tbody=document.getElementById('ord_listBody');
  tbody.innerHTML='';
  let totalQty=0, totalArea=0;
  ORD_PARTS.forEach(p=>{
    totalQty+=p.qty;
    totalArea+=p.w*p.h*p.qty;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td style="font-weight:500">${p.name}</td>
      <td class="tr">${p.w}</td><td class="tr">${p.h}</td>
      <td class="tr" style="color:#94A3B8">${fmt(p.w*p.h)}</td>
      <td class="tr">${p.qty}</td><td style="font-size:10px;color:#64748B">${p.memo}</td>
      <td style="text-align:center"><span onclick="ord_del(${p.id})" style="cursor:pointer;color:#F87171;font-size:12px">✕</span></td>`;
    tbody.appendChild(tr);
  });
  document.getElementById('ord_totalParts').textContent=totalQty+'개';
  document.getElementById('ord_totalArea').innerHTML=totalQty?
    `<b>전체:</b> ${totalQty}개 · 총면적 ${fmt(totalArea)}mm² (${(totalArea/1000000).toFixed(2)}m²)`:'';

  if(!totalQty){
    document.getElementById('ord_sheetCount').textContent='0장';
    document.getElementById('ord_resultArea').innerHTML='<div style="text-align:center;color:#475569;padding:30px">부재를 추가하면 원장 배치를 계산합니다</div>';
    document.getElementById('ord_summaryArea').innerHTML='';
    return;
  }

  // 개별 피스로 전개
  const pieces=[];
  ORD_PARTS.forEach(p=>{
    for(let i=0;i<p.qty;i++){
      pieces.push({name:p.name+(p.qty>1?` #${i+1}`:''),w:p.w,h:p.h,memo:p.memo});
    }
  });

  // bin-pack
  const sheets=ordPack(pieces, ORD_SHEET);
  const nSheets=sheets.length;
  document.getElementById('ord_sheetCount').textContent=nSheets+'장';

  // 배치 시각화
  const resArea=document.getElementById('ord_resultArea');
  resArea.innerHTML='';
  const sheetArea=ORD_SHEET.w*ORD_SHEET.h;
  const colors=['#E11D48','#F59E0B','#3B82F6','#10B981','#8B5CF6','#EC4899','#06B6D4','#84CC16','#F97316','#6366F1'];

  sheets.forEach((s,si)=>{
    const used=s.reduce((a,p)=>a+p.w*p.h,0);
    const pct=(used/sheetArea*100).toFixed(1);
    const waste=sheetArea-used;

    const maxRenderW=420;
    const scale=Math.min(maxRenderW/ORD_SHEET.w, 280/ORD_SHEET.h);
    const sw=Math.round(ORD_SHEET.w*scale), sh=Math.round(ORD_SHEET.h*scale);

    let html=`<div style="display:inline-block;vertical-align:top;margin:0 16px 16px 0">`;
    html+=`<div style="font-size:11px;font-weight:600;color:#E2E8F0;margin-bottom:4px">${si+1}번 원장 <span style="color:#94A3B8;font-weight:400">사용률 ${pct}%</span></div>`;
    html+=`<div class="sheet-box" style="width:${sw}px;height:${sh}px">`;

    s.forEach((p,pi)=>{
      const x=Math.round(p.x*scale),y=Math.round(p.y*scale);
      const pw=Math.round(p.w*scale),ph=Math.round(p.h*scale);
      const c=colors[pi%colors.length];
      html+=`<div class="cut-part" style="left:${x}px;top:${y}px;width:${pw}px;height:${ph}px;background:${c}55;border-color:${c}" title="${p.name} ${p.w}×${p.h}">`;
      if(pw>30&&ph>12){
        html+=`<div class="part-info"><div style="font-size:${Math.min(10,pw/7)}px">${p.name}</div>`;
        if(pw>50&&ph>24) html+=`<div style="font-size:${Math.min(8,pw/9)}px;opacity:.7">${p.w}×${p.h}</div>`;
        html+=`</div>`;
      }
      html+=`</div>`;
    });

    // waste area
    html+=`<div class="cut-waste" style="left:0;top:0;width:${sw}px;height:${sh}px;z-index:0"></div>`;
    html+=`</div>`;

    // 이 원장 부재 리스트
    html+=`<div style="font-size:9px;color:#64748B;margin-top:3px">`;
    s.forEach(p=>{ html+=`${p.name}(${p.w}×${p.h}) `; });
    html+=`<br>자투리: ${fmt(waste)}mm²</div></div>`;

    resArea.innerHTML+=html;
  });

  // 요약
  const totalCost=nSheets*ORD_SHEET.price;
  const totalSheetArea=nSheets*sheetArea;
  const utilPct=(totalArea/totalSheetArea*100).toFixed(1);
  document.getElementById('ord_summaryArea').innerHTML=`
    <div style="background:#0F172A;border:2px solid #334155;border-radius:8px;padding:16px;margin-top:8px">
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center">
        <div>
          <div style="font-size:10px;color:#64748B">필요 원장</div>
          <div style="font-size:28px;font-weight:700;color:#F59E0B">${nSheets}장</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">원장 단가</div>
          <div style="font-size:18px;font-weight:600;color:#E2E8F0">${fmt(ORD_SHEET.price)}원</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">총 자재비</div>
          <div style="font-size:22px;font-weight:700;color:#4ADE80">${fmt(totalCost)}원</div>
          <div style="font-size:10px;color:#64748B">부가세별도</div>
        </div>
        <div>
          <div style="font-size:10px;color:#64748B">사용률</div>
          <div style="font-size:18px;font-weight:600;color:${utilPct>80?'#4ADE80':utilPct>60?'#FACC15':'#F87171'}">${utilPct}%</div>
        </div>
      </div>
      <div class="note" style="margin-top:10px;font-size:10px">
        <b>${ORD_SHEET.label}</b> · 부재 ${totalQty}개 · 총면적 ${fmt(totalArea)}mm² → 원장 ${nSheets}장(${fmt(totalSheetArea)}mm²) · 자투리 ${fmt(totalSheetArea-totalArea)}mm² (${(100-parseFloat(utilPct)).toFixed(1)}%)
      </div>
    </div>`;
}

function ordPack(pieces, sheet){
  // Shelf-based First Fit Decreasing — 결 방향 고정 (회전 없음)
  const KERF=5;
  const sorted=[...pieces].sort((a,b)=>(Math.max(b.w,b.h)-Math.max(a.w,a.h))||(b.w*b.h-a.w*a.h));
  const sheets=[];

  sorted.forEach(piece=>{
    let placed=false;
    for(let si=0;si<sheets.length;si++){
      if(tryPlace(sheets[si],piece,sheet)) {placed=true;break;}
    }
    if(!placed){
      const newSheet=[];
      if(tryPlace(newSheet,piece,sheet)) sheets.push(newSheet);
      else sheets.push([{...piece,x:0,y:0}]); // force
    }
  });
  return sheets;
}

function tryPlace(sheetParts, piece, sheet){
  const KERF=5;
  // 결 방향 고정 — 입력한 가로×세로 그대로 배치 (회전 없음)
  const pw=piece.w, ph=piece.h;
  if(pw+KERF>sheet.w && pw>sheet.w) return false;
  if(ph+KERF>sheet.h && ph>sheet.h) return false;
  const pos=findPos(sheetParts,pw,ph,sheet,KERF);
  if(pos){
    sheetParts.push({...piece,x:pos.x,y:pos.y,w:pw,h:ph});
    return true;
  }
  return false;
}

function findPos(placed,pw,ph,sheet,kerf){
  // Try positions: top-left of sheet, after each placed piece
  const candidates=[{x:0,y:0}];
  placed.forEach(p=>{
    candidates.push({x:p.x+p.w+kerf, y:p.y});
    candidates.push({x:p.x, y:p.y+p.h+kerf});
  });
  candidates.sort((a,b)=>a.y-b.y||a.x-b.x);

  for(const c of candidates){
    if(c.x+pw>sheet.w||c.y+ph>sheet.h) continue;
    let overlap=false;
    for(const p of placed){
      if(c.x<p.x+p.w+kerf && c.x+pw>p.x-kerf && c.y<p.y+p.h+kerf && c.y+ph>p.y-kerf){
        overlap=true;break;
      }
    }
    if(!overlap) return c;
  }
  return null;
}

function ord_print(){
  if(!ORD_PARTS.length){alert('부재를 추가하세요');return;}
  const today=new Date();
  const dateStr=today.getFullYear()+'.'+(today.getMonth()+1).toString().padStart(2,'0')+'.'+today.getDate().toString().padStart(2,'0');
  const pieces=[];
  ORD_PARTS.forEach(p=>{for(let i=0;i<p.qty;i++) pieces.push({name:p.name+(p.qty>1?` #${i+1}`:''),w:p.w,h:p.h,memo:p.memo});});
  const sheets=ordPack(pieces,ORD_SHEET);
  const totalQty=ORD_PARTS.reduce((s,p)=>s+p.qty,0);
  const totalArea=ORD_PARTS.reduce((s,p)=>s+p.w*p.h*p.qty,0);
  const sheetArea=ORD_SHEET.w*ORD_SHEET.h;

  const win=window.open('','_blank');
  win.document.write(`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>합판주문서 - ${dateStr}</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Malgun Gothic',sans-serif;font-size:11px;color:#222;padding:20px;line-height:1.5}
h1{font-size:18px;text-align:center;margin-bottom:2px}
.sub{text-align:center;font-size:11px;color:#666;margin-bottom:14px}
table{width:100%;border-collapse:collapse;margin-bottom:12px;font-size:11px}
th,td{border:1px solid #999;padding:4px 8px}
th{background:#2c3e50;color:#fff;font-weight:600;text-align:center;font-size:10px}
td.r{text-align:right}
.total-row{font-weight:700;background:#e8f5e9}
.summary{border:2px solid #333;padding:14px;border-radius:4px;margin-bottom:14px;text-align:center}
.summary .big{font-size:28px;font-weight:700;color:#e67e22}
.footer{text-align:center;margin-top:16px;font-size:9px;color:#999;border-top:1px solid #ddd;padding-top:8px}
@media print{body{padding:10px}.no-print{display:none}}
</style></head><body>
<div class="no-print" style="text-align:center;margin-bottom:12px">
  <button onclick="window.print()" style="padding:8px 30px;font-size:14px;background:#2c3e50;color:#fff;border:none;border-radius:4px;cursor:pointer">🖨️ 인쇄</button>
  <button onclick="window.close()" style="padding:8px 20px;font-size:14px;background:#999;color:#fff;border:none;border-radius:4px;cursor:pointer;margin-left:8px">닫기</button>
</div>
<h1>📋 합판 주문서</h1>
<div class="sub">에디핏 · ${dateStr}</div>

<div class="summary">
  <div><b>원장:</b> ${ORD_SHEET.label} · ${fmt(ORD_SHEET.price)}원/장</div>
  <div style="margin:8px 0">주문 수량</div>
  <div class="big">${sheets.length}장</div>
  <div style="margin-top:6px"><b>총 금액: ${fmt(sheets.length*ORD_SHEET.price)}원</b> (부가세별도: ${fmt(Math.round(sheets.length*ORD_SHEET.price*1.1))}원)</div>
</div>

<table>
  <thead><tr><th>No.</th><th>부재명</th><th>가로(mm)</th><th>세로(mm)</th><th>면적(mm²)</th><th>수량</th><th>메모</th></tr></thead>
  <tbody>
    ${ORD_PARTS.map((p,i)=>`<tr><td class="r">${i+1}</td><td><b>${p.name}</b></td><td class="r">${p.w}</td><td class="r">${p.h}</td><td class="r">${fmt(p.w*p.h)}</td><td class="r">${p.qty}</td><td style="font-size:9px">${p.memo}</td></tr>`).join('')}
    <tr class="total-row"><td colspan="4">합계</td><td class="r">${fmt(totalArea)}</td><td class="r">${totalQty}</td><td></td></tr>
  </tbody>
</table>

<table>
  <thead><tr><th>원장#</th><th>배치 부재</th><th>사용면적</th><th>사용률</th><th>자투리</th></tr></thead>
  <tbody>
    ${sheets.map((s,i)=>{
      const u=s.reduce((a,p)=>a+p.w*p.h,0);
      return `<tr><td class="r">${i+1}</td><td style="font-size:9px">${s.map(p=>p.name+'('+p.w+'×'+p.h+')').join(', ')}</td><td class="r">${fmt(u)}</td><td class="r">${(u/sheetArea*100).toFixed(1)}%</td><td class="r">${fmt(sheetArea-u)}</td></tr>`;
    }).join('')}
    <tr class="total-row"><td colspan="2">합계: ${sheets.length}장</td><td class="r">${fmt(totalArea)}</td><td class="r">${(totalArea/(sheets.length*sheetArea)*100).toFixed(1)}%</td><td class="r">${fmt(sheets.length*sheetArea-totalArea)}</td></tr>
  </tbody>
</table>

<div class="footer">에디핏 합판주문서 · ${dateStr}</div>
</body></html>`);
  win.document.close();
}

// init order sheet info
document.addEventListener('DOMContentLoaded',function(){ord_getSheet();});

// ===== CUTTING GUIDE TAB =====
let CG_EXTRA_PARTS = [];
let CG_LIST = [];

function cg_structureChanged(){
  const v=document.getElementById('cg_structure').value;
  const desc=document.getElementById('cg_structureDesc');
  if(v==='gawa') desc.innerHTML='측판 = 전체높이 / 상하판 = 가로 - 좌T - 우T';
  else desc.innerHTML='상하판 = 전체가로 / 측판 = 높이 - 상판T - 하판T';
}

function cg_addPart(){
  const name=document.getElementById('cg_addName').value||'추가부재';
  const w=parseInt(document.getElementById('cg_addW').value)||0;
  const h=parseInt(document.getElementById('cg_addH').value)||0;
  const qty=parseInt(document.getElementById('cg_addQty').value)||1;
  if(!w||!h){alert('가로/세로를 입력하세요');return;}
  CG_EXTRA_PARTS.push({name,w,h,qty,edgeFront:1,edgeBack:0,edgeLeft:0,edgeRight:0});
  document.getElementById('cg_addName').value='';
  document.getElementById('cg_addW').value='';
  document.getElementById('cg_addH').value='';
  cg_run();
}

function cg_readInputs(){
  return {
    W:parseInt(document.getElementById('cg_w').value)||900,
    H:parseInt(document.getElementById('cg_h').value)||2100,
    D:parseInt(document.getElementById('cg_d').value)||580,
    leftT:parseInt(document.getElementById('cg_leftT').value)||18,
    rightT:parseInt(document.getElementById('cg_rightT').value)||18,
    structure:document.getElementById('cg_structure').value,
    gap:parseInt(document.getElementById('cg_gap').value)||3,
    nDoors:document.getElementById('cg_openMode').classList.contains('active')?0:(parseInt(document.getElementById('cg_doors').value)||0),
    nShelves:parseInt(document.getElementById('cg_shelves').value)||0,
    nDrawers:document.getElementById('cg_openMode').classList.contains('active')?0:(parseInt(document.getElementById('cg_drawers').value)||0),
    drawerH:parseInt(document.getElementById('cg_drawerH').value)||200,
    toeH:parseInt(document.getElementById('cg_toeH').value)||100,
    hasBack:document.getElementById('cg_back').classList.contains('active'),
    hasToe:document.getElementById('cg_toe').classList.contains('active'),
    noFloor:document.getElementById('cg_nofloor').classList.contains('active'),
    isOpen:document.getElementById('cg_openMode').classList.contains('active'),
    eSideFront:document.getElementById('cg_e_side_front').checked?1:0,
    eSideTop:document.getElementById('cg_e_side_top').checked?1:0,
    eSideBottom:document.getElementById('cg_e_side_bottom').checked?1:0,
    eTbFront:document.getElementById('cg_e_tb_front').checked?1:0,
    eTbLeft:document.getElementById('cg_e_tb_left').checked?1:0,
    eTbRight:document.getElementById('cg_e_tb_right').checked?1:0,
    eShelfFront:document.getElementById('cg_e_shelf_front').checked?1:0,
    eShelfLeft:document.getElementById('cg_e_shelf_left').checked?1:0,
    eShelfRight:document.getElementById('cg_e_shelf_right').checked?1:0,
    id:Date.now()+Math.random()
  };
}
function cg_addToList(){ CG_LIST.push(cg_readInputs()); cg_renderList(); }
function cg_delFromList(id){ CG_LIST=CG_LIST.filter(c=>c.id!==id); cg_renderList(); }
function cg_clearList(){ if(CG_LIST.length&&!confirm('전체 삭제?')) return; CG_LIST=[]; cg_renderList(); }
function cg_renderList(){
  const card=document.getElementById('cg_listCard');
  const tbody=document.getElementById('cg_listBody');
  tbody.innerHTML='';
  card.style.display=CG_LIST.length?'':'none';
  document.getElementById('cg_listCount').textContent=CG_LIST.length+'개';
  CG_LIST.forEach((c,i)=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${i+1}</td><td class="tr">${c.W}</td><td class="tr">${c.H}</td><td class="tr">${c.D}</td>
      <td class="tr">${c.nDoors}</td><td class="tr">${c.nShelves}</td>
      <td style="font-size:10px">${c.structure==='gawa'?'가와':'천지판'}</td>
      <td style="font-size:10px">${c.isOpen?'📦오픈':'🗄️수납'}</td>
      <td style="font-size:9px;color:#64748B">${[c.hasBack?'뒷판':'',c.hasToe?'걸레':'',c.noFloor?'바닥無':''].filter(Boolean).join(' ')}</td>
      <td style="text-align:center"><span onclick="cg_delFromList(${c.id})" style="cursor:pointer;color:#F87171;font-size:12px">✕</span></td>`;
    tbody.appendChild(tr);
  });
}
function cg_runAll(){
  if(!CG_LIST.length) CG_LIST.push(cg_readInputs());
  cg_renderList();
  cg_run();
}

function cg_findPos(placed,pw,ph,sW,sH,kerf){
  const candidates=[{x:0,y:0}];
  placed.forEach(p=>{
    candidates.push({x:p.x+p.w+kerf,y:p.y});
    candidates.push({x:p.x,y:p.y+p.h+kerf});
  });
  candidates.sort((a,b)=>a.y-b.y||a.x-b.x);
  for(const c of candidates){
    if(c.x+pw>sW||c.y+ph>sH) continue;
    let ok=true;
    for(const p of placed){
      if(c.x<p.x+p.w+kerf&&c.x+pw>p.x-kerf&&c.y<p.y+p.h+kerf&&c.y+ph>p.y-kerf){ok=false;break;}
    }
    if(ok) return c;
  }
  return null;
}

function cg_breakCabinet(c, prefix){
  const topT=18, bottomT=18;
  let sideW,sideH,tbW,tbD;
  if(c.structure==='gawa'){ sideH=c.H;sideW=c.D;tbW=c.W-c.leftT-c.rightT;tbD=c.D; }
  else { sideH=c.H-topT-bottomT;sideW=c.D;tbW=c.W;tbD=c.D; }
  const shelfW=c.W-c.leftT-c.rightT;
  const parts=[];
  parts.push({name:prefix+'좌측판',qty:1,designW:sideW,designH:sideH,t:c.leftT,
    eFront:c.eSideFront,eBack:0,eTop:c.eSideTop,eBottom:c.eSideBottom,
    note:c.leftT+'T'+(c.structure==='gawa'?' 가와':''),matType:c.isOpen?'door':'body'});
  parts.push({name:prefix+'우측판',qty:1,designW:sideW,designH:sideH,t:c.rightT,
    eFront:c.eSideFront,eBack:0,eTop:c.eSideTop,eBottom:c.eSideBottom,
    note:c.rightT+'T'+(c.structure==='gawa'?' 가와':''),matType:c.isOpen?'door':'body'});
  parts.push({name:prefix+'상판',qty:1,designW:tbW,designH:tbD,t:topT,
    eFront:c.eTbFront,eBack:0,eLeft:c.eTbLeft,eRight:c.eTbRight,
    note:c.structure==='chunji'?'천판덮음':'',matType:c.isOpen?'door':'body'});
  if(!c.noFloor) parts.push({name:prefix+'하판',qty:1,designW:tbW,designH:tbD,t:bottomT,
    eFront:c.eTbFront,eBack:0,eLeft:c.eTbLeft,eRight:c.eTbRight,
    note:c.structure==='chunji'?'지판덮음':'',matType:c.isOpen?'door':'body'});
  if(c.nShelves>0) parts.push({name:prefix+'선반',qty:c.nShelves,designW:shelfW,designH:c.D-20,t:18,
    eFront:c.eShelfFront,eBack:0,eLeft:c.eShelfLeft,eRight:c.eShelfRight,note:'깊이-20',matType:c.isOpen?'door':'body'});
  if(c.nDoors>0){
    const doorW=Math.floor((c.W-c.gap*(c.nDoors-1))/c.nDoors);
    let doorH=c.H; if(c.hasToe) doorH-=(c.toeH+c.gap); if(c.nDrawers>0) doorH-=(c.drawerH+c.gap)*c.nDrawers;
    parts.push({name:prefix+'도어',qty:c.nDoors,designW:doorW,designH:doorH,t:18,
      eFront:0,eBack:0,eLeft:0,eRight:0,note:'',matType:'door'});
  }
  if(c.nDrawers>0){
    const drwW=c.nDoors>1?Math.floor(c.W/c.nDoors)-c.gap:c.W;
    parts.push({name:prefix+'서랍도어',qty:c.nDrawers,designW:drwW,designH:c.drawerH,t:18,
      eFront:0,eBack:0,eLeft:0,eRight:0,note:'',matType:'door'});
  }
  if(c.hasToe) parts.push({name:prefix+'걸레받이',qty:1,designW:c.W-c.leftT-c.rightT,designH:c.toeH,t:18,
    eFront:c.eTbFront,eBack:0,eLeft:0,eRight:0,note:'',matType:c.isOpen?'door':'body'});
  if(c.hasBack){
    const backH=c.H-topT-bottomT;
    parts.push({name:prefix+'뒷판',qty:1,designW:c.W-c.leftT-c.rightT,designH:backH,t:0,
      eFront:0,eBack:0,eLeft:0,eRight:0,note:'',matType:c.isOpen?'door':'ura'});
  }
  return parts;
}

function cg_run(){
  const siteName=document.getElementById('cg_siteName').value;
  let parts=[];
  CG_LIST.forEach((c,ci)=>{
    const prefix=CG_LIST.length>1?`[${ci+1}]`:'';
    parts=parts.concat(cg_breakCabinet(c, prefix));
  });
  CG_EXTRA_PARTS.forEach(ep=>{
    parts.push({name:ep.name,qty:ep.qty,designW:ep.w,designH:ep.h,t:18,
      eFront:ep.edgeFront,eBack:ep.edgeBack||0,eLeft:ep.edgeLeft||0,eRight:ep.edgeRight||0,
      note:'추가',matType:'body'});
  });
  const c0=CG_LIST[0]||{};
  const W=c0.W||900,H=c0.H||2100,D=c0.D||580;
  const leftT=c0.leftT||18,rightT=c0.rightT||18;
  const structure=c0.structure||'gawa';
  const hasToe=c0.hasToe||false,toeH=c0.toeH||100,noFloor=c0.noFloor||false;
  const nShelves=c0.nShelves||0,nDoors=c0.nDoors||0,isOpen=c0.isOpen||false;
  const gap=c0.gap||3,nDrawers=c0.nDrawers||0,drawerH=c0.drawerH||200;
  const hasBack=c0.hasBack||false;
  const topT=18,bottomT=18;

  // 제단치수 계산 (설계치수 + 엣지보정)
  parts.forEach(p=>{
    const eW=(p.eLeft||0)+(p.eRight||0);   // 가로방향 엣지 수
    const eH=(p.eFront||0)+(p.eBack||0);  // 세로방향(깊이) 엣지 수
    // 측판: w=깊이, h=높이 → front/back은 깊이(w)방향 엣지, top/bottom은 높이(h)방향 엣지
    if(p.name.includes('측판')){
      p.cutW=p.designW+(p.eFront||0)+(p.eBack||0);
      p.cutH=p.designH+(p.eTop||0)+(p.eBottom||0);
      p.edgeDesc=[];
      if(p.eFront) p.edgeDesc.push('전면');
      if(p.eBack) p.edgeDesc.push('후면');
      if(p.eTop) p.edgeDesc.push('상단');
      if(p.eBottom) p.edgeDesc.push('하단');
    } else {
      p.cutW=p.designW+(p.eLeft||0)+(p.eRight||0);
      p.cutH=p.designH+(p.eFront||0)+(p.eBack||0);
      p.edgeDesc=[];
      if(p.eFront) p.edgeDesc.push('전면');
      if(p.eBack) p.edgeDesc.push('후면');
      if(p.eLeft) p.edgeDesc.push('좌');
      if(p.eRight) p.edgeDesc.push('우');
    }
    p.edgeCount=p.edgeDesc.length;
    p.edgeText=p.edgeDesc.length?p.edgeDesc.join('+'):'없음';
  });

  // 렌더
  document.getElementById('cg_resultArea').classList.remove('hidden');
  const tbody=document.getElementById('cg_partsBody');
  tbody.innerHTML='';
  let totalParts=0, totalEdgeLen=0;

  const matGroups=[
    {type:'body',label:'📦 몸통재',color:'#60A5FA',tagClass:'tag-blue'},
    {type:'door',label:'🎨 도어재',color:'#E879F9',tagClass:'tag-pink'},
    {type:'ura',label:'🪵 우라판',color:'#4ADE80',tagClass:'tag-green'},
  ];

  matGroups.forEach(g=>{
    const groupParts=parts.filter(p=>p.matType===g.type);
    if(!groupParts.length) return;
    let groupArea=0;
    // Section header
    const htr=document.createElement('tr');
    htr.style.background='#0F172A';
    htr.innerHTML=`<td colspan="6" style="font-weight:700;color:${g.color};font-size:11px;padding:6px 8px">${g.label}</td>`;
    tbody.appendChild(htr);

    groupParts.forEach(p=>{
      totalParts+=p.qty;
      const hasEdge=p.edgeCount>0;
      const cutChanged=p.cutW!==p.designW||p.cutH!==p.designH;
      let edgeLen=0;
      if(p.name.includes('측판')){
        if(p.eFront) edgeLen+=p.designH;if(p.eBack) edgeLen+=p.designH;
        if(p.eTop) edgeLen+=p.designW;if(p.eBottom) edgeLen+=p.designW;
      } else {
        if(p.eFront) edgeLen+=p.designW;if(p.eBack) edgeLen+=p.designW;
        if(p.eLeft) edgeLen+=p.designH;if(p.eRight) edgeLen+=p.designH;
      }
      totalEdgeLen+=edgeLen*p.qty;
      groupArea+=p.cutW*p.cutH*p.qty;

      const tr=document.createElement('tr');
      tr.innerHTML=`
        <td style="font-weight:600;padding-left:16px">${p.name}${p.t?' <span style="color:#64748B;font-size:9px">${p.t}T</span>':''}</td>
        <td class="tr">${p.designW} × ${p.designH}</td>
        <td class="tr" style="font-size:10px;color:${hasEdge?'#A78BFA':'#475569'}">${p.edgeText}${hasEdge?' <span style="color:#F59E0B">(+'+p.edgeCount+'mm)</span>':''}</td>
        <td class="tr" style="font-weight:700;color:${cutChanged?'#F59E0B':'#E2E8F0'}">${p.cutW} × ${p.cutH}</td>
        <td class="tr">${p.qty}</td>
        <td style="font-size:10px;color:#64748B">${p.note}</td>`;
      tbody.appendChild(tr);
    });
    // Group subtotal
    const str=document.createElement('tr');
    str.style.borderBottom='2px solid #334155';
    str.innerHTML=`<td colspan="4" style="text-align:right;font-size:10px;color:${g.color};padding-right:8px">${g.label} 면적합: ${fmt(groupArea)}mm²</td><td class="tr" style="color:${g.color};font-weight:600">${groupParts.reduce((s,p)=>s+p.qty,0)}개</td><td></td>`;
    tbody.appendChild(str);
  });

  document.getElementById('cg_partCount').textContent=totalParts+'개';
  document.getElementById('cg_edgeSummary').innerHTML=`
    <div class="note">
      <b>엣지 소요:</b> 총 ${(totalEdgeLen/1000).toFixed(1)}m (${fmt(totalEdgeLen)}mm)
      ${parts.some(p=>p.cutW!==p.designW||p.cutH!==p.designH)?'<br><span style="color:#F59E0B">⚠️ 엣지보정으로 제단치수가 설계치수와 다른 부재가 있습니다</span>':''}
    </div>`;

  // 구조도 SVG
  renderStructureDiagram(W,H,D,leftT,rightT,topT,bottomT,structure,hasToe,toeH,noFloor,nShelves,nDoors);

  // 원장 배치도 (소재별)
  const layoutArea=document.getElementById('cg_layoutArea');
  layoutArea.innerHTML='';
  const KERF=5;
  const matSheets={
    body:{label:'📦 몸통재',color:'#60A5FA',shW:1220,shH:2440},
    door:{label:'🎨 도어재',color:'#E879F9',shW:1220,shH:2745},
    ura:{label:'🪵 우라판',color:'#4ADE80',shW:1220,shH:2440}
  };
  const layoutColors=['#E11D48','#F59E0B','#3B82F6','#10B981','#8B5CF6','#EC4899','#06B6D4','#84CC16','#F97316','#6366F1'];

  ['body','door','ura'].forEach(mType=>{
    const mParts=parts.filter(p=>p.matType===mType);
    if(!mParts.length) return;
    const ms=matSheets[mType];

    // 개별 피스 전개 (제단치수 기준)
    const pieces=[];
    mParts.forEach(p=>{
      for(let i=0;i<p.qty;i++) pieces.push({name:p.name+(p.qty>1?' #'+(i+1):''),w:p.cutW,h:p.cutH});
    });
    const sorted=[...pieces].sort((a,b)=>(Math.max(b.w,b.h)-Math.max(a.w,a.h)));

    // bin-pack (결방향 고정)
    const sheets=[];
    sorted.forEach(piece=>{
      let placed=false;
      for(let si=0;si<sheets.length;si++){
        const pos=cg_findPos(sheets[si],piece.w,piece.h,ms.shW,ms.shH,KERF);
        if(pos){sheets[si].push({...piece,x:pos.x,y:pos.y});placed=true;break;}
      }
      if(!placed) sheets.push([{...piece,x:0,y:0}]);
    });

    const totalArea=pieces.reduce((s,p)=>s+p.w*p.h,0);
    const sheetArea=ms.shW*ms.shH;

    let html=`<div style="margin-bottom:16px">
      <div style="font-size:13px;font-weight:700;color:${ms.color};margin-bottom:6px">${ms.label} — ${sheets.length}장 필요 <span style="font-size:10px;color:#94A3B8;font-weight:400">(${ms.shW}×${ms.shH} · 총사용 ${(totalArea/sheetArea*100).toFixed(0)}%)</span></div>`;

    sheets.forEach((s,si)=>{
      const used=s.reduce((a,p)=>a+p.w*p.h,0);
      const pct=(used/sheetArea*100).toFixed(1);
      const scale=Math.min(280/ms.shW, 200/ms.shH);
      const sw=Math.round(ms.shW*scale), sh=Math.round(ms.shH*scale);

      html+=`<div style="display:inline-block;vertical-align:top;margin:0 12px 12px 0">`;
      html+=`<div style="font-size:10px;color:#E2E8F0;margin-bottom:3px">${si+1}번 <span style="color:#94A3B8">${pct}%</span></div>`;
      html+=`<div class="sheet-box" style="width:${sw}px;height:${sh}px">`;
      html+=`<div class="cut-waste" style="left:0;top:0;width:${sw}px;height:${sh}px;z-index:0"></div>`;
      s.forEach((p,pi)=>{
        const x=Math.round(p.x*scale),y=Math.round(p.y*scale);
        const pw=Math.round(p.w*scale),ph=Math.round(p.h*scale);
        const c=layoutColors[pi%layoutColors.length];
        html+=`<div class="cut-part" style="left:${x}px;top:${y}px;width:${pw}px;height:${ph}px;background:${c}55;border-color:${c}" title="${p.name} ${p.w}×${p.h}">`;
        if(pw>20&&ph>8) html+=`<div class="part-info"><div style="font-size:${Math.min(9,pw/8)}px">${p.name}</div>`;
        if(pw>40&&ph>18) html+=`<div style="font-size:${Math.min(7,pw/10)}px;opacity:.7">${p.w}×${p.h}</div>`;
        if(pw>20&&ph>8) html+=`</div>`;
        html+=`</div>`;
      });
      html+=`</div>`;
      html+=`<div style="font-size:8px;color:#64748B;margin-top:2px;max-width:${sw}px;overflow:hidden;white-space:nowrap;text-overflow:ellipsis">${s.map(p=>p.name).join(', ')}</div></div>`;
    });

    html+=`</div>`;
    layoutArea.innerHTML+=html;
  });

  // 데이터 저장
  window._cgData={parts,W,H,D,leftT,rightT,structure,gap,nDoors,nShelves,nDrawers,drawerH,toeH,hasBack,hasToe,noFloor,isOpen,totalEdgeLen,siteName:document.getElementById('cg_siteName').value,cabList:CG_LIST};
}

function renderStructureDiagram(W,H,D,lT,rT,tT,bT,struct,hasToe,toeH,noFloor,nShelves,nDoors){
  const el=document.getElementById('cg_structureDiagram');
  const maxW=500,maxH=320;
  const s=Math.min(maxW/W,maxH/H);
  const sw=Math.round(W*s),sh=Math.round(H*s);
  const lt=Math.max(4,Math.round(lT*s)),rt=Math.max(4,Math.round(rT*s));
  const tt=Math.max(4,Math.round(tT*s)),bt=Math.max(4,Math.round(bT*s));

  let svg=`<svg width="${sw+60}" height="${sh+40}" style="display:inline-block">`;
  svg+=`<g transform="translate(30,20)">`;

  // 외곽선
  svg+=`<rect x="0" y="0" width="${sw}" height="${sh}" fill="none" stroke="#475569" stroke-width="1" stroke-dasharray="4"/>`;

  if(struct==='gawa'){
    // 좌측판 전체높이
    svg+=`<rect x="0" y="0" width="${lt}" height="${sh}" fill="#3B82F6" fill-opacity="0.3" stroke="#3B82F6" stroke-width="1.5"/>`;
    svg+=`<text x="${lt/2}" y="${sh/2}" text-anchor="middle" font-size="9" fill="#93C5FD" transform="rotate(-90,${lt/2},${sh/2})">좌 ${lT}T</text>`;
    // 우측판 전체높이
    svg+=`<rect x="${sw-rt}" y="0" width="${rt}" height="${sh}" fill="#3B82F6" fill-opacity="0.3" stroke="#3B82F6" stroke-width="1.5"/>`;
    svg+=`<text x="${sw-rt/2}" y="${sh/2}" text-anchor="middle" font-size="9" fill="#93C5FD" transform="rotate(90,${sw-rt/2},${sh/2})">우 ${rT}T</text>`;
    // 상판
    svg+=`<rect x="${lt}" y="0" width="${sw-lt-rt}" height="${tt}" fill="#22D3EE" fill-opacity="0.3" stroke="#22D3EE" stroke-width="1"/>`;
    svg+=`<text x="${(sw)/2}" y="${tt/2+3}" text-anchor="middle" font-size="8" fill="#67E8F9">상판</text>`;
    // 하판
    if(!noFloor){
      svg+=`<rect x="${lt}" y="${sh-bt}" width="${sw-lt-rt}" height="${bt}" fill="#22D3EE" fill-opacity="0.3" stroke="#22D3EE" stroke-width="1"/>`;
      svg+=`<text x="${(sw)/2}" y="${sh-bt/2+3}" text-anchor="middle" font-size="8" fill="#67E8F9">하판</text>`;
    }
  } else {
    // 상판 전체가로
    svg+=`<rect x="0" y="0" width="${sw}" height="${tt}" fill="#22D3EE" fill-opacity="0.3" stroke="#22D3EE" stroke-width="1.5"/>`;
    svg+=`<text x="${sw/2}" y="${tt/2+3}" text-anchor="middle" font-size="9" fill="#67E8F9">상판 (천판덮음)</text>`;
    // 하판 전체가로
    if(!noFloor){
      svg+=`<rect x="0" y="${sh-bt}" width="${sw}" height="${bt}" fill="#22D3EE" fill-opacity="0.3" stroke="#22D3EE" stroke-width="1.5"/>`;
      svg+=`<text x="${sw/2}" y="${sh-bt/2+3}" text-anchor="middle" font-size="9" fill="#67E8F9">하판 (지판덮음)</text>`;
    }
    // 좌측판
    svg+=`<rect x="0" y="${tt}" width="${lt}" height="${sh-tt-bt}" fill="#3B82F6" fill-opacity="0.3" stroke="#3B82F6" stroke-width="1"/>`;
    svg+=`<text x="${lt/2}" y="${(sh)/2}" text-anchor="middle" font-size="8" fill="#93C5FD" transform="rotate(-90,${lt/2},${(sh)/2})">좌 ${lT}T</text>`;
    // 우측판
    svg+=`<rect x="${sw-rt}" y="${tt}" width="${rt}" height="${sh-tt-bt}" fill="#3B82F6" fill-opacity="0.3" stroke="#3B82F6" stroke-width="1"/>`;
    svg+=`<text x="${sw-rt/2}" y="${(sh)/2}" text-anchor="middle" font-size="8" fill="#93C5FD" transform="rotate(90,${sw-rt/2},${(sh)/2})">우 ${rT}T</text>`;
  }

  // 선반
  const innerY=struct==='gawa'?tt:tt;
  const innerH=struct==='gawa'?sh-tt-(noFloor?0:bt):sh-tt-(noFloor?0:bt);
  if(nShelves>0){
    for(let i=1;i<=nShelves;i++){
      const sy=innerY+Math.round(innerH*i/(nShelves+1));
      svg+=`<line x1="${lt+4}" y1="${sy}" x2="${sw-rt-4}" y2="${sy}" stroke="#4ADE80" stroke-width="2" stroke-dasharray="6,3"/>`;
      svg+=`<text x="${sw/2}" y="${sy-4}" text-anchor="middle" font-size="7" fill="#6EE7B7">선반${i}</text>`;
    }
  }

  // 치수선
  svg+=`<text x="${sw/2}" y="${sh+14}" text-anchor="middle" font-size="10" fill="#94A3B8">${W}mm</text>`;
  svg+=`<text x="${sw+14}" y="${sh/2}" text-anchor="middle" font-size="10" fill="#94A3B8" transform="rotate(90,${sw+14},${sh/2})">${H}mm</text>`;
  svg+=`</g></svg>`;
  el.innerHTML=svg;
}

function cg_print(){
  const d=window._cgData;
  if(!d){alert('먼저 재단가이드를 생성하세요.');return;}

  const today=new Date();
  const dateStr=today.getFullYear()+'.'+(today.getMonth()+1).toString().padStart(2,'0')+'.'+today.getDate().toString().padStart(2,'0');
  const structLabel=d.structure==='gawa'?'가와덮음 (측판이 상하판을 덮음)':'천지판덮음 (상하판이 측판을 덮음)';

  const win=window.open('','_blank');
  win.document.write(`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>재단가이드 - ${d.siteName||dateStr}</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Malgun Gothic',sans-serif;font-size:11px;color:#222;padding:20px;line-height:1.5}
h1{font-size:18px;text-align:center;margin-bottom:2px}
.sub{text-align:center;font-size:11px;color:#666;margin-bottom:14px}
.info-grid{display:grid;grid-template-columns:1fr 1fr;gap:6px 16px;margin-bottom:16px;border:2px solid #333;padding:12px;border-radius:4px}
.info-grid b{color:#333}
table{width:100%;border-collapse:collapse;margin-bottom:12px;font-size:11px}
th,td{border:1px solid #999;padding:4px 8px}
th{background:#2c3e50;color:#fff;font-weight:600;text-align:center;font-size:10px}
td.r{text-align:right;font-variant-numeric:tabular-nums}
.highlight{background:#fffde7;font-weight:700}
.total-row{font-weight:700;background:#e8f5e9}
.edge-mark{color:#9c27b0;font-weight:600}
.note-box{border:1px dashed #999;padding:8px 12px;margin-bottom:14px;font-size:10px;color:#555;border-radius:4px}
.section-title{font-size:13px;font-weight:700;background:#333;color:#fff;padding:5px 12px;margin:14px 0 8px;border-radius:3px}
.footer{text-align:center;margin-top:16px;font-size:9px;color:#999;border-top:1px solid #ddd;padding-top:8px}
@media print{body{padding:10px}.no-print{display:none}}
</style></head><body>
<div class="no-print" style="text-align:center;margin-bottom:12px">
  <button onclick="window.print()" style="padding:8px 30px;font-size:14px;background:#2c3e50;color:#fff;border:none;border-radius:4px;cursor:pointer">🖨️ 인쇄하기</button>
  <button onclick="window.close()" style="padding:8px 20px;font-size:14px;background:#999;color:#fff;border:none;border-radius:4px;cursor:pointer;margin-left:8px">닫기</button>
</div>

<h1>✂️ 합판 재단가이드</h1>
<div class="sub">${d.siteName?d.siteName+' · ':''}에디핏 · ${dateStr}${d.isOpen?' · <b style="color:#e67e22">📦 오픈장</b>':''}</div>

<div class="info-grid">
  <div><b>외형 치수:</b> ${d.W} × ${d.H} × ${d.D} mm</div>
  <div><b>조립구조:</b> ${structLabel}</div>
  <div><b>좌측판:</b> ${d.leftT}T / <b>우측판:</b> ${d.rightT}T</div>
  <div><b>도어:</b> ${d.nDoors}개 · <b>선반:</b> ${d.nShelves}개 · <b>서랍:</b> ${d.nDrawers}개</div>
  <div><b>옵션:</b> ${d.hasBack?'뒷판 ':''}${d.hasToe?'걸레받이('+d.toeH+'mm) ':''}${d.noFloor?'바닥없음 ':''}${d.isOpen?'오픈장':''}</div>
  <div><b>갭:</b> ${d.gap}mm · <b>엣지보정:</b> 면당 +1mm</div>
</div>

<div class="note-box">
  ⚠️ <b>제단치수 = 설계치수 + 엣지보정</b> (엣지테이프 부착 시 면당 1mm 증가 반영)<br>
  공장에서는 <b>제단치수</b> 기준으로 재단해 주세요. 엣지 부착 후 설계치수가 됩니다.
</div>

<div class="section-title">📋 재단 목록 (총 ${d.parts.reduce((s,p)=>s+p.qty,0)}개)</div>
<table>
  <thead><tr>
    <th>No.</th><th>부재명</th><th>소재</th><th>두께</th><th>설계치수(mm)</th><th>엣지면</th>
    <th style="background:#e67e22">✂️ 제단 가로</th><th style="background:#e67e22">✂️ 제단 세로</th>
    <th>수량</th><th>비고</th>
  </tr></thead>
  <tbody>
    ${[{type:'body',label:'📦 몸통재',bg:'#e3f2fd'},{type:'door',label:'🎨 도어재',bg:'#fce4ec'},{type:'ura',label:'🪵 우라판',bg:'#e8f5e9'}].map(g=>{
      const gp=d.parts.filter(p=>p.matType===g.type);
      if(!gp.length) return '';
      let rows=`<tr style="background:${g.bg}"><td colspan="10" style="font-weight:700;font-size:12px;padding:6px 8px">${g.label} (${gp.reduce((s,p)=>s+p.qty,0)}개)</td></tr>`;
      gp.forEach((p,i)=>{
        const changed=p.cutW!==p.designW||p.cutH!==p.designH;
        rows+=`<tr${changed?' class="highlight"':''}>
          <td class="r">${i+1}</td>
          <td><b>${p.name}</b></td>
          <td style="font-size:9px">${g.label.split(' ')[1]}</td>
          <td class="r">${p.t?p.t+'T':'-'}</td>
          <td class="r">${p.designW} × ${p.designH}</td>
          <td class="${p.edgeCount?'edge-mark':''}">${p.edgeText}</td>
          <td class="r" style="font-weight:700;font-size:13px">${p.cutW}</td>
          <td class="r" style="font-weight:700;font-size:13px">${p.cutH}</td>
          <td class="r">${p.qty}</td>
          <td style="font-size:9px;color:#666">${p.note}</td>
        </tr>`;
      });
      const area=gp.reduce((s,p)=>s+p.cutW*p.cutH*p.qty,0);
      rows+=`<tr style="background:#f5f5f5"><td colspan="8" style="text-align:right;font-size:10px;color:#666">${g.label} 면적합: ${fmt(area)}mm²</td><td class="r" style="font-weight:600">${gp.reduce((s,p)=>s+p.qty,0)}</td><td></td></tr>`;
      return rows;
    }).join('')}
  </tbody>
</table>

<div class="section-title">📐 엣지 소요량</div>
<table>
  <thead><tr><th>부재명</th><th>엣지면</th><th>둘레/개(mm)</th><th>수량</th><th>소계(mm)</th></tr></thead>
  <tbody>
    ${d.parts.filter(p=>p.edgeCount>0).map(p=>{
      let len=0;
      if(p.name.includes('측판')){
        if(p.eFront) len+=p.designH;if(p.eBack) len+=p.designH;
        if(p.eTop) len+=p.designW;if(p.eBottom) len+=p.designW;
      } else {
        if(p.eFront) len+=p.designW;if(p.eBack) len+=p.designW;
        if(p.eLeft) len+=p.designH;if(p.eRight) len+=p.designH;
      }
      return `<tr><td>${p.name}</td><td class="edge-mark">${p.edgeText}</td><td class="r">${fmt(len)}</td><td class="r">${p.qty}</td><td class="r">${fmt(len*p.qty)}</td></tr>`;
    }).join('')}
    <tr class="total-row"><td colspan="4">합계</td><td class="r">${fmt(d.totalEdgeLen)}mm = ${(d.totalEdgeLen/1000).toFixed(1)}m</td></tr>
  </tbody>
</table>

<div class="section-title">🏗️ 조립 참고</div>
<div class="note-box" style="font-size:11px">
  ${d.structure==='gawa'?
    `<b>가와덮음:</b> 좌·우측판(${d.leftT}T/${d.rightT}T)이 전체높이(${d.H}mm)로 서고, 상·하판이 사이에 끼워집니다.<br>
     내부폭 = ${d.W} - ${d.leftT} - ${d.rightT} = <b>${d.W-d.leftT-d.rightT}mm</b>`:
    `<b>천지판덮음:</b> 상·하판이 전체가로(${d.W}mm)로 깔리고, 좌·우측판이 사이에 끼워집니다.<br>
     측판높이 = ${d.H} - 18 - 18 = <b>${d.H-36}mm</b> / 내부폭 = ${d.W} - ${d.leftT} - ${d.rightT} = <b>${d.W-d.leftT-d.rightT}mm</b>`}
</div>

<div class="footer">에디핏 합판 재단가이드 · ${dateStr}</div>
</body></html>`);
  win.document.close();
}

// ===== PRINT CUTTING GUIDE (from 장짜기 tab) =====
function printCutGuide(){
  const d=CUT_GUIDE_DATA;
  if(!d){alert('먼저 비교 계산을 실행해주세요.');return;}

  // Separate parts
  const doorParts=[],bodyParts=[],uraParts=[];
  d.parts.forEach(p=>{
    for(let i=0;i<p.qty;i++){
      const piece={name:p.name+(p.qty>1?` #${i+1}`:''),cat:p.cat,w:p.w,h:p.h,matType:p.matType};
      if(p.matType==='door') doorParts.push(piece);
      else if(p.matType==='ura') uraParts.push(piece);
      else bodyParts.push(piece);
    }
  });

  const doorSheet={w:d.doorMat.w,h:d.doorMat.h,price:d.doorMat.price,label:d.doorMat.label};
  const bodySheet={w:d.bodyMat.w,h:d.bodyMat.h,price:d.bodyMat.price,label:d.bodyMat.label};
  const uraSheet={w:d.uraSheetW||1220,h:d.uraSheetH||2440,price:d.uraPrice,label:`우라판 ${d.uraSheetW||1220}×${d.uraSheetH||2440}`};

  const doorSheets=doorParts.length>0?packParts(doorParts,doorSheet):[];
  const bodySheets=bodyParts.length>0?packParts(bodyParts,bodySheet):[];
  const uraSheets=uraParts.length>0?packParts(uraParts,uraSheet):[];

  const today=new Date();
  const dateStr=today.getFullYear()+'.'+(today.getMonth()+1).toString().padStart(2,'0')+'.'+today.getDate().toString().padStart(2,'0');

  // Build edge list
  let edgeList=[];
  d.parts.forEach(p=>{
    if(p.cat==='우라') return;
    const perimeter=d.edge4?((p.w+p.h)*2):((p.w+p.h)*2*0.6);
    edgeList.push({name:p.name,qty:p.qty,perimeter:Math.round(perimeter),total:Math.round(perimeter*p.qty)});
  });
  const totalEdge=edgeList.reduce((s,e)=>s+e.total,0);

  function sheetSVG(pieces,sheet,colors,maxW){
    const scale=Math.min(maxW/sheet.w, 280/sheet.h);
    const sw=Math.round(sheet.w*scale), sh=Math.round(sheet.h*scale);
    let svg=`<svg width="${sw+2}" height="${sh+2}" style="border:2px solid #333"><rect width="${sw}" height="${sh}" fill="#f5f5f0" stroke="#999"/>`;
    // Grid lines
    for(let x=0;x<=sheet.w;x+=200){
      const px=Math.round(x*scale);
      svg+=`<line x1="${px}" y1="0" x2="${px}" y2="${sh}" stroke="#ddd" stroke-width="0.5"/>`;
    }
    for(let y=0;y<=sheet.h;y+=200){
      const py=Math.round(y*scale);
      svg+=`<line x1="0" y1="${py}" x2="${sw}" y2="${py}" stroke="#ddd" stroke-width="0.5"/>`;
    }
    pieces.forEach((p,i)=>{
      const x=Math.round(p.x*scale),y=Math.round(p.y*scale);
      const pw=Math.round(p.w*scale),ph=Math.round(p.h*scale);
      const c=colors[i%colors.length];
      svg+=`<rect x="${x}" y="${y}" width="${pw}" height="${ph}" fill="${c}" fill-opacity="0.3" stroke="${c}" stroke-width="1.5"/>`;
      if(pw>35&&ph>14){
        const fs=Math.min(11,Math.max(7,Math.min(pw/8,ph/2)));
        svg+=`<text x="${x+pw/2}" y="${y+ph/2-fs*0.3}" text-anchor="middle" font-size="${fs}px" font-weight="600" fill="#333">${p.name}</text>`;
        if(pw>50&&ph>24) svg+=`<text x="${x+pw/2}" y="${y+ph/2+fs*0.8}" text-anchor="middle" font-size="${fs-1}px" fill="#666">${p.w}×${p.h}</text>`;
      }
    });
    svg+=`</svg>`;
    return svg;
  }

  const doorColors=['#e74c3c','#e91e63','#9b59b6','#8e44ad','#6c3483','#c0392b'];
  const bodyColors=['#2980b9','#1abc9c','#27ae60','#16a085','#2ecc71','#3498db'];
  const uraColors=['#7f8c8d','#95a5a6'];

  function sheetSection(sheets,sheet,colors,title){
    if(!sheets.length) return '';
    let html=`<div class="sec-title">${title} — 원장 ${sheet.w}×${sheet.h}mm · ${sheets.length}장 필요</div>`;
    sheets.forEach((s,si)=>{
      const area=sheet.w*sheet.h;
      const used=s.reduce((a,p)=>a+p.w*p.h,0);
      const pct=(used/area*100).toFixed(1);
      html+=`<div class="sheet-block">`;
      html+=`<div class="sheet-header">${si+1}번 원장 — 사용률 ${pct}% · 자투리 ${fmt(area-used)}mm²</div>`;
      html+=`<div class="sheet-flex">`;
      html+=`<div>${sheetSVG(s,sheet,colors,380)}</div>`;
      html+=`<div class="cut-list"><table><thead><tr><th>부재</th><th>가로</th><th>세로</th></tr></thead><tbody>`;
      s.forEach(p=>{
        html+=`<tr><td>${p.name}</td><td class="r">${p.w}</td><td class="r">${p.h}</td></tr>`;
      });
      html+=`</tbody></table></div></div></div>`;
    });
    return html;
  }

  // Generate print HTML
  const win=window.open('','_blank');
  win.document.write(`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>재단가이드 - ${dateStr}</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Malgun Gothic',sans-serif;font-size:11px;color:#222;padding:20px;line-height:1.5}
h1{font-size:18px;text-align:center;margin-bottom:2px}
.sub{text-align:center;font-size:11px;color:#666;margin-bottom:14px}
.info-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:16px;border:1px solid #ccc;padding:10px;border-radius:4px;background:#fafafa}
.info-grid b{color:#333}
.sec-title{font-size:13px;font-weight:700;background:#333;color:#fff;padding:6px 12px;margin:14px 0 8px;border-radius:3px}
table{width:100%;border-collapse:collapse;margin-bottom:8px;font-size:10px}
th,td{border:1px solid #ccc;padding:3px 6px}
th{background:#eee;font-weight:600;text-align:center}
td.r{text-align:right}
.sheet-block{margin-bottom:16px;page-break-inside:avoid;border:1px solid #ddd;padding:10px;border-radius:4px}
.sheet-header{font-weight:700;font-size:11px;margin-bottom:6px;color:#333}
.sheet-flex{display:flex;gap:16px;align-items:flex-start}
.cut-list{flex:1;min-width:150px}
.cut-list table{font-size:10px}
.parts-table{margin-bottom:14px}
.parts-table th{background:#2c3e50;color:#fff;font-size:10px}
.edge-table th{background:#8e44ad;color:#fff;font-size:10px}
.total-row{font-weight:700;background:#ffffcc}
.mode-badge{display:inline-block;padding:2px 8px;border-radius:3px;font-weight:700;font-size:11px}
.footer{text-align:center;margin-top:16px;font-size:9px;color:#999;border-top:1px solid #ddd;padding-top:8px}
@media print{
  body{padding:10px}
  .sheet-block{page-break-inside:avoid}
  .no-print{display:none}
}
</style></head><body>
<div class="no-print" style="text-align:center;margin-bottom:12px">
  <button onclick="window.print()" style="padding:8px 30px;font-size:14px;background:#2c3e50;color:#fff;border:none;border-radius:4px;cursor:pointer">🖨️ 인쇄하기</button>
  <button onclick="window.close()" style="padding:8px 20px;font-size:14px;background:#95a5a6;color:#fff;border:none;border-radius:4px;cursor:pointer;margin-left:8px">닫기</button>
</div>

<h1>✂️ 재단 가이드</h1>
<div class="sub">에디핏 · ${dateStr} ${d.isOpenMode?'<span class="mode-badge" style="background:#f39c12;color:#fff">📦 오픈장 (도어재 전체)</span>':''}</div>

<div class="info-grid">
  <div><b>외형 치수:</b> ${d.W} × ${d.H} × ${d.D} mm (가로×높이×깊이)</div>
  <div><b>판넬 두께:</b> ${d.T}mm · <b>갭:</b> 3mm</div>
  <div><b>도어:</b> ${d.nDoors}개 · <b>선반:</b> ${d.nShelves}개 · <b>서랍:</b> ${d.nDrawers}개</div>
  <div><b>옵션:</b> ${d.hasBack?'뒷판 ':''}${d.hasToe?'걸레받이('+d.toeH+'mm) ':''}${d.noFloor?'바닥없음 ':''}${d.edge4?'4면엣지 ':''}${d.hasLight?'조명홈 ':''}</div>
  <div><b>도어재:</b> ${d.doorIsNone?'사용안함':d.doorIsBody?'→ 몸통재와 동일':doorSheet.label}</div>
  <div><b>몸통재:</b> ${d.isOpenMode||d.bodyIsDoor?'→ 도어재와 동일':bodySheet.label} / <b>우라판:</b> ${d.uraIsDoor?'→ 도어재와 동일':d.uraIsBody?'→ 몸통재와 동일':uraSheet.label}</div>
</div>

<div class="sec-title">📋 부재 목록 (총 ${d.parts.reduce((s,p)=>s+p.qty,0)}개)</div>
<table class="parts-table">
  <thead><tr><th>부재명</th><th>품목</th><th>재료</th><th>가로(mm)</th><th>세로(mm)</th><th>수량</th><th>면적(mm²)</th></tr></thead>
  <tbody>
    ${d.parts.map(p=>{
      let ml;
      if(p.matType==='door'){
        ml=(d.isOpenMode||d.bodyIsDoor)&&!['도어','서랍도어'].includes(p.cat)?'도어재(몸통)':'도어재';
      } else if(p.matType==='body'){
        ml=(d.doorIsNone||d.doorIsBody)&&['도어','서랍도어'].includes(p.cat)?'몸통재(도어)':
           d.uraIsBody&&p.name.includes('뒷판')?'몸통재(뒷판)':'몸통재';
      } else { ml='우라판'; }
      return `<tr><td>${p.name}</td><td>${p.cat}</td><td>${ml}</td><td class="r">${p.w}</td><td class="r">${p.h}</td><td class="r">${p.qty}</td><td class="r">${fmt(p.w*p.h*p.qty)}</td></tr>`;
    }).join('')}
  </tbody>
</table>

<div class="sec-title">📐 엣지 소요량 (총 ${(totalEdge/1000).toFixed(1)}m)</div>
<table class="edge-table">
  <thead><tr><th>부재명</th><th>수량</th><th>둘레/개(mm)</th><th>소계(mm)</th></tr></thead>
  <tbody>
    ${edgeList.map(e=>`<tr><td>${e.name}</td><td class="r">${e.qty}</td><td class="r">${fmt(e.perimeter)}</td><td class="r">${fmt(e.total)}</td></tr>`).join('')}
    <tr class="total-row"><td colspan="3">합계</td><td class="r">${fmt(totalEdge)}mm = ${(totalEdge/1000).toFixed(1)}m</td></tr>
  </tbody>
</table>

${sheetSection(doorSheets,doorSheet,doorColors,'🎨 도어재 재단')}
${sheetSection(bodySheets,bodySheet,bodyColors,'📦 몸통재 재단')}
${sheetSection(uraSheets,uraSheet,uraColors,'🪵 우라판 재단')}

<div class="sec-title">📊 원장 소요 요약</div>
<table>
  <thead><tr><th>재료</th><th>원장규격</th><th>소요장수</th><th>단가</th><th>금액</th></tr></thead>
  <tbody>
    ${doorSheets.length?`<tr><td>도어재</td><td>${doorSheet.w}×${doorSheet.h}mm</td><td class="r">${doorSheets.length}장</td><td class="r">${fmt(doorSheet.price)}원</td><td class="r">${fmt(doorSheets.length*doorSheet.price)}원</td></tr>`:''}
    ${bodySheets.length?`<tr><td>몸통재</td><td>${bodySheet.w}×${bodySheet.h}mm</td><td class="r">${bodySheets.length}장</td><td class="r">${fmt(bodySheet.price)}원</td><td class="r">${fmt(bodySheets.length*bodySheet.price)}원</td></tr>`:''}
    ${uraSheets.length?`<tr><td>우라판</td><td>${uraSheet.w}×${uraSheet.h}mm</td><td class="r">${uraSheets.length}장</td><td class="r">${fmt(d.uraPrice)}원</td><td class="r">${fmt(uraSheets.length*d.uraPrice)}원</td></tr>`:''}
    <tr class="total-row"><td colspan="2">원자재 합계</td><td class="r">${doorSheets.length+bodySheets.length+uraSheets.length}장</td><td></td><td class="r">${fmt(doorSheets.length*doorSheet.price+bodySheets.length*bodySheet.price+uraSheets.length*d.uraPrice)}원</td></tr>
  </tbody>
</table>

<div class="footer">에디핏 통합단가시스템 · 재단가이드 자동생성 · ${dateStr}</div>
</body></html>`);
  win.document.close();
}

function renderSettings(){
  const body=document.getElementById('set_hgBody');
  CATS.forEach(cat=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${cat}</td><td class="tr">${HG_RATES.BM1112[cat]}원</td><td class="tr">${HG_RATES.BM1201[cat]}원</td>`;
    body.appendChild(tr);
  });
  const swBody=document.getElementById('set_swBody');
  CATS.forEach(cat=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${cat}</td><td class="tr">${SW_RATES.standard[cat]}원</td><td class="tr">${SW_RATES.premium[cat]}원</td>`;
    swBody.appendChild(tr);
  });
  const jhBody=document.getElementById('set_jhBody');
  CATS.forEach(cat=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${cat}</td><td class="tr">${JH_RATES.EC811[cat]}원</td><td class="tr">${JH_RATES.P33[cat]}원</td><td class="tr">${JH_RATES.P59[cat]}원</td>`;
    jhBody.appendChild(tr);
  });
  const mkBody=document.getElementById('set_mkBody');
  const mkCols=['PET','PET2','DAISY','WET3000','URBAN','ASH','5000','OAKN','MANHATTAN'];
  CATS.forEach(cat=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${cat}</td>${mkCols.map(g=>`<td class="tr">${MK_RATES[g][cat]}</td>`).join('')}`;
    mkBody.appendChild(tr);
  });
}

// ===== CABINET CALCULATOR =====
function getSelectData(id){
  const sel=document.getElementById(id);
  const opt=sel.options[sel.selectedIndex];
  return {
    value:sel.value,
    price:parseFloat(opt.dataset.price)||0,
    w:parseFloat(opt.dataset.w)||1220,
    h:parseFloat(opt.dataset.h)||2440,
    label:opt.textContent.split(')')[0]+')'||opt.textContent,
  };
}

function toggleOpenMode(el){
  el.classList.toggle('active');
  const isOpen=el.classList.contains('active');
  const desc=document.getElementById('openModeDesc');
  const bodyMat=document.getElementById('cab_bodyMat');
  const uraMat=document.getElementById('cab_uraMat');
  if(isOpen){
    desc.textContent='측판·상하판·선반·뒷판 전부 도어재로 제작 (도어/서랍 없음)';
    desc.style.color='#F59E0B';
    document.getElementById('cab_doors').value=0;
    document.getElementById('cab_drawers').value=0;
    document.getElementById('cab_doors').disabled=true;
    document.getElementById('cab_drawers').disabled=true;
    document.getElementById('cab_drawerH').disabled=true;
    document.getElementById('ch_back').textContent='뒷판(도어재)';
    // 자재 자동변경
    bodyMat._prevValue=bodyMat.value;
    uraMat._prevValue=uraMat.value;
    bodyMat.value='SAME_AS_DOOR';
    uraMat.value='SAME_AS_DOOR';
  } else {
    desc.textContent='';
    document.getElementById('cab_doors').disabled=false;
    document.getElementById('cab_drawers').disabled=false;
    document.getElementById('cab_drawerH').disabled=false;
    document.getElementById('ch_back').textContent='뒷판(우라)';
    // 자재 복원
    if(bodyMat._prevValue) bodyMat.value=bodyMat._prevValue;
    if(uraMat._prevValue) uraMat.value=uraMat._prevValue;
  }
}

function cab_updateDoorInfo(){}

let CAB_LIST = [];

function cab_readInputs(){
  return {
    W:parseInt(document.getElementById('cab_w').value)||900,
    H:parseInt(document.getElementById('cab_h').value)||2100,
    D:parseInt(document.getElementById('cab_d').value)||580,
    nDoors:parseInt(document.getElementById('cab_doors').value)||0,
    nShelves:parseInt(document.getElementById('cab_shelves').value)||0,
    nDrawers:parseInt(document.getElementById('cab_drawers').value)||0,
    drawerH:parseInt(document.getElementById('cab_drawerH').value)||200,
    toeH:parseInt(document.getElementById('cab_toeH').value)||100,
    isOpen:document.getElementById('ch_open').classList.contains('active'),
    hasBack:document.getElementById('ch_back').classList.contains('active'),
    hasToe:document.getElementById('ch_toe').classList.contains('active'),
    noFloor:document.getElementById('ch_nofloor').classList.contains('active'),
    edge4:document.getElementById('ch_edge4').classList.contains('active'),
    hasLight:document.getElementById('ch_light').classList.contains('active'),
    id:Date.now()+Math.random()
  };
}

function cab_addToList(){
  const c=cab_readInputs();
  if(c.isOpen){c.nDoors=0;c.nDrawers=0;}
  CAB_LIST.push(c);
  cab_renderList();
}

function cab_delFromList(id){
  CAB_LIST=CAB_LIST.filter(c=>c.id!==id);
  cab_renderList();
}

function cab_clearList(){
  if(CAB_LIST.length&&!confirm('전체 삭제?')) return;
  CAB_LIST=[];
  cab_renderList();
}

function cab_renderList(){
  const card=document.getElementById('cab_listCard');
  const tbody=document.getElementById('cab_listBody');
  tbody.innerHTML='';
  card.style.display=CAB_LIST.length?'':'none';
  document.getElementById('cab_listCount').textContent=CAB_LIST.length+'개';

  CAB_LIST.forEach((c,i)=>{
    const mode=c.isOpen?'📦오픈장':'🗄️수납장';
    const opts=[];
    if(c.hasBack) opts.push('뒷판');
    if(c.hasToe) opts.push('걸레('+c.toeH+')');
    if(c.noFloor) opts.push('바닥없음');
    if(c.hasLight) opts.push('조명홈');
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${i+1}</td><td class="tr">${c.W}</td><td class="tr">${c.H}</td><td class="tr">${c.D}</td>
      <td class="tr">${c.nDoors}</td><td class="tr">${c.nShelves}</td><td class="tr">${c.nDrawers}</td>
      <td style="font-size:10px">${mode}</td><td style="font-size:9px;color:#64748B">${opts.join(' ')}</td>
      <td style="text-align:center"><span onclick="cab_delFromList(${c.id})" style="cursor:pointer;color:#F87171;font-size:12px">✕</span></td>`;
    tbody.appendChild(tr);
  });
}

function cab_runAll(){
  // 목록이 비어있으면 현재 입력값 하나로 실행
  if(!CAB_LIST.length){
    const c=cab_readInputs();
    if(c.isOpen){c.nDoors=0;c.nDrawers=0;}
    CAB_LIST.push(c);
    cab_renderList();
  }
  cab_run();
}

function cab_run(){
  const doorMatVal=document.getElementById('cab_doorMat').value;
  const bodyMatVal=document.getElementById('cab_bodyMat').value;
  const uraMatVal=document.getElementById('cab_uraMat').value;

  // 1) 몸통재 확정 (SAME_AS_DOOR가 아닌 경우 먼저)
  const bodyMatRaw=getSelectData('cab_bodyMat');
  const bodyIsDoor=bodyMatVal==='SAME_AS_DOOR';

  // 2) 도어재 확정
  const doorMatRaw=getSelectData('cab_doorMat');
  const doorIsNone=doorMatVal==='NONE';
  const doorIsBody=doorMatVal==='SAME_AS_BODY';
  let doorMat, bodyMat;

  if(doorIsNone){
    // 도어재 없음 → 도어 부재도 몸통재로
    bodyMat=bodyMatRaw;
    doorMat={...bodyMat, label:bodyMat.label+' (도어=몸통)'};
  } else if(doorIsBody){
    // 도어재=몸통재
    bodyMat=bodyMatRaw;
    doorMat={...bodyMat, label:bodyMat.label+' (도어=몸통)'};
  } else if(bodyIsDoor){
    // 몸통재=도어재
    doorMat=doorMatRaw;
    bodyMat={...doorMat, label:doorMat.label+' (몸통=도어)'};
  } else {
    doorMat=doorMatRaw;
    bodyMat=bodyMatRaw;
  }

  // 3) 우라판 확정
  const uraSel=document.getElementById('cab_uraMat');
  const uraIsDoor=uraMatVal==='SAME_AS_DOOR';
  const uraIsBody=uraMatVal==='SAME_AS_BODY';
  let uraPrice, uraSheetW, uraSheetH;

  if(uraIsDoor){
    uraPrice=doorMat.price; uraSheetW=doorMat.w; uraSheetH=doorMat.h;
  } else if(uraIsBody){
    uraPrice=bodyMat.price; uraSheetW=bodyMat.w; uraSheetH=bodyMat.h;
  } else {
    uraPrice=parseFloat(uraSel.options[uraSel.selectedIndex].dataset.price)||14500;
    uraSheetW=1220; uraSheetH=2440;
  }

  const isOpenMode=document.getElementById('ch_open').classList.contains('active');
  const T=18;
  const factRate=(parseInt(document.getElementById('cab_factoryRate').value)||23)/10;
  const margRate=(parseInt(document.getElementById('cab_marginRate').value)||30)/100;
  const gap=3;

  // 자재 타입 결정
  let bodyType='body';
  if(isOpenMode||bodyIsDoor) bodyType='door';
  let doorType='door';
  if(doorIsNone||doorIsBody) doorType='body';
  let uraType='ura';
  if(uraIsDoor) uraType='door';
  else if(uraIsBody) uraType='body';

  // 전체 부재 분해 (CAB_LIST 순회)
  const parts=[];
  let hasLight=false;
  CAB_LIST.forEach((c,ci)=>{
    const W=c.W, H=c.H, D=c.D;
    const nDoors=c.isOpen?0:c.nDoors;
    const nShelves=c.nShelves;
    const nDrawers=c.isOpen?0:c.nDrawers;
    const drawerH=c.drawerH, toeH=c.toeH;
    const hasToe=c.hasToe, hasBack=c.hasBack, noFloor=c.noFloor;
    if(c.hasLight) hasLight=true;
    const innerW=W-T*2;
    const bType=(c.isOpen||bodyIsDoor)?'door':bodyType;
    const prefix=CAB_LIST.length>1?`[${ci+1}]`:'';

    parts.push({name:`${prefix}측판(좌)`,cat:'EP',matType:bType,w:D,h:H,qty:1});
    parts.push({name:`${prefix}측판(우)`,cat:'EP',matType:bType,w:D,h:H,qty:1});
    parts.push({name:`${prefix}상판`,cat:'EP',matType:bType,w:innerW,h:D,qty:1});
    if(!noFloor) parts.push({name:`${prefix}하판`,cat:'EP',matType:bType,w:innerW,h:D,qty:1});
    if(nShelves>0) parts.push({name:`${prefix}선반`,cat:'선반',matType:bType,w:innerW,h:D-20,qty:nShelves});
    if(nDoors>0){
      const doorW=Math.floor((W-gap*(nDoors-1))/nDoors);
      let doorH=H;
      if(hasToe) doorH-=(toeH+gap);
      if(nDrawers>0) doorH-=(drawerH+gap)*nDrawers;
      parts.push({name:`${prefix}도어`,cat:'도어',matType:doorType,w:doorW,h:doorH,qty:nDoors});
    }
    if(nDrawers>0){
      const drwW=nDoors>1?Math.floor(W/nDoors)-gap:W;
      parts.push({name:`${prefix}서랍도어`,cat:'서랍도어',matType:doorType,w:drwW,h:drawerH,qty:nDrawers});
    }
    if(hasToe) parts.push({name:`${prefix}걸레받이`,cat:'걸레받이',matType:bType,w:innerW,h:toeH,qty:1});
    if(hasBack){
      const uType=(c.isOpen||uraIsDoor)?'door':uraIsBody?'body':'ura';
      const backLabel=uType==='door'?'뒷판(도어재)':uType==='body'?'뒷판(몸통재)':'뒷판(우라)';
      const backCat=uType==='ura'?'우라':'EP';
      parts.push({name:`${prefix}${backLabel}`,cat:backCat,matType:uType,w:innerW,h:H-T*2,qty:1});
    }
  });

  // 첫번째 장 기준 정보 (요약용)
  const c0=CAB_LIST[0]||{W:900,H:2100,D:580,nDoors:0,nShelves:0,nDrawers:0};
  const W=c0.W,H=c0.H,D=c0.D,nDoors=c0.nDoors,nShelves=c0.nShelves,nDrawers=c0.nDrawers;
  const edge4=c0.edge4||false, noFloor=c0.noFloor||false, hasToe=c0.hasToe||false, hasBack=c0.hasBack||false;

  // 렌더 부재표
  const pBody=document.getElementById('cab_partsBody');
  pBody.innerHTML='';
  let totalParts=0;
  const useDoorForBody=isOpenMode||bodyIsDoor;
  const useBodyForDoor=doorIsNone||doorIsBody;
  parts.forEach(p=>{
    totalParts+=p.qty;
    let matLabel, tagClass;
    if(p.matType==='door'){
      if(useDoorForBody && !['도어','서랍도어'].includes(p.cat)){matLabel='도어재(몸통)';tagClass='tag-yellow';}
      else{matLabel='도어재';tagClass='tag-pink';}
    } else if(p.matType==='body'){
      if(useBodyForDoor && ['도어','서랍도어'].includes(p.cat)){matLabel='몸통재(도어)';tagClass='tag-yellow';}
      else if(uraIsBody && p.name.includes('뒷판')){matLabel='몸통재(뒷판)';tagClass='tag-yellow';}
      else{matLabel='몸통재';tagClass='tag-blue';}
    } else {
      matLabel='우라판';tagClass='tag-green';
    }
    const tr=document.createElement('tr');
    tr.innerHTML=`<td style="font-weight:500">${p.name}</td><td><span class="tag ${tagClass}">${p.cat}</span></td>
      <td><span class="tag tag-cyan">${matLabel}</span></td>
      <td class="tr">${p.w}</td><td class="tr">${p.h}</td><td class="tr">${p.qty}</td>
      <td class="tr">${fmt(p.w*p.h*p.qty)}</td>`;
    pBody.appendChild(tr);
  });
  document.getElementById('cab_partCount').textContent=totalParts+'개';

  // 재단가이드 데이터 저장
  CUT_GUIDE_DATA = {
    parts, doorMat, bodyMat, uraPrice, isOpenMode, uraSheetW, uraSheetH,
    bodyIsDoor, uraIsDoor, uraIsBody, doorIsNone, doorIsBody,
    W, H, D, T, nDoors, nShelves, nDrawers,
    hasBack, hasToe, noFloor, edge4, hasLight,
    toeH:c0.toeH||100, drawerH:c0.drawerH||200,
    cabList:CAB_LIST
  };

  // Render cutting layout
  renderCuttingLayout(parts, doorMat, bodyMat, uraPrice, uraSheetW, uraSheetH);

  // ===== 9모드 계산 =====
  // 원자재 계산 헬퍼: 반장(0.5장) 단위로 올림
  function calcRaw(partsList){
    let doorArea=0, bodyArea=0, uraArea=0;
    partsList.forEach(p=>{
      const area=p.w*p.h*p.qty;
      if(p.matType==='door') doorArea+=area;
      else if(p.matType==='ura') uraArea+=area;
      else bodyArea+=area;
    });
    const doorSheetArea=doorMat.w*doorMat.h;
    const bodySheetArea=bodyMat.w*bodyMat.h;
    const uraSheetArea=uraSheetW*uraSheetH;

    // 반장 단위 올림 (33% 사용 → 0.5장, 60% → 1장, 120% → 1.5장)
    const doorSheets=doorArea>0?Math.ceil(doorArea/doorSheetArea*2)/2:0;
    const bodySheets=bodyArea>0?Math.ceil(bodyArea/bodySheetArea*2)/2:0;
    const uraSheets=uraArea>0?Math.ceil(uraArea/uraSheetArea*2)/2:0;

    const rawDoor=Math.round(doorSheets*doorMat.price);
    const rawBody=Math.round(bodySheets*bodyMat.price);
    const rawUra=Math.round(uraSheets*uraPrice);
    const raw=rawDoor+rawBody+rawUra;
    return {rawDoor,rawBody,rawUra,raw,doorSheets,bodySheets,uraSheets};
  }

  function calcEdifit(partsList){
    const r=calcRaw(partsList);
    // 원자재 합계 × 공장가 배율 = 공장가
    const factoryPrice=Math.round(r.raw*factRate);
    return {...r, factory:factoryPrice};
  }

  function calcSubcon(partsList, rateTable, minCharge){
    const r=calcRaw(partsList);
    let total=0;
    partsList.forEach(p=>{
      if(p.cat==='우라'){
        // 우라는 원자재 그대로
        const uraSheetArea=uraSheetW*uraSheetH;
        const sheets=Math.ceil(p.w*p.h*p.qty/uraSheetArea*2)/2;
        total+=Math.round(sheets*uraPrice);
        return;
      }
      const area=p.w*p.h;
      const rate=rateTable[p.cat]||rateTable['EP']||60;
      let unit=Math.max(minCharge, Math.round((area/1000)*rate));
      total+=unit*p.qty;
    });
    if(hasLight) total+=10000;
    return {...r, factory:total};
  }

  function calcMixed(partsList, rateTable, minCharge){
    const r=calcRaw(partsList);
    // 몸통+우라만 에디핏 (도어는 외주)
    let edifitBodyArea=0, edifitUraArea=0, subTotal=0;
    partsList.forEach(p=>{
      if(p.matType==='door'){
        const area=p.w*p.h;
        const rate=rateTable[p.cat]||rateTable['도어']||60;
        let unit=Math.max(minCharge, Math.round((area/1000)*rate));
        subTotal+=unit*p.qty;
      } else if(p.matType==='ura'){
        edifitUraArea+=p.w*p.h*p.qty;
      } else {
        edifitBodyArea+=p.w*p.h*p.qty;
      }
    });
    // 에디핏 부분 원자재 (반장 올림)
    const bodySheetArea=bodyMat.w*bodyMat.h;
    const uraSheetArea=uraSheetW*uraSheetH;
    const eBodySheets=edifitBodyArea>0?Math.ceil(edifitBodyArea/bodySheetArea*2)/2:0;
    const eUraSheets=edifitUraArea>0?Math.ceil(edifitUraArea/uraSheetArea*2)/2:0;
    const edifitRaw=Math.round(eBodySheets*bodyMat.price)+Math.round(eUraSheets*uraPrice);
    // 에디핏 부분 공장가 = 원자재 × 배율
    const edifitFactory=Math.round(edifitRaw*factRate);
    return {...r, edifitRaw, edifitFactory, subTotal, factory:edifitFactory+subTotal};
  }

  const hgKey=document.getElementById('cab_hgGrade').value;
  const swKey=document.getElementById('cab_swGrade').value;
  const jhKey=document.getElementById('cab_jhGrade').value;
  const mkKey=document.getElementById('cab_mkGrade').value;
  const hgRates=HG_RATES[hgKey]||HG_RATES.BM1112;
  const swRates=SW_RATES[swKey]||SW_RATES.standard;
  const jhRates=JH_RATES[jhKey]||JH_RATES.EC811;
  const mkRates=MK_RATES[mkKey]||MK_RATES.PET;

  const m1=calcEdifit(parts);
  const m2=calcMixed(parts, hgRates, MIN_HG);
  const m3=calcMixed(parts, swRates, MIN_SW);
  const m4=calcMixed(parts, jhRates, MIN_JH);
  const m5=calcMixed(parts, mkRates, MIN_MK);
  const m6=calcSubcon(parts, hgRates, MIN_HG);
  const m7=calcSubcon(parts, swRates, MIN_SW);
  const m8=calcSubcon(parts, jhRates, MIN_JH);
  const m9=calcSubcon(parts, mkRates, MIN_MK);

  const allModes=[m1,m2,m3,m4,m5,m6,m7,m8,m9];
  const sells=allModes.map(m=>Math.round(m.factory/(1-margRate)));
  const margins=sells.map((s,i)=>s-allModes[i].factory);
  const minSell=Math.min(...sells);

  const grid=document.getElementById('cab_compareGrid');
  grid.innerHTML='';
  const oldGrid2=document.getElementById('cab_compareGrid2');
  if(oldGrid2) oldGrid2.remove();
  grid.style.gridTemplateColumns='repeat(5,1fr)';

  function renderCol(parent, m, isMin){
    const col=document.createElement('div');
    col.className='compare-col';
    if(isMin) col.style.border='2px solid #4ADE80';
    const hasRaw=m.raw!==undefined&&m.raw>0;
    const isEdifit=m.title&&m.title.includes('에디핏<br>전체');
    col.innerHTML=`
      <h4 style="color:${m.color};font-size:10px;line-height:1.3">${m.title}${isMin?'<br><span class="tag tag-green" style="font-size:9px">최저가</span>':''}</h4>
      <div style="font-size:8px;color:#64748B;text-align:center;margin-bottom:4px">${m.desc}</div>
      ${isEdifit?`<div style="text-align:center;margin-bottom:2px"><div style="font-size:7px;color:#64748B">원자재 합계</div><div style="font-size:11px;color:#94A3B8">${fmt(m.raw)}</div></div>`:''}
      <div style="text-align:center;margin-bottom:2px"><div style="font-size:7px;color:#64748B">${isEdifit?'공장가 (원자재×'+factRate+')':'원가'}</div><div style="font-size:13px;font-weight:700;color:${m.color}">${fmt(m.factory)}</div></div>
      <div style="text-align:center;margin-bottom:2px"><div style="font-size:7px;color:#6EE7B7">판매가 (÷${(1-margRate).toFixed(1)})</div><div style="font-size:16px;font-weight:700;color:#4ADE80">${fmt(m.sell)}</div></div>
      <div style="text-align:center"><div style="font-size:7px;color:#64748B">마진</div><div style="font-size:11px;font-weight:600;color:#FACC15">${fmt(m.margin)}</div></div>`;
    parent.appendChild(col);
  }

  // 상단: 에디핏 + 도어만외주 4개
  const topModes=[
    {title:'🏭 에디핏<br>전체생산',color:'#22D3EE',raw:m1.raw,factory:m1.factory,sell:sells[0],margin:margins[0],desc:`도어${m1.doorSheets}장 + 몸통${m1.bodySheets}장 + 우라${m1.uraSheets}장 = ${fmt(m1.raw)}`},
    {title:'🔀 도어→홈그린<br>몸통→에디핏',color:'#A78BFA',raw:m2.raw,factory:m2.factory,sell:sells[1],margin:margins[1],desc:`에디핏${fmt(m2.edifitFactory)}+홈그린${fmt(m2.subTotal)}`},
    {title:'🔀 도어→성우<br>몸통→에디핏',color:'#FB923C',raw:m3.raw,factory:m3.factory,sell:sells[2],margin:margins[2],desc:`에디핏${fmt(m3.edifitFactory)}+성우${fmt(m3.subTotal)}`},
    {title:'🔀 도어→일흥<br>몸통→에디핏',color:'#34D399',raw:m4.raw,factory:m4.factory,sell:sells[3],margin:margins[3],desc:`에디핏${fmt(m4.edifitFactory)}+일흥${fmt(m4.subTotal)}`},
    {title:'🔀 도어→목산<br>몸통→에디핏',color:'#F59E0B',raw:m5.raw,factory:m5.factory,sell:sells[4],margin:margins[4],desc:`에디핏${fmt(m5.edifitFactory)}+목산${fmt(m5.subTotal)}`},
  ];
  topModes.forEach(m=>renderCol(grid, m, m.sell===minSell));

  // 하단: 전체외주 4개
  const grid2=document.createElement('div');
  grid2.id='cab_compareGrid2';
  grid2.style.cssText='display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:12px';
  const btmModes=[
    {title:'📦 전체 홈그린',color:'#60A5FA',factory:m6.factory,sell:sells[5],margin:margins[5],desc:`홈그린 ${hgKey}`},
    {title:'📦 전체 성우',color:'#F472B6',factory:m7.factory,sell:sells[6],margin:margins[6],desc:`성우 DC10%`},
    {title:'📦 전체 일흥건영',color:'#A3E635',factory:m8.factory,sell:sells[7],margin:margins[7],desc:`일흥 ${jhRates.label}`},
    {title:'📦 전체 목산',color:'#E879F9',factory:m9.factory,sell:sells[8],margin:margins[8],desc:`목산 ${mkRates.label.split(' ')[0]}`},
  ];
  btmModes.forEach(m=>renderCol(grid2, m, m.sell===minSell));
  grid.parentNode.insertBefore(grid2,grid.nextSibling);

  // 상세 비교표
  const labels=['에디핏','→홈그린','→성우','→일흥','→목산','홈그린','성우','일흥','목산'];
  const colors2=['#22D3EE','#A78BFA','#FB923C','#34D399','#F59E0B','#60A5FA','#F472B6','#A3E635','#E879F9'];
  const detail=document.getElementById('cab_detailArea');
  detail.innerHTML=`
    <div class="note" style="margin-bottom:12px">
      <b>입력:</b> ${CAB_LIST.length}개 장${CAB_LIST.length>1?' — '+CAB_LIST.map((c,i)=>`[${i+1}]${c.W}×${c.H}×${c.D}`).join(' / '):` ${W}×${H}×${D}mm / 도어${nDoors} 선반${nShelves} 서랍${nDrawers}`} · <b>배율:</b> ×${factRate} / <b>마진:</b> ${Math.round(margRate*100)}%<br>
      <b>홈그린:</b> ${hgKey} / <b>성우:</b> ${swRates.label} / <b>일흥:</b> ${jhRates.label} / <b>목산:</b> ${mkRates.label}<br>
      <span style="font-size:10px;color:#94A3B8"><b>계산식:</b> 에디핏 → 원자재(도어+몸통+우라) × ${factRate} = 공장가 → ÷ ${(1-margRate).toFixed(1)} = 판매가 | 하이브리드 → (몸통+우라)×${factRate} + 외주도어가 = 원가</span>
    </div>
    <div style="overflow-x:auto"><table style="font-size:10px">
      <thead><tr><th class="tl" style="font-size:9px">항목</th>${labels.map((l,i)=>`<th class="tr" style="color:${colors2[i]};font-size:9px">${l}</th>`).join('')}</tr></thead>
      <tbody>
        <tr style="background:#0B0D11"><td colspan="${labels.length+1}" style="font-size:9px;color:#64748B;font-weight:600">📦 원자재 (반장 단위 올림) — 전 모드 동일</td></tr>
        <tr><td style="padding-left:12px">도어재 (${m1.doorSheets}장)</td><td class="tr" style="color:#E879F9" colspan="${labels.length}">${fmt(m1.rawDoor)}원</td></tr>
        <tr><td style="padding-left:12px">몸통재 (${m1.bodySheets}장)</td><td class="tr" style="color:#60A5FA" colspan="${labels.length}">${fmt(m1.rawBody)}원</td></tr>
        <tr><td style="padding-left:12px">우라판 (${m1.uraSheets}장)</td><td class="tr" style="color:#4ADE80" colspan="${labels.length}">${fmt(m1.rawUra)}원</td></tr>
        <tr style="border-bottom:2px solid #334155"><td style="font-weight:700">원자재 합계</td><td class="tr" style="font-weight:700;color:#E2E8F0" colspan="${labels.length}">${fmt(m1.raw)}원</td></tr>
        <tr style="background:#0B0D11"><td colspan="${labels.length+1}" style="font-size:9px;color:#64748B;font-weight:600">🏭 공장가 / 매입가</td></tr>
        <tr><td>계산</td>
          <td class="tr" style="font-size:9px;color:#64748B">${fmt(m1.raw)}×${factRate}</td>
          ${[m2,m3,m4,m5].map(m=>`<td class="tr" style="font-size:9px;color:#64748B">${fmt(m.edifitRaw)}×${factRate}+${fmt(m.subTotal)}</td>`).join('')}
          ${[m6,m7,m8,m9].map(m=>`<td class="tr" style="font-size:9px;color:#64748B">외주합산</td>`).join('')}
        </tr>
        <tr><td style="font-weight:600">공장가/매입가</td>${allModes.map((m,i)=>`<td class="tr" style="font-weight:600;color:${colors2[i]}">${fmt(m.factory)}</td>`).join('')}</tr>
        <tr style="background:#0B0D11"><td colspan="${labels.length+1}" style="font-size:9px;color:#64748B;font-weight:600">💰 판매가 = 공장가 ÷ ${(1-margRate).toFixed(1)} (마진 ${Math.round(margRate*100)}%)</td></tr>
        <tr><td style="font-weight:700">판매가</td>${sells.map((s,i)=>`<td class="tr" style="font-weight:700;color:#4ADE80;font-size:12px">${fmt(s)}${s===minSell?' ★':''}</td>`).join('')}</tr>
        <tr><td>마진</td>${margins.map(m=>`<td class="tr" style="color:#FACC15">${fmt(m)}</td>`).join('')}</tr>
        <tr><td>기준대비</td><td class="tr">-</td>${sells.slice(1).map(s=>{const d=s-sells[0];return `<td class="tr" style="color:${d<0?'#4ADE80':'#F87171'};font-size:9px">${d<0?'▼':'▲'}${fmt(Math.abs(d))}</td>`;}).join('')}</tr>
      </tbody>
    </table></div>`;

  document.getElementById('cab_resultArea').classList.remove('hidden');
  document.getElementById('cab_resultArea').scrollIntoView({behavior:'smooth',block:'start'});
}

// ===== CUTTING LAYOUT ENGINE =====
const CUT_COLORS = {
  door: ['#E11D48','#DB2777','#C026D3','#9333EA','#7C3AED','#6366F1'],
  body: ['#0891B2','#0D9488','#059669','#16A34A','#65A30D','#CA8A04'],
  ura:  ['#78716C','#A8A29E'],
};

function renderCuttingLayout(parts, doorMat, bodyMat, uraPrice, uraSheetW, uraSheetH){
  // Separate parts by material type
  const doorParts=[], bodyParts=[], uraParts=[];
  parts.forEach(p=>{
    // Expand qty into individual pieces
    for(let i=0;i<p.qty;i++){
      const piece={name:p.name+(p.qty>1?` #${i+1}`:''), cat:p.cat, w:p.w, h:p.h, matType:p.matType};
      if(p.matType==='door') doorParts.push(piece);
      else if(p.matType==='ura') uraParts.push(piece);
      else bodyParts.push(piece);
    }
  });

  const usw=uraSheetW||1220, ush=uraSheetH||2440;
  const doorSheet={w:doorMat.w, h:doorMat.h, price:doorMat.price, label:`도어재 원장 (${doorMat.w}×${doorMat.h}mm)`};
  const bodySheet={w:bodyMat.w, h:bodyMat.h, price:bodyMat.price, label:`몸통재 원장 (${bodyMat.w}×${bodyMat.h}mm)`};
  const uraSheet={w:usw, h:ush, price:uraPrice, label:`우라판 원장 (${usw}×${ush}mm)`};

  // Legend
  const legend=document.getElementById('cut_legend');
  legend.innerHTML=`
    <div class="legend-item"><div class="legend-dot" style="background:#E11D48"></div>도어재</div>
    <div class="legend-item"><div class="legend-dot" style="background:#0891B2"></div>몸통재</div>
    <div class="legend-item"><div class="legend-dot" style="background:#78716C"></div>우라판</div>
    <div class="legend-item"><div class="legend-dot" style="background:repeating-linear-gradient(45deg,transparent,transparent 3px,rgba(100,116,139,.3) 3px,rgba(100,116,139,.3) 6px)"></div>자투리</div>`;

  let totalSheets=0;

  // Render each material type
  if(doorParts.length>0){
    const result=packAndRender(doorParts, doorSheet, 'door', '🎨 도어재 재단');
    document.getElementById('cut_doorSection').innerHTML=result.html;
    totalSheets+=result.sheetCount;
  } else {
    document.getElementById('cut_doorSection').innerHTML='';
  }

  if(bodyParts.length>0){
    const result=packAndRender(bodyParts, bodySheet, 'body', '📦 몸통재 재단');
    document.getElementById('cut_bodySection').innerHTML=result.html;
    totalSheets+=result.sheetCount;
  } else {
    document.getElementById('cut_bodySection').innerHTML='';
  }

  if(uraParts.length>0){
    const result=packAndRender(uraParts, uraSheet, 'ura', '🪵 우라판 재단');
    document.getElementById('cut_uraSection').innerHTML=result.html;
    totalSheets+=result.sheetCount;
  } else {
    document.getElementById('cut_uraSection').innerHTML='';
  }

  document.getElementById('cut_sheetCount').textContent=totalSheets+'장';

  // Summary
  const doorSheets=doorParts.length>0?packParts(doorParts,doorSheet).length:0;
  const bodySheets=bodyParts.length>0?packParts(bodyParts,bodySheet).length:0;
  const uraSheets=uraParts.length>0?packParts(uraParts,uraSheet).length:0;
  const totalMatCost=doorSheets*doorSheet.price+bodySheets*bodySheet.price+uraSheets*uraSheet.price;

  document.getElementById('cut_summaryArea').innerHTML=`
    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:10px">
      <div class="cost-box"><div class="lb">도어재</div><div class="val" style="color:#E11D48;font-size:15px">${doorSheets}장<br><span style="font-size:11px;color:#94A3B8">${fmt(doorSheets*doorSheet.price)}원</span></div></div>
      <div class="cost-box"><div class="lb">몸통재</div><div class="val" style="color:#0891B2;font-size:15px">${bodySheets}장<br><span style="font-size:11px;color:#94A3B8">${fmt(bodySheets*bodySheet.price)}원</span></div></div>
      <div class="cost-box"><div class="lb">우라판</div><div class="val" style="color:#78716C;font-size:15px">${uraSheets}장<br><span style="font-size:11px;color:#94A3B8">${fmt(uraSheets*uraSheet.price)}원</span></div></div>
      <div class="cost-box" style="border-color:#334155"><div class="lb">원자재 합계</div><div class="val" style="color:#FACC15;font-size:15px">${totalSheets}장<br><span style="font-size:12px">${fmt(totalMatCost)}원</span></div></div>
    </div>`;
}

// Shelf-based First Fit Decreasing bin packing
function packParts(pieces, sheet){
  // Sort by height descending, then width descending
  const sorted=[...pieces].sort((a,b)=>b.h-a.h || b.w-a.w);
  const kerf=5; // 톱날 여유 5mm
  const sheets=[]; // Each sheet: [{x,y,w,h,name,cat}]

  sorted.forEach(piece=>{
    let pw=piece.w+kerf, ph=piece.h+kerf;
    // Try rotating if it fits better
    let rotated=false;
    let placed=false;

    for(let si=0;si<sheets.length;si++){
      const s=sheets[si];
      // Try to place in each shelf
      const pos=findPosition(s, sheet.w, sheet.h, pw, ph);
      if(pos){
        s.push({x:pos.x, y:pos.y, w:piece.w, h:piece.h, name:piece.name, cat:piece.cat});
        placed=true; break;
      }
      // Try rotated
      if(piece.w!==piece.h){
        const pos2=findPosition(s, sheet.w, sheet.h, piece.h+kerf, piece.w+kerf);
        if(pos2){
          s.push({x:pos2.x, y:pos2.y, w:piece.h, h:piece.w, name:piece.name+'(회전)', cat:piece.cat});
          placed=true; break;
        }
      }
    }
    if(!placed){
      // New sheet
      const newSheet=[{x:0, y:0, w:piece.w, h:piece.h, name:piece.name, cat:piece.cat}];
      sheets.push(newSheet);
    }
  });
  return sheets;
}

function findPosition(placedParts, sheetW, sheetH, pw, ph){
  if(pw>sheetW||ph>sheetH) return null;
  if(placedParts.length===0) return {x:0,y:0};

  // Try shelf algorithm: scan Y levels
  const kerf=5;
  // Build occupied rectangles
  const rects=placedParts.map(p=>({x:p.x,y:p.y,w:p.w+kerf,h:p.h+kerf}));

  // Try positions at top-right of each existing piece, and at y=0
  const candidates=[];
  rects.forEach(r=>{
    candidates.push({x:r.x+r.w, y:r.y}); // right of piece
    candidates.push({x:0, y:r.y+r.h}); // below piece, left edge
    candidates.push({x:r.x, y:r.y+r.h}); // below piece, same x
  });
  candidates.push({x:0,y:0});

  // Sort by y then x (prefer top-left)
  candidates.sort((a,b)=>a.y-b.y||a.x-b.x);

  for(const c of candidates){
    if(c.x+pw>sheetW+kerf || c.y+ph>sheetH+kerf) continue;
    // Check overlap
    const newRect={x:c.x,y:c.y,w:pw,h:ph};
    let overlap=false;
    for(const r of rects){
      if(newRect.x<r.x+r.w && newRect.x+newRect.w>r.x && newRect.y<r.y+r.h && newRect.y+newRect.h>r.y){
        overlap=true; break;
      }
    }
    if(!overlap) return c;
  }
  return null;
}

function packAndRender(pieces, sheet, colorGroup, title){
  const sheets=packParts(pieces, sheet);
  const maxDisplayW=420; // max pixel width for each sheet visual
  const scale=Math.min(maxDisplayW/sheet.w, 350/sheet.h);
  const dispW=Math.round(sheet.w*scale);
  const dispH=Math.round(sheet.h*scale);
  const colors=CUT_COLORS[colorGroup];

  let html=`<div style="margin:16px 0 8px"><b style="color:#CBD5E1;font-size:13px">${title}</b> — 원장 ${sheet.label}</div>`;
  html+=`<div class="cutting-sheets">`;

  let totalUsedArea=0;
  const sheetArea=sheet.w*sheet.h;

  sheets.forEach((s,si)=>{
    let usedArea=0;
    s.forEach(p=>{ usedArea+=p.w*p.h; });
    totalUsedArea+=usedArea;
    const usage=(usedArea/sheetArea*100).toFixed(1);

    html+=`<div class="sheet-wrap">`;
    html+=`<div class="sheet-label">${si+1}번 원장</div>`;
    html+=`<div class="sheet-box" style="width:${dispW}px;height:${dispH}px">`;

    // Render parts
    s.forEach((p,pi)=>{
      const x=Math.round(p.x*scale);
      const y=Math.round(p.y*scale);
      const w=Math.round(p.w*scale);
      const h=Math.round(p.h*scale);
      const color=colors[pi%colors.length];
      const showText=w>30&&h>18;
      const showSize=w>55&&h>30;
      html+=`<div class="cut-part" style="left:${x}px;top:${y}px;width:${w}px;height:${h}px;background:${color}" title="${p.name} ${p.w}×${p.h}mm">`;
      if(showText){
        html+=`<div class="part-info">${p.name}${showSize?`<br><span style="font-size:8px;opacity:.8">${p.w}×${p.h}</span>`:''}</div>`;
      }
      html+=`</div>`;
    });

    html+=`</div>`; // sheet-box
    html+=`<div class="sheet-stats">사용률 <b>${usage}%</b> · 자투리 ${fmt(sheetArea-usedArea)}mm²</div>`;
    html+=`</div>`; // sheet-wrap
  });

  html+=`</div>`; // cutting-sheets

  const totalUsage=(totalUsedArea/(sheetArea*sheets.length)*100).toFixed(1);
  html+=`<div class="note" style="margin-top:8px;text-align:center">총 <b>${sheets.length}장</b> 사용 · 평균 사용률 <b>${totalUsage}%</b> · 원장 단가 ${fmt(sheet.price)}원 × ${sheets.length} = <b style="color:#FACC15">${fmt(sheet.price*sheets.length)}원</b></div>`;

  return {html, sheetCount:sheets.length};
}
let s_items=[];

function s_modeChange(){
  const mode=document.getElementById('s_mode').value;
  const matSel=document.getElementById('s_mat');
  const catSel=document.getElementById('s_cat');
  matSel.innerHTML='';
  catSel.innerHTML='';

  if(mode==='edifit'){
    // 에디핏 자재 목록
    const doorMats=MAT_DB.filter(m=>m.type==='도어재');
    const bodyMats=MAT_DB.filter(m=>m.type.includes('몸통'));
    let html='<optgroup label="도어재">';
    doorMats.forEach(m=>{html+=`<option value="${m.name}" data-price="${m.price}">${m.sup} ${m.name} ${fmt(m.price)}원</option>`;});
    html+='</optgroup><optgroup label="몸통재">';
    bodyMats.forEach(m=>{html+=`<option value="${m.name}" data-price="${m.price}">${m.sup} ${m.name} ${fmt(m.price)}원</option>`;});
    html+='</optgroup>';
    matSel.innerHTML=html;
    CATS.forEach(c=>{catSel.innerHTML+=`<option value="${c}">${c}</option>`;});
  } else if(mode==='homgreen'){
    matSel.innerHTML=`
      <option value="BM1112" data-price="85800" data-w="1220" data-h="2745">BM1112 스탠다드 85,800원</option>
      <option value="BM1201" data-price="97900" data-w="1220" data-h="2745">BM1201 프리미엄 97,900원</option>
      <option value="BM1323" data-price="79200" data-w="1220" data-h="2440">BM1323 79,200원</option>`;
    CATS.forEach(c=>{
      const r=HG_RATES.BM1112[c];
      catSel.innerHTML+=`<option value="${c}">${c} (${r}원/1000mm²)</option>`;
    });
  } else if(mode==='sungwoo'){
    matSel.innerHTML=`
      <option value="standard">한솔계열 (안도크림,포그그레이 등)</option>
      <option value="premium">프리미엄 (클레이크림,바이브실버)</option>`;
    CATS.forEach(c=>{
      const r=SW_RATES.standard[c];
      catSel.innerHTML+=`<option value="${c}">${c} (${r}원/1000mm², DC적용)</option>`;
    });
  } else if(mode==='ilheung'){
    matSel.innerHTML=`
      <option value="EC811">포렐스 EC811 (85,800원/장)</option>
      <option value="P33">사비올라 P33 (233,000원/장)</option>
      <option value="P59">사비올라 P59 (233,000원/장)</option>`;
    CATS.forEach(c=>{
      const r=JH_RATES.EC811[c];
      catSel.innerHTML+=`<option value="${c}">${c} (${r}원/1000mm²)</option>`;
    });
  } else if(mode==='moksan'){
    const grades=['PET','PET2','DAISY','WET3000','URBAN','ASH','5000','OAKN','MANHATTAN','SMOKE','DYE'];
    grades.forEach(g=>{
      const mk=MK_RATES[g];
      matSel.innerHTML+=`<option value="${g}">${mk.label} (${mk.tier})</option>`;
    });
    CATS.forEach(c=>{
      const r=MK_RATES.PET[c];
      catSel.innerHTML+=`<option value="${c}">${c} (${r}원/1000mm²)</option>`;
    });
  } else {
    matSel.innerHTML='<option>데이터 입력 대기중</option>';
    catSel.innerHTML='<option>데이터 입력 대기중</option>';
  }
  s_calc();
}

function s_calc(){
  const mode=document.getElementById('s_mode').value;
  const w=parseFloat(document.getElementById('s_w').value);
  const h=parseFloat(document.getElementById('s_h').value);
  const qty=Math.max(1,parseInt(document.getElementById('s_qty').value)||1);
  const factRate=(parseInt(document.getElementById('s_factRate').value)||23)/10;
  const margRate=(parseInt(document.getElementById('s_margRate').value)||30)/100;

  if(!w||!h||w<=0||h<=0){document.getElementById('s_result').classList.add('hidden');return;}
  document.getElementById('s_result').classList.remove('hidden');

  const area=w*h;
  let raw=0, factory=0, modeLabel='';

  if(mode==='edifit'){
    const opt=document.getElementById('s_mat').selectedOptions[0];
    const matPrice=parseFloat(opt?.dataset?.price)||50000;
    const matW=parseFloat(opt?.dataset?.w)||1220;
    const matH=parseFloat(opt?.dataset?.h)||2440;
    const sheetArea=matW*matH;
    raw=Math.round((area/sheetArea)*matPrice);
    factory=Math.round(raw*factRate);
    modeLabel='에디핏';
    document.getElementById('sr_factLabel').textContent=`공장가 (×${factRate})`;
  } else if(mode==='homgreen'){
    const matKey=document.getElementById('s_mat').value;
    const cat=document.getElementById('s_cat').value;
    const rates=HG_RATES[matKey]||HG_RATES.BM1112;
    const rate=rates[cat]||83;
    const mi={BM1112:{p:85800,w:1220,h:2745},BM1201:{p:97900,w:1220,h:2745},BM1323:{p:79200,w:1220,h:2440}}[matKey]||{p:85800,w:1220,h:2745};
    raw=Math.round((area/(mi.w*mi.h))*mi.p);
    factory=Math.max(MIN_HG,Math.round((area/1000)*rate));
    modeLabel='홈그린';
    document.getElementById('sr_factLabel').textContent='홈그린 매입가';
  } else if(mode==='sungwoo'){
    const gradeKey=document.getElementById('s_mat').value;
    const cat=document.getElementById('s_cat').value;
    const rates=SW_RATES[gradeKey]||SW_RATES.standard;
    const rate=rates[cat]||52;
    raw=0;
    factory=Math.max(MIN_SW,Math.round((area/1000)*rate));
    modeLabel='성우산업';
    document.getElementById('sr_factLabel').textContent='성우 매입가 (DC10%)';
  } else if(mode==='ilheung'){
    const gradeKey=document.getElementById('s_mat').value;
    const cat=document.getElementById('s_cat').value;
    const rates=JH_RATES[gradeKey]||JH_RATES.EC811;
    const rate=rates[cat]||68;
    raw=0;
    factory=Math.max(MIN_JH,Math.round((area/1000)*rate));
    modeLabel='일흥건영';
    document.getElementById('sr_factLabel').textContent=`일흥 매입가 (${rates.label})`;
  } else if(mode==='moksan'){
    const gradeKey=document.getElementById('s_mat').value;
    const cat=document.getElementById('s_cat').value;
    const rates=MK_RATES[gradeKey]||MK_RATES.PET;
    const rate=rates[cat]||53;
    raw=0;
    factory=Math.max(MIN_MK,Math.round((area/1000)*rate));
    modeLabel='목산';
    document.getElementById('sr_factLabel').textContent=`목산 매입가 (${rates.label.split(' ')[0]})`;
  } else {
    raw=0; factory=0; modeLabel=mode;
    document.getElementById('sr_factLabel').textContent='매입가 (데이터 없음)';
  }

  const sell=Math.round(factory/(1-margRate));
  const margin=sell-factory;

  document.getElementById('sr_mat').textContent=fmt(raw)+'원';
  document.getElementById('sr_fact').textContent=fmt(factory)+'원';
  document.getElementById('sr_sellLabel').textContent=`판매가 (마진${Math.round(margRate*100)}%)`;
  document.getElementById('sr_sell').textContent=fmt(sell)+'원';
  document.getElementById('sr_margin').textContent=fmt(margin)+'원';

  window._sCalc={mode:modeLabel,mat:document.getElementById('s_mat').value,cat:document.getElementById('s_cat').value,
    w,h,qty,factory,sell,margin};
}

function s_addItem(){
  if(!window._sCalc) return;
  s_items.push({id:Date.now(),...window._sCalc});
  s_renderItems();
  document.getElementById('s_w').value='';
  document.getElementById('s_h').value='';
  document.getElementById('s_result').classList.add('hidden');
}
function s_removeItem(id){s_items=s_items.filter(i=>i.id!==id);s_renderItems();}
function s_renderItems(){
  const card=document.getElementById('s_itemsCard');
  if(!s_items.length){card.classList.add('hidden');return;}
  card.classList.remove('hidden');
  const body=document.getElementById('s_itemsBody');body.innerHTML='';
  let sF=0,sS=0,sM=0;
  s_items.forEach(item=>{
    sF+=item.factory*item.qty;sS+=item.sell*item.qty;sM+=item.margin*item.qty;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${item.cat}</td><td style="font-size:11px;color:#94A3B8">${item.mat}</td><td>${item.w}×${item.h}</td>
      <td><span class="tag ${item.mode==='에디핏'?'tag-cyan':'tag-blue'}">${item.mode}</span></td>
      <td class="tr">${item.qty}</td><td class="tr" style="color:#22D3EE">${fmt(item.factory)}</td>
      <td class="tr" style="color:#4ADE80">${fmt(item.sell)}</td><td class="tr" style="color:#4ADE80;font-weight:600">${fmt(item.sell*item.qty)}</td>
      <td class="tr"><button class="remove-btn" onclick="s_removeItem(${item.id})">✕</button></td>`;
    body.appendChild(tr);
  });
  document.getElementById('s_summary').innerHTML=`
    <div class="cost-box"><div class="lb">총원가</div><div class="val" style="color:#22D3EE">${fmt(sF)}원</div></div>
    <div class="cost-box"><div class="lb">총판매가</div><div class="val" style="color:#4ADE80">${fmt(sS)}원</div></div>
    <div class="cost-box"><div class="lb">총마진</div><div class="val" style="color:#FACC15">${fmt(sM)}원</div></div>
    <div class="cost-box"><div class="lb">마진율</div><div class="val" style="color:#F472B6">${(sM/sS*100).toFixed(1)}%</div></div>`;
}

// ===== 자재 소요량 계산 =====
function su_calc(){
  const W=parseInt(document.getElementById('su_w').value)||900;
  const H=parseInt(document.getElementById('su_h').value)||2100;
  const D=parseInt(document.getElementById('su_d').value)||580;
  const T=parseInt(document.getElementById('su_t').value)||18;
  const nDoors=parseInt(document.getElementById('su_doors').value)||0;
  const nShelves=parseInt(document.getElementById('su_shelves').value)||0;
  const nDrawers=parseInt(document.getElementById('su_drawers').value)||0;
  const toeH=parseInt(document.getElementById('su_toeH').value)||100;
  const hasBack=document.getElementById('su_back').checked;
  const hasToe=document.getElementById('su_toe').checked;
  const noFloor=document.getElementById('su_nofloor').checked;
  const mode=document.getElementById('su_mode').value;

  const doorShW=parseInt(document.getElementById('su_doorShW').value)||1220;
  const doorShH=parseInt(document.getElementById('su_doorShH').value)||2745;
  const doorShP=parseInt(document.getElementById('su_doorShP').value)||85800;
  const bodyShW=parseInt(document.getElementById('su_bodyShW').value)||1220;
  const bodyShH=parseInt(document.getElementById('su_bodyShH').value)||2440;
  const bodyShP=parseInt(document.getElementById('su_bodyShP').value)||30800;
  const uraShW=parseInt(document.getElementById('su_uraShW').value)||1220;
  const uraShH=parseInt(document.getElementById('su_uraShH').value)||2440;
  const uraShP=parseInt(document.getElementById('su_uraShP').value)||15950;

  const innerW=W-T*2;
  const gap=3;

  // 부재 분해 → 면적 합산
  let doorArea=0, bodyArea=0, uraArea=0;
  const parts=[];

  // 측판 ×2
  parts.push({name:'측판(좌)',w:D,h:H,qty:1,type:'body'});
  parts.push({name:'측판(우)',w:D,h:H,qty:1,type:'body'});
  // 상판
  parts.push({name:'상판',w:innerW,h:D,qty:1,type:'body'});
  // 하판
  if(!noFloor) parts.push({name:'하판',w:innerW,h:D,qty:1,type:'body'});
  // 선반
  if(nShelves>0) parts.push({name:'선반',w:innerW,h:D-20,qty:nShelves,type:'body'});
  // 걸레받이
  if(hasToe) parts.push({name:'걸레받이',w:innerW,h:toeH,qty:1,type:'body'});
  // 도어
  if(nDoors>0){
    const doorW=Math.floor((W-gap*(nDoors-1))/nDoors);
    let doorH=H;
    if(hasToe) doorH-=(toeH+gap);
    if(nDrawers>0) doorH-=(200+gap)*nDrawers;
    parts.push({name:'도어',w:doorW,h:doorH,qty:nDoors,type:'door'});
  }
  // 서랍도어
  if(nDrawers>0){
    const drwW=nDoors>1?Math.floor(W/nDoors)-gap:W;
    parts.push({name:'서랍도어',w:drwW,h:200,qty:nDrawers,type:'door'});
  }
  // 뒷판
  if(hasBack) parts.push({name:'뒷판',w:innerW,h:H-T*2,qty:1,type:'ura'});

  // 모드에 따라 재배치
  parts.forEach(p=>{
    const area=p.w*p.h*p.qty;
    if(mode==='allDoor'){
      // 전부 도어재
      doorArea+=area;
    } else if(mode==='noUra'){
      // 우라→몸통재
      if(p.type==='door') doorArea+=area;
      else bodyArea+=area; // ura도 body로
    } else {
      // 일반
      if(p.type==='door') doorArea+=area;
      else if(p.type==='ura') uraArea+=area;
      else bodyArea+=area;
    }
  });

  // 반장 올림
  const doorSheetArea=doorShW*doorShH;
  const bodySheetArea=bodyShW*bodyShH;
  const uraSheetArea=uraShW*uraShH;

  const doorSheets=doorArea>0?Math.ceil(doorArea/doorSheetArea*2)/2:0;
  const bodySheets=bodyArea>0?Math.ceil(bodyArea/bodySheetArea*2)/2:0;
  const uraSheets=uraArea>0?Math.ceil(uraArea/uraSheetArea*2)/2:0;

  const doorCost=Math.round(doorSheets*doorShP);
  const bodyCost=Math.round(bodySheets*bodyShP);
  const uraCost=Math.round(uraSheets*uraShP);
  const totalCost=doorCost+bodyCost+uraCost;

  const doorPct=doorArea>0?(doorArea/doorSheetArea*100).toFixed(1):'0';
  const bodyPct=bodyArea>0?(bodyArea/bodySheetArea*100).toFixed(1):'0';
  const uraPct=uraArea>0?(uraArea/uraSheetArea*100).toFixed(1):'0';

  const modeLabel=mode==='allDoor'?'📦 전부 도어재 (오픈장)':mode==='noUra'?'🔄 뒷판=몸통재':'일반 (몸통+도어+우라)';

  // 부재 목록 HTML
  let partsHtml=parts.map(p=>{
    let matType;
    if(mode==='allDoor') matType='도어재';
    else if(mode==='noUra') matType=p.type==='door'?'도어재':'몸통재';
    else matType=p.type==='door'?'도어재':p.type==='ura'?'우라판':'몸통재';
    const tagClass=matType==='도어재'?'tag-pink':matType==='우라판'?'tag-green':'tag-blue';
    return `<tr><td>${p.name}</td><td class="tr">${p.w}×${p.h}</td><td class="tr">${p.qty}</td><td class="tr">${fmt(p.w*p.h*p.qty)}</td><td><span class="tag ${tagClass}">${matType}</span></td></tr>`;
  }).join('');

  document.getElementById('su_result').innerHTML=`
    <div class="note" style="margin-bottom:10px;font-size:10px"><b>모드:</b> ${modeLabel} · <b>치수:</b> ${W}×${H}×${D}mm (내부폭 ${innerW}mm)</div>
    <div style="overflow-x:auto;margin-bottom:14px"><table style="font-size:10px">
      <thead><tr><th class="tl">부재</th><th class="tr">치수</th><th class="tr">수량</th><th class="tr">면적</th><th class="tl">자재</th></tr></thead>
      <tbody>${partsHtml}</tbody>
    </table></div>
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:14px">
      ${doorSheets>0?`<div style="background:#0F172A;border:2px solid #E879F9;border-radius:8px;padding:14px;text-align:center">
        <div style="font-size:10px;color:#E879F9;margin-bottom:4px">🎨 도어재</div>
        <div style="font-size:28px;font-weight:700;color:#E879F9">${doorSheets}장</div>
        <div style="font-size:10px;color:#94A3B8">${doorShW}×${doorShH} · 사용 ${doorPct}%</div>
        <div style="font-size:14px;font-weight:600;color:#E2E8F0;margin-top:4px">${fmt(doorCost)}원</div>
      </div>`:`<div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px;text-align:center;color:#475569"><div style="font-size:10px">🎨 도어재</div><div style="font-size:18px;font-weight:700">없음</div></div>`}
      ${bodySheets>0?`<div style="background:#0F172A;border:2px solid #60A5FA;border-radius:8px;padding:14px;text-align:center">
        <div style="font-size:10px;color:#60A5FA;margin-bottom:4px">📦 몸통재</div>
        <div style="font-size:28px;font-weight:700;color:#60A5FA">${bodySheets}장</div>
        <div style="font-size:10px;color:#94A3B8">${bodyShW}×${bodyShH} · 사용 ${bodyPct}%</div>
        <div style="font-size:14px;font-weight:600;color:#E2E8F0;margin-top:4px">${fmt(bodyCost)}원</div>
      </div>`:`<div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px;text-align:center;color:#475569"><div style="font-size:10px">📦 몸통재</div><div style="font-size:18px;font-weight:700">없음</div></div>`}
      ${uraSheets>0?`<div style="background:#0F172A;border:2px solid #4ADE80;border-radius:8px;padding:14px;text-align:center">
        <div style="font-size:10px;color:#4ADE80;margin-bottom:4px">🪵 우라판</div>
        <div style="font-size:28px;font-weight:700;color:#4ADE80">${uraSheets}장</div>
        <div style="font-size:10px;color:#94A3B8">${uraShW}×${uraShH} · 사용 ${uraPct}%</div>
        <div style="font-size:14px;font-weight:600;color:#E2E8F0;margin-top:4px">${fmt(uraCost)}원</div>
      </div>`:`<div style="background:#0F172A;border:1px solid #334155;border-radius:8px;padding:14px;text-align:center;color:#475569"><div style="font-size:10px">🪵 우라판</div><div style="font-size:18px;font-weight:700">없음</div></div>`}
    </div>
    <div style="background:#0B0D11;border-radius:8px;padding:14px;text-align:center">
      <div style="font-size:10px;color:#64748B">원자재 합계 (도어${doorSheets}장 + 몸통${bodySheets}장 + 우라${uraSheets}장 = 총 ${doorSheets+bodySheets+uraSheets}장)</div>
      <div style="font-size:28px;font-weight:700;color:#4ADE80;margin-top:4px">${fmt(totalCost)}원</div>
    </div>`;
}

// ===== 자당가 공식 =====
function pc_calc(){
  const bodyP=parseInt(document.getElementById('pc_bodyP').value)||0;
  const bodyQ=parseInt(document.getElementById('pc_bodyQ').value)||0;
  const uraP=parseInt(document.getElementById('pc_uraP').value)||0;
  const uraQ=parseInt(document.getElementById('pc_uraQ').value)||0;
  const doorP=parseInt(document.getElementById('pc_doorP').value)||0;
  const doorQ=parseInt(document.getElementById('pc_doorQ').value)||0;
  const unit=parseFloat(document.getElementById('pc_unit').value)||4;
  const factRate=parseFloat(document.getElementById('pc_factRate').value)||2;
  const margPct=parseFloat(document.getElementById('pc_margin').value)||30;

  const bodyTotal=bodyP*bodyQ;
  const uraTotal=uraP*uraQ;
  const doorTotal=doorP*doorQ;
  const rawTotal=bodyTotal+uraTotal+doorTotal;
  const factory=Math.round(rawTotal*factRate);
  const sell=Math.round(factory/(1-margPct/100));

  document.getElementById('pc_bodyTotal').textContent=fmt(bodyTotal);
  document.getElementById('pc_uraTotal').textContent=fmt(uraTotal);
  document.getElementById('pc_doorTotal').textContent=fmt(doorTotal);

  document.getElementById('pc_result').innerHTML=`
    <div style="background:#0B0D11;border-radius:8px;padding:16px;display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center;margin-bottom:12px">
      <div>
        <div style="font-size:9px;color:#64748B">${unit}자 자재비 원가</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${fmt(bodyTotal)}+${fmt(uraTotal)}+${fmt(doorTotal)}</div>
        <div style="font-size:20px;font-weight:700;color:#E2E8F0">${fmt(rawTotal)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#22D3EE">공장도가 (×${factRate})</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${unit}자: ${fmt(factory)}</div>
        <div style="font-size:20px;font-weight:700;color:#22D3EE">${fmt(factory)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#4ADE80">영업금액 (÷${(1-margPct/100).toFixed(1)})</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${unit}자: ${fmt(sell)}</div>
        <div style="font-size:24px;font-weight:700;color:#4ADE80">${fmt(sell)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#FACC15">마진</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${unit}자: ${fmt(sell-factory)}</div>
        <div style="font-size:20px;font-weight:700;color:#FACC15">${fmt(sell-factory)}원</div>
      </div>
    </div>
    <div style="background:#0F172A;border:2px solid #334155;border-radius:8px;padding:14px;display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center">
      <div>
        <div style="font-size:9px;color:#64748B">자당 자재비</div>
        <div style="font-size:18px;font-weight:700;color:#E2E8F0">${fmt(Math.round(rawTotal/unit))}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#22D3EE">자당 공장도가</div>
        <div style="font-size:18px;font-weight:700;color:#22D3EE">${fmt(Math.round(factory/unit))}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#4ADE80">자당 영업금액</div>
        <div style="font-size:22px;font-weight:700;color:#4ADE80">${fmt(Math.round(sell/unit))}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#FACC15">자당 마진</div>
        <div style="font-size:18px;font-weight:700;color:#FACC15">${fmt(Math.round((sell-factory)/unit))}원</div>
      </div>
    </div>`;
}

// ===== m당 단가 공식 =====
function pm_calc(){
  const bodyP=parseInt(document.getElementById('pm_bodyP').value)||0;
  const bodyQ=parseInt(document.getElementById('pm_bodyQ').value)||0;
  const uraP=parseInt(document.getElementById('pm_uraP').value)||0;
  const uraQ=parseInt(document.getElementById('pm_uraQ').value)||0;
  const doorP=parseInt(document.getElementById('pm_doorP').value)||0;
  const doorQ=parseInt(document.getElementById('pm_doorQ').value)||0;
  const meter=parseFloat(document.getElementById('pm_meter').value)||4.8;
  const factRate=parseFloat(document.getElementById('pm_factRate').value)||2.5;
  const margPct=parseFloat(document.getElementById('pm_margin').value)||30;

  const bodyTotal=bodyP*bodyQ;
  const uraTotal=uraP*uraQ;
  const doorTotal=doorP*doorQ;
  const rawTotal=bodyTotal+uraTotal+doorTotal;
  const perMeter=Math.round(rawTotal/meter);
  const factory=Math.round(perMeter*factRate);
  const sell=Math.round(factory/(1-margPct/100));

  document.getElementById('pm_bodyTotal').textContent=fmt(bodyTotal);
  document.getElementById('pm_uraTotal').textContent=fmt(uraTotal);
  document.getElementById('pm_doorTotal').textContent=fmt(doorTotal);

  document.getElementById('pm_result').innerHTML=`
    <div style="background:#0B0D11;border-radius:8px;padding:16px;display:grid;grid-template-columns:repeat(4,1fr);gap:12px;text-align:center">
      <div>
        <div style="font-size:9px;color:#64748B">소재합계 ÷ ${meter}m</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${fmt(rawTotal)} ÷ ${meter}</div>
        <div style="font-size:9px;color:#64748B;margin-bottom:2px">소재금액 (m당)</div>
        <div style="font-size:20px;font-weight:700;color:#E2E8F0">${fmt(perMeter)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#64748B">× ${factRate}</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${fmt(perMeter)} × ${factRate}</div>
        <div style="font-size:9px;color:#22D3EE;margin-bottom:2px">공장도가 (m당)</div>
        <div style="font-size:20px;font-weight:700;color:#22D3EE">${fmt(factory)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#64748B">÷ ${(1-margPct/100).toFixed(1)}</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${fmt(factory)} ÷ ${(1-margPct/100).toFixed(1)}</div>
        <div style="font-size:9px;color:#4ADE80;margin-bottom:2px">영업금액 (m당)</div>
        <div style="font-size:24px;font-weight:700;color:#4ADE80">${fmt(sell)}원</div>
      </div>
      <div>
        <div style="font-size:9px;color:#64748B">마진</div>
        <div style="font-size:10px;color:#94A3B8;margin:2px 0">${fmt(sell)} - ${fmt(factory)}</div>
        <div style="font-size:9px;color:#FACC15;margin-bottom:2px">마진 (m당)</div>
        <div style="font-size:20px;font-weight:700;color:#FACC15">${fmt(sell-factory)}원</div>
      </div>
    </div>`;
}

// ===== INIT =====
renderDB();
renderSettings();
s_modeChange();
ord_getSheet();
mq_catChanged();
pm_calc();
pc_calc();
su_calc();
</script>
</div><!-- /appContent -->

<script>
const PW_HASH='bd4ad121aba52582410584712b0753e539f56bb4d39b2a54b721666c29845ca8';
async function sha256(msg){
  const buf=await crypto.subtle.digest('SHA-256',new TextEncoder().encode(msg));
  return Array.from(new Uint8Array(buf)).map(b=>b.toString(16).padStart(2,'0')).join('');
}
async function unlock(){
  const pw=document.getElementById('lockPw').value;
  const hash=await sha256(pw);
  if(hash===PW_HASH){
    document.getElementById('lockScreen').style.display='none';
    document.getElementById('appContent').style.display='block';
    sessionStorage.setItem('edifit_auth','1');
  } else {
    document.getElementById('lockErr').style.display='block';
    document.getElementById('lockPw').value='';
    document.getElementById('lockPw').focus();
  }
}
// 세션 유지 (같은 탭에서 새로고침 시 재로그인 불필요)
if(sessionStorage.getItem('edifit_auth')==='1'){
  document.getElementById('lockScreen').style.display='none';
  document.getElementById('appContent').style.display='block';
}
</script>
</body>
</html>
