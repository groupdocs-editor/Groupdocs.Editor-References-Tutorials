---
date: 2026-06-06
description: Pelajari cara membuat daftar format dokumen yang didukung dan menentukan
  ekstensi format file menggunakan GroupDocs.Editor untuk .NET. Panduan langkah demi
  langkah dengan cuplikan kode, jawaban cepat, dan FAQ.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Daftar Format Dokumen yang Didukung
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Daftar Format Dokumen yang Didukung dengan GroupDocs.Editor .NET
type: docs
url: /id/net/document-processing/work-document-formats/
weight: 13
---

# Daftar Format Dokumen yang Didukung

Selamat datang di tutorial komprehensif kami tentang **cara menampilkan daftar format dokumen yang didukung** dengan GroupDocs.Editor untuk .NET. Baik Anda sedang membangun aplikasi web yang berfokus pada dokumen maupun alat desktop kelas perusahaan, mengetahui secara tepat format apa yang dapat Anda edit atau konversi sangat penting. Dalam panduan ini Anda akan menemukan cara menenumerasi format, mengurai ekstensi, dan mengedit dokumen—semua dengan penjelasan yang jelas, ramah manusia, dan cuplikan kode siap dijalankan.

## Jawaban Cepat
- **Bagaimana cara menampilkan semua format yang didukung?** Gunakan `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (atau setara untuk Presentation/Spreadsheet) dan iterasi koleksinya.  
- **Bisakah saya menentukan format dari ekstensi file?** Ya—panggil `DocumentFormatInfo.FromExtension(".docx")`.  
- **Jenis file apa yang didukung oleh GroupDocs.Editor?** Lebih dari 30 format input dan output, termasuk DOCX, XLSX, PPTX, HTML, dan teks biasa.  
- **Apakah saya memerlukan lisensi untuk menampilkan format?** Lisensi sementara membuka penuh API; jika tidak, versi percobaan berfungsi dengan fitur terbatas.  
- **Versi .NET mana yang kompatibel?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu “daftar format dokumen yang didukung”?
Istilah ini merujuk pada pengambilan koleksi tipe file yang secara programatik dapat dibuka, diedit, dan disimpan oleh GroupDocs.Editor. Operasi ini memungkinkan Anda membangun dropdown UI dinamis atau memvalidasi unggahan pengguna sebelum diproses, memastikan hanya file yang kompatibel yang diteruskan ke editor untuk manipulasi lebih lanjut.

## Mengapa harus mencantumkan format dokumen yang didukung?
GroupDocs.Editor **mendukung lebih dari 30 format input dan output** serta dapat menangani file hingga **2 GB** tanpa memuat seluruh dokumen ke memori. Mengetahui daftar tepat mencegah kesalahan runtime, meningkatkan pengalaman pengguna, dan memungkinkan Anda menegakkan aturan bisnis seperti “hanya izinkan dokumen Office yang dapat diedit.” Ini juga membantu Anda menampilkan hanya format yang benar‑benar didukung aplikasi Anda.

## Prasyarat
Sebelum memulai, pastikan Anda memiliki:

1. **Lingkungan pengembangan .NET** – Visual Studio 2022 atau IDE apa pun yang mendukung .NET 6+.  
2. **Pustaka GroupDocs.Editor untuk .NET** – unduh dari [halaman rilis GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Lisensi sementara** – dapatkan [lisensi sementara](https://purchase.groupdocs.com/temporary-license/) untuk akses tanpa batas.  
4. **Pengetahuan dasar C#** – familiar dengan namespace, pernyataan `using`, dan output konsol.

## Cara Menampilkan Daftar Format Dokumen yang Didukung?
Muat koleksi format yang didukung dan cetak nama serta ekstensi masing‑masing. Pola dua langkah ini bekerja untuk dokumen Word Processing, Spreadsheet, dan Presentation. Dengan mengiterasi koleksi, Anda dapat secara dinamis mengisi elemen UI seperti dropdown, memastikan pengguna hanya dapat memilih format yang memang dapat ditangani editor.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Menampilkan Format Pengolahan Kata
`Formats.WordProcessingFormats` adalah enumerasi yang menggambarkan setiap tipe file pengolahan kata yang dikenali oleh editor. Properti `All` mengembalikan koleksi objek format ini.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Penjelasan:**  
1. **Iterasi Melalui Format:** Kami mengiterasi semua format pengolahan kata yang tersedia.  
2. **Tampilkan Detail Format:** Untuk setiap format kami mencetak nama yang bersahabat dan ekstensi file default.

### Menampilkan Format Presentasi
`Formats.PresentationFormats` bekerja dengan cara yang sama untuk file slide, menampilkan setiap tipe presentasi yang didukung melalui koleksi `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Penjelasan:**  
1. **Iterasi Melalui Format:** Logika iterasi yang sama diterapkan pada presentasi.  
2. **Tampilkan Detail Format:** Nama dan ekstensi ditampilkan untuk setiap format.

## Cara Menentukan Ekstensi Format File?
Terkadang Anda hanya memiliki nama file dan perlu menebak `DocumentFormat` yang sesuai. GroupDocs.Editor menyediakan helper statis yang langsung memetakan ekstensi file ke representasi format internal, memungkinkan Anda memvalidasi atau mengkonversi file sebelum memuatnya ke editor.

### Mengurai Format Spreadsheet
`Formats.SpreadsheetFormats.FromExtension` mengubah string ekstensi file menjadi nilai enum format spreadsheet yang cocok.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Penjelasan:**  
1. **Parse Format:** `FromExtension` mengubah ekstensi `.xlsm` menjadi enum `SpreadsheetFormat` internal.  
2. **Output Format:** Nama format yang diparse dicetak, mengonfirmasi pemetaan.

### Mengurai Format Teks
Demikian pula, `Formats.TextualFormats.FromExtension` menyelesaikan ekstensi file teks seperti HTML atau TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Penjelasan:**  
1. **Parse Format:** Metode `FromExtension` menyelesaikan ekstensi `html` menjadi `TextFormat`.  
2. **Output Format:** Nama format teks ditampilkan, berguna untuk editor berbasis web.

## Cara Mengedit Dokumen Setelah Menentukan Format?
Setelah Anda mengetahui formatnya, memuat dan mengedit dokumen mengikuti pola konsisten. Pertama buat instance `Editor` dengan path ke file sumber, lalu panggil `Edit()` untuk memperoleh `EditableDocument`. Dari sana Anda dapat membaca, memodifikasi, dan akhirnya menyimpan konten menggunakan `SaveOptions` yang sesuai.

### Memuat Dokumen
`Editor` adalah kelas inti yang membungkus semua operasi pengeditan untuk file tertentu.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Penjelasan:**  
1. **Inisialisasi Editor:** Buat instance `Editor`, berikan path lengkap file target.  
2. **Pola Dispose:** Pernyataan `using` menjamin semua sumber daya tak terkelola dilepaskan dengan cepat.

### Mengekstrak Konten
`EditableDocument.GetContent()` mengembalikan teks mentah dokumen (atau HTML untuk editor berbasis web), yang dapat Anda tampilkan atau manipulasi.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Penjelasan:**  
1. **Metode Edit:** `Edit()` mengembalikan objek `EditableDocument`.  
2. **Dapatkan Konten:** `GetContent()` mengekstrak teks mentah dokumen (atau HTML untuk editor berbasis web).  
3. **Output Konten:** Konten ditulis ke konsol untuk verifikasi.

### Menyimpan Perubahan
`SaveOptions` memberi tahu editor cara dan dalam format apa menulis kembali dokumen yang telah diedit ke penyimpanan.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Penjelasan:**  
1. **Metode Edit:** Dapatkan kembali `EditableDocument` setelah modifikasi.  
2. **Modifikasi Konten:** Terapkan perubahan pada string (tidak ditampilkan di sini).  
3. **Opsi Simpan:** Konfigurasikan `SaveOptions` dengan format output yang diinginkan.  
4. **Simpan Dokumen:** Persist file yang telah diedit kembali ke disk.

## Cara Bekerja dengan Berbagai Jenis Dokumen?
GroupDocs.Editor menyatukan penanganan Word, Spreadsheet, dan Presentation di balik antarmuka API yang sama, sehingga mudah beralih konteks tanpa harus mempelajari kumpulan kelas baru untuk tiap keluarga dokumen.

### Mengedit Dokumen Spreadsheet
`SpreadsheetSaveOptions` menentukan cara spreadsheet ditulis, termasuk format dan pengaturan kompresi opsional.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Penjelasan:**  
1. **Inisialisasi Editor:** Berikan path file spreadsheet ke konstruktor `Editor`.  
2. **Metode Edit:** Dapatkan `EditableDocument`.  
3. **Dapatkan Konten:** Cetak representasi CSV spreadsheet (atau HTML).  
4. **Modifikasi Konten:** Terapkan perubahan pada tingkat sel yang diperlukan.  
5. **Opsi Simpan:** Pilih `SpreadsheetSaveOptions` yang sesuai.  
6. **Simpan Dokumen:** Tulis spreadsheet yang telah diperbarui kembali ke penyimpanan.

### Mengedit Dokumen Presentasi
`PresentationSaveOptions` mengontrol format output untuk deck slide, memungkinkan Anda mempertahankan atau mengubah tipe file asli.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Penjelasan:**  
1. **Inisialisasi Editor:** Muat file PowerPoint melalui `Editor`.  
2. **Metode Edit:** Peroleh `EditableDocument`.  
3. **Dapatkan Konten:** Ekstrak HTML slide atau teks biasa.  
4. **Modifikasi Konten:** Perbarui judul, poin bullet, atau gambar.  
5. **Opsi Simpan:** Gunakan `PresentationSaveOptions` untuk menentukan format output.  
6. **Simpan Dokumen:** Persist presentasi yang telah diedit.

## Masalah Umum dan Solusinya
- **Kesalahan “Format not supported”:** Pastikan Anda menggunakan versi terbaru GroupDocs.Editor; versi terbaru secara rutin menambah dukungan untuk format Office yang lebih baru.  
- **Konsumsi memori file besar:** Aktifkan mode streaming dengan mengatur `EditorSettings.EnableStreaming = true` sebelum memuat dokumen.  
- **Lisensi tidak diterapkan:** Pastikan file lisensi sementara ditempatkan di root aplikasi atau dimuat via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Pertanyaan yang Sering Diajukan

**Q: Apa perbedaan antara `DocumentFormatInfo` dan `SaveOptions`?**  
**A:** `DocumentFormatInfo` memberikan metadata tentang tipe file yang didukung, sedangkan `SaveOptions` mengonfigurasi cara dokumen ditulis kembali ke disk (format, kompresi, dll.).

**Q: Bisakah saya menampilkan format untuk ekstensi file khusus?**  
**A:** Ya—gunakan `DocumentFormatInfo.FromExtension("yourExt")`; jika ekstensi tidak dikenali, metode akan mengembalikan `null`.

**Q: Apakah GroupDocs.Editor mendukung file yang dilindungi kata sandi?**  
**A:** Tentu saja. Berikan kata sandi ke konstruktor `Editor` melalui `EditorSettings` untuk membuka dokumen terenkripsi.

**Q: Berapa banyak format yang sebenarnya didukung oleh GroupDocs.Editor?**  
**A:** Lebih dari **30 format input dan output**, mencakup Word, Excel, PowerPoint, HTML, dan teks biasa.

**Q: Apakah ada cara membatasi daftar hanya pada format yang dapat diedit?**  
**A:** Gunakan `GetEditableWordProcessingFormats()` (atau setara Spreadsheet/Presentation) untuk mengambil format yang memungkinkan kemampuan edit penuh.

## Sumber Daya Tambahan
- Unduh pustaka dari [halaman rilis GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Dapatkan [lisensi sementara](https://purchase.groupdocs.com/temporary-license/) untuk akses penuh fitur.  
- Coba produk dengan [percobaan gratis](https://releases.groupdocs.com/).  
- Jelajahi contoh penggunaan terperinci dalam [dokumentasi GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Dapatkan bantuan dari komunitas di [forum dukungan](https://forum.groupdocs.com/c/editor/20).

## Kesimpulan
Dengan mengikuti panduan ini Anda kini tahu cara **menampilkan daftar format dokumen yang didukung**, **menentukan format file dari ekstensi**, dan **mengedit dokumen** di seluruh tipe Word, Spreadsheet, dan Presentation menggunakan GroupDocs.Editor untuk .NET. Integrasikan cuplikan kode ini ke dalam proyek Anda untuk membangun aplikasi yang sadar format, kuat, dan memberikan pengalaman pengguna yang mulus serta mengurangi kesalahan runtime.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## Tutorial Terkait

- [Menguasai Pemuatan Dokumen di .NET dengan GroupDocs.Editor: Panduan Komprehensif](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Menguasai Pengeditan Dokumen di .NET dengan GroupDocs.Editor: Panduan Komprehensif](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Mengonversi Word ke HTML Menggunakan GroupDocs.Editor .NET: Panduan Langkah‑per‑Langkah](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)