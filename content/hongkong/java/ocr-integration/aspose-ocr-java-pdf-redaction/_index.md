---
date: '2026-04-20'
description: 學習如何使用 Aspose OCR、Java 及正則表達式安全地遮蔽 PDF 檔案。本指南示範如何在遮蔽敏感 PDF 資料的同時，儲存已遮蔽的
  PDF 文件。
keywords:
- how to redact pdf
- save redacted pdf
- java pdf ocr
- secure pdf redaction
- pdf redaction java
title: 如何使用 Aspose OCR 與 Java 對 PDF 進行遮蔽 - 使用 GroupDocs.Redaction 實作正則表達式模式
type: docs
url: /zh-hant/java/ocr-integration/aspose-ocr-java-pdf-redaction/
weight: 1
---

# 如何使用 Aspose OCR 與 Java 馬賽克 PDF

在當今的數位環境中，安全地 **how to redact PDF** 檔案是處理個人、財務或機密資訊的企業的首要任務。透過結合 Aspose OCR 的雲端功能與 GroupDocs.Redaction 強大的正則表達式引擎，您可以 **secure PDF redaction**、**mask sensitive PDF data**，以及自動 **save redacted PDF** 輸出。本教學將逐步說明從設定環境到套用基於正則表達式的馬賽克的每個步驟，讓您能自信地保護敏感內容。

## 快速回答
- **本教學涵蓋什麼內容？** 在 Java 中將 Aspose OCR 與 GroupDocs.Redaction 結合，使用正則表達式模式對 PDF 進行馬賽克。  
- **我需要授權嗎？** 免費試用可用於評估；正式上線需購買永久授權。  
- **需要哪個 Java 版本？** JDK 8 或以上。  
- **我可以將結果另存為新 PDF 嗎？** 可以——使用 `SaveOptions` 來 **save redacted PDF** 檔案。  
- **此解決方案適用於大型文件嗎？** 透過適當的記憶體管理與可選的平行處理，具備良好擴展性。  

## 什麼是 PDF 馬賽克以及為何使用它？
PDF 馬賽克會永久移除或遮蔽文件中的機密資訊。與單純隱藏不同，馬賽克確保資料無法被復原，因而對遵循 GDPR、HIPAA 以及 PCI‑DSS 等法規至關重要。

## 為何在 Java 中使用安全的 PDF 馬賽克？
- **自動化就緒**：將馬賽克嵌入批次作業或 Web 服務中。  
- **支援 OCR**：即時處理掃描的影像型 PDF。  
- **正則表達式強大**：針對信用卡號碼、日期或自訂識別碼等模式。  
- **跨平台**：在 Windows、Linux 與 macOS 上皆可使用相同的 Java 程式碼。  

## 前置條件
- **GroupDocs.Redaction for Java**（用於套用馬賽克的函式庫）  
- **Aspose.OCR Cloud SDK**（雲端 OCR 引擎）  
- JDK 8 以上，並使用如 IntelliJ IDEA 或 Eclipse 的 IDE  
- 具備 Java、Maven 與正則表達式的基礎知識  

## 設定 GroupDocs.Redaction for Java

您可以透過 Maven 或直接下載 JAR 檔案將函式庫加入專案。

### 使用 Maven

在您的 `pom.xml` 檔案中加入以下設定：

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### 直接下載

或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權步驟
- **免費試用**：先使用免費試用版以探索功能。  
- **臨時授權**：取得臨時授權以進行更長時間的測試。  
- **購買**：購買完整授權以供正式使用。  

## 基本初始化

建立使用 Aspose OCR 連接器的 `Redactor` 實例。此步驟會準備引擎以辨識影像型 PDF 內的文字。

```java
RedactorSettings settings = new RedactorSettings(new AsposeCloudOcrConnector());
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_4OCR", new LoadOptions(), settings)) {
    // Your code will go here...
}
```

## 實作指南

### 使用 Aspose OCR 連接器初始化設定

```java
RedactorSettings settings = new RedactorSettings(new AsposeCloudOcrConnector());
```

- **目的**：將 GroupDocs.Redaction 連接至 Aspose 的 OCR 服務，使掃描影像內的文字可被搜尋。

### 定義取代選項（遮蔽）

```java
ReplacementOptions marker = new ReplacementOptions(java.awt.Color.BLACK);
```

- **說明**：此設定會產生一個黑色方框，於任何正則表達式匹配處 **mask sensitive PDF data**。

### 實作正則表達式模式以進行馬賽克

```java
RedactorChangeLog result = redactor.apply(new Redaction[] {
    new RegexRedaction("(?<=Dear\\s)([^,]+)", marker), // Cardholder name
    new RegexRedaction("\\d{2}/\\d{2}", marker), // Expiration date pattern
    new RegexRedaction("\\d{4}", marker)  // Partial card number sections
});
```

- **說明**：每個 `RegexRedaction` 物件定義一個用於定位個人資訊的模式，並以上述的黑色標記取代。

### 儲存已馬賽克的文件

```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save(new SaveOptions(false, "AsposeOCR", "YOUR_OUTPUT_DIRECTORY"));
}
```

- **說明**：當馬賽克成功時，文件會寫入磁碟，實際上 **saving the redacted PDF**。您可透過 `SaveOptions` 更改輸出資料夾或格式。

## 實務應用
1. **金融文件安全** – 在向客戶發送對帳單前遮蔽信用卡號碼。  
2. **醫療資料保護** – 馬賽克患者識別資訊，以符合 HIPAA 規範。  
3. **企業機密** – 在內部審查合約時隱藏敏感條款。  
4. **法律文件處理** – 分享案件檔案時確保特權資訊保持私密。  
5. **政府紀錄** – 保護公共 PDF 中的公民資料。  

## 效能建議與記憶體管理
- **OCR 設定**：選擇適當的語言套件與 DPI；較高的 DPI 可提升準確度，但會佔用更多記憶體。  
- **串流處理**：對於超過 100 MB 的 PDF，採用串流方式處理頁面，以避免 `OutOfMemoryError`。  
- **平行馬賽克**：使用 Java 的 `ExecutorService` 同時對多個檔案進行馬賽克，但需監控堆積使用情況。  

## 常見問題與故障排除

| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| 未進行任何文字馬賽克 | OCR 未偵測到文字 | 確認 OCR 服務憑證，並提高影像 DPI |
| 馬賽克框位置錯位 | 頁面旋轉不正確 | 使用 `LoadOptions.setRotatePages(true)` |
| 大型 PDF 時應用程式當機 | 堆積記憶體不足 | 增加 JVM `-Xmx` 參數或分批處理頁面 |

## 常見問答

**Q: 什麼是 Aspose OCR？**  
A: 雲端服務，可從影像中擷取文字，實現可搜尋的 PDF 處理。

**Q: 我可以將正則表達式套用於非 PDF 的檔案類型嗎？**  
A: 可以——GroupDocs.Redaction 支援 Word、Excel、PowerPoint 等多種格式。

**Q: 如何處理已是文字型的 PDF？**  
A: 您可以跳過 OCR 步驟，直接對文字層套用正則表達式馬賽克。

**Q: 我的正則表達式未匹配到預期資料，該怎麼辦？**  
A: 使用線上正則表達式測試工具測試模式，並確保在 Java 字串中正確轉義反斜線。

**Q: 我可以在哪裡找到更詳細的 API 文件？**  
A: 請參閱官方文件於 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)。

## 其他資源
- **文件**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)
- **API 參考**: [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)
- **下載**: [Get Group Docs Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- **GitHub 程式庫**: [GroupDocs.Redaction for Java GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- **支援論壇**: [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
- **臨時授權**: [Obtain a Temporary Li

---

**最後更新：** 2026-04-20  
**測試環境：** GroupDocs.Redaction 24.9, Aspose.OCR Cloud SDK (latest)  
**作者：** GroupDocs