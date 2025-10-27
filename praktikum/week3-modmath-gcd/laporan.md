# Laporan Praktikum Kriptografi
Minggu ke-: 3
Topik: [Modular Math (Aritmetika Modular, GCD, Bilangan Prima, Logaritma Diskrit)]  
Nama: Ibnu Sahrul Anwar 
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
1. Menyelesaikan operasi aritmetika modular.
2. Menentukan bilangan prima dan menghitung GCD (Greatest Common Divisor).
3. Menerapkan logaritma diskrit sederhana dalam simulasi kriptografi.

---

## 2. Dasar Teori
Dalam kriptografi, cipher klasik merupakan metode penyandian pesan yang menggunakan transformasi sederhana terhadap huruf atau angka berdasarkan aturan tertentu. Dua jenis cipher klasik yang paling dikenal adalah substitusi (misalnya Caesar Cipher) dan transposisi (misalnya Rail Fence Cipher). Pada substitusi, setiap huruf dalam plaintext diganti dengan huruf lain sesuai pola tertentu, sedangkan pada transposisi, posisi huruf-hurufnya diubah tanpa mengubah identitas huruf itu sendiri. Walau sederhana, cipher klasik menjadi dasar bagi pengembangan sistem kriptografi modern.

Selain itu, konsep aritmetika modular memainkan peran penting dalam kriptografi, khususnya pada algoritma modern seperti RSA dan Diffie-Hellman. Aritmetika modular adalah sistem operasi matematika yang bekerja dalam “lingkaran” nilai tertentu (modulus n), di mana hasil operasi selalu diambil sisa baginya terhadap n. Contohnya, 7+5≡0(mod12). Konsep ini memungkinkan pembentukan operasi yang sulit dibalik tanpa kunci tertentu, yang menjadi dasar keamanan algoritma kunci publik.

Konsep logaritma diskrit juga berperan penting dalam keamanan sistem kriptografi modern. Logaritma diskrit adalah permasalahan mencari eksponen 
x pada persamaan ax≡b(mod n), yang sangat sulit diselesaikan ketika n besar. Kesulitan inilah yang digunakan sebagai dasar keamanan pada protokol seperti Diffie-Hellman Key Exchange dan ElGamal Encryption.

---

## 3. Alat dan Bahan
(- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub 

---

## 4. Langkah Percobaan
**Aritmetika Modular**
- Membuat file `modular_arithmetic.py` di folder `praktikum/week3-modmath-gcd/src/`.
- Menyalin kode program aritmetika modular.
- Menjalankan dengan perintah:

     ```
     python modular_arithmetic.py
     ```
**GCD (Algoritma Euclidean)**
- Membuat file `gcd_euclidean.py` di folder yang sama.
- Menyalin kode program GCD.
- Menjalankan:

     ```
     python gcd_euclidean.py
     ```
**Extended Euclidean Algorithm**
- Membuat file `extended_euclidean.py`.
- Menyalin kode program *Extended Euclidean* dan *Modular Inverse*.
- Menjalankan:

     ```
     python extended_euclidean.py
     ```
**Logaritma Diskrit (Discrete Log)**
- Membuat file `discrete_log.py`.
- Menyalin kode program *Logaritma Diskrit*.
- Menjalankan:

     ```
     python discrete_log.py
     ```

---

## 5. Source Code
# Aritmetika Modular (dengan input dari user)

# Fungsi dasar
def mod_add(a, b, n):
    return (a + b) % n

def mod_sub(a, b, n):
    return (a - b) % n

def mod_mul(a, b, n):
    return (a * b) % n

def mod_exp(base, exp, n):
    return pow(base, exp, n)

# Input dari user
print("=== Aritmetika Modular ===")
a = int(input("Masukkan nilai a: "))
b = int(input("Masukkan nilai b: "))
n = int(input("Masukkan modulus n: "))

# Operasi dasar
print(f"\nHasil operasi:")
print(f"{a} + {b} mod {n} = {mod_add(a, b, n)}")
print(f"{a} - {b} mod {n} = {mod_sub(a, b, n)}")
print(f"{a} * {b} mod {n} = {mod_mul(a, b, n)}")

# Operasi eksponensial modular
base = int(input("\nMasukkan basis untuk eksponensiasi: "))
exp = int(input("Masukkan pangkat: "))
mod_exp_result = mod_exp(base, exp, n)
print(f"{base}^{exp} mod {n} = {mod_exp_result}")

------------------------------------------------------------------------
# GCD & Algoritma Euclidean

def gcd(a, b):
    # Algoritma Euclidean: mencari pembagi bersama terbesar (Greatest Common Divisor)
    while b != 0:
        a, b = b, a % b
    return a

# Input dari user
print("=== GCD (Greatest Common Divisor) ===")
a = int(input("Masukkan bilangan pertama (a): "))
b = int(input("Masukkan bilangan kedua (b): "))

# Hitung GCD
hasil = gcd(a, b)

# Tampilkan hasil
print(f"\nGCD dari {a} dan {b} adalah: {hasil}")

------------------------------------------------------------------------
# Extended Euclidean Algorithm & Modular Inverse

def egcd(a, b):
    """Mengembalikan (gcd, x, y) sehingga ax + by = gcd(a, b)"""
    if a == 0:
        return b, 0, 1
    g, x1, y1 = egcd(b % a, a)
    return g, y1 - (b // a) * x1, x1

def modinv(a, n):
    """Mencari invers modular dari a (mod n) menggunakan Extended Euclidean Algorithm"""
    g, x, _ = egcd(a, n)
    if g != 1:
        # Jika gcd(a, n) ≠ 1 maka tidak ada invers modular
        return None
    else:
        return x % n

# Input dari user
print("=== Extended Euclidean Algorithm & Modular Inverse ===")
a = int(input("Masukkan nilai a: "))
n = int(input("Masukkan modulus n: "))

# Hitung invers modular
invers = modinv(a, n)

if invers is None:
    print(f"Tidak ada invers modular untuk {a} mod {n} (karena gcd({a}, {n}) ≠ 1).")
else:
    print(f"Invers dari {a} mod {n} adalah: {invers}")

------------------------------------------------------------------------
# Logaritma Diskrit (Discrete Logarithm)

def discrete_log(a, b, n):
    """Mencari x sehingga a^x ≡ b (mod n)"""
    for x in range(n):
        if pow(a, x, n) == b:
            return x
    return None  # jika tidak ditemukan

# Input dari user
print("=== Logaritma Diskrit (Discrete Logarithm) ===")
a = int(input("Masukkan nilai a (basis): "))
b = int(input("Masukkan nilai b (hasil): "))
n = int(input("Masukkan modulus n: "))

# Hitung logaritma diskrit
x = discrete_log(a, b, n)

# Tampilkan hasil
if x is not None:
    print(f"\nNilai x yang memenuhi {a}^x ≡ {b} (mod {n}) adalah: {x}")
else:
    print(f"\nTidak ditemukan nilai x yang memenuhi {a}^x ≡ {b} (mod {n}).")


---

## 6. Hasil dan Pembahasan
Keempat program — Aritmetika Modular, GCD (Euclidean), Extended Euclidean (Modular Inverse), dan Logaritma Diskrit — telah diuji dengan beberapa contoh input sederhana dan seluruh hasilnya sesuai dengan ekspektasi perhitungan teoritis. Program aritmetika modular menghasilkan operasi tambah, kurang, kali, dan pangkat dengan benar; algoritma Euclidean berhasil menemukan gcd yang tepat; fungsi extended Euclidean menghasilkan invers modular yang valid saat bilangan relatif prima; dan logaritma diskrit mampu menemukan eksponen yang memenuhi persamaan modular untuk modulus kecil. Error yang umum muncul biasanya terkait kesalahan input (bukan bilangan bulat), lokasi file yang salah, atau kasus tanpa invers (gcd ≠ 1). Semua dapat diatasi dengan validasi input, penanganan exception, serta memastikan file dijalankan dari direktori yang benar.

Hasil Screenshot
*Aritmetika Modular*<img width="1920" height="1080" alt="Screenshot 2025-10-27 211705" src="https://github.com/user-attachments/assets/b4c5e911-cc41-43e5-870f-2724999b8b88" />
*GCD & Algoritma Euclidean*<img width="1920" height="1080" alt="Screenshot 2025-10-27 212214" src="https://github.com/user-attachments/assets/05cffd0a-ed74-471d-9ba2-a96d6385ead9" />
*Extended Euclidean Algorithm & Modular Inverse*<img width="1920" height="1080" alt="Screenshot 2025-10-27 212438" src="https://github.com/user-attachments/assets/1998ef96-a74b-4d88-9fa2-dd56a1faa81d" />
Logaritma Diskrit<img width="1920" height="1080" alt="Screenshot 2025-10-27 212704" src="https://github.com/user-attachments/assets/69c36566-f23c-40a6-95d9-e5b3fbffc010" />

---

## 7. Jawaban Pertanyaan

- Pertanyaan 1: Peran Aritmetika Modular dalam Kriptografi Modern
  Jawab : Aritmetika modular berperan sebagai fondasi utama dalam kriptografi modern karena semua operasi enkripsi dan dekripsi dilakukan di dalam ruang bilangan terbatas yang diatur oleh operasi modulo. Dengan menggunakan aritmetika modular, sistem kriptografi dapat mengontrol besar nilai hasil perhitungan agar tetap dalam rentang tertentu, mencegah overflow, dan menjaga efisiensi komputasi. Selain itu, sifat periodik dan deterministik dari operasi modular membuatnya ideal untuk algoritma seperti RSA, Diffie–Hellman, dan kriptografi eliptik (ECC), yang seluruhnya bergantung pada perhitungan eksponensial dan invers dalam sistem modulo besar.
- Pertanyaan 2: Mengapa Invers Modular Penting dalam Algoritma Kunci Publik (RSA)
Jawab : Invers modular memiliki peran krusial dalam algoritma RSA karena digunakan untuk membentuk hubungan antara kunci publik dan kunci privat. Dalam RSA, kunci privat d dihitung sebagai invers modular dari kunci publik e terhadap fungsi totien φ(n), sehingga memenuhi persamaan e⋅d≡1(mod φ(n)). Hubungan ini memungkinkan pesan yang telah dienkripsi dengan kunci publik untuk dapat dikembalikan ke bentuk semula menggunakan kunci privat. Tanpa invers modular, proses pembalikan enkripsi menjadi mustahil, sehingga keamanan dan fungsi dasar RSA tidak dapat berjalan.
- Pertanyaan 3: Tantangan utama dalam menyelesaikan logaritma diskrit untuk modulus besar adalah tingkat kesulitannya yang sangat tinggi secara komputasional, karena tidak ada algoritma efisien yang dapat menemukan eksponen x dari persamaan y=gx mod p dalam waktu polinomial. Meskipun menghitung hasil perpangkatan modular mudah dilakukan, mencari nilai eksponen baliknya hampir mustahil ketika modulus p sangat besar. Kompleksitas ini menjadi dasar keamanan dari berbagai sistem kriptografi kunci publik seperti Diffie–Hellman dan ElGamal, yang mengandalkan ketidakmampuan penyerang untuk memecahkan logaritma diskrit dalam waktu yang realistis.

---

## 8. Kesimpulan
Dari hasil praktikum, dapat disimpulkan bahwa konsep aritmetika modular, algoritma Euclidean, extended Euclidean, dan logaritma diskrit dapat diimplementasikan dengan baik menggunakan Python. Seluruh algoritma bekerja sesuai teori dasar kriptografi dan menunjukkan pentingnya operasi matematika modular dalam sistem enkripsi modern.

---

## 9. Daftar Pustaka
Modul dan Yotube

---

## 10. Commit Log

```
