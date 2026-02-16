---
date: '2026-02-16'
description: Tìm hiểu cách sử dụng phụ thuộc GroupDocs Maven để thêm hậu tố vào tên
  tệp khi chỉnh sửa tài liệu trong Java. Bao gồm tải từ luồng, xóa chú thích và các
  tùy chọn lưu.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Phụ thuộc groupdocs maven – Thêm hậu tố vào tên tệp trong Java
type: docs
url: /vi/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cách Thêm Hậu Tố vào Tên Tệp Khi Che Mờ Tài Liệu trong Java với GroupDocs.Redaction

Việc che mờ dữ liệu bí mật chỉ là một nửa công việc—bạn cũng cần đảm bảo tệp đã lưu rõ ràng cho thấy nó đã được xử lý. **Sử dụng phụ thuộc groupdocs maven giúp việc này trở nên đơn giản**, cho phép bạn thêm một hậu tố vào tên tệp đầu ra chỉ trong vài dòng mã. Trong hướng dẫn này, bạn sẽ học cách thêm hậu tố vào tên tệp khi lưu tài liệu đã che mờ, cùng với việc tải, chú thích và lưu bằng GroupDocs.Redaction cho Java. Dù bạn đang bảo vệ hợp đồng pháp lý, hồ sơ y tế hay báo cáo tài chính, các bước này sẽ giữ cho quy trình làm việc của bạn vừa an toàn vừa có thể kiểm tra.

## Câu trả lời nhanh
- **“add suffix to filename” có chức năng gì?**  
  Nó sẽ nối thêm một hậu tố tùy chỉnh (ví dụ: “_redacted”) vào tên tệp đầu ra để bạn có thể ngay lập tức nhận diện các tệp đã được xử lý.  
- **Tôi có thể tải tài liệu từ stream không?**  
  Có—GroupDocs.Redaction hỗ trợ tải từ bất kỳ `InputStream` nào, rất phù hợp cho lưu trữ đám mây hoặc xử lý trong bộ nhớ.  
- **Tôi có cần giấy phép cho tính năng này không?**  
  Bản dùng thử miễn phí hoạt động cho việc che mờ cơ bản; giấy phép tạm thời hoặc đầy đủ sẽ mở khóa tất cả các tùy chọn nâng cao, bao gồm xử lý hậu tố.  
- **Các định dạng nào được hỗ trợ?**  
  Thư viện hỗ trợ DOCX, PDF, PPTX, XLSX và nhiều định dạng khác.  
- **Có cần rasterization cho đầu ra PDF không?**  
  Rasterization là tùy chọn; bật nó khi bạn cần làm phẳng tài liệu để tăng bảo mật.

## Thêm Hậu Tố vào Tên Tệp là gì?
Thêm một hậu tố là một quy ước đặt tên đơn giản, cho biết tệp đã được che mờ. Nó ngăn ngừa việc chia sẻ nhầm các phiên bản gốc, chưa che mờ và giúp các pipeline tự động theo dõi trạng thái xử lý.

## Tại sao nên sử dụng GroupDocs.Redaction cho nhiệm vụ này?
GroupDocs.Redaction cung cấp một API Java mượt mà cho phép bạn kết hợp các hành động che mờ với các tùy chọn xử lý tệp—như **thêm hậu tố vào tên tệp**—chỉ trong vài dòng mã. Điều này tiết kiệm thời gian phát triển và giảm rủi ro lỗi thủ công.

## Yêu cầu trước
- **Java Development Kit (JDK):** Phiên bản 8 trở lên.  
- **GroupDocs.Redaction Library:** Thư viện lõi cho các nhiệm vụ che mờ.  
- **IDE:** IntelliJ IDEA, Eclipse, hoặc bất kỳ trình soạn thảo nào tương thích với Java.  
- **Maven:** Để quản lý phụ thuộc.  

### Kiến thức tiên quyết
Quen thuộc với Java I/O và các khái niệm cơ bản về lập trình hướng đối tượng sẽ giúp bạn dễ dàng theo dõi các ví dụ.

## Cài đặt GroupDocs.Redaction cho Java
### Cấu hình Maven
Bao gồm cấu hình sau trong tệp `pom.xml` của bạn để truy cập các thư viện GroupDocs qua Maven:

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
Hoặc, tải phiên bản mới nhất trực tiếp từ [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Nhận giấy phép
1. **Free Trial:** Truy cập chức năng cơ bản mà không có hạn chế.  
2. **Temporary License:** Nhận giấy phép tạm thời để khám phá các tính năng nâng cao.  
3. **Purchase:** Đối với việc sử dụng lâu dài, hãy cân nhắc mua giấy phép đầy đủ.

#### Khởi tạo và Cấu hình Cơ bản
Khởi tạo dự án của bạn bằng cách thêm các import cần thiết:

```java
import com.groupdocs.redaction.Redactor;
```

Với cấu hình này, bạn đã sẵn sàng triển khai các chức năng che mờ tài liệu.

## Hướng dẫn triển khai

### Tính năng 1: Tải tài liệu từ Stream
**Tổng quan:** Tìm hiểu cách tải tài liệu vào `InputStream` để xử lý.

#### Thực hiện từng bước
##### Bước 1.1: Tạo InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Tại sao:** Sử dụng `InputStream` cho phép bạn xử lý các tài liệu được lưu trong nhiều định dạng một cách liền mạch, điều này rất quan trọng khi bạn cần **load document from stream** trong các kịch bản đám mây hoặc micro‑service.

### Tính năng 2: Áp dụng Che Mờ Xóa Chú Thích
**Tổng quan:** Loại bỏ các chú thích khỏi tài liệu của bạn bằng `DeleteAnnotationRedaction`.

#### Thực hiện từng bước
##### Bước 2.1: Áp dụng DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Tại sao:** Bước này đảm bảo mọi chú thích nhạy cảm đều bị xóa, tăng cường tính riêng tư của tài liệu.

### Tính năng 3: Lưu tài liệu với các tùy chọn
**Tổng quan:** Tìm hiểu cách lưu tài liệu đã xử lý với các tùy chọn cụ thể như rasterization và **thêm hậu tố vào tên tệp**.

#### Thực hiện từng bước
##### Bước 3.1: Cấu hình SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Tại sao:** Tùy chỉnh các tùy chọn lưu cho phép linh hoạt về định dạng đầu ra và quy ước đặt tên. Bật `setAddSuffix(true)` **adds suffix to filename**, làm cho rõ ràng rằng tệp đã được che mờ.

## Tổng quan về phụ thuộc groupdocs maven
**groupdocs maven dependency** mang toàn bộ Redaction SDK vào dự án của bạn chỉ với một mục `<dependency>` duy nhất. Nó xử lý các phụ thuộc truyền thống, giữ các thư viện luôn cập nhật và đơn giản hoá việc tự động hoá build. Bằng cách khai báo phụ thuộc trong `pom.xml`, bạn tránh việc quản lý JAR thủ công và đảm bảo tính tương thích với các bản vá bảo mật mới nhất.

## Tại sao việc Thêm Hậu Tố lại quan trọng
- **Auditability:** Các nhóm có thể ngay lập tức nhận biết tệp nào an toàn để phân phối.  
- **Automation:** Các script có thể lọc tệp theo hậu tố, ngăn ngừa việc xử lý nhầm các tài liệu gốc.  
- **Compliance:** Nhiều quy định yêu cầu gắn nhãn rõ ràng cho các tài liệu đã được làm sạch.

## Ứng dụng thực tiễn
Khám phá các trường hợp sử dụng thực tế sau:
1. **Legal Document Redaction:** Bảo mật hợp đồng trước khi chia sẻ với khách hàng.  
2. **Medical Record Handling:** Bảo vệ thông tin nhận dạng bệnh nhân.  
3. **Financial Reporting:** Giữ các con số nhạy cảm ở chế độ bí mật.  
4. **CRM Integration:** Tự động che mờ dữ liệu khách hàng trước khi xuất ra.  
5. **Collaboration Tools:** Đảm bảo các bản nháp được chia sẻ không tiết lộ bình luận ẩn.

## Các yếu tố về hiệu suất
### Tối ưu hóa hiệu suất
- Sử dụng streaming (`load document from stream`) để tránh tải toàn bộ tệp vào bộ nhớ.  
- Đóng các instance `Redactor` kịp thời để giải phóng tài nguyên.

### Hướng dẫn sử dụng tài nguyên
- Giám sát CPU và bộ nhớ trong quá trình chạy batch.  
- Ưu tiên `ByteArrayOutputStream` cho các lần lưu trong bộ nhớ khi làm việc với các tệp có kích thước vừa phải.

### Các thực tiễn tốt nhất cho quản lý bộ nhớ Java
- Tái sử dụng các đối tượng `Redactor` khi xử lý nhiều tệp cùng loại.  
- Gọi `close()` trong khối `try‑with‑resources` để ngăn rò rỉ.

## Các vấn đề thường gặp và giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| **Hậu tố không hiển thị** | `setAddSuffix(false)` hoặc gọi thiếu | Đảm bảo `options.setAddSuffix(true)` được đặt trước khi gọi `save()`. |
| **OutOfMemoryError trên DOCX lớn** | Tải toàn bộ tệp vào bộ nhớ | Chuyển sang tải bằng `InputStream` (xem Tính năng 1). |
| **Chú thích vẫn hiển thị** | Che mờ chưa được áp dụng trước khi lưu | Gọi `redactor.apply(new DeleteAnnotationRedaction())` trước khi `save()`. |
| **Rasterization PDF không được áp dụng** | `setRasterizeToPDF(false)` hoặc bị bỏ qua | Đặt `options.setRasterizeToPDF(true)` khi bạn cần một PDF đã được làm phẳng. |

## Câu hỏi thường gặp

**Q: Tôi có thể che mờ tài liệu PDF bằng GroupDocs.Redaction không?**  
A: Có, thư viện hỗ trợ PDF, DOCX, PPTX, XLSX và nhiều định dạng khác.

**Q: Cách tốt nhất để xử lý các tệp lớn với GroupDocs.Redaction là gì?**  
A: Sử dụng streaming (`load document from stream`) và đóng các tài nguyên kịp thời để giữ mức sử dụng bộ nhớ thấp.

**Q: Có thể tùy chỉnh văn bản hậu tố không?**  
A: API tự động thêm một hậu tố mặc định (ví dụ: “_redacted”). Đối với hậu tố tùy chỉnh, bạn có thể đổi tên tệp đầu ra sau khi lưu.

**Q: Làm thế nào để tôi nhận được giấy phép tạm thời cho GroupDocs.Redaction?**  
A: Truy cập [Temporary License page](https://purchase.groupdocs.com/temporary-license/) và làm theo hướng dẫn.

**Q: Tôi có thể nhận được sự trợ giúp ở đâu nếu gặp vấn đề?**  
A: Tham gia [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) để được hỗ trợ từ các chuyên gia.

## Tài nguyên
- **Documentation:** Khám phá các hướng dẫn chi tiết tại [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Truy cập chi tiết API toàn diện trên [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Tải phiên bản mới nhất từ [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Đóng góp hoặc khám phá mã nguồn tại [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Cập nhật lần cuối:** 2026-02-16  
**Đã kiểm tra với:** GroupDocs.Redaction 24.9 cho Java  
**Tác giả:** GroupDocs