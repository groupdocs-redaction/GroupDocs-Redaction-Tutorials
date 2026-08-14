---
date: '2026-08-14'
description: Cara menyunting teks dalam dokumen Java menggunakan GroupDocs.Redaction
  – menyamarkan informasi pribadi dan mengganti teks sensitif secara efisien.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: Cara menyunting teks dengan GroupDocs.Redaction untuk Java memungkinkan
  Anda menyamarkan data pribadi secara permanen dan mengganti string sensitif di seluruh
  PDF, DOCX, dan lainnya, memastikan kepatuhan terhadap GDPR dan HIPAA.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: Cara menyunting teks dengan GroupDocs.Redaction untuk Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: Cara menyunting teks dengan GroupDocs.Redaction untuk Java
type: docs
url: /id/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Cara menyensor teks dengan GroupDocs.Redaction untuk Java

Dalam tutorial ini Anda akan belajar **cara menyensor teks** dalam dokumen berbasis Java menggunakan GroupDocs.Redaction. Anda akan melihat cara menyamarkan informasi pribadi, mengganti string sensitif dengan placeholder yang aman, dan memproses banyak file secara batch‑friendly. Pada akhir tutorial Anda akan memiliki solusi siap produksi yang melindungi privasi, memenuhi persyaratan GDPR/HIPAA, dan terintegrasi dengan mulus ke dalam aplikasi Java yang ada.

## Jawaban Cepat
- **Perpustakaan apa yang digunakan?** GroupDocs.Redaction for Java.  
- **Bisakah saya menyamarkan informasi pribadi?** Ya – gunakan penyensoran frasa tepat dengan opsi penggantian.  
- **Apakah pemrosesan batch didukung?** Tentu saja, Anda dapat melakukan loop melalui banyak file dengan instance Redactor yang sama.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.

## Apa itu “cara menyensor teks”?

Penyensoran secara permanen menghapus atau menyamarkan data rahasia dari sebuah dokumen. Dengan GroupDocs.Redaction Anda dapat menemukan string tertentu, menggantinya dengan placeholder yang aman, dan menyimpan file yang telah dibersihkan—semua tanpa penyuntingan manual.

## Mengapa menggunakan GroupDocs.Redaction untuk Java?

GroupDocs.Redaction untuk Java mendukung **lebih dari 50 format input dan output** (termasuk PDF, DOCX, XLSX, PPTX, TXT, RTF) dan dapat memproses file berukuran ratusan halaman tanpa memuat seluruh dokumen ke memori, memberikan operasi batch berkecepatan tinggi pada perangkat keras server standar.

## Prasyarat
- **Java Development Kit (JDK):** Versi 8 atau lebih baru.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor kompatibel Java lainnya.  
- **Maven:** Untuk manajemen dependensi.  
- **Pengetahuan dasar Java:** Familiaritas dengan kelas, metode, dan penanganan pengecualian.

## Menyiapkan GroupDocs.Redaction untuk Java
Untuk memulai, tambahkan pustaka ke proyek Maven Anda.

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

### Unduhan langsung
Jika Anda lebih suka, unduh JAR terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
Anda dapat memulai dengan **Free Trial**, meminta **Temporary License** untuk pengujian lanjutan, atau membeli **Commercial License** untuk penggunaan produksi.

## Cara menyensor teks dalam dokumen dengan GroupDocs.Redaction

Bagian-bagian berikut akan memandu Anda melalui langkah-langkah tepat untuk **menyamarkan informasi pribadi** dan **mengganti teks sensitif**.

### Langkah 1: inisialisasi redaktor
`Redactor` adalah kelas inti yang memuat dokumen, menerapkan aturan penyensoran, dan menulis output.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Langkah 2: terapkan penyensoran frasa tepat
`ExactPhraseRedaction` mencari kecocokan string yang tepat, sementara `ReplacementOptions` menentukan bagaimana teks yang cocok harus diganti.  

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameter:**  
  - `"John Doe"` – teks tepat yang akan disensor.  
  - `ReplacementOptions("[personal]")` – string yang akan menggantikan konten asli, secara efektif **menyamarkan informasi pribadi**.

### Langkah 3: simpan dokumen yang disensor
`Redactor.save` menulis dokumen yang telah dimodifikasi ke file baru atau menimpa yang asli, mempertahankan format asli.  

```java
redactor.save();
```

### Langkah 4: bersihkan sumber daya
Selalu panggil `Redactor.close()` untuk melepaskan sumber daya native dan menghindari kebocoran memori.  

```java
finally {
    redactor.close();
}
```

## Cara menyamarkan informasi pribadi dengan callback khusus

Callback khusus memungkinkan Anda merespons setiap peristiwa penyensoran—berguna untuk pencatatan, penggantian bersyarat, atau jejak audit.

### Buat kelas callback
`IRedactionCallback` mendefinisikan metode yang dipanggil sebelum dan setelah setiap operasi penyensoran.  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Gunakan callback saat menginstansiasi Redactor
Berikan implementasi callback Anda melalui `RedactorSettings` sehingga mesin mengetahui untuk memanggilnya selama pemrosesan.  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Aplikasi Praktis
- **Kontrak hukum:** Secara otomatis menyembunyikan nama klien, SSN, atau klausul rahasia sebelum membagikan draf.  
- **Rekam medis:** **Menyamarkan informasi pribadi** seperti pengidentifikasi pasien saat mengekspor rekam ke mitra penelitian.  
- **Komunikasi korporat:** **Mengganti teks sensitif** seperti kode proyek internal sebelum distribusi eksternal, memastikan tidak ada kebocoran tidak sengaja.

## Pertimbangan Kinerja
Saat memproses file yang besar atau banyak, perhatikan tips berikut:

- **Pemrosesan batch:** Loop melalui kumpulan file untuk mengurangi overhead startup.  
- **Manajemen memori:** Lepaskan `Redactor` setelah setiap file; hindari menahan banyak dokumen dalam memori secara bersamaan.  
- **Profiling:** Gunakan profiler Java (misalnya, VisualVM) untuk menemukan bottleneck pada I/O atau logika penyensoran.

## Pertanyaan yang Sering Diajukan
**Q: Bisakah saya menyensor teks dari PDF menggunakan GroupDocs.Redaction?**  
A: Ya, pustaka mendukung PDF, DOCX, XLSX, PPTX, dan banyak format lainnya.

**Q: Apakah penyensoran dapat dibalik?**  
A: Tidak. Penyensoran secara permanen menghapus konten asli, jadi simpan cadangan file sumber.

**Q: Bagaimana cara menangani dokumen sangat besar secara efisien?**  
A: Proses dalam potongan, gunakan mode batch, dan pantau penggunaan memori dengan alat profiling.

**Q: Format teks lain apa yang didukung?**  
A: Selain DOCX dan PDF, Anda dapat menyensor TXT, RTF, XLSX, PPTX, dan lainnya.

**Q: Bisakah saya mengintegrasikan GroupDocs.Redaction ke dalam alur kerja yang ada?**  
A: Tentu saja. API dapat dipanggil dari layanan web, pekerjaan latar belakang, atau pipeline CI/CD.

## Sumber Daya
- **Dokumentasi:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referensi API:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Unduhan:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **Repositori GitHub:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Forum dukungan gratis:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Aplikasi lisensi sementara:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-08-14  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Menyamarkan Data Sensitif Java – Panduan GroupDocs.Redaction](/redaction/java/getting-started/)
- [Menyamarkan Data Sensitif Java – Menyensor Info Pribadi dengan GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Edit Dokumen Java yang Dilindungi Kata Sandi - Menyensor Dokumen Menggunakan GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)