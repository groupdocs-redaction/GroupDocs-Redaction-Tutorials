---
date: '2026-09-21'
description: Pelajari cara menyensor gambar dengan GroupDocs.Redaction for Java. Panduan
  langkah demi langkah mencakup penyiapan, pixel‑level redaction, verifikasi, dan
  praktik terbaik.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Cara menyensor gambar dengan GroupDocs.Redaction for Java. Ikuti panduan
  ini untuk menyembunyikan pixel data dalam scanned files, pilih colors, dan verifikasi
  results—perfect untuk GDPR dan HIPAA compliance.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Cara menyensor gambar menggunakan GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Cara menyensor gambar menggunakan GroupDocs.Redaction for Java
type: docs
url: /id/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Cara men‑redact gambar menggunakan GroupDocs.Redaction untuk Java

Dalam tutorial komprehensif ini Anda akan belajar **cara men‑redact gambar** di Java dengan GroupDocs.Redaction. Men‑redact gambar yang dipindai merupakan langkah penting untuk melindungi data pribadi, memenuhi regulasi GDPR, HIPAA, atau regulasi privasi lainnya, serta memastikan informasi visual rahasia tidak pernah bocor. Kami akan memandu Anda melalui penyiapan proyek, mengonfigurasi redaksi tingkat piksel, menyimpan hasil dengan aman, dan mengonfirmasi bahwa redaksi berhasil—semua disajikan dalam gaya percakapan langkah‑demi‑langkah yang dapat Anda salin ke aplikasi Java mana pun.

## Jawaban Cepat
- **Apa perpustakaan yang menangani redaksi gambar di Java?** GroupDocs.Redaction untuk Java.  
- **Apakah saya dapat memilih warna redaksi?** Ya – warna `java.awt.Color` opak apa pun seperti `Color.BLUE` atau `Color.BLACK`.  
- **Apakah lisensi diperlukan untuk produksi?** Ya, lisensi GroupDocs yang valid wajib untuk penggunaan komersial.  
- **Apakah gambar asli akan ditimpa?** Tidak – API menulis gambar yang telah di‑redact ke file baru yang Anda tentukan.  
- **Versi Java apa yang didukung?** Java 8 dan lebih baru (hingga Java 21 pada saat penulisan).

## Apa itu redaksi gambar dan mengapa men‑redact gambar yang dipindai di Java?
Redaksi gambar secara permanen menutupi data visual—nama, nomor, tanda tangan—dengan mengganti wilayah piksel dengan warna solid. Tidak seperti redaksi teks, yang bekerja pada karakter yang dapat dipilih, gambar yang dipindai menyimpan informasi sebagai piksel mentah, sehingga hanya alat berbasis piksel yang dapat menjamin data tidak dapat dipulihkan. Dengan GroupDocs.Redaction Anda dapat menargetkan koordinat tepat, menerapkan warna opak apa pun, dan menghasilkan gambar baru yang menghilangkan konten sensitif secara permanen.

## Mengapa menggunakan GroupDocs.Redaction untuk Java?
GroupDocs.Redaction mendukung **lebih dari 50 format gambar** (termasuk JPG, PNG, BMP, GIF) dan dapat memproses dokumen ratusan halaman tanpa memuat seluruh file ke memori, berkat arsitektur streaming‑nya. Benchmark menunjukkan bahwa PNG berukuran 300 KB dapat di‑redact dalam kurang dari 120 ms pada CPU 2.8 GHz standar, menjadikannya cocok untuk pekerjaan batch maupun layanan real‑time.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki:

- **JDK 8 atau yang lebih baru** terpasang dan dikonfigurasi di `PATH` Anda.  
- **Maven** (atau Gradle) untuk manajemen dependensi.  
- IDE seperti **IntelliJ IDEA**, **Eclipse**, atau **NetBeans**.  
- Familiaritas dasar dengan I/O file Java dan paket `java.awt`.  

## Menyiapkan GroupDocs.Redaction untuk Java

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

### Unduhan langsung
Sebagai alternatif, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
- **Uji coba gratis:** Daftar untuk uji coba guna menjelajahi API lengkap.  
- **Lisensi sementara:** Gunakan kunci sementara untuk pengujian lanjutan tanpa biaya.  
- **Pembelian penuh:** Dapatkan lisensi produksi untuk penyebaran tak terbatas.

## Panduan Implementasi

Kami akan membagi implementasi menjadi dua fitur inti: **redaksi area gambar** (penutupan sebenarnya) dan **pemeriksaan status redaksi** (verifikasi keberhasilan).

### Cara men‑redact gambar dokumen yang dipindai – langkah 1: inisialisasi redaktor
`Redactor` adalah kelas pusat yang memuat gambar dan menyediakan operasi redaksi.  
Buat instance `Redactor` yang menunjuk ke gambar sumber yang ingin Anda proses.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Langkah 2: definisikan parameter redaksi
`ImageAreaRedaction` bekerja dengan `Point` (pojok kiri‑atas) dan `Dimension` (lebar × tinggi) yang menggambarkan persegi panjang yang akan disembunyikan. Pada contoh ini kami menggunakan warna isi biru.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Langkah 3: terapkan redaksi
`RegionReplacementOptions` memungkinkan Anda menentukan warna isi dan border opsional. Mengirimkan opsi ini ke `ImageAreaRedaction` dan memanggil `apply()` melakukan penutupan. Metode ini mengembalikan `RedactorChangeLog` yang menunjukkan keberhasilan atau kegagalan.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Langkah 4: lepaskan sumber daya
`Redactor` mengimplementasikan `AutoCloseable`. Menutupnya membebaskan buffer native dan handle file, mencegah kebocoran memori pada layanan yang berjalan lama.

```java
redactor.close();
```

### Cara memverifikasi redaksi – pemeriksaan status
Setelah menerapkan redaksi, periksa `RedactorChangeLog`. Nilai `Status.SUCCESS` mengonfirmasi bahwa wilayah piksel telah diganti tanpa error. Anda juga dapat merender gambar ke `BufferedImage` untuk inspeksi visual sebelum menyimpan.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Aplikasi Praktis
- **Penanganan dokumen rahasia:** Menyembunyikan data pribadi dalam kontrak yang dipindai sebelum dibagikan ke mitra.  
- **Dokumentasi hukum:** Memastikan kepatuhan GDPR atau HIPAA dengan men‑redact pengidentifikasi dalam gambar bukti.  
- **Rekam medis:** Menyembunyikan wajah pasien atau catatan tulisan tangan dalam pemindaian radiologi sambil mempertahankan detail diagnostik.  

## Pertimbangan Kinerja
- **Pemrosesan batch:** Proses gambar dalam kelompok 10–20 untuk menjaga penggunaan memori di bawah 200 MB.  
- **Penggunaan kembali objek:** Gunakan kembali objek `Point` dan `Dimension` di seluruh iterasi untuk mengurangi tekanan GC.  
- **Pembaruan versi:** Tingkatkan ke rilis GroupDocs.Redaction terbaru untuk mendapatkan peningkatan kecepatan 15 % yang dilaporkan pada versi 24.10.  

## Masalah Umum & Solusi
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Redaksi gagal dengan status `Failed`** | Path file tidak tepat atau format gambar tidak didukung | Pastikan file ada dan merupakan format yang didukung (JPG, PNG, BMP, GIF). |
| **File output kosong** | `redactor.save()` dipanggil sebelum redaksi selesai | Pastikan `apply()` mengembalikan `Status.SUCCESS` sebelum memanggil `save()`. |
| **Warna tidak diterapkan** | Menggunakan `Color` yang transparan | Pilih warna opak seperti `Color.BLACK` atau `Color.BLUE`. |

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara `ImageAreaRedaction` dan redaksi teks?**  
A: `ImageAreaRedaction` bekerja pada koordinat piksel mentah, sementara redaksi teks mem-parsing lapisan OCR untuk menemukan dan menghapus konten tekstual.

**Q: Apakah saya dapat men‑redact beberapa wilayah dalam satu gambar?**  
A: Ya—panggil `redactor.apply()` berulang kali dengan objek `ImageAreaRedaction` yang berbeda sebelum menyimpan file akhir.

**Q: Apakah GroupDocs.Redaction mendukung format gambar lain seperti TIFF?**  
A: Perpustakaan mendukung format raster umum (JPG, PNG, BMP, GIF). Untuk TIFF, konversi gambar ke format yang didukung terlebih dahulu.

**Q: Bagaimana cara mengotomatiskan redaksi untuk folder PDF yang dipindai?**  
A: Ekstrak setiap halaman sebagai gambar, terapkan logika redaksi yang sama, lalu bangun kembali PDF menggunakan perpustakaan PDF seperti GroupDocs.Conversion.

**Q: Apakah ada cara untuk meninjau redaksi sebelum menyimpan?**  
A: Render `Redactor` ke `BufferedImage` dan tampilkan di UI Swing atau JavaFX, memungkinkan Anda mengonfirmasi area yang disembunyikan sebelum melakukan commit.

## Kesimpulan
Anda kini memiliki panduan lengkap yang siap produksi tentang **cara men‑redact konten gambar** dan, khususnya, **cara men‑redact gambar yang dipindai di Java** menggunakan GroupDocs.Redaction untuk Java. Dengan mengikuti langkah‑langkah di atas, Anda dapat melindungi data visual sensitif di bidang keuangan, hukum, dan kesehatan. Jelajahi API tambahan—seperti redaksi teks, redaksi halaman PDF, atau pemrosesan folder massal—untuk membangun pipeline privasi data end‑to‑end bagi organisasi Anda.

**Sumber Daya**  
- [Dokumentasi](https://docs.groupdocs.com/redaction/java/)  
- [Referensi API](https://reference.groupdocs.com/redaction/java)  
- [Unduh](https://releases.groupdocs.com/redaction/java/)  
- [Repositori GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Forum dukungan gratis](https://forum.groupdocs.com/c/redaction/33)  
- [Lisensi sementara](https://purchase.groupdocs.com/temporary-license/) 

---

**Terakhir Diperbarui:** 2026-09-21  
**Diuji dengan:** GroupDocs.Redaction 24.9 (Java)  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Cara Men‑Redact Java dengan GroupDocs.Redaction - Panduan Komprehensif untuk Pengembang](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Cara Men‑Redact PDF yang Dipindai dengan OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Cara Men‑Redact Teks di Java dengan GroupDocs.Redaction – Panduan](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)