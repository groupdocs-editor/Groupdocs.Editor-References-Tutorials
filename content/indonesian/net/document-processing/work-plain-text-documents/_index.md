---
title: Bekerja dengan Dokumen Teks Biasa
linktitle: Bekerja dengan Dokumen Teks Biasa
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengedit dokumen teks biasa menggunakan GroupDocs.Editor untuk .NET dengan panduan langkah demi langkah kami. Sederhanakan proses pengeditan dokumen .NET Anda.
type: docs
weight: 15
url: /id/net/document-processing/work-plain-text-documents/
---
## Perkenalan
Apakah Anda ingin menyederhanakan proses pengeditan dokumen Anda di .NET? Kunjungi GroupDocs.Editor untuk .NET! API canggih ini memungkinkan Anda mengedit berbagai macam format dokumen dengan mudah. Dalam tutorial ini, kami akan memandu Anda melalui proses bekerja dengan dokumen teks biasa menggunakan GroupDocs.Editor untuk .NET. Pada akhirnya, Anda akan diperlengkapi untuk menangani pengeditan dokumen teks seperti seorang profesional. Siap untuk terjun? Mari kita mulai!
## Prasyarat
Sebelum kita mulai, ada beberapa hal yang perlu Anda siapkan:
- Lingkungan Pengembangan .NET: Pastikan Anda telah menyiapkan lingkungan pengembangan .NET yang berfungsi. Visual Studio adalah pilihan yang populer.
-  GroupDocs.Editor untuk .NET: Unduh dan instal[GroupDocs.Editor untuk .NET](https://releases.groupdocs.com/editor/net/).
- Pengetahuan Dasar C#: Keakraban dengan bahasa pemrograman C# akan membantu Anda mengikuti contoh.
- Editor Teks: Editor teks apa pun bisa digunakan, meskipun Visual Studio Code direkomendasikan karena fitur dan kemudahan penggunaannya.
## Impor Namespace
Untuk mulai menggunakan GroupDocs.Editor untuk .NET, Anda perlu mengimpor namespace yang diperlukan ke dalam proyek Anda. Hal ini memastikan bahwa semua kelas dan metode yang diperlukan tersedia untuk digunakan.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Mari kita bagi prosesnya menjadi langkah-langkah yang dapat dikelola. Ikuti terus saat kami memandu Anda melalui setiap tahap pengeditan dokumen teks biasa menggunakan GroupDocs.Editor untuk .NET.
## Langkah 1: Dapatkan Jalur ke File Input TXT
Pertama, Anda perlu menentukan jalur ke file TXT masukan. Ini bisa berupa jalur ke file lokal atau aliran yang berisi konten file.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Langkah 2: Buat Mesin Virtual Editor
 Selanjutnya, buat sebuah instance dari`Editor` kelas. Kelas ini bertanggung jawab untuk memuat dan mengedit dokumen. Tidak ada opsi pemuatan yang diperlukan pada tahap ini.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Langkah 3: Buat Opsi Pengeditan TXT
Sekarang, buat opsi pengeditan TXT. Opsi ini memungkinkan Anda menentukan bagaimana konten teks harus diproses selama pengeditan.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Langkah 4: Buat Instans EditableDocument
 Dengan mengatur opsi pengeditan, buatlah`EditableDocument` contoh. Ini mewakili dokumen dalam format yang dapat diedit.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Langkah 5: Edit Konten Dokumen
Ambil konten teks asli dan lakukan pengeditan yang Anda inginkan. Untuk contoh ini, kami akan mengganti kata "teks" dengan "teks yang DIEDIT".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Langkah 6: Buat Dokumen yang Dapat Diedit dengan Konten yang Diperbarui
 Setelah melakukan pengeditan yang diperlukan, buat yang baru`EditableDocument` dengan konten yang diperbarui dan sumber daya asli.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Langkah 7: Buat Opsi Penyimpanan Pemrosesan Kata
Siapkan opsi penyimpanan untuk format Pemrosesan Word. Contoh ini menggunakan format DOCM dan menentukan lokalnya.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Langkah 8: Buat Opsi Penyimpanan TXT
Demikian pula, buat opsi penyimpanan untuk format TXT. Pastikan pengkodean diatur ke UTF-8 dan pertahankan tata letak tabel.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Langkah 9: Siapkan Jalur Keluaran
Siapkan jalur untuk menyimpan file DOCX dan TXT yang dihasilkan. Gunakan jalur file masukan untuk menentukan direktori keluaran dan nama file.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Langkah 10: Simpan Dokumen yang Diedit
Terakhir, simpan dokumen yang telah diedit dalam format DOCX dan TXT menggunakan opsi penyimpanan yang ditentukan.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Kesimpulan
 Selamat! Anda telah berhasil mengedit dokumen teks biasa menggunakan GroupDocs.Editor untuk .NET. Alat canggih ini menyederhanakan pengeditan dokumen, sehingga mudah diintegrasikan ke dalam aplikasi .NET Anda. Baik Anda menangani file teks sederhana atau format dokumen kompleks, GroupDocs.Editor siap membantu Anda. Jelajahi lebih banyak fitur dan kemampuan dengan mengunjungi[Dokumentasi GroupDocs.Editor](https://reference.groupdocs.com/editor/net/).
## FAQ
### Format file apa yang didukung GroupDocs.Editor untuk .NET?
 GroupDocs.Editor untuk .NET mendukung berbagai format file, termasuk DOCX, TXT, HTML, dan banyak lagi. Periksalah[dokumentasi](https://reference.groupdocs.com/editor/net/) untuk daftar lengkap.
### Bagaimana saya bisa mendapatkan uji coba gratis GroupDocs.Editor untuk .NET?
 Anda dapat mengunduh uji coba gratis GroupDocs.Editor untuk .NET dari[halaman rilis](https://releases.groupdocs.com/).
### Bisakah saya membeli lisensi sementara untuk GroupDocs.Editor untuk .NET?
Ya, Anda bisa mendapatkan lisensi sementara dari[Halaman pembelian GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Di mana saya bisa mendapatkan dukungan untuk GroupDocs.Editor untuk .NET?
 Dukungan tersedia melalui[Forum dukungan GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Apakah ada dokumentasi terperinci yang tersedia untuk GroupDocs.Editor untuk .NET?
 Ya, dokumentasi terperinci tersedia di[Halaman dokumentasi GroupDocs.Editor](https://reference.groupdocs.com/editor/net/).