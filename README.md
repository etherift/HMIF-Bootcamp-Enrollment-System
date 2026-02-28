# 🎓 HMIF Bootcamp Enrollment System

![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![Next.js](https://img.shields.io/badge/Next.js-15-black.svg)
![Supabase](https://img.shields.io/badge/Supabase-Database-3ECF8E.svg)
![TypeScript](https://img.shields.io/badge/TypeScript-Ready-3178C6.svg)

Platform pendaftaran online berbasis web untuk program bootcamp dan pelatihan yang diselenggarakan oleh **Himpunan Mahasiswa Informatika (HMIF) - Fakultas Teknik, Universitas Tanjungpura** (Pontianak, Kalimantan Barat).

## 📑 Daftar Isi
- [Project Overview](#-project-overview)
- [Problem Statement](#-problem-statement)
- [Solution](#-solution)
- [Features](#-features)
- [User Roles](#-user-roles)
- [Requirements](#-requirements)
- [Technical Specifications](#-technical-specifications)
- [Database Schema](#-database-schema)
- [Workflow](#-workflow)

---

## 🎯 Project Overview
**Tujuan:** Website pendaftaran online untuk program bootcamp/pelatihan HMIF dengan UI *full* Bahasa Indonesia.

* **Visi:** Menyediakan platform pendaftaran bootcamp yang modern, *user-friendly*, dan efisien untuk mahasiswa dan pelajar di Pontianak.
* **Misi:** * Mempermudah proses pendaftaran dengan form digital yang simpel.
  * Meningkatkan transparansi status pendaftaran peserta.
  * Membantu panitia HMIF mengelola pendaftaran secara efisien.
  * Menampilkan riwayat bootcamp sebelumnya untuk meningkatkan kredibilitas.

---

## ⚠️ Problem Statement
Sebelum adanya sistem ini, HMIF menghadapi beberapa tantangan:
1. **Proses Pendaftaran Manual:** Menggunakan Google Forms/Excel, data tersebar, dan sulit melacak status.
2. **Beban Kerja Admin:** Panitia kesulitan mengelola ratusan pendaftaran, proses *review* lambat, dan notifikasi email manual.
3. **Kurangnya Transparansi:** Peserta tidak tahu status pendaftaran mereka dan tidak ada notifikasi otomatis.
4. **UX Kurang Optimal:** Form tidak menarik, tidak ada validasi *real-time*, dan kurang *mobile-friendly*.
5. **Tidak Ada Data Historis:** Calon peserta tidak bisa melihat *success stories* atau galeri alumni dari cohort sebelumnya.

---

## 💡 Solution
Sistem Pendaftaran Berbasis Web dengan fitur unggulan:
* **Modern Scrollytelling Landing Page:** Desain setara Awwwards dengan animasi *image sequence* untuk menarik perhatian.
* **Simple 2-Step Registration Form:** Form input yang ringkas tanpa *upload* dokumen berat, lengkap dengan fitur *auto-save draft*.
* **Real-Time Status Tracking:** Dashboard khusus untuk peserta mengecek status pendaftaran dan menerima notifikasi email otomatis.
* **Admin Panel Terpusat:** Manajemen data pelamar, fitur *approve/reject* dengan catatan, dan ekspor ke CSV.
* **Bootcamp History Showcase:** Menampilkan data cohort sebelumnya, *success stories*, dan galeri.

---

## ✨ Features

### 1. Landing Page (Public)
* **Hero Section:** Animasi *image sequence* (240 frames) berbasis Canvas yang digerakkan oleh *scroll*. CTA "Daftar Sekarang".
* **About & Program Features:** Animasi teks dan layout Bento Grid dengan efek *hover* (scale + glow) untuk fitur program.
* **Bootcamp History:** Filter tahun (2025), kartu cohort, dan halaman detail (statistik, galeri lightbox).
* **Stats & Testimonials:** Animasi angka *count-up* dan *slider autoplay* layar penuh untuk testimoni.
* **Timeline:** Visualisasi alur pendaftaran.

### 2. Registration Form (Protected)
* **Step 1 (Data Pribadi):** Nama Lengkap, Email, Nomor HP, Kategori, Universitas (Kondisional), Program Studi, Semester.
* **Step 2 (Review & Konfirmasi):** Ringkasan data, persetujuan Syarat & Ketentuan, tombol *Submit*.

### 3. User Dashboard (Protected)
* Kartu Status Aplikasi (Konsep, Terkirim, Review, Diterima, Ditolak).
* Timeline progres pendaftaran.
* Akses edit *draft* dan unduh Surat Penerimaan (PDF).

### 4. Admin Dashboard & Manajemen
* **Applications Table:** Kelola pendaftaran dengan filter, pencarian, dan ekspor CSV.
* **Application Detail:** Modal untuk *review* pelamar beserta tombol *Terima* / *Tolak* dan catatan.
* **Manage Cohorts:** CRUD data angkatan, status angkatan (Draft, Active, Completed, Cancelled), dan unggah media.

### 5. Automated Email Notifications (Resend API)
* Email Welcome, Application Submitted, Under Review, Accepted (beserta PDF lampiran), dan Rejected (beserta catatan).

---

## 👥 User Roles
* **Public:** Melihat *landing page*, riwayat, dan detail cohort.
* **Applicant:** Mengisi form pendaftaran, melacak status, dan mengedit *draft*.
* **Admin/Reviewer:** Mengelola pendaftaran, mengelola cohort, dan mengirim notifikasi.

---

## 📋 Requirements

### Functional Requirements
* **FR-1:** Manajemen User (Registrasi, login, reset password).
* **FR-2:** Form pendaftaran 2 langkah, *auto-save*, validasi.
* **FR-3:** Pelacakan status dan unduh surat penerimaan.
* **FR-4:** Panel admin (*filter, search, approve/reject*, CSV).
* **FR-5:** Manajemen cohort (CRUD, unggah media).
* **FR-6:** Notifikasi email otomatis berdasarkan *trigger*.
* **FR-7:** Halaman publik dengan *scrollytelling*.
* **FR-8:** Proteksi rute dan *role-based access*.

### Non-Functional Requirements
* **Performance:** *Load time* < 3 detik, animasi mulus 60fps.
* **Usability:** Responsif (*Mobile First*), validasi *real-time*.
* **Security:** *Password hashing*, proteksi SQLi/XSS, CSRF *tokens*.
* **Reliability & Scalability:** 99.9% *uptime*, *backup* harian, mendukung 1000+ *user concurrent*.
* **Maintainability:** Kode modular (React Components), TypeScript.

---

## 🛠️ Technical Specifications
* **Frontend:** Next.js 15 (App Router), TypeScript, Tailwind CSS, shadcn/ui.
* **Animation:** Framer Motion, GSAP/Lenis (Scroll), Canvas API.
* **Backend:** Supabase (PostgreSQL, Auth, Storage).
* **Email:** Resend API.
* **Deployment:** Vercel.

---

## 🗄️ Database Schema (Ringkasan)
* `users`: Menyimpan data akun (email, nama, role).
* `applications`: Menyimpan data pendaftaran, status, dan data pribadi.
* `notifications`: Riwayat notifikasi sistem.
* `cohorts`: Data angkatan bootcamp (deskripsi, tahun, status).
* `cohort_members`: Relasi antara `users` dan `cohorts` (peserta yang diterima).

---

## 🔄 Workflow

**Alur Pendaftaran User:**
1. Kunjungi Landing Page → Klik "Daftar".
2. Registrasi Akun → Terima Email Welcome.
3. Login → Isi Form Step 1 (*Auto-save*) → Review di Step 2.
4. Submit → Status berubah "Terkirim".
5. Pantau Dashboard untuk status selanjutnya.

**Alur Review Admin:**
1. Login sebagai Admin → Buka Admin Dashboard.
2. Filter/Search aplikasi yang masuk.
3. Buka detail aplikasi → Lakukan *Review*.
4. **Terima:** Status jadi "Accepted" → Email penerimaan + PDF terkirim.
5. **Tolak:** Isi catatan → Status jadi "Rejected" → Email penolakan terkirim.

---
*Dokumentasi ini dirilis pada 16 Februari 2026 - Versi 1.0*
