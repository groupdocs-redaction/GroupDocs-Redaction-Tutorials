---
date: 2026-08-04
description: Pelajari cara memfilter data spreadsheet Java dan secara aman redact
  kolom atau sel dalam spreadsheet Excel menggunakan GroupDocs.Redaction untuk Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Pelajari cara memfilter data spreadsheet Java dan secara aman redact
  kolom atau sel dalam spreadsheet Excel menggunakan GroupDocs.Redaction untuk Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filter data spreadsheet Java – panduan dengan GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filter data spreadsheet Java – panduan dengan GroupDocs.Redaction
type: docs
url: /id/java/spreadsheet-redaction/
weight: 12
---

# Filter data spreadsheet java – Tutorial GroupDocs.Redaction Java

Jika Anda perlu **filter spreadsheet data java** sebelum menerapkan redaksi, Anda berada di panduan yang tepat. Dalam tutorial ini Anda akan menemukan cara mengisolasi baris, kolom, atau sel individual yang berisi informasi pribadi atau rahasia, kemudian menyorotnya dengan aman menggunakan GroupDocs.Redaction untuk Java. Langkah‑langkah dijelaskan dengan bahasa sederhana, termasuk tips praktik terbaik, dan menunjukkan cara menjaga proses tetap cepat bahkan pada buku kerja besar.

## Jawaban Cepat
- **Library mana yang menangani redaksi spreadsheet di Java?** GroupDocs.Redaction for Java.  
- **Bisakah saya memfilter baris tanpa memuat seluruh file ke memori?** Ya – API mengalirkan data dan memungkinkan Anda menerapkan filter secara langsung.  
- **Format file apa yang didukung?** Lebih dari 30 format spreadsheet, termasuk XLS, XLSX, CSV, dan ODS.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi sementara dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Apakah ada batas ukuran buku kerja?** Mesin dapat memproses file hingga 500 MB tanpa konsumsi memori berlebih.

## Apa itu filter spreadsheet data java?
**Filter spreadsheet data java** adalah proses pemilihan programatis baris, kolom, atau sel tertentu dalam buku kerja bergaya Excel menggunakan kode Java sehingga hanya konten yang ditargetkan yang diperiksa atau disunting. Teknik ini mengurangi waktu proses, membatasi perubahan yang tidak perlu, dan membantu memenuhi kepatuhan tipe GDPR.

## Mengapa filter spreadsheet data java?
GroupDocs.Redaction Java mendukung **30+ format spreadsheet** dan dapat memproses buku kerja berukuran **hingga 500 MB** (sekitar 1 juta baris) sambil menjaga penggunaan memori di bawah **200 MB**. Dengan memfilter terlebih dahulu, Anda menghindari menyentuh data yang tidak terkait, yang memotong waktu pemrosesan sebesar **40‑60 %** rata‑rata untuk skenario pembersihan privasi.

## Prasyarat
- Java 17 atau lebih baru terpasang.  
- Sistem build Maven atau Gradle.  
- GroupDocs.Redaction untuk Java (dapat diunduh dari situs resmi).  
- Kunci lisensi sementara atau penuh.  

## Cara memfilter data dalam spreadsheet menggunakan GroupDocs.Redaction Java?
Muat buku kerja, definisikan filter yang cocok dengan sel yang ingin Anda sunting, dan kemudian terapkan operasi redaksi. API melakukan filter secara streaming, sehingga Anda tidak pernah perlu menahan seluruh file di RAM.

Kelas `RedactionFilter` memungkinkan Anda menentukan indeks kolom, rentang baris, atau predikat khusus. Misalnya, Anda dapat menargetkan setiap sel di kolom **B** yang berisi pola alamat email, atau Anda dapat membatasi redaksi pada baris di mana kolom “Status” bernilai “Confidential”.

**Jawaban langsung (40‑70 kata):**  
Buat instance `RedactionFilter`, atur indeks kolom dan kondisi ekspresi reguler, lalu berikan filter ke `Redactor.redact(workbook, filter)`. Filter satu baris ini mengisolasi sel yang tepat yang cocok dengan kriteria Anda, dan redaktor menghapus atau menyamarkannya sementara membiarkan sisanya tetap tidak tersentuh. Operasi selesai dalam waktu linear relatif terhadap baris yang difilter.

### Langkah 1: buat instance filter
`RedactionFilter` adalah kelas inti yang mewakili aturan filter untuk redaksi spreadsheet. Ia menerima nomor kolom, nomor baris, atau ekspresi lambda khusus untuk menentukan data.

### Langkah 2: konfigurasikan kondisi
Gunakan `filter.setColumnIndex(1)` untuk menargetkan kolom B (berbasis nol) dan `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` untuk mencocokkan pola email. Anda juga dapat menggabungkan beberapa kondisi dengan `filter.and(...)` atau `filter.or(...)`.

### Langkah 3: terapkan redaksi
`Redactor` adalah kelas utama yang mengeksekusi operasi redaksi pada buku kerja.  
Berikan buku kerja dan filter yang telah dikonfigurasi ke objek `Redactor`. API mengalirkan buku kerja, menerapkan filter, dan menulis hasil yang disunting ke file baru, mempertahankan format dan formula asli.

## Masalah umum dan solusi
- **Filter tidak cocok dengan sel apa pun:** Verifikasi indeks kolom (berbasis nol) dan pastikan sintaks ekspresi reguler benar untuk Java.  
- **Kesalahan out‑of‑memory pada file besar:** Tingkatkan ukuran heap JVM secara moderat (mis., `-Xmx1g`) atau bagi buku kerja menjadi potongan lebih kecil sebelum memfilter.  
- **Output yang disunting kehilangan format:** `RedactionOptions` memungkinkan Anda menyesuaikan perilaku redaksi, seperti mempertahankan format sel. Gunakan `RedactionOptions.setPreserveFormatting(true)` untuk menjaga gaya sel tetap utuh.

## Mengapa filter data spreadsheet?
Memfilter sebelum redaksi mengisolasi hanya bagian sensitif dari buku kerja, yang berarti Anda menghindari perubahan yang tidak perlu pada data bersih. Pendekatan selektif ini juga mengurangi risiko kehilangan data secara tidak sengaja dan mempercepat audit kepatuhan karena log audit berisi jauh lebih sedikit entri.

## Cara menyunting email di spreadsheet Excel menggunakan GroupDocs.Redaction Java API
Muat file Excel Anda, terapkan filter yang mencari pola email tipikal, dan panggil redaktor. API menggantikan setiap email yang cocok dengan placeholder seperti “***@***.com” sambil mempertahankan tata letak sel di sekitarnya.

## Cara memfilter data – tutorial yang tersedia
- [Cara Menyunting Email di Spreadsheet Excel Menggunakan GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Sumber daya tambahan

- [Dokumentasi GroupDocs.Redaction untuk Java](https://docs.groupdocs.com/redaction/java/)
- [Referensi API GroupDocs.Redaction untuk Java](https://reference.groupdocs.com/redaction/java/)
- [Unduh GroupDocs.Redaction untuk Java](https://releases.groupdocs.com/redaction/java/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Dukungan Gratis](https://forum.groupdocs.com/)
- [Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-08-04  
**Diuji Dengan:** GroupDocs.Redaction 23.11 untuk Java  
**Penulis:** GroupDocs  

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya memfilter beberapa kolom sekaligus?**  
A: Ya, Anda dapat menambahkan indeks kolom tambahan ke instance `RedactionFilter` yang sama atau menggabungkan beberapa filter dengan `filter.or(...)`.

**Q: Apakah filter berfungsi pada buku kerja yang dilindungi kata sandi?**  
A: Berikan kata sandi saat membuka buku kerja; filter beroperasi setelah dekripsi seperti pada file yang tidak dilindungi.

**Q: Berapa banyak baris yang dapat ditangani API dalam satu operasi?**  
A: Mesin dioptimalkan untuk hingga 1 juta baris (≈500 MB) tanpa memuat seluruh file ke memori.

**Q: Apakah memungkinkan untuk melihat pratinjau sel yang akan disunting sebelum menyimpan?**  
A: Ya, panggil `filter.preview(workbook)` untuk mendapatkan daftar alamat sel yang cocok dengan kriteria.

**Q: Model lisensi apa yang diperlukan untuk penggunaan produksi?**  
A: Lisensi komersial penuh diperlukan untuk penerapan produksi; lisensi sementara cukup untuk pengujian dan evaluasi.

## Tutorial Terkait

- [Cara Menyunting Data Sensitif di Spreadsheet Excel Menggunakan GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Data Sensitif Java – Panduan GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mask Data Sensitif Java – Redact Informasi Pribadi dengan GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)