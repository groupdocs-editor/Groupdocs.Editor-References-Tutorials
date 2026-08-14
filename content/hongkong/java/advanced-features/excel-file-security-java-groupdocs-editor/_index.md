---
date: '2026-06-16'
description: 了解如何使用 GroupDocs.Editor 保護 Excel Java，包括如何開啟受密碼保護的活頁簿、設定新密碼以及管理寫入保護。
keywords:
- protect excel java
- open password protected workbook
- java document password protection
schemas:
- author: GroupDocs
  dateModified: '2026-06-16'
  description: Learn how to protect Excel Java using GroupDocs.Editor, including how
    to open password protected workbook, set new passwords, and manage write protection.
  headline: 'Protect Excel Java with GroupDocs.Editor: Password Protection Guide'
  type: TechArticle
- description: Learn how to protect Excel Java using GroupDocs.Editor, including how
    to open password protected workbook, set new passwords, and manage write protection.
  name: 'Protect Excel Java with GroupDocs.Editor: Password Protection Guide'
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
title: 使用 GroupDocs.Editor 保護 Excel Java：密碼保護指南
type: docs
url: /zh-hant/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 保護 Excel Java 與 GroupDocs.Editor

在本完整教學中，您將了解如何使用 GroupDocs.Editor 的強大安全功能來 **protect Excel Java** 應用程式。我們將示範如何載入受密碼保護的活頁簿、處理錯誤密碼、在儲存時設定新密碼，以及啟用寫入保護——同時在處理大型試算表時保持低記憶體使用量。

## 快速解答
- **哪個函式庫可協助保護 Excel Java？** GroupDocs.Editor for Java.  
- **我可以在未提供密碼的情況下開啟受密碼保護的活頁簿嗎？** 不行——嘗試這樣做會拋出 `PasswordRequiredException`。  
- **如何處理錯誤的密碼？** 捕獲 `IncorrectPasswordException` 並再次提示使用者。  
- **儲存時可以設定新密碼嗎？** 可以，呼叫 `SpreadsheetSaveOptions.setPassword`。  
- **在正式環境中需要授權嗎？** 任何正式部署都需要有效的 GroupDocs.Editor 授權。

## 什麼是 protect excel java？
**protect excel java** 指的是使用 Java API 以程式方式對 Excel 活頁簿套用密碼保護與寫入限制。載入活頁簿、驗證密碼，然後以新密碼儲存——只需幾行簡潔的程式碼。此方法可省去手動步驟，確保在自動化管線中保持一致的安全性。

## 為何使用 Java 保護 Excel？
GroupDocs.Editor 支援 **30 多個專用 API 方法** 來處理密碼，能在不將整個檔案載入記憶體的情況下處理 **數百張工作表**，且在重新儲存加密檔案時保證 **100 % 版面配置相同**。使用 Java 來執行保護可減少意外的資料外洩，符合合規要求，並在企業工作流程中實現安全的批次處理。

## 前置條件
- **Java Development Kit (JDK) 8** 或更高版本  
- **Maven** 用於相依性管理  
- 基本的 Java 程式設計知識  
- 一個 **GroupDocs.Editor** 授權（試用或購買）  

## 設定 GroupDocs.Editor for Java

### 使用 Maven
將儲存庫與相依性加入您的 `pom.xml`：

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
`Editor` 類別是 GroupDocs.Editor for Java 中所有文件操作的入口。它將活頁簿載入記憶體，並提供編輯、儲存與安全管理的方法。

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## 實作指南

我們將說明在保護 Excel 活頁簿時可能遇到的四種常見情境。

### 如何使用 Java 保護 Excel – 在未提供密碼的情況下開啟文件
在未提供密碼的情況下嘗試開啟受密碼保護的活頁簿會觸發特定例外，讓您在繼續之前向使用者索取憑證。

**直接答案：** 只使用檔案路徑呼叫 `Editor.edit`；如果活頁簿已加密，GroupDocs.Editor 會拋出 `PasswordRequiredException`，您可以捕獲它以在使用者介面中請求密碼。

#### 概觀
有時您需要在提示使用者之前驗證活頁簿是否受密碼保護。此程式碼片段嘗試在未提供密碼的情況下開啟檔案，並優雅地處理例外。

#### 步驟說明

1. **匯入所需類別**  
   `PasswordRequiredException` 是在活頁簿需要密碼但未提供時拋出的例外類型。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **初始化 Editor**  
   `Editor` 實例代表核心處理引擎；必須使用指向授權檔案的有效 `EditorConfig` 來建構。  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **嘗試在未提供密碼的情況下編輯**  
   當呼叫 `Editor.edit` 並未提供密碼時，GroupDocs.Editor 會檢查檔案標頭。若偵測到保護，則拋出 `PasswordRequiredException`。  

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### 疑難排解提示
- 確認檔案路徑指向現有的活頁簿。  
- 使用捕獲的 `PasswordRequiredException` 觸發 UI 提示以輸入密碼。

### 使用錯誤密碼開啟文件
當使用者提供錯誤的密碼時，GroupDocs.Editor 會拋出 `IncorrectPasswordException`。處理此例外可讓您提供明確的回饋。

**直接答案：** 使用 `SpreadsheetLoadOptions` 並提供密碼載入活頁簿；若密碼不匹配，捕獲 `IncorrectPasswordException` 並通知使用者重新嘗試。

#### 概觀
當使用者提供錯誤的密碼時，GroupDocs.Editor 會拋出 `IncorrectPasswordException`。處理此例外可讓您提供明確的回饋。

#### 步驟說明

1. **匯入所需類別**  
   `IncorrectPasswordException` 表示提供的密碼與活頁簿的加密金鑰不匹配。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **設定載入選項並使用錯誤密碼**  
   `SpreadsheetLoadOptions` 允許在載入時指定密碼；傳入無效值將觸發例外。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **處理例外**  
   將載入呼叫包在 try‑catch 區塊中，捕獲 `IncorrectPasswordException` 以顯示錯誤訊息或限制重試次數。  

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### 疑難排解提示
- 確保密碼字串確實與正確密碼不同。  
- 在 UI 中使用此模式限制重試次數。

### 使用正確密碼開啟文件
提供正確的密碼即可完整存取活頁簿。我們同時會為大型檔案啟用記憶體最佳化。

**直接答案：** 透過 `SpreadsheetLoadOptions.setPassword` 提供正確密碼，啟用 `setOptimizeMemoryUsage(true)`，然後呼叫 `Editor.edit` 取得可編輯的 `Spreadsheet` 物件。

#### 概觀
提供正確的密碼即可完整存取活頁簿。我們也會為大型檔案啟用記憶體最佳化。

#### 步驟說明

1. **匯入所需類別**  
   `SpreadsheetLoadOptions` 設定活頁簿的載入方式，包括密碼與記憶體使用設定。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **使用正確密碼設定載入選項**  
   設定密碼並啟用記憶體最佳化，以在處理大型試算表時保持低 RAM 消耗。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### 主要設定選項
- **setOptimizeMemoryUsage** – 在處理大型試算表時降低 RAM 消耗。

### 設定開啟密碼與儲存時的寫入保護
編輯完成後，您可能想設定新密碼並防止他人修改活頁簿。此範例示範如何同時套用兩者。

**直接答案：** 使用現有密碼載入活頁簿，然後建立 `SpreadsheetSaveOptions` 物件，呼叫 `setPassword` 設定新密碼，啟用 `setWriteProtection(true)`，最後呼叫 `Editor.save`。  

#### 概觀
編輯完成後，您可能想設定新密碼並防止他人修改活頁簿。此範例示範如何同時套用兩者。

#### 步驟說明

1. **匯入所需類別**  
   `SpreadsheetSaveOptions` 定義活頁簿的儲存方式，包括密碼與寫入保護旗標。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **使用現有密碼載入活頁簿**  
   使用 `SpreadsheetLoadOptions` 開啟受保護的檔案，然後進行變更。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **設定儲存選項以使用新密碼與寫入保護**  
   呼叫 `setPassword` 指定新的開啟密碼，並使用 `setWriteProtection(true)` 鎖定活頁簿以防止編輯。  

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### 疑難排解提示
- 為 `setPassword` 呼叫選擇強且難以預測的密碼。  
- `WorksheetProtectionType.All` 旗標會鎖定所有可編輯元素；視需要進行調整。

## 實務應用

1. **安全資料分享** – 在將敏感的財務模型透過電郵發送給利害關係人之前先加以保護。  
2. **自動化文件管線** – 將這些程式碼片段整合到批次作業中，以處理並重新加密大量試算表。  

## 常見問題

**Q: 我可以更改已受保護活頁簿的密碼嗎？**  
A: 可以。使用現有密碼載入活頁簿，然後使用 `SpreadsheetSaveOptions.setPassword` 並提供新密碼儲存。

**Q: 若活頁簿受保護而我未指定密碼就嘗試開啟，會發生什麼情況？**  
A: GroupDocs.Editor 會拋出 `PasswordRequiredException`，您應捕獲它以向使用者請求密碼。

**Q: 是否可以僅保護特定工作表而非整個活頁簿？**  
A: 使用 `WorksheetProtection` 搭配特定的 `WorksheetProtectionType`（例如 `LockedCells`），並透過 API 套用至個別工作表。

**Q: `setOptimizeMemoryUsage(true)` 會影響效能嗎？**  
A: 它會以稍微增加處理開銷為代價降低記憶體消耗，對於非常大的檔案而言是有益的。

**Q: 每個伺服器實例需要單獨的授權嗎？**  
A: 授權條款是依部署計算；請參考 GroupDocs 授權指南以了解多節點情境。

## 結論

透過本教學，您現在了解如何使用 GroupDocs.Editor **protect Excel Java**——載入帶密碼的活頁簿、處理錯誤憑證，並在儲存時套用新密碼與寫入保護。這些功能協助您構建安全、合規且自動化的文件工作流程，從單一檔案擴展至大規模批次處理。

---

**最後更新：** 2026-06-16  
**測試版本：** GroupDocs.Editor 25.3  
**作者：** GroupDocs

## 相關教學

- [在 Java 中使用 GroupDocs.Editor 批次編輯 Word 檔案 – 步驟指南](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [如何在 Java 中使用 GroupDocs.Editor 編輯 Excel 與 Word 檔案](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [如何在 Java 中使用 InputStream 為 GroupDocs.Editor 設定授權：完整指南](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}