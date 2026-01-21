---
date: '2026-01-21'
description: Pelajari cara menyensor PDF dengan OCR dan menyensor dokumen yang dipindai
  menggunakan GroupDocs.Redaction untuk Java dengan integrasi Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Menyensor PDF dengan OCR menggunakan GroupDocs & Azure OCR – Panduan Java
type: docs
url: /id/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Redact PDF dengan OCR menggunakan GroupDocs & Azure OCR – Panduan Java

Dalam tutorial komprehensif ini Anda akan menemukan cara **redact PDF with OCR** di Java, memanfaatkan GroupDocs.Redaction bersama Microsoft Azure OCR. Baik Anda bekerja dengan PDF native maupun gambar hasil pemindaian, panduan ini menunjukkan cara menemukan dan menyembunyikan data sensitif secara akurat, membantu Anda **redact scanned documents** untuk memenuhi regulasi privasi.

## Quick Answers
- **Apa yang dilakukan OCR redaction?** Ia mengekstrak teks dari gambar/PDF dan menerapkan aturan redaksi secara otomatis.  
- **Perpustakaan mana yang menyediakan mesin redaksi?** GroupDocs.Redaction untuk Java.  
- **Layanan OCR mana yang digunakan?** Microsoft Azure OCR connector.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya redact PDF native dan PDF hasil pemindaian?** Ya – OCR memungkinkan redaksi dokumen yang dipindai juga.

## Apa itu “redact PDF with OCR”?
Redact PDF dengan OCR berarti menggunakan optical character recognition untuk mengubah teks visual menjadi string yang dapat dicari, kemudian menerapkan pola redaksi (misalnya regex) untuk menyembunyikan informasi tersebut sebelum file dibagikan atau disimpan.

## Mengapa menggunakan GroupDocs.Redaction dengan Azure OCR?
- **Akurasi tinggi** pada halaman yang dipindai berkat mesin OCR berbasis cloud Azure.  
- **API Java yang sederhana** yang terintegrasi langsung ke alur kerja Anda.  
- **Aturan redaksi fleks** – regex, kata kunci, atau logika khusus.  
- **Output siap kepatuhan** yang secara permanen menghapus data sensitif.

## Prasyarat
- Java Development Kit (JDK) 8 atau yang lebih baru.  
- Maven (atau opsi untuk mengunduh JAR secara manual).  
- Akun Microsoft Azure dengan kredensial OCR.  
- Pengetahuan dasar Java dan pemahaman tentang regular expressions.

## Menyiapkan GroupDocs.Redaction untuk Java

### Maven Setup
Tambahkan repositori GroupDocs dan dependensi ke `pom.xml` Anda:

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
Jika Anda lebih memilih tidak menggunakan Maven, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
- **Free Trial** – jelajahi fitur inti tanpa komitmen.  
- **Temporary License** – perpanjang masa percobaan untuk proyek yang lebih besar.  
- **Full License** – buka penggunaan tak terbatas dan dukungan premium.

### Basic Initialization and Setup
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Cara redact PDF dengan OCR di Java

### Langkah 1: Load Dokumen dengan Pengaturan OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parameter**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – path ke PDF target.  
  - `new LoadOptions()` – konfigurasi pemuatan default.  
  - `settings` – berisi Azure OCR connector.

### Langkah 2: Terapkan Regex Redactions (misalnya Nomor Jaminan Sosial)
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
- **Penjelasan Regex** – `\b\d{3}-\d{2}-\d{4}\b` mencocokkan pola seperti `123-45-6789`.  
- **ReplacementOptions** – menggantikan teks yang terdeteksi dengan `[REDACTED]`.

### Kesalahan Umum & Pemecindai
usi kenyataan yang dipindai.  
3. **Penyedia layanan kesehatan** – melindungi PHI pasien dalam rekam medis yang dipindai.  
4. **Instansi pemerintah** – menghapus data pribadi dari PDF catatan publik.  
5. **Perusahaan** – membersihkan kontrak sebelum audit pihak ketiga.

## Tips Kinerja
- Buat pola regex sespesifik mungkin untuk mengurangi waktu pemrosesan.  
- Segera lepaskan instance `Redactor` (gunakan try‑with‑resources seperti contoh).  
- Untuk pemrosesan batch, pert Apa OCR redaction menggunakan optical character efektif.

**T: Bagaimana cara menangani Uji pola dengan data contoh, gunakan batas kata (`\b`) untuk menghindari pencocokan parsial, dan pertimbangkan memecah ekspresi besar menjadi beberapa redaksi yang lebih sederhana.

**T: Apa saja bottleneck kinerja yang umum. Optimalkan dengan menyetel regex dan menskalakan sumber daya.

**T: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
J: Ajukan pertanyaan di forum komunitas GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Sumber Daya Tambahan
- **Documentation**: https://docs.groupdocs.com/red https://reference.groupdocs.com/redaction/java
- **Download**: https://releases.groupdocs.com/redaction/java/
-.RedactionAuthor:** GroupDocs