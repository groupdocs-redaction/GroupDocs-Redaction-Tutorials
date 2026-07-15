---
date: '2026-06-11'
description: 了解如何使用 GroupDocs.Redaction for .NET 从文档流中提取元数据，涵盖设置、代码示例和实际应用。
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction .NET 从文档流中提取元数据
type: docs
url: /zh/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 从文档流中提取元数据

## 快速回答
- **“提取元数据”是什么意思？** 它指在不将整个文档加载到内存中的情况下读取文件类型、页数和大小等属性。  
- **哪个库负责此功能？** GroupDocs.Redaction for .NET 提供了用于基于流的元数据提取的原生 API。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **我可以处理大于 1 GB 的 PDF 吗？** 可以——流式处理可在不加载整个文件的情况下处理高达 2 GB 的文件。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 和 .NET 6+。

## 什么是从流中提取元数据？
从流中提取元数据是指直接从 `Stream` 对象读取文档属性的过程，避免完整文件加载，从而节省内存和 CPU 时间。此技术非常适合批处理或资源受限的云服务。

## 为什么使用 GroupDocs.Redaction 进行元数据提取？
GroupDocs.Redaction 支持 **30+ 文件格式**（包括 PDF、DOCX、XLSX、PPTX 和图像类型），并且能够在 **2 GB** 大小的文档上运行，同时将内存使用保持在 **50 MB** 以下。其 `Redactor` API 只需一次调用即可获取所有关键文档信息，省去使用多个解析器的麻烦。

## 先决条件

- **GroupDocs.Redaction for .NET**（最新版本）  
- **.NET Framework** 4.5+ **或** **.NET Core/5+/6+**  
- 基本的 C# 知识以及对文件 I/O 的了解  
- Visual Studio 2019 或更高版本  

## 如何设置 GroupDocs.Redaction for .NET？
要开始使用 GroupDocs.Redaction，首先需要将库添加到项目中。可以通过 .NET CLI、Visual Studio 包管理器或 NuGet UI 完成。选择最适合你的工作流的方式；CLI 适合脚本化构建，UI 则提供图形化的版本和依赖项浏览。

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**  
- 在 Visual Studio 中打开 NuGet 包管理器。  
- 搜索 **"GroupDocs.Redaction"** 并安装最新版本。

### 许可证获取步骤
1. **免费试用：** 下载试用许可证以无限制地探索所有功能。  
2. **临时许可证：** 从 [GroupDocs](https://purchase.groupdocs.com/temporary-license/) 请求临时许可证以进行扩展测试。  
3. **购买：** 当准备好投入生产时，购买商业许可证。  

欲了解更多信息，请访问 [GroupDocs website](https://purchase.groupdocs.com/temporary-license/)。  

### 基本初始化和设置
`Redactor` 类是所有操作的入口，包括元数据提取。

`Redactor` 是表示文档实例的核心类，提供编辑、信息检索和文件操作的方法。安装后，你可以按下面的方式创建 `Redactor` 对象：

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

现在库已经准备就绪，让我们深入实现细节。

## 如何从文档流中提取元数据？
将文档以 **只读流** 方式加载，初始化 `Redactor`，并调用 `GetDocumentInfo()` 一次性获取元数据。这种方式避免将整个文件加载到内存中，对大尺寸 PDF 或数百页的 Office 文档尤为关键。

**直接答案：** 使用 `File.OpenRead()` 打开文件，将流传递给 `new Redactor(stream)`，随后调用 `redactor.GetDocumentInfo()` —— 该方法在仅三行代码内返回包含文件类型、页数和大小的对象。

### 步骤 1：准备源文件路径
首先确保源文件存在且输出文件夹已准备好。下面的辅助方法会检查输出目录并在需要时创建它。

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*为什么？* 这确保后续文件操作拥有有效路径，并防止 `DirectoryNotFoundException`。

### 步骤 2：打开文档流
使用 `File.OpenRead()` 将文件以 **只读流** 方式打开，即使是千兆字节级别的文件也能保持低内存占用。

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*为什么？* 流式处理允许按需读取文件的部分内容，而不是一次性加载整个文档。

### 步骤 3：使用文档流初始化 Redactor
`Redactor` 是提供文档级别操作（包括元数据提取）的主要 API 对象。

`Redactor` 表示从流加载的单个文档，并公开诸如 `GetDocumentInfo()` 的方法以快速获取属性。

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*为什么？* 使用流实例化 `Redactor` 可将对象绑定到底层文件，而无需完整加载。

### 步骤 4：检索文档元数据
调用 `GetDocumentInfo()` 返回一个 `DocumentInfo` 对象，其中包含文件格式、页数和文件大小。

`GetDocumentInfo()` 在一次调用中提取核心属性（格式、页数、大小），无需额外解析器。

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*为什么？* 这一步将所有关键元数据汇聚，便于记录、过滤或根据文档特性进行路由。

## 如何为处理后的文件准备输出目录？
在写入任何处理后的文件之前，确保目标文件夹已存在且可写。通过编程方式检查路径并在缺失时创建，可避免常见的运行时异常，如 `DirectoryNotFoundException` 或权限错误。此简单步骤还能让代码在本地、服务器或容器环境中保持可移植性。

**直接答案：** 使用 `Directory.Exists()` 检查文件夹是否存在，若不存在则调用 `Directory.CreateDirectory()` 创建——这行代码即可在任何写入操作前保证路径有效。

### 实现辅助方法
下面的方法封装了检查‑创建逻辑，并返回后续使用的已验证路径。

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*为什么？* 将此逻辑集中管理可减少重复代码，使代码库更易维护。

## 常见问题及解决方案
- **权限错误：** 确保应用程序在具有目标文件夹写入权限的账户下运行。  
- **无效路径：** 仔细检查路径分隔符（Windows 上为 `\\`，Linux/macOS 上为 `/`），以避免 `DirectoryNotFoundException`。  
- **大文件处理：** 及时释放流（使用 `using` 语句），以释放操作系统句柄并防止泄漏。

## 实际应用
1. **自动文档摄取：** 在上传时提取元数据，然后将其存入数据库，以实现快速搜索和合规报告。  
2. **法律与合规审计：** 提取页数和文件类型，以验证文档在归档前符合监管标准。  
3. **企业内容管理：** 使用元数据自动将文件分类到文件夹中，提高组织和检索速度。

## 性能考虑因素
- **内存管理：** 始终在 `using` 块中包装流，以便自动释放。  
- **批处理：** 将文档分批（10‑20 个）处理，以平衡吞吐量和内存使用，尤其在资源受限的服务器上。  
- **并行化：** 利用 `Parallel.ForEach` 处理独立文件，但需监控 CPU 和 I/O，防止争用。

## 结论
你现在拥有一份完整、可投入生产的 **如何使用 GroupDocs.Redaction for .NET 从文档流中提取元数据** 指南。按照上述步骤，你可以高效地检索文件类型、页数和大小，同时保持低内存占用并优雅地处理大文件。

**后续步骤**
- 在 [documentation](https://docs.groupdocs.com/redaction/net/) 中查看完整 API 参考。  
- 深入阅读 [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) 以探索编辑、加水印和 OCR 功能。  
- 尝试不同文件格式（PDF、DOCX、XLSX），观察元数据在不同类型间的差异。  
- 将提取的元数据集成到现有的文档管理或搜索解决方案中。

## 常见问题

**问：GroupDocs.Redaction 的元数据提取主要用例是什么？**  
答：它能够快速、内存高效地检索文档属性，用于索引、合规检查和自动路由，而无需打开完整文件。

**问：我可以从受密码保护的文件中提取元数据吗？**  
答：可以，在构造 `Redactor` 对象时提供密码，API 会在内部解密流。

**问：该库是否支持非 PDF 格式，如 DOCX 或 XLSX？**  
答：当然——GroupDocs.Redaction 处理超过 30 种格式，包括 PDF、DOCX、XLSX、PPTX 和常见图像类型。

**问：使用流可以处理多大的文档？**  
答：流式处理可在保持内存消耗低于 **50 MB** 的情况下处理高达 **2 GB** 的文件。

**问：如果遇到问题，我可以在哪里获取帮助？**  
答：访问 [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) 获取社区支持，或查阅官方文档中的故障排除章节。

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

**资源**  
- **Documentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## 相关教程

- [使用 GroupDocs.Redaction .NET API 的文档元数据检索](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)  
- [使用 GroupDocs.Redaction for .NET 对文档元数据进行编辑的完整指南](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)  
- [在 .NET 中使用流进行安全文档编辑：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)