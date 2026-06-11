---
date: '2026-06-11'
description: Pelajari cara mengekstrak metadata dari aliran dokumen menggunakan GroupDocs.Redaction
  untuk .NET, mencakup pengaturan, contoh kode, dan aplikasi praktis.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Cara Mengekstrak Metadata dari Aliran Dokumen Menggunakan GroupDocs.Redaction
  .NET
type: docs
url: /id/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Cara Mengekstrak Metadata dari Aliran Dokumen Menggunakan GroupDocs.Redaction .NET

Apakah Anda lelah mengekstrak informasi dokumen secara manual atau berurusan dengan file besar yang memperlambat alur kerja Anda? **Cara mengekstrak metadata** dengan cepat adalah tantangan umum, dan pustaka GroupDocs.Redaction untuk .NET menawarkan cara yang cepat dan hemat memori untuk mengambil detail dokumen langsung dari aliran. Dalam tutorial ini, Anda akan belajar cara menyiapkan pustaka, mengambil tipe file, jumlah halaman, dan ukuran dari aliran, serta menyiapkan folder output untuk pemrosesan lebih lanjut.

## Jawaban Cepat
- **Apa arti “extract metadata”?** Itu berarti membaca properti seperti tipe file, jumlah halaman, dan ukuran tanpa membuka dokumen penuh di memori.  
- **Library mana yang menangani ini?** GroupDocs.Redaction untuk .NET menyediakan API native untuk ekstraksi metadata berbasis aliran.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya memproses PDF lebih besar dari 1 GB?** Ya – aliran memungkinkan Anda menangani file hingga 2 GB tanpa memuat seluruh file.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, dan .NET 6+.

## Apa itu ekstraksi metadata dari aliran?
Ekstraksi metadata dari aliran adalah proses membaca properti dokumen secara langsung dari objek `Stream`, menghindari pemuatan penuh file dan sehingga menghemat memori serta waktu CPU. Teknik ini ideal untuk pemrosesan batch atau layanan berbasis cloud di mana sumber daya terbatas.

## Mengapa menggunakan GroupDocs.Redaction untuk ekstraksi metadata?
GroupDocs.Redaction mendukung **lebih dari 30 format file** (termasuk PDF, DOCX, XLSX, PPTX, dan tipe gambar) dan dapat memproses dokumen hingga **2 GB** sambil menjaga penggunaan memori di bawah **50 MB**. API `Redactor`‑nya menyediakan satu panggilan untuk mengambil semua informasi dokumen utama, menghilangkan kebutuhan akan banyak parser.

## Prasyarat

- **GroupDocs.Redaction untuk .NET** (versi terbaru)  
- **.NET Framework** 4.5+ **atau** **.NET Core/5+/6+**  
- Pengetahuan dasar C# dan familiaritas dengan I/O file  
- Visual Studio 2019 atau yang lebih baru

## Bagaimana cara menyiapkan GroupDocs.Redaction untuk .NET?
Untuk mulai menggunakan GroupDocs.Redaction, Anda pertama‑tama perlu menambahkan pustaka ke proyek Anda. Ini dapat dilakukan melalui .NET CLI, Package Manager Visual Studio, atau UI NuGet. Pilih pendekatan yang sesuai dengan alur kerja Anda; CLI ideal untuk build yang dapat diprogram, sementara UI menawarkan cara grafis untuk menelusuri versi dan dependensi.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Buka NuGet Package Manager di Visual Studio.  
- Cari **"GroupDocs.Redaction"** dan instal versi terbaru.

### Langkah-langkah Akuisisi Lisensi
1. **Free Trial:** Unduh lisensi percobaan untuk menjelajahi semua fitur tanpa batasan.  
2. **Temporary License:** Minta lisensi sementara dari [situs web GroupDocs](https://purchase.groupdocs.com/temporary-license/) untuk pengujian lanjutan.  
3. **Purchase:** Saat siap untuk produksi, beli lisensi komersial.  

Untuk informasi lebih lanjut, kunjungi [dokumentasi GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inisialisasi Dasar dan Pengaturan
Kelas `Redactor` adalah titik masuk untuk semua operasi, termasuk ekstraksi metadata.

`Redactor` adalah kelas inti yang mewakili sebuah instance dokumen dan menyediakan metode untuk redaksi, pengambilan informasi, dan manipulasi file. Setelah terinstal, Anda dapat membuat objek `Redactor` seperti contoh di bawah:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Sekarang pustaka siap, mari selami detail implementasinya.

## Bagaimana cara mengekstrak metadata dari aliran dokumen?
Muat dokumen sebagai **aliran baca‑saja**, inisialisasi `Redactor`, dan panggil `GetDocumentInfo()` untuk mengambil metadata dalam satu langkah. Pendekatan ini menghindari pemuatan seluruh file ke memori, yang sangat penting untuk PDF besar atau dokumen Office dengan ratusan halaman.

**Jawaban langsung:** Buka file dengan `File.OpenRead()`, berikan aliran ke `new Redactor(stream)`, lalu panggil `redactor.GetDocumentInfo()` – metode ini mengembalikan objek yang berisi tipe file, jumlah halaman, dan ukuran dalam hanya tiga baris kode.

### Langkah 1: Siapkan jalur file sumber
Pertama, pastikan file sumber ada dan folder output siap. Metode bantuan di bawah memeriksa direktori output dan membuatnya jika diperlukan.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Mengapa?* Ini menjamin jalur yang valid untuk operasi file selanjutnya dan mencegah `DirectoryNotFoundException`.

### Langkah 2: Buka aliran dokumen
Menggunakan `File.OpenRead()` membuka file sebagai **aliran baca‑saja**, yang menjaga penggunaan memori tetap rendah bahkan untuk file berukuran gigabyte.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Mengapa?* Aliran memungkinkan pemrosesan secara langsung, memungkinkan Anda bekerja dengan bagian file alih‑alih seluruh dokumen.

### Langkah 3: Inisialisasi Redactor dengan aliran dokumen
`Redactor` adalah objek API utama yang memberi Anda akses ke operasi tingkat dokumen, termasuk ekstraksi metadata.

`Redactor` mewakili satu dokumen yang dimuat dari aliran dan mengekspos metode seperti `GetDocumentInfo()` untuk pengambilan properti cepat.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Mengapa?* Menginstansiasi `Redactor` dengan aliran mengikat objek ke file dasar tanpa memuatnya sepenuhnya.

### Langkah 4: Ambil metadata dokumen
Memanggil `GetDocumentInfo()` mengembalikan objek `DocumentInfo` yang berisi format file, jumlah halaman, dan ukuran file.

`GetDocumentInfo()` mengekstrak properti inti (format, jumlah halaman, ukuran) dalam satu panggilan, menghilangkan kebutuhan parser terpisah.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Mengapa?* Langkah ini mengkonsolidasikan semua metadata penting, memudahkan pencatatan, penyaringan, atau pengaturan dokumen berdasarkan karakteristiknya.

## Bagaimana cara menyiapkan direktori output untuk file yang diproses?
Sebelum menulis file yang diproses, pastikan folder tujuan ada dan dapat ditulisi. Dengan memeriksa jalur secara programatis dan membuatnya bila belum ada, Anda menghindari pengecualian runtime umum seperti `DirectoryNotFoundException` atau kesalahan izin. Langkah sederhana ini juga membuat kode Anda portabel di berbagai lingkungan, baik dijalankan secara lokal, di server, atau dalam kontainer.

**Jawaban langsung:** Gunakan `Directory.Exists()` untuk memeriksa folder dan `Directory.CreateDirectory()` untuk membuatnya jika tidak ada – pemeriksaan satu baris ini menjamin jalur yang valid sebelum operasi penulisan apa pun.

### Implementasikan metode bantuan
Metode di bawah mengenkapsulasi logika periksa‑dan‑buat, mengembalikan jalur yang telah diverifikasi untuk penggunaan selanjutnya.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Mengapa?* Memusatkan logika ini mengurangi duplikasi dan memudahkan pemeliharaan basis kode.

## Masalah Umum dan Solusi
- **Kesalahan izin:** Pastikan aplikasi dijalankan dengan akun yang memiliki akses menulis ke folder target.  
- **Jalur tidak valid:** Periksa kembali pemisah jalur (`\\` di Windows, `/` di Linux/macOS) untuk menghindari `DirectoryNotFoundException`.  
- **Penanganan file besar:** Segera dispose aliran (`using` statements) untuk membebaskan handle OS dan mencegah kebocoran.

## Aplikasi Praktis
1. **Ingest Dokumen Otomatis:** Ekstrak metadata saat unggahan, lalu simpan di basis data untuk pencarian cepat dan pelaporan kepatuhan.  
2. **Audit Hukum & Kepatuhan:** Tarik jumlah halaman dan tipe file untuk memverifikasi bahwa dokumen memenuhi standar regulasi sebelum diarsipkan.  
3. **Manajemen Konten Perusahaan:** Gunakan metadata untuk mengkategorikan file secara otomatis ke dalam folder, meningkatkan organisasi dan kecepatan pengambilan.

## Pertimbangan Kinerja
- **Manajemen Memori:** Selalu bungkus aliran dalam blok `using` agar otomatis dibuang.  
- **Pemrosesan Batch:** Proses dokumen dalam kelompok 10‑20 untuk menyeimbangkan throughput dan penggunaan memori, terutama pada server dengan sumber daya terbatas.  
- **Paralelisme:** Manfaatkan `Parallel.ForEach` untuk file independen, namun pantau CPU dan I/O agar tidak terjadi kontensi.

## Kesimpulan
Anda kini memiliki panduan lengkap yang siap produksi tentang **cara mengekstrak metadata** dari aliran dokumen menggunakan GroupDocs.Redaction untuk .NET. Dengan mengikuti langkah‑langkah di atas, Anda dapat secara efisien mengambil tipe file, jumlah halaman, dan ukuran sambil menjaga penggunaan memori rendah dan menangani file besar dengan elegan.

**Langkah Selanjutnya**
- Tinjau referensi API lengkap di [dokumentasi](https://docs.groupdocs.com/redaction/net/).  
- Selami lebih dalam [dokumentasi GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) untuk mengeksplorasi fitur redaksi, watermark, dan OCR.  
- Bereksperimen dengan format file berbeda (PDF, DOCX, XLSX) untuk melihat bagaimana metadata bervariasi antar tipe.  
- Integrasikan metadata yang diekstrak ke dalam solusi manajemen dokumen atau pencarian yang sudah ada.

## Pertanyaan yang Sering Diajukan

**T: Apa kasus penggunaan utama untuk ekstraksi metadata GroupDocs.Redaction?**  
J: Memungkinkan pengambilan properti dokumen yang cepat dan hemat memori untuk pengindeksan, pemeriksaan kepatuhan, dan routing otomatis tanpa membuka file secara penuh.

**T: Bisakah saya mengekstrak metadata dari file yang dilindungi kata sandi?**  
J: Ya, berikan kata sandi saat membangun objek `Redactor`; API akan mendekripsi aliran secara internal.

**T: Apakah pustaka ini mendukung format non‑PDF seperti DOCX atau XLSX?**  
J: Tentu – GroupDocs.Redaction menangani lebih dari 30 format, termasuk PDF, DOCX, XLSX, PPTX, dan tipe gambar umum.

**T: Seberapa besar dokumen yang dapat saya proses dengan aliran?**  
J: Aliran memungkinkan pemrosesan file hingga **2 GB** sambil menjaga konsumsi memori di bawah **50 MB**, berkat pembacaan secara langsung.

**T: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
J: Kunjungi [forum GroupDocs](https://forum.groupdocs.com/c/redaction/33) untuk dukungan komunitas, atau konsultasikan dokumentasi resmi untuk tips pemecahan masalah.

---

**Terakhir Diperbarui:** 2026-06-11  
**Diuji Dengan:** GroupDocs.Redaction 23.12 untuk .NET  
**Penulis:** GroupDocs  

**Sumber Daya**  
- **Dokumentasi:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Referensi API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Unduhan:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Tutorial Terkait

- [Menguasai Pengambilan Metadata Dokumen dengan API GroupDocs.Redaction .NET](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [Cara Menyunting Metadata Dokumen Menggunakan GroupDocs.Redaction untuk .NET – Panduan Komprehensif](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [Redaksi Dokumen Aman di .NET Menggunakan Aliran: Panduan untuk GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)