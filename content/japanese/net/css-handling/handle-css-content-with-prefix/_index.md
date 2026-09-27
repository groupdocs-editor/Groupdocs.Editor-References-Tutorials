---
date: 2026-09-26
description: この詳細なステップバイステップチュートリアルで、GroupDocs.Editor for .NET を使用して css プレフィックスを処理し、css
  コンテンツを抽出する方法を学びます。
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: プレフィックスで css コンテンツを処理する
og_description: GroupDocs.Editor for .NET を使用して css プレフィックスを処理し、css コンテンツを抽出する方法をご紹介します。ステップバイステップのガイドに従って、css
  リソースに URL を前置し、スタイルシートを取得しましょう。
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: GroupDocs.Editor for .NET で css プレフィックスを処理する方法
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: GroupDocs.Editor for .NET で css プレフィックスを処理する方法
type: docs
url: /ja/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# GroupDocs.Editor for .NETでcssプレフィックスを処理する方法

このチュートリアルでは、GroupDocs.Editor for .NET を使用してドキュメント内のスタイルシートを操作する際の **cssプレフィックスの処理方法** を学びます。画像、フォント、または任意の外部リソースに URL を前置する必要がある場合、以下の手順で **cssプレフィックスの処理方法** と **cssコンテンツの抽出方法** を正確に示します。ガイドの最後までに、リソースパスを書き換え、CSS の生文字列を取得し、確実にウェブワークフローに統合できるようになります。

## クイック回答
- **「handle css prefix」とは何ですか？** CSSで参照される外部リソースにカスタムURLプレフィックスを追加することです。  
- **どの API メソッドが CSS スタイルを返しますか？** `EditableDocument.GetCssContent(...)`。  
- **ライセンスは必要ですか？** トライアルライセンスが利用可能です。商用環境では商用ライセンスが必要です。  
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.5 以上および .NET Core/5/6。  
- **実行時にプレフィックスを変更できますか？** はい – `GetCssContent` に別の文字列を渡すだけです。

## handle css prefix とは何ですか？
この用語は、CSS ファイル内の画像、フォント、または任意の外部アセットの URL を書き換え、CDN やセキュアサーバーなど、管理下の場所を指すようにすることを指します。一貫したベース URL を前置することで、ドキュメントがブラウザやウェブベースのビューアで表示される際に、すべてのリソースが正しく読み込まれることが保証されます。

## GroupDocs.Editor を使用して css コンテンツを抽出する理由
GroupDocs.Editor は、WordProcessing ドキュメントに埋め込まれた元の CSS を読み取り、生のスタイルシート文字列を返し、レンダリングまたは保存前に操作できるようにします。これにより手動でのパースが不要になり、ドキュメント内部表現への忠実性が保証され、**30 以上のファイル形式** をサポートし、**500 MB** までのファイルをメモリに全体をロードせずに処理できます。

## 前提条件
- Visual Studio: Visual Studio の動作するインストールが必要です。  
- .NET Framework: .NET Framework がインストールされていることを確認してください。  
- GroupDocs.Editor for .NET: [GroupDocs.Editor for .NET ダウンロードページ](https://releases.groupdocs.com/editor/net/) からダウンロードできます。  
- Sample Document: 編集用のサンプルドキュメントを用意してください。

## 名前空間のインポート
まず、コードがスムーズに実行できるように必要な名前空間をインポートしましょう。この手順で GroupDocs.Editor のコアクラスにアクセスできます。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 手順 1: エディタの初期化
`Editor` クラスは、GroupDocs.Editor でドキュメントを操作するためのエントリーポイントです。ロード、編集、保存の操作を管理します。  
最初のステップは、サンプルドキュメントで `Editor` インスタンスを作成することです。これにより編集環境が設定されます。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 手順 2: ドキュメントの編集
`EditableDocument` オブジェクトは、ファイルの編集可能なバージョンを表し、CSS、画像、HTML などの内部パーツを公開します。  
次に、`EditableDocument` オブジェクトを取得します。このオブジェクトを使ってドキュメント内部の CSS を操作できます。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 手順 3: 外部プレフィックスの設定
画像とフォントの URL プレフィックスを定義します。これらのプレフィックスは、CSS 内で見つかるすべての画像およびフォント参照の前に付加されます。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 手順 4: プレフィックス付きで css コンテンツを抽出
`GetCssContent` は、指定したプレフィックス付きの URL をすでに含む CSS スタイルシート文字列のコレクションを返します。  
先ほど定義したプレフィックスを渡して `GetCssContent` を呼び出します。このメソッドは、プレフィックス付き URL を含む CSS スタイルシート文字列のリストを返します。

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## 手順 5: 結果の出力
見つかったスタイルシートの数を出力し、各スタイルシートを表示します。これにより、プレフィックスが正しく適用されたことを確認できます。

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## よくある問題と解決策
- **スタイルシートが返されない** – ソースドキュメントに実際に CSS が含まれていることを確認してください（例: スタイル付きテーブルや埋め込み HTML を含む Word 文書）。  
- **URL が正しくない** – プレフィックス文字列がサーバーのルーティングに合わせて適切な区切り文字（`/` または `=`）で終わっているか再確認してください。  
- **パフォーマンスの懸念** – 非常に大きなドキュメントの場合、メモリ使用量が高くなるのを防ぐためにスタイルシートをバッチ処理することを検討してください。

## よくある質問
**Q: GroupDocs.Editor for .NET を他のドキュメント形式でも使用できますか？**  
A: はい、GroupDocs.Editor for .NET は PDF、Word、Excel、PowerPoint など多数の形式をサポートしています。

**Q: GroupDocs.Editor for .NET の無料トライアルは利用できますか？**  
A: もちろんです！[GroupDocs 無料トライアルページ](https://releases.groupdocs.com/) で無料トライアルを開始できます。

**Q: GroupDocs.Editor for .NET の一時ライセンスはどう取得しますか？**  
A: [一時ライセンスページ](https://purchase.groupdocs.com/temporary-license/) から取得できます。

**Q: GroupDocs.Editor for .NET の詳細なドキュメントはどこで見つけられますか？**  
A: 詳細なドキュメントは [GroupDocs.Editor for .NET ドキュメントサイト](https://tutorials.groupdocs.com/editor/net/) にあります。

**Q: GroupDocs.Editor for .NET のサポートオプションは何がありますか？**  
A: [GroupDocs.Editor サポートフォーラム](https://forum.groupdocs.com/c/editor/20) でサポートを受けられます。

## 追加のよくある質問
**Q: CSS を抽出した後にプレフィックスを変更できますか？**  
A: はい。別のプレフィックス文字列で `GetCssContent` を再度呼び出してください。メソッドは常に実行時に渡した値を使用します。

**Q: パスワード保護されたドキュメントでも動作しますか？**  
A: はい。`Editor` インスタンス作成時に `WordProcessingLoadOptions` でパスワードを指定してください。

**Q: 変更した CSS をドキュメントに保存することは可能ですか？**  
A: 現在、GroupDocs.Editor は CSS への読み取り専用アクセスしか提供していません。変更を永続化するには、ドキュメントの基礎となる XML API を使用して元のスタイルシートを置き換える必要があります。

---

**最終更新日:** 2026-09-26  
**テスト環境:** GroupDocs.Editor 23.12 for .NET  
**作者:** GroupDocs

## 関連チュートリアル
- [GroupDocs.Editor .NET を使用して Word ドキュメントから外部 CSS を抽出する&#58; 包括的ガイド](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [GroupDocs.Editor .NET を使用して Word ドキュメントから HTML を抽出＆プレフィックス付与](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [GroupDocs.Editor .NET を使用して Word ドキュメントの HTML コンテンツを抽出・変更する方法](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)