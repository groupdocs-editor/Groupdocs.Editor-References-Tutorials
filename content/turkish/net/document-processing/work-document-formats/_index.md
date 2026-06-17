---
date: 2026-06-06
description: GroupDocs.Editor for .NET kullanarak desteklenen belge formatlarını nasıl
  listeleyeceğinizi ve dosya uzantısını nasıl belirleyeceğinizi öğrenin. Kod örnekleri,
  hızlı cevaplar ve SSS içeren adım adım kılavuz.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Desteklenen Belge Formatlarını Listele
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
title: GroupDocs.Editor .NET ile Desteklenen Belge Formatlarını Listeleyin
type: docs
url: /tr/net/document-processing/work-document-formats/
weight: 13
---

# Desteklenen Belge Formatlarını Listeleme

GroupDocs.Editor for .NET ile **desteklenen belge formatlarını nasıl listeleyeceğinizi** kapsayan kapsamlı öğreticiye hoş geldiniz. Belge‑odaklı bir web uygulaması ya da kurumsal‑düzeyde bir masaüstü aracı geliştiriyor olun, hangi formatları düzenleyebileceğinizi veya dönüştürebileceğinizi tam olarak bilmek çok önemlidir. Bu rehberde formatları nasıl sıralayacağınızı, uzantıları nasıl ayrıştıracağınızı ve belgeleri nasıl düzenleyeceğinizi keşfedeceksiniz — net, kullanıcı‑dostu açıklamalar ve çalıştırmaya hazır kod parçacıklarıyla.

## Hızlı Yanıtlar
- **Tüm desteklenen formatları nasıl listelerim?** `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (veya Presentation/Spreadsheet eşdeğerlerini) kullanın ve koleksiyonu döngüyle gezinin.  
- **Bir dosya uzantısından formatı belirleyebilir miyim?** Evet—`DocumentFormatInfo.FromExtension(".docx")` metodunu çağırın.  
- **GroupDocs.Editor hangi dosya türlerini destekliyor?** DOCX, XLSX, PPTX, HTML ve düz metin dahil olmak üzere 30’dan fazla giriş ve çıkış formatı.  
- **Formatları listelemek için lisansa ihtiyacım var mı?** Geçici bir lisans tam API'yi açar; aksi takdirde deneme sürümü sınırlı özelliklerle çalışır.  
- **Hangi .NET sürümleri uyumludur?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## “Desteklenen belge formatlarını listeleme” nedir?
Bu ifade, GroupDocs.Editor'ün açabildiği, düzenleyebildiği ve kaydedebildiği dosya türleri koleksiyonunu programlı olarak almayı ifade eder. Bu işlem, dinamik UI açılır menüleri oluşturmanıza veya kullanıcı yüklemelerini işlemden önce doğrulamanıza olanak tanır; böylece yalnızca uyumlu dosyalar editöre aktarılır ve sonraki işlemler için kullanılabilir.

## Neden desteklenen belge formatlarını listeleyelim?
GroupDocs.Editor **30'dan fazla giriş ve çıkış formatını destekler** ve belgeyi belleğe tamamen yüklemeden **2 GB**'a kadar dosyaları işleyebilir. Tam listeyi bilmek çalışma zamanı hatalarını önler, kullanıcı deneyimini iyileştirir ve “yalnızca düzenlenebilir Office belgelerine izin ver” gibi iş kurallarını uygulamanızı sağlar. Ayrıca, kullanıcılarınıza yalnızca uygulamanızın gerçekten desteklediği formatları sunmanıza yardımcı olur.

## Önkoşullar
Başlamadan önce, şunların olduğundan emin olun:

1. **.NET geliştirme ortamı** – Visual Studio 2022 veya .NET 6+ destekleyen herhangi bir IDE.  
2. **GroupDocs.Editor for .NET kütüphanesi** – [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) adresinden indirin.  
3. **Geçici lisans** – sınırsız erişim için bir [temporary license](https://purchase.groupdocs.com/temporary-license/) alın.  
4. **Temel C# bilgisi** – ad alanları, `using` ifadeleri ve konsol çıktısı konularına aşina olun.

## Desteklenen Belge Formatlarını Nasıl Listeleyebilirsiniz?
Desteklenen formatlar koleksiyonunu yükleyin ve her formatın adını ve dosya uzantısını yazdırın. Bu iki adımlı desen Word İşleme, Elektronik Tablo ve Sunum belgeleri için çalışır. Koleksiyonu döngüyle gezerek, açılır menüler gibi UI öğelerini dinamik olarak doldurabilir ve kullanıcıların yalnızca editörün gerçekten işleyebileceği formatları seçmesini sağlayabilirsiniz.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Word İşleme Formatlarını Listeleme
`Formats.WordProcessingFormats` is an enumeration that describes every Word‑processing file type recognized by the editor. The `All` property returns a collection of these format objects.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Açıklama:**  
1. **Formatlar Üzerinde Döngü:** Tüm mevcut Word‑processing formatları üzerinde döngü yaparız.  
2. **Format Detaylarını Çıktıla:** Her format için kullanıcı dostu adını ve varsayılan dosya uzantısını yazdırırız.

### Sunum Formatlarını Listeleme
`Formats.PresentationFormats` works the same way for slide‑deck files, exposing each supported presentation type through the `All` collection.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Açıklama:**  
1. **Formatlar Üzerinde Döngü:** The same looping logic applies to presentations.  
2. **Output Format Details:** The name and extension are displayed for each format.

## Dosya Formatı Uzantısını Nasıl Belirleyebilirsiniz?
Bazen sadece bir dosya adınız olur ve ilgili `DocumentFormat`'ı tahmin etmeniz gerekir. GroupDocs.Editor, bir dosya uzantısını iç format temsiline eşleyen basit bir statik yardımcı sunar; bu sayede dosyaları editöre yüklemeden önce doğrulama veya dönüştürme yapabilirsiniz.

### Elektronik Tablo Formatlarını Ayrıştırma
`Formats.SpreadsheetFormats.FromExtension` converts a file extension string into the matching spreadsheet format enum value.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Açıklama:**  
1. **Formatı Ayrıştır:** `FromExtension`, `.xlsm` uzantısını iç `SpreadsheetFormat` enum'ına dönüştürür.  
2. **Formatı Çıktıla:** Ayrıştırılan formatın adı yazdırılır, eşlemenin doğruluğu teyit edilir.

### Metin Formatlarını Ayrıştırma
Similarly, `Formats.TextualFormats.FromExtension` resolves textual file extensions such as HTML or TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Açıklama:**  
1. **Formatı Ayrıştır:** The `FromExtension` method resolves the `html` extension to a `TextFormat`.  
2. **Formatı Çıktıla:** The name of the textual format is displayed, useful for web‑based editors.

## Formatları Belirledikten Sonra Belgeleri Nasıl Düzenlersiniz?
Formatı öğrendikten sonra bir belgeyi yükleme ve düzenleme tutarlı bir desen izler. İlk olarak kaynak dosyanın yolunu vererek bir `Editor` örneği oluşturursunuz, ardından `Edit()` metodunu çağırarak bir `EditableDocument` elde edersiniz. Buradan içeriği okuyabilir, değiştirebilir ve sonunda uygun `SaveOptions` ile kaydedebilirsiniz.

### Bir Belge Yükleme
`Editor`, belirli bir dosya için tüm düzenleme işlemlerini kapsülleyen temel sınıftır.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Açıklama:**  
1. **Editor'ı Başlat:** Hedef dosyanın tam yolunu vererek bir `Editor` örneği oluşturun.  
2. **Dispose Deseni:** `using` ifadesi, tüm yönetilmeyen kaynakların hızlı bir şekilde serbest bırakılmasını garanti eder.

### İçeriği Çıkarma
`EditableDocument.GetContent()` belge'nin ham metnini (veya web‑tabanlı editörler için HTML) döndürür; bunu görüntüleyebilir veya manipüle edebilirsiniz.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Açıklama:**  
1. **Edit Metodu:** `Edit()` bir `EditableDocument` nesnesi döndürür.  
2. **İçeriği Al:** `GetContent()` belge'nin ham metnini (veya web‑tabanlı editörler için HTML) çıkarır.  
3. **İçeriği Çıktıla:** İçerik doğrulama amacıyla konsola yazdırılır.

### Değişiklikleri Kaydetme
`SaveOptions`, editörün düzenlenmiş belgeyi nasıl ve hangi formatta depolamaya geri yazacağını belirler.

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

**Açıklama:**  
1. **Edit Metodu:** Değişikliklerden sonra `EditableDocument` tekrar elde edilir.  
2. **İçeriği Değiştir:** (burada gösterilmeyen) string üzerinde değişikliklerinizi uygulayın.  
3. **Kaydetme Seçenekleri:** İstenen çıkış formatı ile `SaveOptions` yapılandırılır.  
4. **Belgeyi Kaydet:** Düzenlenmiş dosya diske kaydedilir.

## Farklı Belge Türleriyle Nasıl Çalışılır?
GroupDocs.Editor, Word, Elektronik Tablo ve Sunum işlemlerini aynı API üzerinden soyutlayarak, her belge ailesi için yeni sınıflar öğrenmeye gerek kalmadan bağlamlar arasında geçiş yapmayı kolaylaştırır.

### Elektronik Tablo Belgelerini Düzenleme
`SpreadsheetSaveOptions`, bir elektronik tablonun nasıl yazılacağını, format ve isteğe bağlı sıkıştırma ayarlarını tanımlar.

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

**Açıklama:**  
1. **Editor'ı Başlat:** `Editor` yapıcısına bir elektronik tablo dosya yolu verin.  
2. **Edit Metodu:** Bir `EditableDocument` alın.  
3. **İçeriği Al:** Elektronik tablonun CSV temsilini (veya HTML) yazdırın.  
4. **İçeriği Değiştir:** Gerekli hücre‑seviyesi değişiklikleri uygulayın.  
5. **Kaydetme Seçenekleri:** Uygun `SpreadsheetSaveOptions` seçin.  
6. **Belgeyi Kaydet:** Güncellenmiş elektronik tabloyu depolamaya geri yazın.

### Sunum Belgelerini Düzenleme
`PresentationSaveOptions`, slayt destesi için çıkış formatını kontrol eder; orijinal dosya tipini korumanıza veya değiştirmenize olanak tanır.

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

**Açıklama:**  
1. **Editor'ı Başlat:** `Editor` aracılığıyla bir PowerPoint dosyası yükleyin.  
2. **Edit Metodu:** Bir `EditableDocument` elde edin.  
3. **İçeriği Al:** Slayt HTML'sini veya düz metni çıkarın.  
4. **İçeriği Değiştir:** Başlıkları, madde işaretlerini veya görselleri güncelleyin.  
5. **Kaydetme Seçenekleri:** Çıkış formatını tanımlamak için `PresentationSaveOptions` kullanın.  
6. **Belgeyi Kaydet:** Düzenlenmiş sunumu kaydedin.

## Yaygın Sorunlar ve Çözümler
- **“Format not supported” hatası:** En son GroupDocs.Editor sürümünü kullandığınızdan emin olun; bu sürüm düzenli olarak yeni Office formatlarını destekler.  
- **Büyük dosya bellek tüketimi:** Belgeyi yüklemeden önce `EditorSettings.EnableStreaming = true` ayarını yaparak akış modunu etkinleştirin.  
- **Lisans uygulanmadı:** Geçici lisans dosyasının uygulama kök dizinine yerleştirildiğinden veya `License license = new License(); license.SetLicense("path/to/license.lic");` ile yüklendiğinden emin olun.

## Sık Sorulan Sorular

**S: `DocumentFormatInfo` ve `SaveOptions` arasındaki fark nedir?**  
C: `DocumentFormatInfo`, desteklenen dosya türleri hakkında meta veriler sağlar; `SaveOptions` ise bir belgenin diske nasıl (format, sıkıştırma vb.) yazılacağını yapılandırır.

**S: Özel bir dosya uzantısı için formatları listeleyebilir miyim?**  
C: Evet—`DocumentFormatInfo.FromExtension("yourExt")` kullanın; uzantı tanınmazsa metod `null` döndürür.

**S: GroupDocs.Editor şifre‑korumalı dosyaları destekliyor mu?**  
C: Kesinlikle. Şifreyi `EditorSettings` aracılığıyla `Editor` yapıcısına geçirerek şifreli belgeleri açabilirsiniz.

**S: GroupDocs.Editor gerçekte kaç format destekliyor?**  
C: **30'dan fazla** giriş ve çıkış formatı, Word, Excel, PowerPoint, HTML ve düz metin dahil.

**S: Listeyi yalnızca düzenlenebilir formatlarla sınırlamanın bir yolu var mı?**  
C: Tam düzenleme yeteneklerine izin veren formatları almak için `GetEditableWordProcessingFormats()` (veya Spreadsheet/Presentation eşdeğerlerini) kullanın.

## Ek Kaynaklar
- Kütüphaneyi [GroupDocs releases page](https://releases.groupdocs.com/editor/net/) adresinden indirin.  
- Tam özellik erişimi için bir [temporary license](https://purchase.groupdocs.com/temporary-license/) alın.  
- Ürünü bir [free trial](https://releases.groupdocs.com/) ile deneyin.  
- [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/) içinde ayrıntılı kullanım örneklerini keşfedin.  
- [support forum](https://forum.groupdocs.com/c/editor/20) üzerinden topluluktan yardım alın.

## Sonuç
Bu rehberi izleyerek artık **desteklenen belge formatlarını nasıl listeleyeceğinizi**, **bir uzantıdan dosya formatını nasıl belirleyeceğinizi** ve GroupDocs.Editor for .NET kullanarak Word, Elektronik Tablo ve Sunum türlerinde **belgeleri nasıl düzenleyeceğinizi** biliyorsunuz. Bu kod parçacıklarını kendi projelerinize entegre ederek, son kullanıcıları memnun eden ve çalışma zamanı hatalarını azaltan sağlam, format‑bilinçli uygulamalar oluşturabilirsiniz.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Editor 23.9 for .NET  
**Author:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Editor ile .NET'te Belge Yüklemeyi Ustalaştırma: Kapsamlı Rehber](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [GroupDocs.Editor ile .NET'te Belge Düzenlemeyi Ustalaştırma: Kapsamlı Rehber](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [GroupDocs.Editor .NET ile Word'ü HTML'ye Dönüştürme: Adım‑Adım Rehber](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)