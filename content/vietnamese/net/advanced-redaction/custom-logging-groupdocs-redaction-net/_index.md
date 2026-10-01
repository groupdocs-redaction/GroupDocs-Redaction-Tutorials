---
date: '2026-10-01'
description: Tìm hiểu cách triển khai custom logger c# trong GroupDocs.Redaction cho
  .NET, cho phép ghi log chi tiết và báo cáo tuân thủ dễ dàng hơn.
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: Triển khai custom logger c# trong GroupDocs.Redaction cho .NET để
  ghi lại log chi tiết, lưu tài liệu đã xóa thông tin mà không rasterization, và đáp
  ứng yêu cầu compliance.
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: Triển khai custom logger c# trong GroupDocs.Redaction cho .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: Triển khai custom logger c# trong GroupDocs.Redaction cho .NET
type: docs
url: /vi/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Triển khai logger tùy chỉnh c# trong GroupDocs.Redaction cho .NET

Quản lý việc xóa thông tin trong tài liệu một cách hiệu quả là rất quan trọng, đặc biệt khi xử lý thông tin nhạy cảm. Trong hướng dẫn này, bạn sẽ học **cách triển khai một logger tùy chỉnh c#** với GroupDocs.Redaction cho .NET, cho phép bạn kiểm soát hoàn toàn việc ghi log, xử lý lỗi và tạo chuỗi kiểm toán. Khi kết thúc bài học, bạn sẽ có thể ghi lại các cảnh báo, lỗi và thông báo thông tin, tích hợp logger với các khung ghi log .NET hiện có, và lưu tài liệu đã xóa mà không cần rasterization.

## Câu trả lời nhanh
- **Logger tùy chỉnh c# làm gì?** Nó ghi lại lỗi, cảnh báo và thông báo thông tin trong quá trình xóa, cung cấp cho bạn một chuỗi kiểm toán có thể tìm kiếm.  
- **Thư viện nào cung cấp giao diện ILogger?** GroupDocs.Redaction cho .NET cung cấp giao diện `ILogger`.  
- **Tôi có thể lưu tài liệu đã xóa mà không rasterization không?** Có – gọi `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần giấy phép đầy đủ cho môi trường sản xuất; giấy phép dùng thử có sẵn để đánh giá.  
- **Cách tiếp cận này có tương thích với .NET Core / .NET 6+ không?** Hoàn toàn – cùng một API hoạt động trên .NET Framework, .NET Core, .NET 5 và .NET 6.

## Logger tùy chỉnh c# là gì?

Một **logger tùy chỉnh c#** là một lớp triển khai giao diện `ILogger` do GroupDocs.Redaction cung cấp. Nó cho phép bạn định tuyến các thông điệp log tới bất kỳ nơi nào bạn muốn—console, file, cơ sở dữ liệu, hoặc hệ thống giám sát bên ngoài—đồng thời cung cấp cái nhìn rõ ràng về toàn bộ quy trình xóa.

## Tại sao nên sử dụng logging tùy chỉnh .net với GroupDocs.Redaction?

Tăng cường quy trình xóa của bạn với các log chi tiết, có thể tìm kiếm, đáp ứng các yêu cầu kiểm toán và tăng tốc độ khắc phục sự cố. GroupDocs.Redaction hỗ trợ **hơn 70 định dạng đầu vào và đầu ra** và có thể xử lý tài liệu lên tới 500 trang mà không cần tải toàn bộ tệp vào bộ nhớ, vì vậy một logger được thiết kế tốt sẽ không gây tải nặng đáng kể trong khi cung cấp khả năng quan sát vô giá.

## Yêu cầu trước
- GroupDocs.Redaction cho .NET đã được cài đặt (xem phần **Cài đặt** bên dưới).  
- Môi trường phát triển .NET (Visual Studio, VS Code, hoặc .NET CLI).  
- Kiến thức cơ bản về C# và quen thuộc với luồng tệp.  

## Cài đặt

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Trình quản lý gói**  
```powershell
Install-Package GroupDocs.Redaction
```  

**Giao diện người dùng Trình quản lý Gói NuGet**  
Tìm kiếm **"GroupDocs.Redaction"** và cài đặt phiên bản mới nhất.

## Mua giấy phép

- **Dùng thử miễn phí:** Kiểm tra API với giấy phép tạm thời.  
- **Giấy phép tạm thời:** Nhận quyền truy cập đầy đủ tính năng trong thời gian giới hạn.  
- **Mua:** Mua giấy phép vĩnh viễn cho triển khai sản xuất.

## Hướng dẫn từng bước

### Làm thế nào để triển khai logger tùy chỉnh trong .NET Core?

Tải lớp `CustomLogger` vào dự án .NET Core của bạn và kết nối nó với `RedactorSettings`. Logger hoạt động tương tự trên .NET Framework, .NET 5 và .NET 6, vì vậy bạn có thể chia sẻ cùng một mã trên mọi nền tảng.

### Bước 1: Định nghĩa lớp logger tùy chỉnh (log warnings c#)

Lớp `CustomLogger` triển khai `ILogger`.  
CustomLogger là một lớp do người dùng định nghĩa, thực hiện giao diện `ILogger` để ghi lại các sự kiện xóa.  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**Mỏ neo định nghĩa:** `CustomLogger` là một triển khai do người dùng định nghĩa của giao diện `ILogger` để ghi lại các sự kiện xóa.  
**Giải thích:** Cờ `HasErrors` giúp bạn quyết định có tiếp tục xử lý hay không. Ba phương thức tương ứng với ba mức log bạn sẽ cần trong hầu hết các kịch bản xóa.

### Bước 2: Chuẩn bị đường dẫn tệp và mở tài liệu nguồn

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**Mỏ neo định nghĩa:** `Redactor` là lớp chính trong GroupDocs.Redaction thực hiện các thao tác xóa trên tài liệu PDF.  
**Tại sao điều này quan trọng:** Sử dụng các phương thức tiện ích giúp mã của bạn sạch sẽ và đảm bảo thư mục đầu ra tồn tại trước khi bạn cố gắng **lưu tài liệu đã xóa**.

### Bước 3: Áp dụng các thao tác xóa khi sử dụng logger tùy chỉnh

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**Câu trả lời trực tiếp:** Quy trình xóa bắt đầu bằng việc tạo một thể hiện `Redactor` với `RedactorSettings(logger)`, sau đó áp dụng các đối tượng xóa, kiểm tra `logger.HasErrors`, và cuối cùng gọi `redactor.Save` với rasterization bị tắt. Mô hình này đảm bảo mọi bước đều được ghi log và chỉ lưu tài liệu sạch khi không có lỗi xảy ra.  

**Giải thích:**  
1. `Redactor` được khởi tạo với `RedactorSettings(logger)`, liên kết `CustomLogger` của bạn.  
2. Sau khi áp dụng một thao tác xóa, mã kiểm tra `logger.HasErrors`. Nếu không có lỗi, tài liệu được lưu—điều này minh họa logic **lưu tài liệu đã xóa** mà không cần rasterization.

## Những khó khăn thường gặp & khắc phục

- **Thiếu đầu ra log:** Kiểm tra xem mỗi phương thức `Log*` đã được ghi đè đúng chưa.  
- **Ngoại lệ truy cập tệp:** Đảm bảo ứng dụng có quyền đọc/ghi cho cả đường dẫn nguồn và đầu ra.  
- **Logger chưa được kết nối:** Tham số `RedactorSettings(logger)` là bắt buộc; bỏ qua sẽ tắt tính năng logging tùy chỉnh.

## Ứng dụng thực tế

1. **Báo cáo tuân thủ:** Xuất các mục log ra CSV hoặc cơ sở dữ liệu để tạo chuỗi kiểm toán.  
2. **Theo dõi lỗi:** Nhanh chóng xác định các tệp có vấn đề bằng cách quét đầu ra `LogError`.  
3. **Tự động hoá quy trình:** Kích hoạt các quy trình downstream (ví dụ: thông báo cho nhân viên tuân thủ) khi `LogWarning` được gọi.

## Cân nhắc về hiệu suất

- **Giải phóng luồng ngay khi không cần** để giải phóng bộ nhớ, đặc biệt khi xử lý các lô lớn.  
- **Giám sát CPU & bộ nhớ** trong quá trình xóa hàng loạt; cân nhắc xử lý tài liệu song song với việc đồng bộ logger cẩn thận.  
- **Cập nhật thường xuyên:** Các phiên bản mới của GroupDocs.Redaction thường bao gồm tối ưu hoá hiệu suất và các hook logging bổ sung.

## Kết luận

Bằng cách triển khai một **logger tùy chỉnh c#**, bạn sẽ có được cái nhìn chi tiết vào từng bước của quy trình xóa, giúp dễ dàng đáp ứng các tiêu chuẩn tuân thủ và gỡ lỗi. Cách tiếp cận này hoạt động liền mạch với GroupDocs.Redaction cho .NET và có thể mở rộng để tích hợp với bất kỳ khung ghi log .NET nào bạn đang sử dụng.

---

## Câu hỏi thường gặp

**Q: Mục đích của logging tùy chỉnh với GroupDocs.Redaction là gì?**  
A: Logging tùy chỉnh ghi lại các sự kiện xóa chi tiết, đáp ứng yêu cầu kiểm toán và đơn giản hoá việc khắc phục sự cố bằng cách hiển thị lỗi và cảnh báo trong thời gian thực.

**Q: Làm sao để xử lý lỗi bằng logger tùy chỉnh?**  
A: Triển khai `LogError` trong lớp `CustomLogger` của bạn; cờ `HasErrors` cho phép bạn dừng xử lý nếu phát hiện vấn đề nghiêm trọng.

**Q: Logger tùy chỉnh có thể tích hợp với các hệ thống khác không?**  
A: Có – bạn có thể chuyển tiếp các thông điệp log tới CRM, ERP hoặc công cụ giám sát trung tâm bằng cách mở rộng các phương thức logger.

**Q: Những khó khăn thường gặp khi triển khai logging tùy chỉnh là gì?**  
A: Thiếu ghi đè phương thức, quên truyền `RedactorSettings(logger)`, và quyền truy cập tệp không đủ là những vấn đề phổ biến nhất.

**Q: Logging tùy chỉnh cải thiện quy trình xóa tài liệu như thế nào?**  
A: Các log chi tiết cung cấp khả năng quan sát thời gian thực, giúp gỡ lỗi nhanh hơn và tạo chuỗi kiểm toán cần thiết cho các quy định như GDPR và HIPAA.

## Tài nguyên

- **Documentation:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API reference:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Last updated:** 2026-10-01  
**Tested with:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## Hướng dẫn liên quan

- [How to Load Document with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)  
- [How to Export Redacted Documents with GroupDocs.Redaction .NET](/redaction/net/document-saving/)  
- [Implement Document Redaction Using GroupDocs.Redaction .NET&#58; A Step-by-Step Guide](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)