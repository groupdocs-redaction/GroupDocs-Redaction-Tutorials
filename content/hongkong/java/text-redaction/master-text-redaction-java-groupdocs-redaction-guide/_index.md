---
date: '2026-08-20'
description: 了解如何在 Java 中使用 GroupDocs.Redaction 及正則表達式 (regex) 刪除文字。本分步教學將示範如何套用 regex、設定儲存選項，並保護敏感資料。
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: 學習如何在 Java 中使用 GroupDocs.Redaction 刪除文字。本指南說明 regex 刪除、儲存選項設定，以及保護敏感資料的效能技巧。
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: 在 Java 中使用 GroupDocs.Redaction 進行文字刪除
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 在 Java 中使用 GroupDocs.Redaction 進行文字刪除的完整指南
type: docs
url: /zh-hant/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Redaction 進行文字遮蔽：完整指南

在當今快速發展的數位世界中，文件中 **如何遮蔽文字** 是許多開發人員面臨的問題。無論是保護個人資料、遵守法規，或只是清理草稿，本指南將帶領您使用 GroupDocs.Redaction for Java **快速且安全地套用基於正則表達式的遮蔽**。您將了解遮蔽的重要性、如何設定此函式庫，以及高效能處理的最佳實踐技巧。

## 快速回答
- **GroupDocs.Redaction 的主要目的為何？** 它提供可靠的 API 以在超過 50 種文件格式中定位並遮蔽敏感文字。  
- **如何套用正則表達式進行遮蔽？** 建立一個帶有模式的 `RegexRedaction` 物件，並將其傳遞給 `Redactor.apply()` 方法。  
- **我需要授權嗎？** 免費試用可用於開發；付費授權則解鎖正式環境的全部功能。  
- **我可以同時遮蔽 PDF 與 DOCX 檔案嗎？** 可以 — GroupDocs.Redaction 支援 PDF、DOCX、PPTX 以及許多其他格式。  
- **提升效能的最佳方法是什麼？** 及時關閉 `Redactor` 實例、保持正則表達式簡潔，並以批次方式處理檔案。  

## 什麼是文字遮蔽以及為何重要？
文字遮蔽會永久移除或隱蔽文件中的敏感資訊，確保機密資料（例如社會安全號碼、信用卡資訊或醫療紀錄）不會被未授權的對象恢復或檢視。它透過覆寫原始字元或以遮蔽層取代，使隱藏的內容無法透過複製貼上或 OCR 工具擷取。此舉確保符合隱私法規，並保護個人免於身分盜用或資料外洩。

## 為何使用正則表達式進行文字遮蔽？
正則表達式讓您能定義彈性的模式，以匹配各種資料格式（例如電話號碼、信用卡號碼）。將正則表達式與 GroupDocs.Redaction 結合使用，可精確控制要遮蔽的內容，同時保持實作簡潔且易於維護。

## 前置條件
在開始之前，請確保您已具備以下條件：

- **Java Development Kit (JDK)** 已安裝（Java 8 或更新版本）。  
- 基本熟悉 Java 語法與正則表達式。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE，以執行與偵錯程式碼。  

## 設定 GroupDocs.Redaction for Java
首先，將函式庫加入您的專案。

### Maven 設定
如果您使用 Maven，請在 `pom.xml` 中加入以下內容：

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
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 基本初始化
`Redactor` 是核心類別，用於開啟文件、套用遮蔽規則，並寫入輸出。

函式庫可用後，您即可開始遮蔽文件：

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## 如何在 Java 中使用正則表達式遮蔽文字？
此流程包括將來源檔案載入 `Redactor` 實例、建立定義匹配模式的 `RegexRedaction` 規則、使用 `redactor.apply()` 套用規則，最後以 `SaveOptions` 儲存修改後的文件。遵循這些步驟，即可在支援的格式中可靠地定位並遮蔽任何敏感字串。

`Redactor` 類別是核心元件，負責開啟文件、套用遮蔽規則，並寫入輸出檔案。它在內部管理資源，處理完畢後必須關閉以釋放記憶體。

### 步驟 1：匯入必要類別
以下匯入可讓您存取遮蔽 API：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 步驟 2：初始化 redactor 並套用正則表達式模式
`RegexRedaction` 代表基於正則表達式模式的遮蔽規則。您提供的模式決定哪些文字片段會被取代。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **正則說明**：模式 `\b\d{3}-\d{2}-\d{4}\b` 匹配美國社會安全號碼（三位數、連字號、兩位數、連字號、四位數）。`ReplacementOptions` 讓您選擇實心黑色覆蓋或自訂文字遮蔽。

### 步驟 3：設定儲存選項
`SaveOptions` 控制遮蔽後檔案的寫入方式。加入副檔名可清楚標示哪些檔案已處理，同時保留原始格式以避免不必要的轉換。

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **儲存選項**：`setAddSuffix(true)` 會自動在輸出檔名後加上 “_redacted”，防止意外覆寫。

### 步驟 4：自訂其他儲存設定
您可以透過調整 `SaveOptions` 物件，進一步客製化輸出，例如保留中繼資料或將註解平面化。

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **關鍵設定**：設定 `setPreserveMetadata(true)` 可保留原始文件屬性，這在合規審計時常常是必需的。

## 實務應用
在實務情境中，**如何遮蔽文字** 是必不可少的：

1. **法律文件** – 在與外部律師共享草稿前隱藏客戶識別碼。  
2. **醫療紀錄** – 遮蔽患者姓名、身分證號或健康編號，以符合 HIPAA 規範。  
3. **財務報告** – 在發佈季報時移除機密帳號。  

## 效能考量
- **記憶體管理**：務必呼叫 `redactor.close()` 以釋放檔案句柄與原生資源。  
- **有效的正則表達式**：較簡單的模式執行更快；盡可能使用原子群組以避免過度回溯。  
- **批次處理**：對於大量文件，將檔案分批（20–50 個）處理，以保持堆積使用量可預測。  

## 常見問題與解決方案
| 問題 | 解決方案 |
|-------|----------|
| **正則表達式匹配過多** | 使用線上正則測試工具測試您的模式，並縮小字元類別。 |
| **輸出檔名衝突** | 使用 `setAddSuffix(true)` 或透過 `saveOptions.setOutputPath()` 提供自訂輸出路徑。 |
| **大型 PDF 記憶體泄漏** | 逐頁處理 PDF，或增加 JVM 堆積大小 (`-Xmx2g`)。 |

## 常見問答

**Q: `SaveOptions` 中 `setAddSuffix(true)` 的目的為何？**  
A: 它會自動在輸出檔名後加上副檔名（例如 `_redacted`），以明確標示哪些檔案已被處理。

**Q: 我可以使用除數字外的正則表達式模式進行文字遮蔽嗎？**  
A: 當然可以。任何有效的 Java 正則表達式皆可提供給 `RegexRedaction`，以針對電子郵件、電話號碼、自訂 ID 等。

**Q: 我該如何處理遮蔽過程中的錯誤？**  
A: 將遮蔽邏輯包在 try‑catch 區塊中，記錄例外，並在 finally 區段中始終關閉 `Redactor` 以釋放資源。

**Q: 是否支援 PDF 遮蔽？**  
A: 支援。GroupDocs.Redaction 可處理 PDF、DOCX、PPTX 以及許多其他格式。

**Q: 大規模遮蔽專案的最佳實踐是什麼？**  
A: 使用批次處理、保持正則表達式簡潔，並使用效能分析工具監控記憶體使用情況。

## 其他資源
- **文件說明**： [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**： [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**最後更新：** 2026-08-20  
**測試版本：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學

- [遮蔽敏感資料 Java – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 遮蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [如何使用 Aspose OCR 與 Java 遮蔽 PDF - 使用 GroupDocs.Redaction 實作正則表達式模式](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)