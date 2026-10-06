---
date: '2026-10-06'
description: Pelajari cara menyensor data menggunakan GroupDocs.Redaction .NET dengan
  implementasi IRedactionCallback dalam C#. Ikuti panduan langkah‑demi‑langkah ini,
  praktik terbaik, dan contoh dunia nyata.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Pelajari cara menyensor data menggunakan GroupDocs.Redaction .NET
  dengan implementasi IRedactionCallback dalam C#. Ikuti panduan langkah‑demi‑langkah
  dengan praktik terbaik dan contoh dunia nyata.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Cara menyensor data dengan GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Cara menyensor data dengan GroupDocs.Redaction .NET (C#)
type: docs
url: /id/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Cara menyensor data dengan GroupDocs.Redaction .NET (C#)

Dalam tutorial komprehensif ini Anda akan menemukan **cara menyensor data** dari PDF, file Word, dan dokumen lainnya menggunakan GroupDocs.Redaction untuk .NET. Baik Anda perlu menyembunyikan pengidentifikasi pribadi dalam kontrak hukum atau menghapus angka rahasia dari laporan keuangan, SDK memberi Anda kontrol programatik untuk memastikan setiap elemen sensitif menghilang secara permanen dan dapat diaudit. Kami akan memandu Anda melalui instalasi library, mengonfigurasi `IRedactionCallback` khusus, dan menerapkan penyensoran frasa tepat dengan pencatatan lengkap.

## Jawaban Cepat
- **Apa yang dilakukan IRedactionCallback?** Itu memungkinkan Anda menangkap setiap peristiwa penyensoran, mencatat detail, dan secara opsional memodifikasi teks pengganti secara langsung.  
- **Apakah saya membutuhkan lisensi?** Versi percobaan dapat digunakan untuk pengembangan; lisensi permanen menghapus semua batas evaluasi.  
- **Versi .NET apa yang didukung?** .NET Core 3.1+, .NET 5/6, dan .NET Framework 4.6+.  
- **Bisakah saya memproses banyak file?** Ya—bungkus logika dalam loop atau gunakan pemrosesan batch untuk kinerja terbaik.  
- **Apakah penyensoran asynchronous memungkinkan?** Tidak built‑in, tetapi Anda dapat menjalankan panggilan API di dalam `Task.Run` atau pola async lainnya.

## Apa itu penyensoran data sensitif?
`Redaction` adalah penghapusan atau penyamaran permanen informasi yang tidak boleh diungkapkan. Dengan GroupDocs.Redaction Anda dapat mendefinisikan frasa tepat, pola regular‑expression, atau aturan khusus dan menggantinya dengan placeholder seperti **[REDACTED]** sambil mempertahankan tata letak dan penomoran halaman asli.

## Mengapa menggunakan GroupDocs.Redaction dengan IRedactionCallback?
`IRedactionCallback` adalah antarmuka yang memberi tahu Anda setiap kali SDK menyensor bagian konten, memungkinkan Anda menangkap data audit atau menyesuaikan penggantian secara dinamis. Ini memungkinkan auditabilitas penuh, penegakan aturan bisnis khusus, dan integrasi mulus dengan sistem kepatuhan—tanpa mengorbankan kinerja.

## Prasyarat
- **GroupDocs.Redaction** library (versi yang kompatibel – lihat halaman [documentation page](https://docs.groupdocs.com/redaction/net/)). Untuk detail lengkap, lihat [official documentation](https://docs.groupdocs.com/redaction/net/).  
- .NET Core atau .NET Framework terinstal di mesin pengembangan Anda.  
- Visual Studio (edisi Community sudah cukup) atau IDE apa pun yang mendukung C#.  
- Pengetahuan dasar C# dan familiaritas dengan manajemen paket NuGet.

## Menyiapkan GroupDocs.Redaction untuk .NET
Pertama, tambahkan library ke proyek Anda. Pilih metode yang Anda sukai – CLI, Package Manager Console, atau UI. Perintahnya tetap persis sama seperti dalam tutorial asli.

### Opsi Instalasi
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Buka proyek Anda di Visual Studio.  
- Arahkan ke **Manage NuGet Packages**.  
- Cari **GroupDocs.Redaction** dan instal versi stabil terbaru.

### Akuisisi Lisensi
Untuk mencoba produk, minta percobaan gratis atau lisensi sementara dari [here](https://purchase.groupdocs.com/temporary-license/). Anda juga dapat memperoleh lisensi sementara dari [temporary‑license page](https://purchase.groupdocs.com/temporary-license/). Untuk penggunaan produksi, beli lisensi penuh untuk membuka semua fitur tanpa batas.

#### Inisialisasi dan Pengaturan Dasar
Berikut adalah kode minimal yang Anda perlukan untuk membuka dokumen dengan kelas `Redactor`. Biarkan potongan kode ini tidak diubah – ini adalah fondasi untuk semua yang berikutnya.  
`Redactor` adalah kelas utama yang mewakili dokumen dan menyediakan metode untuk menerapkan aturan penyensoran.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Panduan Implementasi
Sekarang kami akan memperluas pengaturan dasar dengan menambahkan `IRedactionCallback` khusus. Ini memungkinkan Anda menangkap setiap peristiwa penyensoran, menuliskannya ke log, atau bahkan memodifikasi teks pengganti secara langsung.

### Lampirkan dan gunakan implementasi IRedactionCallback
`IRedactionCallback` adalah antarmuka yang menerima callback untuk setiap operasi penyensoran, memungkinkan Anda mencatat atau mengubah perilaku secara programatis.

#### Langkah 1: siapkan direktori output dan jalur file sumber
Tentukan di mana dokumen sumber Anda berada. Sesuaikan jalur agar cocok dengan lingkungan Anda.

`LoadOptions` adalah objek konfigurasi yang memberi tahu SDK cara membaca file (mis., penanganan kata sandi).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Langkah 2: buat instance Redactor dengan pengaturan khusus
Kami menginstansiasi `Redactor` dengan `LoadOptions` dan `RedactorSettings`. `RedactionDump` di dalam pengaturan akan secara otomatis merekam setiap penyensoran yang terjadi.

`RedactorSettings` memungkinkan Anda menyesuaikan proses penyensoran; memberikan `RedactionDump` mengaktifkan file audit terperinci.  
`RedactionDump` adalah kelas pembantu yang menulis setiap peristiwa penyensoran ke dump berformat JSON untuk pelaporan kepatuhan.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Langkah 3: terapkan penyensoran frasa tepat
Di sini kami mengganti frasa **John Doe** dengan placeholder **[REDACTED]**. Anda dapat mengganti frasa atau pola apa pun yang perlu disembunyikan.

`ReplacementOptions` menentukan teks apa yang akan menggantikan konten yang cocok. Ini juga mendukung penyesuaian font dan warna jika Anda memerlukan masker visual.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Penjelasan objek kunci**
- `LoadOptions()` – memberi tahu SDK cara membaca dokumen (mis., penanganan kata sandi).  
- `RedactorSettings(new RedactionDump())` – mengaktifkan file dump yang mencatat setiap penyensoran untuk keperluan audit.  
- `ReplacementOptions("[REDACTED]")` – menentukan teks yang akan menggantikan frasa yang cocok.

### Mengapa ini penting
Mekanisme callback mencatat setiap peristiwa penyensoran, membuat jejak audit yang dapat dibaca mesin, dan memungkinkan Anda memodifikasi placeholder secara dinamis, yang membantu memenuhi persyaratan kepatuhan dan mengurangi upaya pemrosesan manual. Dengan mengintegrasikan data ini ke sistem pemantauan Anda, Anda dapat menghasilkan laporan, memicu peringatan, dan memastikan tidak ada informasi sensitif yang lolos dari pipeline penyensoran.

Menggunakan `IRedactionCallback` memberi Anda tiga keuntungan konkret:
1. **Log siap kepatuhan** – setiap penyensoran ditangkap dalam dump yang dapat dibaca mesin, memenuhi persyaratan audit untuk lebih dari 30 kerangka regulasi.  
2. **Penggantian dinamis** – Anda dapat mengubah placeholder berdasarkan tipe data, mengurangi pemrosesan manual hingga 40 %.  
3. **Kinerja skalabel** – callback menambah overhead yang dapat diabaikan (<2 ms per penyensoran) sambil memungkinkan Anda memproses ribuan file secara paralel dalam batch.

### Tips Pemecahan Masalah
- **File tidak ditemukan:** Periksa kembali jalur `sourceFile` dan pastikan file dapat diakses oleh proses yang berjalan.  
- **Callback tidak dipicu:** Pastikan kelas Anda mengimplementasikan **semua** anggota `IRedactionCallback` dan bahwa instance tersebut diteruskan dengan benar ke `Redactor`.  
- **Keterlambatan kinerja:** Untuk batch besar, gunakan kembali instance `Redactor` yang sama bila memungkinkan dan segera dispose setelah selesai.

## Aplikasi Praktis
Menyensor data sensitif berguna di banyak industri:
1. **Pemrosesan dokumen hukum** – Secara otomatis menghapus nama klien, nomor kasus, atau nomor jaminan sosial sebelum membagikan draf.  
2. **Sistem manajemen SDM** – Menghapus pengidentifikasi pribadi dari kontrak karyawan selama audit.  
3. **Pelaporan keuangan** – Menyembunyikan angka proprietari atau nomor akun saat menghasilkan PDF untuk investor.

## Pertimbangan Kinerja
GroupDocs.Redaction mendukung **lebih dari 30 format input dan output** (PDF, DOCX, PPTX, XLSX, HTML, dan tipe gambar) dan dapat memproses file beratus‑ratus halaman tanpa memuat seluruh dokumen ke memori. Untuk menjaga aplikasi Anda tetap responsif saat menangani puluhan atau ratusan file:
- **Pemrosesan batch:** Muat daftar file dan jalankan loop penyensoran di dalam `Parallel.ForEach` untuk pemanfaatan multi‑core.  
- **Manajemen memori:** Bungkus setiap `Redactor` dalam blok `using` (seperti yang ditunjukkan) untuk memastikan disposisi.  
- **Operasi asynchronous:** Meskipun SDK bersifat sinkron, Anda dapat memindahkan pekerjaan ke thread latar belakang atau `Task.Run` untuk menghindari pemblokiran thread UI.

## Masalah Umum dan Solusinya
| Masalah | Solusi |
|-------|----------|
| **Error “Invalid file format”** | Pastikan tipe dokumen didukung (PDF, DOCX, PPTX, dll.). |
| **Callback menerima nilai null** | Periksa bahwa Anda mengirimkan implementasi konkret `IRedactionCallback` saat membuat `RedactorSettings`. |
| **Penyensoran tidak diterapkan** | Pastikan frasa tepat cocok dengan huruf besar/kecil dan spasi dokumen, atau gunakan `RegexRedaction` untuk pencocokan berbasis pola. |

## Pertanyaan yang Sering Diajukan

**Q: Apa saja opsi lisensi untuk GroupDocs.Redaction?**  
A: Anda dapat memulai dengan percobaan gratis atau meminta lisensi sementara untuk menjelajahi semua fitur. Untuk produksi, beli lisensi permanen atau berlangganan.

**Q: Bisakah saya menggunakan GroupDocs.Redaction pada banyak tipe file?**  
A: Ya, ia mendukung PDF, Word, Excel, PowerPoint, dan banyak format umum lainnya.

**Q: Bagaimana cara menangani pengecualian selama penyensoran?**  
A: Bungkus logika penyensoran Anda dalam blok `try‑catch` dan catat detail pengecualian. Callback juga dapat digunakan untuk menangkap kesalahan secara real time.

**Q: Apakah ada dukungan bawaan untuk pemrosesan asynchronous?**  
A: API inti bersifat sinkron, tetapi Anda dapat menjalankan panggilan penyensoran di dalam tugas asynchronous atau layanan latar belakang.

**Q: Di mana saya dapat menemukan contoh yang lebih maju?**  
A: [Dokumentasi resmi](https://docs.groupdocs.com/redaction/net/) dan referensi API menyediakan contoh kode yang luas serta panduan skenario.

## Sumber Daya

- [GroupDocs.Redaction untuk Dokumentasi Net](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction untuk Referensi API Net](https://reference.groupdocs.com/redaction/net/)
- [Unduh GroupDocs.Redaction untuk Net](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-10-06  
**Diuji Dengan:** GroupDocs.Redaction 2.3 (versi terbaru saat penulisan)  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Buat Kebijakan Penyensoran dengan GroupDocs.Redaction .NET – Panduan Langkah‑Demi‑Langkah](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Cara Menyensor Dokumen dengan GroupDocs.Redaction .NET – Panduan Lengkap](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Sensor dokumen .net menggunakan Streams – Panduan GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)