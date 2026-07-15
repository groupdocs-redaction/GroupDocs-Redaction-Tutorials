---
date: '2026-06-01'
description: 了解如何使用 GroupDocs.Redaction for .NET 隱蔽敏感資訊以及從文件中移除註解，確保合規性與資料私隱。
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction for .NET 隱蔽敏感資訊並移除註解
type: docs
url: /zh-hant/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction for .NET 進行敏感資訊遮蔽與移除註解

在文件中管理機密資料是開發人員、稽核人員與法律團隊每日面臨的挑戰。使用 GroupDocs.Redaction for .NET **快速且可靠地遮蔽敏感資訊**，此函式庫支援超過 30 種檔案格式，且可在不將整份文件載入記憶體的情況下處理高達 2 GB 的檔案。本教學將帶您完成完整工作流程——從安裝套件到使用正規表達式移除特定註解——讓您保護個人資料，並符合 GDPR、HIPAA 等法規要求。

## 快速解答
- **GroupDocs.Redaction 的功能是什麼？** 它以程式方式移除或遮蔽文字、影像與註解，以保護私人資料。  
- **支援哪些檔案類型？** 超過 30 種格式，包括 PDF、DOCX、XLSX、PPTX 以及影像檔案。  
- **開發時需要授權嗎？** 免費試用可用於測試；正式上線需購買永久授權。  
- **能有效處理大型檔案嗎？** 可以——批次處理與串流模式可降低多百頁文件的記憶體使用量。  
- **是否相容於 .NET 6 與 .NET Core？** 完全支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5+ 與 .NET 6+。

## 什麼是「遮蔽敏感資訊」？
*遮蔽敏感資訊* 指永久移除或隱蔽文件中的個人或機密資料，使其無法再被復原。這包括姓名、身分證號碼、財務細節或任何可能識別個人的資料。執行遮蔽可確保符合 GDPR、HIPAA、CCPA 等法規，防止資料外洩，並允許安全地與外部單位分享文件。

## 為何使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction 提供 **可量化的效益**：支援 30 多種輸入與輸出格式，能在不完整載入文件的情況下處理高達 2 GB 的文件，且在標準伺服器上每分鐘可遮蔽多達 10 000 個註解。這些數據使其成為市面上效能與彈性兼具的遮蔽引擎之一。

## 前置條件
開始之前，請確認您具備以下項目：

- **GroupDocs.Redaction for .NET**（版本 20.7 或更新）。
- Visual Studio 2022 或任何相容的 IDE。
- 具備基本的 C# 知識並熟悉正規表達式。

### 必要的函式庫
- **GroupDocs.Redaction for .NET** – 透過 NuGet 安裝（請參閱安裝章節）。

### 環境設定需求
- .NET Framework 4.5+ **或** .NET Core 3.1+。
- 能存取來源文件所在的檔案系統。

## 安裝 – 如何移除註解（步驟 1）
您可以使用以下任一指令將函式庫加入專案。為了保持教學無程式碼示例，未加入程式碼區塊。

**.NET CLI:**  
在終端機執行 `dotnet add package GroupDocs.Redaction --version 20.7.*`。

**Package Manager Console:**  
執行 `Install-Package GroupDocs.Redaction -Version 20.7.*`。

**NuGet Package Manager UI:**  
搜尋 “GroupDocs.Redaction” 並點擊 **Install**。

### 取得授權
若要解鎖完整功能，請從 [GroupDocs](https://purchase.groupdocs.com/temporary-license/) 取得試用或臨時授權。正式上線時，請透過同一入口購買永久授權。

## 實作指南 – 使用正規表達式移除註解
### 概觀
本節說明如何 **移除符合特定模式的註解**——非常適合剔除員工姓名、機密備註或任何自訂標記。

### 步驟 1：準備來源與輸出檔案路徑
首先，定義輸入文件的位置以及遮蔽後檔案要儲存的資料夾。請確保輸出目錄已存在，否則操作會失敗。

*定義說明:* `Path.Combine` 是 .NET 的工具，可安全地在 Windows、Linux 與 macOS 上合併目錄與檔名。

### 步驟 2：套用正規表達式遮蔽
接著，建立一個針對符合正規表達式模式之註解的遮蔽規則。

*定義說明:* `Redactor` 是負責載入文件並套用遮蔽規則的主要類別。  
*定義說明:* `DeleteAnnotationRedaction` 是用於移除內容符合正規表達式過濾條件之註解的類別。  
*定義說明:* `SaveOptions` 讓您控制輸出檔案的寫入方式——可加入副檔名、選擇輸出格式，並停用光柵化以保留向量特性。

**直接答案:** 使用 `Redactor redactor = new Redactor(sourcePath);` 載入來源文件，加入使用正規表達式的 `DeleteAnnotationRedaction`，然後呼叫 `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`。此單行流程會移除符合的註解，並寫入新檔案而不改變原始文件。

### 步驟 3：釋放資源
請務必呼叫 `redactor.Dispose()` 或將實例包在 `using` 區塊中，以即時釋放非受管理資源。  
*定義說明:* `Dispose` 會釋放 Redactor 實例使用的非受管理資源，確保記憶體被釋放。

## 檔案路徑準備以移除註解 – 如何移除 Excel 註解
即使範例以 PDF 為主，同樣的方法亦適用於 Excel 檔案（`.xlsx`）。正確的路徑處理可避免「找不到檔案」錯誤。

*定義說明:* `PrepareOutputDirectory` 是一個輔助方法，用於檢查資料夾是否存在，若不存在則建立。

透過在不同格式間重複使用相同的工具，您可以 **移除 Excel 活頁簿、Word 文件或 PowerPoint 簡報** 的註解，且僅需極少的程式碼變更。

## 實務應用
1. **資料隱私合規** – 透過自動遮蔽個人識別資訊，以符合 GDPR、HIPAA 或 CCPA 的要求。  
2. **法律文件準備** – 在與外部單位分享合約前，移除機密註解。  
3. **企業資料管理** – 以程式方式清理內部報告，確保只有經批准的資訊離開組織。

## 效能考量 – 如何有效率地移除註解
- **有效的記憶體管理：** 在完成每個檔案的處理後立即釋放 `Redactor` 物件。  
- **批次處理：** 迭代資料夾中的文件，對每個檔案套用相同的遮蔽規則；相較於反覆開啟與關閉函式庫，可減少開銷。  
- **最佳化正規表達式：** 使用非捕獲群組並避免大量回溯的模式。例如，優先使用 `\bEmployeeID:\s*\d{4,6}\b` 而非 `.*EmployeeID.*` 以提升匹配速度。

## 常見問題與解決方案
- **大型檔案卡住：** 將文件分割為多個區段，或在 `RedactorSettings` 中提升 `MaxMemoryUsage` 設定。  
- **正規表達式未匹配：** 確認模式包含 `(?i)` 旗標以支援不分大小寫，或在嵌入前使用線上正規表達式測試工具驗證。  
- **輸出檔案覆寫原始檔案：** 請始終指定不同的輸出路徑，或使用 `SaveOptions.Suffix` 自動加上 “_redacted”。

## 常見問答 (新)
**Q: GroupDocs.Redaction 能夠在 Excel 活頁簿中遮蔽註解嗎？**  
A: 可以——透過使用 `Redactor` 載入 `.xlsx` 檔案並套用 `DeleteAnnotationRedaction` 規則，即可移除評論、備註及其他註解類型。

**Q: 如何讓正規表達式模式不分大小寫？**  
A: 在模式前加上 `(?i)`，或在建立 `DeleteAnnotationRedaction` 時使用 `RegexOptions.IgnoreCase` 旗標。

**Q: 能自訂輸出檔案名稱嗎？**  
A: 當然可以。設定 `SaveOptions.Prefix` 或 `SaveOptions.Suffix` 即可在產生的檔名之前或之後加入文字。

**Q: 原始文件在遮蔽後會發生什麼？**  
A: 原始檔案保持不變；遮蔽後的版本會依您在 `SaveOptions` 中提供的路徑儲存。

**Q: 函式庫是否支援對非常大型 PDF 進行串流處理？**  
A: 支援——GroupDocs.Redaction 可在串流模式下逐頁處理，顯著降低記憶體消耗。

## FAQ 區段
1. **如何有效處理大型文件？**  
   - 若可能，將文件分成較小的區段處理，並確保正規表達式已最佳化以提升效能。  
2. **除了 Excel，還能在其他檔案格式上使用 GroupDocs.Redaction 嗎？**  
   - 可以，它支援多種格式，包括 PDF、Word 等。  
3. **遮蔽後原始文件會怎樣？**  
   - 原始文件保持不變，除非覆寫；請始終將變更儲存至新檔案或副本。  
4. **能否使用 GroupDocs.Redaction 自訂輸出檔案名稱？**  
   - 可以，修改 `SaveOptions` 以加入自訂的副檔名或前綴。  
5. **如何確保正規表達式不分大小寫？**  
   - 在正規表達式中使用如 `(i)` 之類的修飾詞，使其不分大小寫。

## 資源
- [文件說明](https://docs.groupdocs.com/redaction/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權申請](https://purchase.groupdocs.com/temporary-license/)

依照本指南，您現在擁有一套強大的方法，可使用 GroupDocs.Redaction for .NET **遮蔽敏感資訊** 並 **移除任何支援文件類型的註解**。實作步驟、以幾個範例檔案測試，並將此邏輯整合至更大的文件處理流程，以達到最高安全性。

---

**最後更新：** 2026-06-01  
**測試環境：** GroupDocs.Redaction 20.7 for .NET  
**作者：** GroupDocs  

---

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## 相關教學

- [如何使用 GroupDocs.Redaction .NET 載入與遮蔽文件：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction for .NET 遮蔽並儲存文件：完整指南](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction 在 .NET 文件中遮蔽精確片語](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)