---
date: 2026-06-11
description: Pelajari cara mengekspor file yang disensor, mengonfigurasi folder output,
  membuat PDF raster, dan menyimpan ke aliran menggunakan GroupDocs.Redaction for
  .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Cara Mengekspor Dokumen yang Disensor dengan GroupDocs.Redaction .NET
type: docs
url: /id/net/document-saving/
weight: 3
---

# Cara Mengekspor Dokumen Redacted dengan GroupDocs.Redaction .NET

Dalam panduan komprehensif ini Anda akan menemukan **cara mengekspor** konten yang telah di‑redact dengan aman dan efisien menggunakan GroupDocs.Redaction untuk .NET. Baik Anda perlu mempertahankan tipe file asli, mengunci dokumen sebagai PDF rasterisasi, atau men-stream hasil langsung di memori, kami akan memandu Anda melalui setiap opsi dengan penjelasan yang jelas, percakapan, dan tip dunia nyata. Pada akhir tutorial ini Anda akan dapat memilih strategi ekspor yang tepat untuk skenario yang didorong oleh kepatuhan.

## Jawaban Cepat
- **Format apa saja yang dapat saya ekspor?** Semua 30+ format native yang didukung oleh GroupDocs.Redaction, plus PDF rasterisasi untuk keamanan maksimal.  
- **Apakah saya memerlukan lisensi untuk streaming?** Ya, lisensi GroupDocs.Redaction yang valid diperlukan untuk streaming produksi.  
- **Bisakah saya mengatur folder output khusus?** Tentu – gunakan properti `OutputPath` atau `SaveOptions` untuk mengkonfigurasinya.  
- **Apakah rasterisasi aman untuk file besar?** Ia menangani dokumen hingga 500 halaman tanpa memuat seluruh file ke memori.  
- **Versi .NET apa yang didukung?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu GroupDocs.Redaction?
GroupDocs.Redaction adalah perpustakaan .NET yang secara programatik menghapus atau menyamarkan informasi sensitif dari PDF, Word, Excel, PowerPoint, gambar, dan banyak format lainnya. Ia menyediakan API tingkat tinggi untuk mendefinisikan wilayah redaksi, menerapkan kebijakan, dan akhirnya mengekspor dokumen yang telah dibersihkan. Ini memudahkan integrasi kemampuan redaksi ke dalam aplikasi .NET apa pun.

## Mengapa Mengekspor Dokumen Redacted sebagai PDF Rasterisasi?
PDF rasterisasi mengubah setiap halaman menjadi gambar datar, menghilangkan lapisan teks tersembunyi yang dapat diekstrak nanti. Format ini menjamin konten yang di‑redact tidak dapat dipulihkan, memenuhi standar regulasi ketat seperti GDPR dan HIPAA. GroupDocs.Redaction dapat menghasilkan PDF rasterisasi hingga 300 dpi, mempertahankan fidelitas visual sambil memastikan keamanan.

## Cara Mengekspor Dokumen Redacted?
Muat file sumber, terapkan aturan redaksi Anda, lalu panggil metode penyimpanan yang sesuai—baik `Save` untuk format asli, `SaveAsRasterizedPdf` untuk PDF hanya‑gambar, atau `SaveToStream` untuk penanganan di memori. Di bawah ini alur kerja langkah‑demi‑langkah. Setiap metode memastikan konten yang di‑redact dihapus secara permanen sambil mempertahankan format output yang diinginkan.

### Langkah 1: Instal Paket NuGet
Tambahkan paket GroupDocs.Redaction terbaru ke proyek Anda:

```bash
dotnet add package GroupDocs.Redaction
```

### Langkah 2: Muat Dokumen dan Tentukan Redaksi
Buat instance `Redactor`, muat file, dan tentukan wilayah yang ingin Anda sembunyikan. Kelas `Redactor` menyediakan fungsionalitas inti untuk memuat dokumen dan menerapkan aturan redaksi.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Langkah 3: Pilih Metode Ekspor
#### Ekspor dalam Format Asli
```csharp
redactor.Save("RedactedReport.docx");
```

#### Ekspor sebagai PDF Rasterisasi
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Ekspor ke Memory Stream (ideal untuk API web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Metode `Save` menulis dokumen yang di‑redact ke file dalam format aslinya. `SaveAsRasterizedPdf` membuat PDF di mana setiap halaman dirender sebagai gambar, menghapus teks tersembunyi apa pun. `SaveToStream` mengembalikan file yang di‑redact sebagai memory stream, cocok untuk respons web.

## Cara Mengonfigurasi Folder Output?
Set properti `OutputPath` pada `Redactor` atau berikan objek `SaveOptions` khusus yang mencakup direktori yang diinginkan. `OutputPath` adalah properti dari `Redactor` yang menentukan folder tempat file output ditulis. `SaveOptions` memungkinkan Anda menyesuaikan berbagai parameter penyimpanan, termasuk folder output. Ini memastikan semua file yang diekspor berada di lokasi yang dapat diprediksi, menyederhanakan pipeline pemrosesan batch. Anda juga dapat menentukan subfolder per tipe dokumen untuk menjaga ruang kerja tetap teratur.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Masalah Umum dan Solusi
- **Redaksi tidak diterapkan:** Pastikan pola pencarian cocok persis dengan teks dokumen; gunakan `RegexOptions.IgnoreCase` bila diperlukan. `RegexOptions` adalah enumerasi yang mengontrol perilaku pencocokan ekspresi reguler, seperti sensitivitas huruf.  
- **File besar menyebabkan tekanan memori:** Aktifkan mode streaming dengan menggunakan `SaveToStream` dan hindari memanggil `Save` pada seluruh dokumen.  
- **PDF rasterisasi terlihat buram:** Tingkatkan DPI di `RasterizationOptions` (misalnya, 300–600) untuk meningkatkan kualitas gambar. `RasterizationOptions` memungkinkan Anda mengatur parameter seperti DPI dan format gambar untuk output PDF rasterisasi.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya mengekspor ke format yang tidak didukung secara asli?**  
J: Ya, GroupDocs.Redaction dapat mengonversi sebagian besar tipe input ke PDF, DOCX, XLSX, PPTX, atau PDF rasterisasi, mencakup lebih dari 30 format.

**T: Bagaimana rasterisasi melindungi data yang di‑redact?**  
J: Dengan merender setiap halaman sebagai gambar datar, semua lapisan teks tersembunyi dihapus, sehingga tidak mungkin mengekstrak konten asli.

**T: Apakah memungkinkan menggabungkan beberapa aturan redaksi?**  
J: Tentu – Anda dapat memanggil `Apply` berulang kali atau memberikan koleksi `RedactionOptions` untuk memproses banyak pola dalam satu kali jalan. `RedactionOptions` mendefinisikan pengaturan untuk satu operasi redaksi, seperti wilayah dan tipe penggantian.

**T: Apakah saya perlu menutup objek Redactor?**  
J: `Redactor` mengimplementasikan `IDisposable`; bungkus dalam blok `using` atau panggil `Dispose()` untuk segera melepaskan handle file. `IDisposable` adalah antarmuka yang menyediakan mekanisme untuk melepaskan sumber daya yang tidak dikelola.

**T: Runtime .NET apa yang secara resmi diuji?**  
J: GroupDocs.Redaction telah divalidasi pada .NET Framework 4.6+, .NET Core 3.1+, dan .NET 5/6/7.

## Sumber Daya Tambahan

### Tutorial yang Tersedia

- [Cara Menyimpan Dokumen sebagai PDF Rasterisasi Menggunakan GroupDocs.Redaction untuk .NET&#58; Panduan Lengkap](./groupdocs-redaction-net-rasterized-pdfs/)
- [Menerapkan Direktori Output di .NET dengan GroupDocs.Redaction&#58; Panduan Komprehensif](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redaksi dan Penyimpanan Dokumen dengan GroupDocs.Redaction untuk .NET&#58; Panduan Lengkap](./redact-save-documents-groupdocs-redaction-net/)
- [Simpan Dokumen Redacted dalam Format Asli Menggunakan GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redaksi Dokumen Aman di .NET Menggunakan Streams&#58; Panduan untuk GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Tautan Berguna

- [GroupDocs.Redaction untuk Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction untuk Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction untuk Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-11  
**Diuji Dengan:** GroupDocs.Redaction 23.11 untuk .NET  
**Penulis:** GroupDocs  

---

## Tutorial Terkait

- [Simpan Dokumen Redacted dalam Format Asli Menggunakan GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Cara Menyimpan Dokumen sebagai PDF Rasterisasi Menggunakan GroupDocs.Redaction untuk .NET: Panduan Lengkap](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Redaksi Dokumen Aman di .NET Menggunakan Streams: Panduan untuk GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)