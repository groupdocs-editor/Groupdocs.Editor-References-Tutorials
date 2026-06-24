---
date: 2026-05-12
description: GroupDocs.Editor for .NET kullanarak belgelerden yazı tiplerini ve diğer
  HTML kaynaklarını nasıl çıkaracağınızı öğrenin. .NET geliştiricileri için adım adım
  rehber.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: HTML Kaynaklarını Klasöre Kaydet
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
title: Yazı Tiplerini Nasıl Çıkarıp HTML Kaynaklarını Klasöre Kaydetmek
type: docs
url: /tr/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Yazı Tiplerini Çıkarma ve HTML Kaynaklarını Klasöre Kaydetme

## Giriş
GroupDocs.Editor for .NET, bir belgeyi HTML'ye dönüştürürken **yazı tiplerini nasıl çıkaracağınızı** ve diğer varlıkları belge üzerinden almanıza olanak tanır. C#'da birkaç satır kodla görüntüleri, stil sayfalarını ve yazı tipi dosyalarını çıkarabilir, ardından istediğiniz bir klasöre kaydedebilirsiniz. Bu eğitim, editörü başlatmaktan her kaynağı diske kaydetmeye kadar tüm iş akışını adım adım gösterir.

## Hızlı Yanıtlar
- **“yazı tiplerini nasıl çıkarılır” ne anlama geliyor?** Bu, HTML dönüşümü sırasında bir kaynak belgede gömülü yazı tipi dosyalarını geri almanın sürecidir.  
- **Hangi kütüphane bunu yönetir?** GroupDocs.Editor for .NET, yazı tiplerini, görüntüleri ve stil sayfalarını çıkarmak için özel bir API sunar.  
- **Bir lisansa ihtiyacım var mı?** Ücretsiz deneme sürümü mevcuttur; üretim kullanımı için ticari lisans gereklidir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Özel bir klasörü hedefleyebilir miyim?** Evet, çıkarılan kaynakları kaydederken istediğiniz yazılabilir yolu belirtebilirsiniz.

## “yazı tiplerini nasıl çıkarılır” nedir?
**Yazı tiplerini nasıl çıkarılır** ifadesi, bir kaynak belgede (ör. DOCX, PPTX) gömülü orijinal yazı tipi dosyalarını alarak oluşturulan HTML'de referans alınabilmesini ifade eder. Bu, metnin tarayıcılarda sistem yazı tiplerine bağımlı olmadan tam olarak istenildiği gibi görüntülenmesini sağlar.

## HTML kaynak çıkarımı için neden GroupDocs.Editor kullanılmalı?
GroupDocs.Editor, **50+ giriş ve çıkış formatını**—DOCX, PPTX, PDF ve HTML dahil—destekler ve **300 sayfaya kadar** belgeleri tüm dosyayı belleğe yüklemeden işleyebilir. API'si, yazı tiplerini, görüntüleri ve CSS'i tek bir geçişte çıkararak manuel ayrıştırmaya kıyasla geliştirme süresini **%70'e kadar** azaltır.

## Önkoşullar
Eğitime başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
1. **C# ve .NET Temel Bilgisi** – C# programlama dili ve .NET çerçevesine aşina olmak, örnekleri takip etmek için gereklidir.  
2. **GroupDocs.Editor for .NET Kütüphanesi** – GroupDocs.Editor for .NET kütüphanesini [web sitesinden](https://releases.groupdocs.com/editor/net/) indirip kurun.  
3. **Geliştirme Ortamı** – Visual Studio gibi tercih ettiğiniz geliştirme ortamını ya da başka bir uyumlu IDE'yi kurun.

## Ad Alanlarını İçe Aktarma
Başlamak için C# projenizde gerekli ad alanlarını içe aktarın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Yazı tiplerini çıkarma ve HTML kaynaklarını bir klasöre kaydetme nasıl yapılır?
Kaynak belgenizi `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` kodu ile yükleyin, ardından `editor.Save("output.html", SaveOptions.Html);` çağrısını yapın. Kaydetme işleminden sonra `Resources` koleksiyonu, yazı tipleri dahil tüm çıkarılan varlıkları içerir; bu varlıkları döngüyle gezerek diske yazabilirsiniz. Bu tek‑adımlı yaklaşım, dönüşüm ve kaynak çıkarımını otomatik olarak gerçekleştirir.

## Adım 1: GroupDocs.Editor'ı Başlatma
`Editor`, belge yükleme, dönüşüm ve kaynak çıkarımını yöneten temel sınıftır. Bellekte tek bir belge oturumunu temsil eder.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
İlk olarak, örnek belgenizin yolunu belirterek `Editor` nesnesini başlatın. Bu örnekte bir Word belgesi kullandığımız için belge türü olarak `WordProcessingLoadOptions` belirtiriz.

## Adım 2: Belgeyi Düzenleme
`EditableDocument`, `Edit` yöntemi tarafından döndürülen düzenlenebilir temsildir ve belgeyi kaydetmeden önce değiştirmenize olanak tanır.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Sonra, `Editor` nesnesinin `Edit` metodunu çağırarak bir `EditableDocument` nesnesi oluşturun. Bu, belge üzerinde düzenleme işlemleri yapmanızı sağlar.

## Adım 3: Kaynakları Çıkarma
`Resources`, çıkarılan varlıkları—görüntüler, yazı tipleri ve stil sayfaları—kolay yönetim için ayrı listelere gruplayan bir koleksiyondur.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Belgeden görüntüler, yazı tipleri ve stil sayfaları gibi kaynakları çıkarın ve ilgili listelerde saklayın.

## Adım 4: Çıktı Klasörünü Belirleme
`outputFolder`, çıkarılan dosyaların yazılacağı yeri tanımlayan bir dizedir. Sunucuda veya yerel makinede herhangi bir yazılabilir dizine işaret edebilirsiniz.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Çıkarılan kaynakların kaydedileceği çıktı klasörünü tanımlayın. Klasör yolunu ihtiyacınıza göre özelleştirebilirsiniz.

## Adım 5: Kaynakları Kaydetme
`SaveResource`, tek bir ikili kaynağı (görüntü, yazı tipi veya stil sayfası) dosya sistemine yazan yardımcı bir rutinidir.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Her bir görüntü kaynağını döngüyle işleyin, çıktı klasörüne kaydedin ve dosya adı, tür ve boyut gibi ilgili bilgileri gösterin.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Benzer şekilde, her bir yazı tipi kaynağını çıktı klasörüne kaydedin.

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
Son olarak, her bir stil sayfasını çıktı klasörüne kaydedin ve düzenleme sürecini tamamlayın.

## Yaygın Sorunlar ve Çözümler
- **Dönüşüm sonrası eksik yazı tipleri** – Kaynak belgenin gerçekten yazı tiplerini gömdüğünden emin olun; aksi takdirde GroupDocs.Editor yalnızca sistem yazı tiplerine referans verebilir.  
- **Erişim reddedildi hataları** – Uygulama sürecinin hedef çıktı klasörüne yazma izni olduğundan emin olun.  
- **Büyük belgeler yüksek bellek kullanımı oluşturur** – Dosyaları tamamen belleğe yüklemek yerine akış olarak işlemek için `LoadOptions` içinde `LoadMode = LoadMode.Stream` kullanın.

## Sık Sorulan Sorular

**S: GroupDocs.Editor, Word dışındaki diğer belge formatlarıyla uyumlu mu?**  
C: Evet, Excel, PowerPoint, PDF, HTML ve düzenleme ve kaynak çıkarımı için 50'den fazla ek formatı destekler.

**S: GroupDocs.Editor'ı bir web uygulamasına entegre edebilir miyim?**  
C: Kesinlikle. API, ASP.NET Core, MVC ve Web API projeleriyle sorunsuz çalışır ve belgeleri sunucu tarafında işlemeye olanak tanır.

**S: GroupDocs.Editor bulut depolama entegrasyonu sağlıyor mu?**  
C: Evet, Google Drive, Dropbox, OneDrive ve Amazon S3 için yerleşik bağlayıcılar içerir; bu sayede belgeleri bulutta doğrudan yükleyip kaydedebilirsiniz.

**S: GroupDocs.Editor için ücretsiz bir deneme sürümü mevcut mu?**  
C: GroupDocs web sitesinden kredi kartı gerektirmeden tam işlevsel 30‑günlük bir deneme sürümü indirilebilir.

**S: Çıkarma sorunları için teknik destek nasıl alabilirim?**  
C: Resmi forum üzerinden GroupDocs destek ekibiyle iletişime geçebilir, müşteri portalı üzerinden bir bilet oluşturabilir veya detaylı API belgelerine başvurabilirsiniz.

---

**Son Güncelleme:** 2026-05-12  
**Test Edildi:** GroupDocs.Editor 23.11 for .NET  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [GroupDocs.Editor .NET ile Verimli Belge Düzenleme: HTML'yi Düzenlenebilir Belgelere Dönüştürme](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [GroupDocs.Editor .NET Kullanarak DOCX Kaynaklarını Verimli Şekilde Çıkarma ve Kaydetme - Tam Kılavuz](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [GroupDocs.Editor .NET ile Belge Düzenleme ve Dönüştürmeyi Ustalaştırma: Tam Kılavuz](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)