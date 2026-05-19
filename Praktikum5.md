
<div align="center">
  <img src="https://codeigniter.com/assets/images/ci-logo-big.png" alt="CodeIgniter 4 Logo" width="150"/>
  
  # 🔍 Laporan Praktikum 5: Paginasi & Pencarian (Search)
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![UI/UX](https://img.shields.io/badge/Pagination_&_Search-success?style=for-the-badge)
</div>

---

## 👨‍💻 Identitas Mahasiswa
* **Nama:** Rizky Maulana
* **NIM:** 312410430
* **Kelas:** I241C
* **Mata Kuliah:** Pemrograman Web 2
* **Dosen Pengampu:** Donny Maulana, S.Kom., M.M.S.I.

---

## 📋 Daftar Isi
1. [🎯 Tujuan Praktikum](#1-tujuan-praktikum)
2. [⚙️ Modifikasi Controller (Search & Paginate)](#2-modifikasi-controller-search--paginate)
3. [🖥️ Modifikasi View (Form Pencarian & Navigasi)](#3-modifikasi-view-form-pencarian--navigasi)
4. [📸 Hasil Akhir (Screenshot)](#4-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
Pada praktikum ini, fitur website portal berita dikembangkan agar lebih *user-friendly* dan optimal dalam menangani data berskala besar. Dua fitur utama yang ditambahkan adalah:
* **Fitur Pencarian (Search):** Memungkinkan pengguna mencari artikel spesifik berdasarkan kata kunci yang ada pada Judul atau Isi artikel.
* **Paginasi (Pagination):** Membatasi jumlah artikel yang ditampilkan dalam satu halaman untuk mempercepat *loading* (dalam praktikum ini dibatasi 2 artikel per halaman) dan membaginya ke dalam beberapa halaman.

---

## 2. ⚙️ Modifikasi Controller (Search & Paginate)
Logika pencarian dan pembagian halaman ditangani sepenuhnya di dalam `Artikel.php` menggunakan fitur bawaan CodeIgniter 4 yaitu `$model->paginate()` dan `$model->like()`.

### 🎮 Cuplikan Logika (`app/Controllers/Artikel.php`)
```php
public function index()
{
    $model = new \App\Models\ArtikelModel();
    
    // 1. Logika Pencarian
    $q = $this->request->getVar('q') ?? '';
    if ($q) {
        $model->like('judul', $q)->orLike('isi', $q);
    }

    // 2. Logika Paginasi (Batas: 2 Data per Halaman)
    $data = [
        'title'   => 'Daftar Artikel',
        'artikel' => $model->paginate(2, 'artikel'),
        'pager'   => $model->pager,
        'q'       => $q
    ];

    return view('artikel/index', $data);
}

```

---

## 3. 🖥️ Modifikasi View (Form Pencarian & Navigasi)

Menambahkan elemen antarmuka berupa `<form>` pencarian menggunakan metode `GET` dan merender tombol navigasi halaman menggunakan objek `$pager`.

### 📄 Cuplikan Tampilan (`app/Views/artikel/index.php`)

```php
<form method="get" style="margin-bottom: 20px;">
    <input type="text" name="q" value="<?= esc($q); ?>" placeholder="Cari artikel...">
    <button type="submit" class="btn">Cari</button>
</form>

<?php foreach($artikel as $row): ?>
    <?php endforeach; ?>

<div style="margin-top: 20px;">
    <?= $pager->links('artikel', 'default_full') ?>
</div>

```

---

## 4. 📸 Hasil Akhir (Screenshot)

### 📌 Halaman Publik dengan Pencarian dan Paginasi


<img width="926" height="602" alt="p5_pagination_search" src="https://github.com/user-attachments/assets/bcfbe704-2b65-46b8-88dd-1f1cc2f676b2" />


---

