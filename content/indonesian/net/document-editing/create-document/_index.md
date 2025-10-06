---
title: Buat Dokumen
linktitle: Buat Dokumen
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengedit dokumen Word, Excel, PowerPoint, Ebook, dan Email menggunakan GroupDocs.Editor untuk .NET dengan tutorial langkah demi langkah yang komprehensif ini.
weight: 10
url: /id/net/document-editing/create-document/
type: docs
---
# Buat Dokumen

## Perkenalan
Apakah Anda bosan dengan kerumitan mengedit berbagai jenis dokumen secara terprogram? GroupDocs.Editor untuk .NET hadir untuk menyederhanakan prosesnya. Alat canggih ini memungkinkan pengembang untuk mengedit berbagai format dokumen seperti Word, Excel, PowerPoint, Ebooks, dan Email dengan mudah. Dalam tutorial ini, kita akan mendalami cara menggunakan GroupDocs.Editor untuk .NET untuk membuat dan mengedit dokumen. Kami akan membagi prosesnya menjadi langkah-langkah yang mudah diikuti, sehingga dapat diakses bahkan jika Anda baru dalam hal ini.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki yang berikut:
- Visual Studio diinstal pada mesin Anda.
- .NET Framework (4.0 atau lebih tinggi).
-  GroupDocs.Editor untuk perpustakaan .NET. Anda dapat mengunduhnya dari[Di Sini](https://releases.groupdocs.com/editor/net/).
- Pengetahuan dasar tentang pemrograman C#.
## Impor Namespace
Pertama, mari impor namespace yang diperlukan. Ini akan membuat kelas dan metode yang diperlukan dapat diakses di aplikasi kita.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Langkah 1: Menyiapkan Aliran
Untuk memulainya, kita perlu menyiapkan aliran memori yang akan bertindak sebagai pengganti konten dokumen.
```csharp
Stream memoryStream = Stream.Null;
```
## Langkah 2: Fungsi Panggilan Balik untuk Menyimpan Dokumen
Selanjutnya, tentukan fungsi panggilan balik yang akan menyimpan aliran dokumen baru. Fungsi ini penting untuk menangani keluaran dari proses pengeditan dokumen.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Langkah 3: Membuat dan Mengedit Dokumen Pemrosesan Word
 Sekarang, mari membuat dan mengedit dokumen Word. Kami akan mulai dengan membuat yang baru`Editor` contoh untuk dokumen Pemrosesan Word dan mengeditnya dengan opsi default.
### Buat dan Edit dengan Opsi Default
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Buat dan Edit dengan Opsi Kustom
Untuk kontrol lebih lanjut, kita dapat menentukan opsi seperti menonaktifkan penomoran halaman dan mengekstrak font yang disematkan.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Langkah 4: Membuat dan Mengedit Dokumen Spreadsheet
Demikian pula, kita dapat membuat dan mengedit dokumen Excel. Inilah cara Anda melakukannya.
### Buat dan Edit dengan Opsi Default
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Buat dan Edit dengan Opsi Kustom
 Untuk menargetkan lembar kerja tertentu atau mengecualikan lembar kerja yang tersembunyi, kami menggunakan`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Langkah 5: Membuat dan Mengedit Dokumen Presentasi
Presentasi PowerPoint juga didukung. Mari kita lihat cara menanganinya.
### Buat dan Edit dengan Opsi Default
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Buat dan Edit dengan Opsi Kustom
Anda dapat menyesuaikan hasil edit Anda dengan menentukan opsi seperti slide mana yang akan ditampilkan dan apakah akan menyertakan slide tersembunyi.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Langkah 6: Membuat dan Mengedit Dokumen Ebook
GroupDocs.Editor juga memungkinkan untuk mengedit format Ebook seperti EPUB. Inilah cara Anda mengatasinya.
### Buat dan Edit dengan Opsi Default
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Buat dan Edit dengan Opsi Kustom
Sesuaikan pengeditan EBook Anda dengan mengaktifkan atau menonaktifkan informasi paginasi dan bahasa.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Langkah 7: Membuat dan Mengedit Dokumen Email
Terakhir, kita akan melihat cara mengedit dokumen email. Ini termasuk format seperti EML.
### Buat dan Edit dengan Opsi Default
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Buat dan Edit dengan Opsi Kustom
Tentukan opsi keluaran pesan email untuk mengontrol proses pengeditan.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Langkah 8: Menyelesaikan Proses
Setelah mengedit dokumen, penting untuk membuang aliran memori dengan benar untuk mengosongkan sumber daya.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Kesimpulan
GroupDocs.Editor untuk .NET adalah alat serbaguna dan canggih yang dapat menyederhanakan tugas mengedit berbagai jenis dokumen secara terprogram. Dengan mengikuti panduan langkah demi langkah ini, Anda dapat membuat dan mengedit dokumen dengan mudah, baik itu file Pemrosesan Word, spreadsheet, presentasi, eBook, atau email. Selami dokumentasi GroupDocs.Editor untuk fitur lebih lanjut dan opsi penyesuaian.
## FAQ
### Jenis dokumen apa yang dapat saya edit dengan GroupDocs.Editor untuk .NET?
Anda dapat mengedit berbagai macam dokumen, termasuk Pemrosesan Word, spreadsheet, presentasi, eBook, dan email.
### Apakah mungkin untuk menyesuaikan opsi pengeditan?
Ya, GroupDocs.Editor untuk .NET memungkinkan penyesuaian ekstensif melalui berbagai opsi pengeditan khusus untuk setiap jenis dokumen.
### Bagaimana cara menangani keluaran dokumen yang diedit?
Anda dapat menggunakan fungsi panggilan balik untuk menyimpan aliran dokumen yang diedit ke lokasi yang Anda inginkan.
### Apakah saya memerlukan lisensi untuk menggunakan GroupDocs.Editor untuk .NET?
 Ya, Anda bisa mendapatkan lisensi dari[Di Sini](https://purchase.groupdocs.com/buy). Ada juga opsi untuk lisensi sementara.
### Di mana saya dapat menemukan dokumentasi yang lebih detail?
 Dokumentasi terperinci tersedia di[GroupDocs.Editor untuk halaman dokumentasi .NET](https://tutorials.groupdocs.com/editor/net/).