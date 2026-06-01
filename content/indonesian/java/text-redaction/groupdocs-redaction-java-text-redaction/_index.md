---
date: '2026-02-26'
description: Pelajari cara menyunting teks dalam dokumen Java menggunakan GroupDocs.Redaction,
  termasuk cara menyamarkan informasi pribadi dan mengganti teks sensitif.
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
title: Cara Menyensor Teks dengan GroupDocs.Redaction untuk Java
type: docs
url: /id/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Cara Menyensor Teks dalam Dokumen Menggunakan GroupDocs.Redaction untuk Java

Dalam panduan ini Anda akan menemukan **cara menyensor teks** dalam dokumen berbasis Java dengan bantuan GroupDocs.Redaction. Baik Anda perlu **menyembunyikan informasi pribadi** atau **mengganti teks sensitif** dengan placeholder, langkah‑langkah di bawah ini akan memandu Anda melalui solusi lengkap yang siap produksi. Pada akhir tutorial Anda akan dapat melindungi privasi, tetap mematuhi regulasi, dan mengotomatiskan penyensoran di berbagai format file.

## Jawaban Cepat
- **Perpustakaan apa yang digunakan?** GroupDocs.Redaction for Java  
- **Apakah saya dapat menyembunyikan informasi pribadi?** Ya – gunakan exact‑phrase redaction dengan opsi penggantian.  
- **Apakah pemrosesan batch didukung?** Tentu saja, Anda dapat loop melalui banyak file dengan instance Redactor yang sama.  
- **Apakah saya memerlukan lisensi?** Free trial dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Versi Java mana yang diperlukan?** JDK 8 atau lebih baru.

## Apa itu “cara menyensor teks”?
Redaction adalah proses menghapus atau menyamarkan data rahasia secara permanen dari sebuah dokumen. Dengan GroupDocs.Redaction Anda dapat secara programatis menemukan string tertentu, menggantinya dengan placeholder yang aman, dan menyimpan file yang telah dibersihkan—semua tanpa penyuntingan manual.

## Mengapa menggunakan GroupDocs.Redaction untuk Java?
- **Dukungan format luas:** DOCX, PDF, XLSX, PPTX, dan lainnya.  
- **Kinerja tinggi:** Dioptimalkan untuk file besar dan operasi batch.  
- **Callback yang dapat diperluas:** Mengaitkan ke peristiwa penyensoran untuk pencatatan atau penanganan khusus.  
- **Siap kepatuhan:** Memenuhi GDPR, HIPAA, dan regulasi privasi lainnya.

## Prasyarat
- **Java Development Kit (JDK):** Versi 8 atau lebih baru.  
- **IDE:** IntelliJ IDEA, Eclipse, atau editor yang kompatibel dengan Java.  
- **Maven:** Untuk manajemen dependensi.  
- **Pengetahuan dasar Java:** Familiaritas dengan kelas, metode, dan penanganan pengecualian.

## Menyiapkan GroupDocs.Redaction untuk Java
Untuk memulai, tambahkan pustaka ke proyek Maven Anda.

### Pengaturan Maven
Add the repository and dependency to your `pom.xml` file:

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
Jika Anda lebih suka, unduh JAR terbaru dari [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
Anda dapat memulai dengan **Free Trial**, meminta **Temporary License** untuk pengujian yang lebih lama, atau membeli **Commercial License** untuk penggunaan produksi.

## Cara Menyensor Teks dalam Dokumen dengan GroupDocs.Redaction
Bagian‑bagian berikut akan memandu Anda melalui langkah‑langkah tepat untuk **menyembunyikan informasi pribadi** dan **mengganti teks sensitif**.

### Langkah 1: Inisialisasi Redactor
Buat instance `Redactor` yang menunjuk ke dokumen yang ingin Anda proses.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Langkah 2: Terapkan Exact‑Phrase Redaction
Gunakan `ExactPhraseRedaction` untuk menemukan frasa seperti “John Doe” dan menggantinya dengan placeholder yang aman.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameter:**  
  - `"John Doe"` – teks tepat yang akan disensor.  
  - `ReplacementOptions("[personal]")` – string yang akan menggantikan konten asli, secara efektif **menyembunyikan informasi pribadi**.

### Langkah 3: Simpan Dokumen yang Disensor
Simpan perubahan ke file baru atau timpa file asli.

```java
redactor.save();
```

### Langkah 4: Bersihkan Sumber Daya
Selalu tutup `Redactor` untuk membebaskan sumber daya native.

```java
finally {
    redactor.close();
}
```

## Cara Menyembunyikan Informasi Pribadi dengan Callback Kustom
Terkadang Anda memerlukan kontrol lebih terhadap apa yang terjadi saat penyensoran terjadi (mis., pencatatan, penggantian kondisional).

### Buat Kelas Callback
Implementasikan `IRedactionCallback` untuk menerima peristiwa penyensoran.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Gunakan Callback Saat Membuat Instance Redactor
Berikan callback melalui `RedactorSettings`.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Aplikasi Praktis
- **Kontrak hukum:** Secara otomatis menyembunyikan nama klien, SSN, atau klausul rahasia.  
- **Rekam medis:** **Menyembunyikan informasi pribadi** seperti identifier pasien sebelum dibagikan ke pihak ketiga.  
- **Komunikasi korporat:** **Mengganti teks sensitif** seperti kode proyek internal sebelum distribusi eksternal.

## Pertimbangan Kinerja
Saat memproses file yang besar atau banyak, perhatikan tips berikut:

- **Pemrosesan batch:** Loop melalui koleksi file untuk mengurangi overhead startup.  
- **Manajemen memori:** Lepaskan `Redactor` setelah setiap file; hindari menahan banyak dokumen dalam memori secara bersamaan.  
- **Profiling:** Gunakan profiler Java (mis., VisualVM) untuk menemukan bottleneck pada I/O atau logika penyensoran.

## Pertanyaan yang Sering Diajukan
**Q: Bisakah saya menyensor teks dari PDF menggunakan GroupDocs.Redaction?**  
A: Ya, pustaka mendukung PDF, DOCX, XLSX, PPTX, dan banyak format lainnya.

**Q: Apakah penyensoran dapat dibalik?**  
A: Tidak. Penyensoran menghapus konten asli secara permanen, jadi simpan cadangan file sumber.

**Q: Bagaimana cara menangani dokumen yang sangat besar secara efisien?**  
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
- **Forum Dukungan Gratis:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Aplikasi Lisensi Sementara:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Terakhir Diperbarui:** 2026-02-26  
**Diuji Dengan:** GroupDocs.Redaction 24.9 untuk Java  
**Penulis:** GroupDocs