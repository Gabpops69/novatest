<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA — Mission Control</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@500;600;700&family=Inter:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --black:#050608;
  --panel:#0b0e12;
  --panel-2:#10141a;
  --line:rgba(255,255,255,.10);
  --line-strong:rgba(255,255,255,.18);
  --white:#f5f7fa;
  --grey:#8f98a6;
  --accent:#ff6a3d;
  --accent-soft:rgba(255,106,61,.12);
  --max:1240px;
  --radius:14px;
  --shadow:0 24px 80px rgba(0,0,0,.35);
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  background:
    radial-gradient(circle at 80% -10%,rgba(255,106,61,.10),transparent 28rem),
    var(--black);
  color:var(--white);
  font-family:'Inter',sans-serif;
  font-weight:400;
  line-height:1.6;
  -webkit-font-smoothing:antialiased;
}
body:before{
  content:"";
  position:fixed;inset:0;pointer-events:none;z-index:99;opacity:.045;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.7'/%3E%3C/svg%3E");
}
a{color:inherit;text-decoration:none}
.wrap{width:min(var(--max),calc(100% - 48px));margin:0 auto}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:20;
  border-bottom:1px solid var(--line);
  background:rgba(5,6,8,.72);
  backdrop-filter:blur(18px);
}
nav .wrap{height:76px;display:flex;align-items:center;justify-content:space-between;gap:28px}
.brand{font-family:'Barlow Condensed',sans-serif;font-weight:700;font-size:1.45rem;letter-spacing:.08em}
.brand span{color:var(--accent)}
.navlinks{display:flex;gap:34px;margin-left:auto}
.navlinks a{font-size:.82rem;color:var(--grey);transition:.2s}
.navlinks a:hover{color:var(--white)}
.nav-cta,.btn-primary,.btn-secondary{
  display:inline-flex;align-items:center;justify-content:center;
  border-radius:7px;font-size:.84rem;font-weight:600;
  transition:transform .2s,background .2s,border-color .2s,color .2s,box-shadow .2s;
}
.nav-cta{border:1px solid var(--line-strong);padding:10px 17px}
.nav-cta:hover{background:var(--white);color:var(--black);transform:translateY(-1px)}
.menu-toggle{display:none;border:0;background:none;color:var(--white);font-size:1.4rem;cursor:pointer}

/* HERO */
.hero{
  position:relative;min-height:100vh;display:flex;align-items:flex-end;
  padding:150px 0 92px;overflow:hidden;border-bottom:1px solid var(--line);
  background:
    radial-gradient(ellipse at 55% 30%,rgba(255,106,61,.15),transparent 44%),
    linear-gradient(180deg,#050608 0%,#090c10 65%,#050608 100%);
}
.hero:after{
  content:"";position:absolute;width:680px;height:680px;right:-220px;top:90px;
  border:1px solid rgba(255,255,255,.06);border-radius:50%;
  box-shadow:0 0 0 70px rgba(255,255,255,.012),0 0 0 140px rgba(255,255,255,.008);
}
.hero-stars{
  position:absolute;inset:0;opacity:.65;
  background-image:
    radial-gradient(1px 1px at 20% 30%,rgba(255,255,255,.6) 50%,transparent),
    radial-gradient(1px 1px at 70% 60%,rgba(255,255,255,.45) 50%,transparent),
    radial-gradient(1px 1px at 40% 80%,rgba(255,255,255,.35) 50%,transparent),
    radial-gradient(1px 1px at 85% 15%,rgba(255,255,255,.5) 50%,transparent),
    radial-gradient(1px 1px at 10% 65%,rgba(255,255,255,.3) 50%,transparent),
    radial-gradient(1px 1px at 60% 25%,rgba(255,255,255,.4) 50%,transparent),
    radial-gradient(1px 1px at 90% 75%,rgba(255,255,255,.3) 50%,transparent);
}
.hero-content{position:relative;z-index:2}
.mission-tag,.section-eyebrow{
  font-family:'IBM Plex Mono',monospace;font-size:.72rem;letter-spacing:.08em;
  color:var(--accent);text-transform:uppercase;
}
.mission-tag{margin-bottom:24px}
h1,h2,.mission-name,.stat-num,.timer-num{
  font-family:'Barlow Condensed',sans-serif;text-transform:uppercase;
}
h1{
  font-weight:700;font-size:clamp(4rem,9vw,8.6rem);line-height:.88;
  letter-spacing:-.025em;max-width:12ch;
}
.hero-desc{margin-top:30px;max-width:57ch;font-size:1.08rem;color:var(--grey)}
.hero-actions{display:flex;gap:12px;flex-wrap:wrap;margin-top:42px}
.btn-primary{background:var(--accent);color:#160a06;padding:14px 24px;box-shadow:0 10px 35px rgba(255,106,61,.18)}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 14px 42px rgba(255,106,61,.28)}
.btn-secondary{border:1px solid var(--line-strong);padding:14px 24px;background:rgba(255,255,255,.02)}
.btn-secondary:hover{border-color:var(--white);background:rgba(255,255,255,.06);transform:translateY(-2px)}

/* COUNTDOWN */
.countdown-strip{border-bottom:1px solid var(--line);background:rgba(11,14,18,.92)}
.countdown-strip .wrap{display:flex;align-items:center;justify-content:space-between;padding:22px 0;gap:25px}
.countdown-label{font-family:'IBM Plex Mono',monospace;font-size:.72rem;color:var(--grey);letter-spacing:.06em}
.countdown-timer{display:flex;gap:34px}
.timer-block{text-align:right;min-width:52px}
.timer-num{font-weight:700;font-size:2rem;line-height:1}
.timer-unit{font-family:'IBM Plex Mono',monospace;font-size:.6rem;color:var(--grey);letter-spacing:.06em;text-transform:uppercase;margin-top:5px}

/* SECTIONS */
section{padding:112px 0;border-bottom:1px solid var(--line)}
.section-eyebrow{margin-bottom:15px}
h2{font-weight:600;font-size:clamp(2.5rem,5vw,4.3rem);line-height:.95;letter-spacing:-.01em;max-width:14ch}

/* STATS */
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-top:64px}
.stat{
  padding:26px 24px 28px;border:1px solid var(--line);border-radius:var(--radius);
  background:linear-gradient(145deg,rgba(255,255,255,.035),rgba(255,255,255,.01));
  transition:transform .25s,border-color .25s,background .25s;
}
.stat:hover{transform:translateY(-4px);border-color:var(--line-strong);background:var(--panel-2)}
.stat-num{font-weight:700;font-size:3.25rem;line-height:1}
.stat-label{font-size:.82rem;color:var(--grey);margin-top:10px}

/* MISSIONS */
.missions{margin-top:62px;border:1px solid var(--line);border-radius:var(--radius);overflow:hidden}
.mission-row{
  display:grid;grid-template-columns:72px 1fr auto auto;gap:24px;align-items:center;
  padding:24px 26px;border-bottom:1px solid var(--line);transition:background .2s,transform .2s;
}
.mission-row:last-child{border-bottom:0}
.mission-row:hover{background:rgba(255,255,255,.025)}
.mission-index{font-family:'IBM Plex Mono',monospace;font-size:.75rem;color:var(--grey)}
.mission-name{font-weight:600;font-size:1.3rem}
.mission-date{font-family:'IBM Plex Mono',monospace;font-size:.72rem;color:var(--grey);white-space:nowrap}
.mission-status{font-size:.68rem;padding:5px 10px;border-radius:999px;border:1px solid var(--line-strong);color:var(--grey);white-space:nowrap}
.mission-status.go{color:var(--accent);border-color:rgba(255,106,61,.5);background:var(--accent-soft)}

/* GALLERY */
.gallery-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-top:62px}
.gallery-grid div{
  position:relative;aspect-ratio:4/3;border:1px solid var(--line);border-radius:12px;
  overflow:hidden;background:
    linear-gradient(135deg,rgba(255,106,61,.12),transparent 48%),
    radial-gradient(circle at 70% 30%,rgba(255,255,255,.08),transparent 35%),var(--panel);
}
.gallery-grid div:before{
  content:"";position:absolute;inset:12px;border:1px solid rgba(255,255,255,.08);
  border-radius:8px;
}
.gallery-grid div:after{
  content:"";position:absolute;left:12%;right:12%;bottom:18%;height:1px;
  background:linear-gradient(90deg,transparent,rgba(255,255,255,.35),transparent);
}
.gallery-grid div{
  display:flex;align-items:center;justify-content:center;
  font-family:'IBM Plex Mono',monospace;font-size:.7rem;color:var(--grey);
}

/* CTA */
.cta-section{text-align:center;padding:140px 0;border-bottom:0}
.cta-section h2{margin:0 auto 34px}
.cta-section .btn-primary{margin:auto}

/* FOOTER */
footer{padding:34px 0}
footer .wrap{display:flex;justify-content:space-between;flex-wrap:wrap;gap:20px;font-family:'IBM Plex Mono',monospace;font-size:.68rem;color:var(--grey)}

/* REVEAL */
.reveal{opacity:0;transform:translateY(22px);transition:opacity .7s ease,transform .7s ease}
.reveal.visible{opacity:1;transform:none}

/* MOBILE */
@media(max-width:800px){
  .wrap{width:min(var(--max),calc(100% - 32px))}
  nav .wrap{height:68px}
  .navlinks{display:none;position:absolute;top:68px;left:0;right:0;padding:18px 16px;background:rgba(5,6,8,.97);border-bottom:1px solid var(--line);flex-direction:column;gap:0}
  .navlinks.open{display:flex}
  .navlinks a{padding:13px 8px}
  .nav-cta{display:none}
  .menu-toggle{display:block}
  .hero{padding:130px 0 70px;min-height:88vh}
  h1{font-size:clamp(3.8rem,18vw,6.5rem)}
  .countdown-strip .wrap{align-items:flex-start;flex-direction:column}
  .countdown-timer{width:100%;justify-content:space-between;gap:12px}
  .timer-block{text-align:left}
  section{padding:82px 0}
  .stats-row{grid-template-columns:repeat(2,1fr);margin-top:42px}
  .mission-row{grid-template-columns:42px 1fr;gap:8px 16px;padding:20px}
  .mission-date{grid-column:2}
  .mission-status{grid-column:2;width:max-content}
  .gallery-grid{grid-template-columns:repeat(2,1fr);gap:10px;margin-top:42px}
}
@media(max-width:480px){
  .stats-row{grid-template-columns:1fr}
  .gallery-grid{grid-template-columns:1fr}
  .hero-actions{flex-direction:column;align-items:stretch}
  .btn-primary,.btn-secondary{width:100%}
  .countdown-timer{gap:7px}
  .timer-num{font-size:1.55rem}
  .mission-name{font-size:1.15rem}
}
@media(prefers-reduced-motion:reduce){
  html{scroll-behavior:auto}
  .reveal{opacity:1;transform:none;transition:none}
  *,*:before,*:after{animation:none!important;transition:none!important}
}
.gallery-grid div {
  position: relative;
  aspect-ratio: 4/3;
  border: 1px solid var(--line);
  border-radius: 12px;
  overflow: hidden;
  background: var(--panel);
  perspective: 800px;
}

.gallery-grid img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
  transform: scale(1) rotateX(0deg) rotateY(0deg);
  transition: transform 0.15s ease-out;
  transform-origin: center center;
  cursor: zoom-in;
}
.gallery-grid div {
  overflow: hidden;
}

.gallery-grid img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transform: scale(1);
  transition: transform 0.1s ease;
}

</style>
</head>
<script>
document.querySelectorAll('.gallery-grid img').forEach(img => {

  let zoom = 1;
  let rotateX = 0;
  let rotateY = 0;

  img.addEventListener('wheel', function(event) {
    event.preventDefault();

    // Molette vers le haut : zoom
    if (event.deltaY < 0) {
      zoom += 0.15;
    } else {
      zoom -= 0.15;
    }

    // Limites
    zoom = Math.max(1, Math.min(3, zoom));

    img.style.transform =
      `scale(${zoom}) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  }, { passive: false });

  // Petit effet 3D avec le déplacement de la souris
  img.addEventListener('mousemove', function(event) {

    const rect = img.getBoundingClientRect();

    const x = (event.clientX - rect.left) / rect.width;
    const y = (event.clientY - rect.top) / rect.height;

    rotateY = (x - 0.5) * 10;
    rotateX = -(y - 0.5) * 10;

    img.style.transform =
      `scale(${zoom}) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
  });

  // Retour à plat quand la souris sort
  img.addEventListener('mouseleave', function() {
    rotateX = 0;
    rotateY = 0;

    img.style.transform =
      `scale(${zoom}) rotateX(0deg) rotateY(0deg)`;
  });

});
</script>
 
<script>
document.querySelectorAll('.gallery-grid img').forEach(img => {
  let zoom = 1;

  img.addEventListener('wheel', function(event) {
    event.preventDefault();

    // Molette vers le haut = zoom
    if (event.deltaY < 0) {
      zoom += 0.1;
    } 
    // Molette vers le bas = dézoom
    else {
      zoom -= 0.1;
    }

    // Limites du zoom
    zoom = Math.max(1, Math.min(2.5, zoom));

    img.style.transform = `scale(${zoom})`;
  }, { passive: false });
});
</script>
<body>

<nav>
  <div class="wrap">
    <div class="brand">NOVA<span>.</span></div>
    <button class="menu-toggle" id="menuToggle" aria-label="Ouvrir le menu">☰</button>
    <div class="navlinks" id="navLinks">
      <a href="#missions">Missions</a>
      <a href="#programme">Programme</a>
      <a href="#galerie">Galerie</a>
    </div>
    <a aria-label="Rejoindre l’équipe NOVA" class="nav-cta" href="nova-team.html" id="navCta">Rejoindre l'équipe</a>
  </div>
</nav>

<header class="hero">
  <div class="hero-stars" aria-hidden="true"></div>
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

<section id="programme" class="reveal">
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

<section id="missions" class="reveal">
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

<section id="galerie" class="reveal">
  <div class="wrap">
    <div class="section-eyebrow">Galerie</div>
    <h2>De l'usine au pas de tir</h2>
    <div class="gallery-grid">
      <div><img src="eso1509b.jpg" alt="Image 1"></div>
  <div><img src="images/image2.jpg" alt="Image 2"></div>
  <div><img src="images/image3.jpg" alt="Image 3"></div>
  <div><img src="images/image4.jpg" alt="Image 4"></div>
  <div><img src="images/image5.jpg" alt="Image 5"></div>
  <div><img src="images/image6.jpg" alt="Image 6"></div>
    </div>
  </div>
</section>

<section class="cta-section reveal" id="contact">
  <div class="wrap">
    <div class="section-eyebrow">Rejoins-nous</div>
    <h2>L'espace a besoin de bâtisseurs</h2>
    <a class="btn-primary" href="nova-team.html">Voir les postes ouverts</a>
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

  // Menu mobile
  const menuToggle = document.getElementById('menuToggle');
  const navLinks = document.getElementById('navLinks');
  menuToggle?.addEventListener('click', () => {
    const open = navLinks.classList.toggle('open');
    menuToggle.setAttribute('aria-expanded', String(open));
  });
  navLinks?.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => navLinks.classList.remove('open'));
  });

  // Apparition progressive des sections
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if(entry.isIntersecting){
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, {threshold: .12});
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Affiche l'état connecté si un compte NOVA est actif dans ce navigateur
  const currentUser = localStorage.getItem('nova_current_user');
  if(currentUser){
    try{
      const user = JSON.parse(currentUser);
      const navCta = document.getElementById('navCta');
      navCta.textContent = `Bonjour, ${user.name} · Déconnexion`;
      navCta.href = '#';
      navCta.addEventListener('click', (e) => {
        e.preventDefault();
        localStorage.removeItem('nova_current_user');
        window.location.reload();
      });
    }catch(err){}
  }
</script>

</body>
</html>
