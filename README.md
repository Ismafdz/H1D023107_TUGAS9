# Tugas Pertemuan 10 — Aplikasi TokoKita (Mobile Programming)

Proyek ini merupakan implementasi tugas praktikum Pemrograman Mobile (Pertemuan 10) menggunakan **Flutter**. Aplikasi ini menampilkan fitur manajemen data toko (**CRUD Produk**) serta sistem otentikasi pengguna (**Login & Register**) yang saling terintegrasi.

---

## Informasi Pengembang
Aplikasi ini dikembangkan oleh **Yaya** menggunakan bahasa pemrograman **Dart**. Fokus pengembangan diarahkan pada:
- Logika navigasi
- Validasi form
- Struktur model data

---

## Penjelasan Kode & Fitur Aplikasi

### 1. Model Data (Mapping JSON)
- `model/registrasi.dart` — Menangkap dan menyimpan respons status dari proses registrasi.
- `model/login.dart` — Menyimpan token otentikasi dan ID pengguna untuk sesi login.
- `model/produk.dart` — Representasi objek produk berisi kode produk, nama produk, dan harga.

---

### 2. Entry Point (main.dart)
- Mengatur tema visual aplikasi secara global.
- Menonaktifkan `debugShowCheckedModeBanner` agar tampilan lebih bersih.
- Menetapkan halaman awal aplikasi ke **Halaman Login**.

---

### 3. Halaman Registrasi
- Menyediakan formulir pendaftaran akun baru.
- Memiliki validasi form, seperti email valid dan password minimal 6 karakter.
- Menggunakan `TextEditingController` untuk mengelola input pengguna.

---

### 4. Halaman Login
- Menggunakan AppBar dengan judul **"Login Yaya"**.
- Menyediakan navigasi menuju halaman Registrasi.
- Memvalidasi input email dan password sebelum diproses.

---

### 5. Halaman List Produk (Read)
- Menampilkan seluruh data produk dalam tampilan list scrollable.
- Menggunakan judul halaman **"List Produk Yaya"**.
- Menyediakan tombol **Tambah Produk (+)** dan menu **Drawer** untuk Logout.

---

### 6. Halaman Tambah & Ubah Produk (Create & Update)
- Dibuat **reusable**, sehingga satu halaman dapat menangani dua fungsi.
- Memiliki logika dinamis:
  - Jika data produk dikirim → mode **Ubah (Update)**
  - Jika tidak ada data → mode **Tambah (Create)**

---

### 7. Halaman Detail Produk (Delete)
- Menampilkan informasi lengkap produk terpilih.
- Memiliki tombol **Edit** dan **Delete**.
- Dilengkapi dialog konfirmasi:
  > “Yakin ingin menghapus data ini?”

---

## Kesimpulan
Aplikasi TokoKita menjadi contoh implementasi dasar aplikasi mobile berbasis Flutter dengan fungsi autentikasi dan CRUD, cocok sebagai referensi pembelajaran mobile programming.

---
