---
date: 2026-03-14
description: GroupDocs.Editor for .NET を使用して、DOCX から画像を抽出し、DOCX を HTML に変換し、ドキュメントを
  HTML として保存する方法を学びましょう。
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: DOCXから画像を抽出 – 高度な編集可能ドキュメントの活用
type: docs
url: /ja/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# DOCX から画像を抽出 – 高度な Editable Document の使用方法

.NET 開発者で、**DOCX から画像を抽出** し、ドキュメント編集機能を強化したい方には、GroupDocs.Editor for .NET が強力なツール群を提供します。この包括的なガイドでは、GroupDocs.Editor を使用した Editable Document の高度な使用方法をステップごとに詳しく解説し、そのすべての機能を活用できるようにします。

## クイック回答
- **DOCX ファイルから画像を抽出するにはどうすればよいですか？** `Editor` でドキュメントをロードした後、`EditableDocument.Images` を使用します。  
- **埋め込みリソース付きで DOCX を HTML に変換できますか？** はい。HTML マークアップには `EditableDocument.GetEmbeddedHtml()` または `GetContent()` を呼び出します。  
- **編集したドキュメントを HTML として保存するメソッドは何ですか？** `EditableDocument.Save(htmlFilePath)` はリソースフォルダー付きの HTML ファイルを作成します。  
- **Word ドキュメントからフォントを抽出できますか？** `EditableDocument.Fonts` を使用してすべてのフォントリソースを取得します。  
- **本番環境で使用するにはライセンスが必要ですか？** 有効な GroupDocs.Editor ライセンスが必要です。無料トライアルも利用可能です。

## **extract images from docx** とは何ですか？
DOCX ファイルから画像を抽出するとは、Word ドキュメントに埋め込まれた各画像をプログラムで取得し、再利用、変更、または個別に保存できるようにすることです。GroupDocs.Editor は `EditableDocument` インスタンス上の `Images` コレクションを公開しており、この作業をシンプルに行えます。

## このワークフローで GroupDocs.Editor を使用する理由
- **フルコントロール**：手動で ZIP を扱うことなく、ドキュメントリソース（画像、フォント、CSS）を完全に管理できます。  
- **シームレスな変換**：レイアウトとスタイルを保持したまま DOCX から HTML へ変換できます。  
- **簡単なリソース抽出**：カスタム画像処理、フォント埋め込み、CDN 配信などに利用できます。  
- **堅牢な破棄パターン**：長時間稼働するサービスでメモリリークが発生しないよう保証します。

## 前提条件
- 開発マシンに Visual Studio がインストールされていること。  
- GroupDocs.Editor と互換性のある .NET Framework。  
- GroupDocs.Editor for .NET ライブラリ。こちらから[ダウンロードできます](https://releases.groupdocs.com/editor/net/)。  
- 有効な GroupDocs.Editor ライセンス。こちらの[無料トライアル](https://releases.groupdocs.com/)または[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)を取得できます。

## 名前空間のインポート
まず、.NET プロジェクトで必要な名前空間をインポートしてください。

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

## 手順 1: EditableDocument インスタンスの作成
最初に、サポートされている形式の入力ドキュメントをロードして編集し、`EditableDocument` のインスタンスを作成する必要があります。

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

この手順では、入力ドキュメントをロードし、編集の準備を行います。

## **extract images from DOCX** の方法は？
以下では、リソース抽出機能を詳しく見ていきます。最も一般的なニーズである Word ファイルからすべての画像を取得する方法から始めます。

## 手順 2: ドキュメントリソースの抽出
`EditableDocument` には抽出および操作可能なさまざまなリソースが含まれています。これらを分解して見ていきましょう。

### 手順 2.1: ドキュメント全体を HTML として抽出
すべてのリソースが埋め込まれた HTML として、ドキュメント全体を単一の文字列で生成できます。

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

この文字列は、スタイルシート、画像、フォントが base64 でエンコードされているため、かなり大きくなります。

### 手順 2.2: すべての画像を抽出 *(primary keyword in action)*
ドキュメントからすべての画像を抽出します—これは **extract images from docx** の核心です。

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### 手順 2.3: すべてのフォントを抽出 *(secondary keyword)*
**extract fonts from word** も必要な場合は、以下の呼び出しを使用します。

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### 手順 2.4: すべてのスタイルシートを抽出
テキスト形式ですべてのスタイルシートを抽出します。

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### 手順 2.5: すべてのリソースを取得
1 回の呼び出しで全リソースを取得します。

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

これには画像、フォント、スタイルシートが含まれます。

### 手順 2.6: HTML マークアップを取得
埋め込みリソースなしでドキュメントの HTML マークアップを取得します。

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## カスタム処理で **convert docx to html** する方法は？
場合によっては、外部リンクを調整して独自のリソースハンドラを指すようにする必要があります。

## 手順 3: 外部リンクの調整
### 手順 3.1: カスタムプレフィックスの準備
元の外部リンクの前に付加するプレフィックスを準備します。

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### 手順 3.2: プレフィックス付き HTML マークアップの生成
調整されたリンクを含む HTML マークアップを生成します。

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### 手順 3.3: 本文のみの HTML コンテンツを取得
一部の WYSIWYG エディタはヘッダーなしの純粋な HTML マークアップのみを扱います。

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### 手順 3.4: プレフィックス付き本文のみコンテンツ
カスタム画像プレフィックスを使用した本文のみのコンテンツを生成します。

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### 手順 3.5: スタイルシートの抽出
ドキュメントで使用されているスタイルシートを抽出します。

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### 手順 3.6: プレフィックス付きスタイルシート
カスタムプレフィックス付きでスタイルシートを抽出します。

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## 正しく **save document as html** する方法は？
## 手順 4: ドキュメントを HTML として保存
編集したドキュメントをリソースを含む HTML ファイルとして保存します。

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

このメソッドは、スタイルシート、画像、フォントなどのリソース用に別個のディレクトリを作成します。

## 手順 5: EditableDocument の破棄
`EditableDocument` は `IDisposable` を実装しており、インスタンスが破棄されたかどうかを確認する機能を提供します。

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### 手順 5.1: Dispose イベントの処理
また、disposing イベントを購読することもできます。

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## 手順 6: HTML から EditableDocument を作成
HTML ドキュメントから `EditableDocument` のインスタンスを作成します。

### 手順 6.1: HTML ファイルから

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### 手順 6.2: HTML マークアップから

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

これらのインスタンス（`afterEditFromFile` と `afterEditFromMarkup`）は、元のインスタンス（`beforeEdit`）と同一です。

## 手順 7: 手動での破棄
`EditableDocument` インスタンスを手動で破棄します。

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

これによりリソースが適切にクリーンアップされます。

## よくある問題と解決策
- **画像が抽出後に表示されない:** ドキュメントに埋め込み画像が実際に含まれていること、そして `Edit` 呼び出し後に `beforeEdit.Images` にアクセスしていることを確認してください。  
- **HTML 出力でフォントが欠落している:** フォント URL を正しく埋め込むために `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` を呼び出していることを確認してください。  
- **大きな HTML 文字列でメモリ圧迫が発生する:** 埋め込みリソースなしのマークアップには `GetContent()` を使用し、画像や CSS は別ファイルで配信してください。

## よくある質問
**Q: GroupDocs.Editor がサポートしているフォーマットは何ですか？**  
A: GroupDocs.Editor は DOCX、XLSX、PPTX など多数の一般的なオフィスフォーマットをサポートしています。

**Q: ライセンスなしで GroupDocs.Editor を使用できますか？**  
A: はい、[無料トライアル](https://releases.groupdocs.com/)または[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)で使用できます。

**Q: ドキュメントから特定のリソースを抽出するにはどうすればよいですか？**  
A: `EditableDocument` インスタンスの `Images`、`Fonts`、`Css` コレクションを使用します。

**Q: HTML 出力のリンクを調整できますか？**  
A: はい、`GetContent` または `GetBodyContent` にカスタム URI プレフィックスを渡すことで、画像、CSS、フォントのリンクを書き換えることができます。

**Q: 編集したドキュメントを HTML ファイルとして保存するにはどうすればよいですか？**  
A: `.html` で終わるファイルパスを指定して、`EditableDocument` インスタンスの `Save` メソッドを呼び出します。

---

**最終更新日:** 2026-03-14  
**テスト環境:** GroupDocs.Editor for .NET（最新リリース）  
**作者:** GroupDocs