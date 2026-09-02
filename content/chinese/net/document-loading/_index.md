---
date: 2026-06-11
description: 了解如何使用 GroupDocs.Redaction for .NET 加载文档，包括从流和受密码保护的文件加载。
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction for .NET 加载文档
type: docs
url: /zh/net/document-loading/
weight: 2
---

# 如何使用 GroupDocs.Redaction for .NET 加载文档

在本指南中，您将了解 **如何加载文档** 文件到 GroupDocs.Redaction for .NET，支持多种来源——本地磁盘、内存流，甚至受密码保护的文件。无论您是在构建脱敏服务、自动合规流水线，还是一个简单的桌面工具，掌握这些加载技术都能让您快速可靠地准备任何文档进行安全脱敏。

## 快速答案
- **第一步是什么？** 安装 GroupDocs.Redaction NuGet 包并添加 `using GroupDocs.Redaction;` 命名空间。  
- **我可以从流加载 PDF 吗？** 可以——将包含 PDF 字节的 `MemoryStream` 传递给 `RedactionEngine` 构造函数。  
- **如何打开受密码保护的文件？** 在创建 `RedactionEngine` 时将密码作为第二个参数提供。  
- **文件大小有上限吗？** GroupDocs.Redaction 可处理高达 2 GB 的文件，而无需将整个文件加载到内存中。  
- **开发时需要许可证吗？** 临时许可证可用于测试；生产部署需要正式许可证。

## 如何加载文档？
`RedactionEngine` 是用于加载和准备文档进行脱敏的核心类。通过使用文件路径（或流）以及必要时的密码创建 `RedactionEngine` 实例来加载文档。此单行调用会读取文件、验证格式，并构建内部文档模型以供脱敏。例如，从磁盘加载 PDF 只需 `new RedactionEngine("sample.pdf")`。需要密码时，使用 `new RedactionEngine("secret.pdf", "MyPassword")`。从流加载遵循相同模式，传入 `MemoryStream` 参数。

## 什么是 GroupDocs.Redaction？
GroupDocs.Redaction 是一个 .NET 库，帮助开发者定位并永久删除 PDF、DOCX、PPTX 以及超过 30 种其他文件格式中的敏感内容。它提供像素级精确脱敏、OCR 支持和批处理功能，是需要在多种文档类型上实现可靠安全数据保护的合规驱动应用的理想选择。

## 为什么在文档加载时使用 GroupDocs.Redaction？
GroupDocs.Redaction 提供高性能、低内存的流式引擎，能够处理高达 2 GB 的大文件，并且开箱即支持受密码保护的文档。这种速度、灵活性和安全性的组合，使其成为需要在应用脱敏规则前快速安全加载文档的开发者的首选。

- **广泛的格式支持：** 处理 **30+** 种文档类型，包括 PDF、Word、Excel、PowerPoint 和图像文件。  
- **高性能流式处理：** 使用低内存流式引擎处理高达 **2 GB** 的文件，消除完整加载文件的需求。  
- **密码处理：** 通过单一方法重载即可无缝打开 **受密码保护的 PDF 和 Office 文件**，降低代码复杂度。  
- **线程安全 API：** 允许在多线程服务中并发加载多个文档而不会出现竞争条件。

## 前置条件
- .NET 6.0 或更高版本（该库还支持 .NET Core 3.1 和 .NET Framework 4.6.1+）。  
- 有效的 GroupDocs.Redaction 许可证（测试用临时许可证）。  
- 能够访问您计划脱敏的文档文件（本地路径、字节数组或流）。

## 从不同来源加载文档

### 从本地磁盘加载
在构造引擎时提供文件的绝对或相对路径。库会自动检测格式并为脱敏做好准备。

### 从内存流加载
将文件读取到 `byte[]`，再包装成 `MemoryStream`，并将该流传递给构造函数。这种方式非常适合接收上传文件的 Web API。

### 加载受密码保护的文件
当文档被加密时，将密码作为第二个参数提供。引擎会即时解密文件，并使内容可用于脱敏，无需额外步骤。

## 常见问题及解决方案

- **错误：“不支持的文件格式”。**  
  验证文件扩展名是否匹配受支持的格式且文件未损坏。GroupDocs.Redaction 支持超过 30 种格式；请查阅 API 参考获取完整列表。

- **密码相关异常。**  
  确保密码字符串正确且文件确实需要密码。向受保护的文件传入空字符串会触发身份验证错误。

- **非常大文件导致内存不足。**  
  使用流式重载 (`RedactionEngine(Stream)`) 而不是通过路径加载文件。即使是上百页的 PDF，也能保持低内存使用。

## 常见问答

**问：我可以像加载 PDF 那样加载 DOCX 文件吗？**  
**答：** 可以——当您传入文件路径或流时，GroupDocs.Redaction 会自动检测 DOCX 格式，无需额外代码。

**问：库是否支持从 Azure Blob Storage 加载文件？**  
**答：** 当然。将 Blob 检索为字节数组或流，然后传入 `RedactionEngine` 构造函数即可。

**问：如果提供了错误的密码会怎样？**  
**答：** 构造函数会抛出 `PasswordIncorrectException`。捕获此异常以提示用户输入正确密码。

**问：是否可以同时加载多个文档？**  
**答：** 可以——每个 `RedactionEngine` 实例都是独立且线程安全的，允许在后台服务中并行处理。

**问：我需要手动释放 RedactionEngine 吗？**  
**答：** 引擎实现了 `IDisposable`。调用 `Dispose()` 或使用 `using` 块来及时释放文件句柄。

## 其他资源

- [如何使用 GroupDocs.Redaction .NET 加载并脱敏文档：完整指南](./groupdocs-redaction-net-load-redact-documents/)
- [如何在 .NET 中使用 GroupDocs.Redaction 安全脱敏受密码保护的文档](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET 文档](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET API 参考](https://reference.groupdocs.com/redaction/net/)
- [下载 GroupDocs.Redaction for .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-06-11  
**测试版本：** GroupDocs.Redaction 5.5 for .NET  
**作者：** GroupDocs

## 相关教程

- [如何使用 GroupDocs.Redaction .NET 加载并脱敏文档：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction for .NET 脱敏并保存文档：完整指南](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)