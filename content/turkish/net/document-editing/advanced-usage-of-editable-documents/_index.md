---
title: Düzenlenebilir Belgelerin Gelişmiş Kullanımı
linktitle: Düzenlenebilir Belgelerin Gelişmiş Kullanımı
second_title: GroupDocs.Editor .NET API'si
description: GroupDocs.Editor for .NET'in program aracılığıyla belgeler oluşturma, düzenleme ve kaynak çıkarma işlemlerinin ileri düzey kullanımını öğrenin.
weight: 11
url: /tr/net/document-editing/advanced-usage-of-editable-documents/
---
## giriiş
Belge düzenleme yeteneklerinizi geliştirmek isteyen bir .NET geliştiricisiyseniz, GroupDocs.Editor for .NET güçlü bir araç paketi sunar. Bu kapsamlı kılavuz, GroupDocs.Editor'ı kullanarak düzenlenebilir belgelerin gelişmiş kullanımı konusunda size yol gösterecek ve tüm potansiyelinden yararlanabilmenizi sağlamak için her adımı ayrıntılı olarak ele alacaktır.
## Önkoşullar
Gelişmiş işlevlere dalmadan önce aşağıdakilere sahip olduğunuzdan emin olun:
- Geliştirme makinenizde Visual Studio yüklü.
- .NET Framework, GroupDocs.Editor ile uyumludur.
-  .NET kitaplığı için GroupDocs.Editor. Yapabilirsiniz[buradan indir](https://releases.groupdocs.com/editor/net/).
-  Geçerli bir GroupDocs.Editor lisansı. Alabilirsin[ücretsiz deneme](https://releases.groupdocs.com/) veya bir satın alın[geçici lisans](https://purchase.groupdocs.com/temporary-license/).
## Ad Alanlarını İçe Aktar
Başlamak için .NET projenize gerekli ad alanlarını içe aktardığınızdan emin olun:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## 1. Adım: EditableDocument Örneği Oluşturma
 İlk önce bir örneğini oluşturmanız gerekir.`EditableDocument` desteklenen formattaki bir giriş belgesini yükleyip düzenleyerek.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Bu adımda giriş dokümanını yükleyip düzenlemeye hazırlıyoruz.
## Adım 2: Belge Kaynaklarının Çıkarılması
`EditableDocument` Çıkarılabilen ve değiştirilebilen çeşitli kaynaklar içerir. Bunları parçalayalım:
### Adım 2.1: Tüm Belgeyi HTML Olarak Çıkarın
Tüm kaynakları HTML olarak katıştırılmış olarak belgenin tamamını içeren tek bir dize oluşturabilirsiniz.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Bu dize, base64'te kodlanmış stil sayfalarını, görüntüleri ve yazı tiplerini içerdiğinden oldukça büyük olacaktır.
### Adım 2.2: Tüm Görüntüleri Çıkarın
Belgedeki tüm görüntüleri çıkarın.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Adım 2.3: Tüm Yazı Tiplerini Çıkarın
Belgede kullanılan tüm yazı tiplerini çıkarın.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Adım 2.4: Tüm Stil Sayfalarını Çıkarın
Tüm stil sayfalarını metin biçiminde çıkarın.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Adım 2.5: Tüm Kaynakları Toplayın
Tüm kaynakları tek bir çağrıda toplayın.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Buna görseller, yazı tipleri ve stil sayfaları dahildir.
### Adım 2.6: HTML İşaretlemesini Alın
Gömülü kaynaklar olmadan belgenin HTML işaretlemesini alın.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## 3. Adım: Dış Bağlantıları Ayarlama
Bazen harici bağlantıları özel bir kaynak işleyicisine işaret edecek şekilde ayarlamanız gerekir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
### Adım 3.1: Özel Önekler Hazırlayın
Orijinal dış bağlantıların başına eklenecek önekleri hazırlayın.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id = ";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id = ";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id = ";
```
### Adım 3.2: Önekli HTML İşaretlemesi Oluşturun
Ayarlanmış bağlantılarla HTML işaretlemesi oluşturun.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Adım 3.3: Yalnızca Gövde HTML İçeriğini Alın
Bazı WYSIWYG düzenleyicileri yalnızca başlıklar olmadan saf HTML işaretlemesini işler.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Adım 3.4: Önekli Yalnızca Gövde İçeriği
Özel görüntü önekleriyle yalnızca gövde içeriği oluşturun.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Adım 3.5: Stil Sayfalarını Çıkarın
Belgede kullanılan stil sayfalarını çıkarın.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Adım 3.6: Önekli Stil Sayfaları
Stil sayfalarını özel öneklerle çıkarın.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Adım 4: Belgeyi HTML olarak kaydedin
Düzenlenen belgeyi kaynaklarıyla birlikte bir HTML dosyası olarak kaydedin.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Bu yöntem stil sayfaları, resimler ve yazı tipleri gibi kaynaklar için ayrı bir dizin oluşturur.
## Adım 5: EditableDocument'in İmha Edilmesi
 EditableDocument uygular`IDisposable` ve örneğin atılıp atılmadığını kontrol etme olanağı sağlar.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Adım 5.1 Atma Olayını İşleme
Ayrıca imha etkinliğine abone olabilirsiniz.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Adım 6: HTML'den EditableDocument Oluşturma
Bir HTML belgesinden EditableDocument örneğini oluşturun.
### Adım 6.1: HTML Dosyasından
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Adım 6.2: HTML İşaretlemesinden
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Bu örnekler (afterEditFromFile ve afterEditFromMarkup) orijinaliyle (beforeEdit) aynıdır.
## Adım 7: Manuel İmha
EditableDocument örneklerinizi manuel olarak atın.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Bu, kaynakların uygun şekilde temizlenmesini sağlar.
## Çözüm
GroupDocs.Editor for .NET, belgeleri programlı olarak düzenlemek için güçlü araçlar sağlar. Bu adım adım kılavuzu izleyerek belge içeriğini, kaynakları ve çıktı formatlarını verimli bir şekilde yönetebilirsiniz. İster kaynak ekliyor olun, ister harici bağlantıları ayarlayın, ister belgeleri HTML'ye dönüştürün, GroupDocs.Editor sizi gelişmiş belge işleme için gereken işlevsellikle donatır.
## SSS'ler
### GroupDocs.Editor hangi formatları destekler?
GroupDocs.Editor, DOCX, XLSX, PPTX ve daha fazlasını içeren çeşitli formatları destekler.
### GroupDocs.Editor'ı lisans olmadan kullanabilir miyim?
 Evet, bunu bir ile kullanabilirsiniz[ücretsiz deneme](https://releases.groupdocs.com/) veya bir[geçici lisans](https://purchase.groupdocs.com/temporary-license/).
### Bir belgeden belirli kaynakları nasıl çıkarabilirim?
 Aşağıdaki gibi sağlanan yöntemleri kullanarak görüntüleri, yazı tiplerini ve stil sayfalarını çıkarabilirsiniz.`Images`, `Fonts` , Ve`Css`.
### HTML çıktısındaki bağlantıları ayarlamak mümkün mü?
Evet, görseller, CSS ve yazı tipleri için özel önekler belirterek harici bağlantıları ayarlayabilirsiniz.
### Düzenlenmiş bir belgeyi HTML dosyası olarak nasıl kaydederim?
 Kullan`Save` yöntemi`EditableDocument`Belgeyi, kaynakları da dahil olmak üzere bir HTML dosyası olarak kaydetmek için sınıf.