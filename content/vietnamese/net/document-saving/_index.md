---
date: 2026-06-11
description: Tìm hiểu cách xuất các tệp đã được che dấu, cấu hình thư mục đầu ra,
  tạo PDF rasterized, và lưu vào luồng sử dụng GroupDocs.Redaction cho .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Cách xuất tài liệu đã được che dấu bằng GroupDocs.Redaction .NET
type: docs
url: /vi/net/document-saving/
weight: 3
---

# Cách xuất tài liệu đã xóa thông tin nhạy cảm với GroupDocs.Redaction .NET

Trong hướng dẫn toàn diện này, bạn sẽ khám phá **cách xuất tài liệu đã xóa** một cách an toàn và hiệu quả bằng cách sử dụng GroupDocs.Redaction cho .NET. Cho dù bạn cần giữ nguyên loại tệp gốc, khóa tài liệu dưới dạng PDF rasterized, hoặc truyền kết quả trực tiếp trong bộ nhớ, chúng tôi sẽ hướng dẫn bạn qua mọi tùy chọn với các giải thích rõ ràng, thân thiện và các mẹo thực tế. Khi kết thúc bài học này, bạn sẽ có thể chọn chiến lược xuất phù hợp cho bất kỳ kịch bản tuân thủ nào.

## Câu trả lời nhanh
- **Các định dạng tôi có thể xuất ra là gì?** Bất kỳ trong hơn 30 định dạng gốc được GroupDocs.Redaction hỗ trợ, cộng thêm PDF rasterized để bảo mật tối đa.  
- **Tôi có cần giấy phép để streaming không?** Có, cần một giấy phép GroupDocs.Redaction hợp lệ cho việc streaming trong môi trường sản xuất.  
- **Tôi có thể đặt thư mục đầu ra tùy chỉnh không?** Chắc chắn – sử dụng thuộc tính `OutputPath` hoặc `SaveOptions` để cấu hình.  
- **Rasterization có an toàn cho tệp lớn không?** Nó xử lý tài liệu lên tới 500 trang mà không cần tải toàn bộ tệp vào bộ nhớ.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## GroupDocs.Redaction là gì?
GroupDocs.Redaction là một thư viện .NET cho phép loại bỏ hoặc che giấu thông tin nhạy cảm khỏi PDF, Word, Excel, PowerPoint, hình ảnh và nhiều định dạng khác một cách lập trình. Nó cung cấp một API cấp cao để định nghĩa các vùng xóa, áp dụng chính sách, và cuối cùng xuất tài liệu đã được làm sạch. Điều này giúp dễ dàng tích hợp khả năng xóa thông tin vào bất kỳ ứng dụng .NET nào.

## Tại sao xuất tài liệu đã xóa dưới dạng PDF rasterized?
PDF rasterized chuyển mỗi trang thành một hình ảnh phẳng, loại bỏ các lớp văn bản ẩn có thể được trích xuất sau này. Định dạng này đảm bảo nội dung đã xóa không thể phục hồi, đáp ứng các tiêu chuẩn quy định nghiêm ngặt như GDPR và HIPAA. GroupDocs.Redaction có thể tạo PDF rasterized lên tới 300 dpi, giữ nguyên độ chính xác hình ảnh đồng thời đảm bảo an ninh.

## Cách xuất tài liệu đã xóa?
Tải tệp nguồn, áp dụng các quy tắc xóa, sau đó gọi phương thức lưu phù hợp—`Save` cho định dạng gốc, `SaveAsRasterizedPdf` cho PDF chỉ chứa hình ảnh, hoặc `SaveToStream` cho xử lý trong bộ nhớ. Dưới đây là quy trình từng bước. Mỗi phương thức đều đảm bảo nội dung đã xóa được loại bỏ vĩnh viễn trong khi giữ định dạng đầu ra mong muốn.

### Bước 1: Cài đặt gói NuGet
Thêm gói GroupDocs.Redaction mới nhất vào dự án của bạn:

```bash
dotnet add package GroupDocs.Redaction
```

### Bước 2: Tải tài liệu và xác định các vùng xóa
Tạo một thể hiện `Redactor`, tải tệp và chỉ định các vùng bạn muốn ẩn. Lớp `Redactor` cung cấp chức năng cốt lõi để tải tài liệu và áp dụng các quy tắc xóa.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Bước 3: Chọn phương pháp xuất
#### Xuất ở định dạng gốc
```csharp
redactor.Save("RedactedReport.docx");
```

#### Xuất dưới dạng PDF rasterized
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Xuất tới Memory Stream (lý tưởng cho API web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Phương thức `Save` ghi tài liệu đã xóa vào tệp ở định dạng gốc. `SaveAsRasterizedPdf` tạo một PDF mà mỗi trang được render dưới dạng hình ảnh, loại bỏ bất kỳ văn bản ẩn nào. `SaveToStream` trả về tệp đã xóa dưới dạng memory stream, phù hợp cho các phản hồi web.

## Cách cấu hình thư mục xuất?
Đặt thuộc tính `OutputPath` trên đối tượng `Redactor` hoặc truyền một đối tượng `SaveOptions` tùy chỉnh bao gồm thư mục mong muốn. `OutputPath` là thuộc tính của `Redactor` xác định thư mục nơi các tệp đầu ra được ghi. `SaveOptions` cho phép bạn tùy chỉnh nhiều tham số lưu, bao gồm thư mục đầu ra. Điều này đảm bảo tất cả các tệp được xuất đều nằm ở vị trí dự đoán được, đơn giản hoá quy trình xử lý hàng loạt. Bạn cũng có thể chỉ định các thư mục con cho từng loại tài liệu để giữ không gian làm việc được tổ chức.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Các vấn đề thường gặp và giải pháp
- **Redaction not applied:** Xác minh mẫu tìm kiếm khớp chính xác với văn bản trong tài liệu; sử dụng `RegexOptions.IgnoreCase` nếu cần. `RegexOptions` là một enumeration kiểm soát hành vi khớp biểu thức chính quy, chẳng hạn như phân biệt chữ hoa/thường.  
- **Large files cause memory pressure:** Kích hoạt chế độ streaming bằng cách sử dụng `SaveToStream` và tránh gọi `Save` trên toàn bộ tài liệu.  
- **Rasterized PDF looks blurry:** Tăng DPI trong `RasterizationOptions` (ví dụ, 300–600) để cải thiện chất lượng hình ảnh. `RasterizationOptions` cho phép bạn đặt các tham số như DPI và định dạng hình ảnh cho đầu ra PDF rasterized.

## Câu hỏi thường gặp

**Q: Tôi có thể xuất sang định dạng không được hỗ trợ ban đầu không?**  
A: Có, GroupDocs.Redaction có thể chuyển đổi hầu hết các loại đầu vào sang PDF, DOCX, XLSX, PPTX, hoặc PDF rasterized, bao phủ hơn 30 định dạng.

**Q: Rasterization bảo vệ dữ liệu đã xóa như thế nào?**  
A: Bằng cách render mỗi trang thành một hình ảnh phẳng, mọi lớp văn bản ẩn đều bị loại bỏ, khiến việc trích xuất nội dung gốc trở nên không thể.

**Q: Có thể xâu chuỗi nhiều quy tắc xóa không?**  
A: Chắc chắn – bạn có thể gọi `Apply` nhiều lần hoặc truyền một collection của `RedactionOptions` để xử lý nhiều mẫu trong một lượt. `RedactionOptions` định nghĩa các cài đặt cho một thao tác xóa duy nhất, như vùng và kiểu thay thế.

**Q: Tôi có cần đóng đối tượng Redactor không?**  
A: Lớp `Redactor` triển khai `IDisposable`; bao bọc nó trong một khối `using` hoặc gọi `Dispose()` để giải phóng các handle tệp kịp thời. `IDisposable` là một interface cung cấp cơ chế giải phóng tài nguyên không quản lý.

**Q: Các runtime .NET nào được kiểm tra chính thức?**  
A: GroupDocs.Redaction đã được xác thực trên .NET Framework 4.6+, .NET Core 3.1+, và .NET 5/6/7.

## Tài nguyên bổ sung

### Các hướng dẫn có sẵn

- [Cách lưu tài liệu dưới dạng PDF rasterized bằng GroupDocs.Redaction cho .NET: Hướng dẫn đầy đủ](./groupdocs-redaction-net-rasterized-pdfs/)
- [Triển khai thư mục đầu ra trong .NET với GroupDocs.Redaction: Hướng dẫn toàn diện](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Xóa và lưu tài liệu với GroupDocs.Redaction cho .NET: Hướng dẫn đầy đủ](./redact-save-documents-groupdocs-redaction-net/)
- [Lưu tài liệu đã xóa ở định dạng gốc bằng GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Xóa thông tin tài liệu an toàn trong .NET bằng Streams: Hướng dẫn cho GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Liên kết hữu ích

- [Tài liệu GroupDocs.Redaction cho .NET](https://docs.groupdocs.com/redaction/net/)
- [Tham chiếu API GroupDocs.Redaction cho .NET](https://reference.groupdocs.com/redaction/net/)
- [Tải xuống GroupDocs.Redaction cho .NET](https://releases.groupdocs.com/redaction/net/)
- [Diễn đàn GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Hỗ trợ miễn phí](https://forum.groupdocs.com/)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-06-11  
**Đã kiểm tra với:** GroupDocs.Redaction 23.11 for .NET  
**Tác giả:** GroupDocs  

## Các hướng dẫn liên quan

- [Lưu tài liệu đã xóa ở định dạng gốc bằng GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Cách lưu tài liệu dưới dạng PDF rasterized bằng GroupDocs.Redaction cho .NET: Hướng dẫn đầy đủ](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Xóa thông tin tài liệu an toàn trong .NET bằng Streams: Hướng dẫn cho GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)