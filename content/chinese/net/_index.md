---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: 了解如何使用 GroupDocs.Redaction for .NET 对 PDF 页面进行编辑、删除 PDF 注释以及编辑 Excel
  单元格——这是一款安全、跨平台的文档编辑 API。
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: GroupDocs.Redaction for .NET 教程
og_description: 使用 GroupDocs.Redaction for .NET 快速编辑 PDF 页面。该 API 可删除 PDF 注释、编辑 Excel
  单元格，并在 30 多种格式中保护敏感数据。
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: 如何编辑 PDF 页面 – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: 如何使用 GroupDocs.Redaction for .NET 对 PDF 页面进行编辑
type: docs
url: /zh/net/
weight: 10
---

# 如何使用 GroupDocs.Redaction for .NET 对 PDF 页面进行编辑

如果您需要快速且可靠地 **编辑 PDF 页面**，GroupDocs.Redaction for .NET 为您提供功能齐全、跨平台的 API，能够从超过 30 种文件格式中移除敏感内容。无论您是在构建合规驱动的工作流、文档管理门户，还是以隐私为先的应用程序，该库都能让您永久擦除机密数据，同时保留文档其余结构。

**GroupDocs.Redaction for .NET 是一个 .NET 库，可实现对超过 30 种文档格式的敏感内容进行永久删除。** 它支持高容量处理，能够在不将整个文档加载到内存中的情况下处理数百页的文件，并提供将文本转换为图像的光栅化选项，以增强安全性。

{{% alert color="primary" %}}
GroupDocs.Redaction for .NET 提供了全面的教程和示例套件，帮助您在 .NET 应用程序中实现安全的文档编辑。无论是基本的文本替换还是高级的元数据清理，这些资源涵盖了编辑文档中敏感信息的关键技术。了解如何从包括 PDF、Word、Excel、PowerPoint 和图像在内的各种文档格式中永久删除私人数据，实现精确控制并彻底清除机密内容。我们的分步指南帮助您掌握标准和高级编辑功能，以满足合规要求并有效保护敏感信息。
{{% /alert %}}

## 快速答案
- **GroupDocs.Redaction 能编辑整个 PDF 页面吗？** 是的，您可以使用单个 API 调用删除单页或页码范围。  
- **它是否支持移除 PDF 注释？** 当然——注释、评论和标记都可以一步完成。  
- **我可以在不转换为 PDF 的情况下编辑 Excel 单元格吗？** 可以，库直接针对 Excel 工作表。  
- **是否支持从流加载 PDF？** API 接受 `Stream` 对象，支持内存中处理。  
- **兼容哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 在 PDF 中，编辑指的是什么？
编辑是指对文档中的敏感内容进行永久删除或遮蔽，使其以后无法恢复或查看。在 PDF 文件中，编辑可以针对文本、图像、注释或整页进行，结果是一个保持原始布局的净化文件。

## 为什么使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction for .NET 提供了强大且高性能的解决方案，能够处理大型文档，同时确保敏感数据的完整删除，内置光栅化、广泛的格式支持以及详细的审计日志，使其成为合规驱动的应用程序和企业环境的理想选择。

- **支持 30+ 种格式** – 包括 PDF、DOCX、XLSX、PPTX、HTML 和常见图像类型。  
- **可扩展性能** – 在普通服务器上可在 5 秒内处理 500 页 PDF，无需将整个文件加载到内存。  
- **内置光栅化** – 将编辑后的页面转换为图像，确保没有隐藏文本。  
- **合规就绪** – 通过审计日志满足 GDPR、HIPAA 和 PCI‑DSS 要求。

## 前置条件
- .NET Framework 4.5+ **或** .NET Core 3.1+ 已在您的开发机器上安装。  
- 有效的 GroupDocs.Redaction 许可证（提供试用评估）。  
- 可访问您计划处理的 PDF、Excel 或 Word 文件。

## 分步编辑 PDF 页面

Redactor 是 GroupDocs.Redaction 中的核心类，用于加载、修改和保存文档。RemovePages 方法从已加载的文档中删除指定的页面。

加载 PDF，定义要删除的页面，执行编辑，并保存结果。以下直接答案解释了核心模式：

使用 `Redactor.Load(streamOrPath)` 加载目标 PDF，调用 `Redactor.RemovePages(pageNumbers)` 删除不需要的页面，最后使用 `Redactor.Save(outputPath)` 保存——此三步流程可在大多数文档中在不到一秒的时间内完成页面编辑。

### 步骤 1：加载 PDF
您可以从磁盘、内存流或远程来源打开文件。API 同时接受文件路径字符串和 `Stream` 对象，非常适合接收上传的 Web 服务。

### 步骤 2：定义要编辑的页面
将零基页面索引列表或类似 `"1-3,5"` 的范围字符串传递给 `RemovePages` 方法。库会验证范围，并在页面不存在时抛出明确的异常。

### 步骤 3：保存已清理的文档
使用所需的输出格式调用 `Save`。您可以保留原始 PDF，导出为光栅化 PDF，或将结果直接流式传输到客户端响应。

## 常见问题及解决方案
- **问题：** 编辑似乎生效，但原始文本仍可搜索。  
  **解决方案：** 在保存前启用光栅化 (`Redactor.Rasterize = true`)；这会将页面转换为图像，去除隐藏的文本层。  

- **问题：** 大型 PDF 导致 OutOfMemory 异常。  
  **解决方案：** 使用 `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` 将文件分块处理。  

- **问题：** 注释未被删除。  
  **解决方案：** 在加载文档后调用 `Redactor.RemoveAnnotations()`；此方法会剥离评论、高亮和表单字段。

## 常见问答

**问：我可以编辑 PDF 页面而不影响文档其余布局吗？**  
答：是的，库会删除指定页面，同时保留页码、书签以及剩余内容的交叉引用。

**问：是否可以仅编辑 PDF 注释？**  
答：完全可以。使用 `Redactor.RemoveAnnotations()` 在一次调用中剥离所有注释对象。

**问：如何直接编辑 Excel 单元格？**  
答：使用 `Redactor.LoadExcel(path)` 加载工作簿，然后调用 `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` 并保存。

**问：GroupDocs.Redaction 是否支持从流加载 PDF？**  
答：是的，您可以将任意 `System.IO.Stream` 传递给 `Load` 方法，这对于处理通过 ASP.NET Core 控制器上传的文件非常理想。

**问：针对高容量生产使用，推荐哪种授权模式？**  
答：计量授权允许您按编辑操作付费，能够随使用峰值灵活、成本有效地扩展。

---

**最后更新：** 2026-10-06  
**测试环境：** GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs  

---

### GroupDocs.Redaction for .NET 教程 – 如何编辑 PDF 页面

### [入门教程](./getting-started/)

如果您是 GroupDocs.Redaction 的新手，请从此开始。本教程将引导您完成安装、授权以及在 .NET 中创建第一个编辑项目的过程。您将了解如何打开文档、定义简单的编辑规则并保存已清理的文件。

### [高级编辑技术](./advanced-redaction/)

深入了解自定义编辑处理程序、策略、回调以及 AI 辅助编辑。本指南展示了如何构建灵活的流水线，以 **编辑 PDF 页面**、处理复杂的文档结构，并集成机器学习模型实现更智能的内容检测。

### [注释编辑教程](./annotation-redaction/)

注释通常包含机密备注。学习如何定位、修改或完全删除 PDF、Word 文件以及其他支持格式中的注释、评论和审阅标记。

### [文档信息教程](./document-information/)

了解文档的元数据是安全编辑的第一步。本教程解释了如何检索文档属性、枚举支持的格式，并在进行任何编辑之前生成预览图像。

### [文档加载教程](./document-loading/)

文档可以位于磁盘、流或身份验证层后。学习安全加载本地文件、内存流以及受密码保护文档的最佳实践。

### [文档保存教程](./document-saving/)

编辑后您需要持久化已清理的文件。本指南涵盖以原始格式保存、导出为光栅化 PDF，以及将结果直接流式传输到客户端应用程序。

### [格式处理教程](./format-handling/)

GroupDocs.Redaction 支持广泛的格式。探索如何处理不同文件类型、创建自定义格式处理程序，并扩展库以覆盖特定的文档标准。

### [图像编辑教程](./image-redaction/)

图像可能隐藏敏感的视觉数据。学习如何编辑特定图像区域、剥离嵌入的图片，并清理图像元数据，以确保没有隐藏信息。

### [授权与配置教程](./licensing-configuration/)

正确的授权对生产使用至关重要。本教程展示了如何应用授权、配置运行时设置，以及实现计量授权以实现可扩展部署。

### [元数据编辑教程](./metadata-redaction/)

元数据常常泄露机密细节。按照本指南从 PDF、Word、Excel 和 PowerPoint 文件中删除文档属性、隐藏评论及其他元数据。

### [OCR 集成教程](./ocr-integration/)

处理扫描的 PDF 或图像时，OCR 是必不可少的。学习集成 OCR 引擎、提取可搜索文本，然后 **编辑包含敏感信息的 PDF 页面**。

### [页面编辑教程](./page-redaction/)

有时您需要删除整页。本教程演示如何删除单页、页码范围以及基于内容有条件地删除页面。

### [PDF 专用编辑教程](./pdf-specific-redaction/)

PDF 具有层、注释和表单字段等独特特性。掌握仅针对 PDF 的编辑技术，包括内容过滤和保持文档完整性。

### [光栅化选项教程](./rasterization-options/)

光栅化 PDF 将内容转换为图像，使数据提取变得不可能。学习配置噪声、倾斜、灰度和边框，并了解如何 **保存光栅化 PDF** 文件以实现最高安全性。

### [电子表格编辑教程](./spreadsheet-redaction/)

Excel 电子表格常包含机密单元格。本指南展示如何定位并 **编辑 Excel 单元格**、隐藏公式以及保护敏感工作表。

### [文本编辑教程](./text-redaction/)

文本是最常需要保护的数据类型。按照分步说明进行精确短语匹配、正则表达式编辑和区分大小写搜索，包括如何高效 **编辑 Word 文本**。

## 相关教程

- [如何删除注释 – GroupDocs.Redaction .NET 注释编辑教程](/redaction/net/annotation-redaction/)
- [如何使用 GroupDocs.Redaction for .NET 删除 PDF 的最后一页](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [如何编辑 PDF 并保存为光栅化 PDF，使用 GroupDocs.Redaction for .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)