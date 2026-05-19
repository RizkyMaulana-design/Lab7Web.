<div align="center">
<img width="231" height="53" alt="logo codelnighter" src="https://github.com/user-attachments/assets/eb540cac-7cf9-4920-ac29-4fb695b3a0f3" />
  
  # 🚀 Laporan Praktikum 2: Framework Lanjutan (CRUD)
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
</div>

---

## 📋 Daftar Isi
1. [🛠️ Persiapan Database](#1-persiapan-database)
2. [🔗 Konfigurasi Koneksi Database](#2-konfigurasi-koneksi-database)
3. [🧩 Membuat Model](#3-membuat-model)
4. [🎮 Membuat Controller (CRUD)](#4-membuat-controller-crud)
5. [🖥️ Membuat View (Antarmuka)](#5-membuat-view-antarmuka)
6. [🛣️ Konfigurasi Routing](#6-konfigurasi-routing)
7. [📸 Hasil Akhir (Screenshot)](#7-hasil-akhir-screenshot)

---

## 1. 🛠️ Persiapan Database
[cite_start]Langkah pertama adalah membuat database `lab_ci4` dan tabel `artikel` di MySQL untuk menyimpan data portal berita [cite: 1007-1018].

```sql
CREATE DATABASE lab_ci4;

USE lab_ci4;

CREATE TABLE artikel (
    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```
> 💡 *Catatan: Data pancingan (dummy data) disisipkan menggunakan perintah INSERT INTO melalui Command Prompt .*

---

## 2. 🔗 Konfigurasi Koneksi Database
Menghubungkan aplikasi CodeIgniter 4 dengan database MySQL menggunakan file `.env` .

```env
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
database.default.port     = 3307
```
> 🔴 **Penting:** Port diubah menjadi `3307` sesuai dengan konfigurasi XAMPP lokal.

---

## 3. 🧩 Membuat Model
Membuat file `ArtikelModel.php` di folder `app/Models/` untuk berinteraksi dengan tabel `artikel` .

```php
<?php
namespace App\Models;
use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```

---

## 4. 🎮 Membuat Controller (CRUD)
Membuat file `Artikel.php` di folder `app/Controllers/` yang menangani seluruh logika bisnis CRUD :

* **Read (Halaman Publik & Detail):** Method `index()` dan `view($slug)`.
* **Read (Halaman Admin):** Method `admin_index()` untuk menampilkan data di tabel admin.
* **Create (Tambah Data):** Method `add()` menggunakan fungsi validasi input.
* **Update (Ubah Data):** Method `edit($id)` untuk memperbarui record berdasarkan ID .
* **Delete (Hapus Data):** Method `delete($id)` untuk menghapus record .

---

## 5. 🖥️ Membuat View (Antarmuka)
Membangun antarmuka pengguna di folder `app/Views/artikel/` yang dipadukan dengan template Header dan Footer :

* `index.php`: Menampilkan daftar artikel untuk pengunjung.
* `detail.php`: Menampilkan isi artikel secara penuh.
* `admin_index.php`: Tabel dasbor admin (lengkap dengan tombol Ubah dan Hapus).
* `form_add.php`: Formulir untuk menambah artikel baru.
* `form_edit.php`: Formulir yang terisi otomatis untuk mengubah data artikel.

---

## 6. 🛣️ Konfigurasi Routing
[cite_start]Mendaftarkan rute di `app/Config/Routes.php` agar URL menjadi bersih (SEO Friendly) dan dikelompokkan dengan metode Grouping untuk halaman admin [cite: 1190, 1270-1276].

```php
$routes->get('/artikel', 'Artikel::index');
$routes->get('/artikel/(:any)', 'Artikel::view/$1');

$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

---

## 7. 📸 Hasil Akhir (Screenshot)

### 📌 Tampilan Halaman Publik (Daftar Artikel)
<img width="875" height="476" alt="daftar artikel" src="https://github.com/user-attachments/assets/02d9e1ec-7280-4373-a7ae-7fa81d97203e" />

### 📌 Tampilan Detail Artikel
<img width="1367" height="358" alt="detail artikel" src="https://github.com/user-attachments/assets/ca9faebd-8b00-4e1d-8b6d-b5140de92964" />

### 📌 Tampilan Dasbor Admin
<img width="361" height="285" alt="admin artikel" src="https://github.com/user-attachments/assets/e43a8c09-33aa-468d-bac0-19476fd7e68c" />

### 📌 Tampilan Form Tambah & Edit

<img width="527" height="359" alt="admin form" src="https://github.com/user-attachments/assets/4088ac11-c067-4203-a23f-c26dd7ce84ec" />

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | Universitas Pelita Bangsa</b><br>
  <i>Dibuat dengan 💻 dan ☕ untuk Tugas Pemrograman Web 2</i>
</div>
