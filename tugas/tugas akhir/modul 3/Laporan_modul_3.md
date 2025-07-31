<img width="1366" height="768" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/0ff5e15c-e708-47a7-9cda-d04413ae4967" /># 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Diva Nur Azizah>`
**NIM**: `<240202859>`
**Kelas**: `<2IKRA>`
**Modul yang Dikerjakan**:
`(Modul 3 — Manajemen Memori Tingkat Lanjut (xv6-public x86))`

---

## 📌 Deskripsi Singkat Tugas

  Pada modul ini saya mengimplementasikan dua fitur penting di xv6:
* Copy-on-Write Fork (CoW Fork) — optimisasi `fork()` agar tidak langsung menyalin seluruh memori proses, melainkan berbagi halaman memori secara read-only, lalu menyalin hanya saat ada penulisan (write).
* Shared Memory — menambahkan mekanisme `shmget()` dan `shmrelease()` untuk memungkinkan dua atau lebih proses berbagi segmen memori.
Tujuan modul ini adalah mengoptimalkan kinerja proses `fork` dan menyediakan mekanisme berbagi data antar proses.
---

## 🛠️ Rincian Implementasi

Copy-on-Write Fork
* Menambahkan fungsi baru `cowuvm()` di `vm.c` untuk membuat page table dengan halaman read-only bersama.
* Memodifikasi `fork()` di `proc.c` untuk memanggil `cowuvm()` alih-alih `copyuvm()`.
* Menambahkan penanganan page fault di `trap.c` untuk mendeteksi penulisan ke halaman read-only, lalu melakukan salin halaman (copy-on-write).
* Menambahkan bit `PTE_COW` di `mmu.h` untuk menandai halaman copy-on-write.
* Memodifikasi `freevm()` dan reference count untuk mendukung halaman bersama.

Shared Memory
* Mendefinisikan `MAX_SHM` di param.h dan membuat tabel global `shmtab` untuk menyimpan informasi shared memory.
* Menambahkan deklarasi dan implementasi `sys_shmget()` dan `sys_shmrelease()` di `sysproc.c`.
* Memanggil `mappages()` untuk memetakan frame shared memory ke alamat virtual di dekat `USERTOP`.
* Menambahkan prototipe fungsi di `defs.h` dan memastikan `myproc()` digunakan alih-alih variabel `proc`.
* Mendefinisikan `USERTOP` di `memlayout.h`.
---

## ✅ Uji Fungsionalitas

Program uji yang digunakan:

* cowtest — menguji apakah `fork()` tidak langsung menyalin memori, tapi baru menyalin saat ada penulisan.
* shmtest — menguji apakah dua proses dapat berbagi segmen memori yang sama melalui `shmget()` dan `shmrelease()`.

---

## 📷 Hasil Uji

<img width="1366" height="768" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/617c3adb-74a8-4d52-81bc-a8e9d3dce4e9" />

### 📍 Contoh Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

<img width="1366" height="768" alt="Screenshot (100)" src="https://github.com/user-attachments/assets/2c6b55d0-7b72-4dba-9a6f-5977d8c24b2e" />

### 📍 Contoh Output `shmtest`:

```
Child reads: A
Parent reads: B
```

## ⚠️ Kendala yang Dihadapi



* `cowuvm` awalnya tidak dikenali karena salah penempatan deklarasi (harus di `defs.h`).
* Error `proc undeclared` di `sysproc.c` karena harus menggunakan `myproc()` bukan variabel global `proc`.
* `USERTOP` belum didefinisikan sehingga harus ditambahkan di `memlayout.h`.
* Beberapa error kompiler karena `MAX_SHM` dan `shmtab` belum dideklarasikan di file header yang tepat.
* Penanganan page fault harus hati-hati agar tidak memicu panic kernel.


---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
