---
date: 2026-06-11
description: Pelajari cara memuat dokumen, termasuk dari streams dan password‑protected
  files, menggunakan GroupDocs.Redaction untuk .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Cara Memuat Dokumen dengan GroupDocs.Redaction untuk .NET
type: docs
url: /id/net/document-loading/
weight: 2
---

# Cara Memuat Dokumen dengan GroupDocs.Redaction untuk .NET

Dalam panduan ini Anda akan menemukan **cara memuat dokumen** ke dalam GroupDocs.Redaction untuk .NET dari berbagai sumber—disk lokal, aliran memori, dan bahkan file yang dilindungi kata sandi. Apakah Anda membangun layanan redaksi, pipeline kepatuhan otomatis, atau utilitas desktop sederhana, menguasai teknik pemuatan ini memungkinkan Anda menyiapkan dokumen apa pun untuk redaksi aman dengan cepat dan dapat diandalkan.

## Jawaban Cepat
- **Apa langkah pertama?** Instal paket NuGet GroupDocs.Redaction dan tambahkan namespace `using GroupDocs.Redaction;`  
- **Bisakah saya memuat PDF dari aliran?** Ya—lewatkan `MemoryStream` yang berisi byte PDF ke konstruktor `RedactionEngine`.  
- **Bagaimana cara membuka file yang dilindungi kata sandi?** Berikan kata sandi sebagai argumen kedua saat membuat `RedactionEngine`.  
- **Apakah ada batas ukuran file?** GroupDocs.Redaction memproses file hingga 2 GB tanpa memuat seluruh file ke memori.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara berfungsi untuk pengujian; lisensi penuh diperlukan untuk penerapan produksi.

## Cara Memuat Dokumen?
`RedactionEngine` adalah kelas inti yang memuat dan menyiapkan dokumen untuk redaksi. Muat dokumen dengan membuat instance `RedactionEngine` menggunakan jalur file (atau aliran) dan, jika diperlukan, kata sandi. Panggilan satu baris ini membaca file, memvalidasi format, dan membangun model dokumen internal yang siap untuk redaksi. Misalnya, memuat PDF dari disk semudah `new RedactionEngine("sample.pdf")`. Ketika kata sandi diperlukan, gunakan `new RedactionEngine("secret.pdf", "MyPassword")`. Memuat dari aliran mengikuti pola yang sama dengan argumen `MemoryStream`.

## Apa itu GroupDocs.Redaction?
GroupDocs.Redaction adalah perpustakaan .NET yang memungkinkan pengembang menemukan dan menghapus secara permanen konten sensitif dari PDF, DOCX, PPTX, dan lebih dari 30 format file lainnya. Ia menawarkan redaksi pixel‑perfect, dukungan OCR, dan pemrosesan batch, menjadikannya ideal untuk aplikasi berbasis kepatuhan yang memerlukan perlindungan data yang andal dan aman di banyak jenis dokumen.

## Mengapa Menggunakan GroupDocs.Redaction untuk Memuat Dokumen?
GroupDocs.Redaction menyediakan mesin streaming berperforma tinggi dan bermemori rendah yang dapat menangani file besar hingga 2 GB, sekaligus mendukung dokumen yang dilindungi kata sandi secara langsung. Kombinasi kecepatan, fleksibilitas, dan keamanan ini menjadikannya pilihan utama bagi pengembang yang perlu memuat dokumen dengan cepat dan aman sebelum menerapkan aturan redaksi.

- **Dukungan format luas:** Menangani **30+** jenis dokumen, termasuk PDF, Word, Excel, PowerPoint, dan file gambar.  
- **Streaming berperforma tinggi:** Memproses file hingga **2 GB** menggunakan mesin streaming bermemori rendah, menghilangkan kebutuhan memuat seluruh file.  
- **Penanganan kata sandi:** Membuka **PDF dan file Office yang dilindungi kata sandi** secara mulus dengan satu overload metode, mengurangi kompleksitas kode.  
- **API thread‑safe:** Memungkinkan pemuatan bersamaan banyak dokumen dalam layanan multi‑thread tanpa kondisi balapan.

## Prasyarat
- .NET 6.0 atau lebih baru (perpustakaan juga mendukung .NET Core 3.1 dan .NET Framework 4.6.1+).  
- Lisensi GroupDocs.Redaction yang valid (lisensi sementara untuk pengujian).  
- Akses ke file dokumen yang ingin Anda redaksi (jalur lokal, array byte, atau aliran).

## Memuat Dokumen dari Berbagai Sumber

### Memuat dari Disk Lokal
Berikan jalur absolut atau relatif ke file saat membangun engine. Perpustakaan secara otomatis mendeteksi format dan menyiapkannya untuk redaksi.

### Memuat dari Memory Stream
Baca file ke dalam `byte[]`, bungkus dalam `MemoryStream`, dan berikan aliran ke konstruktor. Pendekatan ini sempurna untuk API web yang menerima file sebagai unggahan.

### Memuat File yang Dilindungi Kata Sandi
Ketika dokumen terenkripsi, sediakan kata sandi sebagai argumen kedua. Engine mendekripsi file secara langsung dan membuat konten tersedia untuk redaksi tanpa langkah tambahan.

## Masalah Umum dan Solusinya

- **Error: “File format not supported.”**  
  Verifikasi bahwa ekstensi file cocok dengan format yang didukung dan file tidak rusak. GroupDocs.Redaction mendukung lebih dari 30 format; lihat referensi API untuk daftar lengkap.

- **Password‑related exception.**  
  Pastikan string kata sandi benar dan file memang memerlukan kata sandi. Mengirim string kosong ke file yang dilindungi akan memicu kesalahan otentikasi.

- **Out‑of‑memory for very large files.**  
  Gunakan overload streaming (`RedactionEngine(Stream)`) alih-alih memuat file lewat jalur. Ini menjaga penggunaan memori tetap rendah bahkan untuk PDF beratus halaman.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya memuat file DOCX dengan cara yang sama seperti saya memuat PDF?**  
A: Ya—GroupDocs.Redaction secara otomatis mendeteksi format DOCX ketika Anda memberikan jalur file atau aliran, jadi tidak diperlukan kode tambahan.

**Q: Apakah perpustakaan mendukung pemuatan file dari Azure Blob Storage?**  
A: Tentu saja. Ambil blob sebagai array byte atau aliran dan berikan ke konstruktor `RedactionEngine`.

**Q: Apa yang terjadi jika saya memberikan kata sandi yang salah?**  
A: Konstruktor melempar `PasswordIncorrectException`. Tangkap pengecualian ini untuk meminta pengguna memasukkan kata sandi yang benar.

**Q: Apakah memungkinkan memuat beberapa dokumen secara bersamaan?**  
A: Ya—setiap instance `RedactionEngine` bersifat independen dan thread‑safe, memungkinkan pemrosesan paralel dalam layanan latar belakang.

**Q: Apakah saya perlu membuang (dispose) RedactionEngine secara manual?**  
A: Engine mengimplementasikan `IDisposable`. Panggil `Dispose()` atau bungkus dalam blok `using` untuk melepaskan handle file dengan cepat.

## Sumber Daya Tambahan

- [Cara Memuat dan Menyunting Dokumen Menggunakan GroupDocs.Redaction .NET: Panduan Lengkap](./groupdocs-redaction-net-load-redact-documents/)
- [Cara Menyunting Aman Dokumen yang Dilindungi Kata Sandi Menggunakan GroupDocs.Redaction di .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Dokumentasi GroupDocs.Redaction untuk .NET](https://docs.groupdocs.com/redaction/net/)
- [Referensi API GroupDocs.Redaction untuk .NET](https://reference.groupdocs.com/redaction/net/)
- [Unduh GroupDocs.Redaction untuk .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-11  
**Diuji Dengan:** GroupDocs.Redaction 5.5 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Memuat dan Menyunting Dokumen Menggunakan GroupDocs.Redaction .NET: Panduan Lengkap](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Menyunting dan Menyimpan Dokumen dengan GroupDocs.Redaction untuk .NET: Panduan Lengkap](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)