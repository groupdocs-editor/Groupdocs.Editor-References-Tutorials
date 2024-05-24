---
title: Ambil Konten HTML dengan Awalan
linktitle: Ambil Konten HTML dengan Awalan
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengambil konten HTML dari dokumen menggunakan GroupDocs.Editor untuk .NET dengan awalan khusus untuk gambar dan stylesheet. Panduan langkah demi langkah disertakan.
type: docs
weight: 11
url: /id/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## Perkenalan
Selamat datang di tutorial langkah demi langkah kami tentang cara mengambil konten HTML dari dokumen menggunakan GroupDocs.Editor untuk .NET. Baik Anda seorang pengembang berpengalaman atau baru memulai, panduan ini akan memandu Anda melalui proses dengan cara yang mudah diikuti. Kami akan membahas semua yang perlu Anda ketahui, mulai dari menyiapkan lingkungan hingga mengeksekusi kode dengan sukses. Ayo selami!
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:
1.  GroupDocs.Editor untuk .NET: Unduh versi terbaru dari[Unduh Halaman](https://releases.groupdocs.com/editor/net/).
2. Lingkungan Pengembangan: Visual Studio atau lingkungan pengembangan .NET pilihan lainnya.
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda mengikuti contoh.
4. Dokumen untuk Diedit: Siapkan contoh dokumen untuk pengujian, seperti dokumen Word.
5. .NET Framework: Pastikan Anda telah menginstal .NET Framework di mesin Anda.
Sekarang setelah semuanya siap, mari kita mulai!
## Impor Namespace
Pertama, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Namespace ini menyediakan kelas dan metode yang diperlukan untuk bekerja dengan GroupDocs.Editor untuk .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Dengan namespace yang diimpor, kita dapat melanjutkan ke pengaturan editor.
## Langkah 1: Inisialisasi Editor
 Untuk memulai, Anda perlu menginisialisasi`Editor`kelas dengan dokumen Anda. Langkah ini melibatkan penentuan dokumen yang ingin Anda edit dan menyediakan opsi pemuatan yang diperlukan.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Langkah lebih lanjut akan ditambahkan di sini
}
```
 Dalam contoh ini, kami memuat dokumen Word. Anda bisa menggantinya`"Your Sample Document"` dengan jalur ke dokumen Anda.
## Langkah 2: Edit Dokumen
 Selanjutnya, kita perlu membuka dokumen untuk diedit. Ini dilakukan dengan menggunakan`Edit` metode`Editor` kelas, yang membutuhkan`WordProcessingEditOptions` sebagai argumen.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Langkah lebih lanjut akan ditambahkan di sini
}
```
 Itu`EditableDocument` instance mewakili dokumen dalam format yang dapat diedit. Sekarang kami siap mengambil konten HTML.
## Langkah 3: Tentukan Awalan Kustom
Untuk menambahkan awalan khusus untuk gambar dan CSS, kita perlu mendefinisikan awalan sebagai string. Langkah ini memastikan bahwa konten HTML akan memiliki awalan yang ditentukan untuk sumber daya eksternal.
```csharp
string externalImagesPrefix = "http://www.situswebsaya.com/images/id=";
string externalCssPrefix = "http://www.situswebsaya.com/css/id=";
```
Anda dapat mengganti URL dengan awalan yang Anda inginkan. Awalan ini akan digunakan pada langkah berikutnya untuk menyesuaikan keluaran HTML.
## Langkah 4: Ambil Konten HTML
Sekarang setelah awalan kita disetel, kita dapat mengambil konten HTML dari dokumen. Itu`GetContent` metode`EditableDocument` kelas memungkinkan kita menentukan awalan gambar dan CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Cuplikan kode ini mengambil konten HTML dengan awalan khusus dan mencetaknya ke konsol. Anda dapat memproses lebih lanjut atau menyimpan konten HTML ini sesuai kebutuhan.
## Kesimpulan
Dan itu dia! Dengan mengikuti langkah-langkah ini, Anda dapat dengan mudah mengambil konten HTML dari dokumen menggunakan GroupDocs.Editor untuk .NET, lengkap dengan awalan khusus untuk gambar dan stylesheet. Alat canggih ini menyederhanakan manipulasi dokumen, memungkinkan Anda fokus pada pengintegrasian pengeditan dokumen ke dalam aplikasi .NET Anda dengan mulus.
 Untuk informasi lebih detail, lihat[GroupDocs.Editor untuk dokumentasi .NET](https://reference.groupdocs.com/editor/net/) . Jika Anda memiliki pertanyaan atau memerlukan bantuan lebih lanjut, jangan ragu untuk menghubungi[forum dukungan](https://forum.groupdocs.com/c/editor/20).
## FAQ
### Jenis dokumen apa yang dapat saya edit dengan GroupDocs.Editor untuk .NET?
GroupDocs.Editor mendukung berbagai format dokumen termasuk Word, Excel, PowerPoint, PDF, dan banyak lagi.
### Bagaimana cara mendapatkan uji coba gratis GroupDocs.Editor untuk .NET?
 Anda bisa mendapatkan uji coba gratis dari[Situs web GroupDocs](https://releases.groupdocs.com/).
### Bisakah saya menyesuaikan konten HTML lebih lanjut?
Ya, Anda dapat memodifikasi konten HTML yang diambil sesuai kebutuhan sebelum merender atau menyimpannya.
### Apakah mungkin menggunakan GroupDocs.Editor untuk .NET dengan bahasa .NET lainnya?
Ya, Anda dapat menggunakannya dengan bahasa apa pun yang kompatibel dengan .NET seperti VB.NET atau F#.
### Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Editor untuk .NET?
 Anda bisa mendapatkan lisensi sementara dari[halaman pembelian](https://purchase.groupdocs.com/temporary-license/).