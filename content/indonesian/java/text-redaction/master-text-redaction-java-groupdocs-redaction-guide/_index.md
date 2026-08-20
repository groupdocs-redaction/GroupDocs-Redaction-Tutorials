---
date: '2026-08-20'
description: Temukan cara menyensor teks menggunakan regex di Java dengan GroupDocs.Redaction.
  Tutorial langkah demi langkah ini menunjukkan cara menerapkan regex, mengonfigurasi
  opsi penyimpanan, dan melindungi data sensitif.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Pelajari cara menyensor teks di Java menggunakan GroupDocs.Redaction.
  Panduan ini menjelaskan penyensoran regex, konfigurasi opsi penyimpanan, dan tips
  kinerja untuk melindungi data sensitif.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Cara menyensor teks di Java dengan GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Cara menyensor teks di Java dengan GroupDocs.Redaction: Panduan lengkap'
type: docs
url: /id/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Cara menghapus teks dalam Java dengan GroupDocs.Redaction: Panduan lengkap

Di dunia digital yang bergerak cepat saat ini, **cara menghapus teks** dalam dokumen adalah pertanyaan yang dihadapi banyak pengembang. Baik Anda melindungi data pribadi, mematuhi regulasi, atau sekadar membersihkan draf, panduan ini akan memandu Anda menggunakan GroupDocs.Redaction untuk Java untuk **menerapkan redaksi berbasis regex dengan cepat dan aman**. Anda akan mempelajari mengapa redaksi penting, cara mengonfigurasi pustaka, dan tips praktik terbaik untuk pemrosesan berperforma tinggi.

## Jawaban Cepat
- **Apa tujuan utama GroupDocs.Redaction?** Ini menyediakan API yang handal untuk menemukan dan menyamarkan teks sensitif dalam lebih dari 50 format dokumen.  
- **Bagaimana cara menerapkan regex untuk redaksi?** Buat objek `RegexRedaction` dengan pola Anda dan berikan ke metode `Redactor.apply()`.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi berbayar membuka semua fitur untuk produksi.  
- **Bisakah saya menghapus teks pada PDF serta file DOCX?** Ya—GroupDocs.Redaction mendukung PDF, DOCX, PPTX, dan banyak format lainnya.  
- **Apa cara terbaik untuk meningkatkan kinerja?** Tutup instance `Redactor` dengan cepat, pertahankan pola regex sederhana, dan proses file secara batch.  

## Apa itu redaksi teks dan mengapa penting?
Redaksi teks secara permanen menghapus atau menyamarkan informasi sensitif dari sebuah dokumen, memastikan bahwa data rahasia—seperti nomor jaminan sosial, detail kartu kredit, atau rekam medis—tidak dapat dipulihkan atau dilihat oleh pihak yang tidak berwenang. Ini bekerja dengan menimpa karakter asli atau menggantinya dengan masker, sehingga konten yang tersembunyi tidak dapat diekstrak melalui copy‑paste atau alat OCR. Hal ini memastikan kepatuhan terhadap regulasi privasi dan melindungi individu dari pencurian identitas atau pelanggaran data.

## Mengapa menggunakan regex untuk redaksi teks?
Ekspresi reguler memungkinkan Anda mendefinisikan pola fleksibel yang cocok dengan berbagai format data (mis., nomor telepon, nomor kartu kredit). Menggunakan regex dengan GroupDocs.Redaction memberi Anda kontrol yang tepat atas apa yang disembunyikan, sambil menjaga implementasi tetap ringkas dan mudah dipelihara.

## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki:

- **Java Development Kit (JDK)** terpasang (Java 8 atau lebih baru).  
- Pemahaman dasar tentang sintaks Java dan ekspresi reguler.  
- IDE seperti **IntelliJ IDEA** atau **Eclipse** untuk menjalankan dan men-debug kode.  

## Menyiapkan GroupDocs.Redaction untuk Java
Pertama, tambahkan pustaka ke proyek Anda.

### Pengaturan Maven
Jika Anda menggunakan Maven, sisipkan berikut ke dalam `pom.xml` Anda:

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
Atau, unduh JAR terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Inisialisasi dasar
`Redactor` adalah kelas inti yang membuka dokumen, menerapkan aturan redaksi, dan menulis output.

Setelah pustaka tersedia, Anda dapat mulai meredaksi dokumen:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Cara meredaksi teks menggunakan regex di Java?
Proses ini melibatkan memuat file sumber ke dalam instance `Redactor`, membuat aturan `RegexRedaction` yang mendefinisikan pola yang akan dicocokkan, menerapkan aturan dengan `redactor.apply()`, dan akhirnya menyimpan dokumen yang telah dimodifikasi menggunakan `SaveOptions`. Dengan mengikuti langkah-langkah ini Anda dapat secara andal menemukan dan menyamarkan string sensitif apa pun di semua format yang didukung.

Kelas `Redactor` adalah komponen inti yang membuka dokumen, menerapkan aturan redaksi, dan menulis file output. Ia mengelola sumber daya secara internal, sehingga Anda harus menutupnya setelah pemrosesan untuk membebaskan memori.

### Langkah 1: impor kelas yang diperlukan
Impor berikut memberi Anda akses ke API redaksi:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Langkah 2: inisialisasi redactor dan terapkan pola regex
`RegexRedaction` mewakili aturan redaksi berbasis pola ekspresi reguler. Pola yang Anda berikan menentukan fragmen teks mana yang akan diganti.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Penjelasan regex**: Pola `\b\d{3}-\d{2}-\d{4}\b` cocok dengan nomor Jaminan Sosial AS (tiga digit, tanda hubung, dua digit, tanda hubung, empat digit). `ReplacementOptions` memungkinkan Anda memilih overlay hitam solid atau masker teks khusus.

### Langkah 3: konfigurasi opsi penyimpanan
`SaveOptions` mengontrol cara file yang telah diredaksi ditulis. Menambahkan akhiran membuat jelas file mana yang telah diproses, sementara mempertahankan format asli menghindari konversi yang tidak diinginkan.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Opsi penyimpanan**: `setAddSuffix(true)` secara otomatis menambahkan “_redacted” ke nama file output, mencegah penimpaan tidak sengaja.

### Langkah 4: sesuaikan pengaturan penyimpanan tambahan
Anda dapat menyesuaikan output lebih lanjut—seperti mempertahankan metadata atau meratakan anotasi—dengan menyesuaikan objek `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Konfigurasi utama**: Menetapkan `setPreserveMetadata(true)` mempertahankan properti dokumen asli, yang sering diperlukan untuk audit kepatuhan.

## Aplikasi praktis
Skenario dunia nyata di mana **cara menghapus teks** sangat penting:

1. **Dokumen hukum** – Sembunyikan pengidentifikasi klien sebelum membagikan draf kepada penasihat eksternal.  
2. **Rekam medis** – Samarkan nama pasien, ID, atau nomor kesehatan untuk tetap mematuhi HIPAA.  
3. **Laporan keuangan** – Hapus nomor akun rahasia saat mendistribusikan ringkasan kuartalan.  

## Pertimbangan kinerja
- **Manajemen memori**: Selalu panggil `redactor.close()` untuk melepaskan handle file dan sumber daya native.  
- **Regex efisien**: Pola yang lebih sederhana berjalan lebih cepat; hindari back‑tracking berlebihan dengan menggunakan grup atomik bila memungkinkan.  
- **Pemrosesan batch**: Untuk kumpulan dokumen besar, proses file dalam batch 20–50 untuk menjaga penggunaan heap tetap dapat diprediksi.

## Masalah umum dan solusi
| Masalah | Solusi |
|-------|----------|
| **Regex mencocokkan terlalu banyak** | Uji pola Anda dengan penguji regex daring dan persempit kelas karakter. |
| **Konflik nama file output** | Gunakan `setAddSuffix(true)` atau berikan jalur output khusus melalui `saveOptions.setOutputPath()`. |
| **Kebocoran memori pada PDF besar** | Proses PDF halaman demi halaman atau tingkatkan ukuran heap JVM (`-Xmx2g`). |

## Pertanyaan yang sering diajukan

**Q: Apa tujuan `setAddSuffix(true)` dalam SaveOptions?**  
A: Itu secara otomatis menambahkan akhiran (mis., `_redacted`) ke nama file output, membuat jelas file mana yang telah diproses.

**Q: Bisakah saya menggunakan pola regex selain angka untuk redaksi teks?**  
A: Tentu saja. Setiap ekspresi reguler Java yang valid dapat diberikan ke `RegexRedaction` untuk menargetkan email, nomor telepon, ID khusus, dll.

**Q: Bagaimana saya harus menangani kesalahan selama redaksi?**  
A: Bungkus logika redaksi dalam blok try‑catch, catat pengecualian, dan selalu tutup `Redactor` dalam klausa finally untuk melepaskan sumber daya.

**Q: Apakah redaksi PDF didukung?**  
A: Ya. GroupDocs.Redaction bekerja dengan PDF, DOCX, PPTX, dan banyak format lainnya.

**Q: Apa praktik terbaik untuk proyek redaksi skala besar?**  
A: Gunakan pemrosesan batch, pertahankan pola regex sederhana, dan pantau penggunaan memori dengan alat profiling.

## Sumber daya tambahan
- **Dokumentasi**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Referensi API**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Terakhir Diperbarui:** 2026-08-20  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Mask Sensitive Data Java – Panduan GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redaksi Informasi Pribadi dengan GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Cara Meredaksi PDF dengan Aspose OCR dan Java - Menerapkan Pola Regex menggunakan GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)