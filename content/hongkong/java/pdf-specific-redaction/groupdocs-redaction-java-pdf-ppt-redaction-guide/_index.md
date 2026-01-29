---
date: '2026-01-29'
description: 學習如何使用 GroupDocs.Redaction 在 Java 中執行 PDF 文字遮蔽，並了解如何高效地對 PDF Java 文件進行遮蔽。
keywords:
- PDF Redaction Java
- PPT Redaction Java
- GroupDocs.Redaction
title: 使用 GroupDocs.Redaction for Java 進行 PDF 與 PPT 文字遮蔽
type: docs
url: /zh-hant/java/pdf-specific-redaction/groupdocs-redaction-java-pdf-ppt-redaction-guide/
weight: 1
---

# PDF 文本修訂與 PPT 頁面區域修訂 使用 GroupDocs.Redaction for Java

在當今快速變化的數位世界，**pdf text redaction** 是保護機密資料的必要步驟。無論您在處理法律合約、財務報表或公司 PowerPoint 簡報，都需要可靠的方法在分享前隱藏敏感資訊。本教學將指導您如何使用 **GroupDocs.Redaction for Java** 於 PDF 與 PPT 檔案的最後一頁或投影片上修訂文字與圖像。

## 快速解答
- **What is pdf text redaction?** 移除或遮蔽 PDF 檔案中的機密文字與圖像。  
- **Which library supports this in Java?** GroupDocs.Redaction for Java。  
- **Do I need a license?** 免費試用可用於評估；正式環境需購買完整授權。  
- **Can I redact both PDF and PPT with the same code?** 可以 – API 於兩種格式皆使用相同的 Redactor 類別。  
- **What Java version is required?** JDK 8 或更高版本。

## PDF Text Redaction 是什麼？
PDF text redaction 是永久刪除或遮蔽 PDF 文件中選取內容的過程，使其無法被復原或檢視。與單純隱藏不同，修訂會將資料從檔案結構中移除。

## 為何使用 GroupDocs.Redaction for Java？
- **Cross‑format support** – 支援跨格式 – 可處理 PDF、PowerPoint、Word、Excel 等多種檔案。  
- **Fine‑grained area control** – 細緻的區域控制 – 可定位精確的頁面區域，而非整頁。  
- **Built‑in regex engine** – 內建正規表達式引擎 – 自動搜尋敏感片語。  
- **Thread‑safe API** – 執行緒安全的 API – 適用於大規模應用的批次處理。

## 前置條件
在開始之前，請確保您已具備：

- **GroupDocs.Redaction for Java**（可透過 Maven 或直接連結下載）。  
- **JDK 8+** 已安裝並設定。  
- **Maven**（或手動加入 JAR 的能力）。  
- 具備 Java I/O 與正規表達式的基本概念。

## 設定 GroupDocs.Redaction for Java
### Maven 設定
將 GroupDocs 套件庫與相依性加入您的 `pom.xml`：

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
如果您不想使用 Maven，可從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權
- **Free Trial** – 免費試用 – 無需付費即可探索核心功能。  
- **Temporary License** – 暫時授權 – 延長測試期限超過試用期。  
- **Full License** – 完整授權 – 商業部署時必須取得。

### 基本初始化
建立指向欲處理文件的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;
// Initialize the Redactor object
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/YOUR_FILE.pdf");
```

## 實作指南
### 如何使用 GroupDocs.Redaction 於 PDF Java 文件進行修訂？
以下為在 PDF 檔最後一頁右半部執行 **pdf text redaction** 的逐步說明。

#### 步驟 1：載入文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF");
```

#### 步驟 2：定義文字匹配的正規表達式模式
```java
// Compile regex pattern to match specific text
java.util.regex.Pattern rx = java.util.regex.Pattern.compile("urna");
```

#### 步驟 3：設定取代選項
- **Text Redaction** – 文字修訂 – 使用佔位符取代符合的字詞。  
- **Image Redaction** – 圖像修訂 – 在圖像區域覆蓋實心紅色矩形。

```java
ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
optionsText.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1), // Target the last page
    new PageAreaFilter(new java.awt.Point(300, 0), new java.awt.Dimension(300, 840)) // Right half of the page
});
```

```java
RegionReplacementOptions optionsImg = new RegionReplacementOptions(java.awt.Color.RED, new java.awt.Dimension(100, 100));
```

#### 步驟 4：套用修訂
執行 `PageAreaRedaction` 操作以同時執行文字與圖像修訂：

```java
RedactorChangeLog result = redactor.apply(new PageAreaRedaction(rx, optionsText, optionsImg));

if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/output.pdf");
}
```

#### 步驟 5：清理資源
及時關閉 `Redactor` 以釋放原生資源：

```java
finally {
    redactor.close();
}
```

### 如何使用相同方法修訂 PPT 投影片？
工作流程與 PDF 步驟相同；僅檔案副檔名不同。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PPT");
```

遵循上述相同的模式定義、選項設定與套用步驟，並依需求調整輸出檔案名稱。

## 實務應用
- **Legal Document Preparation** – 法律文件準備 – 在提交前修訂客戶姓名、案件編號或機密條款。  
- **Financial Reporting** – 財務報告 – 隱藏 PDF 與投影片中的帳號、利潤率或專有公式。  
- **HR Audits** – 人力資源稽核 – 從大量文件匯出中移除員工識別資訊。

## 效能考量
- **Close resources promptly** – 及時關閉資源，以降低記憶體使用量。  
- **Optimize regex** – 最佳化正規表達式 – 避免使用過於寬泛的模式導致不必要的全檔掃描。  
- **Batch processing** – 批次處理 – 修訂大量檔案時使用執行緒池以提升吞吐量。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| *未套用修訂* | 過濾條件指向錯誤的頁面/區域 | 確認 `PageRangeFilter` 與 `PageAreaFilter` 的座標。 |
| *OutOfMemoryError* | 大型檔案持續開啟 | 改為順序處理檔案或增加 JVM 堆積大小 (`-Xmx`)。 |
| *正規表達式匹配到不需要的文字* | 模式過於寬泛 | 優化正規表達式或使用字邊界 (`\b`)。 |

## 常見問答

**Q: `pdf text redaction` 與僅隱藏文字有何不同？**  
A: 修訂會永久從檔案結構中移除資料，而隱藏僅改變視覺層。

**Q: 我可以使用 GroupDocs.Redaction 修訂受密碼保護的 PDF 嗎？**  
A: 可以 – 在建立 `Redactor` 實例時提供密碼。

**Q: 有沒有辦法在儲存前預覽修訂結果？**  
A: 使用 `redactor.save("output.pdf")` 儲存至暫存位置，然後開啟檔案檢視。

**Q: 此函式庫是否支援其他格式，如 DOCX 或 XLSX？**  
A: 當然 – 相同的 API 可用於所有支援的文件類型。

**Q: 若遇到問題，該向何處尋求協助？**  
A: 前往社群論壇 [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) 取得協助。

## 結論
您現在已擁有使用 GroupDocs.Redaction for Java 進行 **pdf text redaction** 與 PPT 投影片修訂的完整、可投入生產的解決方案。依循上述步驟，即可保護敏感資訊，遵守隱私法規，並在大量文件上自動化修訂工作流程。

---

**最後更新：** 2026-01-29  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs