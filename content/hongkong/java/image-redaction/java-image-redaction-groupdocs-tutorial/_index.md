---
date: '2025-12-29'
description: 了解如何使用 GroupDocs.Redaction for Java 對掃描文件圖像進行遮蔽。一步一步的指南，涵蓋設定、圖像區域遮蔽及驗證。
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: 如何在 Java 中使用 GroupDocs 對掃描文件圖像進行遮蔽
type: docs
url: /zh-hant/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 對掃描文件圖像進行 Redact

在當今的數位環境中，**redact scanned document** 圖像對於保護隱私和滿足合規要求至關重要。無論您需要在掃描的合約中隱藏個人資料，或在醫療圖像中遮蔽患者細節，本教學將向您展示如何使用 **GroupDocs.Redaction for Java** 快速且可靠地 **how to redact image** 內容。我們將從專案設定講解到驗證 Redact 是否成功，讓您能自信地將此解決方案整合至任何 Java 應用程式。

## 快速答案
- **什麼函式庫在 Java 中處理 image redaction？** GroupDocs.Redaction for Java  
- **我可以選擇 redaction 顏色嗎？** 是 – 任意 `java.awt.Color`（例如 `Color.BLUE`）  
- **生產環境需要授權嗎？** 是，需要有效的 GroupDocs 授權  
- **原始圖像會被覆寫嗎？** 否 – 您會將結果儲存為新檔案  
- **支援哪個 Java 版本？** Java 8+（相容於現代 JDK）

## 什麼是 image redaction，為何要 redact 掃描文件圖像？
Image redaction 指永久遮蔽敏感的視覺資訊——例如姓名、編號或簽名——使其無法復原。當您處理掃描文件時，資料以像素形式嵌入，使傳統的文字 redaction 工具無法發揮作用。使用 GroupDocs.Redaction 可讓您精確定位像素區域，並以純色取代，確保資訊徹底移除。

## 前置條件
- **JDK 8 或更新版本** 已安裝  
- **Maven**（或其他建置工具）用於相依管理  
- 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 等 IDE  
- 基本的 Java 知識與檔案 I/O 使用經驗  

## 設定 GroupDocs.Redaction for Java

### Maven 設定
將 GroupDocs 儲存庫與相依性加入您的 `pom.xml`：

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
或者，從官方發佈頁面下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權
- **Free Trial（免費試用）：** 註冊試用以探索 API。  
- **Temporary License（臨時授權）：** 使用臨時金鑰進行延長測試。  
- **Full Purchase（完整購買）：** 取得生產授權以無限制使用。  

## 實作指南

我們將實作分為兩個核心功能：**Image Area Redaction**（實際遮蔽）與 **Redaction Status Check**（驗證成功）。

### 如何 redact 掃描文件圖像 – 步驟 1：初始化 Redactor
首先，建立指向您欲處理圖像的 `Redactor` 實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 步驟 2：定義 Redaction 參數
指定要隱藏矩形的左上角 (`Point`) 與大小 (`Dimension`)。本範例使用藍色填充。

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 步驟 3：套用 Redaction
建立帶有 `RegionReplacementOptions` 的 `ImageAreaRedaction` 物件並執行。此方法會回傳 `RedactorChangeLog`，告知操作是否成功。

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### 步驟 4：釋放資源
完成後務必關閉 `Redactor`，以釋放本機資源。

```java
redactor.close();
```

### 如何驗證 Redaction – 狀態檢查
套用 Redaction 後，您可以檢查 `RedactorChangeLog` 以確認操作未失敗。

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 實務應用
- **Confidential Document Handling（機密文件處理）：** 在與外部單位共享前，自動遮蔽掃描合約中的個人資料。  
- **Legal Documentation（法律文件）：** 透過在證據圖像中 redaction 識別碼，以符合 GDPR 或 HIPAA 規範。  
- **Medical Records（醫療紀錄）：** 透過遮蔽放射圖像中的臉部或手寫註記，保護患者隱私。  

## 效能考量
- **Batch Processing（批次處理）：** 小批次載入與 redaction 圖像，以降低記憶體使用量。  
- **Efficient Data Structures（高效資料結構）：** 在處理大量圖像時重複使用 `Point` 與 `Dimension` 物件。  
- **Stay Updated（保持更新）：** 定期升級至最新的 GroupDocs.Redaction 版本，以獲得效能提升與錯誤修正。  

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| **Redaction 失敗，狀態為 `Failed`** | 檔案路徑不正確或圖像格式不支援 | 確認圖像存在且為支援的格式（JPG、PNG、BMP）。 |
| **輸出檔案為空** | `redactor.save()` 在 redaction 完成前被呼叫 | 確保 `apply()` 回傳成功狀態後再儲存。 |
| **顏色未套用** | 使用透明顏色 | 選擇不透明的 `Color`（例如 `Color.BLACK` 或 `Color.BLUE`）。 |

## 常見問答

**Q: `ImageAreaRedaction` 與文字 redaction 有何差異？**  
A: `ImageAreaRedaction` 作用於像素座標，而文字 redaction 會解析 OCR 層以定位並移除文字內容。

**Q: 我可以在單一圖像中 redaction 多個區域嗎？**  
A: 可以——在儲存前，使用不同的 `ImageAreaRedaction` 物件重複呼叫 `redactor.apply()`。

**Q: GroupDocs.Redaction 支援其他圖像格式如 TIFF 嗎？**  
A: 此函式庫支援常見的點陣格式（JPG、PNG、BMP、GIF）。若為 TIFF，請先轉換為支援的格式。

**Q: 如何自動化 redaction 整個資料夾的掃描 PDF？**  
A: 逐一遍歷從 PDF 中提取的每頁圖像，套用相同的 redaction 邏輯，然後使用 PDF 函式庫重新組合 PDF。

**Q: 有沒有方法在儲存前預覽 redaction？**  
A: 您可以將 `Redactor` 渲染為 `BufferedImage`，並在 Swing 或 JavaFX UI 中顯示，於提交變更前先行預覽。

## 結論
您現在已擁有一份完整、可投入生產的指南，說明 **how to redact image** 內容，以及如何使用 GroupDocs.Redaction for Java **redact scanned document** 圖像。依循上述步驟，即可在各行各業保護敏感的視覺資料。探索其他 API——如文字 redaction 或 PDF 頁面 redaction——以為貴組織打造完整的資料隱私解決方案。

---

**Last Updated:** 2025-12-29  
**Tested With:** GroupDocs.Redaction 24.9 (Java)  
**Author:** GroupDocs  

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/java/)  
- [API 參考](https://reference.groupdocs.com/redaction/java)  
- [下載](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 儲存庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)