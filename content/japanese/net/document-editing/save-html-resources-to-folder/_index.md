---
date: 2026-05-12
description: GroupDocs.Editor for .NET を使用して、ドキュメントからフォントやその他の HTML リソースを抽出する方法を学びます。.NET
  開発者向けのステップバイステップガイドです。
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTMLリソースをフォルダーに保存
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: フォントを抽出し、HTMLリソースをフォルダーに保存する方法
type: docs
url: /ja/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# フォントを抽出し、HTMLリソースをフォルダーに保存する方法

## はじめに
GroupDocs.Editor for .NET は、ドキュメントを HTML に変換しながら、**フォントの抽出方法**やその他のアセットを取得できるようにします。数行の C# で画像、スタイルシート、フォントファイルを抽出し、任意のフォルダーに保存できます。このチュートリアルでは、エディタの初期化から各リソースのディスクへの保存まで、全体のワークフローを順を追って説明します。

## クイック回答
- **「フォントの抽出方法」とは何ですか？** HTML 変換中にソースドキュメントから埋め込まれたフォントファイルを取得するプロセスです。  
- **どのライブラリがこれを処理しますか？** GroupDocs.Editor for .NET は、フォント、画像、スタイルシートの抽出用に専用の API を提供します。  
- **ライセンスは必要ですか？** 無料トライアルが利用可能です。商用利用には商用ライセンスが必要です。  
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7。  
- **カスタムフォルダーを指定できますか？** はい、抽出されたリソースを保存する際に書き込み可能な任意のパスを指定できます。

## 「フォントの抽出方法」とは何ですか？
**フォントの抽出方法** は、ソースドキュメント（例: DOCX、PPTX）に埋め込まれた元のフォントファイルを取得し、生成された HTML から参照できるようにすることを指します。これにより、システムフォントに依存せず、ブラウザでテキストが意図した通りに正確に表示されます。

## HTML リソース抽出に GroupDocs.Editor を使用する理由
GroupDocs.Editor は **50 以上の入力および出力フォーマット**（DOCX、PPTX、PDF、HTML など）をサポートし、**最大 300 ページ**までのドキュメントをファイル全体をメモリに読み込まずに処理できます。API はフォント、画像、CSS を一括で抽出し、手動での解析に比べて開発時間を最大 **70 %** 短縮します。

## 前提条件
チュートリアルに入る前に、以下の前提条件を満たしていることを確認してください：

1. **C# と .NET の基本知識** – C# プログラミング言語と .NET フレームワークに慣れていることが、例題を進める上で必須です。  
2. **GroupDocs.Editor for .NET ライブラリ** – [website](https://releases.groupdocs.com/editor/net/) から GroupDocs.Editor for .NET ライブラリをダウンロードしてインストールしてください。  
3. **開発環境** – Visual Studio など、お好みの開発環境や互換性のある IDE を設定してください。

## 名前空間のインポート
To get started, import the necessary namespaces in your C# project:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## フォントを抽出し、HTML リソースをフォルダーに保存する方法
ソースドキュメントを `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` でロードし、`editor.Save("output.html", SaveOptions.Html);` を呼び出します。保存操作の後、`Resources` コレクションには抽出されたすべてのアセット（フォントを含む）が含まれ、これを反復処理してディスクに書き込むことができます。このワンステップのアプローチは、変換とリソース抽出の両方を自動的に処理します。

## 手順 1: GroupDocs.Editor の初期化
`Editor` は、ドキュメントのロード、変換、リソース抽出を統括するコアクラスです。メモリ内で単一のドキュメントセッションを表します。

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
まず、サンプルドキュメントへのパスを指定して `Editor` オブジェクトを初期化します。この例では Word ドキュメントを使用するため、`WordProcessingLoadOptions` をドキュメントタイプとして指定します。

## 手順 2: ドキュメントの編集
`EditableDocument` は `Edit` メソッドが返す編集可能な表現で、保存前にドキュメントを操作できます。

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
次に、`Editor` オブジェクトの `Edit` メソッドを呼び出して `EditableDocument` オブジェクトを作成します。これにより、ドキュメントに対して編集操作を実行できます。

## 手順 3: リソースの抽出
`Resources` は抽出されたアセット（画像、フォント、スタイルシート）を個別のリストにまとめたコレクションで、扱いやすくなっています。

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
ドキュメントから画像、フォント、スタイルシートなどのリソースを抽出し、各リストに格納します。

## 手順 4: 出力フォルダーの指定
`outputFolder` は抽出されたファイルを書き込む場所を定義する文字列です。サーバーやローカルマシン上の書き込み可能な任意のディレクトリを指定できます。

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
抽出されたリソースを保存する出力フォルダーを定義します。必要に応じてフォルダーパスをカスタマイズできます。

## 手順 5: リソースの保存
`SaveResource` は単一のバイナリリソース（画像、フォント、またはスタイルシート）をファイルシステムに書き込むヘルパー関数です。

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
各画像リソースをループ処理し、出力フォルダーに保存するとともに、ファイル名、タイプ、サイズなどの関連情報を表示します。

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
同様に、各フォントリソースを出力フォルダーに保存します。

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

## よくある問題と解決策
- **変換後にフォントが欠落する** – ソースドキュメントが実際にフォントを埋め込んでいることを確認してください。埋め込まれていない場合、GroupDocs.Editor はシステムフォントのみを参照できます。  
- **アクセス拒否エラー** – アプリケーションプロセスが対象の出力フォルダーに書き込み権限を持っていることを確認してください。  
- **大きなドキュメントでメモリ使用量が増加する** – `LoadOptions` に `LoadMode = LoadMode.Stream` を使用して、ファイル全体をメモリに読み込むのではなくストリーミングしてください。

## よくある質問

**Q: GroupDocs.Editor は Word 以外のドキュメント形式にも対応していますか？**  
A: はい、Excel、PowerPoint、PDF、HTML を含む 50 以上の追加形式に対応し、編集およびリソース抽出の両方が可能です。

**Q: GroupDocs.Editor を Web アプリケーションに統合できますか？**  
A: もちろんです。API は ASP.NET Core、MVC、Web API プロジェクトとシームレスに連携し、サーバー側でドキュメントを処理できます。

**Q: GroupDocs.Editor はクラウドストレージ統合を提供していますか？**  
A: はい、Google Drive、Dropbox、OneDrive、Amazon S3 用の組み込みコネクタが含まれており、クラウド上のドキュメントを直接ロード・保存できます。

**Q: GroupDocs.Editor の無料トライアルはありますか？**  
A: クレジットカード不要で、GroupDocs のウェブサイトから 30 日間のフル機能トライアルをダウンロードできます。

**Q: 抽出に関する技術サポートはどのように受けられますか？**  
A: 公式フォーラムでサポートチームに問い合わせるか、カスタマーポータルからチケットを提出するか、詳細な API ドキュメントをご参照ください。

---

**最終更新日:** 2026-05-12  
**テスト環境:** GroupDocs.Editor 23.11 for .NET  
**作成者:** GroupDocs

## 関連チュートリアル

- [GroupDocs.Editor .NET を使用した効率的なドキュメント編集：HTML を編集可能なドキュメントに変換](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [GroupDocs.Editor .NET を使用した DOCX リソースの効率的な抽出と保存 - 完全ガイド](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [GroupDocs.Editor .NET でドキュメント編集と変換をマスターする：完全ガイド](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)