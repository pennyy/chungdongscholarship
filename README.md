<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>정동제일교회 장학생 추천 발의 · 프로토타입</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Nanum+Myeongjo:wght@700;800&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css" rel="stylesheet">
<style>
/* ───────── Tokens ───────── */
:root{
  --stone:#ECEEE9; --paper:#FFFFFF; --ink:#1E2730; --ink-2:#56606B; --ink-3:#8A929A;
  --line:#D6DAD3; --brick:#9B3A2C; --brick-soft:#F4E6E2; --moss:#4F6B5B; --moss-soft:#E3ECE6;
  --gold:#B08A3E; --seal:#7E2A20; --warn:#A5621B; --warn-soft:#FBF0E1;
  --r:10px; --shadow:0 1px 0 rgba(30,39,48,.04),0 8px 24px -12px rgba(30,39,48,.18);
  --display:"Nanum Myeongjo",serif; --body:"Pretendard",system-ui,sans-serif; --mono:"IBM Plex Mono",monospace;
}
*{box-sizing:border-box}
html,body{margin:0}
body{font-family:var(--body);background:var(--stone);color:var(--ink);font-size:15px;line-height:1.6;-webkit-font-smoothing:antialiased}
button,input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:2px solid var(--brick);outline-offset:2px}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}

/* ───────── Top bar ───────── */
.top{position:sticky;top:0;z-index:20;background:var(--ink);color:#fff}
.top-in{max-width:1080px;margin:auto;display:flex;align-items:center;gap:24px;padding:0 20px;height:60px}
.brand{display:flex;align-items:baseline;gap:10px;white-space:nowrap}
.brand b{font-family:var(--display);font-size:18px;letter-spacing:-.01em}
.brand span{font-size:12px;color:#AEB6BD}
.tabs{display:flex;gap:4px;margin-left:auto}
.tab{background:none;border:0;color:#C9CFD4;padding:8px 14px;border-radius:999px;cursor:pointer;font-size:14px;white-space:nowrap}
.tab:hover{color:#fff}
.tab[aria-current="page"]{background:#fff;color:var(--ink);font-weight:600}
.proto-flag{font-family:var(--mono);font-size:11px;color:var(--ink);background:var(--gold);padding:2px 8px;border-radius:4px}

/* ───────── Layout ───────── */
main{max-width:1080px;margin:auto;padding:36px 20px 96px}
.hero{display:grid;grid-template-columns:1fr auto;gap:24px;align-items:end;margin-bottom:28px}
.eyebrow{font-size:12px;letter-spacing:.14em;color:var(--brick);font-weight:700}
h1{font-family:var(--display);font-size:34px;line-height:1.25;margin:6px 0 8px;letter-spacing:-.02em}
.lede{color:var(--ink-2);margin:0;max-width:620px}
.grid{display:grid;grid-template-columns:minmax(0,1fr) 300px;gap:24px;align-items:start}
@media (max-width:900px){.grid{grid-template-columns:1fr}.hero{grid-template-columns:1fr}.aside{position:static!important}}

/* ───────── Cards / sections ───────── */
.card{background:var(--paper);border:1px solid var(--line);border-radius:var(--r);box-shadow:var(--shadow)}
.sec{padding:26px 28px;border-bottom:1px solid var(--line)}
.sec:last-child{border-bottom:0}
.sec-h{display:flex;gap:14px;align-items:flex-start;margin-bottom:18px}
.num{flex:none;width:30px;height:30px;border-radius:50%;border:1.5px solid var(--ink);display:grid;place-items:center;font-family:var(--mono);font-size:12px;font-weight:500}
.sec.done .num{background:var(--moss);border-color:var(--moss);color:#fff}
.sec-h h2{font-size:17px;margin:2px 0 2px;letter-spacing:-.01em}
.sec-h p{margin:0;color:var(--ink-2);font-size:13.5px}
.sec.locked{opacity:.45;pointer-events:none}

.row{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:14px 16px}
.row.three{grid-template-columns:repeat(3,minmax(0,1fr))}
.row .full{grid-column:1/-1}
@media (max-width:620px){.row,.row.three{grid-template-columns:1fr}.sec{padding:22px 18px}}
label.f{display:block}
.f > span{display:block;font-size:13px;font-weight:600;margin-bottom:6px}
.f > span em{font-style:normal;color:var(--brick);margin-left:2px}
.f small{display:block;color:var(--ink-3);font-size:12px;margin-top:5px}
input[type=text],input[type=date],input[type=tel],input[type=email],select,textarea{
  width:100%;border:1px solid var(--line);background:#FAFBF9;border-radius:8px;padding:10px 12px;transition:border-color .15s,background .15s}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--ink);background:#fff}
textarea{min-height:130px;resize:vertical;line-height:1.7}
.check{display:flex;gap:10px;align-items:flex-start;font-size:14px;cursor:pointer}
.check input{margin-top:4px;accent-color:var(--brick);width:16px;height:16px}
.consent{background:var(--stone);border-radius:8px;padding:14px 16px;margin-top:16px;font-size:13px;color:var(--ink-2)}
.consent .check{color:var(--ink);font-weight:600;margin-top:8px}

.btn{border:0;border-radius:8px;padding:11px 18px;font-weight:600;cursor:pointer;transition:transform .1s,background .15s,opacity .15s;display:inline-flex;align-items:center;gap:8px}
.btn:active{transform:translateY(1px)}
.btn-ink{background:var(--ink);color:#fff}
.btn-ink:hover{background:#0F161C}
.btn-brick{background:var(--brick);color:#fff}
.btn-brick:hover{background:var(--seal)}
.btn-ghost{background:transparent;border:1px solid var(--line);color:var(--ink)}
.btn-ghost:hover{border-color:var(--ink)}
.btn-sm{padding:7px 12px;font-size:13px}
.btn[disabled]{opacity:.35;cursor:not-allowed;transform:none}

/* ───────── Type picker ───────── */
.types{display:grid;grid-template-columns:repeat(5,minmax(0,1fr));gap:10px}
@media (max-width:760px){.types{grid-template-columns:repeat(2,1fr)}}
.type{position:relative;text-align:left;background:#FAFBF9;border:1px solid var(--line);border-radius:10px;padding:14px 12px 12px;cursor:pointer;transition:border-color .15s,background .15s}
.type:hover{border-color:var(--ink-2)}
.type .l{font-family:var(--mono);font-size:11px;color:var(--ink-3)}
.type b{display:block;font-size:14px;margin:4px 0 4px;line-height:1.35}
.type i{font-style:normal;font-size:12px;color:var(--ink-2);line-height:1.45;display:block}
.type[aria-checked="true"]{background:var(--ink);border-color:var(--ink);color:#fff}
.type[aria-checked="true"] .l,.type[aria-checked="true"] i{color:#B9C1C8}
.type input{position:absolute;opacity:0;pointer-events:none}

/* ───────── Verification ───────── */
.verify{display:flex;align-items:center;gap:10px;margin-top:14px;flex-wrap:wrap}
.pill{display:inline-flex;align-items:center;gap:6px;font-size:12.5px;padding:4px 10px;border-radius:999px;font-weight:600}
.pill.ok{background:var(--moss-soft);color:var(--moss)}
.pill.no{background:var(--brick-soft);color:var(--brick)}
.pill.idle{background:var(--stone);color:var(--ink-2)}
.hint{font-size:12px;color:var(--ink-3);margin-top:10px}
.hint code{font-family:var(--mono);font-size:11.5px;background:var(--stone);padding:1px 5px;border-radius:4px}

/* ───────── Rubric ───────── */
.rubric{width:100%;border-collapse:collapse;font-size:13.5px}
.rubric th{font-weight:600;font-size:12px;color:var(--ink-2);text-align:center;padding:0 4px 10px}
.rubric th:first-child{text-align:left}
.rubric td{border-top:1px solid var(--line);padding:12px 4px;text-align:center}
.rubric td:first-child{text-align:left;font-weight:600}
.rubric td:first-child small{display:block;font-weight:400;color:var(--ink-3);font-size:12px}
.dot{position:relative;display:inline-block;width:26px;height:26px;cursor:pointer}
.dot input{position:absolute;inset:0;opacity:0;cursor:pointer;margin:0}
.dot span{position:absolute;inset:4px;border-radius:50%;border:1.5px solid #B7BDB5;transition:all .12s}
.dot input:checked + span{background:var(--ink);border-color:var(--ink);inset:2px}
.dot input:focus-visible + span{outline:2px solid var(--brick);outline-offset:2px}
@media (max-width:620px){.rubric th:not(:first-child){font-size:10px}}

.warnbox{display:flex;gap:10px;background:var(--warn-soft);color:#6E4210;border-radius:8px;padding:10px 14px;font-size:13px;margin-bottom:12px}
.warnbox b{color:var(--warn)}
.counter{display:flex;justify-content:space-between;font-size:12px;margin-top:6px;color:var(--ink-3)}
.counter .n{font-family:var(--mono)}
.counter .n.ok{color:var(--moss);font-weight:500}
.meter{height:3px;background:var(--stone);border-radius:3px;margin-top:6px;overflow:hidden}
.meter i{display:block;height:100%;background:var(--warn);width:0;transition:width .2s,background .2s}
.meter i.ok{background:var(--moss)}

/* ───────── Aside ───────── */
.aside{position:sticky;top:84px;display:flex;flex-direction:column;gap:16px}
.aside .card{padding:20px}
.aside h3{font-size:13px;letter-spacing:.08em;color:var(--ink-2);margin:0 0 12px;font-weight:700}
.todo{list-style:none;margin:0;padding:0;font-size:13.5px}
.todo li{display:flex;gap:8px;align-items:center;padding:5px 0;color:var(--ink-2)}
.todo li::before{content:"";width:14px;height:14px;border-radius:50%;border:1.5px solid #B7BDB5;flex:none}
.todo li.ok{color:var(--ink)}
.todo li.ok::before{background:var(--moss);border-color:var(--moss);box-shadow:inset 0 0 0 2.5px #fff}
.preview-list{list-style:none;padding:0;margin:0;font-size:13px}
.preview-list li{padding:6px 0;border-top:1px dashed var(--line);display:flex;justify-content:space-between;gap:8px}
.preview-list li:first-child{border-top:0}
.preview-list li span:last-child{color:var(--ink-3);text-align:right}
.tag{font-family:var(--mono);font-size:11px;padding:1px 6px;border-radius:4px;background:var(--stone);color:var(--ink-2)}
.blocker{font-size:12.5px;color:var(--ink-3);margin:10px 0 0;padding:0;list-style:none}
.blocker li::before{content:"· "}
#stuBlocker{display:flex;flex-wrap:wrap;gap:6px}
#stuBlocker li{background:var(--warn-soft);color:#6E4210;padding:3px 10px;border-radius:999px;font-size:12px}
#stuBlocker li::before{content:none}

/* ───────── Sealed envelope (signature) ───────── */
.envelope{position:relative;border-radius:var(--r);background:linear-gradient(160deg,#FBFAF7,#F1EFE9);border:1px solid var(--line);padding:22px 22px 22px 92px;overflow:hidden}
.envelope::before{content:"";position:absolute;inset:0;background:
  linear-gradient(to bottom right,transparent 49.6%,var(--line) 50%,transparent 50.4%) left top/50% 58% no-repeat,
  linear-gradient(to bottom left,transparent 49.6%,var(--line) 50%,transparent 50.4%) right top/50% 58% no-repeat;opacity:.9;pointer-events:none}
.seal{position:absolute;left:22px;top:50%;transform:translateY(-50%);width:54px;height:54px}
.envelope b{font-family:var(--display);font-size:17px;display:block;position:relative}
.envelope p{margin:4px 0 0;font-size:13px;color:var(--ink-2);position:relative}
.envelope .redact{display:flex;gap:6px;margin-top:10px;position:relative;flex-wrap:wrap}
.envelope .redact span{height:8px;border-radius:2px;background:#D8D4CB}

/* ───────── Student ───────── */
.stepper{display:flex;gap:0;margin-bottom:22px;counter-reset:s;flex-wrap:wrap}
.stepper li{list-style:none;flex:1;min-width:110px;font-size:12.5px;color:var(--ink-3);padding:10px 0 0;border-top:3px solid var(--line);margin-right:6px}
.stepper li.on{color:var(--ink);border-color:var(--ink);font-weight:600}
.stepper li.ok{color:var(--moss);border-color:var(--moss)}
.welcome{font-family:var(--display);font-size:26px;line-height:1.4;margin:0 0 6px;letter-spacing:-.02em}
.welcome em{font-style:normal;color:var(--brick)}
.otp{display:flex;gap:8px;align-items:end}
.otp .f{flex:1}
.docs{display:grid;gap:10px}
.doc{display:flex;align-items:center;gap:12px;border:1px dashed #BFC5BD;border-radius:8px;padding:12px 14px;background:#FAFBF9}
.doc.ok{border-style:solid;border-color:var(--moss);background:var(--moss-soft)}
.doc .dn{flex:1;min-width:0}
.doc .dn b{display:block;font-size:14px}
.doc .dn small{color:var(--ink-3);font-size:12px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;display:block}
.doc.ok .dn small{color:var(--moss)}
.doc input[type=file]{display:none}
.segs{display:flex;gap:8px;flex-wrap:wrap}
.seg{position:relative}
.seg input{position:absolute;opacity:0}
.seg span{display:inline-block;padding:8px 14px;border:1px solid var(--line);border-radius:999px;font-size:13.5px;cursor:pointer;background:#FAFBF9}
.seg input:checked + span{background:var(--ink);color:#fff;border-color:var(--ink)}
.seg input:focus-visible + span{outline:2px solid var(--brick);outline-offset:2px}
.reapply{border:1px solid var(--line);border-radius:8px;padding:14px 16px;background:#FAFBF9}
.reapply .f{margin-top:14px}
.office{display:flex;gap:10px;align-items:center;background:var(--moss-soft);color:var(--moss);padding:12px 14px;border-radius:8px;font-size:13.5px;font-weight:600}
.fadein{animation:fi .35s ease both}
@keyframes fi{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}

/* ───────── Board ───────── */
.chips{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px}
.chip{border:1px solid var(--line);background:var(--paper);border-radius:999px;padding:6px 12px;font-size:13px;cursor:pointer}
.chip b{font-family:var(--mono);font-weight:500;margin-left:4px;color:var(--ink-3)}
.chip[aria-pressed="true"]{background:var(--ink);color:#fff;border-color:var(--ink)}
.chip[aria-pressed="true"] b{color:#B9C1C8}
.table-wrap{overflow-x:auto}
table.board{width:100%;border-collapse:collapse;font-size:13.5px;min-width:820px}
.board th{text-align:left;font-size:12px;color:var(--ink-2);font-weight:600;padding:14px 16px;border-bottom:1px solid var(--line);background:#F7F8F5}
.board td{padding:14px 16px;border-bottom:1px solid var(--line);vertical-align:middle}
.board tr:last-child td{border-bottom:0}
.mono{font-family:var(--mono);font-size:12.5px}
.st{display:inline-block;font-size:12px;font-weight:600;padding:3px 9px;border-radius:999px;white-space:nowrap}
.st-WAIT{background:var(--warn-soft);color:var(--warn)}
.st-ACCEPT{background:#E4EAF2;color:#2F4F75}
.st-DECLINE{background:var(--stone);color:var(--ink-3)}
.st-DOCS{background:var(--moss-soft);color:var(--moss)}
.st-DONE{background:var(--ink);color:#fff}
.flow{display:flex;align-items:center;gap:6px;flex-wrap:wrap;font-size:12px;color:var(--ink-2);margin:0 0 18px}
.flow i{font-style:normal;color:var(--ink-3)}
.lock{display:inline-flex;align-items:center;gap:4px;font-size:12px;color:var(--ink-3)}

/* ───────── Modal / toast ───────── */
.scrim{position:fixed;inset:0;background:rgba(20,26,32,.55);display:grid;place-items:center;z-index:50;padding:20px}
.modal{background:var(--paper);border-radius:14px;max-width:760px;width:100%;display:grid;grid-template-columns:1fr 280px;overflow:hidden;max-height:92vh}
.modal .mbody{padding:28px;overflow:auto}
.modal .phone{background:#C9D3DC;padding:26px 18px;display:flex;align-items:center}
@media (max-width:700px){.modal{grid-template-columns:1fr}.modal .phone{display:none}}
.bubble{background:#FFF;border-radius:14px;padding:14px 16px;font-size:13px;box-shadow:0 4px 14px -6px rgba(0,0,0,.25)}
.bubble .bh{background:#FEE500;margin:-14px -16px 12px;padding:9px 16px;border-radius:14px 14px 0 0;font-weight:700;font-size:12.5px}
.bubble .link{display:block;text-align:center;margin-top:12px;background:#F2F3F5;border-radius:8px;padding:9px;font-weight:600}
.kv{display:grid;grid-template-columns:110px 1fr;gap:6px 12px;font-size:13.5px;margin:16px 0 20px}
.kv dt{color:var(--ink-3)}
.kv dd{margin:0}
.toast{position:fixed;left:50%;bottom:28px;transform:translateX(-50%);background:var(--ink);color:#fff;padding:12px 18px;border-radius:10px;font-size:14px;z-index:60;box-shadow:var(--shadow);animation:fi .25s ease both;max-width:90vw}
.toast b{color:var(--gold);font-family:var(--mono)}
.empty{text-align:center;padding:48px 20px;color:var(--ink-2)}
</style>
</head>
<body>
<header class="top">
  <div class="top-in">
    <div class="brand"><b>정동 장학</b><span>추천인 발의형 온라인 지원</span></div>
    <span class="proto-flag">PROTOTYPE</span>
    <nav class="tabs" aria-label="화면 전환">
      <button class="tab" data-go="recommend">추천 발의</button>
      <button class="tab" data-go="board">진행 현황</button>
      <button class="tab" data-go="student">학생 화면</button>
    </nav>
  </div>
</header>
<main id="app"></main>
<div id="layer"></div>

<script>
/* =====================================================================
   0. 설정 데이터 — 장학유형별 폼 스키마 (기획안 p.9~14)
   실제 서비스에서는 이 스키마를 서버에서 내려받아 동적으로 렌더링합니다.
   ===================================================================== */
const SEMESTERS = ['1학기','2학기','3학기','4학기','5학기','6학기','7학기','8학기'];
const F = {
  school:   {id:'school', label:'학교명', type:'text', req:true, ph:'예: 감리교신학대학교'},
  major:    {id:'major', label:'전공학과', type:'text', req:true, ph:'예: 신학과'},
  course:   {id:'course', label:'과정', type:'seg', options:['학사','석사','박사'], req:true},
  semester: {id:'semester', label:'현재 학기', type:'select', options:SEMESTERS, req:true},
  community:{id:'community', label:'소속 공동체명', type:'text', req:true, ph:'예: 대학부 2청년'},
  role:     {id:'role', label:'담당 역할', type:'text', req:true, ph:'예: 찬양팀 리더'},
};
const academic = {title:'전공·과정', hint:'학교 및 전공학과 세부 선택', fields:[F.school,F.major,F.course,F.semester]};
const condition = {title:'장학생 조건', hint:'소속 공동체 및 담당 역할', fields:[F.community,F.role]};

const TYPES = {
  A:{ code:'A', name:'신학생(간사)', short:'신학 전공 · 담당 목사 추천', parent:false, reapply:false,
      recommender:'pastor',
      note:'신학생(간사)은 담당 목사의 추천을 승인에 준하여 관리하므로 별도 심의가 생략됩니다.',
      sections:[ academic, condition,
        {title:'자기 소개', hint:'소속 공동체에서의 개인적인 사역 목표', fields:[
          {id:'intro', label:'앞으로 계획하고 있는 신앙 또는 사역 목표', type:'textarea', req:true, min:150}]} ],
      docs:['등록금고지서','재학증명서'] },
  B:{ code:'B', name:'대학생(교회봉사)', short:'신앙 · 봉사 중심', parent:true, reapply:true, recommender:'member',
      sections:[ academic, condition,
        {title:'자기 소개', hint:'신앙 · 봉사 등 지원 이유', fields:[
          {id:'intro', label:'지원 이유와 앞으로 계획하고 있는 신앙 또는 봉사활동', type:'textarea', req:true, min:150}]} ],
      docs:['등록금고지서','재학증명서'] },
  C:{ code:'C', name:'대학생(가계곤란)', short:'신앙 · 봉사 + 경제상황', parent:true, reapply:true, recommender:'member',
      sections:[ academic, condition,
        {title:'자기 소개', hint:'신앙 · 봉사 · 경제상황 등 지원 이유', fields:[
          {id:'intro', label:'지원 이유와 앞으로 계획하고 있는 신앙 또는 봉사활동', type:'textarea', req:true, min:150},
          {id:'economy', label:'가정의 경제 상황', type:'textarea', req:true, min:100, help:'장학금이 필요한 사유를 구체적으로 적어 주세요. 위원회만 열람합니다.'}]} ],
      docs:['등록금고지서','재학증명서','가족관계증명서','건강보험료 납부확인서(부)','건강보험료 납부확인서(모)'] },
  D:{ code:'D', name:'고등학생', short:'보호자 자녀소개 비중 ↑', parent:true, reapply:true, recommender:'member',
      sections:[
        {title:'인적·학적', hint:'학교명 · 학년 · 반 · 연락처', fields:[
          {id:'school', label:'학교명', type:'text', req:true, ph:'예: 배재고등학교'},
          {id:'grade', label:'학년', type:'seg', options:['1학년','2학년','3학년'], req:true},
          {id:'klass', label:'반', type:'text', req:true, ph:'예: 3반'},
          {id:'contact', label:'연락처', type:'tel', req:true, ph:'010-0000-0000'}]},
        {title:'장학생 조건', hint:'소속 공동체 · 봉사 여부 · 출석', fields:[
          {id:'community', label:'소속 공동체명', type:'text', req:true, ph:'예: 고등부 2학년'},
          {id:'service', label:'교회 봉사 여부', type:'seg', options:['봉사 중','봉사하지 않음'], req:true},
          {id:'serviceDetail', label:'봉사 내용', type:'text', req:false, ph:'예: 고등부 찬양팀 건반', showIf:['service','봉사 중']},
          {id:'attend', label:'최근 6개월 예배 출석', type:'select', options:['매주 출석','월 2~3회','월 1회 이하'], req:true}]},
        {title:'자기 소개 + 자녀 소개', hint:'지원자와 보호자 작성란을 따로 둡니다', fields:[
          {id:'intro', label:'[지원자] 지원 이유와 앞으로의 신앙·봉사 계획', type:'textarea', req:true, min:150},
          {id:'parentIntro', label:'[보호자] 자녀 소개', type:'textarea', req:true, min:150, help:'보호자께서 직접 작성해 주세요.'}]} ],
      docs:['가족관계증명서','건강보험료 납부확인서(부)','건강보험료 납부확인서(모)'] },
  E:{ code:'E', name:'교역자자녀', short:'교회사무실 확인 후 등록', parent:false, reapply:false, recommender:'office',
      note:'교역자자녀 지원은 교회 사무실에서 교역자 자녀임을 확인한 뒤 등록합니다.',
      sections:[ academic,
        {title:'장학생 조건', hint:'보호자 직분', fields:[
          {id:'guardianName', label:'보호자 성명', type:'text', req:true},
          {id:'guardianTitle', label:'보호자 직분', type:'seg', options:['교역자','사역자','선교사'], req:true}]} ],
      docs:['등록금고지서','재학증명서'] },
};
const REAPPLY_FIELD = {id:'testimony', label:'장학수여 간증문', type:'textarea', req:true, min:150,
  help:'직전 학기 장학금은 나에게 어떤 도움이 되었고, 어떻게 사용했는지 적어 주세요.'};

const RUBRIC = [
  {id:'attend', name:'출석률', d:'주일예배·소속 모임 출석'},
  {id:'faith', name:'신앙 태도', d:'예배와 말씀에 임하는 자세'},
  {id:'service', name:'봉사 수준', d:'맡은 역할의 지속성과 책임감'},
  {id:'bond', name:'공동체 관계', d:'구성원과의 관계와 섬김'},
  {id:'growth', name:'성장 가능성', d:'장학금 수여 후 기대되는 변화'},
];
const SCALE = ['매우 미흡','미흡','보통','우수','매우 우수'];

const STATUS = {WAIT:'수락·보완 대기 중', ACCEPT:'지원 수락', DECLINE:'지원 미수락', DOCS:'서류 제출 완료', DONE:'최종 지원 완료'};

/* =====================================================================
   1. 상태 저장소 (프로토타입: 메모리 + localStorage)
   ===================================================================== */
const KEY = 'jd-scholar-proto-v1';
const seed = () => ([
  {id:'REC-2026-0012', token:'t8k2qa', type:'C', createdAt:'2026-09-18',
   student:{name:'김하늘', birth:'2006-03-14', phone:'010-2345-6789', email:'sky@example.com'},
   recommender:{name:'김은혜', dept:'청년부', title:'권사'},
   rubric:{attend:4,faith:5,service:4,bond:5,growth:4}, reason:'(비공개)', status:'WAIT', app:null},
  {id:'REC-2026-0011', token:'p3m9zx', type:'D', createdAt:'2026-09-16',
   student:{name:'박온유', birth:'2009-07-02', phone:'010-3456-7890', email:'onyu@example.com'},
   recommender:{name:'박성실', dept:'고등부', title:'장로'},
   rubric:{attend:5,faith:4,service:3,bond:4,growth:5}, reason:'(비공개)', status:'ACCEPT', app:null},
  {id:'REC-2026-0009', token:'w1n5cd', type:'B', createdAt:'2026-09-10',
   student:{name:'이소망', birth:'2004-11-21', phone:'010-4567-8901', email:'hope@example.com'},
   recommender:{name:'이믿음', dept:'대학부', title:'집사'},
   rubric:{attend:5,faith:5,service:5,bond:4,growth:4}, reason:'(비공개)', status:'DONE',
   app:{id:'APP-2026-0007', receipt:'JD-2026-2-0007', submittedAt:'2026-09-14'}},
]);
let DB;
try{ DB = JSON.parse(localStorage.getItem(KEY)) || seed(); }catch(e){ DB = seed(); }
const save = () => { try{ localStorage.setItem(KEY, JSON.stringify(DB)); }catch(e){} };

/* 학생에게 전달되는 투영(projection) — 평가 점수·추천 사유를 제거한다.
   실제 구현에서는 서버 API가 이 필드를 아예 응답하지 않아야 합니다(Read-Only 차단). */
function studentView(rec){
  const {rubric, reason, ...safe} = rec;
  return JSON.parse(JSON.stringify(safe));
}

/* =====================================================================
   2. 유틸
   ===================================================================== */
const $ = (s, el=document) => el.querySelector(s);
const $$ = (s, el=document) => [...el.querySelectorAll(s)];
const esc = s => String(s ?? '').replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const charCount = s => (s||'').replace(/\s/g,'').length;
const today = () => new Date().toISOString().slice(0,10);
function toast(html, ms=2800){
  const t = document.createElement('div'); t.className='toast'; t.innerHTML = html;
  document.body.appendChild(t); setTimeout(()=>t.remove(), ms);
}
const sealSVG = `<svg class="seal" viewBox="0 0 64 64" aria-hidden="true">
  <path d="M32 3c4 3 8 1 11 4s2 7 5 10 7 3 9 7-1 7 0 11 5 6 3 10-7 3-9 7-1 8-5 9-7-2-10 0-5 6-9 6-6-5-10-6-8 1-10-3 0-7-3-10-8-2-9-6 3-7 2-11-4-6-2-10 7-2 9-6-1-8 3-10 7 1 10-2 5-6 10-6z" fill="#7E2A20"/>
  <circle cx="32" cy="32" r="17" fill="none" stroke="#B85444" stroke-width="1.5"/>
  <path d="M32 21v22M24 29h16" stroke="#F1D9D3" stroke-width="3" stroke-linecap="round"/></svg>`;

/* =====================================================================
   3. 라우팅 (#recommend | #board | #student/<token>)
   ===================================================================== */
function route(){
  const [view, token] = (location.hash.slice(1) || 'recommend').split('/');
  $$('.tab').forEach(t => t.setAttribute('aria-current', t.dataset.go === view ? 'page' : 'false'));
  window.scrollTo(0,0);
  if(view === 'board') return renderBoard();
  if(view === 'student') return renderStudent(token);
  return renderRecommend();
}
$$('.tab').forEach(t => t.onclick = () => {
  if(t.dataset.go === 'student'){
    const first = DB.find(r => r.status === 'WAIT') || DB[0];
    location.hash = 'student/' + (first ? first.token : '');
  } else location.hash = t.dataset.go;
});
window.addEventListener('hashchange', route);

/* =====================================================================
   4. 화면 1 · 추천인 전용 '장학생 추천 발의'
   ===================================================================== */
let R; // 추천 폼 상태
function freshR(){ return {student:{name:'',birth:'',phone:'',email:''}, consent:false, type:null,
  rec:{name:'',dept:'',title:''}, officeOk:false, rubric:{}, reason:''}; }

function renderRecommend(){
  if(!R) R = freshR();
  const app = $('#app');
  app.innerHTML = `
  <div class="hero">
    <div>
      <div class="eyebrow">화면 1 · 추천인 전용</div>
      <h1>이 학생을 추천합니다</h1>
      <p class="lede">추천권이 있는 교인이 학생을 먼저 발의합니다. 여기서 지정한 장학 유형에 따라 학생이 받게 될 지원서가 결정됩니다.</p>
    </div>
  </div>
  <div class="grid">
    <form class="card" id="recForm" novalidate>
      <section class="sec" data-s="1">
        <div class="sec-h"><div class="num">01</div><div><h2>피추천인 기본정보</h2><p>학생에게 추천 알림과 지원서 링크가 발송될 연락처입니다.</p></div></div>
        <div class="row">
          <label class="f"><span>성명<em>*</em></span><input type="text" data-k="student.name" value="${esc(R.student.name)}" placeholder="홍길동" autocomplete="off"></label>
          <label class="f"><span>생년월일<em>*</em></span><input type="date" data-k="student.birth" value="${esc(R.student.birth)}"></label>
          <label class="f"><span>휴대전화<em>*</em></span><input type="tel" data-k="student.phone" value="${esc(R.student.phone)}" placeholder="010-0000-0000"></label>
          <label class="f"><span>이메일<em>*</em></span><input type="email" data-k="student.email" value="${esc(R.student.email)}" placeholder="name@example.com"></label>
        </div>
        <div class="consent">
          수집 항목: 성명, 생년월일, 연락처, 이메일 · 이용 목적: 장학생 추천 알림 및 지원서 작성 안내 · 보유 기간: 장학 심사 종료 후 1년
          <label class="check"><input type="checkbox" data-k="consent" ${R.consent?'checked':''}> 피추천인의 개인정보 수집·이용에 동의하며, 학생 본인에게 사전 고지했습니다.</label>
        </div>
      </section>

      <section class="sec" data-s="2">
        <div class="sec-h"><div class="num">02</div><div><h2>장학 유형 선택</h2><p>유형을 먼저 정해야 이후 항목이 열립니다. 학생에게는 이 유형의 맞춤 지원서만 보입니다.</p></div></div>
        <div class="types" role="radiogroup" aria-label="장학 유형">
          ${Object.values(TYPES).map(t => `
            <label class="type" role="radio" aria-checked="${R.type===t.code}" tabindex="0" data-type="${t.code}">
              <input type="radio" name="type" value="${t.code}" ${R.type===t.code?'checked':''}>
              <span class="l">유형 ${t.code}</span><b>${t.name}</b><i>${t.short}</i>
            </label>`).join('')}
        </div>
      </section>

      <section class="sec" data-s="3" id="s3"></section>
      <section class="sec" data-s="4" id="s4"></section>
      <section class="sec" data-s="5" id="s5"></section>
    </form>

    <aside class="aside">
      <div class="card">
        <h3>제출 전 확인</h3>
        <ul class="todo" id="todo"></ul>
        <button class="btn btn-brick" id="submitRec" style="width:100%;justify-content:center;margin-top:16px" disabled>추천서 제출하기</button>
        <ul class="blocker" id="blocker"></ul>
      </div>
      <div class="card" id="formPreview"></div>
    </aside>
  </div>`;

  // 바인딩
  $$('[data-k]', app).forEach(bindInput);
  $$('.type', app).forEach(el => {
    const pick = () => { if(R.type !== el.dataset.type){ R.type = el.dataset.type; R.officeOk=false; } renderRecommendDynamic(); $$('.type').forEach(x=>x.setAttribute('aria-checked', x.dataset.type===R.type)); };
    el.addEventListener('click', e => { e.preventDefault(); pick(); });
    el.addEventListener('keydown', e => { if(e.key===' '||e.key==='Enter'){ e.preventDefault(); pick(); } });
  });
  $('#submitRec').onclick = submitRecommendation;
  renderRecommendDynamic();
}

function bindInput(el){
  const path = el.dataset.k.split('.');
  const ev = el.type === 'checkbox' ? 'change' : 'input';
  el.addEventListener(ev, () => {
    let o = R; path.slice(0,-1).forEach(p => o = o[p]);
    o[path.at(-1)] = el.type === 'checkbox' ? el.checked : el.value;
    if(path[0] === 'reason') paintReason();
    updateRecommendChecks();
  });
}

/* 유형에 따라 03~05 섹션이 달라진다 */
function renderRecommendDynamic(){
  const t = TYPES[R.type];
  const s3 = $('#s3'), s4 = $('#s4'), s5 = $('#s5');
  [s3,s4,s5].forEach(s => s.classList.toggle('locked', !t));

  if(t && t.recommender === 'office'){
    s3.innerHTML = `
      <div class="sec-h"><div class="num">03</div><div><h2>교회사무실 확인</h2><p>${t.note}</p></div></div>
      <label class="check"><input type="checkbox" id="officeOk" ${R.officeOk?'checked':''}> 교회사무실 담당자로서 피추천인이 교역자·사역자·선교사의 자녀임을 확인했습니다.</label>`;
    s4.innerHTML = `<div class="sec-h"><div class="num">04</div><div><h2>루브릭 평가</h2><p>교역자자녀 유형은 루브릭 평가를 생략합니다.</p></div></div>`;
    s5.innerHTML = `<div class="sec-h"><div class="num">05</div><div><h2>추천 사유</h2><p>교역자자녀 유형은 추천 사유 작성을 생략합니다.</p></div></div>`;
    $('#officeOk').onchange = e => { R.officeOk = e.target.checked; updateRecommendChecks(); };
  } else {
    const pastorOnly = t && t.recommender === 'pastor';
    s3.innerHTML = `
      <div class="sec-h"><div class="num">03</div><div><h2>추천인 정보</h2>
        <p>${pastorOnly ? '신학생(간사) 유형은 <b>소속 담당 목사</b>가 추천합니다.' : '추천인의 소속 부서와 직분을 적어 주세요. <b>교역자와 사역자는 추천인이 될 수 없습니다.</b>'}</p></div></div>
      <div class="row three">
        <label class="f"><span>추천인 성명<em>*</em></span><input type="text" data-k="rec.name" value="${esc(R.rec.name)}" autocomplete="off"></label>
        <label class="f"><span>소속 부서<em>*</em></span><input type="text" data-k="rec.dept" value="${esc(R.rec.dept)}" placeholder="예: 청년부"></label>
        <label class="f"><span>직분<em>*</em></span><input type="text" data-k="rec.title" value="${esc(R.rec.title)}" placeholder="${pastorOnly?'예: 담당목사':'예: 권사'}"></label>
      </div>
      <p class="hint">입력한 추천인 정보는 장학사업위원회가 심사 단계에서 확인합니다.</p>`;
    s4.innerHTML = `
      <div class="sec-h"><div class="num">04</div><div><h2>루브릭 평가</h2><p>항목마다 5단계 중 하나를 고르세요. 이 평가는 학생에게 공개되지 않습니다.</p></div></div>
      <table class="rubric">
        <thead><tr><th>평가 항목</th>${SCALE.map(s=>`<th>${s}</th>`).join('')}</tr></thead>
        <tbody>${RUBRIC.map(r => `<tr><td>${r.name}<small>${r.d}</small></td>${SCALE.map((s,i)=>`
          <td><label class="dot" title="${s}"><input type="radio" name="rb-${r.id}" value="${i+1}" ${R.rubric[r.id]==i+1?'checked':''} aria-label="${r.name} ${s}"><span></span></label></td>`).join('')}</tr>`).join('')}
        </tbody></table>`;
    s5.innerHTML = `
      <div class="sec-h"><div class="num">05</div><div><h2>추천 사유</h2><p>학생을 가까이서 본 사람만 쓸 수 있는 구체적인 장면을 적어 주세요.</p></div></div>
      <div class="warnbox"><b>!</b><div>추천 사유가 모호하거나 형식적이면 <b>심사에서 감점되거나 탈락할 수 있습니다.</b> 공백 제외 300자 이상 작성해야 제출할 수 있습니다.</div></div>
      <textarea data-k="reason" placeholder="예) 2년간 대학부 새가족 담당으로 섬기며 매주 결석자에게 먼저 연락했고…">${esc(R.reason)}</textarea>
      <div class="meter"><i id="rMeter"></i></div>
      <div class="counter"><span>공백 제외 기준</span><span class="n" id="rCount"></span></div>`;
    $$('[data-k]', s3).forEach(bindInput);
    $$('[data-k]', s5).forEach(bindInput);
    $$('.rubric input').forEach(el => el.onchange = () => { R.rubric[el.name.slice(3)] = +el.value; updateRecommendChecks(); });
    paintReason();
  }
  renderFormPreview();
  updateRecommendChecks();
}

function paintReason(){
  const n = charCount(R.reason), ok = n >= 300;
  const c = $('#rCount'), m = $('#rMeter'); if(!c) return;
  c.textContent = `${n} / 300자`; c.classList.toggle('ok', ok);
  m.style.width = Math.min(100, n/3) + '%'; m.classList.toggle('ok', ok);
}

const recFilled = () => ['name','dept','title'].every(k => R.rec[k].trim());
function recommendChecks(){
  const s = R.student, t = TYPES[R.type];
  const list = [
    ['피추천인 기본정보', s.name.trim() && s.birth && /^01\d-?\d{3,4}-?\d{4}$/.test(s.phone.trim()) && /\S+@\S+\.\S+/.test(s.email)],
    ['개인정보 수집·이용 동의', R.consent],
    ['장학 유형 선택', !!t],
  ];
  if(t && t.recommender === 'office') list.push(['교회사무실 확인', R.officeOk]);
  else {
    list.push(['추천인 정보 입력', recFilled()]);
    list.push([`루브릭 평가 (${RUBRIC.filter(r=>R.rubric[r.id]).length}/${RUBRIC.length})`, RUBRIC.every(r => R.rubric[r.id])]);
    list.push([`추천 사유 300자 이상 (${charCount(R.reason)}자)`, charCount(R.reason) >= 300]);
  }
  return list;
}
function updateRecommendChecks(){
  const list = recommendChecks();
  $('#todo').innerHTML = list.map(([l,ok]) => `<li class="${ok?'ok':''}">${l}</li>`).join('');
  const all = list.every(x => x[1]);
  $('#submitRec').disabled = !all;
  $('#blocker').innerHTML = all ? '' : `<li>남은 항목 ${list.filter(x=>!x[1]).length}개를 채우면 제출할 수 있습니다.</li>`;
  // 섹션 완료 표시
  const secDone = {1: list[0][1] && list[1][1], 2: list[2][1]};
  const t = TYPES[R.type];
  if(t){ if(t.recommender==='office'){ secDone[3]=R.officeOk; secDone[4]=secDone[5]=R.officeOk; }
    else { secDone[3]=recFilled(); secDone[4]=RUBRIC.every(r=>R.rubric[r.id]); secDone[5]=charCount(R.reason)>=300; } }
  $$('#recForm .sec').forEach(s => s.classList.toggle('done', !!secDone[s.dataset.s]));
}

/* 오른쪽 패널: 선택한 유형이 학생에게 어떤 폼을 보낼지 미리보기 */
function renderFormPreview(){
  const t = TYPES[R.type]; const el = $('#formPreview');
  if(!t){ el.innerHTML = `<h3>학생에게 갈 지원서</h3><p style="margin:0;font-size:13px;color:var(--ink-3)">장학 유형을 고르면 학생이 받게 될 지원서 구성이 여기에 표시됩니다.</p>`; return; }
  el.innerHTML = `<h3>학생에게 갈 지원서</h3>
    <div style="font-weight:700;margin-bottom:8px"><span class="tag">유형 ${t.code}</span> ${t.name}</div>
    <ul class="preview-list">
      <li><span>본인인증·추천 수락</span><span>필수</span></li>
      ${t.parent ? `<li><span>보호자 인증·동의</span><span>필수</span></li>` : ''}
      ${t.sections.map(s => `<li><span>${s.title}</span><span>${s.fields.length}문항</span></li>`).join('')}
      ${t.reapply ? `<li><span>장학수여 간증문</span><span>재지원 시</span></li>` : ''}
      <li><span>증빙서류</span><span>${t.docs.length}종</span></li>
    </ul>
    ${t.note ? `<p class="hint" style="margin-top:12px">${t.note}</p>` : ''}`;
}

function submitRecommendation(){
  const n = String(13 + DB.filter(r=>r.id>'REC-2026-0012').length).padStart(4,'0');
  const rec = {
    id:`REC-2026-${n}`, token: Math.random().toString(36).slice(2,8), type:R.type, createdAt:today(),
    student:{...R.student}, recommender: TYPES[R.type].recommender==='office' ? {name:'교회사무실', dept:'행정', title:'담당자'} : {...R.rec},
    rubric:{...R.rubric}, reason:R.reason, status:'WAIT', app:null };
  DB.unshift(rec); save();
  const t = TYPES[rec.type];
  const link = `${location.pathname}#student/${rec.token}`;
  $('#layer').innerHTML = `
  <div class="scrim" role="dialog" aria-modal="true" aria-labelledby="mt">
    <div class="modal fadein">
      <div class="mbody">
        <div class="eyebrow">화면 2 · 추천 내용 알림</div>
        <h2 id="mt" style="font-family:var(--display);font-size:24px;margin:6px 0 4px">추천서가 제출되었습니다</h2>
        <p style="margin:0;color:var(--ink-2);font-size:14px">지원 현황에 <b>${STATUS.WAIT}</b> 상태로 등록되었습니다. 위원회가 학생과 보호자에게 오른쪽 알림을 보냅니다.</p>
        <dl class="kv">
          <dt>추천서 ID</dt><dd class="mono">${rec.id}</dd>
          <dt>피추천인</dt><dd>${esc(rec.student.name)} · ${esc(rec.student.phone)}</dd>
          <dt>장학 유형</dt><dd>유형 ${t.code} ${t.name}</dd>
          <dt>학생 공개 범위</dt><dd><span class="lock">🔒</span> 추천 사실·추천인 이름만 공개 (평가·사유 비공개)</dd>
        </dl>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <a class="btn btn-ink" href="${link}" id="goStudent">학생 화면 열어 보기</a>
          <a class="btn btn-ghost" href="#board" id="goBoard">진행 현황 보기</a>
          <button class="btn btn-ghost" id="newRec">새 추천 작성</button>
        </div>
      </div>
      <div class="phone"><div class="bubble">
        <div class="bh">알림톡 · 정동제일교회 장학사업위원회</div>
        <b>${esc(rec.student.name)} 님</b>, 교회 공동체(추천인: ${esc(rec.recommender.name)})로부터 <b>${t.name}</b> 장학생으로 추천받으셨습니다.<br><br>
        아래 링크에서 본인 확인 후 추천을 수락하고 지원서를 작성해 주세요.
        <span class="link">지원서 작성하기</span>
      </div></div>
    </div>
  </div>`;
  const close = () => $('#layer').innerHTML = '';
  $('#goStudent').onclick = close; $('#goBoard').onclick = close;
  $('#newRec').onclick = () => { close(); R = freshR(); renderRecommend(); };
  R = freshR();
}

/* =====================================================================
   5. 지원 진행 현황판 (화면 2 / 화면 4 일부)
   ===================================================================== */
let boardFilter = 'ALL';
function renderBoard(){
  const counts = Object.keys(STATUS).reduce((a,k)=>(a[k]=DB.filter(r=>r.status===k).length,a),{});
  const rows = DB.filter(r => boardFilter==='ALL' || r.status===boardFilter);
  $('#app').innerHTML = `
  <div class="hero"><div>
    <div class="eyebrow">위원회 · 지원 진행 현황판</div>
    <h1>누가, 어디까지 왔는지</h1>
    <p class="lede">추천서 ID와 학생 지원서 ID는 최종 제출 시 하나의 통합 접수번호로 묶입니다. 추천 평가 내용은 이 목록에도 노출하지 않습니다.</p>
  </div>
  <button class="btn btn-ghost btn-sm" id="reset">데모 데이터 초기화</button></div>
  <p class="flow">${['WAIT','ACCEPT','DOCS','DONE'].map(k=>`<span class="st st-${k}">${STATUS[k]}</span>`).join('<i>→</i>')} <i>·</i> <span class="st st-DECLINE">${STATUS.DECLINE}</span></p>
  <div class="chips">
    <button class="chip" data-f="ALL" aria-pressed="${boardFilter==='ALL'}">전체<b>${DB.length}</b></button>
    ${Object.entries(STATUS).map(([k,v])=>`<button class="chip" data-f="${k}" aria-pressed="${boardFilter===k}">${v}<b>${counts[k]}</b></button>`).join('')}
  </div>
  <div class="card table-wrap">
    ${rows.length ? `<table class="board">
      <thead><tr><th>추천서 ID</th><th>피추천인</th><th>장학 유형</th><th>추천인</th><th>상태</th><th>통합 접수번호</th><th>학생 링크</th></tr></thead>
      <tbody>${rows.map(r => `<tr>
        <td class="mono">${r.id}<div style="color:var(--ink-3);font-size:11px">${r.createdAt}</div></td>
        <td><b>${esc(r.student.name)}</b><div style="color:var(--ink-3);font-size:12px">${esc(r.student.phone)}</div></td>
        <td><span class="tag">${r.type}</span> ${TYPES[r.type].name}</td>
        <td>${esc(r.recommender.name)} <span style="color:var(--ink-3);font-size:12px">${esc(r.recommender.dept)} ${esc(r.recommender.title)}</span></td>
        <td><span class="st st-${r.status}">${STATUS[r.status]}</span></td>
        <td class="mono">${r.app?.receipt ? `${r.app.receipt}<div style="color:var(--ink-3);font-size:11px">${r.id} + ${r.app.id}</div>` : '—'}</td>
        <td><a class="btn btn-ghost btn-sm" href="#student/${r.token}">열기</a> <button class="btn btn-ghost btn-sm" data-copy="${r.token}">복사</button></td>
      </tr>`).join('')}</tbody></table>`
    : `<div class="empty">이 상태의 지원 건이 없습니다. 다른 상태를 선택하거나 <a href="#recommend">새 추천을 작성</a>하세요.</div>`}
  </div>`;
  $$('.chip').forEach(c => c.onclick = () => { boardFilter = c.dataset.f; renderBoard(); });
  $$('[data-copy]').forEach(b => b.onclick = () => {
    const url = location.href.split('#')[0] + '#student/' + b.dataset.copy;
    navigator.clipboard?.writeText(url); toast('학생 지원서 링크를 복사했습니다');
  });
  $('#reset').onclick = () => { DB = seed(); save(); boardFilter='ALL'; renderBoard(); toast('데모 데이터를 초기화했습니다'); };
}

/* =====================================================================
   6. 화면 3 · 학생 전용 '추천 수락 및 증빙서류 제출'
      — 추천인이 지정한 유형(TYPES[x])의 스키마로 폼을 동적 렌더링
   ===================================================================== */
const S = {}; // 토큰별 학생 세션 상태
function sessionFor(token){
  if(!S[token]) S[token] = {stage:'auth', auth:{name:'',birth:'',phone:'',email:''}, parent:{name:'',phone:'',agree:false}, data:{}, files:{}, reapply:false};
  return S[token];
}

function renderStudent(token){
  const raw = DB.find(r => r.token === token);
  if(!raw){ $('#app').innerHTML = `<div class="card empty"><h2 style="font-family:var(--display)">유효하지 않은 링크입니다</h2><p>알림으로 받은 링크를 다시 열거나 장학사업위원회에 문의하세요.</p><a class="btn btn-ink" href="#board">진행 현황으로</a></div>`; return; }
  const rec = studentView(raw);            // ← 평가 점수·추천 사유가 제거된 데이터만 사용
  const t = TYPES[rec.type]; const ss = sessionFor(token);
  if(raw.status === 'DECLINE') ss.stage = 'declined';
  if(raw.status === 'DONE') ss.stage = 'done';

  const steps = [['auth','본인정보·수락'], ...(t.parent?[['parent','보호자 정보·동의']]:[]), ['form','지원서 작성'], ['done','최종 제출']];
  const idx = steps.findIndex(s => s[0] === ss.stage);

  $('#app').innerHTML = `
  <div class="hero"><div>
    <div class="eyebrow">화면 3 · 학생 전용 <span class="tag" style="margin-left:6px">링크 ${esc(token)}</span></div>
    <p class="welcome" style="margin-top:8px"><em>${esc(rec.student.name)}</em> 님, 공동체가 당신을 추천했습니다.</p>
    <p class="lede">${esc(rec.recommender.dept)} ${esc(rec.recommender.title)} <b>${esc(rec.recommender.name)}</b> 님이 <b>${t.name}</b> 장학생으로 추천했습니다.</p>
  </div></div>
  ${ss.stage!=='declined' ? `<ol class="stepper">${steps.map((s,i)=>`<li class="${i<idx?'ok':i===idx?'on':''}">${i<idx?'✓ ':''}${s[1]}</li>`).join('')}</ol>` : ''}
  <div class="grid">
    <div id="stuMain"></div>
    <aside class="aside">
      <div class="envelope">${sealSVG}
        <b>봉인된 추천서</b>
        <p>평가 점수와 추천 사유는 장학사업위원회만 열람합니다. 학생 화면에서는 열 수 없습니다.</p>
        <div class="redact"><span style="width:60px"></span><span style="width:34px"></span><span style="width:80px"></span><span style="width:46px"></span><span style="width:70px"></span></div>
      </div>
      <div class="card" id="stuSide"></div>
    </aside>
  </div>`;

  const main = $('#stuMain');
  ({auth:stuAuth, parent:stuParent, form:stuForm, done:stuDone, declined:stuDeclined}[ss.stage])(main, raw, rec, t, ss);
  renderStuSide(t, ss);
}

function renderStuSide(t, ss){
  const el = $('#stuSide'); if(!el) return;
  el.innerHTML = `<h3>나의 지원서 구성</h3>
    <div style="font-weight:700;margin-bottom:8px"><span class="tag">유형 ${t.code}</span> ${t.name}</div>
    <ul class="preview-list">${t.sections.map(s=>`<li><span>${s.title}</span><span>${s.hint}</span></li>`).join('')}
    <li><span>증빙서류</span><span>${t.docs.join(' · ')}</span></li></ul>
    ${t.note ? `<p class="hint" style="margin-top:12px">${t.note}</p>`:''}`;
}

/* 6-1 본인정보 입력 및 추천 수락
   대조 서버가 없으므로 정보 일치 확인은 하지 않는다.
   4개 항목을 모두 입력하면 바로 추천 수락 단계가 열린다. (서버 연동 시 이 지점에서 대조) */
const normPhone = v => String(v||'').replace(/\D/g,'');
const authFilled = a => a.name.trim() && a.birth && normPhone(a.phone).length >= 10 && /\S+@\S+\.\S+/.test(a.email.trim());
function stuAuth(main, raw, rec, t, ss){
  main.innerHTML = `<div class="card fadein">
    <section class="sec" id="authSec">
      <div class="sec-h"><div class="num">01</div><div><h2>본인정보 입력</h2><p>성명·생년월일·휴대전화·이메일을 모두 입력하면 아래 추천 수락 단계가 열립니다.</p></div></div>
      <div class="row">
        <label class="f"><span>성명<em>*</em></span><input type="text" id="aName" value="${esc(ss.auth.name)}" autocomplete="name"></label>
        <label class="f"><span>생년월일<em>*</em></span><input type="date" id="aBirth" value="${esc(ss.auth.birth)}"></label>
        <label class="f"><span>휴대전화<em>*</em></span><input type="tel" id="aPhone" value="${esc(ss.auth.phone)}" placeholder="010-0000-0000" autocomplete="tel"></label>
        <label class="f"><span>이메일<em>*</em></span><input type="email" id="aEmail" value="${esc(ss.auth.email)}" placeholder="name@example.com" autocomplete="email"></label>
      </div>
      <div class="verify" id="aState"></div>
    </section>
    <section class="sec locked" id="acceptSec">
      <div class="sec-h"><div class="num">02</div><div><h2>추천 수락</h2><p>수락하면 ${t.parent?'보호자 동의 후 ':''}<b>${t.name}</b> 맞춤 지원서가 열립니다.</p></div></div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn btn-brick" id="accept" disabled>추천을 수락하고 지원합니다</button>
        <button class="btn btn-ghost" id="decline" disabled>이번에는 지원하지 않겠습니다</button>
      </div>
    </section></div>`;
  const refresh = () => {
    ss.auth = {name:$('#aName').value, birth:$('#aBirth').value, phone:$('#aPhone').value, email:$('#aEmail').value};
    const ok = !!authFilled(ss.auth);
    $('#authSec').classList.toggle('done', ok);
    $('#acceptSec').classList.toggle('locked', !ok);
    $('#accept').disabled = $('#decline').disabled = !ok;
    $('#aState').innerHTML = ok ? '<span class="pill ok">✓ 입력 완료 · 추천 수락을 진행하세요</span>' : '<span class="pill idle">네 항목을 모두 입력하세요</span>';
  };
  ['aName','aBirth','aPhone','aEmail'].forEach(id => $('#'+id).addEventListener('input', refresh));
  refresh();
  $('#accept').onclick = () => {
    raw.status = 'ACCEPT'; raw.studentInput = {...ss.auth}; save();
    ss.stage = t.parent ? 'parent' : 'form'; renderStudent(raw.token);
    toast('추천을 수락했습니다');
  };
  $('#decline').onclick = () => {
    if(!confirm('추천을 수락하지 않으면 이번 학기 지원이 종료됩니다. 계속할까요?')) return;
    raw.status = 'DECLINE'; save(); renderStudent(raw.token);
  };
}

/* 6-2 보호자 정보 입력 및 자녀 수락 동의 (유형 B·C·D)
   인증 서버가 없으므로 휴대전화 인증은 하지 않는다.
   보호자 성명·휴대전화를 입력하면 바로 자녀 수락 동의 단계가 열린다. (서버 연동 시 이 지점에서 인증) */
const parentFilled = p => p.name.trim() && normPhone(p.phone).length >= 10;
function stuParent(main, raw, rec, t, ss){
  main.innerHTML = `<div class="card fadein">
    <section class="sec" id="pSec">
      <div class="sec-h"><div class="num">01</div><div><h2>보호자 정보 입력</h2><p>보호자 성명과 휴대전화를 입력하면 아래 자녀 수락 동의 단계가 열립니다.</p></div></div>
      <div class="row">
        <label class="f"><span>보호자 성명<em>*</em></span><input type="text" id="pName" value="${esc(ss.parent.name)}"></label>
        <label class="f"><span>보호자 휴대전화<em>*</em></span><input type="tel" id="pPhone" value="${esc(ss.parent.phone)}" placeholder="010-0000-0000"></label>
      </div>
      <div class="verify" id="pState"></div>
    </section>
    <section class="sec locked" id="pAgreeSec">
      <div class="sec-h"><div class="num">02</div><div><h2>자녀 수락 동의</h2><p>동의하면 지원 화면이 열립니다.</p></div></div>
      <label class="check"><input type="checkbox" id="pAgree" ${ss.parent.agree?'checked':''}> 자녀 ${esc(rec.student.name)}의 장학생 추천 수락과 지원서·증빙서류 제출에 동의합니다.</label>
      <button class="btn btn-brick" id="pNext" style="margin-top:16px" disabled>동의하고 지원서 작성으로</button>
    </section></div>`;
  const refresh = () => {
    ss.parent.name = $('#pName').value; ss.parent.phone = $('#pPhone').value; ss.parent.agree = $('#pAgree').checked;
    const ok = !!parentFilled(ss.parent);
    $('#pSec').classList.toggle('done', ok);
    $('#pAgreeSec').classList.toggle('locked', !ok);
    $('#pAgreeSec').classList.toggle('done', ok && ss.parent.agree);
    $('#pNext').disabled = !(ok && ss.parent.agree);
    $('#pState').innerHTML = ok ? '<span class="pill ok">✓ 입력 완료 · 자녀 수락 동의를 진행하세요</span>' : '<span class="pill idle">보호자 성명과 휴대전화를 입력하세요</span>';
  };
  ['pName','pPhone'].forEach(id => $('#'+id).addEventListener('input', refresh));
  $('#pAgree').addEventListener('change', refresh);
  $('#pNext').onclick = () => { raw.parentInput = {name:ss.parent.name, phone:ss.parent.phone, agreedAt:today()}; save(); ss.stage='form'; renderStudent(raw.token); };
  refresh();
}

/* 6-3 맞춤형 폼 동적 로드 — 스키마 → DOM */
function fieldHTML(f, ss){
  const v = ss.data[f.id] ?? '';
  const req = f.req ? '<em>*</em>' : '';
  const hidden = f.showIf && ss.data[f.showIf[0]] !== f.showIf[1];
  if(hidden) return '';
  const help = f.help ? `<small>${f.help}</small>` : '';
  if(f.type === 'textarea') return `<label class="f full"><span>${f.label}${req}</span>${help}
      <textarea data-f="${f.id}" style="margin-top:6px">${esc(v)}</textarea>
      <div class="meter"><i data-meter="${f.id}"></i></div>
      <div class="counter"><span>공백 제외 ${f.min}자 이상</span><span class="n" data-count="${f.id}"></span></div></label>`;
  if(f.type === 'select') return `<label class="f"><span>${f.label}${req}</span>
      <select data-f="${f.id}"><option value="">선택</option>${f.options.map(o=>`<option ${v===o?'selected':''}>${o}</option>`).join('')}</select>${help}</label>`;
  if(f.type === 'seg') return `<div class="f"><span>${f.label}${req}</span><div class="segs" role="radiogroup" aria-label="${f.label}">
      ${f.options.map(o=>`<label class="seg"><input type="radio" name="sg-${f.id}" data-f="${f.id}" value="${o}" ${v===o?'checked':''}><span>${o}</span></label>`).join('')}</div>${help}</div>`;
  return `<label class="f"><span>${f.label}${req}</span><input type="${f.type==='tel'?'tel':'text'}" data-f="${f.id}" value="${esc(v)}" placeholder="${f.ph||''}">${help}</label>`;
}
function activeFields(t, ss){
  const fs = t.sections.flatMap(s => s.fields).filter(f => !f.showIf || ss.data[f.showIf[0]] === f.showIf[1]);
  if(t.reapply && ss.reapply) fs.push(REAPPLY_FIELD);
  return fs;
}
const fieldOk = (f, ss) => !f.req || (f.type==='textarea' ? charCount(ss.data[f.id]) >= f.min : String(ss.data[f.id]||'').trim() !== '');

function stuForm(main, raw, rec, t, ss){
  let n = 0; const num = () => String(++n).padStart(2,'0');
  main.innerHTML = `<form class="card fadein" id="stuForm" novalidate>
    ${t.recommender==='office' ? `<section class="sec"><div class="office">✓ 교회사무실에서 교역자 자녀임을 확인했습니다</div></section>` : ''}
    ${t.sections.map(s => `<section class="sec" data-sec>
      <div class="sec-h"><div class="num">${num()}</div><div><h2>${s.title}</h2><p>${s.hint}</p></div></div>
      <div class="row" data-fields='${JSON.stringify(s.fields.map(f=>f.id))}'>${s.fields.map(f => fieldHTML(f, ss)).join('')}</div>
    </section>`).join('')}
    ${t.reapply ? `<section class="sec" id="reSec">
      <div class="sec-h"><div class="num">${num()}</div><div><h2>재지원 여부</h2><p>직전 학기에 장학금을 받았다면 간증문 문항이 추가로 열립니다.</p></div></div>
      <div class="reapply"><label class="check"><input type="checkbox" id="reChk" ${ss.reapply?'checked':''}> 직전 학기에 정동제일교회 장학금을 받았습니다 (재지원)</label>
      <div id="reBox">${ss.reapply ? fieldHTML(REAPPLY_FIELD, ss) : ''}</div></div></section>` : ''}
    <section class="sec" data-sec>
      <div class="sec-h"><div class="num">${num()}</div><div><h2>증빙서류 업로드</h2><p>PDF·JPG·PNG, 파일당 10MB 이하. 하나라도 빠지면 최종 제출이 되지 않습니다.</p></div></div>
      <div class="docs">${t.docs.map((d,i) => `
        <div class="doc ${ss.files[d]?'ok':''}" data-doc="${i}">
          <div class="dn"><b>${d}</b><small>${ss.files[d] ? '✓ ' + esc(ss.files[d]) : '아직 올리지 않았습니다'}</small></div>
          <input type="file" id="file${i}" accept=".pdf,.jpg,.jpeg,.png">
          <label for="file${i}" class="btn btn-ghost btn-sm" tabindex="0">${ss.files[d]?'바꾸기':'파일 선택'}</label>
        </div>`).join('')}</div>
    </section>
    <section class="sec">
      <div style="display:flex;gap:10px;flex-wrap:wrap;align-items:center">
        <button type="button" class="btn btn-brick" id="finalSubmit" disabled>지원서 최종 제출</button>
        <span id="finalMsg" style="font-size:13px;color:var(--ink-3)"></span>
      </div>
      <ul class="blocker" id="stuBlocker"></ul>
    </section>
  </form>`;

  const form = $('#stuForm');
  const refreshConditional = () => {           // showIf 조건부 필드 재렌더
    $$('[data-fields]', form).forEach(row => {
      const ids = JSON.parse(row.dataset.fields);
      const fs = t.sections.flatMap(s=>s.fields).filter(f => ids.includes(f.id));
      if(fs.some(f => f.showIf)){ row.innerHTML = fs.map(f => fieldHTML(f, ss)).join(''); }
    });
    paintCounts(); 
  };
  const paintCounts = () => activeFields(t, ss).filter(f=>f.type==='textarea').forEach(f => {
    const c = $(`[data-count="${f.id}"]`, form), m = $(`[data-meter="${f.id}"]`, form); if(!c) return;
    const k = charCount(ss.data[f.id]); c.textContent = `${k} / ${f.min}자`; c.classList.toggle('ok', k>=f.min);
    m.style.width = Math.min(100, k/f.min*100)+'%'; m.classList.toggle('ok', k>=f.min);
  });
  form.addEventListener('input', e => {
    const id = e.target.dataset.f; if(!id) return;
    ss.data[id] = e.target.value;
    if(e.target.type === 'radio') refreshConditional(); else paintCounts();
    check();
  });
  form.addEventListener('change', e => {
    if(e.target.type === 'file'){
      const i = +e.target.id.replace('file',''); const d = t.docs[i]; const file = e.target.files[0]; if(!file) return;
      if(file.size > 10*1024*1024){ toast('10MB 이하 파일만 올릴 수 있습니다'); return; }
      ss.files[d] = file.name;
      const box = $(`[data-doc="${i}"]`, form); box.classList.add('ok');
      $('small', box).textContent = '✓ ' + file.name; $('label', box).textContent = '바꾸기';
      const allDocs = t.docs.every(x => ss.files[x]);
      if(allDocs && raw.status === 'ACCEPT'){ raw.status = 'DOCS'; save(); toast('모든 서류가 올라왔습니다 · 상태: 서류 제출 완료'); }
      check();
    }
  });
  $$('.doc label', form).forEach(l => l.addEventListener('keydown', e => { if(e.key==='Enter'||e.key===' '){ e.preventDefault(); $('#'+l.htmlFor).click(); } }));
  const reChk = $('#reChk');
  if(reChk) reChk.onchange = () => { ss.reapply = reChk.checked; $('#reBox').innerHTML = ss.reapply ? fieldHTML(REAPPLY_FIELD, ss) : ''; paintCounts(); check(); };

  // 실시간 서류 제출 확인 — 누락 시 제출 버튼 비활성
  function check(){
    const missF = activeFields(t, ss).filter(f => !fieldOk(f, ss));
    const missD = t.docs.filter(d => !ss.files[d]);
    const ok = !missF.length && !missD.length;
    $('#finalSubmit').disabled = !ok;
    $('#finalMsg').textContent = ok ? '모든 항목과 서류가 확인되었습니다.' : `미완료 ${missF.length + missD.length}건`;
    $('#stuBlocker').innerHTML = [...missF.map(f=>`<li>${f.label}${f.type==='textarea'?` (${charCount(ss.data[f.id])}/${f.min}자)`:''}</li>`), ...missD.map(d=>`<li>서류: ${d}</li>`)].join('');
  }
  $('#finalSubmit').onclick = () => {
    const seq = String(8 + DB.filter(r => r.app).length).padStart(4,'0');
    raw.app = {id:`APP-2026-${seq}`, receipt:`JD-2026-2-${seq}`, submittedAt:today(), type:t.code, data:{...ss.data}, files:{...ss.files}, reapply:ss.reapply};
    raw.status = 'DONE'; save(); ss.stage = 'done'; renderStudent(raw.token);
  };
  paintCounts(); check();
}

function stuDone(main, raw, rec, t){
  main.innerHTML = `<div class="card fadein" style="padding:36px 32px">
    <div class="eyebrow">최종 지원 완료</div>
    <h2 style="font-family:var(--display);font-size:26px;margin:8px 0 6px">지원서가 접수되었습니다</h2>
    <p style="color:var(--ink-2);margin:0">추천서와 지원서가 하나의 접수번호로 묶여 장학사업위원회 심사에 올라갑니다.${t.code==='A'?' 신학생(간사) 유형은 담당 목사 추천으로 승인에 준해 처리됩니다.':''}</p>
    <dl class="kv">
      <dt>통합 접수번호</dt><dd class="mono" style="font-size:16px;font-weight:500">${raw.app?.receipt||'—'}</dd>
      <dt>결합 내역</dt><dd class="mono">${raw.id} + ${raw.app?.id||''}</dd>
      <dt>장학 유형</dt><dd>유형 ${t.code} ${t.name}</dd>
      <dt>제출일</dt><dd>${raw.app?.submittedAt||''}</dd>
    </dl>
    <a class="btn btn-ghost" href="#board">진행 현황에서 확인</a></div>`;
}
function stuDeclined(main, raw){
  main.innerHTML = `<div class="card fadein" style="padding:36px 32px">
    <div class="eyebrow">지원 미수락</div>
    <h2 style="font-family:var(--display);font-size:24px;margin:8px 0 6px">이번 학기 추천을 수락하지 않았습니다</h2>
    <p style="color:var(--ink-2);margin:0 0 18px">마음이 바뀌었다면 장학사업위원회에 연락해 주세요. 추천해 주신 분께는 결과만 전달됩니다.</p>
    <button class="btn btn-ghost" id="undo">데모: 대기 상태로 되돌리기</button></div>`;
  $('#undo').onclick = () => { raw.status='WAIT'; save(); delete S[raw.token]; renderStudent(raw.token); };
}

route();
</script>
<script type="module" src="https://static.cloudflareinsights.com/beacon.min.js/v31edd6df95cf4e85bb4c19e7a9bdbcba1788362987495" integrity="sha512-iIg7k2xntmwu6/uSb5tpc/hySgZc4eoL31yB29W6tJFo2akwjPWcEqnCEdJvGexCL0KEQwVYv5BlowfhVz26hg==" data-cf-beacon='{"version":"2024.11.0","token":"4edd5f8ec12a48cfa682ab8261b80a79","spa":2}' crossorigin="anonymous"></script>
</body>
</html>
