---
date: '2026-08-20'
description: 了解如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字，涵蓋 exact‑phrase、regex、color
  replacement、annotation 及 metadata redaction，以確保合規安全。
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: 了解如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字，涵蓋 exact‑phrase、regex、color
  replacement、annotation 及 metadata redaction。
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: 如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: 如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字
type: docs
url: /zh-hant/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# 如何在 Java 文件中使用 GroupDocs.Redaction 進行文字遮蔽

在現代應用程式中，**如何遮蔽文字**於 PDF、Word 檔或影像是合規與隱私的常見需求。無論您需要隱藏個人識別資訊、移除機密註解，或剝除中繼資料，GroupDocs.Redaction for Java 都提供乾淨且程式化的方式來實現 **java document security**。本教學將逐步說明所有必要步驟——從設定函式庫到套用精確片語、正規表達式、顏色式、註解與中繼資料遮蔽——讓您能將遮蔽功能直接嵌入後端服務。

## 快速解答
- **什麼函式庫處理 Java 文件遮蔽？** GroupDocs.Redaction for Java.  
- **我可以用顏色取代文字而不是刪除嗎？** 可以，使用「replace text with color」功能。  
- **生產環境需要授權嗎？** 需要臨時或付費授權才能使用完整功能。  
- **支援哪個 Java 版本？** JDK 8 或以上。  
- **唯一的加入函式庫方式是 Maven 嗎？** 建議使用 Maven，但也可以手動下載 JAR。

## 什麼是 Java 中的「文字遮蔽」？
**遮蔽會永久移除或隱蔽敏感內容，使其無法復原。** 在 Java 中，您載入檔案、定義要隱藏的內容、套用遮蔽，並儲存已清理的版本。這確保任何後續使用者只能看到已清理的文件。

## 為何使用 GroupDocs.Redaction for Java？
載入檔案、定義規則，SDK 會處理繁重的工作。GroupDocs.Redaction 支援 **30+ 格式**——包括 DOCX、PDF、PPTX、XLSX、PNG、JPEG、BMP——並透過串流架構處理大型文件。它提供精確片語、正規表達式、顏色式、註解與中繼資料遮蔽，讓您能細緻控制，以符合 GDPR、HIPAA 及其他法規。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝於您的機器上。  
- **Maven** 用於相依管理（或您可以手動下載 JAR）。

### 必要的函式庫與相依性
將 GroupDocs 儲存庫與 Redaction 相依性加入您的 `pom.xml`：

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

您也可以從官方發行頁面下載最新的 JAR：[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 授權取得
生產環境使用時，請取得臨時或完整授權。可提供免費試用以供評估。

## 設定 GroupDocs.Redaction for Java
1. **新增 Maven 相依**（或加入 JAR）。  
2. **設定授權**，在應用程式啟動時呼叫 `License.setLicense("path/to/license.lic")`。`License` 為載入與套用 GroupDocs Redaction 授權檔的類別。  
3. **建立指向來源文件的 `Redactor` 實例**。

**`Redactor` 類別是核心引擎，以記憶體效能的方式載入、修改並儲存文件。** 取得 `Redactor` 物件後，您可以在寫入結果前串接多個遮蔽規則。

現在您已準備好開始遮蔽。

## 實作指南

### 精確片語遮蔽
以佔位文字取代特定片語（例如某人的姓名）。

#### 精確片語遮蔽如何運作？
`ExactPhraseRedaction` 代表一項會移除或取代特定精確文字字串的規則。載入文件，建立針對該精確字串的 `ExactPhraseRedaction` 規則，套用規則，並儲存輸出。SDK 會自動將符合的文字塗白，同時保留版面配置。

1. **以欲處理的文件初始化 Redactor**：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **定義精確片語規則** 並套用：

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **將遮蔽後的檔案儲存**至輸出資料夾：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表達式遮蔽與文字取代
使用正規表達式定位序號等模式，並以通用代碼取代。

#### 正規表達式遮蔽搭配取代如何運作？
`RegexRedaction` 定義一項基於正規表達式的規則，用於尋找並修改符合的文字。您提供包含模式與取代字串的 `RegexRedaction` 物件。引擎掃描文件，替換每個符合項目，並保留周圍格式。

1. 載入文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 建立正規表達式規則並套用：

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. 儲存結果：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表達式遮蔽與顏色取代
您可以 **以顏色取代文字**，在不刪除文字的情況下視覺上遮蔽，同時保留底層字元。

#### 顏色式遮蔽與刪除有何不同？
SDK 會以選定的顏色塗抹符合的文字，使其對肉眼不可讀，但仍保留於檔案串流中。當您需要保留文件結構以供後續處理時，此方式相當有用。

1. 載入文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 定義正規表達式模式並設定取代顏色（例如藍色）：

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. 儲存更新後的檔案：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 刪除註解遮蔽
移除文件中所有註解（評論、標記等），以獲得更乾淨的最終版本。

#### 如何一次移除所有註解？
`AnnotationRedaction` 為移除註解（如評論、標記、印章）的規則。建立針對所有註解類型的 `AnnotationRedaction` 規則，套用後持久化變更。

1. 載入您的檔案：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 套用註解刪除規則：

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. 持久化變更：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### 擦除中繼資料遮蔽
移除所有中繼資料（作者、建立日期、自訂屬性），以保護隱私並符合合規標準。

#### 中繼資料擦除如何保證隱私？
`MetadataRedaction` 會清除文件內建與自訂的中繼資料欄位。此規則會抹除所有內建與自訂的中繼資料，確保檔案屬性中不留任何隱藏識別資訊。

1. 開啟文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 套用中繼資料擦除規則：

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. 儲存已清理的文件：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## 實務應用（為何重要）
- **法律文件準備** – 在與對方律師分享草稿前遮蔽客戶姓名。  
- **醫療合規** – 移除患者識別資訊，以符合 HIPAA 規範，免除手動編輯。  
- **企業資料保護** – 在內部報告發佈前隱藏財務數字或商業機密。

自動化這些步驟可減少人工工作、消除人為錯誤，並確保成千上萬檔案的一致合規。

## 效能考量
- **使用串流而非一次載入** – 對於大型檔案，使用接受 `InputStream` 的 `Redactor` 建構子，以避免將整個文件載入記憶體。  
- **預先編譯正規表達式**，在重複執行相同遮蔽時可降低最高 30% 的 CPU 負載。  
- **監控 JVM 堆積** – 遮蔽可能消耗大量記憶體；對於多 GB 檔案的批次處理，考慮將堆積大小調整為 (`-Xmx2g`)。

## 常見問題與故障排除
| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `apply` 後未見變更 | 文件路徑錯誤或檔案被鎖定 | 確認文件路徑並確保文件未在其他地方開啟 |
| 正規表達式未匹配 | 模式語法錯誤 | 使用線上測試工具測試正規表達式；正確轉義反斜線 |
| 顏色取代未顯示 | 輸出格式不支援文字顏色（例如純文字） | 使用保留樣式的格式，如 DOCX 或 PDF |
| 執行時授權錯誤 | 授權檔缺失或無效 | 將 `.lic` 檔放在可存取的目錄，並在使用任何 Redactor 前呼叫 `License.setLicense` |

## 常見問答

**Q: 我可以在一次執行中結合多個遮蔽規則嗎？**  
A: 可以。建立每個遮蔽物件，分別呼叫 `redactor.apply()`，最後一次儲存。

**Q: GroupDocs.Redaction 支援受密碼保護的檔案嗎？**  
A: 當然支援。將密碼傳入接受 `LoadOptions` 物件的 `Redactor` 建構子。

**Q: 可以在儲存前預覽遮蔽效果嗎？**  
A: 您可以呼叫 `redactor.preview()` 產生暫時檢視，突顯將被遮蔽的區域。

**Q: 支援哪些檔案格式？**  
A: DOCX、PDF、PPTX、XLSX、PNG、JPEG、BMP 等等——總計超過 30 種格式。

**Q: 如何確保遮蔽文件符合 GDPR？**  
A: 使用中繼資料擦除功能，移除註解，並對所有個人資料欄位套用精確片語或正規表達式遮蔽。

## 結論
現在您已擁有使用 GroupDocs.Redaction 在 Java 文件中 **遮蔽文字** 的完整端對端指南。依循精確片語、正規表達式、顏色式、註解與中繼資料遮蔽的步驟，即可實現強大的 **java document security**，同時保持程式碼簡潔易維護。將這些程式碼片段整合至現有服務，自動化批次處理，並遵守隱私法規。

---

**Last Updated:** 2026-08-20  
**Tested with:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## 相關教學

- [replace metadata text java – 使用 GroupDocs 的安全遮蔽](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [如何使用 GroupDocs.Redaction for Java 在 Word 文件中遮蔽影像 – 完整指南](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [如何使用檔案路徑的 GroupDocs Redaction Java 授權遮蔽文件 – 步驟指南](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)