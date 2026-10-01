---
date: '2026-10-01'
description: Tìm hiểu cách xóa author metadata và lưu redacted document files trong
  Java bằng GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Tìm hiểu cách xóa author metadata và lưu redacted document files trong
  Java bằng GroupDocs Redaction. Thực hiện theo step‑by‑step guide.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Cách xóa author metadata trong Java với GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Cách xóa author metadata trong Java với GroupDocs
type: docs
url: /vi/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Cách xóa siêu dữ liệu tác giả trong Java với GroupDocs

Trong bối cảnh kỹ thuật số ngày nay, việc bảo vệ thông tin nhạy cảm ẩn trong tài liệu là một thực hành không thể thiếu. **Xóa siêu dữ liệu tác giả** ngăn ngừa việc tiết lộ vô tình các định danh cá nhân hoặc doanh nghiệp. Hướng dẫn này sẽ chỉ cho bạn, từng bước, cách sử dụng `EraseMetadataRedaction` từ GroupDocs.Redaction cho Java để loại bỏ các trường như *Author* và *Manager* khỏi các tệp Word, và sau đó **lưu các bản tài liệu đã xóa** một cách an toàn để chia sẻ hoặc lưu trữ.

## Câu trả lời nhanh
- **EraseMetadataRedaction làm gì?** Nó loại bỏ các trường siêu dữ liệu đã chọn khỏi tài liệu.  
- **Thư viện nào cung cấp tính năng này?** GroupDocs.Redaction for Java.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho việc thử nghiệm; giấy phép vĩnh viễn cần thiết cho môi trường sản xuất.  
- **Tôi có thể nhắm mục tiêu nhiều trường cùng lúc không?** Có, kết hợp các bộ lọc bằng toán tử OR logic.  
- **Quá trình có an toàn với đa luồng không?** Các đối tượng Redactor không được chia sẻ giữa các luồng; tạo một thể hiện mới cho mỗi thao tác.

## EraseMetadataRedaction là gì?
`EraseMetadataRedaction` là một lớp xóa nội dung tích hợp cho phép bạn chỉ định các mục siêu dữ liệu nào cần bị xóa. Nó hoạt động trên nhiều định dạng tài liệu được GroupDocs.Redaction hỗ trợ, đảm bảo thông tin tác giả ẩn không bao giờ bị rò rỉ. Bạn có thể nhắm mục tiêu các thuộc tính chuẩn như Author, Manager, và cả các trường siêu dữ liệu tùy chỉnh, cung cấp bảo vệ quyền riêng tư toàn diện.

## Tại sao nên sử dụng EraseMetadataRedaction với GroupDocs?
GroupDocs.Redaction hỗ trợ **hơn 100 định dạng đầu vào và đầu ra** và có thể xử lý tài liệu lên tới 500 trang mà không cần tải toàn bộ tệp vào bộ nhớ. Sử dụng lớp này cung cấp cho bạn một API duy nhất, hiệu suất cao để đáp ứng các yêu cầu tuân thủ GDPR, HIPAA, hoặc nội bộ, đồng thời giữ cho mã nguồn của bạn đơn giản.

## Yêu cầu trước
- Java 8 hoặc cao hơn đã được cài đặt.  
- Maven (hoặc khả năng thêm JAR thủ công).  
- GroupDocs.Redaction cho Java (phiên bản 24.9 hoặc mới hơn).  
- Một giấy phép dùng thử hoặc giấy phép vĩnh viễn hợp lệ của GroupDocs.

## Cài đặt GroupDocs.Redaction cho Java

### Cài đặt Maven
Add the GroupDocs repository and dependency to your **pom.xml**:

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

### Tải trực tiếp
Alternatively, download the latest JAR from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Nhận giấy phép
Lấy bản dùng thử miễn phí hoặc mua giấy phép tạm thời từ cổng thông tin GroupDocs. Tệp giấy phép nên được đặt ở vị trí mà ứng dụng của bạn có thể tải (ví dụ: gốc classpath).

### Khởi tạo và cấu hình cơ bản
Below is a minimal example that creates a `Redactor` instance for a DOCX file:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Cách sử dụng EraseMetadataRedaction trong Java
Các phần sau sẽ phân tích triển khai thành các bước rõ ràng, có thể thực hiện được.

### Tính năng: làm sạch các mục siêu dữ liệu cụ thể

#### Tổng quan
Chúng ta sẽ xóa các trường siêu dữ liệu **Author** và **Manager** bằng `EraseMetadataRedaction`. Đây là yêu cầu phổ biến khi chia sẻ báo cáo nội bộ với đối tác bên ngoài.

#### Triển khai từng bước

##### 1️⃣ Khởi tạo đối tượng Redactor
`Redactor` is the core class that loads a document, applies redaction objects, and writes the result. Create a new instance for each file you process:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Áp dụng EraseMetadataRedaction
`MetadataFilters` provides predefined filters for common metadata keys such as Author and Manager.  
`EraseMetadataRedaction` removes metadata entries that match the supplied `MetadataFilters`. The bitwise OR (`|`) combines the `Author` and `Manager` filters so both fields are removed in one call:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Cấu hình tùy chọn lưu
`SaveOptions` lets you specify the output file name, format, and other saving parameters.  
`SaveOptions` lets you control the output file name, format, and whether the document should be rasterized to PDF. Adding a suffix keeps the original file untouched:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Các trường hợp sử dụng phổ biến
1. **Legal documents** – Xóa thông tin tác giả trước khi gửi hợp đồng cho đối tác pháp lý.  
2. **Corporate reports** – Loại bỏ tên quản lý khi công bố kết quả quý cho cổ đông.  
3. **Project files** – Dọn dẹp tài liệu dự án nội bộ trước khi lưu trữ hoặc tải lên kho công cộng.

## Mẹo khắc phục sự cố
- **File not found** – Kiểm tra đường dẫn trong `inputFilePath` có trỏ tới tệp tồn tại và ứng dụng có quyền đọc hay không.  
- **Missing metadata fields** – Không phải tất cả các loại tài liệu đều lưu cùng các khóa siêu dữ liệu; trước tiên kiểm tra thuộc tính tài liệu trong Office.  
- **License errors** – Đảm bảo tệp giấy phép được tải đúng trước khi tạo đối tượng `Redactor`.

## Các cân nhắc về hiệu năng
- Đóng đối tượng `Redactor` ngay khi không cần (như trong khối `finally`) để giải phóng tài nguyên gốc.  
- Tránh raster hóa các tài liệu lớn trừ khi bạn cần bản xem trước PDF; raster hóa có thể tăng mức sử dụng CPU và bộ nhớ lên tới 3× đối với tệp 300 trang.

## Câu hỏi thường gặp

**Q1: Redaction siêu dữ liệu là gì?**  
A1: Redaction siêu dữ liệu liên quan đến việc loại bỏ các thuộc tính ẩn của tài liệu (như tác giả, quản lý, hoặc thẻ tùy chỉnh) để ngăn ngừa việc tiết lộ vô tình thông tin nhạy cảm.

**Q2: Tôi có thể sử dụng GroupDocs.Redaction cho các loại tệp khác không?**  
A2: Có, thư viện hỗ trợ PDF, DOCX, PPTX, XLSX và nhiều định dạng khác—hơn 100 định dạng tổng cộng.

**Q3: Làm thế nào để xử lý lỗi trong quá trình redaction?**  
A3: Bao quanh lời gọi `apply` bằng khối try‑catch và luôn đóng `Redactor` trong khối finally để đảm bảo tài nguyên được giải phóng.

**Q4: Có thể xóa các trường siêu dữ liệu tùy chỉnh không?**  
A5: Chắc chắn. Sử dụng `MetadataFilters.Custom("YourFieldName")` để nhắm mục tiêu bất kỳ thuộc tính tùy chỉnh nào được lưu trong tài liệu.

**Q5: Các thực tiễn tốt nhất khi sử dụng GroupDocs.Redaction là gì?**  
A5:  
- Tải giấy phép sớm trong ứng dụng của bạn.  
- Đóng các đối tượng `Redactor` ngay khi không cần.  
- Sử dụng `SaveOptions` để thêm hậu tố, giữ nguyên các tệp gốc.  
- Kiểm tra redaction trên một bản sao của tài liệu trước khi xử lý hàng loạt.

**Q6: EraseMetadataRedaction có hỗ trợ hoạt động batch không?**  
A6: Bạn có thể lặp qua một tập hợp các đường dẫn tệp, tạo một `Redactor` mới cho mỗi tệp và áp dụng cùng một logic redaction.

**Q7: Tôi có thể kết hợp EraseMetadataRedaction với các loại redaction khác không?**  
A7: Có, bạn có thể nối chuỗi nhiều đối tượng redaction (ví dụ: redaction văn bản rồi redaction siêu dữ liệu) trước khi lưu.

## Tài nguyên
- **Tài liệu**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Tham chiếu API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Tải xuống**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Hỗ trợ miễn phí**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Giấy phép tạm thời**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Cập nhật lần cuối:** 2026-10-01  
**Đã kiểm tra với:** GroupDocs.Redaction 24.9 for Java  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Trích xuất siêu dữ liệu tài liệu Java của Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Cách xóa siêu dữ liệu Java bằng GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Lấy thông tin tài liệu bằng Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)