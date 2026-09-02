---
date: '2026-06-06'
description: Pelajari cara mengambil metadata dan mengekstrak metadata dokumen menggunakan
  GroupDocs.Redaction .NET, memungkinkan manajemen dokumen yang kuat dan kepatuhan.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Cara Mengambil Metadata dengan GroupDocs.Redaction .NET API
type: docs
url: /id/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Cara Mengambil Metadata dengan GroupDocs.Redaction .NET

Di era digital saat ini, **cara mengambil metadata** dari sebuah file adalah langkah mendasar untuk aplikasi yang berfokus pada dokumen. Baik Anda perlu membaca metadata file untuk audit kepatuhan, mengekstrak properti dokumen untuk pengindeksan, atau sekadar menampilkan ukuran dokumen di UI, GroupDocs.Redaction .NET memberikan API yang ringkas untuk melakukannya dalam beberapa baris C#. Tutorial ini memandu Anda melalui seluruh proses, mulai dari penyiapan lingkungan hingga menampilkan informasi yang diambil, sehingga Anda dapat segera mengekstrak metadata dokumen.

## Jawaban Cepat
- **Apa metode utama untuk mendapatkan metadata?** Panggil `Redactor.GetDocumentInfo()` pada instance `Redactor`.  
- **Format apa yang didukung?** Lebih dari 50 format input dan output, termasuk PDF, DOCX, XLSX, PPTX, dan tipe gambar.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi percobaan gratis dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya memproses file besar?** Ya—GroupDocs.Redaction menangani dokumen ratusan halaman tanpa memuat seluruh file ke memori.  
- **Apakah dukungan async tersedia?** API dapat dibungkus dalam pola async untuk menjaga responsifitas thread UI.

## Apa itu pengambilan metadata di GroupDocs.Redaction?
Pengambilan metadata adalah proses mengakses properti bawaan dokumen—seperti tipe file, jumlah halaman, dan ukuran—melalui API perpustakaan. Dengan mengekstrak properti ini, pengembang dapat secara programatis menilai karakteristik dokumen, mendukung pengindeksan, menegakkan aturan kepatuhan, dan membuat keputusan yang tepat tentang langkah pemrosesan selanjutnya.

## Cara Mengambil Metadata Dokumen?
Kelas `Redactor` adalah antarmuka utama untuk memuat dan memeriksa dokumen di GroupDocs.Redaction.  
`GetDocumentInfo()` adalah metode yang mengembalikan objek `DocumentInfo` yang berisi metadata dokumen.  

Muat file Anda dengan `new Redactor("path/to/file")` dan panggil `GetDocumentInfo()`—pemanggilan ini mengembalikan objek `DocumentInfo` yang berisi tipe, jumlah halaman, ukuran, dan properti lainnya. Pendekatan dua langkah ini bekerja untuk semua format yang didukung dan tidak memerlukan konfigurasi tambahan. Anda kemudian dapat membaca bidang seperti `FileType`, `PageCount`, dan `FileSize` untuk menampilkan atau mencatat informasi tersebut.

## Prasyarat

- **GroupDocs.Redaction .NET** versi 21.6 atau lebih baru.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, atau .NET 5/6+.  
- Pengetahuan dasar C# dan IDE pengembangan (Visual Studio, Rider, dll.).

## Menyiapkan GroupDocs.Redaction untuk .NET

Memulai dengan GroupDocs.Redaction sangat mudah. Instal paket menggunakan salah satu metode berikut:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Atau, gunakan **NuGet Package Manager UI**: Cukup cari “GroupDocs.Redaction” dan klik **Install**.

### Akuisisi Lisensi

Untuk mencoba GroupDocs.Redaction, Anda dapat memperoleh lisensi percobaan gratis. Untuk pengembangan berkelanjutan atau penggunaan produksi, beli lisensi penuh atau minta lisensi sementara dari situs resmi.

Setelah terinstal, inisialisasi perpustakaan sebagai berikut:

```csharp
using GroupDocs.Redaction;
```

## Panduan Implementasi

### Fitur Mengambil Informasi Dokumen

Fitur ini berfokus pada mengekstrak metadata penting dari dokumen menggunakan GroupDocs.Redaction .NET. Ikuti langkah-langkah berikut:

#### Langkah 1: Siapkan Jalur Dokumen Anda

Tentukan jalur absolut atau relatif ke file target:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Ganti `YOUR_DOCUMENT_DIRECTORY` dengan folder yang berisi dokumen Anda.

#### Langkah 2: Inisialisasi Instance Redactor

Buat objek `Redactor` yang memberikan akses ke metode metadata:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Langkah 3: Ambil Informasi Dokumen

Panggil `GetDocumentInfo()` pada instance `Redactor` untuk mengambil semua properti yang tersedia:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Objek yang dikembalikan mencakup tipe file, jumlah halaman, dan ukuran file.

#### Langkah 4: Tampilkan Detail Dokumen

Keluarkan informasi ke konsol atau UI. Kode contoh (diberi komentar untuk dijalankan secara mandiri) menunjukkan cara mencetak setiap properti:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Mengapa Menggunakan GroupDocs.Redaction untuk Ekstraksi Metadata?
GroupDocs.Redaction mendukung **lebih dari 50 format file** dan dapat memproses dokumen hingga **2 GB** ukuran sambil menjaga konsumsi memori di bawah **100 MB** untuk beban kerja tipikal. Perpustakaan mengekstrak metadata tanpa memuat seluruh dokumen, memberikan respons cepat—sering kali di bawah **200 ms** untuk PDF 100‑halaman pada perangkat keras server standar.

### Masalah Umum dan Solusinya
- **Jalur file tidak tepat** – Verifikasi string jalur dan pastikan file dapat diakses oleh proses yang berjalan.  
- **Format tidak didukung** – Periksa daftar format; jika suatu format tidak ada, pertimbangkan untuk mengonversinya terlebih dahulu.  
- **Kendala kinerja** – Untuk file yang sangat besar, aktifkan opsi streaming atau proses halaman secara batch untuk membatasi penggunaan memori.

## Aplikasi Praktis

Memahami metadata dokumen memungkinkan beberapa skenario dunia nyata:

1. **Sistem Manajemen Dokumen (DMS)** – Otomatisasi pengkategorian dan pengindeksan berdasarkan tipe, ukuran, atau jumlah halaman.  
2. **Audit Kepatuhan** – Verifikasi bahwa file rahasia memiliki metadata yang diperlukan sebelum diarsipkan.  
3. **Migrasi Data** – Kelompokkan file berdasarkan properti untuk mempermudah tugas migrasi massal.  

## Pertimbangan Kinerja

- **Penggunaan Sumber Daya Efisien** – Gunakan instance `Redactor` dalam blok `using` untuk menjamin pembuangan yang tepat.  
- **Pola Asinkron** – Bungkus panggilan metadata dalam `Task.Run` atau implementasikan pembungkus async untuk menjaga responsifitas thread UI pada aplikasi desktop atau web.

## Pertanyaan yang Sering Diajukan

**Q: Format dokumen apa yang dapat saya ekstrak metadata-nya?**  
A: GroupDocs.Redaction membaca metadata dari lebih dari 50 format, termasuk PDF, DOCX, XLSX, PPTX, HTML, dan tipe gambar umum.

**Q: Bagaimana cara menangani file yang dilindungi kata sandi?**  
A: Berikan kata sandi ke konstruktor `Redactor`; API akan mendekripsi file sebelum mengekstrak metadata.

**Q: Apakah ada batas ukuran file yang dapat saya proses?**  
A: Meskipun tidak ada batas keras, file yang lebih besar dari 2 GB mungkin memerlukan penyesuaian memori tambahan; kinerja tetap linear dengan ukuran file.

**Q: Dapatkah saya mengambil metadata dalam operasi batch?**  
A: Ya—iterasi koleksi jalur file dan panggil `GetDocumentInfo()` untuk masing‑masing; perpustakaan aman untuk thread sehingga dapat dijalankan secara paralel.

**Q: Apakah saya memerlukan lisensi untuk build pengembangan?**  
A: Lisensi percobaan gratis cukup untuk pengembangan dan pengujian; lisensi komersial diperlukan untuk penyebaran produksi.

## Sumber Daya

- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

## Kesimpulan

Anda kini memiliki panduan lengkap langkah‑demi‑langkah tentang **cara mengambil metadata** menggunakan GroupDocs.Redaction .NET. Dengan memanfaatkan metode `Redactor.GetDocumentInfo()`, Anda dapat dengan cepat membaca metadata file, mendukung alur kerja kepatuhan, dan meningkatkan pipeline pemrosesan dokumen apa pun. Jelajahi fitur Redaction tambahan—seperti redaksi konten, watermarking, dan konversi dokumen—untuk membangun solusi manajemen dokumen yang sepenuhnya lengkap.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Author:** GroupDocs  

## Tutorial Terkait

- [How to Extract Document Metadata from Streams Using GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)