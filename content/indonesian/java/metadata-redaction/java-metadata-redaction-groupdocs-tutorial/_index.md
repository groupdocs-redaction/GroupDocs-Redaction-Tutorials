---
date: '2026-01-08'
description: Pelajari cara menggunakan MetadataSearchRedaction dalam Java dengan GroupDocs.Redaction
  untuk menghapus secara aman metadata dokumen yang sensitif.
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: Cara Menggunakan MetadataSearchRedaction di Java dengan GroupDocs
type: docs
url: /id/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Cara Menggunakan MetadataSearchRedaction di Java dengan GroupDocs

Dalam panduan komprehensif ini Anda akan menemukan **cara menggunakan MetadataSearchRedaction** untuk menghapus metadata rahasia—seperti nama perusahaan—dari Word, PDF, dan format dokumen lainnya menggunakan GroupDocs.Redaction untuk Java. Pada akhir tutorial Anda akan dapat mengintegrasikan redaksi metadata ke dalam alur kerja berbasis Java apa pun dan menjaga informasi sensitif tetap aman.

## Quick Answers
- **Apa yang dilakukan MetadataSearchRedaction?** Ia mencari bidang metadata tertentu dan mengganti nilainya dengan teks khusus.  
- **Pustaka apa yang diperlukan?** GroupDocs.Redaction for Java (v24.9 atau lebih baru).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya mempertahankan format file asli?** Ya—gunakan `SaveOptions` untuk mempertahankan format asli.  
- **Apakah pendekatan ini thread‑safe?** Setiap instance `Redactor` bersifat independen, sehingga Anda dapat memproses dokumen secara paralel.

## What is MetadataSearchRedaction?
`MetadataSearchRedaction` adalah kelas redaksi khusus yang memungkinkan Anda menargetkan properti metadata tertentu (misalnya *Company*, *Author*) dan mengganti isinya dengan placeholder. Ini ideal ketika Anda perlu menganonimkan data perusahaan sebelum membagikan dokumen kepada mitra eksternal.

## Why use MetadataSearchRedaction for metadata redaction?
- **Presisi** – Redaksi hanya bidang yang Anda tentukan, meninggalkan sisanya tidak tersentuh.  
- **Kepatuhan** – Membantu memenuhi GDPR, HIPAA, dan regulasi privasi lainnya dengan menghapus pengidentifikasi tersembunyi.  
- **Siap Otomasi** – Terintegrasi mulus ke dalam pipeline pemrosesan batch atau micro‑services.

## Prerequisites
- **GroupDocs.Redaction untuk Java** ≥ 24.9.  
- Java 8 atau lebih baru terpasang di mesin Anda.  
- IDE seperti IntelliJ IDEA atau Eclipse (opsional namun disarankan).  
- Familiaritas dasar dengan Maven (atau kemampuan menambahkan JAR secara manual).  

## Setting Up GroupDocs.Redaction for Java
Tambahkan repositori dan dependensi ke `pom.xml` Anda. Langkah ini memastikan Maven dapat mengunduh pustaka secara otomatis.

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

*Alternatifnya, Anda dapat mengunduh JAR langsung dari halaman rilis resmi:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### License Acquisition
- **Percobaan Gratis** – Unduh lisensi percobaan untuk menjelajahi semua fitur.  
- **Lisensi Sementara** – Digunakan untuk pengujian lanjutan.  
- **Lisensi Penuh** – Diperlukan untuk penerapan produksi.

## Basic Initialization
Buat instance `Redactor` yang menunjuk ke dokumen yang ingin Anda proses.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementation Guide

### Step 1: Import Necessary Classes
Import ini memberi Anda akses ke mesin redaksi, opsi penyimpanan, dan utilitas metadata.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### Step 2: Initialize Redactor
Instansiasi `Redactor` dengan path ke file sumber Anda.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### Step 3: Configure Metadata Search and Redaction
Buat `MetadataSearchRedaction` yang mencari string tepat **"Company Ltd."** dan menggantinya dengan **"--company--"**. Pemanggilan `setFilter` membatasi operasi hanya pada bidang metadata *Company*.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### Step 4: Apply the Redaction
Jalankan redaksi pada dokumen yang telah dibuka.

```java
redactor.apply(redaction);
```

### Step 5: Save with Custom Options
Konfigurasikan `SaveOptions` sehingga file yang telah direduksi mendapatkan akhiran “_Redacted” sambil mempertahankan format aslinya.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
	tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### Step 6: Release Resources
Selalu tutup `Redactor` untuk membebaskan sumber daya native dan menghindari kebocoran memori.

```java
finally {
    redactor.close();
}
```

## Common Issues and Solutions
- **FileNotFoundException** – Periksa kembali path yang Anda berikan ke `Redactor`. Gunakan path absolut atau `Paths.get(...)` untuk keandalan.  
- **Tidak ada perubahan yang terlihat** – Pastikan bidang metadata yang Anda target memang berisi string pencarian; metadata bersifat case‑sensitive secara default.  
- **Kesalahan out‑of‑memory pada file besar** – Proses dokumen dalam batch lebih kecil dan panggil `redactor.close()` segera setelah setiap file.  

## Practical Applications
1. **Dokumentasi Hukum** – Hapus nama perusahaan klien sebelum mengirim kontrak ke pihak ketiga.  
2. **Pelaporan Keuangan** – Anonimkan pengidentifikasi internal dalam file audit.  
3. **Proyek Kolaboratif** – Lindungi informasi kepemilikan saat berbagi draf dengan vendor eksternal.  

## Performance Considerations
- **Manajemen Memori** – Pustaka menyimpan seluruh dokumen di memori; menutup `Redactor` setelah setiap file sangat penting.  
- **Pemrosesan Batch** – Untuk skenario volume tinggi, iterasi melalui koleksi file dan gunakan kembali satu instance `SaveOptions`.  
- **Tetap Terbaru** – Rilis baru membawa perbaikan kinerja dan perbaikan bug; selalu gunakan versi stabil terbaru.  

## Conclusion
Anda kini tahu **cara menggunakan MetadataSearchRedaction** untuk secara aman menghapus metadata perusahaan dari dokumen menggunakan GroupDocs.Redaction untuk Java. Gabungkan langkah‑langkah ini ke dalam pipeline pemrosesan dokumen Anda untuk tetap patuh dan melindungi informasi sensitif.

**Langkah Selanjutnya**
- Eksperimen dengan bidang metadata lain seperti *Author* atau *Creator*.  
- Gabungkan redaksi metadata dengan redaksi teks atau gambar untuk solusi cakupan penuh.  

## Bagian FAQ
1. **Apa itu GroupDocs.Redaction untuk Java?**  
   - Ini adalah pustaka kuat yang memungkinkan Anda meredaksi teks, metadata, dan gambar dalam dokumen menggunakan aplikasi Java.  
2. **Bisakah saya menggunakan GroupDocs.Redaction tanpa membeli lisensi?**  
   - Ya, tetapi dengan batasan. Lisensi percobaan gratis atau lisensi sementara memungkinkan akses penuh untuk tujuan pengujian.  
3. **Bagaimana cara memastikan format dokumen tetap terjaga selama redaksi?**  
   - Gunakan `SaveOptions` untuk menentukan kebutuhan Anda, seperti menghindari rasterisasi ke PDF.  
4. **Jenis dokumen apa yang dapat direduksi menggunakan GroupDocs.Redaction?**  
   - Ia mendukung berbagai jenis, termasuk Word, Excel, PowerPoint, PDF, dan banyak lagi.  
5. **Di mana saya dapat menemukan dukungan jika mengalami masalah?**  
   - Kunjungi [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk bantuan.  

## Pertanyaan yang Sering Diajukan
**Q: Apakah MetadataSearchRedaction bekerja dengan dokumen terenkripsi?**  
A: Ya. Muat dokumen dengan kata sandi yang sesuai menggunakan konstruktor `Redactor` yang menerima parameter kata sandi.

**Q: Bisakah saya menggabungkan beberapa redaksi metadata dalam satu proses?**  
A: Tentu saja. Buat beberapa objek `MetadataSearchRedaction`, atur filter yang berbeda, dan terapkan secara berurutan sebelum menyimpan.

**Q: Apakah memungkinkan untuk melihat pratinjau redaksi sebelum menyimpan?**  
A: Anda dapat memanggil `redactor.getRedactions()` untuk mendapatkan daftar redaksi yang tertunda dan memeriksanya secara programatik.

## Sumber Daya
- **Documentation**: Jelajahi panduan detail di [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference**: Periksa referensi API lengkap di [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download Library**: Akses rilis terbaru dari [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Source Code**: Lihat dan kontribusi di [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Support**: Dapatkan bantuan melalui saluran dukungan gratis di [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

---

**Terakhir Diperbarui:** 2026-01-08  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs  

---