---
title: DSV(구분된 구분 값) 작업
linktitle: DSV(구분된 구분 값) 작업
second_title: GroupDocs.Editor .NET API
description: 이 단계별 가이드를 통해 .NET용 GroupDocs.Editor를 사용하여 CSV 및 TSV 파일을 편집하는 방법을 알아보세요. .NET 프로젝트를 손쉽게 개선하세요.
weight: 12
url: /ko/net/document-processing/work-dsv/
---

# DSV(구분된 구분 값) 작업

## 소개
CSV 또는 TSV 파일과 같은 DSV(구분된 구분 값)를 사용하여 작업하는 개발자라면 이러한 파일을 프로그래밍 방식으로 편집하는 것이 어려운 작업이 될 수 있다는 것을 알고 있습니다. 그러나 .NET용 GroupDocs.Editor를 사용하면 이 작업이 훨씬 더 간단하고 효율적이 됩니다. 이 자습서에서는 .NET용 GroupDocs.Editor를 사용하여 DSV 파일을 읽고 편집하고 저장하는 방법을 안내합니다. 프로세스를 따라하기 쉬운 단계로 나누어 프로젝트에서 쉽게 구현할 수 있도록 하겠습니다.
## 전제조건
튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
- Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요.
-  .NET용 GroupDocs.Editor: .NET용 GroupDocs.Editor 라이브러리를 다운로드하고 참조해야 합니다. 당신은 그것을 다운로드 할 수 있습니다[여기](https://releases.groupdocs.com/editor/net/).
- C#의 기본 이해: 이 자습서에서는 사용자가 C# 및 .NET 개발에 대한 기본 지식을 가지고 있다고 가정합니다.
## 네임스페이스 가져오기
먼저 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 .NET용 GroupDocs.Editor를 사용하는 데 필요한 클래스와 메서드를 제공합니다.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## 1단계: 입력 DSV 파일의 경로 가져오기
먼저 입력 DSV 파일의 경로를 지정해야 합니다. 이 예에서는 CSV 파일이라고 가정합니다.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2단계: 편집기 인스턴스 생성
 인스턴스를 생성합니다.`Editor` 수업. 이 인스턴스는 DSV 파일을 로드하고 조작하는 데 사용됩니다.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3단계: DSV 편집 옵션 만들기
 다음으로 인스턴스를 생성합니다.`DelimitedTextEditOptions` DSV 파일의 구분 기호를 지정합니다. 여기서는 쉼표를 구분 기호로 사용합니다.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## 4단계: EditableDocument 인스턴스 생성
 만들기`EditableDocument` 인스턴스를 사용하여`Editor.Edit` 방법. 그러면 편집할 문서가 준비됩니다.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## 5단계: 문서 내용 편집
원본 텍스트 콘텐츠를 검색하고 필요한 수정을 가합니다. 데모를 위해 일부 텍스트를 교체해 보겠습니다.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6단계: 업데이트된 콘텐츠로 편집 가능한 문서 만들기
 새로 만들기`EditableDocument` 업데이트된 콘텐츠로
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 7단계: CSV 저장 옵션 생성
구분 기호 및 인코딩을 포함하여 CSV 형식에 대한 저장 옵션을 지정합니다.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 8단계: TSV 저장 옵션 생성
마찬가지로 TSV 형식에 대한 저장 옵션을 지정합니다.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 9단계: 스프레드시트 저장 옵션 만들기
문서를 스프레드시트로 저장해야 하는 경우 해당 저장 옵션을 만듭니다.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## 10단계: 저장 경로 준비
편집된 파일이 저장될 경로를 정의합니다.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## 11단계: 편집된 문서 저장
편집된 문서를 지정된 경로에 다른 형식으로 저장합니다.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## 12단계: EditableDocument 인스턴스 삭제
 마지막으로, 반드시 폐기하십시오.`EditableDocument` 인스턴스를 사용하여 리소스를 확보합니다.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## 결론
.NET용 GroupDocs.Editor를 사용하여 DSV 파일을 편집하는 것은 편집기 인스턴스 만들기, 편집 옵션 설정, 콘텐츠 수정 및 변경 사항 저장을 포함하는 간단한 프로세스입니다. 이 단계별 가이드는 이 기능을 .NET 애플리케이션에 쉽게 통합하는 데 도움이 됩니다. CSV, TSV 또는 기타 DSV 형식으로 작업하는 경우 .NET용 GroupDocs.Editor는 강력하고 유연한 솔루션을 제공합니다.
## FAQ
### .NET용 GroupDocs.Editor를 사용하여 대용량 CSV 파일을 편집할 수 있습니까?
예, .NET용 GroupDocs.Editor는 대용량 CSV 파일을 효율적으로 처리할 수 있습니다.
### .NET용 GroupDocs.Editor는 CSV 및 TSV 외에 다른 DSV 형식을 지원합니까?
예, 적절한 구분 기호를 지정하는 한 다양한 DSV 형식을 지원합니다.
### DSV 파일을 저장할 때 인코딩을 사용자 정의할 수 있습니까?
물론 저장 옵션에서 원하는 인코딩을 지정할 수 있습니다.
### .NET용 GroupDocs.Editor를 사용하여 CSV 파일을 Excel 스프레드시트로 변환할 수 있나요?
예, 적절한 저장 옵션을 사용하여 CSV 파일을 Excel 스프레드시트로 저장할 수 있습니다.
### .NET용 GroupDocs.Editor에 대한 추가 문서는 어디서 찾을 수 있나요?
 자세한 문서를 찾을 수 있습니다[여기](https://tutorials.groupdocs.com/editor/net/)