---
date: '2026-02-18'
description: 学习如何在 Java 中使用 GroupDocs.Redaction、正则过滤删除 PDF 注释，并使用文件名后缀保存已编辑的文档。
keywords:
- annotation removal java
- groupdocs redaction setup
- regex annotation cleanup
title: 使用 GroupDocs.Redaction 在 Java 中删除 PDF 注释
type: docs
url: /zh/java/annotation-redaction/master-annotation-removal-java-groupdocs-redaction/
weight: 1
---

# 在 Java 中使用 GroupDocs.Redaction 删除 PDF 注释

如果您需要快速且可靠地**删除 PDF 注释**——无论是评论、突出显示还是便利贴——GroupDocs.Redaction for Java 为您提供了一个干净的编程解决方案。在本教程中，我们将从 Maven 设置讲解到基于正则表达式的过滤器，仅删除您指定的注释，并展示如何**保存已编辑的文档**并添加文件名后缀，以保持原始文件不受影响。

## Quick Answers
- **什么库负责注释删除？** GroupDocs.Redaction for Java.  
- **哪个关键字触发删除？** 您定义的正则表达式模式（例如 `(?im:(use|show|describe))`）。  
- **我需要许可证吗？** 试用版可用于评估；生产环境需要商业许可证。  
- **我可以用新名称保存清理后的文件吗？** 可以——使用 `SaveOptions.setAddSuffix(true)`。  
- **Maven 是唯一的添加库的方式吗？** 不是，您也可以直接下载 JAR。

## 什么是删除 PDF 注释？

删除 PDF 注释是指通过编程方式定位并删除文档中的标记对象（评论、突出显示、便利贴）。使用 GroupDocs.Redaction，您可以根据文本内容定位这些对象，非常适用于**法律文档编辑**、数据匿名化项目或任何需要干净、可共享文件的工作流。

## 为什么使用 GroupDocs.Redaction 删除 PDF 注释？

- **精准** – 正则表达式让您精确指定要擦除的注释。  
- **速度** – 在批处理模式下处理**多个文档**，无需手动打开每个文件。  
- **合规** – 确保敏感评论永不离开贵组织。  
- **跨格式支持** – 支持 PDF、DOCX、XLSX 等多种格式，您可以在同一平台处理所有办公文件。

## Prerequisites
- Java JDK 1.8 或更高版本。  
- 如 IntelliJ IDEA 或 Eclipse 的 IDE。  
- 对正则表达式有基本了解。  

## Maven 依赖 GroupDocs

在您的 `pom.xml` 中添加 GroupDocs 仓库和 Redaction 构件：

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

### Direct Download (alternative)

如果您不想使用 Maven，可从官方页面获取最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### License Acquisition Steps
1. **免费试用** – 下载试用版以体验核心功能。  
2. **临时许可证** – 申请临时密钥以进行完整功能测试。  
3. **购买** – 获取商业许可证用于生产环境。

## Basic Initialization and Setup

以下代码片段展示了如何创建 `Redactor` 实例并配置基本的保存选项：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        // Load the document using Redactor
        final Redactor redactor = new Redactor("path/to/your/document");
        
        try {
            // Perform your redaction operations here
            
            // Save options can be customized as needed
            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);  // Example option: Add suffix to filename
            
            // Save the modified document
            redactor.save(saveOptions, "path/to/output/document");
        } finally {
            redactor.close();  // Always close resources to prevent memory leaks
        }
    }
}
```

## Step‑by‑Step Guide to Remove PDF Annotations

### Step 1: Load Your Document

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/ANNOTATED_XLSX");
```

### Step 2: Apply Regex‑Based Annotation Removal

```java
redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
```

- **说明** – 模式 `(?im:(use|show|describe))` 为不区分大小写 (`i`) 且多行匹配 (`m`)。它匹配任何包含 *use*、*show* 或 *describe* 的注释。

### Step 3: Configure Save Options (add filename suffix)

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Append a suffix to the output filename
saveOptions.setRasterizeToPDF(false);  // Do not convert to PDF format
```

### Step 4: Save and Release Resources (save redacted document)

```java
redactor.save(saveOptions, "YOUR_OUTPUT_DIRECTORY/RedactedDocument");
redactor.close();  // Always close the Redactor instance
```

**故障排除提示**  
- 确认您的正则表达式确实匹配了您想要删除的注释文本。  
- 如果 `save` 调用抛出 `IOException`，请再次检查文件系统权限。  

## Common Use Cases

1. **Java 数据匿名化** – 在共享数据集之前，去除包含个人标识的审阅者评论。  
2. **法律文档编辑** – 自动删除可能泄露机密信息的内部注释。  
3. **批量处理流水线** – 将上述步骤集成到 CI/CD 作业中，**处理多个文档** 并实时清理生成的报告。  

## Performance Considerations

- **优化正则表达式** – 复杂的表达式会增加 CPU 时间，尤其是在大型 PDF 上。  
- **复用 Redactor 实例** 仅在处理同类型的多个文件时使用；否则每个文件实例化一次，以保持低内存占用。  
- **性能分析** – 使用 Java 性能分析工具（如 VisualVM）定位批量操作中的瓶颈。  

## Frequently Asked Questions

**问：GroupDocs.Redaction for Java 是什么？**  
**答：** 这是一款 Java 库，可对多种文档格式的文本、元数据和注释进行编辑。

**问：如何在一次执行中应用多个正则表达式模式？**  
**答：** 在单个模式中使用管道符 (`|`) 组合，或链式调用多个 `DeleteAnnotationRedaction`。

**问：该库是否支持非文本格式，如图像？**  
**答：** 是的，它可以编辑基于图像的 PDF 和其他栅格格式，但注释删除仅适用于受支持的矢量格式。

**问：如果我的文档类型未列在支持列表中怎么办？**  
**答：** 请查看最新的[文档](https://docs.groupdocs.com/redaction/java/)以获取更新，或先将文件转换为受支持的格式。

**问：在编辑过程中应如何处理异常？**  
**答：** 将编辑逻辑放在 try‑catch 块中，记录异常细节，并确保在 finally 子句中调用 `redactor.close()`。

## Additional Resources

- [文档](https://docs.groupdocs.com/redaction/java/)
- [API 参考](https://reference.groupdocs.com/redaction/java)
- [下载 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub 仓库](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)

---

**最后更新：** 2026-02-18  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs