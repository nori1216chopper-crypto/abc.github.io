[vr-homes.html](https://github.com/user-attachments/files/28376662/vr-homes.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VR Homes — VR内見不動産サイト</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg-primary:#ffffff; --bg-secondary:#f4f6f8; --bg-tertiary:#eef1f5;
  --text-primary:#0f1923; --text-secondary:#6b7685; --border:#e0e4ea;
  --blue:#185FA5; --blue-light:#E6F1FB; --blue-mid:#B5D4F4;
  --blue-dark:#0C447C; --blue-navy:#042C53;
  --green:#3B6D11; --green-light:#EAF3DE;
  --red:#A32D2D; --red-light:#FCEBEB; --red-border:#F09595;
  --gold:#A07000; --gold-light:#FFF8E1; --gold-border:#F0D070;
  --warn:#854F0B; --warn-light:#FDF3E3;
  --radius-sm:6px; --radius-md:8px; --radius-lg:12px;
}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Helvetica Neue',sans-serif;background:var(--bg-tertiary)}

/* ── Login gate ── */
#login-gate{position:fixed;inset:0;z-index:9999;background:var(--bg-tertiary);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 16px;overflow-y:auto}
#login-gate.hidden{display:none}

/* ── Tab bar ── */
.tab-bar{background:var(--bg-primary);border-bottom:1px solid var(--border);display:flex;overflow-x:auto;padding:0 12px;position:sticky;top:0;z-index:100}
.tab{padding:14px 14px 12px;font-size:12px;color:var(--text-secondary);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;display:flex;align-items:center;gap:5px;transition:color .15s}
.tab:hover{color:var(--text-primary)}
.tab.active{color:var(--blue);border-bottom-color:var(--blue);font-weight:500}
.tab.hidden{display:none!important}
.screen{display:none}.screen.active{display:block}

/* ── Nav ── */
.nav{background:var(--bg-primary);border-bottom:1px solid var(--border);padding:0 24px;height:56px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:48px;z-index:90}
.logo{display:flex;align-items:center;gap:8px;font-size:16px;font-weight:500;color:var(--text-primary);cursor:pointer}
.logo-icon{width:32px;height:32px;background:var(--blue-light);border-radius:8px;display:flex;align-items:center;justify-content:center;color:var(--blue);font-size:16px}
.nav-links{display:flex;gap:24px}
.nl{font-size:13px;color:var(--text-secondary);cursor:pointer;padding:2px 0;border-bottom:2px solid transparent;transition:color .15s}
.nl:hover,.nl.on{color:var(--blue);border-bottom-color:var(--blue)}
.nav-r{display:flex;gap:8px}

/* ── Buttons ── */
.btn{font-size:13px;padding:7px 16px;border-radius:var(--radius-md);cursor:pointer;font-family:inherit;font-weight:500;border:1px solid var(--border);background:transparent;color:var(--text-primary);transition:all .15s;display:inline-flex;align-items:center;gap:5px}
.btn:hover{background:var(--bg-secondary)}
.btn-p{background:var(--blue);color:#fff;border-color:var(--blue)}
.btn-p:hover{background:var(--blue-dark)}
.btn-sm{font-size:11px;padding:5px 11px}
.btn-gold{background:var(--gold-light);color:var(--gold);border-color:var(--gold-border)}
.btn-gold:hover{background:#fff3c0}

/* ── Tags ── */
.tag{display:inline-flex;align-items:center;gap:3px;font-size:10px;padding:2px 7px;border-radius:4px;font-weight:500}
.tb{background:var(--blue-light);color:var(--blue)}
.tg{background:var(--green-light);color:var(--green)}
.tgr{background:var(--bg-secondary);color:var(--text-secondary)}
.tr{background:var(--red-light);color:var(--red)}
.tgold{background:var(--gold-light);color:var(--gold)}
.tmaster{background:#1a1a2e;color:#e0c97a}

/* ── Form fields ── */
.field{margin-bottom:16px}
.flabel{font-size:12px;font-weight:500;color:var(--text-secondary);margin-bottom:5px;display:flex;align-items:center;gap:4px}
.req{color:var(--red);font-size:11px}
.finput{width:100%;font-size:13px;padding:9px 12px;border-radius:var(--radius-md);border:1px solid var(--border);background:var(--bg-primary);color:var(--text-primary);font-family:inherit;transition:border-color .15s}
.finput:focus{outline:none;border-color:var(--blue);box-shadow:0 0 0 3px var(--blue-light)}

/* ── Card ── */
.card{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);padding:24px}

/* ── Property card ── */
.prop-card{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);overflow:hidden;cursor:pointer;transition:border-color .15s,box-shadow .15s}
.prop-card:hover{border-color:var(--blue-mid);box-shadow:0 2px 12px rgba(24,95,165,.08)}
.prop-img{height:110px;background:#dbe8f4;display:flex;align-items:center;justify-content:center;position:relative}
.fav-btn{position:absolute;top:8px;right:8px;width:28px;height:28px;background:var(--bg-primary);border:1px solid var(--border);border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;color:var(--text-secondary);font-size:13px;transition:all .15s}
.fav-btn.on{color:var(--red);border-color:var(--red-border)}

/* ── Auth styles ── */
.pass-wrap{position:relative}
.pass-wrap .finput{padding-right:40px}
.eye-btn{position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;color:var(--text-secondary);font-size:16px;padding:0;display:flex;align-items:center}
.str-bar{display:flex;gap:3px;margin-top:6px}
.str-seg{flex:1;height:3px;border-radius:2px;background:var(--border)}
.str-seg.weak{background:var(--red)}.str-seg.mid{background:#BA7517}.str-seg.strong{background:var(--green)}

/* ── TOP ── */
.hero{background:var(--blue-light);padding:32px 24px}
.hero-eyebrow{font-size:11px;font-weight:500;color:var(--blue);letter-spacing:.07em;text-transform:uppercase;margin-bottom:6px}
.hero-title{font-size:22px;font-weight:500;color:var(--blue-navy);line-height:1.4;margin-bottom:16px}
.search-bar{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);padding:14px 16px}
.search-row{display:flex;gap:10px;align-items:flex-end;flex-wrap:wrap}
.search-field{display:flex;flex-direction:column;gap:4px;flex:1;min-width:100px}
.search-label{font-size:11px;color:var(--text-secondary);font-weight:500}
.results-bar{padding:12px 24px;background:var(--bg-primary);border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px}
.card-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:14px;padding:20px 24px}
.prop-body{padding:10px 12px}
.prop-price{font-size:15px;font-weight:500;color:var(--blue-navy);margin-bottom:2px}
.prop-name{font-size:13px;color:var(--text-primary);margin-bottom:3px}
.prop-loc{font-size:11px;color:var(--text-secondary);display:flex;align-items:center;gap:3px;margin-bottom:7px}
.prop-tags{display:flex;gap:4px;flex-wrap:wrap}
.prop-footer{padding:8px 12px;border-top:1px solid var(--border);display:flex;justify-content:space-between;align-items:center}
.prop-area{font-size:11px;color:var(--text-secondary)}
.pagination{display:flex;justify-content:center;gap:4px;padding:16px 24px 28px}
.page-btn{width:34px;height:34px;border-radius:var(--radius-md);border:1px solid var(--border);background:transparent;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:13px;color:var(--text-secondary);transition:all .15s}
.page-btn.on{background:var(--blue);color:#fff;border-color:var(--blue)}
.page-btn:hover:not(.on){background:var(--bg-secondary)}

/* ── MAP ── */
.map-wrap{display:flex;height:calc(100vh - 104px)}
.map-sidebar{width:220px;flex-shrink:0;background:var(--bg-primary);border-right:1px solid var(--border);overflow-y:auto;padding:14px}
.map-area{flex:1;background:linear-gradient(135deg,#cfe0ea,#d8eaf3 50%,#c8dae6);position:relative;overflow:hidden}
.map-canvas{position:relative;width:100%;height:100%}
.pin{position:absolute;cursor:pointer}
.pin-circle{width:30px;height:30px;background:var(--blue);border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:11px;font-weight:500;border:2px solid #fff;box-shadow:0 2px 8px rgba(0,0,0,.2);transition:transform .15s}
.pin-circle:hover{transform:scale(1.1)}
.pin-popup{display:none;position:absolute;bottom:38px;left:50%;transform:translateX(-50%);background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);padding:12px 14px;min-width:170px;box-shadow:0 4px 16px rgba(0,0,0,.12);z-index:10}
.pin-popup.show{display:block}
.result-item{background:var(--bg-secondary);border-radius:var(--radius-md);padding:10px;margin-bottom:8px;cursor:pointer;border:1px solid transparent;transition:border-color .15s}
.result-item:hover,.result-item.on{border-color:var(--blue-mid);background:var(--blue-light)}

/* ── MYPAGE ── */
.mypage-wrap{display:flex;min-height:calc(100vh - 104px)}
.mypage-sidebar{width:200px;flex-shrink:0;background:var(--bg-primary);border-right:1px solid var(--border);padding:24px 16px}
.mypage-main{flex:1;padding:24px}
.avatar{width:56px;height:56px;border-radius:50%;background:var(--blue-light);display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:500;color:var(--blue);margin:0 auto 10px}
.mp-nav-item{display:flex;align-items:center;gap:7px;padding:9px 10px;border-radius:var(--radius-md);cursor:pointer;font-size:13px;color:var(--text-secondary);margin-bottom:4px;transition:all .15s}
.mp-nav-item:hover{background:var(--bg-secondary)}
.mp-nav-item.on{background:var(--blue-light);color:var(--blue);font-weight:500}
.badge{margin-left:auto;background:var(--blue);color:#fff;border-radius:10px;padding:1px 7px;font-size:10px}
.prop-list-item{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);display:flex;align-items:center;gap:14px;padding:14px;margin-bottom:10px;transition:border-color .15s}
.prop-list-item:hover{border-color:var(--blue-mid)}
.prop-thumb{width:72px;height:56px;background:#dbe8f4;border-radius:var(--radius-md);flex-shrink:0;display:flex;align-items:center;justify-content:center;color:#85B7EB;font-size:22px}
.hist-item{display:flex;align-items:center;justify-content:space-between;padding:11px 14px;border-bottom:1px solid var(--border);font-size:13px}
.hist-item:last-child{border-bottom:none}

/* ── ADMIN ── */
.admin-wrap{display:flex;min-height:calc(100vh - 104px)}
.admin-sidebar{width:180px;flex-shrink:0;background:var(--bg-primary);border-right:1px solid var(--border);padding:20px 14px}
.admin-main{flex:1;padding:20px 24px;overflow-y:auto}
.admin-nav-item{display:flex;align-items:center;gap:7px;padding:8px 10px;border-radius:var(--radius-md);cursor:pointer;font-size:13px;color:var(--text-secondary);margin-bottom:4px;transition:all .15s}
.admin-nav-item:hover{background:var(--bg-secondary)}
.admin-nav-item.on{background:var(--blue-light);color:var(--blue);font-weight:500}
.stat-mini{background:var(--bg-secondary);border-radius:var(--radius-md);padding:10px;margin-bottom:8px}
.stat-mini-label{font-size:10px;color:var(--text-secondary);margin-bottom:3px}
.stat-mini-val{font-size:20px;font-weight:500;color:var(--text-primary)}
.admin-table-wrap{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);overflow:hidden}
.admin-table-head{background:var(--bg-secondary);padding:9px 14px;font-size:11px;font-weight:500;color:var(--text-secondary);display:grid;gap:0}
.admin-table-row{padding:10px 14px;font-size:12px;border-top:1px solid var(--border);display:grid;gap:0;align-items:center;transition:background .1s}
.admin-table-row:hover{background:var(--bg-secondary)}
.stat-card-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:16px}
.stat-card{background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px}
.stat-card-label{font-size:11px;color:var(--text-secondary);margin-bottom:6px}
.stat-card-val{font-size:26px;font-weight:500;color:var(--text-primary)}
.bar-track{flex:2;background:var(--bg-secondary);border-radius:3px;height:8px;overflow:hidden}
.bar-fill{height:100%;background:var(--blue);border-radius:3px}
.add-form{background:var(--bg-secondary);border:1px solid #B5D4F4;border-radius:var(--radius-lg);padding:16px;margin-bottom:16px;display:none}
.add-form-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}

/* ── MASTER ── */
.master-nav{background:#1a1a2e;border-bottom:1px solid #2d2d4e}
.master-badge{display:inline-flex;align-items:center;gap:5px;background:#e0c97a22;border:1px solid #e0c97a44;color:#e0c97a;border-radius:20px;padding:3px 10px;font-size:11px;font-weight:500}
</style>
</head>
<body>

<!-- ══════ LOGIN GATE ══════ -->
<div id="login-gate">
  <div style="position:fixed;inset:0;pointer-events:none;overflow:hidden;z-index:0">
    <div style="position:absolute;top:-120px;right:-80px;width:420px;height:420px;border-radius:50%;background:radial-gradient(circle,var(--blue-light) 0%,transparent 70%);opacity:.6"></div>
    <div style="position:absolute;bottom:-100px;left:-60px;width:320px;height:320px;border-radius:50%;background:radial-gradient(circle,var(--blue-mid) 0%,transparent 70%);opacity:.3"></div>
  </div>
  <div style="position:relative;z-index:1;width:100%;max-width:420px">
    <div style="text-align:center;margin-bottom:32px">
      <div style="width:64px;height:64px;background:var(--blue);border-radius:18px;display:flex;align-items:center;justify-content:center;margin:0 auto 14px;box-shadow:0 8px 24px rgba(24,95,165,.3)">
        <i class="ti ti-building" style="font-size:30px;color:#fff"></i>
      </div>
      <div style="font-size:26px;font-weight:600;color:var(--blue-navy);letter-spacing:-.5px">VR Homes</div>
      <div style="font-size:14px;color:var(--text-secondary);margin-top:5px">VR内見不動産サービス</div>
    </div>
    <div style="background:var(--bg-primary);border:1px solid var(--border);border-radius:16px;padding:28px;box-shadow:0 4px 32px rgba(0,0,0,.07)">
      <div style="background:var(--blue-light);border:1px solid var(--blue-mid);border-radius:var(--radius-md);padding:10px 14px;font-size:12px;color:var(--blue);margin-bottom:20px;display:flex;align-items:flex-start;gap:8px">
        <i class="ti ti-info-circle" style="flex-shrink:0;margin-top:1px"></i>
        <span>デモ用：<strong>demo@vrhomes.jp</strong> ／ <strong>demo1234</strong></span>
      </div>
      <div style="display:flex;border:1px solid var(--border);border-radius:var(--radius-md);overflow:hidden;margin-bottom:22px">
        <button id="gatab-login" onclick="switchGateAuth('login')" style="flex:1;padding:10px;font-size:13px;font-weight:500;cursor:pointer;font-family:inherit;border:none;background:var(--blue);color:#fff;transition:all .15s">ログイン</button>
        <button id="gatab-reg" onclick="switchGateAuth('reg')" style="flex:1;padding:10px;font-size:13px;font-weight:500;cursor:pointer;font-family:inherit;border:none;background:transparent;color:var(--text-secondary);transition:all .15s">新規登録</button>
      </div>
      <div id="gate-msg" style="display:none;border-radius:var(--radius-md);padding:10px 14px;font-size:13px;margin-bottom:14px;text-align:center"></div>
      <div id="gate-form">
        <div class="field"><div class="flabel">メールアドレス</div><input class="finput" id="g-email" type="text" placeholder="example@email.com"></div>
        <div class="field" style="margin-bottom:6px"><div class="flabel">パスワード</div>
          <div class="pass-wrap"><input class="finput" id="g-pass" type="password" placeholder="••••••••">
          <button class="eye-btn" id="g-eye" type="button" onclick="toggleGateEye()"><i class="ti ti-eye"></i></button></div>
        </div>
        <div style="text-align:right;font-size:11px;color:var(--blue);cursor:pointer;margin-bottom:20px">パスワードをお忘れですか？</div>
        <button class="btn btn-p" type="button" onclick="gateLogin()" style="width:100%;padding:12px;font-size:14px;justify-content:center;border-radius:var(--radius-md)">
          ログイン <i class="ti ti-arrow-right"></i>
        </button>
      </div>
      <div style="text-align:center;font-size:13px;color:var(--text-secondary);margin-top:18px" id="gate-switch-hint">
        アカウントをお持ちでない方は <a style="color:var(--blue);cursor:pointer;font-weight:500" onclick="switchGateAuth('reg')">新規登録</a>
      </div>
    </div>
    <div style="text-align:center;margin-top:20px;font-size:11px;color:var(--text-secondary)">© 2025 VR Homes. All rights reserved.</div>
  </div>
</div>

<!-- TAB BAR -->
<div class="tab-bar">
  <div class="tab active" id="tab-top" onclick="guardedScreen('top')"><i class="ti ti-home"></i>トップ</div>
  <div class="tab" id="tab-map" onclick="guardedScreen('map')"><i class="ti ti-map-pin"></i>マップ</div>
  <div class="tab" id="tab-mypage" onclick="guardedScreen('mypage')"><i class="ti ti-user"></i>マイページ</div>
  <div class="tab hidden" id="tab-admin" onclick="guardedScreen('admin')"><i class="ti ti-settings"></i>管理者</div>
  <div class="tab hidden" id="tab-master" onclick="guardedScreen('master')"><i class="ti ti-crown"></i>マスター</div>
</div>

<!-- ══════ TOP ══════ -->
<div class="screen active" id="s-top">
  <nav class="nav">
    <div class="logo"><div class="logo-icon"><i class="ti ti-building"></i></div>VR Homes</div>
    <div class="nav-links">
      <span class="nl on">物件を探す</span>
      <span class="nl" onclick="guardedScreen('map')">マップで探す</span>
    </div>
    <div class="nav-r">
      <button class="btn btn-sm" onclick="guardedScreen('mypage')"><i class="ti ti-user"></i>マイページ</button>
      <button class="btn btn-p btn-sm hidden" id="nav-admin-btn" onclick="guardedScreen('admin')"><i class="ti ti-settings"></i>管理者</button>
    </div>
  </nav>
  <div class="hero">
    <div class="hero-eyebrow">VR対応物件 掲載中</div>
    <div class="hero-title">自宅にいながら、360°内見できる<br>物件を探そう</div>
    <div class="search-bar">
      <div class="search-row">
        <div class="search-field"><span class="search-label">エリア</span>
          <select class="finput" style="padding:7px 10px;font-size:13px"><option>都道府県を選択</option><option>東京都</option><option>神奈川県</option><option>大阪府</option><option>愛知県</option></select>
        </div>
        <div class="search-field"><span class="search-label">家賃上限</span>
          <select class="finput" style="padding:7px 10px;font-size:13px"><option>上限なし</option><option>〜5万円</option><option>〜8万円</option><option>〜10万円</option><option>〜15万円</option></select>
        </div>
        <div class="search-field"><span class="search-label">間取り</span>
          <select class="finput" style="padding:7px 10px;font-size:13px"><option>指定なし</option><option>1K / 1DK</option><option>1LDK</option><option>2LDK</option><option>3LDK〜</option></select>
        </div>
        <button class="btn btn-p" style="padding:8px 20px" onclick="this.textContent='検索中…';setTimeout(()=>this.innerHTML='<i class=\"ti ti-search\"></i> 検索',600)">
          <i class="ti ti-search"></i> 検索
        </button>
      </div>
    </div>
  </div>
  <div class="results-bar">
    <span style="font-size:13px;color:var(--text-secondary)"><strong style="color:var(--text-primary)">6</strong> 件の物件</span>
    <div style="display:flex;gap:8px;align-items:center">
      <button class="btn btn-sm" onclick="guardedScreen('map')" style="background:var(--blue-light);color:var(--blue);border-color:var(--blue-mid)"><i class="ti ti-map-pin"></i>マップで見る</button>
      <select class="finput" style="padding:5px 9px;font-size:12px;width:auto"><option>新着順</option><option>家賃が安い順</option><option>家賃が高い順</option><option>面積が広い順</option></select>
    </div>
  </div>
  <div class="card-grid" id="card-grid"></div>
  <div class="pagination">
    <button class="page-btn"><i class="ti ti-chevron-left" style="font-size:13px"></i></button>
    <button class="page-btn on">1</button><button class="page-btn">2</button><button class="page-btn">3</button>
    <button class="page-btn" style="width:auto;padding:0 8px;font-size:12px">...</button>
    <button class="page-btn">8</button>
    <button class="page-btn"><i class="ti ti-chevron-right" style="font-size:13px"></i></button>
  </div>
</div>

<!-- ══════ MAP ══════ -->
<div class="screen" id="s-map">
  <nav class="nav">
    <div class="logo"><div class="logo-icon"><i class="ti ti-building"></i></div>VR Homes</div>
    <div class="nav-links"><span class="nl" onclick="guardedScreen('top')">← 一覧</span><span class="nl on">マップ</span></div>
    <div class="nav-r"><button class="btn btn-sm" onclick="guardedScreen('mypage')"><i class="ti ti-user"></i>マイページ</button></div>
  </nav>
  <div class="map-wrap">
    <div class="map-sidebar">
      <div style="font-size:12px;font-weight:500;margin-bottom:10px">絞り込み</div>
      <div class="field"><div class="flabel">家賃上限</div><select class="finput" style="padding:7px 9px;font-size:12px"><option>〜10万円</option><option>〜8万円</option><option>〜6万円</option></select></div>
      <div class="field"><div class="flabel">間取り</div><select class="finput" style="padding:7px 9px;font-size:12px"><option>指定なし</option><option>1K</option><option>1LDK</option><option>2LDK</option></select></div>
      <label style="display:flex;align-items:center;gap:6px;font-size:12px;color:var(--text-secondary);margin-bottom:14px;cursor:pointer">
        <input type="checkbox" checked style="accent-color:var(--blue)"> VR対応のみ
      </label>
      <button class="btn btn-p" style="width:100%;padding:7px;font-size:12px;justify-content:center;margin-bottom:18px">適用</button>
      <div style="font-size:12px;font-weight:500;margin-bottom:8px">検索結果 <span style="font-weight:400;color:var(--text-secondary)">3件</span></div>
      <div class="result-item on"><div style="font-size:12px;font-weight:500">コート渋谷</div><div style="font-size:11px;color:var(--text-secondary);margin:2px 0">¥92,000 / 2LDK</div><span class="tag tb" style="font-size:9px">VR対応</span></div>
      <div class="result-item"><div style="font-size:12px;font-weight:500">グランツ新宿</div><div style="font-size:11px;color:var(--text-secondary);margin:2px 0">¥68,000 / 1LDK</div><span class="tag tb" style="font-size:9px">VR対応</span></div>
      <div class="result-item"><div style="font-size:12px;font-weight:500">ソレイユ目黒</div><div style="font-size:11px;color:var(--text-secondary);margin:2px 0">¥115,000 / 3LDK</div><span class="tag tb" style="font-size:9px">VR対応</span></div>
    </div>
    <div class="map-area">
      <div class="map-canvas">
        <svg style="position:absolute;inset:0;width:100%;height:100%;opacity:.15" xmlns="http://www.w3.org/2000/svg">
          <defs><pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse"><path d="M 40 0 L 0 0 0 40" fill="none" stroke="#185FA5" stroke-width="0.5"/></pattern></defs>
          <rect width="100%" height="100%" fill="url(#grid)"/>
        </svg>
        <svg style="position:absolute;inset:0;width:100%;height:100%;opacity:.2" xmlns="http://www.w3.org/2000/svg">
          <line x1="0" y1="40%" x2="100%" y2="40%" stroke="#185FA5" stroke-width="3"/>
          <line x1="0" y1="65%" x2="100%" y2="65%" stroke="#185FA5" stroke-width="2"/>
          <line x1="35%" y1="0" x2="35%" y2="100%" stroke="#185FA5" stroke-width="3"/>
          <line x1="60%" y1="0" x2="60%" y2="100%" stroke="#185FA5" stroke-width="2"/>
        </svg>
        <div class="pin" style="top:32%;left:36%" onclick="togglePin('pa')">
          <div class="pin-circle">A</div>
          <div class="pin-popup" id="pa">
            <div style="font-size:13px;font-weight:500;margin-bottom:3px">コート渋谷</div>
            <div style="font-size:11px;color:var(--text-secondary);margin-bottom:7px">¥92,000 / 2LDK / 48㎡</div>
            <span class="tag tb" style="font-size:9px;display:inline-flex;margin-bottom:8px">VR対応</span>
            <div><button class="btn btn-sm" style="font-size:11px" onclick="document.getElementById('pa').classList.remove('show')">閉じる</button></div>
          </div>
        </div>
        <div class="pin" style="top:22%;left:55%" onclick="togglePin('pb')">
          <div class="pin-circle">B</div>
          <div class="pin-popup" id="pb">
            <div style="font-size:13px;font-weight:500;margin-bottom:3px">グランツ新宿</div>
            <div style="font-size:11px;color:var(--text-secondary);margin-bottom:7px">¥68,000 / 1LDK / 33㎡</div>
            <span class="tag tb" style="font-size:9px;display:inline-flex;margin-bottom:8px">VR対応</span>
            <div><button class="btn btn-sm" style="font-size:11px" onclick="document.getElementById('pb').classList.remove('show')">閉じる</button></div>
          </div>
        </div>
        <div class="pin" style="top:50%;left:46%" onclick="togglePin('pc')">
          <div class="pin-circle">C</div>
          <div class="pin-popup" id="pc">
            <div style="font-size:13px;font-weight:500;margin-bottom:3px">ソレイユ目黒</div>
            <div style="font-size:11px;color:var(--text-secondary);margin-bottom:7px">¥115,000 / 3LDK / 62㎡</div>
            <span class="tag tb" style="font-size:9px;display:inline-flex;margin-bottom:8px">VR対応</span>
            <div><button class="btn btn-sm" style="font-size:11px" onclick="document.getElementById('pc').classList.remove('show')">閉じる</button></div>
          </div>
        </div>
        <div style="position:absolute;bottom:12px;right:12px;background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-md);padding:7px 12px;font-size:11px;color:var(--text-secondary)">
          <i class="ti ti-info-circle"></i> ピンをクリックで物件情報を表示
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════ MYPAGE ══════ -->
<div class="screen" id="s-mypage">
  <nav class="nav">
    <div class="logo"><div class="logo-icon"><i class="ti ti-building"></i></div>VR Homes</div>
    <div class="nav-r">
      <button class="btn btn-sm" onclick="guardedScreen('top')"><i class="ti ti-home"></i>トップ</button>
      <button class="btn btn-sm" onclick="doLogout()">ログアウト</button>
    </div>
  </nav>
  <div class="mypage-wrap">
    <div class="mypage-sidebar">
      <div style="text-align:center;margin-bottom:24px">
        <div class="avatar" id="mp-avatar">U</div>
        <div style="font-size:14px;font-weight:500;color:var(--text-primary)" id="mp-name">ユーザー</div>
        <div style="font-size:11px;color:var(--text-secondary);margin-top:3px" id="mp-email">-</div>
        <div style="margin-top:6px" id="mp-role-badge"></div>
      </div>
      <div class="mp-nav-item on" onclick="switchMp('fav',this)"><i class="ti ti-heart"></i>お気に入り<span class="badge">2</span></div>
      <div class="mp-nav-item" onclick="switchMp('hist',this)"><i class="ti ti-history"></i>閲覧履歴</div>
      <div class="mp-nav-item" onclick="switchMp('prof',this)"><i class="ti ti-settings"></i>プロフィール</div>
      <!-- コード入力タブ（一般ユーザー・管理者のみ表示） -->
      <div class="mp-nav-item hidden" id="mp-nav-code" onclick="switchMp('code',this)"><i class="ti ti-key"></i>コード入力</div>
    </div>
    <div class="mypage-main">
      <div id="mp-fav">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">お気に入り物件</h2>
        <div class="prop-list-item">
          <div class="prop-thumb"><i class="ti ti-building"></i></div>
          <div style="flex:1">
            <div style="font-size:14px;font-weight:500;margin-bottom:3px">コート渋谷</div>
            <div style="font-size:12px;color:var(--text-secondary);margin-bottom:6px">渋谷区 ／ ¥92,000 ／ 2LDK ／ 48㎡</div>
            <div style="display:flex;gap:5px"><span class="tag tb" style="font-size:10px">VR対応</span><span class="tag tg" style="font-size:10px">ペット可</span></div>
          </div>
          <button class="btn btn-sm" style="color:var(--red);border-color:var(--red-border)">削除</button>
        </div>
        <div class="prop-list-item">
          <div class="prop-thumb"><i class="ti ti-building"></i></div>
          <div style="flex:1">
            <div style="font-size:14px;font-weight:500;margin-bottom:3px">ソレイユ目黒</div>
            <div style="font-size:12px;color:var(--text-secondary);margin-bottom:6px">目黒区 ／ ¥115,000 ／ 3LDK ／ 62㎡</div>
            <div style="display:flex;gap:5px"><span class="tag tb" style="font-size:10px">VR対応</span><span class="tag tgr" style="font-size:10px">南向き</span></div>
          </div>
          <button class="btn btn-sm" style="color:var(--red);border-color:var(--red-border)">削除</button>
        </div>
      </div>
      <div id="mp-hist" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">閲覧履歴</h2>
        <div style="background:var(--bg-primary);border:1px solid var(--border);border-radius:var(--radius-lg);overflow:hidden">
          <div class="hist-item"><div><div style="font-size:13px;font-weight:500;margin-bottom:2px">コート渋谷</div><div style="font-size:11px;color:var(--text-secondary)">渋谷区 / 2LDK</div></div><div style="font-size:11px;color:var(--text-secondary)">1時間前</div></div>
          <div class="hist-item"><div><div style="font-size:13px;font-weight:500;margin-bottom:2px">グランツ新宿</div><div style="font-size:11px;color:var(--text-secondary)">新宿区 / 1LDK</div></div><div style="font-size:11px;color:var(--text-secondary)">昨日</div></div>
          <div class="hist-item"><div><div style="font-size:13px;font-weight:500;margin-bottom:2px">ソレイユ目黒</div><div style="font-size:11px;color:var(--text-secondary)">目黒区 / 3LDK</div></div><div style="font-size:11px;color:var(--text-secondary)">3日前</div></div>
        </div>
      </div>
      <div id="mp-prof" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">プロフィール設定</h2>
        <div class="card" style="max-width:480px">
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px">
            <div class="field"><div class="flabel">姓</div><input class="finput" id="prof-sei" value="田中"></div>
            <div class="field"><div class="flabel">名</div><input class="finput" id="prof-mei" value="太郎"></div>
          </div>
          <div class="field"><div class="flabel">メールアドレス</div><input class="finput" id="prof-email" value=""></div>
          <div class="field"><div class="flabel">電話番号</div><input class="finput" value="090-0000-0000"></div>
          <div class="field"><div class="flabel">都道府県</div><select class="finput"><option>東京都</option><option>神奈川県</option><option>大阪府</option></select></div>
          <div style="display:flex;gap:10px">
            <button class="btn btn-p" style="padding:9px 22px;font-size:13px">変更を保存</button>
            <button class="btn" style="padding:9px 22px;font-size:13px;color:var(--red)">アカウント削除</button>
          </div>
        </div>
      </div>
      <!-- コード入力パネル -->
      <div id="mp-code" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:8px;color:var(--text-primary)">コード入力</h2>
        <p style="font-size:13px;color:var(--text-secondary);margin-bottom:20px">管理者用コードを入力すると、管理者機能が利用できるようになります。</p>
        <div class="card" style="max-width:360px">
          <div class="field">
            <div class="flabel">コード <span class="req">*</span></div>
            <input class="finput" id="code-input" type="password" placeholder="コードを入力" style="letter-spacing:.2em;font-size:16px">
          </div>
          <div id="code-msg" style="display:none;border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px"></div>
          <button class="btn btn-p" onclick="submitCode()" style="width:100%;padding:10px;justify-content:center;font-size:13px">
            <i class="ti ti-check"></i> 認証する
          </button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════ ADMIN ══════ -->
<div class="screen" id="s-admin">
  <nav class="nav" style="background:#042C53;border-bottom-color:#0C447C">
    <div class="logo" style="color:#fff"><div style="width:32px;height:32px;background:rgba(255,255,255,.15);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px"><i class="ti ti-settings"></i></div>管理者パネル</div>
    <div style="display:flex;align-items:center;gap:10px">
      <span style="font-size:12px;color:var(--blue-mid)" id="admin-email-display">-</span>
      <button class="btn btn-sm" onclick="doLogout()" style="border-color:rgba(255,255,255,.2);color:#fff">ログアウト</button>
    </div>
  </nav>
  <div class="admin-wrap">
    <div class="admin-sidebar">
      <div style="font-size:10px;font-weight:500;color:var(--text-secondary);letter-spacing:.06em;margin-bottom:10px">MENU</div>
      <div class="admin-nav-item on" onclick="switchAdmin('props',this)"><i class="ti ti-building"></i>物件管理</div>
      <div class="admin-nav-item" onclick="switchAdmin('users',this)"><i class="ti ti-users"></i>ユーザー管理</div>
      <div class="admin-nav-item" onclick="switchAdmin('stats',this)"><i class="ti ti-chart-bar"></i>アクセス分析</div>
      <div style="margin-top:20px;padding-top:16px;border-top:1px solid var(--border)">
        <div class="stat-mini"><div class="stat-mini-label">物件数</div><div class="stat-mini-val">24</div></div>
        <div class="stat-mini"><div class="stat-mini-label">ユーザー数</div><div class="stat-mini-val" id="admin-user-count">-</div></div>
        <div class="stat-mini"><div class="stat-mini-label">今月の問い合わせ</div><div class="stat-mini-val">348</div></div>
      </div>
    </div>
    <div class="admin-main">
      <div id="admin-props">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px">
          <h2 style="font-size:16px;font-weight:500;color:var(--text-primary)">物件管理</h2>
          <button class="btn btn-p btn-sm" onclick="toggleAddForm()"><i class="ti ti-plus"></i>物件を追加</button>
        </div>
        <div class="add-form" id="add-form">
          <div style="font-size:14px;font-weight:500;margin-bottom:14px;color:var(--text-primary)">新規物件登録</div>
          <div class="add-form-grid">
            <div class="field"><div class="flabel">物件名 <span class="req">*</span></div><input class="finput" placeholder="例：コート渋谷" id="af-name"></div>
            <div class="field"><div class="flabel">エリア <span class="req">*</span></div><input class="finput" placeholder="渋谷区" id="af-area"></div>
            <div class="field"><div class="flabel">家賃 (円) <span class="req">*</span></div><input class="finput" type="number" placeholder="92000" id="af-rent"></div>
            <div class="field"><div class="flabel">間取り <span class="req">*</span></div><select class="finput" id="af-madori"><option>1K</option><option>1DK</option><option>1LDK</option><option>2LDK</option><option>3LDK</option></select></div>
            <div class="field"><div class="flabel">面積 (㎡)</div><input class="finput" type="number" placeholder="48"></div>
            <div class="field"><div class="flabel">最寄り駅</div><input class="finput" placeholder="渋谷駅 徒歩3分"></div>
          </div>
          <div style="display:flex;gap:8px;justify-content:flex-end">
            <button class="btn btn-sm" onclick="toggleAddForm()">キャンセル</button>
            <button class="btn btn-p btn-sm" onclick="addProperty()">登録する</button>
          </div>
        </div>
        <div class="admin-table-wrap">
          <div class="admin-table-head" style="grid-template-columns:2fr 1fr 1fr 90px"><span>物件名</span><span>エリア</span><span>家賃</span><span>操作</span></div>
          <div id="prop-table-body">
            <div class="admin-table-row" style="grid-template-columns:2fr 1fr 1fr 90px"><span style="font-weight:500">コート渋谷</span><span style="color:var(--text-secondary)">渋谷区</span><span>¥92,000</span><span style="display:flex;gap:5px"><button class="btn btn-sm" style="font-size:10px;padding:3px 8px"><i class="ti ti-edit"></i></button><button class="btn btn-sm" style="font-size:10px;padding:3px 8px;color:var(--red);border-color:var(--red-border)" onclick="this.closest('.admin-table-row').remove()"><i class="ti ti-trash"></i></button></span></div>
            <div class="admin-table-row" style="grid-template-columns:2fr 1fr 1fr 90px"><span style="font-weight:500">グランツ新宿</span><span style="color:var(--text-secondary)">新宿区</span><span>¥68,000</span><span style="display:flex;gap:5px"><button class="btn btn-sm" style="font-size:10px;padding:3px 8px"><i class="ti ti-edit"></i></button><button class="btn btn-sm" style="font-size:10px;padding:3px 8px;color:var(--red);border-color:var(--red-border)" onclick="this.closest('.admin-table-row').remove()"><i class="ti ti-trash"></i></button></span></div>
            <div class="admin-table-row" style="grid-template-columns:2fr 1fr 1fr 90px"><span style="font-weight:500">ソレイユ目黒</span><span style="color:var(--text-secondary)">目黒区</span><span>¥115,000</span><span style="display:flex;gap:5px"><button class="btn btn-sm" style="font-size:10px;padding:3px 8px"><i class="ti ti-edit"></i></button><button class="btn btn-sm" style="font-size:10px;padding:3px 8px;color:var(--red);border-color:var(--red-border)" onclick="this.closest('.admin-table-row').remove()"><i class="ti ti-trash"></i></button></span></div>
          </div>
        </div>
      </div>
      <div id="admin-users" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">ユーザー管理</h2>
        <div style="margin-bottom:12px;display:flex;gap:8px">
          <input class="finput" id="user-search" oninput="renderUserTable()" placeholder="名前・メールで検索..." style="max-width:280px;padding:7px 11px;font-size:12px">
          <select class="finput" id="user-filter" onchange="renderUserTable()" style="width:auto;padding:7px 11px;font-size:12px"><option value="">全ロール</option><option value="user">一般</option><option value="admin">管理者</option></select>
        </div>
        <div class="admin-table-wrap">
          <div class="admin-table-head" style="grid-template-columns:1.5fr 2fr 1fr 1fr 1fr"><span>氏名</span><span>メール</span><span>ロール</span><span>ステータス</span><span>操作</span></div>
          <div id="user-table-body"></div>
        </div>
      </div>
      <div id="admin-stats" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">アクセス分析</h2>
        <div class="stat-card-grid">
          <div class="stat-card"><div class="stat-card-label">今月のPV</div><div class="stat-card-val">1,240</div><div style="font-size:11px;color:var(--green);margin-top:4px">↑ 先月比 +12%</div></div>
          <div class="stat-card"><div class="stat-card-label">問い合わせ数</div><div class="stat-card-val">348</div><div style="font-size:11px;color:var(--green);margin-top:4px">↑ 先月比 +24%</div></div>
          <div class="stat-card"><div class="stat-card-label">新規登録</div><div class="stat-card-val">12</div><div style="font-size:11px;color:var(--text-secondary);margin-top:4px">今月</div></div>
        </div>
        <div class="card">
          <div style="font-size:13px;font-weight:500;margin-bottom:14px;color:var(--text-primary)">人気物件ランキング（閲覧数）</div>
          <div style="display:flex;flex-direction:column;gap:12px">
            <div style="display:flex;align-items:center;gap:10px;font-size:13px"><span style="width:24px;height:24px;border-radius:50%;background:var(--blue);color:#fff;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:500;flex-shrink:0">1</span><span style="flex:1;font-weight:500">コート渋谷</span><div class="bar-track"><div class="bar-fill" style="width:80%"></div></div><span style="color:var(--text-secondary);font-size:12px;min-width:36px;text-align:right">120回</span></div>
            <div style="display:flex;align-items:center;gap:10px;font-size:13px"><span style="width:24px;height:24px;border-radius:50%;background:var(--blue-mid);color:#fff;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:500;flex-shrink:0">2</span><span style="flex:1;font-weight:500">ソレイユ目黒</span><div class="bar-track"><div class="bar-fill" style="width:60%;background:var(--blue-mid)"></div></div><span style="color:var(--text-secondary);font-size:12px;min-width:36px;text-align:right">89回</span></div>
            <div style="display:flex;align-items:center;gap:10px;font-size:13px"><span style="width:24px;height:24px;border-radius:50%;background:#B5D4F4;color:var(--blue);display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:500;flex-shrink:0">3</span><span style="flex:1;font-weight:500">グランツ新宿</span><div class="bar-track"><div class="bar-fill" style="width:44%;background:#B5D4F4"></div></div><span style="color:var(--text-secondary);font-size:12px;min-width:36px;text-align:right">67回</span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════ MASTER ══════ -->
<div class="screen" id="s-master">
  <nav class="nav master-nav">
    <div class="logo" style="color:#e0c97a">
      <div style="width:32px;height:32px;background:rgba(224,201,122,.15);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px"><i class="ti ti-crown" style="color:#e0c97a"></i></div>
      マスターパネル
    </div>
    <div style="display:flex;align-items:center;gap:10px">
      <span class="master-badge"><i class="ti ti-crown" style="font-size:10px"></i>nori1216chopper</span>
      <button class="btn btn-sm" onclick="doLogout()" style="border-color:rgba(255,255,255,.2);color:#e0c97a">ログアウト</button>
    </div>
  </nav>
  <div class="admin-wrap">
    <div class="admin-sidebar">
      <div style="font-size:10px;font-weight:500;color:var(--text-secondary);letter-spacing:.06em;margin-bottom:10px">MASTER MENU</div>
      <div class="admin-nav-item on" onclick="switchMaster('users',this)"><i class="ti ti-users"></i>全ユーザー管理</div>
      <div class="admin-nav-item" onclick="switchMaster('roles',this)"><i class="ti ti-shield"></i>ロール変更</div>
      <div style="margin-top:20px;padding-top:16px;border-top:1px solid var(--border)">
        <div class="stat-mini"><div class="stat-mini-label">全ユーザー数</div><div class="stat-mini-val" id="master-user-count">-</div></div>
        <div class="stat-mini"><div class="stat-mini-label">管理者数</div><div class="stat-mini-val" id="master-admin-count">-</div></div>
        <div class="stat-mini"><div class="stat-mini-label">一般ユーザー数</div><div class="stat-mini-val" id="master-regular-count">-</div></div>
      </div>
    </div>
    <div class="admin-main">
      <div id="master-users">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:16px;color:var(--text-primary)">全ユーザー管理</h2>
        <div style="margin-bottom:12px;display:flex;gap:8px">
          <input class="finput" id="master-search" oninput="renderMasterUserTable()" placeholder="名前・メールで検索..." style="max-width:280px;padding:7px 11px;font-size:12px">
          <select class="finput" id="master-filter" onchange="renderMasterUserTable()" style="width:auto;padding:7px 11px;font-size:12px"><option value="">全ロール</option><option value="user">一般</option><option value="admin">管理者</option></select>
        </div>
        <div class="admin-table-wrap">
          <div class="admin-table-head" style="grid-template-columns:1.5fr 2fr 1fr 1fr 1fr"><span>氏名</span><span>メール</span><span>ロール</span><span>ステータス</span><span>操作</span></div>
          <div id="master-user-table-body"></div>
        </div>
      </div>
      <div id="master-roles" style="display:none">
        <h2 style="font-size:16px;font-weight:500;margin-bottom:8px;color:var(--text-primary)">ロール変更</h2>
        <p style="font-size:13px;color:var(--text-secondary);margin-bottom:20px">ユーザーのロールを変更します。管理者にすると管理者パネルが使用可能になります。</p>
        <div class="card" style="max-width:480px">
          <div class="field">
            <div class="flabel">対象ユーザー（メールアドレス）</div>
            <input class="finput" id="role-target-email" placeholder="変更したいユーザーのメール">
          </div>
          <div class="field">
            <div class="flabel">変更後のロール</div>
            <select class="finput" id="role-select">
              <option value="user">一般ユーザー</option>
              <option value="admin">管理者</option>
            </select>
          </div>
          <div id="role-msg" style="display:none;border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px"></div>
          <button class="btn btn-p" onclick="changeUserRole()" style="width:100%;padding:10px;justify-content:center;font-size:13px">
            <i class="ti ti-shield"></i> ロールを変更する
          </button>
        </div>
        <div style="margin-top:20px">
          <h3 style="font-size:14px;font-weight:500;margin-bottom:12px;color:var(--text-primary)">現在のユーザー一覧</h3>
          <div class="admin-table-wrap">
            <div class="admin-table-head" style="grid-template-columns:1.5fr 2fr 1fr 1fr"><span>氏名</span><span>メール</span><span>現在のロール</span><span>クイック変更</span></div>
            <div id="role-table-body"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
/* ══════════════════════════════════════
   CONSTANTS & STATE
══════════════════════════════════════ */
const MASTER_EMAIL = 'nori1216chopper@gmail.com';
const ADMIN_CODE   = '123456';

// ロール定義: 'master' | 'admin' | 'user'
let isLoggedIn  = false;
let currentUser = null;

// ユーザーストア（role: 'user' | 'admin' | 'master'）
const userStore = [
  { name: 'デモユーザー',  email: 'demo@vrhomes.jp',         password: 'demo1234',       role: 'user',   active: true },
  { name: '田中 太郎',     email: 'tanaka@email.com',         password: 'tanaka123',      role: 'user',   active: true },
  { name: '鈴木 花子',     email: 'suzuki@email.com',         password: 'suzuki123',      role: 'admin',  active: true },
  { name: '山本 次郎',     email: 'yamamoto@email.com',       password: 'yamamoto123',    role: 'user',   active: false },
  { name: 'のり',          email: MASTER_EMAIL,               password: 'nori1216master', role: 'master', active: true },
];

/* ══════════════════════════════════════
   ROLE HELPERS
══════════════════════════════════════ */
function isMaster(u)  { return (u||currentUser)?.role === 'master'; }
function isAdmin(u)   { const r=(u||currentUser)?.role; return r==='admin'||r==='master'; }
function isRegular(u) { return (u||currentUser)?.role === 'user'; }

function roleLabel(role) {
  if(role==='master') return '<span class="tag tmaster">マスター</span>';
  if(role==='admin')  return '<span class="tag tgold">管理者</span>';
  return '<span class="tag tgr">一般</span>';
}

/* ══════════════════════════════════════
   UI UPDATE AFTER LOGIN / LOGOUT
══════════════════════════════════════ */
function applyRoleUI() {
  const u = currentUser;
  if(!u) return;

  // --- マイページ上部 ---
  document.getElementById('mp-avatar').textContent = u.name.charAt(0);
  document.getElementById('mp-name').textContent   = u.name;
  document.getElementById('mp-email').textContent  = u.email;
  document.getElementById('mp-role-badge').innerHTML = roleLabel(u.role);
  if(document.getElementById('prof-email')) document.getElementById('prof-email').value = u.email;

  // --- タブバー ---
  const adminTab  = document.getElementById('tab-admin');
  const masterTab = document.getElementById('tab-master');
  // 管理者タブ: admin or master のときだけ表示
  if(isAdmin()) { adminTab.classList.remove('hidden'); } else { adminTab.classList.add('hidden'); }
  // マスタータブ: masterのみ
  if(isMaster()) { masterTab.classList.remove('hidden'); } else { masterTab.classList.add('hidden'); }

  // --- コード入力タブ: 一般 or admin（まだadmin昇格していない人向け）---
  const codeNav = document.getElementById('mp-nav-code');
  // masterは不要、adminは既に昇格済みなので不要、userだけ表示
  if(isRegular()) { codeNav.classList.remove('hidden'); } else { codeNav.classList.add('hidden'); }

  // --- TOP navの管理者ボタン ---
  const adminBtn = document.getElementById('nav-admin-btn');
  if(isAdmin()) { adminBtn.classList.remove('hidden'); } else { adminBtn.classList.add('hidden'); }

  // --- 管理者画面のメール表示 ---
  document.getElementById('admin-email-display').textContent = u.email;

  // --- 統計を最新に ---
  refreshStats();
}

function refreshStats() {
  const total   = userStore.filter(u=>u.role!=='master').length;
  const admins  = userStore.filter(u=>u.role==='admin').length;
  const regulars= userStore.filter(u=>u.role==='user').length;
  const el1 = document.getElementById('admin-user-count');
  const el2 = document.getElementById('master-user-count');
  const el3 = document.getElementById('master-admin-count');
  const el4 = document.getElementById('master-regular-count');
  if(el1) el1.textContent = total;
  if(el2) el2.textContent = userStore.length;
  if(el3) el3.textContent = admins;
  if(el4) el4.textContent = regulars;
}

/* ══════════════════════════════════════
   LOGIN GATE
══════════════════════════════════════ */
function showGateMsg(msg, isError) {
  const el = document.getElementById('gate-msg');
  el.style.background = isError ? 'var(--red-light)' : 'var(--green-light)';
  el.style.border     = isError ? '1px solid var(--red-border)' : '1px solid #a8d080';
  el.style.color      = isError ? 'var(--red)' : 'var(--green)';
  el.textContent = msg;
  el.style.display = 'block';
  if(!isError) setTimeout(() => { el.style.display = 'none'; }, 3000);
}

function switchGateAuth(t) {
  const isLogin = t === 'login';
  const tl = document.getElementById('gatab-login');
  const tr = document.getElementById('gatab-reg');
  tl.style.background = isLogin ? 'var(--blue)' : 'transparent';
  tl.style.color      = isLogin ? '#fff' : 'var(--text-secondary)';
  tr.style.background = isLogin ? 'transparent' : 'var(--blue)';
  tr.style.color      = isLogin ? 'var(--text-secondary)' : '#fff';
  const msg = document.getElementById('gate-msg');
  if(msg) msg.style.display = 'none';
  const hint = document.getElementById('gate-switch-hint');
  if(isLogin) {
    document.getElementById('gate-form').innerHTML = `
      <div class="field"><div class="flabel">メールアドレス</div><input class="finput" id="g-email" type="text" placeholder="example@email.com"></div>
      <div class="field" style="margin-bottom:6px"><div class="flabel">パスワード</div>
        <div class="pass-wrap"><input class="finput" id="g-pass" type="password" placeholder="••••••••">
        <button class="eye-btn" id="g-eye" type="button" onclick="toggleGateEye()"><i class="ti ti-eye"></i></button></div>
      </div>
      <div style="text-align:right;font-size:11px;color:var(--blue);cursor:pointer;margin-bottom:20px">パスワードをお忘れですか？</div>
      <button class="btn btn-p" type="button" onclick="gateLogin()" style="width:100%;padding:12px;font-size:14px;justify-content:center;border-radius:var(--radius-md)">
        ログイン <i class="ti ti-arrow-right"></i>
      </button>`;
    hint.innerHTML = 'アカウントをお持ちでない方は <a style="color:var(--blue);cursor:pointer;font-weight:500" onclick="switchGateAuth(\'reg\')">新規登録</a>';
  } else {
    document.getElementById('gate-form').innerHTML = `
      <div class="field"><div class="flabel">お名前 <span class="req">*</span></div><input class="finput" id="g-name" placeholder="田中 太郎"></div>
      <div class="field"><div class="flabel">メールアドレス <span class="req">*</span></div><input class="finput" id="g-email" type="text" placeholder="example@email.com"></div>
      <div class="field" style="margin-bottom:6px"><div class="flabel">パスワード <span class="req">*</span>（6文字以上）</div>
        <div class="pass-wrap"><input class="finput" id="g-pass" type="password" placeholder="6文字以上">
        <button class="eye-btn" id="g-eye" type="button" onclick="toggleGateEye()"><i class="ti ti-eye"></i></button></div>
        <div class="str-bar" style="margin-top:6px"><div class="str-seg" id="gs1"></div><div class="str-seg" id="gs2"></div><div class="str-seg" id="gs3"></div><div class="str-seg" id="gs4"></div></div>
      </div>
      <button class="btn btn-p" type="button" onclick="gateRegister()" style="width:100%;padding:12px;font-size:14px;justify-content:center;border-radius:var(--radius-md);margin-top:14px">
        <i class="ti ti-user-plus"></i> 会員登録する
      </button>`;
    hint.innerHTML = 'すでにアカウントをお持ちの方は <a style="color:var(--blue);cursor:pointer;font-weight:500" onclick="switchGateAuth(\'login\')">ログイン</a>';
    document.getElementById('g-pass').addEventListener('input', function() {
      const v=this.value, segs=[document.getElementById('gs1'),document.getElementById('gs2'),document.getElementById('gs3'),document.getElementById('gs4')];
      segs.forEach(s=>{s.className='str-seg';});
      if(v.length>=2) segs[0].className='str-seg weak';
      if(v.length>=4) segs[1].className='str-seg weak';
      if(v.length>=6){segs[0].className='str-seg mid';segs[1].className='str-seg mid';segs[2].className='str-seg mid';}
      if(v.length>=10&&/[A-Z]/.test(v)) segs.forEach(s=>s.className='str-seg strong');
    });
  }
}

function toggleGateEye() {
  const inp=document.getElementById('g-pass'), btn=document.getElementById('g-eye');
  const isPass=inp.type==='password';
  inp.type=isPass?'text':'password';
  btn.innerHTML=isPass?'<i class="ti ti-eye-off"></i>':'<i class="ti ti-eye"></i>';
}

function gateLogin() {
  const email=(document.getElementById('g-email')||{}).value?.trim()||'';
  const pass =(document.getElementById('g-pass') ||{}).value||'';
  if(!email||!pass){showGateMsg('メールアドレスとパスワードを入力してください',true);return;}
  const user=userStore.find(u=>u.email===email&&u.password===pass);
  if(!user){showGateMsg('メールアドレスまたはパスワードが違います',true);return;}
  if(!user.active){showGateMsg('このアカウントは停止されています',true);return;}
  isLoggedIn=true; currentUser=user;
  document.getElementById('login-gate').classList.add('hidden');
  applyRoleUI();
  // マスターはマスター画面へ、それ以外はトップへ
  if(isMaster()) {
    renderMasterUserTable();
    renderRoleTable();
    showScreen('master');
  } else {
    showScreen('top');
  }
}

function gateRegister() {
  const name =(document.getElementById('g-name') ||{}).value?.trim()||'';
  const email=(document.getElementById('g-email')||{}).value?.trim()||'';
  const pass =(document.getElementById('g-pass') ||{}).value||'';
  if(!name) {showGateMsg('お名前を入力してください',true);return;}
  if(!email){showGateMsg('メールアドレスを入力してください',true);return;}
  if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)){showGateMsg('正しいメールアドレスを入力してください',true);return;}
  if(pass.length<6){showGateMsg('パスワードは6文字以上で入力してください',true);return;}
  if(userStore.find(u=>u.email===email)){showGateMsg('このメールアドレスはすでに登録されています',true);return;}
  userStore.push({name,email,password:pass,role:'user',active:true});
  showGateMsg('登録完了！ログインしてください',false);
  setTimeout(()=>switchGateAuth('login'),1200);
}

function doLogout() {
  isLoggedIn=false; currentUser=null;
  switchGateAuth('login');
  document.getElementById('login-gate').classList.remove('hidden');
  window.scrollTo(0,0);
}

/* ══════════════════════════════════════
   CODE INPUT (一般ユーザー → 管理者昇格)
══════════════════════════════════════ */
function submitCode() {
  const code=(document.getElementById('code-input')||{}).value?.trim()||'';
  const msgEl=document.getElementById('code-msg');
  if(code===ADMIN_CODE) {
    // 昇格
    currentUser.role='admin';
    const stored=userStore.find(u=>u.email===currentUser.email);
    if(stored) stored.role='admin';
    msgEl.style.cssText='display:block;background:var(--green-light);border:1px solid #a8d080;color:var(--green);border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px';
    msgEl.textContent='✓ 管理者として認証されました！管理者タブが追加されました。';
    applyRoleUI(); // タブ等を更新
    setTimeout(()=>{ msgEl.style.display='none'; document.getElementById('code-input').value=''; },3000);
  } else {
    msgEl.style.cssText='display:block;background:var(--red-light);border:1px solid var(--red-border);color:var(--red);border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px';
    msgEl.textContent='コードが正しくありません。';
    setTimeout(()=>{ msgEl.style.display='none'; },3000);
  }
}

/* ══════════════════════════════════════
   ADMIN: USER TABLE
══════════════════════════════════════ */
function renderUserTable() {
  const q=(document.getElementById('user-search')||{}).value?.toLowerCase()||'';
  const f=(document.getElementById('user-filter')||{}).value||'';
  const tbody=document.getElementById('user-table-body');
  if(!tbody) return;
  // 管理者は master 以外を見せる
  const list=userStore.filter(u=>u.role!=='master')
    .filter(u=>!q||(u.name.toLowerCase().includes(q)||u.email.toLowerCase().includes(q)))
    .filter(u=>!f||u.role===f);
  tbody.innerHTML=list.map(u=>`
    <div class="admin-table-row" style="grid-template-columns:1.5fr 2fr 1fr 1fr 1fr">
      <span style="font-weight:500">${u.name}</span>
      <span style="color:var(--text-secondary);font-size:11px">${u.email}</span>
      <span>${roleLabel(u.role)}</span>
      <span><span class="tag ${u.active?'tg':'tr'}" style="font-size:9px">${u.active?'有効':'停止'}</span></span>
      <span style="display:flex;gap:4px">
        <button class="btn btn-sm" style="font-size:10px;padding:3px 8px" title="削除" onclick="deleteUser('${u.email}')"><i class="ti ti-trash" style="color:var(--red)"></i></button>
      </span>
    </div>`).join('')||'<div style="padding:14px;font-size:13px;color:var(--text-secondary);text-align:center">該当するユーザーはいません</div>';
}

function deleteUser(email) {
  if(email===MASTER_EMAIL){alert('マスターアカウントは削除できません');return;}
  if(email===currentUser?.email){alert('自分自身は削除できません');return;}
  const idx=userStore.findIndex(u=>u.email===email);
  if(idx>-1) userStore.splice(idx,1);
  renderUserTable(); renderMasterUserTable(); renderRoleTable(); refreshStats();
}

/* ══════════════════════════════════════
   MASTER: USER TABLE
══════════════════════════════════════ */
function renderMasterUserTable() {
  const q=(document.getElementById('master-search')||{}).value?.toLowerCase()||'';
  const f=(document.getElementById('master-filter')||{}).value||'';
  const tbody=document.getElementById('master-user-table-body');
  if(!tbody) return;
  const list=userStore
    .filter(u=>!q||(u.name.toLowerCase().includes(q)||u.email.toLowerCase().includes(q)))
    .filter(u=>!f||u.role===f);
  tbody.innerHTML=list.map(u=>`
    <div class="admin-table-row" style="grid-template-columns:1.5fr 2fr 1fr 1fr 1fr">
      <span style="font-weight:500">${u.name}${u.email===MASTER_EMAIL?' <span class="master-badge" style="font-size:9px"><i class="ti ti-crown" style="font-size:9px"></i></span>':''}</span>
      <span style="color:var(--text-secondary);font-size:11px">${u.email}</span>
      <span>${roleLabel(u.role)}</span>
      <span><span class="tag ${u.active?'tg':'tr'}" style="font-size:9px">${u.active?'有効':'停止'}</span></span>
      <span style="display:flex;gap:4px">
        ${u.role!=='master'?`<button class="btn btn-sm" style="font-size:10px;padding:3px 8px" onclick="quickToggleActive('${u.email}')">${u.active?'<i class="ti ti-ban" style="color:var(--warn)"></i>':'<i class="ti ti-check" style="color:var(--green)"></i>'}</button>`:''}
        ${u.email!==MASTER_EMAIL?`<button class="btn btn-sm" style="font-size:10px;padding:3px 8px" onclick="deleteUser('${u.email}')"><i class="ti ti-trash" style="color:var(--red)"></i></button>`:''}
      </span>
    </div>`).join('')||'<div style="padding:14px;font-size:13px;color:var(--text-secondary);text-align:center">該当するユーザーはいません</div>';
}

function quickToggleActive(email) {
  const u=userStore.find(u=>u.email===email);
  if(!u) return;
  u.active=!u.active;
  renderMasterUserTable(); renderUserTable(); renderRoleTable(); refreshStats();
}

/* ══════════════════════════════════════
   MASTER: ROLE CHANGE
══════════════════════════════════════ */
function renderRoleTable() {
  const tbody=document.getElementById('role-table-body');
  if(!tbody) return;
  const list=userStore.filter(u=>u.role!=='master');
  tbody.innerHTML=list.map(u=>`
    <div class="admin-table-row" style="grid-template-columns:1.5fr 2fr 1fr 1fr">
      <span style="font-weight:500">${u.name}</span>
      <span style="color:var(--text-secondary);font-size:11px">${u.email}</span>
      <span id="role-tag-${u.email.replace(/[@.]/g,'_')}">${roleLabel(u.role)}</span>
      <span>
        <select class="finput" style="padding:4px 8px;font-size:11px;width:auto" onchange="quickSetRole('${u.email}',this.value)">
          <option value="user" ${u.role==='user'?'selected':''}>一般</option>
          <option value="admin" ${u.role==='admin'?'selected':''}>管理者</option>
        </select>
      </span>
    </div>`).join('');
}

function changeUserRole() {
  const email=(document.getElementById('role-target-email')||{}).value?.trim()||'';
  const role =document.getElementById('role-select').value;
  const msgEl=document.getElementById('role-msg');
  const u=userStore.find(u=>u.email===email);
  if(!u){
    msgEl.style.cssText='display:block;background:var(--red-light);border:1px solid var(--red-border);color:var(--red);border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px';
    msgEl.textContent='該当するユーザーが見つかりません';
    setTimeout(()=>{msgEl.style.display='none';},3000);return;
  }
  if(u.role==='master'){
    msgEl.style.cssText='display:block;background:var(--red-light);border:1px solid var(--red-border);color:var(--red);border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px';
    msgEl.textContent='マスターアカウントのロールは変更できません';
    setTimeout(()=>{msgEl.style.display='none';},3000);return;
  }
  u.role=role;
  msgEl.style.cssText='display:block;background:var(--green-light);border:1px solid #a8d080;color:var(--green);border-radius:var(--radius-md);padding:9px 13px;font-size:13px;margin-bottom:14px';
  msgEl.textContent=`${u.name} のロールを「${role==='admin'?'管理者':'一般ユーザー'}」に変更しました`;
  setTimeout(()=>{msgEl.style.display='none';},3000);
  renderRoleTable(); renderMasterUserTable(); renderUserTable(); refreshStats();
}

function quickSetRole(email, role) {
  const u=userStore.find(u=>u.email===email);
  if(!u||u.role==='master') return;
  u.role=role;
  renderRoleTable(); renderMasterUserTable(); renderUserTable(); refreshStats();
}

/* ══════════════════════════════════════
   SCREEN NAVIGATION
══════════════════════════════════════ */
function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('s-'+id).classList.add('active');
  const tabEl=document.getElementById('tab-'+id);
  if(tabEl) tabEl.classList.add('active');
  window.scrollTo(0,0);
}

function guardedScreen(id) {
  if(!isLoggedIn){ document.getElementById('login-gate').classList.remove('hidden'); return; }
  // 管理者ページは管理者以上のみ
  if(id==='admin'&&!isAdmin()){ alert('管理者権限が必要です'); return; }
  // マスターページはマスターのみ
  if(id==='master'&&!isMaster()){ alert('マスター権限が必要です'); return; }
  // 管理者画面へ遷移時にユーザーテーブルを最新化
  if(id==='admin') renderUserTable();
  // マスター画面へ遷移時
  if(id==='master'){ renderMasterUserTable(); renderRoleTable(); }
  showScreen(id);
}

/* ══════════════════════════════════════
   PROPERTY DATA & AWS連携
   ─────────────────────────────────────
   AWS API Gateway の URL をここに設定:
     const AWS_API_URL = 'https://xxxx.execute-api.ap-northeast-1.amazonaws.com/prod/properties';
   設定するまではローカルのフォールバックデータを使用します。
══════════════════════════════════════ */

// ▼ AWS連携時にここを書き換える（例）
// const AWS_API_URL = 'https://xxxx.execute-api.ap-northeast-1.amazonaws.com/prod/properties';
const AWS_API_URL = null; // null のままだとローカルデータを使用

// フォールバック用ローカルデータ（AWSが未設定の間はこちらを使う）
const LOCAL_PROPS = [
  {id:1,name:'コート渋谷',area:'渋谷区',station:'渋谷駅 徒歩3分',price:92000,size:48,madori:'2LDK',tags:['ペット可','南向き']},
  {id:2,name:'グランツ新宿',area:'新宿区',station:'新宿駅 徒歩8分',price:68000,size:33,madori:'1LDK',tags:['オートロック']},
  {id:3,name:'ソレイユ目黒',area:'目黒区',station:'目黒駅 徒歩5分',price:115000,size:62,madori:'3LDK',tags:['南向き','宅配BOX']},
  {id:4,name:'アーバン品川',area:'品川区',station:'品川駅 徒歩10分',price:75000,size:40,madori:'1LDK',tags:['ネット無料']},
  {id:5,name:'ルミエール恵比寿',area:'渋谷区',station:'恵比寿駅 徒歩6分',price:88000,size:45,madori:'2LDK',tags:['バルコニー']},
  {id:6,name:'シティ池袋',area:'豊島区',station:'池袋駅 徒歩4分',price:58000,size:28,madori:'1K',tags:['24hゴミ']},
];

// 実行時に使う物件リスト（fetch後にここへ格納）
let PROPS = [...LOCAL_PROPS];
let favs  = new Set([1]);

/* AWS または ローカルから物件を取得してカード・管理テーブルを更新 */
async function fetchAndRenderProps() {
  const grid    = document.getElementById('card-grid');
  const countEl = document.querySelector('.results-bar strong');

  // ── ローディング表示 ──
  grid.innerHTML = `
    <div style="grid-column:1/-1;padding:40px 0;text-align:center;color:var(--text-secondary)">
      <i class="ti ti-loader-2" style="font-size:24px;animation:spin 1s linear infinite;display:inline-block"></i>
      <div style="margin-top:10px;font-size:13px">物件情報を読み込み中…</div>
    </div>`;

  try {
    if(AWS_API_URL) {
      // ── AWS API Gateway から取得 ──
      const res = await fetch(AWS_API_URL, {
        method: 'GET',
        headers: { 'Content-Type': 'application/json' }
      });
      if(!res.ok) throw new Error(`HTTP ${res.status}`);
      const data = await res.json();
      // APIレスポンスが { items: [...] } 形式の場合と配列直接の両方に対応
      PROPS = Array.isArray(data) ? data : (data.items || data.properties || []);
      showDataSourceBadge('AWS');
    } else {
      // ── ローカルフォールバック ──
      await new Promise(r => setTimeout(r, 300)); // 自然な遅延
      PROPS = [...LOCAL_PROPS];
      showDataSourceBadge('local');
    }
  } catch(e) {
    console.warn('AWS fetch failed, using local data:', e);
    PROPS = [...LOCAL_PROPS];
    showDataSourceBadge('error');
  }

  renderCards();
  renderAdminPropTable();
  if(countEl) countEl.textContent = PROPS.length;
  const resultSpan = document.querySelector('.results-bar span');
  if(resultSpan) resultSpan.innerHTML = `<strong style="color:var(--text-primary)">${PROPS.length}</strong> 件の物件`;
}

/* データソースバッジを検索バー下に表示 */
function showDataSourceBadge(source) {
  let badge = document.getElementById('data-source-badge');
  if(!badge) {
    badge = document.createElement('div');
    badge.id = 'data-source-badge';
    badge.style.cssText = 'display:flex;align-items:center;gap:6px;font-size:11px;padding:4px 10px;border-radius:20px;margin-left:8px';
    const bar = document.querySelector('.results-bar .nav-r') || document.querySelector('.results-bar > div:last-child');
    if(bar) bar.prepend(badge);
  }
  if(source==='AWS') {
    badge.style.background='var(--green-light)'; badge.style.color='var(--green)'; badge.style.border='1px solid #a8d080';
    badge.innerHTML='<i class="ti ti-cloud-check"></i>AWS同期済み';
  } else if(source==='error') {
    badge.style.background='var(--warn-light)'; badge.style.color='var(--warn)'; badge.style.border='1px solid #f0c070';
    badge.innerHTML='<i class="ti ti-cloud-off"></i>ローカルデータ（AWS接続エラー）';
  } else {
    badge.style.background='var(--bg-secondary)'; badge.style.color='var(--text-secondary)'; badge.style.border='1px solid var(--border)';
    badge.innerHTML='<i class="ti ti-database"></i>ローカルデータ';
  }
}

/* カードを描画 */
function renderCards() {
  const grid = document.getElementById('card-grid');
  if(!PROPS.length) {
    grid.innerHTML = '<div style="grid-column:1/-1;padding:40px 0;text-align:center;color:var(--text-secondary);font-size:13px"><i class="ti ti-building-off" style="font-size:28px;display:block;margin-bottom:8px"></i>物件が見つかりませんでした</div>';
    return;
  }
  grid.innerHTML = PROPS.map(p => {
    const fav = favs.has(p.id);
    const tags = Array.isArray(p.tags) ? p.tags : (p.tags ? String(p.tags).split(',') : []);
    return `<div class="prop-card">
      <div class="prop-img"><i class="ti ti-building" style="font-size:30px;color:#85B7EB"></i>
        <div class="fav-btn${fav?' on':''}" onclick="toggleFav(${JSON.stringify(p.id)},this)"><i class="ti ti-heart"></i></div>
      </div>
      <div class="prop-body">
        <div class="prop-price">¥${Number(p.price).toLocaleString()}<span style="font-size:11px;font-weight:400;color:var(--text-secondary)">/月</span></div>
        <div class="prop-name">${p.name}</div>
        <div class="prop-loc"><i class="ti ti-map-pin"></i>${p.station||p.area||''}</div>
        <div class="prop-tags"><span class="tag tg">${p.madori||p.layout||''}</span>${tags.map(t=>`<span class="tag tgr">${t}</span>`).join('')}</div>
      </div>
      <div class="prop-footer"><span class="prop-area">${p.size||p.area_sqm||'−'}㎡</span></div>
    </div>`;
  }).join('');
}

/* 管理者パネルの物件テーブルを再描画（addPropertyと共有） */
function renderAdminPropTable() {
  const tbody = document.getElementById('prop-table-body');
  if(!tbody) return;
  tbody.innerHTML = PROPS.map(p => `
    <div class="admin-table-row" style="grid-template-columns:2fr 1fr 1fr 90px">
      <span style="font-weight:500">${p.name}</span>
      <span style="color:var(--text-secondary)">${p.area}</span>
      <span>¥${Number(p.price).toLocaleString()}</span>
      <span style="display:flex;gap:5px">
        <button class="btn btn-sm" style="font-size:10px;padding:3px 8px"><i class="ti ti-edit"></i></button>
        <button class="btn btn-sm" style="font-size:10px;padding:3px 8px;color:var(--red);border-color:var(--red-border)" onclick="this.closest('.admin-table-row').remove()"><i class="ti ti-trash"></i></button>
      </span>
    </div>`).join('');
}

/* ポーリング: AWS_API_URL が設定されていれば 30秒ごとに自動更新 */
function startPolling() {
  if(!AWS_API_URL) return;
  setInterval(async () => {
    try {
      const res  = await fetch(AWS_API_URL, { headers: { 'Content-Type': 'application/json' } });
      if(!res.ok) return;
      const data = await res.json();
      const newProps = Array.isArray(data) ? data : (data.items || data.properties || []);
      // 件数が変わったときだけ再描画
      if(newProps.length !== PROPS.length) {
        PROPS = newProps;
        renderCards();
        renderAdminPropTable();
        const resultSpan = document.querySelector('.results-bar span');
        if(resultSpan) resultSpan.innerHTML = `<strong style="color:var(--text-primary)">${PROPS.length}</strong> 件の物件`;
        showDataSourceBadge('AWS');
      }
    } catch(_) {}
  }, 30000);
}

// スピナー用アニメーション
const _style = document.createElement('style');
_style.textContent = '@keyframes spin{to{transform:rotate(360deg)}}';
document.head.appendChild(_style);

// 初回ロード
fetchAndRenderProps();
startPolling();

function toggleFav(id,el){if(favs.has(id)){favs.delete(id);el.classList.remove('on');}else{favs.add(id);el.classList.add('on');}}
function togglePin(id){['pa','pb','pc'].forEach(p=>{const el=document.getElementById(p);if(p===id){el.classList.toggle('show');}else{el.classList.remove('show');}});}

/* ── Mypage tabs ── */
function switchMp(id,el){
  ['fav','hist','prof','code'].forEach(k=>document.getElementById('mp-'+k).style.display=k===id?'block':'none');
  document.querySelectorAll('.mp-nav-item').forEach(i=>i.classList.remove('on'));
  el.classList.add('on');
}

/* ── Admin tabs ── */
function switchAdmin(id,el){
  ['props','users','stats'].forEach(k=>document.getElementById('admin-'+k).style.display=k===id?'block':'none');
  document.querySelectorAll('.admin-nav-item').forEach(i=>i.classList.remove('on'));
  el.classList.add('on');
  if(id==='users') renderUserTable();
}

/* ── Master tabs ── */
function switchMaster(id,el){
  ['users','roles'].forEach(k=>document.getElementById('master-'+k).style.display=k===id?'block':'none');
  document.querySelectorAll('.admin-nav-item').forEach(i=>i.classList.remove('on'));
  el.classList.add('on');
  if(id==='users') renderMasterUserTable();
  if(id==='roles') renderRoleTable();
}

/* ── Admin: add property ── */
function toggleAddForm(){const f=document.getElementById('add-form');f.style.display=f.style.display==='block'?'none':'block';}
function addProperty(){
  const name=document.getElementById('af-name').value||'新規物件';
  const area=document.getElementById('af-area').value||'−';
  const rent=document.getElementById('af-rent').value;
  const row=document.createElement('div');
  row.className='admin-table-row';row.style.gridTemplateColumns='2fr 1fr 1fr 90px';row.style.background='var(--green-light)';
  row.innerHTML=`<span style="font-weight:500">${name}</span><span style="color:var(--text-secondary)">${area}</span><span>${rent?'¥'+Number(rent).toLocaleString():'−'}</span><span style="display:flex;gap:5px"><button class="btn btn-sm" style="font-size:10px;padding:3px 8px"><i class="ti ti-edit"></i></button><button class="btn btn-sm" style="font-size:10px;padding:3px 8px;color:var(--red);border-color:var(--red-border)" onclick="this.closest('.admin-table-row').remove()"><i class="ti ti-trash"></i></button></span>`;
  document.getElementById('prop-table-body').appendChild(row);
  setTimeout(()=>row.style.background='',1500);
  toggleAddForm();
}
</script>
</body>
</html>
