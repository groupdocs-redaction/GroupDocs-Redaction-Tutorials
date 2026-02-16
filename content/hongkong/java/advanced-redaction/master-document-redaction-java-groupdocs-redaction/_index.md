---
date: '2026-02-16'
description: 學習如何在 Java 中使用 GroupDocs.Redaction 進行敏感資料遮蔽與 PDF 個人資料編輯，確保符合隱私合規與資料保護。
keywords:
- Java document redaction
- GroupDocs.Redaction setup
- Precise document redactions
title: Java 敏感資料遮蔽 – 使用 GroupDocs.Redaction 進行個人資訊刪除
type: docs
url: /zh-hant/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/
weight: 1
---

# 遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 進行個人資訊編輯

在當今快速變化的數位環境中，**masking sensitive data java** 已不再是可選項——它是合規要求。無論你是為客戶準備合約、分享醫療紀錄，或僅僅整理內部報告，都需要一種可靠的方式來隱藏個人識別資訊，同時保持文件原始版面的完整。在本教學中，我們將示範如何使用功能強大的 GroupDocs.Redaction Java 函式庫來 **mask sensitive data java** 以及 **redact personal data pdf**。

## 快速解答
- **“mask sensitive data java” 是什麼意思？** 它指的是在基於 Java 的文件工作流程中，以程式方式定位並隱藏私人資訊（姓名、身分證號等）。  
- **使用哪個函式庫？** GroupDocs.Redaction for Java。  
- **需要授權嗎？** 免費試用版非常適合測試；正式使用則需購買完整授權。  
- **也能編輯 PDF 個人資料檔案嗎？** 當然可以——GroupDocs.Redaction 支援 PDF、DOCX、XLSX、PPTX 以及其他多種格式。  
- **需要哪個 Java 版本？** JDK 8 或更高。

## 什麼是 Mask Sensitive Data Java？

在 Java 中遮蔽敏感資料是指使用程式碼在文件內定位特定字串或模式，並以佔位符（例如「[personal]」）取代。此過程確保原始內容無法復原，同時保留文件的視覺完整性。

## 為什麼使用 GroupDocs.Redaction 進行遮蔽？

- **完整格式支援** – 可直接編輯 PDF、Word 檔案、試算表與簡報，無需轉換。  
- **精確字串匹配** – 針對像 “John Doe” 這樣的精確文字。  
- **自訂取代選項** – 可選擇文字、黑色方框或圖像覆蓋。  
- **符合合規需求** – 開箱即支援 GDPR、HIPAA 以及其他隱私法規。

## 先決條件
- 已安裝 **Java Development Kit (JDK) 8+**。  
- **IDE**（如 IntelliJ IDEA 或 Eclipse）以便輕鬆除錯。  
- **GroupDocs.Redaction for Java**（版本 24.9 或更新）。  
- 基本的 Java 檔案處理知識。

## 設定 GroupDocs.Redaction for Java

### Maven 設定
將 GroupDocs 儲存庫與相依性加入你的 `pom.xml`：

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
如果你偏好手動管理，請從官方發佈頁面取得最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權
- **免費試用** – 非常適合評估 API。  
- **臨時授權** – 用於延長測試而無需購買。  
- **完整授權** – 商業部署與無限制編輯時必須。

## 如何使用 GroupDocs.Redaction 進行 Mask Sensitive Data Java

以下我們將實作分解為清晰的編號步驟。每一步都包含簡短說明，並附上原始程式碼區塊（保持不變）。

### 步驟 1：初始化 Redactor

載入要處理的文件。這會建立一個 `Redactor` 實例，用於管理後續的編輯操作。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Load the document from YOUR_DOCUMENT_DIRECTORY
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

### 步驟 2：定義並套用 Exact‑Phrase Redaction

指定要遮蔽的精確字串（例如某人的姓名）以及最終文件中將顯示的取代文字。

```java
try {
    // Define the phrase to be redacted and its replacement
    ExactPhraseRedaction redaction = new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
    
    // Apply the redaction to the document
    redactor.apply(redaction);
} finally {
    redactor.close();
}
```

**重點說明**  
- `ExactPhraseRedaction` 針對字面字串 “John Doe”。  
- `ReplacementOptions("[personal]")` 告訴引擎將該字串取代為佔位符 “[personal]”。  
- 請務必關閉 `Redactor` 以釋放資源。

### 步驟 3：使用自訂選項儲存已編輯的文件

遮蔽資料後，你可能希望保留原始檔案格式，並在檔名加入有用的後綴（例如日期）。

```java
import com.groupdocs.redaction.options.SaveOptions;
import java.text.SimpleDateFormat;
import java.util.Date;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
try {
    // Define save options for the document
    SaveOptions saveOptions = new SaveOptions();
    
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    saveOptions.setRasterizeToPDF(false); // Do not rasterize content into PDF
    
    // Set a date-based suffix for the redacted file
    String suffix = new SimpleDateFormat("dd-MM-yyyy").format(new Date());
    saveOptions.setRedactedFileSuffix(suffix);
    
    // Save the document with specified options
    redactor.save(saveOptions);
} finally {
    redactor.close();
}
```

**選項說明**  
- `setAddSuffix(true)` 會自動將產生的後綴附加到新檔名。  
- `setRasterizeToPDF(false)` 保留原始格式（DOCX、PDF 等），而非將所有內容轉為影像式 PDF。

## 如何在 Java 中編輯 PDF 個人資料

相同的 API 也適用於 PDF 檔案。只要將 `Redactor` 建構子指向 `.pdf` 檔，即可依照上述精確字串步驟操作。由於函式庫會解析 PDF 的文字層，您可以在合約、發票或其他 PDF 報告中遮蔽識別資訊，同時保留可搜尋的文字。

## 實務應用
1. **法律文件管理** – 在與第三方共享合約前移除客戶姓名。  
2. **醫療資料處理** – 遮蔽患者識別碼，以符合 HIPAA 規範。  
3. **金融服務** – 在審計報表中隱藏帳號。  
4. **人力資源** – 在內部審查時保護員工個人資料。

## 大型檔案效能建議
- **盡快關閉 Redactor 實例** 以釋放記憶體。  
- **批次處理** 多個文件時使用迴圈，盡可能重複利用同一個 `Redactor`。  
- **監控 CPU 與 RAM** 在高負載時；若遇到 `OutOfMemoryError`，考慮增大 JVM 堆積大小。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **未套用編輯** | 確認精確字串的大小寫是否匹配；如有需要，可使用帶 `ignoreCase` 選項的 `ExactPhraseRedaction`。 |
| **PDF 輸出為空白** | 確保已設定 `setRasterizeToPDF(false)`；光柵化會移除可搜尋的文字。 |
| **授權錯誤** | 確認試用版或完整授權檔案已正確放置，且路徑已透過 `License.setLicense("path/to/license.lic")` 提供。 |

## 常見問答

**Q1：如何一次處理多個編輯？**  
A1：您可以使用 `redactor.applyAll()` 套用 `Redaction` 物件清單，於單一次執行中處理多個模式。

**Q2：能將 GroupDocs.Redaction 整合至其他文件管理系統嗎？**  
A2：可以，該 API 與平台無關，可從 Web 服務、微服務或桌面應用程式呼叫。

**Q3：GroupDocs.Redaction 支援哪些檔案格式？**  
A3：支援 DOCX、PDF、XLSX、PPTX 以及其他多種常見商務格式。

**Q4：在編輯大型文件時如何管理效能？**  
A5：考慮使用批次處理、串流輸入檔案，並始終及時關閉 `Redactor` 實例以釋放資源。

---

**最後更新：** 2026-02-16  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs