---
date: '2025-12-16'
description: 學習如何在 Java 中使用 GroupDocs.Editor 開啟無密碼的 Excel，並套用 GroupDocs 密碼保護，實現強大的
  Java Excel 加密。
keywords:
- Excel file security in Java
- GroupDocs.Editor for Java
- Java document password protection
title: 在 Java 中無需密碼打開 Excel：精通 GroupDocs.Editor 安全
type: docs
url: /zh-hant/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

# 使用 GroupDocs.Editor 在 Java 中開啟 Excel（無密碼）

在本完整指南中，您將了解在使用 GroupDocs.Editor 時如何 **開啟 Excel（無密碼）**，以及如何處理錯誤密碼、設定新密碼和套用寫入保護。我們將逐步示範實務情境，讓您能在 Java 應用程式中自信地保護 Excel 檔案。

## 快速解答
- **我可以在不知道密碼的情況下編輯受保護的 Excel 檔案嗎？** 否 – 您必須提供正確的密碼或處理 `PasswordRequiredException`。
- **錯誤密碼會拋出哪個例外？** `IncorrectPasswordException`。
- **在載入大型試算表時，如何降低記憶體使用量？** 使用 `loadOptions.setOptimizeMemoryUsage(true)`。
- **儲存時可以加入寫入保護嗎？** 可以，請使用 `WorksheetProtection` 於 `SpreadsheetSaveOptions` 中設定。
- **哪個函式庫提供這些功能？** GroupDocs.Editor for Java。

## 什麼是「開啟 Excel（無密碼）」？
在未提供密碼的情況下開啟 Excel 活頁簿，即嘗試直接存取檔案。若活頁簿受到保護，GroupDocs.Editor 會拋出 `PasswordRequiredException`，讓您能以程式方式處理。

## 為何在 Java 中使用 GroupDocs.Editor 進行 Excel 加密？
- **強健的安全性** – 套用強密碼與工作表保護。
- **記憶體最佳化** – `optimize memory usage java` 旗標在處理大型檔案時很有幫助。
- **完整的 API 控制** – 以細緻的選項載入、編輯與儲存試算表。

## 前置條件
- **Java Development Kit (JDK)** 8 或以上。  
- **Maven** 用於相依性管理。  
- **基本的 Java 知識**（類別、try‑catch 等）。  
- **GroupDocs.Editor 函式庫**（建議使用最新版本）。

## 設定 GroupDocs.Editor（Java）

### 使用 Maven
Add the repository and dependency to your `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### 直接下載
或者，從 [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/) 下載最新版本。

#### 取得授權
- **免費試用** – 無償探索功能。  
- **臨時授權** – 移除評估限制。  
- **購買** – 從 [GroupDocs](https://purchase.groupdocs.com/temporary-license) 取得完整授權。

### 基本初始化
```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## 實作指南

我們將說明四個核心情境，每個情境皆提供清晰步驟與程式碼摘錄。

### 如何在無密碼情況下開啟 Excel

如果您需要驗證活頁簿是否受密碼保護，請直接嘗試開啟並捕捉例外。

#### 步驟 1 – 匯入必要類別
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

#### 步驟 2 – 初始化 Editor
```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

#### 步驟 3 – 嘗試在未提供密碼的情況下開啟
```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

**提示：** 這個模式可讓您在繼續之前優雅地通知使用者需要密碼。

### 如何處理錯誤的密碼

當使用者提供錯誤的密碼時，GroupDocs.Editor 會拋出 `IncorrectPasswordException`。捕捉它以提供友善的回饋。

#### 步驟 1 – 匯入必要類別
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### 步驟 2 – 使用錯誤的密碼設定 Load Options
```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### 步驟 3 – 捕捉例外
```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

**專業提示：** 記錄失敗的嘗試以作稽核追蹤，但絕不可儲存錯誤的密碼。

### 如何使用正確密碼開啟 Excel

提供正確的密碼即可解鎖活頁簿，讓您可以編輯或轉換。

#### 步驟 1 – 匯入必要類別
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### 步驟 2 – 使用正確的密碼設定 Load Options
```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true); // optimize memory usage java
Editor editor = new Editor(inputFilePath, loadOptions);
```

**關鍵設定：** `setOptimizeMemoryUsage(true)` 可降低大型試算表的記憶體使用量，這是企業級處理的最佳實踐。

### 如何在儲存時設定新開啟密碼與寫入保護

編輯完成後，您可能想重新加密檔案並防止未授權的變更。

#### 步驟 1 – 匯入必要類別
```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

#### 步驟 2 – 使用現有密碼載入文件
```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### 步驟 3 – 使用新密碼與保護設定 Save Options
```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password"); // groupdocs password protection
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

**安全說明：** 請使用強度高且隨機產生的密碼，並安全保存（例如放入保險庫）。

## 實務應用

1. **安全資料共享** – 在將機密財務模型電郵給合作夥伴前加以保護。  
2. **自動化文件工作流程** – 將這些程式碼片段整合至每晚處理上千份試算表的批次作業，確保每個輸出皆已加密。  
3. **合規性** – 透過對所有匯出報告強制執行 `java excel encryption`，符合 GDPR 或 HIPAA 要求。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **`PasswordRequiredException` 即使我已提供密碼** | 確認密碼與活頁簿的保護類型相符（開啟 vs. 寫入）。 |
| **大型檔案的記憶體不足錯誤** | 啟用 `loadOptions.setOptimizeMemoryUsage(true)`，並考慮逐張工作表處理。 |
| **儲存的檔案無法在 Excel 中開啟** | 確保 `SpreadsheetFormats` 與目標副檔名相符（例如，對於含巨集的檔案使用 Xlsm）。 |
| **寫入保護未套用** | 確認已使用 `WorksheetProtectionType.All`，且在呼叫 `editor.save` 時傳入相應的儲存選項。 |

## 常見問答

**Q: 我可以在不重新儲存的情況下變更已受保護活頁簿的密碼嗎？**  
A: 否。您必須使用現有密碼載入文件，透過 `SpreadsheetSaveOptions` 設定新密碼，然後再儲存檔案。

**Q: `optimize memory usage java` 會影響效能嗎？**  
A: 它會稍微降低處理速度，但顯著減少記憶體使用量，對大型批次作業非常適合。

**Q: 可以只保護特定工作表嗎？**  
A: 可以。使用 `WorksheetProtectionType` 之類的選項（如 `SelectLockedCells` 或 `SelectUnlockedCells`）即可針對單獨工作表設定保護。

**Q: 我應該使用哪個版本的 GroupDocs.Editor？**  
A: 請始終使用最新的穩定版；本文示範的 API 可在 25.3 版及以上使用。

**Q: 如何在程式上驗證檔案是否受密碼保護再嘗試開啟？**  
A: 如「在無密碼情況下開啟 Excel」章節所示，嘗試在未提供 Load Options 的情況下建立 `Editor`，並捕捉 `PasswordRequiredException`。

---

**最後更新：** 2025-12-16  
**測試環境：** GroupDocs.Editor 25.3 for Java  
**作者：** GroupDocs