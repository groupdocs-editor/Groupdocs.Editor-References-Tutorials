---
date: 2026-08-10
description: GroupDocs.Editor for .NET を使用して plain text ファイルを編集する方法を学びます。このガイドでは、txt
  ファイルの読み込み、スペースのトリミング、テキストエンコーディングの設定、結果の保存について説明します。
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Plain Text ドキュメントの操作
og_description: GroupDocs.Editor for .NET を使用して plain text ファイルを編集する方法を学びます – txt
  ファイルの読み込み、末尾スペースのトリミング、先頭スペースの変換、テキストエンコーディングの設定、そして効率的な保存。
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: GroupDocs.Editor for .NET を使用した plain text ドキュメントの編集
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: GroupDocs.Editor for .NET を使用した plain text ドキュメントの編集
type: docs
url: /ja/net/document-processing/work-plain-text-documents/
weight: 15
---

# GroupDocs.Editor for .NET を使用したプレーンテキスト文書の編集

## はじめに
.NET アプリケーションで **プレーンテキスト** を迅速かつ確実に編集する必要がある場合、GroupDocs.Editor for .NET が重い作業を代行してくれます。この API は 30 以上のドキュメント形式をサポートし、最大 500 MB のファイルを処理でき、ファイル全体をメモリにロードせずにテキストを操作できます。このチュートリアルでは、txt ファイルの読み込み、末尾スペースのトリム、先頭スペースの変換、正しいエンコーディングの設定、そして最終的に編集した内容をディスクに保存する方法を学びます。さっそく始めましょう！

## クイック回答
- **txt ファイルを編集する最初のステップは何ですか？** `Editor` を使用して、パスまたはストリームでファイルをロードします。  
- **編集中にファイルのエンコーディングを変更できますか？** はい – `TxtSaveOptions` で UTF‑8、UTF‑16、または任意のカスタムエンコーディングを指定できます。  
- **各行の末尾の余分なスペースを削除するには？** テキストを取得し、各行で `TrimEnd()` を呼び出して、再度書き込みます。  
- **GroupDocs.Editor は無料で試せますか？** リリースページから 30 日間のフル機能トライアルが利用可能です。  
- **対応している .NET バージョンは？** .NET Framework 4.6 以上、.NET Core 3.1 以上、そして .NET 5/6/7。

## プレーンテキストの編集とは？
**Edit plain text** は、単純な `.txt` ファイル内の文字をプログラムで変更することを意味します—追加、削除、または再フォーマット—ファイルの元のエンコーディングと改行スタイルを保持したままです。空白のトリミング、改行コードの正規化、設定値の更新、生成コンテンツの挿入などの作業が含まれます。この操作は、標準的なテキストエディタでファイルが読み取れる状態を保ち、BOM マーカーなど既存のメタデータも維持する必要があります。

## プレーンテキスト編集に GroupDocs.Editor を使用する理由
GroupDocs.Editor はストリーミング方式でファイルを処理するため、300 MB のログファイルでも 50 MB 未満の RAM で編集できます。このライブラリは **50 以上の入力および出力フォーマット** をサポートし、改行スタイル（CR、LF、CRLF）を自動検出し、**末尾スペースのトリム** と **先頭スペースの変換** をカスタムパーサーを書かずに組み込みオプションで提供します。

## 前提条件
- **.NET 開発環境** – Visual Studio 2022 または C# 拡張機能付き VS Code。  
- **GroupDocs.Editor for .NET** – [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) のリリースページからダウンロード。  
- **基本的な C# 知識** – ファイル I/O と文字列操作に慣れている必要があります。  
- **テキストエディタ（任意）** – ソースファイルの確認用；VS Code が推奨されます。  
- 詳細な使用方法は、[ドキュメント](https://tutorials.groupdocs.com/editor/net/) を参照してください。  
- また、一般的な [リリースページ](https://releases.groupdocs.com/) も閲覧できます。

## プレーンテキストの編集手順
ファイルをロードし、内容を編集し、保存します—コードは 10 行未満です。以下のセクションで各ステップをわかりやすく説明します。

### 手順 1: 入力 TXT ファイルへのパスを取得
まず、物理的なファイルパスで作業するか、メモリストリームで作業するかを決めます。ローカル開発ではパスを使用するのが最も簡単です。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### 手順 2: Editor インスタンスの作成
`Editor` はドキュメントをロードし、編集機能を提供する主要クラスです。

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### 手順 3: TXT 編集オプションの作成
`TxtEditOptions` はプレーンテキストファイルの解析と編集方法を構成し、エンコーディングやスペース処理ルールを設定できます。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### 手順 4: EditableDocument インスタンスの作成
`EditableDocument` はロードされたドキュメントのメモリ内バージョンを表し、テキストと関連リソースを含みます。

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### 手順 5: ドキュメント内容の編集
元のテキストを取得し、必要な文字列操作（例: 置換、トリム、ケース変換）を適用し、結果を `EditableDocument` に戻します。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### 手順 6: 更新された内容で EditableDocument を作成
テキストを変換した後、編集済み文字列と元のリソースコレクションを含む新しい `EditableDocument` をインスタンス化します。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### 手順 7: WordProcessing 保存オプションの作成
`WordProcessingSaveOptions` は DOCX や DOCM などの Word 互換形式で保存するための設定を定義します。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### 手順 8: TXT 保存オプションの作成
`TxtSaveOptions` は編集されたプレーンテキストファイルの書き込み方法を指定し、エンコーディング、改行の保持、テーブルレイアウトの処理などを含みます。

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### 手順 9: 出力パスの準備
入力ファイルパスから出力ディレクトリを導出し、DOCX と TXT の結果用の完全なファイル名を作成します。

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### 手順 10: 編集済みドキュメントの保存
最後に、`editor.Save` を 2 回呼び出します—WordProcessing オプションで 1 回、TXT オプションで 1 回—1 回の操作で両方の形式を生成します。

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## よくある問題と解決策
- **編集後に末尾スペースが残る** – ドキュメントをロードする前に `TxtEditOptions.TrimTrailingSpaces` が `true` に設定されていることを確認してください。  
- **保存されたファイルのエンコーディングが正しくない** – `TxtSaveOptions.Encoding` が目的のコードページ（例: `Encoding.UTF8`）と一致しているか確認してください。  
- **大きなファイルで OutOfMemoryException が発生** – メモリ使用量を抑えるために、ファイルパスからロードする代わりにストリーミング API（`Editor.Load(Stream)`）を使用してください。  

## よくある質問

**Q: GroupDocs.Editor for .NET がサポートするファイル形式は何ですか？**  
A: ライブラリは 50 以上の形式をサポートし、DOCX、TXT、HTML、PDF、markdown などを含み、シームレスに編集および変換できます。

**Q: GroupDocs.Editor for .NET の無料トライアルはどうやって入手できますか？**  
A: [リリースページ](https://releases.groupdocs.com/) からトライアルをダウンロードしてください。

**Q: テスト用に一時ライセンスを購入できますか？**  
A: はい、一時ライセンスは [GroupDocs 購入ページ](https://purchase.groupdocs.com/temporary-license/) で入手可能です。

**Q: 問題が発生した場合、どこでサポートを受けられますか？**  
A: 公式サポートフォーラムが最適です – [GroupDocs.Editor サポートフォーラム](https://forum.groupdocs.com/c/editor/20) をご覧ください。

**Q: 高度なシナリオ向けの詳細なドキュメントはありますか？**  
A: もちろんです。完全なリファレンスは [GroupDocs.Editor ドキュメントページ](https://tutorials.groupdocs.com/editor/net/) にあります。

## 結論
これで、GroupDocs.Editor for .NET を使用して **プレーンテキスト** ファイルを編集する方法—txt ファイルのロード、スペースのトリム、先頭スペースの変換、適切なエンコーディングの設定、そして TXT と DOCX の両方の形式で保存—を習得しました。この機能により、ログファイルのクリーンアップを自動化したり、設定ファイルをオンザフライで生成したり、独自のテキスト処理パイプラインを構築したりできます。バッチ処理やドキュメント変換などの追加機能は、公式ドキュメントをご覧ください。

---

**最終更新日:** 2026-08-10  
**テスト環境:** GroupDocs.Editor 23.11 for .NET  
**作者:** GroupDocs  

---

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## 関連チュートリアル

- [GroupDocs.Editor for .NET のドキュメントロードチュートリアル](/editor/net/document-loading/)
- [GroupDocs.Editor .NET のドキュメント保存とエクスポートチュートリアル](/editor/net/document-saving/)
- [GroupDocs.Editor .NET のプレーンテキストおよび DSV ドキュメント編集チュートリアル](/editor/net/plain-text-dsv-documents/)