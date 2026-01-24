# Laporan Praktikum Kriptografi
Minggu ke-: 14
Topik: Analisis Serangan 
Nama: Ibnu Sahrul Anwar 
NIM: 230202811
Kelas: 5IKKA 

---

## 1. Tujuan
1. Mengidentifikasi jenis serangan pada sistem informasi nyata.
2. Mengevaluasi kelemahan algoritma kriptografi yang digunakan.
3. Memberikan rekomendasi algoritma kriptografi yang sesuai untuk perbaikan keamanan.

---

## 2. Dasar Teori
Analisis serangan kriptografi bertujuan memahami bagaimana mekanisme pengamanan informasi dapat ditembus melalui eksploitasi kelemahan matematis, implementasi, maupun operasional pada sistem informasi nyata. Dasar teorinya berangkat dari konsep threat model, yaitu pemetaan kemampuan penyerang, aset yang dilindungi, serta permukaan serangan. Jenis serangan kriptografi meliputi brute force attack, ciphertext-only, known-plaintext, chosen-plaintext, man-in-the-middle, hingga side-channel attack yang memanfaatkan kebocoran fisik seperti waktu eksekusi atau konsumsi daya. Identifikasi serangan dilakukan dengan menganalisis alur komunikasi, manajemen kunci, dan konteks penggunaan algoritma dalam sistem aktual, karena algoritma yang kuat secara teori tetap dapat gagal jika diterapkan secara keliru.

Evaluasi kelemahan algoritma kriptografi didasarkan pada asumsi bahwa keamanan tidak hanya bergantung pada panjang kunci, tetapi juga pada ketahanan algoritma terhadap kriptanalisis modern dan kualitas implementasinya. Algoritma lama seperti DES, MD5, atau SHA-1 memiliki kelemahan struktural yang memungkinkan collision atau pencarian kunci lebih cepat dari brute force teoritis, sehingga tidak lagi layak digunakan. Selain itu, penggunaan mode operasi yang salah (misalnya ECB pada AES), manajemen kunci yang buruk, atau tidak adanya randomness yang kuat juga menjadi titik lemah serius. Analisis ini menuntut pendekatan kritis: apakah kelemahan berasal dari desain algoritma, parameter yang dipilih, atau integrasinya dalam sistem informasi.

Berdasarkan analisis serangan dan kelemahan tersebut, rekomendasi algoritma kriptografi harus menyesuaikan tujuan keamanan, kinerja, dan konteks ancaman. Untuk enkripsi data, algoritma simetris modern seperti AES dengan mode GCM atau ChaCha20-Poly1305 direkomendasikan karena memberikan kerahasiaan sekaligus integritas. Untuk pertukaran kunci dan tanda tangan digital, algoritma asimetris seperti RSA dengan panjang kunci memadai atau Elliptic Curve Cryptography (ECC) lebih efisien dan aman terhadap serangan kontemporer. Secara konseptual, dasar teori ini menegaskan bahwa keamanan kriptografi adalah sistemik: algoritma yang tepat, implementasi yang benar, dan kebijakan manajemen kunci yang kuat harus berjalan bersamaan untuk meningkatkan keamanan sistem informasi secara berkelanjutan.

---

## 3. Alat dan Bahan
- Visual Studio Code / editor lain  
- Git dan akun GitHub  
---

## 4. Langkah Percobaan
1. Identifikasi Serangan
2. Evaluasi Kelemahan
3. Rekomendasi Solusi  
---

## 5. Source Code

---

## 6. Hasil dan Pembahasan
 1. Langkah 1 — Identifikasi Serangan

        Studi kasus         : serangan brute force dan dictionary attack terhadap database password yang disimpan menggunakan hash MD5.
        Vektor serangan     : penyerang memperoleh dump hash (misalnya dari kebocoran database), lalu mencocokkannya dengan rainbow table atau melakukan brute force menggunakan GPU.
        Penyebab kelemahan  : MD5 adalah fungsi hash cepat tanpa mekanisme bawaan untuk memperlambat komputasi, sering digunakan tanpa salt, sehingga satu hash dapat diuji jutaan kali per detik. Asumsi tersembunyi sistem lama adalah bahwa hash saja sudah cukup untuk melindungi password.

    2. Langkah 2 — Evaluasi Kelemahan (Uji Kritis)

        Kelemahan algoritma : MD5 secara struktural lemah terhadap collision dan tidak dirancang untuk perlindungan password, sehingga tidak tahan terhadap kriptanalisis modern.
        Kelemahan implementasi dan konfigurasi: penggunaan MD5 tanpa salt, tanpa key stretching, serta tidak adanya pembatasan percobaan login memperparah risiko. Dengan demikian, kerentanan tidak hanya berasal dari algoritma yang usang, tetapi juga dari cara penerapan dan kebijakan keamanan sistem yang keliru.

    3. Langkah 3 — Rekomendasi Solusi (Kesimpulan dan Dampak)

        Solusi yang direkomendasikan : mengganti MD5 dengan algoritma password hashing khusus seperti bcrypt, scrypt, atau Argon2, yang dirancang lambat dan adaptif terhadap peningkatan daya komputasi.
        Alasan pemilihan            : algoritma ini menggunakan salt unik dan cost factor sehingga serangan brute force menjadi mahal secara waktu dan sumber daya.
        Dampak terhadap keamanan    : risiko kompromi password turun signifikan meskipun database bocor, dan sistem menjadi lebih tahan terhadap ancaman jangka panjang, sekaligus mendukung prinsip crypto-agility untuk pembaruan di masa depan.

---

## 7. Jawaban Pertanyaan
1. Sistem lama rentan karena dirancang saat daya komputasi masih terbatas, sehingga menggunakan kata sandi lemah, panjang kunci pendek, dan fungsi hash cepat tanpa salt atau rate limiting. Asumsi bahwa penyerang memiliki sumber daya terbatas sudah tidak relevan, membuat serangan massal kini sangat efektif.
2. Kelemahan algoritma berasal dari cacat desain kriptografis yang tidak bisa diperbaiki tanpa mengganti algoritma (misalnya DES, MD5). Kelemahan implementasi muncul dari penerapan yang salah terhadap algoritma yang sebenarnya aman, seperti mode operasi keliru, manajemen kunci buruk, atau kebocoran side-channel.
3. Organisasi perlu memakai algoritma modern, melakukan audit rutin, dan menerapkan manajemen kunci yang kuat. Prinsip crypto-agility penting agar sistem dapat menyesuaikan diri dengan ancaman baru, karena keamanan kriptografi bersifat dinamis, bukan permanen.
---

## 8. Kesimpulan
-
analisis menunjukkan bahwa banyak serangan kriptografi pada sistem informasi terjadi karena penggunaan algoritma usang seperti MD5 yang tidak dirancang untuk melindungi password serta diperparah oleh implementasi dan konfigurasi yang lemah. Keamanan tidak cukup bergantung pada proses hashing, tetapi pada kesesuaian algoritma dengan tujuan penggunaannya, kualitas penerapan, dan manajemen sistem secara keseluruhan. Dengan mengganti algoritma lemah ke mekanisme modern seperti bcrypt, scrypt, atau Argon2 serta menerapkan prinsip crypto-agility, organisasi dapat meningkatkan ketahanan sistem secara signifikan terhadap serangan saat ini dan ancaman di masa depan.
---

## 9. Daftar Pustaka
- Stallings (2017), Bab 16.
---

## 10. Commit Log

```
commit week14-analisis-serangan
Author: Ibnu Sahrul Anwar <benuibnuanwar@gmail.com>
Date:   2026-24-01
```
