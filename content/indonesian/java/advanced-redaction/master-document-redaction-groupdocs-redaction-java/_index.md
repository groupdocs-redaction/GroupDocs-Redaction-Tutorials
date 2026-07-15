---
date: '2026-05-22'
description: Pelajari cara menambahkan akhiran nama file java menggunakan dependensi
  GroupDocs Maven saat menyunting dokumen. Includes streaming load, annotation deletion,
  and save options.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
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
title: Tambahkan akhiran nama file java dengan GroupDocs Maven
type: docs
url: /id/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Tambahkan akhiran nama file java dengan GroupDocs Maven

Menyensor data rahasia hanyalah separuh dari perjuangan—Anda juga harus memastikan file yang disimpan jelas menunjukkan bahwa file tersebut telah diproses. **Menggunakan dependensi GroupDocs Maven membuat ini menjadi sederhana**, memungkinkan Anda menambahkan akhiran pada nama file output hanya dengan beberapa baris kode. Metode untuk **add suffix filename java** adalah konfigurasi satu baris yang langsung memberi label pada file yang disensor, membantu Anda tetap patuh dan siap audit.

## Jawaban Cepat
- **Apa yang dilakukan “add suffix to filename”?**  
  Ini menambahkan akhiran khusus (misalnya “_redacted”) ke nama file output sehingga Anda dapat langsung mengidentifikasi file yang telah diproses.  
- **Bisakah saya memuat dokumen dari stream?**  
  Ya—GroupDocs.Redaction mendukung pemuatan dari `InputStream` apa pun, cocok untuk penyimpanan cloud atau pemrosesan dalam memori.  
- **Apakah saya memerlukan lisensi untuk fitur ini?**  
  Uji coba gratis berfungsi untuk penyensoran dasar; lisensi sementara atau penuh membuka semua opsi lanjutan, termasuk penanganan akhiran.  
- **Format apa saja yang didukung?**  
  Pustaka ini menangani DOCX, PDF, PPTX, XLSX, dan banyak lagi.  
- **Apakah rasterisasi diperlukan untuk output PDF?**  
  Rasterisasi bersifat opsional; aktifkan bila Anda perlu meratakan dokumen untuk keamanan tambahan.

## Apa itu add suffix filename java?
Teknik **add suffix filename java** menambahkan string yang telah ditentukan ke nama file selama operasi penyimpanan, secara jelas menandai dokumen sebagai tersensor. Konvensi sederhana ini mencegah distribusi tidak sengaja dari file asli yang belum tersensor dan terintegrasi dengan mulus ke dalam pipeline otomatis.

## Mengapa menggunakan GroupDocs.Redaction untuk tugas ini?
GroupDocs.Redaction menyediakan API Java yang lancar yang memungkinkan Anda menggabungkan aksi penyensoran dengan opsi penanganan file—seperti **add suffix filename java**—hanya dengan beberapa baris kode. SDK mendukung **lebih dari 50 format input dan output** dan dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori, memberikan kecepatan dan jejak memori yang rendah.

## Prasyarat
- **Java Development Kit (JDK):** Versi 8 atau lebih tinggi.  
- **GroupDocs.Redaction Library:** Pustaka inti untuk tugas penyensoran.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor Java yang kompatibel.  
- **Maven:** Untuk manajemen dependensi.  

### Prasyarat Pengetahuan
Keterbiasaan dengan Java I/O dan konsep berorientasi objek dasar akan mempermudah pemahaman contoh.

## Menyiapkan GroupDocs.Redaction untuk Java
### Pengaturan Maven
Sertakan konfigurasi berikut dalam file `pom.xml` Anda untuk mengakses pustaka GroupDocs melalui Maven:

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

### Unduhan Langsung
Atau, unduh versi terbaru langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Perolehan Lisensi
1. **Free Trial:** Akses fungsionalitas dasar tanpa batasan.  
2. **Temporary License:** Dapatkan lisensi sementara untuk menjelajahi fitur lanjutan.  
3. **Purchase:** Untuk penggunaan jangka panjang, pertimbangkan membeli lisensi penuh.  

#### Inisialisasi dan Penyiapan Dasar
Inisialisasikan proyek Anda dengan menambahkan impor yang diperlukan:

```java
import com.groupdocs.redaction.Redactor;
```

Dengan penyiapan ini, Anda siap mengimplementasikan fungsionalitas penyensoran dokumen.

## Panduan Implementasi

### Fitur 1: Memuat Dokumen dari Stream
**Overview:** Pelajari cara memuat dokumen ke dalam `InputStream` untuk diproses.

#### Implementasi Langkah demi Langkah
##### Langkah 1.1: Buat InputStream

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

### Fitur 2: Terapkan Penyensoran Penghapusan Anotasi
**Overview:** Hapus anotasi dari dokumen Anda menggunakan `DeleteAnnotationRedaction`.

#### Implementasi Langkah demi Langkah
##### Langkah 2.1: Terapkan DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Why:** Langkah ini memastikan bahwa semua anotasi sensitif (komentar, sorotan, atau catatan tersembunyi) dihapus dari dokumen, meningkatkan privasi dan kepatuhan.

### Fitur 3: Simpan Dokumen dengan Opsi
**Overview:** Pelajari cara menyimpan dokumen yang diproses dengan opsi spesifik seperti rasterisasi dan **add suffix filename java**.

#### Implementasi Langkah demi Langkah
##### Langkah 3.1: Konfigurasikan SaveOptions

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

- **Why:** Menyesuaikan opsi penyimpanan memungkinkan format output yang fleksibel dan konvensi penamaan. Mengaktifkan `setAddSuffix(true)` **adds suffix to filename**, menjadikannya jelas bahwa file telah disensor.

## Cara menambahkan akhiran nama file java saat menyimpan dokumen?
`Redactor` adalah kelas utama di GroupDocs.Redaction yang memuat dokumen dan menerapkan operasi penyensoran.  
`setAddSuffix` adalah metode dari `SaveOptions` yang mengaktifkan penambahan akhiran otomatis ke nama file output.  

Muat instance `Redactor` Anda, terapkan penyensoran yang diinginkan, lalu panggil `save()` dengan `SaveOptions` di mana `setAddSuffix(true)` diaktifkan. Konfigurasi tunggal ini secara otomatis menambahkan “_redacted” (atau akhiran default) ke nama file, menghilangkan kebutuhan penamaan ulang manual dan mengurangi kesalahan manusia. Operasi selesai dalam waktu O(n) relatif terhadap ukuran dokumen dan bekerja untuk semua format yang didukung.

## Gambaran Umum dependensi Maven groupdocs
**groupdocs maven dependency** membawa seluruh Redaction SDK ke dalam proyek Anda dengan satu entri `<dependency>`. Ini menangani dependensi transitif, menjaga pustaka tetap terbaru, dan menyederhanakan otomatisasi build. Dengan mendeklarasikan dependensi di `pom.xml`, Anda menghindari manajemen JAR manual dan memastikan kompatibilitas dengan patch keamanan terbaru.

## Mengapa Menambahkan Akhiran Penting
Menambahkan akhiran memberikan konfirmasi visual langsung bahwa dokumen telah diproses, yang penting untuk jejak audit, alur kerja otomatis, dan kepatuhan regulasi di berbagai industri.

- **Auditability:** Tim dapat langsung melihat file mana yang aman untuk didistribusikan.  
- **Automation:** Skrip dapat menyaring file berdasarkan akhiran, mencegah pemrosesan tidak sengaja dari dokumen asli.  
- **Compliance:** Banyak regulasi mengharuskan pelabelan yang jelas pada dokumen yang telah disanitasi.  

## Aplikasi Praktis
Jelajahi kasus penggunaan dunia nyata berikut:

1. **Legal Document Redaction:** Amankan kontrak sebelum dibagikan ke klien.  
2. **Medical Record Handling:** Lindungi pengidentifikasi pasien sambil mempertahankan data klinis.  
3. **Financial Reporting:** Jaga angka sensitif tetap rahasia selama audit eksternal.  
4. **CRM Integration:** Secara otomatis menyensor data pelanggan sebelum diekspor ke alat pihak ketiga.  
5. **Collaboration Tools:** Pastikan draf yang dibagikan tidak pernah menampilkan komentar tersembunyi atau metadata.  

## Pertimbangan Kinerja
### Mengoptimalkan Kinerja
- Gunakan streaming (`load document from stream`) untuk menghindari memuat seluruh file ke memori.  
- Tutup instance `Redactor` dengan cepat untuk membebaskan sumber daya.  

### Panduan Penggunaan Sumber Daya
- Pantau CPU dan memori selama proses batch.  
- Pilih `ByteArrayOutputStream` untuk penyimpanan dalam memori saat bekerja dengan ukuran file yang sedang.  

### Praktik Terbaik untuk Manajemen Memori Java
- Gunakan kembali objek `Redactor` saat memproses beberapa file dengan tipe yang sama.  
- Panggil `close()` dalam blok `try‑with‑resources` untuk mencegah kebocoran.  

## Masalah Umum dan Solusinya
| Masalah | Penyebab | Solusi |
|---------|----------|--------|
| **Akhiran tidak muncul** | `setAddSuffix(false)` atau panggilan yang hilang | Pastikan `options.setAddSuffix(true)` diatur sebelum `save()`. |
| **OutOfMemoryError pada DOCX besar** | Memuat seluruh file ke memori | Beralih ke pemuatan `InputStream` (lihat Fitur 1). |
| **Anotasi masih terlihat** | Penyensoran tidak diterapkan sebelum penyimpanan | Panggil `redactor.apply(new DeleteAnnotationRedaction())` sebelum `save()`. |
| **Rasterisasi PDF tidak diterapkan** | `setRasterizeToPDF(false)` atau diabaikan | Atur `options.setRasterizeToPDF(true)` ketika Anda membutuhkan PDF yang diratakan. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menyensor dokumen PDF menggunakan GroupDocs.Redaction?**  
A: Ya, pustaka ini mendukung PDF, DOCX, PPTX, XLSX, dan banyak format lainnya.

**Q: Apa cara terbaik menangani file besar dengan GroupDocs.Redaction?**  
A: Gunakan streaming (`load document from stream`) dan tutup sumber daya dengan cepat untuk menjaga penggunaan memori tetap rendah.

**Q: Apakah memungkinkan menyesuaikan teks akhiran?**  
A: API secara otomatis menambahkan akhiran default (misalnya “_redacted”). Untuk akhiran khusus, ganti nama file output setelah disimpan.

**Q: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Redaction?**  
A: Kunjungi [Temporary License page](https://purchase.groupdocs.com/temporary-license/) dan ikuti petunjuknya.

**Q: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
A: Bergabunglah dengan [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk bantuan ahli.

## Sumber Daya
- **Documentation:** Jelajahi panduan terperinci di [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Akses detail API lengkap di [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Dapatkan versi terbaru dari [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Berkontribusi atau jelajahi kode sumber di [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  

---

**Last Updated:** 2026-05-22  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Tutorial Terkait

- [Konversi Word ke PDF dan Simpan Dokumen Tersensor dengan GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Pratinjau Halaman Dokumen Java Loading dengan GroupDocs.Redaction](/redaction/java/document-loading/)
- [Teknik Penyensoran Lanjutan untuk GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)