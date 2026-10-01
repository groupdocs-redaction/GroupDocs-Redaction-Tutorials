---
date: '2026-10-01'
description: 了解如何在 GroupDocs.Redaction for .NET 中实现 custom logger c#，从而实现 detailed
  custom logging .NET 并简化 compliance reporting。
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: 在 GroupDocs.Redaction for .NET 中实现 custom logger c#，以捕获 detailed logs，保存未进行
  rasterization 的已编辑文档，并满足 compliance requirements。
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: 在 GroupDocs.Redaction for .NET 中实现 custom logger c#
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: 在 GroupDocs.Redaction for .NET 中实现 custom logger c#
type: docs
url: /zh/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# 实现自定义日志记录器 C# 于 GroupDocs.Redaction for .NET

有效管理文档脱敏至关重要，尤其是在处理敏感信息时。在本指南中，您将学习 **如何实现自定义日志记录器 C#** 与 GroupDocs.Redaction for .NET，全面掌控日志记录、错误处理和审计追踪。教程结束时，您将能够捕获警告、错误和信息性消息，将日志记录器集成到现有的 .NET 日志框架，并在不进行光栅化的情况下保存脱敏文档。

## 快速答案
- **自定义日志记录器 C# 的作用是什么？** 它在脱敏过程中捕获错误、警告和信息性消息，为您提供可搜索的审计追踪。  
- **哪个库提供 ILogger 接口？** GroupDocs.Redaction for .NET 提供 `ILogger` 接口。  
- **我可以在不进行光栅化的情况下保存脱敏文档吗？** 可以——调用 `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`。  
- **生产环境需要许可证吗？** 生产环境需要完整许可证；可使用试用许可证进行评估。  
- **此方法兼容 .NET Core / .NET 6+ 吗？** 完全兼容——相同的 API 在 .NET Framework、.NET Core、.NET 5 和 .NET 6 上均可使用。

## 什么是自定义日志记录器 C#？

**自定义日志记录器 C#** 是一个实现 GroupDocs.Redaction 提供的 `ILogger` 接口的类。它允许您将日志消息路由到任意位置——控制台、文件、数据库或外部监控系统——并提供对整体脱敏工作流的清晰视图。

## 为什么在 GroupDocs.Redaction 中使用自定义日志记录 .NET？

为您的脱敏过程加载详细且可搜索的日志，以满足监管审计并加快故障排除。GroupDocs.Redaction 支持 **70 多种输入和输出格式**，并且能够在不将整个文件加载到内存的情况下处理最多 500 页的文档，因此精心设计的日志记录器几乎不增加开销，却提供了极其宝贵的可视性。

## 先决条件
- 已安装 GroupDocs.Redaction for .NET（请参阅下面的 **安装** 部分）。  
- .NET 开发环境（Visual Studio、VS Code 或 .NET CLI）。  
- 基础的 C# 知识以及对文件流的了解。  

## 安装

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜索 **"GroupDocs.Redaction"** 并安装最新版本。

## 许可证获取
- **免费试用：** 使用临时许可证测试 API。  
- **临时许可证：** 在有限时间内获取全部功能。  
- **购买：** 获得用于生产部署的永久许可证。

## 分步指南

### 如何在 .NET Core 中实现自定义日志记录器？

将 `CustomLogger` 类加载到您的 .NET Core 项目中，并将其连接到 `RedactorSettings`。该日志记录器在 .NET Framework、.NET 5 和 .NET 6 上的工作方式相同，您可以在所有平台之间共享相同的代码。

### 步骤 1：定义自定义日志记录器类（记录警告 C#）

`CustomLogger` 类实现了 `ILogger`。  
CustomLogger 是一个用户自定义的类，实现 `ILogger` 接口以捕获脱敏事件。  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**定义锚点：** `CustomLogger` 是 `ILogger` 接口的用户自定义实现，用于记录脱敏事件。  
**说明：** `HasErrors` 标志帮助您决定是否继续处理。三个方法对应您在大多数脱敏场景中需要的三种日志级别。

### 步骤 2：准备文件路径并打开源文档

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**定义锚点：** `Redactor` 是 GroupDocs.Redaction 中用于对 PDF 文档执行脱敏操作的主要类。  
**重要性说明：** 使用实用方法可保持代码整洁，并确保在尝试 **保存脱敏文档** 之前输出文件夹已存在。

### 步骤 3：在使用自定义日志记录器时应用脱敏

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**直接答案：** 脱敏工作流首先使用 `RedactorSettings(logger)` 创建 `Redactor` 实例，然后应用脱敏对象，检查 `logger.HasErrors`，最后调用 `redactor.Save` 并禁用光栅化。此模式确保每一步都有日志记录，并且仅在没有错误时才保存干净的文档。  
**说明：**  
1. 使用 `RedactorSettings(logger)` 实例化 `Redactor`，将您的 `CustomLogger` 关联进来。  
2. 在应用脱敏后，代码检查 `logger.HasErrors`。如果没有错误，则保存文档——演示了在不进行光栅化的情况下 **保存脱敏文档** 的逻辑。

## 常见陷阱与故障排除
- **日志输出缺失：** 确认每个 `Log*` 方法已正确重写。  
- **文件访问异常：** 确保应用程序对源路径和输出路径都有读写权限。  
- **日志记录器未连接：** `RedactorSettings(logger)` 参数至关重要，省略它会导致自定义日志记录失效。

## 实际应用
1. **合规报告：** 将日志条目导出为 CSV 或存入数据库，以便审计追踪。  
2. **错误追踪：** 通过扫描 `LogError` 输出快速定位有问题的文件。  
3. **工作流自动化：** 当调用 `LogWarning` 时触发下游流程（例如通知合规官）。

## 性能考虑
- **及时释放流** 以释放内存，尤其在处理大批量时。  
- **监控 CPU 与内存** 在批量脱敏期间；考虑在确保日志记录器同步的前提下并行处理文档。  
- **保持更新：** 新版本的 GroupDocs.Redaction 通常包含性能优化和额外的日志钩子。

## 结论

通过实现 **自定义日志记录器 C#**，您可以对脱敏流水线的每一步获得细粒度的洞察，从而更轻松地满足合规标准并调试问题。此方法与 GroupDocs.Redaction for .NET 无缝配合，并可扩展以集成您已有的任何 .NET 日志框架。

---

## 常见问题

**Q: 使用 GroupDocs.Redaction 的自定义日志记录的目的是什么？**  
A: 自定义日志记录捕获详细的脱敏事件，满足审计要求，并通过实时展示错误和警告简化故障排除。

**Q: 如何使用自定义日志记录器处理错误？**  
A: 在您的 `CustomLogger` 类中实现 `LogError`；`HasErrors` 标志可在检测到关键问题时中止处理。

**Q: 自定义日志记录可以集成到其他系统吗？**  
A: 可以——通过扩展日志记录器方法，您可以将日志消息转发到 CRM、ERP 或集中监控工具。

**Q: 实现自定义日志记录时常见的陷阱有哪些？**  
A: 常见问题包括缺少方法重写、忘记传递 `RedactorSettings(logger)`，以及文件权限不足。

**Q: 自定义日志记录如何改进文档脱敏工作流？**  
A: 详细的日志提供实时可视性，简化调试，并生成 GDPR、HIPAA 等法规要求的审计追踪。

## 资源

- **文档：** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 参考：** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **下载：** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Last updated:** 2026-10-01  
**Tested with:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## 相关教程

- [如何使用 GroupDocs.Redaction for .NET 加载文档](/redaction/net/document-loading/)  
- [如何使用 GroupDocs.Redaction .NET 导出脱敏文档](/redaction/net/document-saving/)  
- [使用 GroupDocs.Redaction .NET 实现文档脱敏：分步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)