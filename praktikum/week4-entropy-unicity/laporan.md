# Laporan Praktikum Kriptografi
Minggu ke-: 4 
Topik: Entropy & Unicity Distance (Evaluasi Kekuatan Kunci dan Brute Force) 
Nama: Ibnu Sahrul Anwar
NIM: 230202811  
Kelas: 5IKKA  

---

## 1. Tujuan
- Menyelesaikan perhitungan sederhana terkait entropi kunci.
- Menggunakan teorema Euler pada contoh perhitungan modular & invers.
- Menghitung unicity distance untuk ciphertext tertentu.
- Menganalisis kekuatan kunci berdasarkan entropi dan unicity distance.
- Mengevaluasi potensi serangan brute force pada kriptosistem sederhana.

---

## 2. Dasar Teori
Entropy (Entropi) dalam kriptografi adalah ukuran tingkat ketidakpastian atau jumlah informasi dalam ruang kunci suatu sistem enkripsi. Semakin besar entropi (dalam satuan bit), semakin sulit bagi penyerang untuk menebak kunci yang benar. Entropi dihitung menggunakan rumus H(K)=log2∣K∣, di mana ∣K∣ adalah jumlah kemungkinan kunci.

Unicity Distance adalah ukuran minimum panjang ciphertext yang dibutuhkan agar pesan dapat dipecahkan secara unik tanpa ambiguitas, berdasarkan redundansi bahasa. Rumusnya U=H(K)/R⋅log⁡2∣A∣, di mana R adalah redundansi bahasa dan ∣A∣ adalah ukuran alfabet. Semakin besar nilai unicity distance, semakin sulit cipher dipecahkan dengan analisis statistik.

Keduanya digunakan untuk mengevaluasi kekuatan kunci dan ketahanan terhadap brute force, di mana sistem dengan entropi tinggi dan unicity distance besar dianggap lebih aman dari serangan.

---

## 3. Alat dan Bahan
- Visual Studio Code / editor lain  
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
- Membuat file entropy_unicity.py di folder C:\Users\LENOVO\source\repos\ibnusahrulanwar\kriptografi-202501-230202811\praktikum\week4-entropy-unicity
- Menyalin kode program Entropy, Unicity Distance, dan Brute Force dari panduan praktikum.
- Menyimpan file dan memastikan tidak ada error sintaks.
- Menjalankan program melalui terminal dengan perintah: python entropy_unicity.py
- Memasukkan nilai input sesuai instruksi (ukuran ruang kunci, redundansi bahasa, ukuran alfabet, dan kecepatan brute force).
- Menganalisis hasil keluaran yang menunjukkan nilai entropi, unicity distance, dan estimasi waktu brute force.
- 
---

## 5. Source Code
# entropy_unicity.py
# Program menghitung Entropi, Unicity Distance, dan waktu Brute Force dengan input dari user

import math

# --- Fungsi 1: Perhitungan Entropi ---
def entropy(keyspace_size):
    """Menghitung entropi (dalam bit) dari ruang kunci."""
    return math.log2(keyspace_size)

# --- Fungsi 2: Menghitung Unicity Distance ---
def unicity_distance(HK, R=0.75, A=26):
    """Menghitung unicity distance (jarak keunikan)."""
    return HK / (R * math.log2(A))

# --- Fungsi 3: Analisis Brute Force ---
def brute_force_time(keyspace_size, attempts_per_second=1e6):
    """Mengestimasi waktu brute force dalam hari."""
    seconds = keyspace_size / attempts_per_second
    days = seconds / (3600 * 24)
    return days

# --- Input dari user ---
print("=== Analisis Keamanan Kriptografi ===")
keyspace = int(input("Masukkan ukuran ruang kunci (|K|): "))
redundancy = float(input("Masukkan nilai redundansi bahasa (misal 0.75 untuk bahasa Inggris): "))
alphabet_size = int(input("Masukkan ukuran alfabet (misal 26 untuk A–Z): "))
speed = float(input("Masukkan kecepatan brute force (percobaan per detik): "))

# --- Perhitungan ---
HK = entropy(keyspace)
U = unicity_distance(HK, redundancy, alphabet_size)
T = brute_force_time(keyspace, speed)

# --- Output hasil ---
print("\n=== HASIL PERHITUNGAN ===")
print(f"Entropi H(K) = {HK:.4f} bit")
print(f"Unicity Distance U = {U:.4f}")
print(f"Estimasi waktu brute force = {T:.6f} hari")

# --- Contoh perbandingan ---
print("\n=== Contoh Perbandingan ===")
print(f"Entropy ruang kunci 26 = {entropy(26):.2f} bit")
print(f"Entropy ruang kunci 2^128 = {entropy(2**128):.2f} bit")

---

## 6. Hasil dan Pembahasan
Hasil percobaan menunjukkan bahwa semakin besar ukuran ruang kunci, nilai entropi yang dihasilkan juga semakin tinggi, menandakan sistem enkripsi tersebut semakin sulit ditebak secara brute force. Nilai unicity distance menunjukkan seberapa panjang ciphertext yang diperlukan agar kunci dapat diidentifikasi secara unik; semakin besar nilainya, semakin kuat cipher terhadap analisis statistik. Pada uji coba, algoritma sederhana seperti Caesar Cipher memiliki entropi rendah dan dapat dipecahkan dalam waktu sangat singkat, sedangkan algoritma modern seperti AES-128 memiliki entropi tinggi dan waktu brute force yang tidak realistis untuk ditembus, sehingga jauh lebih aman.
Hasil Screenshots:<img width="1920" height="1080" alt="Screenshot 2025-10-27 220214" src="https://github.com/user-attachments/assets/53fc9908-2181-4b7c-861d-ec0b40165705" />

---

## 7. Jawaban Pertanyaan
(Jawab pertanyaan diskusi yang diberikan pada modul.  
- Pertanyaan 1: Arti nilai entropy dalam konteks kekuatan kunci:
Jawab: Nilai entropy menunjukkan seberapa besar tingkat ketidakpastian atau banyaknya kemungkinan kunci yang harus ditebak oleh penyerang. Semakin tinggi nilai entropi (dalam bit), semakin besar ruang kunci dan semakin sulit kunci ditebak secara acak. Dengan kata lain, entropi yang tinggi berarti sistem memiliki kekuatan kriptografi yang lebih baik karena peluang keberhasilan brute force menjadi sangat kecil.
- Pertanyaan 2: Pentingnya unicity distance dalam keamanan cipher:
Jawab : Unicity distance menunjukkan panjang minimum ciphertext yang dibutuhkan agar kunci dapat diidentifikasi secara unik melalui analisis statistik. Jika ciphertext yang tersedia lebih pendek dari unicity distance, maka banyak kunci masih mungkin cocok, sehingga cipher tetap aman. Nilai unicity distance yang tinggi berarti cipher lebih tahan terhadap analisis frekuensi dan serangan berbasis teks, terutama untuk bahasa yang memiliki pola berulang.
- Pertanyaan 3: Mengapa brute force masih menjadi ancaman meskipun algoritma sudah kuat:
Jawab : Meskipun algoritma modern seperti AES dirancang sangat aman, brute force tetap menjadi ancaman potensial karena perkembangan teknologi komputasi, seperti penggunaan GPU, superkomputer, dan bahkan komputasi kuantum di masa depan. Selain itu, banyak sistem yang lemah bukan karena algoritmanya, tetapi karena kunci yang pendek, pengelolaan yang buruk, atau implementasi yang tidak aman, sehingga brute force atau serangan serupa masih mungkin berhasil.
)
---

## 8. Kesimpulan
Dapat disimpulkan bahwa nilai entropi dan unicity distance merupakan indikator penting dalam menilai kekuatan sebuah sistem kriptografi. Entropi yang tinggi menunjukkan ruang kunci yang luas dan sulit ditebak, sedangkan unicity distance yang besar menandakan cipher lebih tahan terhadap analisis statistik. Meskipun algoritma modern sangat kuat, ancaman brute force tetap perlu diwaspadai jika kunci atau implementasinya tidak dikelola dengan baik.

---

## 9. Daftar Pustaka
- Stallings, W. (2017). _Cryptography and Network Security: Principles and Practice_ (7th ed.). Pearson Education.
- Paar, C., & Pelzl, J. (2010)._ Understanding Cryptography: A Textbook for Students and Practitioners. Springer.

---
