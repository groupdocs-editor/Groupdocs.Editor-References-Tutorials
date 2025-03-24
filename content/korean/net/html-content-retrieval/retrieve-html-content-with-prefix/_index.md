---
title: 접두사가 포함된 HTML 콘텐츠 검색
linktitle: 접두사가 포함된 HTML 콘텐츠 검색
second_title: GroupDocs.Editor .NET API
description: 이미지 및 스타일시트에 대한 사용자 정의 접두어가 있는 .NET용 GroupDocs.Editor를 사용하여 문서에서 HTML 콘텐츠를 검색하는 방법을 알아보세요. 단계별 가이드가 포함되어 있습니다.
weight: 11
url: /ko/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## 소개
.NET용 GroupDocs.Editor를 사용하여 문서에서 HTML 콘텐츠를 검색하는 방법에 대한 단계별 자습서에 오신 것을 환영합니다. 숙련된 개발자이든 이제 막 시작하는 개발자이든 이 가이드는 따라하기 쉬운 방식으로 프로세스를 안내합니다. 환경 설정부터 코드의 성공적인 실행까지 알아야 할 모든 것을 다룹니다. 뛰어들어보자!
## 전제조건
시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
1.  .NET용 GroupDocs.Editor: 다음에서 최신 버전을 다운로드하세요.[다운로드 페이지](https://releases.groupdocs.com/editor/net/).
2. 개발 환경: Visual Studio 또는 기타 선호하는 .NET 개발 환경.
3. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 예제를 따라가는 데 도움이 됩니다.
4. 편집할 문서: Word 문서와 같이 테스트할 샘플 문서를 준비합니다.
5. .NET Framework: 컴퓨터에 .NET Framework가 설치되어 있는지 확인하세요.
이제 모든 준비가 끝났으니 시작해 보세요!
## 네임스페이스 가져오기
먼저 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 .NET용 GroupDocs.Editor를 사용하는 데 필요한 클래스와 메서드를 제공합니다.
```csharp
using System;
using GroupDocs.Editor.Options;
```
네임스페이스를 가져온 후 편집기 설정으로 넘어갈 수 있습니다.
## 1단계: 편집기 초기화
 시작하려면`Editor`문서로 수업하세요. 이 단계에는 편집하려는 문서를 지정하고 필요한 로드 옵션을 제공하는 작업이 포함됩니다.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // 여기에 추가 단계가 추가됩니다.
}
```
 이 예에서는 Word 문서를 로드하고 있습니다. 교체할 수 있습니다`"Your Sample Document"` 문서의 경로와 함께.
## 2단계: 문서 편집
 다음으로 편집을 위해 문서를 열어야 합니다. 이 작업은 다음을 사용하여 수행됩니다.`Edit` 의 방법`Editor` 요구하는 수업`WordProcessingEditOptions` 논쟁으로.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // 여기에 추가 단계가 추가됩니다.
}
```
 그만큼`EditableDocument` 인스턴스는 편집 가능한 형식으로 문서를 나타냅니다. 이제 HTML 콘텐츠를 검색할 준비가 되었습니다.
## 3단계: 사용자 정의 접두사 정의
이미지와 CSS에 대한 사용자 정의 접두사를 추가하려면 접두사를 문자열로 정의해야 합니다. 이 단계에서는 HTML 콘텐츠에 외부 리소스에 대해 지정된 접두사가 있는지 확인합니다.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
URL을 원하는 접두어로 바꿀 수 있습니다. 이러한 접두어는 다음 단계에서 HTML 출력을 사용자 정의하는 데 사용됩니다.
## 4단계: HTML 콘텐츠 검색
이제 접두어가 설정되었으므로 문서에서 HTML 콘텐츠를 검색할 수 있습니다. 그만큼`GetContent` 의 방법`EditableDocument` 클래스를 사용하면 이미지와 CSS 접두사를 지정할 수 있습니다.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
이 코드 조각은 사용자 정의 접두사가 포함된 HTML 콘텐츠를 가져와서 콘솔에 인쇄합니다. 필요에 따라 이 HTML 콘텐츠를 추가로 처리하거나 저장할 수 있습니다.
## 결론
그리고 거기에 있습니다! 다음 단계를 수행하면 이미지 및 스타일시트에 대한 사용자 정의 접두사가 포함된 .NET용 GroupDocs.Editor를 사용하여 문서에서 HTML 콘텐츠를 쉽게 검색할 수 있습니다. 이 강력한 도구는 문서 조작을 단순화하여 문서 편집을 .NET 애플리케이션에 원활하게 통합하는 데 집중할 수 있도록 해줍니다.
 자세한 내용은 다음을 확인하세요.[.NET 문서용 GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/) . 질문이 있거나 추가 지원이 필요한 경우 언제든지 문의해 주세요.[지원 포럼](https://forum.groupdocs.com/c/editor/20).
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 어떤 유형의 문서를 편집할 수 있나요?
GroupDocs.Editor는 Word, Excel, PowerPoint, PDF 등을 포함한 다양한 문서 형식을 지원합니다.
### .NET용 GroupDocs.Editor의 무료 평가판을 받으려면 어떻게 해야 합니까?
 다음에서 무료 평가판을 받을 수 있습니다.[GroupDocs 웹사이트](https://releases.groupdocs.com/).
### HTML 콘텐츠를 추가로 맞춤설정할 수 있나요?
예, 검색된 HTML 콘텐츠를 렌더링하거나 저장하기 전에 필요에 따라 수정할 수 있습니다.
### 다른 .NET 언어와 함께 .NET용 GroupDocs.Editor를 사용할 수 있습니까?
예, VB.NET 또는 F#과 같은 .NET 호환 언어와 함께 사용할 수 있습니다.
### .NET용 GroupDocs.Editor의 임시 라이센스를 얻으려면 어떻게 해야 합니까?
 임시면허를 발급받으실 수 있습니다.[구매 페이지](https://purchase.groupdocs.com/temporary-license/).