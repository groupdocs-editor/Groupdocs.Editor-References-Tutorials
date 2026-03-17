---
date: '2026-03-17'
description: GroupDocs.Editor를 사용하여 Java에서 PPTX를 편집하고 PPTX를 PPTM으로 변환하는 방법을 배웁니다.
  이 가이드는 프로그래밍 방식의 PowerPoint 편집, 텍스트 교체 및 PPTX 파일을 대량 변환하는 과정을 안내합니다.
keywords:
- GroupDocs.Editor for Java
- presentation editing in Java
- editing PPTX files with Java
title: Java와 GroupDocs를 사용하여 PPTX 편집 및 PPTM으로 변환하는 방법
type: docs
url: /ko/java/presentation-documents/groupdocs-editor-java-presentation-editing-guide/
weight: 1
---

# PPTX를 편집하고 Java에서 GroupDocs로 PPTM으로 변환하는 방법

오늘날 빠르게 변화하는 디지털 세계에서 많은 개발자들이 프로그래밍 방식으로 **how to edit pptx** 파일을 어떻게 편집할지 묻습니다. 텍스트를 교체하거나 매크로를 추가하거나 단순히 **convert PPTX to PPTM**을 원하든, 이 튜토리얼은 GroupDocs.Editor for Java를 사용하여 이러한 목표를 단계별로 달성하는 방법을 보여줍니다. 프레젠테이션을 로드하고, 변경하고, 매크로 사용이 가능한 PPTM으로 결과를 저장하는 방법을 확인할 수 있습니다—서버에 Microsoft Office가 설치되지 않아도 됩니다.

## 빠른 답변
- **What is the primary purpose of this guide?** GroupDocs.Editor for Java를 사용하여 PPTX 파일을 편집하고 PPTX를 PPTM으로 변환하는 방법을 보여주기 위함입니다.  
- **Do I need a license?** 예, 프로덕션 사용을 위해서는 GroupDocs의 체험판 또는 영구 라이선스가 필요합니다.  
- **Can I handle password‑protected files?** 물론입니다—로드 옵션에서 비밀번호를 지정할 수 있습니다.  
- **Which Java version is supported?** Java 8 이상 (JDK 11+ 권장).  
- **Is Maven the only way to add the library?** 아니요, JAR 파일을 직접 다운로드하여 사용할 수도 있습니다.

## “convert PPTX to PPTM”이란?
PPTX 파일을 PPTM으로 변환하면 표준 PowerPoint 프레젠테이션 형식에서 매크로 사용이 가능한 버전(PPTM)으로 파일 형식이 바뀝니다. VBA 매크로를 삽입하거나 PPTX에서 지원하지 않는 고급 기능을 유지해야 할 때 유용합니다.

## PPTX를 편집하기 위해 GroupDocs.Editor for Java를 사용하는 이유
GroupDocs.Editor는 Office Open XML 형식의 복잡성을 추상화한 고수준 API를 제공합니다. 이를 통해 다음을 수행할 수 있습니다:

- 한 번의 호출로 프레젠테이션을 로드(비밀번호 보호 파일 포함).  
- **Programmatic PowerPoint edit**: 슬라이드를 수정하고, 텍스트를 교체하며, 리소스를 조작.  
- 필요에 따라 새 비밀번호를 적용하여 결과를 PPTM으로 저장.  

이 모든 작업을 서버에 Microsoft Office를 설치하지 않고도 수행할 수 있습니다.

## 전제 조건
- **GroupDocs.Editor for Java** – 버전 25.3 이상.  
- **Java Development Kit (JDK)** – 8 이상.  
- IntelliJ IDEA 또는 Eclipse와 같은 IDE.  
- 유효한 GroupDocs 라이선스(무료 체험 또는 구매).  

체험 라이선스는 [GroupDocs 웹사이트](https://purchase.groupdocs.com/temporary-license)에서 얻을 수 있습니다.

## GroupDocs.Editor for Java 설정
프로젝트에 라이브러리를 Maven을 사용하거나 JAR 파일을 직접 다운로드하여 추가할 수 있습니다.

### Maven 사용
`pom.xml` 파일에 다음 구성을 포함하십시오:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### 직접 다운로드
또는 공식 릴리스 페이지에서 최신 JAR를 다운로드하십시오: [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

라이브러리를 클래스패스에 추가하면 `Editor` 인스턴스를 생성할 수 있습니다:

```java
import com.groupdocs.editor.Editor;
// Initialize GroupDocs.Editor (example setup)
Editor editor = new Editor();
```

## PPTX 편집 및 PPTM 변환 방법

### 기능 1: 프레젠테이션 로드 (비밀번호 보호 파일 포함)

#### 개요
프레젠테이션을 로드하는 것은 **convert PPTX to PPTM**하거나 내용을 편집하기 전에 수행해야 하는 첫 번째 단계입니다.

#### 단계별 구현

**1. Define the Path to Your File**  
작업할 PPTX 파일의 위치를 지정하십시오:

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample_pptx.pptx";
```

**2. Create an InputStream**  
파일을 스트림으로 엽니다:

```java
import java.io.FileInputStream;
import java.io.InputStream;

InputStream fs = new FileInputStream(inputFilePath);
```

**3. Set Up Load Options**  
파일이 보호되어 있는 경우 비밀번호를 제공합니다:

```java
import com.groupdocs.editor.options.PresentationLoadOptions;

PresentationLoadOptions loadOptions = new PresentationLoadOptions();
loadOptions.setPassword("some_password_to_open_a_document");
```

**4. Load the Presentation**  
스트림과 옵션을 사용하여 `Editor` 클래스로 로드합니다:

```java
Editor editor = new Editor(fs, loadOptions);
```

**Pro tip:** `InputStream`은 `finally` 블록에서 항상 닫거나 try‑with‑resources를 사용하여 리소스 누수를 방지하십시오.

### 기능 2: 특정 슬라이드 편집 (edit pptx java)

#### 개요
단일 슬라이드를 대상으로 수정합니다—**edit pptx java** 시나리오에 최적입니다.

#### 단계별 구현

**1. Set Up Editing Options**  
편집할 슬라이드를 선택합니다(0부터 시작하는 인덱스):

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.PresentationEditOptions;

PresentationEditOptions editOptions = new PresentationEditOptions();
editOptions.setSlideNumber(0); // Edit the first slide
editOptions.setShowHiddenSlides(true);
```

**2. Obtain an Editable Document**  
슬라이드의 편집 가능한 표현을 가져옵니다:

```java
import com.groupdocs.editor.EditableDocument;

EditableDocument beforeEdit = editor.edit(editOptions);
```

**3. Extract HTML Content and Resources**  
이제 슬라이드의 HTML 마크업과 포함된 리소스를 작업할 수 있습니다:

```java
String originalContent = beforeEdit.getContent();
List<IHtmlResource> allResources = beforeEdit.getAllResources();
```

### 기능 3: 프레젠테이션 슬라이드 내용 수정

#### 개요
텍스트를 교체하거나 새로운 HTML을 슬라이드 마크업에 직접 삽입합니다.

#### 단계별 구현

**1. Replace Text**  
간단한 텍스트 교체 예시:

```java
String editedContent = beforeEdit.getContent().replace("New text", "edited text");
```

**2. Create a New Editable Document**  
수정된 마크업을 `EditableDocument`에 다시 래핑합니다:

```java
EditableDocument afterEdit = EditableDocument.fromMarkup(editedContent, allResources);
```

### 기능 4: 편집된 프레젠테이션 저장 (convert PPTX to PPTM)

#### 개요
편집된 슬라이드 세트를 PPTM 파일로 저장하고, 필요하면 비밀번호로 보호합니다.

#### 단계별 구현

**1. Initialize Save Options**  
PPTM 형식과 새 비밀번호를 지정합니다:

```java
import com.groupdocs.editor.options.PresentationSaveOptions;
import com.groupdocs.editor.formats.PresentationFormats;

PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm);
saveOptions.setPassword("password");
```

**2. Prepare Output Stream**  
결과 파일이 기록될 위치를 정의합니다:

```java
import java.io.ByteArrayOutputStream;
import java.io.FileOutputStream;

String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_out.pptm";
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
```

**3. Save the Edited Document**  
업데이트된 프레젠테이션을 출력 스트림에 씁니다:

```java
editor.save(afterEdit, outputStream, saveOptions);
```

**4. Write to File**  
스트림을 디스크에 영구 저장합니다:

```java
try (FileOutputStream outputFile = new FileOutputStream(outputPath)) {
    outputStream.writeTo(outputFile);
}
```

**Tip:** 저장 후 PowerPoint에서 파일을 열어 매크로 사용이 가능한 형식이 정상적으로 작동하는지 확인할 수 있습니다.

## PPTX 슬라이드에서 텍스트 교체
위 스니펫(`replace text pptx`)은 슬라이드 HTML에서任意 문자열을 교체하는 간단한 방법을 보여줍니다. 여러 슬라이드에 걸쳐 플레이스홀더를 업데이트하는 등 복잡한 시나리오에서는 각 `EditableDocument`를 순회하면서 동일한 `replace` 로직을 적용하면 됩니다.

## PPTX 파일 대량 변환
**bulk convert pptx** 파일을 PPTM(또는 다른 형식)으로 변환해야 하는 경우, 로드‑편집‑저장 단계를 디렉터리의 PPTX 파일을 순회하는 루프에 감싸면 됩니다. 단일 `Editor` 인스턴스를 재사용하면 오버헤드가 감소하고 배치 처리 속도가 빨라집니다.

## 실용적인 적용 사례
GroupDocs.Editor Java API는 다음과 같은 실제 상황에서 빛을 발합니다:

- **Corporate training:** 새로운 정책으로 슬라이드 덱을 빠르게 업데이트.  
- **Marketing campaigns:** 인터랙티브 데모를 위한 매크로 사용 PPT 생성.  
- **Education:** 퀴즈용 VBA 매크로가 포함된 강의 슬라이드 자동 생성.  

## 성능 고려 사항
대용량 PPTX 파일을 처리할 때:

- `-Xmx2g` 이상으로 JVM 힙 크기를 늘려 `OutOfMemoryError`를 방지합니다.  
- 배치 처리 시 동일한 `Editor` 인스턴스를 재사용하여 오버헤드를 줄입니다.  
- 라이브러리를 최신 버전으로 유지하십시오; 최신 릴리스에는 성능 최적화가 포함되어 있습니다.

## 자주 묻는 질문

**Q: 슬라이드를 편집하지 않고 PPTX를 PPTM으로 변환할 수 있나요?**  
A: 예. `PresentationLoadOptions`로 PPTX를 로드한 뒤, PPTM 형식의 `PresentationSaveOptions`로 저장하면 중간 편집 단계 없이 변환이 가능합니다.

**Q: 라이브러리가 다른 PowerPoint 형식(PPT, PPSX 등)을 지원하나요?**  
A: GroupDocs.Editor는 PPT, PPTX, PPSX, PPTM 형식을 모두 로드하고 저장할 수 있습니다. 저장 시 적절한 `PresentationFormats` 열거형을 사용하십시오.

**Q: 비밀번호가 없는 프레젠테이션에 출력 파일에 비밀번호를 설정하려면 어떻게 해야 하나요?**  
A: 비밀번호는 `PresentationSaveOptions`에만 지정하면 됩니다; `PresentationLoadOptions`에 설정할 필요가 없습니다.

**Q: 한 번에 여러 슬라이드를 편집할 수 있나요?**  
A: 예. 슬라이드 번호를 순회하면서 각 `EditableDocument`를 가져와 변경을 적용하고, 저장 전에 결과를 결합하면 됩니다.

**Q: 기존 슬라이드를 편집하는 대신 새 슬라이드를 추가하려면 어떻게 해야 하나요?**  
A: 편집 옵션에서 `PresentationEditOptions.setSlideNumber(-1)`을 설정하여 슬라이드를 추가하고, 원하는 마크업을 삽입하면 됩니다.

**Q: 단일 서비스에서 pptx를 pptm으로 대량 변환하려면 어떻게 해야 하나요?**  
A: 소스 디렉터리를 순회하면서 각 PPTX를 동일한 `Editor` 인스턴스로 로드하고, `PresentationSaveOptions(PresentationFormats.Pptm)`으로 저장하십시오. 스트림은 즉시 닫아야 합니다.

## 결론
이 가이드를 따라 하면 GroupDocs.Editor for Java를 사용하여 **how to edit pptx** 파일과 **convert PPTX to PPTM** 방법을 알게 됩니다. 프레젠테이션을 로드하고, 개별 슬라이드를 수정하고, 텍스트를 교체하며, 매크로 사용이 가능한 PPTM 파일로 저장할 수 있습니다—모두 프로그래밍 방식으로 안전하게 수행됩니다.

**다음 단계:**  
- PPTM 파일에 VBA 매크로를 추가해 보세요.  
- 단일 Java 서비스에서 여러 프레젠테이션을 대량 변환하는 방법을 탐색하세요.  
- 이미지 처리 및 사용자 정의 스타일링과 같은 고급 기능을 위해 전체 GroupDocs.Editor 문서를 검토하세요.

---

**마지막 업데이트:** 2026-03-17  
**테스트 환경:** GroupDocs.Editor 25.3 for Java  
**작성자:** GroupDocs