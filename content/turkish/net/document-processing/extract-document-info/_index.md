---
date: 2026-06-01
description: GroupDocs.Editor for .NET kullanarak sayfa sayısını nasıl alacağınızı
  ve belge meta verilerini nasıl çıkaracağınızı adım adım ayrıntılı bir öğreticide
  öğrenin.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Sayfa Sayısını Alın ve Belge Bilgilerini Çıkarın
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor ile Sayfa Sayısını Alın ve Belge Bilgilerini Çıkarın
type: docs
url: /tr/net/document-processing/extract-document-info/
weight: 10
---

# Sayfa Sayısını Al ve Belge Bilgilerini GroupDocs.Editor ile Çıkar

## Giriş
Bu kapsamlı öğreticide, GroupDocs.Editor for .NET kullanarak **sayfa sayısını al** ve belge hakkında format, boyut ve şifreleme durumu gibi ayrıntılı bilgileri nasıl çıkaracağınızı öğreneceksiniz. Bir belge‑yönetim sistemi, raporlama motoru veya otomatik dönüşüm hattı oluşturuyor olun, bir dosyanın meta verilerini anlamak güvenilir işleme ilk adımıdır. Dosyayı yüklemekten kaynakları güvenli bir şekilde serbest bırakmaya kadar tüm iş akışını adım adım inceleyelim.

## Hızlı Yanıtlar
- **Bir belgenin sayfa sayısını nasıl alırım?**  
  Dosyayı `Editor` ile yükledikten sonra `editor.GetDocumentInfo().PageCount` çağırın.  
- **Meta veri çıkarımı için hangi dosya formatları desteklenir?**  
  DOCX, XLSX, PPTX, PDF, TXT ve HTML dahil olmak üzere 50'den fazla format.  
- **Şifre korumalı dosyalardan meta veri çıkarabilir miyim?**  
  Evet—`Editor` örneğini oluştururken şifreyi sağlayın.  
- **Kaynakları manuel olarak serbest bırakmam gerekiyor mu?**  
  Kesinlikle; her zaman `editor.Dispose()` çağırın veya editörü bir `using` bloğu içinde kullanın.  
- **Hangi GroupDocs.Editor sürümü gereklidir?**  
  Yazı zamanı itibarıyla en son kararlı sürüm (v23.12+), gösterilen tüm özellikleri destekler.

## GroupDocs.Editor'da “sayfa sayısını al” nedir?
`GetDocumentInfo()` yöntemi, belgenin sayfa sayısı, formatı, boyutu ve diğer meta verilerini içeren bir `DocumentInfo` nesnesi döndürür. Bu tek çağrı, dosyayı manuel olarak ayrıştırmadan anında içgörü sağlar. Bu yöntemi kullanarak, büyük dosyalar için belleğe tüm belgeyi yüklemekten kaçınır, performansı artırır ve sunucu kaynak tüketimini azaltırsınız.

## Neden GroupDocs.Editor ile belge meta verilerini çıkaralım?
GroupDocs.Editor **50+ giriş ve çıkış formatı** işleyebilir ve **2 GB**'a kadar dosyalar için meta verileri, belgeyi belleğe tamamen yüklemeden alabilir. Bu verimlilik, tam belge ayrıştırmasına göre sunucu yükünü **%70** kadar azaltır ve yüksek‑verimli uygulamalar için idealdir.

## Önkoşullar
Başlamadan önce şunlara sahip olun:

- **C# geliştirme temelleri** – Visual Studio ve .NET proje yapılarıyla rahat olmalısınız.  
- **Visual Studio 2022** (veya daha yeni bir sürüm) makinenize kurulu olmalı.  
- **GroupDocs.Editor for .NET** – en son paketi [download page](https://releases.groupdocs.com/editor/net/) adresinden indirin.

## Belgenizi Nasıl Yükleyebilirsiniz?
`Editor`, bir belgeyi temsil eden ana sınıftır ve onu yüklemek ve manipüle etmek için yöntemler sağlar. Hedef dosyayı bir `Editor` örneği oluşturarak ve dosya yolunu geçirerek yükleyin. Editör formatı otomatik olarak algılar, bu yüzden yükleme seçeneklerini belirtmeniz gerekmez. Bu yaklaşım, desteklenen herhangi bir dosya türü için çalışır ve ilk kurulumu basitleştirir.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Belge Bilgilerini Nasıl Alabilirsiniz?
`GetDocumentInfo()` meta veri olarak sayfa sayısı, format, boyut ve şifreleme durumu gibi bilgileri içeren bir `DocumentInfo` nesnesi döndürür. Yükleme sonrası bu yöntemi çağırarak nesneyi alın. Döndürülen `DocumentInfo`, dosyanın özelliklerine dair özlü bir özet sunar ve ek işleme gerek kalmadan karar vermenizi sağlar.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Belge Türünü Nasıl Belirlersiniz?
`DocumentType`, belgenin WordProcessing, Spreadsheet veya Text olup olmadığını gösteren bir enum'dur. Bir dosyanın Word işleme, elektronik tablo veya düz metin olup olmadığını bilmek, sonraki adımlarda nasıl ele alacağınızı etkiler. Bu kararı vermek ve mantığınızı dallandırmak için `DocumentInfo` nesnesinin `DocumentType` özelliğini kullanın.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Word İşleme Dosyaları için Ayrıntılı Bilgileri Nasıl Çıkarırsınız?
`WordProcessing`, DOCX, ODT ve RTF gibi kelime işlem dosyalarını ifade eder. Belge türü `WordProcessing` ise, **format**, **extension**, **page count**, **size** ve **encryption flag** gibi ek özellikleri doğrudan `DocumentInfo` nesnesinden okuyabilirsiniz. Bu ayrıntılar, belirli dönüşümler uygulama veya güvenlik kontrolleri yapma gibi işlem adımlarını özelleştirmenize yardımcı olur.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Elektronik Tablo ve Metin Belgelerini Nasıl İşlersiniz?
`Spreadsheet`, XLSX gibi elektronik tablo dosyalarını; `Text` ise düz‑metin belgelerini temsil eder. `Spreadsheet` ve `Text` için `DocumentInfo` nesnesi hâlâ temel meta verileri (extension, size, page count) sağlar. Bazı formatlar sayfa sayısını sunmayabilir; bu durumda değer **0** olur. Diğer meta verilere dayanarak yine de sonraki mantığı yönlendirebilirsiniz.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Şifre Koruması Olan Belgelerle Nasıl Çalışılır?
`Password`, şifreli dosyaları açmak için `Editor` yapıcısına geçirilen bir dizedir. Bir belge şifreliyse, önce şifresiz açmayı deneyin. Başarısız olursa, istisna yakalanır ve doğru şifreyle tekrar denenir. `Editor` yapıcısı bu amaçla bir `Password` parametresi kabul eder, böylece korumalı dosyalar sorunsuz şekilde işlenir.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Metin Tabanlı Belgeleri Nasıl İşlersiniz?
`DocumentInfo`, metin dosyaları için boyut, uzantı ve kodlama gibi temel meta verileri sağlar. Metin dosyaları (ör. `.txt`, `.md`) basit akışlar olarak ele alınır. `DocumentInfo` üzerinden boyut ve kodlama bilgilerini alabilirsiniz; bu, dosya bütünlüğünü doğrulamak veya uygun işleme hattını belirlemek için faydalıdır.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Kaynakları Doğru Şekilde Nasıl Serbest Bırakırsınız?
`Editor`, yönetilmeyen kaynakları tutan ana sınıftır ve kullanım sonrası serbest bırakılmalıdır. Bellek sızıntılarını önlemek için, bilgi çıkarma işlemi bittikten sonra `Editor` örneğini her zaman serbest bırakın. `using` ifadesi, bir istisna oluşsa bile otomatik olarak imha garantisi verdiği için en güvenli yaklaşımdır ve temiz kaynak yönetimini sağlar.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|----------|
| **PageCount returns 0** | Biçim sayfalama desteklemiyor (ör. düz metin) | `PageCount`'a güvenmeden önce `DocumentInfo.DocumentType` kontrol edin. |
| **Unsupported file format** | Dosya uzantısı tanınmadı | Dosyanın 50+ desteklenen formatlardan biri olduğundan emin olun; GroupDocs.Editor'ı en son sürüme güncelleyin. |
| **Password exception** | Yanlış şifre sağlandı | `PasswordProtectedException` yakalayın ve kullanıcıdan şifreyi yeniden girmesini isteyin. |
| **Memory spike on large files** | Çok büyük PDF'leri akış olmadan yüklemek | `LoadOptions` ile `LoadOptions.LoadMode = LoadMode.Stream` kullanın (yeni sürümlerde mevcut). |

## Sıkça Sorulan Sorular

**Q: Hangi belge türlerinden meta veri çıkarabilirim?**  
A: GroupDocs.Editor, Word işleme, elektronik tablo, sunum, PDF ve düz metin dosyalarını—toplamda 50'den fazla formatı—destekler.

**Q: Dosya uzantısını nasıl alırım?**  
A: `GetDocumentInfo()` çağrısından sonra `DocumentInfo.Extension` özelliğine erişin; ön ek nokta olmadan uzantıyı döndürür.

**Q: Bir belgenin boyutunu megabayt olarak alabilir miyim?**  
A: Evet—`DocumentInfo.Size` bayt cinsinden boyutu verir; megabayta çevirmek için 1 048 576'ya bölün.

**Q: Şifre korumalı dosyaları sunucuda işlemek güvenli mi?**  
A: Kesinlikle—GroupDocs.Editor şifreyi diske asla yazmaz ve kullanım sonrası tüm kriptografik nesneleri serbest bırakır.

**Q: Sorun yaşarsam ek yardım nereden bulabilirim?**  
A: [GroupDocs.Editor destek forumundan](https://forum.groupdocs.com/c/editor/20) destek alabilirsiniz.

---

**Son Güncelleme:** 2026-06-01  
**Test Edilen:** GroupDocs.Editor 23.12 for .NET  
**Yazar:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## İlgili Eğitimler

- [GroupDocs.Editor ile .NET'te Meta Veri Çıkarma: Kapsamlı Rehber](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [GroupDocs.Editor for .NET ile Belge Yükleme Eğitimleri](/editor/net/document-loading/)
- [GroupDocs.Editor .NET ile Verimli Belge Düzenleme: HTML'yi Düzenlenebilir Belgelere Dönüştürme](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)