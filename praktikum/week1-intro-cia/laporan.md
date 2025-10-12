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
1. Membuat file `hello_world.py` di folder `praktikum/week1-intro-cia/src/`.
2. Menyalin kode program dari panduan praktikum.
3. Menjalankan program dengan perintah `python hello_world.py`.)

---

## 5. Source Code
# ================================================
# File: hello_world.py
# Program Pengenalan Kriptografi - Caesar Cipher
# ================================================

# Fungsi Enkripsi Caesar Cipher
def caesar_encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            start = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - start + shift) % 26 + start)
        else:
            result += char
    return result

# Fungsi Dekripsi Caesar Cipher
def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)

# ===============================
# Program Utama (Main Program)
# ===============================
print("===========================================")
print("     HELLO WORLD - PROGRAM KRIPTOGRAFI")
print("             CAESAR CIPHER")
print("===========================================")
print("Program ini mengenkripsi dan mendekripsi teks sederhana.")
print("Teknik yang digunakan adalah Caesar Cipher.\n")

# Input dari pengguna
pesan = input("Masukkan pesan (contoh: Hello World): ")
geser = int(input("Masukkan jumlah pergeseran (contoh: 3): "))

# Proses Enkripsi
pesan_terenkripsi = caesar_encrypt(pesan, geser)
print("\n=== HASIL ENKRIPSI ===")
print("Pesan asli       :", pesan)
print("Pesan terenkripsi:", pesan_terenkripsi)

# Proses Dekripsi
pesan_didekripsi = caesar_decrypt(pesan_terenkripsi, geser)
print("\n=== HASIL DEKRIPSI ===")
print("Pesan setelah didekripsi:", pesan_didekripsi)

print("\nTerima kasih! Anda baru saja menjalankan program Hello World versi Kriptografi 🎉")

---

## 6. Hasil dan Pembahasan
(- Lampirkan screenshot hasil eksekusi program (taruh di folder `screenshots/`).  
- Berikan tabel atau ringkasan hasil uji jika diperlukan.
  
- Jelaskan apakah hasil sesuai ekspektasi.
  - Tidak sepenuhnya — karena saat pertama dijalankan Python mengembalikan error file not found → ini tidak sesuai ekspektasi (kita mengharapkan program berjalan).
  - Error kedua (pytho) adalah kesalahan pengetikan, juga tidak sesuai harapan.
  - Setelah memastikan file benar di folder yang aktif (cd src) dan menjalankan python hello_world.py, hasil akan sesuai ekspektasi: program meminta input, menampilkan pesan terenkripsi, lalu mendekripsinya kembali.

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi](C:\Users\LENOVO\OneDrive\画像\Screenshots\Screenshot 2025-10-12 220413.jpg)
![Hasil Input dan Output](C:\Users\LENOVO\OneDrive\画像\Screenshots\Screenshot 2025-10-12 220436.jpg)
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
Hasil pengujian program hello_world.py (Caesar Cipher) menunjukkan bahwa:
- Program berfungsi sesuai ekspektasi setelah dijalankan dari folder yang benar (src) dan menggunakan perintah yang tepat (python hello_world.py).
- Error awal terjadi karena file belum berada di direktori kerja serta adanya typo perintah (pytho), bukan karena kesalahan kode.
- Setelah diperbaiki, program berhasil menampilkan proses enkripsi dan dekripsi teks dengan benar.
Kesimpulan akhir:
Program Caesar Cipher berjalan berhasil dan sesuai tujuan, menunjukkan cara kerja dasar kriptografi klasik melalui pergeseran huruf secara sederhana.

---

## 9. Daftar Pustaka
- Youtube dan AI

---

## 10. Commit Log
```
commit abc12345
Author: Ibnu Sahrul Anwar <benuibnuanwar@gmail.com>
Date:   2025-09-20

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```
