---
title: Belgeyi Kaydet
linktitle: Belgeyi Kaydet
second_title: GroupDocs.Editor .NET API'si
description: GroupDocs.Editor for .NET'i kullanarak belgeleri zahmetsizce düzenleyin ve kaydedin. Bu adım adım kılavuz, geliştiriciler için süreci basitleştirir.
weight: 14
url: /tr/net/document-editing/save-document/
type: docs
---
# Belgeyi Kaydet

## giriiş
GroupDocs.Editor for .NET'i kullanarak belgelerinizi zahmetsizce düzenlemeyi ve kaydetmeyi mi istiyorsunuz? Doğru yerdesiniz! Bu eğitim, belgelerinizi kolayca yönetebilmenizi sağlayacak şekilde süreç boyunca size adım adım rehberlik edecektir. İster deneyimli bir geliştirici olun ister yeni başlayan biri olun, kılavuzumuz size başlamanız için ihtiyacınız olan tüm bilgileri sağlayacaktır.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:
- Geliştirme Ortamı: Makinenizde Visual Studio kuruludur.
- .NET Framework: .NET Framework 4.6.1 veya sonraki bir sürümüne sahip olduğunuzdan emin olun.
-  .NET için GroupDocs.Editor: En son sürümü indirin[Burada](https://releases.groupdocs.com/editor/net/).
- Temel C# Bilgisi: C# programlamaya aşinalık çok önemlidir.
## Ad Alanlarını İçe Aktar
GroupDocs.Editor'ı .NET projenizde kullanmak için gerekli ad alanlarını içe aktarmanız gerekir. İşte bunu nasıl yapacağınız:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Artık ortamımızı ayarladığımıza ve gerekli ad alanlarını içe aktardığımıza göre, GroupDocs.Editor for .NET'i kullanarak bir belgeyi yüklemek, düzenlemek ve kaydetmek için gereken adımlara geçelim.
## 1. Adım: Belgeyi Yükleyin
Öncelikle düzenlemek istediğimiz belgeyi yüklememiz gerekiyor. GroupDocs.Editor bu süreci basitleştirir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Bu adımda düzenlemek istediğimiz belgenin yolunu belirtiyoruz ve örneğini oluşturuyoruz.`Editor` sınıf.`Edit` Daha sonra belgeyi bir dosyaya yüklemek için yöntem çağrılır.`EditableDocument` nesne.
## Adım 2: Belgeyi Değiştirin
Belge yüklendiğinde bazı değişiklikler yapmanın zamanı geldi. Ekli bir WYSIWYG düzenleyicimiz olmadığından, düzenleme sürecini kodda simüle edeceğiz.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Burada belgenin gömülü HTML içeriğini alırız, basit bir metin değişimi gerçekleştiririz ve yeni bir metin oluştururuz.`EditableDocument`değiştirilmiş HTML'den örnek.
## 3. Adım: Belgeyi Kaydedin
Belgeyi düzenledikten sonra son adım onu kaydetmektir. GroupDocs.Editor, belgeyi farklı formatlarda kaydetmek için birden fazla seçenek sunar.
## RTF olarak kaydet
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## DOCM olarak kaydet
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Düz Metin olarak kaydet
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Adım 4: Temizleme
 Son olarak, imha edilmesi çok önemlidir.`EditableDocument` Ve`Editor` Kaynakları boşaltmak için örnekler.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Bu adımları izleyerek, GroupDocs.Editor for .NET'i kullanarak belgeleri verimli bir şekilde yükleyebilir, düzenleyebilir ve kaydedebilirsiniz. Bu güçlü araç, esneklik ve kullanım kolaylığı sağlayarak belge yönetimini çocuk oyuncağı haline getirir.
## Çözüm
GroupDocs.Editor for .NET ile belgeleri programlı olarak düzenlemek ve kaydetmek hiç bu kadar kolay olmamıştı. Bu kılavuz, bir belgenin yüklenmesinden onu çeşitli formatlarda kaydetmeye kadar tüm süreç boyunca size yol gösterdi. GroupDocs.Editor ile belge düzenleme sürecini kolaylaştıran çok yönlü ve sağlam bir çözüm parmaklarınızın ucundadır.
## SSS'ler
### GroupDocs.Editor hangi dosya formatlarını destekliyor?
GroupDocs.Editor, DOCX, RTF, TXT ve çok daha fazlası dahil olmak üzere çeşitli dosya formatlarını destekler. Tam liste için şu adrese göz atın:[dokümantasyon](https://tutorials.groupdocs.com/editor/net/).
### Satın almadan önce GroupDocs.Editor'ı deneyebilir miyim?
 Evet, alabilirsiniz[ücretsiz deneme](https://releases.groupdocs.com/) GroupDocs.Editor'un özelliklerini test etmek için.
### Sorunla karşılaşırsam herhangi bir destek var mı?
 Kesinlikle! Ziyaret edebilirsiniz[destek Forumu](https://forum.groupdocs.com/c/editor/20) Karşılaştığınız herhangi bir sorunla ilgili yardım için.
### Geçici lisansı nasıl alabilirim?
 Bir talepte bulunabilirsiniz[geçici lisans](https://purchase.groupdocs.com/temporary-license/) değerlendirme amaçlı.
### GroupDocs.Editor'un tam sürümünü nereden satın alabilirim?
 Tam sürümünü satın alabilirsiniz[Burada](https://purchase.groupdocs.com/buy).