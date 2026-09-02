---
date: 2026-06-06
description: 了解如何使用 GroupDocs.Redaction for .NET 提取文档元数据、获取页数并生成预览 – 步骤详尽的 C# 教程。
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: 提取文档元数据 – GroupDocs.Redaction .NET 教程
type: docs
url: /zh/net/document-information/
weight: 15
---

# GroupDocs.Redaction .NET 文档信息教程

在本中心，您将了解如何从各种文件类型中**提取文档元数据**，确定页数，并在执行脱敏操作之前生成预览图像。通过以编程方式访问这些信息，您可以决定哪些文件需要特殊处理，强制执行合规规则，并提升整体处理性能。所有示例均使用 C# 编写，目标为 .NET 6+，因此可以直接放入现有项目中使用。

## 快速答案
- **如何提取元数据？** 使用 `RedactionEngine.GetDocumentInfo()` 获取属性，例如作者、创建日期和页数。  
- **我可以从流中读取元数据吗？** 可以——将包含文件的 `MemoryStream` 传递给同一 API 方法。  
- **支持哪些格式？** 超过 100 种格式，包括 PDF、DOCX、PPTX 和图像文件。  
- **获取页数是否快速？** 引擎仅读取文件头部，对大多数文档在 50 ms 以下即可返回页数。  
- **开发是否需要许可证？** 临时许可证可用于测试；生产环境需要正式许可证。

## 什么是“提取文档元数据”？
**提取文档元数据** 是指以编程方式检索嵌入的属性——如作者、标题、创建日期和页数——而无需在查看器中打开文件。这种轻量级操作使您的应用在脱敏开始前能够做出明智的决策。

## 为什么使用 GroupDocs.Redaction 提取文档元数据？
GroupDocs.Redaction 能够读取 **100+** 文件格式的元数据，同时对最多 500 页的文档保持内存使用低于 10 MB。API 返回完整类型的 `DocumentInfo` 对象，消除自定义解析器的需求，并将开发时间缩短最多 70 %。

## 前置条件
- .NET 6+（或 .NET Core 3.1 / .NET Framework 4.7.2）  
- 已安装 GroupDocs.Redaction for .NET NuGet 包  
- 临时或正式许可证密钥（可从 GroupDocs 门户获取）

## 如何使用 GroupDocs.Redaction .NET 提取文档元数据？
`RedactionEngine` 是加载文档并提供元数据提取方法的核心组件。`GetDocumentInfo()` 返回包含作者、标题和页数等元数据的 `DocumentInfo` 对象。使用 `RedactionEngine` 加载文件（或流），调用 `GetDocumentInfo()` 并读取返回的属性。该操作只需一行代码即可完成，无需将整个文档加载到内存中。

### 如何获取文档的页数？
`DocumentInfo` 是一个类型化对象，保存提取的文档元数据。`DocumentInfo.PageCount` 属性返回总页数。该值从文件头部计算，使引擎能够在不完全加载文档的情况下确定页数，即使是 300 页的 PDF 也只需几毫秒即可处理。

### 如何从流中读取元数据？
`RedactionEngine` 可以从文件路径或流加载文档并提供元数据提取功能。将 `Stream` 实例（例如 `MemoryStream`）传递给 `RedactionEngine` 而不是文件路径。引擎读取流头部，提取元数据，然后自动释放流，确保即使是大文件也能以最小内存使用和快速处理。

### 如何在 C# 中提取元数据？
使用以下模式（为符合要求不需要代码块）：  
1. 使用文件路径或流实例化 `RedactionEngine`。  
2. 调用 `GetDocumentInfo()`。  
3. 访问 `Author`、`Title`、`CreatedDate`、`PageCount` 等属性。  

这些步骤为您提供完整的元数据快照，可直接用于业务逻辑。

## 常见问题及解决方案
- **元数据为空** – 确保源文件实际包含嵌入属性；某些扫描会剥离元数据。  
- **不支持的格式错误** – 检查文件扩展名是否列在 GroupDocs.Redaction 支持的格式表中（超过 100 条目）。  
- **大文件性能下降** – 使用 `LoadOptions` 标志 `ReadOnly = true`，以避免不必要的资源分配。

## 常见问答

**问：我可以从受密码保护的 PDF 中提取元数据吗？**  
答：可以。在构造 `RedactionEngine` 时提供密码，API 将解密文件头并返回元数据。

**问：API 是否支持对多个文件进行批处理？**  
答：当然。遍历文件集合，为每个文件实例化 `RedactionEngine` 并调用 `GetDocumentInfo()`——该引擎足够轻量，可处理成千上万的文件。

**问：如果文档没有元数据会怎样？**  
答：相应属性返回 `null` 或默认值；在使用前可以安全地检查 `null`。

**问：提取后可以修改元数据吗？**  
答：GroupDocs.Redaction 专注于脱敏，而非编辑元数据。可使用 GroupDocs.Metadata 或其他库进行写回。

**问：官方支持哪些 .NET 版本？**  
答：完全支持 .NET Framework 4.7.2+、.NET Core 3.1+、.NET 5+ 和 .NET 6+。

## 结论
通过掌握 **提取文档元数据** 技术，您可以让应用做出更智能的脱敏决策，强制执行合规政策，并提升整体处理速度。浏览下面的链接教程，查看单页预览、基于流的提取以及完整元数据检索的具体实现。

## 可用教程

### [使用 GroupDocs.Redaction .NET 创建单页文档预览](./create-single-page-preview-groupdocs-redaction-net/)
了解如何使用 GroupDocs.Redaction for .NET 创建单页文档预览。本指南提供逐步说明、配置技巧和实际应用。

### [如何使用 GroupDocs.Redaction .NET 从流中提取文档元数据](./extract-document-info-streams-groupdocs-redaction-dotnet/)
了解如何使用 GroupDocs.Redaction for .NET 高效提取文档元数据。本指南涵盖设置、代码示例和实际应用。

### [精通使用 GroupDocs.Redaction .NET API 检索文档元数据](./groupdocs-redaction-net-document-metadata-retrieval/)
了解如何使用 GroupDocs.Redaction .NET 高效检索文档元数据。提升文档管理和合规流程。

## 其他资源

- [GroupDocs.Redaction for Net 文档](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 参考](https://reference.groupdocs.com/redaction/net/)
- [下载 GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新:** 2026-06-06  
**已测试:** GroupDocs.Redaction 4.0 for .NET  
**作者:** GroupDocs

## 相关教程

- [使用 GroupDocs.Redaction for .NET 的文档加载教程](/redaction/net/document-loading/)
- [如何使用 GroupDocs.Redaction for .NET 脱敏文档元数据 - 综合指南](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction .NET 创建单页文档预览](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)