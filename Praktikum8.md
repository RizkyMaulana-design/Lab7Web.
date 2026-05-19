
<div align="center">
  <img src="https://codeigniter.com/assets/images/ci-logo-big.png" alt="CodeIgniter 4 Logo" width="150"/>
  
  # ⚡ Laporan Praktikum 8: Implementasi AJAX
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white)
  ![AJAX](https://img.shields.io/badge/AJAX-Dynamic-success?style=for-the-badge)
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
2. [⚙️ Instalasi jQuery Offline](#2-instalasi-jquery-offline)
3. [🚀 Pembuatan AjaxController](#3-pembuatan-ajaxcontroller)
4. [🖥️ Modifikasi View & Logika AJAX](#4-modifikasi-view--logika-ajax)
5. [📸 Hasil Akhir (Screenshot)](#5-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
[cite_start]Praktikum ini bertujuan untuk memahami dan mengimplementasikan konsep **AJAX (Asynchronous JavaScript and XML)**[cite: 209]. [cite_start]Dengan AJAX, aplikasi web dapat memperbarui dan menampilkan data dari server tanpa harus melakukan *reload* halaman secara keseluruhan, sehingga aplikasi terasa lebih responsif, dinamis, dan menghemat *bandwidth*[cite: 211, 212, 230].

---

## 2. ⚙️ Instalasi jQuery Offline
[cite_start]Untuk menangani *request* AJAX secara praktis, pustaka jQuery versi `3.6.0.min.js` diunduh dan disimpan secara lokal di dalam direktori proyek[cite: 242, 243].
* [cite_start]Lokasi penyimpanan: `public/assets/js/jquery-3.6.0.min.js`[cite: 243].
* [cite_start]Pemanggilan pada View: `<script src="<?= base_url('assets/js/jquery-3.6.0.min.js') ?>"></script>`[cite: 294].

---

## 3. 🚀 Pembuatan AjaxController
[cite_start]Dibuat sebuah controller khusus (`AjaxController.php`) untuk menangani *request* di belakang layar[cite: 246, 253].
* [cite_start]`getData()`: Mengambil data dari `ArtikelModel` dan mengembalikannya dalam format JSON menggunakan `$this->response->setJSON($data)`[cite: 259, 268].
* [cite_start]`delete($id)`: Menghapus data spesifik berdasarkan ID dan mengembalikan status konfirmasi dalam format JSON[cite: 270, 273, 278].

---

## 4. 🖥️ Modifikasi View & Logika AJAX
[cite_start]Pemanggilan AJAX dilakukan menggunakan metode `$.ajax()` dari jQuery[cite: 309].
* [cite_start]**Read Data:** Menggunakan *method* `GET` ke *endpoint* `/ajax/getdata` untuk merender tabel secara asinkron saat halaman dimuat[cite: 313, 314].
* **Delete Data:** Menerapkan *event listener* pada tombol kelas `.btn-delete`. [cite_start]Jika diklik, sistem akan mengirim *request* `DELETE` ke *endpoint* `/ajax/delete/id`[cite: 339, 349]. [cite_start]Apabila berhasil, fungsi `loadData()` akan dipanggil kembali untuk memuat ulang isi tabel tanpa me-*refresh* halaman[cite: 351].

---

## 5. 📸 Hasil Akhir (Screenshot)

### 📌 Keberhasilan Hapus Data via AJAX
![Penghapusan Data AJAX](screenshots/p8_ajax_delete_success.png)
*Gambar: Baris data (ID 3) berhasil dihapus dari database dan tabel diperbarui secara asinkron tanpa memuat ulang (refresh) halaman browser.*

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | NIM: 312410430</b><br>
  <i>Laporan Praktikum Web 2 - Universitas Pelita Bangsa</i>
</div>

```

