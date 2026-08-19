---
date: 2026-05-12
description: GroupDocs.Editor for .NET을 사용하여 문서에서 폰트 및 기타 HTML 리소스를 추출하는 방법을 배웁니다.
  .NET 개발자를 위한 단계별 가이드.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML 리소스를 폴더에 저장
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: 폰트를 추출하고 HTML 리소스를 폴더에 저장하는 방법
type: docs
url: /ko/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# 폰트 추출 및 HTML 리소스를 폴더에 저장하는 방법

## 소개
GroupDocs.Editor for .NET를 사용하면 문서를 HTML로 변환하는 동안 **폰트 추출 방법** 및 기타 자산을 문서에서 추출할 수 있습니다. 몇 줄의 C# 코드로 이미지, 스타일시트 및 폰트 파일을 추출하여 원하는 폴더에 저장할 수 있습니다. 이 튜토리얼은 편집기 초기화부터 각 리소스를 디스크에 저장하는 전체 워크플로우를 단계별로 안내합니다.

## 빠른 답변
- **“폰트 추출 방법”이란 무엇입니까?** HTML 변환 중에 소스 문서에 포함된 폰트 파일을 가져오는 과정입니다.  
- **어떤 라이브러리가 이를 처리합니까?** GroupDocs.Editor for .NET는 폰트, 이미지 및 스타일시트를 추출하기 위한 전용 API를 제공합니다.  
- **라이선스가 필요합니까?** 무료 체험판을 사용할 수 있으며, 프로덕션 사용을 위해서는 상업용 라이선스가 필요합니다.  
- **지원되는 .NET 버전은 무엇입니까?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **사용자 지정 폴더를 지정할 수 있습니까?** 예, 추출된 리소스를 저장할 때 쓰기 가능한 경로를 지정하면 됩니다.

## “폰트 추출 방법”이란?
**폰트 추출 방법**은 원본 문서(DOCX, PPTX 등)에 포함된 원본 폰트 파일을 가져와 생성된 HTML에서 참조할 수 있도록 하는 것을 의미합니다. 이를 통해 시스템 폰트에 의존하지 않고 브라우저에서 텍스트가 의도한 대로 정확히 렌더링됩니다.

## HTML 리소스 추출에 GroupDocs.Editor를 사용하는 이유
GroupDocs.Editor는 **50개 이상의 입력 및 출력 형식**(DOCX, PPTX, PDF, HTML 등)을 지원하며 전체 파일을 메모리에 로드하지 않고도 **최대 300페이지** 문서를 처리할 수 있습니다. API는 한 번의 작업으로 폰트, 이미지 및 CSS를 추출하여 수동 파싱에 비해 개발 시간을 **최대 70 %**까지 단축합니다.

## 전제 조건
튜토리얼을 시작하기 전에 다음 전제 조건을 확인하십시오:
1. **C# 및 .NET에 대한 기본 지식** – C# 프로그래밍 언어와 .NET 프레임워크에 익숙해야 예제를 따라할 수 있습니다.  
2. **GroupDocs.Editor for .NET 라이브러리** – [website](https://releases.groupdocs.com/editor/net/)에서 GroupDocs.Editor for .NET 라이브러리를 다운로드하고 설치합니다.  
3. **개발 환경** – Visual Studio 등 선호하는 개발 환경이나 기타 호환 IDE를 설정합니다.

## 네임스페이스 가져오기
시작하려면 C# 프로젝트에 필요한 네임스페이스를 가져오세요:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## 폰트를 추출하고 HTML 리소스를 폴더에 저장하는 방법?
`Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` 로 소스 문서를 로드한 다음 `editor.Save("output.html", SaveOptions.Html);` 를 호출합니다. 저장 작업이 완료되면 `Resources` 컬렉션에 폰트를 포함한 모든 추출된 자산이 들어 있으며, 이를 반복하여 디스크에 기록할 수 있습니다. 이 단일 단계 접근 방식은 변환과 리소스 추출을 자동으로 처리합니다.

## 단계 1: GroupDocs.Editor 초기화
`Editor`는 문서 로드, 변환 및 리소스 추출을 조정하는 핵심 클래스이며 메모리 내에서 단일 문서 세션을 나타냅니다.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
먼저 샘플 문서 경로를 제공하여 `Editor` 객체를 초기화합니다. 이 예제에서는 Word 문서를 사용하므로 `WordProcessingLoadOptions`를 문서 유형으로 지정합니다.

## 단계 2: 문서 편집
`EditableDocument`는 `Edit` 메서드가 반환하는 편집 가능한 표현으로, 저장하기 전에 문서를 조작할 수 있게 해줍니다.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
다음으로 `Editor` 객체의 `Edit` 메서드를 호출하여 `EditableDocument` 객체를 생성합니다. 이를 통해 문서에 편집 작업을 수행할 수 있습니다.

## 단계 3: 리소스 추출
`Resources`는 추출된 자산(이미지, 폰트, 스타일시트)을 별도의 리스트로 그룹화하여 쉽게 처리할 수 있게 하는 컬렉션입니다.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
문서에서 이미지, 폰트 및 스타일시트와 같은 리소스를 추출하여 각각의 리스트에 저장합니다.

## 단계 4: 출력 폴더 지정
`outputFolder`는 추출된 파일이 기록될 위치를 정의하는 문자열이며, 서버나 로컬 머신의 쓰기 가능한 디렉터리를 지정할 수 있습니다.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
추출된 리소스를 저장할 출력 폴더를 정의합니다. 필요에 따라 폴더 경로를 맞춤 설정할 수 있습니다.

## 단계 5: 리소스 저장
`SaveResource`는 단일 바이너리 리소스(이미지, 폰트 또는 스타일시트)를 파일 시스템에 기록하는 헬퍼 루틴입니다.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
각 이미지 리소스를 반복하면서 출력 폴더에 저장하고 파일명, 유형, 차원과 같은 관련 정보를 표시합니다.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
마찬가지로 각 폰트 리소스를 출력 폴더에 저장합니다.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
마지막으로 각 스타일시트를 출력 폴더에 저장하고 편집 과정을 완료합니다.

## 일반적인 문제와 해결책
- **변환 후 폰트 누락** – 소스 문서에 실제로 폰트가 포함되어 있는지 확인하십시오. 그렇지 않으면 GroupDocs.Editor는 시스템 폰트만 참조할 수 있습니다.  
- **액세스 거부 오류** – 애플리케이션 프로세스가 대상 출력 폴더에 대한 쓰기 권한을 가지고 있는지 확인하십시오.  
- **대용량 문서로 메모리 사용량 증가** – `LoadOptions`에 `LoadMode = LoadMode.Stream`을 사용하여 파일을 전체 메모리에 로드하지 않고 스트리밍하십시오.

## 자주 묻는 질문

**Q: GroupDocs.Editor가 Word 외의 다른 문서 형식과 호환됩니까?**  
A: 예, Excel, PowerPoint, PDF, HTML 및 편집 및 리소스 추출을 위한 50가지 이상의 추가 형식을 지원합니다.

**Q: GroupDocs.Editor를 웹 애플리케이션에 통합할 수 있습니까?**  
A: 물론입니다. API는 ASP.NET Core, MVC 및 Web API 프로젝트와 원활하게 작동하여 서버 측에서 문서를 처리할 수 있습니다.

**Q: GroupDocs.Editor가 클라우드 스토리지 통합을 제공합니까?**  
A: 예, Google Drive, Dropbox, OneDrive 및 Amazon S3에 대한 내장 커넥터를 포함하여 클라우드에서 문서를 직접 로드하고 저장할 수 있습니다.

**Q: GroupDocs.Editor의 무료 체험판이 있습니까?**  
A: 신용카드 없이도 GroupDocs 웹사이트에서 30일 완전 기능 체험판을 다운로드할 수 있습니다.

**Q: 추출 문제에 대한 기술 지원은 어떻게 받을 수 있나요?**  
A: 공식 포럼을 통해 GroupDocs 지원팀에 연락하거나 고객 포털에서 티켓을 제출하거나 자세한 API 문서를 참고할 수 있습니다.

---

**마지막 업데이트:** 2026-05-12  
**테스트 환경:** GroupDocs.Editor 23.11 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Editor .NET&#58; HTML을 편집 가능한 문서로 변환](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [GroupDocs.Editor .NET를 사용한 DOCX 리소스 효율적 추출 및 저장 - 완전 가이드](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [GroupDocs.Editor .NET&#58; 문서 편집 및 변환 마스터하기 - 완전 가이드](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)