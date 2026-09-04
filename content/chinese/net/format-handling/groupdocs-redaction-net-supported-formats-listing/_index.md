---
date: '2026-07-20'
description: 了解如何使用 GroupDocs.Redaction .NET 列出格式，将此功能集成到文档工作流中，并提升性能。
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: 了解如何使用 GroupDocs.Redaction .NET 列出格式，查看分步指南，并获取在 .NET 应用程序中实现最佳性能的技巧。
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: 如何使用 GroupDocs.Redaction .NET 列出格式
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
title: 如何使用 GroupDocs.Redaction .NET 列出格式
type: docs
url: /zh/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 列出格式

管理各种文档类型是构建文档中心应用的开发者的日常现实。在本教程中，您将学习 **如何列出格式**，即 GroupDocs.Redaction .NET 能处理的格式，以便在处理前验证文件，为用户提供准确的选项，并保持工作流高效。

## 介绍

高效的文档处理始于准确了解库支持的文件类型。GroupDocs.Redaction 提供内置方法来检索此信息，帮助您构建动态 UI 元素、强制验证规则并避免运行时错误。下面您将找到从安装到实用代码片段和性能提示的全部内容，帮助您快速上手。

### 快速回答
- **“如何列出格式”是什么意思？** 它指的是检索 GroupDocs.Redaction 可以处理的文件扩展名集合。  
- **我需要许可证吗？** 是的，生产环境使用必须拥有有效的 GroupDocs.Redaction 许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。  
- **可用的格式有多少？** 开箱即支持超过 30 种输入和输出格式。  
- **需要任何特殊配置吗？** 除标准库初始化外无需额外配置。

## 什么是“如何列出格式”？

它涉及调用库的 FileType API，获取一个集合，其中每个条目包含文件扩展名和可读的名称。开发者随后可以遍历该集合，以构建验证规则、填充 UI 下拉框或记录受支持的类型，确保仅处理兼容的文档。

## 为什么要使用 GroupDocs.Redaction 列出格式？

GroupDocs.Redaction 支持 **30+** 种不同的文件类型——包括 PDF、DOCX、PPTX 以及图像格式——让您无需第三方转换器即可处理大多数企业文档。通过编程方式列出这些格式，您可以消除猜测、减少支持工单，并确保只有兼容的文件进入处理流水线。

## 前提条件

- **GroupDocs.Redaction for .NET** – 从官方网站下载最新包。  
- **.NET Framework 或 .NET Core** – 与您的开发环境兼容。  
- **Visual Studio**（或任何支持 C# 的 IDE）。  
- 基本的 C# 语法熟悉度。

## 设置 GroupDocs.Redaction for .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### 包管理器
`Install-Package GroupDocs.Redaction`

### NuGet 包管理器 UI
- 搜索 **“GroupDocs.Redaction”** 并安装最新版本。

### 许可证获取
GroupDocs 提供免费试用、用于评估的临时许可证或完整购买选项。访问 GroupDocs 网站获取相应的许可证文件。

### 基本初始化和设置
添加包后，引用命名空间并创建 `Redactor` 实例：

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## 实施指南

### 如何使用 GroupDocs.Redaction .NET 列出格式？
加载库，调用静态帮助方法并对结果进行排序——只需两行代码即可获得可直接使用的集合。使用 `FileType.GetSupportedFileFormats()` 检索 `IEnumerable<FileType>`，其中包含每种格式的扩展名和显示名称，然后按扩展名排序以获得整洁的 UI 列表。

### 检索受支持的文件格式

#### 概述
目标是获取 GroupDocs.Redaction 能处理的文件类型列表，以便将其集成到验证逻辑、UI 下拉框或日志机制中。

#### 步骤实现

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` 返回库识别的所有格式。该方法属于 `GroupDocs.Redaction.FileType` 类，封装了文件扩展名和友好名称等元数据。

**2. Display Supported File Types**  
遍历集合并输出每种格式的扩展名和描述。内联代码示例：

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

该代码段会打印类似 “.pdf – Portable Document Format” 的有序列表，非常适合用于填充 UI 元素。

### 故障排除提示
- **Missing Package** – 验证 NuGet 包引用并在需要时恢复包。  
- **Incorrect License Path** – 确保许可证文件已复制到输出目录，或提供绝对路径。  
- **Unsupported Extension** – 若某格式未列出，请确认您使用的是最新库版本；新版会添加更多格式。

## 实际应用

了解受支持的文件格式可解锁多种真实场景：

1. **文档管理系统** – 根据受支持列表验证上传，防止处理失败。  
2. **内容安全** – 仅对引擎能够安全修改的文件类型应用脱敏规则。  
3. **批量处理流水线** – 在调用脱敏前过滤大批量文件，节省 CPU 和内存。

## 性能考虑

- **Memory Footprint** – 列出格式是轻量操作，不会将任何文档加载到内存中。  
- **Batch Operations** – 处理数百个文件时，建议仅检索一次格式列表并复用，以避免冗余调用。  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` 是线程安全的，可在并行任务中直接调用，无需同步。

## 结论

您现在拥有使用 GroupDocs.Redaction .NET **如何列出格式** 的完整、可投入生产的方案。通过集成此功能，您可以增强验证、提升用户体验，并保持文档流水线的稳健性。

### 接下来的步骤
- 探索 `Redactor` API，根据文件类型应用脱敏规则。  
- 将格式列表与前端下拉框结合，实现无缝文件选择。  
- 查看性能指南，优化大规模批处理作业。

## 常见问题

**Q: 可以在不初始化 Redactor 实例的情况下检索格式列表吗？**  
A: 可以，`FileType.GetSupportedFileFormats()` 为静态方法，无需 `Redactor` 对象。

**Q: 列表是否同时包含输入和输出格式？**  
A: 该方法返回库既能读取又能写入的所有格式；每个 `FileType` 都包含 `CanRead` 和 `CanWrite` 标志。

**Q: 支持的格式列表更新频率如何？**  
A: GroupDocs 随每个库版本发布格式更新；在运行时检查列表可确保始终拥有最新集合。

**Q: 有办法仅筛选 PDF 兼容的格式吗？**  
A: 可以，根据 `format.Extension == ".pdf"` 或 `format.Name.Contains("PDF")` 进行过滤。

**Q: 此方法在 .NET Core 2.1 上能工作吗？**  
A: 该方法要求 .NET Core 3.1 或更高版本，早期运行时不受支持。

## FAQ 部分
1. **如何安装 GroupDocs.Redaction for .NET？**  
   使用 CLI 命令 `dotnet add package GroupDocs.Redaction` 或通过 NuGet 包管理器 UI 安装。  
2. **检索受支持格式时常见问题有哪些？**  
   确保所有依赖已恢复，并引用正确的命名空间 (`GroupDocs.Redaction`)。  
3. **可以在非 .NET 应用中使用此功能吗？**  
   本教程聚焦 .NET，但 GroupDocs 也提供 Java、Python 等平台的类似 API。  
4. **如何优化使用 GroupDocs.Redaction 时的性能？**  
   重用格式列表，避免仅检查兼容性时加载完整文档，并在批处理作业中监控内存使用。  
5. **GroupDocs.Redaction 支持哪些文件类型？**  
   库支持 30+ 种格式，包括 PDF、DOCX、PPTX、XLSX、BMP、PNG、JPEG 等。使用 `FileType.GetSupportedFileFormats()` 可查看完整列表。

## 资源
- [文档](https://docs.groupdocs.com/redaction/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-07-20  
**测试环境：** GroupDocs.Redaction 4.2.0 for .NET  
**作者：** GroupDocs  

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

## 相关教程

- [GroupDocs.Redaction .NET 格式处理教程](/redaction/net/format-handling/)
- [GroupDocs.Redaction for .NET 文档加载教程](/redaction/net/document-loading/)
- [GroupDocs.Redaction .NET 文档保存教程](/redaction/net/document-saving/)