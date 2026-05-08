---
date: '2026-02-13'
description: Pelajari cara membuat PDF grayscale menggunakan GroupDocs.Redaction untuk
  Java, mengonversi PDF ke grayscale secara aman sambil mempertahankan kualitas dokumen.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: Cara membuat PDF grayscale dengan GroupDocs.Redaction Java – Amankan dan Optimalkan
  Dokumen Anda
type: docs
url: /id/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

 shortcodes: none.

Proceed.

# GroupDocs.Redaction Java: Panduan Rasterisasi Grayscale

## Introduction

Jika Anda perlu **membuat pdf grayscale** sambil menjaga dokumen tetap aman dan terlihat profesional, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas langkah‑langkah tepat untuk mengonversi DOCX, PDF, atau file lain yang didukung menjadi versi rasterized grayscale yang bersih menggunakan GroupDocs.Redaction untuk Java. Anda akan mempelajari mengapa rasterisasi menambahkan lapisan keamanan ekstra, cara mengonfigurasi pustaka, dan cara mengelola sumber daya secara efisien—semua dalam gaya percakapan langkah‑demi‑langkah.

## Quick Answers
- **Apa yang dilakukan rasterisasi grayscale?** Itu mengubah setiap halaman dokumen menjadi gambar beresolusi tinggi dan kemudian menerapkan filter grayscale, menghapus semua informasi warna.  
- **Mengapa menggunakan GroupDocs.Redaction untuk ini?** Ia menggabungkan keamanan redaksi dengan opsi rasterisasi yang kuat dalam satu API.  
- **Format apa saja yang didukung?** DOCX, PDF, XLSX, PPTX, RTF, dan banyak lagi.  
- **Apakah saya memerlukan lisensi?** Lisensi GroupDocs.Redaction yang valid diperlukan untuk penggunaan produksi; versi percobaan tersedia untuk pengujian.  
- **Versi Java apa yang diperlukan?** JDK 8 atau lebih tinggi.

## What is **create grayscale pdf**?

Membuat PDF grayscale berarti mengonversi setiap elemen visual dari dokumen asli menjadi nuansa abu‑abu. Hasilnya adalah file yang lebih kecil, ramah cetak, yang menghilangkan gangguan terkait warna dan menambahkan manfaat keamanan halus karena kontennya kini berbasis gambar.

## Why use grayscale rasterization with GroupDocs.Redaction?

- **Keamanan yang ditingkatkan** – halaman yang diraster tidak dapat dipilih, disalin, atau diedit sebagai teks.  
- **Penampilan konsisten** – warna dihilangkan, memberikan tampilan seragam dan profesional.  
- **Dukungan format luas** – API yang sama bekerja untuk DOCX, PDF, PPTX, dan lainnya.  
- **Kontrol yang disesuaikan** – Anda dapat mengatur DPI, format output, dan opsi lanjutan seperti konversi grayscale.

## Prerequisites

- Java Development Kit (JDK) 8 atau yang lebih baru. Verifikasi dengan `java -version`.  
- IDE (IntelliJ IDEA, Eclipse, atau NetBeans) untuk mempermudah penulisan kode dan debugging.  
- GroupDocs.Redaction untuk Java yang ditambahkan melalui Maven atau Gradle.  
- Dokumen contoh (misalnya, DOCX multi‑halaman) yang dapat Anda gunakan untuk bereksperimen secara aman.  
- Ruang disk yang cukup untuk output rasterized (file raster dapat lebih besar daripada sumber).

## Import Packages

Menyiapkan impor yang tepat seperti mengatur kotak perkakas sebelum memulai proyek. Impor berikut memberi Anda akses ke kelas Redactor inti dan opsi rasterisasi yang akan kita gunakan.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Step 1: Initialize the Redactor Object

Membuat instance `Redactor` membuka pintu ke semua kemampuan pemrosesan dokumen.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Ganti `Constants.MULTIPAGE_SAMPLE_DOCX` dengan path ke file yang ingin Anda konversi menjadi PDF grayscale.

## Step 2: Configure Save Options

`SaveOptions` menentukan bagaimana file akhir akan ditulis. Menambahkan akhiran membantu Anda menjaga file asli tetap utuh.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Output akan dinamai `yourfile_scan.docx` (atau format yang Anda tentukan kemudian).

## Step 3: Enable Rasterization

Mengaktifkan rasterisasi memberi tahu mesin untuk merender setiap halaman sebagai gambar sebelum disimpan.

```java
so.getRasterization().setEnabled(true);
```

Rasterisasi adalah dasar untuk membuat PDF grayscale karena mengubah dokumen menjadi representasi berbasis gambar.

## Step 4: Apply Grayscale Conversion

Sekarang kita menambahkan filter grayscale ke pipeline rasterisasi.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

Opsi ini memaksa setiap piksel dirender dalam nuansa abu‑abu, memberikan hasil **create grayscale pdf** yang Anda inginkan.

## Step 5: Execute the Document Transformation

Pemanggilan `save` menjalankan seluruh rantai pemrosesan.

```java
redactor.save(so);
```

Setelah baris ini dijalankan, Anda akan menemukan file baru di disk yang sepenuhnya diraster, grayscale, dan disimpan dengan akhiran `_scan`.

## Step 6: Proper Resource Management

Membersihkan sumber daya mencegah penguncian file dan kebocoran memori.

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

## Advanced Configuration Options

### Adjust DPI for Quality or Size

DPI yang lebih tinggi menghasilkan gambar lebih tajam (baik untuk pencetakan), sementara DPI yang lebih rendah mengurangi ukuran file.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Choose an Output Format

Anda dapat memaksa hasil rasterized ke format kontainer tertentu, seperti PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Common Use Cases

- **Arsip dokumen hukum** – buat PDF grayscale yang tidak dapat diubah.  
- **Laporan siap cetak** – pastikan output hitam‑putih yang konsisten untuk pencetakan massal.  
- **Alur kerja kepatuhan** – gabungkan redaksi dengan rasterisasi grayscale untuk memenuhi regulasi privasi data yang ketat.

## Common Issues and Solutions

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Output file is larger than expected | DPI set too high or image compression disabled | Lower DPI (e.g., 150) or enable compression in `RasterizationOptions`. |
| Text appears blurry | Insufficient DPI for the original font size | Increase DPI to 300 or higher. |
| Process throws `OutOfMemoryError` on large docs | Whole document loaded into memory | Use streaming APIs or process pages in batches if supported. |
| Grayscale not applied | Advanced option not added correctly | Verify `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` is called before `save()`. |

## Frequently Asked Questions

**Q: Can I convert documents to grayscale without rasterization?**  
A: In GroupDocs.Redaction, the grayscale option is tied to rasterization, which ensures consistent results and adds security.

**Q: What document formats support grayscale rasterization?**  
A: All major formats supported by GroupDocs.Redaction—including DOCX, PDF, XLSX, PPTX, RTF, and more—can be rasterized and converted to grayscale.

**Q: Will rasterization affect the file size of my documents?**  
A: Yes. Text‑heavy files may grow, while image‑heavy files might shrink. DPI settings have the biggest impact.

**Q: Is it possible to reverse the grayscale rasterization process?**  
A: No. Rasterization is one‑way; keep a backup of the original if you need to revert.

**Q: How can I optimize the quality of grayscale rasterized documents?**  
A: Use a higher DPI (300 + for print quality) and choose an appropriate output format (PDF is common for archival).

## Conclusion

Anda kini memiliki resep lengkap, siap produksi untuk **create grayscale pdf** menggunakan GroupDocs.Redaction untuk Java. Dengan mengaktifkan rasterisasi, menambahkan opsi lanjutan grayscale, dan mengelola sumber daya secara bertanggung jawab, Anda dapat menghasilkan dokumen yang aman, ramah cetak, dan memenuhi standar kepatuhan.

---

**Last Updated:** 2026-02-13  
**Tested With:** GroupDocs.Redaction 23.11 for Java  
**Author:** GroupDocs  

---