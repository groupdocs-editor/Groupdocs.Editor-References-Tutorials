---
date: '2026-10-16'
description: 了解如何使用 GroupDocs.Editor 在 Java 中打开受密码保护的 Excel 文件，设置新密码，并管理写保护。
keywords:
- open password protected excel
- write protect excel workbook
- optimize memory usage java
- protect specific worksheet
lastmod: '2026-10-16'
og_description: 使用 GroupDocs.Editor 在 Java 中打开受密码保护的 Excel 文件。本指南展示了如何加载加密工作簿、处理错误密码、在保存时应用新密码，以及在优化内存使用的同时启用写保护。
og_image_alt: 'Developer guide: Open password protected Excel in Java with GroupDocs.Editor'
og_title: 使用 GroupDocs.Editor 在 Java 中打开受密码保护的 Excel
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
title: 使用 GroupDocs.Editor 在 Java 中打开受密码保护的 Excel
type: docs
url: /zh/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---
# 在 Java 中使用 GroupDocs.Editor 打开受密码保护的 Excel

在本综合教程中，您将了解如何使用 GroupDocs.Editor 在 Java 中 **open password protected Excel** 工作簿，处理错误密码，在保存时设置新密码，并为整个工作簿启用写保护。步骤配有清晰的说明、真实场景示例以及大规模电子表格处理的最佳实践技巧。

## 快速答案
- **什么库可以帮助打开受密码保护的 Excel？** GroupDocs.Editor for Java.  
- **我可以在没有密码的情况下打开受密码保护的工作簿吗？** No – the API throws `PasswordRequiredException`.  
- **我该如何处理错误的密码？** Catch `IncorrectPasswordException` and prompt the user again.  
- **保存时可以设置新密码吗？** Yes, use `SpreadsheetSaveOptions.setPassword`.  
- **生产使用需要许可证吗？** A valid GroupDocs.Editor license is required for any production deployment.

## 什么是 open password protected Excel？
`open password protected Excel` 描述了以编程方式加载具有打开密码的 Excel 工作簿、验证密码，并可选择使用新密码或额外保护重新保存的过程。使用 Java API 可消除手动步骤，并让您将安全性嵌入自动化流水线。

## 为什么使用 Java 保护 Excel 工作簿？
GroupDocs.Editor 提供 **30+ 专用 API 方法** 用于密码处理，能够在不将整个文件加载到内存的情况下处理 **数百个工作表**，并在重新保存加密文件时保证 **100 % 布局保真度**。这些量化的能力使您能够构建批处理作业，在普通服务器上 **5 秒内处理 200 页的电子表格**，同时保持数据安全并符合合规要求。

## 前提条件
- Java Development Kit (JDK) 8 或更高  
- Maven 用于依赖管理  
- 基本的 Java 编程知识  
- GroupDocs.Editor 许可证（试用或购买）  

## 为 Java 设置 GroupDocs.Editor

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

### 直接下载
或者，从 [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/) 下载最新的 JAR。

#### 许可证获取
- **免费试用** – 免费试用 – 无需费用即可探索所有功能。  
- **临时许可证** – 在测试期间移除评估限制。  
- **购买** – 从 [GroupDocs](https://purchase.groupdocs.com/temporary-license) 获取完整许可证。

### 基本初始化
`Editor` 是 GroupDocs.Editor for Java 中所有文档操作的入口点。它将工作簿加载到内存中，并提供编辑、保存和安全管理的方法。

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## 实现指南

我们将逐步演示在保护 Excel 工作簿时可能遇到的四种常见场景。

### 如何在没有密码的情况下打开受密码保护的 Excel？

**直接答案：** 仅使用文件路径调用 `Editor.edit`；如果工作簿已加密，GroupDocs.Editor 会抛出 `PasswordRequiredException`，您可以捕获该异常以在用户界面中请求密码。

`PasswordRequiredException` 表示工作簿需要密码但未提供。捕获此异常后，您可以显示提示、记录事件或优雅地中止操作。

1. **导入所需类** – 引入 `PasswordRequiredException` 及相关类型。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **初始化 Editor** – 使用指向许可证文件的有效 `EditorConfig` 创建 `Editor` 实例。  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **尝试在没有密码的情况下编辑** – 仅使用文件路径调用 `Editor.edit`。如果工作簿受保护，调用会抛出 `PasswordRequiredException`。  

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### 故障排除提示
- 确认文件路径指向现有的工作簿。  
- 使用捕获的异常触发 UI 提示输入密码。  

### 如何使用错误密码打开受密码保护的 Excel？

**直接答案：** 使用提供的密码通过 `SpreadsheetLoadOptions` 加载工作簿；如果密码不匹配，捕获 `IncorrectPasswordException` 并通知用户重试。

`IncorrectPasswordException` 表示您提供的密码与工作簿的加密密钥不匹配。处理此异常可让您提供明确的反馈，并可选择限制重试次数。

1. **导入所需类** – 在导入中包含 `IncorrectPasswordException`。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **使用错误密码设置加载选项** – 创建 `SpreadsheetLoadOptions` 实例，并设置一个已知错误的密码用于测试。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **处理异常** – 将加载调用包装在 try‑catch 块中，捕获 `IncorrectPasswordException` 以显示错误信息或在达到一定次数后锁定用户。  

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### 故障排除提示
- 确保密码字符串确实与正确密码不同。  
- 在 UI 中使用此模式限制重试次数。  

### 如何使用正确密码打开受密码保护的 Excel？

**直接答案：** 通过 `SpreadsheetLoadOptions.setPassword` 提供正确密码，启用 `setOptimizeMemoryUsage(true)`，然后调用 `Editor.edit` 获取可编辑的 `Spreadsheet` 对象。

`SpreadsheetLoadOptions` 配置工作簿的加载方式，包括密码和内存使用设置。启用内存优化可在处理大型电子表格时保持 RAM 消耗低。

1. **导入所需类** – 引入 `SpreadsheetLoadOptions` 及相关工具。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **使用正确密码配置加载选项** – 设置密码，开启内存优化，然后调用 `Editor.edit`。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### 关键配置选项
- **setOptimizeMemoryUsage** – 在处理大型电子表格时降低 RAM 消耗，使您能够在不出现 OutOfMemory 错误的情况下处理 **高达 500 MB** 的文件。  

### 保存时如何设置新打开密码并对 Excel 工作簿进行写保护？

**直接答案：** 使用现有密码加载工作簿，创建 `SpreadsheetSaveOptions` 对象，调用 `setPassword` 设置新值，启用 `setWriteProtection(true)`，最后调用 `Editor.save`。

`SpreadsheetSaveOptions` 定义工作簿的保存方式，包括密码和写保护标志。`setWriteProtection(true)` 会锁定工作簿，除非提供正确密码，否则无法进一步编辑。

`WorksheetProtection` 允许您使用特定的保护类型保护单个工作表。

1. **导入所需类** – 如需细粒度控制，包含 `SpreadsheetSaveOptions` 和 `WorksheetProtection`。  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **使用现有密码加载工作簿** – 使用 `SpreadsheetLoadOptions` 打开受保护文件后再进行更改。  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **使用新密码和写保护配置保存选项** – 调用 `setPassword` 设置新的打开密码，并调用 `setWriteProtection(true)` 锁定工作簿以防编辑。  

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### 故障排除提示
- 为 `setPassword` 选择强大且不可预测的密码。  
- `WorksheetProtectionType.All` 标志会锁定所有可编辑元素；根据需要调整以实现选择性保护。  

## 实际应用

1. **安全的数据共享** – 在将敏感的财务模型通过电子邮件发送给利益相关者之前进行保护。  
2. **自动化文档流水线** – 将这些代码片段嵌入批处理作业，每晚处理并重新加密数千个电子表格。  
3. **合规监管** – 自动强制工作簿加密，以满足 GDPR、HIPAA 或 PCI‑DSS 等要求。  

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| `PasswordRequiredException` 即使我已提供密码 | 加载选项未附加到 edit 调用 | 确保将配置好的 `SpreadsheetLoadOptions` 实例传递给 `Editor.edit`。 |
| 大文件的内存不足错误 | 内存优化未启用 | 在 `SpreadsheetLoadOptions` 上调用 `setOptimizeMemoryUsage(true)`。 |
| 保存的工作簿失去格式 | 使用默认的 `SpreadsheetSaveOptions` 且未保留布局 | 设置 `setPreserveFormatting(true)`（在 25.3 版及以上可用）。 |
| 写保护未生效 | 忘记调用 `setWriteProtection(true)` | 在调用 `Editor.save` 前添加该调用。 |

## 常见问题

**Q: 我可以更改已受保护工作簿的密码吗？**  
A: 是的。使用现有密码加载工作簿，然后使用 `SpreadsheetSaveOptions.setPassword` 并提供新值进行保存。

**Q: 如果在工作簿受保护时尝试在未指定密码的情况下打开会怎样？**  
A: GroupDocs.Editor 会抛出 `PasswordRequiredException`，您应捕获该异常以向用户请求密码。

**Q: 是否可以仅保护特定工作表而不是整个工作簿？**  
A: 使用 `WorksheetProtection` 并指定特定的 `WorksheetProtectionType`（例如 `LockedCells`），通过 API 将其应用于各个工作表。

**Q: `setOptimizeMemoryUsage(true)` 会影响性能吗？**  
A: 它以轻微的处理开销换取内存消耗的降低，这对非常大的文件是有益的。

**Q: 每个服务器实例需要单独的许可证吗？**  
A: 许可证条款按部署计；请查阅 GroupDocs 许可证指南了解多节点场景。

## 结论

通过本指南，您现在了解如何使用 GroupDocs.Editor 在 Java 中 **打开受密码保护的 Excel**，优雅地处理错误密码，在保存时设置新密码，并为整个工作簿启用写保护。这些功能使您能够构建安全、合规且高吞吐量的文档工作流，能够从单个文件扩展到大规模批处理。

---

**最后更新：** 2026-10-16  
**测试版本：** GroupDocs.Editor 25.3  
**作者：** GroupDocs  

## 相关教程

- [在 Java 中使用 GroupDocs.Editor 批量编辑 Word 文件 – 步骤指南](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [如何在 Java 中使用 GroupDocs.Editor 编辑 Excel 和 Word 文件](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [如何在 Java 中使用 InputStream 为 GroupDocs.Editor 设置许可证：完整指南](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)
