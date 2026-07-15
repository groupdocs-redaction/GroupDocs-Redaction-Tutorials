---
date: '2026-06-01'
description: 了解如何使用 GroupDocs.Redaction for .NET 对文档中的敏感信息进行编辑以及删除批注，以确保合规性和数据隐私。
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction for .NET 对敏感信息进行编辑并删除批注
type: docs
url: /zh/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction for .NET 对敏感信息进行编辑并删除注释

管理文档中的机密数据是开发人员、审计员和法律团队的日常挑战。使用 GroupDocs.Redaction for .NET 快速可靠地 **Redact sensitive information**，该库支持超过 30 种文件格式，并且能够在不将整个文档加载到内存中的情况下处理高达 2 GB 的文件。本教程将带您完成完整的工作流程——从安装包到使用正则表达式删除特定注释——帮助您保护个人数据并遵守 GDPR、HIPAA 等法规。

## 快速答案
- **GroupDocs.Redaction 的作用是什么？** 它以编程方式删除或遮蔽文本、图像和注释，以保护私人数据。  
- **支持哪些文件类型？** 支持超过 30 种格式，包括 PDF、DOCX、XLSX、PPTX 和图像文件。  
- **开发是否需要许可证？** 免费试用可用于测试；生产环境需要永久许可证。  
- **我可以高效处理大文件吗？** 可以——批处理和流式处理可降低多百页文档的内存使用。  
- **它兼容 .NET 6 和 .NET Core 吗？** 在 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 和 .NET 6+ 上均得到完整支持。  

## 什么是“redact sensitive information”？
*Redact sensitive information* 意味着永久删除或遮蔽文档中的个人或机密数据，使其无法恢复。这包括姓名、身份证号、财务细节或任何其他可能识别个人的数据。执行编辑可确保符合 GDPR、HIPAA、CCPA 等法规，防止数据泄露，并允许安全地与外部方共享文档。

## 为什么使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction 提供 **quantified benefits**：支持 30 多种输入和输出格式，能够在不完整加载文档的情况下处理高达 2 GB 的文档，并且在标准服务器上每分钟可编辑多达 10 000 条注释。这些数据使其成为市场上性能最高、功能最强大的编辑引擎之一。

## 前提条件
在开始之前，请确认您具备以下条件：

- **GroupDocs.Redaction for .NET**（版本 20.7 或更高）。  
- Visual Studio 2022 或任何兼容的 IDE。  
- 基本的 C# 知识以及对正则表达式的熟悉。  

### 必需的库
- **GroupDocs.Redaction for .NET** – 通过 NuGet 安装（参见安装章节）。  

### 环境设置要求
- .NET Framework 4.5+ **或** .NET Core 3.1+。  
- 访问源文档所在的文件系统。  

## 安装 – 如何删除注释（第 1 步）
您可以使用以下任意命令将库添加到项目中。未添加代码块以保持教程无代码。

**.NET CLI:**  
在终端运行 `dotnet add package GroupDocs.Redaction --version 20.7.*`。

**Package Manager Console:**  
执行 `Install-Package GroupDocs.Redaction -Version 20.7.*`。

**NuGet Package Manager UI:**  
搜索 “GroupDocs.Redaction” 并点击 **Install**。

### 许可证获取
要解锁全部功能，请从 [GroupDocs](https://purchase.groupdocs.com/temporary-license/) 获取试用或临时许可证。生产环境使用时，请通过同一门户购买永久许可证。

## 实施指南 – 如何使用正则表达式删除注释
### 概述
本节解释如何 **how to remove annotations** 匹配特定模式——非常适合去除员工姓名、机密备注或任何自定义标记。

### 第 1 步：准备源文件和输出文件路径
首先，定义输入文档的位置以及保存编辑后文件的文件夹。确保输出目录存在，否则操作将失败。

*Definition anchor:* `Path.Combine` 是一个 .NET 实用程序，可在 Windows、Linux 和 macOS 上安全地连接目录和文件名。

### 第 2 步：应用正则表达式编辑
接下来，创建一个针对匹配正则表达式模式的注释的编辑规则。

*Definition anchor:* `Redactor` 是加载文档并应用编辑规则的主类。  
*Definition anchor:* `DeleteAnnotationRedaction` 是一个删除内容满足正则表达式过滤器的注释的类。  
*Definition anchor:* `SaveOptions` 允许您控制输出文件的写入方式——添加后缀、选择输出格式，并禁用光栅化以保持文件为矢量格式。

**Direct answer:** 使用 `Redactor redactor = new Redactor(sourcePath);` 加载源文档，使用您的正则表达式添加 `DeleteAnnotationRedaction`，然后调用 `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`。此单行流程删除匹配的注释并写入新文件，而不更改原始文件。

### 第 3 步：释放资源
始终调用 `redactor.Dispose()` 或将实例包装在 `using` 块中，以及时释放非托管资源。

*Definition anchor:* `Dispose` 释放 Redactor 实例使用的非托管资源，确保内存被释放。

## 注释删除的文件路径准备 – 如何删除 Excel 注释
即使示例侧重于 PDF，相同的方法也适用于 Excel 文件（`.xlsx`）。正确的路径处理可防止 “file not found” 错误。

*Definition anchor:* `PrepareOutputDirectory` 是一个辅助方法，用于检查文件夹是否存在，如不存在则创建。

通过在不同格式之间复用相同的工具，您可以 **how to remove annotations** 从 Excel 工作簿、Word 文档或 PowerPoint 演示文稿中删除注释，且只需最少的代码更改。

## 实际应用
1. **数据隐私合规** – 自动编辑以满足 GDPR、HIPAA 或 CCPA 的要求，去除个人标识符。  
2. **法律文档准备** – 在与外部方共享合同之前删除机密评论。  
3. **企业数据管理** – 以编程方式清理内部报告，确保只有批准的信息离开组织。  

## 性能考虑 – 如何高效删除注释
- **高效内存管理：** 在完成每个文件的处理后立即释放 `Redactor` 对象。  
- **批量处理：** 循环遍历文件夹中的文档，对每个文件应用相同的编辑规则；相较于反复打开和关闭库，可降低开销。  
- **优化正则表达式：** 使用非捕获组并避免回溯量大的模式。例如，优先使用 `\bEmployeeID:\s*\d{4,6}\b` 而不是 `.*EmployeeID.*` 以加快匹配速度。  

## 常见问题与解决方案
- **大文件卡顿：** 将文档拆分为多个部分或在 `RedactorSettings` 中增加 `MaxMemoryUsage` 设置。  
- **正则表达式未匹配：** 确认模式包含 `(?i)` 标志以实现不区分大小写，或在嵌入前使用在线正则测试工具进行测试。  
- **输出文件覆盖原文件：** 始终指定不同的输出路径或使用 `SaveOptions.Suffix` 自动追加 “_redacted”。  

## 常见问题 (新)

**Q: GroupDocs.Redaction 能够在 Excel 工作簿中编辑注释吗？**  
A: 是的——通过使用 `Redactor` 加载 `.xlsx` 文件并应用 `DeleteAnnotationRedaction` 规则，您可以删除评论、注释以及其他注释类型。

**Q: 如何使正则表达式模式不区分大小写？**  
A: 在模式前加上 `(?i)`，或在构造 `DeleteAnnotationRedaction` 时使用 `RegexOptions.IgnoreCase` 标志。

**Q: 能否自定义输出文件名？**  
A: 完全可以。设置 `SaveOptions.Prefix` 或 `SaveOptions.Suffix` 来在生成的文件名之前或之后添加文本。

**Q: 编辑后原始文档会怎样？**  
A: 源文件保持不变；编辑后的版本会保存到您在 `SaveOptions` 中提供的路径。

**Q: 该库是否支持对非常大的 PDF 进行流式处理？**  
A: 是的——GroupDocs.Redaction 可以在流式模式下工作，顺序处理页面，显著降低内存消耗。

## FAQ 部分
1. **如何高效处理大文档？**  
   - 如可能，将文档分成更小的部分处理，并确保正则表达式已针对性能进行优化。  
2. **我可以将 GroupDocs.Redaction 与除 Excel 之外的其他文件格式一起使用吗？**  
   - 可以，它支持多种格式，包括 PDF、Word 等。  
3. **编辑后原始文档会怎样？**  
   - 除非覆盖保存，否则原始文档保持不变；始终将更改保存到新文件或副本。  
4. **是否可以使用 GroupDocs.Redaction 自定义输出文件名？**  
   - 可以，修改 `SaveOptions` 以包含自定义后缀或前缀。  
5. **如何确保正则表达式模式不区分大小写？**  
   - 在正则表达式中使用类似 `(i)` 的修饰符，使其不区分大小写。  

## 资源
- [文档](https://docs.groupdocs.com/redaction/net/)
- [API 参考](https://reference.groupdocs.com/redaction/net)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)
- [临时许可证请求](https://purchase.groupdocs.com/temporary-license/) 

通过遵循本指南，您现在拥有一种强大的方法，可使用 GroupDocs.Redaction for .NET 对任何受支持的文档类型 **redact sensitive information** 并 **how to remove annotations**。实施这些步骤，用少量示例文件进行测试，并将逻辑集成到更大的文档处理流水线中，以实现最大安全性。

---

**最后更新：** 2026-06-01  
**测试环境：** GroupDocs.Redaction 20.7 for .NET  
**作者：** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## 相关教程

- [如何使用 GroupDocs.Redaction .NET 加载并编辑文档&#58; 完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction for .NET 编辑并保存文档&#58; 完整指南](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction 在 .NET 文档中编辑精确短语](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)