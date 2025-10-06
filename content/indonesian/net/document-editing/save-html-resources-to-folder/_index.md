---
title: Simpan Sumber Daya HTML ke Folder
linktitle: Simpan Sumber Daya HTML ke Folder
second_title: GroupDocs.Editor .NET API
description: Pelajari cara mengekstrak sumber daya HTML dari dokumen menggunakan Groupdocs.Editor untuk .NET. Tutorial komprehensif ini memberikan panduan langkah demi langkah untuk pengembang.
weight: 13
url: /id/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Simpan Sumber Daya HTML ke Folder

## Perkenalan
Groupdocs.Editor untuk .NET adalah alat canggih yang memungkinkan pengembang memanipulasi dan mengonversi dokumen dalam aplikasi .NET mereka dengan mulus. Baik Anda perlu mengekstrak sumber daya HTML dari dokumen atau melakukan tugas pengeditan lanjutan, Groupdocs.Editor menyederhanakan proses dengan API intuitif dan dokumentasi ekstensif.
## Prasyarat
Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
1. Pengetahuan Dasar tentang C# dan .NET: Keakraban dengan bahasa pemrograman C# dan kerangka .NET sangat penting untuk diikuti dengan contoh.
2.  Groupdocs.Editor untuk .NET Library: Unduh dan instal Groupdocs.Editor untuk .NET Library dari[situs web](https://releases.groupdocs.com/editor/net/).
3. Lingkungan Pengembangan: Siapkan lingkungan pengembangan pilihan Anda seperti Visual Studio atau IDE lain yang kompatibel.

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
##Sekarang, mari kita uraikan proses penyimpanan sumber daya HTML ke folder menggunakan Groupdocs.Editor untuk .NET menjadi beberapa langkah:
## Langkah 1: Inisialisasi Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Pertama, inisialisasi`Editor`objek dengan memberikan jalur ke dokumen sampel Anda. Dalam contoh ini, kami menggunakan dokumen Word, jadi kami tentukan`WordProcessingLoadOptions` sebagai jenis dokumen.
## Langkah 2: Edit Dokumen
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Selanjutnya, buat`EditableDocument` objek dengan memanggil`Edit` metode`Editor` obyek. Ini memungkinkan Anda melakukan operasi pengeditan pada dokumen.
## Langkah 3: Ekstrak Sumber Daya
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Ekstrak sumber daya seperti gambar, font, dan stylesheet dari dokumen dan simpan di daftar masing-masing.
## Langkah 4: Tentukan Folder Output
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Tentukan folder keluaran tempat sumber daya yang diekstraksi akan disimpan. Anda dapat menyesuaikan jalur folder sesuai kebutuhan Anda.
## Langkah 5: Hemat Sumber Daya
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Ulangi setiap sumber gambar, simpan ke folder keluaran, dan tampilkan informasi yang relevan seperti nama file, jenis, dan dimensi.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Demikian pula, simpan setiap sumber font ke folder keluaran.
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
Terakhir, simpan setiap stylesheet ke folder output dan selesaikan proses pengeditan.

## Kesimpulan
Kesimpulannya, Groupdocs.Editor untuk .NET memberikan solusi mudah untuk mengelola dan memanipulasi dokumen secara terprogram dalam aplikasi .NET. Dengan mengikuti tutorial ini, Anda dapat dengan mudah mengekstrak sumber daya HTML dari dokumen dan menyesuaikan prosesnya sesuai dengan kebutuhan spesifik Anda.
## FAQ
### Apakah Groupdocs.Editor kompatibel dengan format dokumen lain selain Word?
Ya, Groupdocs.Editor mendukung berbagai format dokumen termasuk Excel, PowerPoint, PDF, dan banyak lagi.
### Bisakah saya mengintegrasikan Groupdocs.Editor ke dalam aplikasi web saya?
Tentu saja, Groupdocs.Editor menawarkan integrasi tanpa batas dengan aplikasi web yang dikembangkan pada kerangka .NET.
### Apakah Groupdocs.Editor menyediakan dukungan untuk layanan penyimpanan cloud?
Ya, Groupdocs.Editor mendukung integrasi dengan layanan penyimpanan cloud populer seperti Google Drive, Dropbox, dan Microsoft OneDrive.
### Apakah ada uji coba gratis yang tersedia untuk Groupdocs.Editor?
Ya, Anda dapat memanfaatkan uji coba gratis Groupdocs.Editor dari situs web.
### Bagaimana saya bisa mendapatkan dukungan teknis untuk Groupdocs.Editor?
Untuk bantuan teknis dan dukungan komunitas, Anda dapat mengunjungi forum Groupdocs.Editor.