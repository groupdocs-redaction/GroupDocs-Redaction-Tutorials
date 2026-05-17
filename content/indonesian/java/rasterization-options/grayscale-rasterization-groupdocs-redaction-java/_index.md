---
date: '2026-05-17'
description: Pelajari cara merasterkan PDF ke skala abu-abu menggunakan GroupDocs.Redaction
  untuk Java, terapkan filter skala abu-abu, dan jaga dokumen Anda tetap aman serta
  berkualitas tinggi.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Cara merasterkan PDF ke skala abu-abu dengan GroupDocs.Redaction Java – Amankan
  dan Optimalkan Dokumen Anda
type: docs
url: /id/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Cara meraster PDF ke grayscale dengan GroupDocs.Redaction Java

Jika Anda perlu **meraster PDF** ke grayscale sambil menjaga dokumen Anda tetap aman, tampak profesional, dan mudah diarsipkan, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk mengonversi DOCX, PDF, atau file lain yang didukung yang berwarna menjadi versi rasterized grayscale yang bersih menggunakan GroupDocs.Redaction untuk Java. Anda akan memahami mengapa rasterisasi menambahkan lapisan keamanan, cara mengonfigurasi perpustakaan, dan cara mengelola sumber daya secara efisien—semua disajikan dalam gaya yang ramah, langkah demi langkah.

## Jawaban Cepat
- **Apa yang dilakukan rasterisasi grayscale?** Itu mengonversi setiap halaman menjadi gambar beresolusi tinggi dan kemudian menerapkan filter grayscale, menghapus semua informasi warna.  
- **Mengapa menggunakan GroupDocs.Redaction untuk ini?** Ini menggabungkan keamanan redaksi dengan opsi rasterisasi dalam satu API yang mudah digunakan.  
- **Format apa yang didukung?** DOCX, PDF, XLSX, PPTX, RTF, dan lebih dari 100 format lainnya.  
- **Apakah saya memerlukan lisensi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk produksi; percobaan gratis tersedia untuk pengujian.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.

## Cara meraster PDF ke grayscale?

Muat dokumen sumber Anda dengan `new Redactor("path/to/file")`, aktifkan rasterisasi melalui `RasterizationOptions`, tambahkan opsi lanjutan grayscale, dan panggil `save()`—seluruh konversi terjadi dalam beberapa baris singkat. Pendekatan ini menjamin setiap halaman menjadi PDF berbasis gambar, hitam‑putih, mencegah pemilihan teks, dan memastikan tampilan siap cetak yang seragam.

## Apa itu **create grayscale pdf**?

Membuat PDF grayscale berarti mengonversi setiap elemen visual dari dokumen asli menjadi nuansa abu‑abu. Hasilnya adalah file yang lebih kecil, ramah cetak, yang menghilangkan gangguan terkait warna dan menambahkan manfaat keamanan halus karena kontennya kini berbasis gambar.

## Mengapa menggunakan rasterisasi grayscale dengan GroupDocs.Redaction?

Rasterisasi mengubah setiap halaman menjadi gambar, yang berarti teks tidak dapat disalin atau diedit, dan output visual tetap konsisten di semua printer dan penampil. GroupDocs.Redaction mendukung **lebih dari 100 format input dan output**—termasuk DOCX, XLSX, PPTX, HTML, dan tipe gambar—sehingga Anda dapat menerapkan alur kerja yang sama pada hampir semua dokumen yang Anda tangani.

## Prasyarat

- Java Development Kit (JDK) 8 atau yang lebih baru. Verifikasi dengan `java -version`.  
- Sebuah IDE (IntelliJ IDEA, Eclipse, atau NetBeans) untuk memudahkan penulisan kode dan debugging.  
- GroupDocs.Redaction untuk Java yang ditambahkan melalui Maven atau Gradle.  
- Dokumen contoh (misalnya, DOCX multi‑halaman) yang dapat Anda coba dengan aman.  
- Ruang disk yang cukup untuk output rasterized (file raster dapat lebih besar daripada sumber).

## Impor Paket

Impor berikut membawa kelas inti Redactor dan rasterisasi yang diperlukan untuk contoh.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Langkah 1: Inisialisasi Objek Redactor

Kelas `Redactor` adalah titik masuk untuk semua operasi pemrosesan dokumen di GroupDocs.Redaction. Membuat sebuah instance membuka pintu untuk memuat, mengedit, dan menyimpan dokumen.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Ganti `Constants.MULTIPAGE_SAMPLE_DOCX` dengan jalur ke file yang ingin Anda konversi menjadi PDF grayscale.

## Langkah 2: Konfigurasi Opsi Penyimpanan

Kelas `SaveOptions` menentukan bagaimana dokumen yang diproses akan ditulis ke disk, termasuk format dan nama file.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Output akan diberi nama `yourfile_scan.pdf` (atau format yang Anda tentukan kemudian).

## Langkah 3: Aktifkan Rasterisasi

Objek `RasterizationOptions` mengaktifkan rendering berbasis gambar untuk setiap halaman sebelum disimpan.

```java
so.getRasterization().setEnabled(true);
```

## Langkah 4: Terapkan Konversi Grayscale

`AdvancedRasterizationOptions.Grayscale` adalah flag yang memaksa gambar rasterized menggunakan hanya nuansa abu‑abu.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Langkah 5: Jalankan Transformasi Dokumen

Memanggil `save()` menjalankan seluruh pipeline pemrosesan dan menulis file output.

```java
redactor.save(so);
```

Setelah baris ini dijalankan, Anda akan menemukan file baru di disk yang sepenuhnya rasterized, grayscale, dan disimpan dengan akhiran `_scan`.

## Langkah 6: Manajemen Sumber Daya yang Tepat

Metode `close()` melepaskan sumber daya native dan menghapus file sementara.

```java
finally { redactor.close(); }
```

Untuk Java modern Anda juga dapat menggunakan pola try‑with‑resources, yang secara otomatis menutup `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Kedua pendekatan aman; yang terakhir lebih ringkas.

## Opsi Konfigurasi Lanjutan

### Sesuaikan DPI untuk Kualitas atau Ukuran

DPI yang lebih tinggi menghasilkan gambar lebih tajam (baik untuk pencetakan), sementara DPI yang lebih rendah mengurangi ukuran file. Keseimbangan umum adalah 150 DPI untuk tampilan di layar dan 300 DPI untuk PDF siap cetak.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Pilih Format Output

Anda dapat memaksa hasil rasterized ke dalam format kontainer tertentu, seperti PDF, TIFF, atau PNG. PDF adalah format arsip yang paling banyak digunakan.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Kasus Penggunaan Umum

- **Pengarsipan dokumen hukum** – buat PDF grayscale yang tidak dapat diubah.  
- **Laporan siap cetak** – pastikan output hitam‑putih yang konsisten untuk pencetakan massal.  
- **Alur kerja kepatuhan** – gabungkan redaksi dengan rasterisasi grayscale untuk memenuhi regulasi privasi data yang ketat.

## Masalah Umum dan Solusinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| File output lebih besar dari yang diharapkan | DPI diatur terlalu tinggi atau kompresi gambar dinonaktifkan | Turunkan DPI (mis., 150) atau aktifkan kompresi di `RasterizationOptions`. |
| Teks terlihat buram | DPI tidak cukup untuk ukuran font asli | Tingkatkan DPI ke 300 atau lebih tinggi. |
| Proses melempar `OutOfMemoryError` pada dokumen besar | Seluruh dokumen dimuat ke memori | Gunakan API streaming atau proses halaman secara batch jika didukung. |
| Grayscale tidak diterapkan | Opsi lanjutan tidak ditambahkan dengan benar | Pastikan `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` dipanggil sebelum `save()`. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengonversi dokumen ke grayscale tanpa rasterisasi?**  
A: Di GroupDocs.Redaction, opsi grayscale terikat pada rasterisasi, yang memastikan hasil konsisten dan menambahkan lapisan keamanan.

**Q: Format dokumen apa yang mendukung rasterisasi grayscale?**  
A: Semua format utama yang didukung oleh GroupDocs.Redaction—termasuk DOCX, PDF, XLSX, PPTX, RTF, dan lebih dari 100 lainnya—dapat dirasterisasi dan dikonversi ke grayscale.

**Q: Apakah rasterisasi memengaruhi ukuran file dokumen saya?**  
A: Ya. File yang banyak teks dapat menjadi lebih besar, sementara file yang banyak gambar mungkin menyusut. Pengaturan DPI memiliki dampak terbesar.

**Q: Apakah memungkinkan untuk membalik proses rasterisasi grayscale?**  
A: Tidak. Rasterisasi bersifat satu arah; simpan cadangan dokumen asli jika Anda perlu mengembalikannya.

**Q: Bagaimana saya dapat mengoptimalkan kualitas dokumen rasterized grayscale?**  
A: Gunakan DPI yang lebih tinggi (300 + untuk kualitas cetak) dan pilih PDF sebagai format output untuk hasil arsip terbaik.

## Kesimpulan

Anda kini memiliki resep lengkap yang siap produksi untuk **meraster PDF ke grayscale** menggunakan GroupDocs.Redaction untuk Java. Dengan mengaktifkan rasterisasi, menambahkan opsi lanjutan grayscale, dan mengelola sumber daya secara bertanggung jawab, Anda dapat menghasilkan dokumen yang aman, ramah cetak, yang memenuhi standar kepatuhan dan tampak konsisten di semua penampil.

---

**Terakhir Diperbarui:** 2026-05-17  
**Diuji Dengan:** GroupDocs.Redaction 23.11 for Java  
**Penulis:** GroupDocs  

## KATA KUNCI TARGET:

**Kata Kunci Utama (PRIORITAS TERTINGGI):** how to rasterize pdf

**Kata Kunci Sekunder (MENDUKUNG):** java pdf to image, apply grayscale filter pdf

## Tutorial Terkait

- [Tutorial Opsi Rasterisasi untuk GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Cara menggunakan groupdocs redaction untuk Java: Pra‑Rasterisasi dalam Dokumen Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Rasterisasi Noise Kustom di Java&#58; Amankan Informasi Sensitif dengan GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)