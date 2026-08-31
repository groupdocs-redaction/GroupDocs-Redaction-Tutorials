---
date: '2026-03-14'
description: 學習如何為 GroupDocs Redaction 實作自訂 Java 記錄器，以實現對遮蔽、批次處理及除錯的詳細監控。
keywords:
- custom logger java
- batch document processing
- how to monitor redaction
title: 自訂記錄器 Java：進階 GroupDocs 敏感資訊遮蔽日誌
type: docs
url: /zh-hant/java/advanced-redaction/advanced-logging-groupdocs-redaction-java/
weight: 1
---

# 自訂記錄器 Java：進階 GroupDocs Redaction 記錄

您是否在使用 GroupDocs Redaction 的 Java 應用程式時，苦於追蹤變更與錯誤？透過 **custom logger java** 功能，您可以簡化除錯流程、深入了解文件遮蔽的執行方式，甚至支援批次文件處理。在本指南中，我們將說明自訂記錄器的重要性、設定方式，以及如何有效監控遮蔽。

## 快速回答
- **什麼是主要的記錄類別？** 實作 `ILogger` 並將其傳遞給 `RedactorSettings`。  
- **我可以一次處理多個檔案嗎？** 可以——將記錄器與批次文件處理迴圈結合使用。  
- **如何判斷遮蔽是否失敗？** 在儲存前檢查 `logger.hasErrors()`。  
- **記錄功能需要額外授權嗎？** 不需要，同一個 GroupDocs Redaction 授權涵蓋所有功能。  
- **需要哪個 Maven 版本？** GroupDocs.Redaction 24.9 或更新版本。  

## 什麼是 Custom Logger Java？
A **custom logger java** 是使用者自行實作的 `ILogger` 介面，用以捕捉 GroupDocs Redaction 引擎產生的記錄訊息、錯誤與診斷資訊。透過自訂記錄器，您可以決定記錄哪些內容、儲存位置，以及如何與現有的記錄框架（如 Log4j 或 SLF4J）整合。

## 為何在 GroupDocs Redaction 中使用自訂記錄器？
- **細緻的監控** – 精確了解哪些遮蔽成功或失敗。  
- **合規與稽核追蹤** – 為法規需求保留詳細紀錄。  
- **效能洞察** – 記錄執行時間與資源使用情況，對批次文件處理特別有幫助。  
- **無縫整合** – 與您現有的 Java 記錄生態系統掛接。  

## 常見使用情境
1. **合規稽核** – 追蹤每一次遮蔽事件，以符合法律與產業標準。  
2. **自動化批次遮蔽** – 在迴圈中處理數千份文件，同時保留每個檔案的稽核日誌。  
3. **錯誤驅動工作流程** – 當 `logger.hasErrors()` 發出問題訊號時，暫停或重試批次。  

## 前置條件
- **必要函式庫**：GroupDocs.Redaction for Java 版本 24.9 或更新。  
- **環境**：已安裝 Java 8+ 與 Maven。  
- **知識需求**：基本的 Java 程式設計與記錄概念的了解。  

## 設定 GroupDocs.Redaction for Java

### 使用 Maven

在您的 `pom.xml` 檔案中加入以下設定，以納入必要的相依性與儲存庫：

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

**取得授權**：先以免費試用版探索 GroupDocs Redaction 功能。正式使用時，請取得臨時或正式授權。

## 基本初始化與設定

透過建立帶有自訂記錄器的 `RedactorSettings` 實例，來初始化您的專案：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.options.RedactorSettings;
import com.groupdocs.redaction.examples.java.helper_classes.CustomLogger;

CustomLogger logger = new CustomLogger();
RedactorSettings settings = new RedactorSettings(logger);
```

## 實作指南

### 使用自訂記錄器的進階記錄

#### 概觀

進階記錄會捕捉文件操作的詳細資訊，讓除錯與最佳化更為簡便。使用 **custom logger java** 可讓您完整掌控記錄內容與錯誤回報方式。

#### 步驟實作說明

##### 步驟 1：建立自訂記錄器

首先實作一個實作 `ILogger` 介面的類別：

```java
public class CustomLogger implements ILogger {
    // Implement necessary logging methods here
}
```

此自訂記錄器會在遮蔽過程中捕捉與處理記錄訊息。

##### 步驟 2：使用 RedactorSettings 載入文件

使用 `Redactor` 類別載入文件，並傳入自訂記錄器：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX", 
    new LoadOptions(), new RedactorSettings(logger));
```

此設定可確保所有操作皆透過您的自訂實作進行記錄。

##### 步驟 3：套用遮蔽

將所需的遮蔽套用至文件。此處示範刪除註解：

```java
redactor.apply(new com.groupdocs.redaction.redactions.DeleteAnnotationRedaction());
```

##### 步驟 4：條件式儲存變更

僅在未記錄錯誤時才儲存變更：

```java
if (!logger.hasErrors()) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/processed.docx");
}
```

此方式可確保在處理過程中若有問題會即時提示。

##### 步驟 5：清理資源

務必在 `finally` 區塊中關閉 `Redactor` 實例，以正確釋放資源：

```java
finally {
    redactor.close();
}
```

## 如何使用 Custom Logger Java 監控遮蔽

透過檢查 `logger.hasErrors()` 並檢視 `ILogger` 實作捕捉的訊息，即可即時 **how to monitor redaction**。對於大型專案，您可以將記錄寫入資料庫或集中式記錄服務（例如 ELK stack），以分析多份文件的趨勢。

## 效能考量

為了讓應用程式保持快速與回應，即使在處理批次文件時，也請遵循以下建議：

- **資源管理** – 正確關閉 `Redactor` 實例，以防止記憶體泄漏。  
- **記錄層級** – 使用 `info`、`debug`、`error` 等層級來控制詳細程度，減少額外負擔。  
- **批次處理** – 以群組方式處理文件，並重複使用同一個記錄器實例，以減少物件建立。  

## 小技巧與最佳實踐

- **專業提示：** 將記錄器呼叫包在 try‑catch 區塊中，以避免未預期的例外拋出。  
- **避免過度記錄**：在正式環境中除非在除錯，否則切換至 `info` 層級。  
- **持久化記錄**：當需要合規稽核時，將記錄保存至永久儲存（檔案、資料庫或雲端）。  

## 常見問題與解決方案

| 問題 | 解決方案 |
|------|----------|
| 未出現記錄 | 確保您的 `CustomLogger` 實作了所有必要的 `ILogger` 方法，且已將記錄器實例傳遞給 `RedactorSettings`。 |
| 大量批次時應用程式變慢 | 降低記錄細節（例如，從 `debug` 改為 `info`）或以非同步方式寫入記錄。 |
| 錯誤被吞掉 | 確認在呼叫 `save()` 前已檢查 `logger.hasErrors()`。 |

## 常見問答

**Q: 如何為 GroupDocs Redaction 設定自訂記錄器？**  
A: 實作 `ILogger` 介面，建立實例（例如 `CustomLogger logger = new CustomLogger();`），並將其傳遞給 `RedactorSettings`。

**Q: 可以將 GroupDocs Redaction 與其他 Java 記錄框架一起使用嗎？**  
A: 可以。您的自訂記錄器可以委派給 Log4j、SLF4J 或 `java.util.logging`，實現無縫整合。

**Q: GroupDocs Redaction 支援哪些類型的遮蔽？**  
A: 支援的遮蔽包括文字取代、註解刪除、圖像移除等。

**Q: 如何處理遮蔽過程中的錯誤？**  
A: 在套用遮蔽後使用 `logger.hasErrors()`；若返回 true，則跳過 `save()`，並檢查記錄的訊息。

**Q: 能否將 GroupDocs Redaction 與其他系統整合？**  
A: 完全可以。您可以將其連接至文件管理平台、工作流程引擎或雲端儲存服務，以實現端到端自動化。

## 資源
- **文件說明**： [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**： [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**： [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 儲存庫**： [GroupDocs.Redaction for Java on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援論壇**： [GroupDocs Redaction Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**： [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

遵循本指南，即可順利掌握 **custom logger java** 與 GroupDocs Redaction for Java 的使用。祝開發愉快！

---

**最後更新：** 2026-03-14  
**測試環境：** GroupDocs Redaction 24.9  
**作者：** GroupDocs