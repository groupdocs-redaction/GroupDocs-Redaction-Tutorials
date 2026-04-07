---
date: '2026-04-07'
description: 學習如何在 .NET 中使用 GroupDocs.Redaction 進行 PDF 檔案的塗抹，移除 PDF 文字，並安全地儲存已塗抹的
  PDF。
keywords:
- how to redact pdf
- remove text pdf
- redact medical records
- save redacted pdf
title: 如何在 .NET 中使用 GroupDocs.Redaction 進行 PDF 敏感資訊遮蔽
type: docs
url: /zh-hant/net/advanced-redaction/master-custom-redaction-dotnet-groupdocs/
weight: 1
---

# 如何在 .NET 使用 GroupDocs.Redaction 進行 PDF 遮蔽

在當今快速變化的數位世界中，可靠地 **如何遮蔽 PDF** 檔案是許多開發者關心的問題。無論是保護客戶資料、從法律合約中剔除機密條款，或只是從報告中移除不需要的文字，掌握 .NET 中的 PDF 遮蔽即可讓您全面掌控隱私。本指南將逐步說明如何使用 GroupDocs.Redaction 來 **移除 PDF 文字**、**遮蔽醫療紀錄**，以及安全地 **儲存已遮蔽的 PDF** 檔案。

## 快速解答
- **什麼函式庫負責 .NET 中的 PDF 遮蔽？** GroupDocs.Redaction for .NET.  
- **我能只遮蔽特定片語嗎？** 可以 – 使用正規表達式或自訂處理程序。  
- **生產環境是否需要授權？** 需要有效的 GroupDocs 授權才能在生產環境使用。  
- **原始版面會被保留嗎？** 遮蔽引擎會在隱藏內容的同時保持頁面版面不變。  
- **如何儲存最終檔案？** 呼叫 `Redactor.Save` 並傳入 `SaveOptions` 實例即可產生已遮蔽的 PDF。

## 什麼是 PDF 遮蔽以及為何重要？
PDF 遮蔽會永久移除或遮蔽敏感資訊，使其無法復原。與單純隱藏不同，遮蔽會覆寫底層資料，確保符合 GDPR、HIPAA、PCI‑DSS 等法規。使用 GroupDocs.Redaction，您可以直接從 .NET 應用程式自動化此流程。

## 前置條件

在開始之前，請確保您具備以下項目：

- **GroupDocs.Redaction for .NET**（取得函式庫的存取權）。  
- **.NET Framework 4.6+** 或 **.NET Core 3.1+**（任何近期的 .NET 執行環境）。  
- 支援 C# 的 IDE，例如 Visual Studio 或 VS Code。  
- 具備正規表達式的基本知識以進行模式匹配。

## 設定 GroupDocs.Redaction for .NET

首先，將函式庫加入您的專案。

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 套件管理員 UI**  
搜尋 “GroupDocs.Redaction” 並安裝最新版本。

### 取得授權步驟
- **免費試用**：取得臨時授權以探索完整功能。  
- **購買**：若需長期使用，請從 [GroupDocs](https://purchase.groupdocs.com/) 購買訂閱。

套件安裝完成後，您即可建立指向欲處理 PDF 的 `Redactor` 實例。

## 使用自訂處理程序遮蔽 PDF

自訂遮蔽提供精細的控制，適用於如 **遮蔽醫療紀錄** 需要針對特定模式的情境。

### 步驟實作

#### 步驟 1：定義來源與目的地路徑
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF.pdf";
```

#### 步驟 2：建立正規表達式與取代選項  
此處使用簡單的 `.*` 模式作為示範；實際使用時請以更精確的正規表達式取代（例如 SSN、信用卡號碼）。

```csharp
Regex regex = new Regex(".*");
ReplacementOptions optionsText = new ReplacementOptions("[replaced]");
optionsText.CustomRedaction = new TextRedactor();
```

#### 步驟 3：建立遮蔽並套用  
`PageAreaRedaction` 物件將正規表達式與自訂處理程序關聯起來。

```csharp
var textRedaction = new PageAreaRedaction(regex, optionsText);
var redactions = new Redaction[] { textRedaction };

using (Redactor redactor = new Redactor(sourceFile))
{
    RedactorChangeLog result = redactor.Apply(redactions);
    if (result.Status != RedactionStatus.Failed)
    {
        var outputFile = redactor.Save(new Options.SaveOptions(false, "Custom_Redaction_Result"));
        // Output file saved to YOUR_OUTPUT_DIRECTORY.
    }
    else
    {
        Console.WriteLine("Custom redaction failed");
    }
}
```

#### 步驟 4：實作自訂遮蔽處理程序  
此處理程序允許您依需求精確地重新寫入匹配的文字。

```csharp
public class TextRedactor : ICustomRedactionHandler
{
    public CustomRedactionResult Redact(CustomRedactionContext context)
    {
        CustomRedactionResult result = new CustomRedactionResult();
        
        try
        {
            Regex regex = new Regex(@"Lorem ipsum");
            if (regex.IsMatch(context.Text))
            {
                string redactedText = regex.Replace(context.Text, "[redacted‑custom]");
                result.Apply = true;
                result.Text = redactedText;
            }
        }
        catch (System.Exception ex)
        {
            result.Apply = false;
        }

        return result;
    }
}
```

### 為何使用自訂處理程序？
- **精確度** – 僅針對您需要的確切片語。  
- **彈性** – 可將文字替換為自訂字串、遮蔽或甚至圖片。  
- **合規** – 確保已移除的資料無法復原，符合相關法規標準。

#### 疑難排解提示
- 仔細檢查正規表達式語法；微小的錯誤可能會導致漏掉目標文字。  
- 確認應用程式對來源與輸出資料夾具備讀寫權限。  
- 使用 `RedactorChangeLog` 檢查哪些頁面已被修改。

## 實務使用案例

| 情境 | 遮蔽的好處 |
|----------|---------------------|
| **法律文件** | 在分享前隱藏客戶姓名、案件編號或機密條款。 |
| **財務報告** | 移除帳號、餘額或專有公式。 |
| **醫療紀錄** | **遮蔽醫療紀錄** 以符合 HIPAA，並在分享案例研究時使用。 |
| **公司備忘錄** | 從外部傳送的 PDF 中剔除內部專案代碼或密碼。 |
| **文件管理系統** | 在大型文件庫中自動執行隱私保護。 |

## 效能考量

- **分段處理** – 對於非常大的 PDF，分批處理頁面以降低記憶體使用。  
- **高效正規表達式** – 優先使用已編譯的正規表達式 (`new Regex(pattern, RegexOptions.Compiled)`) 以加速匹配。  
- **即時釋放** – 如示範般將 `Redactor` 包於 `using` 區塊，以立即釋放檔案句柄。  

## 結論

現在您已擁有完整、可投入生產的 **如何在 .NET 使用 GroupDocs.Redaction 進行 PDF 遮蔽** 工作流程。透過自訂處理程序，您可以 **移除 PDF 文字**、**遮蔽醫療紀錄**，以及 **儲存已遮蔽的 PDF**，滿足嚴格的隱私需求。

### 後續步驟
- 深入了解 [GroupDocs 文件](https://docs.groupdocs.com/redaction/net/)。  
- 嘗試更複雜的正規表達式模式（例如信用卡號碼、電子郵件地址）。  
- 將遮蔽服務整合至您現有的文件管理流程中。

## 常見問題

**Q: 我能遮蔽受密碼保護的 PDF 嗎？**  
A: 可以。在建立 `Redactor` 實例前，先使用相應的密碼開啟文件。

**Q: GroupDocs.Redaction 是否支援圖片遮蔽？**  
A: 當然可以。您可以同時定義基於圖片的遮蔽區域與文字遮蔽。

**Q: 如何確保已遮蔽的 PDF 符合 HIPAA？**  
A: 使用自訂處理程序針對 PHI 模式、檢查 `RedactorChangeLog`，並保留遮蔽操作的稽核日誌。

**Q: 若需自動遮蔽數千份 PDF 該怎麼辦？**  
A: 建置批次處理器，遍歷檔案、套用相同的遮蔽規則，並將結果寫入指定的輸出資料夾。

**Q: 有沒有方法在儲存前預覽遮蔽效果？**  
A: 您可以呼叫 `Redactor.GetRedactionPreview()`（較新版本提供）以產生每頁的預覽圖像。

## 資源
- **文件**： [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 參考**： [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載**： [GroupDocs Releases](https://releases.groupdocs.com/redaction/net/)  
- **免費支援**： [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**： [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-04-07  
**測試環境：** GroupDocs.Redaction 23.7 for .NET  
**作者：** GroupDocs