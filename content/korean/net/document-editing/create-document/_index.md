---
date: 2026-09-21
description: GroupDocs.Editor for .NET을 사용하여 Office 없이 PowerPoint를 편집하고, Word, Excel,
  EPUB을 편집하며 편집된 문서 스트림을 캡처하는 방법을 알아보세요.
keywords:
- edit powerpoint without office
- GroupDocs.Editor .NET
- document editing .NET
- edit presentation programmatically
lastmod: 2026-09-21
linktitle: 문서 만들기
og_description: GroupDocs.Editor for .NET을 사용하여 Office 없이 PowerPoint를 편집합니다. 이 가이드는
  프레젠테이션, Word, Excel, EPUB을 수정하고 편집된 문서 스트림을 저장하는 방법을 보여줍니다.
og_image_alt: Guide showing code to edit PowerPoint presentations without Microsoft
  Office using GroupDocs.Editor for .NET
og_title: Office 없이 GroupDocs.Editor for .NET으로 PowerPoint 편집
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to edit PowerPoint without Office using GroupDocs.Editor
    for .NET, edit Word, Excel, EPUB and capture the edited document stream.
  headline: Edit powerpoint without office with GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: You can edit WordProcessing, spreadsheets, presentations, ebooks, and
      emails—including PowerPoint files for the **edit powerpoint without office**
      use case.
    question: What types of documents can I edit with GroupDocs.Editor for .NET?
  - answer: Yes, each format has its own options class (e.g., `WordProcessingEditOptions`,
      `SpreadsheetEditOptions`, `PresentationEditOptions`) that let you fine‑tune
      pagination, hidden slides, worksheet selection, etc.
    question: Is it possible to customize the editing options?
  - answer: Use the callback function (`SaveNewDocument`) to capture the edited stream,
      then you can write it to disk, a database, or return it from a web API.
    question: How do I handle the output of the edited documents?
  - answer: Yes, a license is required for production. You can obtain one from the
      [GroupDocs.Editor purchase page](https://purchase.groupdocs.com/buy). A temporary
      trial license is also available.
    question: Do I need a license to use GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation page](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find more detailed documentation?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit powerpoint
- GroupDocs.Editor
- .NET document processing
title: Office 없이 GroupDocs.Editor for .NET으로 PowerPoint 편집
type: docs
url: /ko/net/document-editing/create-document/
weight: 10
---

# Office 없이 PowerPoint 편집 - GroupDocs.Editor for .NET

## 소개
프로그래밍 방식으로 **Office 없이 PowerPoint 편집**을 위한 신뢰할 수 있는 방법을 찾고 있다면, GroupDocs.Editor for .NET이 답입니다. 이 라이브러리를 사용하면 Word, Excel, PowerPoint, Ebook, Email 형식을 모두 단일하고 사용하기 쉬운 API로 작업할 수 있습니다. 이 튜토리얼에서는 지원되는 각 문서 유형을 생성하고 편집하는 과정을 단계별로 안내하고, **편집된 문서** 스트림을 **저장하는 방법**을 보여드리며, 실제 프로젝트에 적용할 수 있는 실용적인 팁을 제공합니다.

## 빠른 답변
- **.NET에서 PowerPoint 파일을 편집할 수 있는 라이브러리는 무엇인가요?** GroupDocs.Editor for .NET.  
- **같은 API로 Word, Excel, Epub 파일을 편집할 수 있나요?** 예, 동일한 `Editor` 클래스가 모든 형식을 지원합니다.  
- **편집된 파일을 어떻게 캡처하나요?** 결과 스트림을 받는 콜백 함수(예: `SaveNewDocument`)를 제공하면 됩니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 예—라이선스를 구매하거나 임시 체험 라이선스를 사용하십시오.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.0+, .NET Core, .NET 5/6.

## Office 없이 PowerPoint 편집이란?
Office 없이 PowerPoint 프레젠테이션을 편집한다는 것은 `.pptx` 파일을 로드하고, 슬라이드, 텍스트 또는 숨겨진 요소를 수정하는 등의 변경을 적용한 뒤, 업데이트된 파일을 가져오는 것을 의미합니다—서버에 Microsoft PowerPoint가 설치되어 있을 필요가 없습니다.

## 왜 GroupDocs.Editor for .NET을 사용해야 하나요?
GroupDocs.Editor는 **5개 이상의 주요 문서 유형**(Word, Excel, PowerPoint, EPUB, Email)을 지원하며, 스트림 기반 아키텍처 덕분에 파일 크기가 **500 MB**까지 처리하면서 메모리 사용량을 **100 MB** 이하로 유지합니다. 이 라이브러리는 **Windows, Linux, macOS**에서 실행되어 클라우드 네이티브 서비스, CI 파이프라인, 컨테이너화된 워크로드에 이상적입니다.

## 사전 요구 사항
- Visual Studio(최근 버전 중 하나).  
- .NET Framework 4.0 이상(또는 .NET Core/.NET 5+).  
- GroupDocs.Editor for .NET 라이브러리 – [GroupDocs.Editor for .NET 라이브러리 다운로드](https://releases.groupdocs.com/editor/net/).  
- 기본 C# 지식.

## 네임스페이스 가져오기
`Editor` 클래스는 `GroupDocs.Editor` 네임스페이스에 존재하며, 형식별 옵션 클래스는 각각의 하위 네임스페이스에 위치합니다.

`Editor`는 문서를 로드하고, 편집 가능한 표현을 제공하며, 수정된 내용을 스트림에 다시 쓰는 핵심 클래스입니다.  

```csharp
using GroupDocs.Editor;
using GroupDocs.Editor.Options;
using System.IO;
```

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## 단계 1: 스트림 설정
스트림을 사용하면 전체 워크플로를 메모리 내에서 유지할 수 있어 웹 API나 서버리스 함수에 적합합니다.

`MemoryStream`은 디스크의 파일을 모방하지만 RAM에 머무르는 가볍고 확장 가능한 버퍼입니다.  

```csharp
byte[] fileBytes = File.ReadAllBytes("sample.pptx");
var inputStream = new MemoryStream(fileBytes);
```

```csharp
Stream memoryStream = Stream.Null;
```

## 단계 2: **편집된 문서 저장** 콜백 함수
콜백은 `Editor`가 처리를 마친 후 편집된 스트림을 받습니다. 이후 이를 디스크, 데이터베이스에 저장하거나 API 엔드포인트에서 반환할 수 있습니다.

`SaveNewDocument`는 편집이 완료되면 SDK가 자동으로 호출하는 사용자 정의 메서드입니다.  

```csharp
void SaveNewDocument(Stream editedStream)
{
    using var file = File.Create("output.pptx");
    editedStream.CopyTo(file);
}
```

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## 단계 3: 워드 프로세싱 문서 생성 및 편집  
(여기서는 **.NET에서 워드 문서 편집**을 수행합니다.)

### 기본 옵션으로 생성 및 편집
`WordProcessingEditOptions` 클래스는 DOCX 파일에 대한 합리적인 기본값을 제공합니다.

`WordProcessingEditOptions`는 편집기가 페이지 매김, 추적된 변경 사항, 임베디드 객체를 처리하는 방식을 정의합니다.  

```csharp
var editor = new Editor(inputStream, new WordProcessingEditOptions());
var editable = editor.Edit();
editable.Replace("{Placeholder}", "Actual value");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### 사용자 지정 옵션으로 생성 및 편집
맞춤법 검사나 변경 추적과 같은 특정 기능을 켜거나 끌 수 있습니다.

`WordProcessingEditOptions`를 사용하면 감사 추적을 위해 `EnableTrackChanges`를 활성화할 수 있습니다.  

```csharp
var options = new WordProcessingEditOptions
{
    EnableTrackChanges = true,
    EnableSpellCheck = false
};
var editor = new Editor(inputStream, options);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```

## 단계 4: 스프레드시트 문서 생성 및 편집  
(이것을 사용하여 **.NET에서 엑셀 파일 편집**을 수행합니다.)

### 기본 옵션으로 생성 및 편집
`SpreadsheetEditOptions`는 로드되는 워크시트와 수식 평가 여부를 제어합니다.

`SpreadsheetEditOptions`는 기본적으로 첫 번째 워크시트를 선택합니다.  

```csharp
var editor = new Editor(inputStream, new SpreadsheetEditOptions());
var editable = editor.Edit();
editable.ReplaceCell("A1", "42");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### 사용자 지정 옵션으로 생성 및 편집
성능을 위해 다른 워크시트 인덱스를 지정하거나 수식 평가를 비활성화할 수 있습니다.

`SpreadsheetEditOptions`를 사용하면 `WorksheetIndex`와 `EnableFormulaEvaluation`를 설정할 수 있습니다.  

```csharp
var options = new SpreadsheetEditOptions
{
    WorksheetIndex = 2,
    EnableFormulaEvaluation = false
};
var editor = new Editor(inputStream, options);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```

## 단계 5: Office 없이 PowerPoint 편집 – 프레젠테이션 문서 생성 및 편집
이는 우리의 주요 키워드 초점의 핵심입니다.

### 기본 옵션으로 생성 및 편집
`PresentationEditOptions`는 숨겨진 슬라이드를 포함할지 여부와 기본 편집 대상 슬라이드를 결정합니다.

`PresentationEditOptions`는 기본적으로 숨겨진 슬라이드를 포함하며, 이를 토글할 수 있습니다.  

```csharp
var editor = new Editor(inputStream, new PresentationEditOptions());
var editable = editor.Edit();
editable.ReplaceSlideText(0, "{Title}", "Quarterly Report");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### 사용자 지정 옵션으로 생성 및 편집
특정 슬라이드를 편집하려면 `SlideNumber`를 변경하거나 노트 페이지 포함을 비활성화할 수 있습니다.

`PresentationEditOptions`를 사용하면 `SlideNumber`와 `IncludeNotes`를 설정할 수 있습니다.  

```csharp
var options = new PresentationEditOptions
{
    SlideNumber = 2,
    IncludeNotes = false
};
var editor = new Editor(inputStream, options);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```

## 단계 6: 전자책 문서 생성 및 편집  
(여기서는 **epub 파일 편집**을 수행합니다.)

### 기본 옵션으로 생성 및 편집
`EbookEditOptions`는 EPUB과 내부 HTML 표현 간의 변환을 처리합니다.

`EbookEditOptions`는 EPUB 콘텐츠에 기본 HTML 렌더러를 사용합니다.  

```csharp
var editor = new Editor(inputStream, new EbookEditOptions());
var editable = editor.Edit();
editable.Replace("{Author}", "Jane Doe");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### 사용자 지정 옵션으로 생성 및 편집
원본 CSS를 보존하거나 순수 텍스트 레이아웃을 강제할 수 있습니다.

`EbookEditOptions`는 `PreserveCss`와 `PlainTextOnly` 플래그를 제공합니다.  

```csharp
var options = new EbookEditOptions
{
    PreserveCss = true,
    PlainTextOnly = false
};
var editor = new Editor(inputStream, options);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```

## 단계 7: 이메일 문서 생성 및 편집

### 기본 옵션으로 생성 및 편집
`EmailEditOptions`를 사용하면 .eml 파일의 본문, 제목 및 첨부 파일을 조작할 수 있습니다.

`EmailEditOptions`는 간단한 교체를 위해 이메일 본문을 순수 텍스트로 로드합니다.  

```csharp
var editor = new Editor(inputStream, new EmailEditOptions());
var editable = editor.Edit();
editable.Replace("{Recipient}", "john@example.com");
editor.Save(SaveNewDocument);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### 사용자 지정 옵션으로 생성 및 편집
원본 MIME 헤더를 유지하거나 깨끗한 텍스트 버전을 위해 제거할 수 있습니다.

`EmailEditOptions`는 MIME 메타데이터를 유지하거나 삭제하기 위해 `KeepHeaders`를 포함합니다.  

```csharp
var options = new EmailEditOptions
{
    KeepHeaders = false
};
var editor = new Editor(inputStream, options);
```

```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```

## 단계 8: 프로세스 마무리
작업이 끝나면 스트림을 폐기하여 리소스를 해제하십시오. 적절한 폐기는 웹 API나 백그라운드 워커와 같은 장기 실행 서비스에서 메모리 누수를 방지합니다.

```csharp
inputStream.Dispose();
```

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## 일반적인 함정 및 팁
- **스트림 폐기를 절대 잊지 마세요** – 열어두면 장기 실행 서비스에서 메모리 누수가 발생할 수 있습니다.  
- **PowerPoint를 편집할 때 `SlideNumber`를 올바르게 설정하세요**; 그렇지 않으면 첫 번째 슬라이드가 복제될 수 있습니다.  
- **원본 파일 이름을 유지해야 하는 경우**, 콜백 전에 저장하고 편집 후 출력 스트림의 이름을 바꾸세요.  
- **대용량 문서의 경우**, 청크 단위로 처리하거나 `Editor`를 임시 파일과 함께 사용하여 메모리 사용량을 줄이세요.  
- 프로덕션에서 예상치 못한 동작을 트러블슈팅해야 할 경우 `EditorOptions`를 통해 **로깅을 활성화**하세요.

## 자주 묻는 질문

**Q: GroupDocs.Editor for .NET으로 어떤 종류의 문서를 편집할 수 있나요?**  
A: WordProcessing, 스프레드시트, 프레젠테이션, 전자책, 이메일을 편집할 수 있습니다—특히 **Office 없이 PowerPoint 편집** 사용 사례를 위한 PowerPoint 파일도 포함됩니다.

**Q: 편집 옵션을 사용자 정의할 수 있나요?**  
A: 예, 각 형식마다 자체 옵션 클래스(`WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions` 등)가 있어 페이지 매김, 숨겨진 슬라이드, 워크시트 선택 등을 세밀하게 조정할 수 있습니다.

**Q: 편집된 문서의 출력을 어떻게 처리하나요?**  
A: 콜백 함수(`SaveNewDocument`)를 사용해 편집된 스트림을 캡처한 뒤, 이를 디스크, 데이터베이스에 저장하거나 웹 API에서 반환할 수 있습니다.

**Q: GroupDocs.Editor for .NET을 사용하려면 라이선스가 필요합니까?**  
A: 예, 프로덕션 사용에는 라이선스가 필요합니다. 라이선스는 [GroupDocs.Editor 구매 페이지](https://purchase.groupdocs.com/buy)에서 얻을 수 있으며, 임시 체험 라이선스도 제공됩니다.

**Q: 자세한 문서는 어디에서 찾을 수 있나요?**  
A: 자세한 문서는 [GroupDocs.Editor for .NET 문서 페이지](https://tutorials.groupdocs.com/editor/net/)에서 확인할 수 있습니다.

## 결론
GroupDocs.Editor for .NET을 사용하면 **Office 없이 PowerPoint 파일** 및 다양한 문서 유형을 손쉽게 **편집**할 수 있습니다. 위 단계들을 따르면 코드를 통해 문서를 생성·수정·**편집된 문서** 스트림을 저장할 수 있으며, Office 설치에 의존하지 않습니다. 라이브러리의 고급 옵션을 탐색하여 비즈니스 요구에 맞게 편집 환경을 맞춤 설정해 보세요.

---

**Last Updated:** 2026-09-21  
**테스트 대상:** GroupDocs.Editor for .NET (최신 릴리스)  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Editor .NET 프레젠테이션 문서 편집 튜토리얼](/editor/net/presentation-documents/)
- [GroupDocs.Editor .NET으로 편집 가능한 문서 만들기](/editor/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/)
- [옵션 없이 .NET에서 문서 로드 – GroupDocs.Editor 종합 가이드](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)