---
date: '2026-02-16'
description: Pelajari cara menggunakan dependensi GroupDocs Maven untuk menambahkan
  akhiran pada nama file saat menyensor dokumen di Java. Termasuk memuat dari aliran,
  menghapus anotasi, dan opsi penyimpanan.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: dependensi maven groupdocs – Tambahkan akhiran pada nama file di Java
type: docs
url: /id/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cara Menambahkan Akhiran ke Nama File Saat Menyunting Dokumen di Java dengan GroupDocs.Redaction

Menyunting data rahasia hanyalah setengah dari perjuangan—Anda juga harus memastikan file yang disimpan jelas menunjukkan bahwa file tersebut telah diproses. **Menggunakan dependensi maven groupdocs membuat ini sederhana**, memungkinkan Anda menambahkan akhiran ke nama file output hanya dalam beberapa baris kode. Dalam panduan ini Anda akan belajar cara menambahkan akhiran ke nama file saat menyimpan dokumen yang telah disunting, bersama dengan memuat, memberi anotasi, dan menyimpan menggunakan GroupDocs.Redaction untuk Java. Baik Anda melindungi kontrak hukum, rekam medis, atau laporan keuangan, langkah‑langkah ini akan menjaga alur kerja Anda tetap aman dan dapat diaudit.

## Jawaban Cepat
- **Apa yang dilakukan “add suffix to filename”?**  
  Ia menambahkan akhiran khusus (misalnya “_redacted”) ke nama file output sehingga Anda dapat langsung mengidentifikasi file yang telah diproses.  
- **Apakah saya dapat memuat dokumen dari stream?**  
  Ya—GroupDocs.Redaction mendukung pemuatan dari `InputStream` apa pun, cocok untuk penyimpanan cloud atau pemrosesan dalam memori.  
- **Apakah saya memerlukan lisensi untuk fitur ini?**  
  Versi percobaan gratis berfungsi untuk penyuntingan dasar; lisensi sementara atau penuh membuka semua opsi lanjutan, termasuk penanganan akhiran.  
- **Format apa saja yang didukung?**  
  Perpustakaan ini menangani DOCX, PDF, PPTX, XLSX, dan banyak lagi.  
- **Apakah rasterisasi diperlukan untuk output PDF?**  
  Rasterisasi bersifat opsional; aktifkan bila Anda perlu meratakan dokumen untuk keamanan tambahan.

## Apa Itu Menambahkan Akhiran ke Nama File?
Menambahkan akhiran adalah konvensi penamaan sederhana yang menandakan sebuah file telah melalui proses penyuntingan. Ini mencegah berbagi tidak sengaja versi asli yang belum disunting dan membantu pipeline otomatis melacak status pemrosesan.

## Mengapa Menggunakan GroupDocs.Redaction untuk Tugas Ini?
GroupDocs.Redaction menyediakan API Java yang fluently yang memungkinkan Anda menggabungkan tindakan penyuntingan dengan opsi penanganan file—seperti **menambahkan akhiran ke nama file**—hanya dalam beberapa baris kode. Ini menghemat waktu pengembangan dan mengurangi risiko kesalahan manual.

## Prerequisites

- **Java Development Kit (JDK):** Versi 8 atau lebih tinggi.  
- **GroupDocs.Redaction Library:** Perpustakaan inti untuk tugas penyuntingan.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor Java‑compatible apa pun.  
- **Maven:** Untuk manajemen dependensi.  

### Prasyarat Pengetahuan
Familiaritas dengan Java I/O dan konsep berorientasi objek dasar akan memudahkan pemahaman contoh.

## Menyiapkan GroupDocs.Redaction untuk Java
### Maven Setup
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

### Direct Download
Atau, unduh versi terbaru langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
1. **Free Trial:** Akses fungsionalitas dasar tanpa batasan.  
2. **Temporary License:** Dapatkan lisensi sementara untuk menjelajahi fitur lanjutan.  
3. **Purchase:** Untuk penggunaan jangka panjang, pertimbangkan membeli lisensi penuh.

#### Basic Initialization and Setup
Inisialisasi proyek Anda dengan menambahkan impor yang diperlukan:

```java
import com.groupdocs.redaction.Redactor;
```

Dengan pengaturan ini, Anda siap mengimplementasikan fungsionalitas penyuntingan dokumen.

## Implementation Guide

### Feature 1: Load Document from Stream
**Gambaran Umum:** Pelajari cara memuat dokumen ke dalam `InputStream` untuk diproses.

#### Step-by-Step Implementation
##### Step 1.1: Create InputStream

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

- **Mengapa:** Menggunakan `InputStream` memungkinkan Anda menangani dokumen yang disimpan dalam berbagai format secara mulus, yang penting ketika Anda perlu **load document from stream** di skenario cloud atau micro‑service.

### Feature 2: Apply Annotation Deletion Redaction
**Gambaran Umum:** Hapus anotasi dari dokumen Anda menggunakan `DeleteAnnotationRedaction`.

#### Step-by-Step Implementation
##### Step 2.1: Apply DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Mengapa:** Langkah ini memastikan semua anotasi sensitif dihapus, meningkatkan privasi dokumen.

### Feature 3: Save Document with Options
**Gambaran Umum:** Pelajari cara menyimpan dokumen yang telah diproses dengan opsi spesifik seperti rasterisasi dan **menambahkan akhiran ke nama file**.

#### Step-by-Step Implementation
##### Step 3.1: Configure SaveOptions

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

- **Mengapa:** Menyesuaikan opsi penyimpanan memungkinkan format output fleksibel dan konvensi penamaan. Mengaktifkan `setAddSuffix(true)` **adds suffix to filename**, menjadikannya jelas bahwa file telah disunting.

## Ikhtisar dependensi maven groupdocs
Dependensi **groupdocs maven** membawa seluruh Redaction SDK ke dalam proyek Anda dengan satu entri `<dependency>`. Ia menangani dependensi transitif, menjaga perpustakaan tetap terbaru, dan menyederhanakan otomatisasi build. Dengan mendeklarasikan dependensi di `pom.xml`, Anda menghindari manajemen JAR manual dan memastikan kompatibilitas dengan patch keamanan terbaru.

## Mengapa Menambahkan Akhiran Penting
- **Auditability:** Tim dapat langsung melihat file mana yang aman untuk didistribusikan.  
- **Automation:** Skrip dapat menyaring file berdasarkan akhiran, mencegah pemrosesan tidak sengaja dokumen asli.  
- **Compliance:** Banyak regulasi mengharuskan pelabelan jelas pada dokumen yang telah disanitasi.  

## Aplikasi Praktis
Jelajahi kasus penggunaan dunia nyata berikut:
1. **Legal Document Redaction:** Amankan kontrak sebelum dibagikan ke klien.  
2. **Medical Record Handling:** Lindungi pengidentifikasi pasien.  
3. **Financial Reporting:** Jaga kerahasiaan angka sensitif.  
4. **CRM Integration:** Secara otomatis menyunting data pelanggan sebelum diekspor.  
5. **Collaboration Tools:** Pastikan draf yang dibagikan tidak pernah menampilkan komentar tersembunyi.

## Pertimbangan Kinerja
### Optimizing Performance
- Gunakan streaming (`load document from stream`) untuk menghindari memuat seluruh file ke memori.  
- Tutup instansi `Redactor` dengan cepat untuk membebaskan sumber daya.

### Resource Usage Guidelines
- Pantau CPU dan memori selama batch run.  
- Pilih `ByteArrayOutputStream` untuk penyimpanan dalam memori saat bekerja dengan ukuran file yang sedang.

### Best Practices for Java Memory Management
- Gunakan kembali objek `Redactor` saat memproses banyak file dengan tipe yang sama.  
- Panggil `close()` dalam blok `try‑with‑resources` untuk mencegah kebocoran.

## Common Issues and Solutions
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Suffix tidak muncul** | `setAddSuffix(false)` atau pemanggilan yang hilang | Pastikan `options.setAddSuffix(true)` diatur sebelum `save()`. |
| **OutOfMemoryError pada DOCX besar** | Memuat seluruh file ke memori | Beralih ke pemuatan `InputStream` (lihat Fitur 1). |
| **Anotasi masih terlihat** | Penyuntingan tidak diterapkan sebelum penyimpanan | Panggil `redactor.apply(new DeleteAnnotationRedaction())` sebelum `save()`. |
| **Rasterisasi PDF tidak diterapkan** | `setRasterizeToPDF(false)` atau tidak disertakan | Atur `options.setRasterizeToPDF(true)` ketika Anda memerlukan PDF yang diratakan. |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menyunting dokumen PDF menggunakan GroupDocs.Redaction?**  
J: Ya, perpustakaan ini mendukung PDF, DOCX, PPTX, XLSX, dan banyak format lainnya.

**T: Apa cara terbaik menangani file besar dengan GroupDocs.Redaction?**  
J: Gunakan streaming (`load document from stream`) dan tutup sumber daya dengan cepat untuk menjaga penggunaan memori tetap rendah.

**T: Apakah memungkinkan menyesuaikan teks akhiran?**  
J: API secara otomatis menambahkan akhiran default (misalnya “_redacted”). Untuk akhiran khusus, Anda dapat mengganti nama file output setelah disimpan.

**T: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Redaction?**  
J: Kunjungi [Temporary License page](https://purchase.groupdocs.com/temporary-license/) dan ikuti instruksinya.

**T: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
J: Bergabunglah dengan [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk bantuan ahli.

## Sumber Daya
- **Documentation:** Jelajahi panduan detail di [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Akses detail API lengkap pada [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Dapatkan versi terbaru dari [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Kontribusi atau jelajahi kode sumber di [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Terakhir Diperbarui:** 2026-02-16  
**Diuji Dengan:** GroupDocs.Redaction 24.9 for Java  
**Penulis:** GroupDocs  

---