---
date: 2026-03-06
description: Pelajari cara menangani konten CSS dengan prefix dan mengekstrak konten
  CSS menggunakan GroupDocs.Editor untuk .NET dalam tutorial langkah demi langkah
  yang mendetail ini.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Tangani Konten CSS dengan Awalan
type: docs
url: /id/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Menangani Konten CSS dengan Prefiks

Dalam tutorial ini Anda akan menemukan **cara menangani prefiks css** saat bekerja dengan stylesheet di dalam dokumen menggunakan GroupDocs.Editor untuk .NET. Baik Anda perlu menambahkan URL ke gambar, font, atau sumber eksternal apa pun, langkah‑langkah di bawah ini menunjukkan secara tepat cara **menangani prefiks css** dan juga cara **mengekstrak konten css** untuk pemrosesan lebih lanjut.

## Jawaban Cepat
- **Apa arti “handle css prefix”?** Menambahkan prefiks URL khusus ke sumber eksternal yang direferensikan dalam CSS.  
- **Metode API mana yang mengembalikan gaya CSS?** `EditableDocument.GetCssContent(...)`.  
- **Apakah saya memerlukan lisensi?** Lisensi percobaan tersedia; lisensi komersial diperlukan untuk produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+ dan .NET Core/5/6.  
- **Bisakah saya mengubah prefiks saat runtime?** Ya – cukup berikan string yang berbeda ke `GetCssContent`.

## Apa itu **handle css prefix**?
Menerapkan prefiks pada sumber daya CSS menulis ulang jalur gambar, font, atau aset lainnya sehingga mereka mengarah ke lokasi yang Anda kontrol (misalnya, CDN atau server yang aman). Ini sangat berguna ketika Anda mengekspor dokumen dan memerlukan semua referensi eksternal dapat diakses dari aplikasi web.

## Mengapa menggunakan GroupDocs.Editor untuk **extract css content**?
GroupDocs.Editor dapat membaca CSS asli yang tertanam dalam dokumen WordProcessing, memberikan Anda string stylesheet mentah, dan memungkinkan Anda memanipulasinya sebelum dirender atau disimpan. Ini menghilangkan kebutuhan parsing manual dan menjamin bahwa CSS yang diekstrak cocok dengan representasi internal dokumen.

## Prasyarat
- Visual Studio: Anda memerlukan instalasi Visual Studio yang berfungsi.  
- .NET Framework: Pastikan Anda telah menginstal .NET Framework.  
- GroupDocs.Editor untuk .NET: Anda dapat mengunduhnya [di sini](https://releases.groupdocs.com/editor/net/).  
- Dokumen Contoh: Siapkan dokumen contoh siap untuk diedit.

## Impor Namespace
Pertama, mari impor namespace yang diperlukan untuk memastikan kode kami berjalan lancar. Langkah ini memberi kami akses ke kelas inti GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Langkah 1: Inisialisasi Editor
Langkah pertama melibatkan pembuatan instance `Editor` dengan dokumen contoh Anda. Ini menyiapkan lingkungan pengeditan.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Langkah 2: Edit Dokumen
Selanjutnya, kami memperoleh objek `EditableDocument`. Objek ini mewakili versi yang dapat diedit dari file dan memungkinkan kami bekerja dengan bagian internalnya.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Langkah 3: Atur Prefiks Eksternal
Tentukan prefiks URL untuk gambar dan font. Prefiks ini akan ditambahkan di depan setiap referensi gambar dan font yang ditemukan dalam CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Langkah 4: **Extract CSS content** dengan Prefiks
Panggil `GetCssContent`, dengan memberikan prefiks yang baru saja Anda definisikan. Metode ini mengembalikan daftar string stylesheet CSS yang sudah berisi URL dengan prefiks.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Langkah 5: Keluarkan Hasil
Cetak jumlah stylesheet yang ditemukan dan tampilkan setiap stylesheet. Ini membantu Anda memverifikasi bahwa prefiks telah diterapkan dengan benar.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Masalah Umum dan Solusinya
- **Tidak ada stylesheet yang dikembalikan** – Pastikan dokumen sumber memang berisi CSS (misalnya, dokumen Word dengan tabel berformat atau HTML yang disematkan).  
- **URL tidak tepat** – Periksa kembali bahwa string prefiks diakhiri dengan delimiter yang sesuai (`/` atau `=`) untuk routing server Anda.  
- **Kekhawatiran kinerja** – Untuk dokumen yang sangat besar, pertimbangkan memproses stylesheet secara batch untuk menghindari penggunaan memori yang tinggi.

## Kesimpulan
Menangani konten CSS dengan prefiks menggunakan GroupDocs.Editor untuk .NET adalah sederhana dan kuat. Dengan mengikuti langkah‑langkah ini Anda dapat **menangani prefiks css**, mengambil CSS mentah melalui **extract css content**, dan mengintegrasikan sumber daya eksternal secara mulus ke dalam alur kerja web Anda. Jelajahi fitur GroupDocs.Editor lainnya seperti konversi HTML, ekstraksi gambar, dan penggabungan dokumen untuk mendapatkan nilai lebih dari API.

## FAQ
### Bisakah saya menggunakan GroupDocs.Editor untuk .NET dengan format dokumen lain?
Ya, GroupDocs.Editor untuk .NET mendukung berbagai format dokumen termasuk PDF, Word, Excel, dan lainnya.

### Apakah ada percobaan gratis yang tersedia untuk GroupDocs.Editor untuk .NET?
Tentu saja! Anda dapat memulai percobaan gratis Anda [di sini](https://releases.groupdocs.com/).

### Bagaimana cara mendapatkan lisensi sementara untuk GroupDocs.Editor untuk .NET?
Anda dapat memperoleh lisensi sementara [di sini](https://purchase.groupdocs.com/temporary-license/).

### Di mana saya dapat menemukan dokumentasi terperinci untuk GroupDocs.Editor untuk .NET?
Dokumentasi terperinci tersedia [di sini](https://tutorials.groupdocs.com/editor/net/).

### Opsi dukungan apa yang tersedia untuk GroupDocs.Editor untuk .NET?
Anda dapat mendapatkan dukungan [di sini](https://forum.groupdocs.com/c/editor/20).

## Pertanyaan Umum Tambahan

**Q: Bisakah saya mengubah prefiks setelah mengekstrak CSS?**  
A: Ya. Panggil `GetCssContent` lagi dengan string prefiks yang berbeda; metode ini selalu menggunakan nilai yang Anda berikan pada runtime.

**Q: Apakah ini bekerja dengan dokumen yang dilindungi kata sandi?**  
A: Ya. Berikan kata sandi dalam `WordProcessingLoadOptions` saat membuat instance `Editor`.

**Q: Apakah memungkinkan menyimpan CSS yang dimodifikasi kembali ke dalam dokumen?**  
A: GroupDocs.Editor saat ini menyediakan akses baca‑saja ke CSS. Untuk mempertahankan perubahan, Anda perlu mengganti stylesheet asli menggunakan API XML dasar dokumen.

---

**Last Updated:** 2026-03-06  
**Tested With:** GroupDocs.Editor 23.12 for .NET  
**Author:** GroupDocs