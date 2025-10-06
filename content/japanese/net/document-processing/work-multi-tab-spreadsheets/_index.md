---
title: 複数タブのスプレッドシートを操作する
linktitle: 複数タブのスプレッドシートを操作する
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor を使用して .NET でマルチタブ スプレッドシートを操作する方法を学びます。ステップ バイ ステップ ガイド、コード例、ベスト プラクティスが含まれています。
weight: 17
url: /ja/net/document-processing/work-multi-tab-spreadsheets/
type: docs
---
# 複数タブのスプレッドシートを操作する

## 導入
複数タブのスプレッドシートの処理は、特に同じドキュメント内の異なるシートからデータを操作または抽出する必要がある場合、非常に困難な作業になることがあります。.NET を使用していて、堅牢なソリューションを探している場合は、GroupDocs.Editor for .NET が最適です。このチュートリアルでは、GroupDocs.Editor for .NET を使用して複数タブのスプレッドシートを操作する手順を説明します。環境の設定から各タブを個別のファイルとして保存するまで、すべてをカバーします。
## 前提条件
チュートリアルに進む前に、次の前提条件が満たされていることを確認してください。
1. Visual Studio: マシンに Visual Studio がインストールされていることを確認します。
2. .NET Framework: GroupDocs.Editor for .NET は、.NET Framework 4.0 以降をサポートしています。
3. GroupDocs.Editor for .NET: GroupDocs.Editor for .NETライブラリをダウンロードしてインストールします。[ダウンロードページ](https://releases.groupdocs.com/editor/net/).
4. ライセンス:[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)ライブラリを試すには、実稼働環境での使用のためにフルライセンスを購入することをお勧めします。
## 名前空間のインポート
コーディングを始める前に、必要な名前空間をインポートする必要があります。.cs ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. 入力ファイルへのパスを取得する
まず、入力スプレッドシート ファイルへのパスを指定する必要があります。このファイルは、複数のタブを持つ XLSX (OOXML) である必要があります。
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. スプレッドシートをエディターインスタンスに読み込む
次に、スプレッドシートを`Editor`インスタンス。これは、ファイル ストリームを使用し、スプレッドシートに適切な読み込みオプションを指定して実行されます。
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        //以降の手順はここを参照してください
    }
}
```
## 3. 最初のタブから編集可能なドキュメントを作成する
特定のタブを編集または操作するには、`EditableDocument`そのタブのインスタンス。タブは 0 から始まるインデックスを使用して指定されます。
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; //最初のタブ
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. 2番目のタブから編集可能なドキュメントを作成する
同様に、`EditableDocument` 2番目のタブ。
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // 2番目のタブ
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. 最初のタブを別のドキュメントに保存する
ここで、最初のタブを別のドキュメントとして保存します。保存形式と出力パスを指定します。
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. 2番目のタブを別のドキュメントに保存する
番目のタブに対しても同じ手順を繰り返しますが、今回は別の形式で保存します。
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. EditableDocumentインスタンスを破棄する
最後に、適切に処分するようにしてください。`EditableDocument`インスタンスを作成してリソースを解放します。
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## 結論
これらの手順に従うと、GroupDocs.Editor を使用して .NET でマルチタブ スプレッドシートを簡単に操作できます。この強力なライブラリにより、スプレッドシート内のさまざまなシートを編集および保存するプロセスが簡素化され、開発タスクの管理が容易になります。複雑なデータ操作でも単純な編集でも、GroupDocs.Editor for .NET は、作業を効率的に行うために必要なツールを提供します。
## よくある質問
### GroupDocs.Editor for .NET とは何ですか?
GroupDocs.Editor for .NET は、開発者が .NET アプリケーション内でさまざまな形式のドキュメントを読み込み、編集、保存できるようにする強力なドキュメント編集 API です。
### 購入前に GroupDocs.Editor for .NET を試すことはできますか?
はい、[無料トライアル](https://releases.groupdocs.com/)またはリクエスト[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)製品を評価するため。
### GroupDocs.Editor for .NET ではどのようなファイル形式がサポートされていますか?
GroupDocs.Editor は、DOCX、XLSX、PPTX、PDF など、幅広い形式をサポートしています。
### GroupDocs.Editor for .NET のサポートを受けるにはどうすればよいですか?
サポートを受けるには、[サポートフォーラム](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET のフル ライセンスはどこで購入できますか?
フルライセンスは以下から購入できます。[購入ページ](https://purchase.groupdocs.com/buy).