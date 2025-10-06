---
title: 문서 만들기
linktitle: 문서 만들기
second_title: GroupDocs.Editor .NET API
description: 이 포괄적인 단계별 자습서를 통해 .NET용 GroupDocs.Editor를 사용하여 Word, Excel, PowerPoint, Ebook 및 이메일 문서를 편집하는 방법을 알아보세요.
weight: 10
url: /ko/net/document-editing/create-document/
type: docs
---
# 문서 만들기

## 소개
다양한 문서 유형을 프로그래밍 방식으로 편집하는 데 따른 번거로움에 지치셨나요? .NET용 GroupDocs.Editor는 프로세스를 단순화하기 위해 여기에 있습니다. 이 강력한 도구를 사용하면 개발자는 Word, Excel, PowerPoint, Ebooks 및 이메일과 같은 다양한 문서 형식을 쉽게 편집할 수 있습니다. 이 자습서에서는 .NET용 GroupDocs.Editor를 사용하여 문서를 만들고 편집하는 방법을 자세히 살펴보겠습니다. 프로세스를 따라하기 쉬운 단계로 나누어 처음 접하는 사람이라도 쉽게 접근할 수 있도록 하겠습니다.
## 전제조건
시작하기 전에 다음 사항이 있는지 확인하세요.
- 컴퓨터에 Visual Studio가 설치되어 있습니다.
- .NET 프레임워크(4.0 이상).
-  .NET 라이브러리용 GroupDocs.Editor. 다음에서 다운로드할 수 있습니다.[여기](https://releases.groupdocs.com/editor/net/).
- C# 프로그래밍에 대한 기본 지식.
## 네임스페이스 가져오기
먼저 필요한 네임스페이스를 가져오겠습니다. 그러면 애플리케이션에서 필요한 클래스와 메서드에 액세스할 수 있게 됩니다.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## 1단계: 스트림 설정
우선, 문서 콘텐츠에 대한 자리 표시자 역할을 할 메모리 스트림을 설정해야 합니다.
```csharp
Stream memoryStream = Stream.Null;
```
## 2단계: 문서 저장을 위한 콜백 함수
다음으로 새 문서 스트림을 저장할 콜백 함수를 정의합니다. 이 기능은 문서 편집 프로세스의 출력을 처리하는 데 필수적입니다.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## 3단계: 워드프로세싱 문서 만들기 및 편집
 이제 Word 문서를 만들고 편집해 보겠습니다. 새로운 것을 만드는 것부터 시작하겠습니다.`Editor` 워드프로세싱 문서용 인스턴스를 만들고 기본 옵션으로 편집합니다.
### 기본 옵션으로 생성 및 편집
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### 사용자 정의 옵션으로 생성 및 편집
더 많은 제어를 위해 페이지 매김 비활성화 및 포함된 글꼴 추출과 같은 옵션을 지정할 수 있습니다.
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
## 4단계: 스프레드시트 문서 생성 및 편집
마찬가지로 Excel 문서를 만들고 편집할 수 있습니다. 방법은 다음과 같습니다.
### 기본 옵션으로 생성 및 편집
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### 사용자 정의 옵션으로 생성 및 편집
 특정 워크시트를 대상으로 하거나 숨겨진 워크시트를 제외하려면 다음을 사용합니다.`SpreadsheetEditOptions`.
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
## 5단계: 프리젠테이션 문서 생성 및 편집
PowerPoint 프레젠테이션도 지원됩니다. 어떻게 처리하는지 살펴보겠습니다.
### 기본 옵션으로 생성 및 편집
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### 사용자 정의 옵션으로 생성 및 편집
표시할 슬라이드, 숨겨진 슬라이드 포함 여부 등의 옵션을 지정하여 편집 내용을 사용자 정의할 수 있습니다.
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
## 6단계: 전자책 문서 생성 및 편집
GroupDocs.Editor를 사용하면 EPUB와 같은 전자책 형식을 편집할 수도 있습니다. 처리 방법은 다음과 같습니다.
### 기본 옵션으로 생성 및 편집
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### 사용자 정의 옵션으로 생성 및 편집
페이지 매기기 및 언어 정보를 활성화 또는 비활성화하여 전자책 편집을 사용자 정의하세요.
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
## 7단계: 이메일 문서 생성 및 편집
마지막으로 이메일 문서를 편집하는 방법을 살펴보겠습니다. 여기에는 EML과 같은 형식이 포함됩니다.
### 기본 옵션으로 생성 및 편집
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### 사용자 정의 옵션으로 생성 및 편집
편집 프로세스를 제어하려면 메일 메시지 출력 옵션을 지정하십시오.
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
## 8단계: 프로세스 마무리
문서를 편집한 후에는 메모리 스트림을 적절하게 처리하여 리소스를 확보하는 것이 중요합니다.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## 결론
.NET용 GroupDocs.Editor는 다양한 문서 유형을 프로그래밍 방식으로 편집하는 작업을 단순화할 수 있는 다재다능하고 강력한 도구입니다. 이 단계별 가이드를 따르면 워드프로세싱 파일, 스프레드시트, 프리젠테이션, 전자책, 이메일 등 문서를 쉽게 만들고 편집할 수 있습니다. 고급 기능과 사용자 정의 옵션을 알아보려면 GroupDocs.Editor 문서를 살펴보세요.
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 어떤 유형의 문서를 편집할 수 있나요?
워드프로세싱, 스프레드시트, 프리젠테이션, 전자책, 이메일 등 다양한 문서를 편집할 수 있습니다.
### 편집 옵션을 사용자 정의할 수 있나요?
예, .NET용 GroupDocs.Editor에서는 각 문서 유형에 맞는 다양한 편집 옵션을 통해 광범위한 사용자 정의가 가능합니다.
### 편집된 문서의 출력을 어떻게 처리합니까?
콜백 함수를 사용하여 편집된 문서 스트림을 원하는 위치에 저장할 수 있습니다.
### .NET용 GroupDocs.Editor를 사용하려면 라이센스가 필요합니까?
 예, 다음에서 라이센스를 얻을 수 있습니다.[여기](https://purchase.groupdocs.com/buy). 임시 라이센스 옵션도 있습니다.
### 더 자세한 문서는 어디서 찾을 수 있나요?
 자세한 문서는 다음에서 확인할 수 있습니다.[.NET 설명서 페이지용 GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).