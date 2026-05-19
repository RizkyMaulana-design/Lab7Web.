




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


