---
date: 2026-06-06
description: GroupDocs.Editor for .NET를 사용하여 지원되는 문서 형식을 나열하고 파일 형식 확장자를 확인하는 방법을
  배웁니다. 코드 스니펫, 빠른 답변 및 FAQ가 포함된 단계별 가이드.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: 지원되는 문서 형식 나열
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor .NET를 사용하여 지원되는 문서 형식 나열
type: docs
url: /ko/net/document-processing/work-document-formats/
weight: 13
---

# 지원되는 문서 형식 나열

GroupDocs.Editor for .NET와 함께 **지원되는 문서 형식을 나열하는 방법**에 대한 포괄적인 튜토리얼에 오신 것을 환영합니다. 문서 중심의 웹 앱을 구축하든 엔터프라이즈급 데스크톱 도구를 만들든, 편집하거나 변환할 수 있는 형식을 정확히 아는 것이 필수적입니다. 이 가이드에서는 형식을 열거하고, 확장자를 파싱하며, 문서를 편집하는 방법을 알아볼 수 있습니다—명확하고 이해하기 쉬운 설명과 바로 실행 가능한 코드 스니펫을 제공합니다.

## 빠른 답변
- **모든 지원 형식을 어떻게 나열합니까?** `DocumentFormatInfo.GetSupportedWordProcessingFormats()`(또는 Presentation/Spreadsheet 동등 메서드)를 사용하고 컬렉션을 반복합니다.  
- **파일 확장자에서 형식을 결정할 수 있나요?** 예—`DocumentFormatInfo.FromExtension(".docx")`를 호출합니다.  
- **GroupDocs.Editor가 지원하는 파일 유형은 무엇인가요?** DOCX, XLSX, PPTX, HTML, 일반 텍스트 등을 포함한 30개 이상의 입력 및 출력 형식이 있습니다.  
- **형식을 나열하려면 라이선스가 필요합니까?** 임시 라이선스를 사용하면 전체 API가 해제됩니다; 그렇지 않으면 제한된 기능으로 체험판을 사용할 수 있습니다.  
- **호환되는 .NET 버전은 무엇인가요?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## “지원되는 문서 형식 나열”이란 무엇인가요?
이 문구는 GroupDocs.Editor가 열고, 편집하고, 저장할 수 있는 파일 유형 컬렉션을 프로그래밍 방식으로 가져오는 것을 의미합니다. 이 작업을 통해 동적 UI 드롭다운을 만들거나 처리 전에 사용자 업로드를 검증하여 호환 가능한 파일만 편집기로 전달되도록 할 수 있습니다.

## 지원되는 문서 형식을 나열해야 하는 이유는 무엇인가요?
GroupDocs.Editor는 **30개 이상의 입력 및 출력 형식**을 지원하며 전체 문서를 메모리에 로드하지 않고 **2 GB**까지의 파일을 처리할 수 있습니다. 정확한 목록을 알면 런타임 오류를 방지하고 사용자 경험을 향상시키며 “편집 가능한 Office 문서만 허용”과 같은 비즈니스 규칙을 적용할 수 있습니다. 또한 애플리케이션이 실제로 지원하는 형식만 사용자에게 표시하는 데 도움이 됩니다.

## 사전 요구 사항
시작하기 전에 다음을 확인하십시오:

1. **.NET 개발 환경** – Visual Studio 2022 또는 .NET 6+를 지원하는 모든 IDE.  
2. **GroupDocs.Editor for .NET 라이브러리** – [GroupDocs releases page](https://releases.groupdocs.com/editor/net/)에서 다운로드합니다.  
3. **임시 라이선스** – 제한 없는 접근을 위해 [temporary license](https://purchase.groupdocs.com/temporary-license/)를 획득합니다.  
4. **기본 C# 지식** – 네임스페이스, `using` 구문, 콘솔 출력에 익숙함.

## 지원되는 문서 형식을 나열하는 방법은?
지원되는 형식 컬렉션을 로드하고 각 형식의 이름과 파일 확장자를 출력합니다. 이 두 단계 패턴은 워드 프로세싱, 스프레드시트, 프레젠테이션 문서에 모두 적용됩니다. 컬렉션을 반복함으로써 드롭다운과 같은 UI 요소를 동적으로 채울 수 있어 사용자가 편집기가 실제로 처리할 수 있는 형식만 선택하도록 보장합니다.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### 워드 프로세싱 형식 나열
`Formats.WordProcessingFormats`는 편집기가 인식하는 모든 워드 프로세싱 파일 유형을 설명하는 열거형입니다. `All` 속성은 이러한 형식 객체들의 컬렉션을 반환합니다.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**설명:**  
1. **형식 반복:** 사용 가능한 모든 워드 프로세싱 형식을 반복합니다.  
2. **형식 세부 정보 출력:** 각 형식에 대해 친숙한 이름과 기본 파일 확장자를 출력합니다.

### 프레젠테이션 형식 나열
`Formats.PresentationFormats`는 슬라이드 파일에 대해 동일하게 작동하며, `All` 컬렉션을 통해 지원되는 각 프레젠테이션 유형을 노출합니다.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**설명:**  
1. **형식 반복:** 프레젠테이션에도 동일한 반복 로직이 적용됩니다.  
2. **형식 세부 정보 출력:** 각 형식의 이름과 확장자가 표시됩니다.

## 파일 형식 확장자를 결정하는 방법은?
때때로 파일 이름만 가지고 해당 `DocumentFormat`을 추론해야 할 때가 있습니다. GroupDocs.Editor는 파일 확장자를 내부 형식 표현에 매핑하는 간단한 정적 헬퍼를 제공하여, 편집기에 로드하기 전에 파일을 검증하거나 변환할 수 있게 합니다.

### 스프레드시트 형식 파싱
`Formats.SpreadsheetFormats.FromExtension`은 파일 확장자 문자열을 해당 스프레드시트 형식 열거값으로 변환합니다.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**설명:**  
1. **형식 파싱:** `FromExtension`은 `.xlsm` 확장자를 내부 `SpreadsheetFormat` 열거형으로 변환합니다.  
2. **형식 출력:** 파싱된 형식의 이름이 출력되어 매핑을 확인합니다.

### 텍스트 형식 파싱
마찬가지로, `Formats.TextualFormats.FromExtension`은 HTML이나 TXT와 같은 텍스트 파일 확장자를 해결합니다.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**설명:**  
1. **형식 파싱:** `FromExtension` 메서드는 `html` 확장자를 `TextFormat`으로 해결합니다.  
2. **형식 출력:** 텍스트 형식의 이름이 표시되어 웹 기반 편집기에 유용합니다.

## 형식을 식별한 후 문서를 편집하는 방법은?
형식을 알게 되면 문서를 로드하고 편집하는 과정은 일관된 패턴을 따릅니다. 먼저 소스 파일 경로로 `Editor` 인스턴스를 생성하고, `Edit()`를 호출해 `EditableDocument`를 얻습니다. 이후 적절한 `SaveOptions`를 사용해 내용을 읽고, 수정하고, 최종적으로 저장할 수 있습니다.

### 문서 로드
`Editor`는 주어진 파일에 대한 모든 편집 작업을 캡슐화하는 핵심 클래스입니다.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**설명:**  
1. **Editor 초기화:** 대상 파일의 전체 경로를 전달하여 `Editor` 인스턴스를 생성합니다.  
2. **Dispose 패턴:** `using` 문은 모든 비관리 리소스가 즉시 해제되도록 보장합니다.

### 콘텐츠 추출
`EditableDocument.GetContent()`는 문서의 원시 텍스트(또는 웹 기반 편집기의 경우 HTML)를 반환하며, 이를 표시하거나 조작할 수 있습니다.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**설명:**  
1. **Edit 메서드:** `Edit()`는 `EditableDocument` 객체를 반환합니다.  
2. **콘텐츠 가져오기:** `GetContent()`는 문서의 원시 텍스트(또는 웹 기반 편집기의 경우 HTML)를 추출합니다.  
3. **콘텐츠 출력:** 검증을 위해 콘솔에 내용을 출력합니다.

### 변경 사항 저장
`SaveOptions`는 편집된 문서를 저장소에 어떤 형식으로 쓸지 편집기에 알려줍니다.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**설명:**  
1. **Edit 메서드:** 수정 후 `EditableDocument`를 다시 가져옵니다.  
2. **콘텐츠 수정:** 문자열에 변경 사항을 적용합니다(여기서는 표시되지 않음).  
3. **저장 옵션:** 원하는 출력 형식으로 `SaveOptions`를 구성합니다.  
4. **문서 저장:** 편집된 파일을 디스크에 저장합니다.

## 다양한 문서 유형을 다루는 방법은?
GroupDocs.Editor는 Word, Spreadsheet, Presentation 처리를 동일한 API 인터페이스 뒤에 추상화하여, 각 문서군마다 새로운 클래스를 배울 필요 없이 컨텍스트를 쉽게 전환할 수 있게 합니다.

### 스프레드시트 문서 편집
`SpreadsheetSaveOptions`는 형식 및 선택적 압축 설정을 포함하여 스프레드시트를 쓰는 방식을 정의합니다.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**설명:**  
1. **Editor 초기화:** 스프레드시트 파일 경로를 `Editor` 생성자에 전달합니다.  
2. **Edit 메서드:** `EditableDocument`를 가져옵니다.  
3. **콘텐츠 가져오기:** 스프레드시트의 CSV 표현(또는 HTML)을 출력합니다.  
4. **콘텐츠 수정:** 필요한 셀 수준 변경을 적용합니다.  
5. **저장 옵션:** 적절한 `SpreadsheetSaveOptions`를 선택합니다.  
6. **문서 저장:** 업데이트된 스프레드시트를 저장소에 기록합니다.

### 프레젠테이션 문서 편집
`PresentationSaveOptions`는 슬라이드 덱의 출력 형식을 제어하며, 원본 파일 유형을 유지하거나 변경할 수 있게 합니다.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**설명:**  
1. **Editor 초기화:** `Editor`를 통해 PowerPoint 파일을 로드합니다.  
2. **Edit 메서드:** `EditableDocument`를 얻습니다.  
3. **콘텐츠 가져오기:** 슬라이드 HTML 또는 일반 텍스트를 추출합니다.  
4. **콘텐츠 수정:** 제목, 글머리표 또는 이미지를 업데이트합니다.  
5. **저장 옵션:** `PresentationSaveOptions`를 사용해 출력 형식을 정의합니다.  
6. **문서 저장:** 편집된 프레젠테이션을 저장합니다.

## 일반적인 문제 및 해결책
- **“지원되지 않는 형식” 오류:** 최신 GroupDocs.Editor 버전을 사용하고 있는지 확인하십시오; 최신 Office 형식 지원이 정기적으로 추가됩니다.  
- **대용량 파일 메모리 사용량:** 문서를 로드하기 전에 `EditorSettings.EnableStreaming = true`로 설정하여 스트리밍 모드를 활성화합니다.  
- **라이선스 적용 안 됨:** 임시 라이선스 파일이 애플리케이션 루트에 있거나 `License license = new License(); license.SetLicense("path/to/license.lic");`를 통해 로드되었는지 확인합니다.

## 자주 묻는 질문

**Q: `DocumentFormatInfo`와 `SaveOptions`의 차이점은 무엇인가요?**  
A: `DocumentFormatInfo`는 지원되는 파일 유형에 대한 메타데이터를 제공하고, `SaveOptions`는 문서를 디스크에 다시 쓸 때(형식, 압축 등) 어떻게 구성할지를 정의합니다.

**Q: 사용자 정의 파일 확장자에 대한 형식을 나열할 수 있나요?**  
A: 예—`DocumentFormatInfo.FromExtension("yourExt")`를 사용합니다; 확장자를 인식하지 못하면 메서드는 `null`을 반환합니다.

**Q: GroupDocs.Editor가 비밀번호로 보호된 파일을 지원하나요?**  
A: 물론입니다. `EditorSettings`를 통해 비밀번호를 `Editor` 생성자에 전달하면 암호화된 문서를 열 수 있습니다.

**Q: GroupDocs.Editor가 실제로 지원하는 형식은 몇 개인가요?**  
A: **30개 이상의 입력 및 출력 형식**을 지원하며, Word, Excel, PowerPoint, HTML, 일반 텍스트 등을 포함합니다.

**Q: 편집 가능한 형식만 목록에 포함하도록 제한할 수 있나요?**  
A: `GetEditableWordProcessingFormats()`(또는 Spreadsheet/Presentation 동등 메서드)를 사용하면 전체 편집 기능을 허용하는 형식을 가져올 수 있습니다.

## 추가 리소스
- [GroupDocs releases page](https://releases.groupdocs.com/editor/net/)에서 라이브러리를 다운로드합니다.  
- 전체 기능 접근을 위해 [temporary license](https://purchase.groupdocs.com/temporary-license/)를 획득합니다.  
- [free trial](https://releases.groupdocs.com/)로 제품을 사용해 보세요.  
- [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/)에서 자세한 사용 예제를 살펴보세요.  
- [support forum](https://forum.groupdocs.com/c/editor/20)에서 커뮤니티의 도움을 받으세요.

## 결론
이 가이드를 따라 이제 **지원되는 문서 형식 나열**, **확장자를 통해 파일 형식 결정**, 그리고 GroupDocs.Editor for .NET을 사용한 Word, Spreadsheet, Presentation 유형의 **문서 편집** 방법을 알게 되었습니다. 이러한 스니펫을 프로젝트에 통합하면 견고하고 형식 인식을 갖춘 애플리케이션을 구축하여 최종 사용자에게 만족을 주고 런타임 오류를 줄일 수 있습니다.

---

**마지막 업데이트:** 2026-06-06  
**테스트 환경:** GroupDocs.Editor 23.9 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Editor와 함께 .NET에서 문서 로딩 마스터하기: 포괄적인 가이드](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [GroupDocs.Editor와 함께 .NET에서 문서 편집 마스터하기: 포괄적인 가이드](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [GroupDocs.Editor .NET을 사용해 Word를 HTML로 변환하기: 단계별 가이드](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)