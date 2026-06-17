---
date: '2026-03-17'
description: GroupDocs.Editor を使用して Java で PPTX を編集し、PPTX を PPTM に変換する方法を学びましょう。このガイドでは、プログラムによる
  PowerPoint の編集、テキストの置換、そして PPTX ファイルの一括変換について解説します。
keywords:
- GroupDocs.Editor for Java
- presentation editing in Java
- editing PPTX files with Java
title: How to Edit PPTX and Convert to PPTM in Java with GroupDocs
type: docs
url: /ja/java/presentation-documents/groupdocs-editor-java-presentation-editing-guide/
weight: 1
---

# Java と GroupDocs で PPTX を編集し PPTM に変換する方法

今日のスピーディなデジタル社会では、多くの開発者がプログラムで **pptx を編集する方法** を尋ねています。テキストの置換、マクロの追加、あるいは単に **PPTX を PPTM に変換**したい場合でも、このチュートリアルでは GroupDocs.Editor for Java を使用してそれらの目標をステップバイステップで達成する方法を示します。プレゼンテーションの読み込み、変更、そしてマクロ対応の PPTM として結果を保存する方法が分かります—サーバーに Microsoft Office をインストールする必要はありません。

## クイック回答
- **このガイドの主な目的は何ですか？** GroupDocs.Editor for Java を使用して PPTX ファイルを編集し、PPTX を PPTM に変換する方法を示すことです。  
- **ライセンスは必要ですか？** はい、実運用には GroupDocs のトライアルまたは永続ライセンスが必要です。  
- **パスワード保護されたファイルを扱えますか？** もちろんです。ロードオプションでパスワードを指定できます。  
- **サポートされている Java バージョンは？** Java 8 以上（JDK 11+ 推奨）。  
- **ライブラリの追加は Maven のみですか？** いいえ、JAR を直接ダウンロードすることもできます。

## “convert PPTX to PPTM” とは？

PPTX ファイルを PPTM に変換すると、標準的な PowerPoint プレゼンテーション形式からマクロ対応バージョン（PPTM）へと形式が変わります。VBA マクロを埋め込む必要がある場合や、PPTX がサポートしていない高度な機能を保持したい場合に便利です。

## なぜ GroupDocs.Editor for Java を使って PPTX を編集するのか？

GroupDocs.Editor は、Office Open XML 形式の複雑さを抽象化したハイレベル API を提供します。これにより、次のことが可能になります：

- 単一の呼び出しでプレゼンテーションをロード（パスワード保護されたものも含む）。  
- **プログラムによる PowerPoint 編集**：スライドの変更、テキストの置換、リソースの操作。  
- 必要に応じて新しいパスワードを設定し、結果を PPTM として保存。  

これらすべては、サーバーに Microsoft Office をインストールせずに実行できます。

## 前提条件

- **GroupDocs.Editor for Java** – バージョン 25.3 以上。  
- **Java Development Kit (JDK)** – 8 以上。  
- IntelliJ IDEA や Eclipse などの IDE。  
- 有効な GroupDocs ライセンス（無料トライアルまたは購入版）。  

トライアルライセンスは [GroupDocs website](https://purchase.groupdocs.com/temporary-license) から取得できます。

## GroupDocs.Editor for Java の設定

ライブラリは Maven を使用するか、JAR を直接ダウンロードしてプロジェクトに追加できます。

### Maven を使用する
`pom.xml` ファイルに以下の設定を追加してください:

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

### 直接ダウンロード
あるいは、公式リリースページから最新の JAR をダウンロードしてください: [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/)。

ライブラリがクラスパスに追加されたら、`Editor` インスタンスを作成できます:

```java
import com.groupdocs.editor.Editor;
// Initialize GroupDocs.Editor (example setup)
Editor editor = new Editor();
```

## PPTX を編集し（PPTM に変換する）方法

### 機能 1: プレゼンテーションのロード（パスワード保護されたファイルを含む）

#### 概要
プレゼンテーションをロードすることは、**PPTX を PPTM に変換**したり内容を編集したりする前の最初のステップです。

#### 手順実装

**1. ファイルへのパスを定義**  
操作したい PPTX の場所を設定します:

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample_pptx.pptx";
```

**2. InputStream を作成**  
ファイルをストリームとして開きます:

```java
import java.io.FileInputStream;
import java.io.InputStream;

InputStream fs = new FileInputStream(inputFilePath);
```

**3. ロードオプションを設定**  
ファイルが保護されている場合は、パスワードを指定します:

```java
import com.groupdocs.editor.options.PresentationLoadOptions;

PresentationLoadOptions loadOptions = new PresentationLoadOptions();
loadOptions.setPassword("some_password_to_open_a_document");
```

**4. プレゼンテーションをロード**  
`Editor` クラスにストリームとオプションを渡して使用します:

```java
Editor editor = new Editor(fs, loadOptions);
```

プロのコツ: `InputStream` は必ず `finally` ブロックで閉じるか、try‑with‑resources を使用してリソースリークを防止してください。

### 機能 2: 特定スライドの編集（edit pptx java）

#### 概要
単一のスライドを対象に変更を加えることで、**edit pptx java** のシナリオに最適です。

#### 手順実装

**1. 編集オプションを設定**  
編集するスライドを選択します（0 から始まるインデックス）:

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.PresentationEditOptions;

PresentationEditOptions editOptions = new PresentationEditOptions();
editOptions.setSlideNumber(0); // Edit the first slide
editOptions.setShowHiddenSlides(true);
```

**2. EditableDocument を取得**  
スライドの編集可能な表現を取得します:

```java
import com.groupdocs.editor.EditableDocument;

EditableDocument beforeEdit = editor.edit(editOptions);
```

**3. HTML コンテンツとリソースを抽出**  
スライドの HTML マークアップと埋め込みリソースを操作できます:

```java
String originalContent = beforeEdit.getContent();
List<IHtmlResource> allResources = beforeEdit.getAllResources();
```

### 機能 3: プレゼンテーションスライドの内容変更

#### 概要
テキストを置換したり、スライドのマークアップに新しい HTML を直接挿入したりします。

#### 手順実装

**1. テキスト置換**  
シンプルな文字列置換の場合:

```java
String editedContent = beforeEdit.getContent().replace("New text", "edited text");
```

**2. 新しい EditableDocument を作成**  
変更したマークアップを `EditableDocument` に再度ラップします:

```java
EditableDocument afterEdit = EditableDocument.fromMarkup(editedContent, allResources);
```

### 機能 4: 編集済みプレゼンテーションの保存（convert PPTX to PPTM）

#### 概要
最後に、編集したスライドセットを PPTM ファイルとして保存します。必要に応じてパスワードで保護することもできます。

#### 手順実装

**1. 保存オプションを初期化**  
PPTM 形式と新しいパスワードを指定します:

```java
import com.groupdocs.editor.options.PresentationSaveOptions;
import com.groupdocs.editor.formats.PresentationFormats;

PresentationSaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptm);
saveOptions.setPassword("password");
```

**2. 出力ストリームを準備**  
結果ファイルの書き込み先を定義します:

```java
import java.io.ByteArrayOutputStream;
import java.io.FileOutputStream;

String outputPath = "YOUR_OUTPUT_DIRECTORY/sample_out.pptm";
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
```

**3. 編集済みドキュメントを保存**  
更新されたプレゼンテーションを出力ストリームに書き込みます:

```java
editor.save(afterEdit, outputStream, saveOptions);
```

**4. ファイルに書き込む**  
ストリームをディスクに永続化します:

```java
try (FileOutputStream outputFile = new FileOutputStream(outputPath)) {
    outputStream.writeTo(outputFile);
}
```

**ヒント:** 保存後、PowerPoint でファイルを開いてマクロ対応形式が期待通りに機能するか確認できます。

## PPTX スライドのテキスト置換

上記のスニペット（`replace text pptx`）は、スライドの HTML 内の任意の文字列を置換する簡単な方法を示しています。複数スライドにわたってプレースホルダーを更新するようなより複雑なシナリオでは、各 `EditableDocument` をループし、同じ `replace` ロジックを適用できます。

## PPTX ファイルの一括変換

**pptx を一括変換**して PPTM（または他の形式）に変換する必要がある場合、ロード・編集・保存の手順を PPTX ファイルが格納されたディレクトリを走査するループで包みます。単一の `Editor` インスタンスを再利用することでオーバーヘッドが減り、バッチ処理が高速化されます。

## 実用的な活用例

GroupDocs.Editor Java API は、実際のシナリオで次のように活躍します:

- **企業研修:** 新しいポリシーでスライドデッキを迅速に更新。  
- **マーケティングキャンペーン:** インタラクティブデモ用にマクロ対応プレゼンテーションを生成。  
- **教育:** クイズ用 VBA マクロを含む講義スライドの作成を自動化。  

## パフォーマンス考慮点

大きな PPTX ファイルを扱う際は以下に注意してください:

- JVM ヒープサイズを増やす（例: `-Xmx2g` 以上）ことで `OutOfMemoryError` を回避。  
- バッチ処理では同じ `Editor` インスタンスを再利用してオーバーヘッドを削減。  
- ライブラリは常に最新に保ちましょう。新しいリリースにはパフォーマンス最適化が含まれています。  

## よくある質問

**Q: スライドを編集せずに PPTX を PPTM に変換できますか？**  
A: はい。`PresentationLoadOptions` で PPTX をロードし、`PresentationSaveOptions` で PPTM 形式で保存すれば、途中の編集ステップは不要です。

**Q: ライブラリは他の PowerPoint 形式（PPT、PPSX など）をサポートしていますか？**  
A: GroupDocs.Editor は PPT、PPTX、PPSX、PPTM 形式のロードと保存が可能です。保存時には適切な `PresentationFormats` 列挙型を使用してください。

**Q: パスワードが設定されていないプレゼンテーションに、出力時にパスワードを付与したい場合はどうすればよいですか？**  
A: `PresentationSaveOptions` にのみ希望のパスワードを指定すればよく、`PresentationLoadOptions` で設定する必要はありません。

**Q: 一度の操作で複数のスライドを編集できますか？**  
A: はい。スライド番号をイテレートし、各 `EditableDocument` を取得して変更を適用し、保存前に結果を結合します。

**Q: 既存スライドを編集するのではなく新しいスライドを追加したい場合は？**  
A: エディタ API を使用して新しいスライドを作成します（例: `PresentationEditOptions.setSlideNumber(-1)` を設定して末尾に追加）し、目的のマークアップを挿入します。

**Q: 単一のサービスで pptx を pptm に一括変換するにはどうすればよいですか？**  
A: ソースディレクトリをループし、同じ `Editor` インスタンスで各 PPTX をロードし、`PresentationSaveOptions(PresentationFormats.Pptm)` を使用して `save` を呼び出します。ストリームは速やかに閉じることを忘れずに。

## 結論

このガイドに従うことで、GroupDocs.Editor for Java を使用して **pptx を編集する方法** と **PPTX を PPTM に変換する方法** が分かります。プレゼンテーションをロードし、個々のスライドを変更し、テキストを置換し、結果をマクロ対応 PPTM ファイルとして保存できます—すべてプログラム上で安全に実行可能です。

**次のステップ:**  
- PPTM ファイルに VBA マクロを追加してみる。  
- 単一の Java サービスで複数のプレゼンテーションを一括変換する方法を検討する。  
- 画像処理やカスタムスタイリングなど高度な機能について、完全な GroupDocs.Editor ドキュメントを確認する。

---

**最終更新日:** 2026-03-17  
**テスト環境:** GroupDocs.Editor 25.3 for Java  
**作者:** GroupDocs