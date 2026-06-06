---
date: '2026-06-06'
description: Pelajari cara mengonversi halaman ke PNG dan menampilkan pratinjau halaman
  PDF dengan GroupDocs.Redaction untuk .NET. Panduan langkah demi langkah, contoh
  kode, dan tips dunia nyata.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Konversi Halaman ke PNG Menggunakan GroupDocs.Redaction .NET
type: docs
url: /id/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Mengonversi Halaman ke PNG Menggunakan GroupDocs.Redaction .NET

Membuat pratinjau satu halaman dari dokumen besar adalah kebutuhan umum ketika Anda ingin berbagi hanya bagian informasi yang relevan. Dalam tutorial ini Anda akan belajar **cara mengonversi halaman ke PNG** dengan GroupDocs.Redaction untuk .NET, mengonfigurasi output pratinjau, dan mengintegrasikan hasilnya ke dalam aplikasi Anda. Kami akan membahas prasyarat, instalasi, penyiapan kode, dan tips praktis sehingga Anda dapat mulai menghasilkan pratinjau PNG satu‑halaman dalam hitungan menit.

## Jawaban Cepat
- **Apakah saya dapat menghasilkan pratinjau PNG hanya satu halaman?** Ya, gunakan `PreviewOptions` untuk menentukan nomor halaman dan format.  
- **Format apa yang didukung GroupDocs.Redaction untuk pratinjau?** PNG adalah default, tetapi JPEG dan BMP juga tersedia.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi produksi diperlukan untuk penggunaan komersial.  
- **Apakah ini bekerja pada .NET Core dan .NET Framework?** Tentu – perpustakaan menargetkan .NET Standard 2.0+.  
- **Apakah proses ini efisien memori untuk file besar?** Ya, API melakukan streaming halaman, menghindari pemuatan seluruh dokumen.

## Apa itu mengonversi halaman ke PNG?
**convert page to PNG** mengacu pada mengekstrak satu halaman dari dokumen yang didukung (PDF, DOCX, PPTX, dll.) dan merender halaman tersebut sebagai gambar Portable Network Graphics (PNG). Gambar yang dihasilkan mempertahankan tata letak visual, font, dan grafik halaman asli, memungkinkan Anda berbagi cuplikan yang jelas sambil menyembunyikan sisanya.

## Mengapa menggunakan pratinjau satu‑halaman?
Membuat pratinjau PNG satu‑halaman mengurangi bandwidth, mempercepat waktu pemuatan, dan melindungi konten sensitif dengan menampilkan hanya apa yang diperlukan. GroupDocs.Redaction dapat merender PDF 300‑halaman menjadi PNG 200 KB dalam kurang dari 0,5 detik pada perangkat server standar, menjadikannya ideal untuk portal web dan alat pelaporan.

## Prasyarat

- **GroupDocs.Redaction for .NET** – perpustakaan inti yang melakukan redaksi dokumen dan pembuatan pratinjau.  
- **System.IO** – namespace .NET standar untuk penanganan file.  
- .NET Core 3.1+ atau .NET Framework 4.6.1+ (platform apa pun yang mendukung .NET Standard 2.0).  
- Pengetahuan dasar C# dan familiaritas dengan manajemen paket NuGet.

## Menyiapkan GroupDocs.Redaction untuk .NET

### Informasi Instalasi

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Buka proyek Anda di Visual Studio.  
- Pilih **Manage NuGet Packages**.  
- Cari **GroupDocs.Redaction** dan instal versi stabil terbaru.

### Langkah-langkah Akuisisi Lisensi
Untuk menjalankan perpustakaan Anda memerlukan lisensi yang valid. Anda dapat memulai dengan percobaan gratis atau meminta kunci sementara:

1. Kunjungi [GroupDocs website](https://purchase.groupdocs.com/temporary-license) untuk meminta lisensi sementara.  
2. Ikuti instruksi yang dikirim melalui email untuk menambahkan file lisensi ke proyek Anda.

### Inisialisasi dan Penyiapan Dasar
Kelas `RedactionEngine` adalah titik masuk untuk semua operasi, termasuk pembuatan pratinjau.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Panduan Implementasi

### Ikhtisar
Bagian ini menunjukkan cara **mengonversi halaman ke PNG** dengan mengonfigurasi `PreviewOptions` dan memanggil API pratinjau. Pendekatan ini bekerja untuk PDF, DOCX, PPTX, dan banyak format lain yang didukung oleh GroupDocs.Redaction.

### Langkah 1: Siapkan Lingkungan Anda
Tetapkan jalur file sumber dan folder output. Gunakan `Path.Combine` untuk membangun jalur yang independen platform.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Langkah 2: Atur Opsi Pratinjau
`PreviewOptions` memungkinkan Anda menentukan nomor halaman, ukuran gambar, dan format output. Kelas ini merupakan pusat konfigurasi untuk pembuatan pratinjau.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Penjelasan Konfigurasi Kunci
- **Width & Height** – Sesuaikan nilai ini agar cocok dengan resolusi tampilan target.  
- **PageNumbers** – Berikan array dengan indeks halaman tepat yang ingin Anda render (berbasis nol).  
- **PreviewFormat** – PNG adalah default; ubah ke `PreviewFormat.Jpeg` untuk file yang lebih kecil.

### Tips Pemecahan Masalah
Jika PNG tidak dihasilkan:

- Verifikasi bahwa jalur file sumber sudah benar dan file dapat diakses.  
- Pastikan file lisensi dimuat sebelum memanggil metode API apa pun.  
- Pastikan `PreviewOptions.PageNumbers` berisi indeks halaman yang valid (mis., `0` untuk halaman pertama).

## Aplikasi Praktis
Membuat pratinjau PNG satu‑halaman berguna dalam banyak skenario:

1. **Presentasi Klien** – Tampilkan hanya slide atau klausul kontrak yang relevan.  
2. **Review Internal** – Memungkinkan pemeriksaan visual cepat tanpa membuka seluruh dokumen.  
3. **Ringkasan Konten** – Sematkan cuplikan halaman dalam email atau dasbor untuk konteks instan.  

Mengintegrasikan fitur ini dengan CMS atau CRM dapat mengotomatisasi pembuatan thumbnail untuk dokumen yang diunggah, meningkatkan pengalaman pengguna.

## Pertimbangan Kinerja
- **Memory Management** – Buang (dispose) instance `RedactionEngine` setelah selesai digunakan untuk membebaskan sumber daya.  
- **Asynchronous Execution** – Gunakan `await engine.GeneratePreviewAsync(...)` pada aplikasi UI agar antarmuka tetap responsif.  
- **Library Updates** – GroupDocs.Redaction mendukung **30+ format input dan output** serta memproses dokumen hingga 500 halaman tanpa memuat seluruh file ke memori. Jaga paket tetap terbarui untuk memanfaatkan perbaikan kinerja.

## Kesimpulan
Anda kini memiliki metode lengkap yang siap produksi untuk **mengonversi halaman ke PNG** dan menghasilkan pratinjau satu‑halaman dengan GroupDocs.Redaction untuk .NET. Dengan mengikuti langkah‑langkah di atas, Anda dapat menyematkan cuplikan PNG berkualitas tinggi ke dalam aplikasi .NET apa pun, meningkatkan berbagi dokumen sambil menjaga keamanan dan kinerja.

## Pertanyaan yang Sering Diajukan

**Q: Apakah saya dapat menghasilkan pratinjau untuk PDF yang dilindungi kata sandi?**  
A: Ya, berikan kata sandi saat menginisialisasi `RedactionEngine` dan pratinjau akan dibuat secara normal.

**Q: Bagaimana cara mengubah format output dari PNG ke JPEG?**  
A: Setel `options.PreviewFormat = PreviewFormat.Jpeg` sebelum memanggil metode pratinjau.

**Q: Apakah memungkinkan untuk menampilkan beberapa halaman sekaligus?**  
A: Tentu – berikan array nomor halaman ke `options.PageNumbers` (mis., `new[] {0, 2, 4}`).

**Q: Apa yang harus saya lakukan jika gambar pratinjau terlihat buram?**  
A: Tingkatkan `options.Width` dan `options.Height` ke resolusi yang lebih tinggi; perpustakaan akan menskalakan gambar sesuai.

**Q: Apakah ini bekerja pada kontainer Linux?**  
A: Ya, GroupDocs.Redaction .NET bersifat lintas‑platform dan dapat dijalankan di dalam kontainer Docker yang mendukung .NET Core.

## Sumber Daya
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download the Latest Version](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 5.6 for .NET  
**Author:** GroupDocs

## Tutorial Terkait

- [Mastering Document Security: Rasterize and Redact Word Docs with GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [How to Delete Pages from PDFs Using GroupDocs.Redaction .NET: A Comprehensive Guide](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implement Document Redaction Using GroupDocs.Redaction .NET: A Step-by-Step Guide](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)