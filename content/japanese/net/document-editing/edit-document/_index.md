---
title: ドキュメントを編集
linktitle: ドキュメントを編集
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用してドキュメントを簡単に編集する方法を学びます。ワード プロセッサおよびスプレッドシート ファイルのステップ バイ ステップ ガイド。
type: docs
weight: 11
url: /ja/net/document-editing/edit-document/
---
## 導入
.NET アプリケーション内でのドキュメント編集の複雑さに悩まされたことはありませんか? 心配はいりません! GroupDocs.Editor for .NET は、この作業を簡素化する強力なツールです。この包括的なガイドでは、この強力なツールを活用してドキュメントを簡単に編集する方法を説明します。ワープロ ドキュメントでもスプレッドシートでも、このチュートリアルを最後まで読めば、GroupDocs.Editor をプロのように使いこなせるようになります。
## 前提条件
チュートリアルに進む前に、次のものを用意してください。
- Visual Studio: インストールされ、準備完了です。
- .NET Framework: システムにインストールされている互換性のあるバージョン。
-  GroupDocs.Editor for .NET: 次のようなことができます[最新バージョンをダウンロード](https://releases.groupdocs.com/editor/net/)そして、[一時ライセンス](https://purchase.groupdocs.com/temporary-license/)必要に応じて。
- C# の基礎知識: このガイドでは、C# および .NET 開発の基礎知識があることを前提としています。
## 名前空間のインポート
まず、必要な名前空間をプロジェクトにインポートする必要があります。C# ファイルの先頭に次の行を追加します。
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.Options;
```
準備が完了したら、ドキュメント編集プロセスを管理しやすいステップに分解してみましょう。
## ステップ1: ワードプロセッサ文書を読み込む
まず、Word Processing ドキュメントを読み込みます。ここで、エディター インスタンスをドキュメントの場所へポイントし、必要に応じて読み込みオプションを指定します。
### 1.1 デフォルトオプションでエディターを初期化する
```csharp
string inputFilePath = "Your Sample Document"; //ドキュメントへのパス
Editor editor1 = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
```
このコード スニペットは、Word Processing ドキュメントの既定の読み込みオプションを使用して、エディター インスタンスを初期化します。
## ステップ2: ドキュメントを編集する
これで、読み込んだドキュメントの編集に進むことができます。GroupDocs.Editor を使用すると、ニーズに合わせて編集オプションをカスタマイズできます。
### 2.1 デフォルトオプションで編集する
```csharp
EditableDocument defaultWordProcessingDoc = editor1.Edit();
```
デフォルトのオプションを使用してドキュメントを編集するのは簡単で、最小限の設定が必要です。
### 2.2 カスタムオプションで編集する
カスタム編集オプションを指定して、より高度な構成について詳しく見ていきましょう。
```csharp
WordProcessingEditOptions wordProcessingEditOptions1 = new WordProcessingEditOptions();
wordProcessingEditOptions1.EnablePagination = false;
wordProcessingEditOptions1.EnableLanguageInformation = true;
wordProcessingEditOptions1.FontExtraction = FontExtractionOptions.ExtractAllEmbedded;
EditableDocument version1WordProcessingDoc = editor1.Edit(wordProcessingEditOptions1);
```
このスニペットでは、ページ区切りを無効にし、言語情報を有効にし、埋め込まれたすべてのフォントを抽出するようにフォント抽出を設定しました。
### 2.3 別の構成例
異なるオプションセットを使用してドキュメントを編集することもできます。
```csharp
WordProcessingEditOptions wordProcessingEditOptions2 = new WordProcessingEditOptions(true);
wordProcessingEditOptions2.FontExtraction = FontExtractionOptions.ExtractAll;
EditableDocument version2WordProcessingDoc = editor1.Edit(wordProcessingEditOptions2);
```
ここでは、ページ区切りを有効にし、すべてのフォントを抽出するようにフォント抽出を設定しました。
## ステップ3: スプレッドシートを読み込んで編集する
GroupDocs.Editor を使用すると、スプレッドシートの編集も同様に簡単です。
### 3.1 スプレッドシートを読み込む
```csharp
Editor editor2 = new Editor("Your Sample Document", delegate { return new SpreadsheetLoadOptions(); });
```
これは、スプレッドシート ドキュメントの Editor インスタンスを初期化します。
### 3.2 最初のタブを編集する
```csharp
SpreadsheetEditOptions sheetTab1EditOptions = new SpreadsheetEditOptions();
sheetTab1EditOptions.WorksheetIndex = 0; //インデックスは0から始まるので、これが最初のタブです
EditableDocument firstTab = editor2.Edit(sheetTab1EditOptions);
```
指定されたオプションを使用して、スプレッドシートの最初のタブを編集できます。
### 3.3 2番目のタブを編集する
```csharp
SpreadsheetEditOptions sheetTab2EditOptions = new SpreadsheetEditOptions();
sheetTab2EditOptions.WorksheetIndex = 1; //インデックスは0から始まるので、これは2番目のタブです
EditableDocument secondTab = editor2.Edit(sheetTab2EditOptions);
```
同様に、このコード スニペットはスプレッドシートの 2 番目のタブを編集します。
## ステップ4: コンテンツの抽出
ドキュメントを編集したら、そのコンテンツを抽出する必要がある場合があります。GroupDocs.Editor には、このためのさまざまなメソッドが用意されています。
### 4.1 HTMLコンテンツを取得する
```csharp
string bodyContent = firstTab.GetBodyContent(); //HTML->BODY要素内からのHTMLマークアップ
string allContent = firstTab.GetContent(); //HTML->HEAD ヘッダーとその内容を含む、すべてのドキュメントの完全な HTML マークアップ
```
このコードは、編集されたドキュメントの HTML コンテンツを抽出します。
### 4.2 リソースの抽出
```csharp
List<IImageResource> onlyImages = firstTab.Images;
List<IHtmlResource> allResourcesTogether = firstTab.AllResources;
```
ここで、ドキュメントから画像やその他のすべての HTML リソースを抽出できます。
## ステップ5: クリーンアップ
リソースを解放するために、すべてのインスタンスを破棄することを忘れないでください。
```csharp
defaultWordProcessingDoc.Dispose();
version1WordProcessingDoc.Dispose();
version2WordProcessingDoc.Dispose();
firstTab.Dispose();
secondTab.Dispose();
editor1.Dispose();
editor2.Dispose();
```
適切に破棄することで、アプリケーションでメモリ リークやパフォーマンスの問題が発生しなくなります。
## 結論
おめでとうございます。これで、GroupDocs.Editor for .NET を使用して、ワード プロセッサ ドキュメントやスプレッドシートからコンテンツを読み込み、編集し、抽出する方法をしっかりと理解できました。この強力なツールは、ドキュメント編集タスクを簡素化し、.NET アプリケーションとシームレスに統合します。詳細については、[ドキュメンテーション](https://reference.groupdocs.com/editor/net/), [最新バージョンをダウンロード](https://releases.groupdocs.com/editor/net/) 、または取得する[一時ライセンス](https://purchase.groupdocs.com/temporary-license/).
## よくある質問
### GroupDocs.Editor for .NET で PDF ドキュメントを編集できますか?
現在、GroupDocs.Editor for .NET は主にワード プロセッサ、スプレッドシート、プレゼンテーション形式をサポートしています。
### 大きな文書を効率的に処理するにはどうすればよいですか?
編集オプションを利用して、ドキュメントの必要な部分のみを読み込んで処理し、インスタンスを適切に破棄してメモリを管理するようにします。
### 編集できるドキュメントのサイズに制限はありますか?
厳密なサイズ制限はありませんが、パフォーマンスはシステムの機能によって異なります。
### HTML 出力をさらにカスタマイズできますか?
はい、GroupDocs.Editor では、さまざまなオプションと設定を通じて HTML 出力を広範囲にカスタマイズできます。
### 問題が発生した場合、どこでサポートを受けることができますか?
訪問することができます[GroupDocs.Editor サポート フォーラム](https://forum.groupdocs.com/c/editor/20)助けと援助を求めて。