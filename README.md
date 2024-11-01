# Petrolida 2025

Project ini dibangun dengan menggunakan Clean Architecture dengan tujuan untuk menciptakan struktur modular yang mendukung skalabilitas, pemeliharaan, serta keterbacaan kode yang baik.

## Tech Stack

- **Bahasa/Framework**:
  - **Go** - Bahasa pemrograman utama.
  - **Gin** - Web framework untuk pengelolaan request dan routing.
  - **GORM** - ORM untuk manajemen database.
- **Commands**:

  - `go mod tidy`: Mengambil semua package yang diperlukan.
  - `go run cmd/app/main.go -config=".env"`: Menjalankan aplikasi dengan konfigurasi yang ditentukan.
  - `go run cmd/app/main.go -config=".env" migrate`: Melakukan migrasi table ke database.
  - `go run cmd/app/main.go -config=".env" seeder`: Melakukan Seeder data ke database.
  - `go run cmd/app/main.go -config=".env" seeder migrate`: Melakukan seeder dan migrate secara bersamaa

  Catatan: Program akan langsung berjalan ketika melakukan migrate atau seeder.

## Workflow

1. Konversi tiket menjadi _issue_.
2. Buat _branch_ baru dari _issue_ (buat referensi branchnya dari branch dev).
3. Ikuti langkah-langkah pengembangan yang diberikan pada _issue_ tersebut.
4. Setelah membuat pengembangan yang diberikan jangan lupa memberikan dokumentasi pada hoppscotch dan memberikan example responsenya minimal 1.
5. Sebelum melakukan push ke _branch_ tiket, lakukan pull dari _branch_ dev untuk menghindari konflik.
6. Push perubahan ke _branch_ tiket dan buat _pull request_ untuk direview.

## Getting Started

### Prasyarat

- Pastikan Go sudah terinstal pada mesin Anda.

### Instalasi

1. Clone repository.

```bash
git clone https://github.com/petrolida2025/petrolida2025-be.git
```

2. Masuk ke direktori proyek.

```bash
cd repo-name
```

3. Instal semua package yang diperlukan.

```bash
go mod tidy
```

4. Setting `.env` nya

```bash
cp .env.example .env
```

5. Jalankan aplikasi.

```bash
go run cmd/app/main.go -config=".env"
```

### Pencerdasan Git

Untuk memudahkan proses version control dalam proyek ini, berikut beberapa perintah Git dasar yang sering digunakan:

1. **Menambahkan Perubahan ke Staging Area**  
   Setelah melakukan perubahan pada kode, gunakan perintah berikut untuk menambahkan file yang telah diubah ke staging area:
   ```bash
   git add .
   ```

Perintah git add . akan menambahkan semua perubahan pada file di direktori proyek saat ini. Untuk menambahkan perubahan pada file tertentu saja, gunakan:

```bash
git add <nama_file>
```

2. **Memeriksa Status Git**
   Untuk melihat status perubahan file yang belum di-commit, gunakan perintah:

```bash
git status
```

Ini akan menampilkan daftar file yang telah dimodifikasi dan status staging-nya (apakah sudah di-add atau belum).

3. **Membuat Commit**
   Setelah menambahkan perubahan ke staging area, buat commit untuk mencatat perubahan dengan pesan deskriptif:

```bash
git commit -m "Pesan commit yang menjelaskan perubahan"
```

Pastikan pesan commit jelas dan singkat untuk memudahkan identifikasi perubahan di masa mendatang.

link convential commit: https://www.conventionalcommits.org/en/v1.0.0/

4. **Mengirim Perubahan ke Remote Repository**
   Setelah melakukan commit, gunakan perintah berikut untuk mengirim (push) perubahan ke branch yang relevan di remote repository:

```bash
git push
```

Pastikan Anda telah melakukan pull dari branch utama (main) terlebih dahulu untuk menghindari konflik yang mungkin terjadi saat push.

## Flow Project (Clean Architecture)

Project ini mengikuti pola Clean Architecture untuk memisahkan tanggung jawab dengan struktur sebagai berikut:

- **Handler/Controller**:

  - Menerima request dari klien, melakukan validasi input, dan meneruskan data ke _Service/Usecase_.
  - Mengirimkan respons dari _Service_ ke klien.

- **Service/Usecase**:

  - Mengelola logika bisnis inti, memproses data, dan berkomunikasi dengan _Repository_.

- **Repository**:

  - Mengakses database secara langsung untuk query.
  - Mengisolasi logika database agar perubahan tidak memengaruhi lapisan lain.

- **Router**:
  - Routing diatur dan dikelompokkan berdasarkan fitur atau modul (contoh: auth, student, course) untuk memastikan struktur yang jelas serta pemisahan tugas yang baik.

### Alur Data

Request → Handler → validasi → Service → proses → Repository → Service → hasil ke Handler → Response

Struktur modular ini mendukung skalabilitas dan mempermudah pemeliharaan.
