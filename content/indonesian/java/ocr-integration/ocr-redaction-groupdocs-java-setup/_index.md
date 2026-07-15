---
date: '2026-06-26'
description: Pelajari cara mengekstrak teks PDF yang dipindai dan menyembunyikan data
  sensitif menggunakan GroupDocs OCR Redaction dengan Azure OCR. Redact social security
  number dan ganti confidential info PDF secara efisien.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Ekstrak Teks PDF yang Dipindai – Sembunyikan Data dengan GroupDocs OCR
type: docs
url: /id/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Ekstrak Teks PDF yang Dipindai – Sembunyikan Data dengan GroupDocs OCR

Dalam dunia yang didorong oleh data saat ini, **mengekstrak teks dari PDF yang dipindai** dan menyembunyikan informasi rahasia adalah langkah kepatuhan yang tidak dapat dinegosiasikan. Tutorial ini memandu Anda menggunakan GroupDocs Redaction bersama Microsoft Azure OCR untuk secara andal mengenali teks tersembunyi pada halaman yang dipindai dan menggantinya dengan placeholder aman seperti **`[REDACTED]`**. Anda akan melihat mengapa kombinasi ini cepat, akurat, dan siap untuk beban kerja tingkat produksi.

## Jawaban Cepat
- **Apa arti “mask sensitive data”?** Itu menggantikan teks rahasia yang teridentifikasi dengan placeholder (misalnya `[REDACTED]`).  
- **Library mana yang menangani OCR?** Microsoft Azure OCR connector, digunakan melalui GroupDocs Redaction.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menghapus (redact) PDF yang dipindai?** Ya—OCR mengekstrak teks tersembunyi sebelum menerapkan redaksi regex.  
- **Apakah solusi ini hanya untuk Java?** Contohnya berbasis Java, tetapi GroupDocs menyediakan API serupa untuk .NET dan platform lainnya.

## Apa itu Redaksi Berbasis OCR?
Redaksi Berbasis OCR pertama-tama menjalankan OCR pada setiap halaman, mengubah gambar menjadi teks yang dapat dicari, kemudian menerapkan pola regex untuk mengganti kecocokan dengan masker seperti `[REDACTED]`. Proses dua langkah ini memungkinkan Anda menyembunyikan data pribadi secara andal bahkan pada PDF yang dipindai, memastikan bahwa semua string sensitif dihapus sebelum dokumen dibagikan atau diarsipkan.

## Mengapa Menggunakan GroupDocs Redaction dengan Azure OCR?
Anda harus menggunakan GroupDocs Redaction dengan Azure OCR karena memberikan **akurasi OCR >98 % pada teks cetak**, mendukung **lebih dari 50 format input dan output**, dan dapat memproses **PDF berjumlah ratusan halaman tanpa memuat seluruh file ke memori**, memastikan redaksi yang cepat dan skalabel untuk kepatuhan. Solusi ini juga **dapat memproses PDF 1.000 halaman dalam waktu kurang dari 2 menit pada server 8‑core**, menjadikan pekerjaan batch praktis.

## Prasyarat
- **Java Development Kit (JDK) 8+** terpasang.  
- **Maven** (jika Anda lebih suka manajemen dependensi) atau kemampuan untuk mengunduh JAR secara manual.  
- **Microsoft Azure OCR credentials** (endpoint dan kunci langganan).  
- Pengetahuan dasar Java dan familiaritas dengan regular expressions.

## Menyiapkan GroupDocs Redaction untuk Java

### Pengaturan Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Jika Anda lebih suka manajemen JAR manual, dapatkan rilis terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
- **Free Trial** – jelajahi semua fitur tanpa biaya.  
- **Temporary License** – perpanjang waktu evaluasi.  
- **Full License** – buka kemampuan siap produksi.

### Inisialisasi dan Pengaturan Dasar
Kelas `Redactor` adalah mesin inti yang melakukan ekstraksi OCR dan menerapkan aturan redaksi pada dokumen PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Cara Menyembunyikan Data Sensitif dengan Redaksi OCR
Menyembunyikan data sensitif dengan Redaksi OCR melibatkan memuat PDF dengan pengaturan Azure OCR, mendefinisikan pola regex untuk data yang ingin Anda sembunyikan, dan memanggil Redactor untuk mengganti setiap kecocokan dengan placeholder seperti `[REDACTED]`. Library menangani OCR, pencocokan pola, dan penulisan ulang PDF dalam satu alur kerja.

### Langkah 1: Muat Dokumen dengan Pengaturan OCR
`LoadOptions` mengonfigurasi cara GroupDocs memuat file, memungkinkan Anda memberikan konektor OCR seperti Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – ganti dengan path ke PDF Anda.  
- **`settings`** – berisi konektor Azure OCR yang Anda buat sebelumnya.

### Langkah 2: Definisikan dan Terapkan Redaksi Regex
`ReplacementOptions` menentukan teks pengganti yang akan menggantikan setiap kecocokan regex selama redaksi.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Pola `\b\d{3}-\d{2}-\d{4}\b` cocok dengan Nomor Jaminan Sosial (Social Security Numbers) AS.  
- `ReplacementOptions("[REDACTED]")` menukar setiap kecocokan dengan masker, secara efektif **menyembunyikan data sensitif**.

## Contoh Penggunaan Umum untuk Menyembunyikan Data Sensitif
1. **Legal Document Management** – sembunyikan pengidentifikasi klien sebelum membagikan draf.  
2. **Financial Reporting** – lindungi nomor akun dan ID transaksi.  
3. **Healthcare Records** – patuhi HIPAA dengan menyorot (redact) pengidentifikasi pasien.  
4. **Government Publications** – hapus data pribadi dari catatan publik.  
5. **Corporate Contracts** – sembunyikan ketentuan kepemilikan selama tinjauan eksternal.

## Tips Kinerja
- **Optimize regex** – hindari pola yang terlalu luas yang meningkatkan waktu pemrosesan; ekspresi yang dirancang dengan baik dapat mengurangi waktu eksekusi hingga 40 %.  
- **Memory Management** – tutup instance `Redactor` dengan cepat (try‑with‑resources melakukannya secara otomatis).  
- **Asynchronous Execution** – untuk pemrosesan massal, jalankan pekerjaan redaksi pada thread terpisah atau gunakan antrian tugas untuk menjaga UI tetap responsif.

## Pemecahan Masalah
- **Azure credentials error** – periksa kembali URL endpoint dan kunci langganan di `MicrosoftAzureOcrConnector`.  
- **Document not loading** – verifikasi path file dan pastikan PDF tidak dilindungi kata sandi (atau berikan kata sandi melalui `LoadOptions`).  
- **No redactions applied** – uji regex Anda dengan string sederhana terlebih dahulu; gunakan `Pattern.compile` dalam unit test untuk mengonfirmasi kecocokan.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu redaksi OCR?**  
A: Redaksi OCR menggunakan Optical Character Recognition untuk mengekstrak teks tersembunyi dari gambar atau PDF yang dipindai, kemudian menerapkan aturan redaksi untuk menyembunyikan teks tersebut.

**Q: Bisakah saya menggunakan GroupDocs Redaction tanpa Azure OCR?**  
A: Ya, tetapi OCR secara dramatis meningkatkan akurasi pada dokumen yang dipindai di mana ekstraksi teks asli gagal.

**Q: Bagaimana cara menangani pola regex yang kompleks?**  
A: Bangun dan uji secara bertahap, menggunakan kelas `Pattern` Java di sandbox sebelum menerapkannya pada dokumen besar.

**Q: Apa saja bottleneck kinerja yang umum?**  
A: PDF besar, regex yang terlalu kompleks, dan panggilan OCR sinkron dapat memperlambat proses; pertimbangkan pemrosesan batch dan pola yang dioptimalkan.

**Q: Apakah dukungan tersedia untuk masalah implementasi?**  
A: Tentu—hubungi melalui [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) untuk bantuan komunitas atau hubungi dukungan GroupDocs.

## Sumber Daya Tambahan
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

**Terakhir Diperbarui:** 2026-06-26  
**Diuji Dengan:** GroupDocs.Redaction 24.9 (Java)  
**Penulis:** GroupDocs  

## Tutorial Terkait

- [Redaksi PDF Aman menggunakan OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Cara Menyensor Teks dengan GroupDocs.Redaction untuk Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Sembunyikan Data Sensitif Java – Redact Informasi Pribadi dengan GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)