---
date: 2026-06-11
description: 了解如何匯出已遮蔽檔案、設定輸出資料夾、建立點陣化 PDF，並使用 GroupDocs.Redaction for .NET 儲存至串流。
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction .NET 匯出已遮蔽文件
type: docs
url: /zh-hant/net/document-saving/
weight: 3
---

# 如何使用 GroupDocs.Redaction .NET 匯出已編輯的文件

在本完整指南中，您將了解 **如何匯出已編輯** 的內容，安全且高效地使用 GroupDocs.Redaction for .NET。無論您是需要保留原始檔案類型、將文件鎖定為光柵化 PDF，或是直接在記憶體中串流結果，我們都會以清晰、口語化的說明和實務技巧逐一說明每個選項。完成本教學後，您將能針對任何合規需求選擇合適的匯出策略。

## 快速解答
- **可以匯出哪些格式？** 任意 GroupDocs.Redaction 支援的 30 多種原生格式，另加光柵化 PDF 以獲得最高安全性。  
- **串流需要授權嗎？** 需要，生產環境的串流必須擁有有效的 GroupDocs.Redaction 授權。  
- **可以設定自訂輸出資料夾嗎？** 當然可以 – 使用 `OutputPath` 屬性或 `SaveOptions` 進行設定。  
- **光柵化對大型檔案安全嗎？** 它可處理最多 500 頁的文件，且不會將整個檔案載入記憶體。  
- **支援哪些 .NET 版本？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。

## 什麼是 GroupDocs.Redaction？
GroupDocs.Redaction 是一套 .NET 函式庫，可程式化地移除或遮蔽 PDF、Word、Excel、PowerPoint、影像以及其他多種格式中的敏感資訊。它提供高階 API 讓您定義編輯區域、套用政策，最後匯出已清理的文件。這使得在任何 .NET 應用程式中整合編輯功能變得相當簡單。

## 為什麼將已編輯的文件匯出為光柵化 PDF？
光柵化 PDF 會將每一頁轉換為平面影像，消除日後可能被提取的隱藏文字層。此格式保證已編輯的內容無法復原，符合 GDPR、HIPAA 等嚴格的法規標準。GroupDocs.Redaction 可產生最高 300 dpi 的光柵化 PDF，兼顧視覺保真度與安全性。

## 如何匯出已編輯的文件？
載入來源檔案，套用編輯規則，然後呼叫相應的儲存方法 — 使用 `Save` 以原始格式儲存，`SaveAsRasterizedPdf` 產生僅含影像的 PDF，或 `SaveToStream` 進行記憶體內處理。以下為逐步工作流程。每種方法皆確保已編輯的內容永久移除，同時保留所需的輸出格式。

### 步驟 1：安裝 NuGet 套件
將最新的 GroupDocs.Redaction 套件加入您的專案：

```bash
dotnet add package GroupDocs.Redaction
```

### 步驟 2：載入文件並定義編輯
建立 `Redactor` 實例，載入檔案，並指定要隱藏的區域。`Redactor` 類別提供載入文件與套用編輯規則的核心功能。

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### 步驟 3：選擇匯出方式
#### 以原始格式匯出
```csharp
redactor.Save("RedactedReport.docx");
```

#### 匯出為光柵化 PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### 匯出至記憶體串流（適用於 Web API）
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save` 方法將已編輯的文件以原始格式寫入檔案。`SaveAsRasterizedPdf` 會產生每頁皆以影像呈現的 PDF，移除所有隱藏文字。`SaveToStream` 會將已編輯的檔案以記憶體串流回傳，適用於 Web 回應。

## 如何設定輸出資料夾？
在 `Redactor` 上設定 `OutputPath` 屬性，或傳入包含目標目錄的自訂 `SaveOptions` 物件。`OutputPath` 為 `Redactor` 的屬性，用於指定輸出檔案寫入的目錄。`SaveOptions` 允許自訂多種儲存參數，包括輸出資料夾。此設定確保所有匯出檔案都落在可預測的位置，簡化批次處理流程。您亦可依文件類型指定子資料夾，以保持工作區井然有序。

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## 常見問題與解決方案
- **編輯未套用：** 確認搜尋模式與文件文字完全相符；必要時使用 `RegexOptions.IgnoreCase`。`RegexOptions` 為列舉，用於控制正規表達式的匹配行為，例如大小寫敏感性。  
- **大型檔案導致記憶體壓力：** 使用 `SaveToStream` 開啟串流模式，避免對整個文件呼叫 `Save`。  
- **光柵化 PDF 看起來模糊：** 在 `RasterizationOptions` 中提高 DPI（例如 300–600）以提升影像品質。`RasterizationOptions` 可設定 DPI、影像格式等光柵化 PDF 輸出的參數。

## 常見問答

**Q: 我可以匯出至原本不支援的格式嗎？**  
A: 可以，GroupDocs.Redaction 能將大多數輸入類型轉換為 PDF、DOCX、XLSX、PPTX 或光柵化 PDF，支援超過 30 種格式。

**Q: 光柵化如何保護已編輯的資料？**  
A: 透過將每頁渲染為平面影像，移除所有隱藏文字層，使得無法提取原始內容。

**Q: 可以串接多個編輯規則嗎？**  
A: 當然可以 — 您可以多次呼叫 `Apply`，或傳入 `RedactionOptions` 集合一次處理多個模式。`RedactionOptions` 定義單一編輯操作的設定，例如區域與替換類型。

**Q: 必須關閉 Redactor 物件嗎？**  
A: `Redactor` 實作 `IDisposable`；請將其放入 `using` 區塊或呼叫 `Dispose()` 以立即釋放檔案句柄。`IDisposable` 為介面，提供釋放非受控資源的機制。

**Q: 官方測試過哪些 .NET 執行環境？**  
A: GroupDocs.Redaction 已在 .NET Framework 4.6+、.NET Core 3.1+、以及 .NET 5/6/7 上驗證。

## 其他資源

### 可用教學
- [如何使用 GroupDocs.Redaction for .NET 將文件儲存為光柵化 PDF：完整指南](./groupdocs-redaction-net-rasterized-pdfs/)
- [在 .NET 中使用 GroupDocs.Redaction 實作輸出目錄：完整指南](./implement-output-directory-groupdocs-redaction-dotnet/)
- [使用 GroupDocs.Redaction for .NET 編輯並儲存文件：完整指南](./redact-save-documents-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction .NET 以原始格式儲存已編輯文件](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [在 .NET 中使用串流進行安全文件編輯：GroupDocs.Redaction 指南](./secure-document-redaction-net-streams-groupdocs-redaction/)

### 有用連結
- [GroupDocs.Redaction for .NET 文件](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET API 參考](https://reference.groupdocs.com/redaction/net/)
- [下載 GroupDocs.Redaction for .NET](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-06-11  
**測試版本：** GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

---

## 相關教學
- [使用 GroupDocs.Redaction .NET 以原始格式儲存已編輯文件](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 將文件儲存為光柵化 PDF：完整指南](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [在 .NET 中使用串流進行安全文件編輯：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)