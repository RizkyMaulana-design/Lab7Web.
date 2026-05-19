
<div align="center">
  <img src="https://codeigniter.com/assets/images/ci-logo-big.png" alt="CodeIgniter 4 Logo" width="150"/>
  
  # ⚡ Laporan Praktikum 8: Implementasi AJAX
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white)
  ![AJAX](https://img.shields.io/badge/AJAX-Dynamic-success?style=for-the-badge)
</div>

---

## 📋 Daftar Isi
1. [🎯 Tujuan Praktikum](#1-tujuan-praktikum)
2. [⚙️ Instalasi jQuery Offline](#2-instalasi-jquery-offline)
3. [🚀 Pembuatan AjaxController](#3-pembuatan-ajaxcontroller)
4. [🖥️ Modifikasi View & Logika AJAX](#4-modifikasi-view--logika-ajax)
5. [📸 Hasil Akhir (Screenshot)](#5-hasil-akhir-screenshot)

---

## 1. 🎯 Tujuan Praktikum
Praktikum ini bertujuan untuk memahami dan mengimplementasikan konsep **AJAX (Asynchronous JavaScript and XML)**[cite: 209]. [cite_start]Dengan AJAX, aplikasi web dapat memperbarui dan menampilkan data dari server tanpa harus melakukan *reload* halaman secara keseluruhan, sehingga aplikasi terasa lebih responsif, dinamis, dan menghemat *bandwidth*.

---

## 2. ⚙️ Instalasi jQuery Offline
Untuk menangani *request* AJAX secara praktis, pustaka jQuery versi `3.6.0.min.js` diunduh dan disimpan secara lokal di dalam direktori proyek.
*Lokasi penyimpanan: `public/assets/js/jquery-3.6.0.min.js`.
* Pemanggilan pada View: `<script src="<?= base_url('assets/js/jquery-3.6.0.min.js') ?>"></script>`.

---

## 3. 🚀 Pembuatan AjaxController
Dibuat sebuah controller khusus (`AjaxController.php`) untuk menangani *request* di belakang layar.
*`getData()`: Mengambil data dari `ArtikelModel` dan mengembalikannya dalam format JSON menggunakan `$this->response->setJSON($data)`.
* `delete($id)`: Menghapus data spesifik berdasarkan ID dan mengembalikan status konfirmasi dalam format JSON.

---

## 4. 🖥️ Modifikasi View & Logika AJAX
Pemanggilan AJAX dilakukan menggunakan metode `$.ajax()` dari jQuery.
* **Read Data:** Menggunakan *method* `GET` ke *endpoint* `/ajax/getdata` untuk merender tabel secara asinkron saat halaman dimuat.
* **Delete Data:** Menerapkan *event listener* pada tombol kelas `.btn-delete`. [cite_start]Jika diklik, sistem akan mengirim *request* `DELETE` ke *endpoint* `/ajax/delete/id`
* Apabila berhasil, fungsi `loadData()` akan dipanggil kembali untuk memuat ulang isi tabel tanpa me-*refresh* halaman.

---

## 5. 📸 Hasil Akhir (Screenshot)

### 📌 Keberhasilan Hapus Data via AJAX

<img width="1707" height="687" alt="p8_ajax_delete_success" src="https://github.com/user-attachments/assets/2ad6fd57-2437-4cf5-88e2-ce5cd448d964" />

*Gambar: Baris data (ID 3) berhasil dihapus dari database dan tabel diperbarui secara asinkron tanpa memuat ulang (refresh) halaman browser.*

---
<div align="center">
  <b>&copy; 2026 Rizky Maulana | NIM: 312410430</b><br>
  <i>Laporan Praktikum Web 2 - Universitas Pelita Bangsa</i>
</div>

```

