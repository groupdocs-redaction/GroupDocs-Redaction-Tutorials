---
date: '2026-08-31'
description: Pelajari cara menghapus data sensitif dalam dokumen Java menggunakan
  GroupDocs.Redaction. Panduan langkah demi langkah mencakup kebijakan, pemrosesan
  batch, dan mempertahankan format asli.
keywords:
- redact sensitive data
- process multiple files
- secure document processing
- save redacted document
lastmod: '2026-08-31'
og_description: Pelajari cara menghapus data sensitif dalam dokumen Java menggunakan
  GroupDocs.Redaction. Panduan ini menjelaskan kebijakan, pemrosesan batch, dan mempertahankan
  format.
og_image_alt: Guide showing how to redact sensitive data in Java using GroupDocs.Redaction
og_title: Hapus data sensitif di Java dengan GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-31'
  description: Learn how to redact sensitive data in Java documents using GroupDocs.Redaction.
    Step‑by‑step guide covers policies, batch processing, and preserving original
    formatting.
  headline: Redact sensitive data in Java with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact sensitive data in Java documents using GroupDocs.Redaction.
    Step‑by‑step guide covers policies, batch processing, and preserving original
    formatting.
  name: Redact sensitive data in Java with GroupDocs.Redaction
  steps:
  - name: '**Legal document processing** – redact client identifiers before sharing
      drafts.'
    text: '**Legal document processing** – redact client identifiers before sharing
      drafts.'
  - name: '**Healthcare data management** – remove patient details to stay HIPAA‑compliant.'
    text: '**Healthcare data management** – remove patient details to stay HIPAA‑compliant.'
  - name: '**Financial reporting** – hide account numbers when distributing reports.'
    text: '**Financial reporting** – hide account numbers when distributing reports.'
  - name: '**Contract review** – protect proprietary clauses during negotiations.'
    text: '**Contract review** – protect proprietary clauses during negotiations.'
  - name: '**Email archiving** – ensure privacy compliance when storing corporate
      email archives.'
    text: '**Email archiving** – ensure privacy compliance when storing corporate
      email archives.'
  type: HowTo
- questions:
  - answer: It means handling, redacting, and storing files so that confidential data
      is protected throughout the entire workflow.
    question: What does secure document processing mean?
  - answer: Yes—by iterating over a folder you can apply the same redaction policy
      to every document automatically.
    question: Can I process multiple files in one run?
  - answer: Create a redaction policy that defines the patterns or objects to hide,
      then run the `Redactor` with that policy.
    question: How do I redact sensitive data?
  - answer: A valid GroupDocs.Redaction license is required for production; a trial
      license is available for evaluation.
    question: Do I need a license for production?
  - answer: Set `RasterizationOptions.setEnabled(false)` to keep the original file
      format unchanged.
    question: Can I save the redacted document without rasterization?
  type: FAQPage
tags:
- redact sensitive data
- GroupDocs.Redaction
- Java document processing
- batch redaction
title: Hapus data sensitif di Java dengan GroupDocs.Redaction
type: docs
url: /id/java/advanced-redaction/java-redaction-groupdocs-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menghapus data sensitif di Java dengan GroupDocs.Redaction

**GroupDocs.Redaction** adalah pustaka Java yang secara programatis menghapus informasi rahasia dari lebih dari 70 format dokumen sambil mempertahankan tata letak asli. Dalam tutorial ini Anda akan belajar cara **menghapus data sensitif** dalam aplikasi Java, menerapkan kebijakan redaksi pada sekumpulan file, dan menyimpan hasilnya tanpa kehilangan format.

## Jawaban cepat
- **Apa arti pemrosesan dokumen yang aman?** Artinya menangani, meredaksi, dan menyimpan file sehingga data rahasia terlindungi sepanjang alur kerja.  
- **Bisakah saya memproses banyak file dalam satu kali jalankan?** Ya—dengan mengiterasi folder Anda dapat menerapkan kebijakan redaksi yang sama ke setiap dokumen secara otomatis.  
- **Bagaimana cara saya menghapus data sensitif?** Buat kebijakan redaksi yang mendefinisikan pola atau objek yang akan disembunyikan, lalu jalankan `Redactor` dengan kebijakan tersebut.  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk produksi; lisensi percobaan tersedia untuk evaluasi.  
- **Bisakah saya menyimpan dokumen yang di‑redact tanpa rasterisasi?** Setel `RasterizationOptions.setEnabled(false)` untuk menjaga format file asli tetap tidak berubah.

## Cara menghapus data sensitif dalam dokumen Java dengan GroupDocs.Redaction?

Muat kebijakan redaksi Anda, jalankan pada setiap file dalam sebuah direktori, dan simpan outputnya—semua dalam beberapa langkah singkat. API GroupDocs.Redaction memungkinkan Anda memproses dokumen secara batch, mempertahankan tata letak sambil secara aman menghapus data yang Anda tentukan, dan menyediakan opsi untuk mengontrol rasterisasi, format output, serta karakteristik kinerja.

### Mengapa menggunakan GroupDocs.Redaction untuk Java?

GroupDocs.Redaction mendukung **lebih dari 70 format input dan output** (PDF, DOCX, PPTX, gambar, dll.) dan memungkinkan Anda mendefinisikan kebijakan detail yang menargetkan teks, gambar, atau metadata tertentu. Pustaka ini memproses batch secara efisien, dan Anda dapat mengaktifkan atau menonaktifkan rasterisasi untuk mempertahankan format asli atau mengonversi halaman menjadi gambar demi keamanan tambahan.

### Prasyarat
- **Java Development Kit (JDK) 8 atau lebih tinggi** terpasang.  
- **Maven** atau alat build lain untuk mengelola dependensi.  
- Pengetahuan dasar Java dan familiaritas dengan file I/O.  

### Menyiapkan GroupDocs.Redaction untuk Java

#### Pengaturan Maven
Tambahkan dependensi berikut ke `pom.xml` Anda:

Dependensi Maven berikut menambahkan GroupDocs.Redaction ke proyek Anda.
```xml
<!-- Maven dependency placeholder -->
```
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

#### Unduhan langsung
Sebagai alternatif, unduh JAR terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Perolehan lisensi

Lisensi percobaan dapat digunakan untuk pengembangan, tetapi penyebaran produksi memerlukan file lisensi permanen yang ditempatkan di folder resources aplikasi Anda dan direferensikan pada saat runtime.

### Inisialisasi dan pengaturan dasar

Impor kelas yang diperlukan dan buat instance `Redactor`. **Redactor** adalah kelas utama yang melakukan operasi redaksi pada dokumen.

```java
// Initialization code placeholder
```
```java
import com.groupdocs.redaction.*;
```

## Panduan implementasi

### Apa itu kebijakan redaksi?

Kebijakan redaksi adalah sekumpulan aturan yang dapat digunakan kembali yang memberi tahu Redactor pola teks, gambar, atau metadata mana yang harus disembunyikan atau dihapus. Anda mendefinisikannya sekali dan menerapkannya ke sejumlah dokumen, memungkinkan kepatuhan konsisten di semua file yang diproses.

```java
RedactionPolicy policy = RedactionPolicy.load("YOUR_POLICY_FILE_PATH");
```

### Muat dan terapkan kebijakan redaksi

**Muat kebijakan** dari file XML atau JSON dan **terapkan** ke setiap dokumen dalam folder:

```java
// Load and apply policy code placeholder
```
```java
for (final File fileEntry : new File("YOUR_DOCUMENT_DIRECTORY").listFiles()) {
    final Redactor redactor = new Redactor(fileEntry.getPath());
    try {
        // Apply the loaded redaction policy
        RedactorChangeLog result = redactor.apply(policy);
        
        // Determine output directory based on processing status
        File resultFolder = new File(result.getStatus() != RedactionStatus.Failed ? "YOUR_OUTPUT_DIRECTORY_DONE" : "YOUR_OUTPUT_DIRECTORY_FAILED");
        
        // Save the processed file
        try (FileOutputStream fileStream = new FileOutputStream(resultFolder.getPath() + "/" + fileEntry.getName())) {
            RasterizationOptions options = new RasterizationOptions();
            options.setEnabled(false);
            redactor.save(fileStream, options);
        }
    } finally {
        redactor.close(); // Ensure resources are released
    }
}
```

### Proses banyak file dalam batch

Iterasi melalui sebuah direktori, buka setiap file dengan `Redactor`, dan terapkan kebijakan yang sama:

```java
// Batch processing code placeholder
```
```java
File inputFile = new File("YOUR_DOCUMENT_DIRECTORY/input.docx");
```

### Simpan dokumen yang diproses dengan opsi rasterisasi

#### Inisialisasi Redactor untuk file input

Buka file target untuk redaksi:

```java
// Open file code placeholder
```
```java
try (Redactor redactor = new Redactor(inputFile.getPath())) {
    try (FileOutputStream fileStream = new FileOutputStream(outputFileDirectory.getPath() + "/processed_output.docx")) {
        RasterizationOptions options = new RasterizationOptions();
        options.setEnabled(false);  // Example option to disable rasterization
        redactor.save(fileStream, options);
    }
}
```

#### Simpan dengan opsi rasterisasi

Konfigurasikan `RasterizationOptions` untuk mempertahankan format asli atau mengonversi halaman menjadi gambar, lalu simpan:

```java
// Save options code placeholder
```

**Opsi utama**  
- `setEnabled(false)` – mempertahankan tipe file asli.  
- `setResolution(150)` – mengatur DPI saat merasterisasi menjadi gambar.  

### Bagaimana cara menyimpan dokumen yang di‑redact tanpa kehilangan format?

Setel flag rasterisasi ke `false` sebelum memanggil `save`. Ini memberi tahu GroupDocs.Redaction untuk menulis output dalam format yang sama dengan sumber, memastikan tabel, font, dan tata letak tetap tidak berubah sambil tetap menerapkan redaksi yang diperlukan.

### Aplikasi praktis

1. **Pemrosesan dokumen hukum** – menghapus identifikasi klien sebelum membagikan draf.  
2. **Manajemen data kesehatan** – menghapus detail pasien untuk tetap mematuhi HIPAA.  
3. **Pelaporan keuangan** – menyembunyikan nomor akun saat mendistribusikan laporan.  
4. **Peninjauan kontrak** – melindungi klausa kepemilikan selama negosiasi.  
5. **Arsip email** – memastikan kepatuhan privasi saat menyimpan arsip email perusahaan.  

### Pertimbangan kinerja

- **Manajemen sumber daya** – selalu tutup `Redactor` untuk membebaskan memori.  
- **Pemrosesan batch** – tangani file dalam grup 10‑20 untuk menyeimbangkan kecepatan dan penggunaan memori.  
- **Kebijakan yang dioptimalkan** – batasi pola hanya pada yang Anda butuhkan; pola yang lebih luas meningkatkan waktu pemrosesan.  

### Jebakan umum & pemecahan masalah

- **Pengecualian lisensi hilang** – pastikan jalur file lisensi benar dan file dapat dibaca.  
- **Tipe file tidak didukung** – periksa daftar format yang didukung; file yang tidak didukung akan memunculkan `UnsupportedFormatException`.  
- **Kesalahan out‑of‑memory pada PDF besar** – tingkatkan heap JVM (`-Xmx2g`) atau bagi PDF menjadi potongan lebih kecil sebelum redaksi.  

## Pertanyaan yang sering diajukan

**Q:** Bagaimana saya dapat memproses banyak file dengan satu perintah?  
**A:** Gunakan loop iterasi direktori yang ditunjukkan dalam contoh “Apply policy to documents”; secara otomatis meredaksi setiap file di folder yang ditentukan.

**Q:** Apa yang sebenarnya dihapus oleh “redact sensitive data”?  
**A:** Kebijakan dapat menargetkan pola teks biasa, gambar, atau metadata, menggantinya dengan kotak hitam atau menghapusnya sepenuhnya berdasarkan konfigurasi Anda.

**Q:** Apakah ada cara untuk meninjau kebijakan redaksi sebelum menerapkannya?  
**A:** Ya—panggil `redactor.preview(policy)` (jika didukung) untuk menghasilkan PDF pratinjau yang menunjukkan secara tepat apa yang akan disembunyikan.

**Q:** Bagaimana cara menyimpan dokumen yang di‑redact tanpa kehilangan format asli?  
**A:** Setel `RasterizationOptions.setEnabled(false)` seperti yang ditunjukkan; ini menjaga file dalam format aslinya sambil tetap menerapkan redaksi.

**Q:** Apakah saya memerlukan lisensi untuk pengujian pengembangan?  
**A:** Lisensi sementara atau percobaan sudah cukup untuk pengembangan; lisensi penuh diperlukan untuk penyebaran produksi.

## Sumber daya

- [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) – unduh file JAR terbaru.  
- [GroupDocs.Redaction Java Docs](https://docs.groupdocs.com/redaction/java/) – dokumentasi resmi dan contoh penggunaan.  
- [API Reference](https://reference.groupdocs.com/redaction/java) – referensi kelas dan metode yang detail.  
- [Latest Releases](https://releases.groupdocs.com/redaction/java/) – lihat riwayat versi dan catatan perubahan.  
- [Source Code on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) – jelajahi repositori open‑source.  
- [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33) – dukungan komunitas dan diskusi.  

## Kesimpulan

Dengan mengikuti panduan ini Anda dapat secara aman **menghapus data sensitif** dari dokumen Java secara skala, menggunakan mesin kebijakan kuat dan kemampuan pemrosesan batch GroupDocs.Redaction. Sesuaikan kebijakan untuk memenuhi persyaratan kepatuhan Anda, atur pengaturan rasterisasi untuk kinerja, dan integrasikan alur kerja ke layanan backend berbasis Java apa pun.

---

**Terakhir Diperbarui:** 2026-08-31  
**Diuji Dengan:** GroupDocs.Redaction 24.9 for Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Menghapus Dokumen dengan Lisensi GroupDocs Redaction Java dari Path File – Panduan Langkah‑per‑Langkah](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)
- [Mask Data Sensitif Java – Panduan GroupDocs.Redaction](/redaction/java/getting-started/)
- [Cara Menghapus Teks dalam Dokumen Java dengan GroupDocs.Redaction](/redaction/java/text-redaction/java-redaction-guide-groupdocs-document-security/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}