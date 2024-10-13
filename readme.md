# Backend Express.js untuk Fitur Upload Banyak File

Proyek ini adalah backend yang dibangun menggunakan Express.js untuk menangani upload banyak file. File yang di-upload akan disimpan dalam kolom `photoCar` di tabel `cars`. API ini mendukung penambahan beberapa file menggunakan endpoint `/api/v1/cars` dengan metode POST.

## Fitur

- **Upload banyak file**: API ini memungkinkan pengguna untuk mengunggah banyak file untuk setiap data mobil.
- **Penyimpanan file**: File yang di-upload akan disimpan sebagai array di kolom `photoCar`.
- **Integrasi mudah**: Menggunakan [ImageKit](https://imagekit.io) untuk penyimpanan dan pengelolaan gambar.

## Endpoint API

### POST `/api/v1/cars`

Endpoint ini digunakan untuk membuat entri mobil baru dengan upload banyak gambar.

#### Permintaan

- **URL**: `/api/v1/cars`
- **Metode**: `POST`
- **Body** (FormData):
  - `model` (string): Model mobil.
  - `plate` (string): Nomor plat mobil.
  - `type` (string): Tipe mobil.
  - `year` (integer): Tahun pembuatan mobil.
  - `photo` (file): Array berisi file gambar untuk di-upload.

#### Contoh Permintaan:

```bash
curl -X POST http://localhost:3000/api/v1/cars \
  -H "Content-Type: multipart/form-data" \
  -F "plate=123ABC" \
  -F "model=Sedan" \
  -F "type=Listrik" \
  -F "year=2024" \
  -F "photo=@path/to/image1.jpg" \
  -F "photo=@path/to/image2.jpg"
```

#### Respon

- **Status**: 200 (Berhasil)
- **message**: Success to create cars data
- **Body**:

```json
{
  "status": "Success",
  "message": "Success get cars data",
  "isSuccess": true,
  "data": {
    "newCar": {
      "model": "Sedan",
      "plate": "123ABC",
      "type": "Listrik",
      "year": 2024,
    }
    "photoCar": [
      "https://ik.imagekit.io/url-gambar-1",
      "https://ik.imagekit.io/url-gambar-2"
    ],
  }
}
```

#### Respon Error

- **Status**: 400 (Permintaan Buruk)
- **Pesan**: Failed to create cars data.

## Langkah-langkah Setup

### Install terlebih dahulu

- [Node.js](https://nodejs.org/) v14 atau lebih baru
- [ImageKit API Key](https://imagekit.io)
- Database PostgreSQL

### Instalasi

1. Clone repositori ini:

```bash
git clone https://github.com/NeoBitose/challenge-ch4-upload-multiple-files.git
cd challenge-ch4-upload-multiple-files
```

2. Install dependensi:

```bash
npm install
```

3. Siapkan variabel lingkungan di file `.env`:

```bash
DB_USERNAME=your_db_username
DB_PASSWORD=your_db_password
DB_NAME=your_db_name

PUBLIC_KEY=your_imagekit_public_key
PRIVATE_KEY=your_imagekit_private_key
URL_ENDPOINT=your_imagekit_url_endpoint
```

4. Jalankan perintah untuk membuat database dan tabel:

```bash
npx sequelize db:create
npx sequelize db:migrate

(opsional, jika anda ingin menambahkan data awal untuk database anda jalankan perintah dibawah)
npx sequelize db:seed:all
```

5. Jalankan server:

```bash
npm run dev
```

6. API akan tersedia di `http://localhost:3000/api/v1/cars`.

## Teknologi yang Digunakan

- **Node.js**: Runtime untuk backend.
- **Express.js**: Framework web untuk Node.js.
- **ImageKit**: Penyimpanan cloud untuk gambar.
- **Sequelize**: ORM untuk PostgreSQL.
- **Multer**: Middleware untuk menangani `multipart/form-data` untuk upload file.
