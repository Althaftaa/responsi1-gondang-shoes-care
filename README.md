# REST API Daftar Barang Cuci Sepatu

## Deskripsi Umum

Proyek ini merupakan sebuah REST API sederhana yang dibangun menggunakan Node.js dan Express.js. API ini berfungsi untuk mengelola data sepatu yang sedang dicuci pada sebuah layanan jasa cuci sepatu.

Tujuan utama proyek ini adalah untuk mempermudah proses pencatatan, pemantauan, dan pembaruan status cucian sepatu secara digital melalui REST API sederhana. Data disimpan dan dikelola menggunakan database Supabase.

## Tujuan

1.  Mengimplementasikan konsep CRUD (Create, Read, Update, Delete) dalam REST API.
2.  Meningkatkan pemahaman penggunaan Express.js sebagai framework backend.
3.  Mengelola data menggunakan format JSON sebagai format pertukaran data utama.
4.  Membangun sistem pencatatan yang relevan dengan kebutuhan bisnis nyata.

## Teknologi yang Digunakan

- **Node.js**: _Runtime environment_ untuk menjalankan JavaScript di sisi server.
- **Express.js**: _Framework_ untuk membangun REST API dengan cepat dan sederhana.
- **Supabase**: Digunakan sebagai Database (Backend as a Service) untuk menyimpan data.
- **Vercel**: Digunakan sebagai platform untuk _deploy_ API agar bisa diakses publik.

## Fitur Utama API

| Metode   | Endpoint         | Deskripsi                                                              |
| :------- | :--------------- | :--------------------------------------------------------------------- |
| `GET`    | `/api/items`     | Menampilkan seluruh daftar sepatu yang sedang dicuci.                  |
| `GET`    | `/api/items/:id` | Menampilkan detail satu sepatu berdasarkan ID.                         |
| `POST`   | `/api/items`     | Menambahkan data sepatu baru ke dalam daftar.                          |
| `PUT`    | `/api/items/:id` | Memperbarui data sepatu (misalnya status dari Dicuci menjadi Selesai). |
| `DELETE` | `/api/items/:id` | Menghapus data sepatu yang sudah selesai dicuci.                       |

### Fitur Tambahan: Filter Status

API ini juga mendukung _filter_ data berdasarkan status melalui _query parameter_.

- **Endpoint**: `GET /api/items?status=Selesai`
- **Deskripsi**: Hanya akan menampilkan daftar sepatu yang memiliki status "Selesai".

## Struktur Data (Tabel Supabase `items`)

Berikut adalah struktur data yang disimpan dalam tabel `items` di Supabase:

- `id` (uuid): Nomor unik sepatu (dibuat otomatis oleh Supabase).
- `created_at` (timestamptz): Tanggal dan waktu data dimasukkan.
- `nama_pelanggan` (text): Nama pemilik sepatu.
- `nama_sepatu` (text): Merek atau jenis sepatu.
- `jenis_layanan` (text): Jenis layanan yang dipilih (misal: "Deep Clean", "Cuci Kilat").
- `status` (text): Status proses cuci (misal: "Diterima", "Dicuci", "Selesai").

## Contoh Request dan Response

1. **POST**/api/items (Membuat Data Baru)
   **Request Body:**

```json
{
  "nama_pelanggan": "Althaf Muh",
  "nama_sepatu": "Adidas samba",
  "jenis_layanan": "Deep Clean",
  "status": "Diterima"
}
```

**Response:**

```json
{
  "id": "c7222830-64bf-44bd-b784-0d4aa20962ad",
  "created_at": "2025-10-23T11:13:49.993502+00:00",
  "nama_pelanggan": "Althaf Muh",
  "nama_sepatu": "Adidas samba",
  "jenis_layanan": "Deep Clean",
  "status": "Diterima"
}
```

2. **GET**/api/items (Mendapatkan Semua Data)

   **Request:**GET http://localhost:3000/api/items

   **Response:**

```json
[
  {
    "id": "c7222830-64bf-44bd-b784-0d4aa20962ad",
    "created_at": "2025-10-23T11:13:49.993502+00:00",
    "nama_pelanggan": "Althaf Muhammad",
    "nama_sepatu": "Nike Air Max",
    "jenis_layanan": "Deep Clean",
    "status": "Dicuci"
  },
  {
    "id": "4075d18b-fdf4-4b86-bced-e74d002c8c30",
    "created_at": "2025-10-23T11:19:19.755961+00:00",
    "nama_pelanggan": "Tafta zaen",
    "nama_sepatu": "compass tribune",
    "jenis_layanan": "Cuci kilat",
    "status": "Selesai"
  },
  {
    "id": "b6632c29-0109-4e75-a13f-81a333d8c577",
    "created_at": "2025-10-23T11:51:27.440415+00:00",
    "nama_pelanggan": "Althaf Muh",
    "nama_sepatu": "Adidas samba",
    "jenis_layanan": "Deep Clean",
    "status": "Diterima"
  }
]
```

3. **GET** /api/items?status=Dicuci (Filter Data)

   **Request:**GET http://localhost:3000/api/items?status=Dicuci

   **Response:**

```json
[
  {
    "id": "c7222830-64bf-44bd-b784-0d4aa20962ad",
    "created_at": "2025-10-23T11:13:49.993502+00:00",
    "nama_pelanggan": "Althaf Muhammad",
    "nama_sepatu": "Nike Air Max",
    "jenis_layanan": "Deep Clean",
    "status": "Dicuci"
  }
]
```

4. **PUT** /api/items/:id (Memperbarui Data)

   **Request:**http://localhost:3000/api/items4075d18b-fdf4-4b86-bced-e74d002c8c30

   **Request Body:**

```json
{
  "status": "Selesai"
}
```

**Response:**

```json
{
  "id": "4075d18b-fdf4-4b86-bced-e74d002c8c30",
  "created_at": "2025-10-23T11:19:19.755961+00:00",
  "nama_pelanggan": "Tafta zaen",
  "nama_sepatu": "compass tribune",
  "jenis_layanan": "Cuci kilat",
  "status": "Selesai"
}
```

5. **DELETE** /api/items/:id (Menghapus Data)

   **Request :**http://localhost:3000/api/items/4075d18b-fdf4-4b86-bced-e74d002c8c30

   **Response:**

```json
{
  "message": "Deleted successfully"
}
```
