# Tugas Pertemuan 10 — Aplikasi TokoKita (Mobile Programming)

Proyek ini merupakan implementasi tugas praktikum **Pemrograman Mobile Pertemuan 10** menggunakan **Flutter**. Aplikasi ini menampilkan fitur manajemen data toko (**CRUD Produk**) serta sistem otentikasi pengguna (**Login & Register**) yang saling terintegrasi.

---
## Identitas Diri
Nama : Isma Fadhilatizzahra
NIM : H1D023107
Shift : C

---

## Penjelasan Kode & Fitur Aplikasi

### 1. Model Data (Mapping JSON)

- **`model/registrasi.dart`**
  - Mendefinisikan class `Registrasi`
  - Memiliki `factory fromJson` untuk mem-parsing respons status pendaftaran dari JSON

- **`model/login.dart`**
  - Membuat class `Login` untuk menampung token, userID, dan userEmail hasil login

- **`model/produk.dart`**
  - Class `Produk` digunakan sebagai DTO
  - Menyimpan atribut `kodeProduk`, `namaProduk`, dan `hargaProduk`

---

### 2. Entry Point (Main)

- **File:** `lib/main.dart`
- Menggunakan widget `MyApp` sebagai root aplikasi
- `debugShowCheckedModeBanner = false` agar tampilan lebih bersih
- Properti `home` diatur ke `LoginPage()` sehingga halaman awal adalah Login

---

### 3. Halaman Registrasi

- **File:** `lib/ui/registrasi_page.dart`
- Menggunakan **StatefulWidget** karena membutuhkan perubahan state saat validasi form
- Memakai `GlobalKey<FormState>` untuk memvalidasi semua field sekaligus
- Menggunakan validator kustom pada `TextFormField` (misalnya regex email)

---

### 4. Halaman Login

- **File:** `lib/ui/login_page.dart`
- Memiliki AppBar dengan judul **"Login Yaya"**
- Navigasi ke halaman Registrasi menggunakan `Navigator.push` pada widget `InkWell`
- Menggunakan `TextEditingController` untuk menangkap input email & password

---

### 5. Halaman List Produk (Read)

- **File:** `lib/ui/produk_page.dart`
- Menampilkan daftar produk menggunakan `ListView`
- Item ditampilkan melalui widget kustom **ItemProduk** (Card + ListTile)
- Klik item menggunakan `GestureDetector` untuk berpindah ke detail produk dengan mengirim objek produk

---

### 6. Halaman Tambah & Ubah Produk (Create/Update)

- **File:** `lib/ui/produk_form.dart`
- Menggunakan pendekatan **Reusable Page**
- Fungsi `isUpdate()` di `initState` mendeteksi mode halaman:
  - Jika `widget.produk != null` → **UBAH PRODUK YAYA**
  - Jika `null` → **TAMBAH PRODUK YAYA**
- Controller otomatis mengisi data lama saat mode update

---

### 7. Halaman Detail Produk (Delete)

- **File:** `lib/ui/produk_detail.dart`
- Menampilkan detail produk melalui akses `widget.produk`
- Fungsi `confirmHapus()` menjalankan `AlertDialog` untuk konfirmasi penghapusan
- Tombol **EDIT** menavigasi ke `ProdukForm` dengan membawa data produk

---

