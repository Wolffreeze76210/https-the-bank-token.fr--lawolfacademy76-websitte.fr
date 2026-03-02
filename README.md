<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>THE BANK TOKEN - LA WOLF ACADEMY 76</title>
    <style>
        :root { --gold: #D4AF37; --dark: #0a0a0a; --glass: rgba(255, 255, 255, 0.15); }
        body { background: var(--dark) url('fond_cosmique.png') no-repeat center center fixed; background-size: cover; color: white; font-family: 'Segoe UI', sans-serif; margin: 0; padding: 0; overflow: hidden; }
        .overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.75); z-index: -1; }
        
        .site-page { display: none; min-height: 100vh; width: 100%; flex-direction: column; align-items: center; justify-content: center; padding: 20px; box-sizing: border-box; }
        .active-page { display: flex; }
        
        .card { background: var(--glass); backdrop-filter: blur(15px); border: 1px solid rgba(212, 175, 55, 0.4); border-radius: 20px; padding: 25px; width: 100%; max-width: 380px; text-align: center; box-shadow: 0 10px 30px rgba(0,0,0,0.8); }
        h1, h2 { color: var(--gold); text-transform: uppercase; letter-spacing: 2px; margin-bottom: 20px; }
        
        input { width: 100%; padding: 12px; margin: 8px 0; border-radius: 10px; border: 1px solid var(--gold); background: rgba(0,0,0,0.6); color: white; text-align: center; font-size: 1rem; }
        button { width: 100%; padding: 14px; border-radius: 30px; border: none; background: linear-gradient(90deg, #D4AF37, #B8860B); color: black; font-weight: bold; cursor: pointer; margin-top: 10px; transition: 0.3s; }
        button:active { transform: scale(0.95); }
        
        .nav-bar { position: fixed; top: 0; width: 100%; background: rgba(0,0,0,0.9); display: none; overflow-x: auto; padding: 10px; gap: 10px; border-bottom: 1px solid var(--gold); z-index: 100; }
        .nav-btn { background: var(--glass); border: 1px solid var(--gold); color: var(--gold); padding: 8px 15px; border-radius: 20px; font-size: 0.8rem; white-space: nowrap; cursor: pointer; }
        .logout-btn { background: #900; color: white; border: 1px solid red; }

        .url-bar { position: fixed; bottom: 0; width: 100%; background: rgba(0,0,0,0.8); color: #888; font-size: 0.6rem; padding: 5px; text-align: center; border-top: 1px solid #333; }
        
        .digicode { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin: 15px 0; }
        .key { background: rgba(255,255,255,0.1); border: 1px solid var(--gold); padding: 15px; border-radius: 10px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>
    <div class="overlay"></div>

    <nav class="nav-bar" id="menu">
        <div class="nav-btn" onclick="showComp('home')">🏠 Accueil</div>
        <div class="nav-btn" onclick="showComp('bank')">🏦 Banque</div>
        <div class="nav-btn" onclick="showComp('admin')">🔒 Admin</div>
        <div class="nav-btn logout-btn" onclick="deconnexion()">🚪 Déconnexion</div>
    </nav>

    <section id="start-page" class="site-page active-page">
        <div class="card">
            <h1>Wolf Academy</h1>
            <button onclick="showAuth('login')">Se Connecter</button>
            <button onclick="showAuth('register')" style="background:none; border:1px solid var(--gold); color:var(--gold);">Créer un Compte</button>
        </div>
    </section>

    <section id="auth-page" class="site-page">
        <div class="card">
            <h2 id="auth-title">Connexion</h2>
            <div id="form-fields">
                <input type="text" id="user-nom" placeholder="Votre Nom">
                <input type="tel" id="user-tel" placeholder="N° Téléphone">
            </div>
            <input type="password" id="pin-view" disabled placeholder="****" style="font-size: 1.5rem; letter-spacing: 5px;">
            <div class="digicode" id="keys"></div>
            <button onclick="validerAuth()">Confirmer</button>
            <button onclick="backToStart()" style="background:none; color:white; font-size:0.8rem;">Retour</button>
        </div>
    </section>

    <main id="main-site" style="display:none; margin-top: 70px;">
        <section id="home" class="site-page active-page">
            <div class="card">
                <h2>Bienvenue</h2>
                <p id="welcome-name" class="gold" style="font-size: 1.5rem;"></p>
                <p>Statut : Compte Élite</p>
            </div>
        </section>

        <section id="bank" class="site-page">
            <div class="card">
                <h2>Portefeuille</h2>
                <div style="font-size: 2.5rem; font-weight: bold; margin: 10px 0;"><span id="solde-val">0</span> pts</div>
                <p style="font-size: 0.8rem;">IBAN: <span id="iban-display" style="color:var(--gold)"></span></p>
                <p style="font-size: 0.8rem;">Code Session: <span id="session-code" style="color:var(--gold)"></span></p>
                <hr style="border:0; border-top:1px solid #444; margin:15px 0;">
                <input type="number" id="v-amt" placeholder="Montant à envoyer">
                <input type="text" id="v-sec" placeholder="Code Session">
                <button onclick="transfert()">Envoyer Tokens</button>
            </div>
        </section>

        <section id="admin" class="site-page">
            <div class="card">
                <h2>Coffre-Fort</h2>
                <input type="password" id="adm-pass" placeholder="Code Maître Admin">
                <button onclick="openVault()">Ouvrir</button>
                <div id="vault-content" style="display:none; margin-top:20px;">
                    <button onclick="dotation()" style="background:cyan;">🚀 Lancer Dotation 56 000</button>
                    <input type="password" id="new-adm" placeholder="Nouveau Code Maître">
                    <button onclick="saveNewPass()" style="background:orange;">Changer Code</button>
                </div>
            </div>
        </section>
    </main>

    <div class="url-bar">https://the-bank-token.fr-@lawolfacademy76/websitte.fr</div>

    <script>
        let currentMode = ""; // 'login' ou 'register'
        let pin = "";
        let currentUser = null;
        let masterPass = localStorage.getItem('masterPass') || "ADMIN76";
        let sessionFR = "FR-" + Math.floor(1000 + Math.random()*8999);

        // --- DIGICODE ---
        const keysDiv = document.getElementById('keys');
        [1,2,3,4,5,6,7,8,9,'C',0,'OK'].forEach(k => {
            let btn = document.createElement('div');
            btn.className = 'key'; btn.innerText = k;
            btn.onclick = () => {
                if(k === 'C') pin = "";
                else if(k === 'OK') validerAuth();
                else if(pin.length < 4) pin += k;
                document.getElementById('pin-view').value = "*".repeat(pin.length);
            };
            keysDiv.appendChild(btn);
        });

        function showAuth(mode) {
            currentMode = mode;
            pin = ""; document.getElementById('pin-view').value = "";
            document.getElementById('auth-title').innerText = mode === 'register' ? "Création Compte" : "Connexion";
            document.getElementById('form-fields').style.display = mode === 'register' ? "block" : "none";
            document.getElementById('start-page').className = "site-page";
            document.getElementById('auth-page').className = "site-page active-page";
        }

        function backToStart() {
            document.getElementById('auth-page').className = "site-page";
            document.getElementById('start-page').className = "site-page active-page";
        }

        function validerAuth() {
            if(currentMode === 'register') {
                let nom = document.getElementById('user-nom').value;
                let tel = document.getElementById('user-tel').value;
                if(!nom || !tel || pin.length < 4) return alert("Champs incomplets");
                let user = { nom: nom, tel: tel, pin: pin, solde: 200 };
                localStorage.setItem('user_' + nom, JSON.stringify(user));
                alert("Compte créé ! Connectez-vous.");
                showAuth('login');
            } else {
                // Tentative de connexion (simulation simplifiée)
                // Ici on cherche dans le localStorage par rapport aux comptes créés
                let found = false;
                for(let i=0; i<localStorage.length; i++) {
                    let key = localStorage.key(i);
                    if(key.startsWith('user_')) {
                        let u = JSON.parse(localStorage.getItem(key));
                        if(u.pin === pin) {
                            currentUser = u; found = true; break;
                        }
                    }
                }
                if(found) lancerSite(); else alert("Code PIN incorrect");
            }
        }

        function lancerSite() {
            document.getElementById('auth-page').style.display = "none";
            document.getElementById('main-site').style.display = "block";
            document.getElementById('menu').style.display = "flex";
            document.getElementById('welcome-name').innerText = currentUser.nom;
            document.getElementById('iban-display').innerText = "TK76-WOLF-" + currentUser.tel.slice(-4);
            document.getElementById('session-code').innerText = sessionFR;
            updateUI();
        }

        function deconnexion() { location.reload(); }

        function showComp(id) {
            document.querySelectorAll('main section').forEach(s => s.classList.remove('active-page'));
            document.getElementById(id).classList.add('active-page');
        }

        function transfert() {
            let m = parseInt(document.getElementById('v-amt').value);
            if(document.getElementById('v-sec').value !== sessionFR) return alert("Code Session Invalide");
            if(currentUser.solde - m < -700000) return alert("Limite de découvert atteinte !");
            currentUser.solde -= m;
            saveUser(); updateUI(); alert("Tokens envoyés");
        }

        function openVault() {
            if(document.getElementById('adm-pass').value === masterPass) {
                document.getElementById('vault-content').style.display = "block";
            } else alert("Accès refusé");
        }

        function saveNewPass() {
            let np = document.getElementById('new-adm').value;
            if(np.length < 4) return alert("Trop court");
            masterPass = np; localStorage.setItem('masterPass', np);
            alert("Code Admin sauvegardé !");
        }

        function dotation() {
            currentUser.solde += 56000;
            saveUser(); updateUI(); alert("Dotation 56k effectuée");
        }

        function saveUser() { localStorage.setItem('user_' + currentUser.nom, JSON.stringify(currentUser)); }
        function updateUI() { document.getElementById('solde-val').innerText = currentUser.solde.toLocaleString(); }
    </script>
</body>
</html>
