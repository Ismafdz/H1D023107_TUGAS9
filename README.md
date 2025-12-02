# Tugas Pertemuan 10 — Aplikasi TokoKita (Mobile Programming)

Proyek ini merupakan implementasi tugas praktikum **Pemrograman Mobile Pertemuan 11** menggunakan **Flutter**. Aplikasi ini menampilkan fitur manajemen data toko (**CRUD Produk**) serta sistem otentikasi pengguna (**Login & Register**) yang saling terintegrasi.

---
## Identitas Diri
Nama : Isma Fadhilatizzahra
NIM : H1D023107
Shift : C

---

## Penjelasan Kode & Fitur Aplikasi

## 1. Screenshot Halaman UI



https://github.com/user-attachments/assets/969c64de-f18f-4869-960a-241e1b9093da



## 2. PROSES LOGIN (Langkah-demi-Langkah)
a. User membuka halaman Login

Pada halaman ini, pengguna menginputkan:

Email

Password

Penjelasan Proses:

Form memvalidasi input tidak boleh kosong

Ketika tombol Login ditekan, data dikirim ke API:

POST /login


Backend CI4 akan mengecek:

Apakah email terdaftar

Apakah password benar

Jika berhasil, server mengembalikan:

status: true

token autentikasi (Bearer token)

data user

Contoh response:

{
  "status": true,
  "message": "Login Berhasil",
  "token": "abc123xyz..."
}

b. Popup Berhasil / Gagal



Jika berhasil → tampil popup berhasil, lalu diarahkan ke Home

Jika gagal → tampil pesan error

Kode Login (Bloc / Controller)
var apiUrl = ApiUrl.login;
var response = await Api().post(apiUrl, data);
var body = json.decode(response.body);

if (body['status'] == true) {
  UserInfo().setToken(body['token']);
  emit(LoginSuccess());
} else {
  emit(LoginError(body['message']));
}

## 3. PROSES READ DATA PRODUK (Menampilkan List Produk)
a. Setelah login, user diarahkan ke halaman Produk



Penjelasan Proses

Flutter memanggil API menggunakan token:

GET /produk
Authorization: Bearer <token>


Server mengirim list produk dalam format JSON

List ini ditampilkan dalam bentuk ListView

Kode Fetch Produk
var response = await Api().get(ApiUrl.listProduk);
var body = json.decode(response.body);
return Produk.fromJsonList(body['data']);

## 4. PROSES TAMBAH DATA PRODUK
a. User membuka form Tambah Produk



Field:

Nama Produk

Harga

Deskripsi

b. Penjelasan Proses

User mengisi form

Flutter mengirim data ke API:

POST /produk


Backend menyimpan ke database

Server mengirim response berhasil

Flutter menampilkan popup sukses dan kembali ke halaman produk

Kode Create Produk
var data = {
  'nama_produk': namaController.text,
  'harga': hargaController.text,
  'deskripsi': deskripsiController.text,
};

var response = await Api().post(ApiUrl.createProduk, data);
var body = json.decode(response.body);

if (body['status'] == true) {
  emit(ProdukAddSuccess());
} else {
  emit(ProdukAddError(body['message']));
}

## 5. PROSES EDIT PRODUK
a. User memilih produk lalu masuk halaman Edit



Penjelasan Proses

Data produk lama ditampilkan di form

User mengubah nilai

Flutter mengirim request:

PUT /produk/{id}


Server memperbarui database

Kode Update Produk
var response = await Api().put(ApiUrl.updateProduk(id), jsonEncode(data));
var body = json.decode(response.body);

## 6. PROSES DELETE PRODUK
a. User menekan tombol hapus pada salah satu produk



Penjelasan Proses

Flutter menampilkan konfirmasi “Yakin hapus?”

Jika Ya, Flutter mengirim:

DELETE /produk/{id}


Server menghapus data di database

Flutter menampilkan popup berhasil

Kode Delete Produk
var response = await Api().delete(ApiUrl.deleteProduk(id));
var body = json.decode(response.body);

## 7. Struktur API yang Digunakan
POST    /registrasi
POST    /login
GET     /produk
POST    /produk
PUT     /produk/{id}
DELETE  /produk/{id}

## 8. Penyimpanan Token

Setelah login, token disimpan menggunakan SharedPreferences:

await prefs.setString('token', token);


Token digunakan untuk semua request lain:

headers: {
  HttpHeaders.authorizationHeader: "Bearer $token"
}

## 9. Cara Menjalankan Aplikasi
Backend (CI4)
php spark serve --host 192.168.1.13 --port 8080

Flutter (Emulator)
flutter run
