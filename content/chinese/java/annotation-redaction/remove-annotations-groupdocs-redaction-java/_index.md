---
date: '2026-06-21'
description: 分步指南，介绍如何在 Java 中使用 GroupDocs.Redaction 删除注释，包括设置、代码和故障排除。
keywords:
- how to remove annotations
- GroupDocs Redaction Java
- annotation removal Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-21'
  description: Step‑by‑step guide on how to remove annotations in Java with GroupDocs.Redaction,
    including setup, code, and troubleshooting.
  headline: How to Remove Annotations Java Using GroupDocs.Redaction
  type: TechArticle
- description: Step‑by‑step guide on how to remove annotations in Java with GroupDocs.Redaction,
    including setup, code, and troubleshooting.
  name: How to Remove Annotations Java Using GroupDocs.Redaction
  steps:
  - name: Import the required classes.
    text: Import the required classes.
  - name: Instantiate `Redactor` with your source file.
    text: Instantiate `Redactor` with your source file.
  - name: Call `apply(new DeleteAnnotationRedaction())`.
    text: Call `apply(new DeleteAnnotationRedaction())`.
  - name: Set `SaveOptions` (add suffix, keep format).
    text: Set `SaveOptions` (add suffix, keep format).
  - name: Invoke `redactor.save(saveOptions)`.
    text: Invoke `redactor.save(saveOptions)`.
  - name: '**Legal Document Review:** Remove reviewer comments before final signatures.'
    text: '**Legal Document Review:** Remove reviewer comments before final signatures.'
  - name: '**Academic Publishing:** Clean manuscripts of peer‑review notes prior to
      journal submission.'
    text: '**Academic Publishing:** Clean manuscripts of peer‑review notes prior to
      journal submission.'
  - name: '**Internal Reports:** Deliver polished reports without draft annotations
      cluttering the view.'
    text: '**Internal Reports:** Deliver polished reports without draft annotations
      cluttering the view.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java API that lets you programmatically redact
      or delete sensitive content—including annotations—from a wide range of document
      formats.
    question: What is GroupDocs.Redaction?
  - answer: Yes, provided you have a valid commercial license. The temporary license
      is for evaluation only.
    question: Can I use this in a commercial project?
  - answer: Absolutely. It works with PDF, DOCX, PPTX, XLSX, and many more—over 50
      formats in total.
    question: Does the API support PDF, DOCX, and other formats?
  - answer: No hard limit; performance depends on document size and system resources.
      Typical 200‑page PDFs with thousands of annotations are processed in under two
      seconds.
    question: Is there any limit to the number of annotations I can delete?
  - answer: The API overwrites the file you save. Keep a backup of the original document
      before running the redaction.
    question: How can I revert changes if I delete annotations by mistake?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction 在 Java 中删除注释
type: docs
url: /zh/java/annotation-redaction/remove-annotations-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction 删除 Java 注释

当您需要 **remove annotations Java** 时，杂乱的评论和标记会使文档难以阅读和处理。无论是清理法律合同、学术草稿还是内部报告，GroupDocs.Redaction 的 Java API 都能以快速、可靠的方式一次性剥离所有注释——通常在两秒内处理完 200 页的 PDF。在本指南中，我们将从环境搭建到清除注释的完整代码逐步演示，帮助您将此功能集成到自己的 Java 应用中。

## 快速答案
- **“remove annotations java” 是什么意思？** 它指的是使用 Java 代码以编程方式删除文档中所有评论类型的对象。  
- **哪个库处理此功能？** GroupDocs.Redaction for Java。  
- **我需要许可证吗？** 临时许可证可用于评估；生产环境需要正式许可证。  
- **我可以保留原始文件格式吗？** 是的，API 默认以原始格式保存文档。  
- **操作需要多长时间？** 对于一般大小的文件通常在一秒以内；较大的 PDF 可能需要几秒。

## 什么是 “remove annotations java”？
**Removing annotations in Java means using the GroupDocs.Redaction SDK to locate every annotation object (comments, highlights, stamps, etc.) in a document and delete them automatically.** 这消除了手动打开每个文件并逐一清除注释的步骤。

## 为什么要删除注释？
**Removing annotations ensures legal compliance, publishing readiness, and better performance.** 例如，合同在不到一秒的时间内即可准备好签署，手稿在提交期刊前去除审稿人备注，且下游处理流水线对无注释文件的加载时间可降低约 30 %。

## 前提条件

- **GroupDocs.Redaction for Java** 版本 24.9 或更新（支持 50 多种输入和输出格式）。  
- **Maven**（如果您偏好依赖管理）或直接下载 JAR。  
- 一个 **JDK**（推荐 Java 8+）以及如 IntelliJ IDEA 或 Eclipse 的 IDE。  
- 基本的 Java 知识并熟悉文件 I/O。

## 设置 GroupDocs.Redaction for Java

### Maven 设置
将仓库和依赖添加到您的 `pom.xml` 中：

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
另外，您可以从 [GroupDocs.Redaction for Java 发布](https://releases.groupdocs.com/redaction/java/) 下载最新的 JAR。

### 获取许可证
要解锁全部功能，请从 [许可证页面](https://purchase.groupdocs.com/temporary-license/) 获取临时许可证。这样即可在不受评估限制的情况下进行测试。

### 基本初始化
下面是一个最小的启动类，用于打开文档。保持代码不变——这就是后面要使用的完整代码块。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Replace with the path to your document
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
        
        try {
            // Basic initialization and setup code here
        } finally {
            redactor.close();
        }
    }
}
```

## 如何在 Java 中删除注释？

`Redactor` 加载文档进行编辑。`DeleteAnnotationRedaction` 删除所有注释对象。`SaveOptions` 配置输出设置。使用 `Redactor` 实例加载源文件，应用 `DeleteAnnotationRedaction`，配置 `SaveOptions` 以保持原始格式，最后调用 `save`。此五步流程在一次操作中删除所有注释，同时保留原始文档的布局和元数据。

### 步骤 1 – 导入包
这些导入让您能够访问 Redactor、保存选项以及特定的脱敏类型。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;
```

### 步骤 2 – 初始化 Redactor
**The `Redactor` class is the core engine that loads and modifies documents in GroupDocs.Redaction.** 创建指向待清理文件的 `Redactor` 实例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

### 步骤 3 – 应用 DeleteAnnotationRedaction
**The `DeleteAnnotationRedaction` class represents a redaction operation that removes all annotation objects from the document.** 这行代码告诉 SDK 剥离所有注释。

```java
redactor.apply(new DeleteAnnotationRedaction());
```

### 步骤 4 – 配置保存选项
**The `SaveOptions` class lets you configure output settings such as file format, suffix, and compression.** 我们为输出文件名添加后缀，以免原文件被修改，并保持原始格式。

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);
saveOptions.setRasterizeToPDF(false);
```

### 步骤 5 – 保存修改后的文档
最后，将更改写回磁盘。

```java
redactor.save(saveOptions);
```

## 完整示例回顾
将各部分组合起来，工作流如下：

1. 导入所需的类。  
2. 使用源文件实例化 `Redactor`。  
3. 调用 `apply(new DeleteAnnotationRedaction())`。  
4. 设置 `SaveOptions`（添加后缀，保持格式）。  
5. 调用 `redactor.save(saveOptions)`。

## 故障排除技巧
- **文件路径错误：** 验证传递给 `Redactor` 的路径是绝对路径或相对于项目的正确相对路径。  
- **缺少依赖项：** 仔细检查你的 `pom.xml` 或 JAR 类路径；没有核心库 Redactor 将无法启动。  
- **许可证未应用：** 如果出现许可证异常，请确保临时许可证文件放在正确的目录并在代码中引用（此处未展示）。

## 实际应用

1. **法律文件审查：** 在最终签署前删除审阅者的评论。  
2. **学术出版：** 在提交期刊前清除手稿中的同行评审备注。  
3. **内部报告：** 提供没有草稿注释的精致报告。  

## 性能考虑因素

- **资源管理：** 始终调用 `redactor.close()`（如初始化示例所示）以释放本地资源。  
- **大文件：** 对于数百页的 PDF，考虑分块处理或增大 JVM 堆大小。  
- **保持更新：** 新版本带来性能改进——请保持 Maven 版本最新。  

## 常见陷阱及避免方法
| 陷阱 | 解决方案 |
|------|----------|
| 忘记调用 `redactor.close()` | 在 try‑finally 块中使用（如入门示例所示）。 |
| 在路径中使用错误的文件扩展名 | 确保路径与实际文件类型（DOCX、PDF 等）匹配。 |
| 未添加后缀导致覆盖原文件 | 设置 `saveOptions.setAddSuffix(true)` 以保留源文件。 |

## 常见问题

**Q: 什么是 GroupDocs.Redaction？**  
A: GroupDocs.Redaction 是一个 Java API，允许您以编程方式脱敏或删除敏感内容——包括注释——适用于多种文档格式。

**Q: 我可以在商业项目中使用吗？**  
A: 可以，前提是您拥有有效的商业许可证。临时许可证仅用于评估。

**Q: API 是否支持 PDF、DOCX 等格式？**  
A: 当然。它支持 PDF、DOCX、PPTX、XLSX 等超过 50 种格式。

**Q: 删除注释的数量有没有限制？**  
A: 没有硬性限制；性能取决于文档大小和系统资源。典型的 200 页、含数千条注释的 PDF 可在两秒内处理完毕。

**Q: 如果误删注释，如何恢复？**  
A: API 会覆盖您保存的文件。请在运行脱敏前备份原始文档。

## 资源

- **文档：** [GroupDocs Redaction Java 文档](https://docs.groupdocs.com/redaction/java/)  
- **API 参考：** [API 参考](https://reference.groupdocs.com/redaction/java)  
- **下载：** [最新发布](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 仓库：** [GroupDocs.Redaction for Java](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持论坛：** [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证：** [获取临时许可证](https://purchase.groupdocs.com/temporary-license/)  

通过本指南，您已经掌握了使用 GroupDocs.Redaction **remove annotations Java** 的可靠方法。将代码片段集成到批处理流水线中，随时享受更清洁、无注释的文档。

---

**最后更新：** 2026-06-21  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [如何使用 GroupDocs.Redaction 对 Java 进行脱敏 - 开发者综合指南](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)  
- [如何使用文件路径的 GroupDocs Redaction Java 许可证对敏感数据进行脱敏 – 步骤指南](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)  
- [Java 文本脱敏教程：使用 GroupDocs.Redaction 的指南](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)