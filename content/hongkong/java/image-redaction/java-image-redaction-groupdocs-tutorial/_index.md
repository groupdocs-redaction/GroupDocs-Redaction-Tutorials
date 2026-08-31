---
date: '2026-03-22'
description: 學習如何使用 GroupDocs.Redaction 於 Java 中對掃描圖像進行遮蔽。此一步步指南涵蓋設定、圖像區域遮蔽及驗證。
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: 如何使用 GroupDocs 在 Java 中對掃描圖像進行遮蔽
type: docs
url: /zh-hant/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs 於 Java 進行掃描圖像遮蔽

在當今的數位環境中，**redact scanned image java** 對於保護隱私和符合合規要求至關重要。無論您需要在掃描合約中隱藏個人資料，或在醫療圖像中遮蔽患者資訊，本教學將示範如何使用 **GroupDocs.Redaction for Java** 快速且可靠地 **how to redact image** 內容。我們將從專案設定說明到驗證遮蔽成功的每一步，讓您能自信地將此解決方案整合至任何 Java 應用程式中。

## 快速答覆
- **什麼程式庫負責在 Java 中進行圖像遮蔽？** GroupDocs.Redaction for Java  
- **我可以選擇遮蔽顏色嗎？** 是 – 任意 `java.awt.Color`（例如 `Color.BLUE`）  
- **生產環境需要授權嗎？** 是，需要有效的 GroupDocs 授權  
- **原始圖像會被覆寫嗎？** 不會 – 您會將結果儲存為新檔案  
- **支援哪個 Java 版本？** Java 8+（相容於現代 JDK）

## 什麼是圖像遮蔽，為何要在 Java 中遮蔽掃描圖像？
圖像遮蔽指的是永久性地隱藏敏感的視覺資訊——例如姓名、編號或簽名——使其無法復原。當您處理掃描文件時，資料以像素形式嵌入，使傳統的文字遮蔽工具無法發揮作用。使用 GroupDocs.Redaction 可精確定位像素區域，並以單色取代，確保資訊徹底移除。

## 前置條件
- **JDK 8 或更新版本** 已安裝  
- **Maven**（或其他建置工具）用於相依管理  
- 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 等 IDE  
- 基本的 Java 知識與檔案 I/O 的熟悉度  

## 設定 GroupDocs.Redaction for Java

### Maven 設定
將 GroupDocs 的儲存庫與相依項目加入您的 `pom.xml`：

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
或者，從官方發行頁面下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權
- **免費試用：** 註冊試用以探索 API。  
- **臨時授權：** 使用臨時金鑰進行延長測試。  
- **完整購買：** 取得生產授權以無限制使用。  

## 實作指南

我們將實作分為兩個核心功能：**Image Area Redaction**（實際遮蔽）與 **Redaction Status Check**（驗證成功）。

### 如何遮蔽掃描文件圖像 – 步驟 1：初始化 Redactor
首先，建立指向欲處理圖像的 `Redactor` 實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 步驟 2：定義遮蔽參數
指定欲隱藏矩形的左上角 (`Point`) 與大小 (`Dimension`)。在此範例中，我們使用藍色填充。

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 步驟 3：套用遮蔽
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

### 如何驗證遮蔽 – 狀態檢查
套用遮蔽後，您可以檢查 `RedactorChangeLog` 以確認操作未失敗。

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 實務應用
- **機密文件處理：** 在將掃描合約分享給外部方之前，自動遮蔽個人資料。  
- **法律文件：** 透過遮蔽證據圖像中的識別資訊，以符合 GDPR 或 HIPAA 規範。  
- **醫療紀錄：** 透過遮蔽放射影像中的臉部或手寫筆記，保護患者隱私。  

## 效能考量
- **批次處理：** 以小批次載入與遮蔽圖像，以降低記憶體使用量。  
- **有效的資料結構：** 處理大量圖像時重複使用 `Point` 與 `Dimension` 物件。  
- **保持更新：** 定期升級至最新的 GroupDocs.Redaction 版本，以獲得效能提升與錯誤修正。  

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| **Redaction fails with `Failed` status** | 檔案路徑不正確或圖像格式不支援 | 確認圖像存在且為支援的格式（JPG、PNG、BMP）。 |
| **Output file is empty** | `redactor.save()` 在遮蔽完成前被呼叫 | 確保 `apply()` 在儲存前回傳成功狀態。 |
| **Color not applied** | 使用了透明顏色 | 選擇不透明的 `Color`（例如 `Color.BLACK` 或 `Color.BLUE`）。 |

## 常見問答

**Q: `ImageAreaRedaction` 與文字遮蔽有何差異？**  
A: `ImageAreaRedaction` 依據像素座標運作，而文字遮蔽則解析 OCR 層以定位並移除文字內容。

**Q: 我可以在單一圖像中遮蔽多個區域嗎？**  
A: 可以——在儲存前，使用不同的 `ImageAreaRedaction` 物件重複呼叫 `redactor.apply()`。

**Q: GroupDocs.Redaction 是否支援其他圖像格式，例如 TIFF？**  
A: 此函式庫支援常見的點陣格式（JPG、PNG、BMP、GIF）。若為 TIFF，請先轉換為支援的格式。

**Q: 如何自動化處理資料夾內的掃描 PDF 進行遮蔽？**  
A: 逐一遍歷從 PDF 中提取的每頁圖像，套用相同的遮蔽邏輯，然後使用 PDF 函式庫重新組合 PDF。

**Q: 有沒有方法在儲存前預覽遮蔽效果？**  
A: 您可以將 `Redactor` 渲染為 `BufferedImage`，並在 Swing 或 JavaFX UI 中顯示，於提交變更前先行預覽。

## 結論
您現在擁有一份完整、可投入生產的指南，說明如何使用 GroupDocs.Redaction for Java **how to redact image**（遮蔽圖像）內容，特別是 **redact scanned image java**（在 Java 中遮蔽掃描圖像）。依循上述步驟，您即可在各行各業保護敏感的視覺資料。探索其他 API——如文字遮蔽或 PDF 頁面遮蔽——以為貴組織打造完整的資料隱私解決方案。

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/java/)  
- [API 參考文件](https://reference.groupdocs.com/redaction/java)  
- [下載](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權](https://purchase.groupdocs.com/temporary-license/) 

---

**最後更新：** 2026-03-22  
**測試環境：** GroupDocs.Redaction 24.9（Java）  
**作者：** GroupDocs