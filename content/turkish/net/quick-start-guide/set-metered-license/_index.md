---
title: Ölçülü Lisansı Ayarla
linktitle: Ölçülü Lisansı Ayarla
second_title: GroupDocs.Editor .NET API'si
description: Kapsamlı kılavuzumuzla GroupDocs.Editor for .NET'i nasıl entegre edeceğinizi ve kullanacağınızı öğrenin. .NET uygulamalarınızdaki güçlü belge düzenleme özelliklerinin kilidini açın.
weight: 12
url: /tr/net/quick-start-guide/set-metered-license/
type: docs
---
# Ölçülü Lisansı Ayarla

## giriiş
GroupDocs.Editor for .NET'in kullanımına ilişkin adım adım kılavuzumuza hoş geldiniz! İster deneyimli bir geliştirici olun ister yeni başlıyor olun, bu eğitim bu güçlü kitaplığın tüm potansiyelinden yararlanmanıza yardımcı olacaktır. GroupDocs.Editor for .NET, .NET uygulamalarınızdaki çeşitli formatlardaki belgeleri zahmetsizce düzenlemenize olanak tanır. Şimdi ayrıntılı bir şekilde inceleyelim ve bu güçlü araçla nasıl başlayabileceğinizi keşfedelim.
## Önkoşullar
Teknik ayrıntılara geçmeden önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
- .NET programlamaya ilişkin temel bilgi: C# ve .NET Framework'e aşinalık.
- Visual Studio yüklü: Makinenizde Visual Studio'nun en son sürümünün yüklü olduğundan emin olun.
-  GroupDocs.Editor for .NET: Kitaplığı şuradan indirin:[indirme sayfası](https://releases.groupdocs.com/editor/net/).
-  Geçerli bir lisans: Geçici veya tam lisansı[GroupDocs satın alma sayfası](https://purchase.groupdocs.com/temporary-license/).
## Ad Alanlarını İçe Aktar
GroupDocs.Editor for .NET'i kullanmak için projenize gerekli ad alanlarını içe aktarmanız gerekir. Bu adım, projenizi kütüphanenin işlevlerini kullanacak şekilde hazırladığı için çok önemlidir.
```csharp
using System;
using GroupDocs.Editor;
```
Kolayca takip edebilmeniz için her örneği birden fazla adıma ayıralım.
## Adım 1: .NET için GroupDocs.Editor'ı yükleyin
Öncelikle projenize GroupDocs.Editor for .NET'i kurmanız gerekiyor. Bunu Visual Studio'daki NuGet Paket Yöneticisi aracılığıyla yapabilirsiniz.
### NuGet Paket Yöneticisi aracılığıyla yükleme
1. Projenizi Visual Studio'da açın.
2.  Git`Tools` >`NuGet Package Manager` >`Manage NuGet Packages for Solution`.
3.  Aramak`GroupDocs.Editor`.
4.  Tıklamak`Install`.
Bu, projenize gerekli referansları ekleyecektir.
## 2. Adım: Ölçülü Lisans Ayarlayın
GroupDocs.Editor'un tüm özelliklerinin kilidini açmak için ölçülü bir lisans ayarlamanız gerekir. Bu, API'yi herhangi bir sınırlama olmadan kullanmanıza olanak tanır.
### Ölçülü Lisansı Ayarlama
1.  Genel ve özel anahtarlarınızı şu adresten edinin:[GroupDocs satın alma sayfası](https://purchase.groupdocs.com/temporary-license/).
2. Ölçülü lisansı ayarlamak için projenize aşağıdaki kodu ekleyin:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## 3. Adım: Belge Yükleme ve Düzenleme
Artık projeniz ayarlanıp lisanslandığına göre belge yükleme ve düzenleme işlemine geçebiliriz.
### Belge Yükleme
1. Bir belgeyi yüklemek için aşağıdaki kodu ekleyin:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### Belgeyi Düzenleme
2. Belgeyi düzenlemek için düzenlenebilir bir biçime dönüştürmeniz gerekir:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## Adım 4: Düzenlenen Belgeyi Kaydedin
Belgeyi düzenledikten sonra son adım değişikliklerinizi kaydetmektir.
### Belgeyi Kaydetme
1. Düzenlenen içeriği orijinal formata geri dönüştürün:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## Çözüm
 Tebrikler! GroupDocs.Editor for .NET'i uygulamanıza başarıyla entegre ettiniz ve kullandınız. Kitaplığın kurulumundan, ölçülü lisans kurulumuna ve belgeleri düzenlemeye kadar tüm önemli adımları tamamladınız. Bu güçlü araç, .NET uygulamalarınızdaki belge düzenleme iş akışlarınızı önemli ölçüde kolaylaştırabilir. Daha fazla bilgi için bkz.[.NET belgeleri için GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## SSS'ler
### GroupDocs.Editor lisansını nasıl edinebilirim?
 adresinden lisans alabilirsiniz.[GroupDocs satın alma sayfası](https://purchase.groupdocs.com/buy) . Geçici lisans için şu adresi ziyaret edin:[Burada](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor'ı ücretsiz deneyebilir miyim?
 Evet, ücretsiz deneme sürümünü şuradan indirebilirsiniz:[indirme sayfası](https://releases.groupdocs.com/) ve geçici bir lisans isteyin.
### GroupDocs.Editor hangi belge formatlarını destekler?
 GroupDocs.Editor, DOCX, PPTX, XLSX, TXT, HTML ve daha fazlasını içeren çeşitli formatları destekler. Tam liste için şurayı kontrol edin:[dokümantasyon](https://tutorials.groupdocs.com/editor/net/).
### GroupDocs.Editor için herhangi bir topluluk desteği var mı?
 Evet, topluluk desteğini alabilirsiniz.[GroupDocs.Editör forumu](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET'i kullanmaya nasıl başlayabilirim?
 Kitaplığı kurmak, lisans almak ve belgeleri düzenlemeye başlamak için adım adım kılavuzumuzu izleyin. Ayrıntılı talimatlar için şu adresi ziyaret edin:[dokümantasyon](https://tutorials.groupdocs.com/editor/net/).