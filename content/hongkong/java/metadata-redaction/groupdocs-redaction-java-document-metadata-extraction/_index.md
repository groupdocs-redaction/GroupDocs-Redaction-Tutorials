---
date: '2026-09-21'
description: 了解如何使用 GroupDocs.Redaction 取得 Java 檔案類型並讀取 Java 檔案中繼資料。有效率地擷取頁數、檔案大小，並處理資料流。
keywords:
- get file type java
- read file metadata java
- java get page count
- read file size java
- metadata extraction java
lastmod: '2026-09-21'
og_description: 快速使用 GroupDocs.Redaction 取得 Java 檔案類型並讀取 Java 檔案中繼資料。本指南說明如何擷取頁數、大小等資訊。
og_image_alt: Guide to extracting file type and metadata in Java with GroupDocs.Redaction
og_title: 取得 Java 檔案類型並使用 GroupDocs.Redaction 讀取中繼資料
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to get file type java and read file metadata java using GroupDocs.Redaction.
    Extract page count, file size, and process streams efficiently.
  headline: Get file type java and read metadata with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to get file type java and read file metadata java using GroupDocs.Redaction.
    Extract page count, file size, and process streams efficiently.
  name: Get file type java and read metadata with GroupDocs.Redaction
  steps:
  - name: open a file stream
    text: Start by creating an `InputStream` for the target document. Using a buffered
      stream improves I/O performance for large files.
  - name: initialize the Redactor
    text: Create a `Redactor` instance using the stream. This object gives you access
      to the document’s metadata.
  - name: retrieve document information
    text: '**`IDocumentInfo` provides properties such as file type, page count, size,
      and custom metadata.** > **Pro tip:** Uncomment the `System.out.println` lines
      only when you need console output; keeping them commented in production reduces
      I/O overhead.'
  - name: close resources
    text: Always close the `Redactor` and the stream in a `finally` block (as shown)
      to avoid memory leaks, especially when processing many documents in parallel.
  type: HowTo
- questions:
  - answer: Primarily for redacting sensitive content, it also provides robust APIs
      to **java read document properties** such as file type and page count.
    question: What is GroupDocs.Redaction used for?
  - answer: Yes, the library works seamlessly with Spring, Jakarta EE, and plain Java
      SE projects.
    question: Can I use GroupDocs.Redaction with other Java frameworks?
  - answer: Wrap the file stream in a `BufferedInputStream`, close resources promptly,
      and process files in a streaming fashion rather than loading the entire document
      into memory.
    question: How do I handle very large documents efficiently?
  - answer: Absolutely—GroupDocs.Redaction handles multiple languages and character
      sets out of the box.
    question: Does the library support non‑English documents?
  - answer: Missing licenses, incorrect file paths, and forgetting to close streams
      are the most common. Always follow the resource‑cleanup pattern shown above.
    question: What are typical pitfalls when extracting metadata?
  type: FAQPage
tags:
- get file type
- GroupDocs.Redaction
- Java metadata extraction
- document processing
- Java file handling
title: 取得 Java 檔案類型並使用 GroupDocs.Redaction 讀取中繼資料
type: docs
url: /zh-hant/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# 使用 GroupDocs.Redaction 取得檔案類型（java）並讀取中繼資料

## 快速解答
- **如何在 Java 中取得文件的檔案類型？** 呼叫 `redactor.getDocumentInfo().getFileType()`。  
- **哪個函式庫可以提取中繼資料且同時支援遮蔽？** GroupDocs.Redaction for Java 在單一 API 中提供兩項功能。  
- **開發時需要授權嗎？** 免費試用可用於評估；正式上線需購買永久授權。  
- **我也能取得頁數嗎？** 可以——在 `IDocumentInfo` 物件上使用 `getPageCount()`。  
- **此方法是否相容於 Java 8 以上？** 完全相容——GroupDocs.Redaction 支援 Java 8 及更新版本。

## 「get file type java」是什麼？為何重要？
`getFileType()` 會回傳一個易讀的列舉，指出文件的確切格式（例如 PDF、DOCX、XLSX）。了解精確的類型可讓應用程式自動將檔案導向適當的處理流程、依格式套用安全政策、產生正確的縮圖，並在使用者介面清單中呈現正確資訊給最終使用者。

## 為何使用 GroupDocs.Redaction 讀取 Java 文件屬性？
GroupDocs.Redaction 是一個 **全功能解決方案**，可在單一、支援串流的 API 中處理遮蔽、中繼資料提取與格式轉換。它支援 **45+ 種輸入與輸出格式**，能在不將整份文件載入記憶體的情況下處理數百頁的檔案，且在關閉 `Redactor` 實例時會自動釋放資源。

## 前置條件
- GroupDocs.Redaction for Java（版本 24.9 或更新）。  
- JDK 8 或更新版本。  
- 具備基本的 Java 知識並熟悉檔案 I/O 串流。  

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
在 `pom.xml` 中加入儲存庫與相依性：

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
或者，直接從 [GroupDocs.Redaction for Java 版本發佈](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權
- **免費試用：** 適合評估 API。  
- **臨時授權：** 官方網站提供短期測試使用。  
- **正式授權：** 準備上線時購買。  

## 基本初始化（Java）

**`Redactor` 是核心類別，用於開啟文件串流並提供中繼資料、遮蔽與轉換功能。**  

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## 逐步指南：取得中繼資料

### 步驟 1：開啟檔案串流
首先為目標文件建立 `InputStream`。使用緩衝串流可提升大型檔案的 I/O 效能。

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### 步驟 2：初始化 Redactor
使用該串流建立 `Redactor` 實例。此物件可讓您存取文件的中繼資料。

```java
final Redactor redactor = new Redactor(stream);
```

### 步驟 3：取得文件資訊
**`IDocumentInfo` 提供檔案類型、頁數、大小與自訂中繼資料等屬性。**  

```java
try {
    IDocumentInfo info = redactor.getDocumentInfo();
    
    // Display document information (uncomment as needed)
    System.out.println("\
File type: " + info.getFileType() +
           "\
Number of pages: " + info.getPageCount() + 
           "\
Document size: " + info.getSize() + " bytes");
} finally {
    redactor.close();
    stream.close();
}
```

> **專業提示：** 只有在需要在主控台輸出時才取消註解 `System.out.println` 行；在正式環境保持註解可減少 I/O 開銷。

### 步驟 4：關閉資源
務必在 `finally` 區塊中關閉 `Redactor` 與串流（如範例所示），以避免記憶體洩漏，特別是在平行處理大量文件時。

## 實務應用（java 讀取文件屬性）

1. **文件管理系統：** 依類型、頁數與大小自動目錄化檔案。  
2. **資料分析管線：** 將中繼資料輸入儀表板以供報表使用。  
3. **內容創作平台：** 在下載或預覽前向最終使用者顯示檔案細節。  

## 效能考量
- 對大型檔案使用 **緩衝串流**（`BufferedInputStream`）以提升 I/O 速度。  
- 即時釋放資源（對 `Redactor` 與串流皆呼叫 `close()`）。  
- 批次處理時，可考慮每個執行緒重複使用單一 `Redactor` 實例，以減少物件建立開銷。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `FileNotFoundException` | 路徑不正確或檔案遺失 | 核對絕對/相對路徑與檔案權限。 |
| `LicenseException` | 未載入有效授權 | 在建立 `Redactor` 前載入試用或正式授權。 |
| `OutOfMemoryError`（大型 PDF） | 未使用緩衝串流或同時處理過多檔案 | 改用 `BufferedInputStream` 並限制同時執行的執行緒數量。 |

## 常見問答

**Q: GroupDocs.Redaction 的用途是什麼？**  
A: 主要用於遮蔽敏感內容，同時也提供強大的 API 讓 **java 讀取文件屬性**，例如檔案類型與頁數。

**Q: 我可以在其他 Java 框架中使用 GroupDocs.Redaction 嗎？**  
A: 可以，該函式庫可無縫搭配 Spring、Jakarta EE 以及純 Java SE 專案使用。

**Q: 如何有效處理非常大的文件？**  
A: 將檔案串流包裹在 `BufferedInputStream`，即時關閉資源，並以串流方式處理檔案，而非一次載入整份文件至記憶體。

**Q: 函式庫是否支援非英文文件？**  
A: 完全支援——GroupDocs.Redaction 內建處理多種語言與字元集。

**Q: 提取中繼資料時常見的陷阱是什麼？**  
A: 常見問題包括缺少授權、路徑錯誤以及忘記關閉串流。請務必遵循上述資源清理模式。

## 結論
您現在已掌握完整、可投入生產的 **get file type java**、讀取其他文件屬性以及 **java get page count** 的範例，皆透過 GroupDocs.Redaction 實作。將這些程式碼片段整合至現有服務，即可即時掌握系統中每份文件的資訊。

**後續步驟**  
- 探索 `IDocumentInfo` 所提供的其他欄位。  
- 將中繼資料提取與遮蔽工作流程結合，實現端到端的文件安全。  
- 研究高流量環境的批次處理模式。

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/java/)  
- [API 參考](https://reference.groupdocs.com/redaction/java)  
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權資訊](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-09-21  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學

- [使用 Groupdocs Redaction Java 取得文件資訊](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)
- [產生預覽與文件頁數 – GroupDocs Java](/redaction/java/document-information/)
- [如何使用 GroupDocs.Redaction 在 Java 中遮蔽中繼資料](/redaction/java/metadata-redaction/)