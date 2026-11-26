# ARABIA — GitHub & Vercel Starter

Website pembelajaran Bahasa Arab untuk siswa MTs/SMP. Dibangun dengan HTML, CSS, JavaScript, Supabase Auth + PostgreSQL, dan Vercel.

## Fitur pada starter ini
- Landing page responsif bergaya gamifikasi.
- Registrasi dan login email/password.
- Profil pengguna otomatis dengan role siswa.
- Dashboard siswa, ringkasan XP dan materi selesai.
- Daftar materi terbit dari database.
- Kuis pilihan ganda.
- Penilaian dan pemberian XP dilakukan melalui fungsi database (bukan dipercaya dari browser).
- SQL schema, Row Level Security (RLS), trigger profil, dan seed satu materi/kuis.

## A. Siapkan Supabase
1. Buat project di https://supabase.com.
2. Buka **SQL Editor**, lalu jalankan seluruh file `supabase/schema.sql`.
3. Buka **Project Settings → API**. Salin Project URL dan anon/public key.
4. Pada Authentication → URL Configuration, masukkan URL deployment Vercel ke Site URL / Redirect URLs bila diperlukan.

## B. Konfigurasi
Salin `config.example.js` menjadi `config.js`, kemudian isi:
```js
window.ARABIA_CONFIG = {
  SUPABASE_URL: "https://PROJECT-REF.supabase.co",
  SUPABASE_ANON_KEY: "SUPABASE_ANON_KEY"
};
```
Untuk lokal, jalankan dengan VS Code Live Server. Jangan membuka `index.html` sebagai file langsung.

**Keamanan:** anon/public key memang digunakan di browser. Jangan pernah memasukkan Supabase `service_role` key ke frontend atau GitHub. Keamanan data harus ditegakkan oleh RLS.

## C. Upload ke GitHub
1. Buat repository baru.
2. Ekstrak ZIP ini.
3. Salin seluruh isi folder ke repository.
4. Jangan commit `config.js` yang berisi konfigurasi pribadi; gunakan `config.example.js` sebagai template.

## D. Deploy ke Vercel
1. Login ke https://vercel.com.
2. Add New → Project → Import Git Repository.
3. Framework Preset: **Other**.
4. Build Command: kosongkan.
5. Output Directory: `.`.
6. Deploy.

Karena aplikasi ini frontend statis, Vercel tidak otomatis menyuntikkan environment variables ke JavaScript browser. Untuk starter tanpa proses build, isi `config.js` sebelum deploy. Anon key boleh tampil di frontend jika RLS benar; service role key tidak boleh.

## E. Buat akun guru/admin
Registrasi publik otomatis membuat role `siswa`. Untuk mengubah role:
1. Daftarkan akun melalui website.
2. Buka Supabase → Table Editor → `profiles`.
3. Ubah `role` menjadi `guru` atau `admin` untuk akun yang dipercaya.
Jangan membuka hak admin untuk pendaftaran publik.

## Struktur
```text
ARABIA_GitHub_Vercel/
├── index.html
├── config.example.js
├── vercel.json
├── assets/css/style.css
├── assets/js/app.js
└── supabase/schema.sql
```

## Batasan versi awal
Versi ini adalah starter deployable, bukan seluruh spesifikasi 12 halaman final. UI dashboard guru/admin, CRUD materi via panel, drag-and-drop game, audio, streak, badge otomatis, leaderboard, dan laporan kelas masih perlu dikembangkan. Materi seed hanya contoh dan perlu disesuaikan dengan kurikulum Bahasa Arab MTs/SMP.
