<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA — Espace membre</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@500;600;700&family=Inter:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">

<style>
:root{
  --black:#060607;
  --panel:#0D0E10;
  --panel2:#111216;
  --line:#232529;
  --white:#F5F5F3;
  --grey:#8A8D93;
  --accent:#E8542A;
  --success:#49C77A;
  --danger:#D94B4B;
}

*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}

html{
  scroll-behavior:smooth;
}

body{
  min-height:100vh;
  background:
    radial-gradient(
      ellipse at 50% 0%,
      rgba(232,84,42,.10),
      transparent 45%
    ),
    var(--black);
  color:var(--white);
  font-family:'Inter',sans-serif;
  font-weight:300;
  -webkit-font-smoothing:antialiased;
}

button,
input{
  font:inherit;
}

button{
  cursor:pointer;
}

a{
  color:inherit;
  text-decoration:none;
}

.wrap{
  width:min(1180px, calc(100% - 64px));
  margin:auto;
}

/* =========================
   NAVIGATION
========================= */

nav{
  position:fixed;
  top:0;
  left:0;
  right:0;
  z-index:50;

  height:68px;

  border-bottom:1px solid var(--line);

  background:rgba(6,6,7,.78);
  backdrop-filter:blur(14px);
}

nav .wrap{
  height:100%;
  display:flex;
  align-items:center;
  justify-content:space-between;
}

.brand{
  font-family:'Barlow Condensed',sans-serif;
  font-weight:700;
  font-size:1.35rem;
  letter-spacing:.07em;
}

.brand span{
  color:var(--accent);
}

.nav-right{
  display:flex;
  align-items:center;
  gap:25px;
}

.back-link{
  color:var(--grey);
  font-size:.8rem;
  transition:.2s;
}

.back-link:hover{
  color:var(--white);
}

/* =========================
   PAGE
========================= */

.page{
  min-height:100vh;
  padding:130px 0 70px;
}

.page-header{
  margin-bottom:40px;
}

.eyebrow{
  font-family:'IBM Plex Mono',monospace;
  font-size:.72rem;
  color:var(--accent);
  letter-spacing:.06em;
  margin-bottom:14px;
}

h1,
h2,
h3{
  font-family:'Barlow Condensed',sans-serif;
  text-transform:uppercase;
}

h1{
  font-size:clamp(3rem,7vw,6rem);
  line-height:.92;
}

.subtitle{
  max-width:600px;
  color:var(--grey);
  margin-top:18px;
  line-height:1.7;
}

/* =========================
   AUTH LAYOUT
========================= */

.auth-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:2px;
  max-width:900px;
  margin:auto;
}

.auth-panel{
  background:var(--panel);
  border:1px solid var(--line);
  padding:40px;
}

.auth-panel h2{
  font-size:2rem;
  margin-bottom:8px;
}

.panel-description{
  color:var(--grey);
  font-size:.88rem;
  line-height:1.6;
  margin-bottom:30px;
}

/* =========================
   FORM
========================= */

.form-group{
  margin-bottom:20px;
}

.form-group label{
  display:block;
  margin-bottom:8px;

  font-family:'IBM Plex Mono',monospace;
  color:var(--grey);
  font-size:.72rem;
  text-transform:uppercase;
}

.form-group input{
  width:100%;

  padding:14px 15px;

  color:var(--white);
  background:#08090A;

  border:1px solid var(--line);
  border-radius:2px;

  outline:none;

  transition:
    border-color .2s,
    box-shadow .2s;
}

.form-group input:focus{
  border-color:var(--accent);
  box-shadow:0 0 0 2px rgba(232,84,42,.08);
}

.form-group input::placeholder{
  color:#55585E;
}

.btn{
  width:100%;

  border:0;
  border-radius:2px;

  padding:14px 20px;

  font-size:.88rem;
  font-weight:500;

  transition:
    transform .2s,
    opacity .2s,
    background .2s;
}

.btn:hover{
  transform:translateY(-1px);
}

.btn-primary{
  color:var(--black);
  background:var(--accent);
}

.btn-primary:hover{
  opacity:.88;
}

.btn-secondary{
  color:var(--white);
  background:transparent;
  border:1px solid var(--line);
}

.btn-secondary:hover{
  border-color:var(--white);
}

.message{
  min-height:20px;
  margin-top:15px;

  font-size:.8rem;
  line-height:1.5;
}

.message.error{
  color:var(--danger);
}

.message.success{
  color:var(--success);
}

/* =========================
   STATUS
========================= */

.system-status{
  display:flex;
  align-items:center;
  gap:9px;

  margin-top:30px;

  font-family:'IBM Plex Mono',monospace;
  font-size:.68rem;
  color:var(--grey);
}

.status-dot{
  width:7px;
  height:7px;

  border-radius:50%;
  background:var(--success);

  box-shadow:0 0 10px rgba(73,199,122,.5);
}

/* =========================
   DASHBOARD
========================= */

.dashboard{
  display:none;
}

.dashboard.active{
  display:block;
}

.profile-grid{
  display:grid;
  grid-template-columns:1.2fr .8fr;
  gap:20px;
}

.card{
  background:var(--panel);
  border:1px solid var(--line);
  padding:32px;
}

.card-header{
  display:flex;
  align-items:flex-start;
  justify-content:space-between;
  gap:20px;

  margin-bottom:28px;
}

.card h2{
  font-size:2rem;
}

.member-badge{
  color:var(--accent);
  border:1px solid var(--accent);
  padding:6px 10px;

  font-family:'IBM Plex Mono',monospace;
  font-size:.65rem;
  white-space:nowrap;
}

.profile-name{
  font-family:'Barlow Condensed',sans-serif;
  font-size:3rem;
  text-transform:uppercase;
}

.profile-email{
  color:var(--grey);
  margin-top:5px;
}

.data-list{
  margin-top:28px;
}

.data-row{
  display:flex;
  justify-content:space-between;
  gap:20px;

  padding:15px 0;
  border-top:1px solid var(--line);

  font-size:.84rem;
}

.data-row span:first-child{
  color:var(--grey);
}

.data-row span:last-child{
  text-align:right;
}

/* =========================
   MISSIONS
========================= */

.mission-card{
  margin-top:20px;
}

.mission-item{
  display:flex;
  align-items:center;
  gap:18px;

  padding:18px 0;
  border-top:1px solid var(--line);
}

.mission-number{
  color:var(--grey);

  font-family:'IBM Plex Mono',monospace;
  font-size:.7rem;
}

.mission-info{
  flex:1;
}

.mission-title{
  font-family:'Barlow Condensed',sans-serif;
  font-size:1.2rem;
  text-transform:uppercase;
}

.mission-date{
  margin-top:3px;

  font-family:'IBM Plex Mono',monospace;
  font-size:.65rem;
  color:var(--grey);
}

.status{
  padding:5px 10px;
  border:1px solid var(--line);
  border-radius:20px;

  color:var(--grey);

  font-size:.65rem;
}

.status.go{
  color:var(--accent);
  border-color:var(--accent);
}

/* =========================
   LOGOUT
========================= */

.logout{
  margin-top:25px;
  color:#999;
  background:none;
  border:0;

  font-family:'IBM Plex Mono',monospace;
  font-size:.7rem;

  transition:.2s;
}

.logout:hover{
  color:var(--danger);
}

/* =========================
   FOOTER
========================= */

footer{
  padding:30px 0;

  border-top:1px solid var(--line);

  color:var(--grey);

  font-family:'IBM Plex Mono',monospace;
  font-size:.65rem;
}

footer .wrap{
  display:flex;
  justify-content:space-between;
  gap:20px;
}

/* =========================
   MOBILE
========================= */

@media(max-width:760px){

  .wrap{
    width:min(100% - 36px,1180px);
  }

  nav{
    height:60px;
  }

  .back-link{
    display:none;
  }

  .page{
    padding-top:105px;
  }

  .auth-grid{
    grid-template-columns:1fr;
  }

  .auth-panel{
    padding:28px 22px;
  }

  .profile-grid{
    grid-template-columns:1fr;
  }

  .card{
    padding:25px 20px;
  }

  .profile-name{
    font-size:2.4rem;
  }

  .mission-item{
    align-items:flex-start;
  }

  .mission-item .status{
    display:none;
  }

  footer .wrap{
    flex-direction:column;
  }
}
</style>
</head>

<body>

<nav>
  <div class="wrap">

    <a href="index.html" class="brand">
      NOVA<span>.</span>
    </a>

    <div class="nav-right">
      <a href="index.html" class="back-link">
        ← Retour à Mission Control
      </a>
    </div>

  </div>
</nav>

<main class="page">

  <div class="wrap">

    <!-- ======================
         AUTHENTIFICATION
    ======================= -->

    <div id="authView">

      <div class="page-header">
        <div class="eyebrow">ACCÈS MEMBRE / NOVA-01</div>

        <h1>
          Centre de contrôle
        </h1>

        <p class="subtitle">
          Connectez-vous à votre espace NOVA pour suivre les missions,
          votre profil et les prochaines opérations.
        </p>
      </div>

      <div class="auth-grid">

        <!-- CONNEXION -->

        <section class="auth-panel">

          <h2>Connexion</h2>

          <p class="panel-description">
            Accédez à votre compte membre NOVA.
          </p>

          <form id="loginForm">

            <div class="form-group">
              <label for="loginEmail">
                Adresse e-mail
              </label>

              <input
                id="loginEmail"
                type="email"
                placeholder="vous@exemple.fr"
                autocomplete="email"
                required
              >
            </div>

            <div class="form-group">
              <label for="loginPassword">
                Mot de passe
              </label>

              <input
                id="loginPassword"
                type="password"
                placeholder="••••••••"
                autocomplete="current-password"
                required
              >
            </div>

            <button class="btn btn-primary" type="submit">
              Se connecter
            </button>

            <div id="loginMessage" class="message"></div>

          </form>

        </section>


        <!-- INSCRIPTION -->

        <section class="auth-panel">

          <h2>Rejoindre NOVA</h2>

          <p class="panel-description">
            Créez votre identité de membre et rejoignez
            la prochaine génération de bâtisseurs.
          </p>

          <form id="registerForm">

            <div class="form-group">
              <label for="registerName">
                Nom complet
              </label>

              <input
                id="registerName"
                type="text"
                placeholder="Jean Dupont"
                autocomplete="name"
                required
              >
            </div>

            <div class="form-group">
              <label for="registerEmail">
                Adresse e-mail
              </label>

              <input
                id="registerEmail"
                type="email"
                placeholder="vous@exemple.fr"
                autocomplete="email"
                required
              >
            </div>

            <div class="form-group">
              <label for="registerPassword">
                Mot de passe
              </label>

              <input
                id="registerPassword"
                type="password"
                placeholder="Minimum 6 caractères"
                minlength="6"
                autocomplete="new-password"
                required
              >
            </div>

            <button class="btn btn-secondary" type="submit">
              Créer mon compte
            </button>

            <div id="registerMessage" class="message"></div>

          </form>

        </section>

      </div>

      <div class="system-status">
        <span class="status-dot"></span>
        SYSTÈME NOVA OPÉRATIONNEL
      </div>

    </div>


    <!-- ======================
         DASHBOARD
    ======================= -->

    <div id="dashboard" class="dashboard">

      <div class="page-header">

        <div class="eyebrow">
          IDENTITÉ CONFIRMÉE / ACCÈS AUTORISÉ
        </div>

        <h1>
          Bienvenue à bord.
        </h1>

        <p class="subtitle">
          Votre accès au réseau NOVA est actif.
          Voici votre centre de contrôle personnel.
        </p>

      </div>


      <div class="profile-grid">

        <!-- PROFIL -->

        <section class="card">

          <div class="card-header">

            <div>
              <div class="eyebrow">
                PROFIL MEMBRE
              </div>

              <h2>
                Identité
              </h2>
            </div>

            <div class="member-badge">
              NOVA MEMBER
            </div>

          </div>

          <div id="profileName" class="profile-name">
            —
          </div>

          <div id="profileEmail" class="profile-email">
            —
          </div>

          <div class="data-list">

            <div class="data-row">
              <span>Statut</span>
              <span style="color:var(--success)">
                ACTIF
              </span>
            </div>

            <div class="data-row">
              <span>Accréditation</span>
              <span>NOVA-01</span>
            </div>

            <div class="data-row">
              <span>Base</span>
              <span>Pas de tir 1</span>
            </div>

            <div class="data-row">
              <span>Inscription</span>
              <span id="profileDate">—</span>
            </div>

          </div>

          <button id="logoutButton" class="logout">
            DÉCONNEXION →
          </button>

        </section>


        <!-- PROCHAINE MISSION -->

        <section class="card">

          <div class="card-header">

            <div>
              <div class="eyebrow">
                PROCHAINE OPÉRATION
              </div>

              <h2>
                Aurora-3
              </h2>
            </div>

            <div class="member-badge">
              GO
            </div>

          </div>

          <p class="panel-description">
            Mission de ravitaillement orbital.
            Préparation finale avant fenêtre de lancement.
          </p>

          <div class="data-list">

            <div class="data-row">
              <span>Date</span>
              <span>14 OCT 2026</span>
            </div>

            <div class="data-row">
              <span>Mission</span>
              <span>AURORA-3</span>
            </div>

            <div class="data-row">
              <span>Type</span>
              <span>Ravitaillement</span>
            </div>

            <div class="data-row">
              <span>Statut</span>
              <span style="color:var(--accent)">
                GO
              </span>
            </div>

          </div>

        </section>

      </div>


      <!-- MISSIONS -->

      <section class="card mission-card">

        <div class="card-header">

          <div>
            <div class="eyebrow">
              MANIFEST
            </div>

            <h2>
              Missions suivies
            </h2>
          </div>

        </div>

        <div class="mission-item">

          <div class="mission-number">
            01
          </div>

          <div class="mission-info">

            <div class="mission-title">
              Aurora-3 — Ravitaillement orbital
            </div>

            <div class="mission-date">
              14 OCT 2026
            </div>

          </div>

          <div class="status go">
            GO
          </div>

        </div>

        <div class="mission-item">

          <div class="mission-number">
            02
          </div>

          <div class="mission-info">

            <div class="mission-title">
              Lunaris — Retour d'équipage
            </div>

            <div class="mission-date">
              02 NOV 2026
            </div>

          </div>

          <div class="status go">
            GO
          </div>

        </div>

        <div class="mission-item">

          <div class="mission-number">
            03
          </div>

          <div class="mission-info">

            <div class="mission-title">
              Helios — Déploiement satellite
            </div>

            <div class="mission-date">
              19 NOV 2026
            </div>

          </div>

          <div class="status">
            PRÉPARATION
          </div>

        </div>

        <div class="mission-item">

          <div class="mission-number">
            04
          </div>

          <div class="mission-info">

            <div class="mission-title">
              Terra Nova — Essai vaisseau
            </div>

            <div class="mission-date">
              05 DÉC 2026
            </div>

          </div>

          <div class="status">
            PRÉPARATION
          </div>

        </div>

      </section>

    </div>

  </div>

</main>


<footer>

  <div class="wrap">

    <span>
      © 2026 — NOVA Aerospace
    </span>

    <span>
      SYSTÈME MEMBRE / NOVA-01
    </span>

  </div>

</footer>


<script>

/* ==========================================
   UTILITAIRES
========================================== */

function getUsers(){

  try{

    return JSON.parse(
      localStorage.getItem('nova_users') || '[]'
    );

  }catch(error){

    return [];

  }

}


function saveUsers(users){

  localStorage.setItem(
    'nova_users',
    JSON.stringify(users)
  );

}


function setMessage(element, text, type){

  element.textContent = text;
  element.className = 'message ' + type;

}


/* ==========================================
   VUES
========================================== */

const authView =
  document.getElementById('authView');

const dashboard =
  document.getElementById('dashboard');


function showDashboard(user){

  authView.style.display = 'none';

  dashboard.classList.add('active');

  document.getElementById(
    'profileName'
  ).textContent = user.name;

  document.getElementById(
    'profileEmail'
  ).textContent = user.email;

  document.getElementById(
    'profileDate'
  ).textContent = user.createdAt || '—';

}


function showAuth(){

  dashboard.classList.remove('active');

  authView.style.display = 'block';

}


/* ==========================================
   INSCRIPTION
========================================== */

document
  .getElementById('registerForm')
  .addEventListener('submit', function(event){

    event.preventDefault();

    const name =
      document
        .getElementById('registerName')
        .value
        .trim();

    const email =
      document
        .getElementById('registerEmail')
        .value
        .trim()
        .toLowerCase();

    const password =
      document
        .getElementById('registerPassword')
        .value;

    const message =
      document.getElementById(
        'registerMessage'
      );

    if(name.length < 2){

      setMessage(
        message,
        'Veuillez entrer un nom valide.',
        'error'
      );

      return;

    }

    if(password.length < 6){

      setMessage(
        message,
        'Le mot de passe doit contenir au moins 6 caractères.',
        'error'
      );

      return;

    }

    const users = getUsers();

    const existingUser =
      users.find(
        user => user.email === email
      );

    if(existingUser){

      setMessage(
        message,
        'Un compte existe déjà avec cette adresse.',
        'error'
      );

      return;

    }

    const user = {

      id:
        'NOVA-' +
        Date.now(),

      name:name,

      email:email,

      password:password,

      createdAt:
        new Date().toLocaleDateString(
          'fr-FR',
          {
            day:'2-digit',
            month:'2-digit',
            year:'numeric'
          }
        )

    };

    users.push(user);

    saveUsers(users);

    localStorage.setItem(
      'nova_current_user',
      JSON.stringify(user)
    );

    showDashboard(user);

  });


/* ==========================================
   CONNEXION
========================================== */

document
  .getElementById('loginForm')
  .addEventListener('submit', function(event){

    event.preventDefault();

    const email =
      document
        .getElementById('loginEmail')
        .value
        .trim()
        .toLowerCase();

    const password =
      document
        .getElementById('loginPassword')
        .value;

    const message =
      document.getElementById(
        'loginMessage'
      );

    const users = getUsers();

    const user =
      users.find(
        user =>
          user.email === email &&
          user.password === password
      );

    if(!user){

      setMessage(
        message,
        'Adresse e-mail ou mot de passe incorrect.',
        'error'
      );

      return;

    }

    localStorage.setItem(
      'nova_current_user',
      JSON.stringify(user)
    );

    showDashboard(user);

  });


/* ==========================================
   DÉCONNEXION
========================================== */

document
  .getElementById('logoutButton')
  .addEventListener('click', function(){

    localStorage.removeItem(
      'nova_current_user'
    );

    showAuth();

    document
      .getElementById('loginForm')
      .reset();

    window.scrollTo({
      top:0,
      behavior:'smooth'
    });

  });


/* ==========================================
   RESTAURATION SESSION
========================================== */

(function restoreSession(){

  const currentUser =
    localStorage.getItem(
      'nova_current_user'
    );

  if(!currentUser){

    showAuth();

    return;

  }

  try{

    const user =
      JSON.parse(currentUser);

    if(user && user.email){

      showDashboard(user);

    }else{

      showAuth();

    }

  }catch(error){

    localStorage.removeItem(
      'nova_current_user'
    );

    showAuth();

  }

})();

</script>

</body>
</html>
