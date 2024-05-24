---
title: ワープロ文書の操作
linktitle: ワープロ文書の操作
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用すると、Word 処理ドキュメントを簡単に編集できます。詳細なステップバイステップのチュートリアルに従って、ドキュメント管理スキルを高めてください。
type: docs
weight: 19
url: /ja/net/document-processing/work-word-processing-documents/
---
## 導入
GroupDocs.Editor for .NET を使用してワード プロセッサ ドキュメントを操作する方法を段階的に説明するこのガイドへようこそ。熟練した開発者でも、初心者でも、このチュートリアルでは、Word ドキュメントを効率的に操作および管理するために必要なすべての情報が提供されます。GroupDocs.Editor for .NET は、複雑なドキュメント編集タスクを処理するために設計された強力なライブラリです。このガイドを読み終えると、.NET アプリケーション内で Word ドキュメントをシームレスに読み込み、編集し、保存できるようになります。
## 前提条件
コーディング手順に進む前に、次の前提条件を満たしていることを確認してください。
1. 開発環境: マシンに .NET 開発環境が設定されていることを確認します。Visual Studio を強くお勧めします。
2.  GroupDocs.Editor for .NET: 最新バージョンをダウンロードしてインストールしてください。[ここ](https://releases.groupdocs.com/editor/net/).
3. ライセンス: 無料トライアルを入手するか、ライセンスを購入してください。[ここ](https://purchase.groupdocs.com/buy)一時ライセンスを申請することもできます[ここ](https://purchase.groupdocs.com/temporary-license/).
4. C# の基礎知識: C# プログラミングの知識があれば、例を理解するのに役立ちます。
## 名前空間のインポート
GroupDocs.Editor for .NET の使用を開始するには、C# コードに必要な名前空間をインポートする必要があります。
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
## ステップ1: 入力ファイルのパスを取得する
まず、入力 Word 文書へのパスを特定します。このチュートリアルでは、サンプルの DOCX ファイルを使用します。
```csharp
string inputFilePath = "YourSampleDocument.docx";
```
## ステップ2: 入力ファイルパスからストリームを作成する
次に、入力ドキュメントを読み取るためのファイル ストリームを作成します。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //次のステップに進む
}
```
## ステップ3: ドキュメントの読み込みオプションを作成する
ドキュメントの読み込みオプションを定義します。ドキュメントがパスワードで保護されている場合は、ここでパスワードを指定します。 
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions
{
    Password = "some_password_to_open_a_document" //オプション（文書が保護されている場合のみ）
};
```
## ステップ4: ドキュメントをエディターインスタンスに読み込む
指定されたオプションでドキュメントをロードするには、Editor インスタンスを使用します。
```csharp
using (Editor editor = new Editor(() => fs, () => loadOptions))
{
    //次のステップに進む
}
```
## ステップ5: 編集オプションを作成する
編集オプションを設定して、ドキュメントの処理方法をカスタマイズします。
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions
{
    FontExtraction = FontExtractionOptions.ExtractEmbeddedWithoutSystem,
    EnableLanguageInformation = true,
    EnablePagination = true
};
```
## ステップ6: 編集可能なドキュメントを作成する
元のドキュメントから中間の EditableDocument を生成します。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    //次のステップに進む
}
```
## ステップ7: テキストコンテンツをHTMLとして抽出する
ドキュメントのテキスト コンテンツとリソースを HTML マークアップとして抽出します。
```csharp
string originalContent = beforeEdit.GetContent();
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## ステップ8: コンテンツを変更する
必要に応じて HTML コンテンツを変更します。この例では、「document」という単語を「edited document」に置き換えます。
```csharp
string editedContent = originalContent.Replace("document", "edited document");
```
## ステップ 9: 編集したコンテンツを含む新しい編集可能なドキュメントを作成する
変更されたコンテンツを使用して新しい EditableDocument インスタンスを作成します。
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(editedContent, allResources))
{
    //ドキュメントの保存に進む
}
```
## ステップ10: ドキュメント保存オプションを作成する
パスワード保護やページ区切りなど、ドキュメントを保存するためのオプションを定義します。
```csharp
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
{
    Password = "password",
    EnablePagination = true,
    Locale = CultureInfo.GetCultureInfo("en-US"),
    OptimizeMemoryUsage = true,
    Protection = new WordProcessingProtection(WordProcessingProtectionType.ReadOnly, "write_password")
};
```
## ステップ11: 編集したドキュメントを保存する
最後に、編集したドキュメントを目的の場所に保存します。
```csharp
string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + ".docm";
string outputPath = Path.Combine("YourOutputDirectory", outputFilename);
using (FileStream outputStream = File.Create(outputPath))
{
    editor.Save(afterEdit, outputStream, saveOptions);
}
Console.WriteLine("Document editing and saving process completed successfully.");
```
## 結論
これで、GroupDocs.Editor for .NET を使用して Word 処理ドキュメントを操作する方法に関する包括的なステップ バイ ステップ ガイドが完了しました。この強力なツールを使用すると、プログラムによるドキュメントの操作と編集が簡単になり、ドキュメント処理ワークフローをカスタマイズするための幅広いオプションが提供されます。
## よくある質問
### GroupDocs.Editor for .NET を使用して他のドキュメント形式を編集できますか?
はい、GroupDocs.EditorはPDF、HTMLなどさまざまなドキュメント形式をサポートしています。[ドキュメンテーション](https://reference.groupdocs.com/editor/net/)サポートされている形式の完全なリストについては、こちらをご覧ください。
### GroupDocs.Editor をライセンスなしで使用することは可能ですか?
無料トライアルを利用するか、一時ライセンスをリクエストすることができます。長期間使用する場合は、ライセンスを購入することをお勧めします。ライセンスを取得する[ここ](https://purchase.groupdocs.com/buy).
### OutOfMemoryException を引き起こす大きなドキュメントをどのように処理すればよいですか?
保存オプションでメモリ最適化を有効にします。`saveOptions.OptimizeMemoryUsage = true;`.
### 保存後にドキュメントをそれ以上編集できないように保護できますか?
はい、次の方法で文書を読み取り専用に設定できます。`WordProcessingProtection`保存オプションで。
### GroupDocs.Editor for .NET のサポートはどこで受けられますか?
ご質問やご不明な点がございましたら、[サポートフォーラム](https://forum.groupdocs.com/c/editor/20).