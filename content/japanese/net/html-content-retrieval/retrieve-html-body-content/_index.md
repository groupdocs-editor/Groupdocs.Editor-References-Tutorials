---
title: HTML 本文コンテンツを取得する
linktitle: HTML 本文コンテンツを取得する
second_title: GroupDocs.Editor .NET API
description: ステップバイステップ ガイドに従って、GroupDocs.Editor for .NET を使用して HTML 本文コンテンツを取得します。.NET アプリケーションを簡単に強化できます。
weight: 10
url: /ja/net/html-content-retrieval/retrieve-html-body-content/
type: docs
---
# HTML 本文コンテンツを取得する

## 導入
.NET アプリケーションでのドキュメント編集方法に革命を起こす準備はできていますか? GroupDocs.Editor for .NET にお任せください。この強力なツールを使用すると、さまざまなドキュメント形式をアプリケーション内で直接シームレスに編集できます。Word、PDF、HTML のいずれで作業する場合でも、GroupDocs.Editor を使用すると、外部ツールを必要とせずにドキュメントを簡単に編集および操作できます。
## 前提条件
始める前に、いくつかの前提条件を満たす必要があります。
- .NET プログラミングの基礎知識: C# と .NET フレームワークの知識があれば、例を理解するのに役立ちます。
-  GroupDocs.Editor for .NET: からダウンロードできます。[GroupDocs.Editor ダウンロード ページ](https://releases.groupdocs.com/editor/net/).
- 有効なライセンス：ライセンスは、[GroupDocs 購入ページ](https://purchase.groupdocs.com/buy)またはリクエスト[一時ライセンス](https://purchase.groupdocs.com/temporary-license/).
- 統合開発環境 (IDE): 最適な開発エクスペリエンスを得るには Visual Studio が推奨されます。
## 名前空間のインポート
GroupDocs.Editor for .NET を使い始めるには、必要な名前空間をインポートする必要があります。これにより、ドキュメント編集に必要なクラスとメソッドにアクセスできるようになります。
```csharp
using System;
using GroupDocs.Editor.Options;
```
## ステップ1: エディターを初期化する
私たちのプロセスの最初のステップは、`Editor`ドキュメントにクラスを追加します。このクラスは、すべての編集操作のエントリ ポイントです。

編集したい文書を読み込む必要があります。この例では、サンプルの Word 文書を使用します。
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    //次のステップに進む
}
```
## ステップ2: ドキュメントを編集する
次に、`Edit`方法の`Editor`ドキュメントの編集可能なバージョンを作成するためのクラスです。

ドキュメントの編集オプションを指定します。この場合、`WordProcessingEditOptions`.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    //次のステップに進む
}
```
## ステップ3: HTML本文コンテンツを取得する
ここで、ドキュメントの本文コンテンツを HTML 形式で取得します。ここで魔法が起こります。

使用方法`GetBodyContent`この方法では、HTMLの内部コンテンツを抽出できます`<body>`要素。
```csharp
string bodyContent = document.GetBodyContent();
Console.WriteLine("Inner content of the HTML->BODY element: {0}", bodyContent);
```

## 結論
おめでとうございます。GroupDocs.Editor for .NET を使用してドキュメントから HTML 本文コンテンツを取得する方法を学習しました。この強力なライブラリは、.NET アプリケーション内でのドキュメント編集を簡素化し、開発者にとって貴重なツールとなります。
## よくある質問
### GroupDocs.Editor はどのようなファイル形式をサポートしていますか?
GroupDocs.Editor は、Word 文書、PDF、Excel スプレッドシート、PowerPoint プレゼンテーション、HTML ファイルなど、幅広いファイル形式をサポートしています。
### GroupDocs.Editor の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスを申請するには、[GroupDocs 一時ライセンス ページ](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor の無料トライアルはありますか?
はい、無料トライアルは以下からダウンロードできます。[GroupDocs.Editor ダウンロード ページ](https://releases.groupdocs.com/).
### GroupDocs.Editor を .NET Core で使用できますか?
はい、GroupDocs.Editor は .NET Core と互換性があり、最新のアプリケーション開発に柔軟性を提供します。
### GroupDocs.Editor のその他の例やドキュメントはどこで見つかりますか?
より多くの例と詳細なドキュメントについては、[GroupDocs.Editor ドキュメント ページ](https://tutorials.groupdocs.com/editor/net/).