---
title: 일반 텍스트 문서 작업
linktitle: 일반 텍스트 문서 작업
second_title: GroupDocs.Editor .NET API
description: 단계별 가이드를 통해 .NET용 GroupDocs.Editor를 사용하여 일반 텍스트 문서를 편집하는 방법을 알아보세요. .NET 문서 편집 프로세스를 단순화하세요.
type: docs
weight: 15
url: /ko/net/document-processing/work-plain-text-documents/
---
## 소개
.NET에서 문서 편집 프로세스를 간소화하고 싶으십니까? .NET용 GroupDocs.Editor만 있으면 됩니다! 이 강력한 API를 사용하면 다양한 문서 형식을 쉽게 편집할 수 있습니다. 이 자습서에서는 .NET용 GroupDocs.Editor를 사용하여 일반 텍스트 문서로 작업하는 과정을 안내합니다. 결국에는 전문가처럼 텍스트 문서 편집을 처리할 수 있는 능력을 갖추게 됩니다. 다이빙할 준비가 되셨나요? 시작하자!
## 전제조건
시작하기 전에 준비해야 할 몇 가지 사항이 있습니다.
- .NET 개발 환경: 작동하는 .NET 개발 환경이 설정되어 있는지 확인하세요. Visual Studio는 널리 사용되는 선택입니다.
-  .NET용 GroupDocs.Editor: 다운로드 및 설치[.NET용 GroupDocs.Editor](https://releases.groupdocs.com/editor/net/).
- 기본 C# 지식: C# 프로그래밍 언어에 익숙하면 예제를 따라가는 데 도움이 됩니다.
- 텍스트 편집기: 모든 텍스트 편집기가 가능하지만 기능과 사용 편의성을 위해 Visual Studio Code를 권장합니다.
## 네임스페이스 가져오기
.NET용 GroupDocs.Editor 사용을 시작하려면 필요한 네임스페이스를 프로젝트로 가져와야 합니다. 이렇게 하면 필요한 모든 클래스와 메서드를 사용할 수 있습니다.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
프로세스를 관리 가능한 단계로 나누어 보겠습니다. .NET용 GroupDocs.Editor를 사용하여 일반 텍스트 문서를 편집하는 각 단계를 안내해 드립니다.
## 1단계: 입력 TXT 파일의 경로 가져오기
먼저 입력 TXT 파일의 경로를 지정해야 합니다. 이는 로컬 파일의 경로일 수도 있고 파일 콘텐츠가 포함된 스트림일 수도 있습니다.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## 2단계: 편집기 인스턴스 생성
 다음으로,`Editor` 수업. 이 클래스는 문서 로드 및 편집을 담당합니다. 이 단계에서는 로드 옵션이 필요하지 않습니다.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3단계: TXT 편집 옵션 생성
이제 TXT 편집 옵션을 만듭니다. 이러한 옵션을 사용하면 편집 중에 텍스트 내용을 처리하는 방법을 지정할 수 있습니다.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## 4단계: EditableDocument 인스턴스 생성
 편집 옵션이 설정된 상태에서`EditableDocument` 사례. 편집 가능한 형식으로 문서를 나타냅니다.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 5단계: 문서 내용 편집
원본 텍스트 콘텐츠를 검색하고 원하는 대로 편집하세요. 이 예에서는 "text"라는 단어를 "EDITED text"로 바꿉니다.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6단계: 업데이트된 콘텐츠로 편집 가능한 문서 만들기
 필요한 수정을 한 후 새 항목을 만듭니다.`EditableDocument` 업데이트된 콘텐츠와 원본 리소스를 사용하세요.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 7단계: 워드프로세싱 저장 옵션 만들기
워드프로세싱 형식에 대한 저장 옵션을 준비합니다. 이 예에서는 DOCM 형식을 사용하고 로케일을 지정합니다.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## 8단계: TXT 저장 옵션 생성
마찬가지로 TXT 형식에 대한 저장 옵션을 만듭니다. 인코딩이 UTF-8로 설정되어 있는지 확인하고 테이블 레이아웃을 유지하세요.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## 9단계: 출력 경로 준비
결과 DOCX 및 TXT 파일을 저장할 경로를 준비합니다. 입력 파일 경로를 사용하여 출력 디렉터리와 파일 이름을 결정합니다.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 10단계: 편집된 문서 저장
마지막으로 지정된 저장 옵션을 사용하여 편집된 문서를 DOCX 및 TXT 형식으로 저장합니다.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## 결론
 축하해요! .NET용 GroupDocs.Editor를 사용하여 일반 텍스트 문서를 성공적으로 편집했습니다. 이 강력한 도구는 문서 편집을 단순화하여 .NET 애플리케이션에 쉽게 통합할 수 있도록 해줍니다. 간단한 텍스트 파일을 처리하든 복잡한 문서 형식을 처리하든 GroupDocs.Editor가 도와드립니다. 다음을 방문하여 더 많은 기능을 살펴보세요.[GroupDocs.Editor 문서](https://reference.groupdocs.com/editor/net/).
## FAQ
### .NET용 GroupDocs.Editor는 어떤 파일 형식을 지원합니까?
 .NET용 GroupDocs.Editor는 DOCX, TXT, HTML 등을 포함한 광범위한 파일 형식을 지원합니다. 을 체크 해봐[선적 서류 비치](https://reference.groupdocs.com/editor/net/) 전체 목록을 보려면.
### .NET용 GroupDocs.Editor의 무료 평가판을 받으려면 어떻게 해야 합니까?
 다음에서 .NET용 GroupDocs.Editor 무료 평가판을 다운로드할 수 있습니다.[릴리스 페이지](https://releases.groupdocs.com/).
### .NET용 GroupDocs.Editor의 임시 라이센스를 구입할 수 있습니까?
네, 임시 면허는 다음 기관에서 받으실 수 있습니다.[GroupDocs 구매 페이지](https://purchase.groupdocs.com/temporary-license/).
### .NET용 GroupDocs.Editor에 대한 지원은 어디서 받을 수 있나요?
 지원은 다음을 통해 제공됩니다.[GroupDocs.Editor 지원 포럼](https://forum.groupdocs.com/c/editor/20).
### .NET용 GroupDocs.Editor에 대한 자세한 설명서가 있습니까?
 예, 자세한 문서는 다음에서 확인할 수 있습니다.[GroupDocs.Editor 문서 페이지](https://reference.groupdocs.com/editor/net/).