---
date: 2026-04-11
description: この詳細なステップバイステップガイドで、GroupDocs.Editor for .NET を使用してプログラムで Word 文書を編集し、Word
  を RTF に変換する方法を学びましょう。
keywords:
- programmatically edit word document
- convert pdf to editable
- replace text in document
- convert word to rtf
- save document to stream
linktitle: .NET 用 GroupDocs.Editor でプログラム的に Word 文書を編集
second_title: GroupDocs.Editor .NET API
title: .NET 用 GroupDocs.Editor でプログラム的に Word 文書を編集する
type: docs
url: /ja/net/document-editing/introduction-groupdocs-editor/
weight: 12
---

# .NET 用 GroupDocs.Editor で Word ドキュメントをプログラムで編集する

.NET 開発者で、**プログラムで Word ドキュメントを編集** する必要がある方—テキストの置換、形式の変換、または結果をストリームに埋め込む場合—GroupDocs.Editor for .NET は堅牢で使いやすいライブラリで、目的を達成できます。このチュートリアルでは、DOCX ファイルの読み込み、コンテンツの編集、結果を RTF に変換し、ディスクまたはメモリストリームに保存する実例を順に説明します。

## クイック回答
- **何を編集できますか？** Word、PDF、HTML、RTF など多数の形式をサポートしています。  
- **テキストを置換できますか？** はい – シンプルな文字列置換またはより高度な DOM 操作を使用します。  
- **PDF を編集可能に変換するには？** `Editor` で PDF を読み込み、生成された HTML を編集します。  
- **ストリームに保存する最も簡単な方法は？** `editor.Save(editableDoc, stream, options)` を使用します。  
- **ライセンスは必要ですか？** 本番環境で使用するには、一時ライセンスまたはフルライセンスが必要です。

## プログラムで Word ドキュメントを編集するとは何ですか？
プログラムで Word ドキュメントを編集することは、UI ではなくコードを使用してファイルを開き、コンテンツ（テキスト、画像、スタイル）を変更し、変更後のバージョンをストレージに書き戻すことを意味します。このアプローチは、自動レポート作成、バルクドキュメント更新、カスタムコンテンツ生成を実現します。

## なぜ GroupDocs.Editor for .NET を使用するのですか？
- **フォーマットの柔軟性:** DOCX、PDF、HTML、RTF などを読み込み、サポートされている任意の形式に保存できます。  
- **Office 依存なし:** サーバーに Microsoft Office がインストールされていなくても動作します。  
- **ストリームフレンドリー:** ファイルシステムではなくストリームから読み書きするクラウドシナリオに最適です。  
- **リッチ API:** 画像、フォント、CSS などのリソースにアクセスでき、フル機能の編集が可能です。

## 前提条件
Before we dive into the implementation, make sure you have:

- Visual Studio 2017 以降。  
- .NET Framework 4.6.1 以降。  
- GroupDocs.Editor for .NET – サイトから[download](https://releases.groupdocs.com/editor/net/)できます。  
- 有効なライセンスまたは GroupDocs の[temporary license](https://purchase.groupdocs.com/temporary-license/) が必要です。

## 名前空間のインポート
To start using GroupDocs.Editor for .NET, import the required namespaces:

```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

以下のセクションでは、ワークフローを小さなステップに分割して、簡単に追従できるようにします。

## ステップ 1: 入力ファイルへのパスを取得する
編集したい Word ファイルの場所を指定します。この例では **Your Sample Document.docx** という DOCX を想定します。

```csharp
string inputFilePath = "Your Sample Document.docx";
```

## ステップ 2: Editor オブジェクトのインスタンス化
`Editor` インスタンスを入力パスで作成します。これによりドキュメントが読み込まれ、編集の準備が整います。

```csharp
using (GroupDocs.Editor.Editor editor = new Editor(inputFilePath))
{
    // Subsequent steps will be nested inside this block
}
```

## ステップ 3: ドキュメントを編集用に開く
`EditableDocument` を取得すると、ドキュメントの HTML 表現とリソースにアクセスできます。

```csharp
EditableDocument beforeEdit = editor.Edit();
```

## ステップ 4: ドキュメントのコンテンツとリソースを取得する
生の HTML、画像、フォント、CSS を取得できます。マークアップを直接操作する必要がある場合に便利です。

```csharp
string content = beforeEdit.GetContent();
var images = beforeEdit.Images;
var fonts = beforeEdit.Fonts;
var stylesheets = beforeEdit.Css;
```

### ステップ 4.1: ドキュメントを単一の Base64 エンコード文字列として取得する
すべての埋め込みリソースを含む単一の文字列が必要な場合は、`GetEmbeddedHtml()` を呼び出します。

```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```

### ステップ 4.2: コンテンツを編集する
シンプルなテキスト置換の例として、単語 **Subtitle** を **Edited subtitle** に置き換えてみましょう。

```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```

## ステップ 5: 新しい EditableDocument インスタンスを作成する
マークアップを編集した後、`EditableDocument` オブジェクトに再度ラップします。

```csharp
EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```

## ステップ 6: 編集したドキュメントを保存する
結果を RTF ファイルとして保存します。ファイルシステムへのパスとメモリストリームの両方のオプションを示します。

### ステップ 6.1: 出力パスの準備
RTF を書き込む場所を定義します。

```csharp
string outputPath = Path.Combine("Output Directory Path", Path.GetFileNameWithoutExtension(inputFilePath) + ".rtf");
```

### ステップ 6.2: 保存オプションの準備
`WordProcessingSaveOptions` を使用して RTF 形式を選択します。

```csharp
Options.WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
```

### ステップ 6.3: パスに保存する
編集したドキュメントをファイルシステムに書き込みます。

```csharp
editor.Save(afterEdit, outputPath, saveOptions);
```

### ステップ 6.4: ストリームに保存する
結果をメモリ上に保持する必要がある場合（例: クラウドストレージにアップロードする場合）は、`MemoryStream` を使用します。

```csharp
using (MemoryStream ms = new MemoryStream())
{
    editor.Save(afterEdit, ms, saveOptions);
}
```

## ステップ 7: Editor と EditableDocument インスタンスを破棄する
リソースを速やかに解放し、メモリリークを防止します。

```csharp
beforeEdit.Dispose();
afterEdit.Dispose();
editor.Dispose();
```

## 一般的な使用例とヒント
- **PDF を編集可能に変換:** `Editor` で PDF を読み込み、生成された HTML を編集し、PDF または別の形式で保存します。  
- **ドキュメント内のテキストを置換:** シンプルなケースでは `string.Replace` を使用し、複雑なシナリオでは DOM を操作します。  
- **Word を RTF に変換:** 上記のように、保存オプションで `WordProcessingFormats.Rtf` を設定します。  
- **ドキュメントをストリームに保存:** クライアントに直接ファイルを返す Web API に最適です。  
- **編集用にドキュメントを読み込む:** 必ず `Editor` を `using` ブロックでラップし、適切に破棄されるようにします。

## よくある質問

**Q: GroupDocs.Editor for .NET で PDF ファイルを編集できますか？**  
A: はい、GroupDocs.Editor は PDF を中間の HTML 表現に変換して編集をサポートします。

**Q: GroupDocs.Editor for .NET の一時ライセンスはどう取得しますか？**  
A: [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) から一時ライセンスを取得できます。

**Q: GroupDocs.Editor for .NET がサポートするファイル形式は何ですか？**  
A: DOCX、PDF、HTML、RTF など多数の形式がサポートされています。

**Q: GroupDocs.Editor をクラウドストレージと統合できますか？**  
A: もちろん可能です。Azure Blob、Amazon S3、Google Cloud Storage などのストリームを読み書きできます。

**Q: GroupDocs.Editor for .NET のドキュメントはどこで見つけられますか？**  
A: ドキュメントは[here](https://tutorials.groupdocs.com/editor/net/) で入手可能です。

---

**最終更新日:** 2026-04-11  
**テスト済みバージョン:** GroupDocs.Editor 23.12 for .NET  
**作者:** GroupDocs