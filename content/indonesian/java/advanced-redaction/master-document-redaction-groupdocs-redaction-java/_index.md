---
date: '2026-11-02'
description: Pelajari cara menambahkan akhiran pada nama file dalam tutorial GroupDocs
  redaction Java menggunakan Maven, streaming load, annotation deletion, dan save
  options.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Pelajari cara menambahkan akhiran pada nama file dalam tutorial GroupDocs
  redaction Java. Ikuti langkah demi langkah setup Maven, streaming load, dan save
  options.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Cara menambahkan akhiran pada nama file di GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Cara menambahkan akhiran pada nama file di GroupDocs redaction Java
type: docs
url: /id/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cara menambahkan akhiran ke nama file di GroupDocs redaction Java

Dalam **groupdocs redaction java tutorial** ini Anda akan belajar cara secara otomatis menambahkan akhiran ke nama file output saat melakukan redaksi dokumen dengan GroupDocs.Redaction. Menambahkan akhiran menghilangkan kebutuhan untuk mengganti nama secara manual, mengurangi risiko kebocoran file yang belum direduksi, dan cocok dengan pipeline CI/CD yang mengandalkan konvensi penamaan. Panduan ini mengarahkan Anda melalui pengaturan Maven, pemuatan dokumen melalui streaming, penghapusan anotasi, dan konfigurasi opsi penyimpanan—semua dengan kode yang ringkas dan siap produksi.

## Jawaban Cepat
- **Apa yang dilakukan “menambahkan akhiran ke nama file”?**  
  Saat Anda mengaktifkan opsi akhiran, SDK secara otomatis menambahkan string yang telah ditentukan (secara default “_redacted”) ke nama dasar file output sebelum ekstensi. Hal ini membuat jelas file mana yang telah diproses, membantu mencegah distribusi tidak sengaja konten asli, dan menyederhanakan otomatisasi downstream yang mengandalkan pola penamaan.  
- **Apakah saya dapat memuat dokumen dari stream?**  
  Ya—GroupDocs.Redaction mendukung pemuatan dari `InputStream` apa pun, cocok untuk penyimpanan cloud atau pemrosesan dalam memori.  
- **Apakah saya memerlukan lisensi untuk fitur ini?**  
  Versi percobaan gratis berfungsi untuk redaksi dasar; lisensi sementara atau penuh membuka semua opsi lanjutan, termasuk penanganan akhiran.  
- **Format apa saja yang didukung?**  
  Perpustakaan menangani DOCX, PDF, PPTX, XLSX, dan banyak lagi.  
- **Apakah rasterisasi diperlukan untuk output PDF?**  
  Rasterisasi bersifat opsional; aktifkan bila Anda perlu meratakan dokumen untuk keamanan tambahan.

## Apa yang dilakukan “menambahkan akhiran ke nama file”?

Saat Anda mengaktifkan opsi akhiran, SDK secara otomatis menambahkan string yang telah ditentukan (secara default “_redacted”) ke nama dasar file output sebelum ekstensi. Hal ini membuat jelas file mana yang telah diproses, membantu mencegah distribusi tidak sengaja konten asli, dan menyederhanakan otomatisasi downstream yang mengandalkan pola penamaan.

## Mengapa menggunakan GroupDocs.Redaction untuk tugas ini?

GroupDocs.Redaction menawarkan API Java berperforma tinggi yang menggabungkan tindakan redaksi dengan opsi penanganan file fleksibel seperti penambahan akhiran otomatis, dukungan streaming, dan pemrosesan batch. Ia mendukung lebih dari 50 format input dan output serta dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori, memastikan penggunaan memori rendah dan eksekusi cepat.

## Prasyarat

- **Java Development Kit (JDK):** Versi 8 atau lebih tinggi.  
- **GroupDocs.Redaction Library:** Perpustakaan inti untuk tugas redaksi.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor Java‑compatible lainnya.  
- **Maven:** Untuk manajemen dependensi.  

### Prasyarat pengetahuan
Familiaritas dengan Java I/O dan konsep berorientasi objek dasar akan memudahkan pemahaman contoh.

## Menyiapkan GroupDocs.Redaction untuk Java

### Pengaturan Maven
Sertakan konfigurasi berikut dalam file `pom.xml` Anda untuk mengakses perpustakaan GroupDocs melalui Maven:

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
Sebagai alternatif, unduh versi terbaru langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi lisensi
1. **Free trial:** Akses fungsionalitas dasar tanpa batasan.  
2. **Temporary license:** Dapatkan lisensi sementara untuk menjelajahi fitur lanjutan.  
3. **Purchase:** Untuk penggunaan jangka panjang, pertimbangkan membeli lisensi penuh.

#### Inisialisasi dasar dan pengaturan
Inisialisasi proyek Anda dengan menambahkan impor yang diperlukan:

```java
import com.groupdocs.redaction.Redactor;
```

Dengan pengaturan ini, Anda siap mengimplementasikan fungsionalitas redaksi dokumen.

## Panduan Implementasi

### Fitur 1: memuat dokumen dari stream
**Overview:** Pelajari cara memuat dokumen ke dalam `InputStream` untuk diproses.

`InputStream` adalah kelas I/O Java yang mewakili aliran byte, memungkinkan Anda membaca data dari file, koneksi jaringan, atau sumber lain tanpa memuat seluruh konten ke memori.

#### Langkah 1.1: buat inputstream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Why:** Menggunakan `InputStream` memungkinkan Anda menangani dokumen yang disimpan di berbagai lokasi—bucket cloud, basis data, atau buffer dalam memori—tanpa harus menulisnya ke disk terlebih dahulu. Pendekatan ini penting ketika Anda perlu **load document from stream** dalam arsitektur mikro‑service.

### Fitur 2: terapkan penghapusan anotasi redaksi
**Overview:** Hapus anotasi dari dokumen Anda menggunakan `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` adalah operasi redaksi yang menghapus semua anotasi—seperti komentar, sorotan, dan catatan—dari dokumen.

#### Langkah 2.1: terapkan deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Why:** Langkah ini memastikan bahwa semua anotasi sensitif (komentar, sorotan, atau catatan tersembunyi) dihapus dari dokumen, meningkatkan privasi dan kepatuhan.

### Fitur 3: simpan dokumen dengan opsi
**Overview:** Pelajari cara menyimpan dokumen yang telah diproses dengan opsi spesifik seperti rasterisasi dan **add suffix filename java**.

`SaveOptions` mengenkapsulasi pengaturan yang mengontrol cara dokumen yang direduksi ditulis, termasuk format, rasterisasi, dan konvensi penamaan.

#### Langkah 3.1: konfigurasikan saveoptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Why:** Menyesuaikan opsi penyimpanan memungkinkan format output dan konvensi penamaan yang fleksibel. Mengaktifkan `setAddSuffix(true)` **adds suffix to filename**, sehingga jelas bahwa file tersebut telah direduksi.

## Cara menambahkan akhiran nama file java saat menyimpan dokumen?

Kelas `Redactor` adalah komponen inti yang memuat dokumen dan menerapkan operasi redaksi. `SaveOptions` menentukan cara dokumen yang direduksi disimpan, termasuk format, rasterisasi, dan konvensi penamaan. Buat instance `Redactor`, terapkan redaksi yang diperlukan, lalu konfigurasikan objek `SaveOptions` dengan `setAddSuffix(true)`. Panggil `redactor.save(outputPath, options)`. SDK secara otomatis menambahkan “_redacted” (atau akhiran yang dikonfigurasi) ke nama file, sehingga Anda tidak pernah perlu mengganti nama file secara manual.

## Ikhtisar dependensi Maven GroupDocs

**groupdocs maven dependency** membawa seluruh Redaction SDK ke dalam proyek Anda dengan satu entri `<dependency>`. Ia menangani dependensi transitif, menjaga perpustakaan tetap terbaru, dan menyederhanakan otomasi build. Dengan mendeklarasikan dependensi di `pom.xml`, Anda menghindari manajemen JAR manual dan memastikan kompatibilitas dengan patch keamanan terbaru.

## Mengapa menambahkan akhiran penting

Menambahkan akhiran memberikan konfirmasi visual langsung bahwa file telah diproses, yang penting untuk jejak audit, alur kerja otomatis, dan kepatuhan regulasi. Ini memungkinkan skrip menyaring file yang direduksi, mencegah distribusi tidak sengaja konten asli, dan memenuhi banyak standar industri yang mengharuskan pelabelan jelas pada dokumen yang telah disanitasi.

## Aplikasi praktis

Jelajahi kasus penggunaan dunia nyata berikut:

1. **Legal document redaction:** Amankan kontrak sebelum dibagikan ke klien.  
2. **Medical record handling:** Lindungi identifier pasien sambil mempertahankan data klinis.  
3. **Financial reporting:** Jaga kerahasiaan angka sensitif selama audit eksternal.  
4. **CRM integration:** Otomatis redaksi data pelanggan sebelum diekspor ke alat pihak ketiga.  
5. **Collaboration tools:** Pastikan draf yang dibagikan tidak pernah mengekspos komentar tersembunyi atau metadata.

## Pertimbangan kinerja

### Mengoptimalkan kinerja
- Gunakan streaming (`load document from stream`) untuk menghindari memuat seluruh file ke memori.  
- Tutup instance `Redactor` segera untuk membebaskan sumber daya.  

### Pedoman penggunaan sumber daya
- Pantau CPU dan memori selama batch run.  
- Pilih `ByteArrayOutputStream` untuk penyimpanan dalam memori ketika bekerja dengan ukuran file yang sedang.

### Praktik terbaik untuk manajemen memori Java
- Gunakan kembali objek `Redactor` saat memproses banyak file dengan tipe yang sama.  
- Panggil `close()` dalam blok `try‑with‑resources` untuk mencegah kebocoran.

## Masalah umum dan solusi

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Suffix tidak muncul** | `setAddSuffix(false)` atau pemanggilan yang terlewat | Pastikan `options.setAddSuffix(true)` diatur sebelum `save()`. |
| **OutOfMemoryError pada DOCX besar** | Memuat seluruh file ke memori | Beralih ke pemuatan `InputStream` (lihat Fitur 1). |
| **Annotations masih terlihat** | Redaksi tidak diterapkan sebelum penyimpanan | Panggil `redactor.apply(new DeleteAnnotationRedaction())` sebelum `save()`. |
| **Rasterisasi PDF tidak diterapkan** | `setRasterizeToPDF(false)` atau terlewat | Atur `options.setRasterizeToPDF(true)` ketika Anda memerlukan PDF yang diratakan. |

## Pertanyaan yang sering diajukan

**Q: Bisakah saya meredaksi dokumen PDF menggunakan GroupDocs.Redaction?**  
A: Ya, perpustakaan mendukung PDF, DOCX, PPTX, XLSX, dan banyak format lainnya.

**Q: Apa cara terbaik menangani file besar dengan GroupDocs.Redaction?**  
A: Gunakan streaming (`load document from stream`) dan tutup sumber daya segera untuk menjaga penggunaan memori tetap rendah.

**Q: Apakah memungkinkan menyesuaikan teks akhiran?**  
A: API secara otomatis menambahkan akhiran default (misalnya “_redacted”). Untuk akhiran khusus, ganti nama file output setelah penyimpanan.

**Q: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Redaction?**  
A: Kunjungi [Temporary License page](https://purchase.groupdocs.com/temporary-license/) dan ikuti instruksinya.

**Q: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
A: Bergabunglah dengan [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk bantuan ahli.

## Sumber daya
- **Documentation:** Jelajahi panduan detail di [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API reference:** Akses detail API lengkap pada [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Dapatkan versi terbaru dari [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repository:** Kontribusi atau jelajahi kode sumber di [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## Tutorial terkait

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)