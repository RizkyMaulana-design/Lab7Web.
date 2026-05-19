
  <img width="231" height="53" alt="logo codelnighter" src="https://github.com/user-attachments/assets/5472efba-6f09-4a50-b536-f6f608878912" />

  
  # 🔐 Laporan Praktikum 4: Modul Login & Autentikasi (Filters)
  
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![CodeIgniter 4](https://img.shields.io/badge/CodeIgniter_4-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![Security](https://img.shields.io/badge/Filter-Authentication-red?style=for-the-badge)
</div>

---

## 📋 Daftar Isi
1. [🧠 Konsep Filter & Autentikasi](#1-konsep-filter--autentikasi)
2. [🗄️ Persiapan Tabel User (Database)](#2-persiapan-tabel-user-database)
3. [🧩 Membuat Model & Controller User](#3-membuat-model--controller-user)
4. [🖥️ Membuat View Form Login](#4-membuat-view-form-login)
5. [🛡️ Membuat & Mendaftarkan Filter Auth](#5-membuat--mendaftarkan-filter-auth)
6. [🛣️ Konfigurasi Routing Terbaru](#6-konfigurasi-routing-terbaru)
7. [📸 Hasil Akhir (Screenshot)](#7-hasil-akhir-screenshot)

---

## 1. 🧠 Konsep Filter & Autentikasi
Praktikum ini bertujuan untuk mengamankan halaman administration portal agar tidak bisa diakses secara ilegal melalui URL tanpa hak akses. Sistem ini memanfaatkan fitur **HTTP Filters** bawaan CodeIgniter 4 yang bertindak sebagai *middleware* atau "satpam" pintu masuk sebelum sebuah *request* rute admin dieksekusi.

---

## 2. 🗄️ Persiapan Tabel User (Database)
Membuat tabel `user` untuk menampung data kredensial Administrator yang akan digunakan saat proses autentikasi.

```sql
USE lab_ci4;

CREATE TABLE user (
    id INT(11) auto_increment,
    username VARCHAR(200) NOT NULL,
    useremail VARCHAR(200),
    userpassword VARCHAR(200),
    PRIMARY KEY(id)
);

```

> 🔒 *Keamanan:* Kata sandi disimpan menggunakan enkripsi hash searah tingkat tinggi berbasis algoritma BCRYPT, sehingga tidak disimpan dalam bentuk teks polos (plain text).

---

## 3. 🧩 Membuat Model & Controller User

Dibuat `UserModel.php` untuk manipulasi data tabel user, dan `User.php` sebagai pengontrol logika utama login, pencocokan password hash via `password_verify()`, set session data, serta fungsi logout.

### 🎮 Cuplikan Logika Autentikasi (`app/Controllers/User.php`)

```php
$verify_pass = password_verify($password, $data['userpassword']);
if ($verify_pass) {
    $ses_data = [
        'useremail' => $data['useremail'],
        'username'  => $data['username'],
        'logged_in' => TRUE
    ];
    $session->set($ses_data);
    return redirect()->to('/admin/artikel');
}

```

---

## 4. 🖥️ Membuat View Form Login

Membuat file antarmuka `app/Views/user/login.php` yang menyediakan input Email dan Password, serta dilengkapi pesan *Flashdata* interaktif apabila input yang dimasukkan salah.

---

## 5. 🛡️ Membuat & Mendaftarkan Filter Auth

Membuat berkas filter di `app/Filters/Auth.php` untuk memotong akses ilegal jika status *session* `logged_in` bernilai FALSE.

```php
// app/Filters/Auth.php
public function before(RequestInterface $request, $arguments = null)
{
    if (!session()->get('logged_in')) {
        return redirect()->to('/user/login');
    }
}

```

Mendaftarkan alias filter tersebut ke dalam file konfigurasi utama `app/Config/Filters.php`:

```php
public array $aliases = [
    'auth' => \App\Filters\Auth::class,
];

```

---

## 6. 🛣️ Konfigurasi Routing Terbaru

Menambahkan filter pengaman `'auth'` ke dalam *group routing* admin di file `app/Config/Routes.php` agar seluruh rute CRUD artikel di bawahnya otomatis terkunci gembok keamanan.

```php
$routes->match(['get', 'post'], '/user/login', 'User::login');
$routes->get('/user/logout', 'User::logout');

$routes->group('admin', ['filter' => 'auth'], function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});

```

---

## 7. 📸 Hasil Akhir (Screenshot)

### 📌 Percobaan Bypass Akses Tanpa Login (Terblokir Filter)


*Gambar: User mencoba mengakses langsung /admin/artikel tetapi ditendang balik ke halaman login.*

### 📌 Sukses Login & Masuk Dasbor Admin

<img width="1641" height="798" alt="p4_1_blocked" src="https://github.com/user-attachments/assets/367bf772-d80b-41c3-b451-6169b6f478af" />


---

### 📷 Persiapan File Gambar Screenshot

<img width="1641" height="798" alt="p4_1_blocked" src="https://github.com/user-attachments/assets/a027135a-bddc-4429-a9b1-d9fb21408037" />

<img width="520" height="378" alt="p4_2_dashboard" src="https://github.com/user-attachments/assets/dd1aed0b-f9fb-415d-ba7b-ffe5c1ae4d83" />

Tugas Praktikum 4 kamu sudah selesai total dan siap dikumpulkan ke dosen pengampu!
