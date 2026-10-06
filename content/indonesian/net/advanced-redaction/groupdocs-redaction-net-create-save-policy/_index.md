---
date: '2026-10-06'
description: Pelajari cara menghapus data sensitif dengan GroupDocs.Redaction .NET.
  Panduan langkah demi langkah ini menunjukkan cara membuat, menerapkan, dan menyimpan
  kebijakan redaksi sebagai XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Pelajari cara menghapus data sensitif dengan GroupDocs.Redaction .NET.
  Panduan langkah demi langkah ini menunjukkan cara membuat, menerapkan, dan menyimpan
  kebijakan redaksi sebagai XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Cara menghapus data sensitif menggunakan GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Cara menghapus data sensitif menggunakan GroupDocs.Redaction .NET
type: docs
url: /id/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Cara menyensor data sensitif menggunakan GroupDocs.Redaction .NET

Melindungi informasi rahasia dalam kontrak, laporan keuangan, atau catatan pasien adalah persyaratan yang tidak dapat dinegosiasikan bagi aplikasi modern. Dalam panduan ini Anda akan belajar **cara menyensor data sensitif** dengan GroupDocs.Redaction untuk .NET, mulai dari menginstal SDK hingga mendefinisikan kebijakan XML yang dapat digunakan kembali dan dapat diterapkan pada jenis dokumen apa pun.

## Jawaban Cepat
- **Apa arti “create redaction policy”?** Ini adalah proses mendefinisikan aturan (teks, regex, gambar, dll.) yang memberi tahu GroupDocs.Redaction cara menyembunyikan atau mengganti konten rahasia.  
- **Perpustakaan mana yang saya butuhkan?** GroupDocs.Redaction untuk .NET, tersedia melalui NuGet.  
- **Apakah saya memerlukan lisensi?** Trial gratis dapat digunakan untuk pengembangan; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menggunakan kembali kebijakan tersebut?** Ya—setelah disimpan sebagai XML Anda dapat memuatnya nanti dan menerapkannya pada dokumen apa pun.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu kebijakan penyensoran?

Kebijakan penyensoran adalah kumpulan aturan yang menentukan *apa* yang harus dihapus atau diganti dan *bagaimana* penggantiannya terlihat. Dengan membuat kebijakan sekali, Anda dapat menerapkan standar keamanan yang konsisten pada setiap dokumen yang diproses oleh aplikasi Anda.

## Bagaimana kebijakan penyensoran bekerja?

Muat dokumen dengan mesin `Redactor`, lampirkan satu atau lebih aturan penyensoran, lalu panggil `Apply`. Mesin akan memindai dokumen, menutupi konten yang cocok, dan secara opsional menghasilkan file baru. Set aturan yang sama dapat diekspor ke XML, memungkinkan Anda menggunakan kembali kebijakan tanpa harus mengkompilasi ulang kode.

## Mengapa menggunakan GroupDocs.Redaction untuk membuat kebijakan penyensoran?

GroupDocs.Redaction menyediakan rangkaian fitur lengkap yang menyederhanakan pembuatan, pengelolaan, dan eksekusi kebijakan penyensoran, memastikan perlindungan data yang konsisten di berbagai jenis dokumen sekaligus memberikan kinerja tinggi dan integrasi mudah ke dalam aplikasi .NET yang ada untuk tim dan organisasi.

- **Dukungan format luas** – SDK menangani 30+ tipe file, termasuk PDF, DOCX, XLSX, PPTX, dan format gambar, serta dapat memproses file hingga 2 GB tanpa memuat seluruh file ke memori.  
- **Presisi programatik** – definisikan frasa tepat, ekspresi reguler, atau logika khusus untuk menargetkan hanya data yang perlu disembunyikan.  
- **Kebijakan XML yang dapat digunakan kembali** – ekspor aturan Anda sekali dan bagikan ke tim, layanan, atau mikro‑layanan.  
- **Mesin yang dioptimalkan untuk kinerja** – perpustakaan memproses dokumen ratusan halaman dalam kurang dari satu detik pada perangkat keras server tipikal, menjadikannya cocok untuk pipeline dengan throughput tinggi.

## Prasyarat
- Perpustakaan GroupDocs.Redaction yang kompatibel dengan runtime .NET Anda.  
- Visual Studio, VS Code, atau IDE apa pun yang mendukung C#.  
- Pemahaman dasar tentang C# dan struktur proyek .NET.

## Menyiapkan GroupDocs.Redaction untuk .NET

Pertama, tambahkan perpustakaan ke proyek Anda.

**Menggunakan .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Menggunakan Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

Atau cari “GroupDocs.Redaction” di UI NuGet Package Manager dan instal dari sana.

### Akuisisi Lisensi
- Mulailah dengan **trial gratis** untuk menjelajahi fitur.  
- Minta **lisensi sementara** untuk pengujian lanjutan, kemudian beli lisensi penuh untuk penggunaan produksi.

### Inisialisasi Dasar
Tambahkan namespace ke file sumber Anda:

```csharp
using GroupDocs.Redaction;
```  

Kelas `Redactor` adalah mesin inti yang memuat dokumen dan menerapkan aturan penyensoran.  
Kelas `Redactor` adalah mesin inti GroupDocs.Redaction yang memuat dokumen dan menerapkan aturan penyensoran.

## Cara membuat kebijakan penyensoran langkah demi langkah

Berikut adalah panduan lengkap yang menunjukkan cara membangun kebijakan penyensoran secara programatik, mengonfigurasi aturannya, menerapkannya pada dokumen, dan akhirnya menyimpan kebijakan tersebut sebagai file XML untuk penggunaan kembali di masa mendatang, memastikan penyensoran yang konsisten di berbagai proyek dan jenis dokumen.

### Langkah 1: siapkan direktori dokumen Anda
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Ganti `"YOUR_DOCUMENT_DIRECTORY"` dengan folder yang berisi dokumen yang ingin Anda lindungi.*

### Langkah 2: muat dokumen
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
Objek `Redactor` membuka file dan mengelola siklus hidupnya.

### Langkah 3: definisikan penyensoran
`ExactPhraseRedaction` mendefinisikan aturan yang mengganti frasa tertentu, sementara `RegexRedaction` menggunakan ekspresi reguler untuk mencocokkan pola.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Di sini kami membuat dua aturan:
1. **ExactPhraseRedaction** – mengganti frasa yang diketahui dengan “[REDACTED]”.  
2. **RegexRedaction** – menemukan tanggal dalam format `YYYY‑MM‑DD` dan menggantinya dengan “[DATE REDACTED]”.

### Langkah 4: terapkan penyensoran
```csharp
redactor.Apply(redactions);
```  
Semua aturan yang didefinisikan dijalankan terhadap dokumen yang dibuka dalam satu kali proses.

### Langkah 5: simpan kebijakan sebagai file XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
File XML menyimpan definisi penyensoran, memungkinkan Anda menggunakan kembali kebijakan yang sama tanpa menulis ulang kode.

## Aplikasi Praktis

- **Firma hukum** dapat menyensor nomor kasus dan nama klien sebelum membagikan draf.  
- **Departemen keuangan** menyembunyikan nomor akun atau tanggal transaksi dalam laporan.  
- **Penyedia layanan kesehatan** memastikan kepatuhan HIPAA dengan menghapus pengidentifikasi pasien.

## Tips Kinerja

- Buka **satu dokumen pada satu waktu** untuk menjaga penggunaan memori tetap rendah.  
- Tulis **ekspresi reguler yang efisien**; hindari pola yang terlalu luas yang meningkatkan waktu pemrosesan.  
- Pastikan perpustakaan **terbaru** untuk mendapatkan manfaat dari peningkatan kinerja dan tipe penyensoran baru.

## Masalah Umum dan Solusinya

| Masalah | Mengapa terjadi | Cara memperbaiki |
|-------|----------------|------------|
| **IO exception saat menyiapkan direktori** | Path salah atau izin menulis tidak ada | Pastikan folder ada dan aplikasi memiliki hak baca/tulis. |
| **Regex tidak cocok dengan teks yang diharapkan** | Polanya terlalu ketat atau karakter escape hilang | Uji regex dengan tester online; sesuaikan kuantifier atau escape karakter khusus. |
| **File kebijakan tidak dibuat** | `SavePolicy` dipanggil sebelum menerapkan penyensoran atau dengan path yang tidak valid | Pastikan direktori output dapat ditulis dan panggil `SavePolicy` setelah `Apply`. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya memuat kebijakan XML yang ada alih-alih membuatnya secara programatik?**  
A: Ya—gunakan `redactor.LoadPolicy("policy.xml")` untuk mengimpor kebijakan yang sebelumnya disimpan.

**Q: Apakah GroupDocs.Redaction mendukung PDF yang dilindungi kata sandi?**  
A: Tentu saja. Berikan kata sandi ke konstruktor `Redactor`: `new Redactor(sourceFile, "password")`.

**Q: Apakah memungkinkan untuk menyensor gambar atau metadata?**  
A: SDK menyediakan kelas `ImageRedaction` dan `MetadataRedaction` untuk skenario tersebut.

**Q: Bagaimana cara menangani dokumen besar (ratusan MB)?**  
A: Proses dokumen tersebut dalam potongan atau gunakan API streaming untuk mengurangi jejak memori; mesin dapat menangani file hingga 2 GB tanpa memuat seluruh file ke RAM.

**Q: Model lisensi apa yang diperlukan untuk penggunaan komersial?**  
A: Lisensi berbayar diperlukan untuk penerapan produksi; lisensi trial cukup untuk pengembangan dan pengujian.

## Kesimpulan

Anda sekarang memiliki **kebijakan penyensoran** yang lengkap dan dapat digunakan kembali yang dapat Anda terapkan pada dokumen apa pun dengan GroupDocs.Redaction untuk .NET. Dengan mengekspor kebijakan ke XML, Anda menyederhanakan pembaruan di masa mendatang dan memastikan perlindungan data yang konsisten di seluruh organisasi Anda.

### Langkah Selanjutnya
- Bereksperimen dengan tipe penyensoran tambahan seperti `ImageRedaction` atau `MetadataRedaction`.  
- Integrasikan logika pemuatan kebijakan ke dalam alur kerja manajemen dokumen Anda untuk penyensoran otomatis.  
- Jelajahi referensi API **GroupDocs.Redaction** untuk penyesuaian lanjutan.

---

**Terakhir Diperbarui:** 2026-10-06  
**Diuji Dengan:** GroupDocs.Redaction 5.8 untuk .NET  
**Penulis:** GroupDocs  

**Sumber Daya**  
- [Dokumentasi](https://docs.groupdocs.com/redaction/net/)  
- [Referensi API](https://reference.groupdocs.com/redaction/net)  
- [Unduhan](https://releases.groupdocs.com/redaction/net/)  
- [Forum Dukungan Gratis](https://forum.groupdocs.com/c/redaction/33)  
- [Aplikasi Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Tutorial Terkait

- [Menyensor Data Sensitif dengan GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implementasi Penyensoran Dokumen Menggunakan GroupDocs.Redaction .NET&#58; Panduan Langkah‑per‑Langkah](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Cara Menyensor Dokumen dengan GroupDocs.Redaction .NET – Panduan Lengkap](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)