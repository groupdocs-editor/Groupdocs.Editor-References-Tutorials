---
title: HTMLリソースをフォルダーに保存
linktitle: HTMLリソースをフォルダーに保存
second_title: GroupDocs.Editor .NET API
description: Groupdocs.Editor for .NET を使用してドキュメントから HTML リソースを抽出する方法を学習します。この包括的なチュートリアルでは、開発者向けにステップバイステップのガイダンスを提供します。
weight: 13
url: /ja/net/document-editing/save-html-resources-to-folder/
---
## 導入
Groupdocs.Editor for .NET は、開発者が .NET アプリケーション内でドキュメントをシームレスに操作および変換できるようにする強力なツールです。ドキュメントから HTML リソースを抽出する必要がある場合でも、高度な編集タスクを実行する必要がある場合でも、Groupdocs.Editor は直感的な API と広範なドキュメントによってプロセスを簡素化します。
## 前提条件
チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。
1. C# と .NET の基礎知識: 例を理解するには、C# プログラミング言語と .NET フレームワークの知識が不可欠です。
2.  Groupdocs.Editor for .NETライブラリ: Groupdocs.Editor for .NETライブラリを以下のサイトからダウンロードしてインストールします。[Webサイト](https://releases.groupdocs.com/editor/net/).
3. 開発環境: Visual Studio やその他の互換性のある IDE など、好みの開発環境を設定します。

## 名前空間のインポート
まず、C# プロジェクトに必要な名前空間をインポートします。
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##ここで、Groupdocs.Editor for .NET を使用して HTML リソースをフォルダーに保存するプロセスを複数のステップに分解してみましょう。
## ステップ 1: Groupdocs.Editor を初期化する
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
まず、`Editor`サンプル文書へのパスを指定してオブジェクトを作成します。この例ではWord文書を使用しているので、`WordProcessingLoadOptions`ドキュメントの種類として。
## ステップ2: ドキュメントを編集する
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
次に、`EditableDocument`オブジェクトを呼び出すことによって`Edit`方法の`Editor`オブジェクト。これにより、ドキュメントに対して編集操作を実行できます。
## ステップ3: リソースの抽出
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
ドキュメントから画像、フォント、スタイルシートなどのリソースを抽出し、それぞれのリストに保存します。
## ステップ4: 出力フォルダを指定する
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
抽出されたリソースが保存される出力フォルダーを定義します。フォルダー パスは必要に応じてカスタマイズできます。
## ステップ5: リソースを保存する
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
各画像リソースをループし、出力フォルダーに保存し、ファイル名、タイプ、寸法などの関連情報を表示します。
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
同様に、各フォント リソースを出力フォルダーに保存します。
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
最後に、各スタイルシートを出力フォルダーに保存し、編集プロセスを完了します。

## 結論
結論として、Groupdocs.Editor for .NET は、.NET アプリケーション内でプログラムによってドキュメントを管理および操作するための便利なソリューションを提供します。このチュートリアルに従うことで、ドキュメントから HTML リソースを簡単に抽出し、特定の要件に応じてプロセスをカスタマイズできます。
## よくある質問
### Groupdocs.Editor は Word 以外のドキュメント形式とも互換性がありますか?
はい、Groupdocs.Editor は、Excel、PowerPoint、PDF など、幅広いドキュメント形式をサポートしています。
### Groupdocs.Editor を Web アプリケーションに統合できますか?
はい、Groupdocs.Editor は、.NET フレームワークで開発された Web アプリケーションとのシームレスな統合を提供します。
### Groupdocs.Editor はクラウド ストレージ サービスをサポートしていますか?
はい、Groupdocs.Editor は、Google Drive、Dropbox、Microsoft OneDrive などの一般的なクラウド ストレージ サービスとの統合をサポートしています。
### Groupdocs.Editor の無料トライアルはありますか?
はい、Web サイトから Groupdocs.Editor の無料トライアルをご利用いただけます。
### Groupdocs.Editor のテクニカル サポートを受けるにはどうすればよいですか?
技術サポートやコミュニティ サポートについては、Groupdocs.Editor フォーラムをご覧ください。