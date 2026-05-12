---
date: '2026-02-16'
description: 學習如何使用 GroupDocs Redaction 搭配預光柵化，安全地在 Word 文件中遮蔽圖像。內容包括逐步設定、程式碼與故障排除。
keywords:
- GroupDocs.Redaction Java
- pre-rasterization Word documents
- image area redaction
title: 如何在 Java 中使用 GroupDocs Redaction：Word 文件的預光柵化
type: docs
url: /zh-hant/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/
weight: 1
---

# 如何在 Java 中使用 GroupDocs Redaction：Word 文件的預光柵化

在本教學中，您將 **使用 GroupDocs Redaction** 於處理 Microsoft Word 檔案時啟用預光柵化，讓您輕鬆 **遮蔽 Word 文件中包含的圖像**。我們將逐步說明完整設定、展示如何配置程式庫，並以清晰、口語化的方式示範圖像區域遮蔽。

## 快速解答
- **預光柵化的作用是什麼？** 它會將嵌入的圖像轉換為點陣圖格式，以便高效編輯或遮蔽。  
- **我需要授權嗎？** 免費試用可用於開發；正式上線需購買完整授權。  
- **需要哪個 Java 版本？** Java 8 或更新版本（建議使用 JDK 11 以上）。  
- **可以一次處理多個檔案嗎？** 可以——將遮蔽邏輯包在迴圈中即可批次處理。  
- **記憶體會是問題嗎？** 大圖像可能需要增加堆積大小，請留意 JVM 記憶體使用情況。

## GroupDocs Redaction 中的預光柵化是什麼？
預光柵化是一種載入選項，會在執行任何遮蔽操作之前，將 Word 文件內的所有圖像轉換為點陣圖資料。此轉換使得 `ImageAreaRedaction` 類別能夠精確定位像素區域，確保視覺內容的精確移除或遮蔽。

## 為何使用 GroupDocs Redaction 來遮蔽 Word 文件中的圖像？
- **安全合規性：** 輕鬆符合 GDPR、HIPAA 或其他資料隱私法規。  
- **自動化就緒：** 可整合至文件管線、內容管理系統或微服務。  
- **效能導向：** 載入時一次光柵化即可減少重複處理的開銷。  

## 前置條件
- **GroupDocs.Redaction 24.9**（或更新版本）——提供光柵化功能的程式庫。  
- **Java Development Kit (JDK)**——已安裝 8 版或更新的 Java。  
- 具備基本的 Java 語法與 Maven 建置工具知識。  

## 為 Java 設定 GroupDocs.Redaction

### Maven 設定
將儲存庫與相依性加入 `pom.xml` 檔案：

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
如果您不想使用 Maven，可從官方發佈頁面下載最新的 JAR 檔案： [GroupDocs.Redaction for Java 版本](https://releases.groupdocs.com/redaction/java/)。

#### 取得授權
先使用免費試用或申請臨時授權以評估產品。若需正式上線功能，請購買永久授權。

## 基本初始化

以下是建立帶有預光柵化功能的 `Redactor` 實例所需的最小 Java 程式碼。請保留此片段，稍後會在此基礎上進一步說明。

```java
// Ensure necessary imports are included
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

public class DocumentRedaction {
    public static void main(String[] args) {
        // Initialize load options with pre-rasterization enabled
        LoadOptions loadOptions = new LoadOptions(true);

        // Create a Redactor instance to manage the document
        try (final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", loadOptions)) {
            // Perform operations on the document
        }
    }
}
```

## 實作指南

### 啟用預光柵化

#### 概觀
當 `LoadOptions` 以 `true` 建構時，GroupDocs.Redaction 會在載入 Word 檔案時光柵化每一張圖像，為像素層級的操作做好準備。

#### 步驟說明

**3.1 Setting Up Load Options**  
建立 `LoadOptions` 物件，將光柵化旗標設為 `true`：

```java
// Set load options with pre-rasterization enabled
LoadOptions loadOptions = new LoadOptions(true);
```

**3.2 Initializing the Redactor Object**  
將 `loadOptions` 傳入 `Redactor` 建構子，使文件以光柵化模式開啟：

```java
// Initialize the Redactor object using specified file path and load options
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", loadOptions);
```

**3.3 Applying Image Area Redaction**  
定義要隱藏的矩形區域 (x, y, width, height)，然後以純色取代該區域：

```java
import com.groupdocs.redaction.redactions.ImageAreaRedaction;
import com.groupdocs.redaction.redactions.RegionReplacementOptions;

// Define the region to be redacted (x, y, width, height)
ImageAreaRedaction areaRedaction = new ImageAreaRedaction(100, 100, 200, 50);

// Apply a solid color as replacement
RegionReplacementOptions options = new RegionReplacementOptions(java.awt.Color.BLACK);

// Execute the redaction on your document
redactor.apply(areaRedaction);
```

### 常見問題與故障排除技巧
- **文件路徑錯誤：** 請確認檔案路徑正確且應用程式具備讀寫權限。  
- **光柵化問題：** 確認 `LoadOptions` 旗標已設為 `true`；否則圖像區域仍為向量形式，無法進行遮蔽。  
- **記憶體限制：** 大型 Word 檔案若包含大量高解析度圖像，可能需要更大的 JVM 堆積 (`-Xmx2g` 或更高)。  

## 實務應用

1. **敏感資料遮蔽：** 在分享前自動隱藏個人照片、簽名或掃描的身分證件。  
2. **合規管理：** 透過清除合約或報告中的視覺資料，符合行業特定法規。  
3. **安全文件共享：** 為合作夥伴提供已遮蔽的文件，同時保留原始版面的布局。  

將 GroupDocs Redaction 整合至現有工作流程（例如 CI/CD 管線、文件管理 API）可進一步自動化合規檢查。

## 效能考量

- **有效記憶體管理：** 配置足夠的堆積空間，並及時關閉 `Redactor` 實例（`try‑with‑resources` 區塊會自動完成此動作）。  
- **資源最佳化：** 明智使用 `LoadOptions`——僅在需要圖像區域編輯時才啟用光柵化，否則保持關閉以加速純文字遮蔽。  

遵循上述做法，即使面對大型、圖像密集的 Word 檔案，也能維持回應迅速的處理效能。

## 結論

您現在已學會如何 **使用 GroupDocs Redaction** 為 Word 文件啟用預光柵化，並執行精確的圖像區域遮蔽。此功能讓您能保護視覺內容、符合合規要求，並簡化安全文件的分發流程。

**下一步：** 探索其他遮蔽類型（文字、元資料），嘗試批次處理，或將程式庫整合至 RESTful 服務以提供即時遮蔽。

## 常見問題

**Q1: 在 GroupDocs Redaction for Java 中，什麼是預光柵化？**  
A: 它會在載入文件時將圖像轉換為點陣圖格式，從而支援像素層級的遮蔽。

**Q2: 如何使用此程式庫執行文字遮蔽？**  
A: 使用 `TextRedaction` 類別指定文字模式與取代選項即可。

**Q3: 可以一次處理多個文件嗎？**  
A: 可以——將遮蔽邏輯包在迴圈中，並為每個檔案重複使用 `LoadOptions`。

**Q4: 我的文件無法載入，應該檢查什麼？**  
A: 請確認檔案路徑正確、檔案未被鎖定，且 `LoadOptions` 已正確設定。

**Q5: 大圖像的遮蔽有沒有限制？**  
A: 大圖像可能需要額外的堆積記憶體；建議提升 JVM `-Xmx` 設定或分頁處理。

**Q6: GroupDocs Redaction 也支援 PDF 檔案嗎？**  
A: 當然支援——PDF 同樣提供類似的光柵化選項，讓您能在多種格式上執行圖像區域遮蔽。

---

**最後更新：** 2026-02-16  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

**資源**
- **文件說明：** [GroupDocs.Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考：** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載：** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 程式庫：** [GroupDocs.Redaction on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援論壇：** [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權：** [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)