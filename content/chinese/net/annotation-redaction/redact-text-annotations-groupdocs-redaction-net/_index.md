---
date: '2026-05-27'
description: 了解如何使用 GroupDocs.Redaction for .NET 对 PDF 中的注释进行脱敏，包括设置、正则表达式脱敏和性能技巧。
keywords:
- how to redact annotations
- apply redaction to pdf
- pdf annotation redaction
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  headline: How to Redact Annotations Using GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  name: How to Redact Annotations Using GroupDocs.Redaction for .NET
  steps:
  - name: Create a Redactor instance (definition anchor)
    text: '`Redactor` is the entry point for all redaction operations; you pass the
      source file path to its constructor.'
  - name: Define your regular expression (definition anchor)
    text: '`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity
      (`i`) and multi‑line mode (`m`) directly in the pattern. - `(?im...)`: Enables
      case‑insensitivity (`i`) and multi‑line search (`m`).'
  - name: Apply the redaction (definition anchor)
    text: '`AnnotationRedaction` is a specialized rule that scans annotation objects
      and replaces matching text with a black rectangle. **Explanation:** - **Parameters:**
      The regex pattern tells the engine which text to target. - **Return Values:**
      This method modifies the document in place; no return value is'
  - name: Save the redacted document (definition anchor)
    text: '`Redactor.Save` writes the modified file to disk, preserving the original
      format unless you specify otherwise.'
  type: HowTo
- questions:
  - answer: Yes. Open the document with `Redactor(string path, string password)` and
      then apply your redaction rules as usual.
    question: Can I redact annotations in password‑protected PDFs?
  - answer: The API works on a copy in memory; the original file remains unchanged
      until you explicitly call `Save`.
    question: Does GroupDocs.Redaction modify the original file?
  - answer: All standard PDF annotation types—including comments, highlights, and
      sticky notes—are fully supported.
    question: How many annotation types are supported?
  - answer: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and
      render it in your UI for a quick preview.
    question: Is there a way to preview redactions before saving?
  - answer: The library can handle files up to **2 GB**; larger files should be split
      before processing.
    question: What is the maximum file size I can process?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction for .NET 对注释进行脱敏
type: docs
url: /zh/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/
weight: 1
---

# 如何使用 GroupDocs.Redaction for .NET 对注释进行脱敏

如果您需要在 PDF 或 Word 文件中 **编辑注释**，您来对地方了。本指南将引导您完成安装 GroupDocs.Redaction for .NET、配置基于正则表达式的注释编辑，以及针对大规模工作负载的性能优化。完成后，您只需几行 C# 代码即可隐藏敏感的评论、备注和其他元数据。

## 快速答案
- **哪个库处理注释编辑？** GroupDocs.Redaction for .NET.  
- **我可以使用正则表达式吗？** 是的——API 接受完整的 .NET 正则表达式语法。  
- **开发需要许可证吗？** 免费试用可用于测试；生产环境需要付费许可证。  
- **它兼容 .NET 6 和 .NET Core 吗？** 完全支持 .NET Framework 4.5+、.NET Core 3.1+ 和 .NET 6+。  
- **大文件的编辑速度如何？** 优化的模式可以在普通服务器上在 5 秒以内处理 500 页的 PDF。

## 什么是注释编辑？
注释编辑会永久删除或遮蔽文档评论、备注、便签以及其他元数据对象中的文本。通过擦除这些隐藏信息，该技术确保机密数据无法被提取或查看，即使文件被分发或在其他应用程序中打开，也能保持隐私和合规性。

## 为什么对 PDF 注释进行编辑？
GroupDocs.Redaction 支持 **30+ 文档格式**，并且能够在不将整个内容加载到内存中的情况下处理高达 **2 GB** 的文件。使用内置的正则表达式引擎相比手动字符串搜索可将处理时间降低最多 **70 %**，这使其非常适合高容量的法律或金融工作流。

## 前置条件

在开始之前，请确认以下内容：

- **GroupDocs.Redaction** 库（最新 NuGet 版本）。  
- 兼容的 **.NET** 运行时（Framework 4.5+、.NET Core 3.1+、.NET 5/6）。  
- IDE，例如 **Visual Studio 2022** 或 **VS Code**。  
- 基本的 C# 知识以及对正则表达式的熟悉。  

## 如何使用 GroupDocs.Redaction 对注释进行编辑？

加载源文档，定义正则表达式模式，应用 `AnnotationRedaction`，并保存结果——全部在简洁的三步流程中完成。以下章节将对每一步进行详细说明，并提供您需要替换为自身值的代码占位符。

### 步骤 1 – 通过 .NET CLI 安装库
**答案：** 在项目文件夹中运行 `dotnet add package GroupDocs.Redaction`；CLI 将下载最新的稳定包并自动更新项目文件。  

```bash
dotnet add package GroupDocs.Redaction
```

### 步骤 2 – 通过包管理器控制台安装库
**答案：** 在 Visual Studio 的包管理器控制台中执行 `Install-Package GroupDocs.Redaction`；该命令会解析依赖并将引用添加到项目中。  

```powershell
Install-Package GroupDocs.Redaction
```

### 步骤 3 – 初始化 Redactor（定义锚点）
`Redactor` 类是加载文档并应用编辑规则的核心引擎。  

```csharp
using System;
using GroupDocs.Redaction.Redactions;

namespace DocumentRedaction
{
    class Program
    {
        static void Main(string[] args)
        {
            string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\annotated.xlsx"; // Replace with actual document path.
            
            using (Redactor redactor = new Redactor(sourceFile))
            {
                // Your redaction logic will go here.
            }
        }
    }
}
```

## 应用注释编辑

### 步骤 1: 创建 Redactor 实例（定义锚点）
`Redactor` 是所有编辑操作的入口；您需要将源文件路径传递给其构造函数。  

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further processing will occur here.
}
```

### 步骤 2: 定义正则表达式（定义锚点）
`Regex` 是 .NET 用于评估模式的类；您可以在模式中直接启用不区分大小写 (`i`) 和多行模式 (`m`)。  

```csharp
string pattern = "(?im:john)";
```
- `(?im...)`：启用不区分大小写 (`i`) 和多行搜索 (`m`)。

### 步骤 3: 应用编辑（定义锚点）
`AnnotationRedaction` 是一种专用规则，扫描注释对象并将匹配的文本替换为黑色矩形。  

```csharp
redactor.Apply(new AnnotationRedaction(pattern));
```

**说明：**  
- **参数：** 正则表达式模式告诉引擎要定位的文本。  
- **返回值：** 此方法在原位修改文档；不需要返回值。

### 步骤 4: 保存编辑后的文档（定义锚点）
`Redactor.Save` 将修改后的文件写入磁盘，除非另行指定，否则保持原始格式。  

```csharp
guardedRedactor.Save();
```

## 常见问题及解决方案
- **未找到匹配项：** 仔细检查正则表达式语法；使用相同 .NET 引擎的在线测试工具。  
- **文件访问错误：** 确保应用程序对源文件夹和目标文件夹具有读/写权限。  
- **性能瓶颈：** 对于超过 500 页的文档，使用并行批处理并在可能的情况下复用单个 `Redactor` 实例。

## 常见问答

**Q: 我可以对受密码保护的 PDF 进行注释编辑吗？**  
A: 可以。使用 `Redactor(string path, string password)` 打开文档，然后像往常一样应用编辑规则。

**Q: GroupDocs.Redaction 会修改原始文件吗？**  
A: API 在内存中的副本上工作；原始文件保持不变，直到您显式调用 `Save`。

**Q: 支持多少种注释类型？**  
A: 所有标准的 PDF 注释类型——包括评论、突出显示和便签——均得到完整支持。

**Q: 是否有办法在保存前预览编辑效果？**  
A: 使用 `Redactor.GetRedactedDocument()` 获取内存流，并在 UI 中渲染以快速预览。

**Q: 我能处理的最大文件大小是多少？**  
A: 该库可处理最高 **2 GB** 的文件；更大的文件应在处理前拆分。

## FAQ 部分

1. **什么是 GroupDocs.Redaction？**  
   - 它是一个用于从各种文档格式中编辑敏感信息的 .NET 库。

2. **如何处理复杂的注释？**  
   - 使用高级正则表达式，并在应用于关键文档之前彻底测试。

3. **可以撤销编辑吗？**  
   - 保存后更改是永久的；请始终备份原始文件。

4. **我可以将 GroupDocs.Redaction 集成到现有应用程序中吗？**  
   - 可以，它的 API 允许与其他基于 .NET 的系统无缝集成。

5. **GroupDocs.Redaction 支持哪些格式？**  
   - 它支持包括 Word、PDF、Excel 在内的多种文档类型。

## 资源

- [GroupDocs Redaction 文档](https://docs.groupdocs.com/redaction/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)
- [临时许可证获取](https://purchase.groupdocs.com/temporary-license/) 

---

**最后更新：** 2026-05-27  
**测试版本：** GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs

## 相关教程

- [使用 GroupDocs.Redaction for .NET 高效移除文档注释](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET 注释编辑教程](/redaction/net/annotation-redaction/)
- [如何使用 GroupDocs.Redaction .NET 加载和编辑文档：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)