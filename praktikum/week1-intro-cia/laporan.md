# Laporan Praktikum Kriptografi
Minggu ke-: 1  
Topik: Sejarah Kriptografi dan Prinsip CIA  
Nama: Ibnu Sahrul Anwar  
NIM: 230202811  
Kelas: 5IKKA  

---

## 1. Tujuan
1. Menjelaskan sejarah dan evolusi kriptografi dari masa klasik hingga modern.
2. Menyebutkan prinsip Confidentiality, Integrity, Availability (CIA) dengan benar.
3. Menyimpulkan peran kriptografi dalam sistem keamanan informasi modern
4. Menyiapkan repositori GitHub sebagai media kerja praktikum.

---

## 2. Dasar Teori
**Sejarah Kriptografi**
Kriptografi adalah ilmu yang digunakan untuk menjaga kerahasiaan informasi. Pada era klasik, metode enkripsi masih sederhana, seperti Caesar Cipher yang mengganti huruf dengan pergeseran alfabet, dan Vigenère Cipher yang memakai kunci berupa kata. Meski efektif pada masanya, metode ini mudah dipecahkan. Memasuki era modern, muncul algoritma yang lebih kuat seperti RSA yang berbasis kunci publik dan AES yang menggunakan enkripsi simetris. Keduanya banyak dipakai pada transaksi online, komunikasi aman, dan sistem keamanan jaringan. Kini, kriptografi berkembang lebih jauh melalui teknologi blockchain dan cryptocurrency, seperti Bitcoin, yang mengandalkan hash dan tanda tangan digital untuk menjaga integritas serta kepercayaan data secara terdistribusi.

**Prinsip CIA**
Keamanan informasi bertumpu pada tiga pilar utama yang dikenal sebagai CIA Triad. Pertama, Confidentiality atau kerahasiaan, memastikan data hanya dapat diakses oleh pihak berwenang. Sebagai contoh, password disimpan dalam bentuk hash terenkripsi sehingga tidak bisa dibaca langsung. Kedua, Integrity atau integritas, menjamin bahwa data tidak diubah secara tidak sah, misalnya melalui verifikasi checksum saat mengunduh aplikasi. Ketiga, Availability atau ketersediaan, memastikan data dan layanan selalu dapat digunakan. Sebagai contoh, bank menyediakan server cadangan agar layanan mobile banking tetap berfungsi meskipun terjadi gangguan sistem.

---

## 3. Alat dan Bahan
(- Python 3.x  
- Visual Studio Code
- Git dan akun GitHub  
---

## 4. Langkah Percobaan
1. Membuat file `caesar_cipher.py` di folder `praktikum/week2-cryptosystem/src/`.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah `python caesar_cipher.py`.)

---

## 5. Source Code
(Salin kode program utama yang dibuat atau dimodifikasi.  
Gunakan blok kode:

```python
# contoh potongan kode
def encrypt(text, key):
    return ...
```
)

---

## 6. Hasil dan Pembahasan
(- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.  
- Jelaskan apakah hasil sesuai ekspektasi.  
- Bahas error (jika ada) dan solusinya. 

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi](screenshots/output.png)
![Hasil Input](screenshots/input.png)
![Hasil Output](screenshots/output.png)
)

---

## 7. Jawaban Pertanyaan
1.	Tokoh yang dianggap sebagai bapak kriptografi modern
    Claude Shannon. Ia dikenal sebagai "Bapak Teori Informasi" dan salah satu pendiri kriptografi modern melalui karyanya        Communication Theory of Secrecy Systems (1949), yang memberikan dasar matematis bagi keamanan enkripsi.
2.	Algoritma kunci publik yang populer digunakan saat ini
    - RSA (Rivest–Shamir–Adleman)
    - ECC (Elliptic Curve Cryptography)
    - DSA (Digital Signature Algorithm, sering dipakai untuk tanda tangan digital)
3.	Perbedaan utama antara kriptografi klasik dan modern
	Kriptografi klasik: 
	- Menggunakan operasi sederhana (pergeseran huruf, substitusi, transposisi).
	- Umumnya berbasis teks alfabet.
	- Mudah dipecahkan dengan analisis frekuensi.
	Kriptografi modern:
	- Berbasis matematika kompleks (teori bilangan, logaritma diskrit, kurva eliptik).
	- Beroperasi pada data biner (bit/byte).
	- Dirancang untuk keamanan tinggi di dunia digital (internet, transaksi online).

---

## 8. Kesimpulan
(Tuliskan kesimpulan singkat (2–3 kalimat) berdasarkan percobaan.  )

---

## 9. Daftar Pustaka
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.  )

---

## 10. Commit Log
```
commit abc12345
Author: Ibnu Sahrul Anwar <benuibnuanwar@gmail.com>
Date:   2025-09-20

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```
