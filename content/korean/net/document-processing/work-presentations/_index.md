---
title: 프리젠테이션 작업
linktitle: 프리젠테이션 작업
second_title: GroupDocs.Editor .NET API
description: .NET용 GroupDocs.Editor를 사용하여 PowerPoint 프레젠테이션을 편집하는 방법을 알아보세요. 문서 편집 프로세스를 간소화하려면 이 단계별 가이드를 따르세요.
weight: 16
url: /ko/net/document-processing/work-presentations/
---
## 소개
오늘날의 디지털 시대에는 효과적인 문서 관리와 편집이 중요합니다. 개발자이든 프레젠테이션을 자주 다루는 사람이든 이러한 프로세스를 간소화하는 도구를 사용하여 작업하는 방법을 알면 시간과 노력을 절약할 수 있습니다. 그러한 도구 중 하나가 프레젠테이션을 포함한 문서를 프로그래밍 방식으로 편집할 수 있는 강력한 API인 .NET용 GroupDocs.Editor입니다. 이 튜토리얼에서는 환경 설정부터 프리젠테이션 파일 편집 및 저장까지 .NET용 GroupDocs.Editor를 사용하여 프리젠테이션 작업을 수행하는 단계를 안내합니다.
## 전제조건
튜토리얼을 시작하기 전에 다음 전제조건이 충족되었는지 확인하십시오.
1. Visual Studio: .NET 개발에 적합한 IDE입니다.
2.  .NET용 GroupDocs.Editor: 다음에서 다운로드할 수 있습니다.[웹사이트](https://releases.groupdocs.com/editor/net/).
3. .NET Framework: 호환 가능한 버전이 설치되어 있는지 확인하세요.
4. 샘플 PPTX 파일: 테스트용 샘플 PowerPoint 파일입니다.
5. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 도움이 됩니다.
## 네임스페이스 가져오기
시작하려면 C# 프로젝트에서 필요한 네임스페이스를 가져옵니다. 이러한 네임스페이스는 프레젠테이션 편집에 필요한 클래스 및 메서드에 대한 액세스를 제공합니다.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
## 1단계: 입력 파일 경로 가져오기
먼저 입력 프리젠테이션 파일의 경로를 지정해야 합니다. 이 파일은 편집 목적으로 사용됩니다.
```csharp
string inputFilePath = "YourSampleDocument.pptx";
```
## 2단계: 파일 스트림 생성
그런 다음 지정된 경로에서 파일 스트림을 만듭니다. 이 스트림은 프레젠테이션을 편집기에 로드하는 데 사용됩니다.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
```
## 3단계: 로드 옵션 생성
프레젠테이션과 관련된 로드 옵션을 만들어야 합니다. 해당하는 경우 이 단계에는 비밀번호로 보호된 파일 처리가 포함됩니다.

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions
{
    Password = "some_password_to_open_a_document"
};
```
## 4단계: 문서를 Editor에 로드
파일 스트림 및 로드 옵션이 준비되면 프레젠테이션을 편집기 인스턴스에 로드합니다.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
```
## 5단계: 편집 옵션 생성
편집하려는 특정 슬라이드, 숨겨진 슬라이드 표시 여부 등 편집 옵션을 설정합니다.
편집하려는 슬라이드의 색인을 지정합니다. 인덱스는 0부터 시작하므로 첫 번째 슬라이드는 인덱스 0입니다.
```csharp
PresentationEditOptions editOptions = new PresentationEditOptions
{
    SlideNumber = 0, // 첫 번째 슬라이드
    ShowHiddenSlides = true
};
```
## 6단계: 편집 가능한 문서 만들기
편집기와 지정된 편집 옵션을 사용하여 편집 가능한 중간 문서를 만듭니다.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
```
## 7단계: 콘텐츠 및 리소스 추출
텍스트 콘텐츠를 HTML 마크업으로 추출하고 원본 문서에서 모든 리소스를 검색합니다.
```csharp
string originalContent = beforeEdit.GetContent();
```
## 7.1단계: 리소스 추출
이미지, 스타일 등 모든 리소스를 검색합니다.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 8단계: 콘텐츠 수정
필요에 따라 내용을 수정합니다. 예를 들어 HTML 콘텐츠의 특정 텍스트를 바꿉니다.
```csharp
string editedContent = originalContent.Replace("New text", "edited text");
```
## 9단계: 편집 가능한 새 문서 만들기
 새 인스턴스 만들기`EditableDocument` 편집된 콘텐츠와 동일한 리소스를 사용합니다.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
```
## 10단계: 저장 옵션 생성
형식, 암호화 등 편집된 문서를 저장하기 위한 옵션을 설정합니다.
```csharp
PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm)
{
    Password = "password"
};
```
## 11단계: 편집된 문서 저장
마지막으로 편집된 프레젠테이션을 원하는 위치에 저장합니다.

```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + saveOptions.OutputFormat.Extension;
string outputPath = Path.Combine("YourOutputDirectory", outputFilename);
```
## 11.1단계: 저장할 파일 스트림 생성
편집된 프레젠테이션을 저장하려면 파일 스트림을 만드세요.
```csharp
using (FileStream outputStream = File.Create(outputPath))
{
```
## 11.2단계: 문서 저장
편집기 인스턴스를 사용하여 문서를 저장합니다.
```csharp
editor.Save(afterEdit, outputStream, saveOptions);
```
```csharp
}
}
}
System.Console.WriteLine("Working with presentations routine has successfully finished");
```
## 결론
.NET용 GroupDocs.Editor를 사용하면 프레젠테이션 작업이 간단하고 효율적입니다. 이 단계별 가이드를 따르면 프로그래밍 방식으로 PowerPoint 파일을 쉽게 편집하고 저장할 수 있습니다. 문서 작업 흐름을 자동화하든 프레젠테이션 편집을 응용 프로그램에 통합하든 GroupDocs.Editor는 작업을 완료하는 데 필요한 도구를 제공합니다.
## FAQ
### .NET용 GroupDocs.Editor는 암호로 보호된 프레젠테이션을 처리할 수 있습니까?
예, 그럴 수 있습니다. 로드 옵션에서 비밀번호를 지정하여 비밀번호로 보호된 프레젠테이션을 열고 편집할 수 있습니다.
### .NET용 GroupDocs.Editor는 프리젠테이션 저장을 위해 어떤 형식을 지원합니까?
GroupDocs.Editor는 PPTX, PPTM 등을 포함한 다양한 형식을 지원합니다. 저장 옵션에서 원하는 형식을 지정할 수 있습니다.
### 여러 슬라이드를 한 번에 편집할 수 있나요?
현재 GroupDocs.Editor를 사용하면 한 번에 하나의 슬라이드를 편집할 수 있습니다. 필요한 경우 슬라이드를 반복하면서 편집 내용을 개별적으로 적용할 수 있습니다.
### 웹 응용 프로그램에서 .NET용 GroupDocs.Editor를 사용할 수 있습니까?
예, .NET용 GroupDocs.Editor는 웹 응용 프로그램에 통합되어 문서 편집 기능을 제공할 수 있습니다.
### 더 자세한 문서와 지원은 어디서 찾을 수 있나요?
 자세한 문서를 찾을 수 있습니다[여기](https://tutorials.groupdocs.com/editor/net/) . 지원을 받으려면 다음을 방문하세요.[지원 포럼](https://forum.groupdocs.com/c/editor/20).