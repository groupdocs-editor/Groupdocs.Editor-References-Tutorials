---
title: パスワードで保護されたスプレッドシートを操作する
linktitle: パスワードで保護されたスプレッドシートを操作する
second_title: GroupDocs.Editor .NET API
description: GroupDocs.Editor for .NET を使用して、パスワードで保護されたスプレッドシートを処理する方法を学びます。この詳細なガイドでは、安全な Excel ファイルを開いて保存するまでの手順を説明します。
weight: 18
url: /ja/net/document-processing/work-password-protected-spreadsheets/
type: docs
---
# パスワードで保護されたスプレッドシートを操作する

## 導入
.NET アプリケーションでパスワード保護されたスプレッドシートを管理するのに苦労していませんか? もしそうなら、ここが最適な場所です! この包括的なガイドでは、GroupDocs.Editor for .NET を使用してパスワード保護されたスプレッドシートを効率的に処理するプロセスについて説明します。 このチュートリアルの最後には、暗号化された Excel ファイルを簡単に開き、編集し、保存できるようになります。
## 前提条件
コードに進む前に、必要なすべてのものが揃っていることを確認しましょう。
- C# の基本知識: このチュートリアルでは、C# プログラミングに精通していることを前提としています。
- .NET Framework: 開発マシンに .NET Framework がインストールされていることを確認します。
-  GroupDocs.Editor for .NET: GroupDocs.Editor for .NETをダウンロードしてインストールします。[ここ](https://releases.groupdocs.com/editor/net/).
## 名前空間のインポート
開始するには、C# プロジェクトに必要な名前空間をインポートする必要があります。これらの名前空間は、GroupDocs.Editor の機能へのアクセスを提供します。
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## ステップ1: 入力ファイルへのパスを取得する
まず、入力ファイルへのパスが必要です。この例では、サンプルのExcelファイル（`Your Sample Document`) はパスワードで保護されています。
```csharp
string inputFilePath = "Your Sample Document";
```
## ステップ2: パスワードなしでドキュメントを開こうとする
パスワードを入力せずにドキュメントを開こうとすると何が起こるか見てみましょう。
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## ステップ3: 間違ったパスワードを指定してみる
ここで、間違ったパスワードを指定して、エディターがどのように応答するかを示します。
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## ステップ4: 正しいパスワードでファイルを開く
正しいパスワードを入力して、ファイルを正常に開きましょう。
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## ステップ5: 編集オプションの作成と調整
スプレッドシートを編集するには、編集オプションを作成して調整する必要があります。
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## ステップ 6: 中間の編集可能なドキュメントを作成する
次に中間体を作成します`EditableDocument`これにより、スプレッドシートに変更を加えることができます。
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    //ステップ7: 保存オプションを作成する
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    //ステップ7.1: 新しいオープニングパスワードを設定する
    saveOptions.Password = "new password";
    //ステップ7.2: 書き込み保護を設定する
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    //ステップ8: ドキュメントを変更せずに保存する
    //ステップ 8.1: 出力ファイル名とパスを準備する
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    //ステップ 8.2: 出力ストリームを作成する
    using (FileStream outputStream = File.Create(outputPath))
    {
        //ステップ8.3: 保存
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
//ステップ9: エディターインスタンスを破棄する
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## 結論
おめでとうございます。GroupDocs.Editor for .NET を使用してパスワードで保護されたスプレッドシートを処理する方法を学習しました。パスワードなしでドキュメントを開くことから、新しい保護設定でドキュメントを保存することまで、すべての重要な手順を学習しました。この知識により、.NET アプリケーション内でセキュリティ保護されたドキュメントを管理する能力が確実に向上します。
## よくある質問
### GroupDocs.Editor for .NET とは何ですか?
GroupDocs.Editor for .NET は、開発者が .NET アプリケーション内でさまざまなドキュメント形式を読み込み、編集し、保存できるようにする強力なドキュメント編集 API です。
### GroupDocs.Editor の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスは以下から取得できます。[ここ](https://purchase.groupdocs.com/temporary-license/)製品の機能を評価します。
### 大きなドキュメントを編集するときにメモリ使用量を最適化することは可能ですか?
はい、メモリの最適化を有効にするには、`OptimizeMemoryUsage`財産に`true`ロードオプションで。
### スプレッドシートを開くときと書き込むときに異なるパスワードを設定できますか?
もちろんです! 保存オプションを使用して、ドキュメントを開くためのパスワードと書き込み保護のためのパスワードを別々に設定できます。
### より詳細なドキュメントはどこで見つかりますか?
 GroupDocs.Editor for .NETの包括的なドキュメントにアクセスできます。[ここ](https://tutorials.groupdocs.com/editor/net/).