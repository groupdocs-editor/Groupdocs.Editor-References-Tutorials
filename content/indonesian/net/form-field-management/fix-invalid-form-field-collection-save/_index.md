---
title: Perbaiki Pengumpulan Bidang Formulir yang Tidak Valid dan Simpan
linktitle: Perbaiki Pengumpulan Bidang Formulir yang Tidak Valid dan Simpan
second_title: GroupDocs.Editor .NET API
description: Pelajari cara memperbaiki kolom formulir yang tidak valid di DOCX menggunakan Groupdocs.Editor untuk .NET. Ikuti panduan ini untuk memastikan dokumen Anda bebas dari kesalahan dan menyimpannya dengan aman.
weight: 11
url: /id/net/form-field-management/fix-invalid-form-field-collection-save/
---
## Perkenalan
Selamat datang! Jika Anda bekerja dengan bidang formulir di dokumen dan menghadapi masalah dengan kumpulan bidang formulir yang tidak valid, Anda berada di tempat yang tepat. Dalam tutorial ini, kita akan mendalami cara memperbaiki kolom formulir yang tidak valid dan menyimpan dokumen Anda menggunakan Groupdocs.Editor untuk .NET. Kami akan memandu Anda melalui proses langkah demi langkah, memastikan Anda memiliki semua detail yang diperlukan agar prosesnya berjalan lancar. Mari kita mulai!
## Prasyarat
Sebelum kita beralih ke kode, ada beberapa hal yang perlu Anda siapkan:
-  Groupdocs.Editor untuk .NET: Pastikan Anda telah menginstal perpustakaan Groupdocs.Editor untuk .NET. Anda dapat mengunduhnya[Di Sini](https://releases.groupdocs.com/editor/net/).
- Lingkungan Pengembangan: Anda harus menyiapkan lingkungan pengembangan .NET, seperti Visual Studio.
- Pengetahuan Dasar C#: Tutorial ini mengasumsikan Anda memiliki pemahaman dasar tentang pemrograman C#.
## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Tambahkan baris berikut di awal file kode Anda:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Langkah 1: Dapatkan Jalur File Input
Langkah pertama adalah menentukan jalur ke file masukan Anda. File ini harus berupa dokumen DOCX yang berisi kolom formulir.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Langkah 2: Buat Aliran dari Jalur File
Selanjutnya, buat aliran file untuk membaca dokumen masukan. Ini akan memungkinkan Anda memuat dokumen ke dalam editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Langkah 3: Buat Opsi Muat untuk Dokumen
Pada langkah ini, Anda perlu membuat opsi pemuatan untuk dokumen Anda. Jika dokumen Anda dilindungi kata sandi, Anda dapat menentukan kata sandinya. Dalam contoh ini, dokumen tidak dilindungi, sehingga kata sandinya diabaikan.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Langkah 4: Muat Dokumen ke dalam Mesin Virtual Editor
Sekarang, muat dokumen dengan opsi yang ditentukan ke dalam instance Editor. Di sinilah operasi utama pada dokumen akan dilakukan.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Langkah 4.1: Baca Instance FormFieldManager
 Itu`FormFieldManager` instance bertanggung jawab untuk mengelola bidang formulir dalam dokumen. Anda harus membaca instance ini untuk mengakses dan memanipulasi kolom formulir.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Langkah 4.2: Baca FormFieldCollection
 Itu`FormFieldCollection` berisi semua bidang formulir dalam dokumen. Anda akan membaca koleksi ini untuk memeriksa dan memperbaiki kolom formulir yang tidak valid.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Langkah 4.3: Perbaiki Otomatis Bidang Formulir yang Tidak Valid
Cobalah untuk memperbaiki secara otomatis setiap bidang formulir yang tidak valid dalam dokumen. Ini adalah langkah awal untuk mengatasi permasalahan yang sudah jelas.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Langkah 4.4: Periksa Bidang Formulir yang Tidak Valid
Periksa apakah masih ada kolom formulir tidak valid yang tersisa setelah upaya perbaikan otomatis.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Langkah 4.4.1: Dapatkan Semua Nama Bidang Formulir yang Tidak Valid
Ambil nama semua bidang formulir yang tidak valid. Nama-nama ini akan digunakan untuk memperbaiki bidang tersebut.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Langkah 4.4.2: Buat Nama Unik untuk Bidang yang Tidak Valid
Untuk setiap bidang formulir yang tidak valid, buat nama unik. Hal ini memastikan tidak ada konflik dengan nama kolom formulir yang ada.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Langkah 4.4.3: Perbaiki Bidang Formulir yang Tidak Valid
Perbaiki bidang formulir yang tidak valid menggunakan nama unik yang dibuat pada langkah sebelumnya.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Langkah 5: Buat Opsi Penyimpanan Dokumen
Atur opsi untuk menyimpan dokumen. Ini termasuk menentukan format dan pengaturan penyimpanan tambahan apa pun.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Langkah 5.1: Optimalkan Penggunaan Memori
 Jika dokumen Anda berukuran besar dan dapat menyebabkan`OutOfMemoryException`aktifkan opsi pengoptimalan memori.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Langkah 5.2: Lindungi Dokumen dari Penulisan
Untuk melindungi dokumen agar tidak diubah, kecuali untuk bidang formulir, tetapkan kata sandi perlindungan.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Langkah 6: Simpan Dokumen
Terakhir, simpan dokumen dengan opsi penyimpanan yang ditentukan. Siapkan aliran memori untuk menyimpan dokumen keluaran.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Kesimpulan
 Dan itu dia! Anda telah berhasil memperbaiki kolom formulir yang tidak valid dan menyimpan dokumen Anda menggunakan Groupdocs.Editor untuk .NET. Panduan langkah demi langkah ini seharusnya membuat prosesnya jelas dan mudah dikelola. Jika Anda mengalami masalah atau memiliki pertanyaan, silakan periksa[dokumentasi](https://tutorials.groupdocs.com/editor/net/) atau menjangkau[mendukung](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Bagaimana jika dokumen saya dilindungi kata sandi?
 Anda dapat menentukan kata sandi di`WordProcessingLoadOptions` untuk membuka dokumen.
### Bagaimana saya tahu jika ada kolom formulir yang tidak valid?
 Menggunakan`HasInvalidFormFields` metode untuk memeriksa bidang formulir yang tidak valid dalam dokumen.
### Bisakah saya memperbaiki kolom formulir tanpa mengubah namanya?
Disarankan untuk membuat nama unik untuk bidang formulir yang tidak valid untuk menghindari konflik.
### Dalam format apa saya dapat menyimpan dokumen?
 Anda dapat menyimpan dokumen dalam berbagai format seperti DOCX, PDF, dan lainnya dengan mengatur yang sesuai`WordProcessingFormats`.
### Bagaimana cara mengoptimalkan penggunaan memori sekaligus menyimpan dokumen berukuran besar?
 Aktifkan`OptimizeMemoryUsage` pilihan di`WordProcessingSaveOptions` untuk menangani dokumen besar secara efisien.