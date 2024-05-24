---
title: 문서 로드
linktitle: 문서 로드
second_title: GroupDocs.Editor .NET API
description: .NET용 GroupDocs.Editor를 사용하여 프로그래밍 방식으로 문서를 편집하는 방법을 알아보세요. 문서 로딩, 비밀번호로 보호된 파일 처리 등에 대한 단계별 가이드입니다.
type: docs
weight: 13
url: /ko/net/document-editing/load-document/
---
## 소개
프로그래밍 방식으로 문서를 편집하는 것은 어려운 작업이 될 수 있습니다. 특히 다양한 파일 형식과 복잡한 구조를 다루는 경우 더욱 그렇습니다. 다행스럽게도 .NET용 GroupDocs.Editor는 다양한 문서 유형을 편집할 수 있는 강력하고 사용하기 쉬운 API를 제공하여 이 작업을 쉽게 수행합니다. 이 튜토리얼에서는 전제 조건, 네임스페이스를 가져오는 방법, 다양한 방법을 사용하여 문서를 로드하는 자세한 단계별 가이드를 포함하여 .NET용 GroupDocs.Editor를 시작하는 데 필요한 모든 것을 안내합니다.
## 전제조건
시작하기 전에 다음과 같은 전제 조건이 설정되어 있는지 확인하세요.
- Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요.
- .NET Framework: .NET용 GroupDocs.Editor는 .NET Framework 2.0 이상을 지원합니다. 프로젝트가 호환 가능한 프레임워크를 대상으로 하는지 확인하세요.
-  .NET용 GroupDocs.Editor: 다음에서 최신 버전을 다운로드하세요.[다운로드 페이지](https://releases.groupdocs.com/editor/net/).
- C#에 대한 기본 지식: 이 튜토리얼을 진행하려면 C# 및 .NET 프로그래밍에 대한 지식이 필요합니다.
## 네임스페이스 가져오기
.NET용 GroupDocs.Editor 사용을 시작하려면 필요한 네임스페이스를 프로젝트로 가져와야 합니다. C# 파일 상단에 다음 using 지시문을 추가합니다.
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
이러한 네임스페이스는 문서 편집 작업에 필요한 클래스 및 메서드에 대한 액세스를 제공합니다.
## 1단계: 파일 경로에서 문서 로드
파일 경로에서 문서를 로드하는 것은 간단합니다. 이 방법은 컴퓨터에 로컬로 저장된 문서에 이상적입니다.

```csharp
string inputPath = "Your Sample Document";
// 로드 옵션 없이 경로를 통해 문서를 파일로 로드
Editor editor1 = new Editor(inputPath);
// 자원 폐기
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## 2단계: 로드 옵션을 사용하여 문서 로드
때로는 비밀번호로 보호된 파일과 같이 특별한 처리가 필요한 문서를 로드해야 할 수도 있습니다. 이러한 경우 로드 옵션을 사용할 수 있습니다.

```csharp
string inputPath = "Your Sample Document";
//Word 문서에 대한 로드 옵션 만들기
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// 경로 및 로드 옵션을 통해 문서를 파일로 로드
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// 자원 폐기
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## 3단계: 바이트 스트림에서 문서 로드
바이트 스트림에서 문서를 로드하는 것은 데이터베이스나 웹 서비스에서 검색된 문서와 같이 파일로 저장되지 않은 문서를 처리해야 할 때 유용합니다.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// 로드 옵션 없이 바이트 스트림의 콘텐츠로 문서 로드
Editor editor3 = new Editor(delegate { return inputStream; });
// 자원 폐기
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## 4단계: 바이트 스트림에서 로드 옵션을 사용하여 문서 로드
바이트 스트림에서 로드할 때 특별한 처리가 필요한 문서의 경우 바이트 스트림 로드를 로드 옵션과 결합할 수 있습니다.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// 스프레드시트에 대한 로드 옵션 만들기
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// 로드 옵션을 사용하여 바이트 스트림의 콘텐츠로 문서 로드
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// 자원 폐기
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## 결론
축하해요! .NET용 GroupDocs.Editor를 사용하여 다양한 방법으로 문서를 로드하는 방법을 성공적으로 배웠습니다. 로컬 파일, 암호로 보호된 문서 또는 바이트 스트림을 처리하는 경우 GroupDocs.Editor는 문서 편집 요구 사항에 맞는 유연하고 강력한 솔루션을 제공합니다. 애플리케이션에서 최적의 성능과 리소스 관리를 보장하려면 항상 리소스를 폐기해야 합니다.
## FAQ
### .NET용 GroupDocs.Editor는 어떤 파일 형식을 지원합니까?
 GroupDocs.Editor는 DOCX, XLSX, PPTX, HTML 등을 포함한 광범위한 파일 형식을 지원합니다. 전체 목록은 다음을 참조하세요.[선적 서류 비치](https://reference.groupdocs.com/editor/net/).
### 비밀번호로 보호된 문서는 어떻게 처리하나요?
 다음과 같은 로드 옵션을 사용할 수 있습니다.`WordProcessingLoadOptions` 비밀번호로 보호된 문서를 로드할 때 비밀번호를 지정합니다.
### 웹 응용 프로그램에서 GroupDocs.Editor를 사용할 수 있습니까?
예, GroupDocs.Editor는 웹 응용 프로그램에서 사용할 수 있습니다. 메모리 누수를 방지하려면 파일 스트림과 리소스 처리를 올바르게 처리해야 합니다.
### GroupDocs.Editor의 임시 라이센스는 어디서 구할 수 있나요?
 임시면허를 취득할 수 있습니다.[임시 라이센스 페이지](https://purchase.groupdocs.com/temporary-license/).
### 문제가 발생하면 지원을 받을 수 있나요?
 예, GroupDocs는 다음을 통해 지원을 제공합니다.[지원 포럼](https://forum.groupdocs.com/c/editor/20).