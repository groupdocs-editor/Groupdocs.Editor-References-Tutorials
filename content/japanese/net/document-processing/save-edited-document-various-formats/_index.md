---
title: 編集した文書をさまざまな形式で保存する
linktitle: 編集した文書をさまざまな形式で保存する
second_title: GroupDocs.Editor .NET API
description: この包括的なステップバイステップ ガイドでは、GroupDocs.Editor for .NET を使用して編集したドキュメントをさまざまな形式で保存する方法を学習します。
type: docs
weight: 11
url: /ja/net/document-processing/save-edited-document-various-formats/
---
## 導入
GroupDocs.Editor for .NET を使用して、編集したドキュメントをさまざまな形式で保存したいとお考えですか? 適切な場所に来ました! この包括的なガイドでは、環境の設定から編集したドキュメントを複数の形式で保存するまで、プロセス全体を順を追って説明します。早速、ドキュメントの編集と保存を簡単にしてみましょう!
## 前提条件
始める前に、以下のものを用意してください。
1.  GroupDocs.Editor for .NET - 最新バージョンをダウンロードするには、[ここ](https://releases.groupdocs.com/editor/net/).
2. 開発環境 - Visual Studio またはその他の .NET 互換 IDE。
3. .NET Framework - .NET Framework 4.6.1 以降がインストールされていることを確認してください。
4. サンプル ドキュメント - 作業に使用するサンプルの WordProcessing ドキュメント。
5. 基本的な C# の知識 - C# プログラミングに精通している必要があります。
## 名前空間のインポート
まず、必要な名前空間を C# プロジェクトにインポートしてください。これは、GroupDocs.Editor 機能にアクセスするために重要です。
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
プロセスを管理しやすいステップに分解してみましょう。各部分を理解できるように注意深く進めてください。
## ステップ1: 入力ファイルへのパスを取得する
まず、入力 WordProcessing ファイルへのパスを指定する必要があります。このファイルが読み込まれ、編集されます。
```csharp
string inputFilePath = "Your Sample Document";
```
## ステップ2: ドキュメントの読み込みオプションを作成する
次に、WordProcessing ドキュメントに固有の読み込みオプションを作成します。これらのオプションは、ドキュメントの読み込み方法をカスタマイズするのに役立ちます。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## ステップ3: オプション付きでドキュメントを読み込む
次に、ドキュメントを`Editor`指定されたロード オプションを使用してインスタンスを作成します。
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## ステップ4: 編集オプションを作成する
ドキュメントの編集オプションを準備します。これらのオプションによって、ドキュメントを編集用に開く方法が決まります。
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## ステップ5: 編集用にドキュメントを開く
ドキュメントを開いて編集するには、`EditableDocument`インスタンス。このインスタンスを使用すると、ドキュメントに変更を加えることができます。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## ステップ6: ドキュメントコンテンツを編集する
次に、ドキュメントの内容を編集します。まず、ドキュメントを単一の base64 エンコードされた文字列として取得します。
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
たとえば、ドキュメント内のサブタイトルを変更してみましょう。
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## ステップ 7: 編集したコンテンツから新しい編集可能なドキュメントを作成する
新しいを作成します`EditableDocument`編集されたコンテンツとリソースからのインスタンス。
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## ステップ8: ドキュメントをさまざまな形式で保存する
最後に、サポートされているすべての WordProcessing 形式を反復処理し、編集したドキュメントを各形式で保存します。
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    //保存オプションを準備する
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    //保存パスを準備する
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    //文書を保存する
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## 完了メッセージ
最後に、プロセスが正常に終了したことを示すメッセージを印刷できます。
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## 結論
おめでとうございます。GroupDocs.Editor for .NET を使用して、編集したドキュメントをさまざまな形式で保存する方法を学習しました。この強力なツールを使用すると、数行のコードで簡単にドキュメントを操作し、複数の形式で保存できます。重要な手順は、ドキュメントの読み込み、コンテンツの編集、および目的の形式での保存です。
## よくある質問
### GroupDocs.Editor for .NET とは何ですか?
GroupDocs.Editor for .NET は、.NET アプリケーションを使用してさまざまな形式のドキュメントを編集できる強力な API です。
### GroupDocs.Editor は無料で使用できますか?
はい、無料トライアルでご利用いただけます。ダウンロードしてください[ここ](https://releases.groupdocs.com/).
### GroupDocs.Editor ではどのような形式がサポートされていますか?
GroupDocs.Editor は、DOCX、PDF、HTML など、幅広い形式をサポートしています。
### GroupDocs.Editor の一時ライセンスを取得するにはどうすればよいですか?
臨時免許証を取得できます[ここ](https://purchase.groupdocs.com/temporary-license/).
### 詳細なドキュメントやサポートはどこで入手できますか?
詳細なドキュメントが利用可能[ここ](https://reference.groupdocs.com/editor/net/) 、サポートを受けることができます[ここ](https://forum.groupdocs.com/c/editor/20).