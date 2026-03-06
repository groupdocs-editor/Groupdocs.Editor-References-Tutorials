---
date: 2026-03-06
description: Bu ayrıntılı adım adım öğreticide, GroupDocs.Editor for .NET kullanarak
  ön ekli CSS içeriğini nasıl yöneteceğinizi ve CSS içeriğini nasıl çıkaracağınızı
  öğrenin.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Önek ile CSS İçeriğini İşleyin
type: docs
url: /tr/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# CSS İçeriğini Önek ile İşleme

Bu öğreticide, GroupDocs.Editor for .NET kullanarak bir belge içinde stil sayfalarıyla çalışırken **css önekini nasıl işleyeceğinizi** keşfedeceksiniz. Görsellere, fontlara veya herhangi bir dış kaynağa bir URL eklemeniz gerekse, aşağıdaki adımlar **css önekini nasıl işleyeceğinizi** ve ayrıca **css içeriğini nasıl çıkaracağınızı** tam olarak gösterir.

## Hızlı Yanıtlar
- **“handle css prefix” ne anlama geliyor?** CSS içinde referans verilen dış kaynaklara özel bir URL öneki eklemek.  
- **Hangi API yöntemi CSS stillerini döndürür?** `EditableDocument.GetCssContent(...)`.  
- **Bir lisansa ihtiyacım var mı?** Deneme lisansı mevcuttur; üretim için ticari lisans gereklidir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+ ve .NET Core/5/6.  
- **Öneki çalışma zamanında değiştirebilir miyim?** Evet – sadece `GetCssContent`'a farklı bir dize geçirin.

## **handle css prefix** nedir?
CSS kaynaklarına bir önek uygulamak, görsellerin, fontların veya diğer varlıkların yollarını, kontrol ettiğiniz bir konuma (ör. bir CDN veya güvenli bir sunucu) işaret edecek şekilde yeniden yazar. Bu, bir belgeyi dışa aktardığınızda tüm dış referansların bir web uygulamasından erişilebilir olmasını sağlamak için özellikle yararlıdır.

## **extract css content** için GroupDocs.Editor neden kullanılmalı?
GroupDocs.Editor, WordProcessing belgelerine gömülü orijinal CSS'i okuyabilir, size ham stil sayfası dizelerini verir ve bunları render etmeden veya kaydetmeden önce manipüle etmenizi sağlar. Bu, manuel ayrıştırma ihtiyacını ortadan kaldırır ve çıkarılan CSS'in belgenin iç temsiline uygun olmasını garanti eder.

## Önkoşullar
- Visual Studio: Çalışır bir Visual Studio kurulumuna ihtiyacınız olacak.  
- .NET Framework: .NET Framework'ün kurulu olduğundan emin olun.  
- GroupDocs.Editor for .NET: Bunu [buradan](https://releases.groupdocs.com/editor/net/) indirebilirsiniz.  
- Örnek Belge: Düzenleme için bir örnek belge hazır bulundurun.

## Ad Alanlarını İçe Aktarın
İlk olarak, kodumuzun sorunsuz çalışmasını sağlamak için gerekli ad alanlarını içe aktaralım. Bu adım, GroupDocs.Editor'ın temel sınıflarına erişim sağlar.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Adım 1: Editörü Başlatma
İlk adım, örnek belgenizle bir `Editor` örneği oluşturmaktır. Bu, düzenleme ortamını hazırlar.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Adım 2: Belgeyi Düzenleme
Sonra bir `EditableDocument` nesnesi elde ederiz. Bu nesne, dosyanın düzenlenebilir sürümünü temsil eder ve iç bölümleriyle çalışmamıza olanak tanır.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Adım 3: Dış Önekleri Ayarlama
Görseller ve fontlar için URL öneklerini tanımlayın. Bu önekler, CSS içinde bulunan her görsel ve font referansının önüne eklenecektir.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Adım 4: Öneklerle **CSS içeriğini çıkarma**
`GetCssContent`'i çağırın ve az önce tanımladığınız önekleri geçirin. Metot, zaten önekli URL'leri içeren bir CSS stil sayfası dizesi listesi döndürür.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Adım 5: Sonuçları Çıktılamak
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

## Yaygın Sorunlar ve Çözümler
- **Stil sayfası döndürülmedi** – Kaynak belgenin gerçekten CSS içerdiğinden emin olun (ör. stil verilmiş tablolar veya gömülü HTML içeren bir Word belgesi).  
- **Yanlış URL'ler** – Önek dizelerinin sunucu yönlendirmesi için uygun ayırıcıyla (`/` veya `=`) bittiğini iki kez kontrol edin.  
- **Performans endişeleri** – Çok büyük belgeler için, yüksek bellek kullanımını önlemek amacıyla stil sayfalarını partiler halinde işlemeyi düşünün.

## Sonuç
GroupDocs.Editor for .NET kullanarak bir önek ile CSS içeriğini işlemek basit ve güçlüdür. Bu adımları izleyerek **css önekini işleyebilir**, ham CSS'i **css içeriğini çıkararak** alabilir ve dış kaynakları web iş akışınıza sorunsuz bir şekilde entegre edebilirsiniz. API'den daha fazla değer elde etmek için HTML dönüşümü, görsel çıkarma ve belge birleştirme gibi diğer GroupDocs.Editor özelliklerini keşfedin.

## SSS'ler
### GroupDocs.Editor for .NET'i diğer belge formatlarıyla kullanabilir miyim?
Evet, GroupDocs.Editor for .NET PDF, Word, Excel ve daha fazlası dahil olmak üzere çeşitli belge formatlarını destekler.

### GroupDocs.Editor for .NET için ücretsiz deneme mevcut mu?
Kesinlikle! Ücretsiz denemenize [buradan](https://releases.groupdocs.com/) başlayabilirsiniz.

### GroupDocs.Editor for .NET için geçici bir lisans nasıl alabilirim?
Geçici bir lisansı [buradan](https://purchase.groupdocs.com/temporary-license/) edinebilirsiniz.

### GroupDocs.Editor for .NET için ayrıntılı belgeleri nerede bulabilirim?
Ayrıntılı belgeler [burada](https://tutorials.groupdocs.com/editor/net/) mevcuttur.

### GroupDocs.Editor for .NET için hangi destek seçenekleri mevcut?
Destek alabilirsiniz [buradan](https://forum.groupdocs.com/c/editor/20).

## Ek Sık Sorulan Sorular

**S: CSS'i çıkardıktan sonra öneki değiştirebilir miyim?**  
C: Evet. Farklı bir önek dizesiyle `GetCssContent`'i tekrar çağırın; metod her zaman çalışma zamanında gönderdiğiniz değerleri kullanır.

**S: Bu, şifre korumalı belgelerle çalışır mı?**  
C: Evet. `Editor` örneğini oluştururken şifreyi `WordProcessingLoadOptions` içinde sağlayın.

**S: Değiştirilmiş CSS'i belgeye geri kaydetmek mümkün mü?**  
C: GroupDocs.Editor şu anda CSS'e yalnızca okuma erişimi sağlar. Değişiklikleri kalıcı hale getirmek için orijinal stil sayfasını belgenin temel XML API'leriyle değiştirmeniz gerekir.

---

**Son Güncelleme:** 2026-03-06  
**Test Edilen Versiyon:** GroupDocs.Editor 23.12 for .NET  
**Yazar:** GroupDocs