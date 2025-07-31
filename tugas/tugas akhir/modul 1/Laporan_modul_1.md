# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Diva Nur Azizah>`
**NIM**: `<240202859>`
**Kelas**: `<2IKRA>`
**Modul yang Dikerjakan**:
`(Modul 1 – System Call dan Instrumentasi Kernel — xv6-public (x86))`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 1 – System Call dan Instrumentasi Kernel**:
  Menambahkan dua system call baru, yaitu `getpinfo()` untuk melihat proses yang aktif dan `getReadCount()` untuk menghitung jumlah pemanggilan `read()` sejak boot.
---

## 🛠️ Rincian Implementasi

* Menambahkan dua system call baru di file `sysproc.c` dan `syscall.c`
* Mengedit `user.h`, `usys.S`, dan `syscall.h` untuk mendaftarkan syscall
* Menambahkan struktur `struct pinfo` di `proc.h`
* Menambahkan counter `readcount` di kernel
* Membuat dua program uji: `ptest.c` dan `rtest.c`
---

## ✅ Uji Fungsionalitas

* `ptest`: untuk menguji `getpinfo()`
* `rtest`: untuk menguji `getReadCount()`
---

## 📷 Hasil Uji


### 📍 Output `ptest`:

```
$ ptest
PID	MEM	NAME
1	12288	init
2	16384	  sh
3	12288	ptest

```

### 📍 Output `rtest`:

```
$ rtest
Read Count Sebelum: 12
hello
Read Count Setelah: 13

```

<img width="1366" height="768" alt="Screenshot (78)" src="https://github.com/user-attachments/assets/144db6e6-a202-4c55-ae09-1ea19086ed81" />


---

## ⚠️ Kendala yang Dihadapi

* `readcount` tidak dikenali yang menyebabkan error undefined reference
* Salah menambahkan field `priority` pada `struct proc` sehingga menyebabkan gagal kompilasi
* Makefile error karena penggunaan spasi bukan tab
* Output ptest tidak rapi karena proses mencetak secara bersamaan tanpa sinkronisasi

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Chat GPT: [https://chat.openai.com/).

---
