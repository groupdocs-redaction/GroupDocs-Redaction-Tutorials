---
date: 2026-03-06
description: 了解如何使用 GroupDocs.Redaction for .NET 建立遮蔽政策、遮蔽資料以及刪除文件元資料。
title: 使用 GroupDocs.Redaction .NET 建立遮蔽政策
type: docs
url: /zh-hant/net/advanced-redaction/
weight: 9
---

# 使用 GroupDocs.Redaction .NET 建立遮蔽政策

在本完整指南中，您將了解 **如何建立遮蔽政策** 物件，讓您能自動移除 PDF、Word 檔案、影像等中的敏感內容。無論您需要遵循 GDPR、HIPAA 或內部安全標準，精通 GroupDocs.Redaction for .NET 的遮蔽政策都能讓您細緻掌控哪些資訊會被隱藏、如何隱藏，甚至如何抹除中繼資料。我們將說明原因、概念與逐步流程，讓您立即開始構建穩健的文件隱私解決方案。

## 快速回答
- **什麼是遮蔽政策？** 一套可重複使用的規則，定義要從文件中移除哪些文字、影像或中繼資料。  
- **為什麼要建立遮蔽政策？** 讓您在多個檔案上套用一致且可重複的資料保護規則，而無需每次重新編寫程式碼。  
- **我可以使用 AI 來定位敏感資料嗎？** 可以——GroupDocs.Redaction 支援 **ai document redaction** 整合，能自動找出個人識別資訊。  
- **如何抹除文件中繼資料？** 在您的政策中加入「erase document metadata」規則，即可去除作者、建立日期及隱藏屬性。  
- **我需要授權嗎？** 正式使用時需具備有效的 GroupDocs.Redaction 授權；測試時可使用臨時授權。

## 什麼是遮蔽政策？

遮蔽政策是一組遮蔽項目的集合——例如精確片語、正規表達式模式或中繼資料欄位——引擎會自動套用。只要定義一次政策，即可在多個文件間重複使用，確保資料隱私處理的一致性。

## 為什麼使用 GroupDocs.Redaction 來建立遮蔽政策？

- **集中式控制：** 一個政策，套用於多個文件。  
- **可擴充的安全性：** 處理大量批次時無需人工介入。  
- **AI 輔助偵測：** 利用 **ai document redaction** 自動標記個人可識別資訊 (PII)。  
- **中繼資料抹除：** 內建支援 **erase document metadata**，保護可能被洩漏的隱藏資訊。  
- **可擴充性：** 結合自訂處理程式、回呼與記錄功能，以支援複雜工作流程。

## 如何在 GroupDocs.Redaction .NET 中建立遮蔽政策

以下是一個簡潔、對話式的操作說明。本段落不需要程式碼區塊，因為原始教學未包含範例程式碼，我們必須保持程式碼區塊的數量不變。

1. **新增 NuGet 套件**  
   透過 NuGet 套件管理員或指令列 (`dotnet add package GroupDocs.Redaction`) 安裝最新的 `GroupDocs.Redaction` 套件。  

2. **實例化 RedactionEngine**  
   建立指向您想保護之文件的 `RedactionEngine` 實例。  

3. **定義遮蔽項目**  
   - 使用 `ExactPhraseRedaction` 針對固定字串（例如「Social Security Number」）。  
   - 使用 `RegexRedaction` 針對模式（例如信用卡號碼）。  
   - 加入 `MetadataRedaction` 項目，以 **erase document metadata** 方式抹除作者或建立日期等資訊。  

4. **將項目組合成政策**  
   將遮蔽項目聚合為 `RedactionPolicy` 物件。此政策可儲存至磁碟 (`policy.Save("MyPolicy.xml")`) 並於日後載入重複使用。  

5. **套用政策**  
   呼叫 `engine.ApplyPolicy(policy)` 以處理文件。引擎會遮蔽所有符合的內容並去除指定的中繼資料。  

6. **儲存已遮蔽的文件**  
   使用 `engine.Save("RedactedFile.pdf")` 將清理後的檔案寫入儲存空間。  

### 如何使用政策遮蔽資料

當您在特定情境下需要 **how to redact data**（例如在一批人力資源 PDF 中遮蔽員工編號）時，只需載入已儲存的政策並套用於每個檔案。這樣可省去重複的程式碼，並確保每份文件遵循相同的安全規則。

### 整合 AI 輔助遮蔽

若您的專案需要智慧偵測 PII，可將 AI 服務（例如 Azure Cognitive Services、AWS Comprehend）接入回呼機制。回呼可在引擎執行前，將 AI 識別的位置回傳至政策，讓您在不更改核心工作流程的情況下，獲得強大的 **ai document redaction** 功能。

## 常見使用情境
- **合規報告：** 在分享報告前自動移除患者姓名、醫療紀錄號碼或金融識別碼。  
- **法律發現：** 從大型文件集合中剔除機密條款與客戶識別資訊。  
- **文件出版：** 在公開發佈前，透過抹除作者註記、評論與隱藏中繼資料，清理草稿。  

## 提示與最佳實踐
- **專業提示：** 將政策存放於版本控制的儲存庫，以便隨時間審核變更。  
- **警告：** 請先在文件副本上測試政策；遮蔽是不可逆的。  
- **效能提示：** 使用非同步呼叫批次處理檔案，以提升大型資料集的吞吐量。  

## 可用教學

### [如何使用 GroupDocs.Redaction .NET&#58; 建立遮蔽政策：一步步指南](./groupdocs-redaction-net-create-save-policy/)
了解如何使用 GroupDocs.Redaction for .NET 建立並儲存自訂遮蔽政策。透過有效遮蔽敏感資訊，保護您的文件安全。

### [在 GroupDocs.Redaction for .NET 中實作自訂記錄&#58; 完整指南](./custom-logging-groupdocs-redaction-net/)
了解如何在 GroupDocs.Redaction for .NET 中實作自訂記錄，以強化文件遮蔽工作流程。探索實用步驟與關鍵功能。

### [在 GroupDocs.Redaction .NET 中實作 IRedactionCallback 以使用 C# 進行安全文件遮蔽](./groupdocs-redaction-net-implement-iredactioncallback-csharp/)
了解如何使用 GroupDocs.Redaction .NET 實作 IRedactionCallback 介面，以實現安全且高效的文件遮蔽工作流程。發掘最佳實踐與實務應用。

### [精通 .NET 遮蔽與 GroupDocs&#58; 高效套用政策至檔案](./net-redaction-groupdocs-apply-policy-files/)
了解如何使用 GroupDocs.Redaction 在 .NET 中自動化遮蔽，確保檔案的資料隱私與合規性。

### [精通 .NET 中的自訂遮蔽與 GroupDocs&#58; 完整指南](./master-custom-redaction-dotnet-groupdocs/)
了解如何使用 GroupDocs.Redaction for .NET 保護文件中的敏感資訊。輕鬆實作自訂遮蔽，確保文件隱私。

### [精通 .NET 中的文件遮蔽與 GroupDocs.Redaction&#58; 完整指南](./master-document-redaction-groupdocs-redaction-net/)
了解如何使用 GroupDocs.Redaction for .NET 保護您的敏感文件。本指南涵蓋設定、遮蔽技術與最佳實踐。

### [精通 .NET 中的文件遮蔽與 GroupDocs.Redaction&#58; 步驟指南](./mastering-document-redaction-dotnet-groupdocs-redaction/)
了解如何在 .NET 中使用 GroupDocs.Redaction 實作安全的文件遮蔽。本指南涵蓋開發者的自訂格式處理程式與精確片語遮蔽。

### [精通文件安全與 GroupDocs.Redaction .NET&#58; 片語與中繼資料遮蔽完整指南](./groupdocs-redaction-net-document-security-guide/)
了解如何使用 GroupDocs.Redaction for .NET 保護敏感文件。本指南涵蓋精確片語、正規表達式遮蔽、註解刪除與中繼資料抹除。

## 其他資源

- [GroupDocs.Redaction for Net 文件說明](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 參考](https://reference.groupdocs.com/redaction/net/)
- [下載 GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 常見問題

**Q: 我可以將多個遮蔽政策合併嗎？**  
A: 可以，您可以以程式方式合併政策，或在套用至文件前依序載入多個政策檔案。

**Q: GroupDocs.Redaction 支援遮蔽掃描圖像嗎？**  
A: 支援，當搭配 OCR 時，OCR 引擎會提取文字，然後可使用相同的政策規則進行遮蔽。

**Q: 「erase document metadata」與一般遮蔽有何不同？**  
A: 中繼資料遮蔽會移除隱藏屬性（作者、時間戳記、自訂欄位），這些資訊在文件內容中不可見，但仍可能洩漏敏感資料。

**Q: AI 輔助遮蔽的準確度足以符合合規需求嗎？**  
A: AI 模型能提供良好的初步篩選；但仍建議檢查標記的項目，特別是在高風險合規情境下。

**Q: 支援哪些 .NET 版本？**  
A: GroupDocs.Redaction .NET 可在 .NET Framework 4.6.1 以上、.NET Core 3.1 以上，以及 .NET 5/6 以上環境運行。

---

**最後更新：** 2026-03-06  
**測試環境：** GroupDocs.Redaction 2.0 for .NET  
**作者：** GroupDocs