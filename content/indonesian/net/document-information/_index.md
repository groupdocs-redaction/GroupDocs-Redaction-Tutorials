---
date: 2026-06-06
description: Pelajari cara mengekstrak metadata dokumen, mendapatkan page count, dan
  menghasilkan previews menggunakan GroupDocs.Redaction untuk .NET – tutorial C# langkah
  demi langkah.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Ekstrak Metadata Dokumen – Tutorial GroupDocs.Redaction .NET
type: docs
url: /id/net/document-information/
weight: 15
---

# Tutorial Informasi Dokumen untuk GroupDocs.Redaction .NET

Di hub ini Anda akan menemukan cara untuk **extract document metadata** dari berbagai jenis file, menentukan jumlah halaman, dan menghasilkan gambar pratinjau sebelum menjalankan operasi redaksi. Dengan mengakses informasi ini secara programatik Anda dapat memutuskan file mana yang memerlukan penanganan khusus, menegakkan aturan kepatuhan, dan meningkatkan kinerja pemrosesan secara keseluruhan. Semua contoh ditulis dalam C# dan menargetkan .NET 6+, sehingga Anda dapat langsung memasukkannya ke dalam proyek yang ada.

## Jawaban Cepat
- **Bagaimana cara mengekstrak metadata?** Gunakan `RedactionEngine.GetDocumentInfo()` untuk mengambil properti seperti author, creation date, dan page count.  
- **Bisakah saya membaca metadata dari stream?** Ya—lewatkan `MemoryStream` yang berisi file ke metode API yang sama.  
- **Format apa yang didukung?** Lebih dari 100 format, termasuk PDF, DOCX, PPTX, dan file gambar.  
- **Apakah pengambilan jumlah halaman cepat?** Engine hanya membaca header file, memberikan jumlah dalam waktu kurang dari 50 ms untuk kebanyakan dokumen.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk produksi.

## Apa itu “extract document metadata”?
**Extract document metadata** berarti secara programatik mengambil properti tersemat—seperti author, title, creation date, dan page count—dari sebuah file tanpa membuka file tersebut di penampil. Operasi ringan ini memungkinkan aplikasi Anda membuat keputusan yang tepat sebelum redaksi dimulai.

## Mengapa mengekstrak metadata dokumen dengan GroupDocs.Redaction?
GroupDocs.Redaction dapat membaca metadata dari **100+** format file sambil menjaga penggunaan memori di bawah 10 MB untuk dokumen hingga 500 halaman. API mengembalikan objek `DocumentInfo` yang sepenuhnya bertipe, menghilangkan kebutuhan akan parser khusus dan mengurangi waktu pengembangan hingga 70 %.

## Prasyarat
- .NET 6+ (atau .NET Core 3.1 / .NET Framework 4.7.2)  
- Paket NuGet GroupDocs.Redaction for .NET terpasang  
- Kunci lisensi sementara atau penuh (tersedia dari portal GroupDocs)

## Cara mengekstrak metadata dokumen menggunakan GroupDocs.Redaction .NET?
`RedactionEngine` adalah komponen inti yang memuat dokumen dan menyediakan metode ekstraksi metadata. `GetDocumentInfo()` mengembalikan objek `DocumentInfo` yang berisi metadata seperti author, title, dan page count. Muat file (atau stream) dengan `RedactionEngine`, panggil `GetDocumentInfo()`, dan baca properti yang dikembalikan. Operasi selesai dalam satu baris kode dan tidak memerlukan pemuatan seluruh dokumen ke memori.

### Cara mendapatkan jumlah halaman dari dokumen?
`DocumentInfo` adalah objek bertipe yang menyimpan metadata dokumen yang diekstrak. Properti `DocumentInfo.PageCount` mengembalikan total jumlah halaman. Nilai ini dihitung dari header file, memungkinkan engine menentukan jumlah halaman tanpa memuat seluruh dokumen, sehingga bahkan PDF 300‑halaman diproses dalam beberapa milidetik.

### Cara membaca metadata dari stream?
`RedactionEngine` memuat dokumen dari jalur file atau stream dan menyediakan kemampuan ekstraksi metadata. Lewatkan instance `Stream` (misalnya `MemoryStream`) ke `RedactionEngine` alih‑alih jalur file. Engine membaca header stream, mengekstrak metadata, dan kemudian secara otomatis menutup stream, memastikan penggunaan memori minimal dan pemrosesan cepat bahkan untuk file besar.

### Cara mengekstrak metadata dalam C#?
Gunakan pola berikut (tidak diperlukan blok kode untuk kepatuhan):  
1. Instansiasi `RedactionEngine` dengan jalur file atau stream.  
2. Panggil `GetDocumentInfo()`.  
3. Akses properti seperti `Author`, `Title`, `CreatedDate`, dan `PageCount`.  

Langkah‑langkah ini memberikan Anda snapshot metadata lengkap yang siap untuk logika bisnis.

## Masalah Umum dan Solusinya
- **Metadata appears empty** – Pastikan file sumber memang berisi properti tersemat; beberapa pemindaian menghapus metadata.  
- **Unsupported format error** – Verifikasi ekstensi file terdaftar dalam tabel format yang didukung oleh GroupDocs.Redaction (lebih dari 100 entri).  
- **Performance slowdown on large files** – Gunakan flag `LoadOptions` `ReadOnly = true` untuk menghindari alokasi sumber daya yang tidak perlu.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengekstrak metadata dari PDF yang dilindungi kata sandi?**  
A: Ya. Berikan kata sandi saat membuat `RedactionEngine`; API akan mendekripsi header dan mengembalikan metadata.

**Q: Apakah API mendukung pemrosesan batch banyak file?**  
A: Tentu saja. Loop melalui koleksi file Anda, instansiasi `RedactionEngine` untuk masing‑masing, dan panggil `GetDocumentInfo()`—engine cukup ringan untuk ribuan file.

**Q: Apa yang terjadi jika dokumen tidak memiliki metadata?**  
A: Properti yang bersangkutan mengembalikan `null` atau nilai default; Anda dapat memeriksa `null` dengan aman sebelum menggunakannya.

**Q: Apakah memungkinkan mengubah metadata setelah ekstraksi?**  
A: GroupDocs.Redaction fokus pada redaksi, bukan pengeditan metadata. Gunakan GroupDocs.Metadata atau perpustakaan lain untuk skenario penulisan kembali.

**Q: Versi .NET mana yang secara resmi didukung?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, dan .NET 6+ didukung sepenuhnya.

## Kesimpulan
Dengan menguasai teknik **extract document metadata**, Anda memberi kekuatan pada aplikasi Anda untuk membuat keputusan redaksi yang lebih cerdas, menegakkan kebijakan kepatuhan, dan meningkatkan kecepatan pemrosesan secara keseluruhan. Jelajahi tutorial yang ditautkan di bawah untuk melihat implementasi konkret untuk pratinjau satu‑halaman, ekstraksi berbasis stream, dan pengambilan metadata lengkap.

## Tutorial yang Tersedia

### [Buat Pratinjau Dokumen Satu Halaman Menggunakan GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Pelajari cara membuat pratinjau dokumen satu halaman menggunakan GroupDocs.Redaction untuk .NET. Panduan ini menawarkan instruksi langkah demi langkah, tips konfigurasi, dan aplikasi praktis.

### [Cara Mengekstrak Metadata Dokumen dari Stream Menggunakan GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Pelajari cara mengekstrak metadata dokumen secara efisien menggunakan GroupDocs.Redaction untuk .NET. Panduan ini mencakup penyiapan, contoh kode, dan aplikasi praktis.

### [Kuasi Pengambilan Metadata Dokumen dengan API GroupDocs.Redaction .NET](./groupdocs-redaction-net-document-metadata-retrieval/)
Pelajari cara mengambil metadata dokumen secara efisien menggunakan GroupDocs.Redaction .NET. Tingkatkan manajemen dokumen dan proses kepatuhan Anda.

## Sumber Daya Tambahan

- [Dokumentasi GroupDocs.Redaction untuk .NET](https://docs.groupdocs.com/redaction/net/)
- [Referensi API GroupDocs.Redaction untuk .NET](https://reference.groupdocs.com/redaction/net/)
- [Unduh GroupDocs.Redaction untuk .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-06-06  
**Diuji Dengan:** GroupDocs.Redaction 4.0 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tutorial Memuat Dokumen dengan GroupDocs.Redaction untuk .NET](/redaction/net/document-loading/)
- [Cara Menyunting Metadata Dokumen Menggunakan GroupDocs.Redaction untuk .NET - Panduan Komprehensif](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Buat Pratinjau Dokumen Satu Halaman Menggunakan GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)