---
title: レガシーフォームフィールドコレクションの操作
linktitle: レガシーフォームフィールドコレクションの操作
second_title: GroupDocs.Editor .NET API
description: 詳細なガイドで、GroupDocs.Editor for .NET を使用して従来のフォーム フィールドを管理する方法を学びます。テキスト フィールド、チェックボックス、日付などの処理に最適です。
type: docs
weight: 12
url: /ja/net/form-field-management/work-legacy-form-field-collection/
---
## 導入
GroupDocs.Editor for .NET を使用して従来のフォーム フィールド コレクションを操作する方法に関する包括的なガイドへようこそ。テキスト フィールド、チェック ボックス、日付フィールド、ドロップダウン メニューのいずれを扱う場合でも、このチュートリアルでは、これらのフィールドを効率的に管理するための手順を 1 つ 1 つ説明します。このガイドを読み終える頃には、GroupDocs.Editor を使用してドキュメント内のさまざまなフォーム フィールドを処理する方法をしっかりと理解できるようになります。さあ、始めましょう!
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
- Visual Studio: 最新バージョンであればどれでも動作します。
- .NET Framework: .NET Framework がインストールされていることを確認します。
-  GroupDocs.Editor for .NET: 最新バージョンをダウンロード[ここ](https://releases.groupdocs.com/editor/net/).
- サンプル ドキュメント: テスト用のフォーム フィールドを含むサンプル DOCX ファイル。
## 名前空間のインポート
まず、プロジェクトに必要な名前空間をインポートします。これらの名前空間は、フォーム フィールドを操作するために必要なクラスとメソッドにアクセスするために不可欠です。
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## ステップ1: 入力ファイルのパスを取得する
まず、入力ファイルへのパスを指定する必要があります。この例では、さまざまなフォーム フィールドを含むサンプル DOCX ファイルを使用します。
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## ステップ2: ファイルパスからストリームを作成する
次に、ドキュメントのコンテンツを読み取るためのファイル ストリームを作成します。このストリームは、ドキュメントを GroupDocs.Editor に読み込むために使用されます。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //追加コードはここに記入します
}
```
## ステップ3: ドキュメントの読み込みオプションを作成する
ドキュメントを読み込む前に、読み込みオプションを作成します。これらのオプションは、パスワードで保護されたドキュメントなどのさまざまなシナリオを処理するのに役立ちます。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
//文書がパスワードで保護されている場合は、パスワードを指定します
loadOptions.Password = "your_password_here"; //必要に応じて実際のパスワードを使用してください
```
## ステップ4: エディターインスタンスでドキュメントをロードする
ここで、先ほど作成したファイル ストリームと読み込みオプションを使用して、ドキュメントをエディター インスタンスに読み込みます。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //追加コードはここに記入します
}
```
## ステップ5: FormFieldManagerインスタンスの読み取り
フォーム フィールドを管理するには、エディターから FormFieldManager インスタンスにアクセスします。このインスタンスを使用すると、ドキュメント内のフォーム フィールドを操作できます。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## ステップ6: FormFieldCollectionの読み取り
FormFieldManager から FormFieldCollection を取得します。このコレクションには、ドキュメント内に存在するすべてのフォーム フィールドが含まれます。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## ステップ7: 各フォームフィールドを反復処理する
コレクション内の各フォーム フィールドをループして、そのタイプを識別します。タイプに応じて、フィールドの値を抽出して操作できます。
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## ステップ8: 結論
これらの手順に従うことで、GroupDocs.Editor for .NET を使用してドキュメント内の従来のフォーム フィールドを効果的に管理および操作できます。テキスト フィールド、チェック ボックス、日付、数値、ドロップダウンなど、このガイドでは、各タイプを処理するための明確で簡潔な方法を説明します。
## 結論
適切なツールを使用すれば、ドキュメント内の従来のフォームフィールドの操作は簡単です。GroupDocs.Editor for .NET は、これらのフィールドを効率的に管理するための強力なソリューションを提供します。このステップバイステップのガイドに従うことで、ドキュメント内のさまざまなフォームフィールドを簡単に操作できるようになります。[ドキュメンテーション](https://reference.groupdocs.com/editor/net/)より高度な機能とオプションについては、こちらをご覧ください。
## よくある質問
### 1. パスワードで保護されたドキュメントで GroupDocs.Editor for .NET を使用できますか?
はい、読み込みオプションでパスワードを指定して、パスワードで保護されたドキュメントを処理できます。
### 2. GroupDocs.Editor for .NET の無料試用版を入手するにはどうすればよいですか?
無料トライアルはこちらからダウンロードできます[ここ](https://releases.groupdocs.com/).
### 3. GroupDocs.Editor for .NET のサポートはありますか?
はい、サポートにアクセスできます[ここ](https://forum.groupdocs.com/c/editor/20).
### 4. GroupDocs.Editor for .NET のライセンスを購入できますか?
はい、ライセンスは以下から購入できます。[ここ](https://purchase.groupdocs.com/buy).
### 5. GroupDocs.Editor for .NET のドキュメントはどこにありますか?
ドキュメントは入手可能です[ここ](https://reference.groupdocs.com/editor/net/).