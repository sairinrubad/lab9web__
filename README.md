# Lab9Web — Praktikum 9: PHP Modular

| | |
|---|---|
| **Nama** | Sairin bin Rubad |
| **NIM** | 312510134 |
| **Mata Kuliah** | Pemrograman Web |
| **Topik** | Praktikum 9 — PHP Modular (Modularisasi Program, Function, Template, dan Routing) |

## 1. Tujuan Project

Repository ini berisi seluruh hasil Praktikum 9. Tujuannya:

1. Memahami modularisasi program PHP dan manfaatnya.
2. Membedakan `include`, `require`, `include_once`, dan `require_once`.
3. Membuat template (header/footer) yang dipakai bersama banyak halaman.
4. Membuat function PHP (parameter, nilai kembalian, type declaration, nilai default) dan memisahkannya ke file helper.
5. Menyusun struktur direktori aplikasi secara modular.
6. Menerapkan routing berbasis parameter URL dengan **whitelist** dan halaman **404**.
7. Merefactor aplikasi CRUD database menjadi modular (template + router + helper + modul).

## 2. Kebutuhan Perangkat

- Web server lokal Apache + PHP 8.0 atau lebih baru + MySQL/MariaDB (XAMPP / Laragon)
- Browser modern
- Visual Studio Code (atau editor sejenis)
- Git

## 3. Cara Menjalankan

1. Ekstrak/clone repository ini, lalu salin folder `Lab9Web` ke *docroot* web server
   (`C:\xampp\htdocs\Lab9Web` untuk XAMPP).
2. Jalankan **Apache** dan **MySQL** dari XAMPP Control Panel.
3. **Khusus Latihan 4 (project CRUD):** impor database
   - buka `http://localhost/phpmyadmin` → tab **Import** → pilih `project/database.sql` → **Go**, atau
   - lewat terminal: `mysql -u root < project/database.sql`
4. Buka di browser:

| Bagian | URL |
|---|---|
| Praktik include/require | `http://localhost/Lab9Web/01_praktik_include/uji-include.php` |
| Template | `http://localhost/Lab9Web/02_template/home.php` |
| Function | `http://localhost/Lab9Web/03_function/contoh-function.php` |
| Latihan 1 | `http://localhost/Lab9Web/latihan1_template/home.php` |
| Latihan 2 | `http://localhost/Lab9Web/latihan2_library_function/produk.php` |
| Latihan 3 | `http://localhost/Lab9Web/latihan3_router/index.php` |
| Latihan 4 (CRUD) | `http://localhost/Lab9Web/project/index.php` |

5. **Login Latihan 4:** username `admin`, password `admin123`.
6. Jika konfigurasi MySQL berbeda, ubah `project/config/database.php` (satu-satunya file konfigurasi koneksi).

## 4. Struktur Direktori

```
Lab9Web/
├── README.md
├── LAPORAN.md                    # jawaban analisis, pertanyaan pemahaman, kendala
├── 01_praktik_include/           # praktik include vs require
├── 02_template/                  # header.php, footer.php, home/about/kontak
├── 03_function/                  # contoh function, helpers.php, latihan function
├── latihan1_template/            # Latihan 1: Home, Profil, Kontak
├── latihan2_library_function/    # Latihan 2: helpers/functions.php (4 function)
├── latihan3_router/              # Latihan 3: router aman (6 rute + 404)
├── project/                      # Latihan 4: CRUD modular
│   ├── index.php                 # router
│   ├── .htaccess                 # URL rewrite (opsional)
│   ├── database.sql
│   ├── config/database.php       # koneksi database (PDO)
│   ├── views/                    # header, footer, dashboard, 404
│   ├── helpers/functions.php     # function umum
│   ├── modules/user/             # list, add, edit, delete
│   ├── modules/auth/             # login, logout
│   └── assets/                   # css/, js/
└── screenshots/                  # bukti hasil praktikum (40 gambar)
```

## 5. Daftar Rute

### Latihan 3 — `latihan3_router/index.php`

| Rute (`?page=`) | File | Keterangan |
|---|---|---|
| `home` (default) | `views/home.php` | Beranda |
| `profil` | `views/profil.php` | Profil mahasiswa |
| `produk` | `views/produk.php` | Daftar produk |
| `artikel` | `views/artikel.php` | Artikel |
| `kontak` | `views/kontak.php` | Kontak |
| `info/tentang` | `views/tentang.php` | Rute bersarang |
| *(lainnya)* | `views/404.php` | Status HTTP 404 |

### Latihan 4 — `project/index.php`

| Rute (`?page=`) | File | Login | Keterangan |
|---|---|:---:|---|
| `dashboard` (default) | `views/dashboard.php` | ✔ | Ringkasan data |
| `user/list` | `modules/user/list.php` | ✔ | Read — daftar + pencarian |
| `user/add` | `modules/user/add.php` | ✔ | Create |
| `user/edit&id=N` | `modules/user/edit.php` | ✔ | Update |
| `user/delete` | `modules/user/delete.php` | ✔ | Delete (hanya POST + CSRF) |
| `auth/login` | `modules/auth/login.php` | – | Login |
| `auth/logout` | `modules/auth/logout.php` | – | Logout (POST + CSRF) |
| *(lainnya)* | `views/404.php` | – | Status HTTP 404 |

## 6. Langkah Praktikum (Ringkas)

1. **Praktik include/require** — `01_praktik_include/`: uji `include` vs `require` saat file hilang (screenshot 03–06).
2. **Template** — `02_template/`: `header.php` & `footer.php` dipakai `home`, `about`, `kontak` (screenshot 07–09).
3. **Function** — `03_function/`: function tanpa/dengan parameter, `return`, type declaration, default value, `helpers.php` (screenshot 10–13).
4. **Latihan 1** — template multi-halaman tanpa salinan header/footer (screenshot 14–16).
5. **Latihan 2** — `helpers/functions.php` berisi `formatRupiah()`, `hitungDiskon()`, `validasiEmail()`, `ringkasTeks()` (+ `e()`), dipakai di 2 halaman (screenshot 17–19).
6. **Latihan 3** — router dengan whitelist 6 rute + 404, input URL tidak dipakai sebagai path file (screenshot 20–24).
7. **Latihan 4** — refactor CRUD: `config/`, `views/`, `helpers/`, `modules/`, `assets/`, router `index.php` (screenshot 25–40, struktur di 01–02).
8. **Tantangan mandiri** — menu aktif, helper pesan flash, pembatasan akses login, dan `.htaccess` URL rewrite sudah diimplementasikan di `project/`.

## 7. Fitur Keamanan pada Latihan 4

- **Whitelist rute** — path file diambil dari array `$routes`, bukan dari input URL.
- **PDO prepared statement** — mencegah SQL injection.
- **Escaping output** `e()` — mencegah XSS.
- **Aksi ubah data via POST + token CSRF** — membuka URL (GET) tidak menghapus data.
- **Password di-hash** (`password_hash` / `password_verify`) dan `session_regenerate_id()` saat login.
- **Detail error database tidak ditampilkan** ke pengguna (`error_log` + pesan umum).

## 8. URL Rewrite (Opsional)

`project/.htaccess` meneruskan `/project/user/list` ke `index.php?page=user/list`.
Syarat: `mod_rewrite` aktif dan `AllowOverride All` pada konfigurasi Apache.
Tautan & aset dibuat lewat helper `url()` dan `asset()` sehingga tetap benar saat URL ditulis ulang.

## 9. Kendala dan Solusi

Lihat bagian *Kendala dan Cara Mengatasinya* pada [`LAPORAN.md`](LAPORAN.md).

## 10. Screenshot

Seluruh bukti ada di folder [`screenshots/`](screenshots/) (diberi nomor urut 01–40 sesuai langkah praktikum).
