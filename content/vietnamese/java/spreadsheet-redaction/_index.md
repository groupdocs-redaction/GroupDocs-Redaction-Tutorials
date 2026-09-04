---
date: 2026-08-04
description: Tìm hiểu cách lọc dữ liệu bảng tính java và ẩn thông tin một cách an
  toàn các cột hoặc ô trong bảng tính Excel bằng GroupDocs.Redaction cho Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Tìm hiểu cách lọc dữ liệu bảng tính java và ẩn thông tin một cách
  an toàn các cột hoặc ô trong bảng tính Excel bằng GroupDocs.Redaction cho Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Lọc dữ liệu bảng tính java – hướng dẫn với GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Lọc dữ liệu bảng tính java – hướng dẫn với GroupDocs.Redaction
type: docs
url: /vi/java/spreadsheet-redaction/
weight: 12
---

# Lọc dữ liệu bảng tính java – Hướng dẫn GroupDocs.Redaction Java

Nếu bạn cần **filter spreadsheet data java** trước khi áp dụng việc che dấu, bạn đã đến đúng hướng dẫn. Trong hướng dẫn này, bạn sẽ khám phá cách cô lập các hàng, cột hoặc ô riêng lẻ chứa thông tin cá nhân hoặc bí mật, sau đó che dấu chúng một cách an toàn bằng GroupDocs.Redaction cho Java. Các bước được giải thích bằng ngôn ngữ đơn giản, bao gồm các mẹo thực tiễn, và cho thấy cách giữ xử lý nhanh ngay cả trên các sổ làm việc lớn.

## Câu trả lời nhanh
- **Thư viện nào xử lý việc che dấu bảng tính trong Java?** GroupDocs.Redaction for Java.  
- **Tôi có thể lọc các hàng mà không tải toàn bộ tệp vào bộ nhớ không?** Yes – the API streams data and lets you apply filters on the fly.  
- **Các định dạng tệp nào được hỗ trợ?** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **Tôi có cần giấy phép cho việc phát triển không?** A temporary license works for testing; a full license is required for production.  
- **Có giới hạn kích thước sổ làm việc không?** The engine can process files up to 500 MB without excessive memory consumption.

## Filter spreadsheet data java là gì?
**Filter spreadsheet data java** là quá trình chọn một cách lập trình các hàng, cột hoặc ô cụ thể trong một sổ làm việc kiểu Excel bằng mã Java để chỉ nội dung mục tiêu được kiểm tra hoặc che dấu. Kỹ thuật này giảm thời gian chạy, hạn chế các thay đổi không cần thiết, và giúp đáp ứng các yêu cầu tuân thủ kiểu GDPR.

## Tại sao phải lọc dữ liệu bảng tính java?
GroupDocs.Redaction Java hỗ trợ **30+ định dạng bảng tính** và có thể xử lý các sổ làm việc chứa **lên tới 500 MB** (khoảng 1 triệu hàng) trong khi giữ mức sử dụng bộ nhớ dưới **200 MB**. Bằng cách lọc trước, bạn tránh thao tác với dữ liệu không liên quan, điều này giảm thời gian xử lý trung bình **40‑60 %** cho các kịch bản xóa bỏ thông tin riêng tư thông thường.

## Yêu cầu trước
- Java 17 hoặc phiên bản mới hơn đã được cài đặt.  
- Hệ thống xây dựng Maven hoặc Gradle.  
- GroupDocs.Redaction for Java (có thể tải xuống từ trang chính thức).  
- Khóa giấy phép tạm thời hoặc đầy đủ.  

## Cách lọc dữ liệu trong bảng tính bằng GroupDocs.Redaction Java?
Tải sổ làm việc, xác định bộ lọc khớp với các ô bạn muốn che dấu, và sau đó áp dụng thao tác che dấu. API thực hiện việc lọc theo dạng streaming, vì vậy bạn không bao giờ cần giữ toàn bộ tệp trong RAM.

Lớp `RedactionFilter` cho phép bạn chỉ định chỉ số cột, phạm vi hàng, hoặc các hàm dự đoán tùy chỉnh. Ví dụ, bạn có thể nhắm mục tiêu mọi ô trong cột **B** chứa mẫu địa chỉ email, hoặc bạn có thể giới hạn việc che dấu ở các hàng mà cột “Status” bằng “Confidential”.

**Câu trả lời trực tiếp (40‑70 từ):**  
Tạo một thể hiện `RedactionFilter`, đặt chỉ số cột và điều kiện biểu thức chính quy, sau đó truyền bộ lọc cho `Redactor.redact(workbook, filter)`. Bộ lọc một dòng này cô lập các ô chính xác khớp với tiêu chí của bạn, và công cụ che dấu sẽ xóa hoặc che khuất chúng trong khi để lại phần còn lại của bảng không bị ảnh hưởng. Thao tác hoàn thành trong thời gian tuyến tính so với số hàng đã lọc.

### Bước 1: tạo thể hiện bộ lọc
`RedactionFilter` là lớp cốt lõi đại diện cho quy tắc lọc cho việc che dấu bảng tính. Nó chấp nhận số cột, số hàng, hoặc các biểu thức lambda tùy chỉnh để xác định dữ liệu.

### Bước 2: cấu hình điều kiện
Sử dụng `filter.setColumnIndex(1)` để nhắm mục tiêu cột B (đánh số từ 0) và `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` để khớp mẫu email. Bạn cũng có thể kết hợp nhiều điều kiện với `filter.and(...)` hoặc `filter.or(...)`.

### Bước 3: áp dụng việc che dấu
`Redactor` là lớp chính thực hiện các thao tác che dấu trên một sổ làm việc.  
Truyền sổ làm việc và bộ lọc đã cấu hình cho đối tượng `Redactor`. API stream sổ làm việc, áp dụng bộ lọc, và ghi kết quả đã che dấu vào một tệp mới, giữ nguyên định dạng và công thức gốc.

## Các vấn đề thường gặp và giải pháp
- **Bộ lọc không khớp với bất kỳ ô nào:** Xác nhận chỉ số cột (đánh số từ 0) và đảm bảo cú pháp biểu thức chính quy đúng cho Java.  
- **Lỗi hết bộ nhớ trên các tệp lớn:** Tăng kích thước heap JVM một cách vừa phải (ví dụ, `-Xmx1g`) hoặc chia sổ làm việc thành các phần nhỏ hơn trước khi lọc.  
- **Kết quả đã che dấu mất định dạng:** `RedactionOptions` cho phép bạn tùy chỉnh hành vi che dấu, chẳng hạn như giữ định dạng ô. Sử dụng `RedactionOptions.setPreserveFormatting(true)` để giữ nguyên kiểu dáng ô.

## Tại sao phải lọc dữ liệu bảng tính?
Việc lọc trước khi che dấu chỉ cô lập các phần nhạy cảm của sổ làm việc, nghĩa là bạn tránh các thay đổi không cần thiết đối với dữ liệu sạch. Cách tiếp cận chọn lọc này cũng giảm nguy cơ mất dữ liệu không mong muốn và tăng tốc độ kiểm toán tuân thủ vì nhật ký kiểm toán chứa ít mục hơn nhiều.

## Cách che dấu email trong bảng tính Excel bằng GroupDocs.Redaction Java API
Tải tệp Excel của bạn, áp dụng bộ lọc tìm mẫu email tiêu chuẩn, và gọi công cụ che dấu. API thay thế mỗi email khớp bằng một placeholder như “***@***.com” trong khi giữ nguyên bố cục ô xung quanh.

## Cách lọc dữ liệu – các hướng dẫn có sẵn
- [Cách che dấu email trong bảng tính Excel bằng GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Tài nguyên bổ sung

- [Tài liệu GroupDocs.Redaction cho Java](https://docs.groupdocs.com/redaction/java/)
- [Tham chiếu API GroupDocs.Redaction cho Java](https://reference.groupdocs.com/redaction/java/)
- [Tải xuống GroupDocs.Redaction cho Java](https://releases.groupdocs.com/redaction/java/)
- [Diễn đàn GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Hỗ trợ miễn phí](https://forum.groupdocs.com/)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-08-04  
**Kiểm tra với:** GroupDocs.Redaction 23.11 for Java  
**Tác giả:** GroupDocs  

## Câu hỏi thường gặp

**Q: Bạn có thể lọc nhiều cột cùng lúc không?**  
A: Có, bạn có thể thêm các chỉ số cột bổ sung vào cùng một thể hiện `RedactionFilter` hoặc nối nhiều bộ lọc với `filter.or(...)`.

**Q: Bộ lọc có hoạt động trên sổ làm việc được bảo vệ bằng mật khẩu không?**  
A: Cung cấp mật khẩu khi mở sổ làm việc; bộ lọc hoạt động sau khi giải mã giống như trên tệp không được bảo vệ.

**Q: API có thể xử lý bao nhiêu hàng trong một thao tác duy nhất?**  
A: Engine được tối ưu cho tới 1 triệu hàng (≈500 MB) mà không cần tải toàn bộ tệp vào bộ nhớ.

**Q: Có thể xem trước các ô sẽ bị che dấu trước khi lưu không?**  
A: Có, gọi `filter.preview(workbook)` để nhận danh sách địa chỉ ô khớp với tiêu chí.

**Q: Mô hình giấy phép nào cần thiết cho việc sử dụng trong môi trường sản xuất?**  
A: Cần một giấy phép thương mại đầy đủ cho triển khai sản xuất; giấy phép tạm thời đủ cho việc thử nghiệm và đánh giá.

## Hướng dẫn liên quan

- [Cách che dấu dữ liệu nhạy cảm trong bảng tính Excel bằng GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Che dấu dữ liệu nhạy cảm Java – Hướng dẫn GroupDocs.Redaction](/redaction/java/getting-started/)
- [Che dấu dữ liệu nhạy cảm Java – Che dấu thông tin cá nhân với GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)