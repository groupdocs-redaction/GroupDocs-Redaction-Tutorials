---
date: 2026-10-16
description: 了解如何使用 GroupDocs.Redaction for .NET 删除 PDF 中的评论并删除所有批注。按照逐步指南来保护您的文档。
keywords:
- delete comments from pdf
- delete all annotations
- document security
lastmod: 2026-10-16
og_description: 了解如何使用 GroupDocs.Redaction for .NET 删除 PDF 中的评论并删除所有批注。按照逐步指南来保护您的文档。
og_image_alt: Guide showing how to remove PDF comments and annotations with GroupDocs.Redaction
  for .NET
og_title: 使用 GroupDocs.Redaction for .NET 删除 PDF 评论
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to delete comments from PDF and delete all annotations using
    GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
  headline: Delete comments from PDF with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to delete comments from PDF and delete all annotations using
    GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
  name: Delete comments from PDF with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF document
    text: Create a `Redactor` instance and open the target PDF file.
  - name: delete comment annotations
    text: Invoke the API to delete comment objects. You can either delete a specific
      comment by its identifier or purge every comment in one call.
  - name: save the sanitized PDF
    text: Save() writes the modified document back to a file or stream. Write the
      modified document back to disk or stream it to the client.
  type: HowTo
- questions:
  - answer: Yes, provide the password when loading the document; the SDK will decrypt,
      redact, and re‑encrypt the file automatically.
    question: Can I delete comments from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, apply the same redaction
      steps, and save each result.
    question: Does the SDK support batch processing of multiple PDFs?
  - answer: No. Only the annotation objects are removed; the underlying content and
      layout remain untouched.
    question: Will the visual appearance of the PDF change after removing comments?
  - answer: You can enumerate comment objects via the API, inspect their IDs or content,
      and decide which ones to remove.
    question: Is there a way to preview which comments will be deleted before applying
      the redaction?
  - answer: Yes, the .NET Core version runs seamlessly in Docker containers on Linux
      distributions.
    question: Does GroupDocs.Redaction work on Linux containers?
  type: FAQPage
tags:
- delete comments
- annotation redaction
- GroupDocs.Redaction
title: 使用 GroupDocs.Redaction for .NET 删除 PDF 评论
type: docs
url: /zh/net/annotation-redaction/
weight: 7
---

# 使用 GroupDocs.Redaction for .NET 删除 PDF 中的评论

如果您需要**删除 PDF 中的评论**并去除任何残留的审阅标记，您来对了教程。本指南将带您使用 GroupDocs.Redaction for .NET 去除评论、高亮和其他注释，确保机密笔记永不离开您的组织。您将了解为何需要删除注释、执行此任务的具体 API 调用，以及构建可靠、可重复的脱敏流水线的最佳实践提示。

## 快速答案

- **我可以只删除特定的评论吗？** 可以，您可以针对单个评论 ID 进行操作。  
- **是否可以一次性清除所有注释？** 当然——单个方法即可删除所有审阅元素。  
- **生产环境使用是否需要许可证？** 商业许可证是非评估部署的必需。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **SDK 能处理大型 PDF 吗？** 它可处理高达 2 GB 的文件，而无需将整个文档加载到内存中。

## 什么是 GroupDocs.Redaction for .NET？

GroupDocs.Redaction for .NET 是一款文档安全 SDK，能够在 PDF、Word 等多种文件格式中对敏感内容进行脱敏、删除或替换。它提供高级 API，实现精确的内容移除，同时保持文档完整性。该 SDK 支持批量处理，能够处理高达 2 GB 的大文件，并可在 .NET Framework 和 .NET Core 环境中运行。

## 为什么要删除注释并删除 PDF 中的评论？

GroupDocs.Redaction 支持**100 多种输入和输出格式**，并且可以在不完整加载内存的情况下处理高达**2 GB**的文档。删除评论可以消除隐藏的个人数据、审阅者备注或机密信息，这些往往在常规安全扫描中被忽视，从而在受监管行业中将合规风险降低至**95 %**。

## 前置条件

- .NET 开发环境（建议使用 Visual Studio 2022 或更高版本）  
- 已安装 GroupDocs.Redaction for .NET NuGet 包  
- 包含评论或其他审阅标记的 PDF 文件  
- 用于生产环境的有效 GroupDocs Redaction 许可证  

## 如何删除 PDF 中的评论？

Redactor 是 GroupDocs.Redaction 中的主要类，用于加载和修改文档。加载 PDF，调用针对评论对象的脱敏方法，然后保存清理后的文件。此操作会删除所有评论注释，同时保留文档其余布局和内容。API 还允许您指定要保留的评论 ID 列表，从而对最终文档中保留的备注进行细粒度控制。

### 步骤 1：加载 PDF 文档

创建一个 `Redactor` 实例并打开目标 PDF 文件。

### 步骤 2：删除评论注释

调用 API 删除评论对象。您可以通过标识符删除特定评论，或一次性清除所有评论。

### 步骤 3：保存已清理的 PDF

`Save()` 将修改后的文档写回文件或流。将修改后的文档写回磁盘，或将其流式传输给客户端。

## 如何删除所有注释？

`RemoveAllAnnotations()` 是一个方法，可删除已加载文档中的所有注释对象。GroupDocs.Redaction 提供一次性删除所有类型注释——评论、突出显示、印章及其他审阅标记的单一调用。您可以在保存之前调用 `Redactor.RemoveAllAnnotations()`，SDK 将自动清除所有注释对象，而不影响文档主体内容。这对于需要确保没有残留标记的批量处理流水线非常理想。

## 常见问题及解决方案

- **保存后注释仍然存在** – 确保在删除操作后调用 `redactor.Save()`。  
- **大文件性能下降** – 启用流式模式或在处理前将 PDF 拆分为更小的块。  
- **缺少许可证错误** – 验证许可证文件是否在应用启动时正确加载。

## 常见问答

**问：我可以删除受密码保护的 PDF 中的评论吗？**  
答：可以，在加载文档时提供密码；SDK 会自动解密、脱敏并重新加密文件。

**问：SDK 是否支持批量处理多个 PDF？**  
答：当然。遍历文件集合，应用相同的脱敏步骤，并保存每个结果。

**问：删除评论后 PDF 的视觉外观会改变吗？**  
答：不会。仅删除注释对象，底层内容和布局保持不变。

**问：是否有办法在执行脱敏前预览将要删除的评论？**  
答：您可以通过 API 枚举评论对象，检查其 ID 或内容，然后决定删除哪些。

**问：GroupDocs.Redaction 能在 Linux 容器中运行吗？**  
答：可以，.NET Core 版本可在 Linux 发行版的 Docker 容器中无缝运行。

## 可用教程

- [使用 GroupDocs.Redaction .NET 高效删除文档中的注释](./mastering-annotation-removal-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction for .NET 高效删除文档注释](./remove-annotations-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction .NET 脱敏注释中的文本：全面指南](./redact-text-annotations-groupdocs-redaction-net/)

## 其他资源

- [GroupDocs.Redaction for Net 文档](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 参考](https://reference.groupdocs.com/redaction/net/)
- [下载 GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-10-16  
**测试环境：** GroupDocs.Redaction 最新版本（截至 2026）  
**作者：** GroupDocs

## 相关教程

- [使用 GroupDocs.Redaction for .NET 删除 PDF 中的注释](/redaction/net/annotation-redaction/mastering-annotation-removal-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 脱敏注释](/redaction/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 加载文档](/redaction/net/document-loading/)