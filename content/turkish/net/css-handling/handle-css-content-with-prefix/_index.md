---
date: 2026-09-26
description: Bu ayrıntılı step‑by‑step öğreticide, GroupDocs.Editor for .NET kullanarak
  css önekini nasıl ele alacağınızı ve css içeriğini nasıl çıkaracağınızı öğrenin.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Önek ile CSS Content'i Yönet
og_description: GroupDocs.Editor for .NET ile css önekini nasıl ele alacağınızı ve
  css içeriğini nasıl çıkaracağınızı keşfedin. URL'leri CSS resources'a eklemek ve
  stylesheets'i geri almak için step‑by‑step rehberi izleyin.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: GroupDocs.Editor for .NET'te css önekini nasıl ele alırız
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: GroupDocs.Editor for .NET'te css önekini nasıl ele alırız
type: docs
url: /tr/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# GroupDocs.Editor for .NET'te css önekini nasıl yönetilir

Bu öğreticide, GroupDocs.Editor for .NET kullanarak bir belge içinde stil sayfalarıyla çalışırken **css önekini nasıl yöneteceğinizi** öğreneceksiniz. Görsellere, fontlara veya herhangi bir dış kaynağa bir URL eklemeniz gerekse, aşağıdaki adımlar **css önekini nasıl yöneteceğinizi** ve ayrıca **css içeriğini nasıl çıkaracağınızı** tam olarak gösterir. Kılavuzun sonunda kaynak yollarını yeniden yazabilecek, ham CSS dizgelerini alabilecek ve bunları web iş akışınıza güvenle entegre edebileceksiniz.

## Hızlı Yanıtlar
- **“css önekini yönetmek” ne anlama gelir?** CSS içinde başvurulan dış kaynaklara özel bir URL öneki eklemek.  
- **Hangi API yöntemi CSS stillerini döndürür?** `EditableDocument.GetCssContent(...)`.  
- **Bir lisansa ihtiyacım var mı?** Deneme lisansı mevcuttur; üretim için ticari lisans gereklidir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+ ve .NET Core/5/6.  
- **Öneki çalışma zamanında değiştirebilir miyim?** Evet – sadece farklı bir dizeyi `GetCssContent` metoduna geçirin.

## css önekini yönetmek nedir?
Bu terim, bir CSS dosyası içindeki görsellerin, fontların veya herhangi bir dış varlığın URL'lerini, sizin kontrol ettiğiniz bir konuma (örneğin bir CDN veya güvenli bir sunucu) yönlendirecek şekilde yeniden yazmayı ifade eder. Tutarlı bir temel URL ekleyerek, belge bir tarayıcıda veya web‑tabanlı bir görüntüleyicide render edildiğinde her kaynağın doğru şekilde yüklendiğini garanti edersiniz.

## CSS içeriğini çıkarmak için GroupDocs.Editor neden kullanılmalı?
GroupDocs.Editor, WordProcessing belgelerine gömülü orijinal CSS'i okuyabilir, ham stil sayfası dizgelerini döndürebilir ve render etmeden veya kaydetmeden önce bunları manipüle etmenize olanak tanır. Bu, manuel ayrıştırmayı ortadan kaldırır, belgenin iç temsiline sadakati garanti eder ve **30+ dosya formatını** desteklerken **500 MB**'a kadar dosyaları, tüm dosyayı belleğe yüklemeden işleyebilir.

## Önkoşullar
Before we get started, make sure you have the following prerequisites in place:
- Visual Studio: Çalışır bir Visual Studio kurulumuna ihtiyacınız olacak.  
- .NET Framework: .NET Framework'ün kurulu olduğundan emin olun.  
- GroupDocs.Editor for .NET: [GroupDocs.Editor for .NET indirme sayfasından](https://releases.groupdocs.com/editor/net/) indirebilirsiniz.  
- Örnek Belge: Düzenleme için bir örnek belge hazır bulundurun.

## Ad Alanlarını İçe Aktarın
İlk olarak, kodumuzun sorunsuz çalışmasını sağlamak için gerekli ad alanlarını içe aktaralım. Bu adım, GroupDocs.Editor'ın temel sınıflarına erişim sağlar.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Adım 1: Editor'ı Başlatın
`Editor` sınıfı, GroupDocs.Editor'da belgelerle çalışmak için giriş noktasıdır. Yükleme, düzenleme ve kaydetme işlemlerini yönetir.  
İlk adım, örnek belgenizle bir `Editor` örneği oluşturmaktır. Bu, düzenleme ortamını hazırlar.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Adım 2: Belgeyi Düzenleyin
`EditableDocument` nesnesi, dosyanın düzenlenebilir sürümünü temsil eder ve CSS, görseller ve HTML gibi iç bölümlerine erişim sağlar.  
Sonra bir `EditableDocument` nesnesi elde ederiz. Bu nesne, belgenin iç CSS'iyle çalışmamıza olanak tanır.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Adım 3: Dış Önekleri Ayarlayın
Görseller ve fontlar için URL öneklerini tanımlayın. Bu önekler, CSS içinde bulunan her görsel ve font referansının önüne eklenecektir.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Adım 4: Öneklerle CSS içeriğini çıkarın
`GetCssContent`, zaten sağladığınız önekli URL'leri içeren bir CSS stil sayfası dizi koleksiyonu döndürür.  
Az önce tanımladığınız önekleri geçirerek `GetCssContent`'i çağırın. Metod, zaten önekli URL'leri içeren bir CSS stil sayfası dizi listesi döndürür.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Adım 5: Sonuçları Çıktılayın
Bulunan stil sayfalarının sayısını yazdırın ve her stil sayfasını gösterin. Bu, öneklerin doğru şekilde uygulandığını doğrulamanıza yardımcı olur.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Yaygın sorunlar ve çözümler
- **Stil sayfası döndürülmedi** – Kaynak belgenin gerçekten CSS içerdiğinden emin olun (örneğin, stil verilmiş tablolar veya gömülü HTML içeren bir Word belgesi).  
- **Yanlış URL'ler** – Önek dizgelerinin sunucu yönlendirmesi için uygun ayırıcıyla (`/` veya `=`) bittiğini iki kez kontrol edin.  
- **Performans endişeleri** – Çok büyük belgeler için, yüksek bellek kullanımını önlemek amacıyla stil sayfalarını partiler halinde işlemeyi düşünün.

## Sıkça Sorulan Sorular

**Q: GroupDocs.Editor for .NET'i diğer belge formatlarıyla kullanabilir miyim?**  
A: Evet, GroupDocs.Editor for .NET PDF, Word, Excel, PowerPoint ve birçok diğer formatı destekler.

**Q: GroupDocs.Editor for .NET için ücretsiz deneme mevcut mu?**  
A: Kesinlikle! Ücretsiz denemenize [GroupDocs ücretsiz deneme sayfasından](https://releases.groupdocs.com/) başlayabilirsiniz.

**Q: GroupDocs.Editor for .NET için geçici bir lisans nasıl alabilirim?**  
A: [Geçici lisans sayfasından](https://purchase.groupdocs.com/temporary-license/) geçici bir lisans edinebilirsiniz.

**Q: GroupDocs.Editor for .NET için ayrıntılı belgeleri nerede bulabilirim?**  
A: Ayrıntılı belgeler [GroupDocs.Editor for .NET dokümantasyon sitesinde](https://tutorials.groupdocs.com/editor/net/) mevcuttur.

**Q: GroupDocs.Editor for .NET için hangi destek seçenekleri mevcuttur?**  
A: [GroupDocs.Editor destek forumu](https://forum.groupdocs.com/c/editor/20) üzerinden destek alabilirsiniz.

## Ek Sıkça Sorulan Sorular

**Q: CSS'i çıkardıktan sonra önek değiştirilebilir mi?**  
A: Evet. Farklı bir önek dizesiyle `GetCssContent`'i tekrar çağırın; metod her zaman çalışma zamanında gönderdiğiniz değerleri kullanır.

**Q: Bu, şifre korumalı belgelerle çalışır mı?**  
A: Evet. `Editor` örneğini oluştururken şifreyi `WordProcessingLoadOptions` içinde sağlayın.

**Q: Değiştirilmiş CSS'i belgeye geri kaydetmek mümkün mü?**  
A: GroupDocs.Editor şu anda CSS'e yalnızca okuma erişimi sağlar. Değişiklikleri kalıcı kılmak için orijinal stil sayfasını belgenin temel XML API'leriyle değiştirmeniz gerekir.

---

**Son Güncelleme:** 2026-09-26  
**Test Edilen:** GroupDocs.Editor 23.12 for .NET  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Editor .NET Kullanarak Word Belgelerinden Dış CSS Çıkarma: Kapsamlı Rehber](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [GroupDocs.Editor .NET Kullanarak Word Belgelerinden HTML Çıkarma ve Önek Ekleme](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [GroupDocs.Editor .NET Kullanarak Word Belgelerinde HTML İçeriğini Çıkarma ve Değiştirme](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)