---
date: '2026-05-22'
description: Pelajari cara mengekstrak gambar dari Word menggunakan GroupDocs.Editor
  untuk Java, termasuk langkah-langkah load word document java dan extract images
  java, contoh extract css java.
keywords:
- extract pictures from word
- load word document java
- extract images java
- extract css java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to extract pictures from Word using GroupDocs.Editor for
    Java, including load word document java steps and extract images java, extract
    css java examples.
  headline: How to Extract Pictures from Word Documents Using GroupDocs.Editor for
    Java
  type: TechArticle
- description: Learn how to extract pictures from Word using GroupDocs.Editor for
    Java, including load word document java steps and extract images java, extract
    css java examples.
  name: How to Extract Pictures from Word Documents Using GroupDocs.Editor for Java
  steps:
  - name: Load and Prepare the Document for Editing
    text: '*The `FontExtractionOptions.ExtractAll` flag guarantees that every embedded
      font is available for extraction.*'
  - name: Extract Images, Fonts, and Stylesheets
    text: '*These three calls give you collections of each resource type, ready for
      further processing.*'
  - name: Save Extracted Resources to Disk
    text: '*Each loop writes the corresponding resource to the `outputFolderPath`,
      preserving the original filenames.*'
  - name: Retrieve Resource Content Directly (Optional)
    text: 'If you need the raw bytes or a Base64 string—for example, to embed an image
      in an HTML email—use:'
  type: HowTo
- questions:
  - answer: Yes, it supports DOCX, DOC, and other Microsoft Word formats.
    question: Is GroupDocs.Editor compatible with all Word file formats?
  - answer: Absolutely. Provide the password via `WordProcessingLoadOptions` when
      creating the `Editor`.
    question: Can I extract resources from password‑protected documents?
  - answer: It’s optimized for speed; for files over 200 MB we recommend batch processing
      or extracting sections sequentially.
    question: How does the API perform with very large documents?
  - answer: Yes. The API is framework‑agnostic; just include the dependency and inject
      `Editor` where needed.
    question: Can I integrate this with Spring Boot or other Java frameworks?
  - answer: Call only `beforeEdit.getImages()` and skip the font/CSS extraction steps.
    question: What if I need to extract only images and not fonts or CSS?
  type: FAQPage
title: Cara Mengekstrak Gambar dari Dokumen Word Menggunakan GroupDocs.Editor untuk
  Java
type: docs
url: /id/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/
weight: 1
---

# Cara Mengekstrak Gambar dari Dokumen Word Menggunakan GroupDocs.Editor untuk Java

Jika Anda perlu **mengekstrak gambar dari Word** secara programatis, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan menjelaskan cara memuat dokumen Word di Java, mengonfigurasi editor, dan mengambil gambar, font, serta CSS—tepat langkah yang Anda butuhkan untuk mengotomatisasi pipeline pemrosesan dokumen dengan GroupDocs.Editor untuk Java.

**Apa yang akan Anda pelajari:**
- Cara **load word document java** dengan GroupDocs.Editor  
- Cara **extract images java** dan aset tersemat lainnya  
- Cara **extract css java** untuk penggunaan kembali styling  
- Cara terbaik (best‑practice) untuk menyimpan sumber daya tersebut ke disk  
- Skenario dunia nyata di mana mengekstrak sumber daya menghemat waktu dan usaha  

Siap menyederhanakan alur kerja dokumen Anda? Mari kita mulai!

## Jawaban Cepat
- **Apa arti “extract pictures from word”?** Itu berarti secara programatis menarik gambar, font, CSS, dan aset tersemat lainnya dari file Word.  
- **Perpustakaan mana yang menangani ini di Java?** GroupDocs.Editor untuk Java menyediakan API tingkat tinggi untuk tugas tersebut.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi penuh diperlukan untuk produksi.  
- **Bisakah saya memproses file DOCX dan DOC?** Ya—kedua format didukung sepenuhnya.  
- **Apakah aman untuk dokumen besar?** Ya, tetapi pertimbangkan pemrosesan batch dan pembuangan memori yang tepat untuk file lebih besar dari 200 MB.  

## Apa Itu Ekstraksi Sumber Daya dalam Dokumen Word?
Ekstraksi sumber daya mengacu pada pengambilan sistematis semua aset tersemat dari file Word, termasuk gambar, font khusus, lembar gaya, makro, dan objek biner lainnya. Dengan mengekstrak komponen‑komponen ini, pengembang dapat menggunakannya kembali dalam aplikasi terpisah, mengarsipkannya untuk kepatuhan, atau mengubahnya menjadi format yang ramah web, sehingga memperluas nilai dokumen asli.

## Mengapa Menggunakan GroupDocs.Editor untuk Java?
GroupDocs.Editor untuk Java mengabstraksi format Office Open XML, memungkinkan Anda fokus pada **cara mengekstrak gambar dari word** tanpa menulis kode ZIP atau XML tingkat rendah. Ia mendukung **lebih dari 30 format input dan output** dan dapat memproses dokumen hingga **500 MB** tanpa memuat seluruh file ke memori, memberikan kecepatan dan skalabilitas.

## Prasyarat
- **Maven** (atau unduhan JAR langsung) untuk mengelola dependensi.  
- **JDK 8+** terpasang pada mesin pengembangan Anda.  
- IDE seperti **IntelliJ IDEA** atau **Eclipse** untuk mengedit dan menjalankan kode Java.

## Menyiapkan GroupDocs.Editor untuk Java
Tambahkan repositori dan dependensi ke `pom.xml` Anda:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

Anda juga dapat mengunduh JAR terbaru dari [GroupDocs.Editor for Java releases](https://releases.groupdocs.com/editor/java/).

### Akuisisi Lisensi
- **Lisensi Gratis:** Sempurna untuk menjelajahi API.  
- **Lisensi Sementara:** Dapatkan satu dari [GroupDocs Temporary License Page](https://purchase.groupdocs.com/temporary-license).  
- **Lisensi Penuh:** Beli untuk penggunaan produksi tanpa batas.

### Inisialisasi Dasar
`Editor` adalah titik masuk utama GroupDocs.Editor untuk Java yang menyediakan metode untuk memuat, menyunting, dan mengekstrak sumber daya dari file Word.

Buat instance `Editor` yang menunjuk ke file Word Anda:

```java
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY";
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Cara Mengekstrak Sumber Daya dari Dokumen Word
Mengekstrak sumber daya dimulai dengan memuat file Word target ke dalam instance `Editor`, kemudian mengonfigurasi `WordProcessingEditOptions` untuk mengaktifkan ekstraksi gambar, font, dan CSS. Setelah dokumen siap, API menyediakan koleksi untuk setiap tipe sumber daya, yang dapat diiterasi dan disimpan ke sistem file atau diproses lebih lanjut sesuai kebutuhan alur kerja Anda.

### Langkah 1: Muat dan Siapkan Dokumen untuk Penyuntingan
```java
// Initialize editor and edit options
String inputFilePath = "YOUR_DOCUMENT_DIRECTORY";
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
editOptions.setFontExtraction(FontExtractionOptions.ExtractAll);
EditableDocument beforeEdit = editor.edit(editOptions);
```  
*Flag `FontExtractionOptions.ExtractAll` menjamin bahwa setiap font tersemat tersedia untuk diekstrak.*

### Langkah 2: Ekstrak Gambar, Font, dan Stylesheet
```java
List<IImageResource> images = beforeEdit.getImages();
```  

```java
List<FontResourceBase> fonts = beforeEdit.getFonts();
```  

```java
List<CssText> stylesheets = beforeEdit.getCss();
```  
*Tiga panggilan ini memberi Anda koleksi masing‑masing tipe sumber daya, siap untuk diproses lebih lanjut.*

### Langkah 3: Simpan Sumber Daya yang Diekstrak ke Disk
```java
String outputFolderPath = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < images.size(); i++) {
    IImageResource oneImage = images.get(i);
    File outputFile = new File(outputFolderPath + oneImage.getFilenameWithExtension());
    oneImage.save(outputFile.getAbsolutePath());
}
```  

```java
for (int i = 0; i < fonts.size(); i++) {
    FontResourceBase oneFont = fonts.get(i);
    File outputFile = new File(outputFolderPath + oneFont.getFilenameWithExtension());
    oneFont.save(outputFile.getAbsolutePath());
}
```  

```java
for (int i = 0; i < stylesheets.size(); i++) {
    CssText oneStylesheet = stylesheets.get(i);
    File outputFile = new File(outputFolderPath + oneStylesheet.getFilenameWithExtension());
    oneStylesheet.save(outputFile.getAbsolutePath());
}
```  
*Setiap loop menulis sumber daya yang bersangkutan ke `outputFolderPath`, mempertahankan nama file asli.*

### Langkah 4: Ambil Konten Sumber Daya Secara Langsung (Opsional)
Jika Anda memerlukan byte mentah atau string Base64—misalnya, untuk menyematkan gambar dalam email HTML—gunakan:

```java
InputStream ms = images.get(0).getByteContent(); // raw bytes
String base64EncodedResource = images.get(0).getTextContent(); // Base64 string
```

## Masalah Umum dan Solusinya
| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **OutOfMemoryError pada file besar** | Sumber daya dimuat ke memori sekaligus. | Proses dokumen dalam batch lebih kecil dan panggil `editor.dispose()` setelah tiap file. |
| **Font hilang setelah ekstraksi** | Ekstraksi font dinonaktifkan dalam opsi. | Pastikan `editOptions.setFontExtraction(FontExtractionOptions.ExtractAll)` sudah diatur. |
| **Gambar disimpan dengan ekstensi salah** | Beberapa gambar tidak memiliki deteksi tipe MIME yang tepat. | Verifikasi `oneImage.getFilenameWithExtension()` sebelum menyimpan; ganti nama jika perlu. |

## Pertanyaan yang Sering Diajukan

**Q: Apakah GroupDocs.Editor kompatibel dengan semua format file Word?**  
A: Ya, ia mendukung DOCX, DOC, dan format Microsoft Word lainnya.

**Q: Bisakah saya mengekstrak sumber daya dari dokumen yang dilindungi kata sandi?**  
A: Tentu saja. Berikan kata sandi melalui `WordProcessingLoadOptions` saat membuat `Editor`.

**Q: Bagaimana kinerja API dengan dokumen yang sangat besar?**  
A: API dioptimalkan untuk kecepatan; untuk file lebih dari 200 MB kami menyarankan pemrosesan batch atau mengekstrak bagian secara berurutan.

**Q: Bisakah saya mengintegrasikan ini dengan Spring Boot atau kerangka kerja Java lainnya?**  
A: Ya. API bersifat framework‑agnostic; cukup sertakan dependensi dan injeksikan `Editor` di tempat yang diperlukan.

**Q: Bagaimana jika saya hanya perlu mengekstrak gambar dan bukan font atau CSS?**  
A: Panggil hanya `beforeEdit.getImages()` dan lewati langkah ekstraksi font/CSS.

## Kesimpulan
Anda kini memiliki panduan lengkap yang siap produksi tentang **cara mengekstrak gambar dari word** dokumen menggunakan GroupDocs.Editor untuk Java. Dengan memuat dokumen, mengonfigurasi opsi penyuntingan, dan mengiterasi koleksi sumber daya yang dikembalikan, Anda dapat mengotomatisasi pengarsipan, pembuatan templat, dan generasi konten dinamis dengan mudah.

**Langkah selanjutnya:**  
- Bereksperimen dengan berbagai `WordProcessingEditOptions` untuk menyempurnakan ekstraksi.  
- Gabungkan alur kerja ini dengan SDK penyimpanan cloud untuk mengunggah sumber daya langsung ke S3 atau Azure Blob.  
- Jelajahi API konversi GroupDocs untuk mengubah aset yang diekstrak ke format lain.

---

**Terakhir Diperbarui:** 2026-05-22  
**Diuji Dengan:** GroupDocs.Editor 25.3 untuk Java  
**Penulis:** GroupDocs  

---

## Tutorial Terkait

- [Cara Mengekstrak Sumber Daya dari Dokumen Word – GroupDocs.Editor Java](/editor/java/word-processing-documents/edit-extract-resources-groupdocs-editor-java/)
- [Muat Dokumen Word Java dengan GroupDocs.Editor – Panduan Lengkap](/editor/java/document-loading/load-word-document-groupdocs-editor-java/)