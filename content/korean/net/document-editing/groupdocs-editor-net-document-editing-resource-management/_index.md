---
date: '2026-03-28'
description: GroupDocs.Editor for .NET를 사용하여 편집 가능한 문서를 만들고, Word에서 이미지와 글꼴을 추출하며,
  Word 문서를 .NET에서 편집하는 방법을 배웁니다. 성능 팁이 포함되어 있습니다.
keywords:
- GroupDocs.Editor for .NET
- document editing .NET
- resource management .NET
title: GroupDocs.Editor .NET을 사용하여 편집 가능한 문서를 만들고 리소스를 관리하기
type: docs
url: /ko/net/document-editing/groupdocs-editor-net-document-editing-resource-management/
weight: 1
---

# GroupDocs.Editor .NET으로 편집 가능한 문서 만들기 및 리소스 관리

귀하의 .NET 애플리케이션에서 효율적인 문서 편집 및 리소스 관리에 어려움을 겪고 있나요? **GroupDocs.Editor for .NET**은 이러한 작업을 간소화하는 강력한 솔루션을 제공합니다. 이 튜토리얼에서는 **editable document** 인스턴스를 생성하고, 이미지와 폰트를 추출하며, 리소스를 성능 있게 처리하는 방법을 배웁니다.

## 빠른 답변
- **“create editable document”는 무엇을 의미합니까?** 파일을 GroupDocs.Editor에 로드하고 프로그래밍 방식으로 수정할 수 있는 `EditableDocument` 객체를 얻는 것을 의미합니다.  
- **Word 파일에서 이미지를 추출하려면 어떻게 합니까?** `EditableDocument.Images` 컬렉션을 사용하고 각 `IImageResource`에 대해 `Save`를 호출합니다.  
- **Word 문서에서 폰트를 추출할 수 있나요?** 예 – `EditableDocument.Fonts` 컬렉션을 통해 모든 포함된 폰트에 접근할 수 있습니다.  
- **Word 문서를 .NET에서 편집하려면 어떤 키워드가 도움이 됩니까?** 주요 API 호출은 `editor.Edit(editOptions)`입니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 비시험 배포에는 유효한 GroupDocs.Editor 라이선스가 필요합니다.

## “create editable document”란 무엇입니까?
`Editor.Edit(...)`를 호출하면 GroupDocs.Editor가 소스 파일을 파싱하고 `EditableDocument`를 반환합니다. 이 객체는 문서의 구조 요소(텍스트, 이미지, 폰트, CSS)를 노출하므로 최종 버전을 저장하기 전에 이를 읽고, 수정하고, 교체할 수 있습니다.

## 리소스 추출을 위해 GroupDocs.Editor를 사용하는 이유
- **중앙 집중식 API** – Word, PDF, Excel, PowerPoint 파일에서 작동합니다.  
- **고충실도** – 레이아웃을 유지하면서 포함된 자산에 대한 저수준 접근을 제공합니다.  
- **성능 최적화** – 리소스를 즉시 해제하여 메모리 사용을 제어할 수 있습니다.

## 사전 요구 사항
- .NET 4.6 이상 (또는 지원되는 .NET Core/5+ 런타임)  
- Visual Studio 또는 다른 C# IDE  
- C# 파일 I/O에 대한 기본 지식 (필수는 아니지만 도움이 됩니다)

## .NET용 GroupDocs.Editor 설정
GroupDocs.Editor를 사용하려면 프로젝트에 종속성으로 추가하세요. 설치 방법은 다음과 같습니다:

### 설치 정보
**.NET CLI 사용:**  
```bash
dotnet add package GroupDocs.Editor
```

**Package Manager 사용:**  
```powershell
Install-Package GroupDocs.Editor
```

**NuGet Package Manager UI:**  
"GroupDocs.Editor"를 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계
- **무료 체험:** 공식 사이트에서 무료 체험판을 다운로드하여 시작합니다.  
- **임시 라이선스:** 전체 기능을 사용하려면 임시 라이선스를 신청합니다.  
- **구매:** 장기 사용이 필요하면 구매를 고려하십시오.

설치가 완료되면 기본 설정으로 GroupDocs.Editor를 초기화합니다:
```csharp
using GroupDocs.Editor;

Editor editor = new Editor("path/to/your/document");
```

## GroupDocs.Editor로 편집 가능한 문서 만들기
다음은 파일을 로드하고, 편집 가능한 문서를 생성한 뒤 리소스를 정리하는 방법을 단계별로 보여주는 안내입니다.

### 단계 1: Editor 초기화
소스 파일 경로를 제공하고 필요한 로드 옵션을 지정합니다(예: Word 처리).  
```csharp
string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

### 단계 2: EditableDocument 인스턴스 생성
편집 옵션을 구성합니다—여기서는 엔진에 **전체** 폰트를 추출하도록 요청합니다. 이는 나중에 폰트를 교체하거나 다른 곳에 삽입할 때 유용합니다.  
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions { FontExtraction = FontExtractionOptions.ExtractAll };
EditableDocument beforeEdit = editor.Edit(editOptions);
beforeEdit.Dispose();
editor.Dispose();
```

> **Pro tip:** 작업이 끝나는 즉시 `EditableDocument`와 `Editor`를 해제하여 메모리 사용량을 낮게 유지하십시오.

## 리소스 추출 및 정보 표시
이제 편집 가능한 문서를 보유했으므로 이미지, 폰트 및 스타일시트를 추출할 수 있습니다.

### 단계 3: 리소스 수집
```csharp
List<IImageResource> images = beforeEdit.Images;
List<FontResourceBase> fonts = beforeEdit.Fonts;
List<CssText> stylesheets = beforeEdit.Css;
```

### 단계 4: 추출된 리소스 저장
다음 루프는 선택한 폴더에 각 리소스를 기록합니다. 이는 미디어 라이브러리를 구축하거나 추가 분석을 수행할 때 유용합니다.  
```csharp
string outputFolderPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "Resources");
Directory.CreateDirectory(outputFolderPath);

foreach (var image in images)
{
    string imagePath = Path.Combine(outputFolderPath, image.FilenameWithExtension);
    image.Save(imagePath);
}

foreach (var font in fonts)
{
    string fontPath = Path.Combine(outputFolderPath, font.FilenameWithExtension);
    font.Save(fontPath);
}

foreach (var stylesheet in stylesheets)
{
    string stylesheetPath = Path.Combine(outputFolderPath, stylesheet.FilenameWithExtension);
    stylesheet.Save(stylesheetPath);
}
```

## 리소스 콘텐츠 직접 접근
때때로 원시 바이트 또는 Base64 문자열이 필요할 수 있습니다(예: HTML 이메일에 이미지를 삽입할 때).

### 단계 5: 바이트 스트림 및 Base64 문자열 가져오기
```csharp
Stream imageStream = images[0].ByteContent; // Get byte stream of the first image
string base64EncodedResource = images[0].TextContent; // Get base64 string of the first image
```

## 실용적인 적용 사례
GroupDocs.Editor .NET은 다양한 시스템에 통합되어 문서 관리 워크플로를 향상시킬 수 있습니다:

1. **자동 문서 처리** – 계약서를 대량 처리하고, 서명을 추출하며, 콘텐츠를 재포맷합니다.  
2. **맞춤형 보고서 생성** – 템플릿의 자리표시자를 프로그래밍 방식으로 교체합니다.  
3. **콘텐츠 관리 시스템(CMS)** – 웹 페이지 전반에 재사용하기 위해 포함된 미디어를 추출합니다.

## 성능 고려 사항
- **조기 해제:** 작업이 끝나는 즉시 `EditableDocument`와 `Editor`에 `Dispose()`를 호출합니다.  
- **비동기 옵션:** 가능한 경우 추출을 백그라운드 스레드에서 실행하여 UI가 응답하도록 유지합니다.  
- **폰트 추출 튜닝:** 모든 폰트가 필요하지 않다면 `FontExtraction`을 `ExtractUsedOnly`로 설정하여 메모리 오버헤드를 줄입니다.

## 일반적인 함정 및 팁
| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **대용량 파일에서 메모리 부족** | 많은 리소스를 처리하는 동안 Editor를 계속 유지하기 때문입니다. | 객체를 즉시 해제하고 파일을 하나씩 처리하십시오. |
| **추출 후 이미지 누락** | 잘못된 컬렉션(`beforeEdit.Images` vs. `beforeEdit.Resources`)을 사용했기 때문입니다. | 항상 `EditableDocument.Images`를 참조하십시오. |
| **잘못된 파일 확장자** | `FilenameWithExtension`을 확인하지 않고 리소스를 저장했기 때문입니다. | 파일 경로를 만들 때 제공된 `FilenameWithExtension` 속성을 사용하십시오. |

## 자주 묻는 질문

**Q: GroupDocs.Editor가 모든 .NET 버전과 호환됩니까?**  
A: 예, .NET Framework 4.6+ 및 최신 .NET Core/5/6 런타임을 지원합니다.

**Q: Word가 아닌 문서에서 리소스를 추출할 수 있나요?**  
A: GroupDocs.Editor는 PDF, 스프레드시트, 프레젠테이션을 지원하므로 해당 형식에서도 이미지, 폰트 및 CSS를 추출할 수 있습니다.

**Q: 대용량 파일을 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 비동기 메서드를 사용하고, 스트림으로 리소스를 처리하며, 작업이 끝나는 즉시 객체를 해제하십시오.

**Q: GroupDocs.Editor의 라이선스 옵션은 무엇인가요?**  
A: 무료 체험으로 시작하고, 평가를 위해 임시 라이선스를 얻거나, 프로덕션을 위한 정식 상용 라이선스를 구매할 수 있습니다.

**Q: 편집 경험을 추가로 맞춤 설정할 수 있나요?**  
A: 물론입니다. API는 사용자 정의 CSS 삽입, 폰트 대체, 레이아웃 조정 등 다양한 옵션을 제공합니다.

## 리소스
- [문서](https://docs.groupdocs.com/editor/net/)
- [API 레퍼런스](https://reference.groupdocs.com/editor/net/)
- [다운로드](https://releases.groupdocs.com/editor/net/)
- [무료 체험](https://releases.groupdocs.com/editor/net/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license)
- [지원 포럼](https://forum.groupdocs.com/c/editor/)

---

**최종 업데이트:** 2026-03-28  
**테스트 환경:** GroupDocs.Editor 23.12 for .NET  
**작성자:** GroupDocs