---
title: 無効なフォームフィールドコレクションを修正して保存する
linktitle: 無効なフォームフィールドコレクションを修正して保存する
second_title: GroupDocs.Editor .NET API
description: Groupdocs.Editor for .NET を使用して DOCX 内の無効なフォーム フィールドを修正する方法を学びます。このガイドに従って、ドキュメントにエラーがないことを確認し、安全に保存します。
weight: 11
url: /ja/net/form-field-management/fix-invalid-form-field-collection-save/
---

# 無効なフォームフィールドコレクションを修正して保存する

## 導入
ようこそ! ドキュメント内のフォーム フィールドを操作していて、無効なフォーム フィールド コレクションに関する問題に直面している場合は、適切な場所にいます。このチュートリアルでは、Groupdocs.Editor for .NET を使用して無効なフォーム フィールドを修正し、ドキュメントを保存する方法について詳しく説明します。このプロセスを段階的にガイドし、シームレスに動作させるために必要なすべての詳細を提供します。さあ、始めましょう!
## 前提条件
コードに進む前に、準備しておくべきことがいくつかあります。
-  Groupdocs.Editor for .NET: Groupdocs.Editorライブラリが.NET用にインストールされていることを確認してください。ダウンロードできます。[ここ](https://releases.groupdocs.com/editor/net/).
- 開発環境: Visual Studio などの .NET 開発環境をセットアップする必要があります。
- C# の基本知識: このチュートリアルでは、C# プログラミングの基本を理解していることを前提としています。
## 名前空間のインポート
まず、C# プロジェクトに必要な名前空間をインポートする必要があります。コード ファイルの先頭に次の行を追加します。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## ステップ1: 入力ファイルのパスを取得する
最初のステップは、入力ファイルへのパスを指定することです。このファイルは、フォーム フィールドを含む DOCX ドキュメントである必要があります。
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## ステップ2: ファイルパスからストリームを作成する
次に、入力ドキュメントを読み取るためのファイル ストリームを作成します。これにより、ドキュメントをエディターに読み込むことができます。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## ステップ3: ドキュメントの読み込みオプションを作成する
この手順では、ドキュメントの読み込みオプションを作成する必要があります。ドキュメントがパスワードで保護されている場合は、パスワードを指定できます。この例では、ドキュメントは保護されていないため、パスワードは無視されます。
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## ステップ4: ドキュメントをエディターインスタンスに読み込む
次に、指定されたオプションを含むドキュメントを Editor インスタンスに読み込みます。ここでドキュメントの主な操作が行われます。
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## ステップ 4.1: FormFieldManager インスタンスの読み取り
の`FormFieldManager`インスタンスは、ドキュメント内のフォーム フィールドの管理を担当します。フォーム フィールドにアクセスして操作するには、このインスタンスを読み取る必要があります。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## ステップ 4.2: FormFieldCollection の読み取り
の`FormFieldCollection`ドキュメント内のすべてのフォーム フィールドが含まれます。このコレクションを読み取って、無効なフォーム フィールドをチェックし、修正します。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## ステップ 4.3: 無効なフォーム フィールドを自動修正する
ドキュメント内の無効なフォーム フィールドを自動修正します。これは明らかな問題に対処するための予備的な手順です。
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## ステップ4.4: 無効なフォームフィールドを確認する
自動修正の試行後に無効なフォーム フィールドが残っているかどうかを確認します。
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## ステップ 4.4.1: 無効なフォームフィールド名をすべて取得する
すべての無効なフォーム フィールドの名前を取得します。これらの名前はフィールドを修正するために使用されます。
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## ステップ4.4.2: 無効なフィールドに一意の名前を作成する
無効なフォーム フィールドごとに一意の名前を作成します。これにより、既存のフォーム フィールド名との競合がなくなります。
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## ステップ4.4.3: 無効なフォームフィールドを修正する
前の手順で作成した一意の名前を使用して、無効なフォーム フィールドを修正します。
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## ステップ5: ドキュメント保存オプションを作成する
ドキュメントを保存するためのオプションを設定します。これには、形式の指定や追加の保存設定が含まれます。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## ステップ5.1: メモリ使用量を最適化する
文書が大きく、`OutOfMemoryException`メモリ最適化オプションを有効にします。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## ステップ5.2: 文書への書き込みを防止する
フォーム フィールドを除いてドキュメントが変更されないように保護するには、保護パスワードを設定します。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## ステップ6: ドキュメントを保存する
最後に、指定された保存オプションでドキュメントを保存します。出力ドキュメントを保存するためのメモリ ストリームを準備します。
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## 結論
これで完了です。Groupdocs.Editor for .NET を使用して無効なフォームフィールドを修正し、ドキュメントを保存できました。このステップバイステップのガイドにより、プロセスが明確になり、管理しやすくなりました。問題が発生したり、質問がある場合は、[ドキュメンテーション](https://tutorials.groupdocs.com/editor/net/)または連絡する[サポート](https://forum.groupdocs.com/c/editor/20).
## よくある質問
### ドキュメントがパスワードで保護されている場合はどうなりますか?
パスワードは`WordProcessingLoadOptions`ドキュメントを開きます。
### 無効なフォーム フィールドがあるかどうかはどうすればわかりますか?
使用`HasInvalidFormFields`ドキュメント内の無効なフォーム フィールドをチェックするメソッド。
### 名前を変更せずにフォームフィールドを修正できますか?
競合を避けるために、無効なフォーム フィールドに一意の名前を作成することをお勧めします。
### どのような形式でドキュメントを保存できますか?
適切な設定を行うことで、DOCX、PDFなどのさまざまな形式で文書を保存できます。`WordProcessingFormats`.
### 大きなドキュメントを保存するときにメモリ使用量を最適化するにはどうすればよいですか?
有効にする`OptimizeMemoryUsage`オプションの`WordProcessingSaveOptions`大きな文書を効率的に処理します。