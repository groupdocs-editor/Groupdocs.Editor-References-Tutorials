---
title: Bekerja dengan Spreadsheet Multi-Tab
linktitle: Bekerja dengan Spreadsheet Multi-Tab
second_title: GroupDocs.Editor .NET API
description: Pelajari cara bekerja dengan spreadsheet multi-tab di .NET menggunakan GroupDocs.Editor. Panduan langkah demi langkah, contoh kode, dan praktik terbaik disertakan.
weight: 17
url: /id/net/document-processing/work-multi-tab-spreadsheets/
---
## Perkenalan
Menangani spreadsheet multi-tab bisa menjadi tugas yang cukup sulit, terutama ketika Anda perlu memanipulasi atau mengekstrak data dari lembar berbeda dalam dokumen yang sama. Jika Anda bekerja dengan .NET dan mencari solusi yang kuat, GroupDocs.Editor untuk .NET adalah pilihan yang sangat baik. Dalam tutorial ini, kami akan memandu Anda melalui proses bekerja dengan spreadsheet multi-tab menggunakan GroupDocs.Editor untuk .NET. Kami akan membahas semuanya mulai dari menyiapkan lingkungan Anda hingga menyimpan setiap tab sebagai file terpisah.
## Prasyarat
Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di mesin Anda.
2. .NET Framework: GroupDocs.Editor untuk .NET mendukung .NET Framework 4.0 atau lebih tinggi.
3. GroupDocs.Editor untuk .NET: Unduh dan instal perpustakaan GroupDocs.Editor untuk .NET. Anda bisa mendapatkannya dari[Unduh Halaman](https://releases.groupdocs.com/editor/net/).
4.  Lisensi: Meskipun Anda dapat menggunakan a[izin sementara](https://purchase.groupdocs.com/temporary-license/) untuk mencoba perpustakaan, disarankan untuk membeli lisensi penuh untuk penggunaan produksi.
## Impor Namespace
Sebelum kita mulai membuat kode, Anda perlu mengimpor namespace yang diperlukan. Tambahkan arahan penggunaan berikut ke bagian atas file .cs Anda:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Dapatkan Jalur ke File Input
Pertama, Anda perlu menentukan jalur ke file spreadsheet masukan Anda. File ini harus berupa XLSX (OOXML) dengan banyak tab.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Muat Spreadsheet ke dalam Mesin Virtual Editor
 Selanjutnya, Anda akan memuat spreadsheet ke dalam`Editor` contoh. Hal ini dilakukan dengan menggunakan aliran file dan menentukan opsi pemuatan yang sesuai untuk spreadsheet.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Langkah selanjutnya akan dilakukan di sini
    }
}
```
## 3. Buat Dokumen yang Dapat Diedit dari Tab Pertama
 Untuk mengedit atau memanipulasi tab tertentu, Anda perlu membuat`EditableDocument` contoh untuk tab itu. Tab ditentukan menggunakan indeks berbasis 0.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // Tab pertama
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Buat Dokumen yang Dapat Diedit dari Tab Kedua
 Demikian pula, buatlah`EditableDocument` untuk tab kedua.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Tab kedua
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Simpan Tab Pertama ke Dokumen Terpisah
Sekarang, simpan tab pertama sebagai dokumen terpisah. Tentukan format penyimpanan dan jalur keluaran.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Simpan Tab Kedua ke Dokumen Terpisah
Ulangi proses untuk tab kedua, tapi kali ini simpan dalam format yang berbeda.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Buang Instans Dokumen yang Dapat Diedit
 Terakhir, pastikan Anda membuangnya dengan benar`EditableDocument` contoh untuk membebaskan sumber daya.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Kesimpulan
Dengan mengikuti langkah-langkah ini, Anda dapat dengan mudah bekerja dengan spreadsheet multi-tab di .NET menggunakan GroupDocs.Editor. Pustaka canggih ini menyederhanakan proses pengeditan dan penyimpanan berbagai lembar dalam spreadsheet, membuat tugas pengembangan Anda lebih mudah dikelola. Baik Anda berurusan dengan manipulasi data yang kompleks atau pengeditan sederhana, GroupDocs.Editor untuk .NET menyediakan alat yang Anda perlukan untuk menyelesaikan pekerjaan secara efisien.
## FAQ
### Apa itu GroupDocs.Editor untuk .NET?
GroupDocs.Editor untuk .NET adalah API pengeditan dokumen canggih yang memungkinkan pengembang memuat, mengedit, dan menyimpan dokumen dalam berbagai format dalam aplikasi .NET.
### Bisakah saya mencoba GroupDocs.Editor untuk .NET sebelum membeli?
 Ya, Anda dapat menggunakan a[uji coba gratis](https://releases.groupdocs.com/) atau meminta a[izin sementara](https://purchase.groupdocs.com/temporary-license/) untuk mengevaluasi produk.
### Format file apa yang didukung oleh GroupDocs.Editor untuk .NET?
GroupDocs.Editor mendukung berbagai format, termasuk DOCX, XLSX, PPTX, PDF, dan banyak lagi.
### Bagaimana cara mendapatkan dukungan untuk GroupDocs.Editor untuk .NET?
 Anda bisa mendapatkan dukungan dengan mengunjungi[forum dukungan](https://forum.groupdocs.com/c/editor/20).
### Di mana saya dapat membeli lisensi penuh GroupDocs.Editor untuk .NET?
 Anda dapat membeli lisensi penuh dari[halaman pembelian](https://purchase.groupdocs.com/buy).