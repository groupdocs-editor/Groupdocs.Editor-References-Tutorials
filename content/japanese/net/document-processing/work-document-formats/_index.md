---
date: 2026-06-06
description: GroupDocs.Editor for .NET を使用して、サポートされているドキュメント形式を一覧表示し、ファイル形式の拡張子を判定する方法を学びます。ステップバイステップガイドで、code
  snippets、quick answers、FAQs を含みます。
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: サポートされているドキュメント形式の一覧
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor .NET でサポートされているドキュメント形式の一覧
type: docs
url: /ja/net/document-processing/work-document-formats/
weight: 13
---

# サポートされているドキュメント形式の一覧

GroupDocs.Editor for .NET を使用した **サポートされているドキュメント形式の一覧方法** に関する包括的なチュートリアルへようこそ。ドキュメント中心の Web アプリやエンタープライズ向けデスクトップツールを構築する場合でも、編集または変換できる形式を正確に把握しておくことは不可欠です。このガイドでは、形式を列挙し、拡張子を解析し、ドキュメントを編集する方法を学びます—すべて分かりやすい説明とすぐに実行できるコードスニペット付きです。

## クイック回答
- **すべてのサポートされている形式を一覧表示するには？** `DocumentFormatInfo.GetSupportedWordProcessingFormats()`（または Presentation/Spreadsheet の同等メソッド）を使用し、コレクションを反復処理します。  
- **ファイル拡張子から形式を判定できますか？** はい、`DocumentFormatInfo.FromExtension(".docx")` を呼び出します。  
- **GroupDocs.Editor がサポートするファイルタイプは何ですか？** DOCX、XLSX、PPTX、HTML、プレーンテキストなど、30 以上の入力および出力形式をサポートしています。  
- **形式を一覧表示するのにライセンスは必要ですか？** 一時ライセンスを使用するとフル API が利用可能になります。ライセンスがない場合は、機能が制限されたトライアルが動作します。  
- **対応している .NET バージョンはどれですか？** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## 「サポートされているドキュメント形式の一覧」とは何ですか？
このフレーズは、GroupDocs.Editor が開く、編集する、保存できるファイルタイプのコレクションをプログラムで取得することを指します。この操作により、動的な UI ドロップダウンを構築したり、処理前にユーザーのアップロードを検証したりでき、互換性のあるファイルのみがエディタに渡されてさらに操作できるようになります。

## サポートされているドキュメント形式を一覧表示する理由は何ですか？
GroupDocs.Editor は **30 以上の入力および出力形式** をサポートし、**2 GB** までのファイルをメモリに全文読み込まずに処理できます。正確な一覧を把握することで、実行時エラーを防止し、ユーザーエクスペリエンスを向上させ、「編集可能な Office ドキュメントのみを許可する」などのビジネスルールを適用できます。また、アプリケーションが実際にサポートする形式だけをユーザーに提示するのにも役立ちます。

## 前提条件
開始する前に、以下が揃っていることを確認してください：

1. **.NET 開発環境** – Visual Studio 2022 または .NET 6+ をサポートする任意の IDE。  
2. **GroupDocs.Editor for .NET ライブラリ** – [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) からダウンロードしてください。  
3. **一時ライセンス** – 無制限にアクセスできるように、[temporary license](https://purchase.groupdocs.com/temporary-license/) を取得してください。  
4. **基本的な C# の知識** – 名前空間、`using` ステートメント、コンソール出力に慣れていること。

## サポートされているドキュメント形式を一覧表示する方法は？
サポートされている形式のコレクションをロードし、各形式の名前とファイル拡張子を出力します。この 2 段階パターンは Word Processing、Spreadsheet、Presentation のドキュメントで機能します。コレクションを反復処理することで、ドロップダウンなどの UI 要素を動的に生成でき、ユーザーがエディタで実際に扱える形式のみを選択できるようにします。

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Word Processing 形式の一覧表示
`Formats.WordProcessingFormats` は、エディタが認識するすべての Word 処理ファイルタイプを表す列挙型です。`All` プロパティはこれらの形式オブジェクトのコレクションを返します。

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**説明:**  
1. **形式のループ:** 利用可能なすべての Word 処理形式を反復処理します。  
2. **形式の詳細出力:** 各形式について、フレンドリーネームとデフォルトのファイル拡張子を出力します。

### プレゼンテーション形式の一覧表示
`Formats.PresentationFormats` はスライドデックファイルに対して同様に機能し、`All` コレクションを通じてサポートされる各プレゼンテーションタイプを公開します。

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**説明:**  
1. **形式のループ:** プレゼンテーションにも同じループロジックが適用されます。  
2. **形式の詳細出力:** 各形式の名前と拡張子が表示されます。

## ファイル形式の拡張子を判定する方法は？
時にはファイル名だけがあり、対応する `DocumentFormat` を推測する必要があります。GroupDocs.Editor は、ファイル拡張子を内部の形式表現にマッピングするシンプルな静的ヘルパーを提供しており、エディタにロードする前にファイルの検証や変換が可能です。

### スプレッドシート形式の解析
`Formats.SpreadsheetFormats.FromExtension` は、ファイル拡張子文字列を対応するスプレッドシート形式の列挙値に変換します。

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**説明:**  
1. **形式の解析:** `FromExtension` は `.xlsm` 拡張子を内部の `SpreadsheetFormat` 列挙型に変換します。  
2. **形式の出力:** 解析された形式の名前が出力され、マッピングが確認できます。

### テキスト形式の解析
同様に、`Formats.TextualFormats.FromExtension` は HTML や TXT などのテキストファイル拡張子を解決します。

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**説明:**  
1. **形式の解析:** `FromExtension` メソッドは `html` 拡張子を `TextFormat` に解決します。  
2. **形式の出力:** テキスト形式の名前が表示され、Web ベースのエディタで役立ちます。

## 形式を特定した後にドキュメントを編集する方法は？
形式が分かれば、ドキュメントのロードと編集は一貫したパターンで行えます。まず、ソースファイルへのパスで `Editor` インスタンスを作成し、`Edit()` を呼び出して `EditableDocument` を取得します。その後、適切な `SaveOptions` を使用して内容を読み取り、変更し、最終的に保存できます。

### ドキュメントのロード
`Editor` は、特定のファイルに対するすべての編集操作をカプセル化するコアクラスです。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**説明:**  
1. **エディタの初期化:** ターゲットファイルのフルパスを渡して `Editor` インスタンスを作成します。  
2. **Dispose パターン:** `using` ステートメントにより、すべてのアンマネージドリソースが速やかに解放されます。

### コンテンツの抽出
`EditableDocument.GetContent()` は、ドキュメントの生テキスト（Web ベースエディタの場合は HTML）を返し、表示または操作できます。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**説明:**  
1. **Edit メソッド:** `Edit()` は `EditableDocument` オブジェクトを返します。  
2. **コンテンツ取得:** `GetContent()` はドキュメントの生テキスト（または Web ベースエディタの場合は HTML）を抽出します。  
3. **コンテンツ出力:** コンテンツがコンソールに書き出され、検証できます。

### 変更の保存
`SaveOptions` は、編集されたドキュメントをどのように、どの形式でストレージに書き戻すかをエディタに指示します。

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**説明:**  
1. **Edit メソッド:** 変更後に `EditableDocument` を再取得します。  
2. **コンテンツの変更:** 文字列に変更を適用します（ここでは省略）。  
3. **保存オプション:** 希望する出力形式で `SaveOptions` を設定します。  
4. **ドキュメントの保存:** 編集されたファイルをディスクに保存します。

## 異なるドキュメントタイプを扱う方法は？
GroupDocs.Editor は、Word、Spreadsheet、Presentation の取り扱いを同一 API で抽象化しているため、各ドキュメントファミリごとに新しいクラスを学習することなく、コンテキストを簡単に切り替えられます。

### スプレッドシートドキュメントの編集
`SpreadsheetSaveOptions` は、スプレッドシートの書き込み方法（形式やオプションの圧縮設定など）を定義します。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**説明:**  
1. **エディタの初期化:** スプレッドシートファイルのパスを `Editor` コンストラクタに渡します。  
2. **Edit メソッド:** `EditableDocument` を取得します。  
3. **コンテンツ取得:** スプレッドシートの CSV 表現（または HTML）を出力します。  
4. **コンテンツの変更:** 必要なセルレベルの変更を適用します。  
5. **保存オプション:** 適切な `SpreadsheetSaveOptions` を選択します。  
6. **ドキュメントの保存:** 更新されたスプレッドシートをストレージに書き戻します。

### プレゼンテーションドキュメントの編集
`PresentationSaveOptions` はスライドデックの出力形式を制御し、元のファイルタイプを保持したり変更したりできます。

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**説明:**  
1. **エディタの初期化:** `Editor` を使用して PowerPoint ファイルをロードします。  
2. **Edit メソッド:** `EditableDocument` を取得します。  
3. **コンテンツ取得:** スライドの HTML またはプレーンテキストを抽出します。  
4. **コンテンツの変更:** タイトル、箇条書き、画像などを更新します。  
5. **保存オプション:** `PresentationSaveOptions` を使用して出力形式を定義します。  
6. **ドキュメントの保存:** 編集されたプレゼンテーションを保存します。

## 一般的な問題と解決策
- **“Format not supported” エラー:** 最新の GroupDocs.Editor バージョンを使用しているか確認してください。新しい Office 形式のサポートが定期的に追加されます。  
- **大きなファイルのメモリ消費:** ドキュメントをロードする前に `EditorSettings.EnableStreaming = true` を設定してストリーミングモードを有効にします。  
- **ライセンスが適用されていない:** 一時ライセンスファイルがアプリケーションのルートに配置されているか、`License license = new License(); license.SetLicense("path/to/license.lic");` でロードされていることを確認してください。

## よくある質問
**Q: `DocumentFormatInfo` と `SaveOptions` の違いは何ですか？**  
**A:** `DocumentFormatInfo` はサポートされているファイルタイプのメタデータを提供し、`SaveOptions` はドキュメントをディスクに書き戻す方法（形式、圧縮など）を構成します。

**Q: カスタムファイル拡張子の形式を一覧表示できますか？**  
**A:** はい、`DocumentFormatInfo.FromExtension("yourExt")` を使用します。拡張子が認識されない場合、メソッドは `null` を返します。

**Q: GroupDocs.Editor はパスワードで保護されたファイルをサポートしていますか？**  
**A:** もちろんです。`EditorSettings` を介してパスワードを `Editor` コンストラクタに渡すことで、暗号化されたドキュメントを開くことができます。

**Q: GroupDocs.Editor は実際に何種類の形式をサポートしていますか？**  
**A:** 30 以上の入力および出力形式をサポートしており、Word、Excel、PowerPoint、HTML、プレーンテキストにまたがります。

**Q: 編集可能な形式だけに一覧を絞る方法はありますか？**  
**A:** `GetEditableWordProcessingFormats()`（または Spreadsheet/Presentation の同等メソッド）を使用して、完全な編集機能が可能な形式だけを取得します。

## 追加リソース
- [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) からライブラリをダウンロードしてください。  
- フル機能にアクセスするには、[temporary license](https://purchase.groupdocs.com/temporary-license/) を取得してください。  
- [free trial](https://releases.groupdocs.com/) で製品をお試しください。  
- [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/) で詳細な使用例を確認してください。  
- [support forum](https://forum.groupdocs.com/c/editor/20) でコミュニティからサポートを受け取れます。

## 結論
このガイドに従うことで、**サポートされているドキュメント形式の一覧表示**、**拡張子からファイル形式を判定**、および **Word、Spreadsheet、Presentation の各タイプのドキュメントを編集** する方法が分かります。これらのスニペットをプロジェクトに組み込むことで、エンドユーザーに喜ばれ、実行時エラーを減らす、堅牢で形式に対応したアプリケーションを構築できます。

---

**最終更新日:** 2026-06-06  
**テスト環境:** GroupDocs.Editor 23.9 for .NET  
**作者:** GroupDocs

## 関連チュートリアル
- [GroupDocs.Editor を使用した .NET のドキュメントロードのマスタリング：包括的ガイド](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [GroupDocs.Editor を使用した .NET のマスタードキュメント編集：包括的ガイド](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [GroupDocs.Editor .NET を使用した Word から HTML への変換：ステップバイステップガイド](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)