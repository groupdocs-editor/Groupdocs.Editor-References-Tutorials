---
title: ドキュメントを読み込む
linktitle: ドキュメントを読み込む
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用してプログラムでドキュメントを編集する方法を学びます。ドキュメントの読み込み、パスワードで保護されたファイルの処理などに関するステップバイステップ ガイドです。
weight: 13
url: /ja/net/document-editing/load-document/
---

# ドキュメントを読み込む

## 導入
プログラムによるドキュメントの編集は、特にさまざまなファイル形式や複雑な構造を扱う場合には、困難な作業になることがあります。幸い、GroupDocs.Editor for .NET では、さまざまなドキュメント タイプを編集するための堅牢で使いやすい API が提供されており、この作業が簡単に行えます。このチュートリアルでは、前提条件、名前空間のインポート方法、さまざまな方法を使用してドキュメントを読み込むための詳細な手順ガイドなど、GroupDocs.Editor for .NET を使い始めるために必要なすべての手順を説明します。
## 前提条件
始める前に、次の前提条件が設定されていることを確認してください。
- Visual Studio: マシンに Visual Studio がインストールされていることを確認します。
- .NET Framework: GroupDocs.Editor for .NET は .NET Framework 2.0 以降をサポートしています。プロジェクトが互換性のあるフレームワークをターゲットにしていることを確認してください。
-  GroupDocs.Editor for .NET: 最新バージョンをダウンロードしてください。[ダウンロードページ](https://releases.groupdocs.com/editor/net/).
- C# の基礎知識: このチュートリアルを実行するには、C# および .NET プログラミングの知識が必要です。
## 名前空間のインポート
GroupDocs.Editor for .NET の使用を開始するには、必要な名前空間をプロジェクトにインポートする必要があります。C# ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
これらの名前空間は、ドキュメント編集タスクに必要なクラスとメソッドへのアクセスを提供します。
## ステップ1: ファイルパスからドキュメントを読み込む
ファイル パスからドキュメントを読み込むのは簡単です。この方法は、マシンにローカルに保存されているドキュメントに最適です。

```csharp
string inputPath = "Your Sample Document";
//パス経由でファイルとしてドキュメントを読み込み、読み込みオプションは使用しません
Editor editor1 = new Editor(inputPath);
//リソースを処分する
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## ステップ2: 読み込みオプションを使用してドキュメントを読み込む
場合によっては、パスワードで保護されたファイルなど、特別な処理が必要なドキュメントをロードする必要があります。このような場合は、ロード オプションを使用できます。

```csharp
string inputPath = "Your Sample Document";
//Word文書の読み込みオプションを作成する
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
//パスと読み込みオプションを使用してドキュメントをファイルとして読み込みます
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
//リソースを処分する
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## ステップ3: バイトストリームからドキュメントを読み込む
バイト ストリームからドキュメントを読み込むことは、データベースや Web サービスから取得されたドキュメントなど、ファイルとして保存されていないドキュメントを処理する必要がある場合に便利です。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
//バイトストリームからコンテンツとしてドキュメントを読み込み、読み込みオプションは使用しません。
Editor editor3 = new Editor(delegate { return inputStream; });
//リソースを処分する
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## ステップ 4: バイト ストリームから読み込みオプションを使用してドキュメントを読み込む
バイト ストリームからロードするときに特別な処理が必要なドキュメントの場合は、バイト ストリームのロードとロード オプションを組み合わせることができます。

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
//スプレッドシートの読み込みオプションを作成する
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
//バイトストリームからコンテンツとしてドキュメントを読み込み、読み込みオプションを指定します。
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
//リソースを処分する
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## 結論
おめでとうございます。GroupDocs.Editor for .NET を使用してさまざまな方法でドキュメントを読み込む方法を学習しました。ローカル ファイル、パスワードで保護されたドキュメント、またはバイト ストリームのいずれを扱う場合でも、GroupDocs.Editor はドキュメント編集のニーズに応える柔軟で強力なソリューションを提供します。アプリケーションで最適なパフォーマンスとリソース管理を確保するには、常にリソースを破棄することを忘れないでください。
## よくある質問
### GroupDocs.Editor for .NET ではどのようなファイル形式がサポートされていますか?
 GroupDocs.Editorは、DOCX、XLSX、PPTX、HTMLなど、幅広いファイル形式をサポートしています。完全なリストについては、[ドキュメンテーション](https://tutorials.groupdocs.com/editor/net/).
### パスワードで保護されたドキュメントをどのように処理すればよいですか?
次のようなロードオプションを使用できます。`WordProcessingLoadOptions`パスワードで保護されたドキュメントを読み込むときにパスワードを指定します。
### GroupDocs.Editor を Web アプリケーションで使用できますか?
はい、GroupDocs.Editor は Web アプリケーションで使用できます。メモリ リークを回避するために、ファイル ストリームとリソースの破棄を適切に処理してください。
### GroupDocs.Editor の一時ライセンスはどこで入手できますか?
臨時免許証は、[一時ライセンスページ](https://purchase.groupdocs.com/temporary-license/).
### 問題が発生した場合、サポートを受けることはできますか?
はい、GroupDocsはサポートを提供しています[サポートフォーラム](https://forum.groupdocs.com/c/editor/20).