---
date: 2026-06-06
description: Pelajari cara **membuat dokumen yang dapat diedit** dari file CSV dan
  TSV menggunakan GroupDocs.Editor untuk .NET. Panduan ini juga menunjukkan cara **membaca
  teks terdelimit C#** dan **mengedit CSV .NET** secara efisien di Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Bekerja dengan Nilai Terpisah Delimited (DSV) – buat dokumen yang dapat
  diedit
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Bekerja dengan Nilai Terpisah Delimited (DSV) – buat dokumen yang dapat diedit
type: docs
url: /id/net/document-processing/work-dsv/
weight: 12
---

# Bekerja dengan Nilai Terpisah Delimited (DSV) – buat dokumen yang dapat diedit

Jika Anda seorang pengembang .NET yang perlu **create editable document** objek dari nilai terpisah delimited (DSV) seperti CSV atau TSV, Anda berada di tempat yang tepat. Dalam 100 kata pertama kami akan menjelaskan mengapa GroupDocs.Editor untuk .NET adalah cara paling andal untuk **read delimited text C#**, mengeditnya, dan kemudian menyimpannya kembali tanpa kehilangan format. Anda akan mendapatkan alur kerja lengkap yang siap disalin‑tempel dan cocok secara alami dalam solusi Visual Studio apa pun.

## Jawaban Cepat
- **Library mana yang menangani penyuntingan CSV terbaik di .NET?** GroupDocs.Editor for .NET.
- **Bisakah saya menyunting file CSV besar di Visual Studio?** Ya – API mem-stream data dan menghindari memuat seluruh file ke memori.
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Lisensi komersial diperlukan; percobaan gratis tersedia.
- **Format apa yang dapat saya hasilkan setelah penyuntingan?** CSV, TSV, dan format spreadsheet yang kompatibel dengan Excel.
- **Apakah API kompatibel dengan .NET 6+?** Tentu – mendukung .NET Framework 4.5+, .NET Core 3.1+, .NET 5, dan .NET 6.

## Apa itu “create editable document” dalam konteks GroupDocs.Editor?
**Create editable document** berarti menghasilkan sebuah instance `EditableDocument` yang mewakili versi yang dapat diubah dari file sumber (CSV, TSV, dll.) dalam memori. Objek ini memungkinkan Anda membaca, memodifikasi, dan menyimpan kembali konten menggunakan API yang sama. Ia menyediakan metode untuk mengambil teks dokumen, menerapkan perubahan, dan menyimpannya kembali dalam berbagai format, memastikan bahwa penjajaran kolom dan kutipan tetap terjaga.

## Mengapa menggunakan GroupDocs.Editor untuk penanganan DSV?
GroupDocs.Editor memproses **lebih dari 50 format input dan output**, termasuk CSV, TSV, dan spreadsheet yang kompatibel dengan Excel, sambil menjaga penggunaan memori di bawah 10 MB untuk file hingga 500 MB. Ia juga secara otomatis mempertahankan penjajaran kolom, aturan kutipan, dan enkoding khusus, yang menghilangkan kebutuhan akan logika parsing manual.

## Prasyarat
Sebelum kita mulai, pastikan Anda telah menginstal hal berikut:

- **Visual Studio** (edisi terbaru apa pun) – Anda akan mengembangkan dan men-debug langsung di dalam IDE.
- **GroupDocs.Editor for .NET** – unduh paket terbaru **[here](https://releases.groupdocs.com/editor/net/)**.
- **Pengetahuan dasar C#** – tutorial mengasumsikan Anda dapat membuat proyek console atau ASP.NET dan menambahkan paket NuGet.

## Impor Namespace
Kelas `Editor`, `EditableDocument`, dan kelas opsi berada di namespace `GroupDocs.Editor`.  

Kelas `DelimitedTextEditOptions` adalah titik masuk untuk mendefinisikan pemisah (koma, tab, dll.) dan aturan parsing lainnya.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Cara membuat dokumen yang dapat diedit dari file CSV?
Muat CSV sumber dengan `Editor` dan panggil metode `Edit`, dengan memberikan instance `DelimitedTextEditOptions` yang menentukan pemisah koma. Metode ini mengembalikan sebuah `EditableDocument` yang dapat Anda manipulasi di memori. Pola dua langkah ini—load → edit—mencakup skenario **read delimited text C#** dan menjamin struktur file asli tetap dipertahankan.

## Langkah 1: Dapatkan Jalur ke File DSV Input
Pertama, Anda perlu menentukan jalur absolut atau relatif ke file DSV sumber. Untuk demonstrasi kami akan menggunakan CSV sederhana yang terletak di folder `Data` proyek.

```csharp
string inputFilePath = "Your Sample Document";
```

## Langkah 2: Buat Instance Editor
`Editor` adalah kelas inti yang mengatur pemuatan, penyuntingan, dan penyimpanan. Menginstansiasinya dengan objek `FileInfo` memberi Anda kontrol penuh atas siklus hidup file.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Langkah 3: Buat Opsi Penyuntingan DSV
`DelimitedTextEditOptions` memberi tahu editor cara menafsirkan file. Anda dapat mengatur pemisah, apakah baris pertama berisi header, dan enkoding karakter.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Langkah 4: Buat Instance EditableDocument
`EditableDocument` mewakili versi dalam memori yang dapat diubah dari file sumber. Memanggil `Editor.Edit` dengan opsi tersebut mengembalikan sebuah `EditableDocument`. Objek ini menyimpan teks file dalam string yang dapat diubah, siap untuk operasi **parse delimited values C#** apa pun yang Anda butuhkan.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Langkah 5: Edit Konten Dokumen
`GetDocumentText()` mengembalikan teks saat ini dari dokumen yang dapat diedit sebagai string. Ambil teks asli melalui `EditableDocument.GetDocumentText()`, lakukan modifikasi Anda (mis., mengganti nilai kolom), dan simpan hasilnya dalam string baru. Di sinilah Anda **edit CSV .NET** tanpa menyentuh aliran file tingkat rendah.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Langkah 6: Buat EditableDocument dengan Konten yang Diperbarui
Bungkus string yang telah dimodifikasi kembali ke dalam `EditableDocument`. Langkah ini menyelesaikan perubahan dan menyiapkan objek untuk disimpan dalam format apa pun yang didukung.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Langkah 7: Buat Opsi Penyimpanan CSV
`DelimitedTextSaveOptions` menentukan cara menulis konten yang telah diedit kembali ke file CSV. Saat Anda siap menyimpan perubahan, konfigurasikan `DelimitedTextSaveOptions`. Anda dapat menentukan pemisah yang sama, yang berbeda, atau bahkan mengubah gaya akhir baris.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Langkah 8: Buat Opsi Penyimpanan TSV
Jika Anda membutuhkan versi dipisahkan tab, cukup ubah pemisah menjadi `\t`. `EditableDocument` yang sama dapat disimpan berkali-kali dengan opsi yang berbeda.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Langkah 9: Buat Opsi Penyimpanan Spreadsheet
`SpreadsheetSaveOptions` mengonfigurasi ekspor dokumen ke format yang kompatibel dengan Excel seperti .xlsx. GroupDocs.Editor juga memungkinkan Anda mengekspor data yang telah diedit ke format yang kompatibel dengan Excel (`.xlsx`). Kelas `SpreadsheetSaveOptions` menangani tipe kolom, formula, dan gaya sel secara otomatis.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Langkah 10: Siapkan Jalur Penyimpanan
Tentukan jalur output yang berbeda untuk setiap format. Menggunakan konvensi penamaan yang jelas (mis., `output.csv`, `output.tsv`, `output.xlsx`) membantu menjaga proyek Anda terorganisir.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Langkah 11: Simpan Dokumen yang Diedit
`Save()` menulis dokumen ke disk menggunakan opsi penyimpanan yang diberikan. Panggil `EditableDocument.Save` dengan opsi yang sesuai untuk setiap format target. API menulis file langsung ke disk, mempertahankan enkoding asli kecuali Anda menggantinya.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Langkah 12: Buang Instance EditableDocument
Baik `Editor` maupun `EditableDocument` mengimplementasikan `IDisposable`. Membuangnya melepaskan handle file dan sumber daya tak terkelola, yang penting saat memproses banyak file dalam pekerjaan batch.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Masalah Umum dan Solusinya
| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Kutipan tambahan tak terduga** | Parser CSV default dapat memperlakukan koma yang tertanam sebagai pemisah. | Set `EscapeMode = EscapeMode.DoubleQuote` di `DelimitedTextEditOptions`. |
| **Lonjakan memori pada file besar** | Memuat file 500 MB tanpa streaming. | Gunakan `Editor.Load` dengan `LoadOptions` yang mengaktifkan lazy loading. |
| **Ketidaksesuaian enkoding** | File sumber menggunakan UTF‑16 tetapi opsi default ke UTF‑8. | Secara eksplisit set `Encoding = Encoding.Unicode` di opsi penyimpanan. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan GroupDocs.Editor untuk .NET untuk menyunting file CSV besar?**  
A: Ya, API mem-stream data dan dapat menangani file lebih besar dari 1 GB tanpa memuat seluruh dokumen ke memori.

**Q: Apakah GroupDocs.Editor untuk .NET mendukung format DSV lain selain CSV dan TSV?**  
A: Tentu – setiap pemisah satu karakter (mis., pipe `|`, titik koma `;`) didukung selama Anda menentukan dalam `DelimitedTextEditOptions`.

**Q: Apakah memungkinkan menyesuaikan enkoding saat menyimpan file DSV?**  
A: Ya, Anda dapat mengatur properti `Encoding` di `DelimitedTextSaveOptions` ke UTF‑8, UTF‑16, ISO‑8859‑1, atau enkoding .NET apa pun yang Anda perlukan.

**Q: Bisakah saya mengonversi file CSV ke spreadsheet Excel menggunakan GroupDocs.Editor untuk .NET?**  
A: Ya – setelah penyuntingan, cukup gunakan `SpreadsheetSaveOptions` untuk mengekspor konten sebagai workbook `.xlsx`.

**Q: Di mana saya dapat menemukan dokumentasi lebih lanjut tentang GroupDocs.Editor untuk .NET?**  
A: Referensi API detail dan contoh kode tersedia **[here](https://tutorials.groupdocs.com/editor/net/)**.

---

**Terakhir Diperbarui:** 2026-06-06  
**Diuji Dengan:** GroupDocs.Editor 23.10 untuk .NET  
**Penulis:** GroupDocs

## Tutorial Terkait

- [Tutorial Penyuntingan Dokumen Teks Biasa dan DSV untuk GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Menguasai GroupDocs.Editor .NET untuk Penyuntingan Dokumen CSV yang Efisien dan Konversi](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Menguasai Pemuatan Dokumen di .NET dengan GroupDocs.Editor: Panduan Komprehensif](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)