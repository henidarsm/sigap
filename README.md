# SIGAP - Sistem Informasi Gudang dan Pengelolaan

Aplikasi web sederhana untuk mengelola gudang & inventory: data barang, transaksi masuk/keluar, dan riwayat.

**Stack:** Laravel 11 · MySQL · Blade · Bootstrap 5 (CDN)

---

## 🚀 Cara Install di Laragon (Rekomendasi)

### 1. Download & Pasang Laragon
- Download Laragon **Full** dari [laragon.org](https://laragon.org)
- Install seperti biasa, jalankan Laragon, klik **Start All** (Apache & MySQL nyala)

### 2. Letakkan Project
- Copy seluruh folder `sigap` ini ke: **`C:\laragon\www\sigap\`**

### 3. Install Dependencies
Klik kanan tray Laragon → **Terminal**, lalu:
```bash
cd C:\laragon\www\sigap
composer install
```
*(Tunggu ± 1-2 menit, akan auto-download Laravel framework & dependency-nya)*

### 4. Setup Environment
```bash
copy .env.example .env
php artisan key:generate
```

### 5. Buat Database
- Buka **phpMyAdmin** lewat menu Laragon (atau `http://localhost/phpmyadmin`)
- Klik **New** → buat database baru bernama: **`sigap_db`** (collation: `utf8mb4_unicode_ci`)

### 6. Jalankan Migrasi & Seeder
```bash
php artisan migrate --seed
php artisan storage:link
```
Ini akan:
- Bikin tabel `users`, `barang`, `transaksi`
- Bikin akun admin default
- Bikin 5 sample barang
- Link folder `storage/app/public` ke `public/storage` (untuk gambar barang)

### 7. Akses Aplikasi
Laragon otomatis bikin URL `http://sigap.test` — tinggal buka di browser.

> ⚠️ Kalau `sigap.test` tidak terbuka, klik kanan tray Laragon → **Apache → Reload**, atau pastikan **Preferences → Hostnames → Auto create virtual hosts** tercentang.

### 8. Login
| Email | Password |
|---|---|
| `admin@sigap.test` | `password` |

---

## 🔧 Cara Install di XAMPP (Alternatif)

1. Copy folder `sigap` ke `C:\xampp\htdocs\sigap\`
2. Start Apache & MySQL via XAMPP Control Panel
3. Buka phpMyAdmin (`http://localhost/phpmyadmin`) → buat database `sigap_db`
4. Buka terminal di folder project (Shift + klik kanan → Open terminal):
   ```bash
   composer install
   copy .env.example .env
   php artisan key:generate
   php artisan migrate --seed
   php artisan storage:link
   php artisan serve
   ```
5. Buka `http://localhost:8000` di browser

---

## 📂 Fitur Utama

| Menu | Fungsi |
|---|---|
| **Dashboard** | Statistik total barang, stok, transaksi masuk/keluar; grafik aktivitas mingguan; daftar stok menipis |
| **Data Barang** | CRUD barang lengkap dengan upload gambar, search, filter |
| **Barang Masuk** | Form catat penambahan stok |
| **Barang Keluar** | Form catat pengurangan stok (dengan validasi stok cukup) |
| **Riwayat Transaksi** | Tabel semua transaksi dengan filter tanggal & jenis |

---

## 📁 Struktur Folder Penting

```
sigap/
├── app/
│   ├── Http/Controllers/   ← Login, Register, Dashboard, Barang, Transaksi
│   ├── Models/             ← Barang, Transaksi, User
│   └── Providers/
├── bootstrap/              ← Laravel 11 entry
├── config/                 ← konfigurasi (database, auth, session, dll)
├── database/
│   ├── migrations/         ← skema tabel
│   └── seeders/            ← data awal (admin + 5 barang sample)
├── public/                 ← document root (index.php)
├── resources/views/        ← template Blade (UI)
├── routes/web.php          ← daftar route
├── storage/                ← upload, cache, log, session
├── .env.example            ← contoh konfigurasi
├── artisan                 ← Laravel CLI
└── composer.json           ← dependency PHP
```

---

## ❓ Troubleshooting

**`composer install` error "PHP version too low"**
→ Update PHP minimal **8.2** (Laragon Full sudah include).

**Halaman login muncul tapi setelah submit redirect ke `/login` lagi**
→ Jalankan `php artisan config:clear` lalu coba lagi.

**Gambar barang tidak muncul setelah upload**
→ Belum jalankan `php artisan storage:link`. Coba sekali lagi.

**Error "SQLSTATE[HY000] [1049] Unknown database"**
→ Database `sigap_db` belum dibuat di phpMyAdmin. Buat dulu.

**Error "No application encryption key has been specified"**
→ Belum jalankan `php artisan key:generate`.

---

## 👨‍💻 Akun Default

```
Email    : admin@sigap.test
Password : password
```

Setelah login, kamu juga bisa daftar user admin baru lewat halaman `/register`.

---

Built for college assignment · 2026
