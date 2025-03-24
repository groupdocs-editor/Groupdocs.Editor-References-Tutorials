---
title: Penggunaan Lanjutan atas Dokumen yang Dapat Diedit
linktitle: Penggunaan Lanjutan atas Dokumen yang Dapat Diedit
second_title: GroupDocs.Editor .NET API
description: Pelajari penggunaan lanjutan GroupDocs.Editor untuk .NET dalam membuat, mengedit, dan mengekstrak sumber daya dari dokumen secara terprogram.
weight: 11
url: /id/net/document-editing/advanced-usage-of-editable-documents/
---

# Penggunaan Lanjutan atas Dokumen yang Dapat Diedit

## Perkenalan
Jika Anda seorang pengembang .NET yang ingin meningkatkan kemampuan pengeditan dokumen Anda, GroupDocs.Editor untuk .NET menawarkan serangkaian alat canggih. Panduan komprehensif ini akan memandu Anda melalui penggunaan lanjutan dokumen yang dapat diedit menggunakan GroupDocs.Editor, menguraikan setiap langkah secara mendetail untuk memastikan Anda dapat memanfaatkan potensi penuhnya.
## Prasyarat
Sebelum mendalami fungsi lanjutan, pastikan Anda memiliki hal berikut:
- Visual Studio diinstal pada mesin pengembangan Anda.
- .NET Framework kompatibel dengan GroupDocs.Editor.
-  GroupDocs.Editor untuk perpustakaan .NET. Kamu bisa[Unduh di sini](https://releases.groupdocs.com/editor/net/).
-  Lisensi GroupDocs.Editor yang valid. Anda bisa mendapatkan[uji coba gratis](https://releases.groupdocs.com/) atau membeli a[izin sementara](https://purchase.groupdocs.com/temporary-license/).
## Impor Namespace
Untuk memulai, pastikan Anda mengimpor namespace yang diperlukan dalam proyek .NET Anda:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Langkah 1: Membuat Instance EditableDocument
 Pertama, Anda perlu membuat sebuah instance dari`EditableDocument` dengan memuat dan mengedit dokumen masukan dalam format yang didukung.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Pada langkah ini, kami memuat dokumen masukan dan mempersiapkannya untuk diedit.
## Langkah 2: Mengekstrak Sumber Daya Dokumen
 Itu`EditableDocument` berisi berbagai sumber daya yang dapat diekstraksi dan dimanipulasi. Mari kita uraikan ini:
### Langkah 2.1: Ekstrak Seluruh Dokumen sebagai HTML
Anda dapat menghasilkan satu string yang berisi seluruh dokumen dengan semua sumber dayanya yang tertanam sebagai HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
String ini akan berukuran cukup besar karena mencakup stylesheet, gambar, dan font yang dikodekan dalam base64.
### Langkah 2.2: Ekstrak Semua Gambar
Ekstrak semua gambar dari dokumen.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Langkah 2.3: Ekstrak Semua Font
Ekstrak semua font yang digunakan dalam dokumen.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Langkah 2.4: Ekstrak Semua Stylesheet
Ekstrak semua stylesheet dalam format tekstual.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Langkah 2.5: Kumpulkan Semua Sumber Daya
Kumpulkan semua sumber daya dalam satu panggilan.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Ini termasuk gambar, font, dan stylesheet.
### Langkah 2.6: Dapatkan Markup HTML
Dapatkan markup HTML dokumen tanpa sumber daya yang disematkan.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Langkah 3: Menyesuaikan Tautan Eksternal
Terkadang, Anda perlu menyesuaikan tautan eksternal agar mengarah ke pengendali sumber daya khusus. Berikut cara melakukannya:
### Langkah 3.1: Siapkan Awalan Kustom
Siapkan awalan yang akan menambahkan tautan eksternal asli.
```csharp
string customImagesRequesthandlerUri = "http://contoh.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://contoh.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://contoh.com/FontsHandler/id=";
```
### Langkah 3.2: Hasilkan Markup HTML Awalan
Hasilkan markup HTML dengan tautan yang disesuaikan.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Langkah 3.3: Dapatkan Konten HTML Khusus Badan
Beberapa editor WYSIWYG hanya menangani markup HTML murni tanpa header.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Langkah 3.4: Konten Khusus Badan yang Diawali
Hasilkan konten khusus isi dengan awalan gambar khusus.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Langkah 3.5: Ekstrak Stylesheet
Ekstrak stylesheet yang digunakan dalam dokumen.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Langkah 3.6: Stylesheet yang Diawali
Ekstrak stylesheet dengan awalan khusus.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Langkah 4: Simpan Dokumen sebagai HTML
Simpan dokumen yang diedit sebagai file HTML, termasuk sumber dayanya.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Metode ini membuat direktori terpisah untuk sumber daya seperti stylesheet, gambar, dan font.
## Langkah 5: Membuang Dokumen yang Dapat Diedit
 Implementasi EditableDocument`IDisposable` dan memberikan kemampuan untuk memeriksa apakah instance tersebut dibuang.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Langkah 5.1 Menangani Peristiwa Buang
Anda juga dapat berlangganan acara pembuangan.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Langkah 6: Membuat Dokumen yang Dapat Diedit dari HTML
Buat instance EditableDocument dari dokumen HTML.
### Langkah 6.1: Dari File HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Langkah 6.2: Dari Markup HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Contoh ini (afterEditFromFile dan afterEditFromMarkup) identik dengan aslinya (beforeEdit).
## Langkah 7: Pembuangan Manual
Buang instance EditableDocument Anda secara manual.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Hal ini memastikan pembersihan sumber daya yang tepat.
## Kesimpulan
GroupDocs.Editor untuk .NET menyediakan alat canggih untuk mengedit dokumen secara terprogram. Dengan mengikuti panduan langkah demi langkah ini, Anda dapat mengelola konten dokumen, sumber daya, dan format keluaran secara efisien. Baik Anda menyematkan sumber daya, menyesuaikan tautan eksternal, atau mengonversi dokumen ke HTML, GroupDocs.Editor membekali Anda dengan fungsionalitas yang diperlukan untuk manipulasi dokumen tingkat lanjut.
## FAQ
### Format apa yang didukung GroupDocs.Editor?
GroupDocs.Editor mendukung berbagai format termasuk DOCX, XLSX, PPTX, dan banyak lagi.
### Bisakah saya menggunakan GroupDocs.Editor tanpa lisensi?
 Ya, Anda dapat menggunakannya dengan a[uji coba gratis](https://releases.groupdocs.com/) atau a[izin sementara](https://purchase.groupdocs.com/temporary-license/).
### Bagaimana cara mengekstrak sumber daya tertentu dari dokumen?
 Anda dapat mengekstrak gambar, font, dan stylesheet menggunakan metode yang disediakan seperti`Images`, `Fonts` , Dan`Css`.
### Apakah mungkin untuk menyesuaikan tautan pada keluaran HTML?
Ya, Anda dapat menyesuaikan tautan eksternal dengan menentukan awalan khusus untuk gambar, CSS, dan font.
### Bagaimana cara menyimpan dokumen yang diedit sebagai file HTML?
 Menggunakan`Save` metode`EditableDocument`kelas untuk menyimpan dokumen sebagai file HTML, termasuk sumber dayanya.