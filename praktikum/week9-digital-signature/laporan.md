# Laporan Praktikum Kriptografi
Minggu ke-: 09  
Topik: Digital Signature
Nama: Ibnu Sahrul Anwar
NIM: 230202811  
Kelas: 5IKKA

---

## 1. Tujuan
1. Mengimplementasikan tanda tangan digital menggunakan algoritma RSA/DSA.
2. Memverifikasi keaslian tanda tangan digital.
3. Menjelaskan manfaat tanda tangan digital dalam otentikasi pesan dan integritas data.

---

## 2. Dasar Teori
Tanda tangan digital adalah mekanisme kriptografi yang digunakan untuk
menjamin bahwa suatu pesan:
- Benar berasal dari pengirim yang sah (otentikasi),
- Tidak mengalami perubahan selama pengiriman (integritas),
- Tidak dapat disangkal oleh pengirim (non-repudiation).

Pada RSA digital signature:
- Pengirim menandatangani hash pesan menggunakan **private key**.
- Penerima memverifikasi tanda tangan menggunakan **public key** pengirim.

---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code
- Git dan akun GitHub  
- Library: pip install pycryptodome

---

## 4. Langkah Percobaan
Program dibuat menggunakan bahasa Python dan library `pycryptodome`.
Langkah utama program:
1. Generate pasangan kunci RSA (private key dan public key).
2. Membuat hash pesan menggunakan SHA-256.
3. Membuat tanda tangan digital menggunakan private key.
4. Memverifikasi tanda tangan menggunakan public key.
5. Menguji kegagalan verifikasi pada pesan yang telah dimodifikasi.
---

## 5. Source Code
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import hashes
from cryptography.exceptions import InvalidSignature

print("Program Digital Signature dijalankan...")

private_key = rsa.generate_private_key(
    public_exponent=65537,
    key_size=2048
)

public_key = private_key.public_key()

message = b"Ini adalah pesan rahasia"

signature = private_key.sign(
    message,
    padding.PSS(
        mgf=padding.MGF1(hashes.SHA256()),
        salt_length=padding.PSS.MAX_LENGTH
    ),
    hashes.SHA256()
)

print("Signature berhasil dibuat")

try:
    public_key.verify(
        signature,
        message,
        padding.PSS(
            mgf=padding.MGF1(hashes.SHA256()),
            salt_length=padding.PSS.MAX_LENGTH
        ),
        hashes.SHA256()
    )
    print("Signature VALID ✅")
except InvalidSignature:
    print("Signature TIDAK VALID ❌")


---

## 6. Hasil dan Pembahasan
### 4.1 Verifikasi Pesan Asli
Pesan asli berhasil diverifikasi menggunakan public key.
Hal ini menunjukkan bahwa tanda tangan digital valid dan pesan tidak
mengalami perubahan.

### 4.2 Verifikasi Pesan Modifikasi
Ketika pesan diubah, proses verifikasi gagal.
Hal ini membuktikan bahwa tanda tangan digital mampu mendeteksi perubahan
data dan menjamin integritas pesan.

Hasil eksekusi program RSA/DSA:
<img width="1920" height="1080" alt="Screenshot 2025-12-25 213538" src="https://github.com/user-attachments/assets/0b67ab6d-ed2f-4052-a627-c433650ba444" />

---

## 7. Jawaban Pertanyaan
### 1. Apa perbedaan utama antara enkripsi RSA dan tanda tangan digital RSA?
Enkripsi RSA bertujuan menjaga kerahasiaan pesan dengan mengenkripsi pesan
menggunakan public key penerima.  
Sedangkan tanda tangan digital RSA bertujuan menjamin keaslian dan integritas
pesan dengan menandatangani hash pesan menggunakan private key pengirim.

### 2. Mengapa tanda tangan digital menjamin integritas dan otentikasi pesan?
Karena tanda tangan digital dibuat dari hash pesan. Jika pesan diubah,
nilai hash akan berubah sehingga verifikasi tanda tangan gagal.
Penggunaan private key juga memastikan bahwa hanya pengirim sah yang dapat
membuat tanda tangan tersebut.

### 3. Bagaimana peran Certificate Authority (CA) dalam sistem tanda tangan digital modern?
Certificate Authority berperan sebagai pihak terpercaya yang mengeluarkan
sertifikat digital untuk mengaitkan identitas pengguna dengan public key.
Hal ini mencegah pemalsuan identitas dalam sistem tanda tangan digital.
---

## 8. Kesimpulan
Tanda tangan digital RSA merupakan metode yang efektif untuk menjamin
keaslian dan integritas pesan. Melalui praktikum ini, terbukti bahwa
perubahan sekecil apa pun pada pesan akan menyebabkan verifikasi tanda
tangan gagal.

---

## 9. Daftar Pustaka
- Stinson, D. R., & Paterson, M. B. (2019). Cryptography: Theory and Practice. CRC Press.  
- Menezes, A. J., et al. (2018). Handbook of Applied Cryptography. CRC Press.  
- PyCryptodome Documentation. Public Key Cryptography and Digital Signatures.

---
