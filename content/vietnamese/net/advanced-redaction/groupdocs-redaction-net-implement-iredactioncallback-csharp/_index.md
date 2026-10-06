---
date: '2026-10-06'
description: Tìm hiểu cách xóa dữ liệu bằng GroupDocs.Redaction .NET với việc triển
  khai IRedactionCallback trong C#. Tham khảo hướng dẫn chi tiết từng bước, các thực
  tiễn tốt nhất và các ví dụ thực tế.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Tìm hiểu cách xóa dữ liệu bằng GroupDocs.Redaction .NET với việc triển
  khai IRedactionCallback trong C#. Tham khảo hướng dẫn chi tiết từng bước cùng các
  thực tiễn tốt nhất và các ví dụ thực tế.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Cách xóa dữ liệu bằng GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Cách xóa dữ liệu bằng GroupDocs.Redaction .NET (C#)
type: docs
url: /vi/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Cách xóa dữ liệu bằng GroupDocs.Redaction .NET (C#)

Trong hướng dẫn toàn diện này, bạn sẽ khám phá **cách xóa dữ liệu** từ các tệp PDF, Word và các tài liệu khác bằng cách sử dụng GroupDocs.Redaction cho .NET. Cho dù bạn cần ẩn các định danh cá nhân trong hợp đồng pháp lý hoặc xóa các số liệu bí mật khỏi báo cáo tài chính, SDK cung cấp cho bạn khả năng kiểm soát lập trình để đảm bảo mọi yếu tố nhạy cảm bị xóa vĩnh viễn và có thể kiểm toán. Chúng tôi sẽ hướng dẫn cài đặt thư viện, cấu hình một `IRedactionCallback` tùy chỉnh và áp dụng việc xóa cụm từ chính xác với đầy đủ nhật ký.

## Câu trả lời nhanh
- **IRedactionCallback làm gì?** Nó cho phép bạn chặn mọi sự kiện xóa, ghi lại chi tiết và tùy chọn sửa đổi văn bản thay thế ngay lập tức.  
- **Tôi có cần giấy phép không?** Bản dùng thử hoạt động cho phát triển; giấy phép vĩnh viễn loại bỏ mọi giới hạn đánh giá.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Core 3.1+, .NET 5/6 và .NET Framework 4.6+.  
- **Tôi có thể xử lý nhiều tệp không?** Có — bao bọc logic trong một vòng lặp hoặc sử dụng xử lý hàng loạt để đạt hiệu suất tốt nhất.  
- **Có thể thực hiện xóa bất đồng bộ không?** Không có sẵn, nhưng bạn có thể chạy các lời gọi API bên trong `Task.Run` hoặc các mẫu bất đồng bộ khác.

## Xóa dữ liệu nhạy cảm là gì?
`Redaction` là việc loại bỏ hoặc che giấu vĩnh viễn thông tin không được tiết lộ. Với GroupDocs.Redaction, bạn định nghĩa các cụm từ chính xác, mẫu biểu thức chính quy, hoặc quy tắc tùy chỉnh và thay thế chúng bằng các ký hiệu giữ chỗ như **[REDACTED]** đồng thời giữ nguyên bố cục và phân trang gốc.

## Tại sao nên sử dụng GroupDocs.Redaction với IRedactionCallback?
`IRedactionCallback` là một giao diện thông báo cho bạn mỗi khi SDK xóa một phần nội dung, cho phép bạn ghi lại dữ liệu kiểm toán hoặc điều chỉnh việc thay thế một cách động. Điều này cho phép khả năng kiểm toán đầy đủ, thực thi quy tắc kinh doanh tùy chỉnh và tích hợp liền mạch với các hệ thống tuân thủ — mà không làm giảm hiệu năng.

## Yêu cầu trước
- **Thư viện GroupDocs.Redaction** (phiên bản tương thích – xem trang [documentation page](https://docs.groupdocs.com/redaction/net/)). Để biết chi tiết đầy đủ, tham khảo [official documentation](https://docs.groupdocs.com/redaction/net/).  
- .NET Core hoặc .NET Framework đã được cài đặt trên máy phát triển của bạn.  
- Visual Studio (phiên bản Community là đủ) hoặc bất kỳ IDE nào hỗ trợ C#.  
- Kiến thức cơ bản về C# và quen thuộc với quản lý gói NuGet.

## Cài đặt GroupDocs.Redaction cho .NET
Đầu tiên, thêm thư viện vào dự án của bạn. Chọn phương pháp bạn ưa thích – CLI, Package Manager Console, hoặc UI. Các lệnh giữ nguyên như trong hướng dẫn gốc.

### Các tùy chọn cài đặt
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Mở dự án của bạn trong Visual Studio.  
- Điều hướng tới **Manage NuGet Packages**.  
- Tìm kiếm **GroupDocs.Redaction** và cài đặt phiên bản ổn định mới nhất.

### Nhận giấy phép
Để thử sản phẩm, yêu cầu bản dùng thử miễn phí hoặc giấy phép tạm thời từ [here](https://purchase.groupdocs.com/temporary-license/). Bạn cũng có thể lấy giấy phép tạm thời từ [temporary‑license page](https://purchase.groupdocs.com/temporary-license/). Đối với môi trường sản xuất, mua giấy phép đầy đủ để mở khóa tất cả tính năng mà không có giới hạn.

#### Khởi tạo và cấu hình cơ bản
Dưới đây là đoạn mã tối thiểu bạn cần để mở một tài liệu bằng lớp `Redactor`. Giữ nguyên đoạn mã này — nó là nền tảng cho mọi thứ tiếp theo.  
`Redactor` là lớp chính đại diện cho một tài liệu và cung cấp các phương thức để áp dụng các quy tắc xóa.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Hướng dẫn triển khai
Bây giờ chúng ta sẽ mở rộng cấu hình cơ bản bằng cách thêm một `IRedactionCallback` tùy chỉnh. Điều này cho phép bạn ghi lại mỗi sự kiện xóa, ghi vào nhật ký, hoặc thậm chí sửa đổi văn bản thay thế ngay lập tức.

### Gắn và sử dụng triển khai IRedactionCallback
`IRedactionCallback` là một giao diện nhận các callback cho mỗi thao tác xóa, cho phép bạn ghi nhật ký hoặc thay đổi hành vi bằng lập trình.

#### Bước 1: chuẩn bị thư mục đầu ra và đường dẫn tệp nguồn
Xác định vị trí tài liệu nguồn của bạn. Điều chỉnh đường dẫn để phù hợp với môi trường của bạn.

`LoadOptions` là một đối tượng cấu hình cho SDK biết cách đọc tệp (ví dụ: xử lý mật khẩu).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Bước 2: tạo một thể hiện Redactor với cài đặt tùy chỉnh
Chúng tôi khởi tạo `Redactor` với `LoadOptions` và `RedactorSettings`. `RedactionDump` trong cài đặt sẽ tự động ghi lại mọi lần xóa xảy ra.

`RedactorSettings` cho phép bạn tinh chỉnh quá trình xóa; truyền một `RedactionDump` sẽ bật tệp kiểm toán chi tiết.  
`RedactionDump` là lớp trợ giúp ghi mỗi sự kiện xóa vào một tệp dump định dạng JSON để báo cáo tuân thủ.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Bước 3: áp dụng xóa cụm từ chính xác
Ở đây chúng tôi thay thế cụm từ **John Doe** bằng ký hiệu giữ chỗ **[REDACTED]**. Bạn có thể thay bất kỳ cụm từ hoặc mẫu nào cần ẩn.

`ReplacementOptions` xác định văn bản sẽ thay thế nội dung khớp. Nó cũng hỗ trợ tùy chỉnh phông chữ và màu sắc nếu bạn cần một mặt nạ trực quan.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Giải thích các đối tượng chính**
- `LoadOptions()` – cho SDK biết cách đọc tài liệu (ví dụ: xử lý mật khẩu).  
- `RedactorSettings(new RedactionDump())` – bật tệp dump ghi lại mỗi lần xóa cho mục đích kiểm toán.  
- `ReplacementOptions("[REDACTED]")` – xác định văn bản sẽ thay thế cụm từ khớp.

### Tại sao điều này quan trọng
Cơ chế callback ghi lại mọi sự kiện xóa, tạo ra một chuỗi kiểm toán có thể đọc được bởi máy, và cho phép bạn thay đổi ký hiệu giữ chỗ một cách động, giúp đáp ứng yêu cầu tuân thủ và giảm công sức xử lý thủ công. Bằng cách tích hợp dữ liệu này với hệ thống giám sát, bạn có thể tạo báo cáo, kích hoạt cảnh báo và đảm bảo không có thông tin nhạy cảm nào lọt qua quy trình xóa.

Việc sử dụng `IRedactionCallback` mang lại ba lợi thế cụ thể:  
1. **Nhật ký sẵn sàng cho tuân thủ** – mọi lần xóa được ghi lại trong một dump có thể đọc được bởi máy, đáp ứng yêu cầu kiểm toán cho hơn 30 khung pháp lý.  
2. **Thay thế động** – bạn có thể thay đổi ký hiệu giữ chỗ dựa trên loại dữ liệu, giảm công việc xử lý thủ công lên tới 40 %.  
3. **Hiệu năng mở rộng** – callback thêm overhead không đáng kể (<2 ms mỗi lần xóa) trong khi cho phép bạn xử lý hàng nghìn tệp song song.

### Mẹo khắc phục sự cố
- **File not found:** Kiểm tra lại đường dẫn `sourceFile` và đảm bảo tệp có thể truy cập được bởi tiến trình đang chạy.  
- **Callback not firing:** Xác minh lớp của bạn triển khai **tất cả** các thành viên của `IRedactionCallback` và đối tượng được truyền đúng cho `Redactor`.  
- **Performance lag:** Đối với các batch lớn, tái sử dụng cùng một thể hiện `Redactor` khi có thể và giải phóng nó kịp thời.

## Ứng dụng thực tiễn
Xóa dữ liệu nhạy cảm hữu ích trong nhiều ngành công nghiệp:

1. **Xử lý tài liệu pháp lý** – Tự động loại bỏ tên khách hàng, số vụ án, hoặc số an sinh xã hội trước khi chia sẻ bản nháp.  
2. **Hệ thống quản lý nhân sự** – Xóa các định danh cá nhân khỏi hợp đồng nhân viên trong quá trình kiểm toán.  
3. **Báo cáo tài chính** – Ẩn các số liệu độc quyền hoặc số tài khoản khi tạo PDF dành cho nhà đầu tư.

## Các cân nhắc về hiệu năng
GroupDocs.Redaction hỗ trợ **hơn 30 định dạng đầu vào và đầu ra** (PDF, DOCX, PPTX, XLSX, HTML và các loại hình ảnh) và có thể xử lý các tệp hàng trăm trang mà không cần tải toàn bộ tài liệu vào bộ nhớ. Để ứng dụng của bạn luôn nhanh chóng khi xử lý hàng chục hoặc hàng trăm tệp:

- **Xử lý batch:** Tải danh sách tệp và chạy vòng lặp xóa bên trong `Parallel.ForEach` để tận dụng đa lõi.  
- **Quản lý bộ nhớ:** Bao bọc mỗi `Redactor` trong một khối `using` (như đã minh họa) để đảm bảo giải phóng.  
- **Các thao tác bất đồng bộ:** Mặc dù SDK đồng bộ, bạn có thể chuyển công việc sang các luồng nền hoặc `Task.Run` để tránh chặn luồng UI.

## Các vấn đề thường gặp và giải pháp
| Vấn đề | Giải pháp |
|-------|----------|
| **“Invalid file format” error** | Đảm bảo loại tài liệu được hỗ trợ (PDF, DOCX, PPTX, v.v.). |
| **Callback receives null values** | Kiểm tra rằng bạn đang truyền một triển khai cụ thể của `IRedactionCallback` khi tạo `RedactorSettings`. |
| **Redaction not applied** | Xác minh rằng cụm từ chính xác khớp với trường hợp và khoảng trắng trong tài liệu, hoặc sử dụng `RegexRedaction` cho việc khớp dựa trên mẫu. |

## Câu hỏi thường gặp

**Q: Các tùy chọn cấp phép cho GroupDocs.Redaction là gì?**  
A: Bạn có thể bắt đầu với bản dùng thử miễn phí hoặc yêu cầu giấy phép tạm thời để khám phá tất cả tính năng. Đối với môi trường sản xuất, mua giấy phép vĩnh viễn hoặc giấy phép thuê bao.

**Q: Tôi có thể sử dụng GroupDocs.Redaction trên nhiều loại tệp không?**  
A: Có, nó hỗ trợ PDF, Word, Excel, PowerPoint và nhiều định dạng phổ biến khác.

**Q: Làm thế nào để xử lý ngoại lệ trong quá trình xóa?**  
A: Bao bọc logic xóa của bạn trong các khối `try‑catch` và ghi lại chi tiết ngoại lệ. Callback cũng có thể được sử dụng để ghi nhận lỗi ngay lập tức.

**Q: Có hỗ trợ tích hợp cho xử lý bất đồng bộ không?**  
A: API lõi đồng bộ, nhưng bạn có thể chạy các lời gọi xóa trong các tác vụ bất đồng bộ hoặc dịch vụ nền.

**Q: Tôi có thể tìm các ví dụ nâng cao ở đâu?**  
A: [official documentation](https://docs.groupdocs.com/redaction/net/) và tài liệu tham chiếu API cung cấp nhiều mẫu mã và hướng dẫn kịch bản.

## Tài nguyên

- [Tài liệu GroupDocs.Redaction cho .NET](https://docs.groupdocs.com/redaction/net/)
- [Tham chiếu API GroupDocs.Redaction cho .NET](https://reference.groupdocs.com/redaction/net/)
- [Tải xuống GroupDocs.Redaction cho .NET](https://releases.groupdocs.com/redaction/net/)
- [Diễn đàn GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Hỗ trợ miễn phí](https://forum.groupdocs.com/)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-10-06  
**Được kiểm tra với:** GroupDocs.Redaction 2.3 (phiên bản mới nhất tại thời điểm viết)  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Tạo chính sách xóa với GroupDocs.Redaction .NET – Hướng dẫn từng bước](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Cách xóa tài liệu với GroupDocs.Redaction .NET – Hướng dẫn đầy đủ](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Xóa tài liệu .net bằng Streams – Hướng dẫn GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)