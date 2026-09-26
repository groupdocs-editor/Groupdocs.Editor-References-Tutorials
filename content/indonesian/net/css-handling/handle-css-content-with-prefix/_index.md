---
date: 2026-09-26
description: Pelajari cara menangani prefix css dan mengekstrak konten css menggunakan
  GroupDocs.Editor for .NET dalam tutorial terperinci langkah demi langkah ini.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Tangani Konten CSS dengan Prefix
og_description: Temukan cara menangani prefix css dan mengekstrak konten css dengan
  GroupDocs.Editor for .NET. Ikuti panduan langkah demi langkah untuk menambahkan
  URL ke sumber daya CSS dan mengambil stylesheet.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Cara menangani prefix css di GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Cara menangani prefix css di GroupDocs.Editor for .NET
type: docs
url: /id/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Cara menangani prefix css di GroupDocs.Editor untuk .NET

Dalam tutorial ini Anda akan belajar **cara menangani prefix css** saat bekerja dengan stylesheet di dalam dokumen menggunakan GroupDocs.Editor untuk .NET. Apakah Anda perlu menambahkan URL ke gambar, font, atau sumber daya eksternal apa pun, langkah‑langkah di bawah ini menunjukkan secara tepat cara **menangani prefix css** dan juga cara **mengekstrak konten css** untuk pemrosesan lebih lanjut. Pada akhir panduan Anda akan dapat menulis ulang jalur sumber daya, mengambil string CSS mentah, dan mengintegrasikannya ke dalam alur kerja web Anda dengan percaya diri.

## Jawaban Cepat
- **Apa arti “handle css prefix”?** Menambahkan prefix URL khusus ke sumber daya eksternal yang direferensikan dalam CSS.  
- **Metode API mana yang mengembalikan gaya CSS?** `EditableDocument.GetCssContent(...)`.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan tersedia; lisensi komersial diperlukan untuk produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+ dan .NET Core/5/6.  
- **Bisakah saya mengubah prefix saat runtime?** Ya – cukup berikan string yang berbeda ke `GetCssContent`.

## Apa itu handle css prefix?
Istilah ini merujuk pada penulisan ulang URL gambar, font, atau aset eksternal apa pun di dalam file CSS sehingga mereka mengarah ke lokasi yang Anda kontrol, seperti CDN atau server aman. Dengan menambahkan prefix URL dasar yang konsisten, Anda menjamin setiap sumber daya dimuat dengan benar ketika dokumen dirender di browser atau penampil berbasis web.

## Mengapa menggunakan GroupDocs.Editor untuk mengekstrak konten css?
GroupDocs.Editor dapat membaca CSS asli yang tertanam dalam dokumen WordProcessing, mengembalikan string stylesheet mentah, dan memungkinkan Anda memanipulasinya sebelum merender atau menyimpan. Ini menghilangkan parsing manual, menjamin kesetiaan pada representasi internal dokumen, dan mendukung **30+ format file** sambil memproses file hingga **500 MB** tanpa harus memuat seluruh file ke memori.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki prasyarat berikut:
- Visual Studio: Anda memerlukan instalasi Visual Studio yang berfungsi.  
- .NET Framework: Pastikan Anda telah menginstal .NET Framework.  
- GroupDocs.Editor for .NET: Anda dapat mengunduhnya dari halaman [GroupDocs.Editor for .NET download page](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Siapkan dokumen contoh yang siap diedit.

## Impor namespace
Pertama, mari impor namespace yang diperlukan untuk memastikan kode kita berjalan lancar. Langkah ini memberi kita akses ke kelas inti GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Langkah 1: Inisialisasi Editor
Kelas `Editor` adalah titik masuk untuk bekerja dengan dokumen di GroupDocs.Editor. Ia mengelola operasi memuat, mengedit, dan menyimpan.  
Langkah pertama melibatkan pembuatan instance `Editor` dengan dokumen contoh Anda. Ini menyiapkan lingkungan pengeditan.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Langkah 2: Edit dokumen
Objek `EditableDocument` mewakili versi yang dapat diedit dari file dan mengekspos bagian internalnya, seperti CSS, gambar, dan HTML.  
Selanjutnya, kami memperoleh objek `EditableDocument`. Objek ini memungkinkan kami bekerja dengan CSS internal dokumen.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Langkah 3: Atur prefix eksternal
Tentukan prefix URL untuk gambar dan font. Prefix ini akan ditambahkan ke setiap referensi gambar dan font yang ditemukan dalam CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Langkah 4: Ekstrak konten css dengan prefix
`GetCssContent` mengembalikan koleksi string stylesheet CSS yang sudah berisi URL yang diprefix sesuai yang Anda berikan.  
Panggil `GetCssContent`, dengan memberikan prefix yang baru saja Anda definisikan. Metode ini mengembalikan daftar string stylesheet CSS yang sudah berisi URL yang diprefix.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Langkah 5: Tampilkan hasil
Cetak jumlah stylesheet yang ditemukan dan tampilkan setiap stylesheet. Ini membantu Anda memverifikasi bahwa prefix telah diterapkan dengan benar.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Masalah umum dan solusi
- **Tidak ada stylesheet yang dikembalikan** – Pastikan dokumen sumber memang berisi CSS (misalnya, dokumen Word dengan tabel berformat atau HTML tersemat).  
- **URL tidak tepat** – Periksa kembali bahwa string prefix berakhir dengan pemisah yang sesuai (`/` atau `=`) untuk routing server Anda.  
- **Kekhawatiran kinerja** – Untuk dokumen yang sangat besar, pertimbangkan memproses stylesheet secara batch untuk menghindari penggunaan memori yang tinggi.

## Pertanyaan yang sering diajukan

**Q:** Apakah saya dapat menggunakan GroupDocs.Editor untuk .NET dengan format dokumen lain?  
**A:** Ya, GroupDocs.Editor untuk .NET mendukung PDF, Word, Excel, PowerPoint, dan banyak format lainnya.

**Q:** Apakah ada percobaan gratis untuk GroupDocs.Editor untuk .NET?  
**A:** Tentu saja! Anda dapat memulai percobaan gratis Anda di halaman [GroupDocs free trial page](https://releases.groupdocs.com/).

**Q:** Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Editor untuk .NET?  
**A:** Anda dapat memperoleh lisensi sementara dari [temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q:** Di mana saya dapat menemukan dokumentasi detail untuk GroupDocs.Editor untuk .NET?  
**A:** Dokumentasi detail tersedia di situs [GroupDocs.Editor for .NET documentation site](https://tutorials.groupdocs.com/editor/net/).

**Q:** Opsi dukungan apa yang tersedia untuk GroupDocs.Editor untuk .NET?  
**A:** Anda dapat mendapatkan dukungan melalui [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

## Pertanyaan tambahan yang sering diajukan

**Q:** Apakah saya dapat mengubah prefix setelah mengekstrak CSS?  
**A:** Ya. Panggil `GetCssContent` lagi dengan string prefix yang berbeda; metode ini selalu menggunakan nilai yang Anda berikan pada runtime.

**Q:** Apakah ini berfungsi dengan dokumen yang dilindungi kata sandi?  
**A:** Ya. Berikan kata sandi dalam `WordProcessingLoadOptions` saat membuat instance `Editor`.

**Q:** Apakah memungkinkan menyimpan CSS yang telah dimodifikasi kembali ke dalam dokumen?  
**A:** GroupDocs.Editor saat ini hanya menyediakan akses baca‑saja ke CSS. Untuk mempertahankan perubahan, Anda harus mengganti stylesheet asli menggunakan API XML dasar dokumen.

---

**Terakhir Diperbarui:** 2026-09-26  
**Diuji Dengan:** GroupDocs.Editor 23.12 untuk .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Extract External CSS from Word Docs Using GroupDocs.Editor .NET&#58; A Comprehensive Guide](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extract & Prefix HTML from Word Docs using GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [How to Extract and Modify HTML Content in Word Documents Using GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)