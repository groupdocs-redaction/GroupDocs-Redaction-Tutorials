---
date: '2026-07-20'
description: 了解如何使用 GroupDocs.Redaction for .NET 对文档进行编辑，隐藏敏感信息，并将编辑后的文件保存到内存流中。
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: 如何使用 GroupDocs.Redaction for .NET 对文档进行编辑。遵循此一步一步的指南，隐藏敏感信息并将编辑后的文件保存到内存流中。
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: 如何使用 GroupDocs.Redaction for .NET 对文档进行编辑
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: 如何使用 GroupDocs.Redaction for .NET 对文档进行编辑 – 完整指南
type: docs
url: /zh/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# 如何使用 GroupDocs.Redaction for .NET 对文档进行脱敏

在现代企业环境中，**如何编辑文档**是保护个人数据、商业机密和合规相关信息的关键技能。本指南将指导您如何从 Word、PDF 或图像文件中编辑敏感信息，并将编辑后的输出直接保存到内存流——全部使用 GroupDocs.Redaction for .NET。

## 快速答案
- **Redaction 的作用是什么？** 它永久地用占位符替换所选内容或将其删除，确保数据永不可恢复。  
- **支持哪些格式？** 超过 30 种文件类型，包括 PDF、DOCX、PPTX 和常见图像格式。  
- **可以在不写入磁盘的情况下进行编辑吗？** 可以——将结果保存到 `MemoryStream` 进行内存内处理。  
- **生产环境需要许可证吗？** 生产使用需要完整许可证；提供免费试用供评估。  
- **它兼容 .NET Core 吗？** 完全兼容——GroupDocs.Redaction 支持 .NET Framework 4.6+、.NET Core 3.1+ 以及 .NET 5/6/7。

## 什么是文档脱敏？
文档脱敏会永久删除或遮蔽文件中的机密文本、图像和元数据，确保隐藏的内容无法被恢复、查看或提取。它用占位符（如黑色矩形或自定义文本）替换敏感元素，并更新文档结构，使脱敏数据不可检索。

## 为什么使用 GroupDocs.Redaction 对文档进行脱敏？
GroupDocs.Redaction 支持 **30+ 种文件格式**，并且能够处理高达 **2 GB** 的文件而无需将整个文档加载到内存中，相比许多竞争对手提供 **30 % 更快的处理时间**。其 API 允许您通过一次方法调用应用精确短语、正则表达式或基于图像的脱敏，使其成为 .NET 开发者的最高效选择。

## 前置条件
- **GroupDocs.Redaction** NuGet 包（最新版本）。  
- 已安装 .NET Framework 4.6+ **或** .NET Core 3.1+。  
- 支持 C# 的 IDE，例如 Visual Studio 2022。  
- 基础的 C# 知识以及对文件 I/O 的了解。

### 必需的库和版本
- **GroupDocs.Redaction** – 始终使用最新发布以获取最新的脱敏算法和安全补丁。  
- **System.IO** – 用于流处理（.NET 内置）。

### 获取许可证的步骤
- **免费试用：** 在 GroupDocs 网站注册，获取 30 天试用。  
- **临时许可证：** 申请临时密钥用于开发测试。  
- **完整许可证：** 购买生产许可证以实现无限使用。

## 基本初始化和设置
`Redactor` 类是 GroupDocs.Redaction 中所有脱敏操作的入口点。安装 NuGet 包后，您需要使用源文档的路径实例化 `Redactor`。

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## 如何在文档中脱敏特定文本？
要脱敏特定文本，使用 `Redactor` 实例加载源文件，然后应用 `ExactPhraseRedaction` 来定位您想隐藏的确切字符串。API 会扫描文档，用选定的覆盖层替换每个匹配项，并将更改记录在更改日志中，便于您在保存前验证脱敏结果。

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

`ExactPhraseRedaction` 类会将每个出现的确切短语替换为黑色矩形（或您配置的任何自定义占位符）。

**步骤：**
1. **加载** – 创建指向您文件的 `Redactor` 实例。  
2. **应用** – 使用 `ExactPhraseRedaction`（或其他脱敏类型）调用 `Apply`。  
3. **检查** – 查看 `RedactorChangeLog` 以确认找到并替换了多少匹配项。  

## 如何将脱敏文档保存到内存流？
`MemoryStream` 是一种 .NET 流，数据存储在内存中，能够实现快速读写而无需磁盘 I/O。使用 `Save` 方法，您可以将脱敏输出直接写入 `MemoryStream`，随后可将其通过网络发送、存入数据库，或直接从 API 端点返回，而无需创建临时文件。

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**关键点：**
- `Save` 方法将脱敏输出写入任何 `Stream` 实现，包括 `MemoryStream`。  
- 不会创建临时文件，从而提升安全性和性能。  
- 您可以将其与 ASP.NET Core 的 `FileStreamResult` 结合使用，直接将文件返回给浏览器。

## 常见陷阱及解决方案
| 问题 | 原因 | 解决方案 |
|-------|----------------|-----|
| **未应用脱敏** | 短语的大小写与源文件不同。 | 使用 `ExactPhraseRedaction("John Doe", caseSensitive: false)` 或正则表达式脱敏以实现灵活匹配。 |
| **大文件导致内存不足** | 尝试将整个文件加载到内存中。 | GroupDocs.Redaction 在内部以流方式处理数据；请确保使用最新版本，它会分块处理文件。 |
| **保存的文件损坏** | 在发送前未重置流。 | 在 `redactor.Save(stream)` 之后，读取或返回之前将 `stream.Position = 0`。 |

## 常见问题解答

**问：我可以使用相同的 API 脱敏 PDF 文件吗？**  
答：可以——GroupDocs.Redaction 对 PDF、DOCX、PPTX 以及许多图像格式的处理方式一致，只需将 `Redactor` 指向 PDF 文件即可。

**问：文档转换为其他格式后，脱敏仍然有效吗？**  
答：完全有效——一旦脱敏，内容即被永久删除，无论后续进行何种转换。

**问：如何自定义脱敏的外观？**  
答：使用 `RedactionOptions` 设置覆盖颜色、不透明度，或用自定义字符串替换文本。

**问：可以使用正则表达式进行脱敏吗？**  
答：可以——`RegexRedaction` 允许您定义如信用卡号或电子邮件地址等模式。

**问：官方支持哪些 .NET 版本？**  
答：.NET Framework 4.6+、.NET Core 3.1+、.NET 5、.NET 6 和 .NET 7。

---

**最后更新：** 2026-07-20  
**测试环境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## 相关教程

- [如何使用 GroupDocs.Redaction .NET 加载并脱敏文档：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction .NET 将脱敏文档保存为原始格式](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [在 .NET 中使用流进行安全文档脱敏：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)