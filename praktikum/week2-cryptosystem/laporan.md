# Laporan Praktikum Kriptografi
Minggu ke-: 2  
Topik: Cryptosystem (Komponen, Enkripsi & Dekripsi, Simetris & Asimetris) 
Nama: Ibnu Sahrul Anwar
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
Setelah mengikuti praktikum ini, mahasiswa diharapkan mampu:  
1. Mengidentifikasi komponen dasar kriptosistem (plaintext, ciphertext, kunci, algoritma).  
2. Menggambarkan proses enkripsi dan dekripsi sederhana.  
3. Mengklasifikasikan jenis kriptosistem (simetris dan asimetris).  

---

## 2. Dasar Teori
Dasar Teori Kriptosistem
Kriptografi adalah teknik untuk menjaga kerahasiaan informasi dengan mengubah data asli (plaintext) menjadi bentuk terenkripsi (ciphertext) menggunakan algoritma dan kunci tertentu.
1.	Cipher Klasik
Cipher klasik menggunakan manipulasi huruf secara sederhana.
Contohnya Caesar Cipher, yang menggeser setiap huruf sejauh nilai tertentu (key).
Rumus dasarnya:
C = (P+K) mod 26
P = (C+P) mod 26
2.	Konsep Modular Aritmetika
Digunakan untuk membatasi hasil pergeseran huruf agar tetap dalam rentang alfabet.
Contoh: (25 + 3) mod 26 = 2, sehingga huruf setelah Z kembali ke A.
3.	Enkripsi dan Dekripsi
Enkripsi: mengubah plaintext menjadi ciphertext.
Dekripsi: mengembalikan ciphertext menjadi plaintext.
4.	Jenis Kriptosistem
Simetris = Menggunakan satu kunci yang sama untuk enkripsi dan dekripsi. Cepat, tapi distribusi kunci berisiko. contoh: AES, DES
Asimetris = Menggunakan dua kunci berbeda (publik dan privat). Lebih aman untuk distribusi kunci, tetapi lebih lambat. contoh RSA, ECC
---

## 3. Alat dan Bahan
(- Python 3.x  
- Visual Studio Code
- Git dan akun GitHub  
- Draw.io

---

## 4. Langkah Percobaan
1. Membuat Diagram Skema Kriptosistem
2. Membuat file `caesar_cipher.py` di folder `praktikum/week2-cryptosystem/src/`.
3. Menyalin kode program dari panduan praktikum.
4. Menjalankan program dengan perintah `python caesar_cipher.py`.)

---

## 5. Source Code

```
# ================================================
# File   : praktikum/week2-cryptosystem/src/simple_crypto.py
# Program: Caesar Cipher (Simple Cryptosystem)
# Tujuan : Mengenal konsep dasar enkripsi dan dekripsi teks
# Metode : Pergeseran huruf sederhana (Caesar Cipher)
# ================================================

def encrypt(plaintext, key):
    """Fungsi untuk mengenkripsi teks menggunakan Caesar Cipher"""
    result = ""
    for char in plaintext:
        if char.isalpha():  # Jika karakter huruf
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift + key) % 26 + shift)
        else:
            result += char  # Karakter selain huruf tidak diubah
    return result


def decrypt(ciphertext, key):
    """Fungsi untuk mendekripsi teks yang telah dienkripsi"""
    result = ""
    for char in ciphertext:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift - key) % 26 + shift)
        else:
            result += char
    return result


# ===============================================
# Program Utama (Main Program)
# ===============================================
if __name__ == "__main__":
    print("===========================================")
    print("   PROGRAM KRIPTOGRAFI SEDERHANA (CAESAR CIPHER)")
    print("===========================================\n")

    # Data uji (bisa kamu ubah nanti)
    message = "Ibnu Sahrul Anwar 230202811"
    key = 3

    # Proses Enkripsi
    encrypted = encrypt(message, key)
    decrypted = decrypt(encrypted, key)

    # Hasil
    print("Plaintext :", message)
    print("Ciphertext:", encrypted)
    print("Decrypted :", decrypted)

    print("\nTerima kasih! Anda telah mempelajari dasar kriptografi klasik.")
```

---

## 6. Hasil dan Pembahasan
Kriptografi : mengubah plaintext menjadi ciphertext menggunakan algoritma dan kunci.
Caesar Cipher: pergeseran huruf: C = (P + K) mod 26, P = (C - K) mod 26.
(Aplikasinya pada program src/simple_crypto.py.)
Berikut tabel atau ringkasan hasil uji
[Tabel 2.docx](https://github.com/user-attachments/files/22905727/Tabel.2.docx)
Apakah Hasil Sesuai Ekspektasi?
Ya — program melakukan enkripsi dan dekripsi sesuai rumus Caesar Cipher:
Huruf besar/kecil dipertahankan.
Pergeseran berulang menggunakan modular 26 (setelah Z kembali ke A).
Karakter non-alfabet (spasi, angka, tanda baca) tidak berubah.
Semua pengujian di atas menghasilkan ciphertext yang dapat didekripsi kembali ke plaintext asli menggunakan kunci yang sama → memenuhi ekspektasi kriptosistem simetris sederhana.

Hasil eksekusi program Caesar Cipher:

![Hasil Eksekusi]<img width="1920" height="1080" alt="Screenshot 2025-10-14 192315" src="https://github.com/user-attachments/assets/397e1c0d-a571-4b0d-8572-7c807faed086" />

![Hasil Input & Output]<img width="1920" height="1080" alt="Screenshot 2025-10-14 192259" src="https://github.com/user-attachments/assets/795368b2-bf4d-41b6-ba3d-778b519d7a27" />


)

---

## 7. Jawaban Pertanyaan
1. Sebutkan komponen utama dalam sebuah kriptosistem.
   Jawab : Plaintext, Ciphertext, Kunci, dan Algoritma.
2. Apa kelebihan dan kelemahan sistem simetris dibandingkan asimetris?
   Jawab : - Kelebihan: proses enkripsi dan dekripsi lebih cepat.
           - Kelemahan: distribusi kunci sulit karena kunci harus dibagikan secara rahasia.
3. Mengapa distribusi kunci menjadi masalah utama dalam kriptografi simetris?
   Jawab: Karena jika kunci berhasil disadap pihak lain, maka seluruh pesan dapat dibuka. Oleh karena itu, pengiriman kunci harus sangat aman.
---

## 8. Kesimpulan
Program simple_crypto.py berhasil menjalankan proses enkripsi dan dekripsi menggunakan algoritma Caesar Cipher dengan benar. Hasil uji menunjukkan ciphertext dapat dikembalikan ke plaintext asli menggunakan kunci yang sama. Tidak ditemukan error pada logika program; kendala yang muncul hanya terkait lokasi file atau versi Python, dan dapat diatasi dengan mudah. Program berjalan sesuai ekspektasi sebagai contoh dasar kriptosistem klasik.

---

## 9. Daftar Pustaka
Modul dan Youtube

---

## 10. Commit Log
```
commit abc12345
Author: Nama Mahasiswa <email>
Date:   2025-09-20

    week2-cryptosystem: implementasi Caesar Cipher dan laporan )
```
