---
date: '2026-03-28'
description: Tìm hiểu cách triển khai một logger tùy chỉnh bằng C# trong GroupDocs.Redaction
  cho .NET, cho phép ghi log chi tiết tùy chỉnh và báo cáo tuân thủ dễ dàng hơn.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Triển khai logger tùy chỉnh C# trong GroupDocs.Redaction cho .NET
type: docs
url: /vi/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Triển khai logger tùy chỉnh c# trong GroupDocs.Redaction cho .NET

Quản lý việc xóa nhạy cảm tài liệu một cách hiệu quả là rất quan trọng, đặc biệt khi xử lý thông tin nhạy cảm. Trong hướng dẫn này, bạn sẽ học **cách triển khai một logger tùy chỉnh c#** với GroupDocs.Redaction cho .NET, cung cấp cho bạn quyền kiểm soát đầy đủ đối với việc ghi log, xử lý lỗi và theo dõi audit.

## Câu trả lời nhanh
- **Logger tùy chỉnh c# làm gì?** Nó ghi lại các lỗi, cảnh báo và thông báo thông tin trong quá trình xóa nhạy cảm.  
- **Thư viện nào cung cấp giao diện ILogger?** GroupDocs.Redaction for .NET.  
- **Tôi có thể lưu tài liệu đã xóa nhạy cảm mà không rasterization không?** Có – sử dụng `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần giấy phép đầy đủ cho môi trường sản xuất; bản dùng thử có sẵn để đánh giá.  
- **Phương pháp này có tương thích với .NET Core / .NET 6+ không?** Hoàn toàn – cùng một API hoạt động trên .NET Framework và .NET Core/5/6.

## Logger tùy chỉnh c# là gì?
Một **logger tùy chỉnh c#** là một lớp triển khai giao diện `ILogger` do GroupDocs.Redaction cung cấp. Nó cho phép bạn chuyển hướng các thông điệp log tới bất kỳ nơi nào bạn cần—console, file, cơ sở dữ liệu, hoặc hệ thống giám sát bên ngoài—đồng thời cung cấp cho bạn cái nhìn rõ ràng về quy trình xóa nhạy cảm.

## Tại sao nên sử dụng logging tùy chỉnh .net với GroupDocs.Redaction?
- **Tuân thủ & Kiểm toán:** Các log chi tiết đáp ứng các yêu cầu quy định.  
- **Hiển thị lỗi:** `LogError` và `LogWarning` cung cấp phản hồi ngay lập tức về các vấn đề.  
- **Tính linh hoạt tích hợp:** Chuyển tiếp log tới các framework logging .NET hiện có (Serilog, NLog, v.v.).

## Yêu cầu trước
- **GroupDocs.Redaction for .NET** đã được cài đặt (xem phần cài đặt bên dưới).  
- Môi trường phát triển .NET (Visual Studio, VS Code, hoặc CLI).  
- Kiến thức cơ bản về C# và quen thuộc với các luồng file.

## Cài đặt

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Tìm kiếm **"GroupDocs.Redaction"** và cài đặt phiên bản mới nhất.

## Đăng ký giấy phép
- **Dùng thử miễn phí:** Kiểm tra API với giấy phép tạm thời.  
- **Giấy phép tạm thời:** Nhận quyền truy cập đầy đủ tính năng trong một thời gian giới hạn.  
- **Mua:** Có được giấy phép vĩnh viễn cho triển khai sản xuất.

## Hướng dẫn từng bước

### Bước 1: Định nghĩa lớp logger tùy chỉnh (log cảnh báo c#)

Tạo một lớp triển khai `ILogger`. Lớp này sẽ ghi lại các lỗi, cảnh báo và thông báo thông tin.

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

**Giải thích:** Cờ `HasErrors` giúp bạn quyết định có tiếp tục xử lý hay không. Ba phương thức tương ứng với ba mức log bạn sẽ cần trong hầu hết các kịch bản xóa nhạy cảm.

### Bước 2: Chuẩn bị đường dẫn file và mở tài liệu nguồn

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Tại sao điều này quan trọng:** Sử dụng các phương thức tiện ích giúp mã của bạn sạch sẽ và đảm bảo thư mục đầu ra tồn tại trước khi bạn cố gắng **lưu tài liệu đã xóa nhạy cảm**.

### Bước 3: Áp dụng xóa nhạy cảm khi sử dụng logger tùy chỉnh

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

**Giải thích:**  
1. `Redactor` được khởi tạo với `RedactorSettings(logger)`, liên kết `CustomLogger` của bạn.  
2. Sau khi áp dụng một redaction, mã kiểm tra `logger.HasErrors`. Nếu không có lỗi nào xảy ra, tài liệu sẽ được lưu—điều này minh họa logic **lưu tài liệu đã xóa nhạy cảm** mà không cần rasterization.

### Những cạm bẫy thường gặp & Khắc phục sự cố
- **Thiếu đầu ra log:** Xác minh rằng mỗi phương thức `Log*` đã được ghi đè đúng cách.  
- **Ngoại lệ truy cập file:** Đảm bảo ứng dụng có quyền đọc/ghi cho cả đường dẫn nguồn và đầu ra.  
- **Logger chưa được kết nối:** Tham số `RedactorSettings(logger)` là cần thiết; bỏ qua nó sẽ tắt logging tùy chỉnh.

## Ứng dụng thực tiễn
1. **Báo cáo tuân thủ:** Xuất các mục log ra CSV hoặc cơ sở dữ liệu để tạo chuỗi audit.  
2. **Theo dõi lỗi:** Nhanh chóng xác định các file có vấn đề bằng cách quét đầu ra `LogError`.  
3. **Tự động hoá quy trình:** Kích hoạt các quy trình tiếp theo (ví dụ, thông báo cho nhân viên tuân thủ) khi `LogWarning` được gọi.

## Các cân nhắc về hiệu năng
- **Giải phóng luồng kịp thời** để giải phóng bộ nhớ, đặc biệt khi xử lý các lô lớn.  
- **Giám sát CPU & bộ nhớ** trong quá trình xóa nhạy cảm hàng loạt; cân nhắc xử lý tài liệu song song với việc đồng bộ logger cẩn thận.  
- **Cập nhật thường xuyên:** Các phiên bản mới hơn của GroupDocs.Redaction thường bao gồm các tối ưu hoá hiệu năng và các hook logging bổ sung.

## Kết luận

Bằng cách triển khai một **logger tùy chỉnh c#**, bạn có được cái nhìn chi tiết về từng bước trong quy trình xóa nhạy cảm, giúp dễ dàng đáp ứng các tiêu chuẩn tuân thủ và gỡ lỗi. Phương pháp được trình bày ở đây hoạt động liền mạch với GroupDocs.Redaction cho .NET và có thể mở rộng để tích hợp với bất kỳ framework logging .NET nào bạn đã sử dụng.

---

## Câu hỏi thường gặp

**Q: Mục đích của logging tùy chỉnh với GroupDocs.Redaction là gì?**  
A: Logging tùy chỉnh giúp theo dõi và quản lý các redaction để tuân thủ, theo dõi lỗi và tối ưu hoá quy trình làm việc.

**Q: Làm thế nào để xử lý lỗi bằng logger tùy chỉnh?**  
A: Triển khai `LogError` trong lớp `CustomLogger` của bạn; cờ `HasErrors` cho phép bạn dừng xử lý nếu cần.

**Q: Logging tùy chỉnh có thể tích hợp với các hệ thống khác không?**  
A: Có, bạn có thể chuyển tiếp các thông điệp log tới CRM, ERP, hoặc các công cụ giám sát trung tâm bằng cách mở rộng các phương thức logger.

**Q: Một số cạm bẫy thường gặp khi triển khai logging tùy chỉnh là gì?**  
A: Các triển khai phương thức không đúng, thiếu `RedactorSettings(logger)`, và vấn đề quyền truy cập file là những vấn đề phổ biến nhất.

**Q: Logging tùy chỉnh cải thiện quy trình xóa nhạy cảm tài liệu như thế nào?**  
A: Các log chi tiết cung cấp khả năng hiển thị thời gian thực, đơn giản hoá việc khắc phục sự cố và đáp ứng các yêu cầu audit.

## Tài nguyên

- **Tài liệu:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **Tham chiếu API:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)
- **Tải xuống:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Cập nhật lần cuối:** 2026-03-28  
**Kiểm tra với:** GroupDocs.Redaction 23.11 for .NET  
**Tác giả:** GroupDocs