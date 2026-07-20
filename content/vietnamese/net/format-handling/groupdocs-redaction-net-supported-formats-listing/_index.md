---
date: '2026-07-20'
description: Tìm hiểu cách liệt kê các định dạng bằng GroupDocs.Redaction .NET, tích
  hợp tính năng này vào quy trình làm việc với tài liệu của bạn và cải thiện hiệu
  suất.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Khám phá cách liệt kê các định dạng bằng GroupDocs.Redaction .NET,
  xem hướng dẫn từng bước và nhận các mẹo để đạt hiệu suất tối ưu trong các ứng dụng
  .NET của bạn.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Cách liệt kê các định dạng với GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Cách liệt kê các định dạng với GroupDocs.Redaction .NET
type: docs
url: /vi/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Cách liệt kê các định dạng với GroupDocs.Redaction .NET

Quản lý một loạt các loại tài liệu là thực tế hàng ngày đối với các nhà phát triển xây dựng các ứng dụng tập trung vào tài liệu. Trong hướng dẫn này, bạn sẽ học **cách liệt kê các định dạng** mà GroupDocs.Redaction .NET có thể xử lý, để bạn có thể xác thực tệp trước khi xử lý, cung cấp cho người dùng các tùy chọn chính xác, và giữ cho quy trình làm việc của bạn hiệu quả.

## Giới thiệu

Xử lý tài liệu hiệu quả bắt đầu bằng việc biết chính xác các loại tệp mà thư viện của bạn hỗ trợ. GroupDocs.Redaction cung cấp một phương thức tích hợp để lấy thông tin này, cho phép bạn xây dựng các thành phần UI động, thực thi các quy tắc xác thực, và tránh các lỗi thời gian chạy. Dưới đây bạn sẽ tìm thấy mọi thứ cần thiết để bắt đầu, từ cài đặt đến các đoạn mã thực tế và mẹo hiệu năng.

### Câu trả lời nhanh
- **What does “how to list formats” mean?** Nó đề cập đến việc lấy bộ sưu tập các phần mở rộng tệp mà GroupDocs.Redaction có thể xử lý.  
- **Do I need a license?** Có, cần có giấy phép GroupDocs.Redaction hợp lệ để sử dụng trong môi trường sản xuất.  
- **Which .NET versions are supported?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **How many formats are available?** Hơn 30 định dạng đầu vào và đầu ra được hỗ trợ ngay từ đầu.  
- **Is any special configuration needed?** Không cần cấu hình đặc biệt nào ngoài việc khởi tạo thư viện tiêu chuẩn.

## “Cách liệt kê các định dạng” là gì?

Nó liên quan đến việc gọi API FileType của thư viện để lấy một bộ sưu tập trong đó mỗi mục chứa phần mở rộng tệp và một tên dễ đọc cho người dùng. Các nhà phát triển sau đó có thể duyệt qua bộ sưu tập này để xây dựng các quy tắc xác thực, điền vào các dropdown UI, hoặc ghi lại các loại được hỗ trợ, đảm bảo chỉ các tài liệu tương thích mới được xử lý.

## Tại sao nên liệt kê các định dạng với GroupDocs.Redaction?

GroupDocs.Redaction hỗ trợ **30+** loại tệp riêng biệt—bao gồm PDF, DOCX, PPTX và các định dạng hình ảnh—cho phép bạn xử lý hầu hết các tài liệu doanh nghiệp mà không cần bộ chuyển đổi bên thứ ba. Bằng cách liệt kê các định dạng này một cách lập trình, bạn loại bỏ việc đoán mò, giảm số lượng phiếu hỗ trợ, và đảm bảo chỉ các tệp tương thích mới vào quy trình xử lý của bạn.

## Yêu cầu trước

- **GroupDocs.Redaction for .NET** – tải gói mới nhất từ trang chính thức.  
- **.NET Framework hoặc .NET Core** – tương thích với môi trường phát triển của bạn.  
- **Visual Studio** (hoặc bất kỳ IDE nào hỗ trợ C#).  
- Kiến thức cơ bản về cú pháp C#.

## Cài đặt GroupDocs.Redaction cho .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### Giao diện quản lý gói NuGet
- Tìm kiếm **“GroupDocs.Redaction”** và cài đặt phiên bản mới nhất.

### Nhận giấy phép
GroupDocs cung cấp bản dùng thử miễn phí, giấy phép tạm thời để đánh giá, hoặc các tùy chọn mua đầy đủ. Truy cập trang web GroupDocs để lấy file giấy phép phù hợp.

### Khởi tạo và cài đặt cơ bản
Sau khi thêm gói, tham chiếu namespace và tạo một thể hiện `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Hướng dẫn triển khai

### Làm thế nào để liệt kê các định dạng với GroupDocs.Redaction .NET?
Tải thư viện, gọi helper tĩnh, và sắp xếp kết quả—điều này cung cấp cho bạn một bộ sưu tập sẵn sàng sử dụng chỉ trong hai dòng mã. Sử dụng `FileType.GetSupportedFileFormats()` để lấy một `IEnumerable<FileType>` bao gồm phần mở rộng và tên hiển thị của mỗi định dạng, sau đó sắp xếp theo phần mở rộng để có danh sách UI sạch sẽ.

### Lấy danh sách các định dạng tệp được hỗ trợ

#### Tổng quan
Mục tiêu là thu được danh sách các loại tệp mà GroupDocs.Redaction có thể xử lý, hỗ trợ việc tích hợp vào logic xác thực, dropdown UI, hoặc cơ chế ghi log.

#### Thực hiện từng bước

**1. Lấy các loại tệp được hỗ trợ**  
`FileType.GetSupportedFileFormats()` trả về mọi định dạng mà thư viện nhận diện. Phương thức này thuộc lớp `GroupDocs.Redaction.FileType`, bao gồm siêu dữ liệu như phần mở rộng tệp và tên thân thiện.

**2. Hiển thị các loại tệp được hỗ trợ**  
Duyệt qua bộ sưu tập và xuất mỗi định dạng cùng phần mở rộng và mô tả. Ví dụ mã nội tuyến:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Đoạn mã này in ra một danh sách được sắp xếp gọn gàng như “.pdf – Portable Document Format”, rất phù hợp để điền vào các thành phần UI.

### Mẹo khắc phục sự cố
- **Missing Package** – Kiểm tra lại tham chiếu gói NuGet và khôi phục các gói nếu cần.  
- **Incorrect License Path** – Đảm bảo file giấy phép được sao chép vào thư mục output hoặc cung cấp đường dẫn tuyệt đối.  
- **Unsupported Extension** – Nếu một định dạng không xuất hiện, xác nhận bạn đang dùng phiên bản thư viện mới nhất; các bản phát hành mới thường bổ sung thêm định dạng.

## Ứng dụng thực tế
Hiểu được các định dạng tệp được hỗ trợ mở ra nhiều kịch bản thực tế:

1. **Hệ thống quản lý tài liệu** – Xác thực các tệp tải lên dựa trên danh sách hỗ trợ để ngăn ngừa lỗi xử lý.  
2. **Bảo mật nội dung** – Áp dụng các quy tắc che dấu chỉ trên các loại tệp mà engine có thể chỉnh sửa an toàn.  
3. **Đường ống xử lý hàng loạt** – Lọc các lô tệp lớn trước khi gọi redaction, tiết kiệm CPU và bộ nhớ.

## Các cân nhắc về hiệu năng
- **Memory Footprint** – Liệt kê các định dạng là thao tác nhẹ; không tải bất kỳ tài liệu nào vào bộ nhớ.  
- **Batch Operations** – Khi xử lý hàng trăm tệp, hãy lấy danh sách định dạng một lần và tái sử dụng để tránh các lời gọi lặp lại.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` an toàn với đa luồng và có thể được gọi từ các tác vụ song song mà không cần đồng bộ.

## Kết luận
Bạn đã có một cách tiếp cận hoàn chỉnh, sẵn sàng cho môi trường sản xuất để **cách liệt kê các định dạng** bằng GroupDocs.Redaction .NET. Bằng cách tích hợp tính năng này, bạn có thể nâng cao việc xác thực, cải thiện trải nghiệm người dùng, và giữ cho các pipeline tài liệu của mình vững chắc.

### Các bước tiếp theo
- Khám phá API `Redactor` để áp dụng các quy tắc che dấu dựa trên loại tệp.  
- Kết hợp danh sách định dạng với dropdown front‑end để lựa chọn tệp một cách liền mạch.  
- Xem lại hướng dẫn hiệu năng để tối ưu các công việc batch quy mô lớn.

## Câu hỏi thường gặp

**Q: Có thể lấy danh sách định dạng mà không khởi tạo thể hiện Redactor không?**  
A: Có, `FileType.GetSupportedFileFormats()` là tĩnh và không yêu cầu đối tượng `Redactor`.

**Q: Danh sách có bao gồm cả định dạng đầu vào và đầu ra không?**  
A: Phương thức trả về tất cả các định dạng mà thư viện có thể đọc và ghi; mỗi `FileType` bao gồm cờ `CanRead` và `CanWrite`.

**Q: Danh sách định dạng được cập nhật bao lâu một lần?**  
A: GroupDocs phát hành cập nhật định dạng cùng mỗi phiên bản thư viện; việc kiểm tra danh sách tại thời gian chạy luôn đảm bảo bạn có bộ dữ liệu mới nhất.

**Q: Có cách lọc chỉ các định dạng tương thích với PDF không?**  
A: Có, lọc bộ sưu tập với điều kiện `format.Extension == ".pdf"` hoặc `format.Name.Contains("PDF")`.

**Q: Cách này có hoạt động trên .NET Core 2.1 không?**  
A: Phương thức yêu cầu .NET Core 3.1 trở lên; các runtime cũ hơn không được hỗ trợ.

## Phần FAQ
1. **Làm thế nào để cài đặt GroupDocs.Redaction cho .NET?**  
   Sử dụng lệnh CLI `dotnet add package GroupDocs.Redaction` hoặc cài đặt qua giao diện NuGet Package Manager UI.  
2. **Những vấn đề phổ biến khi lấy danh sách định dạng hỗ trợ là gì?**  
   Đảm bảo tất cả các phụ thuộc đã được khôi phục và bạn đang tham chiếu đúng namespace (`GroupDocs.Redaction`).  
3. **Có thể sử dụng tính năng này với các ứng dụng không phải .NET không?**  
   Hướng dẫn này tập trung vào .NET, nhưng GroupDocs cung cấp API tương tự cho Java, Python và các nền tảng khác.  
4. **Làm sao tối ưu hiệu năng khi sử dụng GroupDocs.Redaction?**  
   Tái sử dụng danh sách định dạng, tránh tải toàn bộ tài liệu khi chỉ cần kiểm tra tính tương thích, và giám sát việc sử dụng bộ nhớ trong các job batch.  
5. **GroupDocs.Redaction hỗ trợ những loại tệp nào?**  
   Thư viện hỗ trợ hơn 30 định dạng, bao gồm PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG và nhiều hơn nữa. Sử dụng `FileType.GetSupportedFileFormats()` để xem danh sách đầy đủ.

## Tài nguyên
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](httpshttps://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 4.2.0 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Hướng dẫn liên quan

- [Format Handling Tutorials for GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)
- [Document Saving Tutorials for GroupDocs.Redaction .NET](/redaction/net/document-saving/)