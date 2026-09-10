<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA — Mission Control</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@500;600;700&family=Inter:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --black: #060607;
    --panel: #0D0E10;
    --line: #232529;
    --white: #F5F5F3;
    --grey: #8A8D93;
    --accent: #E8542A;
  }
  *{ box-sizing:border-box; margin:0; padding:0; }
  html{ scroll-behavior: smooth; }
  body{
    background: var(--black);
    color: var(--white);
    font-family: 'Inter', sans-serif;
    font-weight: 300;
    -webkit-font-smoothing: antialiased;
  }
  a{ color: inherit; text-decoration: none; }
  .wrap{ max-width: 1180px; margin: 0 auto; padding: 0 32px; }

  /* NAV */
  nav{
    position: fixed; top:0; left:0; right:0; z-index: 20;
    border-bottom: 1px solid var(--line);
    background: rgba(6,6,7,0.75);
    backdrop-filter: blur(10px);
  }
  nav .wrap{ display:flex; align-items:center; justify-content: space-between; height: 68px; }
  .brand{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: 1.3rem;
    letter-spacing: 0.06em;
  }
  .brand span{ color: var(--accent); }
  .navlinks{ display:flex; gap: 34px; }
  .navlinks a{
    font-size: 0.82rem;
    color: var(--grey);
    letter-spacing: 0.03em;
    transition: color 0.2s ease;
  }
  .navlinks a:hover{ color: var(--white); }
  .nav-cta{
    border: 1px solid var(--white);
    padding: 9px 20px;
    font-size: 0.8rem;
    border-radius: 2px;
    transition: background 0.2s ease, color 0.2s ease;
  }
  .nav-cta:hover{ background: var(--white); color: var(--black); }

  /* HERO */
  .hero{
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 140px 0 80px;
    background:
      radial-gradient(ellipse at 50% 20%, rgba(232,84,42,0.10), transparent 55%),
      linear-gradient(180deg, #060607 0%, #0A0B0D 70%, #060607 100%);
    overflow: hidden;
    border-bottom: 1px solid var(--line);
  }
  .hero-stars{
    position: absolute; inset: 0;
    background-image:
      radial-gradient(1px 1px at 20% 30%, rgba(255,255,255,0.5) 50%, transparent),
      radial-gradient(1px 1px at 70% 60%, rgba(255,255,255,0.4) 50%, transparent),
      radial-gradient(1px 1px at 40% 80%, rgba(255,255,255,0.35) 50%, transparent),
      radial-gradient(1px 1px at 85% 15%, rgba(255,255,255,0.45) 50%, transparent),
      radial-gradient(1px 1px at 10% 65%, rgba(255,255,255,0.3) 50%, transparent),
      radial-gradient(1px 1px at 60% 25%, rgba(255,255,255,0.4) 50%, transparent),
      radial-gradient(1px 1px at 90% 75%, rgba(255,255,255,0.3) 50%, transparent);
    background-size: 100% 100%;
    opacity: 0.8;
  }
  .hero-content{ position: relative; z-index: 2; }
  .mission-tag{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent);
    letter-spacing: 0.04em;
    margin-bottom: 22px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards;
  }
  h1{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: clamp(3rem, 9vw, 7.5rem);
    line-height: 0.95;
    letter-spacing: -0.01em;
    text-transform: uppercase;
    max-width: 14ch;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.1s forwards;
  }
  .hero-desc{
    margin-top: 28px;
    max-width: 50ch;
    font-size: 1.1rem;
    color: var(--grey);
    opacity: 0;
    animation: fadeUp 0.8s ease 0.22s forwards;
  }
  .hero-actions{
    margin-top: 40px;
    display: flex; gap: 16px; flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.34s forwards;
  }
  .btn-primary{
    background: var(--accent);
    color: var(--black);
    padding: 14px 28px;
    font-size: 0.9rem;
    font-weight: 500;
    border-radius: 2px;
    transition: opacity 0.2s ease;
  }
  .btn-primary:hover{ opacity: 0.85; }
  .btn-secondary{
    border: 1px solid var(--line);
    color: var(--white);
    padding: 14px 28px;
    font-size: 0.9rem;
    border-radius: 2px;
    transition: border-color 0.2s ease;
  }
  .btn-secondary:hover{ border-color: var(--white); }

  @keyframes fadeUp{
    from{ opacity:0; transform: translateY(16px); }
    to{ opacity:1; transform: translateY(0); }
  }
  @media (prefers-reduced-motion: reduce){
    .mission-tag, h1, .hero-desc, .hero-actions{ animation:none; opacity:1; }
  }

  /* COUNTDOWN STRIP */
  .countdown-strip{
    border-bottom: 1px solid var(--line);
    background: var(--panel);
  }
  .countdown-strip .wrap{
    display: flex; align-items: center; justify-content: space-between;
    padding: 22px 32px; flex-wrap: wrap; gap: 20px;
  }
  .countdown-label{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: var(--grey);
  }
  .countdown-timer{
    display: flex; gap: 26px;
  }
  .timer-block{ text-align: center; }
  .timer-num{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: 1.9rem;
    line-height: 1;
  }
  .timer-unit{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    color: var(--grey);
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  /* SECTIONS */
  section{ padding: 100px 0; border-bottom: 1px solid var(--line); }
  .section-eyebrow{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: var(--accent);
    margin-bottom: 18px;
  }
  h2{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 600;
    font-size: clamp(2rem, 4vw, 3rem);
    text-transform: uppercase;
    max-width: 16ch;
  }

  /* STATS ROW */
  .stats-row{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 40px;
    margin-top: 56px;
  }
  .stat{ border-top: 1px solid var(--line); padding-top: 20px; }
  .stat-num{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: 2.6rem;
    color: var(--white);
  }
  .stat-label{
    font-size: 0.88rem;
    color: var(--grey);
    margin-top: 6px;
  }

  /* MISSIONS LIST */
  .missions{ margin-top: 56px; }
  .mission-row{
    display: grid;
    grid-template-columns: 100px 1fr auto auto;
    gap: 24px;
    align-items: center;
    padding: 22px 0;
    border-top: 1px solid var(--line);
    transition: background 0.2s ease;
  }
  .missions .mission-row:last-child{ border-bottom: 1px solid var(--line); }
  .mission-row:hover{ background: var(--panel); }
  .mission-index{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.8rem;
    color: var(--grey);
  }
  .mission-name{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 600;
    font-size: 1.3rem;
    text-transform: uppercase;
  }
  .mission-date{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.8rem;
    color: var(--grey);
  }
  .mission-status{
    font-size: 0.78rem;
    padding: 6px 14px;
    border-radius: 20px;
    border: 1px solid var(--line);
    color: var(--grey);
    white-space: nowrap;
  }
  .mission-status.go{ color: var(--accent); border-color: var(--accent); }

  /* GALLERY GRID */
  .gallery-grid{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin-top: 56px;
  }
  .gallery-grid div{
    aspect-ratio: 4/3;
    background: var(--panel);
    border: 1px solid var(--line);
    display: flex; align-items:center; justify-content:center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: var(--grey);
    overflow: hidden;
  }
  .gallery-grid img{ width:100%; height:100%; object-fit: cover; filter: grayscale(20%) contrast(1.05); }

  /* CTA */
  .cta-section{
    text-align: center;
    padding: 120px 0;
    border-bottom: none;
  }
  .cta-section h2{ margin: 0 auto 30px; }

  footer{ padding: 50px 0; }
  footer .wrap{
    display:flex; justify-content: space-between; flex-wrap: wrap; gap: 20px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: var(--grey);
  }

  @media (max-width: 700px){
    .mission-row{ grid-template-columns: 1fr; gap: 6px; }
    .gallery-grid{ grid-template-columns: repeat(2, 1fr); }
    .countdown-timer{ gap: 16px; }
    .timer-num{ font-size: 1.5rem; }
  }
</style>
</head>
<body>

<nav>
  <div class="wrap">
    <div class="brand">NOVA<span>.</span></div>
    <div class="navlinks">
      <a href="#missions">Missions</a>
      <a href="#programme">Programme</a>
      <a href="#galerie">Galerie</a>
    </div>
    <a class="nav-cta" href="nova-account.html">Rejoindre l'équipe</a>
  </div>
</nav>

<header class="hero">
  <div class="hero-stars"></div>
  <div class="wrap hero-content">
    <div class="mission-tag">PROCHAIN LANCEMENT — PAS DE TIR 1</div>
    <h1>Rendre la vie multiplanétaire</h1>
    <p class="hero-desc">
      Nous développons les fusées et vaisseaux les plus avancés au monde pour transporter des humains
      vers la Lune, Mars, et au-delà.
    </p>
    <div class="hero-actions">
      <a class="btn-primary" href="#missions">Voir les missions</a>
      <a class="btn-secondary" href="#programme">Le programme</a>
    </div>
  </div>
</header>

<div class="countdown-strip">
  <div class="wrap">
    <div class="countdown-label">MISSION AURORA-3 — DÉCOLLAGE DANS</div>
    <div class="countdown-timer" id="countdown">
      <div class="timer-block"><div class="timer-num" id="cd-days">--</div><div class="timer-unit">Jours</div></div>
      <div class="timer-block"><div class="timer-num" id="cd-hours">--</div><div class="timer-unit">Heures</div></div>
      <div class="timer-block"><div class="timer-num" id="cd-min">--</div><div class="timer-unit">Min</div></div>
      <div class="timer-block"><div class="timer-num" id="cd-sec">--</div><div class="timer-unit">Sec</div></div>
    </div>
  </div>
</div>

<section id="programme">
  <div class="wrap">
    <div class="section-eyebrow">Le programme</div>
    <h2>Construire la génération de fusées réutilisables</h2>
    <div class="stats-row">
      <div class="stat"><div class="stat-num">312</div><div class="stat-label">Lancements réussis</div></div>
      <div class="stat"><div class="stat-num">98%</div><div class="stat-label">Taux de récupération</div></div>
      <div class="stat"><div class="stat-num">14</div><div class="stat-label">Missions habitées</div></div>
      <div class="stat"><div class="stat-num">2031</div><div class="stat-label">Objectif Mars</div></div>
    </div>
  </div>
</section>

<section id="missions">
  <div class="wrap">
    <div class="section-eyebrow">Calendrier</div>
    <h2>Missions à venir</h2>
    <div class="missions">
      <div class="mission-row">
        <div class="mission-index">01</div>
        <div class="mission-name">Aurora-3 — Ravitaillement orbital</div>
        <div class="mission-date">14 OCT 2026</div>
        <div class="mission-status go">GO</div>
      </div>
      <div class="mission-row">
        <div class="mission-index">02</div>
        <div class="mission-name">Lunaris — Retour d'équipage</div>
        <div class="mission-date">02 NOV 2026</div>
        <div class="mission-status go">GO</div>
      </div>
      <div class="mission-row">
        <div class="mission-index">03</div>
        <div class="mission-name">Helios — Déploiement satellite</div>
        <div class="mission-date">19 NOV 2026</div>
        <div class="mission-status">EN PRÉPARATION</div>
      </div>
      <div class="mission-row">
        <div class="mission-index">04</div>
        <div class="mission-name">Terra Nova — Essai vaisseau</div>
        <div class="mission-date">05 DÉC 2026</div>
        <div class="mission-status">EN PRÉPARATION</div>
      </div>
    </div>
  </div>
</section>

<section id="galerie">
  <div class="wrap">
    <div class="section-eyebrow">Galerie</div>
    <h2>De l'usine au pas de tir</h2>
    <div class="gallery-grid">
      <div>Image 1</div>
      <div>Image 2</div>
      <div>Image 3</div>
      <div>Image 4</div>
      <div>Image 5</div>
      <div>Image 6</div>
    </div>
  </div>
</section>

<section class="cta-section" id="contact">
  <div class="wrap">
    <div class="section-eyebrow">Rejoins-nous</div>
    <h2>L'espace a besoin de bâtisseurs</h2>
    <a class="btn-primary" href="nova-account.html">Voir les postes ouverts</a>
  </div>
</section>

<footer>
  <div class="wrap">
    <span>© 2026 — NOVA Aerospace</span>
    <span>Pas de tir 1 · Base côtière</span>
  </div>
</footer>

<script>
  // Compte à rebours vers une date de lancement fictive (14 jours à partir de maintenant)
  const launchDate = new Date();
  launchDate.setDate(launchDate.getDate() + 14);

  function updateCountdown(){
    const now = new Date();
    let diff = launchDate - now;
    if(diff < 0) diff = 0;
    const days = Math.floor(diff / (1000*60*60*24));
    const hours = Math.floor((diff / (1000*60*60)) % 24);
    const mins = Math.floor((diff / (1000*60)) % 60);
    const secs = Math.floor((diff / 1000) % 60);
    document.getElementById('cd-days').textContent = String(days).padStart(2,'0');
    document.getElementById('cd-hours').textContent = String(hours).padStart(2,'0');
    document.getElementById('cd-min').textContent = String(mins).padStart(2,'0');
    document.getElementById('cd-sec').textContent = String(secs).padStart(2,'0');
  }
  updateCountdown();
  setInterval(updateCountdown, 1000);
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA — Accès</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@500;600;700&family=Inter:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --black: #060607;
    --panel: #0D0E10;
    --line: #232529;
    --white: #F5F5F3;
    --grey: #8A8D93;
    --accent: #E8542A;
    --error: #E85A5A;
  }
  *{ box-sizing:border-box; margin:0; padding:0; }
  body{
    background: var(--black);
    color: var(--white);
    font-family: 'Inter', sans-serif;
    font-weight: 300;
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    padding: 24px;
    position: relative;
    overflow: hidden;
  }
  a{ color: inherit; text-decoration: none; }

  .stars{
    position: absolute; inset: 0;
    background-image:
      radial-gradient(1px 1px at 20% 30%, rgba(255,255,255,0.5) 50%, transparent),
      radial-gradient(1px 1px at 70% 60%, rgba(255,255,255,0.4) 50%, transparent),
      radial-gradient(1px 1px at 40% 80%, rgba(255,255,255,0.35) 50%, transparent),
      radial-gradient(1px 1px at 85% 15%, rgba(255,255,255,0.45) 50%, transparent),
      radial-gradient(1px 1px at 10% 65%, rgba(255,255,255,0.3) 50%, transparent),
      radial-gradient(1px 1px at 60% 25%, rgba(255,255,255,0.4) 50%, transparent),
      radial-gradient(1px 1px at 90% 75%, rgba(255,255,255,0.3) 50%, transparent);
    opacity: 0.8;
  }

  .card{
    position: relative; z-index: 2;
    width: 100%; max-width: 420px;
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 4px;
    padding: 44px 38px;
  }
  .brand{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: 1.4rem;
    letter-spacing: 0.06em;
    text-align: center;
    margin-bottom: 6px;
  }
  .brand span{ color: var(--accent); }
  .subtitle{
    text-align: center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.72rem;
    color: var(--grey);
    letter-spacing: 0.04em;
    margin-bottom: 34px;
  }

  .tabs{
    display: flex;
    border: 1px solid var(--line);
    border-radius: 3px;
    margin-bottom: 30px;
    overflow: hidden;
  }
  .tab{
    flex: 1;
    text-align: center;
    padding: 12px;
    font-size: 0.85rem;
    color: var(--grey);
    cursor: pointer;
    transition: background 0.2s ease, color 0.2s ease;
  }
  .tab.active{ background: var(--accent); color: var(--black); font-weight: 500; }

  form{ display: none; flex-direction: column; gap: 18px; }
  form.active{ display: flex; }

  label{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.7rem;
    color: var(--grey);
    letter-spacing: 0.04em;
    text-transform: uppercase;
    margin-bottom: 8px;
    display: block;
  }
  input{
    width: 100%;
    background: var(--black);
    border: 1px solid var(--line);
    color: var(--white);
    padding: 12px 14px;
    font-family: 'Inter', sans-serif;
    font-size: 0.92rem;
    border-radius: 3px;
    outline: none;
    transition: border-color 0.2s ease;
  }
  input:focus{ border-color: var(--accent); }

  .submit-btn{
    background: var(--accent);
    color: var(--black);
    border: none;
    padding: 13px;
    font-family: 'Inter', sans-serif;
    font-size: 0.9rem;
    font-weight: 500;
    border-radius: 3px;
    cursor: pointer;
    transition: opacity 0.2s ease;
    margin-top: 6px;
  }
  .submit-btn:hover{ opacity: 0.88; }
  .submit-btn:disabled{ opacity: 0.5; cursor: not-allowed; }

  .msg{
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.76rem;
    padding: 10px 12px;
    border-radius: 3px;
    display: none;
  }
  .msg.show{ display: block; }
  .msg.error{ background: rgba(232,90,90,0.1); color: var(--error); border: 1px solid rgba(232,90,90,0.3); }
  .msg.success{ background: rgba(232,84,42,0.1); color: var(--accent); border: 1px solid rgba(232,84,42,0.3); }

  .welcome{ display:none; text-align: center; }
  .welcome.show{ display: block; }
  .welcome h2{
    font-family: 'Barlow Condensed', sans-serif;
    font-weight: 700;
    font-size: 1.8rem;
    text-transform: uppercase;
    margin-bottom: 10px;
  }
  .welcome p{ color: var(--grey); font-size: 0.9rem; margin-bottom: 24px; }
  .logout-btn{
    border: 1px solid var(--line);
    padding: 10px 22px;
    font-size: 0.82rem;
    border-radius: 3px;
    cursor: pointer;
    background: transparent;
    color: var(--white);
  }
  .logout-btn:hover{ border-color: var(--white); }

  .hint{
    text-align: center;
    font-size: 0.75rem;
    color: var(--grey);
    margin-top: 22px;
    line-height: 1.5;
  }
</style>
</head>
<body>

<div class="stars"></div>

<div class="card">
  <div id="authView">
    <div class="brand">NOVA<span>.</span></div>
    <div class="subtitle">ACCÈS MISSION CONTROL</div>

    <div class="tabs">
      <div class="tab active" data-tab="login">Se connecter</div>
      <div class="tab" data-tab="signup">Créer un compte</div>
    </div>

    <div class="msg" id="msgBox"></div>

    <form id="loginForm" class="active">
      <div>
        <label>Email</label>
        <input type="email" id="loginEmail" required>
      </div>
      <div>
        <label>Mot de passe</label>
        <input type="password" id="loginPassword" required>
      </div>
      <button type="submit" class="submit-btn">Se connecter</button>
    </form>

    <form id="signupForm">
      <div>
        <label>Nom</label>
        <input type="text" id="signupName" required>
      </div>
      <div>
        <label>Email</label>
        <input type="email" id="signupEmail" required>
      </div>
      <div>
        <label>Mot de passe</label>
        <input type="password" id="signupPassword" required minlength="6">
      </div>
      <button type="submit" class="submit-btn">Créer mon compte</button>
    </form>

    <div class="hint">Compte de démonstration — les identifiants sont stockés pour cet artifact, pas pour un vrai service sécurisé.</div>
  </div>

  <div class="welcome" id="welcomeView">
    <div class="brand" style="margin-bottom:24px;">NOVA<span>.</span></div>
    <h2 id="welcomeName">Bienvenue</h2>
    <p id="welcomeEmail"></p>
    <button class="logout-btn" id="logoutBtn">Se déconnecter</button>
  </div>
</div>

<script>
  const tabs = document.querySelectorAll('.tab');
  const forms = { login: document.getElementById('loginForm'), signup: document.getElementById('signupForm') };
  const msgBox = document.getElementById('msgBox');
  const authView = document.getElementById('authView');
  const welcomeView = document.getElementById('welcomeView');

  tabs.forEach(tab => {
    tab.addEventListener('click', () => {
      tabs.forEach(t => t.classList.remove('active'));
      tab.classList.add('active');
      Object.values(forms).forEach(f => f.classList.remove('active'));
      forms[tab.dataset.tab].classList.add('active');
      hideMsg();
    });
  });

  function showMsg(text, type){
    msgBox.textContent = text;
    msgBox.className = 'msg show ' + type;
  }
  function hideMsg(){
    msgBox.className = 'msg';
  }

  function showWelcome(name, email){
    authView.style.display = 'none';
    welcomeView.classList.add('show');
    document.getElementById('welcomeName').textContent = `Bon retour, ${name}`;
    document.getElementById('welcomeEmail').textContent = email;
  }

  document.getElementById('signupForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    hideMsg();
    const name = document.getElementById('signupName').value.trim();
    const email = document.getElementById('signupEmail').value.trim().toLowerCase();
    const password = document.getElementById('signupPassword').value;
    const btn = e.target.querySelector('.submit-btn');
    btn.disabled = true;

    try{
      let exists = null;
      try{ exists = await window.storage.get('account:' + email, false); } catch(err){ exists = null; }

      if(exists){
        showMsg('Un compte existe déjà avec cet email.', 'error');
        btn.disabled = false;
        return;
      }

      await window.storage.set('account:' + email, JSON.stringify({ name, email, password }), false);
      showMsg('Compte créé avec succès.', 'success');
      setTimeout(() => showWelcome(name, email), 500);
    }catch(err){
      showMsg('Erreur lors de la création du compte. Réessaie.', 'error');
    }
    btn.disabled = false;
  });

  document.getElementById('loginForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    hideMsg();
    const email = document.getElementById('loginEmail').value.trim().toLowerCase();
    const password = document.getElementById('loginPassword').value;
    const btn = e.target.querySelector('.submit-btn');
    btn.disabled = true;

    try{
      let result = null;
      try{ result = await window.storage.get('account:' + email, false); } catch(err){ result = null; }

      if(!result){
        showMsg('Aucun compte trouvé avec cet email.', 'error');
        btn.disabled = false;
        return;
      }
      const account = JSON.parse(result.value);
      if(account.password !== password){
        showMsg('Mot de passe incorrect.', 'error');
        btn.disabled = false;
        return;
      }
      showWelcome(account.name, account.email);
    }catch(err){
      showMsg('Erreur de connexion. Réessaie.', 'error');
    }
    btn.disabled = false;
  });

  document.getElementById('logoutBtn').addEventListener('click', () => {
    welcomeView.classList.remove('show');
    authView.style.display = 'block';
    document.getElementById('loginForm').reset();
    document.getElementById('signupForm').reset();
    hideMsg();
  });
</script>

</body>
</html>
