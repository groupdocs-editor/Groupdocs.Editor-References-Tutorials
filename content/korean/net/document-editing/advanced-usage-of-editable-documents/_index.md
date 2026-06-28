---
date: 2026-03-14
description: GroupDocs.Editor for .NET를 사용하여 DOCX에서 이미지를 추출하고, DOCX를 HTML로 변환하며, 문서를
  HTML로 저장하는 방법을 배워보세요.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: DOCX에서 이미지 추출 – 고급 편집 가능한 문서 사용
type: docs
url: /ko/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# DOCX에서 이미지 추출 – 고급 편집 문서 사용법

.NET 개발자이면서 **DOCX에서 이미지 추출**을 원하고 문서 편집 기능을 강화하고 싶다면 GroupDocs.Editor for .NET이 강력한 도구 모음을 제공합니다. 이 포괄적인 가이드는 GroupDocs.Editor를 사용한 편집 가능한 문서의 고급 사용법을 단계별로 자세히 설명하여 전체 잠재력을 활용할 수 있도록 도와줍니다.

## 빠른 답변
- **DOCX 파일에서 이미지를 어떻게 추출하나요?** `Editor`로 문서를 로드한 뒤 `EditableDocument.Images`를 사용합니다.  
- **임베드된 리소스를 포함한 DOCX를 HTML로 변환할 수 있나요?** 예—`EditableDocument.GetEmbeddedHtml()` 또는 `GetContent()`를 호출하면 HTML 마크업을 얻을 수 있습니다.  
- **편집된 문서를 HTML로 저장하는 메서드는 무엇인가요?** `EditableDocument.Save(htmlFilePath)`를 사용하면 리소스 폴더와 함께 HTML 파일이 생성됩니다.  
- **Word 문서에서 폰트를 추출할 수 있나요?** `EditableDocument.Fonts`를 사용하여 모든 폰트 리소스를 가져옵니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 유효한 GroupDocs.Editor 라이선스가 필요합니다; 무료 체험판을 사용할 수 있습니다.

## **extract images from docx**란?
DOCX 파일에서 이미지를 추출한다는 것은 Word 문서에 삽입된 각 그림을 프로그래밍 방식으로 가져와 별도로 재사용, 수정 또는 저장할 수 있게 하는 것을 의미합니다. GroupDocs.Editor는 `EditableDocument` 인스턴스의 `Images` 컬렉션을 제공하므로 이 작업을 간단히 수행할 수 있습니다.

## 이 워크플로에 GroupDocs.Editor를 사용하는 이유
- **전체 리소스 제어** – 이미지, 폰트, CSS 등을 수동 ZIP 처리 없이 관리합니다.  
- **원활한 변환** – 레이아웃과 스타일을 유지하면서 DOCX를 HTML로 변환합니다.  
- **간편한 리소스 추출** – 커스텀 이미지 처리, 폰트 임베드 또는 CDN 전달에 유용합니다.  
- **견고한 해제 패턴** – 장기 실행 서비스에서 메모리 누수를 방지합니다.

## 사전 요구 사항
- 개발 머신에 Visual Studio가 설치되어 있어야 합니다.  
- GroupDocs.Editor와 호환되는 .NET Framework가 필요합니다.  
- GroupDocs.Editor for .NET 라이브러리. [여기서 다운로드](https://releases.groupdocs.com/editor/net/)할 수 있습니다.  
- 유효한 GroupDocs.Editor 라이선스. [무료 체험판](https://releases.groupdocs.com/)을 받거나 [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)를 구매하세요.

## 네임스페이스 가져오기
프로젝트에서 필요한 네임스페이스를 가져와야 합니다.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## 1단계: EditableDocument 인스턴스 생성
지원되는 형식의 입력 문서를 로드하고 편집 가능한 `EditableDocument` 인스턴스를 생성합니다.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

이 단계에서는 입력 문서를 로드하고 편집 준비를 합니다.

## **DOCX에서 이미지 추출** 방법
아래에서는 가장 일반적인 요구 사항인 Word 파일에서 모든 이미지를 가져오는 방법을 중심으로 리소스 추출 기능을 살펴봅니다.

## 2단계: 문서 리소스 추출
`EditableDocument`에는 추출 및 조작이 가능한 다양한 리소스가 포함되어 있습니다. 각각을 살펴보겠습니다.

### 2.1단계: 전체 문서를 HTML로 추출
문서 전체와 모든 리소스를 임베드한 HTML 문자열을 생성할 수 있습니다.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

이 문자열은 스타일시트, 이미지, 폰트가 base64로 인코딩되어 포함되므로 상당히 큽니다.

### 2.2단계: 모든 이미지 추출 *(핵심 키워드)*
문서에서 모든 이미지를 추출합니다—이것이 **extract images from docx**의 핵심입니다.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### 2.3단계: 모든 폰트 추출 *(보조 키워드)*
**Word에서 폰트를 추출**하려면 다음 코드를 사용하세요.

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### 2.4단계: 모든 스타일시트 추출
텍스트 형식의 스타일시트를 모두 추출합니다.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### 2.5단계: 모든 리소스 한 번에 수집
한 번의 호출로 모든 리소스를 수집합니다.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

여기에는 이미지, 폰트, 스타일시트가 포함됩니다.

### 2.6단계: HTML 마크업 얻기
임베드된 리소스 없이 문서의 HTML 마크업을 가져옵니다.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## **docx를 html로 변환**하면서 커스텀 처리하는 방법
외부 링크를 자체 리소스 핸들러를 가리키도록 조정해야 할 때가 있습니다.

## 3단계: 외부 링크 조정
### 3.1단계: 커스텀 프리픽스 준비
원본 외부 링크 앞에 붙일 프리픽스를 준비합니다.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### 3.2단계: 프리픽스가 적용된 HTML 마크업 생성
조정된 링크가 포함된 HTML 마크업을 생성합니다.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### 3.3단계: 본문 전용 HTML 콘텐츠 얻기
일부 WYSIWYG 편집기는 헤더 없이 순수 HTML 마크업만 처리합니다.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### 3.4단계: 프리픽스가 적용된 본문 전용 콘텐츠
커스텀 이미지 프리픽스와 함께 본문 전용 콘텐츠를 생성합니다.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### 3.5단계: 스타일시트 추출
문서에 사용된 스타일시트를 추출합니다.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### 3.6단계: 프리픽스가 적용된 스타일시트
커스텀 프리픽스와 함께 스타일시트를 추출합니다.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## **HTML로 문서 저장**을 올바르게 하는 방법
## 4단계: HTML로 문서 저장
편집된 문서를 HTML 파일로 저장하고 리소스를 함께 저장합니다.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

이 메서드는 스타일시트, 이미지, 폰트와 같은 리소스용 별도 디렉터리를 생성합니다.

## 5단계: EditableDocument 해제
`EditableDocument`는 `IDisposable`을 구현하며 인스턴스가 해제되었는지 확인할 수 있는 기능을 제공합니다.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### 5.1단계: Dispose 이벤트 처리
Dispose 이벤트에 구독할 수도 있습니다.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## 6단계: HTML에서 EditableDocument 생성
HTML 문서에서 `EditableDocument` 인스턴스를 생성합니다.

### 6.1단계: HTML 파일에서

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### 6.2단계: HTML 마크업에서

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

이 인스턴스(`afterEditFromFile` 및 `afterEditFromMarkup`)는 원본(`beforeEdit`)과 동일합니다.

## 7단계: 수동 해제
`EditableDocument` 인스턴스를 수동으로 해제합니다.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

이를 통해 리소스가 올바르게 정리됩니다.

## 일반적인 문제와 해결책
- **이미지가 추출 후 표시되지 않음:** 문서에 실제로 임베드된 이미지가 있는지 확인하고 `Edit` 호출 후 `beforeEdit.Images`에 접근했는지 점검하세요.  
- **HTML 출력에 폰트 누락:** `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)`를 호출해 폰트 URL이 올바르게 임베드되었는지 확인하세요.  
- **큰 HTML 문자열로 인한 메모리 압박:** 리소스가 임베드되지 않은 마크업을 원한다면 `GetContent()`를 사용하고 이미지/ CSS는 별도 파일로 제공하세요.

## 자주 묻는 질문

**Q: GroupDocs.Editor가 지원하는 형식은 무엇인가요?**  
A: GroupDocs.Editor는 DOCX, XLSX, PPTX 등 다양한 인기 오피스 형식을 지원합니다.

**Q: 라이선스 없이 GroupDocs.Editor를 사용할 수 있나요?**  
A: 예, [무료 체험판](https://releases.groupdocs.com/)이나 [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)를 이용할 수 있습니다.

**Q: 문서에서 특정 리소스를 어떻게 추출하나요?**  
A: `EditableDocument` 인스턴스의 `Images`, `Fonts`, `Css` 컬렉션을 사용하면 됩니다.

**Q: HTML 출력에서 링크를 조정할 수 있나요?**  
A: 예, `GetContent` 또는 `GetBodyContent`에 커스텀 URI 프리픽스를 전달해 이미지, CSS, 폰트 링크를 재작성할 수 있습니다.

**Q: 편집된 문서를 HTML 파일로 저장하려면 어떻게 하나요?**  
A: `EditableDocument` 인스턴스의 `Save` 메서드에 `.html`로 끝나는 파일 경로를 제공하면 됩니다.

---

**마지막 업데이트:** 2026-03-14  
**테스트 환경:** GroupDocs.Editor for .NET (최신 릴리스)  
**작성자:** GroupDocs