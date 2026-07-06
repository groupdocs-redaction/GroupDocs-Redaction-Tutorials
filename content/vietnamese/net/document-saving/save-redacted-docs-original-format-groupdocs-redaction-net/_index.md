---
date: '2026-07-06'
description: Tìm hiểu cách lưu tài liệu đã được xóa thông tin đồng thời giữ nguyên
  định dạng gốc với GroupDocs.Redaction cho .NET. Thực hiện theo hướng dẫn từng bước
  này để thực hiện việc xóa thông tin nhanh chóng và an toàn.
keywords:
- save redacted document
- GroupDocs.Redaction .NET
- document redaction tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  headline: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  name: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  steps:
  - name: Initialize the Redactor
    text: 'Create an instance of the `Redactor` class with your document’s file path:'
  - name: Apply Exact Phrase Redaction
    text: '`ExactPhraseRedaction` is a built‑in redaction type that searches for an
      exact string and replaces it with a black rectangle or custom text.'
  - name: Configure Save Options
    text: '`SaveOptions` lets you keep the source file type, specify a suffix, and
      control memory usage.'
  - name: Save and Output
    text: 'Call the `Save` method with the configured options to write the redacted
      file to disk:'
  type: HowTo
- questions:
  - answer: Over 30 formats, including PDF, DOCX, PPTX, XLSX, and common image types
      such as PNG and JPEG.
    question: What file types can GroupDocs.Redaction handle?
  - answer: Yes – the `Redactor` class provides a `GetRedactions()` method that returns
      a collection you can render in a UI.
    question: Is it possible to preview redactions before saving?
  - answer: Absolutely. Supply the password when constructing the `Redactor` instance
      to unlock the file.
    question: Can I redact password‑protected documents?
  - answer: Yes – the NuGet package is compatible with .NET Framework 4.7.2+, .NET
      Core 3.1+, and .NET 5/6+.
    question: Does the library support .NET Core and .NET 5/6?
  - answer: Purchase a license through the GroupDocs website; a temporary trial license
      is available for evaluation.
    question: How do I obtain a production license?
  type: FAQPage
title: Lưu tài liệu đã được xóa thông tin trong định dạng gốc bằng GroupDocs.Redaction
  .NET
type: docs
url: /vi/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/
weight: 1
---

# Lưu tài liệu đã xóa thông tin trong định dạng gốc bằng GroupDocs.Redaction .NET

Việc xóa thông tin nhạy cảm là một yêu cầu tuân thủ phổ biến, nhưng bạn không muốn mất giao diện và cảm giác của tệp gốc. **Hướng dẫn này cho bạn cách lưu tài liệu đã xóa thông tin trong khi giữ nguyên định dạng gốc** bằng cách sử dụng GroupDocs.Redaction cho .NET. Bạn sẽ nhận được một giải pháp sẵn sàng chạy, hoạt động với PDF, tệp Word và nhiều định dạng khác.

## Câu trả lời nhanh
- **Cách nhanh nhất để lưu tài liệu đã xóa thông tin là gì?** Tải tệp bằng `Redactor`, áp dụng `ExactPhraseRedaction`, sau đó gọi `Save` với `SaveOptions` giữ nguyên loại tệp gốc.  
- **Các định dạng nào được hỗ trợ?** Hơn 30 định dạng, bao gồm PDF, DOCX, PPTX và các loại hình ảnh.  
- **Tôi có cần giấy phép cho việc dùng thử không?** Có – lấy giấy phép tạm thời từ cổng GroupDocs.  
- **Tôi có thể thêm hậu tố tùy chỉnh vào tệp đã lưu không?** Chắc chắn – đặt `SaveOptions.Suffix` thành bất kỳ chuỗi nào (ví dụ: một ngày).  
- **Xử lý tệp lớn có tiết kiệm bộ nhớ không?** Có – GroupDocs.Redaction truyền dữ liệu dạng stream và không bao giờ tải toàn bộ tệp vào bộ nhớ.

## “Lưu tài liệu đã xóa thông tin” là gì?
*Lưu một tài liệu đã xóa thông tin* có nghĩa là ghi lại tệp đã chỉnh sửa trở lại bộ nhớ lưu trữ trong khi giữ nguyên bố cục, loại tệp và siêu dữ liệu gốc. GroupDocs.Redaction thực hiện việc này trong một lần gọi duy nhất, loại bỏ nhu cầu chuyển đổi định dạng thủ công. Quá trình cũng giữ lại các tài nguyên nhúng như phông chữ, hình ảnh và thuộc tính tài liệu, đảm bảo đầu ra trông giống hệt nguồn ngoại trừ nội dung đã bị xóa.

## Tại sao nên sử dụng GroupDocs.Redaction cho .NET?
GroupDocs.Redaction hỗ trợ **hơn 30 định dạng đầu vào và đầu ra** và có thể xử lý các tệp lên tới **500 MB** mà không tải toàn bộ tài liệu vào bộ nhớ, mang lại **tăng hiệu năng 20‑30 %** so với các phương pháp ghi lại tệp một cách thô sơ. API của nó được quản lý hoàn toàn, không yêu cầu phần mềm bên ngoài và tuân thủ GDPR, HIPAA và các quy định khác.

## Yêu cầu trước
- **GroupDocs.Redaction for .NET** – thư viện cốt lõi (phiên bản ổn định mới nhất).  
- **.NET 6+** hoặc **.NET Framework 4.7.2+** đã được cài đặt trên máy phát triển của bạn.  
- Kiến thức cơ bản về C# và quen thuộc với Visual Studio hoặc IDE ưa thích của bạn.

### Thư viện và phụ thuộc cần thiết
- **GroupDocs.Redaction for .NET**: Cần thiết để áp dụng việc xóa thông tin.

### Yêu cầu thiết lập môi trường
- Xác minh dự án của bạn nhắm tới runtime .NET được hỗ trợ. Tham khảo tài liệu chính thức của GroupDocs để biết ma trận phiên bản chính xác.

### Kiến thức tiên quyết
- Hiểu biết về cú pháp C#, I/O tệp và xử lý ngoại lệ.

## Cài đặt GroupDocs.Redaction cho .NET

### Hướng dẫn cài đặt
**Sử dụng .NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Sử dụng Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**Via NuGet Package Manager UI:**  
- Mở NuGet Package Manager trong Visual Studio.  
- Tìm kiếm **"GroupDocs.Redaction"** và cài đặt phiên bản mới nhất.

### Đăng ký giấy phép
Bắt đầu với bản dùng thử miễn phí để thử các tính năng. Truy cập trang web GroupDocs để yêu cầu giấy phép tạm thời nếu cần. Đối với việc sử dụng lâu dài, hãy cân nhắc mua giấy phép từ trang của họ.

Sau khi cài đặt và cấp giấy phép, tham chiếu không gian tên GroupDocs.Redaction trong các tệp mã của bạn:  
```csharp
using GroupDocs.Redaction;
```  

## Hướng dẫn triển khai

### Tạo và cấu hình Redactor
Lớp `Redactor` là thành phần cốt lõi tải tài liệu và áp dụng các thao tác xóa thông tin.  

#### Bước 1: Khởi tạo Redactor  
Tạo một thể hiện của lớp `Redactor` với đường dẫn tệp tài liệu của bạn:  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual path.
using (Redactor redactor = new Redactor(sourceFile))
{
    ...
}
```  

#### Bước 2: Áp dụng Exact Phrase Redaction  
`ExactPhraseRedaction` là loại xóa thông tin tích hợp sẵn, tìm kiếm một chuỗi chính xác và thay thế bằng hình chữ nhật đen hoặc văn bản tùy chỉnh.  
```csharp
// This replaces all instances of "John Doe" with "[personal]".
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```  

### Lưu tài liệu đã xóa thông tin
Giữ nguyên định dạng gốc trong khi thêm hậu tố được xử lý bởi `SaveOptions`.  

#### Bước 3: Cấu hình Save Options  
`SaveOptions` cho phép bạn giữ loại tệp nguồn, chỉ định hậu tố và kiểm soát việc sử dụng bộ nhớ.  
```csharp
var saveOptions = new SaveOptions() 
{
    AddSuffix = true,                  // Adds a suffix like "2023-10-12" to indicate modification.
    RasterizeToPDF = false,           // Ensures the document remains in its original format.
    RedactedFileSuffix = DateTime.Now.ToShortDateString()
};
```  

#### Bước 4: Lưu và xuất  
Gọi phương thức `Save` với các tùy chọn đã cấu hình để ghi tệp đã xóa thông tin ra đĩa:  
```csharp
var outputFile = redactor.Save(saveOptions);
Console.WriteLine($"\nSource document was redacted successfully.\nFile saved to {outputFile}.\n");
```  

### Cách lưu tài liệu đã xóa thông tin trong khi giữ nguyên định dạng gốc?
Tải tệp nguồn bằng `new Redactor("source.pdf")`, áp dụng một hoặc nhiều lần xóa thông tin, cấu hình `SaveOptions` để giữ định dạng gốc và thêm hậu tố (ví dụ: “_redacted”), sau đó gọi `redactor.Save("output.pdf", saveOptions)`. Quy trình một bước này đảm bảo đầu ra giữ nguyên bố cục, phông chữ và siêu dữ liệu giống như tệp đầu vào, trong khi nội dung đã xóa được loại bỏ vĩnh viễn.

### Các vấn đề thường gặp và giải pháp
- **Không tải được tài liệu** – Kiểm tra đường dẫn tệp và đảm bảo quá trình có quyền đọc.  
- **Xóa thông tin thất bại** – Kiểm tra lại chính tả và độ nhạy chữ hoa/thường của cụm từ; sử dụng `IgnoreCase = true` nếu cần.  
- **Tệp đầu ra bị hỏng** – Đảm bảo `SaveOptions` phù hợp với định dạng nguồn; loại không khớp có thể làm hỏng kết quả.

## Ứng dụng thực tế
GroupDocs.Redaction .NET tỏa sáng trong các ngành công nghiệp được quy định:
1. **Quản lý tài liệu pháp lý** – Tự động loại bỏ tên khách hàng, SSN hoặc số vụ án trước khi chia sẻ hợp đồng.  
2. **Bảo mật dữ liệu y tế** – Che dấu thông tin nhận dạng bệnh nhân trong hồ sơ y tế để tuân thủ HIPAA.  
3. **Báo cáo tài chính** – Loại bỏ số tài khoản bí mật khỏi báo cáo quý trước khi phân phối.

## Cân nhắc về hiệu năng
Khi xử lý các tệp lớn (hàng trăm megabyte), hãy tuân theo các thực hành tốt sau:
- Sử dụng mẫu tìm kiếm ngắn gọn để giảm vòng CPU.  
- Giải phóng các thể hiện `Redactor` kịp thời (`using` block) để giải phóng tài nguyên không quản lý.  
- Tận dụng `SaveOptions.Streaming = true` để giảm lượng bộ nhớ sử dụng.

## Kết luận
Bạn hiện đã có một phương pháp hoàn chỉnh, sẵn sàng cho sản xuất để **lưu tài liệu đã xóa thông tin** trong định dạng gốc bằng cách sử dụng GroupDocs.Redaction cho .NET. Bằng cách làm theo các bước trên, bạn có thể tích hợp việc xóa thông tin an toàn vào bất kỳ quy trình .NET nào, đảm bảo tuân thủ mà không làm mất độ trung thực của tài liệu.

Khám phá các tính năng nâng cao như xóa thông tin hàng loạt, hình dạng xóa tùy chỉnh và tích hợp với lưu trữ đám mây để mở rộng giải pháp của bạn hơn nữa.

## Câu hỏi thường gặp

**Q: GroupDocs.Redaction có thể xử lý những loại tệp nào?**  
A: Hơn 30 định dạng, bao gồm PDF, DOCX, PPTX, XLSX và các loại hình ảnh phổ biến như PNG và JPEG.

**Q: Có thể xem trước các lần xóa thông tin trước khi lưu không?**  
A: Có – lớp `Redactor` cung cấp phương thức `GetRedactions()` trả về một bộ sưu tập bạn có thể hiển thị trong giao diện người dùng.

**Q: Tôi có thể xóa thông tin tài liệu được bảo mật bằng mật khẩu không?**  
A: Chắc chắn. Cung cấp mật khẩu khi tạo thể hiện `Redactor` để mở khóa tệp.

**Q: Thư viện có hỗ trợ .NET Core và .NET 5/6 không?**  
A: Có – gói NuGet tương thích với .NET Framework 4.7.2+, .NET Core 3.1+, và .NET 5/6+.

**Q: Làm thế nào để tôi có được giấy phép sản xuất?**  
A: Mua giấy phép qua trang web GroupDocs; giấy phép dùng thử tạm thời có sẵn để đánh giá.

## Tài nguyên
- **Tài liệu**: [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **Tham chiếu API**: [API Reference](https://reference.groupdocs.com/redaction/net)
- **Tải xuống**: [GroupDocs Releases for .NET](https://releases.groupdocs.com/redaction/net/)
- **Hỗ trợ miễn phí**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Giấy phép tạm thời**: [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-07-06  
**Kiểm thử với:** GroupDocs.Redaction 2.0.0 for .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Hướng dẫn lưu tài liệu cho GroupDocs.Redaction .NET](/redaction/net/document-saving/)
- [Xóa thông tin tài liệu an toàn trong .NET bằng Streams: Hướng dẫn cho GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)
- [Cách lưu tài liệu dưới dạng PDF rasterized bằng GroupDocs.Redaction cho .NET: Hướng dẫn đầy đủ](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)