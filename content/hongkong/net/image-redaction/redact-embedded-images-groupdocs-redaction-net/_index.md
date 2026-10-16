---
date: '2026-10-16'
description: 了解如何使用 GroupDocs 及 GroupDocs.Redaction .NET API 在 Word 文件中遮蔽嵌入式圖像，確保敏感資料安全。
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: 如何使用 GroupDocs 以 .NET API 在 Word 文件中遮蔽嵌入式圖像。快速且可靠地保護機密視覺內容。
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: 如何使用 GroupDocs 於 Word 中以 .NET 遮蔽圖像
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: 如何使用 GroupDocs 於 Word 中以 .NET 遮蔽圖像
type: docs
url: /zh-hant/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 .NET 中使用 GroupDocs 對 Word 中的圖像進行遮蔽

當您需要保護 Microsoft Word 檔案中的機密視覺資訊時，**如何使用 GroupDocs** 成為首要問題。本教學將逐步說明如何定位、遮蔽並永久移除嵌入的圖片，確保敏感資訊不會外洩。

## 快速回答
- **GroupDocs 能自動遮蔽所有圖像嗎？** 是的，您可以遍歷每張圖片並套用 `ImageAreaRedaction`。
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。
- **開發需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。
- **會保留原始版面配置嗎？** API 會在清除圖像區域的同時保持文字與格式不變。
- **處理速度如何？** GroupDocs.Redaction 在一般伺服器上可於 2 秒內處理 200 頁文件。

## GroupDocs.Redaction 是什麼？
GroupDocs.Redaction 是一套 .NET 函式庫，可程式化遮蔽文字、圖像與中繼資料，支援超過 20 種文件格式。它在不需要安裝 Microsoft Office 的情況下處理檔案，非常適合伺服器端自動化。提供遮蔽文字、圖像與中繼資料的 API，支援批次處理、自訂遮蔽模式與合規報告。

## 為何在 Word 中使用 GroupDocs 進行圖像遮蔽？
此函式庫支援 **20+ 輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下，處理高達 500 MB 的文件。內建的 `ImageAreaRedaction` 演算法保證遮蔽區域無法復原，符合嚴格的合規標準。

## 前置條件
- 已安裝 .NET Framework 4.5+ **或** .NET Core 3.1+。
- 基本的 C# 知識以及對 Word 檔案結構的了解。
- 取得 **GroupDocs.Redaction** NuGet 套件（免費試用或已授權）。

## 如何在 .NET 中設定 GroupDocs.Redaction

### 如何透過 .NET CLI 安裝 GroupDocs.Redaction？
在專案資料夾中執行以下指令：`dotnet add package GroupDocs.Redaction`。此指令會將最新的穩定版加入您的專案檔。

```bash
dotnet add package GroupDocs.Redaction
```

### 如何使用 Package Manager 安裝 GroupDocs.Redaction？
在 Package Manager Console 中執行 `Install-Package GroupDocs.Redaction`。

```powershell
Install-Package GroupDocs.Redaction
```

### 如何取得並套用臨時授權？
您可以從 [Temporary License](https://purchase.groupdocs.com/temporary-license/) 頁面申請臨時授權。  
臨時授權允許您在無浮水印的情況下評估完整功能。購買後，將授權檔案放置於專案中，並依下列方式載入：

```csharp
using GroupDocs.Redaction;
```

## 如何在 Word 文件中遮蔽嵌入圖像？

要遮蔽圖像，您需要使用 Redactor 實例載入文件，定位每張圖片，定義要隱藏的區域，然後套用 ImageAreaRedaction。API 會覆寫選取的像素，確保原始視覺內容無法復原，同時保留周圍的版面與文字。

### 如何準備來源與輸出路徑？
在建立任何物件之前，先為原始文件與遮蔽結果定義絕對路徑。

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### 如何建立與設定 Redactor 物件？
Redactor 是負責載入文件並執行遮蔽操作的核心類別。  
使用您的文件建立 `Redactor` 實例：

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### 如何指定座標並套用圖像區域遮蔽？
ImageAreaRedaction 是一個將圖像矩形區域以純色遮蔽的方法。  
先找出左上角點 (`samplePoint`) 與欲隱藏區域的大小 (`sampleSize`)，然後呼叫 `ImageAreaRedaction`。此方法會以純色覆寫選取的像素。

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### 如何驗證遮蔽結果並儲存檔案？
呼叫 `Redactor.Apply()` 後，檢查 `Result` 物件。若 `IsSuccess` 為 true，將修改後的文件寫入輸出路徑。

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## 常見問題與故障排除技巧
- **座標錯誤：** 確認 X/Y 值在圖像範圍內；否則 API 會拋出 `ArgumentOutOfRangeException`。
- **缺少授權：** 試用授權在 30 天後過期；請換成永久授權以避免執行時錯誤。
- **不支援的格式：** 請確認檔案副檔名屬於文件中列出的 20 多種格式；較舊的 `.doc` 可能需先轉換為 `.docx`。

## 實務應用
1. **機密報告：** 在對外發佈前遮蔽標誌或圖表。  
2. **法律簡報：** 隱藏包含個人資料的客戶照片或掃描身分證。  
3. **商業合約：** 馬賽克處理顯示商業機密的專有圖示。  
4. **政府發布：** 從由 Word 產生的公開 PDF 中移除敏感的衛星影像。

## 效能考量
- 在處理大量批次時，請順序處理文件以降低記憶體使用。  
- 若在資源受限的伺服器上執行，可使用 `RedactorOptions` 限制執行緒數量。  
- 盡快使用 `using` 釋放 `Redactor` 實例，以釋放非受控資源。

## 結論
您現在已了解 **如何使用 GroupDocs** 可靠地遮蔽 Word 檔案中的嵌入圖像，並透過 .NET API 完成。依循上述步驟，您可以將此功能整合至任何文件處理流程，確保機密視覺資訊不會離開組織。

如需更深入的探索，可嘗試其他遮蔽類型（文字、元資料），並將函式庫整合至 Web 服務、背景工作或 Azure Functions。

## 常見問答

**Q: 我可以一次遮蔽多張圖片嗎？**  
A: 可以，遍歷每個圖片節點，對每個需要隱藏的區域呼叫 `ImageAreaRedaction`。

**Q: GroupDocs.Redaction 支援受密碼保護的 Word 檔案嗎？**  
A: 完全支援。建立 `Redactor` 物件時提供密碼，函式庫會安全開啟文件。

**Q: 除了 DOCX，我還能處理哪些檔案格式？**  
A: API 支援 DOC、DOCX、RTF、HTML、PDF 等超過 20 種格式，讓您能建構通用的遮蔽服務。

**Q: 沒有授權我該如何測試遮蔽功能？**  
A: 使用 GroupDocs 入口網站提供的臨時授權；可在 30 天內完整使用功能且不會出現浮水印。

**Q: 若遇到問題，我該向哪裡尋求協助？**  
A: 前往 [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) 論壇尋求社群協助，或聯絡 GroupDocs 銷售團隊取得企業支援。

## 其他資源

- **文件說明：** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **API 參考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **下載：** [Latest Releases](https://releases.groupdocs.com/redaction/net/)

---

**最後更新:** 2026-10-16  
**測試環境:** GroupDocs.Redaction 23.12 for .NET  
**作者:** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Redaction .NET 進行文件遮蔽 – 完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [遮蔽與儲存文件 Groupdocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [精通大小寫敏感精確片語遮蔽 – 使用 GroupDocs.Redaction .NET 保障文件安全](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}