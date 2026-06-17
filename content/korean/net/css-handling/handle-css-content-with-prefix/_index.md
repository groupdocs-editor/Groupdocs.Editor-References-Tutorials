---
date: 2026-03-06
description: 이 자세한 단계별 튜토리얼에서 접두사가 있는 CSS 콘텐츠를 처리하고 GroupDocs.Editor for .NET을 사용하여
  CSS 콘텐츠를 추출하는 방법을 배워보세요.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: 접두어가 있는 CSS 콘텐츠 처리
type: docs
url: /ko/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# CSS 콘텐츠를 프리픽스로 처리하기

이 튜토리얼에서는 GroupDocs.Editor for .NET을 사용하여 문서 내부의 스타일시트를 작업할 때 **css 프리픽스를 처리하는 방법**을 알아봅니다. 이미지, 폰트 또는 기타 외부 리소스에 URL을 앞에 붙여야 할 경우, 아래 단계에서는 **css 프리픽스를 처리하는 방법**과 **css 콘텐츠를 추출하는 방법**을 정확히 보여줍니다.

## 빠른 답변
- **“handle css prefix”가 의미하는 바는?** CSS에서 참조되는 외부 리소스에 사용자 정의 URL 프리픽스를 추가하는 것입니다.
- **어떤 API 메서드가 CSS 스타일을 반환하나요?** `EditableDocument.GetCssContent(...)`.
- **라이선스가 필요합니까?** 체험 라이선스를 사용할 수 있으며, 프로덕션에서는 상업용 라이선스가 필요합니다.
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.5 이상 및 .NET Core/5/6.
- **런타임에 프리픽스를 변경할 수 있나요?** 예 – `GetCssContent`에 다른 문자열을 전달하면 됩니다.

## **handle css prefix**란 무엇인가요?
CSS 리소스에 프리픽스를 적용하면 이미지, 폰트 또는 기타 자산의 경로가 재작성되어 사용자가 제어하는 위치(예: CDN 또는 보안 서버)를 가리키게 됩니다. 이는 문서를 내보낼 때 모든 외부 참조가 웹 애플리케이션에서 접근 가능하도록 해야 할 경우에 특히 유용합니다.

## **extract css content**를 위해 GroupDocs.Editor를 사용하는 이유
GroupDocs.Editor는 워드 프로세싱 문서에 포함된 원본 CSS를 읽어 원시 스타일시트 문자열을 제공하고, 렌더링이나 저장 전에 이를 조작할 수 있게 해줍니다. 이를 통해 수동 파싱이 필요 없으며 추출된 CSS가 문서의 내부 표현과 일치함을 보장합니다.

## 사전 요구 사항
시작하기 전에 다음 사전 요구 사항이 준비되어 있는지 확인하십시오:
- Visual Studio: Visual Studio가 설치되어 있어야 합니다.  
- .NET Framework: .NET Framework가 설치되어 있는지 확인하십시오.  
- GroupDocs.Editor for .NET: [here](https://releases.groupdocs.com/editor/net/)에서 다운로드할 수 있습니다.  
- Sample Document: 편집할 샘플 문서를 준비하십시오.

## 네임스페이스 가져오기
먼저, 코드가 원활히 실행되도록 필요한 네임스페이스를 가져옵니다. 이 단계에서는 GroupDocs.Editor의 핵심 클래스를 사용할 수 있게 됩니다.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 단계 1: Editor 초기화
첫 번째 단계에서는 샘플 문서를 사용하여 `Editor` 인스턴스를 생성합니다. 이를 통해 편집 환경이 설정됩니다.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 단계 2: 문서 편집
다음으로, `EditableDocument` 객체를 가져옵니다. 이 객체는 파일의 편집 가능한 버전을 나타내며 내부 구성 요소를 작업할 수 있게 해줍니다.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 단계 3: 외부 프리픽스 설정
이미지와 폰트에 대한 URL 프리픽스를 정의합니다. 이 프리픽스는 CSS에서 발견되는 모든 이미지와 폰트 참조 앞에 추가됩니다.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 프리픽스를 사용한 **Extract CSS content**
`GetCssContent`를 호출하고 방금 정의한 프리픽스를 전달합니다. 이 메서드는 이미 프리픽스가 적용된 URL을 포함하는 CSS 스타일시트 문자열 리스트를 반환합니다.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 단계 5: 결과 출력
찾은 스타일시트 수를 출력하고 각 스타일시트를 표시합니다. 이를 통해 프리픽스가 올바르게 적용되었는지 확인할 수 있습니다.

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
- **No stylesheets returned** – 소스 문서에 실제로 CSS가 포함되어 있는지 확인하십시오(예: 스타일이 적용된 표나 임베디드 HTML이 있는 Word 문서).
- **Incorrect URLs** – 프리픽스 문자열이 서버 라우팅에 맞는 구분자(`/` 또는 `=`)로 끝나는지 다시 확인하십시오.
- **Performance concerns** – 매우 큰 문서의 경우 메모리 사용량을 줄이기 위해 스타일시트를 배치 처리하는 것을 고려하십시오.

## 결론
GroupDocs.Editor for .NET을 사용하여 프리픽스로 CSS 콘텐츠를 처리하는 것은 간단하면서도 강력합니다. 이 단계들을 따르면 **handle css prefix**를 수행하고 **extract css content**를 통해 원시 CSS를 가져와 외부 리소스를 웹 워크플로에 원활히 통합할 수 있습니다. HTML 변환, 이미지 추출, 문서 병합 등 다른 GroupDocs.Editor 기능도 살펴보면 API에서 더 큰 가치를 얻을 수 있습니다.

## FAQ
### GroupDocs.Editor for .NET를 다른 문서 형식과 함께 사용할 수 있나요?
예, GroupDocs.Editor for .NET는 PDF, Word, Excel 등을 포함한 다양한 문서 형식을 지원합니다.

### GroupDocs.Editor for .NET의 무료 체험판을 이용할 수 있나요?
물론입니다! 무료 체험을 시작하려면 [here](https://releases.groupdocs.com/)를 클릭하세요.

### GroupDocs.Editor for .NET의 임시 라이선스를 어떻게 얻나요?
임시 라이선스는 [here](https://purchase.groupdocs.com/temporary-license/)에서 얻을 수 있습니다.

### GroupDocs.Editor for .NET에 대한 자세한 문서는 어디서 찾을 수 있나요?
자세한 문서는 [here](https://tutorials.groupdocs.com/editor/net/)에서 확인할 수 있습니다.

### GroupDocs.Editor for .NET에 대한 지원 옵션은 무엇인가요?
지원은 [here](https://forum.groupdocs.com/c/editor/20)에서 받을 수 있습니다.

## 추가 자주 묻는 질문

**Q: CSS를 추출한 후에 프리픽스를 변경할 수 있나요?**  
A: 예. 다른 프리픽스 문자열을 사용해 `GetCssContent`를 다시 호출하면 됩니다; 이 메서드는 항상 런타임에 전달한 값을 사용합니다.

**Q: 비밀번호로 보호된 문서에서도 작동하나요?**  
A: 예. `Editor` 인스턴스를 생성할 때 `WordProcessingLoadOptions`에 비밀번호를 제공하면 됩니다.

**Q: 수정된 CSS를 문서에 다시 저장할 수 있나요?**  
A: 현재 GroupDocs.Editor는 CSS에 대해 읽기 전용 접근만 제공합니다. 변경 사항을 지속하려면 문서의 기본 XML API를 사용해 원본 스타일시트를 교체해야 합니다.

---

**마지막 업데이트:** 2026-03-06  
**테스트 환경:** GroupDocs.Editor 23.12 for .NET  
**작성자:** GroupDocs