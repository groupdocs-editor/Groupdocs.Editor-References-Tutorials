---
title: 編集可能なドキュメントの高度な使用法
linktitle: 編集可能なドキュメントの高度な使用法
second_title: GroupDocs.Editor .NET API
description: プログラムによってドキュメントからリソースを作成、編集、抽出する GroupDocs.Editor for .NET の高度な使用方法を学習します。
weight: 11
url: /ja/net/document-editing/advanced-usage-of-editable-documents/
---
## 導入
ドキュメント編集機能を強化したいと考えている .NET 開発者にとって、GroupDocs.Editor for .NET は強力なツール スイートです。この包括的なガイドでは、GroupDocs.Editor を使用した編集可能なドキュメントの高度な使用法について説明し、各ステップを詳細に説明して、その可能性を最大限に引き出せるようにします。
## 前提条件
高度な機能に進む前に、次のものを用意してください。
- 開発マシンに Visual Studio がインストールされています。
- GroupDocs.Editor と互換性のある .NET Framework。
-  GroupDocs.Editor for .NETライブラリ。[ここからダウンロード](https://releases.groupdocs.com/editor/net/).
- 有効なGroupDocs.Editorライセンス。[無料トライアル](https://releases.groupdocs.com/)または購入する[一時ライセンス](https://purchase.groupdocs.com/temporary-license/).
## 名前空間のインポート
まず、.NET プロジェクトに必要な名前空間をインポートしていることを確認します。
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
## ステップ 1: EditableDocument インスタンスの作成
まず、インスタンスを作成する必要があります`EditableDocument`サポートされている形式の入力ドキュメントを読み込んで編集します。
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
このステップでは、入力ドキュメントを読み込み、編集の準備をします。
## ステップ2: ドキュメントリソースの抽出
の`EditableDocument`抽出および操作できるさまざまなリソースが含まれています。これらを詳しく見てみましょう。
### ステップ 2.1: ドキュメント全体を HTML として抽出する
すべてのリソースが HTML として埋め込まれたドキュメント全体を含む単一の文字列を生成できます。
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
この文字列には、base64 でエンコードされたスタイルシート、画像、フォントが含まれるため、かなり大きくなります。
### ステップ 2.2: すべての画像を抽出する
ドキュメントからすべての画像を抽出します。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### ステップ 2.3: すべてのフォントを抽出する
ドキュメントで使用されているすべてのフォントを抽出します。
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### ステップ 2.4: すべてのスタイルシートを抽出する
すべてのスタイルシートをテキスト形式で抽出します。
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### ステップ2.5: すべてのリソースを収集する
回の呼び出しですべてのリソースを収集します。
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
これには、画像、フォント、スタイルシートが含まれます。
### ステップ 2.6: HTML マークアップを取得する
埋め込まれたリソースなしでドキュメントの HTML マークアップを取得します。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## ステップ3: 外部リンクの調整
場合によっては、外部リンクを調整してカスタム リソース ハンドラーを指すようにする必要があります。その方法は次のとおりです。
### ステップ3.1: カスタムプレフィックスを準備する
元の外部リンクの先頭に追加するプレフィックスを準備します。
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### ステップ 3.2: プレフィックス付き HTML マークアップを生成する
調整されたリンクを含む HTML マークアップを生成します。
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### ステップ 3.3: 本文のみの HTML コンテンツを取得する
一部の WYSIWYG エディターは、ヘッダーのない純粋な HTML マークアップのみを処理します。
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### ステップ 3.4: プレフィックス付きの本文のみのコンテンツ
カスタム画像プレフィックスを使用して本文のみのコンテンツを生成します。
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### ステップ3.5: スタイルシートの抽出
ドキュメントで使用されているスタイルシートを抽出します。
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### ステップ 3.6: プレフィックス付きスタイルシート
カスタムプレフィックスを使用してスタイルシートを抽出します。
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## ステップ4: ドキュメントをHTMLとして保存する
編集したドキュメントを、そのリソースを含めて HTML ファイルとして保存します。
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
この方法では、スタイルシート、画像、フォントなどのリソース用の個別のディレクトリが作成されます。
## ステップ 5: EditableDocument の破棄
EditableDocumentは実装する`IDisposable`インスタンスが破棄されているかどうかを確認する機能も提供します。
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### ステップ 5.1 Dispose イベントの処理
破棄イベントをサブスクライブすることもできます。
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## ステップ 6: HTML から編集可能なドキュメントを作成する
HTML ドキュメントから EditableDocument のインスタンスを作成します。
### ステップ 6.1: HTML ファイルから
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### ステップ 6.2: HTML マークアップから
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
これらのインスタンス (afterEditFromFile および afterEditFromMarkup) は、元のインスタンス (beforeEdit) と同一です。
## ステップ7: 手動での廃棄
EditableDocument インスタンスを手動で破棄します。
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
これにより、リソースが適切にクリーンアップされます。
## 結論
GroupDocs.Editor for .NET は、プログラムでドキュメントを編集するための強力なツールを提供します。このステップ バイ ステップ ガイドに従うことで、ドキュメントのコンテンツ、リソース、および出力形式を効率的に管理できます。リソースを埋め込む場合、外部リンクを調整する場合、またはドキュメントを HTML に変換する場合など、GroupDocs.Editor は高度なドキュメント操作に必要な機能を提供します。
## よくある質問
### GroupDocs.Editor はどのような形式をサポートしていますか?
GroupDocs.Editor は、DOCX、XLSX、PPTX など、さまざまな形式をサポートしています。
### GroupDocs.Editor をライセンスなしで使用できますか?
はい、[無料トライアル](https://releases.groupdocs.com/)または[一時ライセンス](https://purchase.groupdocs.com/temporary-license/).
### ドキュメントから特定のリソースを抽出するにはどうすればよいですか?
提供されているメソッドを使用して、画像、フォント、スタイルシートを抽出できます。`Images`, `Fonts` 、 そして`Css`.
### HTML 出力内のリンクを調整することは可能ですか?
はい、画像、CSS、フォントのカスタムプレフィックスを指定して外部リンクを調整できます。
### 編集したドキュメントを HTML ファイルとして保存するにはどうすればよいですか?
使用`Save`方法の`EditableDocument`クラスを使用して、リソースを含むドキュメントを HTML ファイルとして保存します。