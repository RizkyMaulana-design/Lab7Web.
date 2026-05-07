# Laporan Praktikum 1: PHP Framework (CodeIgniter 4)

**Mata Kuliah:** Pemrograman Web 2  
**Dosen Pengampu:** Donny Maulana, S.Kom., M.M.S.I.

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
