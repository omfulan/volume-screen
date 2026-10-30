# Volume Power App

Aplikasi Android untuk mengunci layar dengan menekan tombol Volume Atas atau Volume Bawah melalui layanan Aksesibilitas Android.

## Build APK Release otomatis (tanpa membuat keystore sendiri)

Project ini dikonfigurasi agar GitHub Actions membangun **APK release yang sudah ditandatangani otomatis** menggunakan debug keystore bawaan Android Gradle Plugin.

- Tidak perlu membuat file `.jks`.
- Tidak perlu mengisi GitHub Secrets.
- Tidak perlu memasukkan password ke GitHub.
- APK dapat dipasang manual di HP Android untuk pengujian/pemakaian pribadi.

**Penting:** tanda tangan otomatis ini menggunakan sertifikat debug, bukan sertifikat rilis pribadi. Cocok untuk sideload/pemakaian sendiri, tetapi bukan pilihan untuk publikasi Google Play atau distribusi profesional. Untuk update di kemudian hari, pertahankan metode/kunci penandatanganan yang sama; bila kuncinya berubah, Android mungkin meminta aplikasi lama dihapus dahulu sebelum memasang versi baru.

## Langkah 1 — Upload project ke GitHub

1. Download ZIP project ini lalu ekstrak.
2. Login ke https://github.com.
3. Tekan tombol **New repository** (atau tanda `+` lalu **New repository**).
4. Isi nama repository: `VolumePowerApp`.
5. Pilih **Public** atau **Private** sesuai keinginan.
6. Tekan **Create repository**.
7. Pada halaman repository, pilih **Add file > Upload files**.
8. Buka folder hasil ekstrak `VolumePowerApp_AutoSigned`, lalu pilih **semua ISI folder** (jangan upload folder pembungkusnya saja).
9. Pastikan di halaman upload terlihat `app`, `.github`, `build.gradle`, `settings.gradle`, `gradle.properties`, dan `README.md` di bagian paling atas/root repository.
10. Gulir ke bawah, tekan **Commit changes**.

Jika menggunakan browser HP, aktifkan **Desktop site** bila tombol upload tidak terlihat. Pastikan folder `.github/workflows` ikut ter-upload; folder titik kadang tersembunyi di file picker.

## Langkah 2 — Jalankan GitHub Actions

1. Buka repository `VolumePowerApp`.
2. Pilih tab **Actions**.
3. Pilih workflow **Build Android APK (Auto Signed)** di sisi kiri.
4. Tekan **Run workflow**.
5. Pilih branch `main` (atau branch default repository).
6. Tekan tombol hijau **Run workflow**.
7. Tunggu sampai proses selesai dan ikon run berubah menjadi centang hijau. Biasanya perlu beberapa menit.

Workflow juga otomatis berjalan setiap kali ada commit/push baru ke branch `main` atau `master`.

## Langkah 3 — Download APK

1. Buka hasil workflow yang sudah centang hijau.
2. Gulir ke bagian **Artifacts** di bawah halaman.
3. Download `VolumePowerApp-release-auto-signed`.
4. Ekstrak ZIP artifact yang diunduh.
5. File APK di dalamnya bernama `app-release.apk`.

Jika workflow merah/gagal, buka run tersebut lalu buka langkah yang berwarna merah dan kirimkan screenshot/log error-nya agar bisa diperiksa.

## Langkah 4 — Install dan aktifkan di HP

1. Pindahkan `app-release.apk` ke HP Android (Android 9/API 28 atau lebih baru).
2. Buka file APK dan izinkan **Install unknown apps / Pasang aplikasi tidak dikenal** untuk aplikasi File/Browser yang digunakan jika Android memintanya.
3. Selesaikan instalasi lalu buka **Volume Power App**.
4. Tekan **Buka Pengaturan Aksesibilitas**.
5. Cari **Volume Power App** pada daftar layanan yang diunduh/terpasang, lalu aktifkan.
6. Setujui dialog konfirmasi Android.
7. Kembali ke aplikasi dan pastikan status menunjukkan layanan **AKTIF**.
8. Tekan Volume Atas atau Volume Bawah satu kali untuk mencoba mengunci layar.

## Cara kerja dan catatan penting

- Saat layanan aktif, tombol Volume Atas dan Volume Bawah diambil alih untuk mengunci layar, sehingga keduanya tidak mengatur volume media.
- Untuk mengembalikan fungsi volume seperti biasa, nonaktifkan layanan di Pengaturan > Aksesibilitas.
- Fungsi kunci layar memakai aksi global Accessibility Android. Perilakunya dapat berbeda pada sebagian ROM/vendor; layanan harus diaktifkan manual oleh pemilik perangkat.
- Jika layar tidak terkunci, periksa kembali bahwa layanan masih aktif dan coba restart perangkat.
- Project ini belum diuji pada semua model HP. Uji pada perangkat target sebelum mengandalkannya.

## Detail teknis

- `applicationId`: `com.example.volumepower`
- `versionName`: `1.0.0` (`versionCode`: `1`)
- Minimum Android: Android 9 / API 28
- Target SDK: API 34
- Java: 17; Android Gradle Plugin: 8.1.1; Gradle: 8.0
- Output: `app/build/outputs/apk/release/app-release.apk`
- Release APK ditandatangani otomatis menggunakan debug signing key; tidak ada signing secret yang dibutuhkan.
