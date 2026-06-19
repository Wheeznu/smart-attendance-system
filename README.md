# Smart Attendance System (Sistem Absensi Himatif)

<p align="center">
  <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="300" alt="Laravel Logo">
</p>

Sistem Absensi Himatif (Smart Attendance System) adalah aplikasi berbasis web yang diintegrasikan dengan pemindai kartu **RFID (Radio Frequency Identification)**. Sistem ini dirancang untuk mencatat kehadiran mahasiswa dan panitia dalam berbagai acara atau kegiatan yang diselenggarakan oleh Himpunan Mahasiswa Informatika (Himatif) secara cepat, akurat, dan real-time.

---

## 🚀 Fitur Utama

1. **Dashboard Statistik Real-time**: 
   Menampilkan ringkasan data seperti total mahasiswa aktif dan jumlah kehadiran pada hari pelaksanaan kegiatan.
2. **Manajemen Acara & Agenda**: 
   Membuat dan mengelola event/acara Himatif beserta rincian jadwal agenda (sesi pagi, sesi sore, atau hari ke-1, hari ke-2), lengkap dengan pengaturan waktu check-in/checkout dan batas keterlambatan.
3. **Manajemen Divisi & Panitia**: 
   Pendaftaran kepanitiaan acara yang dikelompokkan berdasarkan divisi kerja (misalnya Divisi Acara, Humas, Logistik, dll).
4. **Manajemen Mahasiswa**: 
   Basis data mahasiswa yang menyimpan informasi identitas penting beserta kode unik RFID UID milik mereka.
5. **Absensi RFID Presisi Tinggi**:
   * **Emulasi Keyboard RFID**: Proses check-in dan checkout dirancang untuk menangkap input scanner RFID secara otomatis (autofocus).
   * **Proteksi Input Manual**: Fitur keamanan berbasis JavaScript yang secara otomatis membersihkan input jika diketik manual dengan lambat (> 50ms per karakter), sehingga memastikan absensi hanya dapat dilakukan dengan kartu RFID fisik.
   * **Notifikasi Pop-up Interaktif**: Menggunakan library SweetAlert2 untuk menampilkan respon visual langsung (Berhasil/Gagal) disertai suara/pesan sukses.
6. **Laporan & Rekapitulasi**:
   Rekap kehadiran panitia dan mahasiswa per agenda kegiatan dengan penghitungan persentase tingkat kehadiran, serta pencetakan log absensi secara langsung.

---

## 🛠️ Stack Teknologi

* **Backend**: Laravel 13.x (PHP >= 8.3)
* **Frontend**: Tailwind CSS v4, Blade Templating, Vite
* **Database**: MySQL / MariaDB (bisa disesuaikan dengan SQLite atau DBMS lainnya)
* **Real-time / WebSocket**: Laravel Reverb (opsional untuk event broadcasting)
* **Library Tambahan**: 
  * SweetAlert2 (Notifikasi pop-up)
  * Barryvdh Laravel DomPDF (Export laporan PDF)

---

## 📋 Prasyarat Sistem

Sebelum menginstal proyek ini, pastikan mesin lokal Anda sudah memiliki:
* **PHP** versi `8.3` atau lebih tinggi
* **Composer** (Dependency Manager untuk PHP)
* **Node.js & NPM** (untuk kompilasi aset frontend)
* **MySQL / MariaDB Server**
* **RFID Reader** (Keyboard Emulation USB HID) dan **Kartu RFID** (untuk simulasi/penggunaan absensi)

---

## 🔧 Panduan Instalasi & Konfigurasi

Ikuti langkah-langkah di bawah ini untuk menjalankan proyek ini di lingkungan lokal Anda:

### 1. Kloning Repositori
Kloning repositori ini ke komputer lokal Anda:
```bash
git clone <repository-url-dari-himatif-absensi>
cd Absensi
```

### 2. Jalankan Perintah Setup
Proyek ini telah dilengkapi dengan composer script bernama `setup`. Perintah ini akan mengotomatiskan beberapa langkah (instalasi dependensi, penyalinan file `.env`, pembuatan application key, migrasi database, dan instalasi frontend):
```bash
composer setup
```

> **Penting**: Pastikan Anda sudah membuat sebuah database kosong bernama **`absensi`** (atau sesuai konfigurasi di `.env` Anda) pada server database MySQL sebelum menjalankan perintah ini, agar proses migrasi database berjalan sukses.

### 3. Konfigurasi Lingkungan (.env)
Buka file `.env` yang baru dibuat di root direktori proyek, lalu sesuaikan konfigurasi database Anda jika berbeda dari default:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=absensi
DB_USERNAME=root
DB_PASSWORD=your_mysql_password
```

### 4. Jalankan Aplikasi
Untuk menjalankan server development Laravel sekaligus live reload Vite secara paralel, jalankan perintah berikut:
```bash
composer dev
```
Perintah di atas akan menjalankan:
* Laravel Local Development Server di `http://127.0.0.1:8000`
* Vite Server untuk kompilasi dan hot reload aset frontend (Tailwind v4)
* Laravel Queue Listener untuk proses background job

Buka web browser dan akses halaman utama di: **`http://127.0.0.1:8000`**

---

## 💡 Cara Penggunaan Absensi RFID

1. **Pendaftaran Kartu RFID**:
   Pastikan data mahasiswa/panitia sudah didaftarkan di menu **Mahasiswa** bersama dengan kode UID kartu RFID mereka.
2. **Masuk ke Halaman Check-in / Checkout**:
   Pilih salah satu acara dan buka agenda yang aktif. Klik tombol **Check-in** atau **Checkout**.
3. **Melakukan Scan**:
   Halaman scan akan mendeteksi fokus input secara otomatis. Tempelkan kartu RFID ke alat pembaca. RFID Reader akan otomatis menginput kode UID kartu dan mencatat kehadiran serta menampilkan pop-up sukses.
4. **Log Kehadiran**:
   Setiap scan kartu yang berhasil akan memperbarui log absensi secara real-time pada tabel di halaman tersebut.

---

## 📄 Lisensi

Sistem Absensi Himatif ini dilisensikan di bawah [MIT License](https://opensource.org/licenses/MIT).

