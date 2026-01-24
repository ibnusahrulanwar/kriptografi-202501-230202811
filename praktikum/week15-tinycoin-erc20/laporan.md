# Laporan Praktikum Kriptografi
Minggu ke-: 15  
Topik: Proyek Kelompok – TinyCoin ERC20
Nama: Ibnu Sahrul Anwar  
NIM: 230202811 
Kelas: 5IKKA

---

## 1. Tujuan
Setelah mengikuti praktikum ini, mahasiswa diharapkan mampu:
1. Mengembangkan proyek sederhana berbasis algoritma kriptografi.
2. Mendokumentasikan proses implementasi proyek ke dalam repository Git.
3. Menyusun laporan teknis hasil proyek akhir.
(Tuliskan tujuan pembelajaran praktikum sesuai modul.)

---

## 2. Dasar Teori
ERC-20 merupakan standar token pada blockchain Ethereum yang mendefinisikan aturan dan fungsi dasar agar sebuah token dapat beroperasi secara kompatibel dengan berbagai wallet aplikasi terdesentralisasi dan exchange TinyCoin ERC-20 adalah implementasi token sederhana yang mengikuti standar ini untuk tujuan pembelajaran sehingga pengguna dapat memahami bagaimana aset digital diciptakan dikelola dan dipindahkan tanpa otoritas terpusat.

Standar ERC-20 menyediakan fungsi inti seperti pengecekan saldo transfer token serta mekanisme persetujuan penggunaan token oleh pihak lain Dengan mengikuti standar ini TinyCoin dapat berinteraksi dengan ekosistem Ethereum secara luas Setiap transaksi TinyCoin diproses melalui smart contract dan divalidasi oleh jaringan Ethereum sehingga bersifat transparan aman dan tercatat permanen di blockchain.

Meskipun mudah diimplementasikan keamanan TinyCoin ERC-20 sangat bergantung pada kualitas smart contract Kesalahan logika atau bug dapat menimbulkan risiko Oleh karena itu praktik seperti penggunaan library standar pengujian di testnet dan audit kode sangat penting untuk memastikan token berjalan dengan aman dan andal.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub
- Metamask
- REMIX IDE  
- Library tambahan 

---

## 4. Langkah Percobaan
 1. Membuat file `index.html , style.css , script.js , Donation.sol` di folder `praktikum/week15-tinycoin-erc20/src/`.

# 2. Membuat Akun Metamask dan mendownload add on nya

# 3. Buka dan siapkan file `Donation.sol`untuk di simpan di dalam Remix IDE https://remix.ethereum.org 
![Hasil Eksekusi](screenshots/remix1.png)

# 4. Masuk ke menu Solidity Compiler , lalu Compile and Run Script
![Hasil Eksekusi](screenshots/remix2.png)

# 5. Jika sudah membuat dan memiliki Metamask, langkah selanjutnya adalah ganti netwok di metamask menjadi Sepolia. Kemudian copy dan paste wallet addres ke dalam web ini https://sepolia-faucet.pk910.de/#/
![Hasil Eksekusi](screenshots/ether.png)
![Hasil Eksekusi](screenshots/mining1.png)
![Hasil Eksekusi](screenshots/mining2.png)
![Hasil Eksekusi](screenshots/mining3.png)

# Lalu Start Mining, tunggu sampai koin melebihi minimum atau maximum claim

# 6. Langkah selanjutnya kembali ke Remix IDE untuk pengaturan Donate dan membuat smartcontract, Pilih Inject Provide- Metamask di dalam Environment dan Masukkan Wallet Addres Sepolia (otomatis mendeteksi account) , pastikan masih value 0 dan wei.
![Hasil Eksekusi](screenshots/remix4.png)

# Setelah konfirmasi akan muncul view code smartcontract
![Hasil Eksekusi](screenshots/remix5.png)

# di bawahnya ganti wei menjadi gwei dan pilih berapa Value yang kita mau transaksikan..contoh: 1.000.000 gwei yang nantinya akan menjadi 0.001ETH 
![Hasil Eksekusi](screenshots/remix6.png)
![Hasil Eksekusi](screenshots/remix7.png)

# 7. Buka link view etherscan yang muncul di terminal...Maka kita akan melihat transaksi keluar di Wallet Sepolia dan transaksi masuk di Balance Smartcontract yang tadi dibuat
![Hasil Eksekusi](screenshots/remix8.png)
![Hasil Eksekusi](screenshots/remix9.png)
![Hasil Eksekusi](screenshots/remix10.png)
![Hasil Eksekusi](screenshots/remix11.png)
---

## 5. Source Code
# index.html
```python
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Luxury Web3 Donation</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <link rel="stylesheet" href="style.css">
  <script src="https://cdn.jsdelivr.net/npm/ethers@6.9.0/dist/ethers.min.js"></script>
</head>
<body>

<div class="bg-orb orb-1"></div>
<div class="bg-orb orb-2"></div>

<main class="card">
  <h1>Web3 Donation</h1>
  <p class="subtitle">Transparan • Aman • Terdesentralisasi</p>

  <div class="input-group">
    <span>ETH</span>
    <input type="number" id="amount" placeholder="0.01" step="0.001">
  </div>

  <button onclick="donate()">Donate Now</button>

  <div id="status"></div>

  <footer>
    Powered by Ethereum • Sepolia Testnet
  </footer>
</main>

<script src="script.js"></script>
</body>
</html>

```

# style.css
```python
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap');

* {
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

body {
  margin: 0;
  height: 100vh;
  background: radial-gradient(circle at top, #0f172a, #020617);
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  overflow: hidden;
}

/* Background Orbs */
.bg-orb {
  position: absolute;
  width: 420px;
  height: 420px;
  border-radius: 50%;
  filter: blur(140px);
  opacity: 0.45;
}

.orb-1 {
  background: #f59e0b;
  top: -120px;
  left: -120px;
}

.orb-2 {
  background: #38bdf8;
  bottom: -120px;
  right: -120px;
}

/* Card */
.card {
  width: 380px;
  padding: 36px;
  border-radius: 22px;
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(18px);
  box-shadow: 0 25px 80px rgba(0,0,0,0.55);
  text-align: center;
  z-index: 1;
}

.card h1 {
  font-size: 28px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.subtitle {
  font-size: 14px;
  opacity: 0.75;
  margin-bottom: 28px;
}

/* Input */
.input-group {
  display: flex;
  align-items: center;
  background: rgba(255,255,255,0.12);
  border-radius: 14px;
  padding: 12px 14px;
  margin-bottom: 22px;
}

.input-group span {
  font-weight: 600;
  margin-right: 8px;
  opacity: 0.9;
}

.input-group input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  font-size: 15px;
}

/* Button */
button {
  width: 100%;
  padding: 14px;
  border-radius: 14px;
  border: none;
  background: linear-gradient(135deg, #f59e0b, #ef4444);
  color: #fff;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.35s;
}

button:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 30px rgba(245, 158, 11, 0.45);
}

/* Status */
#status {
  margin-top: 18px;
  font-size: 14px;
  min-height: 20px;
}

/* Footer */
footer {
  margin-top: 26px;
  font-size: 12px;
  opacity: 0.55;
}

.donation-stats {
  background: linear-gradient(135deg, #111, #1f1f1f);
  border-radius: 16px;
  padding: 24px;
  margin: 20px 0;
  text-align: center;
  box-shadow: 0 0 20px rgba(255, 215, 0, 0.2);
}

.donation-stats p {
  color: #aaa;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.donation-stats h2 {
  color: gold;
  font-size: 2.2rem;
}

.stats {
  margin-top: 20px;
  padding: 14px;
  background: rgba(255,255,255,0.08);
  border-radius: 14px;
}

.stats h3 {
  margin: 0;
  font-size: 13px;
  opacity: 0.7;
}

#total {
  font-size: 20px;
  font-weight: 600;
}

#history {
  margin-top: 18px;
  list-style: none;
  padding: 0;
  max-height: 120px;
  overflow-y: auto;
}

#history li {
  font-size: 12px;
  opacity: 0.75;
  margin-bottom: 6px;
}
```

# script.js
```python
const contractAddress = "0x8E6e34F439EedE36f4c8fB435511A6BD08E8a259";

const abi = [
  "function donate() payable",
  "function totalDonations() view returns (uint256)"
];

async function donate() {
  if (!window.ethereum) {
    alert("MetaMask tidak ditemukan");
    return;
  }

  const amount = document.getElementById("amount").value;
  if (!amount || amount <= 0) {
    alert("Masukkan jumlah ETH");
    return;
  }

  try {
    const provider = new ethers.BrowserProvider(window.ethereum);
    await provider.send("eth_requestAccounts", []);
    const signer = await provider.getSigner();

    const contract = new ethers.Contract(
      contractAddress,
      abi,
      signer
    );

    document.getElementById("status").innerText =
      "⏳ Menunggu konfirmasi MetaMask...";

    const tx = await contract.donate({
      value: ethers.parseEther(amount)
    });

    document.getElementById("status").innerText =
      "⛓️ Transaksi diproses di blockchain...";

    await tx.wait();

    document.getElementById("status").innerText =
      "✅ Donasi berhasil via Smart Contract! 🤍";

  } catch (err) {
    console.error(err);
    document.getElementById("status").innerText =
      "❌ Transaksi dibatalkan / gagal";
  }
}

```

# donate.sol
```python
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/// @title Donation Smart Contract
/// @author Ramzi
/// @notice Contract untuk menerima donasi ETH
/// @custom:dev-run-script scripts/deploy.js
contract Donation {
    address public owner;
    uint256 public totalDonations;

    constructor() {
        owner = msg.sender;
    }

    function donate() external payable {
        require(msg.value > 0, "Donation must be greater than 0");
        totalDonations += msg.value;
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");

        uint256 balance = address(this).balance;
        require(balance > 0, "No funds");

        (bool success, ) = payable(owner).call{value: balance}("");
        require(success, "ETH transfer failed");
    }
}

```
---

## 6. Hasil dan Pembahasan
- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

1. Hasil Pengujian Menggunakan Remix IDE

Berdasarkan pengujian yang dilakukan menggunakan Remix IDE, fungsi donasi pada smart contract berhasil dijalankan dengan baik. Proses pengujian dilakukan dengan langkah-langkah sebagai berikut:
- Smart contract berhasil di-deploy pada jaringan Sepolia Testnet.
- Pengujian fungsi donate() dilakukan dengan mengisi nilai 0.1 ETH pada kolom Value di Remix IDE.
- Transaksi berhasil dikonfirmasi oleh MetaMask dan tercatat di blockchain.
- Nilai donasi yang dikirim dapat diterima oleh smart contract melalui msg.value.
- Total donasi pada kontrak bertambah sesuai dengan nilai yang dikirim.
Hasil ini menunjukkan bahwa logika smart contract berjalan dengan benar, termasuk validasi require(msg.value > 0) dan pencatatan transaksi donasi.

2. Hasil Pengujian Menggunakan Website (Frontend)

Pengujian selanjutnya dilakukan melalui website yang dibangun menggunakan HTML, CSS, dan JavaScript (ethers.js). Namun, pada tahap ini ditemukan beberapa kendala, yaitu:
- Tombol Donate dapat diklik, tetapi transaksi tidak berhasil mengirimkan nilai ETH sesuai input.
- Transaksi tidak tercatat di blockchain, meskipun fungsi donate() dipanggil.Ini artinya fungsi donate() maupun yang ada di script.js tidak berfungsi dengan baik.
Dengan demikian, fungsi donasi tidak berjalan sebagaimana yang diharapkan.

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi](screenshots/webdonate.png)


---
# index.html
```python
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Luxury Web3 Donation</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <link rel="stylesheet" href="style.css">
  <script src="https://cdn.jsdelivr.net/npm/ethers@6.9.0/dist/ethers.min.js"></script>
</head>
<body>

<div class="bg-orb orb-1"></div>
<div class="bg-orb orb-2"></div>

<main class="card">
  <h1>Web3 Donation</h1>
  <p class="subtitle">Transparan • Aman • Terdesentralisasi</p>

  <div class="input-group">
    <span>ETH</span>
    <input type="number" id="amount" placeholder="0.01" step="0.001">
  </div>

  <button onclick="donate()">Donate Now</button>

  <div id="status"></div>

  <footer>
    Powered by Ethereum • Sepolia Testnet
  </footer>
</main>

<script src="script.js"></script>
</body>
</html>

```

# style.css
```python
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap');

* {
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

body {
  margin: 0;
  height: 100vh;
  background: radial-gradient(circle at top, #0f172a, #020617);
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  overflow: hidden;
}

/* Background Orbs */
.bg-orb {
  position: absolute;
  width: 420px;
  height: 420px;
  border-radius: 50%;
  filter: blur(140px);
  opacity: 0.45;
}

.orb-1 {
  background: #f59e0b;
  top: -120px;
  left: -120px;
}

.orb-2 {
  background: #38bdf8;
  bottom: -120px;
  right: -120px;
}

/* Card */
.card {
  width: 380px;
  padding: 36px;
  border-radius: 22px;
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(18px);
  box-shadow: 0 25px 80px rgba(0,0,0,0.55);
  text-align: center;
  z-index: 1;
}

.card h1 {
  font-size: 28px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.subtitle {
  font-size: 14px;
  opacity: 0.75;
  margin-bottom: 28px;
}

/* Input */
.input-group {
  display: flex;
  align-items: center;
  background: rgba(255,255,255,0.12);
  border-radius: 14px;
  padding: 12px 14px;
  margin-bottom: 22px;
}

.input-group span {
  font-weight: 600;
  margin-right: 8px;
  opacity: 0.9;
}

.input-group input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  font-size: 15px;
}

/* Button */
button {
  width: 100%;
  padding: 14px;
  border-radius: 14px;
  border: none;
  background: linear-gradient(135deg, #f59e0b, #ef4444);
  color: #fff;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.35s;
}

button:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 30px rgba(245, 158, 11, 0.45);
}

/* Status */
#status {
  margin-top: 18px;
  font-size: 14px;
  min-height: 20px;
}

/* Footer */
footer {
  margin-top: 26px;
  font-size: 12px;
  opacity: 0.55;
}

.donation-stats {
  background: linear-gradient(135deg, #111, #1f1f1f);
  border-radius: 16px;
  padding: 24px;
  margin: 20px 0;
  text-align: center;
  box-shadow: 0 0 20px rgba(255, 215, 0, 0.2);
}

.donation-stats p {
  color: #aaa;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.donation-stats h2 {
  color: gold;
  font-size: 2.2rem;
}

.stats {
  margin-top: 20px;
  padding: 14px;
  background: rgba(255,255,255,0.08);
  border-radius: 14px;
}

.stats h3 {
  margin: 0;
  font-size: 13px;
  opacity: 0.7;
}

#total {
  font-size: 20px;
  font-weight: 600;
}

#history {
  margin-top: 18px;
  list-style: none;
  padding: 0;
  max-height: 120px;
  overflow-y: auto;
}

#history li {
  font-size: 12px;
  opacity: 0.75;
  margin-bottom: 6px;
}
```

# script.js
```python
const contractAddress = "0x8E6e34F439EedE36f4c8fB435511A6BD08E8a259";

const abi = [
  "function donate() payable",
  "function totalDonations() view returns (uint256)"
];

async function donate() {
  if (!window.ethereum) {
    alert("MetaMask tidak ditemukan");
    return;
  }

  const amount = document.getElementById("amount").value;
  if (!amount || amount <= 0) {
    alert("Masukkan jumlah ETH");
    return;
  }

  try {
    const provider = new ethers.BrowserProvider(window.ethereum);
    await provider.send("eth_requestAccounts", []);
    const signer = await provider.getSigner();

    const contract = new ethers.Contract(
      contractAddress,
      abi,
      signer
    );

    document.getElementById("status").innerText =
      "⏳ Menunggu konfirmasi MetaMask...";

    const tx = await contract.donate({
      value: ethers.parseEther(amount)
    });

    document.getElementById("status").innerText =
      "⛓️ Transaksi diproses di blockchain...";

    await tx.wait();

    document.getElementById("status").innerText =
      "✅ Donasi berhasil via Smart Contract! 🤍";

  } catch (err) {
    console.error(err);
    document.getElementById("status").innerText =
      "❌ Transaksi dibatalkan / gagal";
  }
}

```

# donate.sol
```python
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/// @title Donation Smart Contract
/// @author Ramzi
/// @notice Contract untuk menerima donasi ETH
/// @custom:dev-run-script scripts/deploy.js
contract Donation {
    address public owner;
    uint256 public totalDonations;

    constructor() {
        owner = msg.sender;
    }

    function donate() external payable {
        require(msg.value > 0, "Donation must be greater than 0");
        totalDonations += msg.value;
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");

        uint256 balance = address(this).balance;
        require(balance > 0, "No funds");

        (bool success, ) = payable(owner).call{value: balance}("");
        require(success, "ETH transfer failed");
    }
}

## 6. Hasil dan Pembahasan
- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

1. Hasil Pengujian Menggunakan Remix IDE

Berdasarkan pengujian yang dilakukan menggunakan Remix IDE, fungsi donasi pada smart contract berhasil dijalankan dengan baik. Proses pengujian dilakukan dengan langkah-langkah sebagai berikut:
- Smart contract berhasil di-deploy pada jaringan Sepolia Testnet.
- Pengujian fungsi donate() dilakukan dengan mengisi nilai 0.1 ETH pada kolom Value di Remix IDE.
- Transaksi berhasil dikonfirmasi oleh MetaMask dan tercatat di blockchain.
- Nilai donasi yang dikirim dapat diterima oleh smart contract melalui msg.value.
- Total donasi pada kontrak bertambah sesuai dengan nilai yang dikirim.
Hasil ini menunjukkan bahwa logika smart contract berjalan dengan benar, termasuk validasi require(msg.value > 0) dan pencatatan transaksi donasi.

2. Hasil Pengujian Menggunakan Website (Frontend)

Pengujian selanjutnya dilakukan melalui website yang dibangun menggunakan HTML, CSS, dan JavaScript (ethers.js). Namun, pada tahap ini ditemukan beberapa kendala, yaitu:
- Tombol Donate dapat diklik, tetapi transaksi tidak berhasil mengirimkan nilai ETH sesuai input.
- Transaksi tidak tercatat di blockchain, meskipun fungsi donate() dipanggil.Ini artinya fungsi donate() maupun yang ada di script.js tidak berfungsi dengan baik.
Dengan demikian, fungsi donasi tidak berjalan sebagaimana yang diharapkan.

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi]![screenshotswebdonate png](https://github.com/user-attachments/assets/23091602-0615-4c6f-8936-6ac486b07528)


---

## 7. Jawaban Pertanyaan

1. Pertanyaan 1 : Apa fungsi utama ERC20 dalam ekosistem blockchain?
Jawab :
ERC-20 berfungsi sebagai standar teknis untuk pembuatan dan pengelolaan token di jaringan Ethereum. Standar ini memastikan bahwa token memiliki antarmuka fungsi yang sama, sehingga dapat digunakan secara kompatibel dengan wallet, exchange, dan aplikasi terdesentralisasi (dApps) tanpa perlu penyesuaian khusus. Dengan ERC-20, pengembang dapat dengan mudah menciptakan token untuk berbagai kebutuhan seperti donasi, utility token, governance token, dan reward system.

Selain itu, ERC-20 mendukung interoperabilitas dalam ekosistem blockchain. Token yang mengikuti standar ini dapat langsung diperdagangkan di decentralized exchange (DEX), disimpan di MetaMask, dan diintegrasikan ke smart contract lain. Hal ini mempercepat adopsi dan mengurangi kompleksitas pengembangan aplikasi blockchain.

2. Pertanyaan 2 :Bagaimana mekanisme transfer token bekerja dalam kontrak ERC20?
Jawab :
Mekanisme transfer token ERC-20 dijalankan melalui fungsi transfer() dan transferFrom(). Fungsi transfer() digunakan untuk mengirim token langsung dari pemilik token ke alamat lain, dengan syarat saldo pengirim mencukupi. Ketika transfer berhasil, kontrak akan memperbarui saldo kedua alamat dan memicu event Transfer sebagai bukti transaksi di blockchain.

Sementara itu, transferFrom() bekerja bersama mekanisme approve() dan allowance(). Pemilik token terlebih dahulu memberikan izin kepada pihak lain (misalnya smart contract atau dApp) untuk menggunakan sejumlah token tertentu. Pihak yang diberi izin kemudian dapat mentransfer token sesuai batas yang ditentukan. Mekanisme ini sangat penting untuk donasi otomatis, marketplace, dan DeFi, karena memungkinkan interaksi tanpa harus memindahkan kontrol penuh atas token.

3. Pertanyaan 3 :Apa risiko utama dalam implementasi smart contract dan bagaimana cara mitigasinya?
Jawab :
Risiko utama dalam implementasi smart contract ERC-20 meliputi bug kode, kesalahan logika, reentrancy attack, integer overflow/underflow, dan kesalahan kontrol akses. Kesalahan kecil dalam kode dapat menyebabkan hilangnya token secara permanen karena smart contract bersifat immutable setelah dideploy.

Mitigasi risiko dapat dilakukan dengan menggunakan library tepercaya seperti OpenZeppelin, menerapkan audit kode, serta melakukan pengujian menyeluruh di testnet sebelum deploy ke mainnet. Selain itu, penggunaan fitur keamanan modern Solidity seperti checks-effects-interactions pattern, require() untuk validasi, dan pembatasan hak akses (modifier onlyOwner) sangat penting untuk menjaga keamanan kontrak ERC-20.

## 8. Kesimpulan
Berdasarkan hasil pengujian yang telah dilakukan, dapat disimpulkan bahwa Remix IDE berfungsi dengan baik dalam melakukan proses donasi, sedangkan website yang dibangun belum dapat menjalankan fungsi donasi dengan benar.

Pada Remix IDE, transaksi donasi berhasil karena:

1. Nilai ETH (value) dikirim secara eksplisit melalui kolom Value saat memanggil fungsi donate().

2. Kontrak dipanggil secara langsung dengan parameter yang sesuai, sehingga msg.value diterima oleh smart contract.

3. Lingkungan Remix telah terkonfigurasi dengan baik (jaringan Sepolia, akun MetaMask, dan ABI yang sesuai).

Sementara itu, pada website yang dibangun, proses donasi tidak berjalan atau dapat donate karena:

1. Nilai donasi tidak terkirim dengan benar dari frontend ke smart contract.

2. Terjadi kesalahan pada integrasi JavaScript (ethers.js), seperti input nilai yang tidak terbaca, kesalahan konversi ethers.parseEther(), atau script tidak ter-load dengan benar.

3. Validasi jaringan, alamat kontrak, atau ABI belum sepenuhnya sinkron dengan yang digunakan di Remix.

4. Transaksi juga tetap tidak tercatat di blockchain, sehingga fungsi donate() tidak bekerja sebagaimana mestinya.

Dengan demikian, dapat disimpulkan bahwa smart contract tidak bermasalah, namun kendala terdapat pada sisi frontend (website), khususnya pada proses pengiriman nilai ETH dan integrasi dengan MetaMask. Diperlukan perbaikan pada struktur file, pemanggilan fungsi JavaScript, serta validasi input dan jaringan agar website dapat berfungsi sama baiknya seperti Remix IDE.
---


## 9. Daftar Pustaka
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.
- Stallings (2017).
- Stinson (2019).
- https://ethereum.org/en/developers/docs/standards/tokens/erc-20/
- https://docs.openzeppelin.com/contracts/erc20 

---

## 10. Commit Log

```
commit week15-tinycoin-erc20
Author: Ibnu Sahrul Anwar <benuibnuanwar@gmail.com>
Date:   2026-01-24

   week15-tinycoin-erc20: Proyek Kelompok – TinyCoin ERC20
```
