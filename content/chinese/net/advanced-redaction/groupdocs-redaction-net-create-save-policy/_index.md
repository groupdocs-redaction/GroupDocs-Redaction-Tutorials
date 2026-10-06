---
date: '2026-10-06'
description: 了解如何使用 GroupDocs.Redaction .NET 对敏感数据进行脱敏。本分步指南展示了如何创建、应用并将脱敏策略保存为 XML。
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: 了解如何使用 GroupDocs.Redaction .NET 对敏感数据进行脱敏。本分步指南展示了如何创建、应用并将脱敏策略保存为
  XML。
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: 使用 GroupDocs.Redaction .NET 对敏感数据进行脱敏
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: 使用 GroupDocs.Redaction .NET 对敏感数据进行脱敏
type: docs
url: /zh/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 对敏感数据进行脱敏

在合同、财务报表或患者记录中保护机密信息是现代应用程序的必不可少的要求。在本指南中，您将学习如何使用 GroupDocs.Redaction for .NET **对敏感数据进行脱敏**，从安装 SDK 到定义可在任何文档类型中使用的可重用 XML 策略。

## 快速答案
- **“create redaction policy” 是什么意思？** 它是定义规则（文本、正则表达式、图像等）的过程，告诉 GroupDocs.Redaction 如何隐藏或替换机密内容。  
- **我需要哪个库？** GroupDocs.Redaction for .NET，可通过 NuGet 获取。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要永久许可证。  
- **我可以重用该策略吗？** 可以——保存为 XML 后，您可以稍后加载并将其应用于任何文档。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什么是脱敏策略？

脱敏策略是一组规则，指定 *要* 删除或替换的内容以及 *替换后* 的显示方式。只需创建一次策略，即可对应用程序处理的每个文档应用一致的安全标准。

## 脱敏策略是如何工作的？

使用 `Redactor` 引擎加载文档，附加一个或多个脱敏规则，然后调用 `Apply`。引擎会扫描文档，遮蔽匹配的内容，并可选择输出新文件。相同的规则集合可以导出为 XML，允许您在无需重新编译代码的情况下重用策略。

## 为什么使用 GroupDocs.Redaction 创建脱敏策略？

GroupDocs.Redaction 提供了一整套功能，简化了脱敏策略的创建、管理和执行，确保在各种文档类型中实现一致的数据保护，同时提供高性能并易于集成到现有的 .NET 应用程序中，适用于团队和组织。

- **广泛的格式支持** – SDK 支持 30 多种文件类型，包括 PDF、DOCX、XLSX、PPTX 和图像格式，并且可以在不将整个文件加载到内存的情况下处理高达 2 GB 的文件。  
- **编程精确度** – 定义精确短语、正则表达式或自定义逻辑，仅针对需要隐藏的数据。  
- **可重用的 XML 策略** – 将规则导出一次，即可在团队、服务或微服务之间共享。  
- **性能优化的引擎** – 该库在典型服务器硬件上可在一秒钟内处理数百页的文档，适用于高吞吐量的流水线。

## 前置条件
- 与您的 .NET 运行时兼容的 GroupDocs.Redaction 库。  
- Visual Studio、VS Code 或任何支持 C# 的 IDE。  
- 对 C# 和 .NET 项目结构有基本了解。

## 为 .NET 设置 GroupDocs.Redaction

首先，将库添加到您的项目中。

**使用 .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**使用 Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

或者在 NuGet 包管理器 UI 中搜索 “GroupDocs.Redaction”，并从那里安装。

### 许可证获取
- 首先使用 **免费试用** 来探索功能。  
- 请求 **临时许可证** 进行扩展测试，然后购买完整许可证用于生产。

### 基本初始化
在源文件中添加命名空间：

`Redactor` 类是加载文档并应用脱敏规则的核心引擎。  
```csharp
using GroupDocs.Redaction;
```  

`Redactor` 类是 GroupDocs.Redaction 的核心引擎，用于加载文档并应用脱敏规则。

## 如何一步步创建脱敏策略

下面是一段完整的演练，演示如何以编程方式构建脱敏策略，配置其规则，将其应用于文档，最后将策略持久化为 XML 文件以供将来重用，确保在多个项目和文档类型中实现一致的脱敏。

### 步骤 1：准备文档目录
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*将 `"YOUR_DOCUMENT_DIRECTORY"` 替换为保存您想要保护的文档的文件夹。*

### 步骤 2：加载文档
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
`Redactor` 对象打开文件并管理其生命周期。

### 步骤 3：定义脱敏规则
ExactPhraseRedaction 定义了一条将特定短语替换的规则，而 `RegexRedaction` 使用正则表达式匹配模式。  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
这里我们创建了两条规则：
1. **ExactPhraseRedaction** – 将已知短语替换为 “[REDACTED]”。  
2. **RegexRedaction** – 查找 `YYYY‑MM‑DD` 格式的日期，并将其替换为 “[DATE REDACTED]”。

### 步骤 4：应用脱敏规则
```csharp
redactor.Apply(redactions);
```  
所有已定义的规则将在一次遍历中对打开的文档执行。

### 步骤 5：将策略保存为 XML 文件
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML 文件存储脱敏定义，允许您在不重新编写代码的情况下重用相同的策略。

## 实际应用

- **律师事务所** 可以在共享草稿之前脱敏案件编号和客户姓名。  
- **财务部门** 在报告中遮蔽账户号码或交易日期。  
- **医疗机构** 通过删除患者标识符来确保 HIPAA 合规。

## 性能技巧

- 同时打开 **一个文档** 以保持低内存使用。  
- 编写 **高效的正则表达式**；避免过于宽泛的模式导致处理时间增加。  
- 保持库 **最新**，以受益于性能改进和新脱敏类型。

## 常见问题及解决方案

| 问题 | 原因 | 解决方法 |
|------|------|----------|
| **准备目录时的 IO 异常** | 路径错误或缺少写入权限 | 确认文件夹存在且应用程序具有读/写权限。 |
| **正则表达式未匹配预期文本** | 模式过于严格或缺少转义字符 | 使用在线测试工具测试正则表达式；调整量词或转义特殊字符。 |
| **策略文件未创建** | `SavePolicy` 在应用脱敏之前调用或路径无效 | 确保输出目录可写，并在 `Apply` 之后调用 `SavePolicy`。 |

## 常见问答

**问：我可以加载已有的 XML 策略，而不是以编程方式构建吗？**  
答：可以——使用 `redactor.LoadPolicy("policy.xml")` 导入之前保存的策略。

**问：GroupDocs.Redaction 是否支持受密码保护的 PDF？**  
答：完全支持。将密码传递给 `Redactor` 构造函数：`new Redactor(sourceFile, "password")`。

**问：可以脱敏图像或元数据吗？**  
答：SDK 提供 `ImageRedaction` 和 `MetadataRedaction` 类来处理这些场景。

**问：如何处理大型文档（数百 MB）？**  
答：可以分块处理或使用流式 API 以降低内存占用；引擎可在不将整个文件加载到 RAM 的情况下处理高达 2 GB 的文件。

**问：商业使用需要什么许可模式？**  
答：生产部署需要付费许可证；开发和测试可以使用试用许可证。

## 结论

您现在拥有完整且可重用的 **脱敏策略**，可以使用 GroupDocs.Redaction for .NET 将其应用于任何文档。通过将策略导出为 XML，您简化了后续更新，并确保在整个组织中实现一致的数据保护。

### 后续步骤
- 尝试使用额外的脱敏类型，如 `ImageRedaction` 或 `MetadataRedaction`。  
- 将策略加载逻辑集成到文档管理工作流中，实现自动脱敏。  
- 探索 **GroupDocs.Redaction** API 参考文档，以进行高级定制。

---

**最后更新：** 2026-10-06  
**测试环境：** GroupDocs.Redaction 5.8 for .NET  
**作者：** GroupDocs  

**资源**  
- [文档](https://docs.groupdocs.com/redaction/net/)  
- [API 参考](https://reference.groupdocs.com/redaction/net)  
- [下载](https://releases.groupdocs.com/redaction/net/)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证申请](https://purchase.groupdocs.com/temporary-license/)

## 相关教程

- [使用 GroupDocs.Redaction .NET (C#) 脱敏敏感数据](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)  
- [使用 GroupDocs.Redaction .NET 实现文档脱敏：一步一步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)  
- [如何使用 GroupDocs.Redaction .NET 脱敏文档 – 完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)