---
title: PDF 문서 작업
linktitle: PDF 문서 작업
second_title: GroupDocs.Editor .NET API
description: 이 튜토리얼을 통해 .NET용 GroupDocs.Editor를 사용하여 PDF 문서를 편집하는 방법을 알아보세요. 콘텐츠를 수정하고, 대용량 파일을 처리하고, 편집 내용을 안전하게 저장하세요.
weight: 14
url: /ko/net/document-processing/work-pdf-documents/
type: docs
---
# PDF 문서 작업

## 소개
.NET용 GroupDocs.Editor를 사용하여 PDF 문서를 조작하고 편집하기 위한 포괄적인 안내서를 찾고 계십니까? 당신은 바로 이곳에 있습니다! 이 튜토리얼에서는 프로젝트 설정부터 편집된 PDF 문서 저장까지 전체 과정을 안내합니다. 숙련된 개발자이든 이제 막 시작하는 개발자이든 이 가이드는 유용하고 따라하기 쉽습니다. 뛰어들어보자!
## 전제조건
시작하기 전에 필요한 몇 가지 사항이 있습니다.
1. .NET 개발 환경: .NET 개발 환경이 설정되어 있는지 확인하세요. 이는 Visual Studio 또는 기타 선호하는 IDE일 수 있습니다.
2. .NET용 GroupDocs.Editor: .NET용 GroupDocs.Editor 라이브러리를 다운로드하고 설치합니다. 에서 받으실 수 있습니다.[릴리스 페이지](https://releases.groupdocs.com/editor/net/).
3. C#에 대한 기본 이해: 이 자습서에는 C# 코드 작성 및 이해가 포함되므로 C# 프로그래밍에 익숙하면 도움이 됩니다.
## 네임스페이스 가져오기
코드를 작성하기 전에 프로젝트에 필요한 네임스페이스를 가져왔는지 확인하세요.
```csharp
using System;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;
```
## 1단계: 입력 파일의 경로 가져오기
먼저 PDF 문서의 경로를 지정해야 합니다. 이 튜토리얼에서는 샘플 PDF 파일이 있다고 가정합니다.
```csharp
string inputFilePath = "Your Sample Document.pdf";
```
## 2단계: 경로에서 스트림 생성
다음으로, 지정한 경로에서 파일 스트림을 생성합니다. 이 스트림은 PDF 문서를 읽는 데 사용됩니다.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 3단계: 문서에 대한 로드 옵션 만들기
PDF 문서를 로드하려면 로드 옵션을 지정해야 합니다. PDF가 비밀번호로 보호되어 있는 경우 여기에 비밀번호를 제공할 수 있습니다.
```csharp
Options.PdfLoadOptions loadOptions = new PdfLoadOptions();
// 문서가 비밀번호로 보호되어 있는 경우
loadOptions.Password = "your_password";
```
## 4단계: 편집기 인스턴스에 문서 로드
이제 파일 스트림 및 로드 옵션을 사용하여 문서를`Editor` 사례.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    var documentInfo = editor.GetDocumentInfo(null);
```
## 5단계: 편집 옵션 생성
문서의 편집 옵션을 설정합니다. 이 경우 페이지 매김 모드를 활성화하겠습니다.
```csharp
Options.PdfEditOptions editOptions = new PdfEditOptions();
editOptions.EnablePagination = true;
```
## 6단계: 중간 편집 가능한 문서 만들기
편집기 인스턴스와 편집 옵션을 사용하여 편집 가능한 중간 문서를 만듭니다.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // 텍스트 콘텐츠를 HTML 마크업으로 추출
    string originalContent = beforeEdit.GetContent();
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 7단계: 콘텐츠 수정
필요에 따라 문서의 내용을 수정합니다. 여기서는 단순히 문서의 단어를 바꾸는 것입니다.
```csharp
string editedContent = originalContent.Replace("document", "edited document");
```
## 8단계: 편집된 콘텐츠로 편집 가능한 새 문서 만들기
 새로 만들기`EditableDocument` 편집된 콘텐츠와 리소스가 포함된 인스턴스입니다.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
    string originalContent3 = afterEdit.GetContent();
```
## 9단계: 문서 저장 옵션 만들기
PDF 문서의 저장 옵션을 지정합니다. 출력 문서에 대한 비밀번호를 설정할 수도 있습니다.
```csharp
FixedLayoutFormats docmFormat = FixedLayoutFormats.Pdf;
Options.PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.Password = "output_password";
saveOptions.OptimizeMemoryUsage = true;
```
## 10단계: 편집된 문서 저장
마지막으로 편집된 문서를 지정된 출력 경로에 저장합니다.
```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + docmFormat.Extension;
string outputPath = Path.Combine("OutputDirectoryPath", outputFilename);
using (FileStream outputStream = File.Create(outputPath))
{
    editor.Save(afterEdit, outputStream, saveOptions);
}
```

## 결론
거기 있어요! 다음 단계를 수행하면 .NET용 GroupDocs.Editor를 사용하여 PDF 문서를 성공적으로 편집할 수 있습니다. 이 강력한 라이브러리를 사용하면 프로그래밍 방식으로 PDF 파일을 쉽게 조작하고 저장할 수 있습니다. 간단한 텍스트 교체이든 더 복잡한 수정이든 .NET용 GroupDocs.Editor가 도와드립니다.
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 다른 문서 형식을 편집할 수 있습니까?
예, .NET용 GroupDocs.Editor는 Word, Excel, PowerPoint 등을 포함한 다양한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Editor의 무료 평가판을 받으려면 어떻게 해야 합니까?
 다음에서 무료 평가판을 다운로드할 수 있습니다.[GroupDocs.Editor 무료 평가판 페이지](https://releases.groupdocs.com/).
### .NET용 GroupDocs.Editor를 사용하여 대용량 PDF 문서를 처리할 수 있습니까?
예, .NET용 GroupDocs.Editor에는 메모리 사용을 최적화하는 옵션이 포함되어 있어 대용량 문서를 처리하는 데 적합합니다.
### 문제가 발생하면 어떻게 지원을 받을 수 있나요?
 지원을 받으려면 다음을 방문하세요.[GroupDocs.Editor 지원 포럼](https://forum.groupdocs.com/c/editor/20).
### PDF 문서를 저장하는 동안 암호화할 수 있나요?
예, 저장 과정에서 PDF 문서를 암호화하기 위한 비밀번호를 설정할 수 있습니다.`PdfSaveOptions.Password` 재산.