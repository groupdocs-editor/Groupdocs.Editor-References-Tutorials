---
title: プレフィックス付きのHTMLコンテンツを取得する
linktitle: プレフィックス付きのHTMLコンテンツを取得する
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用して、画像とスタイルシートのカスタム プレフィックスを使用してドキュメントから HTML コンテンツを取得する方法を学びます。ステップ バイ ステップ ガイドが含まれています。
type: docs
weight: 11
url: /ja/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## 導入
GroupDocs.Editor for .NET を使用してドキュメントから HTML コンテンツを取得する方法についてのステップバイステップのチュートリアルへようこそ。熟練した開発者でも、初心者でも、このガイドではプロセスをわかりやすく説明します。環境の設定からコードの正常な実行まで、知っておく必要のあるすべてのことを説明します。さあ、始めましょう!
## 前提条件
始める前に、次の前提条件が満たされていることを確認してください。
1.  GroupDocs.Editor for .NET: 最新バージョンをダウンロードしてください。[ダウンロードページ](https://releases.groupdocs.com/editor/net/).
2. 開発環境: Visual Studio またはその他の推奨される .NET 開発環境。
3. C# の基礎知識: C# プログラミングの知識があれば、例を理解するのに役立ちます。
4. 編集するドキュメント: Word ドキュメントなどのテスト用のサンプル ドキュメントを用意します。
5. .NET Framework: マシンに .NET Framework がインストールされていることを確認します。
準備が整ったので、始めましょう!
## 名前空間のインポート
まず、C# プロジェクトに必要な名前空間をインポートする必要があります。これらの名前空間は、GroupDocs.Editor for .NET を操作するために必要なクラスとメソッドを提供します。
```csharp
using System;
using GroupDocs.Editor.Options;
```
名前空間をインポートしたら、エディターの設定に進むことができます。
## ステップ1: エディターを初期化する
まず、初期化する必要があります`Editor`クラスをドキュメントに追加します。この手順では、編集するドキュメントを指定し、必要な読み込みオプションを指定します。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //さらなる手順はここに追加されます
}
```
この例では、Word文書を読み込んでいます。`"Your Sample Document"`ドキュメントへのパスを入力します。
## ステップ2: ドキュメントを編集する
次に、ドキュメントを開いて編集します。これは、`Edit`方法の`Editor`クラスでは、`WordProcessingEditOptions`議論として。
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //さらなる手順はここに追加されます
}
```
の`EditableDocument`インスタンスは編集可能な形式でドキュメントを表します。これで HTML コンテンツを取得する準備が整いました。
## ステップ3: カスタムプレフィックスを定義する
画像と CSS にカスタム プレフィックスを追加するには、プレフィックスを文字列として定義する必要があります。この手順により、HTML コンテンツに外部リソースの指定されたプレフィックスが確実に含まれるようになります。
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
URL を希望のプレフィックスに置き換えることができます。これらのプレフィックスは、次の手順で HTML 出力をカスタマイズするために使用されます。
## ステップ4: HTMLコンテンツを取得する
プレフィックスが設定されたので、ドキュメントからHTMLコンテンツを取得できます。`GetContent`方法の`EditableDocument`クラスを使用すると、画像と CSS プレフィックスを指定できます。
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
このコード スニペットは、カスタム プレフィックス付きの HTML コンテンツを取得し、コンソールに出力します。必要に応じて、この HTML コンテンツをさらに処理したり保存したりできます。
## 結論
これで完了です。これらの手順に従うと、GroupDocs.Editor for .NET を使用して、画像やスタイルシートのカスタム プレフィックスを備えたドキュメントから HTML コンテンツを簡単に取得できます。この強力なツールにより、ドキュメントの操作が簡素化され、ドキュメント編集を .NET アプリケーションにシームレスに統合することに集中できます。
詳しい情報については、[.NET ドキュメント用の GroupDocs.Editor](https://reference.groupdocs.com/editor/net/)ご質問やさらなるサポートが必要な場合は、お気軽にお問い合わせください。[サポートフォーラム](https://forum.groupdocs.com/c/editor/20).
## よくある質問
### GroupDocs.Editor for .NET で編集できるドキュメントの種類は何ですか?
GroupDocs.Editor は、Word、Excel、PowerPoint、PDF など、さまざまなドキュメント形式をサポートしています。
### GroupDocs.Editor for .NET の無料試用版を入手するにはどうすればよいですか?
無料トライアルは[GroupDocsウェブサイト](https://releases.groupdocs.com/).
### HTML コンテンツをさらにカスタマイズできますか?
はい、取得した HTML コンテンツをレンダリングまたは保存する前に、必要に応じて変更できます。
### GroupDocs.Editor for .NET を他の .NET 言語で使用することは可能ですか?
はい、VB.NET や F# などの .NET 互換言語で使用できます。
### GroupDocs.Editor for .NET の一時ライセンスを取得するにはどうすればよいですか?
臨時免許証は[購入ページ](https://purchase.groupdocs.com/temporary-license/).