---
title: Simpan Dokumen
linktitle: Simpan Dokumen
second_title: GroupDocs.Editor .NET API
description: Edit dan simpan dokumen dengan mudah menggunakan GroupDocs.Editor untuk .NET. Panduan langkah demi langkah ini menyederhanakan proses bagi pengembang.
weight: 14
url: /id/net/document-editing/save-document/
---
## Perkenalan
Apakah Anda ingin mengedit dan menyimpan dokumen dengan mudah menggunakan GroupDocs.Editor untuk .NET? Anda berada di tempat yang tepat! Tutorial ini akan memandu Anda melalui proses langkah demi langkah, memastikan Anda dapat mengelola dokumen Anda dengan mudah. Baik Anda seorang pengembang berpengalaman atau pemula, panduan kami akan memberi Anda semua informasi yang Anda perlukan untuk memulai.
## Prasyarat
Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
- Lingkungan Pengembangan: Visual Studio diinstal pada mesin Anda.
- .NET Framework: Pastikan Anda memiliki .NET Framework 4.6.1 atau lebih baru.
-  GroupDocs.Editor untuk .NET: Unduh versi terbaru[Di Sini](https://releases.groupdocs.com/editor/net/).
- Pengetahuan Dasar C#: Keakraban dengan pemrograman C# sangat penting.
## Impor Namespace
Untuk menggunakan GroupDocs.Editor di proyek .NET Anda, Anda perlu mengimpor namespace yang diperlukan. Inilah cara Anda melakukannya:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Sekarang setelah lingkungan kita siap dan namespace yang diperlukan telah diimpor, mari selami langkah-langkah yang diperlukan untuk memuat, mengedit, dan menyimpan dokumen menggunakan GroupDocs.Editor untuk .NET.
## Langkah 1: Muat Dokumen
Pertama, kita perlu memuat dokumen yang ingin kita edit. GroupDocs.Editor membuat proses ini menjadi mudah. Inilah cara Anda melakukannya:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Pada langkah ini, kita menentukan jalur ke dokumen yang ingin kita edit dan membuat instance darinya`Editor` kelas. Itu`Edit` metode kemudian dipanggil untuk memuat dokumen ke dalam`EditableDocument` obyek.
## Langkah 2: Ubah Dokumen
Setelah dokumen dimuat, saatnya melakukan beberapa modifikasi. Karena kami tidak memiliki editor WYSIWYG, kami akan menyimulasikan proses pengeditan dalam kode.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Di sini, kami mengambil konten HTML yang disematkan pada dokumen, melakukan penggantian teks sederhana, dan membuat yang baru`EditableDocument`contoh dari HTML yang dimodifikasi.
## Langkah 3: Simpan Dokumen
Setelah dokumen diedit, langkah terakhir adalah menyimpannya. GroupDocs.Editor menyediakan banyak opsi untuk menyimpan dokumen dalam format berbeda.
## Simpan sebagai RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Simpan sebagai DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Simpan sebagai Teks Biasa
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Langkah 4: Pembersihan
 Terakhir, sangat penting untuk membuangnya`EditableDocument` Dan`Editor` contoh untuk membebaskan sumber daya.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Dengan mengikuti langkah-langkah ini, Anda dapat memuat, mengedit, dan menyimpan dokumen secara efisien menggunakan GroupDocs.Editor untuk .NET. Alat canggih ini memberikan fleksibilitas dan kemudahan penggunaan, membuat pengelolaan dokumen menjadi mudah.
## Kesimpulan
Mengedit dan menyimpan dokumen secara terprogram tidak pernah semudah ini dengan GroupDocs.Editor untuk .NET. Panduan ini memandu Anda melalui seluruh proses, mulai dari memuat dokumen hingga menyimpannya dalam berbagai format. Dengan GroupDocs.Editor, Anda memiliki solusi serbaguna dan tangguh di ujung jari Anda, menyederhanakan proses pengeditan dokumen.
## FAQ
### Format file apa yang didukung GroupDocs.Editor?
GroupDocs.Editor mendukung berbagai format file, termasuk DOCX, RTF, TXT, dan masih banyak lagi. Untuk daftar lengkap, lihat[dokumentasi](https://tutorials.groupdocs.com/editor/net/).
### Bisakah saya mencoba GroupDocs.Editor sebelum membeli?
 Ya, Anda bisa mendapatkan[uji coba gratis](https://releases.groupdocs.com/) untuk menguji fitur GroupDocs.Editor.
### Apakah ada dukungan yang tersedia jika saya menghadapi masalah?
 Sangat! Anda dapat mengunjungi[forum dukungan](https://forum.groupdocs.com/c/editor/20) untuk bantuan dengan masalah apa pun yang Anda temui.
### Bagaimana cara mendapatkan lisensi sementara?
 Anda dapat meminta a[izin sementara](https://purchase.groupdocs.com/temporary-license/) untuk tujuan evaluasi.
### Di mana saya dapat membeli GroupDocs.Editor versi lengkap?
 Anda dapat membeli versi lengkapnya[Di Sini](https://purchase.groupdocs.com/buy).