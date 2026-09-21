---
date: '2026-09-21'
description: 如何使用 GroupDocs.Redaction 進行 Java 敏感資訊遮蔽 – 步驟說明指南，教您如何保護 Word、PDF、Excel、PowerPoint
  及圖像檔案中的敏感資料。
keywords:
- how to redact java
- GroupDocs.Redaction Java
- document redaction library
lastmod: '2026-09-21'
og_description: 如何使用 GroupDocs.Redaction 進行 Java 敏感資訊遮蔽。學習初始化、套用精確片語遮蔽，並在數分鐘內儲存安全文件。
og_image_alt: Developer tutorial screen showing Java redaction workflow with GroupDocs.Redaction
og_title: 如何使用 GroupDocs.Redaction 進行 Java 敏感資訊遮蔽 – 快速開發者指南
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: How to redact java using GroupDocs.Redaction – step‑by‑step guide that
    shows you how to protect sensitive data in Word, PDF, Excel, PowerPoint and image
    files.
  headline: 'How to redact java with GroupDocs.Redaction: A comprehensive guide for
    developers'
  type: TechArticle
- description: How to redact java using GroupDocs.Redaction – step‑by‑step guide that
    shows you how to protect sensitive data in Word, PDF, Excel, PowerPoint and image
    files.
  name: 'How to redact java with GroupDocs.Redaction: A comprehensive guide for developers'
  steps:
  - name: '**Legal document processing:** Strip personal identifiers before sharing
      contracts with external counsel.'
    text: '**Legal document processing:** Strip personal identifiers before sharing
      contracts with external counsel.'
  - name: '**Financial auditing:** Remove account numbers and SSNs from audit reports
      while preserving tables and charts.'
    text: '**Financial auditing:** Remove account numbers and SSNs from audit reports
      while preserving tables and charts.'
  - name: '**Healthcare data management:** Ensure patient records comply with HIPAA
      by redacting PHI before archiving or transmitting.'
    text: '**Healthcare data management:** Ensure patient records comply with HIPAA
      by redacting PHI before archiving or transmitting.'
  type: HowTo
- questions:
  - answer: Redaction permanently removes or masks sensitive information from a document
      so it cannot be recovered.
    question: What is redaction?
  - answer: Yes, it supports PDF, Excel, PowerPoint, and common image types such as
      PNG and JPEG.
    question: Can GroupDocs.Redaction be used with non‑Word formats?
  - answer: A temporary license is free for evaluation; a commercial license is required
      for production deployments.
    question: Do I need a license for development?
  - answer: It processes files in a streaming fashion and releases native resources
      promptly, allowing you to work with multi‑hundred‑page documents without exhausting
      heap memory.
    question: How does the library handle large files?
  - answer: Absolutely – any string can be supplied via `ExactPhraseRedaction` or
      `ReplacementOptions`, for example “[personal]”, “***REDACTED***”, or a generated
      placeholder.
    question: Can I customize the replacement text?
  type: FAQPage
tags:
- java redaction
- GroupDocs
- document security
title: 如何使用 GroupDocs.Redaction 進行 Java 敏感資訊遮蔽：開發者完整指南
type: docs
url: /zh-hant/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/
weight: 1
---

# 如何使用 GroupDocs.Redaction 進行 Java 敏感資訊遮蔽：開發人員完整指南

在本教學中，您將學習 **如何使用 Java 進行遮蔽** 文件，使用 GroupDocs.Redaction，這是一個可永久移除或隱藏機密資料，同時保留原始版面的函式庫。無論您是構建以合規為中心的服務、內部稽核工具，或是面向客戶的入口網站，以下步驟皆提供可在任何 JDK 8+ 環境下執行的生產就緒實作。

## 快速解答
- **主要函式庫是什麼？** GroupDocs.Redaction for Java.  
- **我需要授權嗎？** 測試期間可免費取得臨時授權；正式環境需購買完整授權。  
- **支援哪個 JDK 版本？** JDK 8 或更高版本。  
- **我可以遮蔽 Word、PDF 和圖像嗎？** 可以 — 函式庫支援 Word、PDF、Excel、PowerPoint 以及常見圖像格式。  
- **基本實作需要多長時間？** 簡單的精確片語遮蔽大約需要 10‑15 分鐘。

## 什麼是遮蔽以及為何在 Java 中使用它？
遮蔽會永久移除或遮掩敏感內容，使其無法被還原。在 Java 應用程式中，自動化遮蔽可協助您遵守 GDPR、HIPAA、CCPA 等法規，同時防止組織因意外資料外洩而受損。透過在來源端執行遮蔽，可確保下游系統永遠不會看到原始機密資訊，降低在處理、儲存或傳輸過程中洩漏的風險。

## 為何選擇 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支援 **50+ 輸入與輸出格式**，包括 DOCX、XLSX、PPTX、PDF 與 PNG，且可在不將整份文件載入記憶體的情況下處理上百頁的檔案。API 提供精確片語、正規表達式與影像遮蔽，處理大批量檔案時速度可達 **3 倍以上** 的效能提升。

## 前置條件
- **Java 開發工具包：** 已在您的機器上安裝 JDK 8 或更新版本。  
- **Maven（可選）：** 如果您使用 Maven 管理相依性，您需要將 GroupDocs.Redaction 套件加入 `pom.xml`。  
- **基本 Java 知識：** 熟悉 try‑with‑resources 與 Maven 會有幫助，但不是必須的。

### 必要的函式庫與相依性
您需要使用 GroupDocs.Redaction 函式庫。可透過 Maven 或直接下載 JAR 檔案：

- **Maven 設定：**  
  ```xml
  <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
  </dependency>
  ```  

- **直接下載：** 前往 [GroupDocs.Redaction for Java 版本](https://releases.groupdocs.com/redaction/java/) 取得最新的 JAR 檔。欲取得更多產品資訊，請參閱 [GroupDocs 官方網站](https://releases.groupdocs.com/redaction/java/)。

### 環境設定
確保您的 `JAVA_HOME` 指向 JDK 8+ 的安裝目錄，且您的 IDE 或建置工具能正確解析 GroupDocs.Redaction 的相依性。

### 取得授權
從 [臨時授權頁面](https://purchase.groupdocs.com/temporary-license/) 取得暫時評估授權，以在開發期間解鎖全部功能。執行任何遮蔽程式碼前，請將佔位路徑替換為實際授權檔案的位置。

## 如何遮蔽 Java – 步驟指南

### 如何初始化 Redactor？
載入欲保護的文件並建立 `Redactor` 實例。**Redactor** 為入口類別，負責載入文件、驗證格式，並為後續處理準備內部模型。  
```java
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```  
此行程式碼會開啟檔案、驗證格式，並建立內部模型以供後續使用。

### 如何套用精確片語遮蔽？
建立 `ExactPhraseRedaction` 物件，指定目標文字與取代內容。**ExactPhraseRedaction** 定義一條規則，搜尋字面字串並以提供的遮蔽字元取代每一次出現。此物件亦可設定大小寫敏感與全字匹配等選項，讓您精細控制片語的辨識方式。  
```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction("John Doe", "[personal]");
redactor.apply(redaction);
```  
`apply` 呼叫會掃描整份文件，取代每個符合項目，並在不改變周圍內容的前提下更新文件的內部結構。

### 如何安全地儲存已遮蔽的文件？
在所有遮蔽規則套用完畢後，呼叫 `save` 將修改後的檔案寫入新位置。**save** 會產生文件的全新副本，保留原始檔不受影響——這是審計追蹤的最佳實踐。您亦可在儲存時指定 PDF/A 相容性或影像壓縮等輸出格式選項。  
```java
redactor.save("YOUR_OUTPUT_DIRECTORY/sample_redacted.docx");
```  
請確保輸出目錄已存在且具寫入權限，否則會拋出 `IOException`。

### 我該如何釋放資源？
完成工作後務必關閉 `Redactor`。**close** 會釋放 Redactor 實例所佔用的本機記憶體與其他資源。`Redactor` 實作了 `AutoCloseable` 介面，您可以使用 try‑with‑resources 區塊或在 finally 區段呼叫 `close()`。正確的資源釋放可避免本機記憶體泄漏，特別是在處理大型檔案時。  
```java
redactor.close();
```

## 實務應用
GroupDocs.Redaction for Java 可自然融入多種企業工作流程：

1. **法律文件處理：** 在與外部律師共享合約前去除個人識別資訊。  
2. **金融稽核：** 從稽核報告中移除帳號與社會安全號碼，同時保留表格與圖表。  
3. **醫療資料管理：** 在歸檔或傳輸前遮蔽 PHI，確保患者記錄符合 HIPAA。

您可以將遮蔽邏輯嵌入微服務、批次工作或桌面工具——任何 Java 環境皆可呼叫相同的 API。

## 效能考量
- **串流模式：** 對於大於 200 MB 的檔案，啟用串流以避免將整份文件載入堆疊記憶體。  
- **平行處理：** 處理多個獨立文件時，可在不同執行緒上各自執行 `Redactor` 實例；只要每個執行緒使用自己的實例，函式庫即為執行緒安全。  
- **記憶體分析：** 使用 VisualVM 等工具監控 JVM 堆疊；`close()` 被呼叫時，Redactor 會釋放本機緩衝區。

## 常見問題與解決方案
- **記憶體泄漏：** 忘記關閉 `Redactor` 會導致本機記憶體未釋放。請務必使用 try‑with‑resources 或顯式呼叫 `close()`。  
- **檔案未找到錯誤：** 測試期間請確認輸入與輸出路徑為絕對路徑；相對路徑可能因工作目錄不同而解析錯誤。  
- **授權例外：** 若出現 `LicenseException`，請再次確認授權檔案路徑正確且該檔案對執行程序可讀。

## 常見問答

**Q: 什麼是遮蔽？**  
A: 遮蔽會永久移除或遮掩文件中的敏感資訊，使其無法被還原。

**Q: GroupDocs.Redaction 能否用於非 Word 格式？**  
A: 可以，支援 PDF、Excel、PowerPoint 以及 PNG、JPEG 等常見影像類型。

**Q: 開發時需要授權嗎？**  
A: 臨時授權可免費用於評估；正式環境則需購買商業授權。

**Q: 函式庫如何處理大型檔案？**  
A: 以串流方式處理檔案並即時釋放本機資源，讓您能在不耗盡堆疊記憶體的情況下處理上百頁的文件。

**Q: 我可以自訂取代文字嗎？**  
A: 當然可以 — 任何字串皆可透過 `ExactPhraseRedaction` 或 `ReplacementOptions` 提供，例如 “[personal]”、 “***REDACTED***” 或自訂的佔位字元。

## 結論
您現在已掌握 **如何使用 Java 進行遮蔽** 的完整流程，從初始化 `Redactor`、套用精確片語規則，到安全儲存已清理的檔案。依循上述步驟，您可以將強大的遮蔽功能嵌入任何基於 Java 的工作流程，確保符合隱私法規，並保護組織最敏感的資料。

### 後續步驟
- 探索基於正規表達式的遮蔽，以匹配模式（例如信用卡號）。  
- 結合 GroupDocs.Viewer，為最終使用者呈現已淨化的預覽畫面。  
- 將遮蔽服務整合至 CI/CD 流程，自動在文件歸檔前進行清理。

---

**最後更新：** 2026-09-21  
**測試版本：** GroupDocs.Redaction 24.9  
**作者：** GroupDocs

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

```java
import com.groupdocs.redaction.Redactor;

public class FeatureInitializeRedactor {
    public void run() throws Exception {
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
        
        try {
            // Placeholder for further operations
        } finally {
            redactor.close();
        }
    }
}
```

```java
// Initialize the Redactor object with a sample document path
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

```java
try {
    // Placeholder for further operations
} finally {
    redactor.close();
}
```

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

public class FeatureApplyRedaction {
    public void run() throws Exception {
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
        
        try {
            ExactPhraseRedaction exactPhraseRedaction = new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
            // Apply the redaction to the document
            redactor.apply(exactPhraseRedaction);
        } finally {
            redactor.close();
        }
    }
}
```

```java
import com.groupdocs.redaction.Redactor;

public class FeatureSaveRedactedDocument {
    public void run() throws Exception {
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
        
        try {
            // Placeholder for applying redactions
            redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_sample.docx");
        } finally {
            redactor.close();
        }
    }
}
```

## 相關教學

- [如何使用 GroupDocs 在 Java 中遮蔽 PDF 並隱藏敏感資料](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [如何使用 GroupDocs.Redaction for Java 預覽頁面 – 完整指南](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)
- [如何在 Java 中使用 GroupDocs.Redaction 遮蔽文字 – 教學](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)