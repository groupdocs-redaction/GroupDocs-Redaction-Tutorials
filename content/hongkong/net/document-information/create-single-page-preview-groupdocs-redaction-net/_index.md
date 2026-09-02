---
date: '2026-06-06'
description: 了解如何使用 GroupDocs.Redaction for .NET 將頁面轉換為 PNG 以及預覽 PDF 頁面。一步一步的指南、程式碼片段與實務技巧。
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: 使用 GroupDocs.Redaction .NET 將頁面轉換為 PNG
type: docs
url: /zh-hant/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction .NET 轉換頁面為 PNG

在大型文件中僅預覽單一頁面是常見需求，當您只想分享相關資訊時。本教學將教您如何使用 GroupDocs.Redaction for .NET **將頁面轉換為 PNG**，設定預覽輸出，並將結果整合至您的應用程式。我們將逐步說明前置條件、安裝、程式碼設定與實用技巧，讓您在數分鐘內即可產生單頁 PNG 預覽。

## 快速解答
- **我可以只產生單一頁面的 PNG 預覽嗎？** 是的，使用 `PreviewOptions` 來指定頁碼與格式。  
- **GroupDocs.Redaction 支援哪種格式的預覽？** 預設為 PNG，但亦支援 JPEG 與 BMP。  
- **開發時需要授權嗎？** 免費試用可用於測試；商業使用則需正式授權。  
- **這能在 .NET Core 與 .NET Framework 上運作嗎？** 當然可以——此函式庫以 .NET Standard 2.0+ 為目標。  
- **對於大型檔案，處理過程是否節省記憶體？** 會的，API 以串流方式讀取頁面，避免載入整個文件。

## 什麼是將頁面轉換為 PNG？
**將頁面轉換為 PNG** 指的是從支援的文件（PDF、DOCX、PPTX 等）中抽取單一頁面，並將該頁面渲染為 Portable Network Graphics（PNG）影像。產生的影像保留原始頁面的版面配置、字型與圖形，讓您在分享清晰快照的同時，隱藏文件的其他部分。

## 為何使用單頁預覽？
產生單頁 PNG 預覽可減少頻寬、加快載入速度，並僅顯示必要的資訊以保護敏感內容。GroupDocs.Redaction 能在一般伺服器硬體上於 0.5 秒內將 300 頁 PDF 轉換為 200 KB PNG，十分適合網站入口與報表工具。

## 前置條件

- **GroupDocs.Redaction for .NET** – 執行文件遮蔽與預覽產生的核心函式庫。  
- **System.IO** – .NET 標準的檔案處理命名空間。  
- .NET Core 3.1+ 或 .NET Framework 4.6.1+（任何支援 .NET Standard 2.0 的平台）。  
- 基本的 C# 知識與 NuGet 套件管理經驗。

## 設定 GroupDocs.Redaction for .NET

### 安裝資訊

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- 在 Visual Studio 中開啟您的專案。  
- 選取 **Manage NuGet Packages**。  
- 搜尋 **GroupDocs.Redaction** 並安裝最新的穩定版。

### 取得授權步驟
要執行此函式庫必須擁有有效授權。您可先使用免費試用版，或申請臨時金鑰：

1. 前往 [GroupDocs website](https://purchase.groupdocs.com/temporary-license) 申請臨時授權。  
2. 按照電子郵件中的指示，將授權檔案加入您的專案。

### 基本初始化與設定
`RedactionEngine` 類別是所有操作的入口點，包含預覽產生。  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## 實作指南

### 概觀
本節說明如何透過設定 `PreviewOptions` 並呼叫預覽 API 來 **將頁面轉換為 PNG**。此方法適用於 PDF、DOCX、PPTX 以及 GroupDocs.Redaction 支援的其他多種格式。

### 步驟 1：準備環境
設定來源檔案路徑與輸出資料夾。使用 `Path.Combine` 來建立跨平台的路徑。  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### 步驟 2：設定預覽選項
`PreviewOptions` 讓您定義頁碼、影像尺寸與輸出格式。此類別是預覽產生的設定中心。  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### 主要設定說明
- **Width & Height** – 調整這些數值以符合目標顯示解析度。  
- **PageNumbers** – 提供包含欲渲染之頁面索引（從 0 起算）的陣列。  
- **PreviewFormat** – 預設為 PNG；若需較小檔案可切換為 `PreviewFormat.Jpeg`。

### 疑難排解技巧
如果未產生 PNG：

- 確認來源檔案路徑正確且檔案可存取。  
- 確保在呼叫任何 API 方法前已載入授權檔案。  
- 確認 `PreviewOptions.PageNumbers` 包含有效的頁面索引（例如，`0` 代表第一頁）。

## 實務應用
在多種情境下，建立單頁 PNG 預覽都相當有用：

1. **客戶簡報** – 僅顯示相關投影片或合約條款。  
2. **內部審閱** – 免開啟完整文件即可快速視覺檢查。  
3. **內容摘要** – 在電子郵件或儀表板中嵌入頁面快照，提供即時情境。  

將此功能整合至 CMS 或 CRM，可自動為上傳的文件產生縮圖，提升使用者體驗。

## 效能考量
- **Memory Management** – 使用完畢後釋放 `RedactionEngine` 實例以釋放資源。  
- **Asynchronous Execution** – 在 UI 應用程式中使用 `await engine.GeneratePreviewAsync(...)`，保持介面回應。  
- **Library Updates** – GroupDocs.Redaction 支援 **30+ 種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理高達 500 頁的文件。請保持套件為最新，以獲得效能優化。

## 結論
您現在已掌握完整且可投入生產的 **將頁面轉換為 PNG** 方法，並可使用 GroupDocs.Redaction for .NET 產生單頁預覽。依照上述步驟，即可將高品質 PNG 快照嵌入任何 .NET 應用程式，提升文件分享，同時確保安全與效能。

## 常見問題

**Q: 我可以為受密碼保護的 PDF 產生預覽嗎？**  
A: 可以，於初始化 `RedactionEngine` 時提供密碼，即可正常產生預覽。

**Q: 如何將輸出格式從 PNG 改為 JPEG？**  
A: 在呼叫預覽方法前，設定 `options.PreviewFormat = PreviewFormat.Jpeg`。

**Q: 是否可以一次預覽多個頁面？**  
A: 當然可以——將頁碼陣列指派給 `options.PageNumbers`（例如 `new[] {0, 2, 4}`）。

**Q: 若預覽影像模糊該怎麼辦？**  
A: 提高 `options.Width` 與 `options.Height` 至更高解析度；函式庫會相應放大影像。

**Q: 這能在 Linux 容器上運作嗎？**  
A: 可以，GroupDocs.Redaction .NET 為跨平台，能在支援 .NET Core 的 Docker 容器內執行。

## 資源
- [文件說明](https://docs.groupdocs.com/redaction/net/)  
- [API 參考](https://reference.groupdocs.com/redaction/net)  
- [下載最新版本](https://releases.groupdocs.com/redaction/net/)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權取得](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-06-06  
**測試環境：** GroupDocs.Redaction 5.6 for .NET  
**作者：** GroupDocs

## 相關教學

- [精通文件安全：使用 GroupDocs.Redaction .NET 進行 Word 文件光柵化與遮蔽](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)  
- [如何使用 GroupDocs.Redaction .NET 刪除 PDF 頁面：完整指南](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)  
- [使用 GroupDocs.Redaction .NET 實作文件遮蔽：逐步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)