---
date: '2026-06-26'
description: Tìm hiểu cách trích xuất văn bản từ PDF đã quét và che dấu dữ liệu nhạy
  cảm bằng GroupDocs OCR Redaction với Azure OCR. Che dấu social security number và
  thay thế thông tin bí mật trong PDF một cách hiệu quả.
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
title: Trích xuất văn bản từ PDF đã quét – Che dấu dữ liệu với GroupDocs OCR
type: docs
url: /vi/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Trích xuất văn bản từ PDF đã quét – Che giấu dữ liệu với GroupDocs OCR

Trong thế giới hiện đại dựa trên dữ liệu, **việc trích xuất văn bản từ các tệp PDF đã quét** và che giấu thông tin mật là một bước tuân thủ không thể bỏ qua. Hướng dẫn này sẽ chỉ cho bạn cách sử dụng GroupDocs Redaction kết hợp với Microsoft Azure OCR để nhận diện một cách đáng tin cậy văn bản ẩn trên các trang quét và thay thế nó bằng một placeholder an toàn như **`[REDACTED]`**. Bạn sẽ thấy tại sao sự kết hợp này nhanh, chính xác và sẵn sàng cho các khối lượng công việc cấp sản xuất.

## Câu trả lời nhanh
- **“Che giấu dữ liệu nhạy cảm” có nghĩa là gì?** Nó thay thế văn bản mật đã được xác định bằng một placeholder (ví dụ, `[REDACTED]`).  
- **Thư viện nào xử lý OCR?** Kết nối Microsoft Azure OCR, được sử dụng thông qua GroupDocs Redaction.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép vĩnh viễn cần thiết cho môi trường sản xuất.  
- **Tôi có thể redact các PDF đã quét không?** Có — OCR trích xuất văn bản ẩn trước khi áp dụng các redaction bằng regex.  
- **Giải pháp này chỉ dành cho Java?** Ví dụ dựa trên Java, nhưng GroupDocs cung cấp các API tương tự cho .NET và các nền tảng khác.

## Redaction dựa trên OCR là gì?
Redaction dựa trên OCR đầu tiên thực hiện OCR trên mỗi trang, chuyển hình ảnh thành văn bản có thể tìm kiếm, sau đó áp dụng các mẫu regex để thay thế các kết quả khớp bằng một mask như `[REDACTED]`. Quy trình hai bước này cho phép bạn che giấu dữ liệu cá nhân một cách đáng tin cậy ngay cả trong các PDF đã quét, đảm bảo mọi chuỗi nhạy cảm được loại bỏ trước khi tài liệu được chia sẻ hoặc lưu trữ.

## Tại sao nên sử dụng GroupDocs Redaction với Azure OCR?
Bạn nên sử dụng GroupDocs Redaction với Azure OCR vì nó cung cấp **độ chính xác OCR >98 % trên văn bản in**, hỗ trợ **hơn 50 định dạng đầu vào và đầu ra**, và có thể xử lý **các PDF hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ**, đảm bảo việc redaction nhanh chóng và mở rộng cho mục tiêu tuân thủ. Giải pháp cũng **có khả năng xử lý một PDF 1.000 trang trong vòng dưới 2 phút trên máy chủ 8 nhân**, làm cho các công việc batch trở nên thực tế.

## Yêu cầu trước
- **Java Development Kit (JDK) 8+** đã được cài đặt.  
- **Maven** (nếu bạn thích quản lý phụ thuộc) hoặc khả năng tải JAR thủ công.  
- **Thông tin xác thực Microsoft Azure OCR** (endpoint và subscription key).  
- Kiến thức cơ bản về Java và quen thuộc với các biểu thức chính quy.

## Cài đặt GroupDocs Redaction cho Java

### Cài đặt Maven
Thêm repository và dependency của GroupDocs vào file `pom.xml` của bạn:

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

### Tải xuống trực tiếp
Nếu bạn muốn quản lý JAR thủ công, tải bản phát hành mới nhất từ [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Nhận giấy phép
- **Bản dùng thử miễn phí** – khám phá tất cả tính năng mà không tốn phí.  
- **Giấy phép tạm thời** – kéo dài thời gian đánh giá.  
- **Giấy phép đầy đủ** – mở khóa các khả năng sẵn sàng cho sản xuất.

### Khởi tạo và Cài đặt Cơ bản
Lớp `Redactor` là động cơ cốt lõi thực hiện việc trích xuất OCR và áp dụng các quy tắc redaction lên tài liệu PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Cách che giấu dữ liệu nhạy cảm với OCR Redaction
Việc che giấu dữ liệu nhạy cảm với OCR Redaction bao gồm tải PDF với cài đặt Azure OCR, định nghĩa các mẫu regex cho dữ liệu bạn muốn ẩn, và gọi Redactor để thay thế mỗi kết quả khớp bằng một placeholder như `[REDACTED]`. Thư viện xử lý OCR, khớp mẫu và ghi lại PDF trong một quy trình duy nhất.

### Bước 1: Tải tài liệu với cài đặt OCR
`LoadOptions` cấu hình cách GroupDocs tải một tệp, cho phép bạn truyền các kết nối OCR như Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – thay thế bằng đường dẫn tới PDF của bạn.  
- **`settings`** – chứa kết nối Azure OCR mà bạn đã tạo trước đó.

### Bước 2: Định nghĩa và Áp dụng Redaction bằng Regex
`ReplacementOptions` chỉ định văn bản thay thế sẽ thay thế mỗi kết quả khớp regex trong quá trình redaction.  
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
- Mẫu `\b\d{3}-\d{2}-\d{4}\b` khớp với Số An sinh Xã hội (Social Security Number) của Hoa Kỳ.  
- `ReplacementOptions("[REDACTED]")` thay thế mỗi kết quả khớp bằng mask, thực tế **che giấu dữ liệu nhạy cảm**.

## Các trường hợp sử dụng phổ biến cho việc che giấu dữ liệu nhạy cảm
1. **Quản lý tài liệu pháp lý** – ẩn các định danh khách hàng trước khi chia sẻ bản nháp.  
2. **Báo cáo tài chính** – bảo vệ số tài khoản và ID giao dịch.  
3. **Hồ sơ y tế** – tuân thủ HIPAA bằng cách redaction các định danh bệnh nhân.  
4. **Ấn phẩm chính phủ** – loại bỏ dữ liệu cá nhân khỏi hồ sơ công cộng.  
5. **Hợp đồng doanh nghiệp** – giấu các điều khoản sở hữu trong quá trình đánh giá bên ngoài.

## Mẹo hiệu năng
- **Tối ưu regex** – tránh các mẫu quá rộng gây tăng thời gian xử lý; các biểu thức được thiết kế tốt có thể giảm thời gian chạy lên tới 40 %.  
- **Quản lý bộ nhớ** – đóng nhanh instance `Redactor` (try‑with‑resources tự động thực hiện việc này).  
- **Thực thi bất đồng bộ** – cho xử lý hàng loạt, chạy các job redaction trên các luồng riêng hoặc sử dụng hàng đợi tác vụ để giữ UI phản hồi.

## Khắc phục sự cố
- **Lỗi thông tin xác thực Azure** – kiểm tra lại URL endpoint và subscription key trong `MicrosoftAzureOcrConnector`.  
- **Tài liệu không tải** – xác minh đường dẫn tệp và đảm bảo PDF không được bảo vệ bằng mật khẩu (hoặc cung cấp mật khẩu qua `LoadOptions`).  
- **Không có redaction nào được áp dụng** – thử regex của bạn với một chuỗi đơn giản trước; sử dụng `Pattern.compile` trong unit test để xác nhận các khớp.

## Câu hỏi thường gặp

**Hỏi: OCR redaction là gì?**  
**Đáp:** OCR redaction sử dụng Nhận dạng ký tự quang học (Optical Character Recognition) để trích xuất văn bản ẩn từ hình ảnh hoặc PDF đã quét, sau đó áp dụng các quy tắc redaction để che giấu văn bản đó.

**Hỏi: Tôi có thể sử dụng GroupDocs Redaction mà không cần Azure OCR không?**  
**Đáp:** Có, nhưng OCR cải thiện đáng kể độ chính xác trên các tài liệu đã quét nơi việc trích xuất văn bản gốc thất bại.

**Hỏi: Làm thế nào để xử lý các mẫu regex phức tạp?**  
**Đáp:** Xây dựng và kiểm tra chúng từng bước, sử dụng lớp `Pattern` của Java trong môi trường sandbox trước khi áp dụng vào tài liệu lớn.

**Hỏi: Các nút thắt hiệu năng thường gặp là gì?**  
**Đáp:** PDF lớn, regex quá phức tạp và các cuộc gọi OCR đồng bộ có thể làm chậm quá trình; hãy cân nhắc xử lý batch và các mẫu được tối ưu.

**Hỏi: Có hỗ trợ cho các vấn đề triển khai không?**  
**Đáp:** Chắc chắn—liên hệ qua [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) để nhận trợ giúp cộng đồng hoặc liên hệ bộ phận hỗ trợ của GroupDocs.

## Tài nguyên bổ sung
- **Tài liệu**: https://docs.groupdocs.com/redaction/java/  
- **Tham chiếu API**: https://reference.groupdocs.com/redaction/java  
- **Tải xuống**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Hỗ trợ miễn phí**: https://forum.groupdocs.com/c/redaction/33  
- **Giấy phép tạm thời**: https://purchase.groupdocs.com/temporary-license/

---

**Cập nhật lần cuối:** 2026-06-26  
**Đã kiểm tra với:** GroupDocs.Redaction 24.9 (Java)  
**Tác giả:** GroupDocs  

---

## Hướng dẫn liên quan

- [Redaction PDF an toàn bằng OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Cách Redact Văn bản với GroupDocs.Redaction cho Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Che giấu dữ liệu nhạy cảm Java – Redact Thông tin cá nhân với GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)