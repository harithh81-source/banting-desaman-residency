# Panduan Asas SEO (Search Engine Optimization)

Untuk membolehkan laman web anda naik ke **Tempat Pertama (#1)** di Google carian bagi kata kunci tempatan (contoh: *"Rumah Semi-D Banting"*, *"Taman Desa Idaman Olak Lempit"*), anda perlu mengikuti langkah-langkah di bawah.

---

## 🛠️ Langkah 1: Pengoptimuman Teknikal (Telah Selesai)
Saya telah menyediakan asas teknikal SEO terbaik di dalam kod anda:
1. **Meta Tags**: Tajuk halaman dan huraian dioptimumkan menggunakan kata kunci sasaran tempatan.
2. **JSON-LD Schema Markup**: Kod tersusun ditambahkan pada bahagian `<head>` fail `index.html` untuk membolehkan bot Google membaca spesifikasi unit (4 bilik, 2 bilik air, semi-d) secara tersusun.
3. **Robots.txt & Sitemap.xml**: Dicipta dan diletakkan di folder utama untuk memudahkan robot crawler merangkak laman anda.

---

## 🚀 Langkah 2: Daftarkan Laman ke Google Search Console (Paling Penting!)
Laman web baharu memerlukan masa berminggu-minggu untuk ditemui oleh Google secara semula jadi. Daftarkannya sendiri untuk mempercepatkan proses carian (dalam masa 24-48 jam):
1. Pergi ke [Google Search Console](https://search.google.com/search-console).
2. Daftar masuk menggunakan akaun Gmail anda.
3. Tambah properti baharu (**URL Prefix**) dengan memasukkan URL penuh Vercel anda: 
   `https://banting-desa-idaman-residency.vercel.app/`
4. Pilih kaedah pengesahan **HTML Tag**. Google akan memberikan satu baris kod seperti:
   `<meta name="google-site-verification" content="KOD_ANDA" />`
5. Tampal kod tersebut ke dalam fail `index.html` anda (pada bahagian `<head>`, di bawah tajuk) lalu lakukan `git push`. Selepas itu, klik **Verify** pada Google Search Console.
6. Selepas disahkan, klik menu **Sitemaps** di bahagian kiri menu Google Search Console dan masukkan: `sitemap.xml` untuk diserahkan kepada Google.

---

## 📍 Langkah 3: Gunakan Google Business Profile (Tempatan)
Bagi carian tempatan seperti *"Rumah Semi-D Olak Lempit"*, Google biasanya akan memaparkan peta Google Maps terlebih dahulu. Ini adalah cara terpantas untuk berada di tangga #1:
1. Pergi ke [Google Business Profile](https://www.google.com/business/).
2. Daftar profil perniagaan baharu bagi projek perumahan ini (contoh: *Taman Desa Idaman @ Olak Lempit*).
3. Masukkan alamat, waktu operasi, dan **pautan ke laman web Vercel anda**.
4. Apabila pelanggan mencari rumah di Google, Google Maps Listing anda akan muncul di bahagian atas dengan butang pautan terus ke landing page ini.

---

## 🔗 Langkah 4: Bina Pautan Luar (Backlinks)
Google menilai kualiti dan autoriti laman web anda berdasarkan bilangan laman web lain yang memautkan kembali (link back) ke URL anda:
* Kongsi URL laman web anda di akaun media sosial rasmi (Facebook Pages, Instagram, TikTok, LinkedIn).
* Tampal pautan laman web anda di portal-portal hartanah utama (Mudah.my, PropertyGuru, iProperty) dalam bahagian penerangan profil atau iklan anda.
* Terbitkan artikel pengenalan projek ini di blog-blog perumahan tempatan sekiranya ada.
