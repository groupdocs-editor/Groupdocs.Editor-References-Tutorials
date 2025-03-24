---
title: HTML İçeriğini Önekle Al
linktitle: HTML İçeriğini Önekle Al
second_title: GroupDocs.Editor .NET API'si
description: Görüntüler ve stil sayfaları için özel öneklerle GroupDocs.Editor for .NET'i kullanarak belgelerden HTML içeriğini nasıl alacağınızı öğrenin. Adım adım kılavuz dahildir.
weight: 11
url: /tr/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## giriiş
GroupDocs.Editor for .NET'i kullanarak bir belgeden HTML içeriğinin nasıl alınacağına ilişkin adım adım eğitimimize hoş geldiniz. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, bu kılavuz süreç boyunca takip edilmesi kolay bir şekilde size yol gösterecektir. Ortamınızı ayarlamaktan kodu başarıyla çalıştırmaya kadar bilmeniz gereken her şeyi ele alacağız. Hadi dalalım!
## Önkoşullar
Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:
1.  .NET için GroupDocs.Editor: En son sürümü şuradan indirin:[indirme sayfası](https://releases.groupdocs.com/editor/net/).
2. Geliştirme Ortamı: Visual Studio veya tercih edilen herhangi bir başka .NET geliştirme ortamı.
3. Temel C# Bilgisi: C# programlamaya aşinalık, örnekleri takip etmenize yardımcı olacaktır.
4. Düzenlenecek Belge: Word belgesi gibi örnek bir belgeyi test için hazır bulundurun.
5. .NET Framework: Makinenizde .NET Framework'ün kurulu olduğundan emin olun.
Artık her şey hazır olduğuna göre başlayalım!
## Ad Alanlarını İçe Aktar
Öncelikle C# projenize gerekli ad alanlarını içe aktarmanız gerekir. Bu ad alanları, GroupDocs.Editor for .NET ile çalışmak için gereken sınıfları ve yöntemleri sağlar.
```csharp
using System;
using GroupDocs.Editor.Options;
```
İçe aktarılan ad alanları ile düzenleyicinin kurulumuna geçebiliriz.
## 1. Adım: Düzenleyiciyi Başlatın
 Başlamak için, başlatmanız gerekir`Editor`belgenizle birlikte sınıfa girin. Bu adım, düzenlemek istediğiniz belgeyi belirtmeyi ve gerekli yükleme seçeneklerini sağlamayı içerir.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Buraya daha fazla adım eklenecek
}
```
 Bu örnekte bir Word belgesi yüklüyoruz. Değiştirebilirsin`"Your Sample Document"` belgenizin yolu ile birlikte.
## 2. Adım: Belgeyi Düzenleyin
 Daha sonra belgeyi düzenlemek için açmamız gerekiyor. Bu, kullanılarak yapılır.`Edit` yöntemi`Editor` gerektiren sınıf`WordProcessingEditOptions` bir argüman olarak.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Buraya daha fazla adım eklenecek
}
```
`EditableDocument` örnek, belgeyi düzenlenebilir bir biçimde temsil eder. Artık HTML içeriğini almaya hazırız.
## 3. Adım: Özel Önekleri Tanımlayın
Resimlere ve CSS'ye özel önekler eklemek için önekleri dize olarak tanımlamamız gerekir. Bu adım, HTML içeriğinin harici kaynaklar için belirtilen öneklere sahip olmasını sağlar.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id = ";
string externalCssPrefix = "http://www.mywebsite.com/css/id = ";
```
URL'leri istediğiniz öneklerle değiştirebilirsiniz. Bu önekler bir sonraki adımda HTML çıktısını özelleştirmek için kullanılacaktır.
## 4. Adım: HTML İçeriğini Alın
Artık öneklerimizi ayarladığımıza göre, HTML içeriğini belgeden alabiliriz.`GetContent` yöntemi`EditableDocument` class, görseli ve CSS öneklerini belirtmemize olanak tanır.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Bu kod parçacığı, HTML içeriğini özel öneklerle getirir ve konsola yazdırır. Bu HTML içeriğini gerektiği gibi daha fazla işleyebilir veya kaydedebilirsiniz.
## Çözüm
İşte buyur! Bu adımları izleyerek, GroupDocs.Editor for .NET'i kullanarak görüntüler ve stil sayfaları için özel öneklerle tamamlanan HTML içeriğini bir belgeden kolayca alabilirsiniz. Bu güçlü araç, belge düzenlemeyi basitleştirerek belge düzenlemeyi .NET uygulamalarınıza sorunsuz bir şekilde entegre etmeye odaklanmanıza olanak tanır.
 Daha ayrıntılı bilgi için şuraya göz atın:[.NET belgeleri için GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/) . Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız varsa, bizimle iletişime geçmekten çekinmeyin.[destek Forumu](https://forum.groupdocs.com/c/editor/20).
## SSS'ler
### GroupDocs.Editor for .NET ile ne tür belgeleri düzenleyebilirim?
GroupDocs.Editor, Word, Excel, PowerPoint, PDF ve daha fazlasını içeren çeşitli belge formatlarını destekler.
### GroupDocs.Editor for .NET'in ücretsiz deneme sürümünü nasıl edinebilirim?
 adresinden ücretsiz deneme alabilirsiniz.[GroupDocs web sitesi](https://releases.groupdocs.com/).
### HTML içeriğini daha da özelleştirebilir miyim?
Evet, alınan HTML içeriğini oluşturmadan veya kaydetmeden önce gerektiği gibi değiştirebilirsiniz.
### GroupDocs.Editor for .NET'i diğer .NET dilleriyle kullanmak mümkün mü?
Evet, VB.NET veya F# gibi .NET uyumlu herhangi bir dille kullanabilirsiniz.
### GroupDocs.Editor for .NET için geçici lisansı nasıl edinebilirim?
 Geçici lisansı şu adresten alabilirsiniz:[satın alma sayfası](https://purchase.groupdocs.com/temporary-license/).