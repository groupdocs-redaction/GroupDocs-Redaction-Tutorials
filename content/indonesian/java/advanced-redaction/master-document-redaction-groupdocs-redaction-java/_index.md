---
date: '2025-12-17'
description: Pelajari cara menambahkan sufiks ke nama file dan menyensor informasi
  sensitif dari dokumen menggunakan GroupDocs.Redaction untuk Java. Tingkatkan keamanan
  dan privasi dokumen secara efektif.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Cara Menambahkan Akhiran pada Nama File Saat Menyensor Dokumen di Java dengan
  GroupDocs.Redaction
type: docs
url: /id/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cara Menambahkan Akhiran ke Nama File Saat Menyunting Dokumen di Java dengan GroupDocs.Redaction

Menyunting data rahasia hanyalah setengah dari perjuangan—Anda juga harus memastikan file yang disimpan jelas menunjukkan bahwa file tersebut telah diproses. Dalam panduan ini Anda akan mempelajari **cara menambahkan akhiran ke nama file** saat menyimpan dokumen yang telah disunting, bersama dengan memuat, memberi anotasi, dan menyimpan menggunakan GroupDocs.Redaction untuk Java. Baik Anda melindungi kontrak hukum, rekam medis, atau laporan keuangan, langkah‑langkah ini akan menjaga alur kerja Anda tetap aman dan dapat diaudit.

## Jawaban Cepat
- **Apa yang dilakukan “add suffix to filename”?**  
  Ini menambahkan akhiran khusus (misalnya “_redacted”) ke nama file output sehingga Anda dapat langsung mengidentifikasi file yang telah diproses.  
- **Apakah saya dapat memuat dokumen dari stream?**  
  Ya—GroupDocs.Redaction mendukung pemuatan dari `InputStream` apa pun, cocok untuk penyimpanan cloud atau pemrosesan dalam memori.  
- **Apakah saya memerlukan lisensi untuk fitur ini?**  
  Versi percobaan gratis berfungsi untuk penyuntingan dasar; lisensi sementara atau penuh membuka semua opsi lanjutan, termasuk penanganan akhiran.  
- **Format apa saja yang didukung?**  
  Perpustakaan ini menangani DOCX, PDF, PPTX, XLSX, dan banyak lagi.  
- **Apakah rasterisasi diperlukan untuk output PDF?**  
  Rasterisasi bersifat opsional; aktifkan bila Anda perlu meratakan dokumen untuk keamanan tambahan.  

## Apa Itu Menambahkan Akhiran ke Nama File?
Menambahkan akhiran adalah konvensi penamaan sederhana yang menandakan bahwa sebuah penyuntingan. Ini mencegah berbagi tidak sengaja versi asli yang belum disunting dan membantu pipeline otomatis melacak status pemrosesan.

## Mengapa Menggunakan GroupDocs.Redaction untuk Tugas Ini?
GroupDocs.Redaction menyediakan API Java yang fluida yang memungkinkan Anda menggabungkan aksi penyuntingan dengan opsi penanganan file—seperti **menambahkan akhiran ke nama file**—hanya dalam beberapa baris kode. Ini menghemat waktu pengembangan dan mengurangi risiko kesalahan manual.

## Prasyarat
- **Java Development Kit (JDK):** Versi 8 atau lebih tinggi.  
- **GroupDocs.Redaction Library:** Perpustakaan inti untuk tugas penyuntingan.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor yang kompatibel dengan Java apa pun.  
- **Maven:** Untuk manajemen dependensi.  

### Prasyarat Pengetahuan
Keterbiasaan dengan Java I/O dan konsep dasar pemrograman berorientasi objek akan memudahkan pemahaman contoh.

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
Atau, unduh versi terbaru secara langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
1. **Free Trial:** Akses fungsionalitas dasar tanpa batasan.  
2. **Temporary License:** Dapatkan lisensi sementara untuk menjelajahi fitur lanjutan.  
3. **Purchase:** Untuk penggunaan jangka panjang, pertimbangkan membeli lisensi penuh.  

#### Inisialisasi dan Pengaturan Dasar
Inisialisasi proyek Anda dengan menambahkan impor yang diperlukan:

```java
import com.groupdocs.redaction.Redactor;
```

Dengan pengaturan ini, Anda siap mengimplementasikan fungsionalitas penyuntingan dokumen.

## Panduan Implementasi

### Fitur 1: Memuat Dokumen dari Stream
**Gambaran:** Pelajari cara memuat dokumen ke dalam `InputStream` untuk diproses.

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

- **Mengapa:** Menggunakan `InputStream` memungkinkan Anda menangani dokumen yang disimpan dalam berbagai format secara mulus, yang penting ketika Anda perlu **load document from stream** di skenario cloud atau micro‑service.

### Fitur 2: Terapkan Penyuntingan Penghapusan Anotasi
**Gambaran:** Hapus anotasi dari dokumen Anda menggunakan `DeleteAnnotationRedaction`.

#### Implementasi Langkah demi Langkah
##### Langkah 2.1: Terapkan DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Mengapa:** Langkah ini memastikan semua anotasi sensitif dihapus, meningkatkan privasi dokumen.

### Fitur 3: Simpan Dokumen dengan Opsi
**Gambaran:** Pelajari cara menyimpan dokumen yang telah diproses dengan opsi spesifik seperti rasterisasi dan **menambahkan akhiran ke nama file**.

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

- **Mengapa:** Menyesuaikan opsi penyimpanan memungkinkan format output yang fleksibel dan konvensi penamaan. Mengaktifkan `setAddSuffix(true)` **menambahkan akhiran ke nama file**, sehingga jelas bahwa file tersebut telah disunting.

## Mengapa Menambahkan Akhiran Penting
- **Auditabilitas:** Tim dapat melihat file mana yang aman untuk didistribusikan.  
- **Otomasi:** Skrip dapat menyaring file berdasarkan akhiran, mencegah pemrosesan tidak sengaja dokumen asli.  
- **Kepatuhan:** Banyak regulasi mengharuskan pelabelan yang jelas pada dokumen yang telah disanitasi.

## Aplikasi Praktis
Jelajahi contoh penggunaan dunia nyata berikut:
1. **Legal Document Redaction:** Amankan kontrak sebelum dibagikan ke klien.  
2. **Medical Record Handling:** Lindungi pengidentifikasi pasien.  
3. **Financial Reporting:** Jaga kerahasiaan angka sensitif.  
4. **CRM Integration:** Secara otomatis menghapus data pelanggan sebelum diekspor.  
5. **Collaboration Tools:** Pastikan draf yang dibagikan tidak pernah menampilkan komentar tersembunyi.

## Pertimbangan Kinerja
### Mengoptimalkan Kinerja
- Gunakan streaming (`load document from stream`) untuk menghindari memuat seluruh file ke memori.  
- Tutup instance `Redactor` dengan cepat untuk membebaskan sumber daya.

### Pedoman Penggunaan Sumber Daya
- Pantau CPU dan memori selama menjalankan batch.  
- Pilih `ByteArrayOutputStream` untuk penyimpanan dalam memori saat bekerja dengan ukuran file yang sedang.

### Praktik Terbaik untuk Manajemen Memori Java
- Gunakan kembali objek `Redactor` saat memproses banyak file dengan tipe yang sama.  
- Panggil `close()` dalam blok `finally` atau try‑with‑resources untuk mencegah kebocoran.

## Masalah Umum dan Solusinya
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Akhiran tidak muncul** | `setAddSuffix(false)` atau panggilan yang hilang | Pastikan `options.setAddSuffix(true)` diatur sebelum `save()`. |
| **OutOfMemoryError pada DOCX besar** | Memuat seluruh file ke memori | Beralih ke pemuatan dengan `InputStream` (lihat Fitur 1). |
| **Anotasi masih terlihat** | Penyuntingan tidak diterapkan sebelum penyimpanan | Panggil `redactor.apply(new DeleteAnnotationRedaction())` sebelum `save()`. |
| **Rasterisasi PDF tidak diterapkan** | `setRasterizeToPDF(false)` atau tidak disertakan | Atur `options.setRasterizeToPDF(true)` ketika Anda memerlukan PDF yang diratakan. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menyunting dokumen PDF menggunakan GroupDocs.Redaction?**  
A: Ya, perpustakaan ini mendukung PDF, DOCX, PPTX, XLSX, dan banyak format lainnya.

**Q: Apa cara terbaik menangani file besar dengan GroupDocs.Redaction?**  
A: Gunakan streaming (`load document from stream`) dan tutup sumber daya dengan cepat untuk menjaga penggunaan memori tetap rendah.

**Q: Apakah memungkinkan untuk menyesuaikan teks akhiran?**  
A: API secara otomatis menambahkan akhiran default (misalnya “_redacted”). Untuk akhiran khusus, Anda dapat mengganti nama file output setelah disimpan.

**Q: Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Redaction?**  
A: Kunjungi [halaman Lisensi Sementara](https://purchase.groupdocs.com/temporary-license/) dan ikuti petunjuknya.

**Q: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
A: Bergabunglah dengan [Forum Dukungan GroupDocs](https://forum.groupdocs.com/c/redaction/33) untuk bantuan ahli.

## Sumber Daya
- **Documentation:** Jelajahi panduan terperinci di [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Akses detail API lengkap pada [Group API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Dapatkan versi terbaru dari [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Berkontribusi atau jelajahi kode sumber di [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Terakhir Diperbarui:** 2025-12-17  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs