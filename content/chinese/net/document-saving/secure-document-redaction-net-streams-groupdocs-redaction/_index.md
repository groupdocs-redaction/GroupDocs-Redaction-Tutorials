---
date: '2026-07-06'
description: 了解如何使用 GroupDocs.Redaction 通过 streams 对 .net 文档进行编辑。本教程涵盖设置、从流加载文档、应用编辑以及安全保存。
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: 使用 Streams 对 .net 文档进行编辑 – GroupDocs.Redaction 指南
type: docs
url: /zh/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# 使用流对 .net 文档进行编辑 – 综合指南

欢迎！在本教程中，您将通过使用 GroupDocs.Redaction 的流式处理，安全地 **redact documents .net**。我们将逐步演示您需要的全部内容——从安装库、从流加载文档、应用精确的编辑，到在不留下临时文件的情况下保存结果。

## 快速答案
- **What library handles redaction in .NET?** GroupDocs.Redaction for .NET.  
- **Can I load a file directly from a stream?** Yes—use `FileStream` with the Redactor constructor.  
- **Which formats are supported?** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **Do I need a license for production?** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **Is it safe for large files?** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## 什么是 “redact documents .net”？
**“Redact documents .net”** refers to the process of permanently removing or masking sensitive content from files using .NET libraries such as GroupDocs.Redaction. This ensures that confidential data never leaves your system in clear text. It is commonly used in legal, financial, and healthcare sectors to comply with privacy regulations such as GDPR and HIPAA, ensuring that sensitive data cannot be recovered after processing.

## 为什么在编辑时使用流？
GroupDocs.Redaction supports **70+ file formats** and can process files up to **2 GB** without fully loading them into memory. Streaming reduces I/O overhead, improves performance, and aligns with security best practices by keeping data in‑memory only for the short time needed for transformation.

## 前置条件

- **GroupDocs.Redaction for .NET** – install via NuGet (see below).  
- **.NET 6+** (or .NET Framework 4.6.1+).  
- Visual Studio 2022 or any compatible IDE.  
- Basic C# knowledge and familiarity with .NET streams.

## 安装 GroupDocs.Redaction

You can add the package with any of these commands:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Or locate “GroupDocs.Redaction” in the NuGet Package Manager UI and click **Install**.

### 许可证获取步骤
1. **Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – request a short‑term key for evaluation.  
3. **Full Purchase** – obtain a permanent license for production workloads.

Once installed, initialize the library in your code:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## 如何从流加载文档？

A `FileStream` provides a stream for reading from and writing to a file on disk. The `Redactor` class processes the document and applies redaction rules. Load your source file into a `FileStream`, then pass the stream to the `Redactor` constructor. This approach avoids writing the original file to a temporary location and keeps the data in memory only for the duration of processing. This method works for any supported format, including PDFs and Office documents.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## 如何使用流初始化 Redactor？

The `Redactor` class is the core engine that manipulates document content. By supplying the input stream, you enable in‑memory redaction without intermediate files. After creating the instance, you can chain redaction rules, preview changes, and configure options such as rasterization or encryption before committing the final document.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` is the primary class that provides methods to apply, preview, and commit redaction operations on a document loaded from a stream.

## 如何应用编辑？

You can add multiple redaction actions; the example below deletes all annotations, which is a common requirement for removing hidden comments or reviewer notes. Additional redaction types like `DeleteTextRedaction` or `ReplaceTextRedaction` can be combined to remove or mask specific strings, dates, or patterns across the document.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` is a built‑in redaction rule that permanently erases annotation objects such as comments, highlights, and stamps from the document.

## 如何保存已编辑的文档？

Saving directly to a `FileStream` ensures the output is written in a single pass, eliminating unnecessary temporary files. You may also specify output format, compression level, and optional password protection through the `SaveOptions` object to meet security requirements. Finally, close the output stream to release file handles and ensure the file is fully written to disk.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` lets you control how the document is persisted, including rasterization, encryption, and format selection.

## 常见使用场景
- **Legal document handling:** Strip confidential annotations before sharing drafts with clients.  
- **GDPR compliance:** Remove personal identifiers from contracts or employee records.  
- **Internal audit reports:** Hide reviewer notes while preserving the core content for distribution.

## 大文件性能技巧
1. **Dispose streams promptly** – `using` statements automatically close streams, freeing memory.  
2. **Batch processing** – Loop through a collection of files and reuse a single `Redactor` instance when format permits, reducing allocation overhead.  

## 故障排除

1. **File access denied** – Verify the application’s account has read/write permissions on the target folders.  
2. **Redaction not applied** – Ensure the redaction type you chose is compatible with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and DOCX).  

## 常见问题

**Q: Which file formats can be processed with streams?**  
A: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX, PPTX, and HTML—when using stream‑based APIs.

**Q: Can I preview redactions before saving?**  
A: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation that you can render or inspect programmatically.

**Q: How does the library handle password‑protected files?**  
A: Supply the password when opening the stream via `Redactor` overloads that accept `LoadOptions` containing the password.

**Q: Is there a limit on document size?**  
A: The engine can process files up to 2 GB; larger files should be split or processed in chunks to stay within memory limits.

**Q: Do I need a separate license for each deployment environment?**  
A: A single license key can be used across multiple environments as long as the usage complies with the licensing agreement.

## 结论
You now have a complete, step‑by‑step solution for **redact documents .net** using streams with GroupDocs.Redaction. By loading files directly from streams, applying targeted redactions, and saving without intermediate artifacts, you achieve both security and performance. Explore additional redaction types—such as text replacement or metadata removal—to tailor the process to your specific compliance needs.

---

**Last Updated:** 2026-07-06  
**Tested With:** GroupDocs.Redaction 5.0 for .NET  
**Author:** GroupDocs  

## 资源
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## 相关教程

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET&#58; A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redact and Save Documents with GroupDocs.Redaction for .NET&#58; A Complete Guide](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [How to Extract Document Metadata from Streams Using GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)