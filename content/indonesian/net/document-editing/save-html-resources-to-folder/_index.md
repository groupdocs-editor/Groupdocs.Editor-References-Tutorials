---
date: 2026-05-12
description: Pelajari cara mengekstrak font dan sumber daya HTML lainnya dari dokumen
  menggunakan GroupDocs.Editor untuk .NET. Panduan langkah demi langkah untuk pengembang
  .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Simpan Sumber Daya HTML ke Folder
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Cara Mengekstrak Font dan Menyimpan Sumber Daya HTML ke Folder
type: docs
url: /id/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Cara Mengekstrak Font dan Menyimpan Sumber Daya HTML ke Folder

## Pendahuluan
GroupDocs.Editor for .NET memungkinkan Anda **mengekstrak font** dan aset lainnya dari dokumen saat mengonversinya ke HTML. Dalam beberapa baris C# Anda dapat mengambil gambar, stylesheet, dan file font, kemudian menyimpannya ke folder pilihan Anda. Tutorial ini memandu Anda melalui seluruh alur kerja, mulai dari menginisialisasi editor hingga menyimpan setiap sumber daya ke disk.

## Jawaban Cepat
- **Apa arti “mengekstrak font”?** Ini adalah proses mengambil file font yang tersemat dari dokumen sumber selama konversi HTML.  
- **Perpustakaan mana yang menangani ini?** GroupDocs.Editor for .NET menyediakan API khusus untuk mengekstrak font, gambar, dan stylesheet.  
- **Apakah saya memerlukan lisensi?** Tersedia percobaan gratis; lisensi komersial diperlukan untuk penggunaan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Bisakah saya menargetkan folder khusus?** Ya, Anda dapat menentukan jalur yang dapat ditulis saat menyimpan sumber daya yang diekstrak.

## Apa itu “mengekstrak font”?
**Mengekstrak font** mengacu pada pengambilan file font asli yang tersemat dalam dokumen sumber (mis., DOCX, PPTX) sehingga dapat dirujuk oleh HTML yang dihasilkan. Ini memastikan teks ditampilkan persis seperti yang dimaksudkan di peramban tanpa bergantung pada font sistem.

## Mengapa menggunakan GroupDocs.Editor untuk ekstraksi sumber daya HTML?
GroupDocs.Editor mendukung **lebih dari 50 format input dan output**—termasuk DOCX, PPTX, PDF, dan HTML—dan dapat memproses dokumen dengan **hingga 300 halaman** tanpa memuat seluruh file ke memori. API-nya mengekstrak font, gambar, dan CSS dalam satu langkah, mengurangi waktu pengembangan hingga **70 %** dibandingkan dengan parsing manual.

## Prasyarat
1. **Pengetahuan Dasar tentang C# dan .NET** – Familiaritas dengan bahasa pemrograman C# dan kerangka kerja .NET penting untuk mengikuti contoh.  
2. **Perpustakaan GroupDocs.Editor untuk .NET** – Unduh dan instal perpustakaan GroupDocs.Editor untuk .NET dari [website](https://releases.groupdocs.com/editor/net/).  
3. **Lingkungan Pengembangan** – Siapkan lingkungan pengembangan pilihan Anda seperti Visual Studio atau IDE kompatibel lainnya.

## Impor Namespace
Untuk memulai, impor namespace yang diperlukan dalam proyek C# Anda:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Cara mengekstrak font dan menyimpan sumber daya HTML ke folder?
Muat dokumen sumber Anda dengan `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` lalu panggil `editor.Save("output.html", SaveOptions.Html);`. Setelah operasi penyimpanan, koleksi `Resources` berisi semua aset yang diekstrak—termasuk font—yang dapat Anda iterasi dan tulis ke disk. Pendekatan satu‑langkah ini menangani konversi dan ekstraksi sumber daya secara otomatis.

## Langkah 1: Inisialisasi GroupDocs.Editor
`Editor` adalah kelas inti yang mengatur pemuatan dokumen, konversi, dan ekstraksi sumber daya. Ia mewakili satu sesi dokumen dalam memori.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Pertama, inisialisasi objek `Editor` dengan memberikan jalur ke dokumen contoh Anda. Dalam contoh ini, kami menggunakan dokumen Word, jadi kami menentukan `WordProcessingLoadOptions` sebagai tipe dokumen.

## Langkah 2: Edit Dokumen
`EditableDocument` adalah representasi yang dapat diedit yang dikembalikan oleh metode `Edit`, memungkinkan Anda memanipulasi dokumen sebelum menyimpan.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Selanjutnya, buat objek `EditableDocument` dengan memanggil metode `Edit` pada objek `Editor`. Ini memungkinkan Anda melakukan operasi penyuntingan pada dokumen.

## Langkah 3: Ekstrak Sumber Daya
`Resources` adalah koleksi yang mengelompokkan aset yang diekstrak—gambar, font, dan stylesheet—ke dalam daftar terpisah untuk penanganan yang mudah.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Ekstrak sumber daya seperti gambar, font, dan stylesheet dari dokumen dan simpan mereka dalam daftar masing‑masing.

## Langkah 4: Tentukan Folder Output
`outputFolder` adalah string yang menentukan tempat file yang diekstrak akan ditulis. Anda dapat mengarahkannya ke direktori yang dapat ditulis pada server atau mesin lokal.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Tentukan folder output tempat sumber daya yang diekstrak akan disimpan. Anda dapat menyesuaikan jalur folder sesuai kebutuhan.

## Langkah 5: Simpan Sumber Daya
`SaveResource` adalah prosedur bantu yang menulis satu sumber daya biner (gambar, font, atau stylesheet) ke sistem file.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Iterasi setiap sumber daya gambar, simpan ke folder output, dan tampilkan informasi relevan seperti nama file, tipe, dan dimensi.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Demikian pula, simpan setiap sumber daya font ke folder output.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Akhirnya, simpan setiap stylesheet ke folder output dan selesaikan proses penyuntingan.

## Masalah Umum dan Solusinya
- **Font hilang setelah konversi** – Pastikan dokumen sumber memang menyematkan font; jika tidak, GroupDocs.Editor hanya dapat merujuk ke font sistem.  
- **Kesalahan akses ditolak** – Verifikasi bahwa proses aplikasi memiliki izin menulis ke folder output target.  
- **Dokumen besar menyebabkan penggunaan memori tinggi** – Gunakan `LoadOptions` dengan `LoadMode = LoadMode.Stream` untuk men-stream file besar alih-alih memuatnya seluruhnya ke memori.

## Pertanyaan yang Sering Diajukan

**Q: Apakah GroupDocs.Editor kompatibel dengan format dokumen lain selain Word?**  
A: Ya, ia mendukung Excel, PowerPoint, PDF, HTML, dan lebih dari 50 format tambahan untuk penyuntingan dan ekstraksi sumber daya.

**Q: Bisakah saya mengintegrasikan GroupDocs.Editor ke dalam aplikasi web?**  
A: Tentu saja. API bekerja mulus dengan proyek ASP.NET Core, MVC, dan Web API, memungkinkan Anda memproses dokumen di sisi server.

**Q: Apakah GroupDocs.Editor menyediakan integrasi penyimpanan cloud?**  
A: Ya, ia menyertakan konektor bawaan untuk Google Drive, Dropbox, OneDrive, dan Amazon S3, memungkinkan pemuatan dan penyimpanan dokumen secara langsung di cloud.

**Q: Apakah tersedia percobaan gratis untuk GroupDocs.Editor?**  
A: Percobaan penuh selama 30 hari dapat diunduh dari situs web GroupDocs tanpa memerlukan kartu kredit.

**Q: Bagaimana saya dapat mendapatkan dukungan teknis untuk masalah ekstraksi?**  
A: Anda dapat menghubungi tim dukungan GroupDocs melalui forum resmi, mengirim tiket melalui portal pelanggan, atau berkonsultasi dengan dokumentasi API yang detail.

---

**Last Updated:** 2026-05-12  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs

## Tutorial Terkait

- [Efficient Document Editing with GroupDocs.Editor .NET&#58; Transform HTML to Editable Documents](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Efficiently Extract and Save DOCX Resources Using GroupDocs.Editor .NET - Complete Guide](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Mastering Document Editing and Conversion with GroupDocs.Editor .NET&#58; A Complete Guide](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)