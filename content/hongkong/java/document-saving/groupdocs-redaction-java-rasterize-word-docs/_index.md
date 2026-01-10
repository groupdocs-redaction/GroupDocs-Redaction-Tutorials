---
date: '2025-12-21'
description: 學習如何將 docx 轉換為圖像，並使用 GroupDocs Redaction for Java 進行 Word 檔案的遮蔽。一步一步的指南，涵蓋光柵化、圖像區域遮蔽以及
  Maven 設定。
keywords:
- GroupDocs Redaction Java
- Word document rasterization
- secure redaction
title: 如何使用 GroupDocs Redaction Java 將 DOCX 轉換為影像並遮蔽 Word 文件
type: docs
url: /zh-hant/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/
weight: 1
---

# 轉換 DOCX 為圖像並使用 GroupDocs Redaction Java 對 Word 文件進行遮蔽

保護 Microsoft Word 檔案中的敏感資訊是開發以文件為中心的應用程式的開發人員每天面臨的挑戰。無論您需要隱藏個人資料、遵守 GDPR，或是為外部審閱準備法律合約，**在遮蔽前先將 docx 轉換為圖像** 都能確保原始版面保持完整，同時內容得到安全遮蔽。

在本教學中您將學會：

- **Convert DOCX to image** 透過使用 GroupDocs Redaction for Java 將 Word 文件光柵化。  
- 在光柵化的 PDF 上套用 **image area redaction** 以隱藏文字或圖形。  
- 設定 **GroupDocs Maven dependency** 並管理授權。  

讓我們一步步走過完整流程，從環境準備到最終文件儲存。

## 快速解答
- **What does “convert docx to image” mean?** 它會將 Word 檔案的每一頁光柵化為位圖，保留版面以確保可靠的遮蔽。  
- **Which Maven artifact is required?** `com.groupdocs:groupdocs-redaction`（請參閱 *groupdocs maven dependency* 章節）。  
- **Can I hide text in Java?** 可以——使用 `ImageAreaRedaction` 搭配 `RegionReplacementOptions` 來覆蓋實心顏色。  
- **Do I need a license?** 試用授權可用於評估；正式環境需購買商業授權。  
- **Is the output a PDF or an image file?** 光柵化步驟會產生 PDF，且每頁皆為圖像，已可進行遮蔽。

## 什麼是 “convert docx to image”？
將 DOCX 檔案光柵化會將每一頁轉換為圖像（通常嵌入於 PDF 中）。此轉換會移除可選取的文字，使後續的遮蔽不可逆且防篡改。

## 為什麼使用 GroupDocs Redaction for Java？
- **Accurate layout preservation** – 原始 Word 格式保持完全相同。  
- **Fine‑grained redaction** – 您可以針對特定區域、圖像或整頁進行遮蔽。  
- **Seamless Maven integration** – *groupdocs maven dependency* 輕量且定期更新。  
- **Cross‑platform support** – 可在任何支援 Java 8+ 的作業系統上執行。

## 前置條件
- 已安裝 JDK 8 或更新版本。  
- 使用 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。  
- 具備網路連線以下載 Maven 套件或直接取得 JAR。  
- 具備基本的 Java 知識並熟悉 Maven。

## 設定 GroupDocs.Redaction for Java

### Maven 依賴項（groupdocs maven dependency）

將官方 GroupDocs 儲存庫與 Redaction 函式庫加入您的 `pom.xml`：

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

**Direct Download** – 若您不想使用 Maven，可從官方頁面下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權
1. 從 GroupDocs 入口網站申請 **免費試用授權**。  
2. 若於正式環境部署，請購買 **商業授權**，並以永久金鑰取代試用金鑰。

## 步驟說明

### 步驟 1：匯入必要類別（如何光柵化 Word）

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.RasterizationOptions;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.nio.file.Files;
import java.nio.file.Paths;
```

### 步驟 2：載入並光柵化 DOCX（convert docx to image）

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
ByteArrayOutputStream stream = new ByteArrayOutputStream();

try (Redactor rasterizer = new Redactor(inputFilePath)) {
    // Enable rasterization options.
    RasterizationOptions options = new RasterizationOptions();
    options.setEnabled(true);
    
    // Save the document as a byte array in rasterized form.
    rasterizer.save(stream, options);
}
```

**Explanation:** `RasterizationOptions` 告訴 GroupDocs 將每頁渲染為圖像。`ByteArrayOutputStream` 會將結果保留於記憶體中，為下一步做好準備，無需寫入中間檔案。

### 步驟 3：為遮蔽準備光柵化輸出

```java
ByteArrayInputStream inputStream = new ByteArrayInputStream(stream.toByteArray());
```

現在光柵化的 PDF 已可作為 `InputStream` 使用，您可以直接將其輸入遮蔽引擎。

### 步驟 4：套用 Image Area Redaction（如何遮蔽 Word）

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.ImageAreaRedaction;
import com.groupdocs.redaction.redactions.RegionReplacementOptions;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Point;
import java.io.FileOutputStream;

try (Redactor redactor = new Redactor(inputStream)) {
    // Define the area for redaction.
    Point startPoint = new Point(1160, 2375);
    Dimension size = new Dimension(1050, 720);

    // Set up replacement options with a blue color overlay.
    RegionReplacementOptions replaceWithBlue = new RegionReplacementOptions(Color.BLUE, size);

    // Apply the image area redaction.
    RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(startPoint, replaceWithBlue));

    if (result.getStatus() != Redactor.RedactionStatus.Failed) {
        // Save the final document to an output directory.
        String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_raster.pdf";
        try (FileOutputStream fileStream = new FileOutputStream(outputPath)) {
            RasterizationOptions saveOptions = new RasterizationOptions();
            saveOptions.setEnabled(false);
            redactor.save(fileStream, saveOptions);
        }
    }
}
```

**Explanation:**  
- `ImageAreaRedaction` 針對由 `startPoint` 與 `size` 定義的矩形區域。  
- `RegionReplacementOptions` 允許您選擇覆蓋顏色（此例為藍色）以及取代矩形的大小。  
- 套用遮蔽後，文件會以光柵化 PDF 形式儲存，敏感區域已安全隱藏。

## 實務應用（如何遮蔽 Word）

| 情境 | 為何要光柵化並遮蔽？ |
|----------|--------------------------|
| **Legal contracts** | 在分享草稿前確保客戶機密性。 |
| **Medical records** | 移除 PHI 同時保留原始報告版面。 |
| **Financial statements** | 為外部審計遮蔽帳號或專有數字。 |

## 效能考量
- **Memory Management:** 使用串流 (`ByteArrayOutputStream` / `ByteArrayInputStream`) 以避免將整個檔案載入記憶體。  
- **CPU Usage:** 光柵化相當耗用 CPU；對於大型 DOCX 檔案，建議增加 JVM 堆積大小（例如 `-Xmx2g`）。  
- **Version Updates:** 保持 GroupDocs 函式庫為最新版本（如 24.9），以獲得效能優化與錯誤修正。

## 常見問題與解決方案（hide text java）

| 問題 | 解決方案 |
|-------|----------|
| **OutOfMemoryError** 處理大型 DOCX 時發生 | 將文件分段處理或增加 JVM 堆積大小。 |
| **Redaction not applied** | 確認 `result.getStatus()` 不為 `Failed`，且座標在頁面範圍內。 |
| **Output PDF blank** | 確保僅在遮蔽後才將 `RasterizationOptions.setEnabled(false)`，初始光柵化時保持為 `true`。 |

## 常見問答

**Q: What does “convert docx to image” actually produce?**  
A: 此過程會產生一個 PDF，且每頁皆為嵌入的位圖，使文字不可選取且適合進行遮蔽。

**Q: Can I use GroupDocs Redaction for other file types?**  
A: 可以，它支援 PDF、圖像以及許多其他文件格式。

**Q: How does the temporary license work?**  
A: 試用授權在有限期間內解鎖所有功能，讓您無限制地評估光柵化與遮蔽。

**Q: Is there a way to redact multiple regions at once?**  
A: 當然可以——多次呼叫 `redactor.apply()`，或傳入 `ImageAreaRedaction` 物件集合。

**Q: Do I need to convert the DOCX to PDF first?**  
A: 不需要。Redactor 可直接光柵化 DOCX 並一次輸出 PDF，如上所示。

---

**Last Updated:** 2025-12-21  
**Tested With:** GroupDocs.Redaction 24.9 (Java)  
**Author:** GroupDocs