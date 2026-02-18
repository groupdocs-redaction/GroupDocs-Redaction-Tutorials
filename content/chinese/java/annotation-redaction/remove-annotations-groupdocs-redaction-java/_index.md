---
date: '2026-02-18'
description: 学习如何在一步步的 Java 教程中使用 GroupDocs.Redaction API 删除注释。
keywords:
- remove annotations java
- GroupDocs Redaction API
- document annotation removal
title: 使用 GroupDocs.Redaction 在 Java 中删除批注
type: docs
url: /zh/java/annotation-redaction/remove-annotations-groupdocs-redaction-java/
weight: 1
---

# 使用 GroupDocs.Redaction 删除 Java 注释

当您需要 **remove annotations java** 时，杂乱的评论和标记会使文档难以阅读和处理。无论是清理法律合同、学术草稿还是内部报告，GroupDocs.Redaction 的 Java API 都能提供一种快速、可靠的方式，一次调用即可去除所有注释。在本指南中，我们将逐步介绍您需要的全部内容——从环境设置到清除注释的完整代码——帮助您将此功能集成到自己的 Java 应用程序中。

## 快速答案
- **What does “remove annotations java” mean?** 它指的是使用 Java 代码以编程方式删除文档中所有评论类型的对象。  
- **Which library handles this?** GroupDocs.Redaction for Java.  
- **Do I need a license?** 临时许可证可用于评估；生产环境需要正式许可证。  
- **Can I keep the original file format?** 是的，API 默认以原始格式保存文档。  
- **How long does the operation take?** 对于一般大小的文件通常在一秒以内；较大的 PDF 可能需要几秒钟。

## 什么是 “remove annotations java”？
在 Java 中删除注释是指使用 GroupDocs.Redaction SDK 在文档中定位每个注释对象（评论、突出显示、印章等），并自动将其删除。这消除了在文字处理器中逐个打开文件并手动清除注释的步骤。

## 为什么要删除注释？
- **Legal compliance:** 确保合同在签署前没有审阅者的备注。  
- **Publishing readiness:** 在提交前去除稿件中的审稿人评论。  
- **Performance:** 更清洁的文件在后续处理流水线中加载更快。

## 前置条件

在开始之前，请确保您拥有：

- **GroupDocs.Redaction for Java** 版本 24.9 或更高。  
- **Maven**（如果您偏好依赖管理）或直接下载 JAR。  
- **JDK**（推荐 Java 8 以上）以及 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基础的 Java 知识以及文件 I/O 的使用经验。

## 设置 GroupDocs.Redaction for Java

### Maven 设置
在您的 `pom.xml` 中添加仓库和依赖：

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
或者，从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新的 JAR。

### 获取许可证
要解锁全部功能，请从[许可证页面](https://purchase.groupdocs.com/temporary-license/)获取临时许可证。这样您即可在没有评估限制的情况下进行测试。

### 基础初始化
下面是一个最小的启动类，用于打开文档。保持代码不变——这就是您稍后将使用的完整代码块。

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

## 实现指南：删除所有注释

### 概述
我们将使用 `DeleteAnnotationRedaction` 类，它指示 Redactor 删除发现的所有注释。整个过程包括五个明确的步骤。

### 步骤 1 – 导入包
这些导入让您能够访问 Redactor、保存选项以及特定的脱敏类型。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;
```

### 步骤 2 – 初始化 Redactor
创建一个指向您要清理的文件的 `Redactor` 实例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

### 步骤 3 – 应用 DeleteAnnotationRedaction
这一行代码告诉 SDK 从文档中剥离所有注释。

```java
redactor.apply(new DeleteAnnotationRedaction());
```

### 步骤 4 – 配置保存选项
我们为输出文件名添加后缀，以保持原文件不被修改，并保持原始格式。

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

### 完整示例回顾
将上述代码组合起来，工作流如下：

1. 导入所需的类。  
2. 使用源文件实例化 `Redactor`。  
3. 调用 `apply(new DeleteAnnotationRedaction())`。  
4. 设置 `SaveOptions`（添加后缀，保持格式）。  
5. 调用 `redactor.save(saveOptions)`。

## 为什么这很重要：真实场景
- **Batch processing:** 在循环中运行代码片段，以在归档前清理数千个 PDF。  
- **CI/CD pipelines:** 将调用集成到自动化文档生成步骤中，确保输出不含注释。  
- **Compliance audits:** 使用 API 生成干净的审计记录，无需手动编辑。

## 常见问题及解决方案
- **File path errors:** 验证传递给 `Redactor` 的路径是绝对路径或相对于项目的正确相对路径。  
- **Missing dependencies:** 仔细检查您的 `pom.xml` 或 JAR 类路径；没有核心库 Redactor 将无法启动。  
- **License not applied:** 如果出现许可证异常，请确保临时许可证文件放置在正确的目录并在代码中引用（此处未展示）。

## 实际应用

1. **Legal Document Review:** 在最终签署前删除审阅者的评论。  
2. **Academic Publishing:** 在期刊提交前清除稿件中的同行评审备注。  
3. **Internal Reports:** 提交无草稿注释杂乱的精美报告。  

## 性能考虑
- **Resource Management:** 始终调用 `redactor.close()`（如初始化示例所示）以释放本机资源。  
- **Large Files:** 对于数百页的 PDF，考虑分块处理或增大 JVM 堆大小。  
- **Stay Updated:** 新版本会带来性能改进——请保持 Maven 版本为最新。  

## 常见陷阱及避免方法
| 陷阱 | 解决方案 |
|---------|----------|
| 忘记调用 `redactor.close()` | 将使用包装在 try‑finally 块中（如启动类所示）。 |
| 在路径中使用错误的文件扩展名 | 确保路径与实际文件类型（DOCX、PDF 等）匹配。 |
| 未添加后缀导致覆盖原文件 | 设置 `saveOptions.setAddSuffix(true)` 以保留源文件。 |

## 常见问答

**Q: What is GroupDocs.Redaction?**  
A: GroupDocs.Redaction 是一个 Java API，允许您以编程方式对敏感内容（包括注释）进行脱敏或删除，支持多种文档格式。

**Q: Can I use this in a commercial project?**  
A: 可以，只要您拥有有效的商业许可证。临时许可证仅用于评估。

**Q: Does the API support PDF, DOCX, and other formats?**  
A: 当然。它支持 PDF、DOCX、PPTX、XLSX 等多种文件类型。

**Q: Is there any limit to the number of annotations I can delete?**  
A: 没有硬性限制；性能取决于文档大小和系统资源。

**Q: How can I revert the changes if I delete annotations by mistake?**  
A: API 会覆盖您保存的文件。请在运行脱敏前备份原始文档。

## 资源
- **Documentation:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Reference:** [API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Repository:** [GroupDocs.Redaction for Java](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support Forum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

通过本指南，您现在拥有使用 GroupDocs.Redaction **remove annotations java** 的可靠方法。将代码片段集成到批处理流水线中，随时获得更清洁、无注释的文档。

---

**最后更新：** 2026-02-18  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs