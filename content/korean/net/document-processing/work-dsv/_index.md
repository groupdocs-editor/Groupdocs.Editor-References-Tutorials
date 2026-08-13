---
date: 2026-06-06
description: CSV 및 TSV 파일을 사용하여 GroupDocs.Editor for .NET으로 **편집 가능한 문서** 객체를 만드는
  방법을 배웁니다. 이 가이드는 또한 Visual Studio에서 **C#로 구분된 텍스트를 읽고** **CSV .NET을 편집**하는 효율적인
  방법을 보여줍니다.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: 구분된 구분 값(DSV) 작업 – 편집 가능한 문서 만들기
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 구분된 구분 값(DSV) 작업 – 편집 가능한 문서 만들기
type: docs
url: /ko/net/document-processing/work-dsv/
weight: 12
---

# 구분된 구분 값(DSV) 작업 – 편집 가능한 문서 만들기

If you’re a .NET developer who needs to **create editable document** objects from delimited separated values (DSV) such as CSV or TSV, you’ve come to the right place. In the first 100 words we’ll explain why GroupDocs.Editor for .NET is the most reliable way to **read delimited text C#**, edit it, and then save it back without losing formatting. You’ll walk away with a complete, copy‑and‑paste‑ready workflow that fits naturally into any Visual Studio solution.

## 빠른 답변
- **.NET에서 CSV 편집을 가장 잘 처리하는 라이브러리는 무엇인가요?** GroupDocs.Editor for .NET.
- **Visual Studio에서 대용량 CSV 파일을 편집할 수 있나요?** Yes – the API streams data and avoids loading the whole file into memory.
- **프로덕션 사용을 위해 라이선스가 필요합니까?** A commercial license is required; a free trial is available.
- **편집 후 어떤 형식으로 출력할 수 있나요?** CSV, TSV, and Excel‑compatible spreadsheet formats.
- **API가 .NET 6+와 호환되나요?** Absolutely – it supports .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6.

## GroupDocs.Editor 컨텍스트에서 “create editable document”란 무엇인가요?
**Create editable document**는 메모리 내에서 소스 파일(CSV, TSV 등)의 변경 가능한 버전을 나타내는 `EditableDocument` 인스턴스를 생성하는 것을 의미합니다. 이 객체를 사용하면 동일한 API로 내용을 읽고, 수정하고, 다시 저장할 수 있습니다. 문서 텍스트를 가져오고, 변경을 적용하며, 다양한 형식으로 다시 저장하는 메서드를 제공하여 열 정렬 및 인용 부호가 보존되도록 합니다.

## DSV 처리에 GroupDocs.Editor를 사용하는 이유
GroupDocs.Editor는 CSV, TSV 및 Excel 호환 스프레드시트를 포함한 **50개 이상의 입력 및 출력 형식**을 처리하면서 500 MB까지의 파일에 대해 메모리 사용량을 10 MB 이하로 유지합니다. 또한 열 정렬, 인용 규칙 및 사용자 지정 인코딩을 자동으로 보존하므로 수동 파싱 로직이 필요하지 않습니다.

## 사전 요구 사항
- **Visual Studio** (최근 버전) – IDE 내부에서 직접 개발 및 디버깅합니다.
- **GroupDocs.Editor for .NET** – 최신 패키지를 **[here](https://releases.groupdocs.com/editor/net/)**에서 다운로드하십시오.
- **Basic C# knowledge** – 이 튜토리얼은 콘솔 또는 ASP.NET 프로젝트를 만들고 NuGet 패키지를 추가할 수 있다고 가정합니다.

## 네임스페이스 가져오기
`Editor`, `EditableDocument`, 및 옵션 클래스는 `GroupDocs.Editor` 네임스페이스에 있습니다.

`DelimitedTextEditOptions` 클래스는 구분자(쉼표, 탭 등) 및 기타 파싱 규칙을 정의하기 위한 진입점입니다.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## CSV 파일에서 editable document를 만드는 방법?
`Editor`를 사용해 소스 CSV를 로드하고 `Edit` 메서드를 호출하면서 쉼표 구분자를 지정한 `DelimitedTextEditOptions` 인스턴스를 전달합니다. 이 메서드는 메모리 내에서 조작할 수 있는 `EditableDocument`를 반환합니다. 이 두 단계 패턴—load → edit—은 **read delimited text C#** 시나리오를 포괄하며 원본 파일 구조가 유지됨을 보장합니다.

## 단계 1: 입력 DSV 파일 경로 가져오기
먼저, 소스 DSV 파일의 절대 경로나 상대 경로를 지정해야 합니다. 예시로 프로젝트의 `Data` 폴더에 있는 간단한 CSV를 사용하겠습니다.

```csharp
string inputFilePath = "Your Sample Document";
```

## 단계 2: Editor 인스턴스 생성
`Editor`는 로드, 편집 및 저장을 조정하는 핵심 클래스입니다. `FileInfo` 객체와 함께 인스턴스를 생성하면 파일 수명 주기를 완전히 제어할 수 있습니다.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## 단계 3: DSV 편집 옵션 생성
`DelimitedTextEditOptions`는 편집기에게 파일을 어떻게 해석할지 알려줍니다. 구분자, 첫 번째 행에 헤더가 있는지 여부, 문자 인코딩을 설정할 수 있습니다.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## 단계 4: EditableDocument 인스턴스 생성
`EditableDocument`는 소스 파일의 변경 가능한 메모리 내 버전을 나타냅니다. 옵션과 함께 `Editor.Edit`를 호출하면 `EditableDocument`가 반환됩니다. 이 객체는 파일 텍스트를 변경 가능한 문자열로 보관하며, 필요에 따라 **parse delimited values C#** 작업을 수행할 준비가 되어 있습니다.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## 단계 5: 문서 내용 편집
`GetDocumentText()`는 편집 가능한 문서의 현재 텍스트를 문자열로 반환합니다. `EditableDocument.GetDocumentText()`를 통해 원본 텍스트를 가져오고, 수정 작업(예: 열 값 교체)을 수행한 뒤 결과를 새로운 문자열에 저장합니다. 여기에서 **edit CSV .NET**을 수행하면서 저수준 파일 스트림을 건드리지 않을 수 있습니다.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 단계 6: 업데이트된 내용으로 EditableDocument 생성
수정된 문자열을 다시 `EditableDocument`에 래핑합니다. 이 단계에서 변경 사항이 최종 확정되고 객체가 지원되는 모든 형식으로 저장될 준비가 됩니다.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## 단계 7: CSV 저장 옵션 생성
`DelimitedTextSaveOptions`는 편집된 내용을 CSV 파일에 다시 쓰는 방식을 지정합니다. 변경 사항을 저장할 준비가 되면 `DelimitedTextSaveOptions`를 구성합니다. 동일한 구분자, 다른 구분자, 혹은 줄 끝 스타일을 변경할 수도 있습니다.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 단계 8: TSV 저장 옵션 생성
탭 구분 버전이 필요하면 구분자를 `\t`로 바꾸면 됩니다. 동일한 `EditableDocument`를 다양한 옵션으로 여러 번 저장할 수 있습니다.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 단계 9: 스프레드시트 저장 옵션 생성
`SpreadsheetSaveOptions`는 문서를 .xlsx와 같은 Excel 호환 형식으로 내보내도록 구성합니다. GroupDocs.Editor를 사용하면 편집된 데이터를 Excel 호환 형식(`.xlsx`)으로 내보낼 수 있습니다. `SpreadsheetSaveOptions` 클래스는 열 유형, 수식 및 셀 스타일을 자동으로 처리합니다.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## 단계 10: 저장 경로 준비
각 형식에 대해 별개의 출력 경로를 정의합니다. 명확한 명명 규칙(`output.csv`, `output.tsv`, `output.xlsx` 등)을 사용하면 프로젝트를 체계적으로 유지할 수 있습니다.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## 단계 11: 편집된 문서 저장
`Save()`는 제공된 저장 옵션을 사용해 문서를 디스크에 기록합니다. 각 대상 형식에 맞는 옵션으로 `EditableDocument.Save`를 호출합니다. API는 파일을 직접 디스크에 쓰며, 별도로 지정하지 않는 한 원본 인코딩을 보존합니다.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## 단계 12: EditableDocument 인스턴스 해제
`Editor`와 `EditableDocument` 모두 `IDisposable`을 구현합니다. 이를 해제하면 파일 핸들과 관리되지 않는 리소스가 해제되어 배치 작업에서 다수의 파일을 처리할 때 중요합니다.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## 일반적인 문제 및 해결책

| 문제 | 발생 원인 | 해결 방법 |
|-------|----------------|-----|
| **예상치 못한 추가 인용 부호** | 기본 CSV 파서는 포함된 쉼표를 구분자로 오인할 수 있습니다. | `DelimitedTextEditOptions`에서 `EscapeMode = EscapeMode.DoubleQuote`를 설정합니다. |
| **대용량 파일 메모리 급증** | 스트리밍 없이 500 MB 파일을 로드합니다. | 지연 로딩을 활성화하는 `LoadOptions`와 함께 `Editor.Load`를 사용합니다. |
| **인코딩 불일치** | 소스 파일은 UTF‑16을 사용하지만 옵션은 기본적으로 UTF‑8을 사용합니다. | 저장 옵션에서 `Encoding = Encoding.Unicode`를 명시적으로 설정합니다. |

## 자주 묻는 질문

**Q: GroupDocs.Editor for .NET를 사용해 대용량 CSV 파일을 편집할 수 있나요?**  
A: 예, API는 데이터를 스트리밍하며 전체 문서를 메모리에 로드하지 않고 1 GB 이상의 파일을 처리할 수 있습니다.

**Q: GroupDocs.Editor for .NET가 CSV와 TSV 외에 다른 DSV 형식을 지원하나요?**  
A: 물론입니다 – `DelimitedTextEditOptions`에 지정하기만 하면 단일 문자 구분자(예: 파이프 `|`, 세미콜론 `;`)를 모두 지원합니다.

**Q: DSV 파일을 저장할 때 인코딩을 사용자 지정할 수 있나요?**  
A: 예, `DelimitedTextSaveOptions`의 `Encoding` 속성을 UTF‑8, UTF‑16, ISO‑8859‑1 또는 필요한 .NET `Encoding`으로 설정할 수 있습니다.

**Q: GroupDocs.Editor for .NET를 사용해 CSV 파일을 Excel 스프레드시트로 변환할 수 있나요?**  
A: 예 – 편집 후 `SpreadsheetSaveOptions`를 사용해 내용을 `.xlsx` 워크북으로 내보내면 됩니다.

**Q: GroupDocs.Editor for .NET에 대한 자세한 문서는 어디에서 찾을 수 있나요?**  
A: 자세한 API 레퍼런스와 코드 샘플은 **[here](https://tutorials.groupdocs.com/editor/net/)**에서 확인할 수 있습니다.

---

**마지막 업데이트:** 2026-06-06  
**테스트 환경:** GroupDocs.Editor 23.10 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Editor .NET용 일반 텍스트 및 DSV 문서 편집 튜토리얼](/editor/net/plain-text-dsv-documents/)
- [효율적인 CSV 문서 편집 및 변환을 위한 GroupDocs.Editor .NET 마스터](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [GroupDocs.Editor와 함께 .NET에서 문서 로딩 마스터하기: 종합 가이드](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)