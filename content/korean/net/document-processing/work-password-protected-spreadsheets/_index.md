---
title: 비밀번호로 보호된 스프레드시트 작업
linktitle: 비밀번호로 보호된 스프레드시트 작업
second_title: GroupDocs.Editor .NET API
description: .NET용 GroupDocs.Editor를 사용하여 암호로 보호된 스프레드시트를 처리하는 방법을 알아보세요. 이 자세한 가이드는 안전한 Excel 파일을 열어서 저장하는 과정을 안내합니다.
weight: 18
url: /ko/net/document-processing/work-password-protected-spreadsheets/
type: docs
---
# 비밀번호로 보호된 스프레드시트 작업

## 소개
.NET 애플리케이션에서 비밀번호로 보호된 스프레드시트를 관리하는 데 어려움을 겪고 계십니까? 그렇다면, 당신은 바로 이곳에 있습니다! 이 종합 가이드에서는 .NET용 GroupDocs.Editor를 사용하여 암호로 보호된 스프레드시트를 효율적으로 처리하는 과정을 안내합니다. 이 튜토리얼을 마치면 암호화된 Excel 파일을 쉽게 열고, 편집하고, 저장할 수 있게 됩니다.
## 전제조건
코드를 살펴보기 전에 따라야 할 모든 것이 있는지 확인하십시오.
- C#에 대한 기본 지식: 이 자습서에서는 사용자가 C# 프로그래밍에 익숙하다고 가정합니다.
- .NET Framework: 개발 컴퓨터에 .NET Framework가 설치되어 있는지 확인하세요.
-  .NET용 GroupDocs.Editor: 다음에서 .NET용 GroupDocs.Editor를 다운로드하여 설치하세요.[여기](https://releases.groupdocs.com/editor/net/).
## 네임스페이스 가져오기
시작하려면 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 GroupDocs.Editor의 기능에 대한 액세스를 제공합니다.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1단계: 입력 파일의 경로 가져오기
먼저 입력 파일의 경로가 필요합니다. 이 예에서는 샘플 Excel 파일(`Your Sample Document`) 비밀번호로 보호되어 있습니다.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2단계: 비밀번호 없이 문서 열기 시도
비밀번호를 제공하지 않고 문서를 열려고 하면 어떻게 되는지 살펴보겠습니다.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## 3단계: 잘못된 비밀번호를 지정해 보세요
이제 편집자가 어떻게 반응하는지 보여주기 위해 잘못된 비밀번호를 지정하겠습니다.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## 4단계: 올바른 비밀번호로 파일 열기
올바른 비밀번호를 입력하고 파일을 성공적으로 열어 보겠습니다.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## 5단계: 편집 옵션 생성 및 조정
스프레드시트를 편집하려면 편집 옵션을 만들고 조정해야 합니다.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## 6단계: 중간 편집 가능한 문서 만들기
 다음으로 중간체를 생성합니다.`EditableDocument` 이를 통해 스프레드시트를 변경할 수 있습니다.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // 7단계: 저장 옵션 생성
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // 7.1단계: 새 개설 비밀번호 설정
    saveOptions.Password = "new password";
    // 7.2단계: 쓰기 방지 설정
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // 8단계: 수정하지 않고 문서 저장
    //8.1단계: 출력 파일 이름 및 경로 준비
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // 8.2단계: 출력 스트림 생성
    using (FileStream outputStream = File.Create(outputPath))
    {
        // 8.3단계: 저장
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// 9단계: Editor 인스턴스 삭제
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## 결론
축하해요! .NET용 GroupDocs.Editor를 사용하여 암호로 보호된 스프레드시트를 처리하는 방법을 성공적으로 배웠습니다. 비밀번호 없이 문서를 열려고 시도하는 것부터 새로운 보호 설정으로 문서를 저장하는 것까지 모든 필수 단계를 다루었습니다. 이러한 지식을 통해 .NET 응용 프로그램 내에서 보안 문서를 관리하는 능력이 확실히 향상될 것입니다.
## FAQ
### .NET용 GroupDocs.Editor란 무엇입니까?
.NET용 GroupDocs.Editor는 개발자가 .NET 응용 프로그램 내에서 다양한 문서 형식을 로드, 편집 및 저장할 수 있는 강력한 문서 편집 API입니다.
### GroupDocs.Editor의 임시 라이센스를 얻으려면 어떻게 해야 합니까?
 임시면허를 취득하실 수 있습니다.[여기](https://purchase.groupdocs.com/temporary-license/) 제품의 기능을 평가합니다.
### 대용량 문서를 편집하는 동안 메모리 사용량을 최적화할 수 있습니까?
 예, 다음을 설정하여 메모리 최적화를 활성화할 수 있습니다.`OptimizeMemoryUsage` 재산`true`로드 옵션에서.
### 스프레드시트를 열고 쓸 때 비밀번호를 다르게 설정할 수 있나요?
전적으로! 저장 옵션을 사용하여 문서 열기 및 쓰기 방지를 위한 별도의 비밀번호를 설정할 수 있습니다.
### 더 자세한 문서는 어디서 찾을 수 있나요?
 .NET용 GroupDocs.Editor에 대한 포괄적인 문서에 액세스할 수 있습니다.[여기](https://tutorials.groupdocs.com/editor/net/).