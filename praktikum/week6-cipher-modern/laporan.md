# Laporan Praktikum Kriptografi
Minggu ke-: 6  
Topik: Cipher Modern (DES, AES, RSA)
Nama: Ibnu Sahrul Anwar
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
- Mengimplementasikan algoritma DES untuk blok data sederhana.
- Menerapkan algoritma AES dengan panjang kunci 128 bit.
- Menjelaskan proses pembangkitan kunci publik dan privat pada algoritma RSA.

---

## 2. Dasar Teori
Teori Dasar DES (Data Encryption Standard)
DES adalah algoritma kriptografi simetris yang termasuk ke dalam kategori block cipher, di mana proses enkripsi dan dekripsi menggunakan kunci yang sama. DES menggunakan ukuran blok data 64 bit serta kunci 56 bit yang efektif, dan bekerja melalui 16 ronde komputasi menggunakan struktur Feistel Network. Pada setiap ronde, data dibagi menjadi dua bagian—left dan right—yang kemudian diproses dengan operasi ekspansi, pencampuran kunci (XOR), substitusi melalui S-Box, serta permutasi bit untuk memberikan difusi dan konfusi yang kuat. Meskipun DES menjadi standar enkripsi selama beberapa dekade sejak 1977, ukuran kunci yang pendek membuatnya rentan terhadap serangan brute-force pada era modern. Karena itu, DES kini lebih banyak digunakan sebagai dasar konsep atau digantikan oleh algoritma yang lebih kuat seperti Triple-DES dan AES.

Teori Dasar AES (Advanced Encryption Standard)
AES merupakan algoritma block cipher simetris modern yang dikembangkan sebagai pengganti DES, dan resmi dijadikan standar oleh NIST pada tahun 2001. AES menggunakan ukuran blok tetap sebesar 128 bit dan mendukung ukuran kunci 128, 192, atau 256 bit. Algoritma ini menggunakan struktur Substitution–Permutation Network (SPN) yang terdiri dari beberapa langkah utama, yaitu SubBytes, ShiftRows, MixColumns, dan AddRoundKey, yang dilakukan secara berurutan pada tiap ronde. AES-128 memiliki 10 ronde, AES-192 memiliki 12 ronde, dan AES-256 memiliki 14 ronde. Desain AES sangat efisien baik di perangkat keras maupun perangkat lunak, sekaligus memberikan tingkat keamanan yang tinggi berkat struktur matematis yang kuat dan jauh lebih tahan terhadap serangan kriptografi modern dibanding DES. Karena sifatnya yang cepat dan aman, AES digunakan secara luas dalam keamanan komunikasi, penyimpanan data, VPN, Wi-Fi, hingga TLS/SSL.

Teori Dasar RSA (Rivest–Shamir–Adleman)
RSA adalah algoritma kriptografi asimetris yang menggunakan sepasang kunci berbeda, yaitu kunci publik untuk enkripsi dan kunci privat untuk dekripsi. Keamanan RSA bergantung pada kesulitan memfaktorkan bilangan komposit besar menjadi dua bilangan prima, sebuah masalah matematika yang sangat sulit diselesaikan dalam waktu singkat dengan komputer modern. Dalam pembentukan kunci, RSA memilih dua bilangan prima besar, menghitung nilai modulus n=p×q, dan menentukan eksponen publik serta eksponen privat melalui perhitungan fungsi totien Euler. Proses enkripsi dilakukan dengan operasi eksponensial modular menggunakan kunci publik, sedangkan dekripsi menggunakan kunci privat. RSA banyak digunakan dalam pengamanan kunci (key exchange), digital signature, dan autentikasi, namun tidak efisien untuk mengenkripsi data berukuran besar. Oleh karena itu, RSA biasanya dipadukan dengan algoritma simetris seperti AES dalam skema Hybrid Encryption untuk mendapatkan keamanan dan kecepatan sekaligus.

---

## 3. Alat dan Bahan
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan : pycryptodome

---

## 4. Langkah Percobaan
Langkah Percobaan DES
- Siapkan program Python menggunakan library pycryptodome.
- Buat kunci DES 8 byte (64 bit) menggunakan get_random_bytes(8).
- Masukkan plaintext dan lakukan padding agar sesuai blok 8 byte.
- Lakukan enkripsi menggunakan DES.new(key, DES.MODE_ECB) dan fungsi .encrypt().
- Catat hasil ciphertext yang dihasilkan.
- Lakukan dekripsi menggunakan objek DES baru dengan kunci yang sama.
- Pastikan hasil dekripsi sama dengan plaintext asli.

Langkah Percobaan AES-128 (Singkat)
- Import library AES dan buat kunci 16 byte (128 bit) menggunakan get_random_bytes(16).
- Masukkan plaintext dari pengguna.
- Buat objek AES dengan mode EAX untuk enkripsi sekaligus autentikasi.
- Enkripsikan plaintext menggunakan .encrypt_and_digest() sehingga menghasilkan ciphertext dan tag.
- Simpan nilai nonce, ciphertext, dan tag.
- Dekripsi menggunakan objek AES baru dengan nonce yang sama.
- Verifikasi hasil dekripsi agar cocok dengan plaintext awal.

Langkah Percobaan RSA (Singkat)
- Buat pasangan kunci RSA 2048 bit menggunakan RSA.generate(2048).
- Ekstrak public key dan private key yang dihasilkan.
- Masukkan plaintext yang akan dienkripsi.
- Lakukan enkripsi menggunakan public key melalui PKCS1_OAEP.new(public_key).encrypt().
- Catat ciphertext hasil enkripsi.
- Lakukan dekripsi ciphertext dengan private key menggunakan .decrypt().
- Cocokkan hasil dekripsi dengan plaintext awal untuk memastikan keberhasilan percobaan.
---

## 5. Source Code
Implementasi DES
from Crypto.Cipher import DES
from Crypto.Util.Padding import pad, unpad
from Crypto.Random import get_random_bytes

# ------------------------------------------------------
# 1. Membuat kunci DES sepanjang 8 byte (64 bit)
# ------------------------------------------------------
key = get_random_bytes(8)
print("Kunci (hex):", key.hex())

# ------------------------------------------------------
# 2. Input plaintext dari pengguna
# ------------------------------------------------------
plaintext = input("Masukkan plaintext: ").encode()

# ------------------------------------------------------
# 3. Enkripsi DES (MODE ECB)
#    DES hanya menerima blok 8 byte, jadi perlu padding
# ------------------------------------------------------
cipher = DES.new(key, DES.MODE_ECB)
padded_text = pad(plaintext, 8)  # padding ke kelipatan 8 byte

ciphertext = cipher.encrypt(padded_text)
print("Ciphertext (hex):", ciphertext.hex())

# ------------------------------------------------------
# 4. Dekripsi DES
# ------------------------------------------------------
decipher = DES.new(key, DES.MODE_ECB)
decrypted_padded = decipher.decrypt(ciphertext)

# Hilangkan padding
decrypted = unpad(decrypted_padded, 8)

print("Hasil Dekripsi :", decrypted.decode())

Implementasi AES
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

# ------------------------------------------------------
# 1. Membuat kunci AES 128-bit (16 byte)
# ------------------------------------------------------
key = get_random_bytes(16)
print("Kunci (hex):", key.hex())

# ------------------------------------------------------
# 2. Input plaintext dari user
# ------------------------------------------------------
plaintext = input("Masukkan plaintext: ").encode()

# ------------------------------------------------------
# 3. Enkripsi AES MODE EAX (mendukung autentikasi data)
# ------------------------------------------------------
cipher = AES.new(key, AES.MODE_EAX)
ciphertext, tag = cipher.encrypt_and_digest(plaintext)

print("\n=== HASIL ENKRIPSI ===")
print("Nonce      (hex):", cipher.nonce.hex())
print("Ciphertext (hex):", ciphertext.hex())
print("Tag        (hex):", tag.hex())

# ------------------------------------------------------
# 4. Dekripsi AES
# ------------------------------------------------------
cipher_dec = AES.new(key, AES.MODE_EAX, nonce=cipher.nonce)
decrypted = cipher_dec.decrypt_and_verify(ciphertext, tag)

print("\n=== HASIL DEKRIPSI ===")
print("Plaintext:", decrypted.decode())

Implementasi RSA
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

# ------------------------------------------------------
# 1. Generate key RSA 2048 bit
# ------------------------------------------------------
key = RSA.generate(2048)
private_key = key
public_key = key.publickey()

print("=== PUBLIC KEY (PEM) ===")
print(public_key.export_key().decode())

print("=== PRIVATE KEY (PEM) ===")
print(private_key.export_key().decode())

# ------------------------------------------------------
# 2. Input plaintext dari user
# ------------------------------------------------------
plaintext = input("Masukkan plaintext: ").encode()

# ------------------------------------------------------
# 3. Enkripsi menggunakan PUBLIC KEY
# ------------------------------------------------------
cipher_rsa = PKCS1_OAEP.new(public_key)
ciphertext = cipher_rsa.encrypt(plaintext)

print("\nCiphertext (hex):", ciphertext.hex())

# ------------------------------------------------------
# 4. Dekripsi menggunakan PRIVATE KEY
# ------------------------------------------------------
decipher_rsa = PKCS1_OAEP.new(private_key)
decrypted = decipher_rsa.decrypt(ciphertext)

print("Hasil Dekripsi:", decrypted.decode())


---

## 6. Hasil dan Pembahasan
Percobaan DES menunjukkan bahwa proses enkripsi dan dekripsi berjalan dengan benar selama menggunakan kunci yang sama, namun algoritma ini kurang aman karena ukuran kuncinya kecil. Pada percobaan AES-128, ciphertext dan tag autentikasi berhasil dihasilkan dan dapat didekripsi kembali dengan benar menggunakan kunci serta nonce yang sama, sehingga membuktikan bahwa AES lebih aman dan efisien. Percobaan RSA memperlihatkan bahwa enkripsi hanya dapat dilakukan dengan public key dan dekripsi dengan private key, serta plaintext dapat dipulihkan kembali secara tepat. Secara keseluruhan, AES memberikan keamanan dan performa terbaik, RSA cocok untuk pertukaran kunci, sedangkan DES kurang direkomendasikan untuk penggunaan modern.

Hasil eksekusi program Caesar Cipher:
Implementasi DES<img width="1920" height="1080" alt="Screenshot 2025-11-14 222352" src="https://github.com/user-attachments/assets/36096702-27fe-46b2-aae7-e9fcf8e27359" />

Implementasi AES<img width="1920" height="1080" alt="Screenshot 2025-11-14 222914" src="https://github.com/user-attachments/assets/429ccd6a-a546-4ac6-920c-5cdbc9fb5ff0" />

Implementasi RSA<img width="1920" height="1080" alt="Screenshot 2025-11-14 223145" src="https://github.com/user-attachments/assets/808ff590-5912-4759-97be-e248ebbad8f3" />


---

## 7. Jawaban Pertanyaan
1) Apa perbedaan mendasar antara DES, AES, dan RSA dalam hal kunci dan keamanan?
   Jawab:
   DES & AES: sama-sama simetris (1 kunci untuk enkripsi dan dekripsi).
   DES: kunci pendek (56 bit) = tidak aman.
   AES: kunci lebih panjang (128–256 bit) = sangat aman.
   RSA: asimetris (public key & private key), aman tetapi tidak cocok untuk data besar.
2) Mengapa AES lebih banyak digunakan dibanding DES di era modern?
   Jawab: Karena AES punya kunci lebih panjang, jauh lebih aman, lebih cepat, dan tidak rentan brute-force seperti DES.
3) Mengapa RSA dikategorikan sebagai algoritma asimetris, dan bagaimana proses pembangkitan kuncinya?
   Jawab:
   RSA asimetris karena memakai dua kunci berbeda: public untuk enkripsi dan private untuk dekripsi. Kuncinya dibuat dengan
   memilih dua bilangan prima besar, menghitung modulus n=p×q, lalu menghasilkan pasangan (public key, private key).

---

## 8. Kesimpulan

Percobaan menunjukkan bahwa DES, AES, dan RSA memiliki mekanisme dan tingkat keamanan yang berbeda. DES terbukti tidak lagi aman karena ukuran kuncinya terlalu pendek, sementara AES jauh lebih kuat, cepat, dan cocok untuk kebutuhan keamanan modern. RSA bekerja sebagai algoritma asimetris yang efektif untuk enkripsi kunci dan autentikasi, tetapi kurang efisien untuk data besar. Secara keseluruhan, AES adalah pilihan utama untuk enkripsi data, dan RSA digunakan sebagai pendukung dalam sistem keamanan yang memerlukan pertukaran kunci atau digital signature.
---

## 9. Daftar Pustaka
- Stallings, W. (2017). Cryptography and Network Security: Principles and Practice (7th ed.). Pearson.

---

