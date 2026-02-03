# ProjectRamafedri
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Indofood Warehouse QR Scan</title>
<script src="https://unpkg.com/html5-qrcode"></script>

<style>
body {
    margin: 0;
    font-family: "Segoe UI", Arial, sans-serif;
    background: linear-gradient(135deg, #ffffff, #f2f2f2);
    color: #1a1a1a;
}

/* HEADER */
header {
    background: linear-gradient(90deg, #b30000, #003a8f);
    padding: 25px 15px;
    text-align: center;
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

header img {
    height: 60px;
    margin-bottom: 10px;
}

header h1 {
    margin: 0;
    font-size: 30px;
    letter-spacing: 2px;
    color: #ffffff;
}

/* CONTAINER */
.container {
    display: flex;
    justify-content: center;
    gap: 40px;
    padding: 50px 20px;
    flex-wrap: wrap;
}

/* CARD */
.card {
    background: #ffffff;
    border-radius: 20px;
    padding: 35px;
    width: 460px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.15);
    border-top: 6px solid #b30000;
}

.card h2 {
    text-align: center;
    font-size: 26px;
    margin-bottom: 28px;
    padding-bottom: 12px;
    border-bottom: 3px solid #003a8f;
    color: #003a8f;
}

/* SCANNER */
#reader {
    width: 100%;
}

/* DATA ROW */
.data-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 20px 0;
    font-size: 22px;
}

.label {
    color: #555;
    font-weight: 600;
}

.value {
    font-weight: 700;
}

/* STATUS */
.ok {
    color: #1fa84f;
}

.reject {
    color: #d60000;
}

/* FOOTER */
footer {
    text-align: center;
    padding: 20px;
    color: #777;
    font-size: 14px;
}
</style>
</head>

<body>

<header>
    <img src="https://upload.wikimedia.org/wikipedia/commons/7/7e/Indofood_logo.svg" alt="Indofood Logo">
    <h1>WAREHOUSE QR SCAN SYSTEM</h1>
</header>

<div class="container">

    <!-- SCANNER -->
    <div class="card">
        <h2>SCAN QR CODE</h2>
        <div id="reader"></div>
    </div>

    <!-- DETAIL PRODUK -->
    <div class="card">
        <h2>DETAIL PRODUK</h2>

        <div class="data-row">
            <span class="label">Nama Produk</span>
            <span id="nama" class="value">-</span>
        </div>

        <div class="data-row">
            <span class="label">Berat (KG)</span>
            <span id="berat" class="value">-</span>
        </div>

        <div class="data-row">
            <span class="label">Status</span>
            <span id="status" class="value">-</span>
        </div>
    </div>

</div>

<footer>Soal Test Programmer – Sistem Gudang Indofood</footer>

<script>
/* ===== DATABASE SESUAI TABEL DI SOAL ===== */
const database = {
    "1": { nama: "Indomie Kari", berat: "100", status: "OKE" },
    "2": { nama: "Indomie Soto", berat: "500", status: "REJECT" },
    "3": { nama: "Indomie Goreng", berat: "600", status: "OKE" },
    "4": { nama: "Sarimi", berat: "400", status: "REJECT" },
    "5": { nama: "Supermi", berat: "200", status: "OKE" }
};

function onScanSuccess(decodedText) {
    const id = decodedText.match(/\d+/)?.[0];

    if (!database[id]) {
        alert("Produk tidak ditemukan!");
        return;
    }

    const data = database[id];

    document.getElementById("nama").innerText = data.nama;
    document.getElementById("berat").innerText = data.berat + " KG";

    const statusEl = document.getElementById("status");
    statusEl.innerText = data.status;
    statusEl.className = "value " + (data.status === "OKE" ? "ok" : "reject");
}

/* AKTIFKAN SCANNER */
new Html5Qrcode("reader").start(
    { facingMode: "environment" },
    { fps: 10, qrbox: 280 },
    onScanSuccess
);
</script>

</body>
</html>
