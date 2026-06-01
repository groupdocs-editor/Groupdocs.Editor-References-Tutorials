---
date: 2026-06-01
description: Pelajari cara mendapatkan jumlah halaman dan mengekstrak metadata dokumen
  menggunakan GroupDocs.Editor untuk .NET dalam tutorial langkah demi langkah yang
  detail.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Dapatkan Jumlah Halaman & Ekstrak Info Dokumen
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Dapatkan Jumlah Halaman & Ekstrak Info Dokumen dengan GroupDocs.Editor
type: docs
url: /id/net/document-processing/extract-document-info/
weight: 10
---

# Dapatkan Jumlah Halaman & Ekstrak Informasi Dokumen dengan GroupDocs.Editor

## Pendahuluan
Dalam tutorial komprehensif ini Anda akan belajar cara **mendapatkan jumlah halaman** dan mengekstrak informasi dokumen secara detail—termasuk format, ukuran, dan status enkripsi—menggunakan GroupDocs.Editor untuk .NET. Baik Anda membangun sistem manajemen dokumen, mesin pelaporan, atau pipeline konversi otomatis, memahami metadata file adalah langkah pertama menuju pemrosesan yang dapat diandalkan. Mari kita jalani seluruh alur kerja, mulai dari memuat file hingga membuang sumber daya dengan aman.

## Jawaban Cepat
- **Bagaimana cara saya mengambil jumlah halaman dokumen?**  
  Panggil `editor.GetDocumentInfo().PageCount` setelah memuat file dengan `Editor`.
- **Format file apa saja yang didukung untuk ekstraksi metadata?**  
  Lebih dari 50 format, termasuk DOCX, XLSX, PPTX, PDF, TXT, dan HTML.
- **Apakah saya dapat mengekstrak metadata dari file yang dilindungi kata sandi?**  
  Ya—berikan kata sandi saat membuat instance `Editor`.
- **Apakah saya perlu melepaskan sumber daya secara manual?**  
  Tentu saja; selalu panggil `editor.Dispose()` atau bungkus editor dalam blok `using`.
- **Versi GroupDocs.Editor apa yang diperlukan?**  
  Rilis stabil terbaru (v23.12+ pada saat penulisan) mendukung semua fitur yang ditunjukkan.

## Apa itu “get page count” dalam GroupDocs.Editor?
`GetDocumentInfo()` adalah metode yang mengembalikan objek `DocumentInfo` yang berisi jumlah halaman dokumen, format, ukuran, dan metadata lainnya. Panggilan tunggal ini memberi Anda wawasan langsung tanpa harus mem-parsing file secara manual. Dengan menggunakan metode ini Anda menghindari pemuatan seluruh dokumen ke memori, yang meningkatkan kinerja terutama untuk file besar dan mengurangi konsumsi sumber daya server.

## Mengapa mengekstrak metadata dokumen dengan GroupDocs.Editor?
GroupDocs.Editor dapat memproses **lebih dari 50 format input dan output** serta mengambil metadata untuk file hingga **2 GB** tanpa memuat seluruh dokumen ke memori. Efisiensi ini mengurangi beban server hingga **70 %** dibandingkan dengan parsing dokumen penuh, menjadikannya ideal untuk aplikasi dengan throughput tinggi.

## Prasyarat
Sebelum Anda memulai, pastikan Anda memiliki:

- **Dasar pengembangan C#** – Anda harus nyaman dengan Visual Studio dan struktur proyek .NET.
- **Visual Studio 2022** (atau versi terbaru apa pun) terpasang di mesin Anda.
- **GroupDocs.Editor untuk .NET** – unduh paket terbaru dari [halaman unduhan](https://releases.groupdocs.com/editor/net/).

## Cara Memuat Dokumen Anda?
`Editor` adalah kelas utama yang mewakili sebuah dokumen dan menyediakan metode untuk memuat serta memanipulasinya. Muat file target dengan membuat instance `Editor` dan memberikan jalur file. Editor secara otomatis mendeteksi format, sehingga Anda tidak perlu menentukan opsi pemuatan. Pendekatan ini bekerja untuk semua tipe file yang didukung dan menyederhanakan penyiapan awal.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Cara Mengambil Informasi Dokumen?
`GetDocumentInfo()` mengembalikan objek `DocumentInfo` yang berisi metadata seperti jumlah halaman, format, ukuran, dan status enkripsi. Setelah memuat, panggil metode ini untuk mengambil objek tersebut. `DocumentInfo` yang dikembalikan memberikan gambaran singkat tentang karakteristik file, memungkinkan Anda membuat keputusan tanpa pemrosesan lebih lanjut.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Cara Menentukan Tipe Dokumen?
`DocumentType` adalah enum yang menunjukkan apakah dokumen tersebut adalah WordProcessing, Spreadsheet, atau Text. Mengetahui apakah file adalah dokumen pengolah kata, spreadsheet, atau teks biasa memengaruhi cara Anda menanganinya nanti. Gunakan properti `DocumentType` dari objek `DocumentInfo` untuk membuat keputusan ini dan mengarahkan logika Anda sesuai.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Cara Mengekstrak Informasi Detail untuk File Pengolah Kata?
`WordProcessing` mengacu pada dokumen seperti DOCX, ODT, dan RTF yang diperlakukan sebagai file pengolah kata. Jika tipe dokumen adalah `WordProcessing`, Anda dapat membaca properti tambahan seperti **format**, **ekstensi**, **jumlah halaman**, **ukuran**, dan **bendera enkripsi** langsung dari objek `DocumentInfo`. Detail ini membantu Anda menyesuaikan langkah pemrosesan, seperti menerapkan konversi khusus atau pemeriksaan keamanan.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Cara Menangani Spreadsheet dan Dokumen Teks?
`Spreadsheet` menunjukkan file spreadsheet seperti XLSX, sementara `Text` mewakili dokumen teks biasa. Untuk spreadsheet (`Spreadsheet`) dan file teks biasa (`Text`), objek `DocumentInfo` tetap menyediakan metadata inti (ekstensi, ukuran, jumlah halaman). Beberapa format mungkin tidak menampilkan jumlah halaman, dalam hal ini nilai akan menjadi `0`. Anda tetap dapat mengandalkan metadata lain untuk logika downstream.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Cara Bekerja dengan Dokumen yang Dilindungi Kata Sandi?
`Password` adalah string yang diberikan ke konstruktor `Editor` untuk membuka file terenkripsi. Ketika sebuah dokumen dienkripsi, pertama coba buka tanpa kata sandi. Jika gagal, tangkap pengecualian, lalu coba lagi dengan kata sandi yang benar. Konstruktor `Editor` menerima parameter `Password` untuk tujuan ini, memungkinkan penanganan file terlindungi secara mulus.

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

## Cara Memproses Dokumen Berbasis Teks?
`DocumentInfo` menyediakan metadata dasar seperti ukuran, ekstensi, dan encoding untuk file teks. File teks (mis., `.txt`, `.md`) diperlakukan sebagai aliran sederhana. Anda tetap dapat mengambil informasi ukuran dan encoding dari `DocumentInfo`, yang berguna untuk memvalidasi integritas file atau menentukan pipeline pemrosesan yang tepat.

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

## Cara Membebaskan Sumber Daya dengan Benar?
`Editor` adalah kelas utama yang menyimpan sumber daya tidak terkelola dan harus dibebaskan setelah digunakan. Untuk menghindari kebocoran memori, selalu bebaskan instance `Editor` setelah selesai mengekstrak informasi. Pernyataan `using` adalah pola paling aman karena menjamin pembebasan bahkan jika terjadi pengecualian, memastikan manajemen sumber daya yang bersih.

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

## Masalah Umum dan Solusinya
| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| **PageCount returns 0** | Format tidak mendukung paginasi (mis., teks biasa) | Periksa `DocumentInfo.DocumentType` sebelum mengandalkan `PageCount`. |
| **Unsupported file format** | Ekstensi file tidak dikenali | Pastikan file termasuk dalam lebih dari 50 format yang didukung; perbarui GroupDocs.Editor ke versi terbaru. |
| **Password exception** | Kata sandi yang diberikan salah | Tangkap `PasswordProtectedException` dan minta pengguna memasukkan kembali kata sandi. |
| **Memory spike on large files** | Memuat PDF sangat besar tanpa streaming | Gunakan `LoadOptions` dengan `LoadOptions.LoadMode = LoadMode.Stream` (tersedia pada rilis terbaru). |

## Pertanyaan yang Sering Diajukan

**Q: Tipe dokumen apa yang dapat saya ekstrak metadata-nya?**  
A: GroupDocs.Editor mendukung file pengolah kata, spreadsheet, presentasi, PDF, dan teks biasa—lebih dari 50 format secara total.

**Q: Bagaimana cara saya mengambil ekstensi file?**  
A: Akses `DocumentInfo.Extension` setelah memanggil `GetDocumentInfo()`; ia mengembalikan ekstensi tanpa titik di depannya.

**Q: Bisakah saya mendapatkan ukuran dokumen dalam megabyte?**  
A: Ya—`DocumentInfo.Size` mengembalikan ukuran dalam byte; bagi dengan 1.048.576 untuk mengonversinya ke megabyte.

**Q: Apakah aman memproses file yang dilindungi kata sandi di server?**  
A: Tentu saja—GroupDocs.Editor tidak pernah menulis kata sandi ke disk dan membebaskan semua objek kriptografi setelah digunakan.

**Q: Di mana saya dapat menemukan bantuan tambahan jika mengalami masalah?**  
A: Anda dapat mendapatkan dukungan dari [forum dukungan GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Terakhir Diperbarui:** 2026-06-01  
**Diuji Dengan:** GroupDocs.Editor 23.12 untuk .NET  
**Penulis:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Tutorial Terkait

- [Panduan Lengkap Ekstraksi Metadata di .NET dengan GroupDocs.Editor](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Tutorial Memuat Dokumen dengan GroupDocs.Editor untuk .NET](/editor/net/document-loading/)
- [Pengeditan Dokumen Efisien dengan GroupDocs.Editor .NET: Mengubah HTML menjadi Dokumen yang Dapat Diedit](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)