---
title: .NET용 GroupDocs.Editor 소개
linktitle: .NET용 GroupDocs.Editor 소개
second_title: GroupDocs.Editor .NET API
description: 이 상세한 단계별 가이드를 통해 .NET용 GroupDocs.Editor를 사용하여 프로그래밍 방식으로 문서를 편집하는 방법을 알아보세요.
type: docs
weight: 12
url: /ko/net/document-editing/introduction-groupdocs-editor/
---
## 소개 
문서 편집 기능을 .NET 응용 프로그램에 원활하게 통합하려는 개발자라면 .NET용 GroupDocs.Editor를 고려해 볼 만한 강력한 도구입니다. 이 다목적 라이브러리를 사용하면 프로그래밍 방식으로 다양한 문서 형식을 로드, 편집 및 저장할 수 있습니다. Word 문서, PDF 또는 HTML 파일을 처리해야 하는 경우 GroupDocs.Editor는 프로세스를 단순화하여 효율적이고 간단하게 만듭니다. 이 자습서에서는 .NET용 GroupDocs.Editor 사용의 기본 사항을 살펴보고 실제 예제를 단계별로 안내합니다.
## 전제조건
구현을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
- 개발 환경: Visual Studio 2017 이상.
- .NET 프레임워크: .NET 프레임워크 4.6.1 이상.
-  .NET용 GroupDocs.Editor: 다음을 수행할 수 있습니다.[다운로드](https://releases.groupdocs.com/editor/net/) 사이트에서요.
-  라이센스: 유효한 라이센스 또는[임시면허](https://purchase.groupdocs.com/temporary-license/) GroupDocs에서.
## 네임스페이스 가져오기
.NET용 GroupDocs.Editor 사용을 시작하려면 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 문서 편집에 필요한 클래스 및 메서드에 대한 액세스를 제공합니다.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

이 섹션에서는 프로세스를 관리 가능한 단계로 나누어 워크플로의 각 부분을 이해할 수 있도록 하겠습니다.
## 1단계: 입력 파일의 경로 가져오기
먼저 편집하려는 문서의 경로를 지정해야 합니다. 이 예에서는 "Your Sample Document.docx"라는 DOCX 파일이 있다고 가정합니다.
```csharp
string inputFilePath = "Your Sample Document.docx";
```
## 2단계: Editor 개체 인스턴스화
 다음으로,`Editor` 입력 파일을 로드하여 클래스를 생성합니다. 이 단계에서는 추가 처리를 위해 문서를 초기화합니다.
```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    //후속 단계는 이 블록 내에 중첩됩니다.
}
```
## 3단계: 편집할 문서 열기
 문서를 편집하려면 중간 문서를 구하세요.`EditableDocument` 사례. 이 개체를 사용하면 문서 내용 및 관련 리소스를 조작할 수 있습니다.
```csharp
EditableDocument beforeEdit = editor.Edit();
```
## 4단계: 문서 콘텐츠 및 리소스 검색
편집 가능한 문서에서 주요 콘텐츠, 이미지, 글꼴, 스타일시트를 추출합니다. 이 정보는 수정을 수행하는 데 필수적입니다.
```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```
### 4.1단계: 문서를 단일 Base64 인코딩 문자열로 가져오기
또한 모든 리소스를 포함하는 단일 base64 인코딩 문자열로 전체 문서 콘텐츠를 얻을 수도 있습니다.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
### 4.2단계: 콘텐츠 편집
데모를 위해 특정 텍스트를 바꿔서 문서 내용을 수정해 보겠습니다.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## 5단계: 새 EditableDocument 인스턴스 생성
 내용을 편집한 후 새 항목을 만듭니다.`EditableDocument` 수정된 콘텐츠를 사용하는 인스턴스입니다.
```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
## 6단계: 편집된 문서 저장
이제 편집된 문서를 원하는 출력 형식으로 저장하세요. 이 예에서는 이를 RTF 파일로 저장하겠습니다.
### 6.1단계: 출력 경로 준비
출력 문서를 저장할 경로를 지정합니다.
```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```
### 6.2단계: 저장 옵션 준비
문서를 저장할 형식을 지정하여 저장 옵션을 정의합니다.
```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```
### 6.3단계: 경로에 저장
편집된 문서를 지정된 경로에 저장합니다.
```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```
### 6.4단계: 스트림에 저장
또는 출력 문서를 쓰기 가능한 스트림에 저장할 수 있습니다.
```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```
## 7단계: Editor 및 EditableDocument 인스턴스 삭제
 마지막으로, 폐기하여 청소하십시오.`EditableDocument` 인스턴스와`Editor` 리소스를 확보하는 개체입니다.
```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## 결론
.NET용 GroupDocs.Editor를 사용하면 문서 편집 기능을 응용 프로그램에 매우 쉽게 통합할 수 있습니다. 이 튜토리얼에 설명된 단계를 따르면 최소한의 노력으로 프로그래밍 방식으로 문서를 로드, 편집 및 저장할 수 있습니다. Word 문서, PDF 또는 기타 형식을 처리해야 하는 경우 GroupDocs.Editor는 문서 처리 요구 사항에 맞는 강력한 솔루션을 제공합니다.
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 PDF 파일을 편집할 수 있습니까?
예, .NET용 GroupDocs.Editor는 DOCX, HTML 등과 같은 다양한 형식과 함께 PDF 파일 편집을 지원합니다.
### .NET용 GroupDocs.Editor의 임시 라이센스를 얻으려면 어떻게 해야 합니까?
 임시면허를 취득할 수 있습니다.[GroupDocs 웹사이트](https://purchase.groupdocs.com/temporary-license/).
### .NET용 GroupDocs.Editor는 어떤 파일 형식을 지원합니까?
.NET용 GroupDocs.Editor는 DOCX, PDF, HTML, RTF 등 다양한 형식을 지원합니다.
### GroupDocs.Editor를 클라우드 저장소와 통합할 수 있습니까?
예, GroupDocs.Editor를 다양한 클라우드 저장소 솔루션과 통합하여 문서를 관리할 수 있습니다.
### .NET용 GroupDocs.Editor에 대한 설명서는 어디에서 찾을 수 있나요?
문서를 사용할 수 있습니다[여기](https://reference.groupdocs.com/editor/net/).