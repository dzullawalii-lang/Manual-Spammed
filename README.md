# Manual-Spammed
Spam WhatsApp
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>DIZX · WhatsApp Spam (Manual Kirim)</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: radial-gradient(circle at 20% 30%, #0a0f1a, #020107);
            font-family: 'Segoe UI', system-ui, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .glass-card {
            background: rgba(12, 12, 28, 0.85);
            backdrop-filter: blur(12px);
            border-radius: 2rem;
            border: 1px solid rgba(255, 45, 117, 0.5);
            max-width: 550px;
            width: 100%;
            padding: 1.8rem;
            box-shadow: 0 25px 40px -12px black;
        }
        h1 {
            font-size: 1.7rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ff2d75, #ff98bb);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-align: center;
        }
        .sub {
            text-align: center;
            color: #aaa;
            font-size: 0.7rem;
            margin-bottom: 1.5rem;
            border-bottom: 1px dashed #ff2d7544;
            padding-bottom: 0.5rem;
        }
        .input-group {
            margin-bottom: 1rem;
        }
        label {
            font-size: 0.7rem;
            text-transform: uppercase;
            color: #ff98bb;
            display: block;
            margin-bottom: 4px;
        }
        input, textarea, select {
            width: 100%;
            background: #01010e;
            border: 1px solid #2a2a4a;
            border-radius: 1rem;
            padding: 10px 12px;
            color: white;
            font-size: 0.9rem;
        }
        button {
            background: linear-gradient(95deg, #ff2d75, #ff5e9e);
            border: none;
            width: 100%;
            padding: 14px;
            border-radius: 2rem;
            font-weight: bold;
            color: white;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 1rem;
            transition: 0.1s;
        }
        button:active {
            transform: scale(0.97);
        }
        .warning {
            font-size: 0.65rem;
            text-align: center;
            margin-top: 1rem;
            color: #ffaa88;
            background: #ff2d7511;
            padding: 8px;
            border-radius: 1rem;
        }
        .status {
            font-size: 0.75rem;
            text-align: center;
            margin-top: 1rem;
            color: #ffccaa;
        }
    </style>
</head>
<body>
<div class="glass-card">
    <h1>📱 SPAM WHATSAPP (MANUAL)</h1>
    <div class="sub">Buka banyak chat WhatsApp dengan pesan siap kirim</div>

    <div class="input-group">
        <label>📞 NOMOR TARGET (awali 62, tanpa +)</label>
        <input type="tel" id="targetNumber" placeholder="6281234567890">
    </div>
    <div class="input-group">
        <label>💬 PESAN SPAM</label>
        <textarea id="message" rows="3" placeholder="Tulis pesan spam di sini...">Halo, ini pesan spam dari DIZX! 😈</textarea>
    </div>
    <div class="input-group">
        <label>🔁 JUMLAH PENGIRIMAN (buka tab)</label>
        <input type="number" id="jumlah" value="5" min="1" max="20">
    </div>

    <button id="spamBtn">💥 BUKA SPAM CHAT 💥</button>
    <div class="status" id="statusMsg"></div>
    <div class="warning">
        ⚠️ Cara kerja: Setiap tab akan membuka WhatsApp (web atau app) dengan pesan terisi.<br>
        Anda harus mengklik tombol KIRIM secara manual di setiap tab.<br>
        Ini bukan spam otomatis, karena WhatsApp tidak mengizinkan pengiriman otomatis lewat browser.
    </div>
</div>

<script>
    const targetInput = document.getElementById('targetNumber');
    const messageInput = document.getElementById('message');
    const jumlahInput = document.getElementById('jumlah');
    const spamBtn = document.getElementById('spamBtn');
    const statusDiv = document.getElementById('statusMsg');

    function formatNumber(num) {
        let clean = num.replace(/\D/g, '');
        if (clean.startsWith('0')) clean = '62' + clean.substring(1);
        if (!clean.startsWith('62')) clean = '62' + clean;
        return clean;
    }

    function openWhatsAppTabs() {
        let rawNumber = targetInput.value.trim();
        if (rawNumber === "") {
            statusDiv.innerHTML = "❌ Masukkan nomor target!";
            return;
        }
        let message = messageInput.value.trim();
        if (message === "") {
            statusDiv.innerHTML = "❌ Masukkan pesan spam!";
            return;
        }
        let jumlah = parseInt(jumlahInput.value);
        if (isNaN(jumlah) || jumlah < 1) jumlah = 1;
        if (jumlah > 20) jumlah = 20;

        const formattedNumber = formatNumber(rawNumber);
        const encodedMessage = encodeURIComponent(message);
        let opened = 0;

        for (let i = 0; i < jumlah; i++) {
            // jeda 200ms agar tidak diblokir popup
            setTimeout(() => {
                const waLink = `https://wa.me/${formattedNumber}?text=${encodedMessage}`;
                window.open(waLink, '_blank');
                opened++;
                statusDiv.innerHTML = `✅ Membuka tab ke-${opened} dari ${jumlah}...`;
            }, i * 200);
        }

        setTimeout(() => {
            statusDiv.innerHTML = `✔️ Selesai! ${jumlah} tab WhatsApp telah terbuka. Kirim manual setiap tab.`;
        }, jumlah * 200 + 500);
    }

    spamBtn.addEventListener('click', openWhatsAppTabs);
</script>
</body>
</html>
