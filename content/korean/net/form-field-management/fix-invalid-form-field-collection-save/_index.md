---
title: 잘못된 양식 필드 수집 수정 및 저장
linktitle: 잘못된 양식 필드 수집 수정 및 저장
second_title: GroupDocs.Editor .NET API
description: .NET용 Groupdocs.Editor를 사용하여 DOCX의 잘못된 양식 필드를 수정하는 방법을 알아보세요. 문서에 오류가 없는지 확인하고 안전하게 저장하려면 이 가이드를 따르세요.
weight: 11
url: /ko/net/form-field-management/fix-invalid-form-field-collection-save/
---

# 잘못된 양식 필드 수집 수정 및 저장

## 소개
환영! 문서의 양식 필드로 작업 중이고 잘못된 양식 필드 컬렉션 문제에 직면한 경우 올바른 위치에 오셨습니다. 이 튜토리얼에서는 잘못된 양식 필드를 수정하고 .NET용 Groupdocs.Editor를 사용하여 문서를 저장하는 방법을 자세히 살펴보겠습니다. 프로세스를 단계별로 안내하여 원활하게 작동하는 데 필요한 모든 세부 정보를 제공합니다. 시작하자!
## 전제조건
코드를 시작하기 전에 준비해야 할 몇 가지 사항이 있습니다.
-  .NET용 Groupdocs.Editor: .NET용 Groupdocs.Editor 라이브러리를 설치했는지 확인하십시오. 당신은 그것을 다운로드 할 수 있습니다[여기](https://releases.groupdocs.com/editor/net/).
- 개발 환경: Visual Studio와 같은 .NET 개발 환경이 설정되어 있어야 합니다.
- C#에 대한 기본 지식: 이 자습서에서는 사용자가 C# 프로그래밍에 대한 기본 지식을 가지고 있다고 가정합니다.
## 네임스페이스 가져오기
먼저 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 코드 파일 시작 부분에 다음 줄을 추가합니다.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## 1단계: 입력 파일 경로 가져오기
첫 번째 단계는 입력 파일의 경로를 지정하는 것입니다. 이 파일은 양식 필드가 포함된 DOCX 문서여야 합니다.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## 2단계: 파일 경로에서 스트림 생성
다음으로, 입력 문서를 읽기 위한 파일 스트림을 만듭니다. 그러면 문서를 편집기에 로드할 수 있습니다.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 3단계: 문서에 대한 로드 옵션 만들기
이 단계에서는 문서에 대한 로드 옵션을 생성해야 합니다. 문서가 비밀번호로 보호되어 있는 경우 비밀번호를 지정할 수 있습니다. 이 예에서는 문서가 보호되지 않으므로 비밀번호가 무시됩니다.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## 4단계: 편집기 인스턴스에 문서 로드
이제 지정된 옵션이 포함된 문서를 Editor 인스턴스에 로드합니다. 여기에서 문서에 대한 주요 작업이 수행됩니다.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## 4.1단계: FormFieldManager 인스턴스 읽기
 그만큼`FormFieldManager` 인스턴스는 문서의 양식 필드를 관리하는 역할을 담당합니다. 양식 필드에 액세스하고 조작하려면 이 인스턴스를 읽어야 합니다.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## 4.2단계: FormFieldCollection 읽기
 그만큼`FormFieldCollection` 문서의 모든 양식 필드를 포함합니다. 잘못된 양식 필드를 확인하고 수정하려면 이 컬렉션을 읽으세요.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## 4.3단계: 잘못된 양식 필드 자동 수정
문서의 잘못된 양식 필드를 자동 수정해 보세요. 이는 명백한 문제를 해결하기 위한 예비 단계입니다.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## 4.4단계: 잘못된 양식 필드 확인
자동 수정 시도 후 유효하지 않은 양식 필드가 남아 있는지 확인하세요.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## 4.4.1단계: 잘못된 양식 필드 이름 모두 가져오기
유효하지 않은 모든 양식 필드의 이름을 검색합니다. 이 이름은 필드를 수정하는 데 사용됩니다.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## 4.4.2단계: 잘못된 필드에 대한 고유 이름 만들기
유효하지 않은 각 양식 필드에 대해 고유한 이름을 만듭니다. 이렇게 하면 기존 양식 필드 이름과 충돌이 발생하지 않습니다.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## 4.4.3단계: 잘못된 양식 필드 수정
이전 단계에서 생성한 고유 이름을 사용하여 잘못된 양식 필드를 수정하세요.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## 5단계: 문서 저장 옵션 생성
문서 저장 옵션을 설정합니다. 여기에는 형식 지정 및 추가 저장 설정이 포함됩니다.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## 5.1단계: 메모리 사용량 최적화
 문서가 커서 오류가 발생할 수 있는 경우`OutOfMemoryException`메모리 최적화 옵션을 활성화합니다.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## 5.2단계: 문서 쓰기 방지
양식 필드를 제외하고 문서가 수정되지 않도록 보호하려면 보호 비밀번호를 설정하세요.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## 6단계: 문서 저장
마지막으로 지정된 저장 옵션을 사용하여 문서를 저장합니다. 출력 문서를 저장하기 위한 메모리 스트림을 준비합니다.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## 결론
 그리고 거기에 있습니다! 잘못된 양식 필드를 성공적으로 수정하고 .NET용 Groupdocs.Editor를 사용하여 문서를 저장했습니다. 이 단계별 가이드는 프로세스를 명확하고 관리하기 쉽게 만들었습니다. 문제가 발생하거나 궁금한 점이 있으면 언제든지 확인하세요.[선적 서류 비치](https://tutorials.groupdocs.com/editor/net/) 아니면 연락해[지원하다](https://forum.groupdocs.com/c/editor/20).
## FAQ
### 내 문서가 비밀번호로 보호되어 있으면 어떻게 되나요?
 비밀번호는 다음에서 지정할 수 있습니다.`WordProcessingLoadOptions` 문서를 열려면
### 잘못된 양식 필드가 있는지 어떻게 알 수 있나요?
 사용`HasInvalidFormFields` 문서에 잘못된 양식 필드가 있는지 확인하는 방법입니다.
### 이름을 변경하지 않고 양식 필드를 수정할 수 있나요?
충돌을 방지하려면 잘못된 양식 필드에 대해 고유한 이름을 만드는 것이 좋습니다.
### 문서를 어떤 형식으로 저장할 수 있나요?
 적절한 설정을 통해 DOCX, PDF 등과 같은 다양한 형식으로 문서를 저장할 수 있습니다.`WordProcessingFormats`.
### 대용량 문서를 저장하는 동안 메모리 사용량을 최적화하려면 어떻게 해야 합니까?
 활성화`OptimizeMemoryUsage` 옵션`WordProcessingSaveOptions` 대용량 문서를 효율적으로 처리합니다.