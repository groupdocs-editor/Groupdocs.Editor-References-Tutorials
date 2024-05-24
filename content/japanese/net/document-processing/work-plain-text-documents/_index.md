---
title: プレーンテキスト文書の操作
linktitle: プレーンテキスト文書の操作
second_title: GroupDocs.Editor .NET API
description: ステップバイステップ ガイドを使用して、GroupDocs.Editor for .NET を使用してプレーン テキスト ドキュメントを編集する方法を学びます。.NET ドキュメントの編集プロセスを簡素化します。
type: docs
weight: 15
url: /ja/net/document-processing/work-plain-text-documents/
---
## 導入
.NET でのドキュメント編集プロセスを効率化したいとお考えですか? GroupDocs.Editor for .NET が最適です。この強力な API を使用すると、さまざまなドキュメント形式を簡単に編集できます。このチュートリアルでは、GroupDocs.Editor for .NET を使用してプレーン テキスト ドキュメントを操作する手順を説明します。最後には、テキスト ドキュメントの編集をプロのように扱えるようになります。準備はできましたか? さあ、始めましょう!
## 前提条件
始める前に、いくつか準備しておく必要があります。
- .NET 開発環境: 動作する .NET 開発環境が設定されていることを確認します。Visual Studio が一般的な選択肢です。
-  .NET 用 GroupDocs.Editor: ダウンロードしてインストールします[GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).
- 基本的な C# の知識: C# プログラミング言語に精通していると、例を理解するのに役立ちます。
- テキスト エディター: どのテキスト エディターでもかまいませんが、機能と使いやすさの点から Visual Studio Code が推奨されます。
## 名前空間のインポート
GroupDocs.Editor for .NET の使用を開始するには、必要な名前空間をプロジェクトにインポートする必要があります。これにより、必要なすべてのクラスとメソッドが使用できるようになります。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
プロセスを管理しやすいステップに分解してみましょう。GroupDocs.Editor for .NET を使用してプレーン テキスト ドキュメントを編集する各段階をガイドします。
## ステップ1: 入力TXTファイルへのパスを取得する
まず、入力 TXT ファイルへのパスを指定する必要があります。これは、ローカル ファイルへのパス、またはファイル コンテンツを含むストリームへのパスにすることができます。
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## ステップ2: エディターインスタンスを作成する
次に、`Editor`クラス。このクラスはドキュメントの読み込みと編集を担当します。この段階では読み込みオプションは必要ありません。
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## ステップ3: TXT編集オプションを作成する
次に、TXT 編集オプションを作成します。これらのオプションを使用すると、編集中にテキスト コンテンツをどのように処理するかを指定できます。
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## ステップ4: EditableDocumentインスタンスを作成する
編集オプションを設定したら、`EditableDocument`インスタンス。これは編集可能な形式でドキュメントを表します。
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## ステップ5: ドキュメントコンテンツを編集する
元のテキスト コンテンツを取得して、必要な編集を行います。この例では、「text」という単語を「EDITED text」に置き換えます。
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ステップ 6: 更新されたコンテンツを含む編集可能なドキュメントを作成する
必要な編集を行った後、新しい`EditableDocument`更新されたコンテンツと元のリソースを使用します。
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## ステップ7: WordProcessing保存オプションを作成する
WordProcessing 形式の保存オプションを準備します。この例では、DOCM 形式を使用し、ロケールを指定します。
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## ステップ8: TXT保存オプションを作成する
同様に、TXT 形式の保存オプションを作成します。エンコードが UTF-8 に設定され、テーブル レイアウトが保持されていることを確認します。
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## ステップ9: 出力パスを準備する
結果の DOCX ファイルと TXT ファイルを保存するためのパスを準備します。入力ファイル パスを使用して、出力ディレクトリとファイル名を決定します。
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## ステップ10: 編集した文書を保存する
最後に、指定した保存オプションを使用して、編集したドキュメントを DOCX 形式と TXT 形式の両方で保存します。
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## 結論
おめでとうございます。GroupDocs.Editor for .NET を使用してプレーンテキスト ドキュメントを編集できました。この強力なツールはドキュメント編集を簡素化し、.NET アプリケーションへの統合を容易にします。単純なテキスト ファイルでも複雑なドキュメント形式でも、GroupDocs.Editor なら対応できます。その他の機能や機能については、次の Web サイトをご覧ください。[GroupDocs.Editor ドキュメント](https://reference.groupdocs.com/editor/net/).
## よくある質問
### GroupDocs.Editor for .NET はどのようなファイル形式をサポートしていますか?
 GroupDocs.Editor for .NETは、DOCX、TXT、HTMLなど、幅広いファイル形式をサポートしています。[ドキュメンテーション](https://reference.groupdocs.com/editor/net/)完全なリストについてはこちらをご覧ください。
### GroupDocs.Editor for .NET の無料試用版を入手するにはどうすればよいですか?
 GroupDocs.Editor for .NETの無料トライアルは、[リリースページ](https://releases.groupdocs.com/).
### GroupDocs.Editor for .NET の一時ライセンスを購入できますか?
はい、臨時免許証は[GroupDocs 購入ページ](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor for .NET のサポートはどこで受けられますか?
サポートは以下からご利用いただけます。[GroupDocs.Editor サポート フォーラム](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET の詳細なドキュメントはありますか?
はい、詳細なドキュメントは[GroupDocs.Editor ドキュメント ページ](https://reference.groupdocs.com/editor/net/).