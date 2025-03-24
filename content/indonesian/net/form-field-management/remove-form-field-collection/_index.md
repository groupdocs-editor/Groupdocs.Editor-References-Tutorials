---
title: Hapus Koleksi Bidang Formulir
linktitle: Hapus Koleksi Bidang Formulir
second_title: GroupDocs.Editor .NET API
description: Pelajari cara menghapus bidang formulir dari dokumen Word menggunakan GroupDocs.Editor untuk .NET dengan panduan langkah demi langkah ini. Ideal untuk pengembang.
weight: 13
url: /id/net/form-field-management/remove-form-field-collection/
---
## Perkenalan
Apakah Anda ingin mengelola kolom formulir di dokumen Anda secara terprogram? GroupDocs.Editor untuk .NET menawarkan solusi ampuh untuk menangani dan memanipulasi bidang formulir dalam berbagai format dokumen. Dalam tutorial ini, kami akan memandu Anda melalui langkah-langkah untuk menghapus kumpulan bidang formulir dari dokumen Word menggunakan perpustakaan tangguh ini. 
## Prasyarat
Sebelum kita mendalami kodenya, pastikan Anda sudah menyiapkan segalanya untuk pengalaman yang lancar:
1. GroupDocs.Editor untuk .NET: Pastikan Anda telah mengunduh dan menginstal GroupDocs.Editor untuk .NET. Jika belum, Anda dapat mendownloadnya[Di Sini](https://releases.groupdocs.com/editor/net/).
2. Lingkungan Pengembangan: Anda memerlukan lingkungan pengembangan seperti Visual Studio.
3. .NET Framework: Pastikan Anda telah menginstal .NET Framework di mesin Anda.
4.  Contoh Dokumen: Miliki contoh dokumen Word (misalnya,`SampleLegacyFormFields.docx`) dengan bidang formulir yang ingin Anda manipulasi.

## Impor Namespace
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dalam proyek .NET Anda. Ini akan memungkinkan Anda mengakses fungsionalitas GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Langkah 1: Muat Dokumen
Pertama, Anda harus memuat dokumen yang ingin Anda edit. Mari kita uraikan:
### Langkah 1.1: Dapatkan Jalur ke File Input
 Anda perlu menentukan jalur ke file masukan Anda. Untuk contoh ini, kita akan menggunakan file contoh bernama`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Langkah 1.2: Buat FileStream dari Path
 Selanjutnya, buat a`FileStream` untuk membaca dokumen tersebut.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Lanjutkan ke langkah selanjutnya dalam blok penggunaan ini.
}
```
## Langkah 2: Tetapkan Opsi Muat
Saat memuat dokumen, Anda mungkin perlu menentukan opsi pemuatan, terutama jika dokumen Anda dilindungi kata sandi.
### Langkah 2.1: Buat Opsi Muat
 Buat sebuah contoh dari`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Langkah 2.2: Tentukan Kata Sandi (Jika Diperlukan)
Jika dokumen Anda dilindungi kata sandi, Anda dapat menentukan kata sandinya.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Langkah 3: Muat Dokumen ke Editor
 Sekarang, muat dokumen ke dalam`Editor` misalnya menggunakan`FileStream` Dan`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Lanjutkan ke langkah selanjutnya dalam blok penggunaan ini.
}
```
## Langkah 4: Akses dan Kelola Bidang Formulir
Dengan dokumen dimuat, Anda kini dapat mengakses dan memanipulasi bidang formulir.
### Langkah 4.1: Baca FormFieldManager
 Ambil`FormFieldManager` dari`Editor` contoh.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Langkah 4.2: Akses FormFieldCollection
 Ambil`FormFieldCollection` yang berisi semua bidang formulir dalam dokumen.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Langkah 4.3: Hapus Bidang Formulir Teks Tertentu
Untuk menghapus bidang formulir teks tertentu, temukan bidang tersebut berdasarkan namanya, lalu hapus.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Langkah 4.4: Hapus Beberapa Bidang Formulir
Anda juga dapat menghapus beberapa bidang formulir sekaligus dengan menentukan namanya.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Langkah 5: Simpan Dokumen yang Dimodifikasi
Setelah memodifikasi kolom formulir, Anda perlu menyimpan dokumen.
### Langkah 5.1: Buat Opsi Penyimpanan
Tentukan format dan opsi penyimpanan untuk dokumen keluaran.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Langkah 5.2: Optimalkan Penggunaan Memori
Jika berurusan dengan dokumen berukuran besar, Anda mungkin ingin mengoptimalkan penggunaan memori.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Langkah 5.3: Atur Perlindungan (Jika Diperlukan)
Anda dapat melindungi dokumen dari pengeditan lebih lanjut dengan mengatur kata sandi tulis.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Langkah 5.4: Simpan Dokumen
 Terakhir, simpan dokumen menggunakan a`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Kesimpulan
Selamat! Anda telah berhasil menghapus bidang formulir dari dokumen Word menggunakan GroupDocs.Editor untuk .NET. Pustaka canggih ini memudahkan manipulasi konten dokumen secara terprogram, sehingga menghemat waktu dan tenaga Anda.
## FAQ
### Bisakah saya menggunakan GroupDocs.Editor untuk .NET dengan format dokumen lain?
Ya, GroupDocs.Editor untuk .NET mendukung berbagai format dokumen, termasuk PDF, HTML, dan lainnya.
### Apakah mungkin menambahkan bidang formulir menggunakan GroupDocs.Editor untuk .NET?
Ya, Anda dapat menambah, mengubah, dan menghapus bidang formulir secara terprogram.
### Bagaimana jika dokumen saya sangat besar?
Anda dapat mengaktifkan pengoptimalan memori di opsi penyimpanan untuk menangani dokumen besar secara efisien.
### Bisakah saya menggunakan GroupDocs.Editor untuk .NET dalam aplikasi web?
Sangat! GroupDocs.Editor untuk .NET dapat diintegrasikan ke dalam aplikasi web untuk pemrosesan dokumen sisi server.
### Di mana saya bisa mendapatkan dukungan jika saya mengalami masalah?
 Anda dapat mengunjungi[forum dukungan](https://forum.groupdocs.com/c/editor/20) untuk bantuan dalam masalah apa pun.