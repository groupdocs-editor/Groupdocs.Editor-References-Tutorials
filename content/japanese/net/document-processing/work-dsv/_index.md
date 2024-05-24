---
title: 区切り文字で区切られた値 (DSV) の操作
linktitle: 区切り文字で区切られた値 (DSV) の操作
second_title: GroupDocs.Editor .NET API
description: このステップバイステップ ガイドでは、GroupDocs.Editor for .NET を使用して CSV および TSV ファイルを編集する方法を学習します。.NET プロジェクトを簡単に改善できます。
type: docs
weight: 12
url: /ja/net/document-processing/work-dsv/
---
## 導入
CSV や TSV ファイルなどの区切り値 (DSV) を扱う開発者であれば、これらのファイルをプログラムで編集するのは大変な作業になる可能性があることをご存知でしょう。ただし、GroupDocs.Editor for .NET を使用すると、この作業は大幅に簡単かつ効率的になります。このチュートリアルでは、GroupDocs.Editor for .NET を使用して DSV ファイルを読み取り、編集し、保存する方法について説明します。プロセスをわかりやすい手順に分解して、プロジェクトに簡単に実装できるようにします。
## 前提条件
チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。
- Visual Studio: マシンに Visual Studio がインストールされていることを確認します。
-  GroupDocs.Editor for .NET: GroupDocs.Editor for .NETライブラリをダウンロードして参照する必要があります。ダウンロードできます。[ここ](https://releases.groupdocs.com/editor/net/).
- C# の基本的な理解: このチュートリアルでは、C# と .NET 開発の基本的な理解があることを前提としています。
## 名前空間のインポート
まず、プロジェクトに必要な名前空間をインポートする必要があります。これらの名前空間は、GroupDocs.Editor for .NET を操作するために必要なクラスとメソッドを提供します。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## ステップ1: 入力DSVファイルへのパスを取得する
まず、入力 DSV ファイルへのパスを指定する必要があります。この例では、CSV ファイルであると想定します。
```csharp
string inputFilePath = "Your Sample Document";
```
## ステップ2: エディターインスタンスを作成する
インスタンスを作成する`Editor`クラス。このインスタンスは、DSV ファイルの読み込みと操作に使用されます。
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## ステップ3: DSV編集オプションを作成する
次に、インスタンスを作成します`DelimitedTextEditOptions`DSV ファイルの区切り文字を指定します。ここでは、区切り文字としてカンマを使用します。
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## ステップ4: EditableDocumentインスタンスを作成する
作成する`EditableDocument`インスタンスを使用して`Editor.Edit`メソッド。これにより、ドキュメントを編集する準備が整います。
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## ステップ5: ドキュメントコンテンツを編集する
元のテキスト コンテンツを取得し、必要な変更を加えます。デモンストレーションのために、一部のテキストを置き換えてみましょう。
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ステップ 6: 更新されたコンテンツを含む編集可能なドキュメントを作成する
新しいを作成します`EditableDocument`更新されたコンテンツ。
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## ステップ7: CSV保存オプションを作成する
区切り文字やエンコードなど、CSV 形式の保存オプションを指定します。
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## ステップ8: TSV保存オプションを作成する
同様に、TSV 形式の保存オプションを指定します。
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## ステップ9: スプレッドシートの保存オプションを作成する
ドキュメントをスプレッドシートとして保存する必要がある場合は、対応する保存オプションを作成します。
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## ステップ10: 保存パスを準備する
編集したファイルを保存するパスを定義します。
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## ステップ11: 編集したドキュメントを保存する
編集したドキュメントをさまざまな形式で指定されたパスに保存します。
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## ステップ 12: EditableDocument インスタンスを破棄する
最後に、`EditableDocument`インスタンスを作成してリソースを解放します。
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## 結論
GroupDocs.Editor for .NET を使用して DSV ファイルを編集するのは、エディター インスタンスの作成、編集オプションの設定、コンテンツの変更、変更の保存という簡単なプロセスです。このステップ バイ ステップ ガイドは、この機能を .NET アプリケーションに簡単に統合するのに役立ちます。CSV、TSV、またはその他の DSV 形式のいずれを扱う場合でも、GroupDocs.Editor for .NET は堅牢で柔軟なソリューションを提供します。
## よくある質問
### GroupDocs.Editor for .NET を使用して大きな CSV ファイルを編集できますか?
はい、GroupDocs.Editor for .NET は大きな CSV ファイルを効率的に処理できます。
### GroupDocs.Editor for .NET は、CSV と TSV 以外の DSV 形式もサポートしていますか?
はい、適切な区切り文字を指定すれば、さまざまな DSV 形式をサポートします。
### DSV ファイルを保存するときにエンコーディングをカスタマイズすることは可能ですか?
もちろん、保存オプションで希望のエンコードを指定できます。
### GroupDocs.Editor for .NET を使用して CSV ファイルを Excel スプレッドシートに変換できますか?
はい、適切な保存オプションを使用することで、CSV ファイルを Excel スプレッドシートとして保存できます。
### GroupDocs.Editor for .NET に関する詳細なドキュメントはどこで入手できますか?
詳細なドキュメントは以下をご覧ください[ここ](https://reference.groupdocs.com/editor/net/)