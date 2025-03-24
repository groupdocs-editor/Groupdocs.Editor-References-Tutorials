---
title: 편집 가능한 문서의 고급 활용
linktitle: 편집 가능한 문서의 고급 활용
second_title: GroupDocs.Editor .NET API
description: 프로그래밍 방식으로 문서에서 리소스를 생성, 편집 및 추출하는 .NET용 GroupDocs.Editor의 고급 사용법을 알아보세요.
weight: 11
url: /ko/net/document-editing/advanced-usage-of-editable-documents/
---

# 편집 가능한 문서의 고급 활용

## 소개
문서 편집 기능을 향상시키려는 .NET 개발자라면 .NET용 GroupDocs.Editor가 강력한 도구 모음을 제공합니다. 이 포괄적인 가이드는 GroupDocs.Editor를 사용하여 편집 가능한 문서의 고급 사용법을 안내하고 각 단계를 자세히 분석하여 잠재력을 최대한 활용할 수 있도록 합니다.
## 전제조건
고급 기능을 살펴보기 전에 다음 사항을 확인하세요.
- 개발 컴퓨터에 Visual Studio가 설치되어 있습니다.
- GroupDocs.Editor와 호환되는 .NET Framework.
-  .NET 라이브러리용 GroupDocs.Editor. 당신은 할 수 있습니다[여기에서 다운로드하십시오](https://releases.groupdocs.com/editor/net/).
-  유효한 GroupDocs.Editor 라이센스. 당신은 얻을 수 있습니다[무료 시험판](https://releases.groupdocs.com/) 또는 구매[임시면허](https://purchase.groupdocs.com/temporary-license/).
## 네임스페이스 가져오기
시작하려면 .NET 프로젝트에서 필요한 네임스페이스를 가져와야 합니다.
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
 먼저 인스턴스를 생성해야 합니다.`EditableDocument` 지원되는 형식의 입력 문서를 로드하고 편집합니다.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
이 단계에서는 입력 문서를 로드하고 편집할 준비를 합니다.
## 2단계: 문서 리소스 추출
 그만큼`EditableDocument` 추출 및 조작이 가능한 다양한 리소스가 포함되어 있습니다. 다음을 분석해 보겠습니다.
### 2.1단계: 전체 문서를 HTML로 추출
모든 리소스가 HTML로 포함된 전체 문서를 포함하는 단일 문자열을 생성할 수 있습니다.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
이 문자열에는 base64로 인코딩된 스타일시트, 이미지 및 글꼴이 포함되어 있으므로 상당히 큽니다.
### 2.2단계: 모든 이미지 추출
문서에서 모든 이미지를 추출합니다.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### 2.3단계: 모든 글꼴 추출
문서에 사용된 모든 글꼴을 추출합니다.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### 2.4단계: 모든 스타일시트 추출
모든 스타일시트를 텍스트 형식으로 추출합니다.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### 2.5단계: 모든 자원 수집
한 번의 호출로 모든 리소스를 수집합니다.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
여기에는 이미지, 글꼴, 스타일시트가 포함됩니다.
### 2.6단계: HTML 마크업 얻기
포함된 리소스 없이 문서의 HTML 마크업을 가져옵니다.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## 3단계: 외부 링크 조정
경우에 따라 사용자 정의 리소스 핸들러를 가리키도록 외부 링크를 조정해야 합니다. 수행 방법은 다음과 같습니다.
### 3.1단계: 사용자 정의 접두사 준비
원본 외부 링크 앞에 추가될 접두사를 준비합니다.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### 3.2단계: 접두사가 붙은 HTML 마크업 생성
조정된 링크로 HTML 마크업을 생성합니다.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### 3.3단계: 본문 전용 HTML 콘텐츠 가져오기
일부 WYSIWYG 편집기는 헤더 없이 순수 HTML 마크업만 처리합니다.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### 3.4단계: 접두사가 붙은 본문 전용 콘텐츠
사용자 정의 이미지 접두사를 사용하여 본문 전용 콘텐츠를 생성합니다.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### 3.5단계: 스타일시트 추출
문서에 사용된 스타일시트를 추출합니다.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### 3.6단계: 접두사가 붙은 스타일시트
사용자 정의 접두어를 사용하여 스타일시트를 추출합니다.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## 4단계: 문서를 HTML로 저장
편집된 문서를 해당 리소스를 포함하여 HTML 파일로 저장합니다.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
이 방법은 스타일시트, 이미지, 글꼴과 같은 리소스를 위한 별도의 디렉토리를 생성합니다.
## 5단계: 편집 가능한 문서 폐기
 EditableDocument 구현`IDisposable` 인스턴스가 폐기되었는지 확인하는 기능을 제공합니다.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### 5.1단계 Dispose 이벤트 처리
폐기 이벤트를 구독할 수도 있습니다.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## 6단계: HTML에서 편집 가능한 문서 만들기
HTML 문서에서 EditableDocument 인스턴스를 만듭니다.
### 6.1단계: HTML 파일에서
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### 6.2단계: HTML 마크업에서
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
이러한 인스턴스(afterEditFromFile 및 afterEditFromMarkup)는 원본(beforeEdit)과 동일합니다.
## 7단계: 수동 폐기
EditableDocument 인스턴스를 수동으로 삭제하세요.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
이렇게 하면 리소스가 적절하게 정리됩니다.
## 결론
.NET용 GroupDocs.Editor는 프로그래밍 방식으로 문서를 편집하기 위한 강력한 도구를 제공합니다. 이 단계별 가이드를 따르면 문서 내용, 리소스 및 출력 형식을 효율적으로 관리할 수 있습니다. 리소스를 포함하든, 외부 링크를 조정하든, 문서를 HTML로 변환하든 GroupDocs.Editor는 고급 문서 조작에 필요한 기능을 제공합니다.
## FAQ
### GroupDocs.Editor는 어떤 형식을 지원합니까?
GroupDocs.Editor는 DOCX, XLSX, PPTX 등을 포함한 다양한 형식을 지원합니다.
### 라이센스 없이 GroupDocs.Editor를 사용할 수 있습니까?
 예, 다음과 함께 사용할 수 있습니다.[무료 시험판](https://releases.groupdocs.com/) 또는[임시면허](https://purchase.groupdocs.com/temporary-license/).
### 문서에서 특정 리소스를 어떻게 추출합니까?
 다음과 같이 제공된 방법을 사용하여 이미지, 글꼴 및 스타일시트를 추출할 수 있습니다.`Images`, `Fonts` , 그리고`Css`.
### HTML 출력에서 링크를 조정할 수 있습니까?
예, 이미지, CSS 및 글꼴에 대한 사용자 정의 접두사를 지정하여 외부 링크를 조정할 수 있습니다.
### 편집한 문서를 HTML 파일로 저장하려면 어떻게 해야 합니까?
 사용`Save` 의 방법`EditableDocument`리소스를 포함하여 문서를 HTML 파일로 저장하는 클래스입니다.