---
date: '2026-08-09'
description: 了解如何使用 GroupDocs.Redaction for Java 透過 redacting text 與 rasterizing PDFs
  來建立 non editable PDF 檔案。
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: 使用 GroupDocs.Redaction for Java 透過 redacting text 與 rasterizing PDFs
  建立 non editable PDF 檔案。遵循一步一步的指南，了解提示、常見問題與注意事項。
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: 使用 GroupDocs.Redaction Java 建立 non editable PDF
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: 如何使用 GroupDocs.Redaction Java 建立 non editable PDF
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 建立不可編輯的 PDF

在許多受管制的行業中，您必須提供無法被修改或複製的文件。最可靠的保證方式是先對敏感文字進行遮蔽，然後將整份文件光柵化，以**建立不可編輯的 PDF**檔案。GroupDocs.Redaction for Java 提供單行 API 來執行這兩個步驟，讓您在不自行開發 PDF 引擎的情況下滿足合規需求。

## 快速解答
- **什麼是「redact text」？** 它會永久移除或遮蔽敏感字串，使其無法被閱讀或復原。  
- **哪個函式庫負責此工作？** GroupDocs.Redaction for Java 提供內建的遮蔽與光柵化功能。  
- **我需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **我能在一步完成將 DOCX 轉換為光柵化 PDF 嗎？** 可以 — 先套用遮蔽，然後使用啟用光柵化的 `SaveOptions`。  
- **輸出真的不可編輯嗎？** 光柵化的 PDF 以影像形式呈現，防止文字擷取或修改。

## 什麼是文字遮蔽？
文字遮蔽會永久移除或隱蔽機密資訊——例如個人識別碼、財務資料或法律條款——自文件中。與簡單的尋找取代不同，遮蔽保證隱藏的內容無法被任何工具復原。透過刪除原始字元並可選擇以佔位符取代，遮蔽確保敏感資料不可恢復，且文件仍可供授權使用者閱讀。

## 為何使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction for Java 提供完整的功能集，簡化安全文件處理。它支援多種檔案格式、提供多種遮蔽類型，並內建一鍵光柵化以鎖定 PDF。此函式庫針對效能進行最佳化，可在 Windows 與 Linux 上執行，且能輕鬆整合至現有的 Java 應用程式，成為需要大規模保護敏感資訊的企業的可靠選擇。

## 前置條件
- Java Development Kit (JDK 11 或更新版本) 以及如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- GroupDocs.Redaction 函式庫（版本 24.9 或更新）。  
- 基本的 Java 知識——您只需撰寫少量簡短程式碼片段。

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將 GroupDocs 儲存庫與相依性加入您的 `pom.xml`：

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
如果您不使用 Maven，也可以從官方發佈頁面取得 JAR 檔案：[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### 取得授權
- **Free trial** – 免費試用 API。  
- **Temporary license** – 適合長時間測試。  
- **Full license** – 正式部署時必須取得完整授權。

## 基本初始化
`Redactor` 是 GroupDocs.Redaction 的核心類別，用於在記憶體中載入與修改文件。匯入命名空間後，以來源檔案路徑建立 `Redactor` 實例，即可套用遮蔽規則。

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

## 如何在 Java 中建立不可編輯的 PDF？
載入來源文件，套用所需的遮蔽規則，然後以啟用光柵化的方式儲存結果。這個三步流程——載入、遮蔽、光柵化——會產生無法編輯、複製或搜尋的 PDF，符合最嚴格的合規標準。透過將每頁轉換為影像，最終檔案會移除任何可能被之後擷取的隱藏文字層。

## 如何在 Java 中遮蔽文字
以下示範精確片語遮蔽，適合移除已知的識別字串，例如個人姓名。此流程包括匯入必要類別、定義遮蔽規則，並在儲存前套用至文件。

### 步驟 1：匯入所需類別
`ExactPhraseRedaction` 是針對字面字串的遮蔽規則。`ReplacementOptions` 用於告訴引擎在原始文字位置插入何種佔位符。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 步驟 2：套用精確片語遮蔽
以下程式碼會將所有 **“John Doe”** 出現的地方替換為佔位符 **[personal]**：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**為什麼這樣有效：**  
- `ExactPhraseRedaction` 針對字面字串 “John Doe”。  
- `ReplacementOptions` 告訴引擎在原始文字位置插入什麼內容。

**技巧與常見陷阱**  
- 再次確認文件路徑；錯誤的路徑會拋出 `FileNotFoundException`。  
- 確保 Java 程序對輸出資料夾具有寫入權限。

## 如何儲存為光柵化 PDF
遮蔽完成後，您可能需要一個不可編輯的 PDF。光柵化會將每頁轉換為影像，移除選取或編輯文字的功能。此步驟確保最終 PDF 像掃描文件一樣，能抵抗文字擷取工具與意外修改。

### 步驟 1：匯入 `SaveOptions`
`SaveOptions` 用於設定文件的儲存方式，包括光柵化與檔名選項。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### 步驟 2：設定並儲存光柵化 PDF
以下程式碼會停用自動的 “_redacted” 後綴，啟用光柵化，並寫入輸出檔案。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**說明：**  
- `setAddSuffix(false)` 保留原始檔名（若需要可啟用以加入 “_redacted” 後綴）。  
- `setRasterizeToPDF(true)` 告訴 GroupDocs 將每頁渲染為 PDF 內的影像，確保文件 **不可編輯**。

**故障排除**  
- 若光柵化失敗，請確認 Java 執行環境已包含 PDF 渲染相依性（已隨函式庫捆綁）。

## 實務應用
1. **Legal document processing** – 在與對方律師共享前遮蔽客戶姓名。  
2. **HR record management** – 在內部報告中隱藏員工編號。  
3. **Financial reporting** – 在分發審計摘要時保護帳號。  

您可以將這些步驟串接成自動化工作流程，將 GroupDocs.Redaction 與文件管理系統或雲端儲存桶結合。

## 效能考量
- **Batch processing:** 在處理大量檔案時重複使用單一 `Redactor` 實例，可降低高達 40 % 的開銷。  
- **Memory management:** 對於大型文件，在每次 `redactor.close()` 後呼叫 `System.gc()`，或在獨立的 JVM 中執行流程。  
- **Keep dependencies updated:** 新版通常包含 PDF 光柵化的效能調整，於多核心系統上可提升約 20 % 的速度。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| *找不到檔案* | 確認絕對路徑，並確保檔案在伺服器上存在。 |
| *權限被拒* | 以足夠的作業系統權限執行 JVM，或變更輸出資料夾的 ACL。 |
| *光柵化產生空白頁面* | 確認來源文件不是已經是光柵圖像；使用最新版本的函式庫。 |
| *遮蔽後仍留隱藏文字* | 使用 `ExactPhraseRedaction` 搭配 `ReplacementOptions`；避免使用簡單的尋找取代方法。 |

## 常見問答

**Q: 什麼是精確片語遮蔽？**  
A: 它會將特定字串（例如姓名）替換為佔位符，確保原始文字無法復原。

**Q: 為何光柵化 PDF 能提升安全性？**  
A: 光柵化的 PDF 會將每頁渲染為影像，防止文字選取、複製或編輯。

**Q: 我能一次處理多個檔案嗎？**  
A: 可以 — 迭代檔案路徑清單，對每個文件重複使用相同的 `Redactor` 設定。

**Q: 能否整合雲端服務？**  
A: 當然可以。您可以從 AWS S3、Azure Blob 或 Google Cloud Storage 讀寫串流，直接傳遞給 API。

**Q: 新手常見的陷阱是什麼？**  
A: 忘記關閉 `Redactor`（會鎖定檔案）以及使用缺乏光柵化支援的舊版函式庫。

## 資源
- **Documentation:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-08-09  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

---

## 相關教學

- [如何使用 GroupDocs.Redaction Java 建立灰階 PDF – 安全與最佳化您的文件](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [精通 Java 文件安全：精確片語遮蔽與進階光柵化（使用 GroupDocs.Redaction）](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [如何將 DOCX 轉換為影像並使用 GroupDocs Redaction Java 遮蔽 Word 文件](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)