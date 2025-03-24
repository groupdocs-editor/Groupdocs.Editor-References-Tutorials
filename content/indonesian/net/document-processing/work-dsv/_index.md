---
title: Bekerja dengan Nilai Terpisah yang Dibatasi (DSV)
linktitle: Bekerja dengan Nilai Terpisah yang Dibatasi (DSV)
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengedit file CSV dan TSV menggunakan GroupDocs.Editor untuk .NET dengan panduan langkah demi langkah ini. Tingkatkan proyek .NET Anda dengan mudah.
weight: 12
url: /id/net/document-processing/work-dsv/
---
## Perkenalan
Jika Anda seorang pengembang yang bekerja dengan nilai-nilai terpisah yang dibatasi (DSV) seperti file CSV atau TSV, Anda tahu bahwa mengedit file-file ini secara terprogram dapat menjadi tugas yang menakutkan. Namun, dengan GroupDocs.Editor untuk .NET, tugas ini menjadi jauh lebih sederhana dan efisien. Dalam tutorial ini, kami akan memandu Anda tentang cara menggunakan GroupDocs.Editor untuk .NET untuk membaca, mengedit, dan menyimpan file DSV. Kami akan membagi prosesnya menjadi langkah-langkah yang mudah diikuti, sehingga memudahkan Anda menerapkannya dalam proyek Anda.
## Prasyarat
Sebelum kita masuk ke tutorialnya, pastikan Anda memiliki prasyarat berikut:
- Visual Studio: Pastikan Anda telah menginstal Visual Studio di mesin Anda.
-  GroupDocs.Editor untuk .NET: Anda perlu mengunduh dan mereferensikan perpustakaan GroupDocs.Editor untuk .NET. Anda dapat mengunduhnya[Di Sini](https://releases.groupdocs.com/editor/net/).
- Pemahaman Dasar C#: Tutorial ini mengasumsikan Anda memiliki pemahaman dasar tentang pengembangan C# dan .NET.
## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan dalam proyek Anda. Namespace ini menyediakan kelas dan metode yang diperlukan untuk bekerja dengan GroupDocs.Editor untuk .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Langkah 1: Dapatkan Jalur ke File Input DSV
Pertama, Anda perlu menentukan jalur ke file input DSV. Untuk contoh ini, kami berasumsi itu adalah file CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Langkah 2: Buat Mesin Virtual Editor
 Buat sebuah instance dari`Editor` kelas. Contoh ini akan digunakan untuk memuat dan memanipulasi file DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Langkah 3: Buat Opsi Edit DSV
 Selanjutnya, buat sebuah instance dari`DelimitedTextEditOptions` dan tentukan pembatas untuk file DSV. Di sini, kami menggunakan koma sebagai pembatas.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Langkah 4: Buat Instans EditableDocument
 Buat sebuah`EditableDocument` misalnya menggunakan`Editor.Edit` metode. Ini mempersiapkan dokumen untuk diedit.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Langkah 5: Edit Konten Dokumen
Ambil konten teks asli dan lakukan modifikasi yang diperlukan. Untuk tujuan demonstrasi, mari ganti beberapa teks.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Langkah 6: Buat Dokumen yang Dapat Diedit dengan Konten yang Diperbarui
 Buat yang baru`EditableDocument` dengan konten yang diperbarui.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Langkah 7: Buat Opsi Penyimpanan CSV
Tentukan opsi penyimpanan untuk format CSV, termasuk pembatas dan pengkodean.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Langkah 8: Buat Opsi Penyimpanan TSV
Demikian pula, tentukan opsi penyimpanan untuk format TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Langkah 9: Buat Opsi Penyimpanan Spreadsheet
Jika Anda perlu menyimpan dokumen sebagai spreadsheet, buat opsi penyimpanan yang sesuai.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Langkah 10: Siapkan Jalur Simpan
Tentukan jalur penyimpanan file yang diedit.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Langkah 11: Simpan Dokumen yang Diedit
Simpan dokumen yang diedit ke jalur yang ditentukan dalam format berbeda.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Langkah 12: Buang Instans EditableDocument
 Terakhir, pastikan untuk membuangnya`EditableDocument` contoh untuk membebaskan sumber daya.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Kesimpulan
Mengedit file DSV menggunakan GroupDocs.Editor untuk .NET adalah proses mudah yang melibatkan pembuatan instance editor, mengatur opsi edit, memodifikasi konten, dan menyimpan perubahan. Panduan langkah demi langkah ini akan membantu Anda mengintegrasikan fungsi ini ke dalam aplikasi .NET Anda dengan mudah. Baik Anda bekerja dengan CSV, TSV, atau format DSV lainnya, GroupDocs.Editor untuk .NET memberikan solusi yang kuat dan fleksibel.
## FAQ
### Bisakah saya menggunakan GroupDocs.Editor untuk .NET untuk mengedit file CSV besar?
Ya, GroupDocs.Editor untuk .NET mampu menangani file CSV besar secara efisien.
### Apakah GroupDocs.Editor untuk .NET mendukung format DSV lain selain CSV dan TSV?
Ya, ini mendukung berbagai format DSV selama Anda menentukan pembatas yang sesuai.
### Apakah mungkin untuk menyesuaikan pengkodean saat menyimpan file DSV?
Tentu saja, Anda dapat menentukan pengkodean yang diinginkan dalam opsi penyimpanan.
### Bisakah saya mengonversi file CSV ke spreadsheet Excel menggunakan GroupDocs.Editor untuk .NET?
Ya, Anda dapat menyimpan file CSV sebagai spreadsheet Excel dengan menggunakan opsi penyimpanan yang sesuai.
### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang GroupDocs.Editor untuk .NET?
 Anda dapat menemukan dokumentasi terperinci[Di Sini](https://tutorials.groupdocs.com/editor/net/)