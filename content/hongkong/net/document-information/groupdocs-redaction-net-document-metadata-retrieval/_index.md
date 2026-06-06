---
date: '2026-06-06'
description: 了解如何使用 GroupDocs.Redaction .NET 取得元資料並提取文件元資料，從而實現強大的文件管理與合規性。
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction .NET API 取得元資料
type: docs
url: /zh-hant/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 取得元資料

在當今的數位時代，**如何取得元資料**是任何以文件為中心的應用程式的基本步驟。無論您是需要讀取檔案元資料以進行合規審核、提取文件屬性以建立索引，或僅在使用者介面中顯示文件大小，GroupDocs.Redaction .NET 都提供簡潔的 API，讓您只需幾行 C# 程式碼即可完成。本教學將帶您完整了解整個流程，從環境設定到顯示取得的資訊，讓您立即開始提取文件元資料。

## 快速解答
- **取得元資料的主要方法是什麼？** 在 `Redactor` 實例上呼叫 `Redactor.GetDocumentInfo()`。  
- **支援哪些格式？** 支援超過 50 種輸入與輸出格式，包括 PDF、DOCX、XLSX、PPTX 以及影像類型。  
- **開發時需要授權嗎？** 測試可使用免費試用授權；正式上線則需完整授權。  
- **可以處理大型檔案嗎？** 可以——GroupDocs.Redaction 能在不將整個檔案載入記憶體的情況下處理數百頁的文件。  
- **是否支援非同步？** 可將 API 包裝成非同步模式，以保持 UI 執行緒的回應性。

## 在 GroupDocs.Redaction 中什麼是元資料擷取？
元資料擷取是透過函式庫的 API 取得文件內建屬性（例如檔案類型、頁數與大小）的過程。透過提取這些屬性，開發人員可以以程式方式評估文件特性、支援索引、執行合規規則，並對後續處理步驟作出明智的決策。

## 如何取得文件元資料？
`Redactor` 類別是載入與檢查 GroupDocs.Redaction 中文件的主要介面。  
`GetDocumentInfo()` 是一個會回傳包含文件元資料的 `DocumentInfo` 物件的方法。  

使用 `new Redactor("path/to/file")` 載入檔案，然後呼叫 `GetDocumentInfo()`——此呼叫會回傳一個包含類型、頁數、大小及其他屬性的 `DocumentInfo` 物件。此兩步驟方法適用於任何支援的格式，且不需額外設定。之後您可以讀取 `FileType`、`PageCount`、`FileSize` 等欄位，以顯示或記錄相關資訊。

## 前置條件

- **GroupDocs.Redaction .NET** 版本 21.6 或更新。  
- .NET Framework 4.7.2 以上、.NET Core 3.1 以上，或 .NET 5/6+。  
- 基本的 C# 知識與開發 IDE（Visual Studio、Rider 等）。

## 在 .NET 中設定 GroupDocs.Redaction
開始使用 GroupDocs.Redaction 非常簡單。請使用以下任一方式安裝套件：

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

或是使用 **NuGet 套件管理員 UI**：直接搜尋 “GroupDocs.Redaction” 並點選 **Install**。

### 取得授權
若要試用 GroupDocs.Redaction，您可以取得免費試用授權。持續開發或正式上線時，請購買完整授權或向官方網站申請臨時授權。

安裝完成後，請依照以下方式初始化函式庫：

```csharp
using GroupDocs.Redaction;
```

## 實作指南

### 取得文件資訊功能
此功能著重於使用 GroupDocs.Redaction .NET 從文件中提取關鍵元資料。請依照以下步驟操作：

#### 步驟 1：準備文件路徑
定義目標檔案的絕對或相對路徑：

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

將 `YOUR_DOCUMENT_DIRECTORY` 替換為包含您文件的資料夾路徑。

#### 步驟 2：初始化 Redactor 實例
建立一個提供元資料方法存取的 `Redactor` 物件：

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### 步驟 3：取得文件資訊
在 `Redactor` 實例上呼叫 `GetDocumentInfo()` 以取得所有可用屬性：

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

回傳的物件包含檔案類型、頁數以及檔案大小等資訊。

#### 步驟 4：顯示文件詳細資訊
將資訊輸出至主控台或 UI。以下範例程式碼（已註解以便單獨執行）示範如何列印每個屬性：

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### 為何使用 GroupDocs.Redaction 進行元資料擷取？
GroupDocs.Redaction 支援 **50+ 種檔案格式**，且可處理高達 **2 GB** 大小的文件，同時在一般工作負載下將記憶體使用量控制在 **100 MB** 以下。函式庫在不完整載入文件的情況下擷取元資料，提供快速回應——在標準伺服器硬體上，對 100 頁 PDF 的處理時間通常低於 **200 ms**。

### 常見問題與解決方案
- **檔案路徑不正確** – 請確認路徑字串，並確保執行程序能存取該檔案。  
- **不支援的格式** – 請檢查格式清單；若缺少某種格式，請先考慮將其轉換。  
- **效能瓶頸** – 對於非常大的檔案，請啟用串流選項或分批處理頁面，以限制記憶體使用量。

## 實務應用
了解文件的元資料可支援多種實務情境：

1. **文件管理系統 (DMS)** – 根據類型、大小或頁數自動分類與索引。  
2. **合規審核** – 在歸檔前驗證機密檔案是否具備必要的元資料。  
3. **資料遷移** – 依屬性分組檔案，以簡化大量遷移任務。

## 效能考量
- **有效的資源使用** – 在 `using` 區塊中使用 `Redactor` 實例，以確保正確釋放。  
- **非同步模式** – 將元資料呼叫包裝於 `Task.Run` 或實作非同步封裝，以保持桌面或 Web 應用程式的 UI 執行緒回應性。

## 常見問與答

**Q: 哪些文件格式可以提取元資料？**  
A: GroupDocs.Redaction 可從超過 50 種格式讀取元資料，包括 PDF、DOCX、XLSX、PPTX、HTML 以及常見的影像類型。

**Q: 如何處理受密碼保護的檔案？**  
A: 在 `Redactor` 建構子中傳入密碼；API 會在提取元資料前解密檔案。

**Q: 處理的檔案大小有上限嗎？**  
A: 雖然沒有硬性上限，但超過 2 GB 的檔案可能需要額外的記憶體調校；效能仍會隨檔案大小線性增長。

**Q: 可以批次取得元資料嗎？**  
A: 可以——遍歷檔案路徑集合，對每個檔案呼叫 `GetDocumentInfo()`；函式庫支援執行緒安全的平行執行。

**Q: 開發版需要授權嗎？**  
A: 免費試用授權足以支援開發與測試；正式部署則需商業授權。

## 資源
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

## 結論
您現在已擁有使用 GroupDocs.Redaction .NET **如何取得元資料** 的完整步驟指南。透過 `Redactor.GetDocumentInfo()` 方法，您可以快速讀取檔案元資料、支援合規工作流程，並強化任何文件處理管線。探索其他 Redaction 功能——例如內容遮蔽、浮水印與文件轉換——以打造功能完整的文件管理解決方案。

---

**最後更新：** 2026-06-06  
**測試環境：** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**作者：** GroupDocs  

## 相關教學
- [如何使用 GroupDocs.Redaction .NET 從串流中提取文件元資料](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [如何使用 GroupDocs.Redaction for .NET 進行文件元資料遮蔽 - 完整指南](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction for .NET 的文件載入教學](/redaction/net/document-loading/)