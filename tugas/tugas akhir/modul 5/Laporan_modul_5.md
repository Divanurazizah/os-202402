# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Diva Nur Azizah>`
**NIM**: `<240202859>`
**Modul yang Dikerjakan**:
`(Modul 5 – Audit dan Keamanan Sistem (xv6-public))`

---

## 📌 Deskripsi Singkat Tugas

Pada modul ini, saya mengimplementasikan fitur audit log di xv6 untuk merekam setiap pemanggilan system call.
Selain itu, saya juga menambahkan mekanisme kontrol akses agar hanya proses tertentu (PID 1 / init) yang dapat membaca log tersebut melalui syscall khusus.

---

## 🛠️ Rincian Implementasi



* Menambahkan struktur `audit_entry` di `syscall.c` untuk menyimpan PID, nomor syscall, dan tick (waktu).
* Memodifikasi fungsi `syscall()` di `syscall.c` untuk mencatat setiap pemanggilan syscall yang valid ke dalam array `audit_log`.
* Menambahkan syscall baru `get_audit_log()` di `sysproc.c` untuk mengirim isi log ke proses pengguna.
* Membatasi akses `get_audit_log()` hanya untuk proses dengan PID 1 (init) demi keamanan.
* Memperbarui file header:
    * `defs.h` — deklarasi fungsi kernel tambahan.
    * `user.h` — deklarasi fungsi syscall di level user.
    * `syscall.h` — penambahan nomor syscall baru.
    * `usys.S` — registrasi syscall.
* Menambahkan program uji `audit.c` untuk membaca dan menampilkan isi log.
* Mengedit `Makefile` untuk menambahkan program `audit`.

---

## ✅ Uji Fungsionalitas

`audit`: untuk melihat isi log system call (jika dijalankan oleh PID 1)


---

## 📷 Hasil Uji



### 📍 Output `audit`:

```
$ audit
=== Audit Log ===
[0] PID=1 SYSCALL=7 TICK=2
[1] PID=1 SYSCALL=15 TICK=4
...
```

<img width="1366" height="768" alt="Screenshot (97)" src="https://github.com/user-attachments/assets/e96bae4d-2f35-4894-a9ce-d74e94257f49" />


```

---




## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

* Awalnya semua proses bisa membaca log → perlu validasi PID di `sys_get_audit_log()`.
* Saat buffer penuh `(audit_index >= MAX_AUDIT)`, log baru tidak tersimpan → harus disadari sebagai keterbatasan implementasi.
* Jika menjalankan `audit` langsung di shell, hasil selalu “Access denied” karena PID ≠ 1.


---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
