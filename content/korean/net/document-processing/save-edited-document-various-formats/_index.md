---
title: 편집된 문서를 다양한 형식으로 저장
linktitle: 편집된 문서를 다양한 형식으로 저장
second_title: GroupDocs.Editor .NET API
description: 이 포괄적인 단계별 가이드에서 .NET용 GroupDocs.Editor를 사용하여 편집된 문서를 다양한 형식으로 저장하는 방법을 알아보세요.
weight: 11
url: /ko/net/document-processing/save-edited-document-various-formats/
type: docs
---
# 편집된 문서를 다양한 형식으로 저장

## 소개
.NET용 GroupDocs.Editor를 사용하여 편집된 문서를 다양한 형식으로 저장하고 싶으십니까? 당신은 올바른 장소에 왔습니다! 이 포괄적인 가이드는 환경 설정부터 편집된 문서를 다양한 형식으로 저장하는 것까지 전체 프로세스를 안내합니다. 문서를 편집하고 쉽게 저장해 보세요!
## 전제조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1.  .NET용 GroupDocs.Editor - 다음에서 최신 버전을 다운로드하세요.[여기](https://releases.groupdocs.com/editor/net/).
2. 개발 환경 - Visual Studio 또는 기타 .NET 호환 IDE.
3. .NET Framework - .NET Framework 4.6.1 이상이 설치되어 있는지 확인하세요.
4. 샘플 문서 - 작업할 샘플 워드프로세싱 문서입니다.
5. 기본 C# 지식 - C# 프로그래밍에 대한 지식이 필요합니다.
## 네임스페이스 가져오기
시작하려면 필요한 네임스페이스를 C# 프로젝트로 가져와야 합니다. 이는 GroupDocs.Editor 기능에 액세스하는 데 중요합니다.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
프로세스를 관리 가능한 단계로 나누어 보겠습니다. 각 부분을 잘 이해할 수 있도록 주의 깊게 따라가세요.
## 1단계: 입력 파일의 경로 가져오기
먼저 입력 워드프로세싱 파일의 경로를 지정해야 합니다. 이 파일이 로드되고 편집됩니다.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2단계: 문서에 대한 로드 옵션 만들기
다음으로 워드프로세싱 문서와 관련된 로드 옵션을 만듭니다. 이러한 옵션은 문서 로드 방법을 사용자 정의하는 데 도움이 됩니다.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## 3단계: 옵션이 포함된 문서 로드
 이제 문서를`Editor` 지정된 로드 옵션을 사용하는 인스턴스입니다.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## 4단계: 편집 옵션 생성
문서의 편집 옵션을 준비합니다. 이러한 옵션은 편집을 위해 문서를 여는 방법을 결정합니다.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## 5단계: 편집을 위해 문서 열기
 편집할 문서를 생성하여 편집할 문서를 엽니다.`EditableDocument`사례. 이 인스턴스를 사용하면 문서를 변경할 수 있습니다.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## 6단계: 문서 내용 편집
이제 문서의 내용을 편집할 차례입니다. 먼저 문서를 단일 base64 인코딩 문자열로 가져옵니다.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
예를 들어 문서의 자막을 수정해 보겠습니다.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## 7단계: 편집된 콘텐츠에서 편집 가능한 새 문서 만들기
 새로 만들기`EditableDocument` 편집된 콘텐츠 및 리소스의 인스턴스입니다.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## 8단계: 문서를 다양한 형식으로 저장
마지막으로 지원 가능한 모든 워드프로세싱 형식을 반복하고 편집된 문서를 각 형식으로 저장합니다.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // 저장 옵션 준비
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // 저장 경로 준비
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // 문서 저장
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## 완료 메시지
마무리하려면 프로세스가 성공적으로 완료되었음을 나타내는 메시지를 인쇄할 수 있습니다.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## 결론
축하해요! .NET용 GroupDocs.Editor를 사용하여 편집된 문서를 다양한 형식으로 저장하는 방법을 성공적으로 배웠습니다. 이 강력한 도구를 사용하면 단 몇 줄의 코드만으로 다양한 형식의 문서를 쉽게 조작하고 저장할 수 있습니다. 주요 단계에는 문서 로드, 콘텐츠 편집 및 원하는 형식으로 저장이 포함됩니다.
## FAQ
### .NET용 GroupDocs.Editor란 무엇입니까?
.NET용 GroupDocs.Editor는 .NET 응용 프로그램을 사용하여 다양한 형식의 문서를 편집할 수 있는 강력한 API입니다.
### GroupDocs.Editor를 무료로 사용할 수 있나요?
 예, 무료 평가판을 통해 사용할 수 있습니다. 다운로드 해[여기](https://releases.groupdocs.com/).
### GroupDocs.Editor는 어떤 형식을 지원합니까?
GroupDocs.Editor는 DOCX, PDF, HTML 등을 포함한 광범위한 형식을 지원합니다.
### GroupDocs.Editor의 임시 라이센스를 얻으려면 어떻게 해야 합니까?
 임시면허를 취득할 수 있습니다.[여기](https://purchase.groupdocs.com/temporary-license/).
### 추가 문서와 지원은 어디서 찾을 수 있나요?
 자세한 문서가 제공됩니다.[여기](https://tutorials.groupdocs.com/editor/net/) , 지원을 받을 수 있습니다.[여기](https://forum.groupdocs.com/c/editor/20).