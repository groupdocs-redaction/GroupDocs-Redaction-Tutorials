---
date: '2026-02-26'
description: Pelajari cara menyensor teks menggunakan GroupDocs.Redaction Java dan
  menyimpannya sebagai PDF raster dengan penggantian frasa yang tepat serta pengaturan
  PDF khusus.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: Cara Menyensor Teks dengan GroupDocs.Redaction Java
type: docs
url: /id/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Cara Menyensor Teks dengan GroupDocs.Redaction Java

Di dunia yang didorong oleh data saat ini, **cara menyensor teks** dalam dokumen secara aman dan efisien menjadi perhatian utama bagi pengembang dan petugas kepatuhan. Baik Anda perlu menyembunyikan pengidentifikasi pribadi, detail klien yang rahasia, atau kode proyek internal, GroupDocs.Redaction untuk Java memberikan cara yang dapat diandalkan untuk menemukan frasa tepat dan menggantinya dengan overlay yang aman. Tutorial ini juga menunjukkan **cara menyimpan sebagai PDF rasterisasi**, mengubah setiap halaman menjadi PDF berbasis gambar yang memenuhi standar arsip.

## Jawaban Cepat
- **Apa kelas utama untuk penyensoran?** `Redactor`  
- **Apakah saya dapat mengganti frasa dengan overlay berwarna?** Ya, menggunakan `ExactPhraseRedaction` dan `ReplacementOptions`.  
- **Bagaimana cara menghasilkan PDF rasterisasi?** Aktifkan rasterisasi melalui `SaveOptions.getRasterization().setEnabled(true)`.  
- **Level kepatuhan PDF mana yang digunakan dalam contoh?** `PdfComplianceLevel.PdfA1a`.  
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk penerapan produksi.

## Apa itu “cara menyensor teks” dalam Java?
Penyensoran adalah proses menghapus atau menyamarkan konten sensitif secara permanen dari sebuah file. Dengan GroupDocs.Redaction, Anda dapat secara programatis mencari frasa tepat—seperti nama atau ID—dan menggantinya dengan overlay merah, kotak hitam, atau elemen visual kustom apa pun, memastikan data asli tidak dapat dipulihkan.

## Mengapa Menggunakan GroupDocs.Redaction untuk Java?
- **Pencocokan frasa tepat** menghilangkan hasil positif palsu.  
- **Rasterisasi bawaan** memungkinkan Anda membuat PDF yang mematuhi PDF/A, hanya gambar, untuk penyimpanan jangka panjang.  
- **Dukungan lintas format** bekerja dengan DOCX, PDF, PPTX, dan lainnya, sehingga Anda dapat menerapkan kode yang sama pada berbagai jenis dokumen.  
- **API berfokus pada kinerja** memungkinkan Anda memproses batch kumpulan dokumen besar sambil menjaga penggunaan memori tetap rendah.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki hal berikut:

- **GroupDocs.Redaction untuk Java** (v24.9 atau lebih baru).  
- **Java Development Kit (JDK) 8+**.  
- Sebuah IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.  
- Maven untuk manajemen dependensi.  

### Perpustakaan dan Dependensi yang Diperlukan
- **GroupDocs.Redaction untuk Java** – tambahkan repositori dan dependensi ke `pom.xml` Anda (lihat blok kode di bawah).  
- **Opsional**: Perpustakaan logging tambahan apa pun yang Anda sukai.

### Prasyarat Pengetahuan
- Sintaks Java dasar dan I/O file.  
- Familiaritas dengan struktur `pom.xml` Maven.  

## Menyiapkan GroupDocs.Redaction untuk Java
### Pengaturan Maven
Tambahkan repositori dan dependensi ke file `pom.xml` Anda:

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
Sebagai alternatif, Anda dapat mengunduh versi terbaru langsung dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
- **Free Trial** – jelajahi API tanpa kunci lisensi.  
- **Temporary License** – gunakan untuk evaluasi yang diperpanjang.  
- **Full License** – diperlukan untuk lingkungan produksi.

### Inisialisasi dan Pengaturan Dasar
Berikut adalah kode minimal untuk membuat instance `Redactor` yang mengarah ke file DOCX contoh:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Cara Menyensor Teks – Contoh Frasa Tepat
### Langkah 1: Impor Kelas yang Diperlukan
Impor ini memberi Anda akses ke mesin penyensoran dan opsi penggantian:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Langkah 2: Buat dan Terapkan Penyensoran
Potongan kode berikut mencari frasa **“John Doe”** dan menggantinya dengan overlay merah:

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

**Mengapa ini penting:** `ReplacementOptions` memungkinkan Anda mengontrol gaya visual penyensoran, memastikan konten tersembunyi tidak dapat dipulihkan melalui copy‑paste atau OCR.

## Cara Menyimpan sebagai PDF Rasterisasi
### Langkah 1: Impor Kelas SaveOptions
Kelas-kelas ini memungkinkan Anda mengkonfigurasi output PDF, termasuk rasterisasi dan level kepatuhan:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Langkah 2: Konfigurasi dan Terapkan Opsi Penyimpanan
Setelah penyensoran, Anda dapat mengekspor dokumen sebagai PDF rasterisasi. Contoh di bawah merasterisasi hanya halaman 5 dan memaksa kepatuhan PDF/A‑1a:

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

**Poin utama:** Merasterisasi PDF **mengubah setiap halaman menjadi gambar**, yang menghapus lapisan teks tersembunyi dan membuat dokumen tahan manipulasi—ideal untuk arsip hukum.

## Aplikasi Praktis
1. **Penyensoran Data Sensitif** – Secara otomatis menyembunyikan pengidentifikasi pribadi sebelum membagikan kontrak.  
2. **Pengarsipan Dokumen** – Mengonversi laporan final menjadi PDF/A rasterisasi untuk kepatuhan jangka panjang.  
3. **Pembaruan Konten Massal** – Mengganti terminologi usang di ratusan file dengan satu skrip.  

## Pertimbangan Kinerja
- **Tutup `Redactor`** setelah setiap operasi untuk melepaskan handle file dan memori.  
- **Pemrosesan Batch** – Muat daftar file dan iterasi melalui mereka, menggunakan kembali satu instance `Redactor` bila memungkinkan.  
- **Pantau Sumber Daya** – Gunakan alat profiling Java untuk memantau penggunaan CPU dan heap selama penyensoran skala besar.  

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana cara menginstal GroupDocs.Redaction dalam proyek Maven?**  
A: Tambahkan repositori GroupDocs dan dependensi `groupdocs-redaction` ke `pom.xml` Anda seperti yang ditunjukkan pada bagian Pengaturan Maven.

**Q: Bisakah saya menyensor teks dari file PDF menggunakan perpustakaan ini?**  
A: Ya, GroupDocs.Redaction mendukung PDF, DOCX, PPTX, dan banyak format lainnya.

**Q: Apa yang terjadi jika frasa tepat tidak ditemukan?**  
A: `RedactorChangeLog` akan mengembalikan status `Failed`. Verifikasi ejaan dan sensitivitas huruf pada frasa tersebut.

**Q: Bagaimana saya dapat menangani dokumen sangat besar secara efisien?**  
A: Proses mereka dalam rentang halaman yang lebih kecil, aktifkan rasterisasi hanya bila diperlukan, dan selalu tutup `Redactor` untuk membebaskan sumber daya.

**Q: Apakah memungkinkan menyimpan PDF rasterisasi dengan rentang halaman tertentu?**  
A: Tentu saja. Gunakan `options.getRasterization().setPageIndex()` dan `setPageCount()` untuk menargetkan halaman tepat yang ingin Anda rasterisasi.

## Kesimpulan
Anda kini memiliki panduan lengkap, end‑to‑end tentang **cara menyensor teks** dengan GroupDocs.Redaction Java dan **menyimpan sebagai PDF rasterisasi**. Dengan mengikuti langkah‑langkah ini, Anda dapat melindungi informasi sensitif, memenuhi persyaratan kepatuhan, dan mempertahankan kinerja tinggi dalam beban kerja produksi.

**Langkah Selanjutnya**  
- Selami lebih dalam API dengan menjelajahi [dokumentasi resmi](https://docs.groupdocs.com/redaction/java/).  
- Bereksperimen dengan tipe penyensoran lain (mis., `RegexRedaction`, `ImageRedaction`).  
- Bergabung dengan komunitas di [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) untuk tips dan praktik terbaik.

---

**Terakhir Diperbarui:** 2026-02-26  
**Diuji Dengan:** GroupDocs.Redaction Java 24.9  
**Penulis:** GroupDocs