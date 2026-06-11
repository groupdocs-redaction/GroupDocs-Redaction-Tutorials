---
date: 2026-06-11
description: 了解如何使用 GroupDocs.Redaction for .NET 导出 redacted files、configure output
  folders、create rasterized PDFs，并 save to streams。
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
title: 如何使用 GroupDocs.Redaction .NET 导出 redacted documents
type: docs
url: /zh/net/document-saving/
weight: 3
---

# 如何使用 GroupDocs.Redaction .NET 导出已编辑文档

在本综合指南中，您将了解 **如何导出已编辑** 内容，安全且高效地使用 GroupDocs.Redaction for .NET。无论您是需要保留原始文件类型、将文档锁定为光栅化 PDF，还是直接在内存中流式传输结果，我们都会通过清晰、对话式的解释和实际技巧逐一介绍所有选项。完成本教程后，您将能够为任何合规驱动的场景选择合适的导出策略。

## 快速答案
- **我可以导出哪些格式？** 任意 GroupDocs.Redaction 支持的 30 多种原生格式，另加用于最高安全性的光栅化 PDF。  
- **流式传输是否需要许可证？** 是的，生产环境的流式传输需要有效的 GroupDocs.Redaction 许可证。  
- **我可以设置自定义输出文件夹吗？** 当然可以——使用 `OutputPath` 属性或 `SaveOptions` 进行配置。  
- **光栅化对大文件安全么？** 它可处理最多 500 页的文档，而无需将整个文件加载到内存中。  
- **支持哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。

## 什么是 GroupDocs.Redaction？
GroupDocs.Redaction 是一个 .NET 库，可以编程方式从 PDF、Word、Excel、PowerPoint、图像以及许多其他格式中删除或遮蔽敏感信息。它提供了用于定义编辑区域、应用策略并最终导出已清理文档的高级 API。这使得在任何 .NET 应用程序中集成编辑功能变得轻而易举。

## 为什么将已编辑文档导出为光栅化 PDF？
光栅化 PDF 将每页转换为平面图像，消除后续可能被提取的隐藏文本层。此格式确保已编辑内容无法恢复，符合 GDPR、HIPAA 等严格监管标准。GroupDocs.Redaction 能生成最高 300 dpi 的光栅化 PDF，既保留视觉保真度，又确保安全性。

## 如何导出已编辑文档？
加载源文件，应用编辑规则，然后调用相应的保存方法——`Save` 用于原始格式，`SaveAsRasterizedPdf` 用于仅图像的 PDF，或 `SaveToStream` 用于内存处理。以下是逐步工作流。每种方法都确保已编辑内容被永久移除，同时保留所需的输出格式。

### 步骤 1：安装 NuGet 包
将最新的 GroupDocs.Redaction 包添加到您的项目中：

```bash
dotnet add package GroupDocs.Redaction
```

### 步骤 2：加载文档并定义编辑
创建 `Redactor` 实例，加载文件，并指定要隐藏的区域。`Redactor` 类提供了加载文档和应用编辑规则的核心功能。

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

### 步骤 3：选择导出方法
#### 导出为原始格式
```csharp
redactor.Save("RedactedReport.docx");
```

#### 导出为光栅化 PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### 导出到内存流（适用于 Web API）
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save` 方法将已编辑文档以原始格式写入文件。`SaveAsRasterizedPdf` 创建每页渲染为图像的 PDF，去除所有隐藏文本。`SaveToStream` 将已编辑文件作为内存流返回，适用于 Web 响应。

## 如何配置输出文件夹？
在 `Redactor` 上设置 `OutputPath` 属性，或传递包含目标目录的自定义 `SaveOptions` 对象。`OutputPath` 是 `Redactor` 的属性，用于指定输出文件写入的目录。`SaveOptions` 允许您自定义各种保存参数，包括输出文件夹。此方式确保所有导出文件落在可预测的位置，简化批处理流水线。您还可以根据文档类型指定子文件夹，以保持工作区有序。

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## 常见问题及解决方案
- **编辑未生效：** 确认搜索模式与文档文本完全匹配；如有需要使用 `RegexOptions.IgnoreCase`。`RegexOptions` 是一个枚举，用于控制正则表达式匹配行为，例如大小写敏感性。  
- **大文件导致内存压力：** 使用 `SaveToStream` 启用流式模式，避免对整个文档调用 `Save`。  
- **光栅化 PDF 看起来模糊：** 在 `RasterizationOptions` 中提高 DPI（例如 300–600），以提升图像质量。`RasterizationOptions` 允许您设置 DPI 和图像格式等参数，用于光栅化 PDF 输出。

## 常见问答

**问：我可以导出为原本不支持的格式吗？**  
答：可以，GroupDocs.Redaction 能将大多数输入类型转换为 PDF、DOCX、XLSX、PPTX 或光栅化 PDF，覆盖超过 30 种格式。

**问：光栅化如何保护已编辑的数据？**  
答：通过将每页渲染为平面图像，任何隐藏的文本层都会被移除，原始内容无法被提取。

**问：可以链式应用多个编辑规则吗？**  
答：完全可以——您可以多次调用 `Apply`，或传递 `RedactionOptions` 集合一次性处理多个模式。`RedactionOptions` 定义单个编辑操作的设置，如区域和替换类型。

**问：需要关闭 Redactor 对象吗？**  
答：`Redactor` 实现了 `IDisposable`；请将其放在 `using` 块中或调用 `Dispose()` 以及时释放文件句柄。`IDisposable` 是一个接口，提供释放非托管资源的机制。

**问：官方测试的 .NET 运行时有哪些？**  
答：GroupDocs.Redaction 已在 .NET Framework 4.6+、.NET Core 3.1+ 和 .NET 5/6/7 上验证。

## 附加资源

### 可用教程

- [如何使用 GroupDocs.Redaction for .NET 将文档保存为光栅化 PDF：完整指南](./groupdocs-redaction-net-rasterized-pdfs/)
- [在 .NET 中使用 GroupDocs.Redaction 实现输出目录：综合指南](./implement-output-directory-groupdocs-redaction-dotnet/)
- [使用 GroupDocs.Redaction for .NET 编辑并保存文档：完整指南](./redact-save-documents-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction .NET 将已编辑文档保存为原始格式](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [在 .NET 中使用流进行安全文档编辑：GroupDocs.Redaction 指南](./secure-document-redaction-net-streams-groupdocs-redaction/)

### 有用链接

- [GroupDocs.Redaction for .NET 文档](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET API 参考](https://reference.groupdocs.com/redaction/net/)
- [下载 GroupDocs.Redaction for .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

**最后更新：** 2026-06-11  
**测试版本：** GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

## 相关教程

- [使用 GroupDocs.Redaction .NET 将已编辑文档保存为原始格式](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 将文档保存为光栅化 PDF：完整指南](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [在 .NET 中使用流进行安全文档编辑：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)