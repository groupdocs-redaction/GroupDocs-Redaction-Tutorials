---
date: '2026-08-20'
description: Pelajari cara menyensor teks dengan GroupDocs.Redaction Java, menyimpan
  sebagai rasterized PDF, mengganti frasa tepat, dan menerapkan custom PDF settings.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Cara menyensor teks dengan GroupDocs.Redaction Java. Panduan ini menunjukkan
  penggantian frasa tepat, pembuatan rasterized PDF, dan kepatuhan PDF/A‑1a dalam
  beberapa langkah.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Cara menyensor teks dengan GroupDocs.Redaction Java library
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Cara menyensor teks dengan GroupDocs.Redaction Java
type: docs
url: /id/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Cara menyensor teks dengan GroupDocs.Redaction Java

Dalam aplikasi modern, **cara menyensor teks** dalam sebuah dokumen sambil menjaga alur kerja tetap cepat dan sesuai regulasi merupakan tantangan yang sering dihadapi oleh pengembang, auditor, dan pejabat kepatuhan. Tutorial ini memandu Anda menggunakan GroupDocs.Redaction untuk Java untuk menemukan frasa tepat, menggantinya dengan overlay aman, dan akhirnya mengekspor hasilnya sebagai dokumen PDF/A‑1a yang dirasterisasi—sempurna untuk arsip atau distribusi hukum.

## Jawaban Cepat
- **Apa kelas utama untuk penyensoran?** `Redactor`  
- **Bisakah saya mengganti frasa dengan overlay berwarna?** Ya, menggunakan `ExactPhraseRedaction` dan `ReplacementOptions`.  
- **Bagaimana cara menghasilkan PDF yang dirasterisasi?** Aktifkan rasterisasi melalui `SaveOptions.getRasterization().setEnabled(true)`.  
- **Level kepatuhan PDF mana yang digunakan dalam contoh?** `PdfComplianceLevel.PdfA1a`.  
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk penyebaran produksi.

## Apa itu “cara menyensor teks” dalam Java?
`Redaction` adalah penghapusan atau penyamaran permanen konten sensitif dari sebuah file sehingga tidak dapat dipulihkan atau dibaca kembali. Dengan GroupDocs.Redaction Anda dapat secara programatis mencari frasa tepat—seperti nomor jaminan sosial atau kode proyek rahasia—dan menggantinya dengan overlay merah, kotak hitam, atau elemen visual kustom apa pun, menjamin data asli tidak dapat dipulihkan.

## Mengapa menggunakan GroupDocs.Redaction untuk Java?
GroupDocs.Redaction mendukung **lebih dari 30 format input dan output** (PDF, DOCX, PPTX, XLSX, HTML, dan tipe gambar) dan dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori. Algoritma pencocokan frasa tepatnya mengurangi positif palsu lebih dari > 95 % dibandingkan pencarian kata kunci umum, dan mesin rasterisasi bawaan memungkinkan Anda menghasilkan file PDF/A‑1a yang sepenuhnya berbasis gambar untuk preservasi jangka panjang.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki:

- **GroupDocs.Redaction untuk Java** (v24.9 atau lebih baru).  
- **Java Development Kit (JDK) 8+**.  
- Sebuah IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.  
- Maven untuk manajemen dependensi.  

### Perpustakaan dan dependensi yang diperlukan
- GroupDocs.Redaction untuk Java – tambahkan repositori dan dependensi ke `pom.xml` Anda (lihat bagian pengaturan Maven).  
- Opsional: kerangka logging apa pun yang Anda sukai (SLF4J, Log4j, dll.).

### Prasyarat pengetahuan
- Sintaks Java dasar dan I/O file.  
- Familiaritas dengan struktur `pom.xml` Maven.

## Menyiapkan GroupDocs.Redaction untuk Java
### Pengaturan Maven
Tambahkan repositori GroupDocs dan dependensi `groupdocs-redaction` ke file `pom.xml` Anda:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Unduhan langsung
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi lisensi
- **Uji coba gratis** – jelajahi API tanpa kunci lisensi.  
- **Lisensi sementara** – gunakan untuk evaluasi yang diperpanjang.  
- **Lisensi penuh** – diperlukan untuk lingkungan produksi.

### Inisialisasi dan pengaturan dasar
Kelas `Redactor` adalah titik masuk untuk semua operasi penyensoran. Ia memuat dokumen, menerapkan aturan penyensoran, dan menyimpan hasilnya.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Cara menyensor teks – contoh frasa tepat
Redactor adalah kelas utama yang memuat dokumen dan menerapkan aturan penyensoran. ExactPhraseRedaction mendefinisikan aturan yang mencocokkan string tertentu. Contoh ini menunjukkan cara memuat file, membuat aturan ExactPhraseRedaction, dan mengeksekusi penyensoran dalam satu langkah, memberikan alur kerja yang ringkas bagi pengembang sambil memastikan konten asli tersamarkan secara permanen.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Cara menyimpan sebagai PDF yang dirasterisasi
SaveOptions adalah objek konfigurasi yang mengontrol cara penyimpanan dokumen. Dengan mengaktifkan fitur rasterisasinya dan memilih kepatuhan PDF/A‑1a, Anda dapat menghasilkan PDF hanya gambar di mana setiap halaman dirender sebagai bitmap, memenuhi standar arsip dan mencegah ekstraksi teks.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Aplikasi praktis
1. **Penyensoran data sensitif** – secara otomatis menyembunyikan pengidentifikasi pribadi sebelum membagikan kontrak.  
2. **Pengarsipan dokumen** – mengonversi laporan akhir menjadi PDF/A yang dirasterisasi untuk kepatuhan jangka panjang.  
3. **Pembaruan konten massal** – mengganti terminologi usang di ratusan file dengan satu skrip.

## Pertimbangan kinerja
- **Tutup `Redactor`** setelah setiap operasi untuk melepaskan handle file dan memori.  
- **Pemrosesan batch** – muat daftar file dan iterasi melalui mereka, menggunakan kembali satu instance `Redactor` bila memungkinkan.  
- **Pantau sumber daya** – gunakan alat profiling Java untuk memantau penggunaan CPU dan heap selama penyensoran skala besar.

## Pertanyaan yang sering diajukan

**Q: Bagaimana cara menginstal GroupDocs.Redaction dalam proyek Maven?**  
A: Tambahkan repositori GroupDocs dan dependensi `groupdocs-redaction` ke `pom.xml` Anda seperti yang ditunjukkan pada bagian Pengaturan Maven.

**Q: Bisakah saya menyensor teks dari file PDF menggunakan perpustakaan ini?**  
A: Ya, GroupDocs.Redaction mendukung PDF, DOCX, PPTX, dan banyak format lainnya.

**Q: Apa yang terjadi jika frasa tepat tidak ditemukan?**  
A: `RedactorChangeLog` akan mengembalikan status `Failed`. Verifikasi ejaan dan sensitivitas huruf pada frasa tersebut.

**Q: Bagaimana saya dapat menangani dokumen sangat besar secara efisien?**  
A: Proses mereka dalam rentang halaman yang lebih kecil, aktifkan rasterisasi hanya bila diperlukan, dan selalu tutup `Redactor` untuk membebaskan sumber daya.

**Q: Apakah memungkinkan menyimpan PDF yang dirasterisasi dengan rentang halaman tertentu?**  
A: Tentu saja. Gunakan `options.getRasterization().setPageIndex()` dan `setPageCount()` untuk menargetkan halaman tepat yang ingin Anda rasterisasi.

## Kesimpulan
Anda kini memiliki panduan lengkap, end‑to‑end tentang **cara menyensor teks** dengan GroupDocs.Redaction Java dan **menyimpan sebagai PDF yang dirasterisasi**. Dengan mengikuti langkah‑langkah ini, Anda dapat melindungi informasi sensitif, memenuhi standar kepatuhan yang ketat, dan menjaga layanan Java Anda tetap berperforma pada skala besar.

**Langkah selanjutnya**  
- Selami lebih dalam API dengan menjelajahi [dokumentasi resmi](https://docs.groupdocs.com/redaction/java/).  
- Bereksperimen dengan tipe penyensoran lain seperti `RegexRedaction` dan `ImageRedaction`.  
- Bergabung dengan komunitas di [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk tips dan praktik terbaik.

---

**Terakhir Diperbarui:** 2026-08-20  
**Diuji Dengan:** GroupDocs.Redaction Java 24.9  
**Penulis:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Tutorial Terkait

- [Cara Menyensor Teks dengan GroupDocs.Redaction untuk Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Tutorial Penyensoran Teks Java: Panduan dengan GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)