---
date: 2026-01-18
description: 學習如何使用 GroupDocs.Redaction for Java 在圖像和掃描文件中遮蔽 OCR 內容。提供結合 Azure 與 Aspose
  OCR 的逐步教學。
title: 如何使用 GroupDocs.Redaction Java 教程對 OCR 進行遮蔽
type: docs
url: /zh-hant/java/ocr-integration/
weight: 10
---

# 如何使用 GroupDocs.Redaction Java 進行 OCR 敏感資訊遮蔽

在本指南中，您將了解 **如何遮蔽 OCR** 嵌入於圖像和掃描檔案中的資料，使用 GroupDocs.Redaction for Java。我們將帶您了解三種強大的 OCR 引擎——Aspose.OCR On‑Premise、Aspose.OCR Cloud 以及 Microsoft Azure Computer Vision——讓您能建立安全的遮蔽工作流程，即使原始文件不是機器可讀的，也能保護敏感資訊。

## 快速解答
- **「如何遮蔽 OCR」是什麼意思？** 它指的是透過 OCR 在基於圖像的文件中定位文字，然後套用遮蔽遮罩以隱藏該文字。  
- **涵蓋哪些 OCR 服務？** Aspose.OCR（本地部署與雲端）以及 Microsoft Azure Computer Vision。  
- **我需要 GroupDocs.Redaction 授權嗎？** 是的，正式環境使用需擁有有效授權。  
- **我可以同時處理 PDF 與圖像嗎？** 當然可以——GroupDocs.Redaction 能在同一工作流程中處理兩種格式。  
- **有 Java 範例程式碼嗎？** 以下每個教學都包含可直接執行的 Java 程式碼片段。

## 如何遮蔽 OCR – 概觀
OCR 產生文字的遮蔽遵循以下三個基本步驟：

1. **提取文字**：使用 OCR 引擎從圖像或掃描的 PDF 中提取文字。  
2. **識別敏感模式**（例如 SSN、信用卡號碼），透過正則表達式或關鍵字比對。  
3. **套用遮蔽**：使用 GroupDocs.Redaction，將找到的文字替換為黑色方框、自訂圖像或覆蓋層。

此方法讓您能保護本來只能以點陣圖形式存在、無法搜尋或編輯的文件。

## 為何選擇 GroupDocs.Redaction 進行 OCR 遮蔽？
- **準確性** – 結合業界領先的 OCR 引擎與精確的遮蔽遮罩。  
- **彈性** – 支援本地部署、雲端以及 Azure 服務，讓您挑選最佳的成本效能平衡。  
- **可擴展性** – 可批次處理上千頁文件，無需人工干預。  
- **合規性** – 符合 GDPR、HIPAA 及其他資料隱私法規，確保不留下任何殘餘文字。

## 前置條件
- Java Development Kit (JDK 8 或更新版本)。  
- GroupDocs.Redaction for Java 程式庫（從以下連結下載）。  
- 所選 OCR 服務的存取憑證（Aspose Cloud API 金鑰或 Azure 訂閱金鑰）。  
- GroupDocs.Redaction 的臨時或完整授權。

## 可用教學

### [使用 GroupDocs 與 Microsoft Azure OCR 在 Java 中實作基於 OCR 的遮蔽](./ocr-redaction-groupdocs-java-setup/)
了解如何使用 GroupDocs.Redaction for Java 實作基於 OCR 的遮蔽。透過精確的文字辨識與遮蔽確保資料隱私。

### [使用 Aspose OCR 與 Java&#58; 實作正則表達式模式的 PDF 安全遮蔽](./aspose-ocr-java-pdf-redaction/)
了解如何使用 Aspose OCR 與 Java 保護 PDF 中的敏感資訊。依照本指南使用 GroupDocs.Redaction 進行正則表達式基礎的遮蔽。

## 其他資源
- [GroupDocs.Redaction for Java 文件](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 參考](https://reference.groupdocs.com/redaction/java/)
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 常見問題與解決方案
| 問題 | 解決方案 |
|-------|----------|
| OCR 回傳空文字 | 確認影像品質（≥300 dpi）以及 OCR 請求中的語言設定。 |
| 遮蔽遮罩未對齊 | 使用 `RedactionOptions.setPageNumber()` 指定正確頁碼，並調整 `RedactionArea` 座標。 |
| 大量批次處理時效能下降 | 使用平行串流處理文件，並重複使用 OCR 客戶端實例。 |

## 常見問答

**Q: 我可以在同一專案中混合使用不同的 OCR 供應商嗎？**  
A: 是的，您可以實例化多個 OCR 客戶端，並依文件類型或效能需求選擇供應商。

**Q: GroupDocs.Redaction 會在 OCR 後移除隱藏的文字層嗎？**  
A: 遮蔽過程會覆寫原始點陣圖區域，確保底層的 OCR 文字層也被移除。

**Q: 我該如何處理受密碼保護的 PDF？**  
A: 將密碼傳入 `Redactor` 建構子；程式庫會自動開啟、遮蔽並重新加密檔案。

**Q: 有沒有辦法在套用前預覽遮蔽效果？**  
A: 使用 `RedactionPreview` API 產生帶有遮蔽矩形標示的 PDF 預覽。

**Q: 推薦的正式環境授權模式為何？**  
A: 永久授權提供無限制的遮蔽次數，而訂閱模式則在擴展工作負載時提供彈性。

---

**最後更新：** 2026-01-18  
**測試環境：** GroupDocs.Redaction for Java 23.12  
**作者：** GroupDocs