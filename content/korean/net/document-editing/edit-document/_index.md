---
title: 문서 편집
linktitle: 문서 편집
second_title: GroupDocs.Editor .NET API
description: .NET용 GroupDocs.Editor를 사용하여 손쉽게 문서를 편집하는 방법을 알아보세요. 워드 프로세싱 및 스프레드시트 파일에 대한 단계별 가이드입니다.
weight: 11
url: /ko/net/document-editing/edit-document/
type: docs
---
# 문서 편집

## 소개
.NET 애플리케이션 내에서 문서 편집의 복잡성으로 인해 어려움을 겪은 적이 있습니까? 두려워하지 마세요! .NET용 GroupDocs.Editor를 사용하면 이 작업을 단순화할 수 있는 강력한 동맹자가 됩니다. 이 종합 가이드는 이 강력한 도구를 활용하여 문서를 쉽게 편집하는 방법을 안내합니다. 워드 프로세싱 문서를 다루든 스프레드시트를 다루든 이 튜토리얼이 끝나면 전문가처럼 GroupDocs.Editor를 탐색하게 될 것입니다.
## 전제조건
튜토리얼을 시작하기 전에 다음 사항을 확인하세요.
- Visual Studio: 설치되었으며 사용할 준비가 되었습니다.
- .NET Framework: 시스템에 설치된 호환 버전입니다.
-  .NET용 GroupDocs.Editor: 다음을 수행할 수 있습니다.[최신 버전을 다운로드하세요](https://releases.groupdocs.com/editor/net/) 그리고[임시면허](https://purchase.groupdocs.com/temporary-license/) 필요한 경우.
- C#에 대한 기본 지식: 이 가이드에서는 사용자가 C# 및 .NET 개발에 대한 기본 지식을 가지고 있다고 가정합니다.
## 네임스페이스 가져오기
시작하려면 필요한 네임스페이스를 프로젝트로 가져와야 합니다. C# 파일 상단에 다음 줄을 추가합니다.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
이제 모든 설정이 완료되었으므로 문서 편집 프로세스를 관리 가능한 단계로 나누어 보겠습니다.
## 1단계: 워드 프로세싱 문서 로드
먼저 워드 프로세싱 문서를 로드해 보겠습니다. 여기에서 Editor 인스턴스가 문서 위치를 가리키고 필요한 경우 로드 옵션을 지정할 수 있습니다.
### 1.1 기본 옵션으로 편집기 초기화
```csharp
string inputFilePath = "Your Sample Document"; // 문서 경로
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
이 코드 조각은 워드 프로세싱 문서의 기본 로드 옵션을 사용하여 Editor 인스턴스를 초기화합니다.
## 2단계: 문서 편집
이제 로드된 문서 편집을 진행할 수 있습니다. GroupDocs.Editor를 사용하면 필요에 맞게 편집 옵션을 사용자 정의할 수 있습니다.
### 2.1 기본 옵션으로 편집
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
기본 옵션을 사용하여 문서를 편집하는 것은 간단하며 최소한의 구성이 필요합니다.
### 2.2 사용자 정의 옵션으로 편집
사용자 정의 편집 옵션을 지정하여 더욱 고급 구성을 살펴보겠습니다.
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
이 코드 조각에서는 페이지 매김을 비활성화하고, 언어 정보를 활성화하고, 포함된 모든 글꼴을 추출하도록 글꼴 추출을 설정했습니다.
### 2.3 또 다른 구성 예
다양한 옵션 세트를 사용하여 문서를 편집할 수도 있습니다.
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
여기서는 페이지 매김을 활성화하고 글꼴 추출을 설정하여 모든 글꼴을 추출했습니다.
## 3단계: 스프레드시트 로드 및 편집
GroupDocs.Editor를 사용하면 스프레드시트 편집도 마찬가지로 간단합니다.
### 3.1 스프레드시트 로드
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
이는 스프레드시트 문서에 대한 Editor 인스턴스를 초기화합니다.
### 3.2 첫 번째 탭 편집
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; // 인덱스는 0부터 시작하므로 이것이 첫 번째 탭입니다.
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
지정된 옵션을 사용하여 스프레드시트의 첫 번째 탭을 편집할 수 있습니다.
### 3.3 두 번째 탭 편집
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; // 인덱스는 0부터 시작하므로 두 번째 탭입니다.
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
마찬가지로 이 코드 조각은 스프레드시트의 두 번째 탭을 편집합니다.
## 4단계: 콘텐츠 추출
문서를 편집한 후에는 해당 내용을 추출해야 할 수도 있습니다. GroupDocs.Editor는 이를 위한 다양한 방법을 제공합니다.
### 4.1 HTML 콘텐츠 가져오기
```csharp
string bodyContent = firstTab.GetBodyContent(); // HTML->BODY 요소 내부의 HTML 마크업
string allContent = firstTab.GetContent(); // HTML->HEAD 헤더 및 해당 내용을 포함한 모든 문서의 전체 HTML 마크업
```
이 코드는 편집된 문서의 HTML 콘텐츠를 추출합니다.
### 4.2 자원 추출
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
여기에서는 문서에서 이미지와 기타 모든 HTML 리소스를 추출할 수 있습니다.
## 5단계: 정리
리소스를 확보하려면 모든 인스턴스를 폐기하는 것을 잊지 마세요.
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
적절하게 폐기하면 애플리케이션에 메모리 누수나 성능 문제가 발생하지 않습니다.
## 결론
 축하해요! 이제 .NET용 GroupDocs.Editor를 사용하여 워드 프로세싱 문서 및 스프레드시트의 콘텐츠를 로드, 편집 및 추출하는 방법을 확실하게 이해하게 되었습니다. 이 강력한 도구는 문서 편집 작업을 단순화하고 .NET 애플리케이션과 원활하게 통합됩니다. 자세한 내용은 다음을 참조하세요.[선적 서류 비치](https://tutorials.groupdocs.com/editor/net/), [최신 버전을 다운로드하세요](https://releases.groupdocs.com/editor/net/) , 또는[임시면허](https://purchase.groupdocs.com/temporary-license/).
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 PDF 문서를 편집할 수 있습니까?
현재 .NET용 GroupDocs.Editor는 주로 워드 프로세싱, 스프레드시트 및 프레젠테이션 형식을 지원합니다.
### 대용량 문서를 효율적으로 처리하려면 어떻게 해야 합니까?
편집 옵션을 활용하여 문서에서 필요한 부분만 로드 및 처리하고, 인스턴스를 적절하게 폐기하여 메모리를 관리하세요.
### 편집할 수 있는 문서 크기에 제한이 있나요?
엄격한 크기 제한은 없지만 성능은 시스템 기능에 따라 달라집니다.
### HTML 출력을 추가로 사용자 정의할 수 있나요?
예, GroupDocs.Editor에서는 다양한 옵션과 설정을 통해 HTML 출력을 광범위하게 사용자 정의할 수 있습니다.
### 문제가 발생하면 어디서 지원을 받을 수 있나요?
 당신은 방문 할 수 있습니다[GroupDocs.Editor 지원 포럼](https://forum.groupdocs.com/c/editor/20) 도움과 지원을 위해.