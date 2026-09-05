---
date: '2026-08-14'
description: 使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字 – 高效遮蔽個人資訊並取代敏感文字。
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: 使用 GroupDocs.Redaction for Java 可永久遮蔽個人資料，並在 PDF、DOCX 等檔案中取代敏感字串，確保符合
  GDPR 與 HIPAA 規範。
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: 如何使用 GroupDocs.Redaction for Java 遮蔽文字
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
title: 如何使用 GroupDocs.Redaction for Java 遮蔽文字
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# 如何使用 GroupDocs.Redaction for Java 進行文字遮蔽

在本教學中，您將學習 **如何遮蔽文字**，使用 GroupDocs.Redaction 處理基於 Java 的文件。您將看到如何遮蔽個人資訊、以安全的佔位符取代敏感字串，並以批次友善的方式處理多個檔案。完成後，您將擁有一個可投入生產的解決方案，保護隱私、符合 GDPR/HIPAA 要求，且能順利整合至現有的 Java 應用程式。

## 快速解答
- **使用的程式庫是什麼？** GroupDocs.Redaction for Java.  
- **我可以遮蔽個人資訊嗎？** 是 — 使用 exact‑phrase redaction 搭配 replacement options.  
- **支援批次處理嗎？** 絕對支援，您可以使用相同的 Redactor 實例迴圈處理多個檔案。  
- **需要授權嗎？** 免費試用可用於評估；商業授權則需於正式環境使用。  
- **需要哪個 Java 版本？** JDK 8 或更高版本。

## 什麼是「如何遮蔽文字」？

遮蔽會永久移除或隱蔽文件中的機密資料。使用 GroupDocs.Redaction，您可以定位特定字串、以安全的佔位符取代，並儲存已清理的檔案——全部不需手動編輯。

## 為什麼要使用 GroupDocs.Redaction for Java？

GroupDocs.Redaction for Java 支援 **50+ 輸入與輸出格式**（包括 PDF、DOCX、XLSX、PPTX、TXT、RTF），且能在不將整個文件載入記憶體的情況下處理數百頁的檔案，於標準伺服器硬體上提供高吞吐量的批次作業。

## 前置條件
- **Java Development Kit (JDK)：** Version 8 或更新版本。  
- **IDE：** IntelliJ IDEA、Eclipse，或任何相容 Java 的編輯器。  
- **Maven：** 用於相依性管理。  
- **Basic Java knowledge：** 熟悉類別、方法與例外處理。

## 設定 GroupDocs.Redaction for Java

首先，將程式庫加入您的 Maven 專案。

### Maven 設定

將儲存庫與相依性加入您的 `pom.xml` 檔案：

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

### 直接下載

如果您偏好，可從 [GroupDocs Redaction Java 文件說明](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權

您可以先使用 **Free Trial**，或申請 **Temporary License** 以進行延長測試，亦或購買 **Commercial License** 以供正式環境使用。

## 如何使用 GroupDocs.Redaction 在文件中遮蔽文字

以下章節將逐步說明如何 **遮蔽個人資訊** 與 **取代敏感文字**。

### 步驟 1：初始化 Redactor

`Redactor` 是核心類別，用於載入文件、套用遮蔽規則，並寫入輸出。  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### 步驟 2：套用 exact‑phrase redaction

`ExactPhraseRedaction` 會搜尋完全相符的字串，而 `ReplacementOptions` 定義匹配文字的取代方式。

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **參數：**  
  - `"John Doe"` – 要被遮蔽的精確文字。  
  - `ReplacementOptions("[personal]")` – 用於取代原始內容的字串，實際上 **遮蔽個人資訊**。

### 步驟 3：儲存已遮蔽的文件

`Redactor.save` 將修改後的文件寫入新檔或覆寫原檔，並保留原始格式。

```java
redactor.save();
```

### 步驟 4：清理資源

務必呼叫 `Redactor.close()` 以釋放本機資源，避免記憶體泄漏。

```java
finally {
    redactor.close();
}
```

## 如何使用自訂回呼遮蔽個人資訊

自訂回呼允許您對每個遮蔽事件作出回應——對於記錄、條件性取代或稽核追蹤皆相當有用。

### 建立回呼類別

`IRedactionCallback` 定義在每次遮蔽操作前後會被呼叫的方法。

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### 在實例化 Redactor 時使用回呼

透過 `RedactorSettings` 傳入您的回呼實作，讓引擎在處理時知道呼叫它。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## 實務應用
- **Legal contracts：** 在分享草稿前自動隱藏客戶姓名、社會安全號碼或機密條款。  
- **Medical records：** 在將紀錄匯出給研究合作夥伴時 **遮蔽個人資訊**，例如患者識別碼。  
- **Corporate communications：** 在對外發佈前 **取代敏感文字**，如內部專案代碼，確保不會意外洩漏。

## 效能考量
處理大量或多檔案時，請留意以下建議：

- **Batch processing：** 迴圈處理檔案集合，以減少啟動開銷。  
- **Memory management：** 每處理完一個檔案後釋放 `Redactor`；避免同時在記憶體中保留多個文件。  
- **Profiling：** 使用 Java 效能分析工具（例如 VisualVM）找出 I/O 或遮蔽邏輯的瓶頸。

## 常見問題
**Q: 我可以使用 GroupDocs.Redaction 從 PDF 中遮蔽文字嗎？**  
A: 是的，程式庫支援 PDF、DOCX、XLSX、PPTX 以及其他多種格式。

**Q: 遮蔽是可逆的嗎？**  
A: 否。遮蔽會永久移除原始內容，請保留來源檔案的備份。

**Q: 如何有效處理非常大的文件？**  
A: 將其分段處理，使用批次模式，並使用效能分析工具監控記憶體使用情況。

**Q: 支援哪些其他文字格式？**  
A: 除了 DOCX 與 PDF，還可遮蔽 TXT、RTF、XLSX、PPTX 等。

**Q: 我可以將 GroupDocs.Redaction 整合到現有工作流程嗎？**  
A: 當然可以。API 可從 Web 服務、背景工作或 CI/CD 流程中呼叫。

## 資源
- **Documentation：** [GroupDocs Redaction Java 文件說明](https://docs.groupdocs.com/redaction/java/)  
- **API reference：** [GroupDocs Java API 參考文件](https://reference.groupdocs.com/redaction/java)  
- **Download：** [GroupDocs.Redaction 下載](https://releases.groupdocs.com/redaction/java/)  
- **GitHub repository：** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support forum：** [GroupDocs 免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license application：** [申請臨時授權](https://purchase.groupdocs.com/temporary-license/)

**最後更新：** 2026-08-14  
**測試版本：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學

- [遮蔽敏感資料 Java – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 遮蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [編輯受密碼保護的文件 Java – 使用 GroupDocs.Redaction 遮蔽文件](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)