---
date: '2026-08-14'
description: 使用 GroupDocs.Redaction 在 Java 文档中进行文本脱敏 – 高效地遮蔽个人信息并替换敏感文本。
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: 使用 GroupDocs.Redaction for Java 可永久遮蔽个人数据并在 PDF、DOCX 等文件中替换敏感字符串，确保符合
  GDPR 和 HIPAA 标准。
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: 如何使用 GroupDocs.Redaction for Java 对文本进行脱敏
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: 如何使用 GroupDocs.Redaction for Java 对文本进行脱敏
type: docs
url: /zh/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# 如何使用 GroupDocs.Redaction for Java 对文本进行脱敏

在本教程中，您将学习 **如何在基于 Java 的文档中脱敏文本**，使用 GroupDocs.Redaction。您将看到如何遮蔽个人信息、用安全占位符替换敏感字符串，以及以批量友好的方式处理多个文件。完成后，您将拥有一个可投入生产的解决方案，保护隐私，满足 GDPR/HIPAA 要求，并平滑集成到现有的 Java 应用程序中。

## 快速答案
- **使用的库是什么？** GroupDocs.Redaction for Java。  
- **我可以遮蔽个人信息吗？** 是的 – 使用 exact‑phrase redaction 并配合 replacement options。  
- **支持批量处理吗？** 当然，您可以使用同一个 Redactor 实例循环处理多个文件。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要商业许可证。  
- **需要哪个 Java 版本？** JDK 8 或更高。

## 什么是“文本脱敏”？

脱敏会永久删除或隐藏文档中的机密数据。使用 GroupDocs.Redaction，您可以定位特定字符串，将其替换为安全的占位符，并保存已清理的文件——无需手动编辑。

## 为什么使用 GroupDocs.Redaction for Java？

GroupDocs.Redaction for Java 支持 **50 多种输入和输出格式**（包括 PDF、DOCX、XLSX、PPTX、TXT、RTF），并且能够在不将整个文档加载到内存的情况下处理数百页的文件，在标准服务器硬件上实现高吞吐量的批量操作。

## 前置条件
- **Java Development Kit (JDK)：** 8 版或更高。  
- **IDE：** IntelliJ IDEA、Eclipse 或任何兼容 Java 的编辑器。  
- **Maven：** 用于依赖管理。  
- **基本的 Java 知识：** 熟悉类、方法和异常处理。

## 设置 GroupDocs.Redaction for Java
要开始，请将库添加到您的 Maven 项目中。

### Maven 设置
将仓库和依赖添加到您的 `pom.xml` 文件：

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### 直接下载
如果您更喜欢，可以从 [GroupDocs.Redaction for Java 发布](https://releases.groupdocs.com/redaction/java/) 获取最新的 JAR。

### 获取许可证
您可以先使用 **Free Trial** 开始评估，申请 **Temporary License** 进行更长时间的测试，或购买 **Commercial License** 用于生产环境。

## 如何使用 GroupDocs.Redaction 对文档进行文本脱敏

以下章节将逐步演示实现 **遮蔽个人信息** 和 **替换敏感文本** 所需的具体步骤。

### 步骤 1：初始化 Redactor

`Redactor` 是加载文档、应用脱敏规则并写入输出的核心类。  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### 步骤 2：应用 exact‑phrase 脱敏

`ExactPhraseRedaction` 用于搜索精确匹配的字符串，而 `ReplacementOptions` 定义匹配文本的替换方式。  

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **参数：**  
  - `"John Doe"` – 要脱敏的精确文本。  
  - `ReplacementOptions("[personal]")` – 用于替换原始内容的字符串，实际上 **遮蔽个人信息**。

### 步骤 3：保存脱敏后的文档

`Redactor.save` 将修改后的文档写入新文件或覆盖原文件，保持原始格式。  

```java
redactor.save();
```

### 步骤 4：清理资源

始终调用 `Redactor.close()` 以释放本机资源，防止内存泄漏。  

```java
finally {
    redactor.close();
}
```

## 如何使用自定义回调遮蔽个人信息

自定义回调可以让您对每个脱敏事件作出响应——这对于日志记录、条件替换或审计追踪非常有用。

### 创建回调类

`IRedactionCallback` 定义了在每次脱敏操作前后被调用的方法。  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### 实例化 Redactor 时使用回调

通过 `RedactorSettings` 传入您的回调实现，使引擎在处理过程中调用它。  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## 实际应用
- **法律合同：** 在共享草稿前自动隐藏客户姓名、社会保险号或机密条款。  
- **医疗记录：** 在将记录导出给研究合作方时 **遮蔽个人信息**，例如患者标识符。  
- **企业沟通：** 在对外分发前 **替换敏感文本**，如内部项目代码，确保不会意外泄露。

## 性能考虑因素
在处理大量或大型文件时，请记住以下提示：

- **批量处理：** 循环遍历文件集合以降低启动开销。  
- **内存管理：** 每处理完一个文件后释放 `Redactor`；避免同时在内存中保留多个文档。  
- **性能分析：** 使用 Java 分析工具（如 VisualVM）定位 I/O 或脱敏逻辑的瓶颈。

## 常见问题
**Q：我可以使用 GroupDocs.Redaction 对 PDF 文本进行脱敏吗？**  
A：是的，该库支持 PDF、DOCX、XLSX、PPTX 以及许多其他格式。

**Q：脱敏是可逆的吗？**  
A：不可以。脱敏会永久删除原始内容，请保留源文件的备份。

**Q：如何高效处理超大文档？**  
A：将文档分块处理，使用批量模式，并使用分析工具监控内存使用情况。

**Q：还支持哪些文本格式？**  
A：除了 DOCX 和 PDF，还可以脱敏 TXT、RTF、XLSX、PPTX 等格式。

**Q：我可以将 GroupDocs.Redaction 集成到现有工作流中吗？**  
A：当然可以。该 API 可在 Web 服务、后台任务或 CI/CD 流水线中调用。

## 资源
- **文档：** [GroupDocs Redaction Java 文档](https://docs.groupdocs.com/redaction/java/)  
- **API 参考：** [GroupDocs API 参考（Java）](https://reference.groupdocs.com/redaction/java)  
- **下载：** [GroupDocs.Redaction 下载](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 仓库：** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持论坛：** [GroupDocs 免费支持](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证申请：** [申请临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-08-14  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [Java 脱敏数据指南 – GroupDocs.Redaction](/redaction/java/getting-started/)
- [Java 脱敏数据 – 使用 GroupDocs.Redaction 脱敏个人信息](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [编辑受密码保护的 Java 文档 - 使用 GroupDocs.Redaction 脱敏文档](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)