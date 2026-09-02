---
date: '2026-06-01'
description: 了解如何在 Java 的 GroupDocs.Redaction 中使用 tilt effect，包含逐步程式碼說明、效能技巧與自訂選項。
keywords:
- how to use tilt
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  headline: How to Use Tilt Effect with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  name: How to Use Tilt Effect with GroupDocs.Redaction Java
  steps:
  - name: Initialize Redactor and Save Options
    text: First, create a `Redactor` instance pointing at your source file, then prepare
      `SaveOptions` that will hold the rasterization configuration.
  - name: Configure Tilt Effect Settings
    text: Enable rasterization and define the tilt angle boundaries. The `AdvancedRasterizationOptions.Tilt`
      object lets you set `minAngle` and `maxAngle` in degrees, controlling how much
      each page can rotate.
  - name: Save Document with Tilt Effect
    text: Run the redaction process and output the rasterized, tilted document. The
      `save` call writes each page as an image (PNG by default) while applying the
      random tilt you specified.
  type: HowTo
- questions:
  - answer: It redacts sensitive content while preserving document layout and also
      supports advanced rasterization features like the tilt effect.
    question: What is GroupDocs.Redaction Java used for?
  - answer: By enabling rasterization and adding the `Tilt` advanced option with `minAngle`
      and `maxAngle` parameters, as shown in the code samples.
    question: How do I apply a tilt effect in my document using GroupDocs?
  - answer: Yes, a free trial is available. For production use, obtain a temporary
      or permanent license.
    question: Can I use GroupDocs.Redaction for free?
  - answer: It enhances visual appeal, adds a creative touch, and can help differentiate
      marketing or presentation materials.
    question: What are the benefits of using a tilt effect in documents?
  - answer: Very large files may increase processing time and memory usage; proper
      resource allocation mitigates this.
    question: Are there any limitations to applying custom effects with GroupDocs.Redaction
      Java?
  type: FAQPage
title: 如何在 GroupDocs.Redaction Java 中使用 Tilt Effect
type: docs
url: /zh-hant/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/
weight: 1
---

# 如何在 GroupDocs.Redaction Java 中使用傾斜效果

在本教學中，您將了解 **如何使用傾斜** 為光柵化文件賦予動態、手持的外觀，了解此效果對現代簡報的重要性，以及在 GroupDocs.Redaction for Java 中需要的具體設定。我們將一步步說明整個流程——從安裝函式庫到微調效能——讓您能在實際專案中自信地套用傾斜效果。

## 快速回答
- **傾斜效果的作用是什麼？** 它會在定義的範圍內以隨機角度旋轉每個光柵化頁面，產生動態且略為傾斜的外觀。  
- **哪個函式庫提供此功能？** GroupDocs.Redaction for Java（版本 24.9 或更新）。  
- **我需要授權嗎？** 免費試用可用於評估；正式上線需取得永久或臨時授權。  
- **它會佔用大量記憶體嗎？** 會增加一些 CPU 負載，但適當的記憶體設定可使其在大型檔案下仍保持效率。  
- **我可以自訂角度範圍嗎？** 可以——在光柵化選項中使用 `minAngle` 和 `maxAngle` 參數。

## 什麼是自訂傾斜效果？

自訂傾斜效果是在將文件的每頁轉換為影像時套用的視覺變換。透過指定最小與最大角度，光柵化器會隨機傾斜頁面，為最終輸出帶來藝術化、類似「手持」的感受。當您想打破標準 PDF 那種僵硬、完全對齊的外觀，並加入個性化元素時，此效果特別有用。

## 為何在 GroupDocs.Redaction 中套用自訂傾斜效果？

GroupDocs.Redaction 支援對 **70 多種輸入與輸出格式** 進行光柵化，且可在不將整個檔案載入記憶體的情況下處理最多 **2,000 頁** 的 PDF。利用其內建的傾斜選項，即可避免使用第三方影像函式庫、降低整合複雜度，並將整個工作流程維持在單一、經過充分測試的 SDK 內。

- **吸引力：** 傾斜的頁面能抓住讀者目光，非常適合簡報或行銷手冊。  
- **品牌形象：** 在不改變原始內容的前提下，加入獨特的視覺標誌。  
- **彈性：** 您可控制角度範圍，實現細微或誇張的傾斜。  
- **整合性：** 此效果已內建於 GroupDocs.Redaction 的光柵化管線，無需外部影像處理工具。

## 前置條件

- 已安裝 Java 8 或更新版本。  
- Maven（或其他建置工具）以管理相依性。  
- GroupDocs.Redaction 24.9 或更新版本（本教學使用最新發行版）。  
- 具備基本的 Java 檔案處理知識。

## 設定 GroupDocs.Redaction for Java

### 安裝資訊

**Maven**

在您的 Maven 專案中加入以下儲存庫與相依性至 `pom.xml` 檔案，即可將 GroupDocs.Redaction 包含進來：

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

**直接下載**

或者，直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

#### 授權取得

要完整使用 GroupDocs.Redaction：

- **免費試用** – 無償探索核心功能。  
- **臨時授權** – 透過 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 申請時間限制的金鑰，以完整評估。  
- **購買** – 取得永久授權以供正式使用。

### 基本初始化與設定

`Redactor` 類別是 GroupDocs.Redaction 中所有遮蔽與光柵化操作的入口點。它負責文件的載入、處理與儲存，並確保資源自動釋放。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## 如何在光柵化過程中套用自訂傾斜效果

載入來源檔案、啟用光柵化、設定所需的傾斜範圍，然後儲存轉換後的文件——只需幾個簡潔步驟。本概述說明完整工作流程，讓您清楚知道要建立哪些物件、設定哪些選項，以及如何呼叫儲存操作，之後再深入檢視詳細程式碼。

### 步驟實作

#### 步驟 1：初始化 Redactor 與 Save Options

首先，建立指向來源檔案的 `Redactor` 實例，然後準備用於保存光柵化設定的 `SaveOptions`。

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### 步驟 2：設定傾斜效果參數

啟用光柵化並定義傾斜角度的界限。`AdvancedRasterizationOptions.Tilt` 物件允許您以度數設定 `minAngle` 與 `maxAngle`，控制每頁的旋轉幅度。

```java
saveOptions.getRasterization().setEnabled(true);
HashMap<String, String> tiltSettings = new HashMap<>();
tiltSettings.put("minAngle", "15"); // Set the minimum angle for the tilt effect
	tiltSettings.put("maxAngle", "30"); // Set the maximum angle for the tilt effect

saveOptions.getRasterization().addAdvancedOption(
    AdvancedRasterizationOptions.Tilt, 
    tiltSettings
);
```

#### 步驟 3：儲存帶有傾斜效果的文件

執行遮蔽流程並輸出光柵化且已傾斜的文件。`save` 呼叫會將每頁寫入影像（預設為 PNG），同時套用您指定的隨機傾斜。

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### 參數說明

- **minAngle** – 可套用於頁面的最小旋轉角度（度）。  
- **maxAngle** – 可允許的最大旋轉角度（度）。  

調整這些值即可實現細微或明顯的傾斜。

#### 疑難排解技巧

- 確認來源與輸出目錄對 JVM 可寫入。  
- 確認使用的是 GroupDocs.Redaction 24.9 或更新版本；舊版缺少 `Tilt` 選項。  
- 若輸出過於失真，請降低 `maxAngle` 的數值。

## 實務應用

1. **創意文件簡報** – 為投影片或客戶提案加入動態外觀。  
2. **行銷素材** – 使手冊與傳單更具手工感。  
3. **數位典藏** – 為歷史掃描件賦予細微、風格化的外觀，以供線上展覽使用。

## 效能考量

### 效能最佳化

- **記憶體管理：** 處理多頁 PDF 時分配足夠的堆積空間（如 `-Xmx2g` 或更高）。  
- **I/O 效率：** 批次處理檔案，盡可能重複使用單一 `Redactor` 實例。

### Java 記憶體管理最佳實踐

- 謹慎呼叫 `System.gc()`；依賴 JVM 的垃圾回收機制。  
- 及時關閉串流（GroupDocs.Redaction 內部已處理大部分清理工作）。

## 常見問題與解決方案

| 問題 | 可能原因 | 解決方案 |
|-------|--------------|----------|
| 未套用傾斜 | 光柵化未啟用 | 確保 `saveOptions.getRasterization().setEnabled(true);` |
| 輸出檔案為空 | 輸出路徑不正確 | 確認目錄存在且具有寫入權限 |
| 角度異常 | `minAngle` > `maxAngle` | 交換數值，使 `minAngle` ≤ `maxAngle` |

## 常見問答

**Q: GroupDocs.Redaction Java 的用途是什麼？**  
A: 它在保留文件版面配置的同時遮蔽敏感內容，並支援如傾斜效果等進階光柵化功能。

**Q: 如何在文件中使用 GroupDocs 套用傾斜效果？**  
A: 只要啟用光柵化，並在進階選項中加入 `Tilt`，設定 `minAngle` 與 `maxAngle` 參數，如程式碼範例所示。

**Q: 我可以免費使用 GroupDocs.Redaction 嗎？**  
A: 可以，提供免費試用。正式使用時需取得臨時或永久授權。

**Q: 在文件中使用傾斜效果有什麼好處？**  
A: 它提升視覺吸引力，增添創意感，並有助於讓行銷或簡報素材與眾不同。

**Q: 在 GroupDocs.Redaction Java 中套用自訂效果有什麼限制嗎？**  
A: 超大型檔案可能會延長處理時間並增加記憶體使用；適當的資源配置可減輕此問題。

## 資源
- [GroupDocs Redaction 文件說明](https://docs.groupdocs.com/redaction/java/)
- [API 參考文件](https://reference.groupdocs.com/redaction/java)
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GitHub 倉庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權申請](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-06-01  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

---

## 相關教學

- [GroupDocs.Redaction Java 光柵化選項教學](/redaction/java/rasterization-options/)
- [Java 自訂噪點光柵化：使用 GroupDocs.Redaction 保護敏感資訊](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)
- [如何在 Java 中使用 GroupDocs Redaction：Word 文件的預光柵化](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)