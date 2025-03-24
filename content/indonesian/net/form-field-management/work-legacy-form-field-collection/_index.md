---
title: Bekerja dengan Koleksi Bidang Formulir Warisan
linktitle: Bekerja dengan Koleksi Bidang Formulir Warisan
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengelola bidang formulir lama menggunakan GroupDocs.Editor untuk .NET dengan panduan terperinci kami. Sempurna untuk menangani bidang teks, kotak centang, tanggal, dan banyak lagi.
weight: 12
url: /id/net/form-field-management/work-legacy-form-field-collection/
---
## Perkenalan
Selamat datang di panduan komprehensif tentang cara bekerja dengan kumpulan bidang formulir lama menggunakan GroupDocs.Editor untuk .NET. Baik Anda menangani bidang teks, kotak centang, bidang tanggal, atau menu tarik-turun, tutorial ini akan memandu Anda melalui setiap langkah untuk mengelola bidang ini secara efisien. Di akhir panduan ini, Anda akan memiliki pemahaman yang kuat tentang cara memanfaatkan GroupDocs.Editor untuk menangani berbagai bidang formulir di dokumen Anda. Ayo selami!
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
- Visual Studio: Versi terbaru apa pun akan berfungsi.
- .NET Framework: Pastikan Anda telah menginstal .NET Framework.
-  GroupDocs.Editor untuk .NET: Unduh versi terbaru[Di Sini](https://releases.groupdocs.com/editor/net/).
- Contoh Dokumen: Contoh file DOCX dengan kolom formulir untuk tujuan pengujian.
## Impor Namespace
Untuk memulainya, impor namespace yang diperlukan dalam proyek Anda. Namespace ini penting untuk mengakses kelas dan metode yang diperlukan untuk memanipulasi kolom formulir.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Langkah 1: Dapatkan Jalur File Input
Pertama, Anda perlu menentukan jalur ke file masukan Anda. Dalam contoh ini, kita akan menggunakan contoh file DOCX yang berisi berbagai bidang formulir.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Langkah 2: Buat Aliran dari Jalur File
Selanjutnya, buat aliran file untuk membaca konten dokumen Anda. Aliran ini akan digunakan untuk memuat dokumen ke GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Kode tambahan akan dimasukkan ke sini
}
```
## Langkah 3: Buat Opsi Muat untuk Dokumen
Sebelum memuat dokumen, buat opsi pemuatan. Opsi ini akan membantu menangani berbagai skenario, seperti dokumen yang dilindungi kata sandi.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Jika dokumen dilindungi kata sandi, tentukan kata sandinya
loadOptions.Password = "your_password_here"; // Gunakan kata sandi sebenarnya jika perlu
```
## Langkah 4: Muat Dokumen dengan Editor Instance
Sekarang, muat dokumen ke dalam instance Editor menggunakan aliran file dan opsi muat yang Anda buat sebelumnya.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Kode tambahan akan dimasukkan ke sini
}
```
## Langkah 5: Baca Instance FormFieldManager
Untuk mengelola bidang formulir, akses instans FormFieldManager dari Editor. Contoh ini akan memungkinkan Anda untuk berinteraksi dengan bidang formulir dalam dokumen Anda.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Langkah 6: Baca FormFieldCollection
Ambil FormFieldCollection dari FormFieldManager. Koleksi ini berisi semua bidang formulir yang ada dalam dokumen.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Langkah 7: Iterasi Melalui Setiap Bidang Formulir
Ulangi setiap bidang formulir dalam koleksi dan identifikasi jenisnya. Bergantung pada jenisnya, Anda dapat mengekstrak dan memanipulasi nilai bidang.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Langkah 8: Kesimpulan
Dengan mengikuti langkah-langkah ini, Anda dapat secara efektif mengelola dan berinteraksi dengan bidang formulir lama di dokumen Anda menggunakan GroupDocs.Editor untuk .NET. Baik itu bidang teks, kotak centang, tanggal, angka, atau dropdown, panduan ini memberikan cara yang jelas dan ringkas untuk menangani setiap jenis.
## Kesimpulan
 Bekerja dengan bidang formulir lama di dokumen dapat dilakukan dengan mudah jika menggunakan alat yang tepat. GroupDocs.Editor untuk .NET memberikan solusi tangguh untuk mengelola bidang ini secara efisien. Dengan mengikuti panduan langkah demi langkah ini, Anda sekarang dapat memanipulasi berbagai bidang formulir di dokumen Anda dengan mudah. Jangan lupa untuk menjelajahinya[dokumentasi](https://tutorials.groupdocs.com/editor/net/)untuk fitur dan opsi lebih lanjut.
## FAQ
### 1. Bisakah saya menggunakan GroupDocs.Editor untuk .NET dengan dokumen yang dilindungi kata sandi?
Ya, Anda dapat menentukan kata sandi dalam opsi pemuatan untuk menangani dokumen yang dilindungi kata sandi.
### 2. Bagaimana cara mendapatkan uji coba gratis GroupDocs.Editor untuk .NET?
 Anda dapat mengunduh uji coba gratis dari[Di Sini](https://releases.groupdocs.com/).
### 3. Apakah ada dukungan yang tersedia untuk GroupDocs.Editor untuk .NET?
 Ya, Anda dapat mengakses dukungan[Di Sini](https://forum.groupdocs.com/c/editor/20).
### 4. Dapatkah saya membeli lisensi GroupDocs.Editor untuk .NET?
 Ya, Anda dapat membeli lisensi dari[Di Sini](https://purchase.groupdocs.com/buy).
### 5. Di mana saya dapat menemukan dokumentasi GroupDocs.Editor untuk .NET?
Dokumentasi tersedia[Di Sini](https://tutorials.groupdocs.com/editor/net/).