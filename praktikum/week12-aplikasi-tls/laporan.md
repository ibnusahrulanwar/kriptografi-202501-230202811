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
- Python 3.x 
- Web browser untuk menguji koneksi HTTPS
- OpenSSL / sertifikat TLS
- VS Code
---

## 4. Langkah Percobaan
1. Membuat server sederhana yang menggunakan TLS (menggunakan Python + OpenSSL).
2. Membuat sertifikat TLS menggunakan openssl untuk server.
3. Mengonfigurasi server agar menerima koneksi TLS.
4. Mengakses server melalui browser atau klien TLS lain untuk melihat koneksi terenkripsi (HTTPS).
5. Mencatat hasil koneksi dan validasi sertifikat.

---

## 5. Source Code
import ssl
import socket

context = ssl.SSLContext(ssl.PROTOCOL_TLS_SERVER)
context.load_cert_chain(certfile="server.pem", keyfile="server.key")

with socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0) as sock:
    sock.bind(('127.0.0.1', 8443))
    sock.listen(5)
    print("TLS Server running on https://localhost:8443")

    with context.wrap_socket(sock, server_side=True) as ssock:
        conn, addr = ssock.accept()
        print("Client connected:", addr)
        conn.send(
            b"HTTP/1.1 200 OK\r\n"
            b"Content-Type: text/plain\r\n\r\n"
            b"Hello, this connection is secured with TLS"
        )
        conn.close()


---

## 6. Hasil dan Pembahasan
-
---

## 7. Jawaban Pertanyaan
- Pertanyaan 1: Apa fungsi utama TLS?
Jawaban: TLS berfungsi untuk mengamankan komunikasi data dengan menyediakan enkripsi, autentikasi, dan integritas data antara client dan server.
- Pertanyaan 2: Sebutkan contoh penerapan TLS dalam kehidupan sehari-hari.
Jawaban: TLS digunakan pada HTTPS (website aman), email (SMTP/IMAP), VPN, API web, dan aplikasi pesan instan.
---

## 8. Kesimpulan
-

---

## 9. Daftar Pustaka
(Cantumkan referensi yang digunakan.  
Contoh:  
- Katz, J., & Lindell, Y. *Introduction to Modern Cryptography*.  
- Stallings, W. *Cryptography and Network Security*.  )

---

