---
date: '2026-07-20'
description: Pelajari cara menyunting dokumen, menyembunyikan informasi sensitif,
  dan menyimpan file yang telah disunting ke dalam memory stream menggunakan GroupDocs.Redaction
  untuk .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Cara menyunting dokumen dengan GroupDocs.Redaction untuk .NET. Ikuti
  panduan langkah demi langkah ini untuk menyembunyikan informasi sensitif dan menyimpan
  file yang disunting ke dalam memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Cara Menyunting Dokumen dengan GroupDocs.Redaction untuk .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Cara Menyunting Dokumen dengan GroupDocs.Redaction untuk .NET – Panduan Lengkap
type: docs
url: /id/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Cara Menyensor Dokumen dengan GroupDocs.Redaction untuk .NET

Dalam lingkungan perusahaan modern, **cara menyensor dokumen** adalah keterampilan penting untuk melindungi data pribadi, rahasia dagang, dan informasi terkait kepatuhan. Panduan ini memandu Anda melalui proses menyensor informasi sensitif dari file Word, PDF, atau gambar dan kemudian menyimpan output yang disensor langsung ke memory stream—semua dengan GroupDocs.Redaction untuk .NET.

## Jawaban Cepat
- **Apa yang dilakukan penyensoran?** Itu secara permanen menggantikan konten yang dipilih dengan placeholder atau menghapusnya, memastikan data tidak pernah dapat dipulihkan.  
- **Format apa yang didukung?** Lebih dari 30 jenis file, termasuk PDF, DOCX, PPTX, dan format gambar umum.  
- **Bisakah saya menyensor tanpa menulis ke disk?** Ya—simpan hasilnya ke `MemoryStream` untuk pemrosesan dalam memori.  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi penuh diperlukan untuk penggunaan produksi; percobaan gratis tersedia untuk evaluasi.  
- **Apakah kompatibel dengan .NET Core?** Tentu—GroupDocs.Redaction bekerja dengan .NET Framework 4.6+, .NET Core 3.1+, dan .NET 5/6/7.

## Apa itu Penyensoran Dokumen?
Penyensoran dokumen secara permanen menghapus atau menyamarkan teks, gambar, dan metadata rahasia dari sebuah file, memastikan bahwa konten yang disembunyikan tidak dapat dipulihkan, dilihat, atau diekstrak kemudian. Ini menggantikan elemen sensitif dengan placeholder seperti persegi hitam atau teks khusus, dan memperbarui struktur dokumen sehingga data yang disensor tidak dapat dipulihkan.

## Mengapa Menggunakan GroupDocs.Redaction untuk Menyensor Dokumen?
GroupDocs.Redaction mendukung **lebih dari 30 format file** dan dapat menangani file hingga **2 GB** tanpa memuat seluruh dokumen ke dalam memori, memberikan **waktu pemrosesan 30 % lebih cepat** dibandingkan banyak pesaing. API-nya memungkinkan Anda menerapkan penyensoran frasa tepat, ekspresi reguler, atau berbasis gambar dengan satu panggilan metode, menjadikannya pilihan paling efisien untuk pengembang .NET.

## Prasyarat
- **Paket NuGet GroupDocs.Redaction** (versi terbaru).  
- .NET Framework 4.6+ **atau** .NET Core 3.1+ terpasang.  
- IDE yang kompatibel dengan C# seperti Visual Studio 2022.  
- Pengetahuan dasar C# dan familiaritas dengan file I/O.

### Perpustakaan dan Versi yang Diperlukan
- **GroupDocs.Redaction** – selalu gunakan rilis terbaru untuk mengakses algoritma penyensoran terbaru dan patch keamanan.  
- **System.IO** – untuk penanganan stream (bawaan .NET).

### Langkah-langkah Akuisisi Lisensi
- **Percobaan Gratis:** Daftar di situs web GroupDocs untuk percobaan 30 hari.  
- **Lisensi Sementara:** Minta kunci sementara untuk pengujian pengembangan.  
- **Lisensi Penuh:** Beli lisensi produksi untuk penggunaan tak terbatas.

## Inisialisasi dan Penyiapan Dasar
Kelas `Redactor` adalah titik masuk untuk semua operasi penyensoran di GroupDocs.Redaction. Setelah Anda menginstal paket NuGet, Anda membuat instance `Redactor` dengan jalur ke dokumen sumber.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Cara Menyensor Teks Spesifik dalam Dokumen?
Untuk menyensor teks spesifik, muat file sumber dengan instance `Redactor`, lalu terapkan `ExactPhraseRedaction` yang menargetkan string tepat yang ingin Anda sembunyikan. API memindai dokumen, menggantikan setiap kecocokan dengan overlay yang dipilih, dan mencatat perubahan dalam log perubahan, memungkinkan Anda memverifikasi penyensoran sebelum menyimpan.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

Kelas `ExactPhraseRedaction` menggantikan setiap kemunculan frasa tepat dengan persegi hitam (atau placeholder khusus apa pun yang Anda konfigurasikan).  

**Langkah‑per‑Langkah:**
1. **Muat** – Buat instance `Redactor` yang mengarah ke file Anda.  
2. **Terapkan** – Panggil `Apply` dengan `ExactPhraseRedaction` (atau tipe penyensoran lain).  
3. **Periksa** – Tinjau `RedactorChangeLog` untuk mengonfirmasi berapa banyak kecocokan yang ditemukan dan diganti.  

## Cara Menyimpan Dokumen yang Disensor ke Memory Stream?
`MemoryStream` adalah stream .NET yang menyimpan data di memori, memungkinkan baca/tulis cepat tanpa I/O disk. Dengan menggunakan metode `Save`, Anda dapat mengarahkan output yang disensor ke `MemoryStream`, yang kemudian dapat dikirim melalui jaringan, disimpan dalam basis data, atau dikembalikan langsung dari endpoint API tanpa membuat file sementara.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Poin Penting:**
- Metode `Save` menulis output yang disensor ke implementasi `Stream` apa pun, termasuk `MemoryStream`.  
- Tidak ada file sementara yang dibuat, yang meningkatkan keamanan dan kinerja.  
- Anda dapat menggabungkannya dengan `FileStreamResult` ASP.NET Core untuk mengembalikan file langsung ke browser.

## Kesalahan Umum dan Solusinya
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Penyensoran tidak diterapkan** | Kasus huruf pada frasa berbeda dari sumber. | Gunakan `ExactPhraseRedaction("John Doe", caseSensitive: false)` atau penyensoran ekspresi reguler untuk pencocokan fleksibel. |
| **File besar menyebabkan OutOfMemory** | Mencoba memuat seluruh file ke memori. | GroupDocs.Redaction melakukan streaming data secara internal; pastikan Anda menggunakan versi terbaru yang memproses file dalam potongan. |
| **File yang disimpan rusak** | Stream tidak direset sebelum dikirim. | Setelah `redactor.Save(stream)`, setel `stream.Position = 0` sebelum membaca atau mengembalikannya. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menyensor file PDF menggunakan API yang sama?**  
A: Ya—GroupDocs.Redaction memperlakukan PDF, DOCX, PPTX, dan banyak format gambar secara seragam; cukup arahkan `Redactor` ke file PDF.

**Q: Apakah penyensoran tetap ada setelah mengonversi dokumen ke format lain?**  
A: Tentu—setelah disensor, konten dihapus secara permanen, terlepas dari konversi selanjutnya.

**Q: Bagaimana cara menyesuaikan tampilan penyensoran?**  
A: Gunakan `RedactionOptions` untuk mengatur warna overlay, opasitas, atau mengganti teks dengan string khusus.

**Q: Apakah memungkinkan menyensor menggunakan ekspresi reguler?**  
A: Ya—`RegexRedaction` memungkinkan Anda mendefinisikan pola seperti nomor kartu kredit atau alamat email.

**Q: Versi .NET apa yang secara resmi didukung?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, dan .NET 7.

**Terakhir Diperbarui:** 2026-07-20  
**Diuji Dengan:** GroupDocs.Redaction 23.12 for .NET  
**Penulis:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Tutorial Terkait

- [Cara Memuat dan Menyensor Dokumen Menggunakan GroupDocs.Redaction .NET&#58; Panduan Lengkap](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Simpan Dokumen yang Disensor dalam Format Asli Menggunakan GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Penyensoran Dokumen Aman di .NET Menggunakan Streams&#58; Panduan untuk GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)