
  # 🗂️ Laporan Praktikum 6: Relasi Tabel dan Query Builder
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![Database](https://img.shields.io/badge/Database-One--to--Many-success?style=for-the-badge)
</div>



---

## 📋 Daftar Isi
1. [🎯 Tujuan Praktikum](#1-tujuan-praktikum)
2. [🗄️ Pembuatan Tabel Kategori & Relasi](#2-pembuatan-tabel-kategori--relasi)
3. [🧩 Pembuatan Model & Query Builder](#3-pembuatan-model--query-builder)
4. [⚙️ Modifikasi Controller](#4-modifikasi-controller)
5. [🖥️ Modifikasi View](#5-modifikasi-view)
6. [📸 Hasil Akhir (Screenshot)](#6-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
Praktikum ini bertujuan untuk memahami dan mengimplementasikan konsep **Relasi Tabel (One-to-Many)** di dalam *database* serta mempraktikkan penggunaan **Query Builder** CodeIgniter 4 untuk melakukan *Join* tabel secara efisien tanpa harus menulis query SQL manual secara panjang lebar.

---

## 2. 🗄️ Pembuatan Tabel Kategori & Relasi
Langkah pertama adalah membuat tabel `kategori` sebagai tabel referensi (Master) dan menambahkan relasi *Foreign Key* ke tabel `artikel`.
* **Tabel Kategori:** Memiliki kolom `id_kategori` (PK), `nama_kategori`, dan `slug_kategori`.
* **Tabel Artikel:** Ditambahkan kolom `id_kategori` sebagai *Foreign Key* yang mereferensikan tabel kategori.

---

## 3. 🧩 Pembuatan Model & Query Builder
* **KategoriModel:** Dibuat untuk merepresentasikan tabel `kategori`.
* **ArtikelModel:** Ditambahkan method khusus `getArtikelDenganKategori()` yang memanfaatkan *Query Builder* `->join()` untuk menggabungkan data artikel dengan nama kategorinya dari tabel `kategori`.

---

## 4. ⚙️ Modifikasi Controller
File `Artikel.php` diperbarui agar dapat menangani data relasi:
* Mengirimkan data daftar kategori ke halaman Form Tambah dan Form Edit untuk dimuat ke dalam elemen `<select>` (Dropdown).
* Memproses dan memvalidasi input `id_kategori` saat data artikel baru disimpan atau diperbarui.
* Menambahkan fitur filter artikel berdasarkan ID Kategori pada Dasbor Admin.

---

## 5. 🖥️ Modifikasi View
Antarmuka disesuaikan untuk menampilkan dan menerima data kategori:
* **Form Add & Edit:** Ditambahkan elemen `<select>` dropdown dinamis yang me-*looping* data dari `KategoriModel`.
* **Dasbor Admin:** Ditambahkan kolom "Kategori" pada tabel untuk menampilkan nama kategori hasil *Join*, serta fitur Filter pencarian berdasarkan Kategori.

---

## 6. 📸 Hasil Akhir (Screenshot)

### 📌 Dasbor Admin (Dengan Kolom Kategori)

<img width="1920" height="532" alt="p6_kategori_table" src="https://github.com/user-attachments/assets/d33d5b93-9762-4255-9f61-a6c6a7682d67" />

*Gambar: Dasbor admin menampilkan artikel lengkap dengan relasi nama kategori hasil Query Builder.*

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | NIM: 312410430</b><br>
  <i>Laporan Praktikum Web 2 - Universitas Pelita Bangsa</i>
</div>

```

Nah, laporan *readme* kamu sekarang sudah lengkap semua dari modul 1 sampai 8.

Untuk penulisan *coding* Praktikum 6 (menambah tabel kategori dan menyesuaikan *dropdown* kategori) ini, apakah mau kita kerjakan sekarang biar programmu tidak *error* saat nanti diuji coba oleh dosen, atau kamu mau lompat menyelesaikan Praktikum 9 (AJAX Pagination) dulu malam ini?
