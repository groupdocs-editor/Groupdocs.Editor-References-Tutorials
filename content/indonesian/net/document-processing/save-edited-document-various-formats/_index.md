---
title: Simpan Dokumen yang Diedit ke Berbagai Format
linktitle: Simpan Dokumen yang Diedit ke Berbagai Format
second_title: GroupDocs.Editor .NET API
description: Pelajari cara menyimpan dokumen yang diedit ke berbagai format menggunakan GroupDocs.Editor untuk .NET dalam panduan langkah demi langkah yang komprehensif ini.
weight: 11
url: /id/net/document-processing/save-edited-document-various-formats/
type: docs
---
# Simpan Dokumen yang Diedit ke Berbagai Format

## Perkenalan
Apakah Anda ingin menyimpan dokumen yang diedit ke berbagai format menggunakan GroupDocs.Editor untuk .NET? Anda datang ke tempat yang tepat! Panduan komprehensif ini akan memandu Anda melalui seluruh proses, mulai dari menyiapkan lingkungan hingga menyimpan dokumen yang telah diedit dalam berbagai format. Mari selami dan lakukan pengeditan dan penyimpanan dokumen dengan mudah!
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki yang berikut:
1.  GroupDocs.Editor untuk .NET - Unduh versi terbaru dari[Di Sini](https://releases.groupdocs.com/editor/net/).
2. Lingkungan Pengembangan - Visual Studio atau IDE lain yang kompatibel dengan .NET.
3. .NET Framework - Pastikan Anda telah menginstal .NET Framework 4.6.1 atau lebih tinggi.
4. Contoh Dokumen - Contoh dokumen Pemrosesan Kata untuk digunakan.
5. Pengetahuan C# Dasar - Diperlukan keakraban dengan pemrograman C#.
## Impor Namespace
Untuk memulai, pastikan Anda mengimpor namespace yang diperlukan ke proyek C# Anda. Ini penting untuk mengakses fungsionalitas GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Mari kita bagi prosesnya menjadi langkah-langkah yang dapat dikelola. Ikuti dengan cermat untuk memastikan Anda memahami setiap bagian.
## Langkah 1: Dapatkan Jalur ke File Input
Pertama, Anda perlu menentukan jalur ke file input WordProcessing Anda. File ini akan dimuat dan diedit.
```csharp
string inputFilePath = "Your Sample Document";
```
## Langkah 2: Buat Opsi Muat untuk Dokumen
Selanjutnya, buat opsi pemuatan khusus untuk dokumen Pemrosesan Word. Opsi ini akan membantu menyesuaikan cara dokumen dimuat.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Langkah 3: Muat Dokumen dengan Opsi
 Sekarang, muat dokumen ke dalam`Editor` misalnya menggunakan opsi pemuatan yang ditentukan.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Langkah 4: Buat Opsi Pengeditan
Siapkan opsi pengeditan untuk dokumen. Opsi ini akan menentukan bagaimana dokumen dibuka untuk diedit.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Langkah 5: Buka Dokumen untuk Diedit
 Buka dokumen untuk diedit dengan membuat`EditableDocument`contoh. Contoh ini memungkinkan Anda membuat perubahan pada dokumen.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Langkah 6: Edit Konten Dokumen
Sekarang saatnya mengedit isi dokumen. Pertama, dapatkan dokumen sebagai string berkode base64 tunggal.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Misalnya, mari kita ubah subtitle pada dokumen.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Langkah 7: Buat Dokumen Baru yang Dapat Diedit dari Konten yang Diedit
 Buat yang baru`EditableDocument` contoh dari konten dan sumber daya yang diedit.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Langkah 8: Simpan Dokumen ke Berbagai Format
Terakhir, ulangi semua format Pemrosesan Word yang didukung dan simpan dokumen yang diedit dalam setiap format.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Siapkan opsi penyimpanan
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Siapkan jalur penyimpanan
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Simpan dokumennya
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Pesan Penyelesaian
Sebagai penutup, Anda dapat mencetak pesan yang menunjukkan bahwa proses telah berhasil diselesaikan.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Kesimpulan
Selamat! Anda telah berhasil mempelajari cara menyimpan dokumen yang diedit ke berbagai format menggunakan GroupDocs.Editor untuk .NET. Alat canggih ini memudahkan manipulasi dan menyimpan dokumen dalam berbagai format hanya dengan beberapa baris kode. Ingat, langkah-langkah utamanya melibatkan memuat dokumen, mengedit konten, dan menyimpannya dalam format yang diinginkan.
## FAQ
### Apa itu GroupDocs.Editor untuk .NET?
GroupDocs.Editor untuk .NET adalah API canggih yang memungkinkan Anda mengedit dokumen dalam berbagai format menggunakan aplikasi .NET.
### Bisakah saya menggunakan GroupDocs.Editor secara gratis?
 Ya, Anda dapat menggunakannya dengan uji coba gratis. Unduh itu[Di Sini](https://releases.groupdocs.com/).
### Format apa yang didukung oleh GroupDocs.Editor?
GroupDocs.Editor mendukung berbagai format, termasuk DOCX, PDF, HTML, dan banyak lagi.
### Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Editor?
 Anda bisa mendapatkan lisensi sementara[Di Sini](https://purchase.groupdocs.com/temporary-license/).
### Di mana saya dapat menemukan lebih banyak dokumentasi dan dukungan?
 Dokumentasi terperinci tersedia[Di Sini](https://tutorials.groupdocs.com/editor/net/) , dan Anda bisa mendapatkan dukungan[Di Sini](https://forum.groupdocs.com/c/editor/20).