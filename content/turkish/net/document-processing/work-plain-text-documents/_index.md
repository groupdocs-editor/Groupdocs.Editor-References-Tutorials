---
title: Düz Metin Belgeleriyle Çalışma
linktitle: Düz Metin Belgeleriyle Çalışma
second_title: GroupDocs.Editor .NET API'si
description: Adım adım kılavuzumuzla GroupDocs.Editor for .NET'i kullanarak düz metin belgelerini düzenlemeyi öğrenin. .NET belge düzenleme sürecinizi basitleştirin.
weight: 15
url: /tr/net/document-processing/work-plain-text-documents/
---
## giriiş
.NET'te belge düzenleme sürecinizi kolaylaştırmak mı istiyorsunuz? .NET için GroupDocs.Editor'dan başka bir yere bakmayın! Bu güçlü API, çok çeşitli belge formatlarını kolaylıkla düzenlemenize olanak tanır. Bu öğreticide, GroupDocs.Editor for .NET'i kullanarak düz metin belgeleriyle çalışma sürecinde size rehberlik edeceğiz. Sonunda, metin belgesi düzenlemeyi bir profesyonel gibi yapabilecek donanıma sahip olacaksınız. Dalmaya hazır mısınız? Başlayalım!
## Önkoşullar
Başlamadan önce, hazır bulundurmanız gereken birkaç şey var:
- .NET Geliştirme Ortamı: Çalışan bir .NET geliştirme ortamı kurduğunuzdan emin olun. Visual Studio popüler bir seçimdir.
-  .NET için GroupDocs.Editor: İndirin ve yükleyin.[.NET için GroupDocs.Editor](https://releases.groupdocs.com/editor/net/).
- Temel C# Bilgisi: C# programlama diline aşina olmak, örnekleri takip etmenize yardımcı olacaktır.
- Metin Düzenleyici: Herhangi bir metin düzenleyici işe yarayacaktır, ancak özellikleri ve kullanım kolaylığı nedeniyle Visual Studio Code önerilir.
## Ad Alanlarını İçe Aktar
GroupDocs.Editor for .NET'i kullanmaya başlamak için gerekli ad alanlarını projenize aktarmanız gerekir. Bu, gerekli tüm sınıfların ve yöntemlerin kullanıma hazır olmasını sağlar.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Süreci yönetilebilir adımlara ayıralım. GroupDocs.Editor for .NET'i kullanarak düz metin belgelerini düzenlemenin her aşamasında size rehberlik ettiğimizi takip edin.
## Adım 1: Giriş TXT Dosyasının Yolunu Alın
Öncelikle giriş TXT dosyasının yolunu belirtmeniz gerekir. Bu, yerel bir dosyanın yolu veya dosya içeriğini içeren bir akış olabilir.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## 2. Adım: Düzenleyici Örneği Oluşturun
 Daha sonra, örneğinin bir örneğini oluşturun.`Editor` sınıf. Bu sınıf belgelerin yüklenmesinden ve düzenlenmesinden sorumludur. Bu aşamada herhangi bir yükleme seçeneğine gerek yoktur.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3. Adım: TXT Düzenleme Seçeneklerini Oluşturun
Şimdi TXT düzenleme seçeneklerini oluşturun. Bu seçenekler, düzenleme sırasında metin içeriğinin nasıl işlenmesi gerektiğini belirtmenize olanak tanır.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## 4. Adım: DüzenlenebilirDocument Örneği Oluşturun
 Düzenleme seçenekleri ayarlandığında, bir`EditableDocument` misal. Bu, belgeyi düzenlenebilir bir biçimde temsil eder.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Adım 5: Belge İçeriğini Düzenleyin
Orijinal metin içeriğini alın ve istediğiniz düzenlemeleri yapın. Bu örnekte "metin" kelimesini "DÜZENLENMİŞ metin" ile değiştireceğiz.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. Adım: Güncellenmiş İçerikle Düzenlenebilir Bir Belge Oluşturun
 Gerekli düzenlemeleri yaptıktan sonra yeni bir tane oluşturun.`EditableDocument` güncellenmiş içerik ve orijinal kaynaklarla.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Adım 7: Kelime İşleme Kaydetme Seçenekleri Oluşturun
Kelime İşleme formatı için kaydetme seçeneklerini hazırlayın. Bu örnek DOCM biçimini kullanır ve yerel ayarı belirtir.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Adım 8: TXT Kaydetme Seçeneklerini Oluşturun
Benzer şekilde TXT formatı için kaydetme seçeneklerini oluşturun. Kodlamanın UTF-8 olarak ayarlandığından emin olun ve tablo düzenini koruyun.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Adım 9: Çıkış Yollarını Hazırlayın
Ortaya çıkan DOCX ve TXT dosyalarını kaydetmek için yolları hazırlayın. Çıkış dizinini ve dosya adlarını belirlemek için giriş dosyası yolunu kullanın.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Adım 10: Düzenlenen Belgeyi Kaydedin
Son olarak, düzenlenen belgeyi belirtilen kaydetme seçeneklerini kullanarak hem DOCX hem de TXT formatlarında kaydedin.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Çözüm
 Tebrikler! GroupDocs.Editor for .NET'i kullanarak düz metin belgesini başarıyla düzenlediniz. Bu güçlü araç, belge düzenlemeyi basitleştirerek .NET uygulamalarınızla entegrasyonunu kolaylaştırır. İster basit metin dosyalarıyla ister karmaşık belge formatlarıyla çalışıyor olun, GroupDocs.Editor ihtiyacınızı karşılar. adresini ziyaret ederek daha fazla özellik ve yeteneği keşfedin[GroupDocs.Editor belgeleri](https://tutorials.groupdocs.com/editor/net/).
## SSS'ler
### GroupDocs.Editor for .NET hangi dosya formatlarını destekler?
 GroupDocs.Editor for .NET, DOCX, TXT, HTML ve daha fazlasını içeren çok çeşitli dosya formatlarını destekler. Kontrol edin[dokümantasyon](https://tutorials.groupdocs.com/editor/net/) tam liste için.
### GroupDocs.Editor for .NET'in ücretsiz deneme sürümünü nasıl edinebilirim?
 GroupDocs.Editor for .NET'in ücretsiz deneme sürümünü şu adresten indirebilirsiniz:[sürümler sayfası](https://releases.groupdocs.com/).
### GroupDocs.Editor for .NET için geçici bir lisans satın alabilir miyim?
Evet, geçici lisansı şu adresten alabilirsiniz:[GroupDocs satın alma sayfası](https://purchase.groupdocs.com/temporary-license/).
### .NET için GroupDocs.Editor desteğini nereden alabilirim?
 Destek şu adresten edinilebilir:[GroupDocs.Editor destek forumu](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET'e ilişkin ayrıntılı belgeler mevcut mu?
 Evet, ayrıntılı belgeler şu adreste mevcuttur:[GroupDocs.Editor dokümantasyon sayfası](https://tutorials.groupdocs.com/editor/net/).