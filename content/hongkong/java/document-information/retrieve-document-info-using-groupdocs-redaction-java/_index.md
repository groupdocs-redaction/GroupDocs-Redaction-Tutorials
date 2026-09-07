---
date: '2026-09-06'
description: 了解如何在 Java 中取得 file extension、檢索 document size、page count 以及 PDF metadata，使用
  GroupDocs.Redaction for Java。立即提升您的 Java 應用程式的文件處理能力。
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: 探索如何在 Java 中取得 file extension、document size、page count 以及 PDF metadata，使用
  GroupDocs.Redaction for Java。簡易程式碼，快速結果。
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: 如何在 Java 中使用 GroupDocs.Redaction 取得 file extension
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: 如何在 Java 中使用 GroupDocs.Redaction 取得 file extension
type: docs
url: /zh-hant/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction 取得 Java 檔案副檔名

在處理使用者上傳檔案的現代 Java 應用程式中，提前了解檔案的正確類型——**java get file extension**——對於路由、安全性與資源規劃都相當重要。本教學將示範如何使用 GroupDocs.Redaction 套件取得檔案副檔名、文件大小、頁數，甚至讀取 PDF 中的中繼資料。完成後，你只需一次低記憶體呼叫，即可取得所有關鍵屬性。

## 快速回答
- **哪個方法會回傳檔案類型？** `IDocumentInfo.getFileType()`
- **如何取得頁數？** `IDocumentInfo.getPageCount()`
- **哪個呼叫會回傳檔案大小（位元組）？** `IDocumentInfo.getSize()`
- **執行範例是否需要授權？** 評估時使用試用或臨時授權即可。
- **需要哪個 Java 版本？** Java 8 或以上。

## 什麼是「java get file extension」？
**java get file extension** 指的是在 Java 中以程式方式從文件中抽取檔案格式（例如 DOCX、PDF）。GroupDocs.Redaction 透過 `IDocumentInfo` 介面提供此資訊，只要呼叫一次方法即可取得副檔名字串。

## 為什麼使用 GroupDocs.Redaction 來擷取中繼資料？
GroupDocs.Redaction 能從 **50+** 種輸入格式（包括 PDF、DOCX、XLSX、PPTX 以及各種影像類型）讀取中繼資料，且不需將整個檔案載入記憶體。它在一般伺服器上能於 200 ms 內處理 300 頁的 PDF，RAM 使用量低於 20 MB。這種效能優化的做法讓你在批次工作中保持高擴充性，同時在所有支援格式上取得一致結果。

## 前置條件
- 已安裝 Java 8 或更新版本。
- 支援 Maven 的 IDE（IntelliJ IDEA、Eclipse 等）。
- 取得 GroupDocs.Redaction 授權（免費試用或臨時授權）。

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將以下儲存庫與相依性加入 `pom.xml` 檔案：

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
或是從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

#### 取得授權
- **免費試用：** 先使用免費試用版評估套件。  
- **臨時授權：** 取得臨時授權以延長評估時間。  
- **購買：** 若符合需求，可考慮正式購買。

## 為什麼「java get file extension」在實務專案中很重要
在檔案上傳瞬間即判斷其類型，可將檔案導向正確的處理管線——PDF 交給遮蔽、Word 檔交給轉換、影像交給 OCR。此舉亦能執行安全檢查（阻擋可執行檔），並在文件管理系統中顯示正確的 UI 圖示。

## 如何同時取得檔案副檔名、文件大小與頁數（Java）
只要一次呼叫 `IDocumentInfo` 即可取得檔案類型、大小與頁數。此呼叫僅讀取文件標頭，即使是大型檔案也能快速完成且佔用最小記憶體。此輕量化方式非常適合在批次處理前先取得摘要資訊，再決定後續動作。`IDocumentInfo` 介面會提供檔案類型、頁數與大小等中繼資料，且不會載入完整文件。

### 步驟 1：匯入必要類別
在 Java 檔案的最上方加入所需的匯入語句：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### 步驟 2：初始化 Redactor
`Redactor` 類別是核心引擎，負責開啟文件並提供中繼資料存取。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### 步驟 3：取得並顯示文件資訊
`IDocumentInfo` 提供你需要的中繼資料。先呼叫一次 `getDocumentInfo()`，再查詢三個屬性。

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

上述三行 `System.out.println` 會分別輸出檔案類型、頁數與位元組大小——正是下游處理所需的資料。

## 如何取得 PDF 中繼資料（Java）
使用 `Redactor` 載入 PDF 後呼叫 `getDocumentInfo()`。同一方法會回傳 PDF 專屬欄位，如版本與加密狀態，無需額外程式碼。回傳的 `IDocumentInfo` 物件同時包含 PDF 版本號、加密旗標以及標準中繼資料（作者、標題、建立日期），你可直接透過 getter 取得，並在顯示或記錄時使用。

## 常見使用情境
1. **文件管理系統：** 在儲存前依檔案類型或大小自動分類。  
2. **內容處理管線：** 依頁數選擇不同策略（例如大量 PDF 進行批次遮蔽，小型 Word 檔直接轉換）。  
3. **數位資產庫：** 在不開啟檔案的情況下快速顯示文件屬性預覽。

## 常見問題與解決方案
- **找不到檔案：** 請確認傳入 `Redactor` 的絕對或相對路徑正確。  
- **不支援的格式：** 確認檔案副檔名屬於 GroupDocs.Redaction 支援的 50+ 種格式之一。  
- **授權錯誤：** 使用有效的試用或正式授權，否則 API 會拋出授權例外。

## 疑難排解技巧（讀取文件中繼資料 Java）
- 將中繼資料呼叫包在 `try‑catch` 區塊，以優雅處理損毀檔案。  
- 若可用，使用 `redactor.isEncrypted()` 先偵測 PDF 是否加密，再讀取中繼資料。  
- 處理大量檔案時，重複使用執行緒池，並及時關閉每個 `Redactor` 實例，以防止檔案句柄洩漏。

## 效能考量
大量批次處理時：

- 使用 `try‑with‑resources` 區塊開啟每個文件，確保檔案句柄及時釋放。  
- 僅快取所需的中繼資料，除非必要，否則不要載入完整文件內容。

## 常見問答
**Q: 什麼是 GroupDocs.Redaction？**  
A: GroupDocs.Redaction 是一套 Java 函式庫，提供遮蔽、 中繼資料擷取 與跨 50 多種檔案類型的格式無關文件處理功能。

**Q: 能否從 PDF 取得中繼資料？**  
A: 能，`IDocumentInfo` 會回傳 PDF 版本、加密狀態以及基本中繼資料，無需額外程式碼。

**Q: 取得文件資訊時如何處理例外？**  
A: 將 `getDocumentInfo()` 包在 `try‑catch` 區塊，捕捉 `RedactionException` 以處理損毀或不支援的檔案。

**Q: 可以取得哪些文件資訊？**  
A: 檔案類型、頁數、位元組大小、PDF 版本、加密旗標，以及基本的作者/建立日期等中繼資料。

**Q: 是否支援高效能的批次處理？**  
A: 支援。可在執行緒池內為每個檔案建立獨立 `Redactor`，並重複使用同一 JVM 以達到高吞吐量。

## 結論
現在你已掌握如何 **java get file extension**、**get document size java**、**get page count java**，以及 **retrieve pdf metadata java**，全部透過 GroupDocs.Redaction 完成。將這些程式碼片段整合至你的 Java 應用程式，即可更智慧地處理文件、提升效能，並提供更豐富的使用者體驗。

---

**最後更新：** 2026-09-06  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

**資源**  
- **文件說明：** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載：** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub：** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援：** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權：** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 相關教學

- [java read file metadata – file type with GroupDocs.Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Generate Preview & Document Page Count – GroupDocs Java](/redaction/java/document-information/)
- [How to Preview Page with GroupDocs.Redaction for Java – A Comprehensive Guide](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)