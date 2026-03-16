# Mpay-
Hos Mpay kan du både ha dine penge men du kan også sende dem til hele verden til 0 kr i oprettets 

<!DOCTYPE html>
<html lang="da">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Mpay 2026 - The Global Hub</title>
    <style>
        :root {
            --glass: rgba(255, 255, 255, 0.08);
            --accent: #00f2ff;
            --accent-glow: rgba(0, 242, 255, 0.5);
            --bg: #02050a;
            --success: #00ff88;
            --danger: #ff3366;
            --text-main: #ffffff;
            --trustpilot: #00b67a;
        }

        body {
            margin: 0; background: var(--bg); color: var(--text-main);
            font-family: 'Inter', -apple-system, sans-serif; overflow: hidden; height: 100vh;
            background: radial-gradient(circle at 50% -10%, #1a2a44 0%, #02050a 100%);
        }

        .glass { background: var(--glass); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.12); border-radius: 32px; }
        .container { padding: 25px; height: calc(100vh - 160px); overflow-y: auto; scrollbar-width: none; }
        .hidden { display: none !important; }

        /* Mpay Card */
        .mpay-card {
            background: linear-gradient(135deg, rgba(255,255,255,0.15), rgba(255,255,255,0.02));
            padding: 25px; border-radius: 28px; border: 1px solid rgba(255,255,255,0.2);
            position: relative; margin-bottom: 25px; box-shadow: 0 15px 35px rgba(0,0,0,0.4);
        }
        .privacy-toggle { position: absolute; top: 20px; right: 20px; font-size: 20px; cursor: pointer; }
        .card-data { font-family: 'Courier New', monospace; letter-spacing: 2px; transition: 0.3s; }
        .blurred { filter: blur(10px); }

        /* Payment Methods */
        .method-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 20px; }
        .method-btn { padding: 15px; text-align: center; border-radius: 18px; border: 1px solid rgba(255,255,255,0.1); cursor: pointer; font-size: 13px; background: rgba(255,255,255,0.03); }
        .method-btn.selected { background: var(--accent); color: #000; font-weight: bold; border-color: var(--accent); }

        /* Inputs & Buttons */
        .cyber-input { width: 100%; box-sizing: border-box; background: rgba(0,0,0,0.5); border: 1px solid rgba(255,255,255,0.1); padding: 16px; border-radius: 16px; color: #fff; margin-bottom: 12px; font-size: 16px; outline: none; }
        .btn-pay { width: 100%; padding: 18px; background: var(--accent); color: #000; border: none; border-radius: 18px; font-weight: 900; cursor: pointer; text-transform: uppercase; }

        /* Settings */
        .settings-row { display: flex; justify-content: space-between; align-items: center; padding: 15px 0; border-bottom: 1px solid rgba(255,255,255,0.05); }
        select { background: rgba(255,255,255,0.1); color: white; border: none; padding: 8px; border-radius: 10px; }

        /* Trustpilot */
        .tp-badge { margin-top: 30px; padding: 20px; text-align: center; background: rgba(0, 182, 122, 0.1); border: 1px solid var(--trustpilot); border-radius: 20px; }
        .stars { color: var(--trustpilot); font-size: 22px; margin-bottom: 5px; }

        /* Nav */
        .nav-bar { position: fixed; bottom: 30px; left: 25px; right: 25px; height: 80px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; }
        .nav-item { font-size: 24px; opacity: 0.3; cursor: pointer; transition: 0.3s; }
        .nav-item.active { opacity: 1; color: var(--accent); transform: translateY(-5px); }

        /* Receipt */
        #receipt-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 3000; display: flex; align-items: center; justify-content: center; backdrop-filter: blur(10px); }
        .receipt-box { width: 80%; padding: 30px; background: #fff; color: #000; border-radius: 24px; text-align: center; }
    </style>
</head>
<body>

<div id="view-auth" style="text-align: center; padding: 100px 30px;">
    <h1 style="letter-spacing: 15px; color: var(--accent); text-shadow: 0 0 20px var(--accent-glow);">MPAY</h1>
    <div class="glass" style="padding: 30px; margin-top: 30px;">
        <input type="text" id="reg-user" class="cyber-input" placeholder="Brugernavn">
        <input type="email" id="reg-mail" class="cyber-input" placeholder="E-mail">
        <button class="btn-pay" onclick="initApp()">Log ind</button>
    </div>
</div>

<div id="main-app" class="hidden">
    <div class="container">
        
        <div id="view-home">
            <div style="text-align: center; padding: 20px 0;">
                <div style="font-size: 10px; opacity: 0.5; letter-spacing: 2px;" id="txt-bal-label">SALDO</div>
                <div style="font-size: 46px; font-weight: 900;" id="main-bal">0.00 kr.</div>
            </div>

            <div class="mpay-card">
                <div class="privacy-toggle" onclick="togglePrivacy()" id="p-icon">👁️</div>
                <div style="font-weight: bold; color: var(--accent); margin-bottom: 10px; font-size: 12px;">MPAY ELITE</div>
                <div id="display-user" style="font-size: 10px; margin-bottom: 15px; opacity: 0.7; text-transform: uppercase;">-</div>
                <div class="card-data blurred" style="font-size: 18px; margin-bottom: 15px;">4571 8820 1192 4403</div>
                <div style="display: flex; justify-content: space-between; font-size: 10px;">
                    <div class="card-data blurred">REG: 9022<br>KONTO: 12883901</div>
                    <div class="card-data blurred" style="text-align: right;">CVV: 319<br>12/28</div>
                </div>
            </div>

            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 30px;">
                <button class="glass" style="padding: 15px; color: var(--success); font-weight: bold;" onclick="openTransfer('in')">📥 INDSÆT</button>
                <button class="glass" style="padding: 15px; color: var(--accent); font-weight: bold;" onclick="openTransfer('out')">📤 SEND</button>
            </div>

            <h3 style="font-size: 13px; opacity: 0.6; margin-bottom: 10px;">AKTIVITET</h3>
            <div id="tx-feed"><div style="text-align: center; opacity: 0.2; padding: 20px; font-size: 12px;">Klar til brug</div></div>
        </div>

        <div id="view-transfer" class="hidden">
            <h2 id="hub-title">Handling</h2>
            <p style="font-size: 12px; opacity: 0.5; margin-bottom: 20px;">Vælg betalingsmetode:</p>
            
            <div class="method-grid">
                <div class="method-btn" onclick="selectM('MobilePay', this)">MobilePay</div>
                <div class="method-btn" onclick="selectM('Apple Pay', this)">Apple Pay</div>
                <div class="method-btn" onclick="selectM('Google Pay', this)">Google Pay</div>
                <div class="method-btn" onclick="selectM('Kort / Bank', this)">Kort / Bank</div>
            </div>

            <div class="glass" style="padding: 25px;">
                <input type="number" id="h-val" class="cyber-input" placeholder="0,00">
                <input type="text" id="h-info" class="cyber-input" placeholder="Modtager / Info">
                <button id="h-btn" class="btn-pay" onclick="processAction()">Gennemfør</button>
            </div>
            <button onclick="showPage('home')" style="width:100%; background:none; border:none; color:grey; margin-top:20px;">Annuller</button>
        </div>

        <div id="view-settings" class="hidden">
            <h2 id="txt-settings-label">Indstillinger</h2>
            <div class="glass" style="padding: 20px;">
                <div class="settings-row">
                    <span>Sprog</span>
                    <select id="lang-select" onchange="updateLang()">
                        <option value="da">Dansk 🇩🇰</option>
                        <option value="en">English 🇬🇧</option>
                        <option value="de">Deutsch 🇩🇪</option>
                    </select>
                </div>
                <div class="settings-row">
                    <span>Valuta</span>
                    <select id="curr-select" onchange="updateUI()">
                        <option value="kr.">DKK (kr.)</option>
                        <option value="$">USD ($)</option>
                        <option value="€">EUR (€)</option>
                    </select>
                </div>
            </div>

            <div class="tp-badge">
                <div style="font-weight: bold; font-size: 14px;">Trustpilot</div>
                <div class="stars">★★★★★</div>
                <div style="font-size: 11px; opacity: 0.8;">Mpay har 5 stjerner på Trustpilot</div>
            </div>

            <button class="btn-pay" style="margin-top: 30px; background: var(--danger); color: white;" onclick="location.reload()">Log ud</button>
        </div>

    </div>

    <nav class="glass nav-bar">
        <div class="nav-item active" onclick="showPage('home')">🏠</div>
        <div class="nav-item" onclick="openTransfer('in')">📥</div>
        <div class="nav-item" onclick="openTransfer('out')">📤</div>
        <div class="nav-item" onclick="showPage('settings')">⚙️</div>
    </nav>
</div>

<div id="receipt-overlay" class="hidden">
    <div class="receipt-box">
        <div style="color: var(--success); font-size: 40px; margin-bottom: 10px;">✓</div>
        <h2 style="margin: 0;">Mpay Kvittering</h2>
        <hr style="border: none; border-top: 1px dashed #ccc; margin: 20px 0;">
        <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
            <span>Beløb:</span><strong id="r-amt"></strong>
        </div>
        <div style="display: flex; justify-content: space-between; margin-bottom: 20px;">
            <span>Via:</span><strong id="r-via"></strong>
        </div>
        <button class="btn-pay" style="background: #000; color: #fff;" onclick="closeReceipt()">Luk</button>
    </div>
</div>

<script>
    let balance = 0.00;
    let isBlurred = true;
    let currentMode = ""; 
    let selectedMethod = "";

    const trans = {
        da: { bal: "SALDO", set: "Indstillinger", in: "Indbetaling", out: "Udbetaling" },
        en: { bal: "BALANCE", set: "Settings", in: "Deposit", out: "Withdrawal" },
        de: { bal: "KONTOSTAND", set: "Einstellungen", in: "Einzahlung", out: "Auszahlung" }
    };

    function initApp() {
        const user = document.getElementById('reg-user').value;
        if(user && document.getElementById('reg-mail').value.includes('@')) {
            document.getElementById('display-user').innerText = "Bruger: " + user;
            document.getElementById('view-auth').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            updateUI();
        }
    }

    function togglePrivacy() {
        isBlurred = !isBlurred;
        document.querySelectorAll('.card-data').forEach(el => isBlurred ? el.classList.add('blurred') : el.classList.remove('blurred'));
        document.getElementById('p-icon').innerText = isBlurred ? '👁️' : '🔒';
    }

    function showPage(page) {
        ['home', 'settings', 'transfer'].forEach(p => document.getElementById('view-'+p).classList.add('hidden'));
        document.getElementById('view-'+page).classList.remove('hidden');
        
        const items = document.querySelectorAll('.nav-item');
        items.forEach(i => i.classList.remove('active'));
        if(page === 'home') items[0].classList.add('active');
        if(page === 'settings') items[3].classList.add('active');
    }

    function openTransfer(dir) {
        currentMode = dir;
        const l = document.getElementById('lang-select').value;
        document.getElementById('hub-title').innerText = trans[l][dir];
        document.getElementById('h-btn').style.background = dir === 'in' ? 'var(--success)' : 'var(--accent)';
        showPage('transfer');
        
        const items = document.querySelectorAll('.nav-item');
        items.forEach(i => i.classList.remove('active'));
        if(dir === 'in') items[1].classList.add('active');
        else items[2].classList.add('active');
    }

    function selectM(m, el) {
        selectedMethod = m;
        document.querySelectorAll('.method-btn').forEach(b => b.classList.remove('selected'));
        el.classList.add('selected');
    }

    function processAction() {
        const val = parseFloat(document.getElementById('h-val').value);
        if(!selectedMethod || isNaN(val) || val <= 0) { alert("Vælg metode og beløb!"); return; }

        if(currentMode === 'out' && val > balance) {
            alert("Fejl: Ingen dækning på kontoen!");
            return;
        }

        if(currentMode === 'in') {
            balance += val;
            addTx(selectedMethod, val, 'plus');
        } else {
            balance -= val;
            addTx(document.getElementById('h-info').value || "Udbetaling", val, 'minus');
        }

        const symbol = document.getElementById('curr-select').value;
        document.getElementById('r-amt').innerText = val.toLocaleString('da-DK') + " " + symbol;
        document.getElementById('r-via').innerText = selectedMethod;
        document.getElementById('receipt-overlay').classList.remove('hidden');
        updateUI();
    }

    function closeReceipt() {
        document.getElementById('receipt-overlay').classList.add('hidden');
        showPage('home');
        document.getElementById('h-val').value = '';
        document.getElementById('h-info').value = '';
    }

    function updateLang() {
        const l = document.getElementById('lang-select').value;
        document.getElementById('txt-bal-label').innerText = trans[l].bal;
        document.getElementById('txt-settings-label').innerText = trans[l].set;
    }

    function updateUI() {
        const symbol = document.getElementById('curr-select').value;
        document.getElementById('main-bal').innerText = balance.toLocaleString('da-DK', {minimumFractionDigits: 2}) + " " + symbol;
    }

    function addTx(name, val, type) {
        const feed = document.getElementById('tx-feed');
        if(feed.innerText.includes('Klar')) feed.innerHTML = '';
        const color = type === 'plus' ? 'var(--success)' : 'white';
        const prefix = type === 'plus' ? '+' : '-';
        const symbol = document.getElementById('curr-select').value;
        
        feed.innerHTML = `
            <div class="glass" style="padding:15px; margin-bottom:10px; display:flex; justify-content:space-between; font-size:13px;">
                <span>${name}</span>
                <span style="font-weight:900; color:${color}">${prefix}${val.toLocaleString('da-DK')} ${symbol}</span>
            </div>
        ` + feed.innerHTML;
    }
</script>

</body>
</html>
