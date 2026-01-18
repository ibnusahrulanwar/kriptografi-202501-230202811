# Laporan Praktikum Kriptografi
Minggu ke-: 11
Topik: Secret Sharing
Nama: Ibnu Sahrul Anwar
NIM: 230202811 
Kelas: 5IKKA 

---

## 1. Tujuan
1. Menjelaskan konsep Shamir Secret Sharing (SSS).
2. Melakukan simulasi pembagian rahasia ke beberapa pihak menggunakan skema SSS.
3. Menganalisis keamanan skema distribusi rahasia.
---

## 2. Dasar Teori
**Secret sharing** adalah teknik kriptografi untuk membagi sebuah informasi rahasia (*secret*) menjadi beberapa bagian (*shares*) yang dibagikan ke beberapa pihak. Rahasia tersebut hanya dapat dikembalikan jika sejumlah *shares* tertentu digabungkan sesuai aturan *threshold* (t, n), di mana *n* adalah jumlah total *shares* dan *t* adalah jumlah minimum *shares* yang dibutuhkan untuk merekonstruksi rahasia. Jika jumlah *shares* yang dikumpulkan kurang dari *t*, maka informasi rahasia tetap tidak dapat diketahui.

Salah satu metode paling terkenal adalah **Shamir’s Secret Sharing**, yang menggunakan polinomial matematika berderajat *(t–1)* dengan nilai rahasia sebagai konstanta. Setiap *share* merupakan titik pada polinomial tersebut, dan dengan minimal *t* titik, rahasia dapat dihitung kembali menggunakan interpolasi. Skema ini aman secara teoritis karena kurang dari *t* *shares* tidak memberikan informasi apa pun tentang rahasia, sehingga banyak digunakan untuk pengamanan kunci kriptografi dan sistem yang membutuhkan kerja sama beberapa pihak.


---

## 3. Alat dan Bahan
- Python 3.x  
- Visual Studio Code 
- Git dan akun GitHub  
- Library tambahan : sympy

---

## 4. Langkah Percobaan
- Membuat file sss.py pada folder praktikum/week11-secret-sharing/src/.
- Mengimplementasikan algoritma Shamir’s Secret Sharing untuk membagi sebuah secret menjadi beberapa share.
- Menentukan parameter jumlah share (n) dan threshold (t).
- Menjalankan program menggunakan perintah python sss.py.
- Menguji rekonstruksi secret menggunakan minimal t share.
- Menyimpan hasil eksekusi program dalam folder screenshots/.

---

## 5. Source Code
import random
from sympy import symbols, interpolate

# Membuat polynomial dengan derajat t-1
def generate_polynomial(secret, t):
    coeffs = [secret] + [random.randint(1, 100) for _ in range(t - 1)]
    return coeffs

# Menghitung nilai polynomial
def evaluate_polynomial(coeffs, x):
    y = 0
    for i, coef in enumerate(coeffs):
        y += coef * (x ** i)
    return y

# Membuat shares
def generate_shares(secret, n, t):
    coeffs = generate_polynomial(secret, t)
    shares = []
    for i in range(1, n + 1):
        shares.append((i, evaluate_polynomial(coeffs, i)))
    return shares

# Rekonstruksi secret
def reconstruct_secret(shares):
    x = symbols('x')
    points = shares
    poly = interpolate(points, x)
    return poly.subs(x, 0)

# Contoh penggunaan
secret = 123
n = 5
t = 3

shares = generate_shares(secret, n, t)
print("Shares:", shares)

recovered_secret = reconstruct_secret(shares[:t])
print("Recovered Secret:", recovered_secret)

)

---

## 6. Hasil dan Pembahasan
- Program berhasil membagi sebuah secret menjadi beberapa share sesuai nilai n.
- Secret dapat direkonstruksi kembali dengan menggunakan minimal t share.
- Ketika jumlah share kurang dari threshold, secret tidak dapat dikembalikan dengan benar.
- Hasil eksekusi menunjukkan bahwa algoritma bekerja sesuai teori Shamir’s Secret Sharing.

Hasil eksekusi :
<img width="517" height="109" alt="Screenshot 2026-01-18 221346" src="https://github.com/user-attachments/assets/e0b92a94-e467-4330-b7e6-2adb89eb7d6e" />

---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Mengapa diperlukan threshold dalam secret sharing?
  Jawaban: Threshold digunakan untuk memastikan bahwa secret hanya dapat diakses jika sejumlah pihak bekerja sama, sehingga meningkatkan keamanan -dan menghindari single point of failure.

- Pertanyaan 2: Apa kelebihan Shamir’s Secret Sharing?
  Jawaban: Skema ini aman secara informasi-teoretik karena secret tidak dapat ditebak meskipun penyerang memiliki komputasi tak terbatas selama jumlah share kurang dari threshold.
---

## 8. Kesimpulan
- Percobaan secret sharing menggunakan Shamir’s Secret Sharing berhasil dilakukan dengan baik. Secret dapat dibagi dan direkonstruksi sesuai nilai threshold yang ditentukan. Metode ini efektif untuk pengamanan data yang membutuhkan kerja sama beberapa pihak.
---

## 9. Daftar Pustaka
- Katz, J., & Lindell, Y. Introduction to Modern Cryptography.
- Stallings, W. Cryptography and Network Security.
- Shamir, A. “How to Share a Secret”, Communications of the ACM.

---


