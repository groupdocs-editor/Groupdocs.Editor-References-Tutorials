---
date: '2026-01-13'
description: GroupDocs.Editor를 사용하여 Java에서 PPTX를 PPTM으로 변환하는 방법을 배웁니다. 이 가이드는 PPTX
  Java 프로젝트를 효율적으로 편집하는 방법도 보여줍니다.
keywords:
- GroupDocs.Editor for Java
- presentation editing in Java
- editing PPTX files with Java
title: GroupDocs.Editor를 사용한 Java에서 PPTX를 PPTM으로 변환
type: docs
url: /ko/java/presentation-documents/groupdocs-editor-java-presentation-editing-guide/
weight: 1
---

# Java와 GroupDocs.Editor를 사용한 PPTX를 PPTM으로 변환

## 소개

오늘날 빠르게 변화하는 디지털 환경에서 **PPTX를 PPTM으로 변환**하는 능력은 큰 생산성 향상을 가져다 줍니다. 특히 **Java에서 PPTX 편집**이 필요할 때 더욱 유용합니다. 클라이언트 프레젠테이션용 슬라이드 덱을 업데이트하거나 비밀번호로 보호된 파일을 처리하든, GroupDocs.Editor for Java는 프레젠테이션을 로드하고, 편집하고, 저장할 수 있는 깔끔하고 프로그래밍 가능한 방법을 제공합니다. 이 튜토리얼은 PPTX 파일을 로드하는 단계부터 PPTM 형식으로 변환하는 단계까지 모든 과정을 안내하므로, 프레젠테이션 편집 기능을 Java 애플리케이션에 직접 통합할 수 있습니다.

### 빠른 답변
- **이 가이드의 주요 목적은 무엇인가요?** PPTX를 PPTM으로 변환하고 GroupDocs.Editor for Java를 사용해 프레젠테이션을 편집하는 방법을 보여줍니다.  
- **라이선스가 필요하나요?** 예, 프로덕션 사용을 위해서는 GroupDocs의 체험판 또는 정식 라이선스가 필요합니다.  
- **비밀번호 보호 파일을 처리할 수 있나요?** 물론입니다—로드 옵션에서 비밀번호를 지정하면 됩니다.  
- **지원되는 Java 버전은 무엇인가요?** Java 8 이상 (JDK 11+ 권장).  
- **라이브러리를 추가하는 방법이 Maven뿐인가요?** 아니요, JAR 파일을 직접 다운로드해서 사용할 수도 있습니다.

## “convert PPTX to PPTM”이란?

PPTX 파일을 PPTM으로 변환하면 표준 PowerPoint 프레젠테이션 형식에서 매크로가 포함된 버전(PPTM)으로 파일 형식이 바뀝니다. VBA 매크로를 삽입하거나 PPTX에서 지원하지 않는 고급 기능을 유지해야 할 때 유용합니다.

## Java에서 PPTX를 편집하기 위해 GroupDocs.Editor를 사용하는 이유

GroupDocs.Editor는 Office Open XML 형식의 복잡성을 추상화한 고수준 API를 제공합니다. 이를 통해 다음을 할 수 있습니다:

- 한 번의 호출로 프레젠테이션을 로드(비밀번호 보호 파일 포함).  
- 개별 슬라이드를 편집하고, 텍스트를 교체하며, 리소스를 조작.  
- 필요에 따라 새 비밀번호를 적용해 결과를 PPTM으로 저장.  

이 모든 작업을 서버에 Microsoft Office를 설치하지 않고도 수행할 수 있습니다.

## 사전 요구 사항

- **GroupDocs.Editor for Java** – 버전 25.3 이상.  
- **Java Development Kit (JDK)** – 8 이상.  
- IntelliJ IDEA 또는 Eclipse와 같은 IDE.  
- 유효한 GroupDocs 라이선스(무료 체험 또는 구매).  

시험 라이선스는 [GroupDocs 웹사이트](https://purchase.groupdocs.com/temporary-license)에서 받을 수 있습니다.

## GroupDocs.Editor for Java 설정

Maven을 사용하거나 JAR 파일을 직접 다운로드하여 라이브러리를 프로젝트에 추가할 수 있습니다.

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

## 구현 가이드

### 기능 1: 프레젠테이션 로드 (비밀번호 보호 파일 포함)

#### 개요
프레젠테이션을 로드하는 것은 **PPTX를 PPTM으로 변환**하거나 내용을 편집하기 전에 수행해야 하는 첫 번째 단계입니다.

#### 단계별 구현

**1. 파일 경로 정의**  
작업할 PPTX 파일의 위치를 지정합니다:

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample_pptx.pptx";
```

**2. InputStream 생성**  
파일을 스트림으로 엽니다:

```java
import java.io.FileInputStream;
import java.io.InputStream;

InputStream fs = new FileInputStream(inputFilePath);
```

**3. 로드 옵션 설정**  
파일이 보호된 경우 비밀번호를 제공합니다:

```java
import com.groupdocs.editor.options.PresentationLoadOptions;

PresentationLoadOptions loadOptions = new PresentationLoadOptions();
loadOptions.setPassword("some_password_to_open_a_document");
```

**4. 프레젠테이션 로드**  
스트림과 옵션을 사용해 `Editor` 클래스를 호출합니다:

```java
Editor editor = new Editor(fs, loadOptions);
```

**팁:** `InputStream`은 `finally` 블록에서 닫거나 try‑with‑resources를 사용해 리소스 누수를 방지하십시오.

### 기능 2: 특정 슬라이드 편집 (edit pptx java)

#### 개요
단일 슬라이드를 대상으로 수정합니다—**edit pptx java** 시나리오에 적합합니다.

#### 단계별 구현

**1. 편집 옵션 설정**  
편집할 슬라이드 번호(0부터 시작)를 선택합니다:

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.PresentationEditOptions;

PresentationEditOptions editOptions = new PresentationEditOptions();
editOptions.setSlideNumber(0); // Edit the first slide
editOptions.setShowHiddenSlides(true);
```

**2. 편집 가능한 문서 가져오기**  
슬라이드의 편집 가능한 표현을 가져옵니다:

```java
import com.groupdocs.editor.EditableDocument;

EditableDocument beforeEdit = editor.edit(editOptions);
```

**3. HTML 콘텐츠 및 리소스 추출**  
이제 슬라이드의 HTML 마크업과 포함된 리소스를 활용할 수 있습니다:

```java
String originalContent = beforeEdit.getContent();
List<IHtmlResource> allResources = beforeEdit.getAllResources();
```

### 기능 3: 프레젠테이션 슬라이드 내용 수정

#### 개요
텍스트를 교체하거나 새로운 HTML을 직접 슬라이드 마크업에 삽입합니다.

#### 단계별 구현

**1. 텍스트 교체**  
간단한 텍스트 치환 예시:

```java
String editedContent = beforeEdit.getContent().replace("New text", "edited text");
```

**2. 새로운 편집 문서 생성**  
수정된 마크업을 `EditableDocument`에 다시 래핑합니다:

```java
EditableDocument afterEdit = EditableDocument.fromMarkup(editedContent, allResources);
```

### 기능 4: 편집된 프레젠테이션 저장 (convert PPTX to PPTM)

#### 개요
편집된 슬라이드 세트를 PPTM 파일로 저장하고, 필요하면 비밀번호를 설정합니다.

#### 단계별 구현

**1. 저장 옵션 초기화**  
PPTM 형식과 새 비밀번호를 지정합니다:

```java
import com.groupdocs.editor.options.PresentationSaveOptions;
import com.groupdocs.editor.formats.PresentationFormats;

PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm);
saveOptions.setPassword("password");
```

**2. 출력 스트림 준비**  
결과 파일이 기록될 위치를 정의합니다:

```java
import java.io.ByteArrayOutputStream;
import java.io.FileOutputStream;

String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_out.pptm";
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
```

**3. 편집된 문서 저장**  
업데이트된 프레젠테이션을 출력 스트림에 씁니다:

```java
editor.save(afterEdit, outputStream, saveOptions);
```

**4. 파일에 기록**  
스트림을 디스크에 영구 저장합니다:

```java
try (FileOutputStream outputFile = new FileOutputStream(outputPath)) {
    outputStream.writeTo(outputFile);
}
```

**팁:** 저장 후 PowerPoint에서 파일을 열어 매크로가 포함된 형식이 정상적으로 동작하는지 확인할 수 있습니다.

## 실용적인 적용 사례

GroupDocs.Editor Java API는 다음과 같은 실제 시나리오에서 빛을 발합니다:

- **기업 교육:** 새로운 정책을 반영해 슬라이드 덱을 빠르게 업데이트.  
- **마케팅 캠페인:** 인터랙티브 데모용 매크로 포함 프레젠테이션을 자동 생성.  
- **교육 현장:** 퀴즈용 VBA 매크로가 포함된 강의 슬라이드를 자동으로 제작.

## 성능 고려 사항

대용량 PPTX 파일을 처리할 때:

- JVM 힙 크기를 늘리세요(`-Xmx2g` 이상) to avoid `OutOfMemoryError`.  
- 배치 처리 시 동일한 `Editor` 인스턴스를 재사용해 오버헤드를 감소.  
- 라이브러리를 최신 버전으로 유지하면 성능 최적화가 포함됩니다.

## 자주 묻는 질문

**Q: 슬라이드를 편집하지 않고 PPTX를 PPTM으로 변환할 수 있나요?**  
A: 가능합니다. `PresentationLoadOptions`로 PPTX를 로드한 뒤, PPTM 형식의 `PresentationSaveOptions`로 저장하면 중간 편집 단계가 필요 없습니다.

**Q: 라이브러리가 다른 PowerPoint 형식(PPT, PPSX 등)을 지원하나요?**  
A: GroupDocs.Editor는 PPT, PPTX, PPSX, PPTM 형식을 모두 로드하고 저장할 수 있습니다. 저장 시 적절한 `PresentationFormats` 열거형을 사용하십시오.

**Q: 비밀번호가 없는 프레젠테이션에 출력 파일에만 비밀번호를 설정하고 싶다면?**  
A: `PresentationSaveOptions`에 원하는 비밀번호만 지정하면 됩니다. `PresentationLoadOptions`에 비밀번호를 설정할 필요가 없습니다.

**Q: 한 번에 여러 슬라이드를 편집할 수 있나요?**  
A: 가능합니다. 슬라이드 번호를 순회하면서 각 `EditableDocument`를 가져와 변경하고, 저장 전에 결과를 결합하면 됩니다.

**Q: 기존 슬라이드를 편집하는 대신 새 슬라이드를 추가하려면 어떻게 해야 하나요?**  
A: 편집 API에서 `PresentationEditOptions.setSlideNumber(-1)`을 사용해 새 슬라이드를 추가한 뒤 원하는 마크업을 삽입하면 됩니다.

## 결론

이 가이드를 따라 **PPTX를 PPTM으로 변환**하고 **Java에서 PPTX 편집**을 수행하는 방법을 익혔습니다. 이제 프레젠테이션을 로드하고, 개별 슬라이드를 수정하며, 텍스트를 교체하고, 매크로가 포함된 PPTM 파일로 저장할 수 있습니다—모두 프로그래밍 방식으로 안전하게 처리됩니다.

**다음 단계:**  
- PPTM 파일에 VBA 매크로를 추가해 보세요.  
- 단일 Java 서비스에서 여러 프레젠테이션을 일괄 변환하는 방식을 탐색하세요.  
- 이미지 처리 및 사용자 정의 스타일링 등 고급 기능은 전체 GroupDocs.Editor 문서를 참고하십시오.

---

**마지막 업데이트:** 2026-01-13  
**테스트 환경:** GroupDocs.Editor 25.3 for Java  
**작성자:** GroupDocs