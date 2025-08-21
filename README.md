# Kasir-retail
Aplikasi Kasir Grosir (Online &amp; Offline) 
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kasir Retail</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h2>Kasir Retail</h2>

  <div id="loginBox">
    <input id="username" placeholder="Username">
    <input id="password" type="password" placeholder="Password">
    <button onclick="login()">Login</button>
  </div>

  <div id="app" style="display:none">
    <h3>Transaksi Baru</h3>
    <input id="item" placeholder="Nama Barang">
    <input id="price" placeholder="Harga" type="number">
    <button onclick="addItem()">Tambah</button>

    <ul id="list"></ul>
    <p>Total: <span id="total">0</span></p>
    <button onclick="printReceipt()">Cetak Struk</button>
  </div>

  <script src="app.js"></script>
</body>
</html>
let total = 0;

function login() {
  const user = document.getElementById("username").value;
  const pass = document.getElementById("password").value;
  if(user === "admin" && pass === "123") {
    document.getElementById("loginBox").style.display = "none";
    document.getElementById("app").style.display = "block";
  } else {
    alert("Login gagal!");
  }
}

function addItem() {
  const item = document.getElementById("item").value;
  const price = parseInt(document.getElementById("price").value);
  if(item && price) {
    const li = document.createElement("li");
    li.textContent = `${item} - Rp${price}`;
    document.getElementById("list").appendChild(li);
    total += price;
    document.getElementById("total").textContent = total;
  }
}

function printReceipt() {
  let text = "=== Struk Kasir Retail ===\n";
  document.querySelectorAll("#list li").forEach(li => {
    text += li.textContent + "\n";
  });
  text += `Total: Rp${total}\nTerima kasih!`;

  // cetak via RawBT (Bluetooth Printer di Android)
  const blob = new Blob([text], {type: "text/plain"});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url;
  a.download = "struk.txt";
  a.click();
}
{
  "name": "kasir-retail",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "build": "electron-packager . KasirRetail --platform=win32 --arch=x64 --out=dist --overwrite"
  },
  "devDependencies": {
    "electron": "^28.0.0",
    "electron-packager": "^17.1.1"
  }
}
const { app, BrowserWindow } = require("electron");

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: { nodeIntegration: true }
  });
  win.loadFile("../web/index.html");
}

app.whenReady().then(createWindow);
# Build Android APK (Kasir Retail)

1. Install Node.js & Android Studio
2. Di root project jalankan:
3. Dari Android Studio → Build APK → Install ke HP.
# Kasir Retail

Aplikasi kasir sederhana (online/offline) untuk grosir & eceran.

### Fitur
- Login sederhana (username: admin, password: 123)
- Input transaksi
- Hitung total
- Cetak struk via Bluetooth Printer (RawBT)

### Cara Jalankan
#### Web/PWA
Buka `web/index.html` di browser.

#### Windows
#### Android
Ikuti `android/README.md`.
