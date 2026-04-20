---
date: '2026-04-20'
description: 學習如何使用 GroupDocs.Redaction for Java 對 PDF 最後一頁進行塗黑、使用 Java 替換 PDF 文字，並有效隱藏
  PDF 敏感資料。
keywords:
- redact last page pdf
- replace text pdf java
- hide sensitive data pdf
title: 使用 GroupDocs.Redaction for Java 對 PDF 最後一頁進行遮蔽
type: docs
url: /zh-hant/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# 使用 GroupDocs.Redaction for Java 隱藏 PDF 最後一頁

在當今的數位環境中，**redact last page pdf** 檔案對於保護機密資訊並遵守隱私法規至關重要。本教學將指導您使用 GroupDocs.Redaction for Java 針對 PDF 的最後一頁，並在特定區域隱藏敏感資料。完成後，您將能夠以 Java 方式取代文字 pdf，並自信地在任何出現的地方隱藏敏感資料 pdf。

## 快速解答
- **主要目標是什麼？** 隱蔽 PDF 的最後一頁以及其中的特定區域。  
- **使用哪個函式庫？** GroupDocs.Redaction for Java。  
- **需要授權嗎？** 試用或臨時授權可用於測試；正式環境需購買完整授權。  
- **需要哪個 Java 版本？** Java 8 或更高版本，並支援 Maven。  
- **可以針對其他頁面嗎？** 可以，使用相同的過濾器即可調整為任意頁面範圍。

## 什麼是 PDF 隱蔽？
隱蔽指永久移除或遮蔽 PDF 中的內容，使其無法復原。當您 **redact last page pdf** 時，即可確保最後一頁的任何機密資訊徹底隱藏。

## 為何使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 提供豐富的過濾器——頁面範圍、區域以及文字——讓您精確控制要移除的內容。特別適用於：
- **Replacing text pdf java** 風格的文字取代，而不影響文件其他部分。  
- **Hiding sensitive data pdf**，例如個人識別碼、財務數字或法律條款。  
- 在大量文件批次中自動化合規檢查。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝。  
- **Maven** 用於相依管理。  
- 取得 **GroupDocs.Redaction** 授權（試用、臨時或購買）。

## 設定 GroupDocs.Redaction for Java

### Maven 設定
將儲存庫與相依項目加入您的 `pom.xml`：

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
如果您不想使用 Maven，可從官方網站下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

#### 取得授權步驟
- **Free Trial:** 無需承諾即可測試所有功能。  
- **Temporary License:** 用於短期專案或評估。  
- **Purchase:** 解鎖無限制使用與優先支援。

## 基本初始化
首先，建立指向 PDF 檔案的 `Redactor` 實例：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

此物件是所有隱蔽操作的入口。

## 如何隱蔽 PDF 最後一頁 – 步驟指南

### 功能 1：隱蔽最後一頁的特定區域

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得頁面資訊
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```
了解最後一頁的尺寸可讓您定義精確的座標。

#### 步驟 3：定義取代選項
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```
此處選擇將取代隱蔽內容的佔位文字。

#### 步驟 4：設定目標隱蔽的過濾器
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```
- `PageRangeFilter` 選取 **最後一頁**。  
- `PageAreaFilter` 將操作限制於該頁的下半部。

#### 步驟 5：套用隱蔽 (replace text pdf java)
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```
字串 “bibliography” 只在定義的區域內被替換為 “[secret]”。

#### 步驟 6：驗證成功並儲存
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```
寫入輸出檔案前請務必檢查狀態。

#### 步驟 7：清理資源
```java
redactor.close();
```
關閉 `Redactor` 可釋放記憶體與檔案句柄。

### 功能 2：頁面範圍過濾以進行隱蔽

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得文件資訊
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### 步驟 3：建立頁面範圍過濾器 (hide sensitive data pdf)
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```
此過濾器會將最後一頁隔離，讓您可套用任何所需的隱蔽邏輯。

### 功能 3：基於區域的 PDF 頁面隱蔽

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得頁面細節
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 步驟 3：定義區域過濾器 (hide sensitive data pdf)
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```
此過濾器針對最後一頁的下半部——非常適合移除頁腳或簽名。

#### 步驟 4：釋放資源
```java
redactor.close();
```

## 實務應用
- **Legal Documents:** 在分享前隱蔽最後一頁的客戶名稱或案件編號。  
- **Financial Reports:** 隱蔽帳號或機密摘要。  
- **Healthcare Records:** 移除患者識別資訊以符合 HIPAA。  
- **Pre‑Release Drafts:** 隱蔽仍在審核中的段落。

## 效能技巧
- **Reuse the `Redactor`** 在批次處理多個 PDF 時重複使用。  
- **Close the object promptly** 以避免記憶體洩漏，尤其是大型檔案。  
- **Test on a sample** 在正式文件上執行前先於樣本測試，以驗證過濾座標。

## 常見問題

**Q: 可以一次隱蔽多個頁面嗎？**  
A: 可以。調整 `PageRangeFilter` 參數即可包含任意範圍（例如 `new PageRangeFilter(1, 5)` 代表第 1‑5 頁）。

**Q: 此函式庫支援受密碼保護的 PDF 嗎？**  
A: 當然支援。將密碼傳遞給 `Redactor` 建構子即可開啟加密檔案。

**Q: 如何變更隱蔽的顏色或覆蓋層？**  
A: 使用 `ReplacementOptions` 來指定自訂圖像、顏色或文字覆蓋層。

**Q: 隱蔽是永久性的嗎？**  
A: 是的。被移除的內容不會保留在輸出 PDF 中，無法復原。

**Q: 如果需要根據正規表達式模式進行隱蔽該怎麼辦？**  
A: GroupDocs.Redaction 提供 `RegexRedaction`，其運作方式類似 `ExactPhraseRedaction`。

---

**最後更新:** 2026-04-20  
**測試於:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs