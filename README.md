# worm-game
just a normal worm world.
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🪱 ЧЕРВЬ</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Unbounded:wght@300;400;700;900&family=Martian+Mono:wght@300;400;700&display=swap');

:root {
  --bg: #0a0602;
  --dirt1: #180e02;
  --dirt2: #221400;
  --green: #4ab84f;
  --green2: #7fd984;
  --orange: #f06000;
  --orange2: #ff9040;
  --text: #f2e8d0;
  --text2: #c8b898;
  --muted: rgba(242,232,208,0.38);
  --border: rgba(74,184,79,0.22);
  --glass: rgba(255,255,255,0.03);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  font-family: 'Unbounded', sans-serif;
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
}

body::after {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.025'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 999;
}

.crawler {
  position: fixed; font-size: 1.3rem;
  pointer-events: none; z-index: 1; opacity: 0.1;
  animation: crawl linear infinite;
}
@keyframes crawl {
  0%   { transform: translateX(-50px) scaleX(1); }
  49%  { transform: translateX(calc(100vw + 50px)) scaleX(1); }
  50%  { transform: translateX(calc(100vw + 50px)) scaleX(-1); }
  100% { transform: translateX(-50px) scaleX(-1); }
}

/* ── NAV ── */
nav {
  position: fixed; bottom: 0; left: 0; right: 0; z-index: 200;
  background: rgba(10,6,2,0.9);
  border-top: 1px solid var(--border);
  display: flex; justify-content: space-around;
  padding: 10px 0 18px;
  backdrop-filter: blur(28px);
}
.nav-btn {
  background: none; border: none; color: var(--muted);
  font-family: 'Unbounded', sans-serif;
  font-size: 0.44rem; letter-spacing: 0.08em;
  cursor: pointer; display: flex; flex-direction: column;
  align-items: center; gap: 5px; padding: 4px 10px;
  transition: color 0.22s; text-transform: uppercase; position: relative;
}
.nav-btn .icon { font-size: 1.3rem; transition: transform 0.22s; }
.nav-btn.active { color: var(--green2); }
.nav-btn.active .icon { transform: scale(1.2) translateY(-2px); }
.nav-btn.active::after {
  content: ''; position: absolute; bottom: -18px; left: 50%;
  transform: translateX(-50%); width: 28px; height: 2px;
  background: var(--green2); border-radius: 2px;
}
.nav-btn:hover { color: var(--text); }

/* ── PAGES ── */
.page { display: none; min-height: 100vh; padding: 46px 20px 100px; }
.page.active { animation: pgIn 0.35s ease both; }
@keyframes pgIn {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ══ HOME ══ */
#home {
  display: none; flex-direction: column;
  align-items: center; justify-content: center;
  text-align: center; min-height: 100vh;
  background:
    radial-gradient(ellipse 80% 55% at 50% 25%, rgba(74,184,79,0.07), transparent),
    radial-gradient(ellipse 60% 40% at 50% 90%, rgba(240,96,0,0.04), transparent);
}
#home.active { display: flex; }

.home-worm {
  font-size: 5.5rem;
  animation: homeWorm 3.5s ease-in-out infinite;
  margin-bottom: 16px;
  filter: drop-shadow(0 0 32px rgba(74,184,79,0.42));
}
@keyframes homeWorm {
  0%,100% { transform: rotate(-6deg) scale(1); }
  50%      { transform: rotate(6deg) scale(1.07); }
}
.home-title {
  font-size: clamp(3.2rem, 16vw, 9rem);
  font-weight: 900; letter-spacing: -0.04em; line-height: 0.86;
  color: var(--orange);
  text-shadow: 0 0 60px rgba(240,96,0,0.2);
  margin-bottom: 14px;
}
.home-sub {
  font-size: clamp(0.55rem, 1.6vw, 0.72rem);
  letter-spacing: 0.38em; color: var(--green2);
  text-transform: uppercase; margin-bottom: 44px; opacity: 0.72;
}
.home-quote {
  max-width: 380px;
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.82rem, 2.4vw, 1rem);
  line-height: 1.85; color: var(--text2);
  border-left: 2px solid var(--green);
  padding-left: 18px; text-align: left;
}
.home-pill {
  margin-top: 36px;
  display: inline-flex; align-items: center; gap: 10px;
  background: var(--glass); border: 1px solid var(--border);
  border-radius: 100px; padding: 8px 20px; backdrop-filter: blur(12px);
}
.home-pill span { font-size: 0.5rem; letter-spacing: 0.18em; color: var(--muted); text-transform: uppercase; }
.home-pill .dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--green2); box-shadow: 0 0 8px var(--green2);
  animation: dotBlink 1.8s ease infinite;
}
@keyframes dotBlink { 0%,100%{opacity:1}50%{opacity:0.3} }

/* ══ SECTION HEADER ══ */
.sh { text-align: center; margin-bottom: 32px; }
.sh h2 {
  font-size: clamp(1.5rem, 5.5vw, 2.4rem);
  font-weight: 900; color: var(--orange);
  letter-spacing: -0.02em; margin-bottom: 8px;
}
.sh p {
  font-size: 0.52rem; letter-spacing: 0.3em;
  color: var(--green2); text-transform: uppercase; opacity: 0.62;
}

/* ══ WISDOM ══ */
#wisdom { display: none; flex-direction: column; align-items: center; }
#wisdom.active { display: flex; }

.wisdom-card {
  background: linear-gradient(145deg, rgba(34,20,0,0.92), rgba(10,6,2,0.96));
  border: 1px solid var(--border);
  max-width: 560px; width: 100%;
  padding: 28px 28px 32px;
  margin-bottom: 12px;
  position: relative; cursor: pointer; overflow: hidden;
  transition: transform 0.25s cubic-bezier(0.34,1.56,0.64,1), border-color 0.2s, box-shadow 0.2s;
}
.wisdom-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(127,217,132,0.35), transparent);
}
.wisdom-card:hover {
  transform: translateY(-4px) translateX(2px);
  border-color: rgba(127,217,132,0.4);
  box-shadow: 0 14px 40px rgba(0,0,0,0.5);
}
.worm-tag {
  font-size: 0.5rem; letter-spacing: 0.25em;
  color: var(--green2); text-transform: uppercase;
  margin-bottom: 12px; opacity: 0.6;
}
.wisdom-text {
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.85rem, 2.4vw, 1rem);
  line-height: 1.9; color: var(--text);
}
.wisdom-text em { color: var(--orange2); font-style: normal; font-weight: 700; }
.wisdom-card::after {
  content: '🪱'; position: absolute;
  bottom: -11px; right: 12px; font-size: 1.1rem;
  animation: wiggle 2.3s ease-in-out infinite;
}
@keyframes wiggle { 0%,100%{transform:rotate(-16deg)} 50%{transform:rotate(16deg) scaleX(-1)} }

/* ══ ORACLE ══ */
#oracle { display: none; flex-direction: column; align-items: center; }
#oracle.active { display: flex; }

.oracle-wrap { position: relative; margin: 10px auto 24px; }
.oracle-ball {
  width: min(230px, 62vw); height: min(230px, 62vw);
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, #0f1f0f, #060d06, #010201);
  border: 1.5px solid rgba(74,184,79,0.45);
  display: flex; align-items: center; justify-content: center;
  position: relative; overflow: hidden;
  box-shadow: 0 0 50px rgba(74,184,79,0.14), inset 0 0 60px rgba(0,0,0,0.65);
  cursor: pointer;
  transition: transform 0.2s cubic-bezier(0.34,1.56,0.64,1), box-shadow 0.2s;
}
.oracle-ball:hover {
  transform: scale(1.05);
  box-shadow: 0 0 70px rgba(74,184,79,0.25), inset 0 0 60px rgba(0,0,0,0.65);
}
.oracle-ball:active { transform: scale(0.92); }
.oracle-glow {
  position: absolute; inset: 0; border-radius: 50%;
  background: radial-gradient(circle at 28% 26%, rgba(74,184,79,0.14), transparent 52%);
  pointer-events: none;
}
.oracle-worm {
  font-size: 3.6rem; z-index: 2;
  filter: drop-shadow(0 0 16px rgba(74,184,79,0.5));
  animation: orbWorm 2.8s ease-in-out infinite;
}
@keyframes orbWorm { 0%,100%{transform:rotate(-5deg) scale(1)} 50%{transform:rotate(5deg) scale(1.09)} }
.oracle-ring {
  position: absolute; border-radius: 50%;
  border: 1px solid rgba(74,184,79,0.09);
  animation: ringP 3.5s ease-in-out infinite; pointer-events: none;
}
.oracle-ring:nth-child(1) { inset: -16px; animation-delay: 0s; }
.oracle-ring:nth-child(2) { inset: -32px; animation-delay: 0.7s; }
.oracle-ring:nth-child(3) { inset: -50px; animation-delay: 1.4s; }
@keyframes ringP { 0%,100%{opacity:0.15}50%{opacity:0.42} }

.oracle-hint {
  font-size: 0.52rem; letter-spacing: 0.3em; color: var(--green2);
  text-transform: uppercase; margin-bottom: 22px; opacity: 0.52;
  animation: hintP 2.2s ease-in-out infinite;
}
@keyframes hintP { 0%,100%{opacity:0.3}50%{opacity:0.65} }

.oracle-answer {
  max-width: 480px; width: 100%;
  background: linear-gradient(145deg, rgba(34,20,0,0.92), rgba(10,6,2,0.96));
  border: 1px solid var(--border);
  padding: 24px 24px; min-height: 90px;
  display: flex; flex-direction: column; justify-content: center;
  transition: opacity 0.28s; position: relative; overflow: hidden;
}
.oracle-answer::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(74,184,79,0.3), transparent);
}
.ans-tag {
  font-size: 0.48rem; letter-spacing: 0.26em; color: var(--green2);
  text-transform: uppercase; margin-bottom: 12px; opacity: 0.55;
}
.ans-text {
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.85rem, 2.4vw, 1rem);
  line-height: 1.85; color: var(--text);
}
.ans-text em { color: var(--orange2); font-style: normal; font-weight: 700; }
.oracle-answer.fading { opacity: 0; }
.oracle-answer::after {
  content: '🪱'; position: absolute;
  bottom: -11px; right: 12px; font-size: 1rem;
  animation: wiggle 2s ease-in-out infinite;
}

/* ══ FACTS ══ */
#facts { display: none; flex-direction: column; align-items: center; }
#facts.active { display: flex; }
.fact-grid { max-width: 560px; width: 100%; display: flex; flex-direction: column; gap: 10px; }
.fact-item {
  background: rgba(24,14,2,0.75);
  border-left: 2.5px solid var(--green);
  padding: 20px 22px 20px 22px;
  display: flex; gap: 16px; align-items: flex-start;
  transition: background 0.2s, border-color 0.2s;
}
.fact-item:hover { background: rgba(34,20,0,0.92); border-color: var(--green2); }
.fact-num {
  font-family: 'Martian Mono', monospace; font-size: 0.58rem;
  color: var(--green); opacity: 0.5; min-width: 22px; padding-top: 2px; flex-shrink: 0;
}
.fact-body {
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.82rem, 2.2vw, 0.95rem);
  line-height: 1.8; color: var(--text);
}
.fact-body em { color: var(--orange2); font-style: normal; }

/* ══ GAME ══ */
#game { display: none; flex-direction: column; align-items: center; }
#game.active { display: flex; }

.game-area {
  max-width: 480px; width: 100%;
  background: linear-gradient(180deg, rgba(10,20,10,0.95), rgba(24,14,2,0.95));
  border: 1px solid var(--border);
  padding: 28px 24px;
  position: relative; overflow: hidden;
  margin-bottom: 14px;
}
.game-area::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(127,217,132,0.35), transparent);
}

.game-worm-display {
  text-align: center; margin-bottom: 20px;
}
.game-worm-emoji {
  font-size: clamp(3.5rem, 14vw, 6rem);
  display: block; margin-bottom: 8px;
  animation: gameWorm 2s ease-in-out infinite;
  filter: drop-shadow(0 0 20px rgba(74,184,79,0.4));
  transition: transform 0.15s;
}
@keyframes gameWorm {
  0%,100% { transform: rotate(-4deg); }
  50%      { transform: rotate(4deg); }
}
.game-worm-emoji.nom {
  animation: nom 0.3s ease;
}
@keyframes nom {
  0%   { transform: scale(1) rotate(0deg); }
  30%  { transform: scale(1.35) rotate(-8deg); }
  60%  { transform: scale(0.9) rotate(4deg); }
  100% { transform: scale(1) rotate(0deg); }
}

.game-worm-name {
  font-size: clamp(1rem, 4vw, 1.4rem);
  font-weight: 900; color: var(--orange2);
  margin-bottom: 4px; letter-spacing: -0.01em;
}
.game-worm-mood {
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.72rem, 2vw, 0.85rem);
  color: var(--text2); line-height: 1.5;
}

/* stats bars */
.game-stats { margin-bottom: 22px; display: flex; flex-direction: column; gap: 12px; }
.stat-row { display: flex; flex-direction: column; gap: 6px; }
.stat-row-label {
  display: flex; justify-content: space-between; align-items: center;
}
.stat-row-label span:first-child {
  font-size: 0.5rem; letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--text2); opacity: 0.7;
}
.stat-row-label span:last-child {
  font-family: 'Martian Mono', monospace;
  font-size: 0.62rem; color: var(--text2);
}
.bar-track {
  height: 6px; background: rgba(255,255,255,0.06);
  border-radius: 3px; overflow: hidden;
}
.bar-fill {
  height: 100%; border-radius: 3px;
  transition: width 0.5s cubic-bezier(0.34,1.56,0.64,1);
}
.bar-hunger { background: linear-gradient(90deg, var(--orange), var(--orange2)); }
.bar-happy  { background: linear-gradient(90deg, var(--green), var(--green2)); }
.bar-size   { background: linear-gradient(90deg, #7b61ff, #b8a9ff); }

/* food buttons */
.food-grid {
  display: grid; grid-template-columns: repeat(3, 1fr);
  gap: 8px; margin-bottom: 16px;
}
.food-btn {
  background: rgba(34,20,0,0.8);
  border: 1px solid var(--border);
  border-radius: 4px; padding: 12px 6px;
  cursor: pointer; text-align: center;
  transition: all 0.18s; display: flex;
  flex-direction: column; align-items: center; gap: 5px;
}
.food-btn:hover {
  border-color: rgba(127,217,132,0.45);
  background: rgba(50,30,0,0.9);
  transform: translateY(-2px);
}
.food-btn:active { transform: scale(0.93); }
.food-btn .food-emoji { font-size: 1.8rem; }
.food-btn .food-name {
  font-size: 0.44rem; letter-spacing: 0.1em;
  color: var(--text2); text-transform: uppercase;
}
.food-btn .food-pts {
  font-family: 'Martian Mono', monospace;
  font-size: 0.5rem; color: var(--green2);
}

/* action buttons */
.action-row { display: flex; gap: 8px; }
.act-btn {
  flex: 1; background: rgba(34,20,0,0.8);
  border: 1px solid var(--border);
  padding: 12px 8px; cursor: pointer;
  font-family: 'Unbounded', sans-serif;
  font-size: 0.48rem; letter-spacing: 0.08em;
  color: var(--text2); text-transform: uppercase;
  transition: all 0.18s; text-align: center;
}
.act-btn:hover { border-color: rgba(127,217,132,0.45); color: var(--green2); }
.act-btn:active { transform: scale(0.95); }

/* log */
.game-log {
  max-width: 480px; width: 100%;
  background: rgba(10,6,2,0.8);
  border: 1px solid var(--border);
  padding: 16px 18px;
  max-height: 130px; overflow-y: auto;
}
.game-log::-webkit-scrollbar { width: 3px; }
.game-log::-webkit-scrollbar-track { background: transparent; }
.game-log::-webkit-scrollbar-thumb { background: var(--green); border-radius: 2px; }
.log-entry {
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.7rem, 1.9vw, 0.82rem);
  color: var(--text2); line-height: 1.6;
  padding: 3px 0; opacity: 0;
  animation: logIn 0.3s ease forwards;
}
.log-entry:not(:last-child) { border-bottom: 1px solid rgba(255,255,255,0.04); }
.log-entry.good { color: var(--green2); }
.log-entry.bad  { color: #ff6b6b; }
.log-entry.wow  { color: var(--orange2); }
@keyframes logIn { from{opacity:0;transform:translateX(-6px)} to{opacity:1;transform:none} }

/* ══ ABOUT ══ */
#about { display: none; flex-direction: column; align-items: center; }
#about.active { display: flex; }

.about-portrait {
  width: 115px; height: 115px; border-radius: 50%;
  background: radial-gradient(circle at 35% 35%, var(--dirt2), var(--bg));
  border: 1.5px solid rgba(240,96,0,0.5);
  display: flex; align-items: center; justify-content: center;
  font-size: 3.8rem; margin-bottom: 20px;
  box-shadow: 0 0 40px rgba(240,96,0,0.14);
  animation: homeWorm 3.5s ease-in-out infinite;
}
.about-name {
  font-size: clamp(1.6rem, 6.5vw, 2.8rem); font-weight: 900;
  color: var(--orange); letter-spacing: -0.02em; margin-bottom: 6px;
}
.about-role {
  font-size: 0.56rem; letter-spacing: 0.28em; color: var(--green2);
  text-transform: uppercase; margin-bottom: 32px; opacity: 0.65;
}
.stat-grid {
  max-width: 480px; width: 100%;
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 8px; margin-bottom: 24px;
}
.stat-box {
  background: rgba(24,14,2,0.75); border: 1px solid var(--border);
  padding: 18px 14px; text-align: center;
  transition: border-color 0.2s, background 0.2s;
}
.stat-box:hover { border-color: rgba(127,217,132,0.35); background: rgba(34,20,0,0.92); }
.stat-val {
  font-size: clamp(1.3rem, 4vw, 2rem); font-weight: 900;
  color: var(--orange2); display: block; margin-bottom: 5px;
}
.stat-label { font-size: 0.48rem; letter-spacing: 0.18em; color: var(--muted); text-transform: uppercase; }
.about-bio {
  max-width: 480px; width: 100%;
  font-family: 'Martian Mono', monospace;
  font-size: clamp(0.82rem, 2.2vw, 0.95rem);
  line-height: 2; color: var(--text2);
  background: rgba(24,14,2,0.75);
  border-left: 2.5px solid var(--green);
  padding: 24px 24px;
}
.about-bio em { color: var(--orange2); font-style: normal; }
</style>
</head>
<body>

<div class="crawler" style="top:7%;  animation-duration:15s; animation-delay:0s">🪱</div>
<div class="crawler" style="top:29%; animation-duration:11s; animation-delay:3s">🪱</div>
<div class="crawler" style="top:54%; animation-duration:18s; animation-delay:7s">🪱</div>
<div class="crawler" style="top:76%; animation-duration:13s; animation-delay:2s">🪱</div>

<!-- HOME -->
<div class="page active" id="home">
  <div class="home-worm">🪱</div>
  <div class="home-title">ЧЕРВЬ</div>
  <div class="home-sub">официальное приложение 🪱 2026</div>
  <div class="home-quote" id="homeQuote">загружаем мудрость...</div>
  <div class="home-pill">
    <div class="dot"></div>
    <span>червь онлайн · земля в порядке</span>
  </div>
</div>

<!-- WISDOM -->
<div class="page" id="wisdom">
  <div class="sh"><h2>МУДРОСТЬ</h2><p>🪱 червь сказал 🪱</p></div>
  <div id="wisdomList"></div>
</div>

<!-- ORACLE -->
<div class="page" id="oracle">
  <div class="sh"><h2>ОРАКУЛ</h2><p>🪱 спроси червя 🪱</p></div>
  <div class="oracle-wrap">
    <div class="oracle-ring"></div>
    <div class="oracle-ring"></div>
    <div class="oracle-ring"></div>
    <div class="oracle-ball" onclick="askOracle()">
      <div class="oracle-glow"></div>
      <div class="oracle-worm" id="oracleWorm">🪱</div>
    </div>
  </div>
  <div class="oracle-hint">нажми на червя</div>
  <div class="oracle-answer" id="oracleAnswer">
    <div class="ans-tag">🪱 червь говорит</div>
    <div class="ans-text" id="ansText">нажми на червя. <em>он ждёт.</em></div>
  </div>
</div>

<!-- FACTS -->
<div class="page" id="facts">
  <div class="sh"><h2>ФАКТЫ</h2><p>🪱 научно доказано 🪱</p></div>
  <div class="fact-grid" id="factGrid"></div>
</div>

<!-- GAME -->
<div class="page" id="game">
  <div class="sh"><h2>КОРМИТЬ ЧЕРВЯ</h2><p>🪱 тамагочи · 2026 🪱</p></div>

  <div class="game-area">
    <div class="game-worm-display">
      <span class="game-worm-emoji" id="gameWormEmoji">🪱</span>
      <div class="game-worm-name" id="gameWormName">Червяк</div>
      <div class="game-worm-mood" id="gameWormMood">смотрит на тебя. ждёт.</div>
    </div>


    <div class="game-stats">
      <div class="stat-row">
        <div class="stat-row-label">
          <span>🍽️ голод</span>
          <span id="hungerVal">50%</span>
        </div>
        <div class="bar-track"><div class="bar-fill bar-hunger" id="hungerBar" style="width:50%"></div></div>
      </div>
      <div class="stat-row">
        <div class="stat-row-label">
          <span>😊 счастье</span>
          <span id="happyVal">70%</span>
        </div>
        <div class="bar-track"><div class="bar-fill bar-happy" id="happyBar" style="width:70%"></div></div>
      </div>
      <div class="stat-row">
        <div class="stat-row-label">
          <span>📏 размер</span>
          <span id="sizeVal">1</span>
        </div>
        <div class="bar-track"><div class="bar-fill bar-size" id="sizeBar" style="width:10%"></div></div>
      </div>
    </div>

    <div class="food-grid">
      <button class="food-btn" onclick="feed('dirt')">
        <span class="food-emoji">🌱</span>
        <span class="food-name">земля</span>
        <span class="food-pts">+15 еда</span>
      </button>
      <button class="food-btn" onclick="feed('cucumber')">
        <span class="food-emoji">🥒</span>
        <span class="food-name">огурец</span>
        <span class="food-pts">+25 всё</span>
      </button>
      <button class="food-btn" onclick="feed('apple')">
        <span class="food-emoji">🍎</span>
        <span class="food-name">яблоко</span>
        <span class="food-pts">+20 еда</span>
      </button>
      <button class="food-btn" onclick="feed('leaf')">
        <span class="food-emoji">🍃</span>
        <span class="food-name">листик</span>
        <span class="food-pts">+10 счастье</span>
      </button>
      <button class="food-btn" onclick="feed('mushroom')">
        <span class="food-emoji">🍄</span>
        <span class="food-name">гриб</span>
        <span class="food-pts">+30 еда!</span>
      </button>
      <button class="food-btn" onclick="feed('bread')">
        <span class="food-emoji">🍞</span>
        <span class="food-name">хлеб</span>
        <span class="food-pts">+18 еда</span>
      </button>
    </div>

    <div class="action-row">
      <button class="act-btn" onclick="petWorm()">🤝 погладить</button>
      <button class="act-btn" onclick="talkWorm()">💬 поговорить</button>
      <button class="act-btn" onclick="sleepWorm()">😴 спать</button>
    </div>
  </div>

  <div class="game-log" id="gameLog">
    <div class="log-entry">🪱 червь появился. смотрит на тебя. ждёт огурец.</div>
  </div>
</div>
<!-- ABOUT -->
<div class="page" id="about">
  <div class="about-portrait">🪱</div>
  <div class="about-name">ЧЕРВЬ</div>
  <div class="about-role">философ · оракул · сосед · 2026</div>
  <div class="stat-grid">
    <div class="stat-box"><span class="stat-val">∞</span><span class="stat-label">лет мудрости</span></div>
    <div class="stat-box"><span class="stat-val">0</span><span class="stat-label">плохих дней</span></div>
    <div class="stat-box"><span class="stat-val">🥒</span><span class="stat-label">любимая еда</span></div>
    <div class="stat-box"><span class="stat-val">🌍</span><span class="stat-label">место работы</span></div>
  </div>
  <div class="about-bio">
    червь живёт в земле с начала времён.<br>
    не торопится. не жалуется. <em>просто живёт.</em><br><br>
    видел динозавров. не впечатлился.<br>
    видел людей. <em>заинтересовался.</em><br><br>
    лучший сосед которого у тебя никогда не было.<br>
    знает твой пароль. не использует.<br>
    <em>это называется уважение.</em>
  </div>
</div>

<nav>
  <button class="nav-btn active" onclick="showPage('home',this)"><span class="icon">🏠</span>главная</button>
  <button class="nav-btn" onclick="showPage('wisdom',this)"><span class="icon">🧠</span>мудрость</button>
  <button class="nav-btn" onclick="showPage('oracle',this)"><span class="icon">🔮</span>оракул</button>
  <button class="nav-btn" onclick="showPage('game',this)"><span class="icon">🪱</span>кормить</button>
  <button class="nav-btn" onclick="showPage('facts',this)"><span class="icon">📋</span>факты</button>
</nav>

<script>
// ═══════════════════════════
//  DATA
// ═══════════════════════════
const wisdom = [
  { tag: 'о жизни',    text: 'червь живёт в темноте и делает землю лучше. никто не видит. никто не говорит спасибо. он всё равно делает. <em>подумай об этом.</em>' },
  { tag: 'о времени',  text: 'червь не торопится. земля никуда не денется. <em>ты тоже не торопись.</em> всё успеется.' },
  { tag: 'о смысле',   text: 'смысл не приходит когда ждёшь. приходит когда ешь бутерброд в 2 ночи и смотришь в окно. <em>червь проверил.</em>' },
  { tag: 'о себе',     text: 'червь не сравнивает себя с другими червями. они все в разной земле. <em>ты тоже в своей земле.</em>' },
  { tag: 'о темноте',  text: 'темнота в которой живёт червь — это не наказание. это просто его мир. <em>у каждого свой мир.</em>' },
  { tag: 'об ошибках', text: 'червь сделал ошибку. земля не провалилась. он пополз дальше. <em>земля стала лучше.</em>' },
  { tag: 'о цели',     text: 'червь не красивый. не быстрый. не громкий. но земля без него умрёт. <em>иногда самое важное выглядит вот так.</em>' },
  { tag: 'о страхе',   text: 'страшно идти вперёд. червь тоже не видит куда ползёт. <em>всё равно ползёт.</em>' },
];

const oracleAnswers = [
  'червь говорит: <em>да.</em> но ты уже знала.',
  'ответ в земле. <em>иди ищи.</em>',
  'червь молчит три минуты. потом кивает. <em>это хороший знак.</em>',
  'червь видел как это заканчивается. <em>не переживай.</em>',
  'вопрос хороший. ответ ещё лучше. червь <em>пока не скажет.</em>',
  'червь прополз всю землю ради этого ответа: <em>просто живи.</em>',
  'спроси позже. червь ест. <em>огурец.</em>',
  'да. нет. может быть. <em>червь уклончив сегодня.</em>',
  'ты уже знаешь ответ. червь тоже знает. <em>вы оба знаете.</em>',
  'червь говорит: не туда смотришь. <em>повернись.</em>',
  'ответ придёт сам. как червь после дождя. <em>неожиданно и вовремя.</em>',
  'червь думал об этом 200 миллионов лет. <em>всё будет нормально.</em>',
  'червь посмотрел в твои глаза. увидел ответ. <em>ты тоже видела. просто не поверила.</em>',
  'земля говорит да. небо говорит подожди. червь говорит: <em>слушай землю.</em>',
  'это произойдёт. не сейчас. но <em>произойдёт.</em>',
  'червь видел тысячи таких ситуаций. все они закончились. <em>эта тоже закончится.</em>',
  'не спрашивай когда. спрашивай <em>зачем.</em> червь уже знает ответ на второй вопрос.',
  'огурец сказал нет. лосось сказал подумай. червь сказал: <em>делай что хочешь. я рядом.</em>',
  'червь молчит. но его молчание значит: <em>иди. просто иди.</em>',
  'три раза спросишь — три раза скажет одно и то же. <em>потому что ответ один.</em>',
  'червь видел как вселенная создавалась. и разрушалась. и снова. <em>это нормально.</em>',
  'сегодня не день для ответов. <em>сегодня день для вопросов.</em>',
  'червь знает твоё прошлое. не осуждает. <em>вообще не осуждает.</em>',
  'ответ: <em>да, но позже.</em> червь уточнять не будет.',
  'иногда червь просто смотрит в темноту. и темнота смотрит обратно. <em>это и есть ответ.</em>',
  'червь уснул пока думал. проснулся с ответом. ответ: <em>всё хорошо.</em>',
  'ты спрашиваешь сердцем или головой? червь отвечает <em>только сердцу.</em>',
  'червь говорит: земля тёплая сегодня. <em>хороший знак.</em>',
  'нет. подожди. снова нет. подожди дольше. <em>теперь да.</em>',
  'червь засмеялся. у червей нет рта. <em>но он засмеялся.</em>',
];

const facts = [
  { text: 'червь существует <em>600 миллионов лет.</em> пережил всё. включая динозавров. включая понедельники.' },
  { text: 'один червь улучшает <em>тонну земли в год.</em> молча. без резюме. без linkedin.' },
  { text: 'червь не имеет мозга в привычном смысле. <em>принимает лучшие решения из всех.</em>' },
  { text: 'если разрезать червя — <em>зависит от вида.</em> червь просит не проверять.' },
  { text: 'червь чувствует вибрации земли. <em>знает когда ты идёшь.</em> всегда знал.' },
  { text: 'дарвин изучал червей <em>40 лет.</em> написал книгу. червь книгу не читал. и так всё знает.' },
  { text: 'червь дышит через кожу. <em>никаких лишних органов.</em> эффективность максимальная.' },
  { text: 'без червей не было бы почвы. без почвы не было бы еды. <em>без еды не было бы тебя.</em> ты должна червю.' },
];

const homeQuotes = [
  'червь не ждёт когда станет лучше. делает лучше прямо сейчас. прямо в темноте.',
  'просыпаешься. червь уже не спал. он никогда не спит. он ждал.',
  'жизнь это не пункт назначения. это просто земля которую ты проходишь.',
  'червь знает твой пароль от всего. не использует. это называется доверие.',
];

// ═══════════════════════════
//  BUILD STATIC CONTENT
// ═══════════════════════════
const wl = document.getElementById('wisdomList');
wisdom.forEach(w => {
  const d = document.createElement('div');
  d.className = 'wisdom-card';
  d.innerHTML = `<div class="worm-tag">🪱 ${w.tag}</div><div class="wisdom-text">${w.text}</div>`;
  wl.appendChild(d);
});

const fg = document.getElementById('factGrid');
facts.forEach((f, i) => {
  const d = document.createElement('div');
  d.className = 'fact-item';
  d.innerHTML = `<span class="fact-num">0${i+1}</span><div class="fact-body">${f.text}</div>`;
  fg.appendChild(d);
});

document.getElementById('homeQuote').textContent = homeQuotes[Math.floor(Math.random()*homeQuotes.length)];

// ═══════════════════════════
//  ORACLE
// ═══════════════════════════
let used = [];
function askOracle() {
  const ball = document.querySelector('.oracle-ball');
  const ans  = document.getElementById('oracleAnswer');
  const txt  = document.getElementById('ansText');

  ball.style.transform = 'scale(0.90)';
  setTimeout(() => ball.style.transform = '', 180);

  ans.classList.add('fading');
  setTimeout(() => {
    if (used.length === oracleAnswers.length) used = [];
    let idx;
    do { idx = Math.floor(Math.random() * oracleAnswers.length); } while (used.includes(idx));
    used.push(idx);
    txt.innerHTML = oracleAnswers[idx];
    ans.classList.remove('fading');
  }, 280);
}

// ═══════════════════════════
//  GAME
// ═══════════════════════════
const WORM_NAMES = ['Червяк','Борис','Земляша','Огурчик','Тьма','Глубина','Мудрец','Червиус'];
let worm = {
  name: WORM_NAMES[Math.floor(Math.random()*WORM_NAMES.length)],
  hunger: 50, happy: 70, size: 1, maxSize: 20,
  sleeping: false,
};

document.getElementById('gameWormName').textContent = worm.name;
const foods = {
  dirt:     { hunger: 15, happy: 5,  size: 1, msgs: ['ам. земля. <em>нормально.</em>', 'привычная еда. червь доволен.', 'земля в порядке. как всегда.'] },
  cucumber: { hunger: 25, happy: 20, size: 2, msgs: ['🥒 ОГУРЕЦ! червь в <em>восторге.</em>', 'огурец — лучшее что было в этой жизни.', 'червь плакал от счастья. <em>внутри.</em>'] },
  apple:    { hunger: 20, happy: 10, size: 1, msgs: ['яблоко. неплохо. <em>не огурец.</em>', 'кисловато. но червь не жалуется.', 'яблоко съедено. червь размышляет.'] },
  leaf:     { hunger: 5,  happy: 15, size: 0, msgs: ['листик! <em>как вкусно.</em>', 'червь танцует. у него нет ног. <em>всё равно танцует.</em>', 'листик напомнил о лете.'] },
  mushroom: { hunger: 30, happy: 5,  size: 2, msgs: ['гриб! большой! <em>червь справился.</em>', 'это был серьёзный гриб. червь серьёзный червь.', 'гриб съеден. земля уважает.'] },
  bread:    { hunger: 18, happy: 8,  size: 1, msgs: ['хлеб. простая еда. <em>лучшая еда.</em>', 'кто-то ел бутерброд и уронил. <em>червь не осуждает.</em>', 'хлеб есть хлеб. червь съел.'] },
};

const petMsgs = [
  'червь зажмурился. <em>приятно.</em>',
  'погладила червя. червь не против. <em>продолжай.</em>',
  'червь покраснел. у него нет кожи. <em>всё равно покраснел.</em>',
  'это было неожиданно. <em>в хорошем смысле.</em>',
  'червь запомнил этот момент. <em>навсегда.</em>',
];

const talkMsgs = [
  ['о чём говорили? неважно. <em>червь слушал.</em>', 'good'],
  ['червь кивнул. потом ещё раз. <em>он понял всё.</em>', 'good'],
  ['червь рассказал про землю. ты слушала? <em>он заметил.</em>', 'good'],
  ['разговор был хорошим. тишина после — <em>ещё лучше.</em>', 'wow'],
  ['червь сказал кое-что важное. на языке червей. <em>смотри в оба.</em>', 'wow'],
];

const sleepMsgs = [
  'червь уснул. <em>наконец-то.</em>',
  'zzz... червь видит сны о земле.',
  'спит. не беспокоить. <em>серьёзно.</em>',
];

function getMoodText() {
  const h = worm.hunger, hp = worm.happy, s = worm.size;
  if (h < 20) return 'голодный. смотрит на тебя. намёк понят?';
  if (hp < 20) return 'грустно. нужен огурец или разговор.';
  if (hp > 85 && h > 80) return `счастливый толстый червь. уровень ${s}. доволен.`;
  if (s >= 15) return 'большой мудрый червь. почти легенда.';
  if (worm.sleeping) return 'спит. не трогай. зzzz...';
  return ['смотрит на тебя. ждёт.','думает о земле.','просто существует.','наблюдает.'][Math.floor(Math.random()*4)];
}

function getWormEmoji() {
  if (worm.size >= 18) return '🐍';
  if (worm.size >= 12) return '🪱🪱';
  if (worm.size >= 6)  return '🪱';
  return '🪱';
}

function updateUI() {
  const h = Math.max(0, Math.min(100, worm.hunger));
  const hp = Math.max(0, Math.min(100, worm.happy));
  const s = Math.min(100, (worm.size / worm.maxSize) * 100);

  document.getElementById('hungerBar').style.width = h + '%';
  document.getElementById('happyBar').style.width = hp + '%';
  document.getElementById('sizeBar').style.width = s + '%';
  document.getElementById('hungerVal').textContent = Math.round(h) + '%';
  document.getElementById('happyVal').textContent = Math.round(hp) + '%';
  document.getElementById('sizeVal').textContent = worm.size;
  document.getElementById('gameWormMood').innerHTML = getMoodText();
  document.getElementById('gameWormEmoji').textContent = getWormEmoji();
}

function addLog(msg, type = '') {
  const log = document.getElementById('gameLog');
  const entry = document.createElement('div');
  entry.className = 'log-entry' + (type ? ' ' + type : '');
  entry.innerHTML = msg;
  log.insertBefore(entry, log.firstChild);
  while (log.children.length > 12) log.removeChild(log.lastChild);
}
function nomAnim() {
  const el = document.getElementById('gameWormEmoji');
  el.classList.remove('nom');
  void el.offsetWidth;
  el.classList.add('nom');
  setTimeout(() => el.classList.remove('nom'), 400);
}

function feed(type) {
  if (worm.sleeping) { addLog('червь спит. подожди.', 'bad'); return; }
  const f = foods[type];
  worm.hunger = Math.min(100, worm.hunger + f.hunger);
  worm.happy  = Math.min(100, worm.happy  + f.happy);
  if (worm.hunger > 90 && f.size > 0) {
    worm.size = Math.min(worm.maxSize, worm.size + f.size);
    if (f.size > 0) addLog(`🎉 червь вырос! теперь уровень <em>${worm.size}</em>`, 'wow');
  }
  nomAnim();
  const msg = f.msgs[Math.floor(Math.random() * f.msgs.length)];
  addLog(msg, type === 'cucumber' ? 'wow' : 'good');
  updateUI();
}

function petWorm() {
  if (worm.sleeping) { worm.sleeping = false; addLog('червь проснулся. не очень доволен. но простил.', 'bad'); updateUI(); return; }
  worm.happy = Math.min(100, worm.happy + 12);
  addLog(petMsgs[Math.floor(Math.random()*petMsgs.length)], 'good');
  updateUI();
}

function talkWorm() {
  if (worm.sleeping) { addLog('червь спит. он тебя слышит. но не отвечает.', ''); return; }
  worm.happy = Math.min(100, worm.happy + 8);
  const [msg, type] = talkMsgs[Math.floor(Math.random()*talkMsgs.length)];
  addLog(msg, type);
  updateUI();
}

function sleepWorm() {
  if (worm.sleeping) { addLog('червь уже спит. ты разбудила его. он смотрит.', 'bad'); worm.sleeping = false; updateUI(); return; }
  worm.sleeping = true;
  addLog(sleepMsgs[Math.floor(Math.random()*sleepMsgs.length)], '');
  setTimeout(() => {
    if (worm.sleeping) {
      worm.hunger = Math.min(100, worm.hunger + 20);
      worm.happy  = Math.min(100, worm.happy + 15);
      worm.sleeping = false;
      addLog('червь проснулся. отдохнул. <em>готов к огурцу.</em>', 'good');
      updateUI();
    }
  }, 4000);
}

// passive hunger decay
setInterval(() => {
  if (!worm.sleeping) {
    worm.hunger = Math.max(0, worm.hunger - 3);
    worm.happy  = Math.max(0, worm.happy  - 1);
    if (worm.hunger < 15) addLog('червь голоден. <em>это намёк.</em>', 'bad');
    updateUI();
  }
}, 8000);

updateUI();

// ═══════════════════════════
//  NAV
// ═══════════════════════════
function showPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  btn.classList.add('active');
}
</script>
</body>
</html>
