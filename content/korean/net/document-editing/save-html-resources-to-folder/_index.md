---
title: HTML 리소스를 폴더에 저장
linktitle: HTML 리소스를 폴더에 저장
second_title: GroupDocs.Editor .NET API
description: .NET용 Groupdocs.Editor를 사용하여 문서에서 HTML 리소스를 추출하는 방법을 알아보세요. 이 포괄적인 튜토리얼은 개발자를 위한 단계별 지침을 제공합니다.
weight: 13
url: /ko/net/document-editing/save-html-resources-to-folder/
---

# HTML 리소스를 폴더에 저장

## 소개
.NET용 Groupdocs.Editor는 개발자가 .NET 응용 프로그램 내에서 문서를 원활하게 조작하고 변환할 수 있게 해주는 강력한 도구입니다. 문서에서 HTML 리소스를 추출해야 하거나 고급 편집 작업을 수행해야 하는 경우 Groupdocs.Editor는 직관적인 API와 광범위한 문서를 통해 프로세스를 단순화합니다.
## 전제조건
튜토리얼을 시작하기 전에 다음 전제조건이 충족되었는지 확인하십시오.
1. C# 및 .NET에 대한 기본 지식: 예제를 따라가려면 C# 프로그래밍 언어 및 .NET 프레임워크에 대한 지식이 필수적입니다.
2.  .NET 라이브러리용 Groupdocs.Editor: 다음에서 .NET 라이브러리용 Groupdocs.Editor를 다운로드하고 설치합니다.[웹사이트](https://releases.groupdocs.com/editor/net/).
3. 개발 환경: Visual Studio 또는 기타 호환 가능한 IDE와 같이 선호하는 개발 환경을 설정합니다.

## 네임스페이스 가져오기
시작하려면 C# 프로젝트에서 필요한 네임스페이스를 가져옵니다.
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##이제 .NET용 Groupdocs.Editor를 사용하여 HTML 리소스를 폴더에 저장하는 과정을 여러 단계로 나누어 보겠습니다.
## 1단계: Groupdocs.Editor 초기화
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 먼저, 초기화`Editor`샘플 문서의 경로를 제공하여 개체를 생성합니다. 이 예에서는 Word 문서를 사용하므로 다음을 지정합니다.`WordProcessingLoadOptions` 문서 유형으로.
## 2단계: 문서 편집
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 다음으로`EditableDocument` 호출하여 객체를 생성합니다.`Edit` 의 방법`Editor` 물체. 이를 통해 문서에 대한 편집 작업을 수행할 수 있습니다.
## 3단계: 리소스 추출
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
문서에서 이미지, 글꼴, 스타일시트 등의 리소스를 추출하여 해당 목록에 저장합니다.
## 4단계: 출력 폴더 지정
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
추출된 리소스가 저장될 출력 폴더를 정의합니다. 요구 사항에 따라 폴더 경로를 사용자 정의할 수 있습니다.
## 5단계: 리소스 저장
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
각 이미지 리소스를 반복하여 출력 폴더에 저장하고 파일 이름, 유형, 크기 등 관련 정보를 표시합니다.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
마찬가지로 각 글꼴 리소스를 출력 폴더에 저장합니다.
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
마지막으로 각 스타일시트를 출력 폴더에 저장하고 편집 프로세스를 완료합니다.

## 결론
결론적으로, .NET용 Groupdocs.Editor는 .NET 응용 프로그램 내에서 프로그래밍 방식으로 문서를 관리하고 조작하기 위한 편리한 솔루션을 제공합니다. 이 튜토리얼을 따르면 문서에서 HTML 리소스를 쉽게 추출하고 특정 요구 사항에 따라 프로세스를 사용자 정의할 수 있습니다.
## FAQ
### Groupdocs.Editor는 Word 이외의 다른 문서 형식과 호환됩니까?
예, Groupdocs.Editor는 Excel, PowerPoint, PDF 등을 포함한 광범위한 문서 형식을 지원합니다.
### Groupdocs.Editor를 내 웹 응용 프로그램에 통합할 수 있나요?
물론, Groupdocs.Editor는 .NET 프레임워크에서 개발된 웹 응용 프로그램과의 원활한 통합을 제공합니다.
### Groupdocs.Editor는 클라우드 저장소 서비스를 지원합니까?
예, Groupdocs.Editor는 Google Drive, Dropbox 및 Microsoft OneDrive와 같은 널리 사용되는 클라우드 저장소 서비스와의 통합을 지원합니다.
### Groupdocs.Editor에 대한 무료 평가판이 있습니까?
예, 웹사이트에서 Groupdocs.Editor 무료 평가판을 이용할 수 있습니다.
### Groupdocs.Editor에 대한 기술 지원을 받으려면 어떻게 해야 합니까?
기술 지원 및 커뮤니티 지원을 받으려면 Groupdocs.Editor 포럼을 방문하세요.