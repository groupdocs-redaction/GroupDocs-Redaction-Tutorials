---
date: '2026-03-22'
description: Pelajari cara menyensor gambar hasil pemindaian di Java dengan GroupDocs.Redaction.
  Panduan langkah demi langkah ini mencakup penyiapan, penyensoran area gambar, dan
  verifikasi.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: Cara menyensor gambar yang dipindai menggunakan Java dengan GroupDocs
type: docs
url: /id/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Cara men‑redact gambar hasil scan java menggunakan GroupDocs

Dalam lanskap digital saat ini, **redact scanned image java** sangat penting untuk melindungi privasi dan memenuhi persyaratan kepatuhan. Baik Anda perlu menyembunyikan data pribadi dalam kontrak yang dipindai atau menyamarkan detail pasien dalam gambar medis, tutorial ini menunjukkan **cara men‑redact gambar** dengan cepat dan dapat diandalkan menggunakan **GroupDocs.Redaction for Java**. Kami akan membahas semuanya mulai dari penyiapan proyek hingga memverifikasi bahwa redaction berhasil, sehingga Anda dapat mengintegrasikan solusi ini ke dalam aplikasi Java apa pun dengan percaya diri.

## Jawaban Cepat
- **Perpustakaan apa yang menangani redaction gambar di Java?** GroupDocs.Redaction for Java  
- **Apakah saya dapat memilih warna redaction?** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **Apakah lisensi diperlukan untuk produksi?** Yes, a valid GroupDocs license is needed  
- **Apakah gambar asli akan ditimpa?** No – you save the result to a new file  
- **Versi Java apa yang didukung?** Java 8+ (compatible with modern JDKs)

## Apa itu redaction gambar dan mengapa men‑redact scanned image java?
Redaction gambar berarti secara permanen menyamarkan informasi visual sensitif—seperti nama, nomor, atau tanda tangan—sehingga tidak dapat dipulihkan. Ketika Anda bekerja dengan dokumen yang dipindai, data tersemat sebagai piksel, membuat alat redaction teks tradisional tidak efektif. Menggunakan GroupDocs.Redaction memungkinkan Anda menargetkan wilayah piksel yang tepat dan menggantinya dengan warna solid, memastikan informasi benar‑benar dihapus.

## Prasyarat
- **JDK 8 atau lebih baru** terpasang  
- **Maven** (atau alat build lain) untuk manajemen dependensi  
- IDE seperti **IntelliJ IDEA**, **Eclipse**, atau **NetBeans**  
- Pengetahuan dasar Java dan familiaritas dengan file I/O  

## Menyiapkan GroupDocs.Redaction untuk Java

### Penyiapan Maven
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
Sebagai alternatif, unduh JAR terbaru dari halaman rilis resmi: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Akuisisi Lisensi
- **Free Trial:** Daftar untuk percobaan guna menjelajahi API.  
- **Temporary License:** Gunakan kunci sementara untuk pengujian yang lebih lama.  
- **Full Purchase:** Dapatkan lisensi produksi untuk penggunaan tak terbatas.  

## Panduan Implementasi
Kami akan membagi implementasi menjadi dua fitur inti: **Image Area Redaction** (penyembunyian sebenarnya) dan **Redaction Status Check** (memverifikasi keberhasilan).

### Cara men‑redact gambar dokumen yang dipindai – Langkah 1: Inisialisasi Redactor
Pertama, buat instance `Redactor` yang menunjuk ke gambar yang ingin Anda proses.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Langkah 2: Tentukan Parameter Redaction
Tentukan sudut kiri‑atas (`Point`) dan ukuran (`Dimension`) dari persegi panjang yang ingin Anda sembunyikan. Pada contoh ini kami menggunakan isi biru.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Langkah 3: Terapkan Redaction
Buat objek `ImageAreaRedaction` dengan `RegionReplacementOptions` dan jalankan. Metode ini mengembalikan `RedactorChangeLog` yang memberi tahu Anda apakah operasi berhasil.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Langkah 4: Lepaskan Sumber Daya
Selalu tutup `Redactor` setelah selesai untuk membebaskan sumber daya native.

```java
redactor.close();
```

### Cara memverifikasi redaction – Pemeriksaan Status
Setelah menerapkan redaction, Anda dapat memeriksa `RedactorChangeLog` untuk memastikan bahwa operasi tidak gagal.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Aplikasi Praktis
- **Penanganan Dokumen Rahasia:** Secara otomatis menyamarkan data pribadi dalam kontrak yang dipindai sebelum dibagikan ke pihak eksternal.  
- **Dokumentasi Hukum:** Memastikan kepatuhan dengan GDPR atau HIPAA dengan men‑redact pengidentifikasi dalam gambar bukti.  
- **Rekam Medis:** Melindungi privasi pasien dengan menyamarkan wajah atau catatan tulisan tangan dalam gambar radiologi.  

## Pertimbangan Kinerja
- **Pemrosesan Batch:** Muat dan redacted gambar dalam batch kecil untuk menjaga penggunaan memori tetap rendah.  
- **Struktur Data Efisien:** Gunakan kembali objek `Point` dan `Dimension` saat memproses banyak gambar.  
- **Tetap Terbaru:** Secara rutin tingkatkan ke versi GroupDocs.Redaction terbaru untuk perbaikan kinerja dan perbaikan bug.  

## Masalah Umum & Solusi
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Redaction gagal dengan status `Failed`** | Path file tidak benar atau format gambar tidak didukung | Verifikasi bahwa gambar ada dan merupakan format yang didukung (JPG, PNG, BMP). |
| **File output kosong** | `redactor.save()` dipanggil sebelum redaction selesai | Pastikan `apply()` mengembalikan status berhasil sebelum menyimpan. |
| **Warna tidak diterapkan** | Menggunakan warna transparan | Pilih `Color` yang tidak tembus (misalnya `Color.BLACK` atau `Color.BLUE`). |

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara `ImageAreaRedaction` dan redaction teks?**  
A: `ImageAreaRedaction` bekerja pada koordinat piksel, sementara redaction teks mem‑parsing lapisan OCR untuk menemukan dan menghapus konten teks.

**Q: Bisakah saya men‑redact beberapa wilayah dalam satu gambar?**  
A: Ya—panggil `redactor.apply()` berulang kali dengan objek `ImageAreaRedaction` yang berbeda sebelum menyimpan.

**Q: Apakah GroupDocs.Redaction mendukung format gambar lain seperti TIFF?**  
A: Perpustakaan ini mendukung format raster umum (JPG, PNG, BMP, GIF). Untuk TIFF, konversi terlebih dahulu ke format yang didukung.

**Q: Bagaimana cara mengotomatisasi redaction untuk folder PDF yang dipindai?**  
A: Iterasi setiap gambar halaman yang diekstrak dari PDF, terapkan logika redaction yang sama, lalu bangun kembali PDF menggunakan perpustakaan PDF.

**Q: Apakah ada cara untuk melihat pratinjau redaction sebelum menyimpan?**  
A: Anda dapat merender `Redactor` ke `BufferedImage` dan menampilkannya di UI Swing atau JavaFX sebelum melakukan perubahan.

## Kesimpulan
Anda kini memiliki panduan lengkap yang siap produksi tentang **cara men‑redact gambar** dan, khususnya, **men‑redact scanned image java** menggunakan GroupDocs.Redaction untuk Java. Dengan mengikuti langkah‑langkah di atas, Anda dapat melindungi data visual sensitif di berbagai industri. Jelajahi API tambahan—seperti redaction teks atau redaction halaman PDF—untuk membangun solusi privasi data yang komprehensif bagi organisasi Anda.

**Sumber Daya**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Terakhir Diperbarui:** 2026-03-22  
**Diuji Dengan:** GroupDocs.Redaction 24.9 (Java)  
**Penulis:** GroupDocs