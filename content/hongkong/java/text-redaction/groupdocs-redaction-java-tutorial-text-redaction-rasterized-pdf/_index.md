---
date: '2026-08-20'
description: 了解如何使用 GroupDocs.Redaction Java 進行文字遮蔽、儲存為點陣 PDF、取代精確片語，並套用自訂 PDF 設定。
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: 如何使用 GroupDocs.Redaction Java 進行文字遮蔽。本指南示範如何取代精確片語、建立點陣 PDF，以及在幾個步驟內達成
  PDF/A‑1a 相容性。
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: 如何使用 GroupDocs.Redaction Java 函式庫進行文字遮蔽
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: 如何使用 GroupDocs.Redaction Java 進行文字遮蔽
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 進行文字遮蔽

在現代應用程式中，**如何遮蔽文字** 在文件中同時保持工作流程快速且符合規範，是開發人員、稽核員和合規官員常見的挑戰。本教學將指導您使用 GroupDocs.Redaction for Java 來定位精確片語、以安全覆蓋層取代，最後將結果匯出為光柵化的 PDF/A‑1a 文件——非常適合存檔或法律分發。

## 快速答案
- **主要的遮蔽類別是什麼？** `Redactor`  
- **我可以用彩色覆蓋層取代片語嗎？** 是的，使用 `ExactPhraseRedaction` 和 `ReplacementOptions`。  
- **如何產生光柵化的 PDF？** 透過 `SaveOptions.getRasterization().setEnabled(true)` 來啟用光柵化。  
- **範例中使用哪個 PDF 合規等級？** `PdfComplianceLevel.PdfA1a`。  
- **生產環境需要授權嗎？** 需要有效的 GroupDocs.Redaction 授權才能在生產部署中使用。

## 在 Java 中什麼是「如何遮蔽文字」？
`Redaction` 是從檔案中永久移除或遮蔽敏感內容，使其無法在之後被恢復或讀取。使用 GroupDocs.Redaction，您可以以程式方式搜尋精確片語——例如社會安全號碼或機密專案代碼——並以紅色覆蓋層、黑色方框或任何自訂視覺元素取代，確保原始資料無法恢復。

## 為什麼要在 Java 中使用 GroupDocs.Redaction？
GroupDocs.Redaction 支援 **30 多種輸入與輸出格式**（PDF、DOCX、PPTX、XLSX、HTML 以及各種影像類型），且能在不將整個檔案載入記憶體的情況下處理上百頁的文件。其精確片語匹配演算法相較於一般關鍵字搜尋，可將誤報率降低超過 95%，內建的光柵化引擎則讓您產生完全以影像為基礎的 PDF/A‑1a 檔案，以符合長期保存需求。

## 前置條件
開始之前，請確保您已擁有：

- **GroupDocs.Redaction for Java**（v24.9 或更新版本）。  
- **Java Development Kit (JDK) 8+**。  
- 如 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。  
- 用於相依管理的 Maven。  

### 必要的函式庫與相依性
- GroupDocs.Redaction for Java – 將儲存庫與相依性加入您的 `pom.xml`（請參閱 Maven 設定部分）。  
- 可選：您偏好的任何日誌框架（SLF4J、Log4j 等）。

### 知識前置條件
- 基本的 Java 語法與檔案 I/O。  
- 熟悉 Maven 的 `pom.xml` 結構。

## 設定 GroupDocs.Redaction for Java
### Maven 設定
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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
或者，您也可以直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權
- **免費試用** – 在沒有授權金鑰的情況下探索 API。  
- **臨時授權** – 用於延長評估。  
- **完整授權** – 生產環境必須使用。

### 基本初始化與設定
`Redactor` 類別是所有遮蔽操作的入口點。它會載入文件、套用遮蔽規則，並儲存結果。

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## 如何遮蔽文字 – 精確片語範例
`Redactor` 是載入文件並套用遮蔽規則的主要類別。`ExactPhraseRedaction` 定義一個匹配特定字串的規則。此範例示範如何載入檔案、建立 `ExactPhraseRedaction` 規則，並在單一步驟中執行遮蔽，為開發人員提供簡潔的工作流程，同時確保原始內容永久被遮蔽。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## 如何儲存為光柵化 PDF
`SaveOptions` 是控制文件儲存方式的設定物件。啟用其光柵化功能並選擇 PDF/A‑1a 合規性，即可產生僅含影像的 PDF，每頁皆以位圖方式呈現，符合存檔標準且防止文字抽取。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## 實務應用
1. **敏感資料遮蔽** – 在分享合約前自動隱藏個人識別資訊。  
2. **文件存檔** – 將最終報告轉換為光柵化 PDF/A，以符合長期合規需求。  
3. **批次內容更新** – 使用單一腳本在數百個檔案中取代過時的術語。

## 效能考量
- **在每次操作後關閉 `Redactor`**，以釋放檔案句柄與記憶體。  
- **批次處理** – 載入檔案清單並迭代，盡可能重複使用單一 `Redactor` 實例。  
- **監控資源** – 使用 Java 效能分析工具監測大型遮蔽作業期間的 CPU 與堆積使用情況。

## 常見問題

**Q: 如何在 Maven 專案中安裝 GroupDocs.Redaction？**  
A: 如 Maven 設定部分所示，將 GroupDocs 儲存庫與 `groupdocs-redaction` 相依性加入您的 `pom.xml`。

**Q: 我可以使用此函式庫遮蔽 PDF 檔案中的文字嗎？**  
A: 可以，GroupDocs.Redaction 支援 PDF、DOCX、PPTX 以及許多其他格式。

**Q: 若找不到精確片語會發生什麼情況？**  
A: `RedactorChangeLog` 會回傳 `Failed` 狀態。請確認片語的拼寫與大小寫是否正確。

**Q: 如何有效處理非常大的文件？**  
A: 將其分成較小的頁範圍處理，僅在需要時啟用光柵化，且務必關閉 `Redactor` 以釋放資源。

**Q: 能否將光柵化 PDF 只儲存特定頁範圍？**  
A: 完全可以。使用 `options.getRasterization().setPageIndex()` 與 `setPageCount()` 來指定要光柵化的頁面。

## 結論
您現在已擁有一套完整、端到端的 **如何使用 GroupDocs.Redaction Java 進行文字遮蔽** 以及 **儲存為光柵化 PDF** 的指南。遵循這些步驟，您可以保護敏感資訊，符合嚴格的合規標準，並確保 Java 服務在大規模下仍具效能。

**下一步**  
- 透過探索 [official documentation](https://docs.groupdocs.com/redaction/java/) 更深入了解 API。  
- 嘗試其他遮蔽類型，例如 `RegexRedaction` 與 `ImageRedaction`。  
- 加入 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 社群，獲取技巧與最佳實踐。

---

**最後更新：** 2026-08-20  
**測試環境：** GroupDocs.Redaction Java 24.9  
**作者：** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## 相關教學

- [如何使用 GroupDocs.Redaction for Java 遮蔽文字](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)  
- [Java 文字遮蔽教學：使用 GroupDocs.Redaction 的指南](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)