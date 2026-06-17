---
date: '2026-04-11'
description: GroupDocs.Editor for .NET를 사용하여 편집 가능한 문서를 만드는 방법을 배우고, 문서를 효율적으로 HTML로
  저장하세요.
keywords:
- create editable document
- extract images from document
- save document as html
title: GroupDocs.Editor .NET으로 편집 가능한 문서 만들기
type: docs
url: /ko/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# GroupDocs.Editor .NET으로 편집 가능한 문서 만들기

오늘날 디지털 시대에 **편집 가능한 문서 만들기**는 모든 현대 워크플로우의 핵심 요구 사항입니다. 협업 편집기, 콘텐츠 관리 시스템, 자동 보고 도구를 구축하든, 프로그래밍 방식으로 HTML 파일을 편집하고 저장하는 기능은 수많은 시간을 절약할 수 있습니다. 이 튜토리얼에서는 GroupDocs.Editor for .NET을 사용하여 **편집 가능한 문서** 인스턴스를 만들고, 리소스를 추출하며, **문서를 HTML로 저장**하는 방법을 보여줍니다.

## 빠른 답변
- **“편집 가능한 문서 만들기”는 무엇을 의미합니까?** 프로그래밍 방식으로 수정할 수 있는 GroupDocs.Editor `EditableDocument` 객체에 소스 파일을 로드하는 것을 의미합니다.  
- **HTML로 변환할 수 있는 형식은 무엇입니까?** Word, Excel, PowerPoint 및 기타 많은 Office 형식이 지원됩니다.  
- **문서에서 이미지를 추출하려면 어떻게 해야 하나요?** `EditableDocument.Images` 컬렉션을 사용합니다.  
- **모든 리소스가 포함된 단일 HTML 문자열을 생성할 수 있나요?** 예—`GetEmbeddedHtml()`을 호출합니다.  
- **프로덕션에 라이선스가 필요합니까?** 평가용으로는 체험판이 작동하지만, 상업적 사용을 위해서는 영구 라이선스가 필요합니다.

## “편집 가능한 문서 만들기”란 무엇입니까?
편집 가능한 문서를 만든다는 것은 소스 파일(예: .docx)을 GroupDocs.Editor에 로드하여 `EditableDocument` 객체를 반환하는 것을 의미합니다. 이 객체는 문서의 HTML 마크업, 이미지, 폰트 및 CSS를 노출하여 콘텐츠를 편집하고, 리소스를 교체하거나 전체를 웹 페이지에 삽입할 수 있게 합니다.

## 이 작업에 GroupDocs.Editor .NET을 사용하는 이유
- **전체 기능 API** – Word, Excel, PowerPoint 등을 처리합니다.  
- **리소스 추출** – 간단한 속성을 사용하여 이미지, 폰트 및 스타일시트를 추출합니다.  
- **임베디드 HTML 생성** – 모든 리소스를 포함하는 단일 HTML 문자열을 생성하여 이메일이나 단일 페이지 앱에 적합합니다.  
- **성능 중심** – 객체를 즉시 폐기하고 필요할 때 비동기 패턴을 사용합니다.

## 전제 조건
Before implementing GroupDocs.Editor .NET features, ensure:
- **.NET 환경**: .NET 애플리케이션용 개발 환경을 설정합니다.
- **라이브러리 및 종속성**:
  - 다음 방법 중 하나를 사용하여 GroupDocs.Editor를 설치합니다:
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI**: 최신 버전을 검색하고 설치합니다.
- **지식 전제 조건**: C# 프로그래밍 및 기본 문서 처리 개념에 익숙한 것이 권장됩니다.

## .NET용 GroupDocs.Editor 설정
### 설치 안내
시작하려면 프로젝트에 GroupDocs.Editor를 설정합니다:
1. **.NET CLI를 통한 설치**:
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Package Manager 사용**:
   - Package Manager Console을 열고 다음을 실행합니다:
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI**:
   - NuGet으로 이동하여 "GroupDocs.Editor"를 검색하고 설치합니다.

### 라이선스 획득
- **무료 체험 및 임시 라이선스**:
  [GroupDocs releases](https://releases.groupdocs.com/editor/net/)에서 다운로드하여 무료 체험을 시작합니다. 장기 테스트를 위해서는 [구매 페이지](https://purchase.groupdocs.com/temporary-license)에서 임시 라이선스를 신청하세요.

### 기본 초기화 및 설정
다음은 애플리케이션에서 GroupDocs.Editor를 초기화하는 방법입니다:
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## GroupDocs.Editor .NET으로 편집 가능한 문서 만드는 방법
### EditableDocument 인스턴스 만들기
**개요**: `EditableDocument` 인스턴스를 생성하여 문서를 로드하고 편집합니다.

#### 문서 로드
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## 임베디드 HTML 생성 방법
### EditableDocument에서 임베디드 HTML 생성
**개요**: 전체 문서를 스타일시트와 리소스를 포함한 단일 임베디드 HTML 문자열로 변환합니다.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## 문서에서 이미지 추출 방법
### EditableDocument에서 리소스 추출
**개요**: 문서에서 이미지, 폰트, CSS 및 기타 리소스를 가져옵니다.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 문서에서 폰트 추출 방법
*위의 동일한 코드 블록은 `beforeEdit.Fonts`를 통해 폰트 리소스를 가져오는 방법도 보여줍니다.*

## 순수 HTML 콘텐츠 얻는 방법
### EditableDocument에서 HTML 콘텐츠 얻기
**개요**: 임베디드 리소스 없이 순수 HTML 콘텐츠를 추출합니다.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## HTML 콘텐츠에서 외부 링크 조정 방법
### HTML 콘텐츠에서 외부 링크 조정
**개요**: 사용자 정의 접두사를 사용하여 이미지, CSS 및 폰트의 외부 링크를 수정합니다.
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## 문서를 HTML로 저장하는 방법
### EditableDocument를 HTML 파일로 저장
**개요**: 편집된 문서를 HTML 형식으로 디스크에 저장합니다.
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## EditableDocument의 폐기 및 이벤트 처리
**개요**: 리소스 폐기를 관리하고 문서 수명 주기와 관련된 이벤트를 처리합니다.
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## HTML 콘텐츠에서 편집 가능한 문서 만들기
### HTML 콘텐츠에서 EditableDocument 만들기
**개요**: 기존 HTML 콘텐츠에서 `EditableDocument` 인스턴스를 재구성합니다.
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## 실용적인 적용 사례
GroupDocs.Editor .NET은 다양한 실제 시나리오에 활용될 수 있습니다:
- **협업 편집**: 여러 사용자가 원활하게 문서를 편집할 수 있도록 합니다.
- **웹 게시**: 문서를 웹 친화적인 형식으로 변환하여 온라인 보기 및 상호 작용을 가능하게 합니다.
- **콘텐츠 관리 시스템**: CMS 플랫폼과 통합하여 동적 콘텐츠 업데이트를 허용합니다.
- **자동 보고서 생성**: 다양한 데이터 소스에서 보고서 생성 및 서식을 자동화합니다.

## 성능 고려 사항
GroupDocs.Editor .NET의 성능을 최적화하려면:
- 사용 후 객체를 즉시 폐기하여 메모리를 효율적으로 관리합니다.  
- 파일 경로와 URL을 최적화하여 리소스 로딩 시간을 최소화합니다.  
- 적용 가능한 경우 비동기 처리를 사용하여 애플리케이션 응답성을 향상시킵니다.

## 일반적인 문제 및 해결책
- **대용량 파일은 높은 메모리 사용을 초래합니다** – 처리 완료 즉시 `EditableDocument` 객체를 폐기합니다.  
- **변환 후 이미지 링크가 깨짐** – `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)`를 호출할 때 올바른 리소스 핸들러 URI를 사용했는지 확인합니다.  
- **생성된 HTML에 폰트가 누락됨** – 소스 문서에 필요한 폰트가 포함되어 있거나 서버에 해당 폰트가 있는지 확인합니다.

## 자주 묻는 질문

**Q: GroupDocs.Editor .NET은 모든 문서 형식과 호환됩니까?**  
A: GroupDocs.Editor는 Word, Excel, PowerPoint 및 기타 많은 형식을 포함한 광범위한 형식을 지원하므로 다양한 사용 사례에 대한 유연성을 제공합니다.

**Q: GroupDocs.Editor를 사용하여 대용량 파일을 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 가능한 경우 비동기 API를 사용하고, 파일을 청크로 처리하며, 메모리를 해제하기 위해 `EditableDocument`와 `Editor` 객체를 항상 즉시 폐기합니다.

**Q: GroupDocs.Editor를 클라우드 스토리지 솔루션과 통합할 수 있나요?**  
A: 예, 파일 스트림을 `Editor` 생성자에 전달하여 Azure Blob Storage, Amazon S3, Google Cloud Storage 또는 기타 클라우드 제공업체와 연결할 수 있습니다.

**Q: GroupDocs.Editor의 라이선스 옵션은 무엇인가요?**  
A: 무료 체험으로 시작하거나 평가용으로 임시 라이선스를 신청할 수 있습니다. 프로덕션 배포에는 유료 라이선스가 필요합니다.

**Q: 문제가 발생하면 어디에서 지원을 받을 수 있나요?**  
A: [GroupDocs Support Forum](https://forum.groupdocs.com)에서 도움을 받을 수 있으며, GroupDocs 지원 팀에 직접 연락할 수도 있습니다.

---

**마지막 업데이트:** 2026-04-11  
**테스트 환경:** GroupDocs.Editor 23.12 for .NET  
**작성자:** GroupDocs  

---