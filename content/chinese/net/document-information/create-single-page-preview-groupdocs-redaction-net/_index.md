---
date: '2026-06-06'
description: 了解如何使用 GroupDocs.Redaction for .NET 将页面转换为 PNG 并预览 PDF 页面。一步一步的指南、代码片段和实战技巧。
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: 使用 GroupDocs.Redaction .NET 将页面转换为 PNG
type: docs
url: /zh/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# 将页面转换为 PNG 使用 GroupDocs.Redaction .NET

创建大型文档的单页预览是当您只想共享相关信息片段时的常见需求。在本教程中，您将学习 **如何将页面转换为 PNG**，使用 GroupDocs.Redaction for .NET 配置预览输出，并将结果集成到您的应用程序中。我们将逐步介绍前提条件、安装、代码设置以及实用技巧，让您能够在几分钟内开始生成单页 PNG 预览。

## 快速答案
- **我可以仅生成单页的 PNG 预览吗？** 是的，使用 `PreviewOptions` 指定页码和格式。  
- **GroupDocs.Redaction 支持哪些预览格式？** PNG 为默认格式，但也支持 JPEG 和 BMP。  
- **开发是否需要许可证？** 免费试用可用于测试；商业使用需购买正式许可证。  
- **这在 .NET Core 和 .NET Framework 上都能工作吗？** 当然——该库面向 .NET Standard 2.0+。  
- **该过程对大文件是否内存高效？** 是的，API 会流式处理页面，避免完整加载文档。

## 什么是将页面转换为 PNG？
**将页面转换为 PNG** 是指从受支持的文档（PDF、DOCX、PPTX 等）中提取单页，并将该页渲染为 Portable Network Graphics（PNG）图像。生成的图像保留原始页面的视觉布局、字体和图形，便于您共享清晰的快照，同时隐藏文档的其余部分。

## 为什么使用单页预览？
生成单页 PNG 预览可以降低带宽消耗、加快加载速度，并通过仅展示所需内容来保护敏感信息。GroupDocs.Redaction 能在典型服务器硬件上将 300 页 PDF 渲染为 200 KB PNG，耗时不足 0.5 秒，适用于 Web 门户和报表工具。

## 前提条件

- **GroupDocs.Redaction for .NET** – 执行文档编辑和预览生成的核心库。  
- **System.IO** – .NET 标准的文件处理命名空间。  
- .NET Core 3.1+ 或 .NET Framework 4.6.1+（任何支持 .NET Standard 2.0 的平台）。  
- 基本的 C# 知识以及对 NuGet 包管理的熟悉。

## 设置 GroupDocs.Redaction for .NET

### 安装信息

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- 在 Visual Studio 中打开您的项目。  
- 选择 **Manage NuGet Packages**。  
- 搜索 **GroupDocs.Redaction** 并安装最新的稳定版本。

### 获取许可证步骤
要运行该库，您需要有效的许可证。您可以先使用免费试用或请求临时密钥：

1. 访问 [GroupDocs 网站](https://purchase.groupdocs.com/temporary-license) 以请求临时许可证。  
2. 按照邮件中的说明将许可证文件添加到项目中。

### 基本初始化和设置
`RedactionEngine` 类是所有操作的入口点，包括预览生成。  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## 实现指南

### 概述
本节展示如何通过配置 `PreviewOptions` 并调用预览 API 来 **将页面转换为 PNG**。该方法适用于 PDF、DOCX、PPTX 以及 GroupDocs.Redaction 支持的许多其他格式。

### 步骤 1：准备环境
设置源文件路径和输出文件夹。使用 `Path.Combine` 构建跨平台路径。  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### 步骤 2：设置预览选项
`PreviewOptions` 允许您定义页码、图像尺寸和输出格式。该类是预览生成的配置中心。  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### 关键配置说明
- **Width & Height** – 调整这些值以匹配目标显示分辨率。  
- **PageNumbers** – 提供包含要渲染的确切页索引的数组（从零开始）。  
- **PreviewFormat** – PNG 为默认；如需更小的文件可切换为 `PreviewFormat.Jpeg`。

### 故障排除提示
如果未生成 PNG：

- 确认源文件路径正确且文件可访问。  
- 确保在调用任何 API 方法前已加载许可证文件。  
- 确认 `PreviewOptions.PageNumbers` 包含有效的页索引（例如，`0` 表示第一页）。

## 实际应用
创建单页 PNG 预览在许多场景中都很有用：

1. **客户演示** – 仅展示相关的幻灯片或合同条款。  
2. **内部审查** – 在不打开完整文档的情况下快速进行视觉检查。  
3. **内容摘要** – 将页面快照嵌入电子邮件或仪表板，提供即时上下文。  

将此功能与 CMS 或 CRM 集成，可为上传的文档自动生成缩略图，提升用户体验。

## 性能考虑
- **内存管理** – 使用后释放 `RedactionEngine` 实例以释放资源。  
- **异步执行** – 在 UI 应用中使用 `await engine.GeneratePreviewAsync(...)`，保持界面响应。  
- **库更新** – GroupDocs.Redaction 支持 **30 多种输入和输出格式**，并能在不将整个文件加载到内存的情况下处理最多 500 页的文档。保持包的更新以获得性能改进。

## 结论
现在，您已经拥有完整的、可投入生产的 **将页面转换为 PNG** 方法，可使用 GroupDocs.Redaction for .NET 生成单页预览。按照上述步骤，您可以将高质量的 PNG 快照嵌入任何 .NET 应用程序，提升文档共享，同时保持安全性和性能。

## 常见问题

**问：我可以为受密码保护的 PDF 生成预览吗？**  
答：可以，在初始化 `RedactionEngine` 时提供密码，预览将正常生成。

**问：如何将输出格式从 PNG 改为 JPEG？**  
答：在调用预览方法前设置 `options.PreviewFormat = PreviewFormat.Jpeg`。

**问：是否可以一次预览多个页面？**  
答：完全可以——将页面编号数组分配给 `options.PageNumbers`（例如 `new[] {0, 2, 4}`）。

**问：如果预览图像模糊该怎么办？**  
答：提升 `options.Width` 和 `options.Height` 到更高分辨率；库会相应地放大图像。

**问：这在 Linux 容器上能工作吗？**  
答：可以，GroupDocs.Redaction .NET 跨平台，可在支持 .NET Core 的 Docker 容器中运行。

## 资源
- [文档](https://docs.groupdocs.com/redaction/net/)  
- [API 参考](https://reference.groupdocs.com/redaction/net)  
- [下载最新版本](https://releases.groupdocs.com/redaction/net/)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证获取](https://purchase.groupdocs.com/temporary-license)

---

**最后更新：** 2026-06-06  
**测试环境：** GroupDocs.Redaction 5.6 for .NET  
**作者：** GroupDocs

## 相关教程

- [精通文档安全：使用 GroupDocs.Redaction .NET 对 Word 文档进行栅格化和编辑](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)  
- [使用 GroupDocs.Redaction .NET 删除 PDF 页面：完整指南](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)  
- [使用 GroupDocs.Redaction .NET 实现文档编辑：分步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)