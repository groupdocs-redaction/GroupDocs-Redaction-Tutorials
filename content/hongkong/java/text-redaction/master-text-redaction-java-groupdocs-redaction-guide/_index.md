---
date: '2026-03-01'
description: 了解如何在 Java 中使用正則表達式與 GroupDocs.Redaction 進行文字遮蔽。此逐步教學將示範如何套用正則表達式、設定儲存選項，並保護敏感資料。
keywords:
- text redaction in Java
- regex text redaction
- GroupDocs.Redaction
title: 如何在 Java 中使用 GroupDocs.Redaction 進行文字遮蔽：完整指南
type: docs
url: /zh-hant/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Redaction 進行文字遮蔽：完整指南

在當今快速變化的數位世界中，文件中**如何遮蔽文字**是許多開發者面臨的問題。無論是保護個人資料、遵守法規，或只是清理草稿，本指南將帶領您使用 GroupDocs.Redaction for Java，快速且安全地**如何套用正規表達式**進行遮蔽。

我們將涵蓋從設定函式庫、編寫正規表達式模式、配置儲存選項，到說明遮蔽重要性的實務案例等全部內容。

## 快速解答
- **GroupDocs.Redaction 的主要目的為何？** 它提供可靠的 API 以在多種文件格式中定位並遮蔽敏感文字。  
- **如何套用正規表達式進行遮蔽？** 建立帶有您的模式的 `RegexRedaction` 物件，並將其傳遞給 `Redactor.apply()` 方法。  
- **我需要授權嗎？** 免費試用可用於開發；付費授權則解鎖正式環境的全部功能。  
- **我可以同時遮蔽 PDF 與 DOCX 檔案嗎？** 可以——GroupDocs.Redaction 支援 PDF、DOCX、PPTX 等多種格式。  
- **提升效能的最佳方法是什麼？** 盡快關閉 `Redactor` 實例，並盡量保持正規表達式簡潔。  

## 什麼是文字遮蔽，為何它很重要？
文字遮蔽是永久移除或隱蔽文件中敏感資訊的過程。它確保機密資料（例如身分證號碼、醫療紀錄或財務細節）不會被未授權的人士恢復或檢視。

## 為何使用正規表達式進行文字遮蔽？
正規表達式讓您能定義彈性的模式，以匹配各種資料格式（例如電話號碼、信用卡號碼）。將正規表達式與 GroupDocs.Redaction 結合，可精確控制要隱蔽的內容，同時保持實作簡潔。

## 前置條件
在開始之前，請確保您已具備以下條件：

- 已安裝 **Java Development Kit (JDK)**（Java 8 或更新版本）。  
- 具備 Java 語法與正規表達式的基本認識。  
- 使用如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE 來執行與除錯程式碼。  

## 設定 GroupDocs.Redaction（Java 版）
首先，將函式庫加入您的專案中。

### Maven 設定
如果您使用 Maven，請將以下內容插入 `pom.xml`：

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
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR 檔案。

### 基本初始化
函式庫可用後，即可開始對文件進行遮蔽：

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

## 如何在 Java 中使用正規表達式遮蔽文字？
以下是逐步說明，展示 **如何遮蔽文字** 之正規表達式模式的使用方式。

### 功能 1：正規表達式文字遮蔽
**概述**：此功能示範核心的 `RegexRedaction` 工作流程。

#### 步驟 3.1：匯入必要類別
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### 步驟 3.2：初始化 Redactor 並套用正規表達式模式
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **正規表達式說明**：此模式匹配符合特定格式的數字序列（例如日期或身分證號碼）。`ReplacementOptions` 使用藍色覆蓋層來標示被遮蔽的區域。

#### 步驟 3.3：配置儲存選項
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

- **儲存選項**：加入後綴可清楚標示已處理的檔案，同時保留原始格式以避免不必要的轉換。

#### 疑難排解技巧
- 確認正規表達式正確捕捉您欲隱蔽的資料。  
- 再次檢查檔案路徑，並確保應用程式具備讀寫權限。  

### 功能 2：儲存選項設定
**概述**：在遮蔽後微調輸出檔案。

#### 步驟 3.4：自訂儲存設定
```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **關鍵設定**：此程式碼片段協助您管理輸出檔名並保留原始文件結構。

## 實務應用
在以下實務情境中，**如何遮蔽文字** 是必須的：

1. **法律文件** – 在與外部律師共享草稿前，隱蔽客戶識別資訊。  
2. **醫療紀錄** – 隱蔽患者姓名、身分證號或健康編號，以符合 HIPAA 規範。  
3. **財務報告** – 在發佈季報時移除機密帳號。  

## 效能考量
- **記憶體管理**：始終關閉 `Redactor` 實例（`redactor.close()`）以釋放資源。  
- **有效率的正規表達式**：較簡單的模式執行更快；盡量避免過於複雜的表達式。  
- **批次處理**：對於大量文件，分批處理以保持記憶體使用可預測。  

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **正規表達式匹配過多** | 使用線上正規表達式測試工具測試您的模式，並縮小字元類別。 |
| **輸出檔名衝突** | 使用 `setAddSuffix(true)` 或透過 `saveOptions.setOutputPath()` 提供自訂輸出路徑。 |
| **大型 PDF 記憶體洩漏** | 逐頁處理 PDF，或增加 JVM 堆積大小（`-Xmx2g`）。 |

## 常見問答

**Q: `setAddSuffix(true)` 在 SaveOptions 中的用途是什麼？**  
A: 它會自動在輸出檔名後加上後綴（例如 `_redacted`），以明確標示哪些檔案已被處理。

**Q: 我可以使用除數字外的正規表達式模式進行文字遮蔽嗎？**  
A: 當然可以。任何有效的 Java 正規表達式皆可提供給 `RegexRedaction`，以針對電子郵件、電話號碼、自訂 ID 等進行遮蔽。

**Q: 我該如何處理遮蔽過程中的錯誤？**  
A: 將遮蔽邏輯包在 try‑catch 區塊中，記錄例外，並在 finally 區塊中始終關閉 `Redactor` 以釋放資源。

**Q: 是否支援 PDF 遮蔽？**  
A: 支援。GroupDocs.Redaction 可處理 PDF、DOCX、PPTX 以及其他多種格式。

**Q: 大規模遮蔽專案的最佳實踐是什麼？**  
A: 使用批次處理、保持正規表達式簡潔，並使用效能分析工具監控記憶體使用情況。

## 資源
以下提供更深入的說明與官方指引：

- **文件說明**： [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**： [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**最後更新：** 2026-03-01  
**測試版本：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs