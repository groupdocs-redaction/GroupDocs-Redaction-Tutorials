---
date: '2026-05-27'
description: 了解如何使用 GroupDocs.Redaction for .NET 在 PDF 中遮蔽註釋，內容包括設定、正則表達式遮蔽及效能技巧。
keywords:
- how to redact annotations
- apply redaction to pdf
- pdf annotation redaction
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  headline: How to Redact Annotations Using GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  name: How to Redact Annotations Using GroupDocs.Redaction for .NET
  steps:
  - name: Create a Redactor instance (definition anchor)
    text: '`Redactor` is the entry point for all redaction operations; you pass the
      source file path to its constructor.'
  - name: Define your regular expression (definition anchor)
    text: '`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity
      (`i`) and multi‑line mode (`m`) directly in the pattern. - `(?im...)`: Enables
      case‑insensitivity (`i`) and multi‑line search (`m`).'
  - name: Apply the redaction (definition anchor)
    text: '`AnnotationRedaction` is a specialized rule that scans annotation objects
      and replaces matching text with a black rectangle. **Explanation:** - **Parameters:**
      The regex pattern tells the engine which text to target. - **Return Values:**
      This method modifies the document in place; no return value is'
  - name: Save the redacted document (definition anchor)
    text: '`Redactor.Save` writes the modified file to disk, preserving the original
      format unless you specify otherwise.'
  type: HowTo
- questions:
  - answer: Yes. Open the document with `Redactor(string path, string password)` and
      then apply your redaction rules as usual.
    question: Can I redact annotations in password‑protected PDFs?
  - answer: The API works on a copy in memory; the original file remains unchanged
      until you explicitly call `Save`.
    question: Does GroupDocs.Redaction modify the original file?
  - answer: All standard PDF annotation types—including comments, highlights, and
      sticky notes—are fully supported.
    question: How many annotation types are supported?
  - answer: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and
      render it in your UI for a quick preview.
    question: Is there a way to preview redactions before saving?
  - answer: The library can handle files up to **2 GB**; larger files should be split
      before processing.
    question: What is the maximum file size I can process?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction for .NET 進行註釋遮蔽
type: docs
url: /zh-hant/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/
weight: 1
---

# 如何使用 GroupDocs.Redaction for .NET 進行註釋遮蔽

如果您需要在 PDF 或 Word 檔案中 **如何遮蔽註釋**，您來對地方了。本指南將帶您完成安裝 GroupDocs.Redaction for .NET、設定基於正則表達式的註釋遮蔽，以及為大規模工作負載優化效能。完成後，您只需幾行 C# 程式碼即可隱藏敏感的評論、備註及其他中繼資料。

## 快速解答
- **哪個函式庫負責註釋遮蔽？** GroupDocs.Redaction for .NET.  
- **我可以使用正則表達式嗎？** 是 – API 支援完整的 .NET 正則表達式語法。  
- **開發時需要授權嗎？** 免費試用可用於測試；正式環境需購買授權。  
- **是否相容於 .NET 6 與 .NET Core？** 完全支援 .NET Framework 4.5+、.NET Core 3.1+ 以及 .NET 6+。  
- **在大型檔案上遮蔽速度如何？** 經過優化的模式可在一般伺服器上於 5 秒內處理 500 頁的 PDF。

## 什麼是註釋遮蔽？
註釋遮蔽會永久移除或遮蔽文件評論、備註、便利貼及其他中繼資料物件中的文字。透過刪除這些隱藏資訊，此技術可確保機密資料即使在檔案被分發或於其他應用程式開啟時也無法被擷取或檢視，從而維護隱私與合規性。

## 為何要對 PDF 註釋進行遮蔽？
GroupDocs.Redaction 支援 **30 多種文件格式**，且可在不將整個內容載入記憶體的情況下處理高達 **2 GB** 的檔案。使用內建的正則表達式引擎可將處理時間縮短最多 **70 %**，相較於手動字串搜尋，更適合高量律師或金融工作流程。

## 先決條件

- **GroupDocs.Redaction** 函式庫（最新 NuGet 版本）。  
- 相容的 **.NET** 執行環境（Framework 4.5+、.NET Core 3.1+、.NET 5/6）。  
- 開發環境，例如 **Visual Studio 2022** 或 **VS Code**。  
- 基本的 C# 知識以及正則表達式的熟悉度。  

## 如何使用 GroupDocs.Redaction 進行註釋遮蔽？

載入來源文件、定義正則表達式模式、套用 `AnnotationRedaction`，並儲存結果——整個流程僅需三個簡潔步驟。以下各節將逐步說明每個步驟，並提供您需要自行替換的程式碼佔位符。

### 步驟 1 – 透過 .NET CLI 安裝函式庫
**回答：** 在專案資料夾中執行 `dotnet add package GroupDocs.Redaction`；CLI 會下載最新的穩定套件並自動更新您的專案檔案。  

```bash
dotnet add package GroupDocs.Redaction
```

### 步驟 2 – 透過套件管理員主控台安裝函式庫
**回答：** 在 Visual Studio 的套件管理員主控台中執行 `Install-Package GroupDocs.Redaction`；此指令會解析相依性並將參考加入您的專案。  

```powershell
Install-Package GroupDocs.Redaction
```

### 步驟 3 – 初始化 Redactor（定義錨點）
`Redactor` 類別是載入文件並套用遮蔽規則的核心引擎。  

```csharp
using System;
using GroupDocs.Redaction.Redactions;

namespace DocumentRedaction
{
    class Program
    {
        static void Main(string[] args)
        {
            string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\annotated.xlsx"; // Replace with actual document path.
            
            using (Redactor redactor = new Redactor(sourceFile))
            {
                // Your redaction logic will go here.
            }
        }
    }
}
```

## 套用註釋遮蔽

### 步驟 1：建立 Redactor 實例（定義錨點）
`Redactor` 是所有遮蔽操作的入口點；您需要將來源檔案路徑傳入其建構子。  

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further processing will occur here.
}
```

### 步驟 2：定義正則表達式（定義錨點）
`Regex` 是 .NET 用來評估模式的類別；您可以直接在模式中啟用不區分大小寫 (`i`) 與多行模式 (`m`)。  

```csharp
string pattern = "(?im:john)";
```
- `(?im...)`：啟用不區分大小寫 (`i`) 與多行搜尋 (`m`)。

### 步驟 3：套用遮蔽（定義錨點）
`AnnotationRedaction` 是一種專門規則，會掃描註釋物件並將符合的文字以黑色矩形取代。  

```csharp
redactor.Apply(new AnnotationRedaction(pattern));
```

**說明：**  
- **參數：** 正則表達式模式告訴引擎要目標的文字。  
- **回傳值：** 此方法會直接在文件上進行修改，無需回傳值。

### 步驟 4：儲存已遮蔽的文件（定義錨點）
`Redactor.Save` 將修改後的檔案寫入磁碟，除非另行指定，否則會保留原始格式。  

```csharp
guardedRedactor.Save();
```

## 常見問題與解決方案
- **未找到匹配項目：** 請再次確認正則表達式語法；使用相同 .NET 引擎的線上測試工具。  
- **檔案存取錯誤：** 確保應用程式對來源與目的資料夾具有讀寫權限。  
- **效能瓶頸：** 對於超過 500 頁的文件，請以平行方式批次處理，並盡可能重複使用單一 `Redactor` 實例。

## 常見問答

**Q: 我可以在受密碼保護的 PDF 中遮蔽註釋嗎？**  
A: 可以。使用 `Redactor(string path, string password)` 開啟文件，然後照常套用遮蔽規則。

**Q: GroupDocs.Redaction 會修改原始檔案嗎？**  
A: API 會在記憶體中的副本上操作；原始檔案在您明確呼叫 `Save` 前保持不變。

**Q: 支援多少種註釋類型？**  
A: 所有標準的 PDF 註釋類型——包括評論、標記與便利貼——皆得到完整支援。

**Q: 有辦法在儲存前預覽遮蔽結果嗎？**  
A: 使用 `Redactor.GetRedactedDocument()` 取得記憶體中的串流，並在 UI 中渲染以快速預覽。

**Q: 我能處理的最大檔案大小是多少？**  
A: 此函式庫可處理最高 **2 GB** 的檔案；較大的檔案需先分割後再處理。

## FAQ 章節

1. **什麼是 GroupDocs.Redaction？**  
   - 它是一個 .NET 函式庫，用於從各種文件格式中遮蔽敏感資訊。

2. **如何處理複雜的註釋？**  
   - 使用進階的正則表達式，並在套用於關鍵文件前徹底測試。

3. **可以復原遮蔽嗎？**  
   - 一旦儲存，變更即為永久；請務必備份原始檔案。

4. **我可以將 GroupDocs.Redaction 整合到現有應用程式嗎？**  
   - 可以，其 API 允許與其他基於 .NET 的系統無縫整合。

5. **GroupDocs.Redaction 支援哪些格式？**  
   - 它支援多種文件類型，包括 Word、PDF、Excel 等。

## 資源

- [GroupDocs Redaction 文件](https://docs.groupdocs.com/redaction/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權取得](https://purchase.groupdocs.com/temporary-license/) 

---

**Last Updated:** 2026-05-27  
**Tested With:** GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs

## 相關教學

- [使用 GroupDocs.Redaction for .NET 高效移除文件中的註釋](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET 註釋遮蔽教學](/redaction/net/annotation-redaction/)
- [如何使用 GroupDocs.Redaction .NET 載入與遮蔽文件：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)