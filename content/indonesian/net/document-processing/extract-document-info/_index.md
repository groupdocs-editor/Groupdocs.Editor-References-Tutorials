---
title: Ekstrak Info Dokumen
linktitle: Ekstrak Info Dokumen
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengekstrak informasi dokumen menggunakan GroupDocs.Editor untuk .NET dengan tutorial langkah demi langkah kami yang mendetail. Sempurna untuk mengelola berbagai jenis dokumen.
weight: 10
url: /id/net/document-processing/extract-document-info/
type: docs
---
# Ekstrak Info Dokumen

## Perkenalan
Selamat datang di tutorial komprehensif tentang mengekstrak informasi dokumen menggunakan GroupDocs.Editor untuk .NET. Dalam panduan ini, kami akan memandu Anda melalui proses langkah demi langkah, memastikan Anda memahami setiap bagian dengan jelas dan ringkas. Baik Anda seorang pengembang berpengalaman atau baru memulai, tutorial ini akan membantu Anda mengintegrasikan GroupDocs.Editor dengan lancar ke dalam proyek .NET Anda untuk mengelola dan memanipulasi dokumen secara efisien.
## Prasyarat
Sebelum mendalami kodenya, pastikan Anda memiliki semua yang Anda perlukan:
- Pengetahuan Dasar C#: Memahami dasar-dasar pemrograman C# sangatlah penting.
- Visual Studio: Pastikan Anda telah menginstal Visual Studio.
-  GroupDocs.Editor untuk .NET: Anda memerlukan perpustakaan GroupDocs.Editor untuk .NET. Anda dapat mengunduhnya dari[Unduh Halaman](https://releases.groupdocs.com/editor/net/).
## Impor Namespace
Untuk memulai, Anda harus mengimpor namespace yang diperlukan. Ini memungkinkan Anda mengakses kelas dan metode yang diperlukan untuk memanipulasi dokumen.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Langkah 1: Muat Dokumen Anda
Pertama, Anda perlu memuat dokumen yang informasinya ingin Anda ekstrak. Hal ini dapat dilakukan dengan menyediakan jalur file ke dokumen.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Langkah 2: Ambil Informasi Dokumen
 Selanjutnya, Anda akan mengambil informasi dokumen menggunakan`GetDocumentInfo` metode. Metode ini tidak memerlukan opsi pemuatan khusus apa pun jika Anda tidak yakin tentang format dokumen.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Langkah 3: Tentukan Jenis Dokumen
Sekarang, Anda perlu memeriksa jenis dokumen yang Anda tangani. Ini penting karena menentukan bagaimana Anda akan menangani dokumen tersebut.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Langkah 4: Ekstrak Informasi Rinci
Jika dokumen tersebut adalah dokumen Pemrosesan Kata, Anda dapat mengekstrak informasi detail seperti format, ekstensi, jumlah halaman, ukuran, dan apakah dokumen tersebut dienkripsi.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Langkah 5: Ulangi untuk Jenis Dokumen Berbeda
Ulangi langkah yang sama untuk tipe dokumen lain seperti Spreadsheet dan dokumen Tekstual.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Langkah 6: Tangani Dokumen yang Dilindungi Kata Sandi
Saat menangani dokumen yang dilindungi kata sandi, pertama-tama Anda harus mencoba membukanya tanpa kata sandi, lalu dengan kata sandi yang salah, dan terakhir dengan kata sandi yang benar.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Langkah 7: Tangani Dokumen Berbasis Teks
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Langkah 8: Buang Sumber Daya
Terakhir, pastikan Anda membuang semua sumber daya untuk mencegah kebocoran memori.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Kesimpulan
Selamat! Anda sekarang telah mempelajari cara mengekstrak informasi dokumen menggunakan GroupDocs.Editor untuk .NET. Pustaka canggih ini menyederhanakan manajemen dan manipulasi dokumen, memungkinkan Anda menangani berbagai jenis dokumen dengan lancar. Baik Anda berurusan dengan dokumen Pemrosesan Kata, Spreadsheet, atau berbasis Teks, GroupDocs.Editor memberikan solusi yang kuat.
## FAQ
### Jenis dokumen apa yang dapat ditangani GroupDocs.Editor?
GroupDocs.Editor dapat menangani berbagai jenis dokumen termasuk Pemrosesan Kata, Spreadsheet, dan dokumen berbasis teks.
### Bisakah GroupDocs.Editor mengelola dokumen yang dilindungi kata sandi?
Ya, GroupDocs.Editor dapat mengelola dokumen yang dilindungi kata sandi. Itu dapat mengidentifikasi dan membuka dokumen-dokumen ini dengan kata sandi yang benar.
### Apakah objek Editor perlu dibuang?
Ya, membuang objek Editor sangatlah penting untuk mengosongkan sumber daya dan mencegah kebocoran memori.
### Bisakah saya mengekstrak informasi detail tentang format dan ukuran dokumen?
Sangat! GroupDocs.Editor memungkinkan Anda mengekstrak informasi terperinci termasuk format, ekstensi, ukuran, jumlah halaman, dan status enkripsi.
### Di mana saya bisa mendapatkan dukungan jika saya mengalami masalah?
 Anda bisa mendapatkan dukungan dari[Forum dukungan GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).