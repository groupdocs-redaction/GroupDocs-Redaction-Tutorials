---
date: '2026-09-26'
description: 了解如何使用 GroupDocs 在 Java 中遮蔽 metadata，安全地移除機密文件的 metadata，同時保持原始格式不變。
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: 如何使用 GroupDocs 在 Java 中遮蔽 metadata – 一步步指南，教您安全地剝除機密文件的 metadata，並保持原始格式。
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: 如何使用 GroupDocs 在 Java 中遮蔽 metadata
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: 如何使用 GroupDocs 在 Java 中遮蔽 metadata
type: docs
url: /zh-hant/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs 在 Java 中編輯元資料

在本完整教學中，您將學習**如何編輯元資料**，從 Word、PDF 以及其他多種文件類型中使用 GroupDocs.Redaction for Java。完成本指南後，您將能將元資料編輯功能嵌入任何基於 Java 的服務，確保公司名稱、作者或自訂屬性等機密資訊不會離開您的組織。

## 快速解答
- **MetadataSearchRedaction 的功能是什麼？** 它會搜尋特定的元資料欄位，並將其值替換為自訂文字。  
- **需要哪個函式庫？** GroupDocs.Redaction for Java (v24.9 or newer)。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需要完整授權。  
- **我可以保留原始檔案格式嗎？** 可以—使用 `SaveOptions` 以保留原始格式。  
- **此方法是執行緒安全的嗎？** 每個 `Redactor` 實例彼此獨立，您可以平行處理文件。

## 如何使用 GroupDocs 編輯元資料？
`Redactor` 是載入文件並提供編輯操作的核心類別。  
使用 `Redactor` 實例載入來源文件，設定針對欲清除之特定元資料鍵的 `MetadataSearchRedaction`，套用編輯，最後使用 `SaveOptions` 儲存檔案。整個工作流程只需少量程式碼，且支援所有支援的格式，從 DOCX 到 PDF 甚至其他格式。

## 什麼是使用 GroupDocs 的元資料編輯？
`MetadataSearchRedaction` 是一個專門的類別，可讓您針對特定的元資料屬性（例如 *Company*、*Author*）並以佔位符取代其內容。當您需要在與外部合作夥伴共享文件前匿名化公司資料時，這非常理想。編輯過程不會改變文件的其他元素，確保在移除元資料後，視覺版面與內容保持完整。

## 為什麼要使用 GroupDocs 進行元資料編輯？
使用 GroupDocs 進行元資料編輯提供了一種可靠的方式，從文件中剔除敏感資訊，同時保留其原始外觀與結構。透過僅針對元資料欄位，您能快速符合隱私標準，而不必修改可見內容或冒著意外資料外洩的風險。

- **Precision** – 精確性 – 只編輯您指定的欄位，其他文件內容保持不變。  
- **Compliance** – 合規性 – 透過移除隱藏識別子，協助符合 GDPR、HIPAA 及其他隱私法規。  
- **Automation‑ready** – 自動化就緒 – 可無縫整合至批次處理管線或微服務。  
- **Broad format support** – 廣泛格式支援 – GroupDocs.Redaction 支援 **50+ 輸入與輸出格式**（包括 DOCX、PDF、PPTX、XLSX 及影像類型），且能在不將整個文件載入記憶體的情況下處理數百頁的檔案。

## 前置條件
- **GroupDocs.Redaction for Java** ≥ 24.9。  
- Java 8 或更新版本已安裝於您的機器上。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE（可選，但建議使用）。  
- 基本熟悉 Maven（或能手動加入 JAR）。

## 設定 GroupDocs.Redaction for Java

將儲存庫與相依性加入您的 `pom.xml`。此步驟可確保 Maven 能自動下載此函式庫。

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

*或者，您也可以直接從官方發佈頁面下載 JAR：*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 取得授權
- **Free trial** – 下載試用授權以探索全部功能。  
- **Temporary license** – 用於延長測試。  
- **Full license** – 正式部署時必須的完整授權。

## 基本初始化
`Redactor` 載入文件並提供套用各種編輯的方法。  
建立指向您欲處理文件的 `Redactor` 實例。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

### 步驟 1：匯入必要的類別
這些匯入讓您能使用編輯引擎、儲存選項與元資料工具。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 步驟 2：初始化 Redactor
使用來源檔案的路徑建立 `Redactor` 實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 步驟 3：設定元資料搜尋與編輯
建立一個 `MetadataSearchRedaction`，搜尋精確字串 **"Company Ltd."** 並以 **"--company--"** 取代。`setFilter` 呼叫僅將操作限制於 *Company* 元資料欄位。

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### 步驟 4：套用編輯
對已開啟的文件執行編輯。

```java
redactor.apply(redaction);
```

### 步驟 5：使用自訂選項儲存
`SaveOptions` 允許您為編輯後的文件指定輸出格式、檔名及其他儲存參數。設定 `SaveOptions` 使編輯後的檔案在保留原始格式的同時，加上 “_Redacted” 後綴。

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 步驟 6：釋放資源
務必關閉 `Redactor` 以釋放原生資源，避免記憶體洩漏。

```java
finally {
    redactor.close();
}
```

## 常見問題與解決方案
- **FileNotFoundException** – 檢查傳遞給 `Redactor` 的路徑是否正確。建議使用絕對路徑或 `Paths.get(...)` 以提升可靠性。  
- **No changes observed** – 確認您目標的元資料欄位確實包含搜尋字串；預設情況下元資料區分大小寫。  
- **Out‑of‑memory errors on large files** – 將文件分成較小批次處理，並在每個檔案處理完畢後立即呼叫 `redactor.close()`。

## 實務應用
1. **Legal documentation** – 在將合約寄給第三方前，移除客戶公司名稱。  
2. **Financial reporting** – 在審計檔案中匿名化內部識別碼。  
3. **Collaborative projects** – 在與外部供應商共享草稿時保護專有資訊。

## 效能考量
- **Memory management** – 此函式庫會將整個文件載入記憶體；每個檔案處理完畢後關閉 `Redactor` 為必要步驟。  
- **Batch processing** – 在高量情境下，遍歷檔案集合並重複使用單一 `SaveOptions` 實例。  
- **Stay updated** – 新版本會帶來效能調整與錯誤修正，請始終使用最新的穩定版。

## 常見問答

**Q: GroupDocs.Redaction for Java 是什麼？**  
A: 它是一個功能強大的函式庫，讓您能在 Java 應用程式中編輯文件的文字、元資料與影像。

**Q: 我可以在未購買授權的情況下使用 GroupDocs.Redaction 嗎？**  
A: 可以，但會有限制。免費試用或臨時授權可在測試目的下完整使用。

**Q: 我如何確保在編輯過程中文件格式得以保留？**  
A: 使用 `SaveOptions` 指定需求，例如在儲存為 PDF 時避免光柵化。

**Q: 使用 GroupDocs.Redaction 可以編輯哪些類型的文件？**  
A: 支援多種格式，包括 Word、Excel、PowerPoint、PDF 等等。

**Q: 若遇到問題，我可以在哪裡取得支援？**  
A: 請前往 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 取得協助。

**Q: MetadataSearchRedaction 能處理加密文件嗎？**  
A: 可以。使用接受密碼參數的 `Redactor` 建構子，載入帶有相應密碼的文件。

**Q: 我可以在一次執行中串接多個元資料編輯嗎？**  
A: 當然可以。建立多個 `MetadataSearchRedaction` 物件，設定不同的過濾條件，並在儲存前依序套用。

**Q: 是否可以在儲存前預覽編輯結果？**  
A: 您可以呼叫 `redactor.getRedactions()` 取得待編輯列表，並以程式方式檢查。

## 其他資源
- **Documentation**：在 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) 探索詳細指南。  
- **API reference**：在 [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) 查看完整 API 參考。  
- **Download library**：從 [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) 取得最新發佈版。  
- **Source code**：在 [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) 查看並貢獻程式碼。  
- **Support**：透過 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 的免費支援渠道取得協助。

---

**最後更新：** 2026-09-26  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學

- [Groupdocs Redaction Java 文件元資料提取](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [replace metadata text java – 使用 GroupDocs 的安全編輯](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [使用 Groupdocs Redaction Java 取得文件資訊](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)