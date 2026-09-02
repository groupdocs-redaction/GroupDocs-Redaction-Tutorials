---
date: '2026-06-06'
description: Tìm hiểu cách chuyển đổi trang sang PNG và xem trước các trang PDF bằng
  GroupDocs.Redaction cho .NET. Hướng dẫn từng bước, đoạn mã mẫu và các mẹo thực tế.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Chuyển đổi trang sang PNG bằng GroupDocs.Redaction .NET
type: docs
url: /vi/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Chuyển Trang sang PNG bằng GroupDocs.Redaction .NET

Creating a preview of a single page from a large document is a common need when you want to share just the relevant slice of information. In this tutorial you’ll learn **how to convert a page to PNG** with GroupDocs.Redaction for .NET, configure the preview output, and integrate the result into your applications. We’ll walk through prerequisites, installation, code setup, and practical tips so you can start generating single‑page PNG previews in minutes.

## Câu trả lời nhanh
- **Có thể tạo bản xem trước PNG chỉ cho một trang không?** Có, sử dụng `PreviewOptions` để chỉ định số trang và định dạng.  
- **Định dạng nào mà GroupDocs.Redaction hỗ trợ cho bản xem trước?** PNG là mặc định, nhưng JPEG và BMP cũng có sẵn.  
- **Tôi có cần giấy phép cho việc phát triển không?** Bản dùng thử miễn phí hoạt động cho việc kiểm tra; giấy phép sản xuất là bắt buộc cho sử dụng thương mại.  
- **Điều này có hoạt động trên .NET Core và .NET Framework không?** Chắc chắn – thư viện nhắm tới .NET Standard 2.0+.  
- **Quá trình có tiết kiệm bộ nhớ cho các tệp lớn không?** Có, API truyền dữ liệu các trang, tránh tải toàn bộ tài liệu.

## Convert page to PNG là gì?
**convert page to PNG** đề cập đến việc trích xuất một trang duy nhất từ tài liệu được hỗ trợ (PDF, DOCX, PPTX, v.v.) và hiển thị trang đó dưới dạng ảnh Portable Network Graphics (PNG). Ảnh kết quả giữ nguyên bố cục trực quan, phông chữ và đồ họa của trang gốc, cho phép bạn chia sẻ một ảnh chụp nhanh rõ ràng trong khi giữ phần còn lại của tài liệu ẩn.

## Tại sao nên sử dụng bản xem trước một trang?
Tạo bản xem trước PNG một trang giúp giảm băng thông, tăng tốc thời gian tải và bảo vệ nội dung nhạy cảm bằng cách chỉ hiển thị những gì cần thiết. GroupDocs.Redaction có thể chuyển đổi một PDF 300 trang thành PNG 200 KB trong chưa tới 0,5 giây trên phần cứng máy chủ tiêu chuẩn, làm cho nó trở thành lựa chọn lý tưởng cho các cổng thông tin web và công cụ báo cáo.

## Các yêu cầu trước
- **GroupDocs.Redaction for .NET** – thư viện cốt lõi thực hiện việc che dấu tài liệu và tạo bản xem trước.  
- **System.IO** – không gian tên .NET chuẩn cho việc xử lý tệp.  
- .NET Core 3.1+ hoặc .NET Framework 4.6.1+ (bất kỳ nền tảng nào hỗ trợ .NET Standard 2.0).  
- Kiến thức cơ bản về C# và quen thuộc với quản lý gói NuGet.

## Cài đặt GroupDocs.Redaction cho .NET

### Thông tin Cài đặt

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Mở dự án của bạn trong Visual Studio.  
- Chọn **Manage NuGet Packages**.  
- Tìm kiếm **GroupDocs.Redaction** và cài đặt phiên bản ổn định mới nhất.

### Các bước lấy Giấy phép
Để chạy thư viện, bạn cần một giấy phép hợp lệ. Bạn có thể bắt đầu với bản dùng thử miễn phí hoặc yêu cầu một khóa tạm thời:

1. Truy cập [GroupDocs website](https://purchase.groupdocs.com/temporary-license) để yêu cầu giấy phép tạm thời.  
2. Làm theo hướng dẫn trong email để thêm tệp giấy phép vào dự án của bạn.

### Khởi tạo và Cấu hình Cơ bản
The `RedactionEngine` class is the entry point for all operations, including preview generation.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Hướng dẫn Triển khai

### Tổng quan
Phần này trình bày cách **convert page to PNG** bằng cách cấu hình `PreviewOptions` và gọi API xem trước. Cách tiếp cận này hoạt động cho PDF, DOCX, PPTX và nhiều định dạng khác được hỗ trợ bởi GroupDocs.Redaction.

### Bước 1: Chuẩn bị Môi trường
Set the source file path and output folder. Use `Path.Combine` to build platform‑independent paths.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Bước 2: Cấu hình Tùy chọn Xem trước
`PreviewOptions` lets you define the page number, image size, and output format. The class is the configuration hub for preview generation.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Giải thích các Cấu hình Chính
- **Width & Height** – Điều chỉnh các giá trị này để phù hợp với độ phân giải hiển thị mục tiêu.  
- **PageNumbers** – Cung cấp một mảng với chỉ số trang chính xác mà bạn muốn hiển thị (đánh số từ 0).  
- **PreviewFormat** – PNG là mặc định; chuyển sang `PreviewFormat.Jpeg` để có tệp nhỏ hơn.

### Mẹo Khắc phục Sự cố
If the PNG isn’t generated:

- Xác minh đường dẫn tệp nguồn đúng và tệp có thể truy cập được.  
- Đảm bảo tệp giấy phép đã được tải trước khi gọi bất kỳ phương thức API nào.  
- Xác nhận rằng `PreviewOptions.PageNumbers` chứa một chỉ số trang hợp lệ (ví dụ, `0` cho trang đầu).

## Ứng dụng Thực tiễn
Tạo bản xem trước PNG một trang hữu ích trong nhiều tình huống:

1. **Client Presentations** – Chỉ hiển thị slide hoặc điều khoản hợp đồng liên quan.  
2. **Internal Reviews** – Cho phép kiểm tra nhanh bằng hình ảnh mà không cần mở toàn bộ tài liệu.  
3. **Content Summaries** – Nhúng ảnh chụp trang vào email hoặc bảng điều khiển để cung cấp ngữ cảnh ngay lập tức.  

Việc tích hợp tính năng này với CMS hoặc CRM có thể tự động tạo thumbnail cho các tài liệu đã tải lên, cải thiện trải nghiệm người dùng.

## Các lưu ý về Hiệu suất
- **Memory Management** – Giải phóng các thể hiện `RedactionEngine` sau khi sử dụng để giải phóng tài nguyên.  
- **Asynchronous Execution** – Sử dụng `await engine.GeneratePreviewAsync(...)` trong các ứng dụng UI để giữ giao diện phản hồi.  
- **Library Updates** – GroupDocs.Redaction hỗ trợ **hơn 30 định dạng đầu vào và đầu ra** và xử lý tài liệu lên tới 500 trang mà không tải toàn bộ tệp vào bộ nhớ. Giữ gói cập nhật để hưởng lợi từ các cải tiến hiệu suất.

## Kết luận
Bây giờ bạn đã có một phương pháp hoàn chỉnh, sẵn sàng cho sản xuất để **convert page to PNG** và tạo bản xem trước một trang với GroupDocs.Redaction cho .NET. Bằng cách làm theo các bước trên, bạn có thể nhúng các ảnh PNG chất lượng cao vào bất kỳ ứng dụng .NET nào, nâng cao việc chia sẻ tài liệu đồng thời bảo vệ bảo mật và hiệu suất.

## Câu hỏi thường gặp

**Q: Có thể tạo bản xem trước cho PDF được bảo mật bằng mật khẩu không?**  
A: Có, cung cấp mật khẩu khi khởi tạo `RedactionEngine` và bản xem trước sẽ được tạo bình thường.

**Q: Làm thế nào để thay đổi định dạng đầu ra từ PNG sang JPEG?**  
A: Đặt `options.PreviewFormat = PreviewFormat.Jpeg` trước khi gọi phương thức xem trước.

**Q: Có thể xem trước nhiều trang cùng lúc không?**  
A: Chắc chắn – gán một mảng các số trang cho `options.PageNumbers` (ví dụ, `new[] {0, 2, 4}`).

**Q: Nên làm gì nếu ảnh xem trước bị mờ?**  
A: Tăng `options.Width` và `options.Height` lên độ phân giải cao hơn; thư viện sẽ mở rộng ảnh tương ứng.

**Q: Điều này có hoạt động trên container Linux không?**  
A: Có, GroupDocs.Redaction .NET là đa nền tảng và chạy trong các container Docker hỗ trợ .NET Core.

## Tài nguyên
- [Tài liệu](https://docs.groupdocs.com/redaction/net/)  
- [Tham chiếu API](https://reference.groupdocs.com/redaction/net)  
- [Tải phiên bản mới nhất](https://releases.groupdocs.com/redaction/net/)  
- [Diễn đàn Hỗ trợ miễn phí](https://forum.groupdocs.com/c/redaction/33)  
- [Lấy Giấy phép Tạm thời](https://purchase.groupdocs.com/temporary-license)  

---

**Cập nhật lần cuối:** 2026-06-06  
**Kiểm tra với:** GroupDocs.Redaction 5.6 for .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Làm chủ Bảo mật Tài liệu: Rasterize và Redact tài liệu Word với GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)  
- [Cách Xóa Trang khỏi PDF bằng GroupDocs.Redaction .NET: Hướng dẫn Toàn diện](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)  
- [Triển khai Redaction Tài liệu bằng GroupDocs.Redaction .NET: Hướng dẫn Từng bước](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)