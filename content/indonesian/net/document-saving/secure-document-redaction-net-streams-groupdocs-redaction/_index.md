---
date: '2026-07-06'
description: Pelajari cara meredaksi dokumen .net menggunakan streams dengan GroupDocs.Redaction.
  Tutorial ini mencakup setup, load document from stream, applying redactions, dan
  saving securely.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: Redaksi dokumen .net menggunakan Streams – Panduan GroupDocs.Redaction
type: docs
url: /id/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Menyunting dokumen .net menggunakan Streams – Panduan Komprehensif

Selamat datang! Dalam tutorial ini Anda akan menemukan cara **redact documents .net** secara aman dengan memanfaatkan streams menggunakan GroupDocs.Redaction. Kami akan membahas semua yang Anda perlukan—mulai dari menginstal pustaka, memuat dokumen dari stream, menerapkan redaksi yang tepat, hingga menyimpan hasil tanpa meninggalkan file sementara di disk.

## Jawaban Cepat
- **Perpustakaan apa yang menangani redaksi di .NET?** GroupDocs.Redaction for .NET.  
- **Bisakah saya memuat file langsung dari stream?** Ya—gunakan `FileStream` dengan konstruktor Redactor.  
- **Format apa yang didukung?** Lebih dari 70 format input dan output, termasuk PDF, DOCX, XLSX, PPTX.  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk penggunaan non‑trial.  
- **Apakah aman untuk file besar?** Pemrosesan berbasis stream menghindari memuat seluruh file ke memori, memungkinkan penanganan dokumen multi‑gigabyte.

## Apa itu “redact documents .net”?
**“Redact documents .net”** mengacu pada proses menghapus atau menyamarkan secara permanen konten sensitif dari file menggunakan pustaka .NET seperti GroupDocs.Redaction. Ini memastikan data rahasia tidak pernah keluar dari sistem Anda dalam teks jelas. Hal ini biasanya digunakan di sektor hukum, keuangan, dan perawatan kesehatan untuk mematuhi regulasi privasi seperti GDPR dan HIPAA, memastikan data sensitif tidak dapat dipulihkan setelah diproses.

## Mengapa menggunakan streams untuk redaksi?
GroupDocs.Redaction mendukung **lebih dari 70 format file** dan dapat memproses file hingga **2 GB** tanpa memuatnya sepenuhnya ke memori. Streaming mengurangi beban I/O, meningkatkan kinerja, dan selaras dengan praktik keamanan terbaik dengan menyimpan data di memori hanya untuk waktu singkat yang diperlukan untuk transformasi.

## Prasyarat
- **GroupDocs.Redaction for .NET** – instal melalui NuGet (lihat di bawah).  
- **.NET 6+** (atau .NET Framework 4.6.1+).  
- Visual Studio 2022 atau IDE kompatibel apa pun.  
- Pengetahuan dasar C# dan familiaritas dengan .NET streams.

## Menginstal GroupDocs.Redaction
Anda dapat menambahkan paket dengan salah satu perintah berikut:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Atau temukan “GroupDocs.Redaction” di UI NuGet Package Manager dan klik **Install**.

### Langkah-langkah Akuisisi Lisensi
1. **Free Trial** – unduh percobaan dari [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – minta kunci jangka pendek untuk evaluasi.  
3. **Full Purchase** – dapatkan lisensi permanen untuk beban kerja produksi.

Setelah diinstal, inisialisasi pustaka dalam kode Anda:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Cara memuat dokumen dari stream?
Sebuah `FileStream` menyediakan stream untuk membaca dan menulis file di disk. Kelas `Redactor` memproses dokumen dan menerapkan aturan redaksi. Muat file sumber Anda ke dalam `FileStream`, lalu berikan stream tersebut ke konstruktor `Redactor`. Pendekatan ini menghindari penulisan file asli ke lokasi sementara dan menyimpan data di memori hanya selama proses berlangsung. Metode ini bekerja untuk semua format yang didukung, termasuk PDF dan dokumen Office.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Cara menginisialisasi Redactor dengan stream?
Kelas `Redactor` adalah mesin inti yang memanipulasi konten dokumen. Dengan menyediakan stream input, Anda memungkinkan redaksi dalam memori tanpa file perantara. Setelah membuat instance, Anda dapat menambahkan aturan redaksi secara berurutan, meninjau perubahan, dan mengonfigurasi opsi seperti rasterisasi atau enkripsi sebelum menyimpan dokumen akhir.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` adalah kelas utama yang menyediakan metode untuk menerapkan, meninjau, dan menyimpan operasi redaksi pada dokumen yang dimuat dari stream.

## Cara menerapkan redaksi?
Anda dapat menambahkan beberapa aksi redaksi; contoh di bawah menghapus semua anotasi, yang merupakan kebutuhan umum untuk menghapus komentar tersembunyi atau catatan peninjau. Tipe redaksi tambahan seperti `DeleteTextRedaction` atau `ReplaceTextRedaction` dapat digabungkan untuk menghapus atau menyamarkan string, tanggal, atau pola tertentu di seluruh dokumen.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` adalah aturan redaksi bawaan yang secara permanen menghapus objek anotasi seperti komentar, penyorotan, dan stempel dari dokumen.

## Cara menyimpan dokumen yang telah diredaksi?
Menyimpan langsung ke `FileStream` memastikan output ditulis dalam satu kali proses, menghilangkan file sementara yang tidak diperlukan. Anda juga dapat menentukan format output, tingkat kompresi, dan perlindungan password opsional melalui objek `SaveOptions` untuk memenuhi persyaratan keamanan. Akhirnya, tutup stream output untuk melepaskan handle file dan memastikan file sepenuhnya ditulis ke disk.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` memungkinkan Anda mengontrol cara dokumen disimpan, termasuk rasterisasi, enkripsi, dan pemilihan format.

## Kasus Penggunaan Umum
- **Legal document handling:** Hapus anotasi rahasia sebelum membagikan draf kepada klien.  
- **GDPR compliance:** Hapus pengidentifikasi pribadi dari kontrak atau catatan karyawan.  
- **Internal audit reports:** Sembunyikan catatan peninjau sambil mempertahankan konten inti untuk distribusi.

## Tips Kinerja untuk File Besar
1. **Dispose streams promptly** – pernyataan `using` secara otomatis menutup stream, membebaskan memori.  
2. **Batch processing** – Loop melalui koleksi file dan gunakan kembali satu instance `Redactor` ketika format memungkinkan, mengurangi beban alokasi.

## Pemecahan Masalah
1. **File access denied** – Pastikan akun aplikasi memiliki izin baca/tulis pada folder target.  
2. **Redaction not applied** – Pastikan tipe redaksi yang Anda pilih kompatibel dengan format dokumen (mis., `DeleteAnnotationRedaction` berfungsi untuk PDF dan DOCX).

## Pertanyaan yang Sering Diajukan
**Q: Format file apa yang dapat diproses dengan streams?**  
A: GroupDocs.Redaction mendukung lebih dari 70 format—termasuk PDF, DOCX, XLSX, PPTX, dan HTML—ketika menggunakan API berbasis stream.

**Q: Bisakah saya meninjau redaksi sebelum menyimpan?**  
A: Ya, panggil `redactor.GetRedactedDocument()` untuk mendapatkan representasi dalam memori yang dapat Anda render atau inspeksi secara programatik.

**Q: Bagaimana pustaka menangani file yang dilindungi password?**  
A: Berikan password saat membuka stream melalui overload `Redactor` yang menerima `LoadOptions` berisi password.

**Q: Apakah ada batas ukuran dokumen?**  
A: Mesin dapat memproses file hingga 2 GB; file yang lebih besar harus dibagi atau diproses dalam potongan untuk tetap berada dalam batas memori.

**Q: Apakah saya memerlukan lisensi terpisah untuk setiap lingkungan deployment?**  
A: Satu kunci lisensi dapat digunakan di beberapa lingkungan selama penggunaan mematuhi perjanjian lisensi.

## Kesimpulan
Anda kini memiliki solusi lengkap langkah demi langkah untuk **redact documents .net** menggunakan streams dengan GroupDocs.Redaction. Dengan memuat file langsung dari streams, menerapkan redaksi yang ditargetkan, dan menyimpan tanpa artefak perantara, Anda memperoleh keamanan dan kinerja. Jelajahi tipe redaksi tambahan—seperti penggantian teks atau penghapusan metadata—untuk menyesuaikan proses dengan kebutuhan kepatuhan spesifik Anda.

---

**Terakhir Diperbarui:** 2026-07-06  
**Diuji Dengan:** GroupDocs.Redaction 5.0 for .NET  
**Penulis:** GroupDocs  

## Sumber Daya
- [Dokumentasi](https://docs.groupdocs.com/redaction/net/)
- [Referensi API](https://reference.groupdocs.com/redaction/net)
- [Unduh](https://releases.groupdocs.com/redaction/net/)
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/redaction/33)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## Tutorial Terkait

- [Cara Memuat dan Menyunting Dokumen Menggunakan GroupDocs.Redaction .NET&#58; Panduan Lengkap](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Menyunting dan Menyimpan Dokumen dengan GroupDocs.Redaction untuk .NET&#58; Panduan Lengkap](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Cara Mengekstrak Metadata Dokumen dari Streams Menggunakan GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)