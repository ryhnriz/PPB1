# Pastel - Manajemen Produk & Kategori

Aplikasi Flutter dengan CRUD Produk dan Kategori yang terhubung ke backend PHP + MySQL (Docker).

## Fitur
- Produk: tambah, lihat daftar dan detail, ubah, hapus
- Cari produk, filter per kategori, ringkasan jumlah/total stok/nilai stok
- Ubah stok cepat dengan tombol +/- di halaman detail
- Kategori: tambah, ubah nama (produk ikut diperbarui), hapus (ditolak jika masih dipakai produk)
- Pengaturan: ubah dan tes alamat server langsung dari aplikasi

## Teknologi
Flutter (provider, go_router, dio), PHP 8.3 (Apache, mysqli), MySQL, Docker Compose.

## Persiapan
- Flutter SDK, Docker Desktop, container MySQL yang sudah berjalan
- Salin `.env.example` menjadi `.env`, lalu isi `DB_PASS` dengan password MySQL

## Menjalankan backend
1. Buat tabel di MySQL (lihat `backend/database/schema.sql`):
   tabel `products` dan `categories`
2. Jalankan API:
   ```
   docker compose up -d --build
   ```
3. Tes: buka http://localhost:8085/api/products.php (harus keluar JSON)

## Menjalankan aplikasi
```
flutter pub get
flutter run
```
Alamat server:
- Android emulator: otomatis `http://10.0.2.2:8085`
- HP fisik: isi `kServerUrl` di bagian atas `lib/main.dart` dengan `http://IP_KOMPUTER:8085`
  (HP dan komputer harus satu Wi-Fi), atau isi lewat tab Pengaturan
- Chrome/Windows: otomatis `http://localhost:8085`

Android memerlukan `android:usesCleartextTraffic="true"` pada tag `<application>` di
`android/app/src/main/AndroidManifest.xml` karena API memakai HTTP.

## Endpoint API
| Method | URL | Fungsi |
|---|---|---|
| GET | /api/products.php | Daftar produk |
| GET | /api/products.php?id=1 | Detail produk |
| POST | /api/products.php | Tambah produk |
| PUT | /api/products.php | Ubah produk (id di body) |
| DELETE | /api/products.php?id=1 | Hapus produk |
| GET | /api/categories.php | Daftar kategori |
| POST | /api/categories.php | Tambah kategori |
| PUT | /api/categories.php | Ubah kategori (id di body) |
| DELETE | /api/categories.php?id=1 | Hapus kategori |

Format respons: `{"status":"success|error","message":"...","data":...}`

## Tangkapan layar
Lihat folder `docs/screenshots/`.

## Pemecahan masalah
- "Tidak dapat terhubung ke server": cek Docker berjalan, alamat di tab Pengaturan, dan firewall port 8085
- Setelah mengubah AndroidManifest.xml, hentikan aplikasi lalu `flutter run` ulang (hot reload tidak cukup)
