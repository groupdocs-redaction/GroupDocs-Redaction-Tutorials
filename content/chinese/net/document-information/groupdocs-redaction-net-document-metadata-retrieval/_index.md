---
date: '2026-06-06'
description: 了解如何使用 GroupDocs.Redaction .NET 检索元数据并提取文档元数据，实现强大的文档管理和合规性。
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction .NET API 检索元数据
type: docs
url: /zh/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 检索元数据

在当今数字时代，**检索元数据**是任何以文档为中心的应用程序的基本步骤。无论您是需要读取文件元数据以进行合规审计、提取文档属性用于索引，还是仅在 UI 中显示文档大小，GroupDocs.Redaction .NET 为您提供简洁的 API，只需几行 C# 即可完成。本教程将带您完成整个过程，从环境设置到显示检索到的信息，让您立即开始提取文档元数据。

## 快速答案
- **获取元数据的主要方法是什么？** 在 `Redactor` 实例上调用 `Redactor.GetDocumentInfo()`。  
- **支持哪些格式？** 支持超过 50 种输入和输出格式，包括 PDF、DOCX、XLSX、PPTX 和图像类型。  
- **开发是否需要许可证？** 免费试用许可证可用于测试；生产环境需要正式许可证。  
- **我可以处理大文件吗？** 是的——GroupDocs.Redaction 能在不将整个文件加载到内存的情况下处理数百页的文档。  
- **是否支持异步？** 可以将 API 包装为异步模式，以保持 UI 线程的响应性。

## GroupDocs.Redaction 中的元数据检索是什么？

元数据检索是通过库的 API 访问文档内置属性（如文件类型、页数和大小）的过程。通过提取这些属性，开发人员可以以编程方式评估文档特性、支持索引、强制执行合规规则，并对后续处理步骤做出明智决策。

## 如何检索文档元数据？

`Redactor` 类是加载和检查 GroupDocs.Redaction 中文档的主要接口。  
`GetDocumentInfo()` 是一个返回包含文档元数据的 `DocumentInfo` 对象的方法。  

使用 `new Redactor("path/to/file")` 加载文件并调用 `GetDocumentInfo()`——该调用返回一个包含类型、页数、大小等属性的 `DocumentInfo` 对象。这种两步方法适用于任何受支持的格式，无需额外配置。然后您可以读取 `FileType`、`PageCount`、`FileSize` 等字段，以显示或记录信息。

## 前提条件

- **GroupDocs.Redaction .NET** 版本 21.6 或更高。  
- .NET Framework 4.7.2 及以上，.NET Core 3.1 及以上，或 .NET 5/6 及以上。  
- 基本的 C# 知识和开发 IDE（Visual Studio、Rider 等）。

## 为 .NET 设置 GroupDocs.Redaction

开始使用 GroupDocs.Redaction 非常简单。使用以下方法之一安装包：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

或者，使用 **NuGet 包管理器 UI**：只需搜索 “GroupDocs.Redaction” 并点击 **Install**。

### 许可证获取

要试用 GroupDocs.Redaction，您可以获取免费试用许可证。持续开发或生产使用时，请购买正式许可证或从官方网站请求临时许可证。

安装后，按如下方式初始化库：

```csharp
using GroupDocs.Redaction;
```

## 实施指南

### 获取文档信息功能

此功能专注于使用 GroupDocs.Redaction .NET 提取文档的关键元数据。请按以下步骤操作：

#### 步骤 1：准备文档路径

定义目标文件的绝对或相对路径：

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

将 `YOUR_DOCUMENT_DIRECTORY` 替换为包含您文档的文件夹。

#### 步骤 2：初始化 Redactor 实例

创建一个提供元数据方法访问的 `Redactor` 对象：

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### 步骤 3：检索文档信息

在 `Redactor` 实例上调用 `GetDocumentInfo()` 以获取所有可用属性：

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

返回的对象包括文件类型、页数和文件大小。

#### 步骤 4：显示文档详情

将信息输出到控制台或 UI。示例代码（为独立运行已注释）演示了如何打印每个属性：

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### 为什么使用 GroupDocs.Redaction 进行元数据提取？

GroupDocs.Redaction 支持 **50+ 种文件格式**，并且能够处理高达 **2 GB** 的文档，同时在典型工作负载下将内存消耗保持在 **100 MB** 以下。该库在不完全加载文档的情况下提取元数据，响应速度快——在标准服务器硬件上，处理 100 页 PDF 通常在 **200 ms** 以下。

### 常见问题及解决方案

- **文件路径不正确** – 验证路径字符串并确保文件对运行进程可访问。  
- **不支持的格式** – 检查格式列表；如果缺少某种格式，请考虑先进行转换。  
- **性能瓶颈** – 对于非常大的文件，启用流式选项或批量处理页面以限制内存使用。

## 实际应用

了解文档的元数据可实现多种实际场景：

1. **文档管理系统 (DMS)** – 基于类型、大小或页数自动进行分类和索引。  
2. **合规审计** – 在归档前验证机密文件是否包含所需的元数据。  
3. **数据迁移** – 按属性对文件进行分组，以简化批量迁移任务。

## 性能考虑

- **高效资源使用** – 在 `using` 块中使用 `Redactor` 实例，以确保正确释放。  
- **异步模式** – 将元数据调用包装在 `Task.Run` 中或实现异步包装器，以保持桌面或 Web 应用中的 UI 线程响应。

## 常见问题

**Q: 我可以从哪些文档格式中提取元数据？**  
A: GroupDocs.Redaction 可读取超过 50 种格式的元数据，包括 PDF、DOCX、XLSX、PPTX、HTML 和常见图像类型。

**Q: 如何处理受密码保护的文件？**  
A: 将密码传递给 `Redactor` 构造函数；API 会在提取元数据之前解密文件。

**Q: 我可以处理的文件大小是否有限制？**  
A: 虽然没有硬性限制，但超过 2 GB 的文件可能需要额外的内存调优；性能随文件大小线性增长。

**Q: 我可以批量检索元数据吗？**  
A: 可以——遍历文件路径集合，对每个路径调用 `GetDocumentInfo()`；该库对并行执行是线程安全的。

**Q: 开发构建是否需要许可证？**  
A: 免费试用许可证足以用于开发和测试；生产部署需要商业许可证。

## 资源

- [文档](https://docs.groupdocs.com/redaction/net/)  
- [API 参考](https://reference.groupdocs.com/redaction/net)  
- [下载](https://releases.groupdocs.com/redaction/net/)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证信息](https://purchase.groupdocs.com/temporary-license/)

## 结论

您现在拥有使用 GroupDocs.Redaction .NET **检索元数据** 的完整分步指南。通过利用 `Redactor.GetDocumentInfo()` 方法，您可以快速读取文件元数据，支持合规工作流，并提升任何文档处理管道。探索其他 Redaction 功能——如内容遮蔽、水印和文档转换——以构建功能齐全的文档管理解决方案。

---

**最后更新：** 2026-06-06  
**测试环境：** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**作者：** GroupDocs  

## 相关教程

- [如何使用 GroupDocs.Redaction .NET 从流中提取文档元数据](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [使用 GroupDocs.Redaction for .NET 对文档元数据进行遮蔽的完整指南](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction for .NET 的文档加载教程](/redaction/net/document-loading/)