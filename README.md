# 🚀 SQL Cheatsheet untuk Pemula

Panduan praktis untuk belajar SQL dari dasar hingga mahir. Cheatsheet ini dirancang khusus untuk pemula dengan contoh yang mudah dipahami.

![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)

## 📑 Daftar Isi
- [Dasar Query SQL](#dasar-query-sql)
- [Memanipulasi Data](#memanipulasi-data)
- [Fungsi Agregat](#fungsi-agregat)
- [Menghubungkan Tabel (JOIN)](#menghubungkan-tabel-join)
- [View](#view)
- [Manajemen Tabel](#manajemen-tabel)
- [Indeks](#indeks)
- [Fungsi Lanjutan](#fungsi-lanjutan)

## 🎯 Dasar Query SQL

### SELECT - Mengambil Data
```sql
-- Mengambil semua kolom
SELECT * FROM nama_tabel;

-- Mengambil kolom tertentu
SELECT nama, email FROM pengguna;

-- Mengambil data unik (tanpa duplikat)
SELECT DISTINCT kota FROM pelanggan;
```

### WHERE - Memfilter Data
```sql
-- Filter dasar
SELECT * FROM produk WHERE harga > 100000;

-- Kombinasi filter
SELECT * FROM pesanan 
WHERE status = 'pending' 
AND tanggal >= '2024-01-01';

-- Mencari dalam rentang
SELECT * FROM produk 
WHERE harga BETWEEN 100000 AND 500000;

-- Mencari dengan beberapa nilai
SELECT * FROM kategori 
WHERE nama IN ('Elektronik', 'Fashion', 'Makanan');
```

### ORDER BY - Mengurutkan Data
```sql
-- Urut naik (ascending)
SELECT * FROM produk ORDER BY harga ASC;

-- Urut turun (descending)
SELECT * FROM produk ORDER BY harga DESC;

-- Multiple ordering
SELECT * FROM pesanan 
ORDER BY tanggal DESC, total_harga ASC;
```

### LIMIT - Membatasi Hasil
```sql
-- Mengambil 5 data teratas
SELECT * FROM produk LIMIT 5;

-- Mengambil data dengan offset
SELECT * FROM produk LIMIT 10 OFFSET 5;  -- Skip 5 data pertama
```

## 💾 Memanipulasi Data

### INSERT - Menambah Data
```sql
-- Menambah satu data
INSERT INTO produk (nama, harga, stok) 
VALUES ('Laptop Gaming', 15000000, 10);

-- Menambah multiple data
INSERT INTO kategori (nama) VALUES 
('Elektronik'),
('Fashion'),
('Makanan');
```

### UPDATE - Mengubah Data
```sql
-- Update satu kolom
UPDATE produk 
SET harga = 16000000 
WHERE id = 1;

-- Update multiple kolom
UPDATE pengguna 
SET 
    nama = 'John Doe',
    email = 'john@example.com'
WHERE id = 1;
```

### DELETE - Menghapus Data
```sql
-- Hapus data tertentu
DELETE FROM produk WHERE id = 1;

-- Hapus semua data
DELETE FROM temp_log;  -- Hati-hati menggunakan ini!
```

## 📊 Fungsi Agregat

```sql
-- Menghitung jumlah data
SELECT COUNT(*) FROM pesanan;

-- Menghitung total
SELECT SUM(total_harga) FROM pesanan;

-- Rata-rata
SELECT AVG(harga) FROM produk;

-- Nilai minimum dan maksimum
SELECT 
    MIN(harga) as harga_terendah,
    MAX(harga) as harga_tertinggi
FROM produk;

-- Grouping data
SELECT 
    kategori_id,
    COUNT(*) as jumlah_produk,
    AVG(harga) as rata_rata_harga
FROM produk
GROUP BY kategori_id;
```

## 🔄 Menghubungkan Tabel (JOIN)

### INNER JOIN
```sql
-- Menggabungkan data yang cocok dari kedua tabel
SELECT 
    p.nama as nama_produk,
    k.nama as kategori
FROM produk p
INNER JOIN kategori k ON p.kategori_id = k.id;
```

### LEFT JOIN
```sql
-- Mengambil semua data dari tabel kiri
SELECT 
    p.nama as nama_produk,
    k.nama as kategori
FROM produk p
LEFT JOIN kategori k ON p.kategori_id = k.id;
```

## 👁️ View

```sql
-- Membuat view
CREATE VIEW produk_kategori AS
SELECT 
    p.nama as nama_produk,
    k.nama as kategori,
    p.harga
FROM produk p
JOIN kategori k ON p.kategori_id = k.id;

-- Menggunakan view
SELECT * FROM produk_kategori;
```

## 📝 Manajemen Tabel

### Membuat Tabel
```sql
CREATE TABLE produk (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nama VARCHAR(100) NOT NULL,
    harga DECIMAL(10,2) NOT NULL,
    stok INT DEFAULT 0,
    kategori_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (kategori_id) REFERENCES kategori(id)
);
```

### Mengubah Struktur Tabel
```sql
-- Menambah kolom
ALTER TABLE produk ADD deskripsi TEXT;

-- Mengubah tipe data kolom
ALTER TABLE produk MODIFY harga DECIMAL(12,2);

-- Menghapus kolom
ALTER TABLE produk DROP COLUMN deskripsi;
```

## 🔍 Indeks

```sql
-- Membuat indeks
CREATE INDEX idx_nama ON produk(nama);

-- Membuat indeks unik
CREATE UNIQUE INDEX idx_email ON pengguna(email);
```

## 🔥 Fungsi Lanjutan

### Subquery
```sql
-- Subquery dalam SELECT
SELECT nama, harga,
    (SELECT AVG(harga) FROM produk) as rata_rata_harga
FROM produk;

-- Subquery dalam WHERE
SELECT * FROM produk 
WHERE harga > (SELECT AVG(harga) FROM produk);
```

### Transaction
```sql
-- Memulai transaksi
START TRANSACTION;

-- Operasi database
INSERT INTO pesanan (...) VALUES (...);
UPDATE produk SET stok = stok - 1 WHERE id = 1;

-- Jika sukses
COMMIT;

-- Jika gagal
ROLLBACK;
```

## 📚 Tips untuk Pemula

1. **Mulai dari Yang Sederhana**
   - Kuasai SELECT, WHERE, dan JOIN dasar terlebih dahulu
   - Praktikkan query sederhana sebelum mencoba yang kompleks

2. **Gunakan Indentasi**
   - Buat query mudah dibaca dengan indentasi yang rapi
   - Pisahkan bagian query dengan baris baru

3. **Backup Data**
   - Selalu backup data sebelum melakukan operasi UPDATE atau DELETE
   - Gunakan WHERE untuk memastikan operasi tepat sasaran

4. **Optimasi Query**
   - Hindari SELECT * jika tidak perlu semua kolom
   - Gunakan indeks untuk kolom yang sering dicari
   - Batasi hasil dengan LIMIT untuk data besar

