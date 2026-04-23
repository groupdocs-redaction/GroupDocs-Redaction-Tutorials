---
date: '2026-03-17'
description: 學習如何在 Java 中實作自訂格式處理程式，並使用 GroupDocs.Redaction 儲存已編輯的文件，有效保護敏感資料。
keywords:
- implement custom format handlers Java
- apply redactions GroupDocs Redaction
- Java data protection
title: 使用 GroupDocs.Redaction 在 Java 中實作自訂格式處理器
type: docs
url: /zh-hant/java/format-handling/implement-custom-format-handlers-java-groupdocs-redaction/
weight: 1
---

# 使用 GroupDocs.Redaction 實作 Java 自訂格式處理程式

在當今以數據為驅動的世界，保護敏感資訊至關重要，學習如何在 Java 中 **implement custom format handler** 能讓你靈活處理任何遇到的檔案類型。無論是處理法律合約、財務報表或個人記錄，本教學將指導你為純文字檔案註冊自訂格式處理程式，並使用 GroupDocs.Redaction 套用遮蔽，以安全地處理並 **save redacted document** 檔案。

## 快速解答
- **What is a custom format handler java?** 一個告訴 GroupDocs.Redaction 如何讀取與處理非標準檔案副檔名的外掛程式。  
- **Why use GroupDocs.Redaction for redaction?** 它提供可靠且高效能的遮蔽 API，支援多種文件類型。  
- **Which Java version is required?** Java 8 或更新版本；開發機必須安裝 JDK。  
- **Do I need a license?** 可使用免費試用版，但正式環境需購買永久授權。  
- **Can I batch‑process files?** 可以——在迴圈中為每個檔案初始化 Redactor，或使用平行串流。

## 你將學會
- 為特定檔案類型註冊 **custom format handler**。  
- 使用 GroupDocs.Redaction 的 API **Redact text java** 文件。  
- 真實案例：資料保護與安全 **replace sensitive text**。  
- 提升效能的調校技巧，以有效管理資源。

## 前置條件
在開始之前，請確保具備以下項目：

### 必要的函式庫與版本
- **GroupDocs.Redaction**：版本 24.9 或以上。

### 環境設定需求
- 已安裝 Java Development Kit (JDK)。  
- 使用 IntelliJ IDEA 或 Eclipse 等 IDE 進行程式開發與執行。

### 知識前提
- 具備 Java 程式設計的基本概念。  
- 熟悉 Maven 以管理相依性（有助但非必須）。

確認上述前置條件後，讓我們為你的 Java 專案設定 GroupDocs.Redaction。

## 為 Java 設定 GroupDocs.Redaction
要將 GroupDocs.Redaction 整合至 Java 應用程式，有兩種主要方式：使用 Maven 或直接下載。我們將逐一說明兩種選項，確保不論你的設定偏好皆能順利使用。

### 使用 Maven
在 `pom.xml` 檔案中加入以下設定：

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
或者，直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

#### 取得授權步驟
1. **Free Trial**：先使用免費試用版以探索功能。  
2. **Temporary License**：取得臨時授權以延長測試時間。  
3. **Purchase**：購買授權以取得完整功能。

### 基本初始化與設定
安裝完成後，請依照下列方式初始化 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        Redactor redactor = new Redactor("path/to/your/document");
        // Perform operations with the redactor instance.
        redactor.close();
    }
}
```

完成 GroupDocs.Redaction 設定後，我們即可深入探討 **how to implement custom format handler** 並套用遮蔽。

## 如何在 Java 中實作自訂格式處理程式

### 功能 1：自訂格式處理程式註冊

#### 概述
註冊 **custom format handler** 可擴充 GroupDocs.Redaction 的功能，以處理特定文件類型，例如具有特殊副檔名的純文字檔案。

#### 實作步驟

##### 步驟 1：匯入必要類別
首先匯入設定所需的類別：

```java
import com.groupdocs.redaction.configuration.DocumentFormatConfiguration;
import com.groupdocs.redaction.integration.DocumentFormatInstance;
import com.groupdocs.redaction.examples.java.helper_classes.CustomTextualDocument;
```

##### 步驟 2：設定文件格式
設定文件格式配置，以指定哪個副檔名與類別負責處理自訂格式：

```java
class CustomFormatHandlerRegistration {
    public static void main(String[] args) {
        DocumentFormatConfiguration config = new DocumentFormatConfiguration();
        // Set the file extension for this handler.
        config.setExtensionFilter(".dump");
        // Specify handling by CustomTextualDocument class.
        config.setDocumentType(CustomTextualDocument.class);
        // Add to available formats list.
        DocumentFormatInstance.getDefaultConfiguration().getAvailableFormats().add(config);
    }
}
```

**關鍵設定選項**  
- `setExtensionFilter`：決定處理程式適用的檔案副檔名。  
- `setDocumentType`：連結用於處理的文件類別。

### 功能 2：遮蔽應用

#### 概述
此功能示範如何 **redact text java** 文件，確保所有 **replace sensitive text** 操作皆安全執行。

#### 實作步驟

##### 步驟 1：匯入必要類別
匯入執行遮蔽所需的類別：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

##### 步驟 2：初始化 Redactor 並套用遮蔽
使用文件路徑初始化 Redactor，套用所需的遮蔽，並以新名稱 **save redacted document**：

```java
class RedactionApplication {
    public static void main(String[] args) throws Exception {
        final Redactor redactor = new Redactor(YOUR_DOCUMENT_DIRECTORY + "/sample.dump");
        try {
            // Apply an exact phrase redaction.
            redactor.apply(new ExactPhraseRedaction("dolor", false, new ReplacementOptions("[redacted]")));
            // Save the document with a new name.
            redactor.save(new SaveOptions(false, "AnyText"));
        } finally {
            redactor.close();
        }
    }
}
```

#### 疑難排解技巧
- 確認檔案路徑正確且可存取。  
- 若自訂處理程式無法載入，請再次檢查設定。

## 實務應用
以下為可套用此技術的真實情境：

1. **Legal Document Protection** – 在對外分享文件前遮蔽敏感案件細節。  
2. **Financial Records Security** – 透過隱藏帳號與個人資訊，安全處理銀行對帳單。  
3. **HR Data Management** – 在稽核或外部審查時保護員工記錄。  
4. **Integration with CRM Systems** – 在從 CRM 平台匯出報告前自動遮蔽客戶資料。  
5. **Automated Compliance Reporting** – 確保合規文件不會洩漏敏感資料。

## 效能考量
使用 GroupDocs.Redaction 時，請參考以下效能最佳化建議：

- **Optimize Resource Usage** – 在處理完每個檔案後立即關閉 Redactor 實例。  
- **Batch Processing** – 以批次方式遮蔽多個文件，以縮短載入時間。  
- **Profile and Benchmark** – 定期對應用程式進行效能分析，找出瓶頸。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| 處理程式未被識別 | 副檔名過濾不匹配 | 確認 `setExtensionFilter` 完全符合檔案的副檔名（例如 `.dump`）。 |
| 遮蔽未套用 | 片語大小寫敏感 | 在 `ExactPhraseRedaction` 中將 `ignoreCase` 旗標設為 `true`。 |
| 記憶體不足錯誤 | 同時載入大型檔案 | 改為順序處理檔案，或在可能的情況下使用串流 API。 |

## 結論
此時，你應已對如何 **implement custom format handler** 以及使用 GroupDocs.Redaction for Java **redact text java** 文件有扎實的了解。這些技能對於保護各類文件的敏感資訊非常寶貴。欲進一步提升專業，可探索如基於模式的遮蔽等進階技巧，並考慮將工作流程整合至 CI/CD 管線，以實現自動合規檢查。

### 後續步驟
- 嘗試基於模式的遮蔽，自動偵測並取代敏感資料。  
- 將遮蔽流程整合至建置管線，在部署前強制執行資料保護政策。

## 常見問答

**Q1: 我可以使用自訂格式處理程式處理哪些檔案類型？**  
A1: 你可以透過指定副檔名與對應的文件類別，為任何檔案類型設定處理程式。

**Q2: 我如何取得 GroupDocs.Redaction 的臨時授權？**  
A: 前往 [GroupDocs' official site](https://products.groupdocs.com/redaction) 申請臨時授權。

**Q3: 我能有效率地處理大量文件批次嗎？**  
A: 可以——使用效能考量章節中的批次處理技巧，並在處理完每個檔案後立即關閉 Redactor 實例。

**Q4: 能否使用相同的處理程式遮蔽 PDF 檔案？**  
A: GroupDocs.Redaction 已內建原生 PDF 支援；自訂處理程式通常用於非標準格式，如 `.dump`。

**Q5: API 是否支援非同步操作？**  
A: 雖然核心 API 為同步，但你可以將呼叫包裝於 Java `CompletableFuture`，或使用平行串流以實現併發。

---

**最後更新:** 2026-03-17  
**測試環境:** GroupDocs.Redaction 24.9  
**作者:** GroupDocs