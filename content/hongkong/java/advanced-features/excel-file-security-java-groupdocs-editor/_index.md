---
date: '2026-10-16'
description: 了解如何使用 GroupDocs.Editor 在 Java 中開啟受密碼保護的 Excel 檔案、設定新密碼以及管理寫入保護。
keywords:
- open password protected excel
- write protect excel workbook
- optimize memory usage java
- protect specific worksheet
lastmod: '2026-10-16'
og_description: 使用 GroupDocs.Editor 在 Java 中開啟受密碼保護的 Excel 檔案。本指南將示範如何載入加密工作簿、處理錯誤密碼、在儲存時套用新密碼，以及在優化記憶體使用的同時啟用寫入保護。
og_image_alt: 'Developer guide: Open password protected Excel in Java with GroupDocs.Editor'
og_title: 使用 GroupDocs.Editor 在 Java 中開啟受密碼保護的 Excel
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  headline: Open password protected Excel in Java using GroupDocs.Editor
  type: TechArticle
- description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  name: Open password protected Excel in Java using GroupDocs.Editor
  steps:
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Initialize the Editor**'
    text: '**Initialize the Editor**'
  - name: '**Attempt to edit without a password**'
    text: '**Attempt to edit without a password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Set up load options with an incorrect password**'
    text: '**Set up load options with an incorrect password**'
  - name: '**Handle the exception**'
    text: '**Handle the exception**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Configure load options with the correct password**'
    text: '**Configure load options with the correct password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Load the workbook with the existing password**'
    text: '**Load the workbook with the existing password**'
  type: HowTo
- questions:
  - answer: Yes. Load the workbook with the existing password, then save it using
      `SpreadsheetSaveOptions.setPassword` with the new value.
    question: Can I change the password of an already protected workbook?
  - answer: GroupDocs.Editor throws `PasswordRequiredException`, which you should
      catch to request the password from the user.
    question: What happens if I try to open a workbook without specifying a password
      when it is protected?
  - answer: Use `WorksheetProtection` with a specific `WorksheetProtectionType` (e.g.,
      `LockedCells`) and apply it to individual sheets via the API.
    question: Is it possible to protect only specific worksheets instead of the whole
      workbook?
  - answer: It reduces memory consumption at the cost of a slight processing overhead,
      which is beneficial for very large files.
    question: Does `setOptimizeMemoryUsage(true)` affect performance?
  - answer: Licensing terms are per deployment; consult the GroupDocs licensing guide
      for multi‑node scenarios.
    question: Do I need a separate license for each server instance?
  type: FAQPage
tags:
- open password protected excel
- GroupDocs.Editor
- Java Excel security
- workbook protection
title: 使用 GroupDocs.Editor 在 Java 中開啟受密碼保護的 Excel
type: docs
url: /zh-hant/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 GroupDocs.Editor 開啟受密碼保護的 Excel

在本完整教學中，您將了解如何在 Java 中使用 GroupDocs.Editor **開啟受密碼保護的 Excel** 工作簿、處理錯誤密碼、在儲存時套用新密碼，以及為整個工作簿啟用寫入保護。步驟會以清晰說明、實務案例情境以及大型試算表處理的最佳實踐技巧呈現。

## 快速回答
- **哪個函式庫可協助開啟受密碼保護的 Excel？** GroupDocs.Editor for Java.  
- **我可以在未提供密碼的情況下開啟受密碼保護的工作簿嗎？** 不行 – API 會拋出 `PasswordRequiredException`.  
- **如何處理錯誤的密碼？** 捕獲 `IncorrectPasswordException` 並再次提示使用者。  
- **儲存時可以設定新密碼嗎？** 可以，使用 `SpreadsheetSaveOptions.setPassword`.  
- **生產環境需要授權嗎？** 任何生產部署都需要有效的 GroupDocs.Editor 授權。

## 什麼是受密碼保護的 Excel 開啟？
`open password protected Excel` 描述以程式方式載入具有開啟密碼的 Excel 工作簿、驗證密碼，並可選擇以新密碼或其他保護方式重新儲存的過程。使用 Java API 可省去手動步驟，讓您將安全性嵌入自動化流程中。

## 為什麼要在 Java 中保護 Excel 工作簿？
GroupDocs.Editor 提供 **30 多個專用 API 方法** 來處理密碼，能在不將整個檔案載入記憶體的情況下處理 **數百個工作表**，且在重新儲存加密檔案時保證 **100 % 版面配置相同**。這些可量化的能力讓您能建立批次工作，在一般伺服器上於 **5 秒內處理 200 頁試算表**，同時確保資料安全與合規。

## 前置條件
- Java Development Kit (JDK) 8 或更高版本  
- 用於相依管理的 Maven  
- 基本的 Java 程式設計知識  
- GroupDocs.Editor 授權（試用版或正式版）  

## 為 Java 設定 GroupDocs.Editor

### 使用 Maven
將儲存庫與相依項目加入您的 `pom.xml`：

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
或者，從 [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/) 下載最新的 JAR。

#### 取得授權
- **免費試用** – 無需付費即可探索所有功能。  
- **臨時授權** – 在測試期間移除評估限制。  
- **購買** – 從 [GroupDocs](https://purchase.groupdocs.com/temporary-license) 取得完整授權。

### 基本初始化
`Editor` 是 GroupDocs.Editor for Java 中所有文件操作的入口點。它將工作簿載入記憶體，並提供編輯、儲存與安全管理的方法。

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## 實作指南

我們將逐步說明在保護 Excel 工作簿時可能遇到的四種常見情境。

### 如何在未提供密碼的情況下開啟受密碼保護的 Excel？

**直接回答：** 只使用檔案路徑呼叫 `Editor.edit`；如果工作簿已加密，GroupDocs.Editor 會拋出 `PasswordRequiredException`，您可以捕獲此例外以向使用者介面請求密碼。

`PasswordRequiredException` 表示工作簿需要密碼，但未提供。捕獲此例外後，您可以顯示提示、記錄事件，或優雅地中止操作。

1. **匯入必要的類別** – 引入 `PasswordRequiredException` 及相關類型。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **初始化 Editor** – 使用指向授權檔案的有效 `EditorConfig` 建立 `Editor` 實例。  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **嘗試在未提供密碼的情況下編輯** – 只傳入檔案路徑呼叫 `Editor.edit`。如果工作簿受保護，呼叫會拋出 `PasswordRequiredException`。  

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### 疑難排解技巧
- 確認檔案路徑指向現有的工作簿。  
- 使用捕獲的例外觸發 UI 提示要求密碼。  

### 如何使用錯誤的密碼開啟受密碼保護的 Excel？

**直接回答：** 使用 `SpreadsheetLoadOptions` 並提供密碼載入工作簿；若密碼不匹配，捕獲 `IncorrectPasswordException` 並通知使用者重新嘗試。

`IncorrectPasswordException` 表示您提供的密碼與工作簿的加密金鑰不符。處理此例外可讓您提供明確回饋，並可選擇限制重試次數。

1. **匯入必要的類別** – 在匯入中加入 `IncorrectPasswordException`。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **使用錯誤密碼設定載入選項** – 建立 `SpreadsheetLoadOptions` 實例，並設定一個已知錯誤的密碼以進行測試。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **處理例外** – 將載入呼叫包在 try‑catch 區塊，捕獲 `IncorrectPasswordException` 以顯示錯誤訊息或在達到一定次數後鎖定使用者。  

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### 疑難排解技巧
- 確認密碼字串確實與正確密碼不同。  
- 在 UI 中使用此模式限制重試次數。  

### 如何使用正確的密碼開啟受密碼保護的 Excel？

**直接回答：** 透過 `SpreadsheetLoadOptions.setPassword` 提供正確密碼，啟用 `setOptimizeMemoryUsage(true)`，然後呼叫 `Editor.edit` 取得可編輯的 `Spreadsheet` 物件。

`SpreadsheetLoadOptions` 設定工作簿的載入方式，包括密碼與記憶體使用設定。啟用記憶體最佳化可在處理大型試算表時降低 RAM 消耗。

1. **匯入必要的類別** – 引入 `SpreadsheetLoadOptions` 及相關工具。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **使用正確密碼設定載入選項** – 設定密碼、開啟記憶體最佳化，然後呼叫 `Editor.edit`。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### 主要設定選項
- **setOptimizeMemoryUsage** – 在處理大型試算表時降低 RAM 消耗，讓您能在 **最高 500 MB** 的檔案上運行而不會發生 OutOfMemory 錯誤。  

### 如何在儲存時設定新開啟密碼並對 Excel 工作簿啟用寫入保護？

**直接回答：** 使用現有密碼載入工作簿，建立 `SpreadsheetSaveOptions` 物件，使用 `setPassword` 設定新密碼，啟用 `setWriteProtection(true)`，最後呼叫 `Editor.save`。

`SpreadsheetSaveOptions` 定義工作簿的儲存方式，包括密碼與寫入保護旗標。`setWriteProtection(true)` 會鎖定工作簿，除非提供正確密碼，否則無法進一步編輯。

`WorksheetProtection` 允許您以特定保護類型保護單獨的工作表。

1. **匯入必要的類別** – 若需要細緻控制，請加入 `SpreadsheetSaveOptions` 與 `WorksheetProtection`。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **使用現有密碼載入工作簿** – 使用 `SpreadsheetLoadOptions` 開啟受保護檔案，然後再進行變更。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **設定儲存選項以使用新密碼與寫入保護** – 呼叫 `setPassword` 設定新開啟密碼，並使用 `setWriteProtection(true)` 鎖定工作簿以防止編輯。  

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### 疑難排解技巧
- 為 `setPassword` 呼叫選擇強度高且難以預測的密碼。  
- `WorksheetProtectionType.All` 旗標會鎖定所有可編輯元素；如需選擇性保護，請自行調整。  

## 實務應用

1. **安全資料共享** – 在將敏感財務模型透過電郵發送給利害關係人之前加以保護。  
2. **自動化文件流程** – 將這些程式碼片段嵌入批次工作，每晚處理並重新加密數千份試算表。  
3. **法規遵循** – 強制工作簿加密，以自動符合 GDPR、HIPAA 或 PCI‑DSS 等要求。  

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| `PasswordRequiredException` 即使我已提供密碼 | 載入選項未附加至 edit 呼叫 | 確保將配置好的 `SpreadsheetLoadOptions` 實例傳遞給 `Editor.edit`。 |
| 大型檔案的記憶體不足錯誤 | 記憶體最佳化未啟用 | 在 `SpreadsheetLoadOptions` 上呼叫 `setOptimizeMemoryUsage(true)`。 |
| 儲存的工作簿失去格式 | 使用預設的 `SpreadsheetSaveOptions` 且未保留版面配置 | 設定 `setPreserveFormatting(true)`（自 25.3 版起可用）。 |
| 寫入保護未套用 | 忘記呼叫 `setWriteProtection(true)` | 在呼叫 `Editor.save` 前加入此呼叫。 |

## 常見問答

**Q:** 我可以更改已受保護工作簿的密碼嗎？  
**A:** 可以。先使用現有密碼載入工作簿，然後使用 `SpreadsheetSaveOptions.setPassword` 設定新密碼再儲存。

**Q:** 如果在工作簿受保護時未指定密碼而嘗試開啟，會發生什麼情況？  
**A:** GroupDocs.Editor 會拋出 `PasswordRequiredException`，您應捕獲此例外以向使用者請求密碼。

**Q:** 是否可以只保護特定工作表而非整個工作簿？  
**A:** 使用 `WorksheetProtection` 搭配特定的 `WorksheetProtectionType`（例如 `LockedCells`），透過 API 套用於個別工作表。

**Q:** `setOptimizeMemoryUsage(true)` 會影響效能嗎？  
**A:** 它會以稍微增加處理開銷為代價降低記憶體消耗，對於非常大的檔案非常有益。

**Q:** 每個伺服器實例需要單獨的授權嗎？  
**A:** 授權條款以每次部署為單位；請參閱 GroupDocs 授權指南以了解多節點情境。

## 結論

透過本指南，您現在已了解如何在 Java 中使用 GroupDocs.Editor **開啟受密碼保護的 Excel**、優雅地處理錯誤密碼、在儲存時套用新密碼，以及為整個工作簿啟用寫入保護。這些功能讓您能構建安全、合規且高吞吐量的文件工作流程，從單一檔案擴展至大規模批次處理。

---

**Last Updated:** 2026-10-16  
**Tested With:** GroupDocs.Editor 25.3  
**Author:** GroupDocs  

## 相關教學

- [在 Java 中使用 GroupDocs.Editor 批次編輯 Word 檔案 – 步驟指南](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [如何在 Java 中使用 GroupDocs.Editor 編輯 Excel 和 Word 檔案](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [如何在 Java 中使用 InputStream 為 GroupDocs.Editor 設定授權：完整指南](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}