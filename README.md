# Aplikasi Kafe Sederhana (Android & Web) ☕

Aplikasi pemesanan untuk kafe yang dibangun menggunakan Flutter dan Firebase. Proyek ini dirancang untuk platform **Android** dan **Web**.

Aplikasi ini memiliki sistem menu dinamis yang dikelola oleh admin dan alur pembayaran yang disederhanakan dengan verifikasi manual oleh staf di meja pelanggan.

---

## Daftar Isi
1.  [Daftar Halaman Aplikasi](#daftar-halaman-aplikasi)
2.  [Akun Login & Nama Kelompok](#akun-login--nama-kelompok)
3.  [Persiapan & Instalasi](#persiapan--instalasi)
4.  [Alur Kerja Git & Kontribusi Kode](#alur-kerja-git--kontribusi-kode)
5.  [Struktur Database (Firestore)](#struktur-database-firestore)
6.  [Arsitektur & State Management](#arsitektur--state-management)

---

## Daftar Halaman Aplikasi

### Halaman Sisi Pelanggan (User)
1.  **Layar Autentikasi:** Mencakup halaman Login, Register, dan Lupa Password.
2.  **Dashboard Pengguna:** Halaman utama terpadu yang menampilkan daftar menu dari Firestore dan ringkasan keranjang belanja di bagian bawah.
3.  **Profil Pengguna:** Halaman untuk mengelola data pribadi, serta fitur Logout dan Hapus Akun.

### Halaman Sisi Admin
1.  **Dashboard Admin:** Halaman utama yang menampilkan daftar pesanan masuk (`pesanan` baru) secara *real-time*.
2.  **Detail Pesanan:** Halaman yang menampilkan rincian lengkap dari sebuah pesanan yang dipilih.
3.  **Manajemen Menu (CRUD):** Halaman untuk menambah, mengubah, dan menghapus item di koleksi `menu`.
4.  **Profil Admin:** Halaman sederhana untuk admin melakukan Logout.

---

## Akun Login & Nama Kelompok

### 🔐 Akun Login
**Akun Admin:**
- Email: `admin@example.com`
- Password: `admin123`

**Akun User:**
- Email: `user@example.com`
- Password: `user123`

### 👥 Nama Kelompok
> Kelompok 8 ✨

---

## Persiapan & Instalasi

Pastikan Anda sudah menginstal Flutter SDK (versi 3.x.x atau lebih baru).

### Langkah-langkah

1.  **Clone repository ini:**
    ```bash
    git clone https://github.com/Azhriler7/flutter-mycafe.git
    ```

2.  **Masuk ke direktori proyek:**
    ```bash
    cd flutter-mycafe
    ```

3.  **Setup Firebase:**
    - Buat project Firebase baru di [https://console.firebase.google.com](https://console.firebase.google.com)
    - Aktifkan layanan berikut:
      - **Authentication** (Email/Password)
      - **Cloud Firestore**
    - Download file konfigurasi:
      - Untuk Android: `google-services.json`
      - Untuk Web: salin konfigurasi dan tambahkan di `index.html`
    - Jalankan konfigurasi Firebase CLI:
      ```bash
      flutterfire configure
      ```

4.  **Install semua package:**
    ```bash
    flutter pub get
    ```

5.  **Jalankan aplikasi:**
    ```bash
    flutter run -d chrome  # Untuk Web
    flutter run            # Untuk Android
    ```

---

## Alur Kerja Git & Kontribusi Kode

Semua pekerjaan harus dilakukan di *branch* terpisah untuk menjaga *branch* `main` tetap stabil.

1.  **Update `main`:**
    ```bash
    git checkout main
    git pull origin main
    ```
2.  **Buat Branch Baru:**
    ```bash
    git checkout -b feature/nama-fitur-baru
    ```
3.  **Commit & Push:**
    ```bash
    git add .
    git commit -m "deskripsi commit"
    git push -u origin feature/nama-fitur-baru
    ```
4.  **Buat Pull Request** di GitHub untuk di-review.

---

## Struktur Database (Firestore)

### Koleksi: `users`
- ID: UID dari Firebase Authentication
- Fields:
  - `username`: String
  - `email`: String
  - `gender`: String
  - `createdAt`: Timestamp
  - `isAdmin`: Boolean

### Koleksi: `menu`
- ID: Auto-ID
- Fields:
  - `namaMenu`: String
  - `harga`: Number
  - `kategori`: String (`makanan`, `minuman`, dll.)
  - `isTersedia`: Boolean

### Koleksi: `pesanan`
- ID: Auto-ID
- Fields:
  - `userId`: String
  - `namaPemesan`: String
  - `noMeja`: String
  - `items`: Array of Maps
    - Setiap item: `namaMenu`, `harga`, `jumlah`
  - `totalHarga`: Number
  - `statusPesanan`: String (`baru`, `selesai`)
  - `waktuPesan`: Timestamp

---

## Arsitektur & State Management

Proyek ini menggunakan arsitektur **MVC (Model-View-Controller)** dengan pendekatan modular.

- **Model:** Struktur data di `lib/model/`
- **View:** UI pages di `lib/view/screen/{auth, admin, user}/`
- **Controller:** `lib/controller/` (menggunakan `ChangeNotifier` dari Provider)

### Paket yang Digunakan:
- `firebase_core`, `firebase_auth`, `cloud_firestore`
- `provider` untuk state management
- `get` untuk navigasi
- `intl` untuk format mata uang

---

Selamat mencoba & selamat ngopi! ☕🍩
