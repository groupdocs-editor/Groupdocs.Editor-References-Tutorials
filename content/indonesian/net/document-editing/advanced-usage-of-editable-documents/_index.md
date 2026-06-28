---
date: 2026-03-14
description: Pelajari cara mengekstrak gambar dari DOCX, mengonversi DOCX ke HTML,
  dan menyimpan dokumen sebagai HTML menggunakan GroupDocs.Editor untuk .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Ekstrak Gambar dari DOCX – Penggunaan Dokumen Editabel Tingkat Lanjut
type: docs
url: /id/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

 didn't translate URLs. Good.

Now produce final answer.# Ekstrak Gambar dari DOCX – Penggunaan Dokumen Editable Lanjutan

Jika Anda seorang pengembang .NET yang ingin **mengekstrak gambar dari DOCX** dan meningkatkan kemampuan pengeditan dokumen Anda, GroupDocs.Editor untuk .NET menawarkan rangkaian alat yang kuat. Panduan komprehensif ini akan memandu Anda melalui penggunaan lanjutan dokumen editable menggunakan GroupDocs.Editor, memecah setiap langkah secara detail sehingga Anda dapat memanfaatkan potensinya secara penuh.

## Jawaban Cepat
- **Bagaimana cara mengekstrak gambar dari file DOCX?** Gunakan `EditableDocument.Images` setelah memuat dokumen dengan `Editor`.
- **Apakah saya dapat mengonversi DOCX ke HTML dengan sumber daya tersemat?** Ya—panggil `EditableDocument.GetEmbeddedHtml()` atau `GetContent()` untuk markup HTML.
- **Metode apa yang menyimpan dokumen yang diedit sebagai HTML?** `EditableDocument.Save(htmlFilePath)` membuat file HTML dengan folder sumber daya.
- **Apakah memungkinkan mengekstrak font dari dokumen Word?** Gunakan `EditableDocument.Fonts` untuk mengambil semua sumber daya font.
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Lisensi GroupDocs.Editor yang valid diperlukan; percobaan gratis tersedia.

## Apa itu **extract images from docx**?
Mengekstrak gambar dari file DOCX berarti secara programatik mengambil setiap gambar yang tersemat dalam dokumen Word sehingga Anda dapat menggunakan kembali, memodifikasi, atau menyimpannya secara terpisah. GroupDocs.Editor mengekspos koleksi `Images` pada instance `EditableDocument`, membuat tugas ini menjadi sederhana.

## Mengapa menggunakan GroupDocs.Editor untuk alur kerja ini?
- **Kontrol penuh** atas sumber daya dokumen (gambar, font, CSS) tanpa penanganan ZIP manual.  
- **Konversi mulus** dari DOCX ke HTML sambil mempertahankan tata letak dan gaya.  
- **Ekstraksi sumber daya mudah** untuk penanganan gambar khusus, penyematan font, atau pengiriman CDN.  
- **Pola pembuangan yang kuat** memastikan tidak ada kebocoran memori pada layanan yang berjalan lama.

## Prasyarat
- Visual Studio terpasang pada mesin pengembangan Anda.  
- .NET Framework yang kompatibel dengan GroupDocs.Editor.  
- Perpustakaan GroupDocs.Editor untuk .NET. Anda dapat [mengunduhnya di sini](https://releases.groupdocs.com/editor/net/).  
- Lisensi GroupDocs.Editor yang valid. Anda dapat memperoleh [percobaan gratis](https://releases.groupdocs.com/) atau membeli [lisensi sementara](https://purchase.groupdocs.com/temporary-license/).

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
Pertama, Anda perlu membuat instance `EditableDocument` dengan memuat dan mengedit dokumen input dalam format yang didukung.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

Pada langkah ini, kami memuat dokumen input dan menyiapkannya untuk diedit.

## Cara **extract images from DOCX**?
Di bawah ini kami menyelami kemampuan ekstraksi sumber daya, dimulai dengan kebutuhan paling umum—mengambil semua gambar dari file Word.

## Langkah 2: Mengekstrak Sumber Daya Dokumen
`EditableDocument` berisi berbagai sumber daya yang dapat diekstrak dan dimanipulasi. Mari kita uraikan:

### Langkah 2.1: Mengekstrak Seluruh Dokumen sebagai HTML
Anda dapat menghasilkan satu string yang berisi seluruh dokumen dengan semua sumber dayanya tersemat sebagai HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

String ini akan cukup besar karena mencakup stylesheet, gambar, dan font yang dikodekan dalam base64.

### Langkah 2.2: Mengekstrak Semua Gambar *(kata kunci utama dalam aksi)*
Ekstrak semua gambar dari dokumen—ini adalah inti dari **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Langkah 2.3: Mengekstrak Semua Font *(kata kunci sekunder)*
Jika Anda juga perlu **extract fonts from word**, gunakan panggilan berikut:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Langkah 2.4: Mengekstrak Semua Stylesheet
Ekstrak semua stylesheet dalam format teks.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Langkah 2.5: Mengumpulkan Semua Sumber Daya
Kumpulkan semua sumber daya dalam satu panggilan.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Ini mencakup gambar, font, dan stylesheet.

### Langkah 2.6: Mendapatkan Markup HTML
Dapatkan markup HTML dokumen tanpa sumber daya tersemat.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Cara **convert docx to html** dengan penanganan khusus?
Terkadang Anda perlu menyesuaikan tautan eksternal sehingga mengarah ke penangan sumber daya milik Anda.

## Langkah 3: Menyesuaikan Tautan Eksternal
### Langkah 3.1: Menyiapkan Prefiks Kustom
Siapkan prefiks yang akan menambahkan di depan tautan eksternal asli.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Langkah 3.2: Menghasilkan Markup HTML dengan Prefiks
Hasilkan markup HTML dengan tautan yang disesuaikan.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Langkah 3.3: Mendapatkan Konten HTML Hanya Body
Beberapa editor WYSIWYG hanya menangani markup HTML murni tanpa header.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Langkah 3.4: Konten Hanya Body dengan Prefiks
Hasilkan konten hanya body dengan prefiks gambar kustom.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Langkah 3.5: Mengekstrak Stylesheet
Ekstrak stylesheet yang digunakan dalam dokumen.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Langkah 3.6: Stylesheet dengan Prefiks
Ekstrak stylesheet dengan prefiks kustom.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Cara **save document as html** dengan benar?
## Langkah 4: Menyimpan Dokumen sebagai HTML
Simpan dokumen yang diedit sebagai file HTML, termasuk sumber dayanya.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Metode ini membuat direktori terpisah untuk sumber daya seperti stylesheet, gambar, dan font.

## Langkah 5: Membuang (Dispose) EditableDocument
`EditableDocument` mengimplementasikan `IDisposable` dan menyediakan kemampuan untuk memeriksa apakah instance telah dibuang.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Langkah 5.1 Menangani Event Dispose
Anda juga dapat berlangganan ke event disposing.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Langkah 6: Membuat EditableDocument dari HTML
Buat instance `EditableDocument` dari dokumen HTML.

### Langkah 6.1: Dari File HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Langkah 6.2: Dari Markup HTML

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Instance ini (`afterEditFromFile` dan `afterEditFromMarkup`) identik dengan yang asli (`beforeEdit`).

## Langkah 7: Pembuangan Manual
Buang secara manual instance `EditableDocument` Anda.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Ini memastikan pembersihan sumber daya yang tepat.

## Masalah Umum dan Solusinya
- **Gambar tidak muncul setelah ekstraksi:** Pastikan dokumen memang berisi gambar tersemat dan Anda mengakses `beforeEdit.Images` setelah memanggil `Edit`.  
- **Font tidak muncul dalam output HTML:** Pastikan Anda memanggil `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` untuk menyematkan URL font dengan benar.  
- **String HTML besar menyebabkan tekanan memori:** Gunakan `GetContent()` untuk markup tanpa sumber daya tersemat dan layani gambar/CSS dari file terpisah.

## Pertanyaan yang Sering Diajukan

**Q: Format apa yang didukung oleh GroupDocs.Editor?**  
A: GroupDocs.Editor mendukung DOCX, XLSX, PPTX, dan banyak format kantor populer lainnya.

**Q: Bisakah saya menggunakan GroupDocs.Editor tanpa lisensi?**  
A: Ya, Anda dapat menggunakannya dengan [percobaan gratis](https://releases.groupdocs.com/) atau [lisensi sementara](https://purchase.groupdocs.com/temporary-license/).

**Q: Bagaimana cara mengekstrak sumber daya spesifik dari dokumen?**  
A: Gunakan koleksi `Images`, `Fonts`, dan `Css` pada instance `EditableDocument`.

**Q: Apakah memungkinkan menyesuaikan tautan dalam output HTML?**  
A: Ya, berikan prefiks URI kustom ke `GetContent` atau `GetBodyContent` untuk menulis ulang tautan gambar, CSS, dan font.

**Q: Bagaimana cara menyimpan dokumen yang diedit sebagai file HTML?**  
A: Panggil metode `Save` pada instance `EditableDocument`, dengan memberikan jalur file yang berakhiran `.html`.

---

**Terakhir Diperbarui:** 2026-03-14  
**Diuji Dengan:** GroupDocs.Editor untuk .NET (rilis terbaru)  
**Penulis:** GroupDocs