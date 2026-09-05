---
date: '2026-08-31'
description: 學習如何使用 GroupDocs.Redaction for Java redact PDF，建立 redaction policies，移除
  annotations，並以程式化、合規的方式擦除 metadata。
keywords:
- how to redact pdf
- erase metadata pdf
- remove annotations java
- GroupDocs.Redaction Java
- document redaction
lastmod: '2026-08-31'
og_description: 如何使用 GroupDocs.Redaction for Java redact PDF。建立 policies，移除 annotations，並快速且安全地擦除
  metadata。
og_image_alt: Guide showing how to redact PDF files with GroupDocs.Redaction in Java
og_title: 如何使用 GroupDocs.Redaction for Java redact PDF
schemas:
- author: GroupDocs
  dateModified: '2026-08-31'
  description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  headline: How to redact PDF with GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  name: How to redact PDF with GroupDocs.Redaction for Java
  steps:
  - name: configure redactions
    text: 'Configure the redactions using different classes provided by GroupDocs.Redaction:'
  - name: save redaction policy
    text: 'Save the configured policy as an XML file:'
  - name: create exact phrase redaction
    text: 'Implement an exact phrase redaction:'
  - name: create regex redaction
    text: 'Define a regex‑based redaction:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that programmatically removes or
      replaces sensitive content in PDFs and other document formats.
    question: What is GroupDocs.Redaction?
  - answer: Add the Maven dependency, obtain a trial license, and follow the initialization
      steps shown above.
    question: How do I get started with GroupDocs.Redaction?
  - answer: Yes—use exact‑phrase redactions, regular‑expression redactions, or the
      built‑in metadata removal classes.
    question: Can I customize redaction patterns in GroupDocs.Redaction?
  - answer: Absolutely—save your `RedactionPolicy` as an XML file and load it later
      for batch processing.
    question: Is it possible to save and reuse redaction configurations?
  - answer: Apply only required redactions, tune Java heap size, and craft efficient
      regex patterns to minimise CPU usage.
    question: What are the best practices for optimizing performance with GroupDocs.Redaction?
  type: FAQPage
tags:
- redact PDF
- GroupDocs.Redaction
- Java document processing
- erase metadata pdf
- remove annotations java
title: 如何使用 GroupDocs.Redaction for Java redact PDF
type: docs
url: /zh-hant/java/advanced-redaction/master-redaction-groupdocs-java-guide/
weight: 1
---

# 如何使用 GroupDocs.Redaction for Java 對 PDF 進行遮蔽

在當今以數據為驅動的世界中，保護 PDF 檔案內的機密資訊是不可妥協的需求。本教學示範 **如何遮蔽 PDF** 文件，涵蓋政策建立、註解移除以及中繼資料刪除。完成後您將擁有可重複使用的 XML 遮蔽政策，可套用於任意數量的 PDF，協助您遵循 GDPR、HIPAA 及其他法規。

## 快速回答
- **GroupDocs.Redaction 的主要目的為何？** 以程式方式遮蔽 PDF 及其他文件格式中的敏感內容。  
- **我可以使用 Java 移除註解嗎？** 是—使用 `DeleteAnnotationRedaction` 類別 (remove annotations java)。  
- **開發時需要授權嗎？** 免費試用或臨時授權可用於測試；正式環境需購買正式授權。  
- **支援哪個 Java 版本？** JDK 8 或更新版本。  
- **XML 政策檔案放在哪裡？** 您在程式碼中定義輸出路徑，並呼叫 `policy.save(...)`。  

`DeleteAnnotationRedaction` 類別會移除 PDF 中的註解物件，例如評論、標記或印章。  
`RedactionPolicy` 類別代表一組遮蔽規則，可儲存至或從 XML 檔案載入。  

## 什麼是遮蔽政策，以及如何建立遮蔽政策？
遮蔽政策是一組基於 XML 的規則，告訴 GroupDocs.Redaction 在 PDF 中要隱藏、刪除或取代哪些文字、模式、註解或中繼資料。只要定義一次並儲存為 XML 檔案，即可在多個 PDF 上套用相同的 **遮蔽敏感資訊**，無需重寫程式碼。  

## 為何使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 使用 **記憶體效能高的引擎** 處理 PDF，能在使用低於 150 MB 記憶體的情況下處理超過 500 頁的檔案。它支援 **30 多種輸入與輸出格式**，包括 DOCX、XLSX、PPTX、HTML 以及常見影像類型，並內建 GDPR 與 HIPAA 的合規功能。此函式庫亦提供對精確字串、正規表達式、註解與中繼資料遮蔽的細緻控制，是 Java 開發者最具彈性的解決方案。  

## 前置條件
- **函式庫與相依性** – 透過 Maven 將 GroupDocs.Redaction 加入專案，或直接下載 JAR。  
- **Java 環境** – 已安裝並設定 JDK 8 或更新版本。  
- **基礎知識** – 熟悉 Java 語法與正規表達式可加速政策建立。  

## 設定 GroupDocs.Redaction for Java

### 安裝資訊
**Maven:**  
若要使用 Maven 整合 GroupDocs.Redaction，請將以下內容加入 `pom.xml`：

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

**Direct download:**  
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。  

### 取得授權
先使用免費試用或取得臨時授權以探索全部功能。長期使用則需購買正式授權。

**Basic initialization:**  
在專案中初始化 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;

public class RedactionSetup {
    public static void main(String[] args) {
        // Initialize the Redactor object with your document path
        try (Redactor redactor = new Redactor("path/to/your/document.pdf")) {
            // Perform operations here
        }
    }
}
```

## 實作指南

### 如何建立遮蔽政策：建立並儲存遮蔽政策
載入遮蔽設定，加入所需的遮蔽物件，並將政策持久化為 XML 檔案。此兩步驟流程讓您可在多個 PDF 中重複使用相同規則，而無需每次重新建立政策。

#### 概觀
此功能允許您設定多種遮蔽類型，如精確字串、正規表達式與中繼資料刪除，之後可將這些設定儲存為 XML 檔案以供日後使用。

##### 步驟 1：設定遮蔽
使用 GroupDocs.Redaction 提供的不同類別設定遮蔽：

```java
import com.groupdocs.redaction.RedactionPolicy;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Configure redactions
RedactionPolicy policy = new RedactionPolicy(new Redaction[] {
    // Exact Phrase Redaction replaces "Redaction" with "[Product]"
    new ExactPhraseRedaction("Redaction", new ReplacementOptions("[Product]")),
    
    // Regex Redaction searches for specific patterns and replaces them with a blue rectangle
    new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(Color.BLUE)),
    
    // Delete Annotation Redaction removes all annotations
    new DeleteAnnotationRedaction(),
    
    // Erase Metadata Redaction deletes all metadata
    new EraseMetadataRedaction(MetadataFilters.All)
});
```

##### 步驟 2：儲存遮蔽政策
將設定好的政策儲存為 XML 檔案：

```java
// Define your output directory path
String outputPath = YOUR_DOCUMENT_DIRECTORY + "YOUR_OUTPUT_DIRECTORY/POLICY_SAVE.xml";
policy.save(outputPath);
```

### 如何使用 Java 移除註解：設定精確字串遮蔽
載入 PDF，定義要隱藏的精確字串，並將遮蔽加入政策。該字串將被黑框或自訂文字取代。

#### 概觀
此功能針對特定字串進行遮蔽，並以預先定義的文字取代。

##### 步驟 1：建立精確字串遮蔽
實作精確字串遮蔽：

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;

// Configure the redaction for a specific phrase
Redaction exactPhraseRedaction = new ExactPhraseRedaction(
    "Redaction", // Phrase to be redacted
    new ReplacementOptions("[Product]") // Replacement text
);
```

### 如何使用 Java 移除註解：設定正規表達式遮蔽
使用正規表達式定位如社會安全號碼或信用卡格式等模式，然後自動取代或刪除。

#### 概觀
使用正規表達式辨識並取代文件中的模式。

##### 步驟 1：建立正規表達式遮蔽
定義基於正規表達式的遮蔽：

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Implement regex redaction for pattern matching
Redaction regexRedaction = new RegexRedaction(
    "\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", // Pattern to match
    new ReplacementOptions(Color.BLUE) // Replace matches with blue rectangle
);
```

## 實務應用
1. **機密文件管理** – 自動 **遮蔽敏感資訊**，如姓名、社會安全號碼或財務資料，適用於法律與人力資源文件。  
2. **合規自動化** – 透過剔除客戶通訊中的個人識別資訊，以符合 GDPR、HIPAA 及其他法規要求。  
3. **測試資料匿名化** – 使用正規表達式遮蔽，匿名化測試資料集，同時保留文件結構。  

## 效能考量
- **最佳化遮蔽** – 僅套用必要的遮蔽，以降低處理時間。  
- **記憶體管理** – 監控 Java 堆積使用量；GroupDocs.Redaction 以串流方式處理頁面，避免一次載入整個檔案。  
- **有效的正規表達式** – 撰寫簡潔的正規表達式，避免過度回溯與 CPU 負載。  

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| 未套用遮蔽 | 字串錯誤或大小寫敏感 | 使用不分大小寫的選項或確認精確文字字串 |
| 註解仍然存在 | 未將 `DeleteAnnotationRedaction` 加入政策 | 在政策陣列中加入 `new DeleteAnnotationRedaction()` |
| 大型 PDF 處理緩慢 | 不必要的正規表達式掃描 | 限制正規表達式範圍或在套用模式前先過濾頁面 |

## 常見問答

**Q: 什麼是 GroupDocs.Redaction？**  
A: GroupDocs.Redaction 是一個 Java 函式庫，可程式化地移除或取代 PDF 及其他文件格式中的敏感內容。  

**Q: 如何開始使用 GroupDocs.Redaction？**  
A: 加入 Maven 相依性，取得試用授權，並依照上述初始化步驟操作。  

**Q: 我可以自訂 GroupDocs.Redaction 的遮蔽模式嗎？**  
A: 可以——使用精確字串遮蔽、正規表達式遮蔽，或內建的中繼資料移除類別。  

**Q: 能否儲存並重複使用遮蔽設定？**  
A: 完全可以——將 `RedactionPolicy` 儲存為 XML 檔案，之後再載入以進行批次處理。  

**Q: 使用 GroupDocs.Redaction 時，最佳的效能優化做法是什麼？**  
A: 僅套用必要的遮蔽、調整 Java 堆積大小，並撰寫高效的正規表達式以降低 CPU 使用率。  

## 資源
- [文件說明](https://docs.groupdocs.com/redaction/java/)
- [API 參考](https://reference.groupdocs.com/redaction/java)
- [下載](https://releases.groupdocs.com/redaction/java/)
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-08-31  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

## 相關教學

- [如何使用 GroupDocs.Redaction Java 移除註解](/redaction/java/annotation-redaction/)
- [如何使用 GroupDocs.Redaction Java 遮蔽中繼資料](/redaction/java/metadata-redaction/)
- [如何使用 Java 遮蔽 PDF – 針對 PDF 的遮蔽教學](/redaction/java/pdf-specific-redaction/)