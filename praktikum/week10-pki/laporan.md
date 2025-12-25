# Laporan Praktikum Kriptografi
Minggu ke-: 10
Topik: PKI & Cerificate Authority 
Nama: Ibnu Sahrul Anwar
NIM: 230202811
Kelas: 5IKKA 

---

## 1. Tujuan
1. Membuat sertifikat digital sederhana.
2. Menjelaskan peran Certificate Authority (CA) dalam sistem PKI.
3. Mengevaluasi fungsi PKI dalam komunikasi aman (contoh: HTTPS, TLS).

---

## 2. Dasar Teori
Public Key Infrastructure (PKI) adalah sistem yang digunakan untuk
mengelola kunci publik dan sertifikat digital. PKI memungkinkan pihak
yang tidak saling mengenal untuk berkomunikasi secara aman melalui
sertifikat digital yang dikeluarkan oleh pihak terpercaya.

Certificate Authority (CA) adalah entitas terpercaya yang bertugas:
- Memverifikasi identitas pemilik sertifikat
- Menerbitkan sertifikat digital
- Menjamin keaslian public key yang digunakan

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library: pip install cryptography pyopenssl


---

## 4. Langkah Percobaan
Program dibuat menggunakan bahasa Python dan library `cryptography`.
Langkah utama implementasi:
1. Membuat pasangan kunci RSA.
2. Membuat sertifikat digital self-signed.
3. Menyimpan sertifikat dalam format `.pem`.
4. Menampilkan informasi sertifikat yang dihasilkan.

Sertifikat self-signed digunakan untuk simulasi konsep CA sederhana.

---

## 5. Source Code
from Crypto.PublicKey import RSA
from Crypto.Signature import pkcs1_15
from Crypto.Hash import SHA256

print("=== SIMULASI PKI SEDERHANA ===\n")

# ===============================
# 1. CA membuat pasangan kunci
# ===============================
ca_key = RSA.generate(2048)
ca_private = ca_key
ca_public = ca_key.publickey()

print("CA: pasangan kunci dibuat")

# ===============================
# 2. User membuat pasangan kunci
# ===============================
user_key = RSA.generate(2048)
user_private = user_key
user_public = user_key.publickey()

print("User: pasangan kunci dibuat")

# ===============================
# 3. CA membuat sertifikat user
# ===============================
certificate_data = user_public.export_key()
hash_cert = SHA256.new(certificate_data)

certificate_signature = pkcs1_15.new(ca_private).sign(hash_cert)

print("\nCA: sertifikat user ditandatangani")

# ===============================
# 4. Verifikasi sertifikat user
# ===============================
try:
    pkcs1_15.new(ca_public).verify(hash_cert, certificate_signature)
    print("Verifikasi sertifikat: BERHASIL (VALID)")
except (ValueError, TypeError):
    print("Verifikasi sertifikat: GAGAL")

# ===============================
# 5. Simulasi sertifikat palsu
# ===============================
fake_key = RSA.generate(2048)
fake_cert_data = fake_key.publickey().export_key()
fake_hash = SHA256.new(fake_cert_data)

print("\nUji sertifikat palsu")

try:
    pkcs1_15.new(ca_public).verify(fake_hash, certificate_signature)
    print("Verifikasi sertifikat palsu: BERHASIL (SEHARUSNYA GAGAL)")
except (ValueError, TypeError):
    print("Verifikasi sertifikat palsu: GAGAL (TIDAK VALID)")


---

## 6. Hasil dan Pembahasan
Program berhasil menghasilkan:
- Private key dalam file `private_key.pem`
- Sertifikat digital dalam file `cert.pem`

Sertifikat berisi informasi identitas pemilik, public key, masa berlaku,
dan tanda tangan digital.

Hasil eksekusi program pki:
<img width="1920" height="1080" alt="Screenshot 2025-12-25 215828" src="https://github.com/user-attachments/assets/ee725012-f1e7-4964-82aa-3d914ee1f8b9" />

---

## 7. Jawaban Pertanyaan
### 1. Apa fungsi utama Certificate Authority (CA)?
CA berfungsi sebagai pihak terpercaya yang menerbitkan dan menandatangani
sertifikat digital untuk mengaitkan identitas pengguna dengan public key.

### 2. Mengapa self-signed certificate tidak cukup untuk sistem produksi?
Karena sertifikat self-signed tidak diverifikasi oleh pihak terpercaya,
sehingga rentan terhadap serangan pemalsuan identitas.

### 3. Bagaimana PKI mencegah serangan MITM dalam komunikasi TLS/HTTPS?
PKI memastikan bahwa public key server diverifikasi oleh CA terpercaya.
Browser akan menolak koneksi jika sertifikat tidak valid, sehingga
mencegah penyerang melakukan penyadapan atau manipulasi data.

---

## 8. Kesimpulan
PKI dan Certificate Authority merupakan komponen penting dalam sistem
keamanan modern. Melalui praktikum ini, dapat dipahami bahwa sertifikat
digital berperan besar dalam menjamin keaslian identitas dan keamanan
komunikasi data.

---

## 9. Daftar Pustaka
- Stallings, W. (2017). Cryptography and Network Security: Principles and Practice.
- Pearson Education.

---
