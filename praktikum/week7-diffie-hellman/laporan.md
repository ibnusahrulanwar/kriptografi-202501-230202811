<img width="1920" height="1080" alt="Screenshot 2025-11-14 232032" src="https://github.com/user-attachments/assets/80dafdfe-57f4-4f41-8b13-a46c69b9f9cc" /># Laporan Praktikum Kriptografi
Minggu ke-: 7
Topik: Diffie-Hellman Key Exchange 
Nama: Ibnu Sahrul Anwar
NIM: 230202811
Kelas: 5IKKA 

---

## 1. Tujuan
- Melakukan simulasi protokol Diffie-Hellman untuk pertukaran kunci publik.
- Menjelaskan mekanisme pertukaran kunci rahasia menggunakan bilangan prima dan logaritma diskrit.
- Menganalisis potensi serangan pada protokol Diffie-Hellman (termasuk serangan Man-in-the-Middle / MITM).

---

## 2. Dasar Teori
Dasar Teori Serangan MITM pada Diffie–Hellman
Diffie–Hellman adalah metode pertukaran kunci yang memungkinkan dua pihak membentuk kunci rahasia bersama melalui media publik. Keamanannya bergantung pada sulitnya menyelesaikan Discrete Logarithm Problem. Namun, protokol ini tidak memiliki autentikasi bawaan, sehingga tidak dapat memastikan apakah public key yang diterima benar-benar milik pihak asli.

Kelemahan ini membuka peluang Man-in-the-Middle Attack (MITM). Dalam serangan MITM, penyerang (Eve) mencegat dan mengganti public key yang dipertukarkan antara Alice dan Bob. Akibatnya, Alice membentuk kunci dengan Eve, dan Bob juga membentuk kunci lain dengan Eve. Alice dan Bob memiliki kunci berbeda, sementara Eve mengetahui keduanya sehingga dapat membaca, mengubah, dan meneruskan pesan tanpa terdeteksi.

Untuk mencegah MITM, Diffie–Hellman harus dilengkapi autentikasi seperti tanda tangan digital, sertifikat TLS/SSL, atau protokol STS yang mengikat identitas pada public key yang dipertukarkan.

---

## 3. Alat dan Bahan
- Laptop & Windows
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
- Library tambahan ; secrets, random

---

## 4. Langkah Percobaan
A. Percobaan 1 – Simulasi Diffie–Hellman Normal (Tanpa Serangan)
- Siapkan skrip Python simulasi Diffie–Hellman (kode dasar pertukaran kunci).
- Tentukan parameter publik:
    Bilangan prima kecil, misalnya p=23
    Generator g=5
- Jalankan program untuk menghasilkan:
    Kunci privat Alice dan Bob
    Public key A dan B
- Amati hasil perhitungan:
    Alice menghitung kunci bersama
    Bob menghitung kunci bersama
- Catat bahwa kedua kunci yang dihasilkan harus sama.

B. Percobaan 2 – Simulasi Serangan Man-in-the-Middle (MITM)
- Tambahkan fungsi simulasi MITM yang telah dibuat sebelumnya.
- Jalankan program MITM untuk mensimulasikan:
    Eve mencegat public key dari Alice dan Bob
    Eve mengganti public key tersebut dengan miliknya
- Program akan menghasilkan:
    Kunci yang dihitung Alice
    Kunci yang dihitung Bob
    Dua kunci yang dihitung Eve (kunci dengan Alice & kunci dengan Bob)
- Bandingkan kunci yang diperoleh:
    Kunci Alice dan Bob tidak sama
    Eve mengetahui kedua kunci
- Catat perbedaan hasil dengan percobaan pertama.

C. Analisis Hasil
- Bandingkan hasil percobaan normal vs MITM.
- Jelaskan bahwa perbedaan kunci terjadi karena Eve mengganti public key selama pertukaran.
- Simpulkan bahwa Diffie–Hellman tanpa autentikasi rentan terhadap MITM.

---

## 5. Source Code
Diffie-Hellman Normal
import secrets
import random
from typing import Tuple

# ---------------------------
# Util: Miller-Rabin primality
# ---------------------------
def is_probable_prime(n: int, k: int = 8) -> bool:
    """Miller-Rabin probabilistic primality test. k = number of rounds."""
    if n < 2:
        return False
    small_primes = [2,3,5,7,11,13,17,19,23,29]
    for p in small_primes:
        if n % p == 0:
            return n == p
    # write n-1 as d * 2^s
    s = 0
    d = n - 1
    while d % 2 == 0:
        d //= 2
        s += 1
    for _ in range(k):
        a = secrets.randbelow(n - 3) + 2  # random in [2, n-2]
        x = pow(a, d, n)
        if x == 1 or x == n - 1:
            continue
        composite = True
        for _ in range(s - 1):
            x = pow(x, 2, n)
            if x == n - 1:
                composite = False
                break
        if composite:
            return False
    return True

def generate_prime(bits: int = 256) -> int:
    """Generate a probable prime with given bit-length."""
    assert bits >= 2
    while True:
        # ensure top bit set so number has correct bit length, and odd
        candidate = secrets.randbits(bits) | (1 << (bits - 1)) | 1
        if is_probable_prime(candidate):
            return candidate

# ---------------------------
# Diffie-Hellman functions
# ---------------------------
def generate_private_key(p: int) -> int:
    """Generate private key in range [2, p-2]"""
    return secrets.randbelow(p - 3) + 2

def generate_public_key(g: int, private: int, p: int) -> int:
    """Compute public key g^private mod p"""
    return pow(g, private, p)

def compute_shared_secret(peer_public: int, private: int, p: int) -> int:
    """Compute shared secret (peer_public^private mod p)"""
    return pow(peer_public, private, p)

def dh_simulate(p: int, g: int) -> Tuple[int,int,int,int,int]:
    """
    Simulate one DH exchange.
    Returns (a_priv, b_priv, A_pub, B_pub, shared_secret)
    """
    a = generate_private_key(p)
    b = generate_private_key(p)
    A = generate_public_key(g, a, p)
    B = generate_public_key(g, b, p)
    sA = compute_shared_secret(B, a, p)
    sB = compute_shared_secret(A, b, p)
    assert sA == sB
    return a, b, A, B, sA

# ---------------------------
# Demo / contoh penggunaan
# ---------------------------
def demo_small_example():
    # contoh edukasi: p=23, g=5 (sama seperti yang Anda berikan)
    p = 23
    g = 5
    print("=== Demo kecil (edukasi) ===")
    a, b, A, B, s = dh_simulate(p, g)
    print(f"Parameter publik: p={p}, g={g}")
    print(f"Alice private a = {a}, public A = {A}")
    print(f"Bob   private b = {b}, public B = {B}")
    print(f"Kunci bersama = {s}")
    print()

def demo_large_example(bits: int = 512):
    # contoh praktis: generate prime p dan pilih g=2 (sering dipakai)
    print("=== Demo besar (lebih realistis) ===")
    print(f"Menghasilkan prime ~{bits} bit (mungkin perlu beberapa detik)...")
    p = generate_prime(bits)
    g = 2
    a, b, A, B, s = dh_simulate(p, g)
    print(f"p (bits) = {p.bit_length()} bit")
    print(f"g = {g}")
    print(f"Alice public (A) sample (hex, 64 chars): {hex(A)[:66]}")
    print(f"Bob   public (B) sample (hex, 64 chars): {hex(B)[:66]}")
    print(f"Kunci bersama (sample hex): {hex(s)[:66]}")
    print()

def demo_with_eavesdropper(p: int, g: int):
    # tunjukkan bahwa eavesdropper melihat p,g,A,B tapi tidak dapat menghitung s mudahnya
    print("=== Demo: eavesdropper melihat publik tetapi tidak bisa mudahkan s ===")
    a, b, A, B, s = dh_simulate(p, g)
    print("Publik: p, g, A, B")
    print(f"p = {p}")
    print(f"g = {g}")
    print(f"A = {A}")
    print(f"B = {B}")
    print("Eavesdropper harus memecahkan discrete log (sulit) untuk menemukan a atau b.")
    print(f"Kunci bersama yang didapat Alice/Bob = {s}")
    print()

if __name__ == "__main__":
    # Demo ringkas
    demo_small_example()
    # Jika ingin demo besar, uncomment baris berikut (akan butuh waktu tergantung bits).
    # demo_large_example(bits=512)
    # demo_with_eavesdropper(p=23, g=5)


Diffie_Hellman + MITM
import random

# ===============================
# PARAMETER UMUM
# ===============================
p = 23  # bilangan prima
g = 5   # generator


# ===============================
# FUNGSI SIMULASI NORMAL
# ===============================
def diffie_hellman_normal():
    print("\n=== SIMULASI NORMAL TANPA MITM ===")

    # private key
    a = random.randint(1, p-1)
    b = random.randint(1, p-1)

    # public key
    A = pow(g, a, p)
    B = pow(g, b, p)

    # shared secret
    sA = pow(B, a, p)
    sB = pow(A, b, p)

    print("Private Alice :", a)
    print("Private Bob   :", b)
    print("Public Alice  :", A)
    print("Public Bob    :", B)
    print("Shared Alice  :", sA)
    print("Shared Bob    :", sB)

    return sA, sB


# ===============================
# FUNGSI SIMULASI MITM
# ===============================
def diffie_hellman_MITM():
    print("\n=== SIMULASI MITM (Man-in-the-Middle Attack) ===")

    # private key normal
    a = random.randint(1, p-1)  # Alice
    b = random.randint(1, p-1)  # Bob

    # private key Eve
    e1 = random.randint(1, p-1)
    e2 = random.randint(1, p-1)

    # public key normal
    A = pow(g, a, p)
    B = pow(g, b, p)

    # public key Eve
    E1 = pow(g, e1, p)
    E2 = pow(g, e2, p)

    # Eve mengganti public key
    intercepted_A = E1   # Alice menerima milik Eve
    intercepted_B = E2   # Bob menerima milik Eve

    # kunci bersama yang terbentuk (TIDAK SAMA)
    shared_Alice = pow(intercepted_B, a, p)  # kunci Alice–Eve
    shared_Bob   = pow(intercepted_A, b, p)  # kunci Bob–Eve

    # Eve menghitung kedua kunci
    eve_with_Alice = pow(A, e1, p)
    eve_with_Bob   = pow(B, e2, p)

    print("Public Alice (A) :", A)
    print("Public Bob   (B) :", B)
    print("Eve kirim ke Alice :", intercepted_B)
    print("Eve kirim ke Bob   :", intercepted_A)

    print("\nKunci Alice : ", shared_Alice)
    print("Kunci Bob   : ", shared_Bob)

    print("\nEve tahu kunci Alice:", eve_with_Alice)
    print("Eve tahu kunci Bob  :", eve_with_Bob)

    return shared_Alice, shared_Bob, eve_with_Alice, eve_with_Bob


# ===============================
# JALANKAN SEMUA SIMULASI
# ===============================

normal = diffie_sim()
mitm    = diffie_hellman_mitm()


---

## 6. Hasil dan Pembahasan
Pada simulasi normal, Diffie–Hellman berjalan aman karena Alice dan Bob berhasil menghasilkan shared secret yang sama meskipun bertukar kunci melalui saluran publik. Namun pada simulasi MITM, Eve mencegat dan mengganti kunci publik sehingga Alice dan Bob tidak lagi memiliki kunci yang sama. Sebaliknya, Eve memperoleh dua kunci berbeda (kunci dengan Alice dan kunci dengan Bob), sehingga dapat membaca dan memanipulasi komunikasi. Hal ini menunjukkan bahwa Diffie–Hellman tanpa autentikasi rentan terhadap serangan MITM dan membutuhkan mekanisme verifikasi identitas seperti tanda tangan digital atau sertifikat untuk menjadi aman.

Hasil eksekusi program<img width="1920" height="1080" alt="Screenshot 2025-11-14 232032" src="https://github.com/user-attachments/assets/eab1c82d-d9fa-42b8-9692-dc4e5140f686" />


---

## 7. Jawaban Pertanyaan
1) Mengapa Diffie-Hellman memungkinkan pertukaran kunci di saluran publik?
   Jawab: Karena Diffie–Hellman memanfaatkan sifat one-way function dari operasi eksponensial modulo bilangan prima. Kunci publik dapat dibagikan secara terbuka, tetapi kunci privat tetap aman karena sangat sulit (secara komputasi) menghitung discrete logarithm untuk mendapatkan kunci privat dari kunci publik. Akibatnya, kedua pihak dapat menghasilkan kunci rahasia yang sama tanpa pernah mengirimkan kunci rahasia itu sendiri.
3) Apa kelemahan utama protokol Diffie-Hellman murni?
 Jawab: Kelemahan utamanya adalah tidak memiliki autentikasi, sehingga rentan terhadap Man-in-the-Middle Attack (MITM). Penyerang dapat mencegat dan mengganti kunci publik, lalu membuat dua kunci rahasia berbeda dengan masing-masing pihak tanpa mereka sadari.
5) Bagaimana cara mencegah serangan MITM pada protokol ini?
Jawab: Serangan MITM dapat dicegah dengan menambahkan autentikasi identitas, misalnya dengan:
- Digital signature (menandatangani kunci publik)
- Sertifikat digital dari CA (seperti pada TLS/HTTPS)
- Public Key Infrastructure (PKI)
- Variasi aman seperti Authenticated Diffie–Hellman atau ECDHE dengan sertifikat
---

## 8. Kesimpulan
Protokol Diffie–Hellman memungkinkan dua pihak membentuk kunci rahasia bersama meskipun berkomunikasi melalui saluran publik karena keamanan matematis dari discrete logarithm problem. Namun, versi murninya tidak menyediakan autentikasi sehingga rentan terhadap serangan Man-in-the-Middle, di mana penyerang dapat mengubah kunci publik dan mengambil alih komunikasi. Untuk menjadikan pertukaran kunci ini benar-benar aman, Diffie–Hellman harus dikombinasikan dengan mekanisme autentikasi seperti tanda tangan digital atau sertifikat digital agar identitas pengirim dapat diverifikasi.
---

## 9. Daftar Pustaka
- Stallings, W. (2017). Cryptography and Network Security: Principles and Practice. Pearson.

---

