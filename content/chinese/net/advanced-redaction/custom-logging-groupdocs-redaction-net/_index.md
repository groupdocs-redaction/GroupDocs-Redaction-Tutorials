---
date: '2026-03-28'
description: 了解如何在 GroupDocs.Redaction for .NET 中实现自定义 C# 日志记录器，以实现详细的自定义日志记录并更轻松地进行合规报告。
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: 在 GroupDocs.Redaction for .NET 中实现自定义日志记录器（C#）
type: docs
url: /zh/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# 在 GroupDocs.Redaction for .NET 中实现自定义日志记录器 C#

管理文档脱敏效率至关重要，尤其是在处理敏感信息时。在本指南中，您将学习 **如何在 GroupDocs.Redaction for .NET 中实现自定义日志记录器 C#**，从而全面控制日志记录、错误处理和审计跟踪。

## 快速答案
- **自定义日志记录器 C# 的作用是什么？** 它在脱敏过程中捕获错误、警告和信息性消息。  
- **哪个库提供 ILogger 接口？** GroupDocs.Redaction for .NET。  
- **我可以在不进行光栅化的情况下保存脱敏文档吗？** 可以——使用 `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`。  
- **生产环境使用是否需要许可证？** 生产环境需要完整许可证；可使用试用版进行评估。  
- **此方法是否兼容 .NET Core / .NET 6+？** 完全兼容——相同的 API 在 .NET Framework 和 .NET Core/5/6 上均可使用。

## 什么是自定义日志记录器 C#？
**自定义日志记录器 C#** 是一个实现 GroupDocs.Redaction 提供的 `ILogger` 接口的类。它允许您将日志消息路由到任意位置——控制台、文件、数据库或外部监控系统——并让您清晰地了解脱敏工作流。

## 为什么在 GroupDocs.Redaction 中使用自定义日志记录 .NET？
- **合规与审计：** 详细日志满足监管要求。  
- **错误可见性：** `LogError` 和 `LogWarning` 为您提供即时的错误反馈。  
- **集成灵活性：** 将日志转发到现有的 .NET 日志框架（Serilog、NLog 等）。

## 先决条件
- **已安装 GroupDocs.Redaction for .NET**（请参见下文的安装步骤）。  
- 具备 .NET 开发环境（Visual Studio、VS Code 或 CLI）。  
- 基本的 C# 知识并熟悉文件流。

## 安装

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 包管理器 UI**  
搜索 **"GroupDocs.Redaction"** 并安装最新版本。

## 许可证获取
- **免费试用：** 使用临时许可证测试 API。  
- **临时许可证：** 在有限期间内获取全部功能。  
- **购买：** 获得用于生产部署的永久许可证。

## 分步指南

### 步骤 1：定义自定义日志记录器类（记录警告 C#）

创建一个实现 `ILogger` 的类。该类将捕获错误、警告和信息性消息。

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

**说明：** `HasErrors` 标志帮助您决定是否继续处理。三个方法对应大多数脱敏场景中需要的三个日志级别。

### 步骤 2：准备文件路径并打开源文档

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**为何重要：** 使用实用方法保持代码整洁，并确保在尝试 **保存脱敏文档** 之前输出文件夹已存在。

### 步骤 3：在使用自定义日志记录器的同时应用脱敏

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

**说明：**  
1. 使用 `RedactorSettings(logger)` 实例化 `Redactor`，将您的 `CustomLogger` 关联进去。  
2. 在应用脱敏后，代码检查 `logger.HasErrors`。如果没有错误发生，则保存文档——演示了在不进行光栅化的情况下 **保存脱敏文档** 的逻辑。

## 常见陷阱与故障排除

- **日志输出缺失：** 确认每个 `Log*` 方法已正确重写。  
- **文件访问异常：** 确保应用程序对源路径和输出路径都有读写权限。  
- **日志记录器未连接：** `RedactorSettings(logger)` 参数至关重要，省略它会导致自定义日志失效。

## 实际应用

1. **合规报告：** 将日志条目导出为 CSV 或数据库，以用于审计追踪。  
2. **错误追踪：** 通过扫描 `LogError` 输出快速定位有问题的文件。  
3. **工作流自动化：** 当调用 `LogWarning` 时触发下游流程（例如通知合规官）。

## 性能考虑

- **及时释放流** 以释放内存，尤其在处理大批量时。  
- **监控 CPU 与内存** 在批量脱敏期间；考虑在并行处理文档时谨慎同步日志记录器。  
- **保持更新：** 新版本的 GroupDocs.Redaction 通常包含性能优化和额外的日志钩子。

## 结论

通过实现 **自定义日志记录器 C#**，您可以细致了解脱敏流水线的每一步，从而更容易满足合规标准并调试问题。此方法可无缝配合 GroupDocs.Redaction for .NET 使用，并可扩展以集成您已有的任何 .NET 日志框架。

---

## 常见问题

**问：使用 GroupDocs.Redaction 的自定义日志记录的目的是什么？**  
**答：** 自定义日志记录有助于跟踪和管理脱敏，以满足合规、错误追踪和工作流优化的需求。

**问：如何使用自定义日志记录器处理错误？**  
**答：** 在您的 `CustomLogger` 类中实现 `LogError`；`HasErrors` 标志可在需要时中止处理。

**问：自定义日志记录可以与其他系统集成吗？**  
**答：** 可以，通过扩展日志记录器方法将日志消息转发到 CRM、ERP 或集中监控工具。

**问：实现自定义日志记录时常见的陷阱有哪些？**  
**答：** 方法实现错误、缺少 `RedactorSettings(logger)`、文件权限问题是最常见的。

**问：自定义日志记录如何改进文档脱敏工作流？**  
**答：** 详细日志提供实时可视性，简化故障排除，并满足审计要求。

## 资源

- **文档：** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 参考：** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **下载：** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**最后更新：** 2026-03-28  
**测试环境：** GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs