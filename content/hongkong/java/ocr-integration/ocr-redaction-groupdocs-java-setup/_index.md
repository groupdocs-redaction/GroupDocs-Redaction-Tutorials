---
date: '2026-06-26'
description: 了解如何使用 GroupDocs OCR Redaction 與 Azure OCR，extract text scanned PDF 並
  mask 敏感資料。Redact social security number 並 replace confidential info PDF，以提升效率。
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Extract Text Scanned PDF – 使用 GroupDocs OCR 進行資料遮蔽
type: docs
url: /zh-hant/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# 提取掃描 PDF 文本 – 使用 GroupDocs OCR 掩碼資料

在當今以數據為驅動的世界，**從掃描的 PDF 中提取文本** 並掩碼機密資訊是不可協商的合規步驟。本教程將指導您如何結合 GroupDocs Redaction 與 Microsoft Azure OCR，可靠地識別掃描頁面的隱藏文字，並以安全的佔位符（例如 **`[REDACTED]`**）取代。您將了解為何此組合快速、精確，且適用於生產級工作負載。

## 快速解答
- **「掩碼敏感資料」是什麼意思？** 它會將已識別的機密文字以佔位符取代（例如 `[REDACTED]`）。  
- **哪個函式庫負責 OCR？** Microsoft Azure OCR 連接器，透過 GroupDocs Redaction 使用。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **我可以對掃描的 PDF 進行遮蔽嗎？** 可以——OCR 會在套用正則表達式遮蔽前提取隱藏文字。  
- **此解決方案僅限 Java 嗎？** 範例基於 Java，但 GroupDocs 亦提供 .NET 等平台的相似 API。  

## 什麼是基於 OCR 的遮蔽？
基於 OCR 的遮蔽會先對每頁執行 OCR，將影像轉換為可搜尋的文字，然後套用正則表達式模式，以 `[REDACTED]` 等遮蔽字元取代匹配項目。這兩步驟流程可可靠地隱藏掃描 PDF 中的個人資料，確保在文件分享或存檔前移除所有敏感字串。

## 為何使用 GroupDocs Redaction 搭配 Azure OCR？
您應該使用 GroupDocs Redaction 搭配 Azure OCR，因為它在印刷文字上提供 **>98 % 的 OCR 正確率**，支援 **超過 50 種輸入與輸出格式**，且能在 **不將整個檔案載入記憶體的情況下處理多百頁的 PDF**，確保合規的快速且可擴展的遮蔽。此解決方案亦 **能在 8 核心伺服器上於 2 分鐘內處理 1,000 頁 PDF**，使批次作業變得實用。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝。  
- **Maven**（若您偏好相依管理）或能手動下載 JAR。  
- **Microsoft Azure OCR 憑證**（端點與訂閱金鑰）。  
- 基本的 Java 知識與正則表達式的熟悉度。  

## 為 Java 設定 GroupDocs Redaction

### Maven 設定
將 GroupDocs 的儲存庫與相依加入您的 `pom.xml`：

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
若您偏好手動管理 JAR，請從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 取得最新版本。

### 取得授權
- **免費試用** – 無償探索所有功能。  
- **臨時授權** – 延長評估時間。  
- **完整授權** – 解鎖生產就緒功能。  

### 基本初始化與設定
`Redactor` 類別是執行 OCR 提取並對 PDF 文件套用遮蔽規則的核心引擎。  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## 如何使用 OCR 遮蔽掩碼敏感資料
使用 OCR 遮蔽掩碼敏感資料的流程包括以 Azure OCR 設定載入 PDF、為欲隱藏的資料定義正則表達式模式，並呼叫 Redactor 以 `[REDACTED]` 等佔位符取代每個匹配項目。此函式庫在單一工作流程中處理 OCR、模式匹配與 PDF 重寫。

### 步驟 1：以 OCR 設定載入文件
`LoadOptions` 設定 GroupDocs 載入檔案的方式，讓您能傳入如 Azure 等 OCR 連接器。  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – 請替換為您的 PDF 路徑。  
- **`settings`** – 包含先前建立的 Azure OCR 連接器。  

### 步驟 2：定義並套用正則表達式遮蔽
`ReplacementOptions` 指定在遮蔽過程中取代每個正則匹配的文字。  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- 模式 `\b\d{3}-\d{2}-\d{4}\b` 可匹配美國社會安全號碼。  
- `ReplacementOptions("[REDACTED]")` 會將每個匹配項目換成遮蔽字元，從而有效 **掩碼敏感資料**。  

## 掩碼敏感資料的常見使用情境
1. **法律文件管理** – 在分享草稿前隱藏客戶識別碼。  
2. **財務報告** – 保護帳號與交易編號。  
3. **醫療紀錄** – 依照 HIPAA 需求遮蔽患者識別資訊。  
4. **政府出版物** – 從公開紀錄中移除個人資料。  
5. **企業合約** – 在外部審查時隱藏專有條款。  

## 效能建議
- **優化正則表達式** – 避免過於寬泛的模式以免增加處理時間；精心設計的表達式可將執行時間縮短最高達 40 %。  
- **記憶體管理** – 盡快關閉 `Redactor` 實例（使用 try‑with‑resources 會自動完成）。  
- **非同步執行** – 大量處理時，將遮蔽工作放在獨立執行緒或使用任務佇列，以保持 UI 響應。  

## 疑難排解
- **Azure 憑證錯誤** – 請再次確認 `MicrosoftAzureOcrConnector` 中的端點 URL 與訂閱金鑰。  
- **文件無法載入** – 檢查檔案路徑，並確保 PDF 未受密碼保護（或透過 `LoadOptions` 提供密碼）。  
- **未套用遮蔽** – 先以簡單字串測試正則表達式；可在單元測試中使用 `Pattern.compile` 以確認匹配。  

## 常見問答

**Q: 什麼是 OCR 遮蔽？**  
A: OCR 遮蔽利用光學字符辨識（Optical Character Recognition）從影像或掃描的 PDF 中提取隱藏文字，然後套用遮蔽規則以掩碼該文字。

**Q: 我可以在不使用 Azure OCR 的情況下使用 GroupDocs Redaction 嗎？**  
A: 可以，但在原生文字提取失敗的掃描文件上，OCR 能顯著提升準確度。

**Q: 如何處理複雜的正則表達式模式？**  
A: 請逐步構建與測試，於沙盒環境使用 Java 的 `Pattern` 類別，確保在套用至大型文件前能正確匹配。

**Q: 典型的效能瓶頸是什麼？**  
A: 大型 PDF、過於複雜的正則表達式，以及同步的 OCR 呼叫都會拖慢處理速度；建議使用批次處理與最佳化的模式。

**Q: 是否提供實作問題的支援？**  
A: 當然——可透過 [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) 尋求社群協助，或直接聯絡 GroupDocs 支援。

## 其他資源
- **文件說明**: https://docs.groupdocs.com/redaction/java/  
- **API 參考**: https://reference.groupdocs.com/redaction/java  
- **下載**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **免費支援**: https://forum.groupdocs.com/c/redaction/33  
- **臨時授權**: https://purchase.groupdocs.com/temporary-license/  

---

**最後更新:** 2026-06-26  
**測試環境:** GroupDocs.Redaction 24.9 (Java)  
**作者:** GroupDocs  

---

## 相關教學

- [使用 OCR 的安全 PDF 遮蔽 – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [如何使用 GroupDocs.Redaction for Java 遮蔽文字](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [在 Java 中掩碼敏感資料 – 使用 GroupDocs.Redaction 遮蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)