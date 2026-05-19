
  # 📸 Laporan Praktikum 7: Fitur Upload Gambar pada Artikel
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![Backend](https://img.shields.io/badge/File-Upload-blue?style=for-the-badge)
</div>

---

## 📋 Daftar Isi
1. [🎯 Tujuan Praktikum](#1-tujuan-praktikum)
2. [🗄️ Perubahan Struktur Database & Model](#2-perubahan-struktur-database--model)
3. [📝 Modifikasi Form Tambah Artikel (Multipart Data)](#3-modifikasi-form-tambah-artikel-multipart-data)
4. [⚙️ Logika Validasi & Pemindahan File di Controller](#4-logika-validasi--pemindahan-file-di-controller)
5. [🖥️ Menampilkan Gambar di Sisi Admin dan Publik](#5-menampilkan-gambar-di-sisi-admin-dan-publik)
6. [📸 Hasil Akhir (Screenshot)](#6-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
Praktikum ini berfokus pada pengembangan fitur penanganan berkas (*file handling*), yaitu memberikan kemampuan bagi Administrator untuk mengunggah berkas gambar ilustrasi saat membuat artikel baru. Berkas yang diunggah akan divalidasi, diubah namanya secara acak (untuk menghindari duplikasi), disimpan ke dalam direktori server lokal, dan nama berkasnya dicatat ke dalam database.

---

## 2. 🗄️ Perubahan Struktur Database & Model

### 🗜️ SQL Alter Table
Menambahkan kolom `gambar` ke dalam tabel `artikel` setelah kolom `slug`:
```sql
ALTER TABLE artikel ADD gambar VARCHAR(255) NULL AFTER slug;

```

### 🧩 Pembaruan Model (`app/Models/ArtikelModel.php`)

Mendaftarkan properti `'gambar'` ke dalam array `$allowedFields` agar diizinkan oleh sistem keamanan *Mass Assignment* CodeIgniter 4.

```php
protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];

```

---

## 3. 📝 Modifikasi Form Tambah Artikel (Multipart Data)

Agar formulir HTML dapat mengirimkan berkas biner (gambar), atribut `enctype="multipart/form-data"` wajib disisipkan ke dalam tag `<form>` pada file `app/Views/artikel/form_add.php`.

```html
<form action="" method="post" enctype="multipart/form-data">
    <p>
        <label><b>Upload Gambar Ilustrasi:</b></label><br><br>
        <input type="file" name="gambar">
    </p>
    <p><input type="submit" value="Kirim Artikel" class="btn btn-large"></p>
</form>

```

---

## 4. ⚙️ Logika Validasi & Pemindahan File di Controller

Proses penangkapan berkas dilakukan menggunakan method `$this->request->getFile('gambar')`. Jika berkas valid, namanya akan diacak menggunakan `$file->getRandomName()` dan dipindahkan ke folder target `public/uploads/`.

### 🎮 Cuplikan Logika `app/Controllers/Artikel.php`

```php
$file = $this->request->getFile('gambar');
$fileName = '';

if ($file && $file->isValid() && !$file->hasMoved()) {
    $fileName = $file->getRandomName();
    $file->move(ROOTPATH . 'public/uploads', $fileName);
}

$artikel->insert([
    'judul'  => $this->request->getPost('judul'),
    'isi'    => $this->request->getPost('isi'),
    'slug'   => url_title($this->request->getPost('judul'), '-', true),
    'gambar' => $fileName,
]);

```

---

## 5. 🖥️ Menampilkan Gambar di Sisi Admin dan Publik

### 🛠️ Pada Dashboard Admin (`admin_index.php`)

Gambar ditampilkan dalam bentuk *thumbnail* kecil (ukuran lebar 100px) menggunakan fungsi pembantu `base_url('uploads/' . $row['gambar'])`. Jika artikel tidak memiliki gambar, sistem akan menampilkan teks alternatif secara dinamis.

### 🌐 Pada Halaman Publik (`index.php` & `detail.php`)

Gambar dirender secara dinamis di atas teks konten dengan properti CSS yang responsif (`max-width: 100%; height: auto;`) agar proporsional di berbagai ukuran layar device.

---

## 6. 📸 Hasil Akhir (Screenshot)

### 📌 Upload Sukses & Tampil di Tabel Dashboard Admin


<img width="1920" height="553" alt="Upload foto" src="https://github.com/user-attachments/assets/e56cf2f5-da3a-4acf-be57-a6db683b9334" />

---



