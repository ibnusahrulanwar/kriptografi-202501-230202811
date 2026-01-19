# Laporan Praktikum Kriptografi
Minggu ke-: 13
Topik: Tinycoin 
Nama: Ibnu Sahrul Anwar
NIM: 230202811
Kelas: 5IKKA

---

## 1. Tujuan
1. Menjelaskan peran hash function dalam blockchain.
2. Melakukan simulasi sederhana Proof of Work (PoW).
3. Menganalisis keamanan cryptocurrency berbasis kriptografi.

---

## 2. Dasar Teori
TinyChain adalah model blockchain sederhana yang digunakan untuk menjelaskan prinsip dasar teknologi blockchain, seperti struktur blok, fungsi hash kriptografis, dan mekanisme konsensus. Setiap blok memuat transaksi, hash blok sebelumnya, dan nonce, sehingga keterkaitan hash antarblok menciptakan sifat immutability, di mana perubahan satu blok memengaruhi seluruh rantai.

Proof of Work (PoW) pada TinyChain berfungsi sebagai mekanisme konsensus dengan mengharuskan node mencari nilai nonce yang menghasilkan hash sesuai tingkat kesulitan tertentu. Mekanisme ini memanfaatkan sifat satu arah fungsi hash, sehingga validasi mudah dilakukan tetapi pemalsuan data memerlukan biaya komputasi tinggi.

Secara konseptual, TinyChain menunjukkan bahwa keamanan blockchain dibangun dari kriptografi dan komputasi terdistribusi, bukan kepercayaan pada otoritas tunggal. Walaupun sederhana, TinyChain efektif untuk memahami desentralisasi serta trade-off antara keamanan, efisiensi, dan skalabilitas.


---

## 3. Alat dan Bahan
- Python 3.1
- Visual Studio Code
- Git dan akun GitHub 
---

## 4. Langkah Percobaan
1. Membuat Struktur Blok
2. Membuat Blockchain
3. Analisis Proof of Work

---

## 5. Source Code
1. Blok
    import hashlib
    import time

    class Block:
    def __init__(self, index, previous_hash, data, timestamp=None):
        self.index = index
        self.timestamp = timestamp or time.time()
        self.data = data
        self.previous_hash = previous_hash
        self.nonce = 0
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        value = str(self.index) + str(self.timestamp) + str(self.data) + str(self.previous_hash) + str(self.nonce)
        return hashlib.sha256(value.encode()).hexdigest()

    def mine_block(self, difficulty):
        while self.hash[:difficulty] != "0" * difficulty:
            self.nonce += 1
            self.hash = self.calculate_hash()
        print(f"Block mined: {self.hash}")
2. Blockchain
    class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.difficulty = 4

    def create_genesis_block(self):
        return Block(0, "0", "Genesis Block")

    def get_latest_block(self):
        return self.chain[-1]

    def add_block(self, new_block):
        new_block.previous_hash = self.get_latest_block().hash
        new_block.mine_block(self.difficulty)
        self.chain.append(new_block)

        # Uji coba blockchain
        my_chain = Blockchain()
        print("Mining block 1...")
        my_chain.add_block(Block(1, "", "Transaksi A → B: 10 Coin"))

        print("Mining block 2...")
        my_chain.add_block(Block(2, "", "Transaksi B → C: 5 Coin"))
```

## 6. Hasil dan Pembahasan
pada kode <Block> yang sebelum diubah,output tidak muncul karena metode mine_block() tidak pernah dipanggil. Class hanyalah blueprint; tanpa instansiasi dan pemanggilan metode, tidak ada proses yang berjalan dan tidak ada output yang dicetak.

---

## 7. Jawaban Pertanyaan
1. Tanpa fungsi hash, blockchain hanyalah daftar data biasa. Hash menjadikannya struktur data yang aman secara kriptografis, bukan sekadar database terdistribusi.
2. PoW mencegah double spending bukan dengan larangan langsung, tetapi dengan membuat kecurangan menjadi tidak rasional secara ekonomi.
3. PoW kuat secara keamanan, tetapi lemah secara efisiensi energi, sehingga memicu lahirnya alternatif seperti Proof of Stake (PoS) yang mengalihkan keamanan dari energi ke kepemilikan aset.
---

## 8. Kesimpulan
Implementasi dasar blockchain dengan Proof of Work, di mana setiap blok ditambang menggunakan hash SHA-256 hingga memenuhi tingkat kesulitan tertentu. Proses ini memastikan integritas data melalui keterkaitan hash antarblok, sehingga cocok sebagai simulasi sederhana untuk konsep mining dan keamanan blockchain.
---

## 9. Daftar Pustaka
- Stallings (2017), Bab 16.
- Stinson (2019), Bab 8.

---

## 10. Commit Log

commit : week13-tinytchain
Author: Ibnu Sahrul Anwar <benuibnuanwar@gmail.com>
Date:   2026-01-19
