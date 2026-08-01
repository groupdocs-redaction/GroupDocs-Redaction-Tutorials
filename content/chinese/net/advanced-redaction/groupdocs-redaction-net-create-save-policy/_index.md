---
date: '2026-03-30'
description: 学习如何在 .NET 中使用 GroupDocs.Redaction 创建编辑策略。本教程展示了如何构建、应用并将编辑策略保存为 XML
  文件。
keywords:
- GroupDocs.Redaction .NET
- create redaction policy
- save XML policy
title: 使用 GroupDocs.Redaction .NET 创建遮蔽策略 – 步骤指南
type: docs
url: /zh/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 创建编辑策略

在现代应用程序中，保护文档内部的机密数据是必不可少的安全措施。无论您处理的是合同、财务报表还是患者记录，通常都需要**create redaction policy**，自动遮蔽或删除敏感信息。本指南将带您完整了解整个过程——安装库、定义编辑、应用编辑，最后将策略保存为 XML 文件，以便在项目之间重复使用。

## 快速答案
- **“create redaction policy” 是什么意思？** 这是定义规则（文本、正则表达式、图像等）的过程，用来告诉 GroupDocs.Redaction 如何隐藏或替换机密内容。  
- **我需要哪个库？** GroupDocs.Redaction for .NET（可通过 NuGet 获取）。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要正式许可证。  
- **我可以重复使用该策略吗？** 可以——保存为 XML 后，可在以后加载并应用到任何文档。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什么是编辑策略？

编辑策略是一组规则，指定*要删除或替换的内容*以及*替换的方式*。只需创建一次策略，即可对应用程序处理的每个文档统一应用安全标准。

## 为什么使用 GroupDocs.Redaction 来创建编辑策略？

- **全文档格式支持** – Word、PDF、Excel、PowerPoint 等众多格式。  
- **可编程控制** – 定义精确短语、正则表达式，甚至自定义逻辑。  
- **可复用的 XML 策略** – 一次导出规则，即可在团队或服务之间共享。  
- **性能优化引擎** – 高效处理大文件，随工作负载水平扩展。

## 前置条件

- **GroupDocs.Redaction** 库（兼容您的 .NET 运行时）。  
- Visual Studio、VS Code 或任何支持 C# 的 IDE。  
- 对 C# 和 .NET 项目结构有基本了解。

## 设置 GroupDocs.Redaction for .NET

首先，将库添加到项目中。

**使用 .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**使用 Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

或在 NuGet 包管理器 UI 中搜索 “GroupDocs.Redaction” 并进行安装。

### 许可证获取
- 先使用**免费试用**探索功能。  
- 申请**临时许可证**进行扩展测试，然后购买正式许可证用于生产。

### 基本初始化
在源文件中添加命名空间：

```csharp
using GroupDocs.Redaction;
```

## 如何使用 GroupDocs.Redaction .NET 创建编辑策略

下面提供逐步演示，展示如何构建并持久化编辑策略。

### 步骤 1：准备文档目录
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```
*将 `"YOUR_DOCUMENT_DIRECTORY"` 替换为存放待保护文档的文件夹。*

### 步骤 2：加载文档
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```
`Redactor` 对象打开文件并管理其生命周期。

### 步骤 3：定义编辑
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```
这里我们创建两条规则：
1. **ExactPhraseRedaction** – 将已知短语替换为 “[REDACTED]”。  
2. **RegexRedaction** – 查找 `YYYY‑MM‑DD` 格式的日期并替换为 “[DATE REDACTED]”。

### 步骤 4：应用编辑
```csharp
redactor.Apply(redactions);
```
所有已定义的规则一次性对打开的文档执行。

### 步骤 5：将策略保存为 XML 文件
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```
XML 文件存储编辑定义，便于在无需重新编写代码的情况下重复使用同一策略。

## 实际应用场景

- **律师事务所** 在共享草稿前删除案号和客户姓名。  
- **财务部门** 在报告中掩码账号或交易日期。  
- **医疗机构** 通过删除患者标识符确保 HIPAA 合规。

## 性能提示

- **一次只打开一个文档**，以降低内存占用。  
- 编写**高效的正则表达式**；避免使用过于宽泛的模式导致处理时间增加。  
- 保持库**最新**，以获得性能改进和新编辑类型。

## 常见问题及解决方案

| 问题 | 原因 | 解决方法 |
|-------|----------------|------------|
| **准备目录时出现 IO 异常** | 路径错误或缺少写入权限 | 确认文件夹存在且应用具有读写权限。 |
| **正则表达式未匹配预期文本** | 模式过于严格或缺少转义字符 | 使用在线测试工具验证正则表达式；调整量词或转义特殊字符。 |
| **策略文件未创建** | 在应用编辑之前或使用了无效路径调用 `SavePolicy` | 确保输出目录可写，并在 `Apply` 之后调用 `SavePolicy`。 |

## 常见问答

**Q: 我可以加载已有的 XML 策略，而不是编程构建吗？**  
A: 可以——使用 `redactor.LoadPolicy("policy.xml")` 导入之前保存的策略。

**Q: GroupDocs.Redaction 是否支持受密码保护的 PDF？**  
A: 完全支持。将密码传递给 `Redactor` 构造函数：`new Redactor(sourceFile, "password")`。

**Q: 能否编辑图像或元数据？**  
A: 库提供 `ImageRedaction` 和 `MetadataRedaction` 类来处理这些场景。

**Q: 如何处理大型文档（数百 MB）？**  
A: 可分块处理或使用流式 API 减少内存占用；如出现 OutOfMemory 错误，也可考虑增大 JVM 堆（若使用 Java 环境）。

**Q: 商业使用需要哪种授权模式？**  
A: 生产部署必须使用付费许可证；开发和测试阶段使用试用许可证即可。

## 结论

现在您已经拥有完整且可复用的**编辑策略**，可通过 GroupDocs.Redaction for .NET 应用于任何文档。将策略导出为 XML，可简化后续更新，并确保组织内部数据保护的一致性。

### 后续步骤
- 试验其他编辑类型，如 `ImageRedaction` 或 `MetadataRedaction`。  
- 将策略加载逻辑集成到文档管理工作流，实现自动化编辑。  
- 浏览 **GroupDocs.Redaction** API 参考文档，进行高级定制。

---

**最后更新：** 2026-03-30  
**测试环境：** GroupDocs.Redaction 5.8 for .NET  
**作者：** GroupDocs  

**资源**  
- [文档](https://docs.groupdocs.com/redaction/net/)  
- [API 参考](https://reference.groupdocs.com/redaction/net)  
- [下载](https://releases.groupdocs.com/redaction/net/)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证申请](https://purchase.groupdocs.com/temporary-license/)