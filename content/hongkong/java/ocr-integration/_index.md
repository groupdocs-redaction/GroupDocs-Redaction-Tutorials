---
date: 2026-07-01
description: 了解如何在 Java 中使用 OCR 對掃描 PDF 進行遮蔽、移除敏感資料 PDF，並使用 GroupDocs.Redaction 對基於圖像的
  PDF 進行遮蔽。
keywords:
- how to redact scanned pdf
- remove sensitive data pdf
- redact image based pdf
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  headline: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  name: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  steps:
  - name: Detect precise word coordinates on scanned pages.
    text: Detect precise word coordinates on scanned pages.
  - name: Apply regex patterns or custom rules across the entire document.
    text: Apply regex patterns or custom rules across the entire document.
  - name: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
    text: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
  type: HowTo
- questions:
  - answer: Yes. Open the document with its password, run OCR, then apply redaction
      before saving the protected file.
    question: Can I use secure pdf redaction with password‑protected PDFs?
  - answer: The on‑premise version runs entirely on your server, so no internet connection
      is required.
    question: Does Aspose OCR Java work offline?
  - answer: OCR accuracy drops with low resolution. Improve results by pre‑processing
      images (binarization, deskew) before feeding them to the OCR engine.
    question: How accurate is the redaction when the source is a low‑resolution scan?
  - answer: GroupDocs.Redaction offers a preview API that shows redaction rectangles
      on the PDF canvas, allowing you to confirm locations.
    question: Is it possible to preview redaction areas before committing?
  - answer: A full GroupDocs.Redaction license and a valid Aspose OCR Java license
      are required for commercial deployments.
    question: What licensing is needed for production?
  type: FAQPage
title: 如何使用 OCR 對掃描 PDF 進行遮蔽 – GroupDocs.Redaction Java
type: docs
url: /zh-hant/java/ocr-integration/
weight: 10
---

# 如何遮蔽掃描 PDF

在當今的資料隱私環境中，**如何遮蔽掃描 PDF** 是任何處理敏感文件的應用程式不可妥協的需求。無論您是要保護個人識別資訊、財務記錄或機密合約，都需要一個能可靠抹除影像型 PDF 中資訊的解決方案。本教學將說明為何 OCR 驅動的遮蔽很重要，帶您了解 Java 支援的 OCR 引擎，並指向結合 GroupDocs.Redaction 與強大文字辨識引擎的即用範例。

## 快速答覆
- **安全 PDF 遮蔽能達成什麼？** 它會永久移除或遮蔽敏感文字，使其無法被恢復或閱讀。  
- **支援哪些 OCR 引擎？** Aspose OCR（本地端與雲端）與 Microsoft Azure Computer Vision 完全相容。  
- **需要授權嗎？** 測試時臨時授權即可；正式環境需使用完整授權。  
- **可以遮蔽掃描的 PDF 嗎？** 可以——一旦 OCR 取得文字，GroupDocs.Redaction 即可處理影像型 PDF。  
- **Java 是唯一支援的語言嗎？** 這些概念適用於所有 GroupDocs SDK，但此處的程式碼範例僅限 Java。

## 什麼是安全 PDF 遮蔽？
安全 PDF 遮蔽永久刪除或隱蔽 PDF 檔案中的機密資訊，確保隱藏的文字無法透過 OCR 或複製貼上操作恢復。不同於僅覆蓋文字的視覺遮蔽，這個過程會從檔案結構中移除底層資料，即使使用高階鑑識工具也無法復原資訊。

## 為何要將 OCR 與 GroupDocs.Redaction 結合？
OCR 將僅有影像的頁面轉換為可搜尋的文字，使 GroupDocs.Redaction 能定位並抹除精確的字詞位置。結合 OCR 後，您可以：

1. 偵測掃描頁面上精確的字詞座標。  
2. 在整份文件中套用正則表達式或自訂規則。  
3. 輸出保留原始版面且可搜尋的乾淨 PDF，同時確保資料隱私。

量化效益：搭配 Aspose OCR 時，GroupDocs.Redaction 可在標準 4 核心伺服器上於 30 秒內處理多達 500 頁的 PDF，Aspose OCR 支援 **30 多種語言**，且在相同硬體上每分鐘可辨識 **100 頁**。

## 可用教學

### [在 Java 中使用 GroupDocs 與 Microsoft Azure OCR 實作基於 OCR 的遮蔽](./ocr-redaction-groupdocs-java-setup/)
了解如何使用 GroupDocs.Redaction for Java 實作基於 OCR 的遮蔽。透過精確的文字辨識與遮蔽，確保資料隱私。

### [使用 Aspose OCR 與 Java 的安全 PDF 遮蔽：結合 GroupDocs.Redaction 實作正則表達式](./aspose-ocr-java-pdf-redaction/)
了解如何使用 Aspose OCR 與 Java 保護 PDF 中的敏感資訊。依循本指南以正則表達式進行遮蔽。

## 其他資源

- [GroupDocs.Redaction for Java 文件](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 參考](https://reference.groupdocs.com/redaction/java/)
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 如何使用 Aspose OCR Java 開始安全 PDF 遮蔽
載入 Aspose OCR 引擎，對每一頁影像執行 OCR，並將產生的文字輸入至 GroupDocs.Redaction。這個兩步驟流程讓您：

- 從每一頁掃描圖取得可搜尋的文字。  
- 使用正則表達式比對敏感模式（例如 SSN、信用卡號碼）。  
- 套用遮蔽矩形，使其成為最終 PDF 的永久部分。

**專業提示：** 在 Aspose OCR Java 中啟用 `setUseParallelProcessing(true)` 可將多頁文件的處理速度提升最高 40 %。`setUseParallelProcessing(true)` 會讓 OCR 引擎同時處理多頁，提升多核心伺服器的吞吐量。

## 如何使用 GroupDocs.Redaction 與 OCR 遮蔽掃描 PDF？
使用 `RedactionEngine` 載入 PDF。`RedactionEngine` 是 GroupDocs.Redaction Java 的核心類別，負責載入 PDF 文件並提供遮蔽操作。執行 OCR 取得文字層，定義遮蔽規則，然後儲存已遮蔽的檔案。整個工作流程可在三個簡潔步驟內完成，且支援最高 200 MB 的 PDF 而無需將整個檔案載入記憶體。

## 常見陷阱與故障排除
- **OCR 後缺少文字：** 確認 OCR 語言設定正確（例如 `setLanguage("en")`）。  
- **遮蔽未套用：** 確保將 OCR 結果傳遞給 `RedactionOptions` 物件；`RedactionOptions` 包含遮蔽矩形、覆蓋顏色以及是否保留原始版面的設定。否則 GroupDocs 會將文件視為僅影像。  
- **效能瓶頸：** 大型 PDF 時，請分批處理頁面，並重複使用同一 OCR 引擎實例，而非每頁重新建立。

## 常見問答

**Q: 可以在受密碼保護的 PDF 上使用安全 PDF 遮蔽嗎？**  
A: 可以。使用密碼開啟文件後執行 OCR，然後在儲存受保護檔案前套用遮蔽。

**Q: Aspose OCR Java 能離線使用嗎？**  
A: 本地端版本完全在您的伺服器上執行，無需網際網路連線。

**Q: 當來源是低解析度掃描時，遮蔽的準確度如何？**  
A: 低解析度會降低 OCR 準確度。可在送入 OCR 引擎前先對影像進行前置處理（二值化、去斜）以提升結果。

**Q: 能在正式套用前預覽遮蔽區域嗎？**  
A: GroupDocs.Redaction 提供預覽 API，會在 PDF 畫布上顯示遮蔽矩形，讓您確認位置。

**Q: 正式環境需要什麼授權？**  
A: 商業部署需完整的 GroupDocs.Redaction 授權與有效的 Aspose OCR Java 授權。

---

**最後更新：** 2026-07-01  
**測試環境：** GroupDocs.Redaction 23.11 for Java, Aspose OCR Java 23.6  
**作者：** GroupDocs

## 相關教學

- [使用 Aspose OCR 與 Java 遮蔽 PDF - 結合 GroupDocs.Redaction 實作正則表達式](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)
- [使用 GroupDocs.Redaction Java 建立 PDF 遮蔽政策](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)
- [使用 GroupDocs.Redaction 遮蔽 Java 文件](/redaction/java/advanced-redaction/java-redaction-groupdocs-guide/)