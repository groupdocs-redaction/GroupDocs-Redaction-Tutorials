---
date: '2026-07-20'
description: 了解如何使用 GroupDocs.Redaction .NET 列出格式，將此功能整合至您的文件工作流程，並提升效能。
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: 探索如何使用 GroupDocs.Redaction .NET 列出格式，參閱逐步指南，並獲取在 .NET 應用程式中達致最佳效能的技巧。
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: 如何使用 GroupDocs.Redaction .NET 列出格式
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: 如何使用 GroupDocs.Redaction .NET 列出格式
type: docs
url: /zh-hant/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# 如何列出 GroupDocs.Redaction .NET 支援的格式

管理各式各樣的文件類型是開發文件中心應用程式的日常現實。在本教學中，您將學習 **如何列出** GroupDocs.Redaction .NET 能處理的格式，從而在處理前驗證檔案、為使用者提供正確的選項，並保持工作流程的效率。

## 介紹

有效率的文件處理始於清楚了解您的函式庫支援哪些檔案類型。GroupDocs.Redaction 提供內建方法來取得此資訊，讓您能建立動態 UI 元件、強制驗證規則，並避免執行時錯誤。以下您將找到從安裝到實用程式碼片段與效能建議的完整說明。

### 快速回答
- **「如何列出格式」是什麼意思？** 它指的是取得 GroupDocs.Redaction 可處理的檔案副檔名集合。  
- **需要授權嗎？** 是的，正式環境使用需具備有效的 GroupDocs.Redaction 授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.6 以上、.NET Core 3.1 以上、.NET 5/6/7。  
- **支援多少種格式？** 內建支援超過 30 種輸入與輸出格式。  
- **需要特別設定嗎？** 除了標準函式庫初始化外，無需額外設定。

## 什麼是「如何列出格式」？

它是透過呼叫函式庫的 FileType API 取得一個集合，每個項目包含檔案副檔名與可讀的名稱。開發者可遍歷此集合以建立驗證規則、填充 UI 下拉選單，或記錄支援的類型，確保僅處理相容的文件。

## 為何要使用 GroupDocs.Redaction 列出格式？

GroupDocs.Redaction 支援 **30+** 種不同的檔案類型，包括 PDF、DOCX、PPTX 以及影像格式，讓您無需第三方轉換器即可處理大多數企業文件。透過程式化列出這些格式，可消除猜測、減少支援工單，並確保只有相容的檔案進入處理流程。

## 前置條件

- **GroupDocs.Redaction for .NET** – 從官方網站下載最新套件。  
- **.NET Framework 或 .NET Core** – 與您的開發環境相容。  
- **Visual Studio**（或任何相容 C# 的 IDE）。  
- 具備基本的 C# 語法知識。

## 設定 GroupDocs.Redaction for .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### 套件管理員
`Install-Package GroupDocs.Redaction`

### NuGet 套件管理員 UI
- 搜尋 **“GroupDocs.Redaction”** 並安裝最新版本。

### 取得授權
GroupDocs 提供免費試用、評估用臨時授權或正式購買方案。請前往 GroupDocs 官方網站取得相應的授權檔案。

### 基本初始化與設定
加入套件後，引用命名空間並建立 `Redactor` 實例：

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## 實作指南

### 如何使用 GroupDocs.Redaction .NET 列出格式？
載入函式庫，呼叫靜態輔助方法並排序結果——只需兩行程式碼即可取得可直接使用的集合。使用 `FileType.GetSupportedFileFormats()` 取得 `IEnumerable<FileType>`，其中包含每種格式的副檔名與顯示名稱，然後依副檔名排序以得到整潔的 UI 列表。

### 取得支援的檔案格式

#### 概觀
目標是取得 GroupDocs.Redaction 可處理的檔案類型清單，以便整合至驗證邏輯、UI 下拉選單或記錄機制。

#### 步驟說明

**1. 取得支援的檔案類型**  
`FileType.GetSupportedFileFormats()` 會回傳函式庫識別的所有格式。此方法屬於 `GroupDocs.Redaction.FileType` 類別，封裝了檔案副檔名與友好名稱等中繼資料。

**2. 顯示支援的檔案類型**  
遍歷集合並輸出每種格式的副檔名與說明。以下為內嵌程式碼範例：

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

此程式碼片段會印出如「.pdf – Portable Document Format」的整齊排序清單，非常適合填充 UI 元件。

### 疑難排解提示
- **缺少套件** – 請確認 NuGet 套件參考，必要時還原套件。  
- **授權路徑錯誤** – 確認授權檔已複製至輸出目錄，或提供絕對路徑。  
- **不支援的副檔名** – 若某格式未列出，請確認使用最新的函式庫版本；較新版本會加入更多格式。

## 實務應用
了解支援的檔案格式可開啟多種實務情境：

1. **文件管理系統** – 依支援清單驗證上傳檔案，避免處理失敗。  
2. **內容安全** – 僅對引擎能安全修改的檔案類型套用遮蔽規則。  
3. **批次處理流程** – 在呼叫遮蔽前篩選大量檔案批次，節省 CPU 與記憶體。

## 效能考量
- **記憶體佔用** – 列出格式是輕量操作，並不會載入任何文件至記憶體。  
- **批次作業** – 處理數百檔案時，僅取得一次格式清單並重複使用，以避免重複呼叫。  
- **執行緒安全** – `FileType.GetSupportedFileFormats()` 為執行緒安全，可在平行任務中直接呼叫，無需同步機制。

## 結論
現在您已掌握使用 GroupDocs.Redaction .NET **列出格式** 的完整、可投入生產的做法。整合此功能後，可加強驗證、提升使用者體驗，並讓文件處理流程更穩健。

### 後續步驟
- 探索 `Redactor` API，根據檔案類型套用遮蔽規則。  
- 將格式清單與前端下拉選單結合，實現無縫檔案選擇。  
- 檢視效能指南，以最佳化大規模批次作業。

## 常見問題

**Q: 可以在未初始化 Redactor 實例的情況下取得格式清單嗎？**  
A: 可以，`FileType.GetSupportedFileFormats()` 為靜態方法，無需 `Redactor` 物件。

**Q: 清單是否同時包含輸入與輸出格式？**  
A: 此方法回傳函式庫可讀寫的所有格式；每個 `FileType` 都包含 `CanRead` 與 `CanWrite` 標誌。

**Q: 支援的格式清單更新頻率為何？**  
A: GroupDocs 會隨每個函式庫版本釋出格式更新；在執行時檢查清單即可確保取得最新集合。

**Q: 有辦法只篩選與 PDF 相容的格式嗎？**  
A: 可以，篩選集合中 `format.Extension == ".pdf"` 或 `format.Name.Contains("PDF")` 的項目。

**Q: 此做法能在 .NET Core 2.1 上運作嗎？**  
A: 此方法需要 .NET Core 3.1 或更新版本，較早的執行環境不支援。

## FAQ 區段
1. **如何安裝 GroupDocs.Redaction for .NET？**  
   使用 CLI 指令 `dotnet add package GroupDocs.Redaction`，或透過 NuGet 套件管理員 UI 安裝。

2. **取得支援格式時常見的問題有哪些？**  
   確保已還原所有相依性，且引用正確的命名空間 (`GroupDocs.Redaction`)。

3. **此功能能在非 .NET 應用程式中使用嗎？**  
   本教學聚焦於 .NET，但 GroupDocs 亦提供 Java、Python 等平台的類似 API。

4. **使用 GroupDocs.Redaction 時，如何最佳化效能？**  
   重複使用格式清單、僅在檢查相容性時避免載入完整文件，並於批次作業期間監控記憶體使用情況。

5. **GroupDocs.Redaction 支援哪些檔案類型？**  
   函式庫支援超過 30 種格式，包括 PDF、DOCX、PPTX、XLSX、BMP、PNG、JPEG 等等。使用 `FileType.GetSupportedFileFormats()` 可查看完整清單。

## 資源
- [文件說明](https://docs.groupdocs.com/redaction/net/)
- [API 參考文件](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新日期：** 2026-07-20  
**測試環境：** GroupDocs.Redaction 4.2.0 for .NET  
**作者：** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## 相關教學

- [GroupDocs.Redaction .NET 格式處理教學](/redaction/net/format-handling/)
- [GroupDocs.Redaction for .NET 文件載入教學](/redaction/net/document-loading/)
- [GroupDocs.Redaction .NET 文件儲存教學](/redaction/net/document-saving/)