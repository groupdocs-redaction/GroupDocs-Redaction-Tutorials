---
date: '2026-10-01'
description: 了解如何在 Java 中使用 GroupDocs Redaction 移除作者元資料並儲存已遮蔽的文件檔案。
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: 了解如何在 Java 中使用 GroupDocs Redaction 移除作者元資料並儲存已遮蔽的文件檔案。請參考逐步指南。
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: 如何在 Java 中使用 GroupDocs 移除作者元資料
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: 如何在 Java 中使用 GroupDocs 移除作者元資料
type: docs
url: /zh-hant/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 移除作者元資料

在當今的數位環境中，保護文件內隱藏的敏感資訊是必備的做法。**移除作者元資料** 可防止個人或公司識別資訊意外洩漏。本教學將一步步示範如何使用 GroupDocs.Redaction for Java 的 `EraseMetadataRedaction` 來刪除 Word 檔案中的 *Author* 與 *Manager* 等欄位，並且 **安全地儲存已編輯的文件** 副本以供分享或存檔。

## 快速解答
- **EraseMetadataRedaction 的功能是什麼？** 它會從文件中移除選取的元資料欄位。  
- **哪個函式庫提供此功能？** GroupDocs.Redaction for Java。  
- **我需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **我可以一次針對多個欄位嗎？** 可以，使用邏輯 OR 結合過濾條件。  
- **此程序是執行緒安全的嗎？** Redactor 實例不會在執行緒間共享；每次操作請建立新實例。

## EraseMetadataRedaction 是什麼？
`EraseMetadataRedaction` 是內建的編輯類別，可讓您指定要刪除的元資料項目。它適用於 GroupDocs.Redaction 支援的多種文件格式，確保隱藏的作者資訊不會外洩。您可以針對如 Author、Manager 等標準屬性，以及自訂元資料欄位，提供完整的隱私保護。

## 為何在 GroupDocs 中使用 EraseMetadataRedaction？
GroupDocs.Redaction 支援 **超過 100 種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理最多 500 頁的文件。使用此類別可讓您透過單一高效能 API 符合 GDPR、HIPAA 或內部合規需求，同時保持程式碼簡潔。

## 前置條件
- 安裝 Java 8 或更新版本。  
- Maven（或能手動加入 JAR）。  
- GroupDocs.Redaction for Java（版本 24.9 或更新）。  
- 有效的 GroupDocs 試用或永久授權。

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將 GroupDocs 的儲存庫與相依性加入您的 **pom.xml**：

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
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權
從 GroupDocs 入口網站取得免費試用或購買臨時授權。授權檔案須放置於應用程式可載入的位置（例如 classpath 根目錄）。

### 基本初始化與設定
以下是一個最小範例，建立用於 DOCX 檔案的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## 如何在 Java 中使用 EraseMetadataRedaction
以下各節將實作步驟拆解為清晰、可執行的步驟。

### 功能：清除特定元資料項目

#### 概觀
我們將使用 `EraseMetadataRedaction` 刪除 **Author** 與 **Manager** 兩個元資料欄位。這在將內部報告分享給外部合作夥伴時是常見需求。

#### 步驟實作

##### 1️⃣ 初始化 Redactor 物件
`Redactor` 是核心類別，負責載入文件、套用編輯物件並寫入結果。每處理一個檔案請建立新實例：

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ 套用 EraseMetadataRedaction
`MetadataFilters` 提供常見元資料鍵（如 Author、Manager）的預設過濾條件。  
`EraseMetadataRedaction` 會移除符合提供的 `MetadataFilters` 的元資料項目。位元 OR (`|`) 可將 `Author` 與 `Manager` 過濾條件結合，於一次呼叫中刪除兩個欄位：

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ 設定儲存選項
`SaveOptions` 讓您指定輸出檔名、格式及其他儲存參數。  
`SaveOptions` 可控制輸出檔名、格式，以及文件是否要光柵化為 PDF。加入副檔名可保留原始檔案不被改動：

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## 常見使用情境
1. **法律文件** – 在將合約寄給對方律師前，刪除作者資訊。  
2. **公司報告** – 發佈季報給股東時，移除經理姓名。  
3. **專案檔案** – 在存檔或上傳至公共倉庫前，清理內部專案文件。

## 疑難排解技巧
- **找不到檔案** – 確認 `inputFilePath` 所指路徑存在且應用程式具有讀取權限。  
- **缺少元資料欄位** – 並非所有文件類型都儲存相同的元資料鍵；請先在 Office 中檢查文件屬性。  
- **授權錯誤** – 在建立 `Redactor` 實例前，確保授權檔案已正確載入。

## 效能考量
- 盡快關閉 `Redactor` 物件（如 `finally` 區塊所示），以釋放原生資源。  
- 除非需要 PDF 預覽，否則避免將大型文件光柵化；光柵化可能使 300 頁檔案的 CPU 與記憶體使用量增加至原本的 3 倍。

## 常見問與答

**Q1: 什麼是元資料編輯？**  
A1: 元資料編輯是指移除文件的隱藏屬性（如作者、經理或自訂標籤），以防止敏感資訊意外洩漏。

**Q2: 我可以在其他檔案類型上使用 GroupDocs.Redaction 嗎？**  
A2: 可以，函式庫支援 PDF、DOCX、PPTX、XLSX 等超過 100 種格式。

**Q3: 如何處理編輯過程中的錯誤？**  
A3: 將 `apply` 呼叫包在 try‑catch 區塊，並在 finally 子句中始終關閉 `Redactor`，以確保釋放資源。

**Q4: 能否編輯自訂的元資料欄位？**  
A5: 當然可以。使用 `MetadataFilters.Custom("YourFieldName")` 來針對文件中儲存的任何自訂屬性。

**Q5: 使用 GroupDocs.Redaction 的最佳實踐是什麼？**  
A5:  
- 盡早在應用程式中載入授權。  
- 及時關閉 `Redactor` 物件。  
- 使用 `SaveOptions` 加上副檔名，保留原始檔案不變。  
- 在批次處理前，先在文件副本上測試編輯效果。

**Q6: EraseMetadataRedaction 支援批次操作嗎？**  
A6: 您可以遍歷檔案路徑集合，為每個檔案建立新的 `Redactor`，並套用相同的編輯邏輯。

**Q7: 我可以將 EraseMetadataRedaction 與其他編輯類型結合使用嗎？**  
A7: 可以，在儲存之前串接多個編輯物件（例如先文字編輯再進行元資料編輯）。

## 資源
- **文件說明**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-10-01  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學
- [Groupdocs Redaction Java 文件元資料擷取](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)  
- [如何使用 GroupDocs.Redaction 移除 Java 元資料](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)  
- [使用 Groupdocs Redaction Java 取得文件資訊](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)