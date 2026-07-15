---
date: '2026-04-26'
description: 學習如何使用 GroupDocs.Redaction 在 .NET 中自動化文件遮蔽並保存已遮蔽的檔案，以實現安全、合規的檔案處理。
keywords:
- automate document redaction
- save redacted documents
- GroupDocs.Redaction .NET
title: 使用 GroupDocs 在 .NET 中自動化文件遮蔽 – 高效套用政策
type: docs
url: /zh-hant/net/advanced-redaction/net-redaction-groupdocs-apply-policy-files/
weight: 1
---

# 在 .NET 中使用 GroupDocs 自動化文件遮蔽：高效套用政策於檔案

## 快速解答
- **「automate document redaction」是什麼意思？** 它表示使用程式碼在不需要人工介入的情況下，對檔案套用預先定義的遮蔽規則。  
- **哪個函式庫可以協助我儲存已遮蔽的文件？** GroupDocs.Redaction for .NET。  
- **我在正式環境使用是否需要授權？** 是的——完整授權會移除試用限制。  
- **我可以一次處理多種檔案類型嗎？** 當然可以——支援 PDF、Word、Excel 等多種格式。  
- **是否支援非同步處理？** 您可以將 API 呼叫包裝在 async 程式碼中，以提升可擴充性。

## 什麼是 automate document redaction？
自動化文件遮蔽是指透過程式化方式，根據您定義的一組規則，辨識並遮蔽機密資訊——例如社會安全號碼、信用卡號碼或個人識別碼。此過程在無需人工介入的情況下執行，確保一致性與速度。

## 為什麼要使用 GroupDocs.Redaction for .NET？
- **Compliance‑ready** – 符合 GDPR、HIPAA 以及其他法規。  
- **Batch processing** – 只需一個迴圈即可將相同政策套用至數百個檔案。  
- **Fine‑grained control** – 選擇要遮蔽的頁面、圖層或物件。  
- **Performance‑optimized** – 基於原生 .NET 函式庫構建，具備低記憶體開銷。

## 前置條件

在開始之前，請確保您已具備以下項目：

- **GroupDocs.Redaction for .NET**（最新 NuGet 套件）  
- .NET 開發環境（Visual Studio、VS Code 或 Rider）  
- 基本的 C# 知識以及對檔案系統操作的熟悉度  

### 必要的函式庫
- GroupDocs.Redaction for .NET（最新版本）

### 環境設定需求
- .NET 開發環境（例如 Visual Studio）  
- 基本的 C# 程式設計與檔案處理概念  

### 知識前提
- 熟悉 .NET 中的檔案系統操作  
- 了解資料遮蔽概念  

## 設定 GroupDocs.Redaction for .NET

使用您偏好的方式安裝 NuGet 套件。

**.NET CLI**

```shell
dotnet add package GroupDocs.Redaction
```

**Package Manager**

```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 套件管理員 UI**  
- 搜尋 “GroupDocs.Redaction” 並安裝最新版本。

### 取得授權

若要解鎖所有功能，請取得授權——可先使用免費試用或申請臨時授權以進行評估。正式環境部署需使用完整授權。

安裝完成後，將基本命名空間加入您的專案：

```csharp
using GroupDocs.Redaction;
// Your code setup goes here.
```

## 實作指南

### 功能 1：高效套用遮蔽政策於檔案

此範例示範如何對資料夾中的每個文件執行遮蔽政策，並將 **已遮蔽的文件** 儲存至成功或失敗的子資料夾中。

#### 步驟 1：準備輸出目錄

建立用於成功與失敗處理結果的資料夾。

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/PolicyFile.json");
var path = Path.GetDirectoryName(sourceFile);
string success_path = Path.Combine(path, "Success");
if (!Directory.Exists(success_path)) { Directory.CreateDirectory(success_path); }
string fail_path = Path.Combine(path, "Fail");
if (!Directory.Exists(fail_path)) { Directory.CreateDirectory(fail_path); }
```

#### 步驟 2：載入遮蔽政策

載入定義需遮蔽項目的 JSON 政策。

```csharp
RedactionPolicy policy = RedactionPolicy.Load(sourceFile);
```

#### 步驟 3：將遮蔽政策套用至檔案

遍歷每個檔案，套用政策，並依處理狀態儲存輸出。

```csharp
foreach (var fileEntry in Directory.GetFiles("YOUR_DOCUMENT_DIRECTORY/Inbound"))
{
    using (Redactor redactor = new Redactor(fileEntry))
    {
        // Apply the redaction policy.
        RedactorChangeLog result = redactor.Apply(policy);

        // Determine where to save the output based on processing status.
        String resultFolder = result.Status != RedactionStatus.Failed ? success_path : fail_path;
        var outputFile = Path.Combine(resultFolder, Path.GetFileName(fileEntry));

        // Save the processed file.
        using (Stream fileStream = File.Create(outputFile))
        {
            redactor.Save(fileStream, new RasterizationOptions() { Enabled = false });
        }
    }
}
```

### 功能 2：為遮蔽輸出準備目錄

上述程式碼已確保在處理任何檔案之前，輸出目錄已存在，避免執行時錯誤並保持工作流程整潔。

## 實務應用

GroupDocs.Redaction 可應用於多種實務情境：

1. **Legal Document Management** – 自動從合約中遮蔽客戶識別碼。  
2. **Financial Reporting** – 在向稽核員分享報告前遮蔽機密數字。  
3. **Healthcare Records Processing** – 移除患者識別資料，以符合 HIPAA 規範。  
4. **Government Document Sharing** – 在公開發佈的 PDF 中保護公民資料。  
5. **Human Resources Management** – 在分發內部政策時匿名化員工資訊。

## 效能考量

在擴展至大型資料集時，請留意以下建議：

- 使用非同步檔案 I/O（`FileStream` 搭配 `async/await`）以避免阻塞執行緒。  
- 及時釋放 `Redactor` 與串流物件（如 `using` 所示）。  
- 記錄處理時間與狀態，以早期發現瓶頸。  

遵循 .NET 記憶體管理最佳實踐，即使處理數千個檔案，也能保持應用程式的回應性。

## 結論

您現在已擁有完整、可投入生產的模式，使用 GroupDocs.Redaction 在 .NET 中 **自動化文件遮蔽** 並 **儲存已遮蔽的文件**。將此工作流程整合至現有管線，可大幅減少人工工作、消除人為錯誤，並符合產業法規。

**後續步驟**  
- 將 JSON 政策擴充至自訂正規表達式模式。  
- 結合訊息佇列（如 Azure Service Bus）以實現真正的非同步批次處理。  
- 探索其他 GroupDocs.Redaction 功能，例如自訂遮蔽顏色或稽核日誌。

## 常見問答

1. **What is GroupDocs.Redaction for .NET?**  
   - 一個讓開發者能對文件套用遮蔽政策的函式庫，確保機密資訊被安全遮蔽或移除。  

2. **How do I set up my development environment for using GroupDocs.Redaction?**  
   - 安裝 NuGet 套件，並針對相容的 .NET 框架版本（例如 .NET 6）進行設定。  

3. **Can I customize the redaction policy rules?**  
   - 可以，於 JSON 檔案中定義自訂規則，以明確指定需遮蔽的資料。  

4. **What file formats are supported by GroupDocs.Redaction?**  
   - 支援 PDF、Word、Excel、PowerPoint 以及其他多種常見辦公格式。  

5. **Is there any performance impact when using GroupDocs.Redaction on large files?**  
   - 效能受檔案大小與規則複雜度影響；遵循上述記憶體管理最佳實踐可降低影響。  

## 常見問題

**Q: How can I ensure the redacted output is saved in a specific folder structure?**  
A: 使用程式碼範例中 `Path.Combine` 的邏輯，將成功與失敗的檔案分別儲存至不同目錄。

**Q: Does GroupDocs.Redaction support password‑protected PDFs?**  
A: 是的——在開啟受保護文件時，將密碼傳遞給 `Redactor` 建構函式。

**Q: Can I run this process in a cloud‑native environment like Azure Functions?**  
A: 當然可以。將迴圈包裹在函式觸發器中，並使用非同步 I/O 以符合執行限制。

**Q: What if a document fails to process?**  
A: 範例程式碼會自動將失敗的檔案儲存至 *Fail* 資料夾，您可稍後檢查 `RedactorChangeLog` 以取得詳細資訊。

**Q: Is there a way to generate a report of all redactions performed?**  
A: `RedactorChangeLog` 物件包含所有已套用的遮蔽清單；您可將其序列化為 JSON 或 CSV 以作稽核用途。

## 資源

- **文件說明**: [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 參考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載 GroupDocs.Redaction**: [Releases Page](https://releases.groupdocs.com/redaction/net/)  
- **免費支援論壇**: [GroupDocs Support](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**: [Request Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-04-26  
**測試環境：** GroupDocs.Redaction 7.5（撰寫時的最新版本）  
**作者：** GroupDocs