---
date: 2026-07-01
description: 了解如何在 Java 中使用 OCR 对扫描的 PDF 进行脱敏，删除敏感数据 PDF，并使用 GroupDocs.Redaction 对基于图像的
  PDF 进行脱敏。
keywords:
- how to redact scanned pdf
- remove sensitive data pdf
- redact image based pdf
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  headline: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  name: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  steps:
  - name: Detect precise word coordinates on scanned pages.
    text: Detect precise word coordinates on scanned pages.
  - name: Apply regex patterns or custom rules across the entire document.
    text: Apply regex patterns or custom rules across the entire document.
  - name: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
    text: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
  type: HowTo
- questions:
  - answer: Yes. Open the document with its password, run OCR, then apply redaction
      before saving the protected file.
    question: Can I use secure pdf redaction with password‑protected PDFs?
  - answer: The on‑premise version runs entirely on your server, so no internet connection
      is required.
    question: Does Aspose OCR Java work offline?
  - answer: OCR accuracy drops with low resolution. Improve results by pre‑processing
      images (binarization, deskew) before feeding them to the OCR engine.
    question: How accurate is the redaction when the source is a low‑resolution scan?
  - answer: GroupDocs.Redaction offers a preview API that shows redaction rectangles
      on the PDF canvas, allowing you to confirm locations.
    question: Is it possible to preview redaction areas before committing?
  - answer: A full GroupDocs.Redaction license and a valid Aspose OCR Java license
      are required for commercial deployments.
    question: What licensing is needed for production?
  type: FAQPage
title: 如何使用 OCR 对扫描的 PDF 进行脱敏 – GroupDocs.Redaction Java
type: docs
url: /zh/java/ocr-integration/
weight: 10
---

# 如何编辑扫描的 PDF

在当今的数据隐私环境中，**如何编辑扫描的 PDF** 是任何处理敏感文档的应用程序的不可协商的需求。无论您是要保护个人标识符、财务记录还是机密合同，您都需要一种能够可靠擦除基于图像的 PDF 中信息的解决方案。本教程向您展示为何基于 OCR 的编辑至关重要，带您了解 Java 支持的 OCR 引擎，并指向结合 GroupDocs.Redaction 与强大文本识别引擎的即用示例。

## 快速答案
- **安全 PDF 编辑能实现什么？** 它永久删除或遮蔽敏感文本，使其无法被恢复或读取。  
- **支持哪些 OCR 引擎？** Aspose OCR（本地部署和云）以及 Microsoft Azure Computer Vision 完全兼容。  
- **我需要许可证吗？** 临时许可证足以用于测试；生产使用需要完整许可证。  
- **我可以编辑扫描的 PDF 吗？** 可以——一旦 OCR 提取文本，GroupDocs.Redaction 即可处理基于图像的 PDF。  
- **Java 是唯一支持的语言吗？** 这些概念适用于所有 GroupDocs SDK，但此处的代码示例特定于 Java。

## 什么是安全 PDF 编辑？
安全 PDF 编辑永久删除或遮蔽 PDF 文件中的机密信息，确保隐藏的文本无法通过 OCR 或复制粘贴操作恢复。不同于仅覆盖文本的视觉编辑，此过程从文件结构中移除底层数据，保证即使使用高级取证工具也无法恢复信息。

## 为什么将 OCR 与 GroupDocs.Redaction 结合？
OCR 将仅图像页面转换为可搜索的文本，使 GroupDocs.Redaction 能够定位并擦除精确的单词位置。通过集成 OCR，您可以实现：

1. 检测扫描页面上精确的单词坐标。  
2. 在整个文档中应用正则表达式模式或自定义规则。  
3. 输出保持原始布局且保证数据隐私的干净、可搜索的 PDF。

量化收益：在标准 4 核服务器上，结合 Aspose OCR（支持 **30+ 种语言**，并且在相同硬件上可识别 **每分钟 100 页**），GroupDocs.Redaction 能在 30 秒内处理多达 500 页的 PDF。

## 可用教程

### [在 Java 中使用 GroupDocs 和 Microsoft Azure OCR 实现基于 OCR 的编辑](./ocr-redaction-groupdocs-java-setup/)
了解如何使用 GroupDocs.Redaction for Java 实现基于 OCR 的编辑。通过精确的文本识别和编辑确保数据隐私。

### [使用 Aspose OCR 和 Java 的安全 PDF 编辑：使用 GroupDocs.Redaction 实现正则表达式模式](./aspose-ocr-java-pdf-redaction/)
了解如何使用 Aspose OCR 和 Java 保护 PDF 中的敏感信息。按照本指南使用 GroupDocs.Redaction 进行基于正则表达式的编辑。

## 其他资源

- [GroupDocs.Redaction for Java 文档](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 参考](https://reference.groupdocs.com/redaction/java/)
- [下载 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

## 如何使用 Aspose OCR Java 开始安全 PDF 编辑
加载 Aspose OCR 引擎，对每个页面图像进行处理，并将生成的文本输入到 GroupDocs.Redaction。此两步流水线让您能够：

- 从每个扫描页面提取可搜索的文本。  
- 使用正则表达式匹配敏感模式（例如，SSN、信用卡号）。  
- 应用编辑矩形，使其成为最终 PDF 的永久部分。

**技巧提示：** 在 Aspose OCR Java 中启用 `setUseParallelProcessing(true)` 可将多页文档的处理速度提升至 40 %。`setUseParallelProcessing(true)` 将 OCR 引擎配置为并行处理多个页面，提升多核服务器的吞吐量。

## 如何使用 GroupDocs.Redaction 和 OCR 编辑扫描的 PDF？
使用 `RedactionEngine` 加载您的 PDF。`RedactionEngine` 是 GroupDocs.Redaction Java 的核心类，用于加载 PDF 文档并提供编辑操作。运行 OCR 以获取文本层，定义编辑规则，然后保存编辑后的文件。整个工作流可在三个简洁步骤中完成，并且可处理高达 200 MB 的 PDF 而无需将整个文件加载到内存中。

## 常见陷阱与故障排除
- **OCR 后缺失文本：** 确认 OCR 语言设置正确（例如，`setLanguage("en")`）。  
- **编辑未生效：** 确保将 OCR 结果传递给 `RedactionOptions` 对象；`RedactionOptions` 包含编辑矩形、覆盖颜色以及是否保留原始布局等设置。否则 GroupDocs 会将文档视为仅图像。  
- **性能瓶颈：** 对于大型 PDF，批量处理页面并复用 OCR 引擎实例，而不是为每页创建新实例。

## 常见问题

**Q: 我可以对受密码保护的 PDF 使用安全 PDF 编辑吗？**  
A: 可以。使用密码打开文档，运行 OCR，然后在保存受保护的文件前进行编辑。

**Q: Aspose OCR Java 能离线工作吗？**  
A: 本地部署版本完全在您的服务器上运行，无需互联网连接。

**Q: 当源文件是低分辨率扫描时，编辑的准确性如何？**  
A: 低分辨率会降低 OCR 准确性。通过在将图像输入 OCR 引擎前进行预处理（二值化、去倾斜）可提升效果。

**Q: 是否可以在提交前预览编辑区域？**  
A: GroupDocs.Redaction 提供预览 API，在 PDF 画布上显示编辑矩形，帮助您确认位置。

**Q: 生产环境需要什么许可证？**  
A: 商业部署需要完整的 GroupDocs.Redaction 许可证以及有效的 Aspose OCR Java 许可证。

---

**最后更新：** 2026-07-01  
**测试环境：** GroupDocs.Redaction 23.11 for Java, Aspose OCR Java 23.6  
**作者：** GroupDocs

## 相关教程

- [如何使用 Aspose OCR 和 Java 编辑 PDF - 使用 GroupDocs.Redaction 实现正则表达式模式](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)
- [使用 GroupDocs.Redaction Java 为 PDF 创建编辑策略](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)
- [如何使用 GroupDocs.Redaction 编辑 Java 文档](/redaction/java/advanced-redaction/java-redaction-groupdocs-guide/)