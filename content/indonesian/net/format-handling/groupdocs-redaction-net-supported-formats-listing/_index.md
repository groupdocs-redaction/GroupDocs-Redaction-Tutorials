---
date: '2026-07-20'
description: Pelajari cara menampilkan daftar format menggunakan GroupDocs.Redaction
  .NET, integrasikan fitur ini ke dalam alur kerja dokumen Anda, dan tingkatkan kinerja.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Temukan cara menampilkan daftar format menggunakan GroupDocs.Redaction
  .NET, lihat panduan langkah demi langkah, dan dapatkan tips untuk kinerja optimal
  dalam aplikasi .NET Anda.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Cara Menampilkan Daftar Format dengan GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Cara Menampilkan Daftar Format dengan GroupDocs.Redaction .NET
type: docs
url: /id/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Cara Menampilkan Daftar Format dengan GroupDocs.Redaction .NET

Mengelola berbagai jenis dokumen adalah kenyataan sehari-hari bagi pengembang yang membangun aplikasi berfokus pada dokumen. Dalam tutorial ini Anda akan belajar **cara menampilkan daftar format** yang dapat ditangani oleh GroupDocs.Redaction .NET, sehingga Anda dapat memvalidasi file sebelum diproses, menyajikan opsi yang akurat kepada pengguna, dan menjaga alur kerja tetap efisien.

## Pendahuluan

Penanganan dokumen yang efisien dimulai dengan mengetahui secara tepat jenis file apa yang didukung oleh pustaka Anda. GroupDocs.Redaction menyediakan metode bawaan untuk mengambil informasi ini, memungkinkan Anda membangun elemen UI dinamis, menegakkan aturan validasi, dan menghindari kesalahan runtime. Di bawah ini Anda akan menemukan semua yang Anda perlukan untuk memulai, mulai dari instalasi hingga contoh kode praktis dan tips kinerja.

### Jawaban Cepat
- **Apa arti “cara menampilkan daftar format”?** Ini merujuk pada pengambilan koleksi ekstensi file yang dapat diproses oleh GroupDocs.Redaction.  
- **Apakah saya memerlukan lisensi?** Ya, lisensi GroupDocs.Redaction yang valid diperlukan untuk penggunaan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Berapa banyak format yang tersedia?** Lebih dari 30 format input dan output didukung secara bawaan.  
- **Apakah diperlukan konfigurasi khusus?** Tidak ada konfigurasi tambahan yang diperlukan selain inisialisasi pustaka standar.

## Apa itu “cara menampilkan daftar format”?

Ini melibatkan pemanggilan API FileType dari pustaka untuk memperoleh koleksi di mana setiap entri berisi ekstensi file dan nama yang dapat dibaca manusia. Pengembang kemudian dapat mengiterasi koleksi ini untuk membangun aturan validasi, mengisi dropdown UI, atau mencatat tipe yang didukung, memastikan hanya dokumen yang kompatibel yang diproses.

## Mengapa menampilkan daftar format dengan GroupDocs.Redaction?

GroupDocs.Redaction mendukung **lebih dari 30** jenis file yang berbeda—termasuk PDF, DOCX, PPTX, dan format gambar—memungkinkan Anda menangani sebagian besar dokumen perusahaan tanpa konverter pihak ketiga. Dengan menampilkan format ini secara programatik Anda menghilangkan tebakan, mengurangi tiket dukungan, dan memastikan hanya file yang kompatibel yang masuk ke pipeline pemrosesan Anda.

## Prasyarat

- **GroupDocs.Redaction untuk .NET** – unduh paket terbaru dari situs resmi.  
- **.NET Framework atau .NET Core** – kompatibel dengan lingkungan pengembangan Anda.  
- **Visual Studio** (atau IDE apa pun yang kompatibel dengan C#).  
- Pemahaman dasar tentang sintaks C#.

## Menyiapkan GroupDocs.Redaction untuk .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### UI NuGet Package Manager
- Cari **“GroupDocs.Redaction”** dan instal versi terbaru.

### Akuisisi Lisensi
GroupDocs menawarkan percobaan gratis, lisensi sementara untuk evaluasi, atau opsi pembelian penuh. Kunjungi situs web GroupDocs untuk mendapatkan file lisensi yang sesuai.

### Inisialisasi dan Penyiapan Dasar
Setelah menambahkan paket, referensikan namespace dan buat instance `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Panduan Implementasi

### Bagaimana cara menampilkan daftar format dengan GroupDocs.Redaction .NET?
Muat pustaka, panggil helper statis, dan urutkan hasilnya—ini memberi Anda koleksi siap pakai dalam hanya dua baris kode. Gunakan `FileType.GetSupportedFileFormats()` untuk mengambil `IEnumerable<FileType>` yang mencakup ekstensi dan nama tampilan setiap format, kemudian urutkan berdasarkan ekstensi untuk daftar UI yang bersih.

### Mengambil Format File yang Didukung

#### Gambaran Umum
Tujuannya adalah mendapatkan daftar jenis file yang dapat ditangani oleh GroupDocs.Redaction, memudahkan integrasi ke dalam logika validasi, dropdown UI, atau mekanisme pencatatan.

#### Implementasi Langkah‑per‑Langkah

**1. Mengambil File Type yang Didukung**  
`FileType.GetSupportedFileFormats()` mengembalikan setiap format yang dikenali pustaka. Metode ini merupakan bagian dari kelas `GroupDocs.Redaction.FileType`, yang menyimpan metadata seperti ekstensi file dan nama yang ramah.

**2. Menampilkan File Type yang Didukung**  
Iterasi koleksi dan keluarkan setiap ekstensi dan deskripsi format. Contoh kode inline:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Potongan kode ini mencetak daftar terurut rapi seperti “.pdf – Portable Document Format”, menjadikannya sempurna untuk mengisi elemen UI.

### Tips Pemecahan Masalah
- **Package Hilang** – Verifikasi referensi paket NuGet dan pulihkan paket jika diperlukan.  
- **Path Lisensi Tidak Benar** – Pastikan file lisensi disalin ke direktori output atau berikan path absolut.  
- **Ekstensi Tidak Didukung** – Jika suatu format tidak terdaftar, pastikan Anda menggunakan versi pustaka terbaru; rilis terbaru menambahkan format tambahan.

## Aplikasi Praktis
Memahami format file yang didukung membuka beberapa skenario dunia nyata:

1. **Sistem Manajemen Dokumen** – Validasi unggahan terhadap daftar yang didukung untuk mencegah kegagalan pemrosesan.  
2. **Keamanan Konten** – Terapkan aturan redaksi hanya pada tipe file yang dapat dimodifikasi dengan aman oleh mesin.  
3. **Pipeline Pemrosesan Batch** – Filter batch file besar sebelum memanggil redaksi, menghemat CPU dan memori.

## Pertimbangan Kinerja
- **Jejak Memori** – Menampilkan format adalah operasi ringan; tidak memuat dokumen apa pun ke memori.  
- **Operasi Batch** – Saat memproses ratusan file, ambil daftar format sekali dan gunakan kembali untuk menghindari panggilan berulang.  
- **Keamanan Thread** – `FileType.GetSupportedFileFormats()` aman untuk thread dan dapat dipanggil dari tugas paralel tanpa sinkronisasi.

## Kesimpulan
Anda kini memiliki pendekatan lengkap dan siap produksi untuk **menampilkan daftar format** menggunakan GroupDocs.Redaction .NET. Dengan mengintegrasikan fitur ini, Anda dapat meningkatkan validasi, memperbaiki pengalaman pengguna, dan menjaga pipeline dokumen Anda tetap kuat.

### Langkah Selanjutnya
- Jelajahi API `Redactor` untuk menerapkan aturan redaksi berdasarkan tipe file.  
- Gabungkan daftar format dengan dropdown front‑end untuk pemilihan file yang mulus.  
- Tinjau panduan kinerja untuk mengoptimalkan pekerjaan batch berskala besar.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengambil daftar format tanpa menginisialisasi instance Redactor?**  
A: Ya, `FileType.GetSupportedFileFormats()` bersifat statis dan tidak memerlukan objek `Redactor`.

**Q: Apakah daftar tersebut mencakup format input dan output?**  
A: Metode ini mengembalikan semua format yang dapat dibaca dan ditulis oleh pustaka; setiap `FileType` menyertakan flag `CanRead` dan `CanWrite`.

**Q: Seberapa sering daftar format yang didukung diperbarui?**  
A: GroupDocs merilis pembaruan format dengan setiap versi pustaka; memeriksa daftar pada runtime memastikan Anda selalu memiliki set terbaru.

**Q: Apakah ada cara untuk menyaring hanya format yang kompatibel dengan PDF?**  
A: Ya, saring koleksi dimana `format.Extension == ".pdf"` atau dimana `format.Name.Contains("PDF")`.

**Q: Apakah pendekatan ini bekerja pada .NET Core 2.1?**  
A: Metode ini memerlukan .NET Core 3.1 atau lebih baru; runtime yang lebih lama tidak didukung.

## Bagian FAQ
1. **Bagaimana cara menginstal GroupDocs.Redaction untuk .NET?**  
   Gunakan perintah CLI `dotnet add package GroupDocs.Redaction` atau instal melalui UI NuGet Package Manager.  

2. **Apa saja masalah umum saat mengambil format yang didukung?**  
   Pastikan semua dependensi dipulihkan dan Anda merujuk ke namespace yang benar (`GroupDocs.Redaction`).  

3. **Bisakah saya menggunakan fitur ini dengan aplikasi non‑.NET?**  
   Tutorial ini berfokus pada .NET, tetapi GroupDocs menyediakan API serupa untuk Java, Python, dan platform lainnya.  

4. **Bagaimana cara mengoptimalkan kinerja saat menggunakan GroupDocs.Redaction?**  
   Gunakan kembali daftar format, hindari memuat dokumen penuh ketika hanya memeriksa kompatibilitas, dan pantau penggunaan memori selama pekerjaan batch.  

5. **Format file apa yang didukung oleh GroupDocs.Redaction?**  
   Pustaka ini mendukung lebih dari 30 format, termasuk PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG, dan banyak lagi. Gunakan `FileType.GetSupportedFileFormats()` untuk melihat daftar lengkap.

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/redaction/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/redaction/33)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-07-20  
**Diuji Dengan:** GroupDocs.Redaction 4.2.0 untuk .NET  
**Penulis:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Tutorial Terkait

- [Tutorial Penanganan Format untuk GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Tutorial Memuat Dokumen dengan GroupDocs.Redaction untuk .NET](/redaction/net/document-loading/)
- [Tutorial Menyimpan Dokumen untuk GroupDocs.Redaction .NET](/redaction/net/document-saving/)