---
date: '2026-07-01'
description: 了解如何在 Java 中使用 GroupDocs.Redaction 對 PDF 與 PowerPoint 檔案進行遮蔽。提供 PDF 遮蔽
  Java、PPT 遮蔽以及批次處理的逐步指南。
keywords:
- how to redact pdf
- pdf redaction java
- how to redact ppt
- redact confidential data
- batch pdf redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  headline: How to Redact PDF and PPT Text with GroupDocs for Java
  type: TechArticle
- description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  name: How to Redact PDF and PPT Text with GroupDocs for Java
  steps:
  - name: Configure Replacement Options
    text: '- **Text Redaction** – replace the matched word with a placeholder such
      as “█”. - **Image Redaction** – overlay a solid red rectangle on image areas
      to obscure visual data.'
  - name: Apply Redactions
    text: '`PageAreaRedaction` is an operation that applies redaction to specified
      page areas. Run the `PageAreaRedaction` operation to perform both text and image
      redactions in one pass:'
  - name: Cleanup Resources
    text: 'Always close the `Redactor` to free native resources and avoid memory leaks:'
  type: HowTo
- questions:
  - answer: Redaction permanently removes the data from the file structure, while
      hiding only changes the visual layer.
    question: What is the difference between pdf text redaction and simply hiding
      text?
  - answer: Yes – provide the password when constructing the `Redactor` instance.
    question: Can I use GroupDocs.Redaction to redact password‑protected PDFs?
  - answer: Use `redactor.save("output.pdf")` to a temporary location and open the
      file for review.
    question: Is there a way to preview redaction results before saving?
  - answer: Absolutely – the same API works across 20+ supported document types.
    question: Does the library support other formats like DOCX or XLSX?
  - answer: Visit the community forum at [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I get help if I run into problems?
  type: FAQPage
title: 如何使用 GroupDocs for Java 對 PDF 與 PPT 文字進行遮蔽
type: docs
url: /zh-hant/java/pdf-specific-redaction/groupdocs-redaction-java-pdf-ppt-redaction-guide/
weight: 1
---

# 如何使用 GroupDocs for Java 對 PDF 與 PPT 文字進行遮蔽

在當今快速變化的數位世界中，**如何遮蔽 PDF** 檔案是保護機密資料的必備步驟。無論您在處理法律合約、財務報表，或是公司 PowerPoint 簡報，都需要可靠的方法在分享前隱藏敏感資訊。本教學將帶您使用 **GroupDocs.Redaction for Java** 於 PDF 與 PPT 檔案的最後一頁或投影片上遮蔽文字與影像，並說明如何將此流程擴展至批次作業。

## 快速解答
- **什麼是 PDF 文字遮蔽？** 它會永久移除或遮蔽機密文字與影像，使其無法被恢復。  
- **哪個 Java 函式庫支援此功能？** GroupDocs.Redaction for Java 提供統一的 API，支援 PDF、PPT、DOCX、XLSX 等多種格式。  
- **我需要授權嗎？** 免費試用可用於評估；正式使用則需購買完整授權。  
- **我可以使用相同程式碼同時遮蔽 PDF 與 PPT 嗎？** 可以——相同的 `Redactor` 類別可處理兩種格式。  
- **需要哪個 Java 版本？** JDK 8 或更高版本。

## 什麼是 PDF 文字遮蔽？
**PDF 文字遮蔽會永久刪除或隱蔽 PDF 文件中選取的內容，使其無法被恢復或檢視。** 與單純隱藏不同，遮蔽會將資料從檔案結構中移除，確保符合 GDPR、HIPAA 等隱私法規。

## 為何使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支援 **20 多種輸入與輸出格式**，包括 PDF、PPT、DOCX、XLSX 以及常見影像類型，且能在不將整個檔案載入記憶體的情況下處理數百頁的文件。API 提供細緻的區域控制、內建正規表達式引擎以自動偵測片語，並具備執行緒安全設計，可在多核心伺服器上擴展至批次作業。

## 前置條件
- **GroupDocs.Redaction for Java**（可透過 Maven 或直接下載取得）。  
- **JDK 8+** 已安裝並在開發機上配置。  
- **Maven**（或能手動將 JAR 加入 classpath 的方式）。  
- 基本熟悉 Java I/O 與正規表達式。

## 設定 GroupDocs.Redaction for Java
### Maven 設定
將 GroupDocs 的儲存庫與相依性加入您的 `pom.xml` 中：

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
如果您不想使用 Maven，可從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權
- **Free Trial** – 無償探索核心功能。  
- **Temporary License** – 延長測試期限超過試用期。  
- **Full License** – 商業部署必須取得完整授權。

### 基本初始化
`Redactor` 是代表文件並提供所有遮蔽操作的核心類別。建立指向欲處理文件的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;
// Initialize the Redactor object
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/YOUR_FILE.pdf");
```

## 實作指南
### 如何使用 GroupDocs.Redaction 於 Java 中遮蔽 PDF 文件？
載入 PDF、定義正規表達式模式、設定取代選項，並在單一流暢的工作流程中套用遮蔽。此方法可讓您在最後一頁的右半部遮蔽文字，並在偵測到的影像上覆蓋實心矩形。

#### 步驟 1：載入文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF");
```

#### 步驟 2：定義文字匹配的正規表達式模式
```java
// Compile regex pattern to match specific text
java.util.regex.Pattern rx = java.util.regex.Pattern.compile("urna");
```

#### 步驟 3：設定取代選項
- **Text Redaction** – 將匹配的字詞替換為如 “█” 的佔位符。  
- **Image Redaction** – 在影像區域覆蓋實心紅色矩形，以隱蔽視覺資料。

```java
ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
optionsText.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1), // Target the last page
    new PageAreaFilter(new java.awt.Point(300, 0), new java.awt.Dimension(300, 840)) // Right half of the page
});
```

```java
RegionReplacementOptions optionsImg = new RegionReplacementOptions(java.awt.Color.RED, new java.awt.Dimension(100, 100));
```

#### 步驟 4：套用遮蔽
`PageAreaRedaction` 是對指定頁面區域套用遮蔽的操作。  
執行 `PageAreaRedaction` 可在一次處理中同時執行文字與影像的遮蔽：

```java
RedactorChangeLog result = redactor.apply(new PageAreaRedaction(rx, optionsText, optionsImg));

if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/output.pdf");
}
```

#### 步驟 5：清理資源
始終關閉 `Redactor` 以釋放原生資源並避免記憶體洩漏：

```java
finally {
    redactor.close();
}
```

### 如何使用相同方法遮蔽 PPT 投影片？
工作流程與 PDF 步驟相同，僅檔案副檔名不同。載入 PPTX、套用相同的正規表達式與區域過濾，最後儲存已遮蔽的簡報。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PPT");
```

## 實務應用
- **Legal Document Preparation** – 在向法院提交前遮蔽客戶姓名、案件編號或機密條款。  
- **Financial Reporting** – 隱藏 PDF 與投影片中的帳號、利潤率或專有公式。  
- **HR Audits** – 從大量文件匯出中移除員工識別資訊，以符合隱私法規。

## 效能考量
- **Close resources promptly** – 及時關閉資源以降低記憶體使用，特別是在處理大量批次時。  
- **Optimize regex patterns** – 避免使用過於寬泛的表達式，導致不必要的全文件掃描。  
- **Batch processing** – 使用執行緒池，並在每個檔案上重複使用單一 `Redactor` 實例，以提升多核心伺服器的吞吐量。

## 常見問題與解決方案
如 `PageRangeFilter` 與 `PageAreaFilter` 等過濾器可將遮蔽限制於特定頁面或區域。

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| *未套用遮蔽* | 過濾器指向錯誤的頁面/區域 | 確認 `PageRangeFilter` 與 `PageAreaFilter` 的座標。 |
| *記憶體不足錯誤* | 大型檔案保持開啟 | 逐一處理檔案或增加 JVM 堆疊大小 (`-Xmx`)。 |
| *正規表達式匹配到不需要的文字* | 模式過於寬泛 | 調整正規表達式或使用字界 (`\b`)。 |

## 常見問答

**Q: PDF 文字遮蔽與單純隱藏文字有何不同？**  
A: 遮蔽會永久從檔案結構中移除資料，而隱藏僅改變視覺層。

**Q: 我可以使用 GroupDocs.Redaction 來遮蔽受密碼保護的 PDF 嗎？**  
A: 可以——在建立 `Redactor` 實例時提供密碼。

**Q: 有沒有方法在儲存前預覽遮蔽結果？**  
A: 使用 `redactor.save("output.pdf")` 儲存至暫存位置，然後開啟檔案檢視。

**Q: 此函式庫是否支援其他格式，如 DOCX 或 XLSX？**  
A: 當然支援——相同的 API 可用於 20 多種支援的文件類型。

**Q: 若遇到問題，我該向何處尋求協助？**  
A: 前往社群論壇 [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) 取得協助。

---

**最後更新:** 2026-07-01  
**測試環境:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Redaction 在 Java 中遮蔽文字：完整指南](/redaction/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/)
- [如何在 Java 中遮蔽 PDF – 針對 PDF 的遮蔽教學](/redaction/java/pdf-specific-redaction/)
- [遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 隱蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)