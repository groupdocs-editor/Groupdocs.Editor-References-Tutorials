---
date: 2026-06-06
description: GroupDocs.Editor for .NET kullanarak **her Excel sekmesini kaydetmeyi**
  öğrenin – adım adım kılavuz, kod parçacıkları ve XLSX dosyalarını bölme konusunda
  en iyi uygulamalar.
keywords:
- save each excel tab
- read multiple sheets
- convert excel tab pdf
- split xlsx files
linktitle: Çoklu Sekmeli E-tablolarla Çalışma
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  headline: How to save each Excel tab with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to **save each Excel tab** using GroupDocs.Editor for .NET
    – step‑by‑step guide, code snippets, and best practices for splitting XLSX files.
  name: How to save each Excel tab with GroupDocs.Editor .NET
  steps:
  - name: Get a Path to the Input File
    text: First, specify the full path to the source XLSX that contains multiple tabs.
  - name: Load the Spreadsheet into the Editor Instance
    text: The `Editor` class is the entry point for all document operations in GroupDocs.Editor.
      It reads the file stream and prepares the document for editing or extraction.
  - name: Create an EditableDocument from the First Tab
    text: '`EditableDocument` represents a single, editable sheet within the workbook.
      The constructor takes the `Editor` instance and a zero‑based sheet index.'
  - name: Create an EditableDocument from the Second Tab
    text: You can repeat the same pattern for any additional sheet by changing the
      index value.
  - name: Save the First Tab to a Separate Document
    text: '`Save` writes the edited document to a file in the specified format. Call
      it on the `EditableDocument` instance, providing the output path and format
      (e.g., `SaveFormat.Xlsx`).'
  - name: Save the Second Tab to a Separate Document
    text: The same `Save` call works for the second sheet, and you can choose a different
      format such as PDF if needed.
  - name: Dispose of EditableDocument Instances
    text: '`Dispose` releases unmanaged resources held by the document, such as file
      handles, ensuring no leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: Hidden sheets are treated like any other sheet; you can access them by
      index and save them, but you may need to set `EditableDocument.IsVisible = true`
      before saving if you want them visible in the output.
    question: What if my workbook contains hidden sheets?
  - answer: Yes, specify `SaveFormat.Pdf` when calling `Save` on the `EditableDocument`.
      The library preserves layout, images, and charts during conversion.
    question: Can I convert an Excel tab directly to PDF?
  - answer: Absolutely. Use `SaveFormat.Csv` for each `EditableDocument` to generate
      plain‑text CSV representations of each sheet.
    question: Is it possible to split a workbook into CSV files instead of XLSX?
  - answer: It does. Provide the password via `LoadOptions.Password` when creating
      the `Editor` instance.
    question: Does GroupDocs.Editor support password‑protected Excel files?
  - answer: The official documentation and sample projects on the [download page](https://releases.groupdocs.com/editor/net/)
      contain additional use‑cases.
    question: Where can I find more examples of working with spreadsheets?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: GroupDocs.Editor .NET ile her Excel sekmesini kaydetme
type: docs
url: /tr/net/document-processing/work-multi-tab-spreadsheets/
weight: 17
---

# Çoklu Sekmeli E-Tablolarla Çalışma

## Giriş
Eğer **her bir Excel sekmesini kaydet**meniz gerekiyorsa, GroupDocs.Editor for .NET bu süreci zahmetsiz hâle getirir. Finansal raporları çıkartıyor, departmana göre çalışma sayfaları oluşturuyor veya sekmeleri PDF'ye dönüştürüyor olsanız da, bu öğretici sizi ortam kurulumundan kaynakların serbest bırakılmasına kadar tüm iş akışı boyunca yönlendirir—böylece çoklu sayfa işlemlerini güvenle otomatikleştirebilirsiniz.

## Hızlı Yanıtlar
- **GroupDocs.Editor bir XLSX'i ayrı dosyalara bölebilir mi?** Evet, çalışma kitabını yükleyebilir ve her sayfayı ayrı ayrı dışa aktarabilirsiniz.  
- **Her sekme hangi formatlarda kaydedilebilir?** XLSX, CSV, PDF, HTML ve daha fazlası – 30'dan fazla çıktı formatı desteklenir.  
- **Bu özellik için lisansa ihtiyacım var mı?** Test için geçici bir lisans yeterlidir; üretim için tam lisans gereklidir.  
- **.NET Core destekleniyor mu?** Kesinlikle – kütüphane .NET Framework 4.0+ ve .NET Core/5/6+ ile çalışır.  
- **Bir kerede kaç sekme işlenebilir?** GroupDocs.Editor, tüm dosyayı belleğe yüklemeden 500'den fazla sayfaya sahip çalışma kitaplarını işleyebilir.

## “Her bir Excel sekmesini kaydet” nedir?
**“Her bir Excel sekmesini kaydet”**, çok sayfalı bir çalışma kitabındaki her çalışma sayfasını çıkartıp her birini kendi bağımsız belgesine (ör. ayrı XLSX veya PDF dosyaları) yazmak anlamına gelir. Bu yaklaşım, her sayfa için bir dosya sağlayarak sonraki işlem, raporlama ve dağıtımı basitleştirir; böylece dosyalar paylaşılabilir, arşivlenebilir veya bağımsız olarak daha da dönüştürülebilir.

## Bu görev için neden GroupDocs.Editor kullanılmalı?
GroupDocs.Editor **30'dan fazla giriş ve çıkış formatını** destekler ve **1.000'e kadar sayfa** içeren elektronik tabloları, tüm dosyayı belleğe yüklemek yerine verileri akış olarak işleyerek düşük bellek kullanımıyla işleyebilir. API ayrıca hücre stillerini, formülleri ve gömülü resimleri korur, böylece dışa aktarılan her sekme orijinaliyle aynı görünür.

## Ön Koşullar
Başlamadan önce, aşağıdakilere sahip olduğunuzu doğrulayın:

1. **Visual Studio** – herhangi bir yeni sürüm (Community, Professional veya Enterprise).  
2. **.NET Framework 4.0+** – ya da çapraz platform çalışma zamanı tercih ediyorsanız .NET Core/5/6.  
3. **GroupDocs.Editor for .NET** – bunu [download page](https://releases.groupdocs.com/editor/net/) adresinden indirin.  
4. **License** – test için bir [temporary license](https://purchase.groupdocs.com/temporary-license/) yeterlidir; üretim kullanımı için tam lisans satın alın.  
5. **Free trial** – kütüphaneyi ayrıca [free trial](https://releases.groupdocs.com/) sayfasından deneyebilirsiniz.  
6. **Support** – **issues** karşılaşırsanız, [support forum](https://forum.groupdocs.com/c/editor/20) adresini ziyaret edin veya **full license** için [purchase page](https://purchase.groupdocs.com/buy) sayfasını değerlendirin.

## Ad Alanlarını İçe Aktarma
Kodlamaya başlamadan önce gerekli ad alanlarını içe aktarmanız gerekir. `.cs` dosyanızın en üstüne aşağıdaki using yönergelerini ekleyin:

```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```

## Her bir Excel sekmesini ayrı bir dosya olarak nasıl kaydedersiniz?
Çalışma kitabını yükleyin, her sayfa için bir `EditableDocument` oluşturun ve istediğiniz formatla `Save` metodunu çağırın. Bu süreç her sekmeyi izole eder, farklı bir çıktı yolu seçmenizi sağlar ve kaynakları otomatik olarak serbest bırakır. Aşağıda, her API çağrısının açıklamaları ve yaygın hatalardan kaçınmak için en iyi uygulama ipuçlarıyla birlikte adım adım izleyeceğiniz iş akışı yer almaktadır.

### Adım 1: Giriş Dosyasının Yolunu Alın
İlk olarak, birden fazla sekme içeren kaynak XLSX dosyasının tam yolunu belirtin.

```csharp
string inputFilePath = "Your Sample Document";
```

### Adım 2: Elektronik Tabloyu Editor Örneğine Yükleyin
`Editor` sınıfı, GroupDocs.Editor'deki tüm belge işlemlerinin giriş noktasıdır. Dosya akışını okur ve belgeyi düzenleme ya da çıkarma için hazırlar.

```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Further steps will go here
    }
}
```

### Adım 3: İlk Sekmeden EditableDocument Oluşturun
`EditableDocument`, çalışma kitabındaki tek bir düzenlenebilir sayfayı temsil eder. Yapıcı, `Editor` örneğini ve sıfır‑tabanlı bir sayfa indeksini alır.

```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // First tab
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```

### Adım 4: İkinci Sekmeden EditableDocument Oluşturun
İndeks değerini değiştirerek ek sayfalar için aynı deseni tekrarlayabilirsiniz.

```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Second tab
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```

### Adım 5: İlk Sekmeyi Ayrı Bir Belgeye Kaydedin
`Save`, düzenlenmiş belgeyi belirtilen formatta bir dosyaya yazar. `EditableDocument` örneği üzerinde çağırın ve çıktı yolunu ve formatını (ör. `SaveFormat.Xlsx`) belirtin.

```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```

### Adım 6: İkinci Sekmeyi Ayrı Bir Belgeye Kaydedin
Aynı `Save` çağrısı ikinci sayfa için de çalışır ve gerekirse PDF gibi farklı bir format seçebilirsiniz.

```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```

### Adım 7: EditableDocument Örneklerini Serbest Bırakın
`Dispose`, belge tarafından tutulan yönetilmeyen kaynakları (ör. dosya tutamaçları) serbest bırakır ve uzun süre çalışan hizmetlerde sızıntı olmadığından emin olur.

```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Yaygın Sorunlar ve Çözümler
- **“File is locked” hataları** – Her `EditableDocument` ve `Editor` örneği üzerinde `Dispose()` çağrısı yaptığınızdan emin olun veya `using` ifadeleriyle sarın.  
- **Dışa aktarma sonrası eksik stiller** – Stil desteği sunan bir formata (ör. XLSX veya PDF) kaydettiğinizi doğrulayın. CSV tasarım gereği biçimlendirmeyi kaybeder.  
- **Büyük çalışma kitapları yavaş performansa neden olur** – Bellek kullanımını düşük tutmak için akış yükleme seçeneklerini (`LoadOptions.Streaming = true`) kullanın.

## Sık Sorulan Sorular

**S: Çalışma kitabım gizli sayfalar içeriyorsa ne olur?**  
C: Gizli sayfalar diğer sayfalar gibi ele alınır; indeksle erişebilir ve kaydedebilirsiniz, ancak çıktıda görünür olmalarını istiyorsanız kaydetmeden önce `EditableDocument.IsVisible = true` ayarlamanız gerekebilir.

**S: Bir Excel sekmesini doğrudan PDF'ye dönüştürebilir miyim?**  
C: Evet, `EditableDocument` üzerinde `Save` çağrısı yaparken `SaveFormat.Pdf` belirtebilirsiniz. Kütüphane dönüşüm sırasında düzeni, resimleri ve grafikleri korur.

**S: Bir çalışma kitabını XLSX yerine CSV dosyalarına bölmek mümkün mü?**  
C: Kesinlikle. Her `EditableDocument` için `SaveFormat.Csv` kullanarak her sayfanın düz metin CSV temsillerini oluşturabilirsiniz.

**S: GroupDocs.Editor şifre korumalı Excel dosyalarını destekliyor mu?**  
C: Evet. `Editor` örneğini oluştururken şifreyi `LoadOptions.Password` aracılığıyla sağlayın.

**S: Elektronik tablolarla çalışmaya dair daha fazla örnek nerede bulunabilir?**  
C: Resmi dokümantasyon ve örnek projeler [download page](https://releases.groupdocs.com/editor/net/) adresinde ek kullanım senaryoları içerir.

## Sonuç
Bu adımları izleyerek **her bir Excel sekmesini** bağımsız bir belge olarak kaydedebilir, sekmeleri PDF'ye dönüştürebilir veya büyük çalışma kitaplarını yönetilebilir parçalara bölebilirsiniz—hepsi güvenilir ve yüksek performanslı GroupDocs.Editor for .NET kütüphanesi ile. Bu yetenek raporlama süreçlerini basitleştirir, veri çıkarımını otomatikleştirir ve manuel elektronik tablo işlemlerini azaltır.

---

**Son Güncelleme:** 2026-06-06  
**Test Edilen Versiyon:** GroupDocs.Editor 23.11 for .NET  
**Yazar:** GroupDocs  

---

## İlgili Öğreticiler

- [GroupDocs.Editor ile .NET'te Elektronik Tablo Sekmesi Çıkarma Uzmanı](/editor/net/spreadsheet-documents/mastering-spreadsheet-tab-extraction-dotnet-groupdocs-editor/)
- [GroupDocs.Editor for .NET ile Excel Dosyalarını Şifreleme | Güvenli Elektronik Tablo Yönetimi](/editor/net/spreadsheet-documents/groupdocs-editor-net-password-excel-files/)
- [GroupDocs.Editor ile .NET'te Belge Yüklemeyi Ustalıkla Öğrenme: Kapsamlı Rehber](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)