---
date: '2026-06-11'
description: 了解如何使用 GroupDocs.Redaction for .NET 從文件流中提取元資料，涵蓋設定、程式碼範例與實際應用。
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction .NET 從文件流中提取元資料
type: docs
url: /zh-hant/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 從文件流中提取元資料

您是否厭倦了手動提取文件資訊或處理會拖慢工作流程的大檔案？**快速提取元資料**是一項常見挑戰，而 GroupDocs.Redaction .NET 函式庫提供了一種快速且記憶體效率高的方式，直接從串流中取得文件詳細資訊。在本教學中，您將學習如何設定函式庫、從串流中取得檔案類型、頁數與大小，並為後續處理準備輸出資料夾。

## 快速解答
- **「提取元資料」是什麼意思？** 它指的是在不將整個文件載入記憶體的情況下，讀取檔案類型、頁數與大小等屬性。  
- **哪個函式庫負責此功能？** GroupDocs.Redaction for .NET 提供原生 API 以基於串流的方式提取元資料。  
- **我需要授權嗎？** 免費試用可用於開發；正式環境需購買商業授權。  
- **我能處理大於 1 GB 的 PDF 嗎？** 可以——使用串流可處理高達 2 GB 的檔案，而無需載入整個檔案。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5 以上，以及 .NET 6 以上。

## 什麼是從串流提取元資料？
從串流提取元資料是直接從 `Stream` 物件讀取文件屬性的過程，避免完整載入檔案，從而節省記憶體與 CPU 時間。此技術非常適合資源受限的批次處理或雲端服務。

## 為何使用 GroupDocs.Redaction 進行元資料提取？
GroupDocs.Redaction 支援 **30 多種檔案格式**（包括 PDF、DOCX、XLSX、PPTX 以及各類影像），且可處理高達 **2 GB** 的文件，同時將記憶體使用量控制在 **50 MB** 以下。其 `Redactor` API 只需一次呼叫即可取得所有關鍵文件資訊，免除使用多個解析器的需求。

## 前置條件

- **GroupDocs.Redaction for .NET**（最新版本）  
- **.NET Framework** 4.5+ **或** **.NET Core/5+/6+**  
- 基本的 C# 知識與檔案 I/O 的熟悉度  
- Visual Studio 2019 或更新版本  

## 如何設定 GroupDocs.Redaction for .NET？
要開始使用 GroupDocs.Redaction，您首先需要將函式庫加入專案中。可透過 .NET CLI、Visual Studio 套件管理員或 NuGet UI 完成。選擇最符合工作流程的方式；CLI 適合腳本化建置，而 UI 則提供圖形化的版本與相依性瀏覽。

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- 在 Visual Studio 中開啟 NuGet 套件管理員。  
- 搜尋 **"GroupDocs.Redaction"** 並安裝最新版本。

### 取得授權步驟
1. **免費試用：** 下載試用授權以無限制探索所有功能。  
2. **臨時授權：** 從 [GroupDocs](https://purchase.groupdocs.com/temporary-license/) 申請臨時授權，以進行延長測試。  
3. **購買：** 生產環境就緒時，購買商業授權。  

欲取得更多資訊，請造訪 [GroupDocs 網站](https://purchase.groupdocs.com/temporary-license/)。

### 基本初始化與設定
`Redactor` 類別是所有操作的入口點，包括元資料提取。

`Redactor` 是代表文件實例的核心類別，提供遮蔽、資訊取得與檔案操作等方法。安裝完成後，您可以如以下示範建立 `Redactor` 物件：

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

函式庫已就緒，現在讓我們深入實作細節。

## 如何從文件串流提取元資料？
將文件以 **唯讀串流** 載入，初始化 `Redactor`，並呼叫 `GetDocumentInfo()` 以單一步驟取得元資料。此方法避免將整個檔案載入記憶體，對於大型 PDF 或數百頁的 Office 文件尤為重要。

**直接答案：** 使用 `File.OpenRead()` 開啟檔案，將串流傳入 `new Redactor(stream)`，然後呼叫 `redactor.GetDocumentInfo()`——此方法僅需三行程式碼即可回傳包含檔案類型、頁數與大小的物件。

### 步驟 1：準備來源檔案路徑
首先，確保來源檔案存在且輸出資料夾已備妥。以下輔助方法會檢查輸出目錄，若不存在則建立。

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*為什麼？* 這可確保後續檔案操作的路徑有效，避免 `DirectoryNotFoundException`。

### 步驟 2：開啟文件串流
使用 `File.OpenRead()` 以 **唯讀串流** 開啟檔案，即使是千兆位元組大小的檔案也能保持低記憶體使用量。

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*為什麼？* 串流支援即時處理，讓您只處理檔案的部分，而非整個文件。

### 步驟 3：以文件串流初始化 Redactor
`Redactor` 是主要的 API 物件，讓您存取文件層級的操作，包括元資料提取。

`Redactor` 代表從串流載入的單一文件，並提供如 `GetDocumentInfo()` 等方法以快速取得屬性。

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*為什麼？* 使用串流實例化 `Redactor` 可將物件與底層檔案關聯，而不需完整載入。

### 步驟 4：取得文件元資料
呼叫 `GetDocumentInfo()` 會回傳 `DocumentInfo` 物件，內含檔案格式、頁數與檔案大小。

`GetDocumentInfo()` 在單一次呼叫中提取核心屬性（格式、頁數、大小），免除使用獨立解析器的需求。

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*為什麼？* 此步驟彙總所有關鍵元資料，讓您能輕鬆記錄、篩選或依特徵路由文件。

## 如何為處理後的檔案準備輸出目錄？
在寫入任何處理後的檔案之前，請確保目標資料夾已存在且具寫入權限。透過程式檢查路徑並在缺失時建立，可避免常見的執行時例外，如 `DirectoryNotFoundException` 或權限錯誤。此簡單步驟亦使程式碼在本機、伺服器或容器等環境中具可移植性。

**直接答案：** 使用 `Directory.Exists()` 檢查資料夾是否存在，若不存在則使用 `Directory.CreateDirectory()` 建立——此單行檢查可在任何寫入操作前保證路徑有效。

### 實作輔助方法
以下方法封裝了檢查與建立的邏輯，回傳驗證過的路徑供後續使用。

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*為什麼？* 集中此邏輯可減少重複，讓程式碼基礎更易維護。

## 常見問題與解決方案
- **權限錯誤：** 確保應用程式以具有目標資料夾寫入權限的帳戶執行。  
- **無效路徑：** 仔細檢查路徑分隔符（Windows 為 `\\`，Linux/macOS 為 `/`），以避免 `DirectoryNotFoundException`。  
- **大型檔案處理：** 及時釋放串流（使用 `using` 陳述式），以釋放 OS 句柄並防止洩漏。

## 實務應用
1. **自動文件匯入：** 上傳時提取元資料，並將其存入資料庫以供快速搜尋與合規報告。  
2. **法律與合規稽核：** 抽取頁數與檔案類型，以驗證文件在歸檔前符合規範標準。  
3. **企業內容管理：** 利用元資料自動將檔案分類至資料夾，提升組織與檢索速度。

## 效能考量
- **記憶體管理：** 總是將串流包在 `using` 區塊中，以自動釋放。  
- **批次處理：** 將文件分成 10‑20 個一組處理，以平衡吞吐量與記憶體使用，特別是在資源受限的伺服器上。  
- **平行處理：** 使用 `Parallel.ForEach` 處理獨立檔案，但需監控 CPU 與 I/O，避免資源爭用。

## 結論
您現在已擁有一份完整、可投入生產的指南，說明如何使用 GroupDocs.Redaction for .NET **提取文件串流的元資料**。依循上述步驟，即可高效取得檔案類型、頁數與大小，同時保持低記憶體使用，優雅地處理大型檔案。

**下一步**
- 檢視完整的 API 參考文件於 [documentation](https://docs.groupdocs.com/redaction/net/)。  
- 深入探索 [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) 以了解遮蔽、浮水印與 OCR 功能。  
- 嘗試不同檔案格式（PDF、DOCX、XLSX），觀察元資料在各類型間的差異。  
- 將提取的元資料整合至現有的文件管理或搜尋解決方案中。

## 常見問答

**Q: GroupDocs.Redaction 的元資料提取主要使用情境是什麼？**  
A: 它能快速且記憶體效率高地取得文件屬性，用於索引、合規檢查與自動路由，無需開啟完整檔案。

**Q: 我能從受密碼保護的檔案提取元資料嗎？**  
A: 可以，於建立 `Redactor` 物件時提供密碼，API 會在內部解密串流。

**Q: 此函式庫是否支援非 PDF 格式，如 DOCX 或 XLSX？**  
A: 當然支援——GroupDocs.Redaction 處理超過 30 種格式，包括 PDF、DOCX、XLSX、PPTX 以及常見影像類型。

**Q: 使用串流能處理多大的文件？**  
A: 串流可處理高達 **2 GB** 的檔案，且記憶體消耗保持在 **50 MB** 以下，得益於即時讀取。

**Q: 若遇到問題，我該向哪裡尋求協助？**  
A: 前往 [GroupDocs 論壇](https://forum.groupdocs.com/c/redaction/33) 取得社群支援，或參考官方文件中的故障排除指南。

**最後更新：** 2026-06-11  
**測試環境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs  

**資源**  
- **文件：** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 參考：** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載：** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## 相關教學

- [使用 GroupDocs.Redaction .NET API 完成文件元資料檢索](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [使用 GroupDocs.Redaction for .NET 進行文件元資料遮蔽的完整指南](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [在 .NET 中使用串流進行安全文件遮蔽：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)