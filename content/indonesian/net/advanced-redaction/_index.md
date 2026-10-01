---
date: 2026-10-01
description: Panduan langkah demi langkah tentang cara mengaburkan file PDF, mengotomatiskan
  pengaburan dokumen, dan melakukan penghapusan metadata PDF menggunakan GroupDocs.Redaction
  untuk .NET.
keywords:
- how to redact pdf
- metadata removal pdf
- automate document redaction
lastmod: 2026-10-01
og_description: Pelajari cara mengaburkan file PDF, mengotomatiskan pengaburan dokumen,
  dan menghapus metadata PDF menggunakan GroupDocs.Redaction untuk .NET dalam beberapa
  langkah sederhana.
og_image_alt: Guide to redacting PDF documents with GroupDocs.Redaction for .NET
og_title: Cara mengaburkan PDF dengan kebijakan di GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Step-by-step guide on how to redact PDF files, automate document redaction,
    and perform metadata removal PDF using GroupDocs.Redaction for .NET.
  headline: How to redact PDF with a policy in GroupDocs.Redaction .NET
  type: TechArticle
- description: Step-by-step guide on how to redact PDF files, automate document redaction,
    and perform metadata removal PDF using GroupDocs.Redaction for .NET.
  name: How to redact PDF with a policy in GroupDocs.Redaction .NET
  steps:
  - name: '**Add the NuGet package** – Install the latest `GroupDocs.Redaction` package
      via the NuGet Package Manager or the CLI (`dotnet add package GroupDocs.Redaction`).'
    text: '**Add the NuGet package** – Install the latest `GroupDocs.Redaction` package
      via the NuGet Package Manager or the CLI (`dotnet add package GroupDocs.Redaction`).'
  - name: '**Instantiate the RedactionEngine** – `RedactionEngine` is the core class
      that loads a document and performs redaction operations.'
    text: '**Instantiate the RedactionEngine** – `RedactionEngine` is the core class
      that loads a document and performs redaction operations.'
  - name: '**Define redaction items**'
    text: '**Define redaction items**'
  - name: '**Combine items into a RedactionPolicy** – Group the redaction items into
      a `RedactionPolicy` object, which can be saved (`policy.Save("MyPolicy.xml")`)
      and later loaded for reuse.'
    text: '**Combine items into a RedactionPolicy** – Group the redaction items into
      a `RedactionPolicy` object, which can be saved (`policy.Save("MyPolicy.xml")`)
      and later loaded for reuse.'
  - name: '**Apply the policy** – Call `engine.ApplyPolicy(policy)`; the engine scans
      the document, redacts matching content, and erases the specified metadata.'
    text: '**Apply the policy** – Call `engine.ApplyPolicy(policy)`; the engine scans
      the document, redacts matching content, and erases the specified metadata.'
  - name: '**Save the redacted document** – Use `engine.Save("RedactedFile.pdf")`
      to write the cleaned file to storage.'
    text: '**Save the redacted document** – Use `engine.Save("RedactedFile.pdf")`
      to write the cleaned file to storage.'
  type: HowTo
- questions:
  - answer: Yes, you can merge policies programmatically or load several policy files
      sequentially before applying them to a document.
    question: Can I combine multiple redaction policies together?
  - answer: It does when paired with OCR; the OCR engine extracts text, which can
      then be redacted using the same policy rules.
    question: Does GroupDocs.Redaction support redacting scanned images?
  - answer: Metadata redaction removes hidden properties (author, timestamps, custom
      fields) that are not visible in the content but may still expose sensitive information.
    question: How does “erase document metadata” differ from normal redaction?
  - answer: AI models provide a strong first pass; you should still review flagged
      items, especially for high‑risk compliance scenarios.
    question: Is AI‑assisted redaction accurate enough for compliance?
  - answer: GroupDocs.Redaction .NET works with .NET Framework 4.6.1+, .NET Core 3.1+,
      and .NET 5/6+.
    question: What .NET versions are supported?
  type: FAQPage
tags:
- redaction policy
- GroupDocs.Redaction
- .NET document security
- PDF privacy
title: Cara mengaburkan PDF dengan kebijakan di GroupDocs.Redaction .NET
type: docs
url: /id/net/advanced-redaction/
weight: 9
---

# Cara men‑redact PDF dengan kebijakan di GroupDocs.Redaction .NET

Dalam panduan komprehensif ini Anda akan belajar **cara men‑redact PDF** dengan membuat kebijakan redaksi yang dapat digunakan kembali, mengotomatiskan redaksi dokumen secara batch, dan menghapus metadata tersembunyi PDF. Apakah Anda perlu memenuhi GDPR, HIPAA, atau standar keamanan internal, menguasai kebijakan redaksi di GroupDocs.Redaction untuk .NET memberi Anda kontrol detail tentang apa yang disembunyikan, bagaimana cara menyembunyikannya, dan bagaimana metadata dihapus. Mari kita jelajahi konsepnya, mengapa penting, dan langkah tepat untuk mengimplementasikannya hari ini.

## Jawaban Cepat
- **Apa itu kebijakan redaksi?** Sekumpulan aturan yang dapat digunakan kembali yang memberi tahu engine teks, gambar, atau metadata mana yang harus dihapus dari dokumen.  
- **Mengapa membuat kebijakan redaksi?** Ini memungkinkan Anda menerapkan aturan perlindungan data yang konsisten dan dapat diulang pada banyak file tanpa menulis ulang kode setiap kali.  
- **Bisakah saya menggunakan AI untuk menemukan data sensitif?** Ya—GroupDocs.Redaction mendukung integrasi **ai document redaction** yang secara otomatis menemukan pengidentifikasi pribadi.  
- **Bagaimana cara menghapus metadata dokumen?** Tambahkan aturan “erase document metadata” ke kebijakan Anda; aturan ini menghapus penulis, tanggal pembuatan, dan properti tersembunyi.  
- **Apakah saya memerlukan lisensi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk penggunaan produksi; lisensi sementara tersedia untuk pengujian.

## Apa itu kebijakan redaksi?
Kebijakan redaksi adalah kumpulan item redaksi—seperti frasa tepat, pola regular‑expression, atau bidang metadata—yang diterapkan secara otomatis oleh engine. Dengan mendefinisikan kebijakan sekali, Anda dapat menggunakannya kembali pada banyak dokumen, memastikan penanganan privasi data yang konsisten. Kebijakan ini dapat disimpan ke disk, dikontrol versi, dan dimuat oleh aplikasi berbeda, memudahkan pemeliharaan kepatuhan di seluruh tim dan proyek.

## Mengapa menggunakan GroupDocs.Redaction untuk membuat kebijakan redaksi?
GroupDocs.Redaction memungkinkan Anda memusatkan aturan keamanan, memproses batch besar, dan mengintegrasikan deteksi berbantuan AI sekaligus menangani penghapusan metadata PDF dalam satu proses. Engine ini mendukung **lebih dari 50 format input dan output** dan dapat memproses dokumen hingga 2 GB tanpa memuat seluruh file ke memori, memberikan kinerja yang dapat diskalakan untuk beban kerja perusahaan.

## Cara men‑redact PDF menggunakan kebijakan redaksi di GroupDocs.Redaction .NET
Muat PDF target, buat kebijakan yang menjelaskan apa yang harus disembunyikan, dan terapkan kebijakan tersebut dalam satu panggilan. Pendekatan ini mengurangi duplikasi kode, memastikan setiap dokumen mengikuti aturan kepatuhan yang sama, dan menyelesaikan redaksi dalam aliran yang efisien memori.

1. **Tambahkan paket NuGet** – Install paket `GroupDocs.Redaction` terbaru melalui NuGet Package Manager atau CLI (`dotnet add package GroupDocs.Redaction`).  

2. **Instansiasi RedactionEngine** – `RedactionEngine` adalah kelas inti yang memuat dokumen dan melakukan operasi redaksi.  
   *Definition anchor:* `RedactionEngine` adalah kelas inti yang memuat dokumen dan melakukan operasi redaksi.  

3. **Definisikan item redaksi**  
   - **ExactPhraseRedaction** – Gunakan kelas ini untuk string tetap seperti “Social Security Number”.  
     *Definition anchor:* `ExactPhraseRedaction` mencocokkan kemunculan teks literal dalam dokumen.  
   - **RegexRedaction** – Terapkan pola regular‑expression untuk menangkap data variabel seperti nomor kartu kredit.  
     *Definition anchor:* `RegexRedaction` mengevaluasi regular expression .NET terhadap konten dokumen.  
   - **MetadataRedaction** – Sertakan item ini untuk menghapus metadata dokumen seperti penulis, tanggal pembuatan, dan bidang kustom tersembunyi.  
     *Definition anchor:* `MetadataRedaction` menghapus properti tak terlihat yang dapat mengungkap informasi sensitif.  

4. **Gabungkan item menjadi RedactionPolicy** – Kelompokkan item redaksi ke dalam objek `RedactionPolicy`, yang dapat disimpan (`policy.Save("MyPolicy.xml")`) dan nanti dimuat untuk penggunaan kembali.  
   *Definition anchor:* `RedactionPolicy` adalah wadah yang menyimpan sekumpulan aturan redaksi dan dapat dipertahankan ke disk.  

5. **Terapkan kebijakan** – Panggil `engine.ApplyPolicy(policy)`; engine memindai dokumen, men‑redact konten yang cocok, dan menghapus metadata yang ditentukan.  

6. **Simpan dokumen yang telah di‑redact** – Gunakan `engine.Save("RedactedFile.pdf")` untuk menulis file bersih ke penyimpanan.

### Cara men‑redact data menggunakan kebijakan
Muat kebijakan yang disimpan dan panggil pada setiap PDF yang perlu dibersihkan. Panggilan satu baris ini menjamin setiap file menerima perlindungan yang identik tanpa kode tambahan.

### Mengintegrasikan redaksi berbantuan AI
Sambungkan layanan AI (misalnya Azure Cognitive Services atau AWS Comprehend) ke antarmuka `IRedactionCallback`. Callback dapat mengirimkan lokasi yang diidentifikasi AI kembali ke kebijakan sebelum engine dijalankan, memberi Anda kemampuan **ai document redaction** yang kuat tanpa mengubah alur kerja inti.

## Kasus penggunaan umum
- **Compliance reporting:** Otomatis menghapus nama pasien, nomor rekam medis, atau pengidentifikasi keuangan sebelum membagikan laporan.  
- **Legal discovery:** Hapus klausa rahasia dan pengidentifikasi klien dari kumpulan dokumen besar.  
- **Document publishing:** Bersihkan draf dengan menghapus catatan penulis, komentar, dan metadata tersembunyi sebelum rilis publik.  

## Tips & praktik terbaik
- **Pro tip:** Simpan kebijakan dalam repositori yang dikontrol versi sehingga Anda dapat mengaudit perubahan seiring waktu.  
- **Warning:** Selalu uji kebijakan pada salinan dokumen terlebih dahulu; redaksi tidak dapat dibatalkan.  
- **Performance tip:** Proses batch file menggunakan panggilan asynchronous untuk meningkatkan throughput pada dataset besar.  

## Tutorial yang tersedia

### [Cara Membuat Kebijakan Redaksi Menggunakan GroupDocs.Redaction .NET: Panduan Langkah‑per‑Langkah](./groupdocs-redaction-net-create-save-policy/)
Pelajari cara membuat dan menyimpan kebijakan redaksi khusus dengan GroupDocs.Redaction untuk .NET. Amankan dokumen Anda dengan men‑redact informasi sensitif secara efisien.

### [Implementasi Logging Kustom di GroupDocs.Redaction untuk .NET: Panduan Komprehensif](./custom-logging-groupdocs-redaction-net/)
Pelajari cara mengimplementasikan logging kustom dengan GroupDocs.Redaction untuk .NET guna meningkatkan alur kerja redaksi dokumen. Temukan langkah praktis dan fitur utama.

### [Implementasi IRedactionCallback di GroupDocs.Redaction .NET untuk Redaksi Dokumen Aman dengan C#](./groupdocs-redaction-net-implement-iredactioncallback-csharp/)
Pelajari cara mengimplementasikan antarmuka IRedactionCallback menggunakan GroupDocs.Redaction .NET untuk alur kerja redaksi dokumen yang aman dan efisien. Temukan praktik terbaik dan aplikasi praktis.

### [Kuasi Redaksi .NET dengan GroupDocs: Terapkan Kebijakan ke File secara Efisien](./net-redaction-groupdocs-apply-policy-files/)
Pelajari cara mengotomatiskan redaksi di .NET menggunakan GroupDocs.Redaction, memastikan privasi data dan kepatuhan di seluruh file.

### [Kuasi Redaksi Kustom di .NET Menggunakan GroupDocs: Panduan Komprehensif](./master-custom-redaction-dotnet-groupdocs/)
Pelajari cara mengamankan informasi sensitif dalam dokumen menggunakan GroupDocs.Redaction untuk .NET. Implementasikan redaksi kustom dengan mudah dan pastikan privasi dokumen.

### [Kuasi Redaksi Dokumen di .NET Menggunakan GroupDocs.Redaction: Panduan Lengkap](./master-document-redaction-groupdocs-redaction-net/)
Pelajari cara mengamankan dokumen sensitif Anda dengan GroupDocs.Redaction untuk .NET. Panduan ini mencakup pengaturan, teknik redaksi, dan praktik terbaik.

### [Kuasi Redaksi Dokumen di .NET menggunakan GroupDocs.Redaction: Panduan Langkah‑per‑Langkah](./mastering-document-redaction-dotnet-groupdocs-redaction/)
Pelajari cara mengimplementasikan redaksi dokumen yang aman di .NET dengan GroupDocs.Redaction. Panduan ini mencakup penangan format kustom dan redaksi frasa tepat untuk pengembang.

### [Menguasai Keamanan Dokumen dengan GroupDocs.Redaction .NET: Panduan Komprehensif untuk Redaksi Frasa dan Metadata](./groupdocs-redaction-net-document-security-guide/)
Pelajari cara mengamankan dokumen sensitif menggunakan GroupDocs.Redaction untuk .NET. Panduan ini mencakup redaksi frasa tepat, redaksi berbasis regex, penghapusan anotasi, dan penghapusan metadata.

## Sumber daya tambahan

- [Dokumentasi GroupDocs.Redaction untuk .NET](https://docs.groupdocs.com/redaction/net/)
- [Referensi API GroupDocs.Redaction untuk .NET](https://reference.groupdocs.com/redaction/net/)
- [Unduh GroupDocs.Redaction untuk .NET](https://releases.groupdocs.com/redaction/net/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menggabungkan beberapa kebijakan redaksi bersama?**  
**A:** Ya, Anda dapat menggabungkan kebijakan secara programatis atau memuat beberapa file kebijakan secara berurutan sebelum menerapkannya ke dokumen.

**Q: Apakah GroupDocs.Redaction mendukung redaksi gambar yang dipindai?**  
**A:** Ya, ketika dipasangkan dengan OCR; mesin OCR mengekstrak teks, yang kemudian dapat di‑redact menggunakan aturan kebijakan yang sama.

**Q: Bagaimana “erase document metadata” berbeda dari redaksi normal?**  
**A:** Redaksi metadata menghapus properti tersembunyi (penulis, cap waktu, bidang kustom) yang tidak terlihat dalam konten tetapi masih dapat mengungkap informasi sensitif.

**Q: Apakah redaksi berbantuan AI cukup akurat untuk kepatuhan?**  
**A:** Model AI memberikan penyaringan awal yang kuat; Anda tetap harus meninjau item yang ditandai, terutama untuk skenario kepatuhan berisiko tinggi.

**Q: Versi .NET apa yang didukung?**  
**A:** GroupDocs.Redaction .NET bekerja dengan .NET Framework 4.6.1+, .NET Core 3.1+, dan .NET 5/6+.

---

**Terakhir Diperbarui:** 2026-10-01  
**Diuji Dengan:** GroupDocs.Redaction 2.0 for .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Buat Kebijakan Redaksi dengan GroupDocs.Redaction .NET – Panduan Langkah‑per‑Langkah](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Otomatisasi redaksi dokumen di .NET dengan GroupDocs – Terapkan Kebijakan secara Efisien](/redaction/net/advanced-redaction/net-redaction-groupdocs-apply-policy-files/)
- [Cara Men‑Redact PDF dan Menyimpan sebagai PDF Rasterized dengan GroupDocs.Redaction untuk .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)