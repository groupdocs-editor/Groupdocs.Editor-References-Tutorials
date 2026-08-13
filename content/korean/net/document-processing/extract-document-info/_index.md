---
date: 2026-06-01
description: GroupDocs.Editor for .NET를 사용하여 페이지 수를 확인하고 문서 메타데이터를 추출하는 방법을 자세한 단계별
  튜토리얼에서 배워보세요.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: 페이지 수 확인 및 문서 정보 추출
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor로 페이지 수 확인 및 문서 정보 추출
type: docs
url: /ko/net/document-processing/extract-document-info/
weight: 10
---

# 페이지 수 가져오기 및 GroupDocs.Editor로 문서 정보 추출

## 소개
이 포괄적인 튜토리얼에서는 **get page count**를 수행하고 GroupDocs.Editor for .NET을 사용하여 형식, 크기 및 암호화 상태를 포함한 자세한 문서 정보를 추출하는 방법을 배웁니다. 문서 관리 시스템, 보고 엔진 또는 자동 변환 파이프라인을 구축하든, 파일 메타데이터를 이해하는 것이 안정적인 처리를 위한 첫 번째 단계입니다. 파일을 로드하는 것부터 리소스를 안전하게 해제하는 것까지 전체 워크플로를 단계별로 살펴보겠습니다.

## 빠른 답변
- **문서의 페이지 수를 어떻게 가져오나요?**  
  파일을 `Editor`로 로드한 후 `editor.GetDocumentInfo().PageCount`를 호출합니다.
- **메타데이터 추출을 지원하는 파일 형식은 무엇인가요?**  
  DOCX, XLSX, PPTX, PDF, TXT, HTML 등을 포함한 50개 이상의 형식이 지원됩니다.
- **암호로 보호된 파일에서도 메타데이터를 추출할 수 있나요?**  
  예—`Editor` 인스턴스를 생성할 때 비밀번호를 제공하면 됩니다.
- **리소스를 수동으로 해제해야 하나요?**  
  물론입니다; 항상 `editor.Dispose()`를 호출하거나 `using` 블록으로 에디터를 감싸야 합니다.
- **필요한 GroupDocs.Editor 버전은 무엇인가요?**  
  작성 시점 최신 안정 버전(v23.12 이상)에서 모든 기능을 지원합니다.

## GroupDocs.Editor에서 “get page count”란 무엇인가요?
`GetDocumentInfo()`는 문서의 페이지 수, 형식, 크기 및 기타 메타데이터를 포함하는 `DocumentInfo` 객체를 반환하는 메서드입니다. 이 한 번의 호출만으로 파일을 수동으로 파싱하지 않고도 즉시 정보를 얻을 수 있습니다. 이 메서드를 사용하면 전체 문서를 메모리에 로드하지 않아 대용량 파일의 성능이 향상되고 서버 리소스 사용량이 감소합니다.

## 왜 GroupDocs.Editor로 문서 메타데이터를 추출해야 할까요?
GroupDocs.Editor는 **50개 이상의 입력 및 출력 형식**을 처리하고 전체 문서를 메모리에 로드하지 않고 **2 GB**까지의 파일 메타데이터를 가져올 수 있습니다. 이 효율성은 전체 문서 파싱에 비해 서버 부하를 **70 %**까지 감소시켜 고처리량 애플리케이션에 이상적입니다.

## 전제 조건
- **C# 개발 기본** – Visual Studio와 .NET 프로젝트 구조에 익숙해야 합니다.
- **Visual Studio 2022**(또는 최신 버전) 가 설치되어 있어야 합니다.
- **GroupDocs.Editor for .NET** – 최신 패키지는 [download page](https://releases.groupdocs.com/editor/net/)에서 다운로드하세요.

## 문서를 어떻게 로드하나요?
`Editor`는 문서를 나타내는 주요 클래스이며 로드 및 조작 메서드를 제공합니다. 파일 경로를 전달하여 `Editor` 인스턴스를 생성하면 대상 파일을 로드할 수 있습니다. 에디터는 형식을 자동으로 감지하므로 로드 옵션을 지정할 필요가 없습니다. 이 방법은 모든 지원 파일 유형에 적용되며 초기 설정을 단순화합니다.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## 문서 정보를 어떻게 가져오나요?
`GetDocumentInfo()`는 페이지 수, 형식, 크기 및 암호화 상태와 같은 메타데이터를 포함하는 `DocumentInfo` 객체를 반환합니다. 로드 후 이 메서드를 호출하면 객체를 가져올 수 있습니다. 반환된 `DocumentInfo`는 파일 특성의 간결한 스냅샷을 제공하여 추가 처리 없이도 결정을 내릴 수 있게 합니다.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## 문서 유형을 어떻게 결정하나요?
`DocumentType`은 문서가 WordProcessing, Spreadsheet 또는 Text인지 나타내는 열거형입니다. 파일이 워드 프로세싱 문서인지, 스프레드시트인지, 일반 텍스트인지 여부를 알면 이후 처리 방식을 결정하는 데 영향을 줍니다. `DocumentInfo` 객체의 `DocumentType` 속성을 사용하여 이 결정을 내리고 로직을 분기하세요.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## 워드 프로세싱 파일에 대한 자세한 정보를 어떻게 추출하나요?
`WordProcessing`은 DOCX, ODT, RTF와 같은 워드 프로세싱 파일을 의미합니다. 문서 유형이 `WordProcessing`인 경우 `DocumentInfo` 객체에서 **format**, **extension**, **page count**, **size**, **encryption flag**와 같은 추가 속성을 직접 읽을 수 있습니다. 이러한 세부 정보는 특정 변환 적용이나 보안 검사와 같은 처리 단계를 맞춤화하는 데 도움이 됩니다.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## 스프레드시트 및 텍스트 문서는 어떻게 처리하나요?
`Spreadsheet`는 XLSX와 같은 스프레드시트 파일을 의미하고, `Text`는 일반 텍스트 문서를 나타냅니다. 스프레드시트(`Spreadsheet`)와 일반 텍스트 파일(`Text`)의 경우에도 `DocumentInfo` 객체는 핵심 메타데이터(확장자, 크기, 페이지 수)를 제공합니다. 일부 형식은 페이지 수를 제공하지 않을 수 있으며, 이 경우 값은 `0`이 됩니다. 이후 로직에서는 다른 메타데이터를 활용할 수 있습니다.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## 암호로 보호된 문서는 어떻게 처리하나요?
`Password`는 암호화된 파일을 열기 위해 `Editor` 생성자에 전달되는 문자열입니다. 문서가 암호화된 경우 먼저 비밀번호 없이 열어보세요. 실패하면 예외를 잡고 올바른 비밀번호로 다시 시도합니다. `Editor` 생성자는 이 목적을 위해 `Password` 매개변수를 받아 보호된 파일을 원활하게 처리할 수 있게 합니다.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## 텍스트 기반 문서는 어떻게 처리하나요?
`DocumentInfo`는 텍스트 파일에 대한 크기, 확장자, 인코딩과 같은 기본 메타데이터를 제공합니다. 텍스트 파일(예: `.txt`, `.md`)은 단순 스트림으로 처리됩니다. `DocumentInfo`에서 크기와 인코딩 정보를 여전히 가져올 수 있으며, 이는 파일 무결성 검증이나 적절한 처리 파이프라인을 결정하는 데 유용합니다.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## 리소스를 올바르게 해제하려면 어떻게 해야 하나요?
`Editor`는 비관리 리소스를 보유하는 주요 클래스이며 사용 후 반드시 해제해야 합니다. 메모리 누수를 방지하려면 정보 추출이 끝난 후 항상 `Editor` 인스턴스를 해제하세요. `using` 구문은 예외가 발생하더라도 해제를 보장하므로 가장 안전한 패턴이며, 깔끔한 리소스 관리를 보장합니다.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## 일반적인 문제와 해결책
| 문제 | 원인 | 해결책 |
|-------|-------|----------|
| **PageCount가 0을 반환함** | 형식이 페이지 매김을 지원하지 않음(예: 일반 텍스트) | `PageCount`에 의존하기 전에 `DocumentInfo.DocumentType`을 확인하세요. |
| **지원되지 않는 파일 형식** | 파일 확장자를 인식하지 못함 | 파일이 50개 이상의 지원 형식 중 하나인지 확인하고, GroupDocs.Editor를 최신 버전으로 업데이트하세요. |
| **비밀번호 예외** | 잘못된 비밀번호가 제공됨 | `PasswordProtectedException`을 잡고 사용자가 비밀번호를 다시 입력하도록 요청하세요. |
| **대용량 파일에서 메모리 급증** | 스트리밍 없이 매우 큰 PDF를 로드함 | `LoadOptions.LoadMode = LoadMode.Stream`을 사용하세요(`LoadOptions`에 포함, 최신 릴리스에서 사용 가능). |

## 자주 묻는 질문

**Q: 어떤 문서 유형의 메타데이터를 추출할 수 있나요?**  
A: GroupDocs.Editor는 워드 프로세싱, 스프레드시트, 프레젠테이션, PDF 및 일반 텍스트 파일을 지원하며, 총 50개 이상의 형식을 지원합니다.

**Q: 파일 확장자를 어떻게 가져오나요?**  
A: `GetDocumentInfo()`를 호출한 후 `DocumentInfo.Extension`에 접근하면 앞의 점 없이 확장자를 반환합니다.

**Q: 문서 크기를 메가바이트 단위로 얻을 수 있나요?**  
A: 예—`DocumentInfo.Size`는 바이트 단위 크기를 반환하므로 1,048,576으로 나누면 메가바이트로 변환됩니다.

**Q: 서버에서 암호로 보호된 파일을 처리하는 것이 안전한가요?**  
A: 물론입니다—GroupDocs.Editor는 비밀번호를 디스크에 기록하지 않으며 사용 후 모든 암호화 객체를 해제합니다.

**Q: 문제 발생 시 추가 도움을 어디서 찾을 수 있나요?**  
A: 다음 [GroupDocs.Editor 지원 포럼](https://forum.groupdocs.com/c/editor/20)에서 지원을 받을 수 있습니다.

---

**마지막 업데이트:** 2026-06-01  
**테스트 환경:** GroupDocs.Editor 23.12 for .NET  
**작성자:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## 관련 튜토리얼

- [GroupDocs.Editor를 사용한 .NET 메타데이터 추출 마스터: 포괄적인 가이드](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [GroupDocs.Editor for .NET 문서 로딩 튜토리얼](/editor/net/document-loading/)
- [GroupDocs.Editor .NET을 이용한 효율적인 문서 편집: HTML을 편집 가능한 문서로 변환](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)