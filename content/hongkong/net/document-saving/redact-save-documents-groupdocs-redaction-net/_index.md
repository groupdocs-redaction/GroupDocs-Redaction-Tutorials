---
date: '2026-07-20'
description: 了解如何使用 GroupDocs.Redaction for .NET 塗抹文件、隱藏敏感資訊，並將塗抹後的檔案儲存至記憶體串流。
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: 使用 GroupDocs.Redaction for .NET 進行文件塗抹。請依照本逐步指南隱藏敏感資訊，並將塗抹後的檔案儲存至記憶體串流。
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: 如何使用 GroupDocs.Redaction for .NET 塗抹文件
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: 使用 GroupDocs.Redaction for .NET 進行文件塗抹的完整指南
type: docs
url: /zh-hant/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# 如何使用 GroupDocs.Redaction for .NET 進行文件塗銷

在現代企業環境中，**如何塗銷文件** 是保護個人資料、商業機密及合規相關資訊的關鍵技能。本指南將帶領您從 Word、PDF 或圖像檔案中塗銷敏感資訊，並直接將塗銷後的輸出儲存至記憶體串流——全部使用 GroupDocs.Redaction for .NET。

## 快速解答
- **塗銷的作用是什麼？** 它會永久以佔位符取代選取的內容或將其移除，確保資料永遠無法復原。  
- **支援哪些格式？** 超過 30 種檔案類型，包括 PDF、DOCX、PPTX 以及常見的圖像格式。  
- **可以在不寫入磁碟的情況下進行塗銷嗎？** 可以——將結果儲存至 `MemoryStream` 以進行記憶體內處理。  
- **生產環境需要授權嗎？** 生產使用需購買完整授權；亦提供免費試用供評估。  
- **是否相容 .NET Core？** 完全相容——GroupDocs.Redaction 支援 .NET Framework 4.6+、.NET Core 3.1+ 以及 .NET 5/6/7。

## 什麼是文件塗銷？
文件塗銷會永久移除或遮蔽檔案中的機密文字、圖像與中繼資料，確保隱藏的內容無法在之後被復原、檢視或擷取。它會以佔位符（如黑色矩形或自訂文字）取代敏感元素，並更新文件結構，使塗銷的資料無法恢復。

## 為何使用 GroupDocs.Redaction 來塗銷文件？
GroupDocs.Redaction 支援 **30+ 種檔案格式**，且可處理高達 **2 GB** 的檔案而無需將整個文件載入記憶體，較多數競爭對手提供 **30 % 更快的處理時間**。其 API 允許您透過單一方法呼叫套用精確片語、正規表達式或基於圖像的塗銷，使其成為 .NET 開發者最有效率的選擇。

## 前置條件
- **GroupDocs.Redaction** NuGet 套件（最新版本）。  
- .NET Framework 4.6+ **或** .NET Core 3.1+ 已安裝。  
- 支援 C# 的 IDE，例如 Visual Studio 2022。  
- 基本的 C# 知識與檔案 I/O 的熟悉度。

### 必要的函式庫與版本
- **GroupDocs.Redaction** – 請始終使用最新版本，以取得最新的塗銷演算法與安全修補。  
- **System.IO** – 用於串流處理（內建於 .NET）。

### 取得授權步驟
- **免費試用：** 前往 GroupDocs 官方網站註冊 30 天試用。  
- **臨時授權：** 申請臨時金鑰以進行開發測試。  
- **完整授權：** 購買正式授權以獲得無限制使用。

## 基本初始化與設定
`Redactor` 類別是 GroupDocs.Redaction 所有塗銷操作的入口點。安裝 NuGet 套件後，您可使用來源文件的路徑建立 `Redactor` 實例。

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## 如何在文件中塗銷特定文字？
若要塗銷特定文字，先使用 `Redactor` 實例載入來源檔案，然後套用 `ExactPhraseRedaction` 以針對欲隱藏的精確字串。API 會掃描文件，將每個符合項目以選定的覆蓋層取代，並將變更記錄於變更日誌中，讓您在儲存前驗證塗銷結果。

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

`ExactPhraseRedaction` 類別會將每一次出現的精確片語以黑色矩形（或您自訂的任何佔位符）取代。

**步驟說明：**
1. **載入** – 建立指向您檔案的 `Redactor` 實例。  
2. **套用** – 使用 `ExactPhraseRedaction`（或其他塗銷類型）呼叫 `Apply`。  
3. **檢查** – 檢視 `RedactorChangeLog` 以確認找到並取代了多少符合項目。  

## 如何將塗銷後的文件儲存至 Memory Stream？
`MemoryStream` 是一種 .NET 串流，將資料儲存在記憶體中，允許在不進行磁碟 I/O 的情況下快速讀寫。透過 `Save` 方法，您可以將塗銷後的輸出直接寫入 `MemoryStream`，之後可將其傳送至網路、儲存於資料庫，或直接從 API 端點回傳，而無需產生暫存檔案。

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**重點說明：**
- `Save` 方法會將塗銷後的輸出寫入任何 `Stream` 實作，包括 `MemoryStream`。  
- 不會產生暫存檔案，提升安全性與效能。  
- 您可將其與 ASP.NET Core 的 `FileStreamResult` 結合，直接將檔案回傳至瀏覽器。

## 常見問題與解決方案
| 問題 | 為何發生 | 解決方式 |
|------|----------|----------|
| **未套用塗銷** | 片語大小寫與來源不同。 | 使用 `ExactPhraseRedaction("John Doe", caseSensitive: false)` 或正規表達式塗銷以彈性匹配。 |
| **大型檔案導致 OutOfMemory** | 嘗試將整個檔案載入記憶體。 | GroupDocs.Redaction 內部以串流方式處理資料；請確保使用最新版本以分塊處理檔案。 |
| **儲存的檔案損毀** | 在傳送前未重設串流位置。 | 在 `redactor.Save(stream)` 後，於讀取或回傳前將 `stream.Position = 0`。 |

## 常見問答

**問：我可以使用相同的 API 塗銷 PDF 檔案嗎？**  
答：可以——GroupDocs.Redaction 會一致地處理 PDF、DOCX、PPTX 以及多種圖像格式；只需將 `Redactor` 指向 PDF 檔案即可。

**問：塗銷後的內容在將文件轉換為其他格式後仍會保留嗎？**  
答：絕對會——一旦完成塗銷，內容即永久移除，無論之後如何轉換格式皆不會復原。

**問：如何自訂塗銷的外觀？**  
答：使用 `RedactionOptions` 設定覆蓋顏色、透明度，或以自訂字串取代文字。

**問：能否使用正規表達式進行塗銷？**  
答：可以——`RegexRedaction` 允許您定義如信用卡號碼或電子郵件地址等模式。

**問：官方支援哪些 .NET 版本？**  
答：.NET Framework 4.6+、.NET Core 3.1+、.NET 5、.NET 6 以及 .NET 7。

---

**最後更新：** 2026-07-20  
**測試版本：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## 相關教學

- [如何使用 GroupDocs.Redaction .NET 載入並塗銷文件：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction .NET 以原始格式儲存塗銷文件](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [在 .NET 中使用串流進行安全文件塗銷：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)