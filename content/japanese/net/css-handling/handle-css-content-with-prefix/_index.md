---
date: 2026-03-06
description: この詳細なステップバイステップチュートリアルで、プレフィックス付きCSSコンテンツの扱い方と、GroupDocs.Editor for .NET
  を使用したCSSコンテンツの抽出方法を学びましょう。
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: プレフィックスでCSSコンテンツを処理する
type: docs
url: /ja/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# プレフィックス付き CSS コンテンツの処理

このチュートリアルでは、GroupDocs.Editor for .NET を使用してドキュメント内のスタイルシートを扱う際の **css プレフィックスの処理方法** を学びます。画像、フォント、または任意の外部リソースに URL を前置する必要がある場合、以下の手順で **css プレフィックスの処理方法** と **css コンテンツの抽出方法** を正確に示します。

## クイック回答
- **“handle css prefix” とは何ですか？** CSS で参照される外部リソースにカスタム URL プレフィックスを追加することです。
- **どの API メソッドが CSS スタイルを返しますか？** `EditableDocument.GetCssContent(...)`。
- **ライセンスは必要ですか？** トライアルライセンスが利用可能です。商用環境では商用ライセンスが必要です。
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.5 以上、および .NET Core/5/6。
- **実行時にプレフィックスを変更できますか？** はい – `GetCssContent` に別の文字列を渡すだけです。

## **handle css prefix** とは何ですか？
CSS リソースにプレフィックスを適用すると、画像、フォント、その他のアセットのパスが書き換えられ、制御下の場所（例: CDN やセキュアサーバー）を指すようになります。これは、ドキュメントをエクスポートし、すべての外部参照がウェブアプリケーションからアクセス可能である必要がある場合に特に有用です。

## **extract css content** に GroupDocs.Editor を使用する理由
GroupDocs.Editor は WordProcessing ドキュメントに埋め込まれた元の CSS を読み取り、未加工のスタイルシート文字列を取得し、レンダリングや保存前に操作できるようにします。これにより手動でのパースが不要になり、抽出された CSS がドキュメントの内部表現と一致することが保証されます。

## 前提条件
開始する前に、以下の前提条件が整っていることを確認してください：
- Visual Studio: 動作する Visual Studio がインストールされている必要があります。  
- .NET Framework: .NET Framework がインストールされていることを確認してください。  
- GroupDocs.Editor for .NET: こちらからダウンロードできます [here](https://releases.groupdocs.com/editor/net/)。  
- Sample Document: 編集用のサンプルドキュメントを用意してください。

## 名前空間のインポート
まず、コードがスムーズに実行できるように必要な名前空間をインポートしましょう。この手順で GroupDocs.Editor のコアクラスにアクセスできます。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## 手順 1: エディタの初期化
最初の手順では、サンプルドキュメントを使用して `Editor` インスタンスを作成します。これにより編集環境が設定されます。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## 手順 2: ドキュメントの編集
次に、`EditableDocument` オブジェクトを取得します。このオブジェクトはファイルの編集可能なバージョンを表し、内部パーツに対して操作できるようにします。

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## 手順 3: 外部プレフィックスの設定
画像とフォントの URL プレフィックスを定義します。これらのプレフィックスは CSS 内で見つかるすべての画像およびフォント参照の先頭に付加されます。

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## 手順 4: プレフィックス付き **Extract CSS content**
`GetCssContent` を呼び出し、先ほど定義したプレフィックスを渡します。このメソッドは、プレフィックス付き URL がすでに含まれた CSS スタイルシート文字列のリストを返します。

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
- **URL が正しくない** – プレフィックス文字列がサーバーのルーティングに適した区切り文字（`/` または `=`）で終わっているか再確認してください。
- **パフォーマンスの懸念** – 非常に大きなドキュメントの場合、メモリ使用量を抑えるためにスタイルシートをバッチ処理することを検討してください。

## 結論
GroupDocs.Editor for .NET を使用したプレフィックス付き CSS コンテンツの処理はシンプルで強力です。これらの手順に従うことで **handle css prefix** を行い、**extract css content** によって未加工の CSS を取得し、外部リソースをウェブワークフローにシームレスに統合できます。HTML 変換、画像抽出、ドキュメント結合など、他の GroupDocs.Editor 機能も探索して、API からさらに価値を引き出しましょう。

## FAQ
### GroupDocs.Editor for .NET を他のドキュメント形式で使用できますか？
はい、GroupDocs.Editor for .NET は PDF、Word、Excel など、さまざまなドキュメント形式をサポートしています。

### GroupDocs.Editor for .NET の無料トライアルは利用可能ですか？
もちろんです！無料トライアルは [here](https://releases.groupdocs.com/) から開始できます。

### GroupDocs.Editor for .NET の一時ライセンスはどう取得しますか？
一時ライセンスは [here](https://purchase.groupdocs.com/temporary-license/) から取得できます。

### GroupDocs.Editor for .NET の詳細ドキュメントはどこで見つけられますか？
詳細なドキュメントは [here](https://tutorials.groupdocs.com/editor/net/) で利用できます。

### GroupDocs.Editor for .NET のサポートオプションは何がありますか？
サポートは [here](https://forum.groupdocs.com/c/editor/20) で受けられます。

## 追加のよくある質問

**Q: CSS を抽出した後にプレフィックスを変更できますか？**  
A: はい。別のプレフィックス文字列で `GetCssContent` を再度呼び出してください。メソッドは常に実行時に渡した値を使用します。

**Q: パスワード保護されたドキュメントでも動作しますか？**  
A: はい。`Editor` インスタンスを作成する際に `WordProcessingLoadOptions` でパスワードを指定してください。

**Q: 変更した CSS をドキュメントに保存できますか？**  
A: 現在、GroupDocs.Editor は CSS への読み取り専用アクセスのみを提供しています。変更を永続化するには、ドキュメントの基礎となる XML API を使用して元のスタイルシートを置き換える必要があります。

---

**最終更新日:** 2026-03-06  
**テスト環境:** GroupDocs.Editor 23.12 for .NET  
**作者:** GroupDocs