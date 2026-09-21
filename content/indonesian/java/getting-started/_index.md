---
date: 2026-09-21
description: Pelajari cara merasterisasi halaman yang disensor sambil menyembunyikan
  data sensitif di Java menggunakan GroupDocs.Redaction. Panduan langkah demi langkah
  mencakup instalasi, lisensi, pembuatan aturan, dan praktik terbaik.
keywords:
- rasterize redacted pages
- hide personal identifiers
- mask credit card numbers
- mask sensitive data java
- redact pdf java
lastmod: 2026-09-21
og_description: Rasterisasi halaman yang disensor sambil menyembunyikan data sensitif
  di Java dengan GroupDocs.Redaction. Temukan cara menyembunyikan pengenal pribadi,
  menyamarkan nomor kartu kredit, dan mematuhi GDPR dalam hitungan menit.
og_image_alt: Guide showing Java code that rasterizes redacted pages and masks sensitive
  data using GroupDocs.Redaction
og_title: Rasterisasi halaman yang disensor dan sembunyikan data sensitif di Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  headline: Rasterize redacted pages and mask sensitive data in Java
  type: TechArticle
- description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  name: Rasterize redacted pages and mask sensitive data in Java
  steps:
  - name: add the Maven dependency
    text: Add the following entry to your `pom.xml` (or the equivalent Gradle snippet).
      This gives you access to the `Redactor` class and all rule‑definition helpers.
  - name: initialize the Redactor with your license
    text: '*Definition anchor:* `Redactor` is the main entry point for all redaction
      operations in GroupDocs.Redaction for Java.'
  - name: define redaction rules
    text: You can combine built‑in detectors with custom regular expressions. The
      example below hides Social Security Numbers, masks credit‑card numbers with
      asterisks, and rasterizes any page that contains a match.
  - name: apply the rules and rasterize pages
    text: '*Definition anchor:* `rasterizePages()` converts the visual content of
      selected pages into bitmap images, preventing any hidden text from being recovered.'
  - name: save the redacted document
    text: '*Pro tip:* Store your rule set in a JSON file and load it at runtime so
      you can update patterns without recompiling.'
  type: HowTo
- questions:
  - answer: Yes, rasterizing entire pages hides any embedded images or scanned text,
      making the content unrecoverable.
    question: Can I redact images that contain text?
  - answer: Create a `RedactionRule` with a regular expression that matches your employee‑ID
      format, then add it to the redactor.
    question: How do I redact custom patterns like employee IDs?
  - answer: Use `RedactionResult.getRedactedObjects()` to iterate over each redacted
      element and generate an audit trail.
    question: Is it possible to keep a log of what was redacted?
  - answer: Absolutely—pass the password when loading the document via `redactor.load(inputStream,
      "password")`.
    question: Does the library support password‑protected documents?
  - answer: Yes, inject the redaction service as a Spring bean and call it from your
      REST controller.
    question: Can I integrate this into a Spring Boot microservice?
  type: FAQPage
tags:
- redaction
- GroupDocs.Redaction
- Java document processing
- data privacy
title: Rasterisasi halaman yang disensor dan sembunyikan data sensitif di Java
type: docs
url: /id/java/getting-started/
weight: 1
---

# Rasterisasi halaman yang disensor dan sembunyikan data sensitif di Java

Dalam tutorial komprehensif ini Anda akan belajar cara **rasterize redacted pages** dan menyembunyikan data sensitif yang dihadapi pengembang Java setiap hari. Apakah Anda perlu menyembunyikan pengidentifikasi pribadi, menyamarkan nomor kartu kredit, atau mematuhi GDPR dan HIPAA, GroupDocs.Redaction memberikan API yang mudah digunakan yang mengotomatiskan seluruh alur kerja. Anda akan melihat mengapa rasterisasi halaman mempertahankan tata letak, cara mendefinisikan aturan penyensoran yang fleksibel, dan langkah apa yang diperlukan untuk mendapatkan solusi siap produksi yang berjalan di Java 8+.

## Jawaban Cepat
- **What does “mask sensitive data Java” mean?** Itu berarti menggunakan kode Java dan GroupDocs.Redaction untuk secara otomatis menemukan dan menyamarkan informasi rahasia di dalam dokumen.  
- **Do I need a license?** Ya, lisensi GroupDocs.Redaction yang valid diperlukan untuk penggunaan produksi.  
- **Which document types are supported?** PDF, DOCX, PPTX, XLSX, gambar, dan banyak format umum lainnya.  
- **Can I process documents in bulk?** Tentu—aturan penyensoran dapat diterapkan pada batch besar melalui loop sederhana.  
- **Is the library compatible with Java 8+?** Ya, ia bekerja dengan Java 8 dan versi yang lebih baru.  

## Apa itu “mask sensitive data Java”?
Menyamarkan data sensitif di Java berarti secara programatik menemukan informasi pribadi atau rahasia dalam dokumen dan menyembunyikannya. Dengan menggunakan GroupDocs.Redaction, pengembang dapat mendefinisikan pola atau detektor yang secara otomatis mengganti data dengan asterisk, kotak hitam, atau gambar raster, memastikan tata letak asli tetap tidak berubah sambil melindungi privasi.  
Kelas `Redactor` memuat dokumen, menerapkan aturan penyensoran, dan menulis output yang disensor.

## Mengapa menggunakan GroupDocs.Redaction untuk penyembunyian?
GroupDocs.Redaction menawarkan detektor bawaan dengan akurasi 99,7 % untuk SSN, nomor kartu kredit, dan email, serta dapat merasterisasi halaman untuk membuat konten tersembunyi tidak dapat dipulihkan. Ia mendukung lebih dari 50 format, bekerja pada Java 8+, dan memproses file besar secara efisien, membantu Anda memenuhi kepatuhan GDPR, HIPAA, dan PCI‑DSS.

## Prasyarat
- Java 8 atau yang lebih baru terpasang pada mesin pengembangan Anda.  
- Maven atau Gradle untuk manajemen dependensi.  
- File lisensi GroupDocs.Redaction (lisensi sementara tersedia untuk evaluasi).  

## Cara menyamarkan data sensitif di Java
Untuk menyamarkan data sensitif di Java, buat instance `Redactor`, tambahkan aturan penyensoran yang diperlukan, aktifkan rasterisasi untuk halaman yang mengandung kecocokan, dan simpan dokumen. Alur kerja satu langkah ini menyederhanakan implementasi dan memastikan baik penyensoran maupun perlindungan visual diterapkan secara konsisten.

### Langkah 1: tambahkan dependensi Maven
Tambahkan entri berikut ke `pom.xml` Anda (atau potongan Gradle yang setara). Ini memberi Anda akses ke kelas `Redactor` dan semua pembantu definisi aturan.

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-redaction</artifactId>
    <version>3.0</version>
</dependency>
```

### Langkah 2: inisialisasi Redactor dengan lisensi Anda
```java
Redactor redactor = new Redactor();
redactor.setLicense("path/to/license.lic");
```
*Definition anchor:* `Redactor` adalah titik masuk utama untuk semua operasi penyensoran di GroupDocs.Redaction untuk Java.

### Langkah 3: definisikan aturan penyensoran
Anda dapat menggabungkan detektor bawaan dengan ekspresi reguler khusus. Contoh di bawah menyembunyikan Nomor Jaminan Sosial, menyamarkan nomor kartu kredit dengan asterisk, dan merasterisasi setiap halaman yang mengandung kecocokan.

```java
redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.SSN())
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withPattern("\\b\\d{4}[- ]?\\d{4}[- ]?\\d{4}[- ]?\\d{4}\\b")
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.PATTERN("\\bCONFIDENTIAL\\b"))
    .withRedactionType(RedactionType.RASTERIZE));
```

### Langkah 4: terapkan aturan dan rasterisasi halaman
```java
redactor.load("input.pdf");
redactor.applyRules();               // runs all defined rules
redactor.rasterizePages();           // converts matched pages to images
```
*Definition anchor:* `rasterizePages()` mengubah konten visual halaman yang dipilih menjadi gambar bitmap, mencegah teks tersembunyi apa pun dipulihkan.

### Langkah 5: simpan dokumen yang disensor
```java
redactor.save("output.pdf");
redactor.close();    // releases all resources
```
*Pro tip:* Simpan set aturan Anda dalam file JSON dan muat pada runtime sehingga Anda dapat memperbarui pola tanpa harus mengkompilasi ulang.

## Kesalahan umum & pemecahan masalah

- **Rule not triggering** – Verifikasi bahwa ekspresi reguler Anda benar dan sensitivitas huruf detektor sesuai dengan data sumber.  
- **Performance lag on large PDFs** – Aktifkan mode streaming dengan `redactor.setUseMemoryStream(false)` untuk menjaga penggunaan memori tetap rendah.  
- **Output file corrupted** – Selalu tutup instance `Redactor` atau gunakan blok try‑with‑resources untuk memastikan aliran (streams) dibersihkan.  

## Pertanyaan yang sering diajukan

**Q: Can I redact images that contain text?**  
A: Ya, merasterisasi seluruh halaman menyembunyikan gambar yang disematkan atau teks yang dipindai, membuat konten tidak dapat dipulihkan.

**Q: How do I redact custom patterns like employee IDs?**  
A: Buat `RedactionRule` dengan ekspresi reguler yang cocok dengan format ID karyawan Anda, lalu tambahkan ke redactor.

**Q: Is it possible to keep a log of what was redacted?**  
A: Gunakan `RedactionResult.getRedactedObjects()` untuk mengiterasi setiap elemen yang disensor dan menghasilkan jejak audit.

**Q: Does the library support password‑protected documents?**  
A: Tentu—lewatkan kata sandi saat memuat dokumen melalui `redactor.load(inputStream, "password")`.

**Q: Can I integrate this into a Spring Boot microservice?**  
A: Ya, injeksikan layanan penyensoran sebagai bean Spring dan panggil dari controller REST Anda.

## Sumber daya tambahan

- [Dokumentasi GroupDocs.Redaction untuk Java](https://docs.groupdocs.com/redaction/java/)
- [Referensi API GroupDocs.Redaction untuk Java](https://reference.groupdocs.com/redaction/java/)
- [Unduh GroupDocs.Redaction untuk Java](https://releases.groupdocs.com/redaction/java/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

## Tutorial yang Tersedia

### [Menerapkan Redaksi Java dengan GroupDocs.Redaction: Panduan Komprehensif untuk Pengembang](./implement-java-redaction-groupdocs-redaction-guide/)
Pelajari cara menerapkan redaksi yang efektif di Java menggunakan GroupDocs.Redaction. Lindungi informasi sensitif secara mulus sambil mempertahankan integritas dokumen.

### [Panduan Redaksi Java: Manajemen Dokumen Efisien dengan GroupDocs.Redaction](./java-redaction-groupdocs-efficient-document-setup/)
Pelajari cara menyiapkan dan mengelola redaksi dokumen secara efisien di Java menggunakan GroupDocs.Redaction. Sempurna untuk melindungi informasi sensitif.

### [Tutorial Redaksi Java: Menggunakan API GroupDocs.Redaction untuk Mengamankan Dokumen](./java-groupdocs-redaction-tutorial/)
Pelajari cara menggunakan pustaka GroupDocs.Redaction Java untuk menyensor informasi sensitif dari dokumen. Panduan komprehensif ini mencakup penyiapan, implementasi, dan praktik terbaik.

### [Menguasai Redaksi Dokumen di Java Menggunakan GroupDocs.Redaction: Panduan Langkah‑Demi‑Langkah](./master-document-redaction-java-groupdocs/)
Pelajari cara menyensor data sensitif dari PDF dan file Word menggunakan GroupDocs.Redaction untuk Java. Terapkan redaksi frasa tepat, rasterisasi dokumen untuk privasi, dan pastikan kepatuhan dengan mudah.

---

**Terakhir Diperbarui:** 2026-09-21  
**Diuji Dengan:** GroupDocs.Redaction 3.0 (Java)  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Merasterisasi PDF dengan GroupDocs.Redaction Java – Tutorial](/redaction/java/rasterization-options/)
- [Cara merasterisasi PDF ke skala abu-abu dengan GroupDocs.Redaction Java – Amankan dan Optimalkan Dokumen Anda](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Redaksi Teks Groupdocs Redaction Java Rasterisasi Pdf](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/)