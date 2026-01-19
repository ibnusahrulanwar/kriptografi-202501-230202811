# Laporan Praktikum Kriptografi
Minggu ke-: 12
Topik: Aplikasi TLS & E-commerce
Nama: Ibnu Sahrul Anwar 
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
1. Menganalisis penggunaan kriptografi pada email dan SSL/TLS.
2. Menjelaskan enkripsi dalam transaksi e-commerce.
3. Mengevaluasi isu etika & privasi dalam penggunaan kriptografi di kehidupan sehari-hari.
---

## 2. Dasar Teori
Transport Layer Security (TLS) adalah protokol kriptografi yang digunakan untuk mengamankan komunikasi data antara dua pihak melalui jaringan, terutama Internet. TLS menyediakan enkripsi data, autentikasi server (dan kadang client), serta integritas pesan, sehingga informasi seperti kata sandi, transaksi, dan data pribadi tetap terlindungi dari penyadapan dan pemalsuan oleh pihak ketiga. TLS adalah penerus dari SSL (Secure Sockets Layer) dan merupakan standar keamanan jaringan modern yang banyak digunakan.

Aplikasi TLS sangat luas dan mencakup berbagai layanan dan protokol jaringan, antara lain:
- Web aman (HTTPS) – TLS mengamankan komunikasi antara browser dan server web dengan menampilkan ikon gembok di URL, yang menandakan bahwa data terenkripsi selama pengiriman.
- Email (SMTP, IMAP, POP3) – TLS melindungi pengiriman dan penerimaan email agar tidak disadap saat transit.
- Virtual Private Networks (VPN) – Banyak layanan VPN menggunakan TLS untuk membuat terowongan data terenkripsi antara klien dan jaringan perusahaan atau pribadi.
- Transfer file aman (FTPS) – Protokol transfer file seperti FTP dapat diamankan dengan TLS sehingga data yang dikirim tidak bisa dilihat atau diubah oleh pihak lain.
- Komunikasi real-time (VoIP, Messaging) – Aplikasi seperti VoIP dan layanan pesan instan dapat menggunakan TLS untuk menjaga privasi dan integritas komunikasi suara dan teks.
- Aplikasi IoT, API, Database – TLS juga digunakan untuk mengamankan pertukaran data antara perangkat IoT, layanan API, dan koneksi aplikasi ke database.

---

## 3. Alat dan Bahan
- Git dan Akun GitHub
- VS Code
---

## 4. Langkah Percobaan
- Analisis SSL/TLS pada Email & Web
- Studi Kasus E-commerce
- Analisis Etika & Privasi

---

## 5. Source Code
-
---

## 6. Hasil dan Pembahasan
a. E-commerce
Platform seperti Tokopedia dan Shopee menggunakan HTTPS (TLS) untuk mengamankan login dan transaksi pembayaran. TLS melindungi data pengguna, menjaga integritas transaksi, serta memastikan keaslian server melalui sertifikat digital.

b. Email
TLS mengamankan jalur komunikasi email (SMTP, IMAP, POP3), sementara PGP atau S/MIME melindungi isi email secara end-to-end, sehingga keamanan komunikasi lebih optimal.

Isu Etika & Privasi
Enkripsi melindungi privasi pengguna, tetapi memunculkan dilema hukum terkait pengawasan. Tantangan utama adalah menyeimbangkan hak privasi dengan kepentingan keamanan publik.
---

## 7. Jawaban Pertanyaan
1. HTTP tidak aman karena data dikirim plaintext, sedangkan HTTPS menggunakan TLS untuk enkripsi, integritas, dan autentikasi server.
2. Sertifikat digital memastikan identitas server dan mencegah serangan man-in-the-middle.
3. Kriptografi melindungi privasi, tetapi menimbulkan dilema antara keamanan publik dan hak individu.

---

## 8. Kesimpulan
TLS merupakan komponen penting dalam keamanan email dan e-commerce. Selain aspek teknis, penerapannya harus mempertimbangkan etika, privasi, dan regulasi.

---

## 9. Daftar Pustaka
 - Stallings, W. (2017). Cryptography and Network Security, Bab 15.

---

