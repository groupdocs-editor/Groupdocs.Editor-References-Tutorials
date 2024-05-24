---
title: 문서 저장
linktitle: 문서 저장
second_title: GroupDocs.Editor .NET API
description: .NET용 GroupDocs.Editor를 사용하여 문서를 손쉽게 편집하고 저장하세요. 이 단계별 가이드는 개발자의 프로세스를 단순화합니다.
type: docs
weight: 14
url: /ko/net/document-editing/save-document/
---
## 소개
.NET용 GroupDocs.Editor를 사용하여 문서를 쉽게 편집하고 저장하고 싶으십니까? 당신은 바로 이곳에 있습니다! 이 튜토리얼은 문서를 쉽게 관리할 수 있도록 프로세스를 단계별로 안내합니다. 숙련된 개발자이든 초보자이든 상관없이 저희 가이드는 시작하는 데 필요한 모든 정보를 제공합니다.
## 전제조건
튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
- 개발 환경: 컴퓨터에 Visual Studio가 설치되어 있습니다.
- .NET Framework: .NET Framework 4.6.1 이상이 있는지 확인하세요.
-  .NET용 GroupDocs.Editor: 최신 버전 다운로드[여기](https://releases.groupdocs.com/editor/net/).
- 기본 C# 지식: C# 프로그래밍에 대한 지식이 필수적입니다.
## 네임스페이스 가져오기
.NET 프로젝트에서 GroupDocs.Editor를 사용하려면 필요한 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
이제 환경을 설정하고 필요한 네임스페이스를 가져왔으므로 .NET용 GroupDocs.Editor를 사용하여 문서를 로드, 편집 및 저장하는 데 필요한 단계를 살펴보겠습니다.
## 1단계: 문서 로드
먼저 편집하려는 문서를 로드해야 합니다. GroupDocs.Editor는 이 프로세스를 간단하게 만듭니다. 방법은 다음과 같습니다.

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 이 단계에서는 편집하려는 문서의 경로를 지정하고`Editor` 수업. 그만큼`Edit` 그런 다음 문서를 로드하기 위해 메서드가 호출됩니다.`EditableDocument` 물체.
## 2단계: 문서 수정
문서가 로드되었으므로 이제 몇 가지 수정 작업을 수행할 차례입니다. WYSIWYG 편집기가 연결되어 있지 않으므로 코드에서 편집 프로세스를 시뮬레이션하겠습니다.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 여기에서는 문서에 포함된 HTML 콘텐츠를 검색하고, 간단한 텍스트 교체를 수행하고, 새`EditableDocument`수정된 HTML의 인스턴스입니다.
## 3단계: 문서 저장
문서를 편집한 후 마지막 단계는 문서를 저장하는 것입니다. GroupDocs.Editor는 문서를 다양한 형식으로 저장할 수 있는 여러 옵션을 제공합니다.
## RTF로 저장
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## DOCM으로 저장
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## 일반 텍스트로 저장
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## 4단계: 정리
 마지막으로, 폐기하는 것이 중요합니다.`EditableDocument` 그리고`Editor` 인스턴스를 사용하여 리소스를 확보합니다.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
다음 단계를 수행하면 .NET용 GroupDocs.Editor를 사용하여 문서를 효율적으로 로드, 편집 및 저장할 수 있습니다. 이 강력한 도구는 유연성과 사용 편의성을 제공하여 문서 관리를 간편하게 해줍니다.
## 결론
.NET용 GroupDocs.Editor를 사용하면 프로그래밍 방식으로 문서를 편집하고 저장하는 것이 그 어느 때보다 쉬워졌습니다. 이 가이드는 문서 로드부터 다양한 형식으로 저장까지 전체 과정을 안내했습니다. GroupDocs.Editor를 사용하면 다용도의 강력한 솔루션을 손쉽게 사용할 수 있어 문서 편집 프로세스가 단순화됩니다.
## FAQ
### GroupDocs.Editor는 어떤 파일 형식을 지원합니까?
GroupDocs.Editor는 DOCX, RTF, TXT 등을 포함한 다양한 파일 형식을 지원합니다. 전체 목록을 보려면 다음을 확인하세요.[선적 서류 비치](https://reference.groupdocs.com/editor/net/).
### 구매하기 전에 GroupDocs.Editor를 사용해 볼 수 있나요?
 예, 다음을 얻을 수 있습니다.[무료 시험판](https://releases.groupdocs.com/) GroupDocs.Editor의 기능을 테스트합니다.
### 문제가 발생하면 지원을 받을 수 있나요?
 전적으로! 당신은 방문 할 수 있습니다[지원 포럼](https://forum.groupdocs.com/c/editor/20) 발생한 문제에 대한 도움을 받으려면
### 임시면허는 어떻게 취득하나요?
 다음을 요청할 수 있습니다.[임시면허](https://purchase.groupdocs.com/temporary-license/) 평가 목적으로.
### GroupDocs.Editor 정식 버전은 어디서 구입할 수 있나요?
 정식 버전을 구매하실 수 있습니다[여기](https://purchase.groupdocs.com/buy).