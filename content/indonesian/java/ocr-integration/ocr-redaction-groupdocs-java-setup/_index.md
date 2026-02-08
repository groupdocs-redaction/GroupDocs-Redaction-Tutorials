---
date: '2026-02-08'
description: Pelajari cara menyamarkan data sensitif dan menyensor file PDF Java menggunakan
  GroupDocs OCR Redaction dengan Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Menyamarkan Data Sensitif pada PDF dengan Redaksi OCR GroupDocs
type: docs
url: /id/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Menyamarkan Data Sensitif dalam PDF dengan GroupDocs OCR Redaction

Dalam lanskap digital saat ini, melindungi informasi pribadi dan rahasia merupakan prioritas utama. Dalam tutorial ini, **Anda akan belajar cara menyamarkan data sensitif** dalam file PDF dengan menggabungkan GroupDocs Redaction dengan Microsoft Azure OCR. Pendekatan ini memberikan pengenalan teks yang dapat diandalkan pada halaman yang dipindai dan memungkinkan Anda **redact PDF Java** dokumen dengan presisi, memastikan kepatuhan terhadap regulasi privasi.

## Jawaban Cepat
- **Apa arti “mask sensitive data”?** Itu menggantikan teks rahasia yang teridentifikasi dengan placeholder (mis., `[REDACTED]`).  
- **Library mana yang menangani OCR?** Microsoft Azure OCR connector, yang digunakan melalui GroupDocs Redaction.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Bisakah saya menyunting PDF yang dipindai?** Ya—OCR mengekstrak teks tersembunyi sebelum menerapkan redaksi regex.  
- **Apakah solusi ini hanya untuk Java?** Contohnya berbasis Java, tetapi GroupDocs menyediakan API serupa untuk .NET dan platform lainnya.

## Apa itu Redaksi Berbasis OCR?
Redaksi berbasis OCR pertama-tama menjalankan Optical Character Recognition pada setiap halaman dokumen, mengubah gambar teks menjadi string yang dapat dicari. Setelah teks dapat dicari, Anda dapat menerapkan aturan regular‑expression (regex) untuk menemukan informasi sensitif—seperti Social Security Numbers, nomor kartu kredit, atau pengenal pribadi—dan menggantinya dengan masker seperti **`[REDACTED]`**.

## Mengapa Menggunakan GroupDocs Redaction dengan Azure OCR?
- **Akurasi tinggi** pada PDF dan gambar yang dipindai.  
- **Integrasi Java yang mulus** melalui Maven atau unduhan JAR langsung.  
- **Mesin regex yang fleksibel** memungkinkan Anda mendefinisikan pola khusus untuk tipe data apa pun.  
- **Skalabel** untuk batch dokumen besar, dengan opsi pemrosesan asynchronous.

## Prasyarat
- **Java Development Kit (JDK) 8+** terpasang.  
- **Maven** (jika Anda lebih suka manajemen dependensi) atau kemampuan mengunduh JAR secara manual.  
- **Kredensial Microsoft Azure OCR** (endpoint dan subscription key).  
- Pengetahuan dasar Java dan familiaritas dengan regular expressions.

## Menyiapkan GroupDocs Redaction untuk Java

### Pengaturan Maven
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

### Unduhan Langsung
Jika Anda lebih suka manajemen JAR manual, dapatkan rilis terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
- **Free Trial** – jelajahi semua fitur tanpa biaya.  
- **Temporary License** – memperpanjang waktu evaluasi.  
- **Full License** – membuka kemampuan siap produksi.

### Inisialisasi dan Pengaturan Dasar
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Cara Menyamarkan Data Sensitif dengan Redaksi OCR

### Langkah 1: Muat Dokumen dengan Pengaturan OCR
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
- **`LoadOptions`** – pemuatan default; Anda dapat menyesuaikannya jika diperlukan.  
- **`settings`** – berisi Azure OCR connector yang Anda buat sebelumnya.

### Langkah 2: Definisikan dan Terapkan Redaksi Regex
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
- Pola `\b\d{3}-\d{2}-\d{4}\b` cocok dengan Social Security Numbers Amerika Serikat.  
- `ReplacementOptions("[REDACTED]")` mengganti setiap kecocokan dengan masker, secara efektif **menyamarkan data sensitif**.

## Kasus Penggunaan Umum untuk Menyamarkan Data Sensitif
1. **Legal Document Management** – menyembunyikan pengenal klien sebelum membagikan draf.  
2. **Financial Reporting** – melindungi nomor akun dan ID transaksi.  
3. **Healthcare Records** – mematuhi HIPAA dengan menyunting pengenal pasien.  
4. **Government Publications** – menghapus data pribadi dari catatan publik.  
5. **Corporate Contracts** – menyembunyikan ketentuan kepemilikan selama tinjauan eksternal.

## Tips Kinerja
- **Optimalkan regex** – hindari pola yang terlalu luas yang meningkatkan waktu pemrosesan.  
- **Manajemen Memori** – tutup instance `Redactor` dengan cepat (try‑with‑resources melakukannya secara otomatis).  
- **Eksekusi Asynchronous** – untuk pemrosesan massal, jalankan pekerjaan redaksi pada thread terpisah atau gunakan antrian tugas.  

## Pemecahan Masalah
- **Kesalahan kredensial Azure** – periksa kembali URL endpoint dan subscription key di `MicrosoftAzureOcrConnector`.  
- **Dokumen tidak dapat dimuat** – verifikasi path file dan pastikan PDF tidak dilindungi kata sandi (atau berikan kata sandi melalui `LoadOptions`).  
- **Tidak ada redaksi yang diterapkan** – uji regex Anda dengan string sederhana terlebih dahulu; gunakan `Pattern.compile` dalam unit test untuk memastikan kecocokan.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu redaksi OCR?**  
A: Redaksi OCR menggunakan Optical Character Recognition untuk mengekstrak teks tersembunyi dari gambar atau PDF yang dipindai, kemudian menerapkan aturan redaksi untuk menyamarkan teks tersebut.

**Q: Bisakah saya menggunakan GroupDocs Redaction tanpa Azure OCR?**  
A: Ya, tetapi OCR secara dramatis meningkatkan akurasi pada dokumen yang dipindai di mana ekstraksi teks native gagal.

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

---

**Terakhir Diperbarui:** 2026-02-08  
**Diuji Dengan:** GroupDocs.Redaction 24.9 (Java)  
**Penulis:** GroupDocs