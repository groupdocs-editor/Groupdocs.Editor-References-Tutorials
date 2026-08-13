---
date: 2026-06-06
description: GroupDocs.Editor for .NET を使用して CSV および TSV ファイルから **create editable
  document** オブジェクトを作成する方法を学びます。このガイドでは、Visual Studio で **read delimited text C#**
  と **edit CSV .NET** を効率的に行う方法も示します。
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Delimited Separated Values (DSV) を操作する – 編集可能なドキュメントを作成
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Delimited Separated Values (DSV) を操作する – 編集可能なドキュメントを作成
type: docs
url: /ja/net/document-processing/work-dsv/
weight: 12
---

# 区切り文字付き値 (DSV) の操作 – 編集可能なドキュメントの作成

.NET 開発者で、CSV や TSV などの区切り文字付き値 (DSV) から **editable document** オブジェクトを作成したい方は、正しい場所に来ました。最初の 100 語で、GroupDocs.Editor for .NET が **read delimited text C#** を最も信頼できる方法で読み取り、編集し、書式を失わずに保存できる理由を説明します。Visual Studio ソリューションに自然に組み込める、コピー＆ペースト可能な完全なワークフローを手に入れられます。

## クイック回答
- **どのライブラリが .NET で CSV 編集に最適ですか？** GroupDocs.Editor for .NET.
- **Visual Studio で大きな CSV ファイルを編集できますか？** はい – API はデータをストリーミングし、ファイル全体をメモリにロードしません。
- **本番環境で使用するにはライセンスが必要ですか？** 商用ライセンスが必要です。無料トライアルが利用可能です。
- **編集後に出力できるフォーマットは？** CSV、TSV、Excel 互換のスプレッドシート形式です。
- **API は .NET 6+ と互換性がありますか？** もちろんです – .NET Framework 4.5+、.NET Core 3.1+、.NET 5、.NET 6 をサポートしています。

## GroupDocs.Editor のコンテキストで「create editable document」とは何ですか？
**Create editable document** とは、`EditableDocument` インスタンスを生成し、メモリ上にソースファイル (CSV、TSV など) の可変バージョンを表すことを意味します。このオブジェクトを使用すると、同じ API でコンテンツを読み取り、変更し、再保存できます。ドキュメントテキストの取得、変更の適用、さまざまな形式での再保存メソッドが提供され、列の整列や引用符が保持されます。

## DSV の取り扱いに GroupDocs.Editor を使用する理由は？
GroupDocs.Editor は **50 以上の入力および出力フォーマット** を処理し、CSV、TSV、Excel 互換スプレッドシートを含みます。500 MB までのファイルでもメモリ使用量は 10 MB 未満に抑えられます。また、列の整列、引用符ルール、カスタムエンコーディングを自動的に保持するため、手動のパースロジックが不要です。

## 前提条件
- **Visual Studio**（任意の最新エディション） – IDE 内で直接開発およびデバッグできます。
- **GroupDocs.Editor for .NET** – 最新パッケージは **[here](https://releases.groupdocs.com/editor/net/)** からダウンロードしてください。
- **Basic C# knowledge** – 本チュートリアルは、コンソールまたは ASP.NET プロジェクトを作成し、NuGet パッケージを追加できることを前提としています。

## 名前空間のインポート
`Editor`、`EditableDocument`、およびオプションクラスは `GroupDocs.Editor` 名前空間にあります。

`DelimitedTextEditOptions` クラスは、区切り文字（カンマ、タブなど）やその他のパースルールを定義するエントリーポイントです。

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## CSV ファイルから editable document を作成する方法は？
`Editor` でソース CSV をロードし、カンマ区切りを指定した `DelimitedTextEditOptions` インスタンスを渡して `Edit` メソッドを呼び出します。メソッドはメモリ上の `EditableDocument` を返し、これを操作できます。この 2 段階パターン（ロード → 編集）は **read delimited text C#** シナリオをカバーし、元のファイル構造が保持されます。

## 手順 1: 入力 DSV ファイルへのパスを取得する
まず、ソース DSV ファイルへの絶対パスまたは相対パスを指定する必要があります。デモ用にプロジェクトの `Data` フォルダーにあるシンプルな CSV を使用します。

```csharp
string inputFilePath = "Your Sample Document";
```

## 手順 2: Editor インスタンスを作成する
`Editor` はロード、編集、保存を統括するコアクラスです。`FileInfo` オブジェクトでインスタンス化すると、ファイルライフサイクルを完全に制御できます。

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## 手順 3: DSV 編集オプションを作成する
`DelimitedTextEditOptions` はエディタにファイルの解釈方法を指示します。区切り文字、ヘッダー行の有無、文字エンコーディングなどを設定できます。

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## 手順 4: EditableDocument インスタンスを作成する
`EditableDocument` はソースファイルの可変メモリバージョンを表します。オプションを指定して `Editor.Edit` を呼び出すと `EditableDocument` が返されます。このオブジェクトはテキストを可変文字列として保持し、任意の **parse delimited values C#** 操作に備えます。

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## 手順 5: ドキュメント内容を編集する
`GetDocumentText()` は editable document の現在のテキストを文字列で返します。`EditableDocument.GetDocumentText()` で元テキストを取得し、列の値を置換するなどの変更を加えて新しい文字列に保存します。これにより **edit CSV .NET** が低レベルのファイルストリームに触れずに実現できます。

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## 手順 6: 更新されたコンテンツで EditableDocument を作成する
変更後の文字列を再び `EditableDocument` にラップします。このステップで変更が確定し、任意のサポート形式で保存できる状態になります。

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## 手順 7: CSV 保存オプションを作成する
`DelimitedTextSaveOptions` は編集後のコンテンツを書き戻す際の設定を指定します。変更を永続化する準備ができたら、同じ区切り文字や別の区切り文字、改行スタイルなどを構成できます。

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 手順 8: TSV 保存オプションを作成する
タブ区切り版が必要な場合は、区切り文字を `\t` に切り替えるだけです。同じ `EditableDocument` を異なるオプションで複数回保存できます。

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## 手順 9: スプレッドシート保存オプションを作成する
`SpreadsheetSaveOptions` はドキュメントを .xlsx などの Excel 互換形式にエクスポートする設定です。GroupDocs.Editor は編集データを Excel 互換形式（`.xlsx`）にエクスポートでき、`SpreadsheetSaveOptions` クラスが列タイプ、数式、セルスタイルを自動的に処理します。

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## 手順 10: 保存パスを準備する
各形式ごとに異なる出力パスを定義します。`output.csv`、`output.tsv`、`output.xlsx` のように明確な命名規則を使用すると、プロジェクトが整理しやすくなります。

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## 手順 11: 編集済みドキュメントを保存する
`Save()` は提供された保存オプションを使用してディスクに書き込みます。各ターゲット形式に対して適切なオプションで `EditableDocument.Save` を呼び出してください。API は元のエンコーディングを保持し、上書きしない限りそのまま保存します。

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## 手順 12: EditableDocument インスタンスを破棄する
`Editor` と `EditableDocument` はどちらも `IDisposable` を実装しています。破棄するとファイルハンドルとアンマネージドリソースが解放され、バッチジョブで多数のファイルを処理する際に重要です。

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## よくある問題と解決策
| 問題 | 発生理由 | 解決策 |
|------|----------|--------|
| **予期しない余分な引用符** | デフォルトの CSV パーサーは、埋め込みのコンマを区切り文字として扱う可能性があります。 | `DelimitedTextEditOptions` で `EscapeMode = EscapeMode.DoubleQuote` を設定してください。 |
| **大きなファイルでメモリ使用量が急増** | ストリーミングせずに 500 MB のファイルをロードしています。 | 遅延ロードを有効にする `LoadOptions` を使用して `Editor.Load` を呼び出してください。 |
| **エンコーディングの不一致** | ソースファイルは UTF‑16 を使用していますが、オプションはデフォルトで UTF‑8 です。 | 保存オプションで明示的に `Encoding = Encoding.Unicode` を設定してください。 |

## よくある質問

**Q: GroupDocs.Editor for .NET を使用して大きな CSV ファイルを編集できますか？**  
A: はい、API はデータをストリーミングし、ドキュメント全体をメモリにロードせずに 1 GB を超えるファイルも処理できます。

**Q: GroupDocs.Editor for .NET は CSV と TSV 以外の DSV フォーマットもサポートしていますか？**  
A: もちろんです – `DelimitedTextEditOptions` で指定すれば、任意の単一文字区切り（例: パイプ `|`、セミコロン `;`）がサポートされます。

**Q: DSV ファイルを保存する際にエンコーディングをカスタマイズできますか？**  
A: はい、`DelimitedTextSaveOptions` の `Encoding` プロパティを UTF‑8、UTF‑16、ISO‑8859‑1、または必要な任意の .NET `Encoding` に設定できます。

**Q: GroupDocs.Editor for .NET を使用して CSV ファイルを Excel スプレッドシートに変換できますか？**  
A: はい – 編集後に `SpreadsheetSaveOptions` を使用してコンテンツを `.xlsx` ワークブックとしてエクスポートすれば完了です。

**Q: GroupDocs.Editor for .NET の詳細なドキュメントはどこで見つけられますか？**  
A: 詳細な API リファレンスとコードサンプルは **[here](https://tutorials.groupdocs.com/editor/net/)** で入手できます。

**最終更新日:** 2026-06-06  
**テスト環境:** GroupDocs.Editor 23.10 for .NET  
**作者:** GroupDocs

## 関連チュートリアル

- [GroupDocs.Editor .NET 用 プレーンテキストおよび DSV ドキュメント編集チュートリアル](/editor/net/plain-text-dsv-documents/)
- [効率的な CSV ドキュメント編集と変換のための GroupDocs.Editor .NET マスターガイド](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [.NET でのドキュメントロードの完全ガイド – GroupDocs.Editor を活用](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)