---
date: '2026-10-01'
description: Pelajari cara menghapus author metadata dan menyimpan redacted document
  files di Java menggunakan GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Pelajari cara menghapus author metadata dan menyimpan redacted document
  files di Java menggunakan GroupDocs Redaction. Ikuti panduan langkah demi langkah.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Cara menghapus author metadata di Java dengan GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Cara menghapus author metadata di Java dengan GroupDocs
type: docs
url: /id/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Cara menghapus metadata penulis di Java dengan GroupDocs

Di lanskap digital saat ini, melindungi informasi sensitif yang tersembunyi di dalam dokumen merupakan praktik yang wajib dimiliki. **Menghapus metadata penulis** mencegah pengungkapan tidak sengaja dari identitas pribadi atau perusahaan. Tutorial ini menunjukkan kepada Anda, langkah demi langkah, cara menggunakan `EraseMetadataRedaction` dari GroupDocs.Redaction untuk Java untuk menghapus bidang seperti *Author* dan *Manager* dari file Word, dan kemudian **menyimpan salinan dokumen yang telah di-redact** dengan aman untuk dibagikan atau diarsipkan.

## Jawaban Cepat
- **Apa yang dilakukan EraseMetadataRedaction?** Itu menghapus bidang metadata yang dipilih dari sebuah dokumen.  
- **Perpustakaan mana yang menyediakan fitur ini?** GroupDocs.Redaction untuk Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menargetkan beberapa bidang sekaligus?** Ya, gabungkan filter dengan operator logika OR.  
- **Apakah proses ini thread‑safe?** Instance Redactor tidak dibagikan antar thread; buat instance baru untuk setiap operasi.  

## Apa itu EraseMetadataRedaction?
`EraseMetadataRedaction` adalah kelas redaksi bawaan yang memungkinkan Anda menentukan entri metadata mana yang harus dihapus. Ia bekerja pada berbagai format dokumen yang didukung oleh GroupDocs.Redaction, memastikan bahwa informasi penulisan tersembunyi tidak pernah bocor. Anda dapat menargetkan properti standar seperti Author, Manager, serta bidang metadata khusus, memberikan perlindungan privasi yang komprehensif.

## Mengapa menggunakan EraseMetadataRedaction dengan GroupDocs?
GroupDocs.Redaction mendukung **lebih dari 100 format input dan output** dan dapat memproses dokumen hingga 500 halaman tanpa memuat seluruh file ke dalam memori. Menggunakan kelas ini memberi Anda satu API berperforma tinggi untuk memenuhi persyaratan GDPR, HIPAA, atau kepatuhan internal sambil menjaga basis kode Anda tetap sederhana.

## Prasyarat
- Java 8 atau lebih tinggi terpasang.  
- Maven (atau kemampuan menambahkan JAR secara manual).  
- GroupDocs.Redaction untuk Java (versi 24.9 atau lebih baru).  
- Lisensi percobaan atau lisensi permanen GroupDocs yang valid.  

## Menyiapkan GroupDocs.Redaction untuk Java

### Instalasi Maven
Add the GroupDocs repository and dependency to your **pom.xml**:

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
Sebagai alternatif, unduh JAR terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
Dapatkan percobaan gratis atau beli lisensi sementara dari portal GroupDocs. File lisensi harus ditempatkan di lokasi yang dapat dimuat oleh aplikasi Anda (mis., root classpath).

### Inisialisasi dan Pengaturan Dasar
Below is a minimal example that creates a `Redactor` instance for a DOCX file:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Cara menggunakan EraseMetadataRedaction di Java
Bagian-bagian berikut memecah implementasi menjadi langkah-langkah yang jelas dan dapat ditindaklanjuti.

### Fitur: bersihkan item metadata spesifik

#### Gambaran Umum
Kami akan menghapus bidang metadata **Author** dan **Manager** menggunakan `EraseMetadataRedaction`. Ini adalah kebutuhan umum saat membagikan laporan internal kepada mitra eksternal.

#### Implementasi langkah‑demi‑langkah

##### 1️⃣ Inisialisasi objek Redactor
`Redactor` is the core class that loads a document, applies redaction objects, and writes the result. Create a new instance for each file you process:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Terapkan EraseMetadataRedaction
`MetadataFilters` provides predefined filters for common metadata keys such as Author and Manager.  
`EraseMetadataRedaction` removes metadata entries that match the supplied `MetadataFilters`. The bitwise OR (`|`) combines the `Author` and `Manager` filters so both fields are removed in one call:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Konfigurasi opsi penyimpanan
`SaveOptions` lets you specify the output file name, format, and other saving parameters.  
`SaveOptions` lets you control the output file name, format, and whether the document should be rasterized to PDF. Adding a suffix keeps the original file untouched:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Kasus penggunaan umum
1. **Legal documents** – Redact informasi penulis sebelum mengirim kontrak ke penasihat lawan.  
2. **Laporan korporat** – Hapus nama manajer saat mempublikasikan hasil kuartalan kepada pemegang saham.  
3. **File proyek** – Bersihkan dokumentasi proyek internal sebelum diarsipkan atau diunggah ke repositori publik.  

## Tips Pemecahan Masalah
- **File not found** – Verifikasi bahwa jalur di `inputFilePath` mengarah ke file yang ada dan aplikasi memiliki izin baca.  
- **Missing metadata fields** – Tidak semua tipe dokumen menyimpan kunci metadata yang sama; periksa properti dokumen di Office terlebih dahulu.  
- **License errors** – Pastikan file lisensi dimuat dengan benar sebelum membuat instance `Redactor`.  

## Pertimbangan Kinerja
- Tutup objek `Redactor` dengan cepat (seperti yang ditunjukkan dalam blok `finally`) untuk membebaskan sumber daya native.  
- Hindari merasterkan dokumen besar kecuali Anda memerlukan pratinjau PDF; rasterisasi dapat meningkatkan penggunaan CPU dan memori hingga 3× untuk file 300‑halaman.  

## Pertanyaan yang Sering Diajukan

**Q1: Apa itu redaksi metadata?**  
A1: Redaksi metadata melibatkan penghapusan properti dokumen tersembunyi (seperti penulis, manajer, atau tag khusus) untuk mencegah pengungkapan tidak sengaja informasi sensitif.

**Q2: Bisakah saya menggunakan GroupDocs.Redaction untuk tipe file lain?**  
A2: Ya, perpustakaan ini mendukung PDF, DOCX, PPTX, XLSX, dan banyak format lainnya—lebih dari 100 secara total.

**Q3: Bagaimana cara menangani kesalahan selama redaksi?**  
A3: Bungkus pemanggilan `apply` dalam blok try‑catch dan selalu tutup `Redactor` dalam klausa finally untuk memastikan sumber daya dilepaskan.

**Q4: Apakah memungkinkan untuk meredaksi bidang metadata khusus?**  
A5: Tentu saja. Gunakan `MetadataFilters.Custom("YourFieldName")` untuk menargetkan properti khusus apa pun yang disimpan dalam dokumen.

**Q5: Apa praktik terbaik untuk menggunakan GroupDocs.Redaction?**  
A5:  
- Muat lisensi di awal aplikasi Anda.  
- Tutup objek `Redactor` dengan cepat.  
- Gunakan `SaveOptions` untuk menambahkan sufiks, menjaga file asli tidak tersentuh.  
- Uji redaksi pada salinan dokumen sebelum memproses batch.

**Q6: Apakah EraseMetadataRedaction mendukung operasi batch?**  
A6: Anda dapat melakukan loop pada koleksi jalur file, membuat `Redactor` baru untuk setiap file dan menerapkan logika redaksi yang sama.

**Q7: Bisakah saya menggabungkan EraseMetadataRedaction dengan tipe redaksi lain?**  
A7: Ya, Anda dapat menautkan beberapa objek redaksi (mis., redaksi teks diikuti oleh redaksi metadata) sebelum menyimpan.

## Sumber Daya

- **Dokumentasi**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referensi API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Unduhan**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Dukungan gratis**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Lisensi sementara**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Terakhir Diperbarui:** 2026-10-01  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Ekstraksi Metadata Dokumen Java Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Cara Menghapus Metadata Java Menggunakan GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Mengambil Info Dokumen Menggunakan Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)