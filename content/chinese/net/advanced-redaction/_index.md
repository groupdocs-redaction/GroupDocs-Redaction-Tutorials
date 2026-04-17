---
date: 2026-03-06
description: 了解如何使用 GroupDocs.Redaction for .NET 创建编辑策略、编辑数据并擦除文档元数据。
title: 使用 GroupDocs.Redaction .NET 创建编辑策略
type: docs
url: /zh/net/advanced-redaction/
weight: 9
---

# 使用 GroupDocs.Redaction .NET 创建遮蔽策略

在本完整指南中，您将了解 **如何创建 redaction policy** 对象，帮助您自动删除 PDF、Word 文件、图像等中的敏感内容。无论是需要遵循 GDPR、HIPAA，还是内部安全标准，掌握 GroupDocs.Redaction for .NET 中的遮蔽策略都能让您细粒度地控制哪些内容被隐藏、如何隐藏，甚至如何擦除元数据。我们将逐一讲解 why、what 和 step‑by‑step 过程，让您立即开始构建可靠的文档隐私解决方案。

## 快速回答
- **什么是 redaction policy？** 一组可复用的规则，定义应从文档中删除的文本、图像或元数据。  
- **为什么要创建 redaction policy？** 在多个文件之间应用一致、可重复的数据保护规则，而无需每次都重写代码。  
- **我可以使用 AI 来定位敏感数据吗？** 可以——GroupDocs.Redaction 支持 **ai document redaction** 集成，自动查找个人标识信息。  
- **如何擦除文档元数据？** 在策略中加入 “erase document metadata” 规则，即可剥离作者、创建日期和隐藏属性。  
- **是否需要许可证？** 生产环境必须使用有效的 GroupDocs.Redaction 许可证；测试时可使用临时许可证。

## 什么是 Redaction Policy？
Redaction policy 是一组遮蔽项的集合——例如精确短语、正则表达式模式或元数据字段——引擎会自动应用这些规则。只需定义一次策略，即可在多个文档中复用，确保数据隐私处理的一致性。

## 为什么使用 GroupDocs.Redaction 来创建 Redaction Policies？
- **集中控制：** 一个策略，多个文档。  
- **可扩展安全性：** 处理大批量文件，无需人工干预。  
- **AI 辅助检测：** 利用 **ai document redaction** 自动标记个人可识别信息（PII）。  
- **元数据擦除：** 内置 **erase document metadata** 支持，保护可能泄露的隐藏信息。  
- **可扩展：** 结合自定义处理器、回调和日志记录，构建复杂工作流。

## 如何在 GroupDocs.Redaction .NET 中创建 Redaction Policy
下面是简明、对话式的步骤说明。原教程未包含代码块，我们保持代码块数量不变。

1. **添加 NuGet 包**  
   通过 NuGet 包管理器或 CLI（`dotnet add package GroupDocs.Redaction`）安装最新的 `GroupDocs.Redaction` 包。  

2. **实例化 RedactionEngine**  
   创建指向待保护文档的 `RedactionEngine` 实例。  

3. **定义遮蔽项**  
   - 使用 `ExactPhraseRedaction` 处理固定字符串（例如 “Social Security Number”）。  
   - 使用 `RegexRedaction` 处理模式（例如信用卡号）。  
   - 添加 `MetadataRedaction` 项以 **erase document metadata**，如作者或创建日期。  

4. **将项组合成策略**  
   将遮蔽项聚合到 `RedactionPolicy` 对象中。该策略可保存到磁盘（`policy.Save("MyPolicy.xml")`），以后可加载复用。  

5. **应用策略**  
   调用 `engine.ApplyPolicy(policy)` 处理文档。引擎会遮蔽所有匹配内容并剥离指定的元数据。  

6. **保存已遮蔽的文档**  
   使用 `engine.Save("RedactedFile.pdf")` 将清理后的文件写入存储。

### 如何使用策略遮蔽数据
当您需要在特定场景下 **how to redact data**（例如在一批 HR PDF 中遮蔽员工 ID）时，只需加载已保存的策略并对每个文件应用。这样即可消除重复编码，确保每份文档遵循相同的安全规则。

### 集成 AI 辅助遮蔽
如果项目需要智能检测 PII，可将 AI 服务（如 Azure Cognitive Services、AWS Comprehend）接入回调机制。回调可在引擎运行前将 AI 识别的位置反馈到策略中，从而实现强大的 **ai document redaction** 能力，而无需更改核心工作流。

## 常见使用场景
- **合规报告：** 在共享报告前自动删除患者姓名、病历号或金融标识符。  
- **法律发现：** 从大型文档集合中剥离机密条款和客户标识符。  
- **文档发布：** 在公开发布前清除草稿中的作者备注、评论和隐藏元数据。  

## 提示与最佳实践
- **专业提示：** 将策略存放在受版本控制的仓库中，以便随时审计变更。  
- **警告：** 首先在文档副本上测试策略；遮蔽是不可逆的。  
- **性能提示：** 使用异步调用批量处理文件，提高大数据集的吞吐量。  

## 可用教程

### [How to Create a Redaction Policy Using GroupDocs.Redaction .NET&#58; A Step-by-Step Guide](./groupdocs-redaction-net-create-save-policy/)
了解如何使用 GroupDocs.Redaction for .NET 创建并保存自定义遮蔽策略。通过高效遮蔽敏感信息来保护文档。

### [Implement Custom Logging in GroupDocs.Redaction for .NET&#58; A Comprehensive Guide](./custom-logging-groupdocs-redaction-net/)
了解如何在 GroupDocs.Redaction for .NET 中实现自定义日志记录，以增强文档遮蔽工作流。发现实用步骤和关键特性。

### [Implementing IRedactionCallback in GroupDocs.Redaction .NET for Secure Document Redaction with C#](./groupdocs-redaction-net-implement-iredactioncallback-csharp/)
了解如何使用 GroupDocs.Redaction .NET 实现 IRedactionCallback 接口，实现安全高效的文档遮蔽工作流。掌握最佳实践和实际应用。

### [Master .NET Redaction with GroupDocs&#58; Apply Policies to Files Efficiently](./net-redaction-groupdocs-apply-policy-files/)
了解如何使用 GroupDocs.Redaction 在 .NET 中自动化遮蔽，确保文件的数据隐私和合规性。

### [Master Custom Redaction in .NET Using GroupDocs&#58; A Comprehensive Guide](./master-custom-redaction-dotnet-groupdocs/)
了解如何使用 GroupDocs.Redaction for .NET 保护文档中的敏感信息。轻松实现自定义遮蔽，确保文档隐私。

### [Master Document Redaction in .NET Using GroupDocs.Redaction&#58; A Complete Guide](./master-document-redaction-groupdocs-redaction-net/)
了解如何使用 GroupDocs.Redaction for .NET 保护敏感文档。本指南涵盖设置、遮蔽技术和最佳实践。

### [Master Document Redaction in .NET using GroupDocs.Redaction&#58; A Step-by-Step Guide](./mastering-document-redaction-dotnet-groupdocs-redaction/)
了解如何在 .NET 中使用 GroupDocs.Redaction 实现安全文档遮蔽。本指南涵盖自定义格式处理器和精确短语遮蔽，适合开发者使用。

### [Mastering Document Security with GroupDocs.Redaction .NET&#58; A Comprehensive Guide to Phrase and Metadata Redaction](./groupdocs-redaction-net-document-security-guide/)
了解如何使用 GroupDocs.Redaction for .NET 保护敏感文档。本指南涵盖精确短语、正则表达式遮蔽、注释删除和元数据擦除。

## 其他资源

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## 常见问题

**Q: 我可以将多个 redaction policy 合并使用吗？**  
A: 可以，您可以通过编程方式合并策略，或在应用到文档前顺序加载多个策略文件。

**Q: GroupDocs.Redaction 支持遮蔽扫描图像吗？**  
A: 支持，只要配合 OCR 使用；OCR 引擎提取文本后即可使用相同的策略规则进行遮蔽。

**Q: “erase document metadata” 与普通遮蔽有何不同？**  
A: 元数据遮蔽会删除隐藏属性（作者、时间戳、自定义字段），这些信息虽不在文档内容中显示，却可能泄露敏感信息。

**Q: AI 辅助遮蔽的准确性足以满足合规要求吗？**  
A: AI 模型提供强有力的第一轮筛选；对于高风险合规场景，仍建议人工复核标记项。

**Q: 支持哪些 .NET 版本？**  
A: GroupDocs.Redaction .NET 支持 .NET Framework 4.6.1+、.NET Core 3.1+ 以及 .NET 5/6+。

---

**最后更新：** 2026-03-06  
**测试环境：** GroupDocs.Redaction 2.0 for .NET  
**作者：** GroupDocs