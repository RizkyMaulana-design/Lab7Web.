# Laporan Praktikum 1: PHP Framework (CodeIgniter 4)

**Mata Kuliah:** Pemrograman Web 2  
**Dosen Pengampu:** Agung Nugroho, S.Kom., M.Kom., S.Kom., M. Kom

## Identitas Mahasiswa
* **Nama:** Rizky Maulana
* **NIM:** 312410430
* **Kelas:** I241C

---

## Daftar Isi
1. [Persiapan Konfigurasi PHP](#1-persiapan-konfigurasi-php)
2. [Instalasi CodeIgniter 4 Secara Manual](#2-instalasi-codeigniter-4-secara-manual)
3. [Menjalankan CLI (Command Line Interface)](#3-menjalankan-cli-command-line-interface)
4. [Mengaktifkan Mode Debugging](#4-mengaktifkan-mode-debugging)
5. [Memahami Struktur Direktori dan Konsep MVC](#5-memahami-struktur-direktori-dan-konsep-mvc)
6. [Routing dan Controller](#6-routing-dan-controller)
7. [Membuat View dan Layout Web dengan CSS](#7-membuat-view-dan-layout-web-dengan-css)

---

## 1. Persiapan Konfigurasi PHP
Sebelum memulai, dilakukan aktivasi beberapa ekstensi PHP pada webserver XAMPP yang dibutuhkan oleh CodeIgniter 4. Langkah-langkahnya:
* Membuka XAMPP Control Panel.
* Klik **Config** -> **PHP (php.ini)** pada baris Apache.
* Menghapus tanda titik koma (`;`) pada ekstensi berikut:
    - `extension=intl` (untuk multibahasa)
    - `extension=mbstring` (untuk bekerja dengan string)
    - `extension=curl` (untuk HTTP request)
* Menyimpan file dan melakukan restart pada Apache.

<img width="791" height="543" alt="php my ini" src="https://github.com/user-attachments/assets/1c42ddfe-6b4c-4db6-a675-3876e7765952" />

*Gambar 1.1: Aktivasi ekstensi intl dan mbstring pada file php.ini*

---

## 2. Instalasi CodeIgniter 4 Secara Manual
Proses instalasi dilakukan tanpa menggunakan composer:
* Mengunduh file framework dari [CodeIgniter.com](https://codeigniter.com/download).
* Mengekstrak file zip ke direktori `C:\xampp\htdocs\lab11_php_ci`.
* Mengubah nama folder utama menjadi `ci4`.
* Melakukan pengujian akses awal melalui URL: `http://localhost/lab11_php_ci/ci4/public/`.

<img width="906" height="427" alt="srukture folfer ci4" src="https://github.com/user-attachments/assets/4dae7551-5d84-4f9f-90bf-7adc8ca5b82f" />

*Gambar 2.1: Struktur folder project di dalam direktori htdocs*

---

## 3. Menjalankan CLI (Command Line Interface)
CodeIgniter 4 menyediakan tools berbasis baris perintah untuk mempermudah development.
* Membuka Terminal atau Command Prompt.
* Masuk ke direktori project: `cd htdocs\lab11_php_ci\ci4`.
* Menjalankan perintah: `php spark` untuk melihat daftar perintah yang tersedia.
* Perintah ini digunakan untuk menjalankan server lokal, generate kode, hingga migrasi database.

---

## 4. Mengaktifkan Mode Debugging
Fitur ini diaktifkan agar pesan error yang muncul saat pengembangan bersifat detail dan informatif.
* Mengubah nama file `env` pada root direktori menjadi `.env`.
* Mencari baris `# CI_ENVIRONMENT = production` dan mengubahnya menjadi:
  ```bash
  CI_ENVIRONMENT = development
  ```
* Hal ini akan mengubah tampilan error standard "Whoops!" menjadi halaman trace error yang lengkap.

<img width="686" height="518" alt="env" src="https://github.com/user-attachments/assets/3fc75231-1fcb-43d8-9e2d-c3fa82c12d38" />

*Gambar 4.1: Perubahan environment dari production ke development*

---

## 5. Memahami Struktur Direktori dan Konsep MVC
Sesuai modul, dipahami bahwa area kerja utama berada pada:
* **Folder `app`**: Berisi kode aplikasi (Controller, Model, View).
* **Folder `public`**: Berisi aset publik (index.php, CSS, Gambar, JS).
* **Konsep MVC**: Memisahkan logika proses (Controller), objek data (Model), dan tampilan interface (View).

---

## 6. Routing dan Controller
Mengatur rute URL aplikasi dan membuat logika penanganannya.

### Menambahkan Route Baru (`app/Config/Routes.php`)
```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

<img width="482" height="340" alt="code routes php" src="https://github.com/user-attachments/assets/0c0e2add-7313-4126-b145-6a1275e87646" />

*Gambar 6.1: Menambahkan route baru*

### Membuat Controller Page (`app/Controllers/Page.php`)
Membuat class `Page` untuk menangani request halaman statis:
```php
<?php
namespace App\Controllers;

class Page extends BaseController
{
    public function about() {
        return view('about', [
            'title' => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }
}
```

<img width="866" height="889" alt="screenshot code page php" src="https://github.com/user-attachments/assets/6232bb3d-f9ec-4dd0-8681-76026fc1ce1f" />

*Gambar 6.2: Penulisan logika Controller untuk memanggil view*

---

## 7. Membuat View dan Layout Web dengan CSS
Menerapkan desain yang konsisten menggunakan sistem template (Header dan Footer).

* **Folder Template**: Dibuat di `app/Views/template/` berisi `header.php` dan `footer.php` dengan gaya desain navigasi yang clean tanpa logo.
* **Aset CSS**: File `style.css` diletakkan di folder `public/` untuk mengatur layout navigasi, sidebar, dan konten utama.
* **Integrasi View**: Menggunakan fungsi `$this->include()` untuk menggabungkan bagian-bagian template.

<img width="237" height="279" alt="file footer dan header" src="https://github.com/user-attachments/assets/a27e24ff-13f2-4263-8eb2-6cee96e714d0" />

*Gambar 7.1: File header.php dan footer.php di folder Views/template*

### Contoh Implementasi View `about.php`:
```php
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```

<img width="783" height="370" alt="screen shoot hasil akhir" src="https://github.com/user-attachments/assets/4154de23-c8b8-4a87-8502-618ed43316de" />

*Gambar 7.2: Tampilan halaman About yang sudah rapi dengan CSS*

---
&copy; 2026 Rizky Maulana - NIM 312410430 | Universitas Pelita Bangsa

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


---
<div align="center">
<img width="231" height="53" alt="logo codelnighter" src="https://github.com/user-attachments/assets/d858d271-c130-4aee-ad86-b337c4185a03" />
  
  # 🎨 Laporan Praktikum 3: View Layout dan View Cell
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MVC](https://img.shields.io/badge/Layout-Inheritance-success?style=for-the-badge)
  ![Component](https://img.shields.io/badge/View-Cell-blue?style=for-the-badge)
</div>

---

## 📋 Daftar Isi
1. [🏗️ Konsep View Layout](#1-konsep-view-layout)
2. [🖼️ Membuat Layout Utama (Parent)](#2-membuat-layout-utama-parent)
3. [🧩 Implementasi Template Inheritance (Child)](#3-implementasi-template-inheritance-child)
4. [📱 Menampilkan Data Dinamis dengan View Cell](#4-menampilkan-data-dinamis-dengan-view-cell)
5. [📸 Hasil Akhir (Screenshot)](#5-hasil-akhir-screenshot)

---

## 1. 🏗️ Konsep View Layout
Pada praktikum ini, kita beralih dari penggunaan template parsial (menggunakan `include`) ke konsep **View Layout**.View Layout memungkinkan kita mendefinisikan satu kerangka utama (parent) dan halaman-halaman lain (child) hanya perlu mengisi bagian konten spesifiknya saja.Hal ini membuat kode lebih modular, mudah dipelihara, dan menghindari pengulangan kode header/footer yang sama[cite: 976].

---

## 2. 🖼️ Membuat Layout Utama (Parent)
Langkah awal adalah membuat file layout induk di direktori `app/Views/layout/main.php`.File ini berisi struktur HTML lengkap dengan placeholder `renderSection()` untuk menyisipkan konten dinamis.

### 🛠️ Kode Layout Utama (`app/Views/layout/main.php`)
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title ?? 'My Website' ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header><h1>Layout Sederhana</h1></header>
        <nav>
            <a href="<?= base_url('/'); ?>" class="active">Home</a>
            <a href="<?= base_url('/artikel'); ?>">Artikel</a>
            <a href="<?= base_url('/about'); ?>">About</a>
            <a href="<?= base_url('/contact'); ?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
                <?= $this->renderSection('content') ?> </section>
            <aside id="sidebar">
                <?= view_cell('\App\Libraries\Widget::artikel_terkini') ?>
                
                <div class="widget-box">
                    <h3 class="title">Widget Text</h3>
                    <p>Vestibulum lorem elit, iaculis in nisl volutpat, malesuada tincidunt arcu...</p>
                </div>
            </aside>
        </section>
        <footer><p>&copy; 2026 Rizky Maulana - Universitas Pelita Bangsa</p></footer>
    </div>
</body>
</html>
```

---

## 3. 🧩 Implementasi Template Inheritance (Child)
Setelah layout utama siap, halaman seperti **About** dimodifikasi agar menggunakan fungsi `extend()` untuk merujuk ke layout induk dan `section()` untuk mendefinisikan kontennya.

### 📄 Contoh Implementasi (`app/Views/about.php`)
```php
<?= $this->extend('layout/main') ?> <?= $this->section('content') ?>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
<?= $this->endSection() ?>
```

---

## 4. 📱 Menampilkan Data Dinamis dengan View Cell
**View Cell** digunakan untuk merender komponen UI kecil (seperti widget sidebar) yang bisa dipanggil di banyak tempat secara modular.

### 🛠️ Langkah Implementasi:
1. **Update Database:** Menambahkan field `waktu` pada tabel artikel untuk mendukung pengambilan data terbaru.
2. **Membuat Library Class:** Membuat kelas `Widget` di `app/Libraries/` untuk mengambil data 5 artikel terkini dari database.
3. **Membuat View Cell:** Membuat tampilan khusus di `app/Views/components/artikel_terkini.php`.

```php
<div class="widget-box">
    <h3 class="title">Artikel Terkini</h3>
    <ul>
        <?php foreach ($artikel as $row): ?>
            <li>
                <a href="<?= base_url('/artikel/' . $row['slug']) ?>">
                    <?= $row['judul'] ?>
                </a>
            </li>
        <?php endforeach; ?>
    </ul>
</div>
```

---

## 5. 📸 Hasil Akhir (Screenshot)

### 📌 Halaman Artikel dengan View Cell Sidebar

<img width="987" height="507" alt="implementasi praktikum 3" src="https://github.com/user-attachments/assets/d8e2c04d-375a-4e1a-8045-6bf0457907ca" />
*Gambar: Tampilan daftar artikel yang sudah menggunakan View Layout induk dan menampilkan widget "Artikel Terkini" di sidebar melalui View Cell.*

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | NIM: 312410430</b><br>
  <i>Laporan Praktikum Web 2 - Universitas Pelita Bangsa</i>
</div>
```

