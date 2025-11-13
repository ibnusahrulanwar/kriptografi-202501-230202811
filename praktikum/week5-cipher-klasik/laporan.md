# Laporan Praktikum Kriptografi
Minggu ke-: 5 
Topik: Cipher Klasik (Caesar, Vigenère, Transposisi)  
Nama: Ibnu Sahrul Anwar 
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
- Menerapkan algoritma Caesar Cipher untuk enkripsi dan dekripsi teks.
- Menerapkan algoritma Vigenère Cipher dengan variasi kunci.
- Mengimplementasikan algoritma transposisi sederhana.
- Menjelaskan kelemahan algoritma kriptografi klasik.


---

## 2. Dasar Teori
Dasar Teori Cipher Klasik (Caesar, Vigenère, dan Transposisi)

Cipher klasik merupakan teknik kriptografi yang digunakan pada masa awal perkembangan ilmu keamanan informasi sebelum munculnya algoritma modern berbasis matematika kompleks. Teknik ini bertujuan untuk mengubah pesan asli (plaintext) menjadi bentuk yang tidak dapat langsung dibaca (ciphertext) agar isi pesan tetap terjaga kerahasiaannya. Tiga jenis cipher klasik yang paling dikenal dan sering digunakan dalam pembelajaran dasar kriptografi adalah Caesar Cipher, Vigenère Cipher, dan Transposisi Cipher.

Caesar Cipher merupakan salah satu algoritma kriptografi paling sederhana yang dikembangkan oleh Julius Caesar pada masa Romawi Kuno. Metode ini termasuk ke dalam kategori substitution cipher, karena setiap huruf pada plaintext digantikan dengan huruf lain berdasarkan jarak pergeseran tertentu yang disebut sebagai kunci (key). Misalnya, jika menggunakan kunci 3, maka huruf A akan digeser menjadi D, B menjadi E, dan seterusnya. Contoh penerapannya yaitu pesan “CLASSIC CIPHER” dengan kunci 3 akan dienkripsi menjadi “FODVVLF FLSKHU”. Meskipun mudah digunakan dan dipahami, Caesar Cipher memiliki kelemahan utama karena mudah dipecahkan menggunakan analisis frekuensi huruf atau metode brute force yang mencoba semua kemungkinan kunci.

Selanjutnya, Vigenère Cipher merupakan pengembangan dari Caesar Cipher yang menggunakan lebih dari satu alfabet penggeseran, sehingga disebut sebagai polyalphabetic substitution cipher. Cipher ini diperkenalkan oleh Blaise de Vigenère pada abad ke-16 untuk meningkatkan keamanan dari cipher substitusi tunggal. Proses enkripsinya dilakukan dengan menggunakan kata kunci yang terdiri dari huruf, misalnya “KEY”. Kunci ini diulang sesuai panjang teks, lalu setiap huruf plaintext digeser sesuai nilai huruf pada kunci. Sebagai contoh, huruf “K” dalam kunci berarti pergeseran 10 huruf, “E” berarti 4 huruf, dan “Y” berarti 24 huruf. Dengan demikian, plaintext “KRIPTOGRAFI” dengan kunci “KEY” akan menjadi ciphertext “UVCZXSQVLKZ”. Keunggulan metode ini adalah hasil enkripsinya lebih sulit dianalisis karena pergeseran huruf berbeda-beda, namun kelemahannya muncul apabila kunci yang digunakan terlalu pendek atau berulang, karena masih dapat dianalisis menggunakan metode Kasiski atau frequency analysis.

Sedangkan Transposisi Cipher atau Permutation Cipher merupakan metode enkripsi yang tidak mengubah karakter pada pesan, melainkan hanya menukar atau mengubah urutan penulisannya berdasarkan pola tertentu. Dalam metode ini, plaintext ditulis ke dalam tabel dengan jumlah kolom sesuai nilai kunci, kemudian hasil enkripsi diperoleh dengan membaca huruf-huruf dalam urutan kolom tertentu. Misalnya, pada plaintext “TRANSPOSITIONCIPHER” dengan kunci 5, huruf-huruf disusun dalam tabel lima kolom, lalu dibaca secara vertikal per kolom sehingga menghasilkan ciphertext “TPIPROHSASINNICIERTO”. Keuntungan dari cipher ini adalah pesan menjadi sulit dikenali secara langsung karena urutan hurufnya berubah, namun tetap memiliki kelemahan karena struktur huruf aslinya masih dapat direkonstruksi jika pola penulisan diketahui.

Secara keseluruhan, ketiga cipher klasik tersebut menjadi dasar penting dalam memahami konsep kriptografi, terutama mengenai bagaimana pesan dapat diubah bentuknya untuk menjaga kerahasiaan informasi. Walaupun kini algoritma cipher klasik tidak lagi digunakan dalam sistem keamanan modern karena mudah dipecahkan, prinsip dasar substitusi dan transposisi tetap menjadi pondasi dalam pengembangan algoritma kriptografi modern seperti AES, DES, dan RSA.

---

## 3. Alat dan Bahan
(- Python 3.x  
- Visual Studio Code / editor lain  
- Git dan akun GitHub  

---

## 4. Langkah Percobaan
Persiapan singkat
    Simpan masing-masing program sebagai: caesar_cipher.py, vigenere_cipher.py, transposisi_cipher.py di satu folder.
    Pastikan Python terinstal dan terminal berada di folder yang sama.
1. Caesar
   Jalankan: python caesar_cipher.py
   Masukkan teks (mis. CLASSIC CIPHER) dan kunci angka (mis. 3).
   Pilih Enkripsi → catat ciphertext.
   Uji Dekripsi dengan ciphertext dan kunci yang sama → harus kembali ke plaintext.
   (Opsional cepat) Coba brute-force: coba kunci 1–25 untuk melihat semua kemungkinan.
2. Vigenère
   Jalankan: python vigenere_cipher.py
   Masukkan teks (mis. KRIPTOGRAFI) dan kunci huruf (mis. KEY).
   Pilih Enkripsi → catat ciphertext.
   Uji Dekripsi dengan ciphertext dan kunci yang sama → kembali ke plaintext.
   (Variasi) Ganti kunci pendek vs panjang, amati perbedaan pola
3. Transposisi (uji cepat)
   Jalankan: python transposisi_cipher.py
   Masukkan teks (mis. TRANSPOSITIONCIPHER) dan kunci angka (mis. 5).
   Pilih Enkripsi → catat ciphertext.
   Uji Dekripsi dengan ciphertext dan kunci yang sama → kembali ke plaintext.
   (Variasi) Uji kunci lain (3,6,8) dan teks dengan panjang bukan kelipatan kunci.

---

## 5. Source Code
1. Caesar Cipher

# Program Caesar Cipher Sederhana

def caesar_cipher(text, key, mode):
    result = ""

    for char in text:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            if mode == 'encrypt':
                result += chr((ord(char) - base + key) % 26 + base)
            elif mode == 'decrypt':
                result += chr((ord(char) - base - key) % 26 + base)
        else:
            result += char
    return result

print("=== Program Caesar Cipher Sederhana ===")
text = input("Masukkan teks: ")
key = int(input("Masukkan kunci (angka): "))

print("\nPilih mode:")
print("1. Enkripsi")
print("2. Dekripsi")
mode = input("Pilihan (1/2): ")

if mode == '1':
    output = caesar_cipher(text, key, 'encrypt')
    print("\nHasil enkripsi:", output)
elif mode == '2':
    output = caesar_cipher(text, key, 'decrypt')
    print("\nHasil dekripsi:", output)
else:
    print("Pilihan tidak valid.")

2. Vigenere Cipher

# Program Vigenère Cipher Sederhana

def vigenere_encrypt(plaintext, key):
    result = []
    key = key.lower()
    key_index = 0
    for char in plaintext:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - 97
            base = 65 if char.isupper() else 97
            result.append(chr((ord(char) - base + shift) % 26 + base))
            key_index += 1
        else:
            result.append(char)
    return "".join(result)


def vigenere_decrypt(ciphertext, key):
    result = []
    key = key.lower()
    key_index = 0
    for char in ciphertext:
        if char.isalpha():
            shift = ord(key[key_index % len(key)]) - 97
            base = 65 if char.isupper() else 97
            result.append(chr((ord(char) - base - shift) % 26 + base))
            key_index += 1
        else:
            result.append(char)
    return "".join(result)


# --- Program utama ---
print("=== Program Vigenère Cipher Sederhana ===")
text = input("Masukkan teks: ")
key = input("Masukkan kunci (huruf): ")

print("\nPilih mode:")
print("1. Enkripsi")
print("2. Dekripsi")
mode = input("Pilihan (1/2): ")

if mode == '1':
    output = vigenere_encrypt(text, key)
    print("\nHasil enkripsi:", output)
elif mode == '2':
    output = vigenere_decrypt(text, key)
    print("\nHasil dekripsi:", output)
else:
    print("Pilihan tidak valid.")

3. Transposisi Cipher

# Program Transposisi Cipher Sederhana

def transpose_encrypt(plaintext, key=5):
    ciphertext = [''] * key
    for col in range(key):
        pointer = col
        while pointer < len(plaintext):
            ciphertext[col] += plaintext[pointer]
            pointer += key
    return ''.join(ciphertext)


def transpose_decrypt(ciphertext, key=5):
    num_of_cols = int(len(ciphertext) / key + 0.9999)
    num_of_rows = key
    num_of_shaded_boxes = (num_of_cols * num_of_rows) - len(ciphertext)
    plaintext = [''] * num_of_cols
    col = 0
    row = 0

    for symbol in ciphertext:
        plaintext[col] += symbol
        col += 1
        if (col == num_of_cols) or (col == num_of_cols - 1 and row >= num_of_rows - num_of_shaded_boxes):
            col = 0
            row += 1
    return ''.join(plaintext)


# --- Program utama ---
print("=== Program Transposisi Cipher Sederhana ===")
text = input("Masukkan teks: ")
key = int(input("Masukkan kunci (angka): "))

print("\nPilih mode:")
print("1. Enkripsi")
print("2. Dekripsi")
mode = input("Pilihan (1/2): ")

if mode == '1':
    output = transpose_encrypt(text, key)
    print("\nHasil enkripsi:", output)
elif mode == '2':
    output = transpose_decrypt(text, key)
    print("\nHasil dekripsi:", output)
else:
    print("Pilihan tidak valid.")

---

## 6. Hasil dan Pembahasan
Hasil percobaan menunjukkan bahwa Caesar Cipher hanya melakukan pergeseran huruf tetap berdasarkan kunci numerik. Misalnya, dengan kunci 3, huruf A menjadi D, B menjadi E, dan seterusnya.
Saat dilakukan dekripsi dengan kunci yang sama, teks kembali ke bentuk semula. Namun, hasil juga memperlihatkan kelemahan utama Caesar Cipher — karena hanya memiliki 25 kemungkinan kunci, dapat dengan mudah dipecahkan menggunakan brute force atau analisis frekuensi huruf.

Kesimpulan:
Caesar Cipher mudah digunakan tetapi sangat lemah terhadap serangan sederhana.

Hasil eksekusi program Caesar Cipher:
Caaesar Ciper<img width="1920" height="1080" alt="Screenshot 2025-11-13 215920" src="https://github.com/user-attachments/assets/9f3cdeb1-4c19-421f-8c6a-9059a979ed7c" />
Vigenere Ciper<img width="1920" height="1080" alt="Screenshot 2025-11-13 213730" src="https://github.com/user-attachments/assets/3279092e-d8ce-4bc6-8d02-3c13c1e7806d" />
Transposisi Ciper<img width="1920" height="1080" alt="Screenshot 2025-11-13 214357" src="https://github.com/user-attachments/assets/ac78b7c6-9ed2-4e77-8053-d08e5f8f0d0c" />


---

## 7. Jawaban Pertanyaan
1. Apa kelemahan utama algoritma Caesar Cipher dan Vigenère Cipher?
   Jawab:
   Caesar: Kuncinya terbatas (hanya 25), mudah dipecahkan dengan brute force.
    Vigenère: Lemah jika kunci pendek atau berulang, bisa diserang dengan analisis pola (Kasiski).

3. Mengapa cipher klasik mudah diserang dengan analisis frekuensi?
   Jawab: Karena cipher klasik tidak mengubah frekuensi huruf, pola huruf masih bisa dikenali.
   
5. Bandingkan kelebihan dan kelemahan cipher substitusi vs transposisi.
   Jawab:
    Substitusi: Mengganti huruf → frekuensi masih sama.
    Transposisi: Mengacak posisi huruf → urutan berubah tapi huruf tetap sama.
    Kombinasi keduanya lebih aman.
---

## 8. Kesimpulan
Cipher klasik seperti Caesar, Vigenère, dan Transposisi menunjukkan dasar teknik enkripsi sederhana. Namun, karena pola huruf dan struktur bahasa masih terlihat, cipher ini mudah diserang menggunakan analisis frekuensi. Untuk keamanan lebih baik, perlu digunakan kunci yang panjang atau kombinasi antara substitusi dan transposisi.

---

## 9. Daftar Pustaka
- Youtube
- Stallings, W. (2017). Cryptography and Network Security: Principles and Practice (7th ed.). Pearson Education.
---

