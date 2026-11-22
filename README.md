<!--
╔══════════════════════════════════════════════════════════════════╗
║  لعبة CITY OF RAIN — مدينة المطر                                 ║
║  عالم مفتوح • تحديات • ضرب نار • جرافيك نوار بكسل                ║
║                                                                  ║
║  ⚠️ لو شايف الكود كنص: الملف اتحفظ بامتداد غلط.                  ║
║  1) افتح تطبيق الملفات → اضغط مطولاً على الملف → إعادة تسمية     ║
║  2) خلي الاسم:  rain.html   (لازم .html مش .md ولا .txt)         ║
║  3) افتحه بـ Chrome → اللعبة تشتغل فوراً بدون إنترنت.            ║
║                                                                  ║
║  التحكم: عصا يسار للحركة • ◎ نار • E تفاعل • R تلقيم            ║
╚══════════════════════════════════════════════════════════════════╝
-->
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
<meta name="theme-color" content="#0a0806">
<title>CITY OF RAIN — مدينة المطر</title>
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3E%3Crect width='16' height='16' fill='%230a0806'/%3E%3Crect x='6' y='2' width='4' height='8' fill='%23d99a2b'/%3E%3Crect x='3' y='11' width='10' height='3' fill='%2322d3ee'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0806; --surface:#171008; --panel:#120d08;
  --amber:#d99a2b; --amber2:#ffcf6e; --warm:#8a5a2b; --wood:#5a3b22;
  --cyan:#5eead4; --rain:#7fb4d9; --red:#c0392b; --blood:#8e1f1f;
  --green:#7fb069; --ink:#f2e9d8; --dim:#a89877; --line:#3a2c1a;
  --reserve:132px; --px:'Press Start 2P',monospace; --ar:'Cairo',system-ui,sans-serif;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow:hidden}
body{background:var(--bg);color:var(--ink);font-family:var(--ar);user-select:none;-webkit-user-select:none;touch-action:manipulation;
  background-image:radial-gradient(900px 400px at 80% -10%,rgba(217,154,43,.10),transparent 60%),
  radial-gradient(800px 400px at 10% 110%,rgba(127,180,217,.08),transparent 60%),linear-gradient(180deg,#0a0806,#0d0a07 55%,#0a0806)}
#app{height:100vh;display:flex;flex-direction:column}
@supports (height:100dvh){#app{height:100dvh}}
#topbar{flex:0 0 auto;display:flex;align-items:center;gap:8px;padding:7px 10px;padding-top:calc(7px + env(safe-area-inset-top));
  background:linear-gradient(180deg,rgba(23,16,8,.95),rgba(23,16,8,.6));border-bottom:1px solid rgba(217,154,43,.3);
  box-shadow:0 1px 0 rgba(94,234,212,.08),0 8px 24px rgba(0,0,0,.5);position:relative;z-index:40}
#logo{font-family:var(--px);font-size:9px;letter-spacing:1px;color:var(--amber);text-shadow:0 0 8px rgba(217,154,43,.7),2px 2px 0 rgba(127,180,217,.4);white-space:nowrap}
#logo b{color:var(--rain)}
#locTag{font-size:11px;font-weight:700;color:var(--dim);flex:1;text-align:center;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
#locTag em{font-style:normal;color:var(--amber2)}
.tbtn{font-family:var(--ar);font-weight:700;font-size:12px;color:var(--ink);background:rgba(217,154,43,.1);border:1px solid rgba(217,154,43,.45);
  border-radius:8px;padding:5px 9px;cursor:pointer;display:flex;align-items:center;gap:5px;transition:all .15s;min-height:32px}
.tbtn:hover{background:rgba(217,154,43,.25);box-shadow:0 0 12px rgba(217,154,43,.4)}
.tbtn:active{transform:translateY(1px) scale(.97)}
.tbtn .ic{font-size:14px;line-height:1}
#btnSound[data-muted="1"]{border-color:rgba(192,57,43,.6);background:rgba(192,57,43,.12);color:#e8a79f}
#btnPause:disabled{opacity:.35;cursor:default}
#stage{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:8px;padding:6px;min-height:0;position:relative}
#frame{position:relative;width:min(100%,calc((100vh - var(--reserve))*16/9));aspect-ratio:16/9;border-radius:8px;overflow:hidden;
  border:1px solid rgba(217,154,43,.35);box-shadow:0 0 0 1px rgba(127,180,217,.1),0 0 30px rgba(217,154,43,.15),0 20px 50px rgba(0,0,0,.65);background:#050403}
@supports (height:100dvh){#frame{width:min(100%,calc((100dvh - var(--reserve))*16/9))}}
#game{width:100%;height:100%;display:block;image-rendering:pixelated;image-rendering:crisp-edges}
#frame::after{content:"";position:absolute;inset:0;pointer-events:none;z-index:5;
  background:repeating-linear-gradient(0deg,rgba(0,0,0,.12) 0 1px,transparent 1px 3px),
  radial-gradient(120% 95% at 50% 45%,transparent 52%,rgba(0,0,0,.6) 100%);mix-blend-mode:multiply}
/* HUD */
#hud{position:absolute;inset:0;pointer-events:none;z-index:10;display:none}
body[data-state="playing"] #hud,body[data-state="paused"] #hud{display:block}
.hudTL{position:absolute;top:7px;right:7px;display:flex;flex-direction:column;gap:4px;width:140px}
.bar{height:10px;background:rgba(5,4,3,.8);border:1px solid rgba(168,152,119,.4);border-radius:3px;overflow:hidden;position:relative;direction:ltr}
.bar i{position:absolute;inset:0;transform-origin:left center;transition:transform .12s;display:block}
#hpFill{background:linear-gradient(90deg,#8e1f1f,#c0392b 60%,#e67e22);box-shadow:0 0 8px rgba(192,57,43,.6)}
.barLbl{position:absolute;inset:0;display:flex;align-items:center;justify-content:space-between;padding:0 5px;font-size:8px;font-weight:900;color:#fff;text-shadow:0 1px 2px #000;direction:rtl}
#ammoRow{display:flex;align-items:center;gap:4px;direction:ltr}
#ammoPips{display:flex;gap:2px}
#ammoPips span{width:5px;height:10px;background:var(--amber2);box-shadow:0 0 4px rgba(255,207,110,.6);border-radius:1px}
#ammoPips span.off{background:#3a2c1a;box-shadow:none}
#resVal{font-family:var(--px);font-size:8px;color:var(--dim)}
#relBar{height:3px;background:#3a2c1a;border-radius:2px;overflow:hidden;display:none;direction:ltr}
#relBar.on{display:block}
#relBar i{display:block;height:100%;background:var(--cyan);width:0}
.hudTR{position:absolute;top:7px;left:7px;text-align:left;max-width:46%;direction:rtl}
#missionTitle{font-size:10px;font-weight:900;color:var(--amber2);text-shadow:0 0 6px rgba(217,154,43,.5)}
#objVal{font-size:10px;color:var(--dim);line-height:1.5;margin-top:2px}
#compass{position:absolute;top:7px;left:50%;transform:translateX(-50%);display:flex;align-items:center;gap:6px;
  background:rgba(5,4,3,.7);border:1px solid rgba(94,234,212,.35);border-radius:8px;padding:3px 10px;font-size:10px;font-weight:700;color:var(--cyan);white-space:nowrap}
#compArrow{font-size:12px;display:inline-block;transition:transform .2s}
#prompt{position:absolute;bottom:52px;left:50%;transform:translateX(-50%);background:rgba(5,4,3,.85);border:1px solid var(--amber);
  border-radius:8px;padding:4px 12px;font-size:11px;font-weight:900;color:var(--amber2);opacity:0;transition:opacity .15s;white-space:nowrap;box-shadow:0 0 14px rgba(217,154,43,.3)}
#prompt.show{opacity:1}
#prompt b{font-family:var(--px);font-size:8px;background:rgba(217,154,43,.2);border:1px solid var(--amber);border-radius:3px;padding:2px 4px;margin-left:4px}
#banner{position:absolute;top:38%;left:0;right:0;text-align:center;pointer-events:none;opacity:0;transition:opacity .5s}
#banner.show{opacity:1}
#banner .bn{font-family:var(--px);font-size:13px;color:var(--ink);text-shadow:0 0 12px rgba(217,154,43,.6),2px 2px 0 #000}
#banner .bs{font-size:11px;color:var(--dim);margin-top:6px;letter-spacing:2px}
/* dialogue */
#dlg{position:absolute;left:4%;right:4%;bottom:8px;z-index:22;display:none;background:linear-gradient(180deg,rgba(18,13,8,.96),rgba(10,8,6,.98));
  border:1px solid rgba(217,154,43,.5);border-radius:10px;padding:10px 14px;box-shadow:0 0 24px rgba(0,0,0,.7),0 0 14px rgba(217,154,43,.15)}
#dlg.on{display:block}
#dlgName{font-family:var(--px);font-size:8px;color:var(--amber);margin-bottom:6px}
#dlgText{font-size:13px;line-height:1.8;color:var(--ink);min-height:44px}
#dlgHint{font-size:9px;color:var(--dim);text-align:left;margin-top:4px;animation:blink 1.2s infinite}
@keyframes blink{50%{opacity:.3}}
/* touch */
#touch{position:absolute;left:0;right:0;bottom:0;z-index:20;display:none;justify-content:space-between;align-items:flex-end;padding:10px;direction:ltr;pointer-events:none}
body[data-state="playing"] #touch{display:flex}
body:not(.coarse) #touch{display:none!important}
#stick{width:104px;height:104px;border-radius:50%;border:2px solid rgba(168,152,119,.5);background:rgba(5,4,3,.45);position:relative;pointer-events:auto;touch-action:none}
#stickKnob{position:absolute;left:50%;top:50%;width:44px;height:44px;margin:-22px 0 0 -22px;border-radius:50%;
  background:rgba(217,154,43,.35);border:2px solid var(--amber);box-shadow:0 0 12px rgba(217,154,43,.4)}
.tgroup{display:flex;gap:10px;align-items:flex-end;pointer-events:auto}
.tc{width:58px;height:58px;border-radius:50%;border:2px solid;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:1px;
  font-family:var(--ar);font-weight:900;font-size:9px;color:var(--ink);background:rgba(5,4,3,.55);transition:transform .08s,box-shadow .12s;touch-action:none;cursor:pointer}
.tc .ti{font-size:18px;line-height:1}
.tc:active,.tc.held{transform:scale(.92)}
.tc.fire{border-color:rgba(192,57,43,.9);width:72px;height:72px}.tc.fire.held{background:rgba(192,57,43,.35);box-shadow:0 0 20px rgba(192,57,43,.8)}
.tc.act{border-color:rgba(217,154,43,.85)}.tc.act.held{background:rgba(217,154,43,.3);box-shadow:0 0 16px rgba(217,154,43,.7)}
.tc.rel{border-color:rgba(94,234,212,.8)}.tc.rel.held{background:rgba(94,234,212,.25);box-shadow:0 0 16px rgba(94,234,212,.7)}
@media (pointer:coarse) and (orientation:portrait){:root{--reserve:252px}
  #touch{position:static;width:100%;max-width:560px;padding:4px 8px calc(8px + env(safe-area-inset-bottom))}}
@media (pointer:coarse) and (orientation:landscape){:root{--reserve:86px}
  .tc{width:50px;height:50px}.tc.fire{width:60px;height:60px}#stick{width:88px;height:88px}
  #topbar{padding:4px 8px}.tbtn{min-height:26px;padding:3px 7px;font-size:10px}}
#hints{flex:0 0 auto;text-align:center;font-size:10px;color:var(--dim);padding:3px 8px 7px;direction:ltr}
#hints b{color:var(--amber2)}
body.coarse #hints{display:none}
/* overlays */
.overlay{position:absolute;inset:0;z-index:30;display:grid;place-items:center;padding:12px;overflow:auto;
  background:radial-gradient(90% 90% at 50% 40%,rgba(10,8,6,.78),rgba(5,4,3,.94));scrollbar-width:thin;scrollbar-color:var(--amber) var(--surface)}
.overlay::-webkit-scrollbar{width:8px}.overlay::-webkit-scrollbar-track{background:var(--surface)}
.overlay::-webkit-scrollbar-thumb{background:linear-gradient(var(--amber),var(--warm));border-radius:4px}
[hidden]{display:none!important}
.panel{width:min(94%,430px);text-align:center;padding:18px 16px;border-radius:12px;position:relative;
  background:linear-gradient(160deg,rgba(28,20,10,.96),rgba(12,9,6,.98));border:1px solid rgba(217,154,43,.5);
  box-shadow:0 0 0 1px rgba(127,180,217,.1),0 0 34px rgba(217,154,43,.18),0 18px 44px rgba(0,0,0,.7);animation:pop .35s cubic-bezier(.2,1.4,.4,1)}
@keyframes pop{from{transform:scale(.88) translateY(12px);opacity:0}to{transform:none;opacity:1}}
.panel::before{content:"";position:absolute;inset:5px;border:1px dashed rgba(217,154,43,.2);border-radius:8px;pointer-events:none}
.bigLogo{font-family:var(--px);font-size:clamp(15px,5vw,24px);line-height:1.6;color:var(--amber);
  text-shadow:0 0 14px rgba(217,154,43,.8),3px 3px 0 rgba(127,180,217,.45);animation:flick 4s infinite}
.bigLogo b{color:var(--rain);text-shadow:0 0 14px rgba(127,180,217,.8),3px 3px 0 rgba(217,154,43,.4)}
@keyframes flick{0%,90%,100%{opacity:1}92%{opacity:.6}94%{opacity:1}96%{opacity:.75}}
.subAr{font-size:15px;font-weight:900;margin-top:6px}
.tagline{font-size:11px;color:var(--dim);margin-top:4px;line-height:1.8}
.pills{display:flex;gap:7px;justify-content:center;margin:12px 0 4px;flex-wrap:wrap}
.pill{font-weight:700;font-size:11px;padding:5px 13px;border-radius:18px;cursor:pointer;border:1px solid rgba(168,152,119,.5);background:rgba(26,19,10,.6);color:var(--dim);transition:all .15s}
.pill[aria-pressed="true"]{background:linear-gradient(90deg,rgba(217,154,43,.3),rgba(138,90,43,.3));border-color:var(--amber);color:#fff;box-shadow:0 0 12px rgba(217,154,43,.4)}
.btn{font-family:var(--ar);font-weight:900;font-size:14px;color:#fff;cursor:pointer;border-radius:10px;padding:10px 22px;margin:5px 3px 0;border:1px solid;transition:all .15s;min-width:120px}
.btn:active{transform:translateY(2px) scale(.98)}
.btn.primary{background:linear-gradient(90deg,var(--warm),var(--amber));border-color:var(--amber2);box-shadow:0 0 18px rgba(217,154,43,.5),inset 0 1px 0 rgba(255,255,255,.25)}
.btn.primary:hover{filter:brightness(1.12);box-shadow:0 0 28px rgba(217,154,43,.8)}
.btn.ghost{background:rgba(94,234,212,.07);border-color:rgba(94,234,212,.55);color:var(--cyan)}
.btn.ghost:hover{background:rgba(94,234,212,.18);box-shadow:0 0 14px rgba(94,234,212,.4)}
.btn.warn{background:rgba(192,57,43,.12);border-color:rgba(192,57,43,.6);color:#e8a79f}
.legend{margin-top:12px;font-size:10px;color:var(--dim);line-height:2;direction:ltr}
.legend b{color:var(--amber2);font-family:var(--px);font-size:7px;background:rgba(217,154,43,.12);border:1px solid rgba(217,154,43,.4);border-radius:3px;padding:2px 4px;margin:0 2px}
.statGrid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin:12px 0 4px;text-align:right}
.stat{background:rgba(26,19,10,.7);border:1px solid rgba(217,154,43,.3);border-radius:8px;padding:7px 9px}
.stat .k{font-size:9px;color:var(--dim)}.stat .v{font-family:var(--px);font-size:11px;color:var(--cyan);margin-top:4px;direction:ltr;text-align:right}
.stat.gold .v{color:var(--amber2)}
h2.ovTitle{font-family:var(--px);font-size:13px;line-height:1.7;margin-bottom:4px}
h2.ovTitle.red{color:var(--red);text-shadow:0 0 14px rgba(192,57,43,.8)}
h2.ovTitle.gold{color:var(--amber2);text-shadow:0 0 16px rgba(217,154,43,.9)}
h2.ovTitle.cyan{color:var(--cyan);text-shadow:0 0 12px rgba(94,234,212,.7)}
.ovSub{font-size:12px;font-weight:700;color:var(--dim)}
#rankGlyph{font-family:var(--px);font-size:40px;color:var(--amber);margin:6px 0;text-shadow:0 0 22px rgba(217,154,43,.9),4px 4px 0 rgba(127,180,217,.4)}
#mapList{display:flex;flex-direction:column;gap:6px;margin:12px 0;text-align:right}
.mapRow{display:flex;align-items:center;gap:8px;background:rgba(26,19,10,.7);border:1px solid rgba(168,152,119,.3);border-radius:8px;padding:7px 10px;font-size:12px;font-weight:700}
.mapRow .mi{font-size:15px}.mapRow.here{border-color:var(--cyan);box-shadow:0 0 10px rgba(94,234,212,.25)}
.mapRow.target{border-color:var(--amber);box-shadow:0 0 10px rgba(217,154,43,.3)}
.mapRow .tag{margin-right:auto;font-size:9px;color:var(--cyan)}
.mapRow.target .tag{color:var(--amber2)}
#toast{position:absolute;top:48px;left:50%;transform:translateX(-50%) translateY(-8px);z-index:25;background:rgba(5,4,3,.9);border:1px solid var(--cyan);
  border-radius:8px;padding:5px 14px;font-size:12px;font-weight:900;color:var(--cyan);opacity:0;pointer-events:none;transition:all .25s;white-space:nowrap;max-width:92%;overflow:hidden;text-overflow:ellipsis;box-shadow:0 0 16px rgba(94,234,212,.3)}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
#toast.warn{border-color:var(--amber);color:var(--amber2);box-shadow:0 0 16px rgba(217,154,43,.3)}
#toast.bad{border-color:var(--red);color:#e8a79f;box-shadow:0 0 16px rgba(192,57,43,.35)}
#toast.big{font-size:14px;padding:9px 20px;border-color:var(--amber);color:#fff;text-shadow:0 0 10px rgba(217,154,43,.8)}
.credit{margin-top:10px;font-size:8px;color:#6b5c42;font-family:var(--px);direction:ltr}
noscript{position:fixed;inset:0;display:grid;place-items:center;background:var(--bg);color:var(--ink);font-size:18px;z-index:99}
</style>
</head>
<body data-state="title">
<noscript>فعّل JavaScript لتشغيل اللعبة 🎮</noscript>
<div id="app">
  <header id="topbar">
    <div id="logo">CITY<b>▮</b>RAIN</div>
    <div id="locTag">مدينة المطر <em>// ليلة طويلة</em></div>
    <button class="tbtn" id="btnSound" data-muted="0" type="button"><span class="ic" id="sndIc">🔊</span><span id="sndTxt">الصوت</span></button>
    <button class="tbtn" id="btnMap" type="button"><span class="ic">🗺</span></button>
    <button class="tbtn" id="btnPause" type="button" disabled><span class="ic" id="pauseIc">⏸</span></button>
    <button class="tbtn" id="btnFull" type="button"><span class="ic">⛶</span></button>
  </header>
  <div id="stage">
    <div id="frame">
      <canvas id="game" width="480" height="270"></canvas>
      <div id="hud">
        <div class="hudTL">
          <div class="bar"><i id="hpFill"></i><span class="barLbl"><span>الصحة</span><span id="hpNum">100</span></span></div>
          <div id="ammoRow"><div id="ammoPips"></div><span id="resVal">40</span></div>
          <div id="relBar"><i></i></div>
        </div>
        <div class="hudTR"><div id="missionTitle">القضية</div><div id="objVal">…</div></div>
        <div id="compass"><span id="compArrow">➤</span><span id="compTxt">…</span></div>
        <div id="prompt"><b>E</b><span id="promptTxt">تفاعل</span></div>
        <div id="banner"><div class="bn" id="bnName"></div><div class="bs" id="bnSub"></div></div>
      </div>
      <div id="dlg"><div id="dlgName"></div><div id="dlgText"></div><div id="dlgHint">E / اضغط للمتابعة ▸</div></div>
      <div id="touch">
        <div id="stick"><div id="stickKnob"></div></div>
        <div class="tgroup">
          <button class="tc rel" id="btnRel" type="button"><span class="ti">↻</span>تلقيم</button>
          <button class="tc act" id="btnAct" type="button"><span class="ti">✋</span>تفاعل</button>
          <button class="tc fire" id="btnFire" type="button"><span class="ti">◎</span>نار</button>
        </div>
      </div>
      <div id="toast"></div>
      <div class="overlay" id="ovTitle">
        <div class="panel">
          <div class="bigLogo">CITY OF<br><b>RAIN</b></div>
          <div class="subAr">مدينة المطر — قضية هنري</div>
          <div class="tagline">عالم مفتوح تحت المطر: شقة، حانة، عيادة، مستودع، سطح.<br>تحديات، أدلة، وضرب نار في أزقة لا تنام.</div>
          <div class="pills" id="diffPills">
            <button class="pill" data-d="0" type="button" aria-pressed="false">هادئ</button>
            <button class="pill" data-d="1" type="button" aria-pressed="true">عادي</button>
            <button class="pill" data-d="2" type="button" aria-pressed="false">قاتل</button>
          </div>
          <button class="btn primary" id="btnStart" type="button">▶ ابدأ الليلة</button>
          <div class="legend" id="legendDesk"><b>A/D</b> حركة <b>W/S</b> تصويب <b>J</b> نار <b>E</b> تفاعل <b>R</b> تلقيم <b>M</b> خريطة</div>
          <div class="legend" id="legendTouch" hidden>عصا يسار للحركة والتصويب • ◎ نار • ✋ تفاعل • ↻ تلقيم</div>
          <div class="credit">NOIR OPEN WORLD // v1.0</div>
        </div>
      </div>
      <div class="overlay" id="ovPause" hidden>
        <div class="panel">
          <h2 class="ovTitle cyan">PAUSED</h2><div class="ovSub">المطر لن ينتظر</div>
          <div style="margin-top:10px">
            <button class="btn primary" id="btnResume" type="button">▶ استئناف</button><br>
            <button class="btn warn" id="btnRetryP" type="button">↺ نقطة الحفظ</button>
            <button class="btn ghost" id="btnMapP" type="button">🗺 الخريطة</button>
            <button class="btn ghost" id="btnMenuP" type="button">القائمة</button>
          </div>
        </div>
      </div>
      <div class="overlay" id="ovMap" hidden>
        <div class="panel">
          <h2 class="ovTitle gold">DISTRICT MAP</h2><div class="ovSub">خريطة الحي — أنت والهدف</div>
          <div id="mapList"></div>
          <button class="btn primary" id="btnMapClose" type="button">إغلاق</button>
        </div>
      </div>
      <div class="overlay" id="ovDead" hidden>
        <div class="panel">
          <h2 class="ovTitle red">THE NIGHT ENDS</h2><div class="ovSub">سقطت تحت المطر…</div>
          <div class="statGrid">
            <div class="stat gold"><div class="k">القتلى</div><div class="v" id="dKills">0</div></div>
            <div class="stat"><div class="k">الدقة</div><div class="v" id="dAcc">0%</div></div>
          </div>
          <button class="btn primary" id="btnRetry" type="button">↺ انهض مجدداً</button>
          <button class="btn ghost" id="btnMenuD" type="button">القائمة</button>
        </div>
      </div>
      <div class="overlay" id="ovWin" hidden>
        <div class="panel">
          <h2 class="ovTitle gold">CASE CLOSED ★</h2><div class="ovSub">أُغلقت القضية… والمدينة ما زالت تمطر</div>
          <div id="rankGlyph">S</div>
          <div class="statGrid">
            <div class="stat"><div class="k">الوقت</div><div class="v" id="wTime">0s</div></div>
            <div class="stat"><div class="k">القتلى</div><div class="v" id="wKills">0</div></div>
            <div class="stat"><div class="k">الدقة</div><div class="v" id="wAcc">0%</div></div>
            <div class="stat gold"><div class="k">تحدي القوارير</div><div class="v" id="wBottles">0/3</div></div>
          </div>
          <button class="btn primary" id="btnRoam" type="button">🌧 تجول بحرية</button>
          <button class="btn ghost" id="btnMenuW" type="button">القائمة</button>
        </div>
      </div>
    </div>
    <div id="hints"><b>A/D</b> حركة • <b>W/S</b> تصويب • <b>J/Space</b> نار • <b>E</b> تفاعل • <b>R</b> تلقيم • <b>M</b> خريطة • <b>P</b> إيقاف</div>
  </div>
</div>
<script>
(function(){
'use strict';
var VW=480,VH=270,FLOOR=214,STEP=1/60;
var cv=$('game'),ctx=cv.getContext('2d');ctx.imageSmoothingEnabled=false;
function $(id){return document.getElementById(id)}
function clamp(v,a,b){return v<a?a:v>b?b:v}
function lerp(a,b,t){return a+(b-a)*t}
function rnd(a,b){return a+Math.random()*(b-a)}
function sgn(v){return v<0?-1:v>0?1:0}
function rgba(h,a){var n=parseInt(h.slice(1),16);return'rgba('+((n>>16)&255)+','+((n>>8)&255)+','+(n&255)+','+a+')'}
function mkC(w,h){var c=document.createElement('canvas');c.width=Math.ceil(w);c.height=Math.ceil(h);var x=c.getContext('2d');x.imageSmoothingEnabled=false;return[c,x]}
function mtof(m){return 440*Math.pow(2,(m-69)/12)}
function LSg(k,d){try{var v=localStorage.getItem(k);return v===null?d:v}catch(e){return d}}
function LSs(k,v){try{localStorage.setItem(k,v)}catch(e){}}
var FONT={A:[2,5,7,5,5],B:[6,5,6,5,6],C:[3,4,4,4,3],D:[6,5,5,5,6],E:[7,4,6,4,7],F:[7,4,6,4,4],G:[3,4,5,5,3],H:[5,5,7,5,5],I:[7,2,2,2,7],J:[1,1,1,5,2],K:[5,5,6,5,5],L:[4,4,4,4,7],M:[7,7,5,5,5],N:[6,5,5,5,5],O:[2,5,5,5,2],P:[6,5,6,4,4],Q:[2,5,5,2,1],R:[6,5,6,5,5],S:[3,4,2,1,6],T:[7,2,2,2,2],U:[5,5,5,5,7],V:[5,5,5,5,2],W:[5,5,5,7,5],X:[5,5,2,5,5],Y:[5,5,2,2,2],Z:[7,1,2,4,7],'0':[7,5,5,5,7],'1':[2,6,2,2,7],'2':[6,1,2,4,7],'3':[7,1,3,1,7],'4':[5,5,7,1,1],'5':[7,4,6,1,6],'6':[3,4,7,5,7],'7':[7,1,2,2,2],'8':[7,5,7,5,7],'9':[7,5,7,1,6],'-':[0,0,7,0,0],'+':[0,2,7,2,0],'.':[0,0,0,0,2],':':[0,2,0,2,0],'/':[1,1,2,4,4],'!':[2,2,2,0,2],'>':[4,2,1,2,4],' ':[0,0,0,0,0],'%':[5,1,2,4,5]};
function pT(c,s,x,y,col,sc){sc=sc||1;c.fillStyle=col;for(var i=0;i<s.length;i++){var g=FONT[String(s[i]).toUpperCase()];if(!g)continue;for(var r=0;r<5;r++)for(var b=0;b<3;b++)if(g[r]&(4>>b))c.fillRect(x+i*4*sc+b*sc,y+r*sc,sc,sc)}}
function pW(s,sc){return s.length*4*(sc||1)-(sc||1)}
function glow(c,x,y,r,col,a){if(!(r>0))return;var g=c.createRadialGradient(x,y,0,x,y,r);g.addColorStop(0,rgba(col,a));g.addColorStop(1,rgba(col,0));c.fillStyle=g;c.fillRect(x-r,y-r,r*2,r*2)}
/* ---------- AUDIO ---------- */
var AC=null,master,musG,sfxG,ambG,rainG,nBuf,dly,muted=LSg('cr_mute','0')==='1';
var nNote=0,sIdx=0,BPM=76,SPB=60/BPM,combatMus=0;
var CH=[[50,53,57,64],[46,50,53,57],[43,46,50,53],[45,49,52,58]];
var LEAD=[{s:4,m:69},{s:12,m:72},{s:20,m:74},{s:28,m:72},{s:36,m:69},{s:44,m:65},{s:52,m:64},{s:60,m:62}];
function initAudio(){if(AC)return;try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){return}
 var cp=AC.createDynamicsCompressor();cp.threshold.value=-16;cp.ratio.value=4;cp.connect(AC.destination);
 master=AC.createGain();master.gain.value=muted?0:1;master.connect(cp);
 musG=AC.createGain();musG.gain.value=.42;musG.connect(master);
 sfxG=AC.createGain();sfxG.gain.value=.95;sfxG.connect(master);
 ambG=AC.createGain();ambG.gain.value=.5;ambG.connect(master);
 nBuf=AC.createBuffer(1,AC.sampleRate*2,AC.sampleRate);var d=nBuf.getChannelData(0);for(var i=0;i<d.length;i++)d[i]=Math.random()*2-1;
 dly=AC.createDelay(1);dly.delayTime.value=SPB*.66;var fb=AC.createGain();fb.gain.value=.3;dly.connect(fb);fb.connect(dly);dly.connect(musG);
 var rs=AC.createBufferSource();rs.buffer=nBuf;rs.loop=true;var lp=AC.createBiquadFilter();lp.type='lowpass';lp.frequency.value=1500;
 var hp=AC.createBiquadFilter();hp.type='highpass';hp.frequency.value=400;rainG=AC.createGain();rainG.gain.value=.4;
 rs.connect(lp);lp.connect(hp);hp.connect(rainG);rainG.connect(ambG);rs.start();
 nNote=AC.currentTime+.1;sIdx=0;setInterval(schedMus,25)}
function schedMus(){if(!AC)return;while(nNote<AC.currentTime+.14){stepMus(sIdx,nNote);sIdx=(sIdx+1)%64;nNote+=SPB/4}}
function stepMus(st,t){var bar=Math.floor(st/16)%4,s=st%16,ch=CH[bar],i;
 if(s===0||s===6||s===8||s===14){var bm=[ch[0]-12,ch[0]-5,ch[0]-9,ch[0]-12][[0,1,2,3].indexOf([0,6,8,14].indexOf(s))];
  var o=AC.createOscillator();o.type='triangle';o.frequency.value=mtof(bm);var g=AC.createGain();
  g.gain.setValueAtTime(.0001,t);g.gain.exponentialRampToValueAtTime(.22,t+.02);g.gain.exponentialRampToValueAtTime(.001,t+SPB*.6);
  o.connect(g);g.connect(musG);o.start(t);o.stop(t+SPB*.7)}
 if(s%2===1){var h=AC.createBufferSource();h.buffer=nBuf;var hf=AC.createBiquadFilter();hf.type='highpass';hf.frequency.value=8000;
  var hg=AC.createGain();hg.gain.setValueAtTime(.045,t);hg.gain.exponentialRampToValueAtTime(.001,t+.05);
  h.connect(hf);hf.connect(hg);hg.connect(musG);h.start(t);h.stop(t+.06)}
 if(s===0){for(i=0;i<4;i++){var o2=AC.createOscillator();o2.type='triangle';o2.frequency.value=mtof(ch[i]);o2.detune.value=(i-1)*4;
  var g2=AC.createGain();g2.gain.setValueAtTime(.0001,t);g2.gain.linearRampToValueAtTime(.035,t+.04);g2.gain.exponentialRampToValueAtTime(.001,t+SPB*3.4);
  o2.connect(g2);g2.connect(musG);g2.connect(dly);o2.start(t);o2.stop(t+SPB*3.5)}}
 for(i=0;i<LEAD.length;i++)if(LEAD[i].s===st){var o3=AC.createOscillator();o3.type='sawtooth';o3.frequency.value=mtof(LEAD[i].m);
  var f3=AC.createBiquadFilter();f3.type='lowpass';f3.frequency.value=1100;var g3=AC.createGain();
  g3.gain.setValueAtTime(.0001,t);g3.gain.linearRampToValueAtTime(.05,t+.06);g3.gain.exponentialRampToValueAtTime(.001,t+.7);
  o3.connect(f3);f3.connect(g3);g3.connect(musG);g3.connect(dly);o3.start(t);o3.stop(t+.75)}
 if(combatMus>0){if(s%4===0){var k=AC.createOscillator();k.type='sine';k.frequency.setValueAtTime(95,t);k.frequency.exponentialRampToValueAtTime(38,t+.1);
  var kg=AC.createGain();kg.gain.setValueAtTime(.3,t);kg.gain.exponentialRampToValueAtTime(.001,t+.12);k.connect(kg);kg.connect(musG);k.start(t);k.stop(t+.14)}
  if(s%2===0){var b=AC.createOscillator();b.type='square';b.frequency.value=mtof(ch[0]-12);var bf=AC.createBiquadFilter();bf.type='lowpass';bf.frequency.value=400;
   var bg=AC.createGain();bg.gain.setValueAtTime(.0001,t);bg.gain.exponentialRampToValueAtTime(.09,t+.01);bg.gain.exponentialRampToValueAtTime(.001,t+.12);
   b.connect(bf);bf.connect(bg);bg.connect(musG);b.start(t);b.stop(t+.14)}}}
function tone(f0,f1,d,ty,v,at){if(!AC)return;var t=AC.currentTime+(at||0);var o=AC.createOscillator();o.type=ty||'square';
 o.frequency.setValueAtTime(Math.max(1,f0),t);o.frequency.exponentialRampToValueAtTime(Math.max(1,f1),t+d);
 var g=AC.createGain();g.gain.setValueAtTime(.0001,t);g.gain.exponentialRampToValueAtTime(v,t+.008);g.gain.exponentialRampToValueAtTime(.0001,t+d);
 o.connect(g);g.connect(sfxG);o.start(t);o.stop(t+d+.02)}
function nz(d,v,ft,f0,f1,at){if(!AC)return;var t=AC.currentTime+(at||0);var s=AC.createBufferSource();s.buffer=nBuf;s.loop=true;
 var f=AC.createBiquadFilter();f.type=ft;f.frequency.setValueAtTime(f0,t);if(f1)f.frequency.exponentialRampToValueAtTime(Math.max(20,f1),t+d);
 var g=AC.createGain();g.gain.setValueAtTime(.0001,t);g.gain.exponentialRampToValueAtTime(v,t+.01);g.gain.exponentialRampToValueAtTime(.0001,t+d);
 s.connect(f);f.connect(g);g.connect(sfxG);s.start(t);s.stop(t+d+.02)}
var sfx={
 shot:function(){nz(.12,.5,'lowpass',4200,380);tone(170,48,.09,'sine',.4);nz(.02,.15,'highpass',3000)},
 eshot:function(){nz(.1,.3,'lowpass',3000,300);tone(130,42,.08,'sine',.25)},
 shotgun:function(){nz(.2,.55,'lowpass',3500,200);tone(110,35,.14,'sine',.45)},
 ric:function(){tone(2400,1100,.06,'square',.1)},
 flesh:function(){nz(.06,.25,'lowpass',650);tone(95,40,.06,'sine',.2)},
 rel:function(){tone(900,900,.03,'square',.12);tone(620,620,.03,'square',.12,.45);tone(1100,1100,.03,'square',.1,.9)},
 empty:function(){tone(300,200,.04,'square',.1)},
 door:function(){tone(180,110,.2,'triangle',.14);nz(.12,.08,'lowpass',320)},
 pick:function(){tone(700,1050,.07,'square',.12)},
 phone:function(){tone(1250,1250,.09,'sine',.14);tone(1550,1550,.09,'sine',.14,.12)},
 blip:function(){tone(520,520,.02,'square',.05)},
 sting:function(){[392,466,587,784].forEach(function(f,i){tone(f,f,.13,'triangle',.14,i*.1)})},
 death:function(){tone(210,30,.7,'sawtooth',.3);nz(.5,.2,'lowpass',700,120)},
 boss:function(){tone(72,44,.55,'sawtooth',.35);tone(75,46,.55,'sawtooth',.25)},
 foot:function(){nz(.015,.03,'highpass',2200)},
 melee:function(){nz(.08,.22,'bandpass',900)},
 bottle:function(){tone(1800,900,.08,'triangle',.14);nz(.06,.12,'highpass',4000)},
 ui:function(){tone(700,700,.04,'square',.08)}};
function setMuted(m){muted=m;LSs('cr_mute',m?'1':'0');if(AC&&master)master.gain.linearRampToValueAtTime(m?0:1,AC.currentTime+.15);
 $('btnSound').dataset.muted=m?'1':'0';$('sndIc').textContent=m?'🔇':'🔊';$('sndTxt').textContent=m?'صامت':'الصوت'}
function unlock(){initAudio();if(AC&&AC.state==='suspended')AC.resume()}
/* ---------- STATE ---------- */
var DIFF=[{dmg:.65,fire:1.35},{dmg:1,fire:1},{dmg:1.4,fire:.72}];
var S={state:'title',diff:clamp(parseInt(LSg('cr_diff','1'),10)||1,0,2),loc:'street',cam:0,t:0,shakeT:0,shakeM:0,hurtF:0,
 freeze:0,slowT:0,ts:1,fade:0,fadeTo:null,fadeX:0,lightT:rnd(12,24),lightF:0,deadT:0,
 kills:0,shots:0,hits:0,bottles:0,startTime:0,elapsed:0,deaths:0};
var P={x:120,y:FLOOR,vx:0,face:1,hp:100,mag:8,res:40,relT:0,fireCd:0,meleeCd:0,ifr:0,aim:0,anim:0,stepT:0,dead:false,muzzle:0,walk:0};
var M={idx:0,step:0,ambushDone:false,whClear:false,clClear:false};
var deadKeys={},takenKeys={},corpses={},bottleDead={};
var input={mx:0,aim:0,fire:false,act:false,rel:false};
var coarse=matchMedia('(pointer:coarse)').matches||('ontouchstart'in window);
if(coarse)document.body.classList.add('coarse');
$('legendDesk').hidden=coarse;$('legendTouch').hidden=!coarse;
var bullets=[],parts=[],floats=[],rain=[],splashes=[];
for(var i=0;i<110;i++)rain.push({x:rnd(0,VW),y:rnd(0,VH),v:rnd(430,560)});
var dlgQ=[],dlgI=0,dlgChar=0,dlgT=0,dlgOn=false;
/* ---------- LOCATIONS ---------- */
var LOCS={};
function door(x,to,tx,label){return{x:x,to:to,tx:tx,label:label}}
function buildLocs(){
 LOCS.street={id:'street',name:'الشارع الرئيسي',sub:'MAIN STREET — RAIN',w:2500,out:true,
  doors:[door(260,'apartment',70,'شقة هنري'),door(820,'bar',70,'حانة سال'),door(1380,'clinic',70,'العيادة'),door(1900,'warehouse',70,'المستودع'),door(2280,'alley',60,'الزقاق')],
  enemies:[],items:[],npcs:[]};
 LOCS.apartment={id:'apartment',name:'شقة هنري',sub:"HENRI'S APARTMENT",w:700,out:false,
  doors:[door(40,'street',260,'الخروج للشارع')],enemies:[],items:[],npcs:[]};
 LOCS.bar={id:'bar',name:'حانة سال',sub:"SAL'S BAR",w:800,out:false,
  doors:[door(40,'street',820,'الخروج للشارع')],enemies:[],items:[],npcs:[{x:520,name:'سال'}]};
 LOCS.clinic={id:'clinic',name:'العيادة',sub:'NIGHT CLINIC',w:620,out:false,
  doors:[door(40,'street',1380,'الخروج للشارع')],enemies:[],items:[],npcs:[]};
 LOCS.warehouse={id:'warehouse',name:'المستودع',sub:'PIER 9 WAREHOUSE',w:1000,out:false,
  doors:[door(40,'street',1900,'الخروج للشارع')],enemies:[],items:[],npcs:[]};
 LOCS.alley={id:'alley',name:'الزقاق',sub:'BACK ALLEY',w:500,out:true,
  doors:[door(40,'street',2280,'الشارع'),door(380,'rooftop',80,'سلّم الحريق ▲')],enemies:[],items:[],npcs:[]};
 LOCS.rooftop={id:'rooftop',name:'السطح',sub:'ROOFTOP — FINALE',w:720,out:true,
  doors:[door(60,'alley',360,'نزول ▼')],enemies:[],items:[],npcs:[]};
}
function loc(){return LOCS[S.loc]}
function eKey(l,id){return l+':'+id}
function spawnFor(l){
 var L=LOCS[l];L.enemies=[];L.items=[];
 function en(id,type,x,hp){if(deadKeys[eKey(l,id)])return;L.enemies.push({id:id,type:type,x:x,y:FLOOR,hp:hp,max:hp,face:-1,face0:-1,
  state:'patrol',stT:rnd(.5,2),fireT:rnd(1,2),wind:0,burst:0,burstT:0,flash:0,dead:false,alert:false,b0:x-70,b1:x+70,anim:rnd(0,9),vx:0,phase:1,p2:false,p3:false,spawnT:5})}
 function it(id,type,x){if(takenKeys[eKey(l,id)])return;L.items.push({id:id,type:type,x:x,y:FLOOR-8,taken:false})}
 if(l==='street'&&M.idx===1&&M.step===1&&!M.ambushDone){en('a1','gun',980,40);en('a2','gun',1120,40);en('a3','shot',1240,55)}
 if(l==='warehouse'&&M.idx===2){en('w1','gun',380,40);en('w2','gun',540,40);en('w3','shot',680,55);en('w4','gun',800,40);en('w5','gun',900,40);
  if(M.whClear)it('ledger','ledger',930)}
 if(l==='clinic'&&M.idx===3){en('c1','gun',300,40);en('c2','shot',420,55);en('c3','gun',520,40);it('file','file',560)}
 if(l==='rooftop'&&M.idx===4){en('boss','boss',540,320)}
 if(l==='apartment'){it('ammoA','ammo',180);it('medA','med',560)}
 if(l==='bar'){it('ammoB','ammo',660)}
 if(l==='clinic'){it('ammoC','ammo',200);it('medC','med',250)}
 if(l==='warehouse'){it('ammoW','ammo',240)}
 if(l==='alley'){it('ammoAl','ammo',200)}
}
function enterLoc(l,x,silent){
 S.loc=l;spawnFor(l);P.x=x;P.y=FLOOR;P.vx=0;P.face=1;bullets=[];parts=[];floats=[];splashes=[];
 S.cam=clamp(P.x-VW/2,0,LOCS[l].w-VW);
 $('locTag').innerHTML=LOCS[l].name+' <em>// '+LOCS[l].sub+'</em>';
 if(!silent){banner(LOCS[l].name,LOCS[l].sub);sfx.door()}
 if(AC&&rainG)rainG.gain.linearRampToValueAtTime(LOCS[l].out?.4:.07,AC.currentTime+.6);
 updateHUD();
}
/* ---------- MISSIONS ---------- */
function missionInfo(){
 if(M.idx===0)return{title:'١ • المكالمة',obj:'ادخل شقة هنري وافحص الهاتف',loc:'apartment',x:300};
 if(M.idx===1)return M.step===0?{title:'٢ • المُخبر',obj:'قابل سال في الحانة',loc:'bar',x:520}:
  {title:'٢ • الكمين',obj:'انجُ من الكمين في الشارع',loc:'street',x:1100};
 if(M.idx===2)return{title:'٣ • الدفتر الأسود',obj:M.whClear?'خذ الدفتر من آخر المستودع':'طهّر المستودع ('+killCount('warehouse')+'/5)',loc:'warehouse',x:M.whClear?930:640};
 if(M.idx===3)return{title:'٤ • الشاهد',obj:'اجلب ملف الشاهد من العيادة',loc:'clinic',x:560};
 if(M.idx===4)return{title:'٥ • الحساب الأخير',obj:'اصعد للسطح واقضِ على «الحلاق»',loc:'rooftop',x:540};
 return{title:'قضية مغلقة',obj:'تجول بحرية في مدينة المطر',loc:S.loc,x:P.x};
}
function killCount(l){var n=0;for(var k in deadKeys)if(k.indexOf(l+':')===0&&k.indexOf('boss')<0)n++;return n}
function targetDoor(){
 var mi=missionInfo();if(mi.loc===S.loc)return null;
 var L=loc();
 if(S.loc==='street'){var want=mi.loc==='rooftop'?'alley':mi.loc;
  for(var i=0;i<L.doors.length;i++)if(L.doors[i].to===want)return L.doors[i];return L.doors[0]}
 if(S.loc==='alley'&&mi.loc==='rooftop')return L.doors[1];
 return L.doors[0];
}
function advanceMission(){}
function checkMission(){
 if(M.idx===1&&M.step===1&&!M.ambushDone){
  var alive=LOCS.street.enemies.some(function(e){return!e.dead&&e.id[0]==='a'});
  if(!alive&&S.loc==='street'){M.ambushDone=true;M.idx=2;toast('✔ نجوت من الكمين — Richtung المستودع','big');toast('✔ نجوت!下一步: المستودع','big');sfx.sting()}}
 if(M.idx===2&&!M.whClear){var a2=LOCS.warehouse.enemies.some(function(e){return!e.dead});
  if(!a2&&S.loc==='warehouse'){M.whClear=true;spawnFor('warehouse');toast('✔ المستودع نظيف — الدفتر في الآخر','big');sfx.sting()}}
}
/* ---------- DIALOGUE ---------- */
function say(name,lines,cb){dlgQ=lines;dlgI=0;dlgChar=0;dlgT=0;dlgOn=true;dlgCB=cb||null;
 $('dlgName').textContent=name;$('dlgText').textContent='';$('dlg').classList.add('on')}
var dlgCB=null;
function dlgNext(){if(!dlgOn)return;
 if(dlgChar<dlgQ[dlgI].length){dlgChar=dlgQ[dlgI].length;$('dlgText').textContent=dlgQ[dlgI];return}
 dlgI++;dlgChar=0;
 if(dlgI>=dlgQ.length){dlgOn=false;$('dlg').classList.remove('on');var cb=dlgCB;dlgCB=null;if(cb)cb()}
 else{$('dlgText').textContent='';sfx.blip()}}
function updDlg(dt){if(!dlgOn)return;dlgT+=dt;
 if(dlgChar<dlgQ[dlgI].length){dlgChar=Math.min(dlgQ[dlgI].length,dlgChar+dt*40);
  $('dlgText').textContent=dlgQ[dlgI].slice(0,Math.floor(dlgChar));
  if(Math.floor(dlgChar)%3===0)sfx.blip()}}
/* ---------- INTERACT ---------- */
function nearestInteract(){
 var L=loc(),best=null,bd=26;
 L.doors.forEach(function(d){var dx=Math.abs(P.x-d.x);if(dx<bd){bd=dx;best={kind:'door',o:d,label:d.label}}});
 L.npcs.forEach(function(n){if(M.idx===1&&M.step===0&&n.name==='سال'){var dx=Math.abs(P.x-n.x);if(dx<bd){bd=dx;best={kind:'npc',o:n,label:'تحدث مع سال'}}});
 L.items.forEach(function(it){if(it.taken)return;var dx=Math.abs(P.x-it.x);if(dx<bd){bd=dx;
  var lb=it.type==='ammo'?'خذ ذخيرة':it.type==='med'?'حقيبة إسعاف':it.type==='ledger'?'خذ الدفتر الأسود':it.type==='file'?'خذ ملف الشاهد':'افحص';
  best={kind:'item',o:it,label:lb}}});
 if(S.loc==='apartment'&&M.idx===0){var dx2=Math.abs(P.x-300);if(dx2<bd){bd=dx2;best={kind:'phone',label:'افحص الهاتف'}}
 if(S.loc==='alley'){for(var b=0;b<3;b++)if(!bottleDead[b]){}}
 return best;
}
function doInteract(){
 if(dlgOn){dlgNext();return}
 var n=nearestInteract();if(!n){return}
 if(n.kind==='door'){sfx.door();S.fadeTo=n.o.to;S.fadeX=n.o.tx;S.fade=1;return}
 if(n.kind==='npc'){sfx.blip();say('سال',['المطر لا يغسل هذه المدينة يا هنري.','«الحلاق» يدير كل شيء من سطح البرج… والدفتر في مستودع الرصيف ٩.','خذ هذا. ستحتاجه أكثر مني.'],function(){P.res=Math.min(96,P.res+24);M.idx=1;M.step=1;spawnFor('street');toast('⚠ كمين في الشارع!','bad');sfx.boss();updateHUD()});return}
 if(n.kind==='phone'){sfx.phone();say('الهاتف',['«هنري… إن كنت تسمع هذا، فقد بدأوا بالفعل.»','«الدفتر الأسود في المستودع. لا تثق بأحد تحت المطر.»','انقطع الخط. بقيت نغمة واحدة… ثم الصمت.'],function(){M.idx=1;M.step=0;sfx.sting();toast('✔ دليل جديد: حانة سال','big');updateHUD()});return}
 if(n.kind==='item'){var it=n.o;it.taken=true;takenKeys[eKey(S.loc,it.id)]=true;sfx.pick();
  if(it.type==='ammo'){P.res=Math.min(96,P.res+20);floatTxt(it.x,it.y-14,'+20 ذخيرة','#ffcf6e')}
  else if(it.type==='med'){P.hp=Math.min(100,P.hp+35);floatTxt(it.x,it.y-14,'+35 صحة','#7fb069')}
  else if(it.type==='ledger'){say('الدفتر الأسود',['أسماء، تواريخ، مبالغ… كل قذر في المدينة مكتوب هنا.','اسم واحد circled ثلاث مرات: «الحلاق». السطح. الليلة.'],function(){M.idx=3;sfx.sting();toast('✔ الدفتر معك — العيادة التالية','big');updateHUD()})}
  else if(it.type==='file'){say('ملف الشاهد',['الشاهد رأى الحلاق يطلق النار على الصحفي في الزقاق.','وقّع الشهادة… ثم اختفى. الملف يكفي لإسقاطه.'],function(){M.idx=4;sfx.sting();toast('✔ القضية اكتملت — اصعد للسطح','big');updateHUD()})}
  updateHUD();return}
}
/* ---------- COMBAT ---------- */
function pBox(){return{x:P.x-6,y:P.y-32,w:12,h:32}}
function eBox(e){return e.type==='boss'?{x:e.x-14,y:e.y-40,w:28,h:40}:{x:e.x-6,y:e.y-30,w:12,h:30}}
function hit(b,x,y,r){return x+r>b.x&&x-r<b.x+b.w&&y+r>b.y&&y-r<b.y+b.h}
function floatTxt(x,y,s,c){floats.push({x:x,y:y,s:s,c:c||'#f2e9d8',life:.9,max:.9})}
function spark(x,y,c,n,sp){for(var i=0;i<n;i++){var a=rnd(0,6.28),v=rnd(20,sp||120);parts.push({t:'s',x:x,y:y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-30,life:rnd(.15,.4),max:.4,c:c,sz:rnd(1,2.2)})}}
function blood(x,y,n){for(var i=0;i<n;i++)parts.push({t:'b',x:x,y:y,vx:rnd(-90,90),vy:rnd(-140,-20),life:rnd(.3,.7),max:.7,c:'#8e1f1f',sz:rnd(1,2.5)})}
function shell(x,y,f){parts.push({t:'c',x:x,y:y,vx:-f*rnd(40,80),vy:-rnd(60,110),life:.6,max:.6,c:'#d99a2b',sz:1.5})}
function shake(t,m){S.shakeT=Math.max(S.shakeT,t);S.shakeM=Math.max(S.shakeM,m)}
function muzzle(x,y){parts.push({t:'f',x:x,y:y,life:.06,max:.06,c:'#ffcf6e',sz:26})}
function firePlayer(){
 if(P.relT>0||P.fireCd>0||P.dead)return;
 if(P.mag<=0){if(P.res>0)startRel();else{melee();}return}
 P.mag--;P.fireCd=.2;P.muzzle=.06;S.shots++;
 var gy=P.y-20,aimY=P.aim*0.5,best=null,bd=1e9,L=loc();
 for(var i=0;i<L.enemies.length;i++){var e=L.enemies[i];if(e.dead)continue;
  var ex=e.x-P.x,ey=(e.y-18)-gy;
  if(ex*P.face>0&&Math.abs(ex)<320&&Math.abs(ey)<90){var d=Math.abs(ex);if(d<bd){bd=d;best=e}}}
 var dx=P.face,dy=aimY;
 if(best){var tx=best.x-P.x,ty=(best.y-18)-gy,tl=Math.hypot(tx,ty)||1;dx=tx/tl;dy=ty/tl}
 var l=Math.hypot(dx,dy)||1;dx/=l;dy/=l;
 bullets.push({x:P.x+P.face*10,y:gy,vx:dx*540,vy:dy*540,life:.8,from:'p',dmg:20});
 muzzle(P.x+P.face*12,gy);shell(P.x,P.y-22,P.face);sfx.shot();shake(.08,2);P.vx-=P.face*10;
 updateHUD();
}
function melee(){if(P.meleeCd>0)return;P.meleeCd=.45;sfx.melee();spark(P.x+P.face*14,P.y-18,'#a89877',4,70);
 var L=loc();for(var i=0;i<L.enemies.length;i++){var e=L.enemies[i];
  if(!e.dead&&Math.abs(e.x-P.x)<26&&sgn(e.x-P.x)===P.face){hurtEnemy(e,25)}}}
function startRel(){if(P.relT>0||P.mag>=8||P.res<=0)return;P.relT=1.05;sfx.rel();$('relBar').classList.add('on')}
function hurtEnemy(e,dmg){
 e.hp-=dmg;e.flash=.08;e.alert=true;blood(e.x,e.y-18,6);sfx.flesh();S.hits++;
 if(e.hp<=0&&!e.dead)killEnemy(e);
}
function killEnemy(e){
 e.dead=true;deadKeys[eKey(S.loc,e.id)]=true;S.kills++;
 (corpses[S.loc]=corpses[S.loc]||[]).push({x:e.x,y:e.y,type:e.type,face:e.face});
 blood(e.x,e.y-16,12);spark(e.x,e.y-16,'#ffcf6e',5,90);sfx.death();shake(.18,3);S.freeze=Math.max(S.freeze,.04);
 if(Math.random()<.4)loc().items.push({id:'drop'+Math.random(),type:'ammo',x:e.x+rnd(-8,8),y:FLOOR-8,taken:false});
 if(Math.random()<.15)loc().items.push({id:'dropM'+Math.random(),type:'med',x:e.x+rnd(-8,8),y:FLOOR-8,taken:false});
 if(e.type==='boss'){bossDown(e)}
 checkMission();updateHUD();
}
function bossDown(e){
 S.slowT=1;S.ts=.3;shake(.6,7);sfx.boss();
 say('الحلاق',['كنت تظن أن المطر يغسل الأسماء؟','الدفتر… الشهادة… أنت. كلها تختفي الليلة.','…ربما ليس تحت هذا المطر.'],function(){winGame()});
}
function hurtPlayer(dmg,dir){
 if(P.ifr>0||P.dead)return;dmg=Math.round(dmg*DIFF[S.diff].dmg);
 P.hp-=dmg;P.ifr=.7;P.vx=dir*130;S.hurtF=1;shake(.25,4);sfx.flesh();blood(P.x,P.y-18,8);
 if(P.hp<=0){P.hp=0;P.dead=true;S.deadT=1.1;S.slowT=.9;S.ts=.3;S.deaths++;sfx.death();blood(P.x,P.y-16,16)}
 updateHUD();
}
/* ---------- ENEMY AI ---------- */
function updEnemies(dt){
 var L=loc(),dm=DIFF[S.diff];combatMus=Math.max(0,combatMus-dt);
 for(var i=0;i<L.enemies.length;i++){var e=L.enemies[i];if(e.dead)continue;
  e.flash=Math.max(0,e.flash-dt);e.anim+=dt*6;
  var dx=P.x-e.x,dist=Math.abs(dx);
  if(!P.dead&&dist<280){if(!e.alert){e.alert=true;floatTxt(e.x,e.y-38,'!','#c0392b');sfx.blip()}combatMus=2}
  if(e.type==='boss'){updBoss(e,dt,dm);continue}
  if(e.alert&&!P.dead){
   e.face=sgn(dx)||e.face;
   var want=dist>(e.type==='shot'?110:190)?1:dist<(e.type==='shot'?60:120)?-1:0;
   e.x+=e.face*want*45*dt;
   if(e.wind>0){e.wind-=dt;if(e.wind<=0){
    if(e.type==='shot'){for(var s=-1;s<=1;s++){var a=s*.14;bullets.push({x:e.x+e.face*10,y:e.y-20,vx:Math.cos(a)*e.face*250,vy:Math.sin(a)*250,life:1.4,from:'e',dmg:9})}sfx.shotgun()}
    else{var n=e.burst;for(var b=0;b<n;b++)(function(b){setTimeout(function(){if(!e.dead&&!P.dead&&S.state==='playing'){
      var ddx=P.x-e.x,ddy=(P.y-18)-(e.y-20),ll=Math.hypot(ddx,ddy)||1;
      bullets.push({x:e.x+e.face*10,y:e.y-20,vx:ddx/ll*270*dm.fire,vy:ddy/ll*270*dm.fire,life:1.6,from:'e',dmg:8});sfx.eshot()}},b*140)})(b)}
    muzzle(e.x+e.face*12,e.y-20);shake(.06,1.5)}}
   else{e.fireT-=dt;if(e.fireT<=0){e.wind=.35;e.burst=e.type==='shot'?1:2;e.fireT=(e.type==='shot'?2.2:1.6)*dm.fire+rnd(0,.5)}}
  }else{e.x+=e.face*22*dt;if(e.x<e.b0)e.face=1;if(e.x>e.b1)e.face=-1}
  e.x=clamp(e.x,16,L.w-16);
  if(!P.dead&&P.ifr<=0&&hit(eBox(e),P.x,P.y-16,6))hurtPlayer(10,sgn(dx)||1);
 }
}
function updBoss(e,dt,dm){
 var dx=P.x-e.x;e.face=sgn(dx)||e.face;
 if(e.hp<e.max*.66&&!e.p2){e.p2=true;e.phase=2;sfx.boss();toast('⚠ الحلاق غاضب!','bad')}
 if(e.hp<e.max*.33&&!e.p3){e.p3=true;e.phase=3;sfx.boss();toast('🔥 المرحلة الأخيرة!','bad')}
 if(e.phase===3){e.spawnT-=dt;if(e.spawnT<=0){e.spawnT=7;var al=loc().enemies.filter(function(q){return!q.dead&&q.type!=='boss'}).length;
  if(al<2){loc().enemies.push({id:'add'+Math.random(),type:'gun',x:e.x-80,y:FLOOR,hp:35,max:35,face:1,state:'patrol',stT:1,fireT:1,wind:0,burst:0,burstT:0,flash:0,dead:false,alert:true,b0:e.x-160,b1:e.x+60,anim:0,vx:0,phase:1});toast('⚠ استدعى رجاله!','warn')}}}
 if(e.wind>0){e.wind-=dt;if(e.wind<=0){
  var base=Math.atan2((P.y-18)-(e.y-22),dx),n=e.phase===3?5:3;
  for(var i=0;i<n;i++){var a=base+(i-(n-1)/2)*.13;
   bullets.push({x:e.x+e.face*12,y:e.y-22,vx:Math.cos(a)*300,vy:Math.sin(a)*300,life:2,from:'e',dmg:10})}
  sfx.shotgun();muzzle(e.x+e.face*14,e.y-22);shake(.1,2)}}
 else{e.fireT-=dt;if(e.fireT<=0&&!P.dead){e.wind=.4;e.fireT=(e.phase===3?1.1:e.phase===2?1.5:1.9)*dm.fire}}
 e.x+=e.face*(e.phase===3?35:20)*dt;e.x=clamp(e.x,200,LOCS.rooftop.w-40);
 if(!P.dead&&P.ifr<=0&&hit(eBox(e),P.x,P.y-16,7))hurtPlayer(18,sgn(dx)||1);
}
/* ---------- UPDATE ---------- */
function updPlayer(dt){
 if(P.dead)return;
 P.ifr=Math.max(0,P.ifr-dt);P.fireCd-=dt;P.meleeCd-=dt;P.muzzle=Math.max(0,P.muzzle-dt);
 if(P.relT>0){P.relT-=dt;$('relBar').firstElementChild.style.width=((1-P.relT/1.05)*100)+'%';
  if(P.relT<=0){var need=8-P.mag,take=Math.min(need,P.res);P.mag+=take;P.res-=take;$('relBar').classList.remove('on');updateHUD()}}
 var mx=input.mx;
 if(Math.abs(mx)>.15){P.face=sgn(mx);P.vx=mx*150;P.walk+=dt*10;
  P.stepT-=dt;if(P.stepT<=0){P.stepT=.3;sfx.foot()}}
 else{P.vx*=Math.pow(.001,dt);P.walk=0}
 P.x=clamp(P.x+P.vx*dt,12,loc().w-12);
 P.aim=input.aim;
 if(input.fire)firePlayer();
 if(input.rel){input.rel=false;startRel()}
 if(input.act){input.act=false;doInteract()}
 P.anim+=dt;
}
function updBullets(dt){
 var L=loc();
 for(var i=bullets.length-1;i>=0;i--){var b=bullets[i];b.x+=b.vx*dt;b.y+=b.vy*dt;b.life-=dt;
  var rm=b.life<=0||b.x<4||b.x>L.w-4||b.y<30||b.y>FLOOR+2;
  if(rm&&b.life>0){spark(b.x,b.y,'#a89877',3,70);sfx.ric()}
  if(!rm&&b.from==='p'){
   for(var e=0;e<L.enemies.length;e++){var en=L.enemies[e];
    if(!en.dead&&hit(eBox(en),b.x,b.y,3)){hurtEnemy(en,b.dmg);rm=true;break}}
   if(S.loc==='alley'){for(var bt=0;bt<3;bt++){if(!bottleDead[bt]&&Math.abs(b.x-(300+bt*22))<5&&Math.abs(b.y-(FLOOR-34))<8){
    bottleDead[bt]=true;S.bottles++;sfx.bottle();spark(300+bt*22,FLOOR-34,'#7fb069',8,90);floatTxt(300+bt*22,FLOOR-44,'+قارورة','#7fb069');
    if(S.bottles===3){P.res=Math.min(96,P.res+24);toast('✔ تحدي القوارير 3/3 — +24 ذخيرة','big');sfx.sting()}rm=true;break}}}
  }
  if(!rm&&b.from==='e'&&!P.dead&&P.ifr<=0&&hit(pBox(),b.x,b.y,3)){hurtPlayer(b.dmg,sgn(b.vx)||1);rm=true}
  if(rm)bullets.splice(i,1)}
}
function updItems(){var L=loc();
 for(var i=0;i<L.items.length;i++){var it=L.items[i];if(it.taken)continue;
  if((it.type==='ammo'||it.type==='med')&&Math.abs(P.x-it.x)<12&&!P.dead){
   it.taken=true;takenKeys[eKey(S.loc,it.id)]=true;sfx.pick();
   if(it.type==='ammo'){P.res=Math.min(96,P.res+12);floatTxt(it.x,it.y-12,'+12','#ffcf6e')}
   else{P.hp=Math.min(100,P.hp+25);floatTxt(it.x,it.y-12,'+25','#7fb069')}
   updateHUD()}}
}
function updParts(dt){
 for(var i=parts.length-1;i>=0;i--){var p=parts[i];p.life-=dt;if(p.life<=0){parts.splice(i,1);continue}
  if(p.t!=='f'){p.x+=p.vx*dt;p.y+=p.vy*dt;p.vy+=(p.t==='c'?420:p.t==='b'?380:160)*dt;
   if(p.y>FLOOR){p.y=FLOOR;p.vy*=-.3;p.vx*=.6}}}
 for(var f=floats.length-1;f>=0;f--){var ft=floats[f];ft.life-=dt;ft.y-=22*dt;if(ft.life<=0)floats.splice(f,1)}
}
function updAmbient(dt){
 S.t+=dt;S.lightT-=dt;if(S.lightT<=0){S.lightT=rnd(14,28);S.lightF=.8;if(loc().out)sfx.ric()}
 S.lightF=Math.max(0,S.lightF-dt*2);S.hurtF=Math.max(0,S.hurtF-dt*2.5);
 S.shakeT=Math.max(0,S.shakeT-dt);if(S.shakeT<=0)S.shakeM=0;
 if(loc().out){for(var i=0;i<rain.length;i++){var d=rain[i];d.y+=d.v*dt;d.x-=70*dt;
  if(d.y>VH){d.y=-8;d.x=rnd(0,VW+50);if(splashes.length<30)splashes.push({x:rnd(0,VW),y:FLOOR+rnd(2,20),life:.15})}}
  for(var s=splashes.length-1;s>=0;s--){splashes[s].life-=dt;if(splashes[s].life<=0)splashes.splice(s,1)}}
}
function updCamera(dt){S.cam=clamp(lerp(S.cam,P.x-VW/2+P.face*30,Math.min(1,dt*5)),0,loc().w-VW)}
function updatePlaying(dt){
 if(dlgOn){updDlg(dt);updAmbient(dt);updParts(dt);return}
 S.elapsed+=dt;
 updPlayer(dt);updEnemies(dt);updBullets(dt);updItems();updParts(dt);updAmbient(dt);updCamera(dt);
 if(P.dead){S.deadT-=dt;if(S.deadT<=0)gameOver()}
 updateHUD();
}
/* ---------- DRAW WORLD ---------- */
function drawWorld(c){
 var L=loc();c.save();c.translate(-Math.round(S.cam),0);
 DRAW[L.id](c,L);
 drawDoors(c,L);
 (corpses[S.loc]||[]).forEach(function(cp){drawCorpse(c,cp)});
 L.items.forEach(function(it){if(!it.taken)drawItem(c,it)});
 L.npcs.forEach(function(n){drawNPC(c,n)});
 if(S.loc==='apartment')drawPhone(c,300);
 if(S.loc==='alley')drawBottles(c);
 L.enemies.forEach(function(e){if(!e.dead)drawEnemy(c,e)});
 drawPlayer(c);
 drawBullets(c);drawParts(c);drawFloats(c);
 c.restore();
}
function drawDoors(c,L){L.doors.forEach(function(d){
 var x=d.x;
 if(L.out&&S.loc!=='alley'&&S.loc!=='rooftop'){
  c.fillStyle='#1a1208';c.fillRect(x-16,FLOOR-58,32,58);
  c.fillStyle='#2a1c0e';c.fillRect(x-14,FLOOR-56,28,56);
  c.fillStyle='#0d0a06';c.fillRect(x-10,FLOOR-46,20,30);
  c.fillStyle=rgba('#ffcf6e',.5);c.fillRect(x-8,FLOOR-44,16,26);
  c.fillStyle='#3a2c1a';c.fillRect(x-16,FLOOR-62,32,5);
  c.fillStyle='#0d0a06';c.fillRect(x-20,FLOOR-74,40,12);
  c.strokeStyle=rgba('#d99a2b',.7);c.strokeRect(x-20.5,FLOOR-74.5,41,13);
  pT(c,d.label.length>8?'ENTER':d.label,x-pW(d.label.length>8?'ENTER':d.label,1)/2,FLOOR-71,'#ffcf6e',1);
 }else if(S.loc==='alley'&&d.to==='rooftop'){
  c.fillStyle='#2a2a2e';c.fillRect(x-3,FLOOR-120,6,120);
  for(var r=0;r<8;r++)c.fillRect(x-10,FLOOR-110+r*14,20,3);
  c.fillStyle='#0d0a06';c.fillRect(x-16,FLOOR-132,32,11);pT(c,'UP',x-pW('UP',1)/2,FLOOR-129,'#5eead4',1);
 }else if(S.loc==='rooftop'){
  c.fillStyle='#2a2a2e';c.fillRect(x-12,FLOOR-26,24,26);c.fillStyle='#0d0a06';c.fillRect(x-8,FLOOR-20,16,14);
  pT(c,'DOWN',x-pW('DOWN',1)/2,FLOOR-34,'#5eead4',1);
 }else{
  c.fillStyle='#241708';c.fillRect(x-14,FLOOR-56,28,56);
  c.fillStyle='#3a2412';c.fillRect(x-12,FLOOR-54,24,54);
  c.fillStyle='#0d0a06';c.fillRect(x-8,FLOOR-44,16,22);
  c.fillStyle=rgba('#7fb4d9',.35);c.fillRect(x-6,FLOOR-42,12,18);
  c.fillStyle='#d99a2b';c.fillRect(x+7,FLOOR-28,2,3);
  c.fillStyle='#0d0a06';c.fillRect(x-16,FLOOR-68,32,11);
  pT(c,'EXIT',x-pW('EXIT',1)/2,FLOOR-65,'#ffcf6e',1);
 }})}
function drawPhone(c,x){
 c.fillStyle='#2a1c0e';c.fillRect(x-14,FLOOR-26,28,26);
 c.fillStyle='#3a2412';c.fillRect(x-14,FLOOR-26,28,3);
 c.fillStyle='#c9b896';c.fillRect(x-6,FLOOR-34,12,9);
 c.fillStyle='#8a7a5a';c.fillRect(x-4,FLOOR-32,8,4);
 c.fillStyle='#2a2a2e';c.fillRect(x-8,FLOOR-37,16,3);
 c.strokeStyle='#8a7a5a';c.beginPath();c.moveTo(x+6,FLOOR-30);c.quadraticCurveTo(x+12,FLOOR-20,x+8,FLOOR-12);c.stroke();
 if(M.idx===0){c.globalCompositeOperation='lighter';glow(c,x,FLOOR-32,10+Math.sin(S.t*4)*3,'#ffcf6e',.5);c.globalCompositeOperation='source-over';
  pT(c,'!',x-1,FLOOR-46+Math.sin(S.t*5)*2,'#ffcf6e',1)}
}
function drawBottles(c){for(var b=0;b<3;b++){if(bottleDead[b])continue;var x=300+b*22;
 c.fillStyle='#3f6b3f';c.fillRect(x-2,FLOOR-38,4,10);c.fillRect(x-1,FLOOR-42,2,4);
 c.fillStyle=rgba('#7fb069',.6);c.fillRect(x-1,FLOOR-37,1,7)}}
function drawItem(c,it){var x=it.x,y=it.y,bob=Math.sin(S.t*3+x)*1.5;
 if(it.type==='ammo'){c.fillStyle='#3a2c1a';c.fillRect(x-6,y-6+bob,12,9);c.fillStyle='#d99a2b';c.fillRect(x-4,y-4+bob,3,5);c.fillRect(x,y-4+bob,3,5);c.strokeStyle='#8a5a2b';c.strokeRect(x-6.5,y-6.5+bob,13,10)}
 else if(it.type==='med'){c.fillStyle='#e8e0d0';c.fillRect(x-6,y-6+bob,12,10);c.fillStyle='#c0392b';c.fillRect(x-1,y-4+bob,2,6);c.fillRect(x-3,y-2+bob,6,2)}
 else if(it.type==='ledger'){c.fillStyle='#1a1a22';c.fillRect(x-6,y-8+bob,12,10);c.fillStyle='#d99a2b';c.fillRect(x-4,y-6+bob,8,1);c.fillRect(x-4,y-3+bob,8,1);c.globalCompositeOperation='lighter';glow(c,x,y-3+bob,12,'#d99a2b',.4);c.globalCompositeOperation='source-over'}
 else{c.fillStyle='#c9b896';c.fillRect(x-6,y-8+bob,12,10);c.fillStyle='#8a7a5a';c.fillRect(x-4,y-6+bob,8,1);c.fillRect(x-4,y-3+bob,8,1);c.globalCompositeOperation='lighter';glow(c,x,y-3+bob,12,'#5eead4',.35);c.globalCompositeOperation='source-over'}}
function drawNPC(c,n){var x=n.x;
 c.fillStyle='#2a2a2e';c.fillRect(x-6,FLOOR-30,12,18);
 c.fillStyle='#e8e0d0';c.fillRect(x-5,FLOOR-28,10,14);
 c.fillStyle='#c9a06a';c.fillRect(x-4,FLOOR-37,8,7);
 c.fillStyle='#3a2c1a';c.fillRect(x-4,FLOOR-38,8,3);
 c.fillStyle='#2a2a2e';c.fillRect(x-7,FLOOR-12,5,12);c.fillRect(x+2,FLOOR-12,5,12);
 if(M.idx===1&&M.step===0){pT(c,'!',x-1,FLOOR-48+Math.sin(S.t*5)*2,'#ffcf6e',1)}}
function drawCorpse(c,cp){c.save();c.translate(cp.x,cp.y);c.scale(cp.face,1);
 c.fillStyle=cp.type==='boss'?'#d8d0c0':'#2a2230';c.fillRect(-14,-5,24,5);
 c.fillStyle='#c9a06a';c.fillRect(10,-6,6,5);
 c.fillStyle=rgba('#8e1f1f',.5);c.fillRect(-16,-1,30,2);c.restore()}
function drawPlayer(c){
 if(P.dead&&S.deadT<.6)return;
 if(P.ifr>0&&Math.floor(S.t*18)%2===0)return;
 var x=Math.round(P.x),y=P.y,f=P.face,walk=Math.abs(P.vx)>20,ph=Math.sin(P.walk*2);
 c.save();c.translate(x,y);c.scale(f,1);
 var bob=walk?Math.abs(ph)*1.2:Math.sin(S.t*2)*.6;c.translate(0,-bob);
 c.fillStyle='#14141a';
 if(walk){c.fillRect(-4+ph*3,-10,3,10);c.fillRect(1-ph*3,-10,3,10)}else{c.fillRect(-4,-10,3,10);c.fillRect(1,-10,3,10)}
 c.fillStyle='#0a0a0e';c.fillRect(-5+(walk?ph*3:0),-2,4,2);c.fillRect(0-(walk?ph*3:0),-2,4,2);
 c.fillStyle='#1a1a22';c.fillRect(-5,-26,10,16);
 c.fillStyle='#26262e';c.fillRect(-5,-26,2,15);
 c.fillStyle='#c9a06a';c.fillRect(-1,-25,2,10);
 c.fillStyle='#14141a';c.fillRect(-5,-13,10,2);
 c.fillStyle='#c9a06a';c.fillRect(-3,-33,7,7);
 c.fillStyle='#1a1410';c.fillRect(-3,-35,7,3);c.fillRect(-4,-34,2,4);
 c.fillStyle='#0a0a0e';c.fillRect(2,-31,2,1);
 var gun=P.muzzle>0||input.fire||P.relT>0;
 c.fillStyle='#1a1a22';
 if(gun){c.fillRect(2,-22,7,3);c.fillStyle='#2a2a2e';c.fillRect(8,-23,7,3);c.fillStyle='#0a0a0e';c.fillRect(13,-22,3,2);
  if(P.muzzle>0){c.globalCompositeOperation='lighter';glow(c,17,-21,12,'#ffcf6e',.9);c.fillStyle='#fff';c.fillRect(15,-22,4,2);c.globalCompositeOperation='source-over'}}
 else{c.fillRect(2,-24,3,8);c.fillStyle='#2a2a2e';c.fillRect(2,-17,4,3)}
 c.restore();
}
function drawEnemy(c,e){
 var x=Math.round(e.x),y=e.y,f=e.face,flash=e.flash>0,walk=e.alert||e.state==='patrol',ph=Math.sin(e.anim*2);
 c.save();c.translate(x,y);c.scale(f,1);
 if(e.type==='boss'){
  c.fillStyle=flash?'#fff':'#d8d0c0';c.fillRect(-8,-38,16,26);
  c.fillStyle=flash?'#fff':'#b8b0a0';c.fillRect(-8,-38,3,26);
  c.fillStyle='#8e1f1f';c.fillRect(-2,-36,2,12);
  c.fillStyle='#c9a06a';c.fillRect(-5,-46,10,8);
  c.fillStyle='#e8e0d0';c.fillRect(-5,-48,10,3);
  c.fillStyle='#8e1f1f';c.fillRect(2,-43,3,1);
  c.fillStyle='#1a1a22';c.fillRect(-6,-12,5,12);c.fillRect(1,-12,5,12);
  c.fillStyle='#d8d0c0';c.fillRect(3,-26,8,3);c.fillStyle='#2a2a2e';c.fillRect(10,-27,8,3);
  if(e.wind>0){c.globalCompositeOperation='lighter';glow(c,14,-25,10,'#c0392b',.7);c.globalCompositeOperation='source-over'}
  c.restore();return;
 }
 var jacket=e.type==='shot'?'#4a3a22':'#3a2230';
 c.fillStyle='#14141a';
 if(walk){c.fillRect(-4+ph*2,-10,3,10);c.fillRect(1-ph*2,-10,3,10)}else{c.fillRect(-4,-10,3,10);c.fillRect(1,-10,3,10)}
 c.fillStyle=flash?'#fff':jacket;c.fillRect(-5,-26,10,16);
 c.fillStyle=flash?'#fff':'#26262e';c.fillRect(-5,-26,2,15);
 c.fillStyle='#c9a06a';c.fillRect(-3,-32,7,6);
 c.fillStyle=e.type==='shot'?'#2a2a1a':'#1a1410';c.fillRect(-4,-34,9,3);
 c.fillStyle='#0a0a0e';c.fillRect(2,-30,2,1);
 c.fillStyle=jacket;c.fillRect(2,-22,6,3);
 c.fillStyle='#2a2a2e';c.fillRect(7,-23,e.type==='shot'?9:6,3);
 if(e.wind>0){c.fillStyle='#ffcf6e';c.fillRect(12,-23,2,2);c.globalCompositeOperation='lighter';glow(c,13,-22,7,'#c0392b',.5);c.globalCompositeOperation='source-over'}
 c.restore();
 if(e.alert&&!e.dead){var hpw=e.hp/e.max;c.fillStyle='rgba(5,4,3,.7)';c.fillRect(x-8,y-40,16,2);
  c.fillStyle='#c0392b';c.fillRect(x-8,y-40,16*hpw,2)}
}
function drawBullets(c){c.globalCompositeOperation='lighter';
 bullets.forEach(function(b){var l=Math.hypot(b.vx,b.vy)||1,nx=b.vx/l,ny=b.vy/l,col=b.from==='p'?'#ffcf6e':'#e67e22';
  var g=c.createLinearGradient(b.x-nx*9,b.y-ny*9,b.x,b.y);g.addColorStop(0,rgba(col,0));g.addColorStop(1,rgba(col,.9));
  c.strokeStyle=g;c.lineWidth=1.5;c.beginPath();c.moveTo(b.x-nx*9,b.y-ny*9);c.lineTo(b.x,b.y);c.stroke();
  c.fillStyle='#fff';c.fillRect(b.x-1,b.y-1,2,2)});
 c.globalCompositeOperation='source-over';c.lineWidth=1}
function drawParts(c){parts.forEach(function(p){var a=p.life/p.max;
 if(p.t==='f'){c.globalCompositeOperation='lighter';glow(c,p.x,p.y,p.sz,p.c,a);c.globalCompositeOperation='source-over'}
 else if(p.t==='c'){c.fillStyle=rgba(p.c,a);c.fillRect(p.x,p.y,2,1)}
 else{c.fillStyle=rgba(p.c,a);c.fillRect(p.x-p.sz/2,p.y-p.sz/2,p.sz,p.sz)}})}
function drawFloats(c){floats.forEach(function(f){var a=Math.min(1,f.life/f.max*2);
 c.font='7px Cairo';c.fillStyle=rgba(f.c==='#f2e9d8'?'#f2e9d8':f.c,a);c.textAlign='center';c.fillText(f.s,f.x,f.y);c.textAlign='left'})}
/* ---------- LOCATION ART ---------- */
var DRAW={
 street:function(c,L){
  var g=c.createLinearGradient(0,0,0,VH);g.addColorStop(0,'#05070d');g.addColorStop(.6,'#0a0d16');g.addColorStop(1,'#0d0a08');
  c.fillStyle=g;c.fillRect(0,0,L.w,VH);
  for(var bx=0;bx<L.w;bx+=140){var bh=90+((bx*7)%60);
   c.fillStyle='#0a0c14';c.fillRect(bx,150-bh,120,bh+60);
   for(var wy=160-bh;wy<140;wy+=12)for(var wx=bx+8;wx<bx+112;wx+=14)
    if(((wx*wy)%7)<2){c.fillStyle=rgba(((wx+wy)%3)?'#ffcf6e':'#7fb4d9',.25+((wx*wy)%5)*.08);c.fillRect(wx,wy,5,6)}}
  c.fillStyle='#0d0a08';c.fillRect(0,150,L.w,64);
  for(var sx=0;sx<L.w;sx+=180){c.fillStyle='#171008';c.fillRect(sx,150,150,64);
   c.fillStyle='#241708';c.fillRect(sx+6,158,60,40);c.fillStyle=rgba('#ffcf6e',.3);c.fillRect(sx+8,160,56,36);
   c.fillStyle='#1a1208';c.fillRect(sx+80,160,50,54);
   var neon=['#c0392b','#5eead4','#d99a2b'][(sx/180)%3];
   c.fillStyle='#0d0a06';c.fillRect(sx+20,140,60,14);c.strokeStyle=rgba(neon,.8);c.strokeRect(sx+20.5,140.5,59,13);
   pT(c,['BAR','HOTEL','24H','DINER'][(sx/180)%4],sx+28,144,neon,1);
   c.globalCompositeOperation='lighter';glow(c,sx+50,147,26,neon,.3);c.globalCompositeOperation='source-over'}
  c.fillStyle='#141210';c.fillRect(0,FLOOR,L.w,10);c.fillStyle='#2a2620';c.fillRect(0,FLOOR,L.w,2);
  c.fillStyle='#0a0908';c.fillRect(0,FLOOR+10,L.w,VH-FLOOR-10);
  for(var lx=120;lx<L.w;lx+=300){c.fillStyle='#1a1a1e';c.fillRect(lx,FLOOR-70,3,70);c.fillRect(lx-8,FLOOR-70,19,3);
   c.fillStyle='#ffcf6e';c.fillRect(lx-6,FLOOR-67,4,3);c.fillRect(lx+7,FLOOR-67,4,3);
   c.globalCompositeOperation='lighter';var cg=c.createLinearGradient(0,FLOOR-64,0,FLOOR);
   cg.addColorStop(0,rgba('#d99a2b',.16));cg.addColorStop(1,rgba('#d99a2b',0));
   c.fillStyle=cg;c.beginPath();c.moveTo(lx-6,FLOOR-64);c.lineTo(lx-22,FLOOR);c.lineTo(lx+28,FLOOR);c.lineTo(lx+10,FLOOR-64);c.closePath();c.fill();
   glow(c,lx+2,FLOOR-65,16,'#d99a2b',.5);c.globalCompositeOperation='source-over';
   var rg=c.createLinearGradient(0,FLOOR+10,0,VH);rg.addColorStop(0,rgba('#d99a2b',.2));rg.addColorStop(1,rgba('#d99a2b',0));
   c.fillStyle=rg;c.fillRect(lx-4,FLOOR+10,10,VH-FLOOR-10)}
  for(var cx2=400;cx2<L.w;cx2+=700){c.fillStyle='#1a1a22';c.fillRect(cx2,FLOOR-18,60,18);c.fillRect(cx2+8,FLOOR-26,40,10);
   c.fillStyle='#0a0a0e';c.fillRect(cx2+10,FLOOR-24,14,7);c.fillRect(cx2+32,FLOOR-24,14,7);
   c.fillStyle='#2a2a2e';c.fillRect(cx2+6,FLOOR-4,10,4);c.fillRect(cx2+44,FLOOR-4,10,4);
   c.fillStyle=rgba('#c0392b',.6);c.fillRect(cx2+56,FLOOR-14,3,3)}
  for(var dx=200;dx<L.w;dx+=520){c.fillStyle='#1a2a1a';c.fillRect(dx,FLOOR-16,22,16);c.fillStyle='#243424';c.fillRect(dx-2,FLOOR-18,26,4)}
 },
 apartment:function(c,L){
  c.fillStyle='#241708';c.fillRect(0,0,L.w,VH);
  for(var px=0;px<430;px+=14){c.fillStyle=['#3a2412','#42291a','#352010'][((px/14)|0)%3];c.fillRect(px,40,13,FLOOR-40);
   c.fillStyle=rgba('#000',.25);c.fillRect(px+12,40,1,FLOOR-40)}
  c.fillStyle='#1a1208';c.fillRect(0,36,430,6);
  c.fillStyle='#2a1c0e';c.fillRect(0,FLOOR,L.w,VH-FLOOR);
  c.fillStyle='#5a1f1f';c.fillRect(20,FLOOR+2,380,14);c.fillStyle=rgba('#000',.3);c.fillRect(20,FLOOR+14,380,2);
  c.fillStyle='#1a1208';c.fillRect(90,80,60,80);c.fillStyle='#0d0a06';c.fillRect(94,84,52,72);
  c.fillStyle=rgba('#7fb4d9',.25);c.fillRect(96,86,48,68);
  for(var ry=88;ry<152;ry+=6){c.fillStyle=rgba('#7fb4d9',.3);c.fillRect(96+((ry*3)%40),ry,1,4)}
  c.fillStyle='#3a2412';c.fillRect(118,84,3,72);c.fillRect(94,118,52,3);
  c.fillStyle='#c9b896';c.fillRect(30,110,16,22);c.fillStyle='#8a7a5a';c.fillRect(33,114,10,8);
  c.strokeStyle='#8a7a5a';c.beginPath();c.moveTo(38,132);c.quadraticCurveTo(42,150,36,160);c.stroke();
  c.fillStyle='#2a1c0e';c.fillRect(250,FLOOR-24,70,24);c.fillStyle='#3a2412';c.fillRect(250,FLOOR-24,70,3);
  c.fillStyle='#241708';c.fillRect(430,40,270,FLOOR-40);
  for(var ty=120;ty<FLOOR;ty+=12)for(var tx=430;tx<L.w;tx+=12){c.fillStyle=((tx+ty)/12)%2?'#b8a888':'#c9b896';c.fillRect(tx,ty,11,11);
   c.fillStyle=rgba('#000',.12);c.fillRect(tx,ty+10,11,1)}
  c.fillStyle='#8a7a5a';c.fillRect(430,116,270,4);
  c.fillStyle='#e8e0d0';c.fillRect(470,FLOOR-26,20,26);c.fillRect(474,FLOOR-34,12,8);
  c.fillStyle='#c9c0b0';c.fillRect(470,FLOOR-26,20,3);
  c.fillStyle='#e8e0d0';c.fillRect(530,FLOOR-30,22,6);c.fillRect(538,FLOOR-24,6,24);
  c.fillStyle='#c9c0b0';c.fillRect(530,FLOOR-30,22,2);
  c.fillStyle='#8a9aa8';c.fillRect(534,FLOOR-70,16,26);c.fillStyle=rgba('#7fb4d9',.5);c.fillRect(536,FLOOR-68,12,22);
  c.fillStyle=rgba('#fff',.35);c.fillRect(538,FLOOR-66,3,18);
  c.fillStyle='#2a2a2e';c.fillRect(600,60,80,4);c.fillStyle=rgba('#7fb4d9',.2);c.fillRect(602,64,76,FLOOR-64);
  c.strokeStyle='#3a3a3e';c.strokeRect(600.5,64.5,79,FLOOR-65);
  c.fillStyle='#1a1a22';c.fillRect(610,70,14,50);c.fillRect(630,66,12,60);c.fillRect(650,72,16,44);
  c.fillStyle='#e8e0d0';c.fillRect(560,52,40,5);c.fillStyle='#fff';c.fillRect(562,54,36,2);
  c.fillStyle='#2a1c0e';c.fillRect(330,FLOOR-30,60,30);c.fillStyle='#3a2412';c.fillRect(330,FLOOR-30,60,3);
  c.fillStyle='#c9b896';c.fillRect(340,FLOOR-38,14,8);
 },
 bar:function(c,L){
  c.fillStyle='#1a1208';c.fillRect(0,0,L.w,VH);
  for(var px=0;px<L.w;px+=16){c.fillStyle=((px/16)|0)%2?'#241708':'#2a1c0e';c.fillRect(px,40,15,FLOOR-40)}
  c.fillStyle='#141210';c.fillRect(0,FLOOR,L.w,VH-FLOOR);
  for(var fx=0;fx<L.w;fx+=24){c.fillStyle=rgba('#000',.3);c.fillRect(fx,FLOOR,1,VH-FLOOR)}
  c.fillStyle='#3a2412';c.fillRect(420,FLOOR-34,260,34);c.fillStyle='#4a3018';c.fillRect(420,FLOOR-34,260,4);
  c.fillStyle='#241708';c.fillRect(430,FLOOR-70,240,36);
  for(var bx=436;bx<664;bx+=12){var bc=['#3f6b3f','#8e1f1f','#d99a2b','#5eead4'][(bx/12)%4];
   c.fillStyle=bc;c.fillRect(bx,FLOOR-64,5,16);c.fillRect(bx+1,FLOOR-68,3,4);
   c.fillStyle=rgba('#fff',.25);c.fillRect(bx+1,FLOOR-62,1,12)}
  c.fillStyle='#1a1208';c.fillRect(430,FLOOR-46,240,3);
  for(var st=460;st<660;st+=60){c.fillStyle='#2a2a2e';c.fillRect(st,FLOOR-20,4,20);c.fillStyle='#5a1f1f';c.fillRect(st-7,FLOOR-24,18,5)}
  c.fillStyle='#0d0a06';c.fillRect(180,80,70,50);c.strokeStyle='#d99a2b';c.strokeRect(180.5,80.5,69,49);
  pT(c,'SAL',200,92,'#ffcf6e',1);pT(c,'BAR',200,104,'#c0392b',1);
  c.globalCompositeOperation='lighter';glow(c,215,105,34,'#d99a2b',.35);glow(c,215,105,20,'#c0392b',.25);c.globalCompositeOperation='source-over';
  c.fillStyle='#2a1c0e';c.fillRect(120,FLOOR-26,50,26);c.fillStyle='#3a2412';c.fillRect(120,FLOOR-26,50,3);
  c.fillStyle='#1a1a22';c.fillRect(300,60,40,60);c.fillStyle=rgba('#5eead4',.3);c.fillRect(304,64,32,52);
  pT(c,'JAZZ',306,80,'#5eead4',1);
  c.globalCompositeOperation='lighter';glow(c,320,90,24,'#5eead4',.3);c.globalCompositeOperation='source-over';
  for(var hl=200;hl<L.w;hl+=200){c.fillStyle='#1a1a1e';c.fillRect(hl,40,2,20);c.fillStyle='#ffcf6e';c.fillRect(hl-4,60,10,4);
   c.globalCompositeOperation='lighter';glow(c,hl+1,64,20,'#d99a2b',.4);c.globalCompositeOperation='source-over'}
 },
 clinic:function(c,L){
  c.fillStyle='#1a2028';c.fillRect(0,0,L.w,VH);
  for(var ty=100;ty<FLOOR;ty+=12)for(var tx=0;tx<L.w;tx+=12){c.fillStyle=((tx+ty)/12)%2?'#9aa8a8':'#b8c4c0';c.fillRect(tx,ty,11,11);
   c.fillStyle=rgba('#000',.1);c.fillRect(tx,ty+10,11,1)}
  c.fillStyle='#5a6a6a';c.fillRect(0,96,L.w,4);
  c.fillStyle='#2a3038';c.fillRect(0,FLOOR,L.w,VH-FLOOR);
  for(var fx=0;fx<L.w;fx+=20){c.fillStyle=rgba('#000',.25);c.fillRect(fx,FLOOR,1,VH-FLOOR)}
  c.fillStyle='#e8e0d0';c.fillRect(240,FLOOR-24,80,10);c.fillStyle='#c9c0b0';c.fillRect(240,FLOOR-14,80,14);
  c.fillStyle='#8a9aa8';c.fillRect(244,FLOOR-30,72,6);
  c.fillStyle='#e8e0d0';c.fillRect(420,FLOOR-40,50,40);c.fillStyle='#c9c0b0';c.fillRect(420,FLOOR-40,50,3);
  c.fillStyle='#8e1f1f';c.fillRect(440,FLOOR-34,10,3);c.fillRect(443,FLOOR-37,4,9);
  c.fillStyle='#9aa8a8';c.fillRect(120,FLOOR-50,40,50);c.fillStyle='#7a8a8a';c.fillRect(120,FLOOR-50,40,3);
  c.fillStyle=rgba('#5eead4',.3);c.fillRect(126,FLOOR-44,28,20);
  c.fillStyle='#e8e0d0';c.fillRect(340,52,60,5);c.fillStyle='#fff';c.fillRect(342,54,56,2);
  c.fillStyle='#0d0a06';c.fillRect(480,70,60,40);c.strokeStyle='#5eead4';c.strokeRect(480.5,70.5,59,39);
  pT(c,'FILES',492,84,'#5eead4',1);
 },
 warehouse:function(c,L){
  c.fillStyle='#141210';c.fillRect(0,0,L.w,VH);
  for(var px=0;px<L.w;px+=20){c.fillStyle=((px/20)|0)%2?'#1a1814':'#201c16';c.fillRect(px,30,19,FLOOR-30);
   c.fillStyle=rgba('#000',.3);c.fillRect(px+18,30,1,FLOOR-30)}
  c.fillStyle='#0d0a08';c.fillRect(0,26,L.w,6);
  c.fillStyle='#2a2620';c.fillRect(0,FLOOR,L.w,VH-FLOOR);
  for(var fx=0;fx<L.w;fx+=30){c.fillStyle=rgba('#000',.3);c.fillRect(fx,FLOOR,1,VH-FLOOR)}
  for(var cr=180;cr<L.w-100;cr+=160){var ch=30+((cr*7)%30);
   c.fillStyle='#3a2c1a';c.fillRect(cr,FLOOR-ch,44,ch);c.fillStyle='#4a3a22';c.fillRect(cr,FLOOR-ch,44,3);
   c.strokeStyle=rgba('#8a5a2b',.5);c.strokeRect(cr+.5,FLOOR-ch+.5,43,ch-1);
   c.beginPath();c.moveTo(cr,FLOOR-ch);c.lineTo(cr+44,FLOOR);c.moveTo(cr+44,FLOOR-ch);c.lineTo(cr,FLOOR);c.stroke();
   if((cr%320)<160){c.fillStyle='#3a2c1a';c.fillRect(cr+6,FLOOR-ch-24,32,24);c.fillStyle='#4a3a22';c.fillRect(cr+6,FLOOR-ch-24,32,3)}}
  for(var sh=300;sh<L.w;sh+=300){c.fillStyle='#2a2a2e';c.fillRect(sh,80,60,4);c.fillRect(sh,110,60,4);
   c.fillRect(sh,80,3,FLOOR-80);c.fillRect(sh+57,80,3,FLOOR-80);
   for(var bb=sh+6;bb<sh+54;bb+=10){c.fillStyle=['#3a2c1a','#4a3a22','#2a2a2e'][(bb/10)%3];c.fillRect(bb,96,8,14)}}
  for(var hl=150;hl<L.w;hl+=250){c.fillStyle='#1a1a1e';c.fillRect(hl,26,2,26);c.fillStyle='#3a3a3e';c.fillRect(hl-6,52,14,5);
   c.fillStyle='#ffcf6e';c.fillRect(hl-4,57,10,2);
   c.globalCompositeOperation='lighter';var cg=c.createLinearGradient(0,58,0,FLOOR);
   cg.addColorStop(0,rgba('#d99a2b',.14));cg.addColorStop(1,rgba('#d99a2b',0));
   c.fillStyle=cg;c.beginPath();c.moveTo(hl-4,58);c.lineTo(hl-26,FLOOR);c.lineTo(hl+30,FLOOR);c.lineTo(hl+8,58);c.closePath();c.fill();
   glow(c,hl+1,58,16,'#d99a2b',.45);c.globalCompositeOperation='source-over'}
  c.fillStyle='#0d0a06';c.fillRect(860,80,80,30);c.strokeStyle='#d99a2b';c.strokeRect(860.5,80.5,79,29);
  pT(c,'PIER 9',876,90,'#ffcf6e',1);
 },
 alley:function(c,L){
  var g=c.createLinearGradient(0,0,0,VH);g.addColorStop(0,'#05070d');g.addColorStop(1,'#0d0a08');
  c.fillStyle=g;c.fillRect(0,0,L.w,VH);
  c.fillStyle='#1a1208';c.fillRect(0,40,120,FLOOR-40);c.fillStyle='#241708';c.fillRect(400,40,100,FLOOR-40);
  for(var by=44;by<FLOOR;by+=10){c.fillStyle=rgba('#000',.25);c.fillRect(0,by,120,1);c.fillRect(400,by,100,1)}
  c.fillStyle='#0d0a06';c.fillRect(120,60,280,10);
  c.fillStyle='#141210';c.fillRect(0,FLOOR,L.w,VH-FLOOR);c.fillStyle='#2a2620';c.fillRect(0,FLOOR,L.w,2);
  c.fillStyle='#1a2a1a';c.fillRect(150,FLOOR-24,50,24);c.fillStyle='#243424';c.fillRect(148,FLOOR-28,54,5);
  c.fillStyle='#1a2a1a';c.fillRect(280,FLOOR-20,60,20);c.fillStyle='#243424';c.fillRect(278,FLOOR-24,64,5);
  c.fillStyle='#2a2a2e';c.fillRect(370,40,4,120);
  for(var r=0;r<8;r++)c.fillRect(362,50+r*14,20,3);
  c.fillStyle='#0d0a06';c.fillRect(200,70,60,16);c.strokeStyle='#5eead4';c.strokeRect(200.5,70.5,59,15);
  pT(c,'ALLEY',212,75,'#5eead4',1);
  c.globalCompositeOperation='lighter';glow(c,230,78,24,'#5eead4',.3);
  glow(c,180,FLOOR-40,30,'#d99a2b',.2);c.globalCompositeOperation='source-over';
  c.fillStyle=rgba('#7fb4d9',.12);c.fillRect(220,FLOOR+10,60,VH-FLOOR-10);
 },
 rooftop:function(c,L){
  var g=c.createLinearGradient(0,0,0,VH);g.addColorStop(0,'#04060c');g.addColorStop(.7,'#0a0d16');g.addColorStop(1,'#0d0a08');
  c.fillStyle=g;c.fillRect(0,0,L.w,VH);
  for(var bx=0;bx<L.w;bx+=90){var bh=60+((bx*13)%80);
   c.fillStyle='#0a0c14';c.fillRect(bx,170-bh,70,bh+40);
   for(var wy=176-bh;wy<166;wy+=10)for(var wx=bx+6;wx<bx+64;wx+=12)
    if(((wx*wy)%5)<2){c.fillStyle=rgba(((wx+wy)%3)?'#ffcf6e':'#7fb4d9',.2+((wx*wy)%4)*.08);c.fillRect(wx,wy,4,5)}}
  c.globalCompositeOperation='lighter';glow(c,360,60,50,'#c0392b',.12);c.globalCompositeOperation='source-over';
  c.fillStyle='#141210';c.fillRect(0,FLOOR,L.w,VH-FLOOR);c.fillStyle='#2a2620';c.fillRect(0,FLOOR,L.w,2);
  c.fillStyle='#1a1814';c.fillRect(0,FLOOR-8,L.w,8);
  c.fillStyle='#2a2a2e';c.fillRect(200,FLOOR-70,50,70);c.fillStyle='#3a3a3e';c.fillRect(196,FLOOR-74,58,6);
  c.fillStyle='#1a1a1e';c.fillRect(210,FLOOR-90,4,20);c.fillRect(236,FLOOR-90,4,20);
  c.fillStyle='#2a2a2e';c.fillRect(450,FLOOR-100,3,100);c.fillRect(440,FLOOR-90,23,2);c.fillRect(444,FLOOR-70,15,2);
  c.fillStyle=Math.sin(S.t*3)>0?'#c0392b':'#5a1f1f';c.fillRect(450,FLOOR-104,3,3);
  c.fillStyle='#0d0a06';c.fillRect(560,70,100,26);c.strokeStyle='#c0392b';c.strokeRect(560.5,70.5,99,25);
  pT(c,'BARBER',578,78,'#c0392b',1);pT(c,'CLUB',584,88,'#ffcf6e',1);
  c.globalCompositeOperation='lighter';glow(c,610,83,40,'#c0392b',.3);c.globalCompositeOperation='source-over';
  for(var vx=100;vx<L.w;vx+=180){c.fillStyle='#1a1a1e';c.fillRect(vx,FLOOR-16,16,16);c.fillStyle='#2a2a2e';c.fillRect(vx+2,FLOOR-20,12,4)}
 }
};
/* ---------- LIGHTING ---------- */
var lightC=mkC(VW,VH),lc=lightC[1];
function lights(){
 var L=loc(),arr=[],cam=S.cam;
 function add(x,y,r,col,a){arr.push({x:x-cam,y:y,r:r,c:col,a:a})}
 add(P.x,P.y-18,46,'#c9b896',.28);
 if(S.loc==='street'){for(var lx=120;lx<L.w;lx+=300)add(lx+2,FLOOR-64,95,'#d99a2b',.85);
  for(var sx=0;sx<L.w;sx+=180)add(sx+50,147,50,['#c0392b','#5eead4','#d99a2b'][(sx/180)%3],.5)}
 if(S.loc==='apartment'){add(300,FLOOR-30,60,'#ffcf6e',.6);add(580,56,80,'#e8f0ff',.7*(Math.sin(S.t*13)>-.6?1:.3));
  add(120,110,55,'#7fb4d9',.4);add(350,FLOOR-30,45,'#d99a2b',.4)}
 if(S.loc==='bar'){for(var hl=200;hl<L.w;hl+=200)add(hl+1,64,80,'#d99a2b',.7);add(215,105,60,'#c0392b',.5);add(320,90,50,'#5eead4',.45);add(550,FLOOR-50,70,'#ffcf6e',.5)}
 if(S.loc==='clinic'){add(370,56,90,'#e8f0ff',.75*(Math.sin(S.t*17)>-.7?1:.35));add(510,90,45,'#5eead4',.4);add(280,FLOOR-30,50,'#c9d8d8',.35)}
 if(S.loc==='warehouse'){for(var h=150;h<L.w;h+=250)add(h+1,60,90,'#d99a2b',.7);add(900,95,45,'#ffcf6e',.4)}
 if(S.loc==='alley'){add(230,78,50,'#5eead4',.5);add(180,FLOOR-40,60,'#d99a2b',.4);add(380,FLOOR-80,40,'#7fb4d9',.3)}
 if(S.loc==='rooftop'){add(610,83,70,'#c0392b',.55);add(300,100,80,'#7fb4d9',.25);add(450,FLOOR-100,30,'#c0392b',.3)}
 parts.forEach(function(p){if(p.t==='f')add(p.x,p.y,p.sz*2.2,'#ffcf6e',.9*(p.life/p.max))});
 bullets.forEach(function(b){if(b.from==='p')add(b.x,b.y,14,'#ffcf6e',.3)});
 if(S.lightF>0)add(S.cam+VW/2,60,300,'#cfe8ff',S.lightF*.5);
 return arr;
}
function renderLight(){
 lc.setTransform(1,0,0,1,0,0);lc.globalCompositeOperation='source-over';
 lc.fillStyle=loc().out?'#0a0c14':'#100e12';lc.fillRect(0,0,VW,VH);
 lc.globalCompositeOperation='lighter';
 lights().forEach(function(l){if(l.x<-l.r||l.x>VW+l.r)return;
  var g=lc.createRadialGradient(l.x,l.y,0,l.x,l.y,l.r);
  g.addColorStop(0,rgba(l.c,l.a));g.addColorStop(.5,rgba(l.c,l.a*.45));g.addColorStop(1,rgba(l.c,0));
  lc.fillStyle=g;lc.fillRect(l.x-l.r,l.y-l.r,l.r*2,l.r*2)});
 lc.globalCompositeOperation='source-over';
 ctx.globalCompositeOperation='multiply';ctx.drawImage(lightC[0],0,0);ctx.globalCompositeOperation='source-over';
}
/* ---------- RENDER ---------- */
var grain=mkC(128,128),gc=grain[1];
(function(){var id=gc.createImageData(128,128);for(var i=0;i<id.data.length;i+=4){var v=Math.random()*255;id.data[i]=id.data[i+1]=id.data[i+2]=v;id.data[i+3]=22}gc.putImageData(id,0,0)})();
function render(){
 var shx=0,shy=0;if(S.shakeT>0){shx=rnd(-1,1)*S.shakeM*S.shakeT;shy=rnd(-1,1)*S.shakeM*S.shakeT}
 ctx.setTransform(1,0,0,1,0,0);ctx.fillStyle='#050403';ctx.fillRect(0,0,VW,VH);
 ctx.save();ctx.translate(Math.round(shx),Math.round(shy));
 drawWorld(ctx);
 ctx.restore();
 renderLight();
 if(loc().out){ctx.strokeStyle='rgba(180,210,235,.4)';ctx.beginPath();
  rain.forEach(function(d){ctx.moveTo(d.x,d.y);ctx.lineTo(d.x-2,d.y+7)});ctx.stroke();
  ctx.fillStyle='rgba(200,225,245,.5)';splashes.forEach(function(s){ctx.fillRect(s.x-1,s.y,3,1)})}
 if(S.loc==='apartment'){ctx.strokeStyle='rgba(127,180,217,.35)';ctx.beginPath();
  for(var i=0;i<14;i++){var rx=96+((i*13+S.t*60)%48),ry=86+((i*29+S.t*140)%68);ctx.moveTo(rx,ry);ctx.lineTo(rx-1,ry+4)}ctx.stroke()}
 ctx.globalAlpha=.5;ctx.drawImage(grain[0],(Math.random()*64)|0,(Math.random()*64)|0,128,128,0,0,VW,VH);ctx.globalAlpha=1;
 if(S.lightF>0&&loc().out){ctx.fillStyle=rgba('#cfe8ff',S.lightF*.25);ctx.fillRect(0,0,VW,VH)}
 if(S.hurtF>0){ctx.fillStyle=rgba('#8e1f1f',S.hurtF*.25);ctx.fillRect(0,0,VW,VH)}
 if(dlgOn){ctx.fillStyle='#000';ctx.fillRect(0,0,VW,16);ctx.fillRect(0,VH-16,VW,16)}
 if(S.fade>0){ctx.fillStyle=rgba('#000',Math.min(1,S.fade));ctx.fillRect(0,0,VW,VH)}
}
/* ---------- HUD ---------- */
var hc={};
function setT(id,v){if(hc[id]!==v){hc[id]=v;$(id).textContent=v}}
function updateHUD(){
 $('hpFill').style.transform='scaleX('+(P.hp/100)+')';setT('hpNum',String(Math.ceil(P.hp)));
 var pips=$('ammoPips');if(pips.children.length!==8){pips.innerHTML='';for(var i=0;i<8;i++)pips.appendChild(document.createElement('span'))}
 for(var j=0;j<8;j++)pips.children[j].className=j<P.mag?'':'off';
 setT('resVal',String(P.res));
 var mi=missionInfo();setT('missionTitle',mi.title);setT('objVal',mi.obj);
 var td=targetDoor();
 if(td){var dir=td.x>P.x?1:-1;setT('compTxt',td.label+' '+Math.round(Math.abs(td.x-P.x)/10)+'م');
  $('compArrow').style.transform=dir>0?'scaleX(-1)':'none';$('compass').style.display='flex'}
 else if(mi.loc===S.loc&&M.idx<5){var dir2=mi.x>P.x?1:-1;setT('compTxt',mi.obj.slice(0,18)+' '+Math.round(Math.abs(mi.x-P.x)/10)+'م');
  $('compArrow').style.transform=dir2>0?'scaleX(-1)':'none';$('compass').style.display='flex'}
 else $('compass').style.display='none';
 var n=dlgOn?null:nearestInteract();
 if(n){$('promptTxt').textContent=n.label;$('prompt').classList.add('show')}
 else if(dlgOn){$('promptTxt').textContent='متابعة';$('prompt').classList.add('show')}
 else $('prompt').classList.remove('show');
}
var bnT=null;
function banner(n,s){$('bnName').textContent=n;$('bnSub').textContent=s;$('banner').classList.add('show');
 clearTimeout(bnT);bnT=setTimeout(function(){$('banner').classList.remove('show')},2200)}
var toastT=null;
function toast(m,c){var t=$('toast');t.textContent=m;t.className=c||'';void t.offsetWidth;t.classList.add('show');
 clearTimeout(toastT);toastT=setTimeout(function(){t.classList.remove('show')},2400)}
/* ---------- FLOW ---------- */
function setState(st){S.state=st;document.body.dataset.state=st;
 $('ovTitle').hidden=st!=='title';$('ovPause').hidden=st!=='paused';$('ovMap').hidden=st!=='map';
 $('ovDead').hidden=st!=='dead';$('ovWin').hidden=st!=='win';
 $('btnPause').disabled=!(st==='playing'||st==='paused');
 $('pauseIc').textContent=st==='paused'?'▶':'⏸';
 if(AC&&musG)musG.gain.linearRampToValueAtTime(st==='paused'||st==='map'?.1:.42,AC.currentTime+.3);
 if(st!=='playing'){input.fire=false;input.mx=0;document.querySelectorAll('.tc.held').forEach(function(b){b.classList.remove('held')});
  $('stickKnob').style.transform='translate(0,0)'}
}
function startRun(){
 M={idx:0,step:0,ambushDone:false,whClear:false,clClear:false};
 deadKeys={};takenKeys={};corpses={};bottleDead={};
 S.kills=0;S.shots=0;S.hits=0;S.bottles=0;S.deaths=0;S.elapsed=0;
 P.hp=100;P.mag=8;P.res=40;P.dead=false;P.relT=0;
 buildLocs();enterLoc('apartment',120,true);banner('شقة هنري',"HENRI'S APARTMENT — 2:47 AM");
 setState('playing');toast('افحص الهاتف… القضية تبدأ هناك','warn');sfx.sting();
}
function retry(){
 P.hp=100;P.mag=8;P.res=Math.max(P.res,32);P.dead=false;P.relT=0;P.ifr=1;
 var mi=missionInfo();
 for(var k in deadKeys)if(k.indexOf(mi.loc+':')===0)delete deadKeys[k];
 if(M.idx===1&&M.step===1)M.ambushDone=false;
 if(M.idx===2)M.whClear=false;
 enterLoc(mi.loc==='rooftop'?'alley':mi.loc,mi.loc==='street'?900:120,true);
 setState('playing');toast('انهض… المطر ما زال يهطل','warn');
}
function gameOver(){$('dKills').textContent=String(S.kills);
 $('dAcc').textContent=(S.shots?Math.round(S.hits/S.shots*100):0)+'%';setState('dead')}
function winGame(){
 var acc=S.shots?Math.round(S.hits/S.shots*100):0;
 var rank=acc>=60&&S.deaths===0?'S':acc>=45?'A':acc>=30?'B':'C';
 $('rankGlyph').textContent=rank;
 $('rankGlyph').style.color=rank==='S'?'#ffcf6e':rank==='A'?'#d99a2b':rank==='B'?'#5eead4':'#a89877';
 $('wTime').textContent=Math.floor(S.elapsed)+'s';$('wKills').textContent=String(S.kills);
 $('wAcc').textContent=acc+'%';$('wBottles').textContent=S.bottles+'/3';
 M.idx=5;setState('win');sfx.sting();
}
function openMap(){
 var mi=missionInfo(),html='';
 var icons={street:'🌧',apartment:'🏠',bar:'🍸',clinic:'🏥',warehouse:'📦',alley:'🪜',rooftop:'🌃'};
 var order=['street','apartment','bar','clinic','warehouse','alley','rooftop'];
 order.forEach(function(id){var L=LOCS[id],here=id===S.loc,tgt=mi.loc===id&&M.idx<5;
  html+='<div class="mapRow'+(here?' here':'')+(tgt?' target':'')+'"><span class="mi">'+icons[id]+'</span><span>'+L.name+'</span><span class="tag">'+(here?'أنت هنا':'')+(tgt?' ★ الهدف':'')+'</span></div>'});
 $('mapList').innerHTML=html;setState('map');
}
function closeMap(){setState('playing')}
function pauseGame(){if(S.state==='playing')setState('paused')}
function resumeGame(){if(S.state==='paused')setState('playing')}
function toMenu(){setState('title')}
/* ---------- LOOP ---------- */
var last=performance.now(),acc=0;
function loop(now){
 requestAnimationFrame(loop);
 var dt=Math.min(.05,(now-last)/1000);last=now;
 if(S.freeze>0)S.freeze-=dt;
 if(S.slowT>0){S.slowT-=dt;if(S.slowT<=0)S.ts=1}
 if(S.fade>0){S.fade-=dt*3;if(S.fade<=0&&S.fadeTo){var to=S.fadeTo,tx=S.fadeX;S.fadeTo=null;enterLoc(to,tx);S.fade=-1}
  if(S.fade<0){S.fade+=dt*3;if(S.fade>=0)S.fade=0}}
 var st=S.state;
 if(st==='playing'){if(S.freeze<=0){acc+=dt*S.ts;var g=0;while(acc>=STEP&&g<5){updatePlaying(STEP);acc-=STEP;g++}if(g>=5)acc=0}
  updAmbient(0);updateHUD()}
 else if(st==='title'){acc=0;S.t+=dt;updAmbient(dt);S.cam=(Math.sin(S.t*.05)*.5+.5)*(LOCS.street.w-VW)*.4}
 else if(st==='dead'||st==='win'){acc=0;updAmbient(dt);updParts(dt)}
 else acc=0;
 render();
}
/* ---------- INPUT ---------- */
var keys={};
addEventListener('keydown',function(e){unlock();
 if(e.code==='KeyM'){if(S.state==='playing')openMap();else if(S.state==='map')closeMap();return}
 if(e.code==='KeyP'||e.code==='Escape'){if(S.state==='playing')pauseGame();else if(S.state==='paused')resumeGame();else if(S.state==='map')closeMap();return}
 if(e.code==='Enter'){if(dlgOn){dlgNext();return}
  if(S.state==='title')startRun();else if(S.state==='dead')retry();else if(S.state==='win')setState('playing');return}
 if(e.code==='KeyE'){input.act=true;e.preventDefault();return}
 if(e.code==='KeyR'){input.rel=true;return}
 if(e.code==='KeyJ'||e.code==='Space'){input.fire=true;e.preventDefault();return}
 keys[e.code]=true;
 if(['Space','ArrowUp','ArrowDown','ArrowLeft','ArrowRight'].indexOf(e.code)>=0)e.preventDefault();
});
addEventListener('keyup',function(e){keys[e.code]=false;
 if(e.code==='KeyJ'||e.code==='Space')input.fire=false});
function pollKeys(){
 if(S.state!=='playing')return;
 var mx=(keys.KeyD||keys.ArrowRight?1:0)-(keys.KeyA||keys.ArrowLeft?1:0);
 if(mx)input.mx=mx;else if(!stickActive)input.mx=0;
 var aim=(keys.KeyS||keys.ArrowDown?1:0)-(keys.KeyW||keys.ArrowUp?1:0);
 if(aim)input.aim=aim;else if(!stickActive)input.aim=0;
}
setInterval(pollKeys,30);
/* stick */
var stickActive=false,stickId=null;
var stick=$('stick'),knob=$('stickKnob');
function stickMove(e){var r=stick.getBoundingClientRect(),cx=r.left+r.width/2,cy=r.top+r.height/2;
 var dx=(e.clientX-cx)/(r.width/2),dy=(e.clientY-cy)/(r.height/2);
 var l=Math.hypot(dx,dy);if(l>1){dx/=l;dy/=l}
 knob.style.transform='translate('+dx*26+'px,'+dy*26+'px)';
 input.mx=Math.abs(dx)>.2?dx:0;input.aim=Math.abs(dy)>.4?sgn(dy):0;}
stick.addEventListener('pointerdown',function(e){e.preventDefault();unlock();stickActive=true;stickId=e.pointerId;
 try{stick.setPointerCapture(e.pointerId)}catch(x){}stickMove(e)});
stick.addEventListener('pointermove',function(e){if(stickActive&&e.pointerId===stickId)stickMove(e)});
function stickUp(e){if(e.pointerId!==stickId)return;stickActive=false;stickId=null;input.mx=0;input.aim=0;knob.style.transform='translate(0,0)'}
stick.addEventListener('pointerup',stickUp);stick.addEventListener('pointercancel',stickUp);
function holdBtn(id,on,off){var b=$(id);
 b.addEventListener('pointerdown',function(e){e.preventDefault();unlock();b.classList.add('held');try{b.setPointerCapture(e.pointerId)}catch(x){}on()});
 function up(e){b.classList.remove('held');if(off)off()}
 b.addEventListener('pointerup',up);b.addEventListener('pointercancel',up);b.addEventListener('lostpointercapture',up);
 b.addEventListener('contextmenu',function(e){e.preventDefault()})}
holdBtn('btnFire',function(){input.fire=true},function(){input.fire=false});
holdBtn('btnAct',function(){input.act=true});
holdBtn('btnRel',function(){input.rel=true});
cv.addEventListener('pointerdown',function(e){unlock();if(dlgOn){dlgNext();return}});
$('dlg').addEventListener('pointerdown',function(e){e.preventDefault();unlock();dlgNext()});
addEventListener('pointerdown',unlock,{passive:true});
$('frame').addEventListener('contextmenu',function(e){e.preventDefault()});
document.addEventListener('visibilitychange',function(){if(document.hidden&&S.state==='playing')pauseGame();
 if(!document.hidden&&AC&&AC.state==='suspended')AC.resume()});
addEventListener('blur',function(){if(S.state==='playing')pauseGame()});
/* ---------- UI ---------- */
function bind(id,fn){$(id).addEventListener('click',function(e){unlock();sfx.ui();fn();e.currentTarget.blur()})}
bind('btnStart',startRun);
bind('btnResume',resumeGame);bind('btnRetryP',function(){setState('playing');retry()});
bind('btnMapP',openMap);bind('btnMenuP',toMenu);
bind('btnMap',function(){if(S.state==='playing')openMap();else if(S.state==='map')closeMap()});
bind('btnMapClose',closeMap);
bind('btnRetry',retry);bind('btnMenuD',toMenu);
bind('btnRoam',function(){setState('playing');toast('🌧 المدينة لك… تجول بحرية','big')});
bind('btnMenuW',toMenu);
bind('btnPause',function(){if(S.state==='playing')pauseGame();else if(S.state==='paused')resumeGame()});
$('btnSound').addEventListener('click',function(){unlock();setMuted(!muted);sfx.ui();this.blur()});
$('btnFull').addEventListener('click',function(){unlock();sfx.ui();var el=$('app');
 try{if(!document.fullscreenElement){if(el.requestFullscreen)el.requestFullscreen().catch(function(){})}else if(document.exitFullscreen)document.exitFullscreen()}catch(x){}this.blur()});
document.querySelectorAll('#diffPills .pill').forEach(function(p){
 p.addEventListener('click',function(){unlock();sfx.ui();S.diff=parseInt(p.dataset.d,10);LSs('cr_diff',String(S.diff));
  document.querySelectorAll('#diffPills .pill').forEach(function(q){q.setAttribute('aria-pressed',q===p?'true':'false')});p.blur()});
 p.setAttribute('aria-pressed',parseInt(p.dataset.d,10)===S.diff?'true':'false')});
setMuted(muted);
/* ---------- BOOT ---------- */
buildLocs();enterLoc('street',300,true);setState('title');
requestAnimationFrame(function(t){last=t;requestAnimationFrame(loop)});
})();
</script>
</body>
</html>
