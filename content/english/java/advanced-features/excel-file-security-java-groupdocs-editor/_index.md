---
title: "Save Excel with Password in Java Using GroupDocs.Editor"
description: "Learn how to save Excel with password in Java using GroupDocs.Editor, and discover how to open Excel without password and add write protection Excel."
date: "2026-02-01"
weight: 1
url: "/java/advanced-features/excel-file-security-java-groupdocs-editor/"
keywords:
- Excel file security in Java
- GroupDocs.Editor for Java
- Java document password protection
type: docs
---

# Save Excel with Password in Java Using GroupDocs.Editor

In this guide you'll learn how to **save Excel with password** using GroupDocs.Editor in Java. We'll walk through opening Excel files—both with and without passwords—handling incorrect password attempts, and finally applying write protection when you save the document. By the end, you’ll have a solid, production‑ready approach for securing Excel workbooks in your Java applications.

## Quick Answers
- **How do I open an Excel file without a password?** Use `Editor.edit()` directly; catch `PasswordRequiredException` if the file is protected.  
- **What exception is thrown for a wrong password?** `IncorrectPasswordException`.  
- **Can I set a new password when saving?** Yes, via `SpreadsheetSaveOptions.setPassword(...)`.  
- **How do I add write protection to a sheet?** Use `WorksheetProtection` with `WorksheetProtectionType.All`.  
- **Which Maven artifact do I need?** `com.groupdocs:groupdocs-editor:25.3`.

## What You'll Learn

- Integrate GroupDocs.Editor into your Java projects  
- Open Excel files **without password** or with correct/incorrect passwords  
- Manage incorrect password attempts effectively  
- **Add write protection Excel** and set new passwords when saving  
- Optimize performance for document processing  

## Prerequisites

Before we begin, ensure you have the following:

- **Java Development Kit (JDK)**: Version 8 or higher is required.  
- **Maven**: For managing dependencies and building your project efficiently.  
- **Basic Java Knowledge**: Familiarity with Java syntax and concepts is recommended.  
- **GroupDocs.Editor Library**: We'll be using version 25.3, which you can include via Maven.  

## Setting Up GroupDocs.Editor for Java

To start working with GroupDocs.Editor in your Java projects, follow these installation steps:

### Using Maven

Add the following repository and dependency to your `pom.xml` file:

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

### Direct Download

Alternatively, download the latest version from [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

#### License Acquisition

- **Free Trial**: Start by downloading a free trial version to explore the features.  
- **Temporary License**: Apply for a temporary license to remove any limitations during your evaluation period.  
- **Purchase**: For production use, purchase a license from [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Basic Initialization

To initialize GroupDocs.Editor in your Java application:

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Implementation Guide

We'll break down the implementation into four distinct features, each addressing a specific functionality related to document security.

### How to Open Excel Without Password

If you need to check whether a workbook can be accessed without a password, this snippet demonstrates the approach.

#### Step 1 – Import Required Classes

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

#### Step 2 – Initialize the Editor

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

#### Step 3 – Attempt to Open Without a Password

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### Troubleshooting Tips
- Verify that the file path points to an existing workbook.  
- Catch `PasswordRequiredException` to gracefully handle protected files.

### How to Open Excel With Incorrect Password

When a user supplies the wrong password, `IncorrectPasswordException` is thrown. This example shows how to capture that scenario.

#### Step 1 – Import Required Classes

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### Step 2 – Set Up Load Options with an Incorrect Password

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Step 3 – Handle the Incorrect Password Exception

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### Troubleshooting Tips
- Ensure the password you pass is indeed wrong for testing purposes.  
- Use this pattern to inform end‑users that their credential entry failed.

### How to Open Excel With Correct Password

This section demonstrates the proper way to open a password‑protected workbook using the right credentials, enabling **groupdocs password protection** features.

#### Step 1 – Import Required Classes

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

#### Step 2 – Configure Load Options with the Correct Password

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

**Key Configuration Options**  
- `setOptimizeMemoryUsage(true)`: Reduces memory footprint when working with large spreadsheets.

### How to Save Excel with Password and Add Write Protection Excel

Now we combine everything: open the workbook with the correct password, then **save Excel with password** while also applying **add write protection excel** to prevent unauthorized edits.

#### Step 1 – Import Required Classes

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

#### Step 2 – Load the Protected Workbook

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Step 3 – Configure Save Options with a New Password and Write Protection

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### Troubleshooting Tips
- Choose a strong `new_password` to keep the file secure.  
- The `WorksheetProtectionType.All` flag protects every sheet against editing without the `write_password`.

## Practical Applications

1. **Secure Data Sharing** – Protect confidential financial models before emailing them to stakeholders.  
2. **Automated Document Pipelines** – Integrate these snippets into batch jobs that process and re‑encrypt large numbers of spreadsheets.

## Conclusion

By mastering the use of GroupDocs.Editor in Java, you can confidently **save Excel with password**, open files with or without passwords, and **add write protection Excel** to safeguard your data. These capabilities give you fine‑grained control over workbook security, helping you meet compliance requirements and protect intellectual property.

---

**Last Updated:** 2026-02-01  
**Tested With:** GroupDocs.Editor 25.3  
**Author:** GroupDocs  

---