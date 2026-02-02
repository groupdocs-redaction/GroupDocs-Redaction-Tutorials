---
date: '2026-01-16'
description: 學習如何使用 Aspose OCR、Java 及正則表達式安全地編輯 PDF 檔案。本指南將示範如何在遮蔽敏感 PDF 資料的同時，儲存已編輯的
  PDF 文件。
keywords:
- secure PDF redaction
- Aspose OCR integration Java
- regex patterns GroupDocs Redaction
title: 如何使用 Aspose OCR 與 Java 對 PDF 進行遮蔽 - 使用 GroupDocs.Redaction 實作正則表達式模式
type: docs
url: /zh-hant/java/ocr-integration/aspose-ocr-java-pdf-redaction/
weight: 1
---

# 如何使用 Aspose OCR 與 Java 進行 PDF 敏感資訊遮蔽

在當今的數位環境中，安全地 **如何遮蔽 PDF** 檔案是處理個人、財務或機密資訊的企業的首要任務。透過結合 Aspose OCR 的雲端功能與 GroupDocs.Redaction 強大的正則表達式引擎，您可以 **安全的 PDF 遮蔽**、**遮蔽敏感的 PDF 資料**，以及自動 **儲存已遮蔽的 PDF** 輸出。本教學將逐步說明從環境設定到套用基於正則表達式的遮蔽，讓您能自信地保護敏感內容。

## 快速答覆
- **本教學涵蓋什麼內容？** 在 Java 中將 Aspose OCR 與 GroupDocs.Redaction 結合，使用正則表達式模式對 PDF 進行遮蔽。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **需要哪個 Java 版本？** JDK 8 或以上。  
- **可以將結果另存為新 PDF 嗎？** 可以——使用 `SaveOptions` 來 **儲存已遮蔽的 PDF** 檔案。  
- **此解決方案適用於大型文件嗎？** 只要妥善管理記憶體並可選擇平行處理，即可良好擴展。

## 什麼是 PDF 遮蔽以及為何使用它？

PDF 遮蔽會永久移除或遮蔽文件中的機密資訊。不同於單純的隱藏，遮蔽確保資料無法被復原，因而對遵守 GDPR、HIPAA 以及 PCI‑DSS 等法規至關重要。

## 前置條件

- **GroupDocs.Redaction for Java**（用於執行遮蔽的函式庫）  
- **Aspose.OCR Cloud SDK**（雲端 OCR 引擎）  
- JDK 8 以上，及 IntelliJ IDEA 或 Eclipse 等開發環境  
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
- **臨時授權**：取得臨時授權以延長測試時間。  
- **購買**：取得正式授權以供生產環境使用。  

## 基本初始化

建立使用 Aspose OCR 連接器的 `Redactor` 實例。此步驟會讓引擎能辨識基於影像的 PDF 內文字。

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

- **說明**：此設定會產生一個黑色方框，於正則表達式匹配之處 **遮蔽敏感的 PDF 資料**。

### 實作正則表達式模式進行遮蔽

```java
RedactorChangeLog result = redactor.apply(new Redaction[] {
    new RegexRedaction("(?<=Dear\\s)([^,]+)", marker), // Cardholder name
    new RegexRedaction("\\d{2}/\\d{2}", marker), // Expiration date pattern
    new RegexRedaction("\\d{4}", marker)  // Partial card number sections
});
```

- **說明**：每個 `RegexRedaction` 物件會定義一個模式以定位個人資訊，並以先前定義的黑色標記取代。

### 儲存已遮蔽的文件

```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save(new SaveOptions(false, "AsposeOCR", "YOUR_OUTPUT_DIRECTORY"));
}
```

- **說明**：遮蔽成功後，文件會寫入磁碟，實際上 **儲存已遮蔽的 PDF**。您可透過 `SaveOptions` 更改輸出資料夾或格式。

## 實務應用

1. **金融文件安全** – 在向客戶發送對帳單前遮蔽信用卡號碼。  
2. **醫療資料保護** – 遮蔽患者識別資訊，以符合 HIPAA 規範。  
3. **企業機密** – 在內部審查合約時隱藏敏感條款。  
4. **法律文件處理** – 在分享案件檔案時確保特權資訊保持私密。  
5. **政府紀錄** – 在公開 PDF 中保護公民資料。  

## 效能考量

- **OCR 設定**：根據文件品質調整 Aspose OCR 的速度與精確度。  
- **記憶體管理**：以串流方式處理大型 PDF，避免 `OutOfMemoryError`。  
- **平行處理**：利用 Java 的 `ExecutorService` 同時遮蔽多個檔案。  

## 常見問題與除錯

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 沒有文字被遮蔽 | OCR 未偵測到文字 | 核對 OCR 服務憑證，並提升影像 DPI |
| 遮蔽方框位置錯位 | 頁面旋轉不正確 | 使用 `LoadOptions.setRotatePages(true)` |
| 大型 PDF 時應用程式當機 | 堆疊記憶體不足 | 增加 JVM `-Xmx` 參數或分批處理頁面 |

## 常見問答

**Q: 什麼是 Aspose OCR？**  
A: 一項雲端服務，可從影像中擷取文字，讓 PDF 可被搜尋。

**Q: 可以將正則表達式套用於 PDF 以外的檔案類型嗎？**  
A: 可以——GroupDocs.Redaction 支援 Word、Excel、PowerPoint 等多種格式。

**Q: 若 PDF 已是文字型別，該如何處理？**  
A: 您可以跳過 OCR 步驟，直接對文字層套用正則表達式遮蔽。

**Q: 我的正則表達式未匹配到預期資料，該怎麼辦？**  
A: 使用線上正則表達式測試工具測試模式，並確保在 Java 字串中使用正確的跳脫序列。

**Q: 在哪裡可以找到更詳細的 API 文件？**  
A: 請參閱官方文件 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)。  

## 資源

- **文件**：[GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**：[GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**：[Get Group Docs Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 倉庫**：[GroupDocs.Redaction for Java GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **支援論壇**：[GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**：[Obtain a Temporary Li  

**最後更新：** 2026-01-16  
**測試環境：** GroupDocs.Redaction 24.9、Aspose.OCR Cloud SDK（最新）  
**作者：** GroupDocs