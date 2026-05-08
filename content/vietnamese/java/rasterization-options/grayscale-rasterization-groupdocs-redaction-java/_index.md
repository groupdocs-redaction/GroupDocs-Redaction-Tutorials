---
date: '2026-02-13'
description: Tìm hiểu cách tạo PDF đen trắng bằng GroupDocs.Redaction cho Java, chuyển
  đổi PDF sang đen trắng một cách an toàn đồng thời bảo toàn chất lượng tài liệu.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: Cách tạo PDF đen trắng với GroupDocs.Redaction Java – Bảo mật và Tối ưu hóa
  tài liệu của bạn
type: docs
url: /vi/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

 etc.

**Tested With:** -> "**Kiểm tra với:**"

**Author:** -> "**Tác giả:**"

Now produce final markdown with translations.

Check we kept all placeholders.

Now produce final answer.# GroupDocs.Redaction Java: Hướng dẫn raster hóa thang xám

## Giới thiệu

Nếu bạn cần **tạo PDF thang xám** while keeping your documents safe and professional‑looking, you’ve come to the right place. In this tutorial we’ll walk through the exact steps to convert colorful DOCX, PDF, or other supported files into a clean, grayscale rasterized version using GroupDocs.Redaction for Java. You’ll learn why rasterization adds an extra security layer, how to configure the library, and how to manage resources efficiently—all in a conversational, step‑by‑step style.

## Câu trả lời nhanh
- **Grayscale rasterization làm gì?** It converts each page of a document into a high‑resolution image and then applies a grayscale filter, removing all color information.  
- **Tại sao nên sử dụng GroupDocs.Redaction cho việc này?** It combines redaction security with powerful rasterization options in a single API.  
- **Các định dạng nào được hỗ trợ?** DOCX, PDF, XLSX, PPTX, RTF and many more.  
- **Tôi có cần giấy phép không?** A valid GroupDocs.Redaction license is required for production use; a trial is available for testing.  
- **Phiên bản Java nào được yêu cầu?** JDK 8 or higher.

## **create grayscale pdf** là gì?

Creating a grayscale PDF means converting every visual element of the original document into shades of gray. The result is a smaller, print‑friendly file that eliminates color‑related distractions and adds a subtle security benefit because the content is now image‑based.

## Tại sao nên sử dụng raster hóa thang xám với GroupDocs.Redaction?

- **Enhanced security** – rasterized pages cannot be selected, copied, or edited as text.  
- **Consistent appearance** – colors are stripped, giving a uniform, professional look.  
- **Broad format support** – the same API works for DOCX, PDF, PPTX, and more.  
- **Fine‑tuned control** – you can adjust DPI, output format, and advanced options such as grayscale conversion.

## Yêu cầu trước

- Java Development Kit (JDK) 8 hoặc mới hơn. Verify with `java -version`.  
- Một IDE (IntelliJ IDEA, Eclipse hoặc NetBeans) for easier coding and debugging.  
- GroupDocs.Redaction for Java added via Maven or Gradle.  
- Một tài liệu mẫu (ví dụ: a multi‑page DOCX) that you can safely experiment on.  
- Đủ không gian đĩa cho đầu ra raster (raster files can be larger than the source).

## Nhập các gói

Setting up the right imports is like organizing your toolbox before a project. The following imports give you access to the core Redactor class and the rasterization options we’ll need.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Bước 1: Khởi tạo đối tượng Redactor

Creating a `Redactor` instance opens the door to all document‑processing capabilities.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Thay thế `Constants.MULTIPAGE_SAMPLE_DOCX` bằng đường dẫn tới tệp bạn muốn chuyển đổi thành PDF thang xám.

## Bước 2: Cấu hình tùy chọn lưu

`SaveOptions` defines how the final file will be written. Adding a suffix helps you keep the original file intact.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Đầu ra sẽ được đặt tên là `yourfile_scan.docx` (or the format you later specify).

## Bước 3: Bật rasterization

Turning on rasterization tells the engine to render each page as an image before saving.

```java
so.getRasterization().setEnabled(true);
```

Rasterization is the foundation for creating a grayscale PDF because it converts the document into an image‑based representation.

## Bước 4: Áp dụng chuyển đổi thang xám

Now we add the grayscale filter to the rasterization pipeline.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

This option forces every pixel to be rendered in shades of gray, giving you the **create grayscale pdf** result you’re after.

## Bước 5: Thực thi chuyển đổi tài liệu

The `save` call runs the entire processing chain.

```java
redactor.save(so);
```

After this line executes, you’ll find a new file on disk that is fully rasterized, grayscale, and saved with the `_scan` suffix.

## Bước 6: Quản lý tài nguyên đúng cách

Cleaning up resources prevents file locks and memory leaks.

```java
finally { redactor.close(); }
```

For modern Java you can also use the try‑with‑resources pattern, which automatically closes the `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Both approaches are safe; the latter is more concise.

## Các tùy chọn cấu hình nâng cao

### Điều chỉnh DPI cho chất lượng hoặc kích thước

Higher DPI yields sharper images (good for printing), while lower DPI reduces file size.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Chọn định dạng đầu ra

You can force the rasterized result into a specific container format, such as PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Các trường hợp sử dụng phổ biến

- **Legal document archiving** – tạo immutable grayscale PDFs that cannot be edited.  
- **Print‑ready reports** – ensure consistent black‑and‑white output for bulk printing.  
- **Compliance workflows** – combine redaction with grayscale rasterization to meet strict data‑privacy regulations.

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| Tệp đầu ra lớn hơn mong đợi | DPI được đặt quá cao hoặc nén hình ảnh bị tắt | Giảm DPI (ví dụ: 150) hoặc bật nén trong `RasterizationOptions`. |
| Văn bản bị mờ | DPI không đủ cho kích thước phông chữ gốc | Tăng DPI lên 300 hoặc cao hơn. |
| Quá trình ném `OutOfMemoryError` trên tài liệu lớn | Toàn bộ tài liệu được tải vào bộ nhớ | Sử dụng API streaming hoặc xử lý các trang theo lô nếu được hỗ trợ. |
| Chưa áp dụng thang xám | Tùy chọn nâng cao không được thêm đúng cách | Kiểm tra `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` được gọi trước `save()`. |

## Câu hỏi thường gặp

**Q: Tôi có thể chuyển đổi tài liệu sang thang xám mà không rasterization không?**  
A: Trong GroupDocs.Redaction, tùy chọn thang xám gắn liền với rasterization, đảm bảo kết quả nhất quán và tăng bảo mật.

**Q: Các định dạng tài liệu nào hỗ trợ rasterization thang xám?**  
A: Tất cả các định dạng chính được GroupDocs.Redaction hỗ trợ — bao gồm DOCX, PDF, XLSX, PPTX, RTF và nhiều hơn nữa — có thể được raster và chuyển sang thang xám.

**Q: Rasterization có ảnh hưởng đến kích thước tệp của tài liệu không?**  
A: Có. Các tệp chứa nhiều văn bản có thể tăng kích thước, trong khi các tệp chứa nhiều hình ảnh có thể giảm. Cài đặt DPI có ảnh hưởng lớn nhất.

**Q: Có thể đảo ngược quá trình rasterization thang xám không?**  
A: Không. Rasterization là một chiều; hãy giữ bản sao lưu của tệp gốc nếu cần khôi phục.

**Q: Làm thế nào tôi có thể tối ưu chất lượng của tài liệu rasterized thang xám?**  
A: Sử dụng DPI cao hơn (300 + cho chất lượng in) và chọn định dạng đầu ra phù hợp (PDF thường được dùng cho lưu trữ).

## Kết luận

You now have a complete, production‑ready recipe to **create grayscale pdf** files using GroupDocs.Redaction for Java. By enabling rasterization, adding the grayscale advanced option, and managing resources responsibly, you can produce secure, print‑friendly documents that meet compliance standards.

---

**Cập nhật lần cuối:** 2026-02-13  
**Kiểm tra với:** GroupDocs.Redaction 23.11 for Java  
**Tác giả:** GroupDocs