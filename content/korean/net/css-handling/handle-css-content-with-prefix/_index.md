---
date: 2026-09-26
description: 이 상세한 단계별 튜토리얼에서 GroupDocs.Editor for .NET을 사용하여 CSS 접두사를 처리하고 CSS 콘텐츠를
  추출하는 방법을 배웁니다.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: 접두사를 사용한 CSS 콘텐츠 처리
og_description: GroupDocs.Editor for .NET을 사용하여 CSS 접두사를 처리하고 CSS 콘텐츠를 추출하는 방법을 알아보세요.
  CSS 리소스에 URL을 앞에 추가하고 스타일시트를 가져오는 단계별 가이드를 따라 보세요.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: GroupDocs.Editor for .NET에서 CSS 접두사를 처리하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: GroupDocs.Editor for .NET에서 CSS 접두사를 처리하는 방법
type: docs
url: /ko/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# GroupDocs.Editor for .NET에서 CSS 접두사 처리 방법

이 튜토리얼에서는 GroupDocs.Editor for .NET을 사용하여 문서 내부의 스타일시트를 작업할 때 **CSS 접두사 처리 방법**을 배웁니다. 이미지, 폰트 또는 기타 외부 리소스에 URL을 앞에 붙여야 할 경우, 아래 단계에서는 정확히 **CSS 접두사 처리 방법**과 **CSS 콘텐츠 추출 방법**을 보여줍니다. 가이드를 마치면 리소스 경로를 재작성하고, 원시 CSS 문자열을 가져와 웹 워크플로에 자신 있게 통합할 수 있습니다.

## 빠른 답변
- **“CSS 접두사 처리”는 무엇을 의미합니까?** CSS에서 참조되는 외부 리소스에 사용자 정의 URL 접두사를 추가하는 것입니다.  
- **어떤 API 메서드가 CSS 스타일을 반환합니까?** `EditableDocument.GetCssContent(...)`.  
- **라이선스가 필요합니까?** 체험 라이선스를 사용할 수 있으며, 프로덕션 환경에서는 상용 라이선스가 필요합니다.  
- **지원되는 .NET 버전은 무엇입니까?** .NET Framework 4.5+ 및 .NET Core/5/6.  
- **런타임에 접두사를 변경할 수 있습니까?** 예 – `GetCssContent`에 다른 문자열을 전달하면 됩니다.

## CSS 접두사 처리란 무엇입니까?
이 용어는 CSS 파일 내 이미지, 폰트 또는 기타 외부 자산의 URL을 재작성하여 CDN이나 보안 서버와 같이 제어 가능한 위치를 가리키도록 하는 것을 의미합니다. 일관된 기본 URL을 앞에 붙이면 브라우저나 웹 기반 뷰어에서 문서를 렌더링할 때 모든 리소스가 올바르게 로드됩니다.

## CSS 콘텐츠를 추출하기 위해 GroupDocs.Editor를 사용하는 이유는 무엇입니까?
GroupDocs.Editor는 WordProcessing 문서에 포함된 원본 CSS를 읽고, 원시 스타일시트 문자열을 반환하며, 렌더링 또는 저장 전에 이를 조작할 수 있게 해줍니다. 이를 통해 수동 파싱을 없애고, 문서 내부 표현에 대한 충실도를 보장하며, **30개 이상의 파일 형식**을 지원하고 **500 MB**까지 파일을 메모리에 전체 로드하지 않고 처리할 수 있습니다.

## 전제 조건
- Visual Studio: 작업 가능한 Visual Studio 설치가 필요합니다.  
- .NET Framework: .NET Framework가 설치되어 있는지 확인하십시오.  
- GroupDocs.Editor for .NET: [GroupDocs.Editor for .NET 다운로드 페이지](https://releases.groupdocs.com/editor/net/)에서 다운로드할 수 있습니다.  
- 샘플 문서: 편집할 샘플 문서를 준비하십시오.

## 네임스페이스 가져오기
먼저 필요한 네임스페이스를 가져와 코드가 원활히 실행되도록 합니다. 이 단계에서는 GroupDocs.Editor의 핵심 클래스를 사용할 수 있게 됩니다.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 1단계: Editor 초기화
`Editor` 클래스는 GroupDocs.Editor에서 문서를 작업하기 위한 진입점이며, 로드, 편집 및 저장 작업을 관리합니다.  
첫 번째 단계에서는 샘플 문서를 사용해 `Editor` 인스턴스를 생성합니다. 이렇게 하면 편집 환경이 설정됩니다.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 2단계: 문서 편집
`EditableDocument` 객체는 파일의 편집 가능한 버전을 나타내며 CSS, 이미지, HTML 등 내부 파트를 노출합니다.  
다음으로 `EditableDocument` 객체를 얻습니다. 이 객체를 통해 문서 내부 CSS를 작업할 수 있습니다.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 3단계: 외부 접두사 설정
이미지와 폰트에 대한 URL 접두사를 정의합니다. 이 접두사는 CSS에서 찾은 모든 이미지 및 폰트 참조 앞에 자동으로 붙습니다.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 4단계: 접두사가 포함된 CSS 콘텐츠 추출
`GetCssContent`는 이미 정의한 접두사가 포함된 CSS 스타일시트 문자열 컬렉션을 반환합니다.  
정의한 접두사를 전달하여 `GetCssContent`를 호출하면, 접두사가 포함된 CSS 스타일시트 문자열 목록을 얻을 수 있습니다.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 5단계: 결과 출력
찾은 스타일시트 수를 출력하고 각 스타일시트를 표시합니다. 이를 통해 접두사가 올바르게 적용되었는지 확인할 수 있습니다.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## 일반적인 문제 및 해결책
- **스타일시트가 반환되지 않음** – 소스 문서에 실제로 CSS가 포함되어 있는지 확인하십시오(예: 스타일이 적용된 표나 임베디드 HTML이 있는 Word 문서).  
- **잘못된 URL** – 접두사 문자열이 서버 라우팅에 맞는 구분자(`/` 또는 `=`)로 끝나는지 다시 확인하십시오.  
- **성능 문제** – 매우 큰 문서의 경우 메모리 사용량을 줄이기 위해 스타일시트를 배치 처리하는 것을 고려하십시오.

## 자주 묻는 질문

**Q: GroupDocs.Editor for .NET를 다른 문서 형식과 함께 사용할 수 있습니까?**  
A: 예, GroupDocs.Editor for .NET는 PDF, Word, Excel, PowerPoint 등 많은 형식을 지원합니다.

**Q: GroupDocs.Editor for .NET에 대한 무료 체험판이 있습니까?**  
A: 물론입니다! [GroupDocs 무료 체험 페이지](https://releases.groupdocs.com/)에서 무료 체험을 시작할 수 있습니다.

**Q: GroupDocs.Editor for .NET에 대한 임시 라이선스를 어떻게 얻을 수 있습니까?**  
A: [임시 라이선스 페이지](https://purchase.groupdocs.com/temporary-license/)에서 임시 라이선스를 받을 수 있습니다.

**Q: GroupDocs.Editor for .NET에 대한 자세한 문서는 어디에서 찾을 수 있습니까?**  
A: 자세한 문서는 [GroupDocs.Editor for .NET 문서 사이트](https://tutorials.groupdocs.com/editor/net/)에서 확인할 수 있습니다.

**Q: GroupDocs.Editor for .NET에 대한 지원 옵션은 무엇입니까?**  
A: [GroupDocs.Editor 지원 포럼](https://forum.groupdocs.com/c/editor/20)을 통해 지원을 받을 수 있습니다.

## 추가 자주 묻는 질문

**Q: CSS를 추출한 후에 접두사를 변경할 수 있습니까?**  
A: 예. 다른 접두사 문자열을 사용해 `GetCssContent`를 다시 호출하면 런타임에 전달한 값이 적용됩니다.

**Q: 비밀번호로 보호된 문서에서도 작동합니까?**  
A: 예. `Editor` 인스턴스를 만들 때 `WordProcessingLoadOptions`에 비밀번호를 제공하면 됩니다.

**Q: 수정된 CSS를 문서에 다시 저장할 수 있습니까?**  
A: 현재 GroupDocs.Editor는 CSS에 대해 읽기 전용 액세스만 제공합니다. 변경 사항을 지속하려면 문서의 기본 XML API를 사용해 원본 스타일시트를 교체해야 합니다.

---

**최종 업데이트:** 2026-09-26  
**테스트 환경:** GroupDocs.Editor 23.12 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Editor .NET를 사용하여 Word 문서에서 외부 CSS 추출: 종합 가이드](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [GroupDocs.Editor .NET를 사용하여 Word 문서에서 HTML 추출 및 접두사 추가](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [GroupDocs.Editor .NET를 사용하여 Word 문서에서 HTML 콘텐츠 추출 및 수정 방법](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)