  
  # 🚀 Laporan Praktikum 9: Implementasi AJAX Pagination dan Search
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white)
  ![AJAX](https://img.shields.io/badge/AJAX-Asynchronous-success?style=for-the-badge)
</div>


---

## 📋 Daftar Isi
1. [🎯 Tujuan Praktikum](#1-tujuan-praktikum)
2. [⚙️ Modifikasi Controller (Backend JSON)](#2-modifikasi-controller-backend-json)
3. [🖥️ Modifikasi View (Frontend jQuery)](#3-modifikasi-view-frontend-jquery)
4. [🎨 Styling CSS Pagination](#4-styling-css-pagination)
5. [📸 Hasil Akhir (Screenshot)](#5-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
Praktikum ini bertujuan untuk menyempurnakan fitur *Dashboard Admin* dengan menerapkan **AJAX (Asynchronous JavaScript and XML)** pada fitur pencarian (*Search*), filter kategori, dan navigasi halaman (*Pagination*). Dengan pendekatan ini, aplikasi dapat mengambil dan merender data baru dari *server* secara *real-time* tanpa perlu melakukan *refresh* atau memuat ulang keseluruhan halaman web, sehingga memberikan pengalaman pengguna (UX) yang sangat responsif dan modern.

---

## 2. ⚙️ Modifikasi Controller (Backend JSON)
File `app/Controllers/Artikel.php` (khususnya *method* `admin_index`) dimodifikasi untuk dapat mendeteksi jenis *request* yang masuk:
* Jika *request* berasal dari AJAX (`$this->request->isAJAX()`), maka *controller* akan merespons dengan mengembalikan data dalam format **JSON** (`return $this->response->setJSON($data)`).
* Data JSON yang dikirim mencakup array artikel hasil *Query Builder* dan juga struktur HTML murni untuk tombol *pagination* bawaan CI4 (`$pager->links('artikel', 'default_full')`).
* Batas data per halaman diatur menjadi 2 baris (`paginate(2)`) agar fungsi *pagination* dapat langsung diuji coba.

---

## 3. 🖥️ Modifikasi View (Frontend jQuery)
File `app/Views/artikel/admin_index.php` dirombak total menggunakan DOM manipulation dengan jQuery:
* **Fungsi `fetchData(url)`:** Bertugas menembak *endpoint URL* ke *controller* dan mengambil balasan JSON. Selama proses berjalan, indikator *"Memuat data..."* ditampilkan.
* **Fungsi `renderArticles()` & `renderPagination()`:** Mengurai data JSON yang diterima, membangun ulang struktur tabel HTML secara dinamis, dan menempelkan tombol *pagination* ke dalam layar.
* **Event Listener:** Diimplementasikan pada *form search* (saat di-*submit*), *dropdown* kategori (saat nilainya diubah / *on change*), dan tautan nomor halaman (menggunakan *Event Delegation* pada `.pagination a`) untuk memicu fungsi `fetchData` tanpa me-*reload* *browser*.

---

## 4. 🎨 Styling CSS Pagination
Agar tombol navigasi halaman yang dikirim dari *server* tampil rapi dan profesional, ditambahkan gaya CSS internal menggunakan *Flexbox* (`display: flex; gap: 5px;`) sehingga elemen `<ul>` dan `<li>` bawaan CI4 berubah menjadi deretan tombol kotak yang menyamping dan memiliki efek *hover*.

---

## 5. 📸 Hasil Akhir (Screenshot)

### 📌 Implementasi AJAX Pagination & Search Berhasil

<img width="1920" height="605" alt="p9_ajax_pagination" src="https://github.com/user-attachments/assets/b4dbfbbc-df85-4b0a-81df-6f7c813c9597" />

*Gambar: Halaman Dasbor Admin berhasil merender data terbatas (2 baris) dan memunculkan tombol pagination berderet rapi yang berfungsi secara asinkron.*

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | NIM: 312410430</b><br>
  <i>Tugas Akhir Praktikum Web 2 - Universitas Pelita Bangsa</i>
</div>

```

