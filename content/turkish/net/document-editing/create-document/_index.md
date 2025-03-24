---
title: Belge Oluştur
linktitle: Belge Oluştur
second_title: GroupDocs.Editor .NET API'si
description: Bu kapsamlı adım adım eğitimle GroupDocs.Editor for .NET'i kullanarak Word, Excel, PowerPoint, E-kitap ve E-posta belgelerini nasıl düzenleyeceğinizi öğrenin.
weight: 10
url: /tr/net/document-editing/create-document/
---
## giriiş
Farklı belge türlerini programlı olarak düzenlemenin getirdiği zorluklardan bıktınız mı? GroupDocs.Editor for .NET, süreci basitleştirmek için burada. Bu güçlü araç, geliştiricilerin Word, Excel, PowerPoint, E-kitaplar ve E-postalar gibi çeşitli belge formatlarını kolaylıkla düzenlemesine olanak tanır. Bu öğreticide, belgeleri oluşturmak ve düzenlemek için GroupDocs.Editor for .NET'in nasıl kullanılacağını ayrıntılı olarak ele alacağız. Süreci takip edilmesi kolay adımlara ayıracağız ve bu konuda yeni olsanız bile erişilebilir olmasını sağlayacağız.
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
- Makinenizde Visual Studio yüklü.
- .NET Framework (4.0 veya üzeri).
-  .NET kitaplığı için GroupDocs.Editor. Şuradan indirebilirsiniz[Burada](https://releases.groupdocs.com/editor/net/).
- Temel C# programlama bilgisi.
## Ad Alanlarını İçe Aktar
Öncelikle gerekli ad alanlarını içe aktaralım. Bu, gerekli sınıfları ve yöntemleri uygulamamızda erişilebilir hale getirecektir.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## 1. Adım: Akışı Ayarlama
Başlangıç olarak belge içeriği için yer tutucumuz görevi görecek bir bellek akışı ayarlamamız gerekiyor.
```csharp
Stream memoryStream = Stream.Null;
```
## Adım 2: Belgeyi Kaydetmek için Geri Arama İşlevi
Daha sonra yeni belge akışını kaydedecek bir geri çağırma işlevi tanımlayın. Bu işlev, belge düzenleme işleminin çıktısını işlemek için gereklidir.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Adım 3: Kelime İşleme Belgesi Oluşturma ve Düzenleme
 Şimdi bir Word belgesi oluşturup düzenleyelim. Yeni bir tane oluşturarak başlayacağız`Editor` WordProcessing belgelerinin örneğini oluşturun ve varsayılan seçeneklerle düzenleyin.
### Varsayılan Seçeneklerle Oluşturun ve Düzenleyin
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Özel Seçeneklerle Oluşturun ve Düzenleyin
Daha fazla kontrol için sayfalandırmayı devre dışı bırakmak ve gömülü yazı tiplerini çıkarmak gibi seçenekleri belirtebiliriz.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Adım 4: Elektronik Tablo Belgesi Oluşturma ve Düzenleme
Benzer şekilde bir Excel belgesi oluşturabilir ve düzenleyebiliriz. İşte bunu nasıl yapacağınız.
### Varsayılan Seçeneklerle Oluşturun ve Düzenleyin
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Özel Seçeneklerle Oluşturun ve Düzenleyin
 Belirli çalışma sayfalarını hedeflemek veya gizli olanları hariç tutmak için şunu kullanırız:`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Adım 5: Sunum Belgesi Oluşturma ve Düzenleme
PowerPoint sunumları da desteklenmektedir. Bunları nasıl halledeceğimizi görelim.
### Varsayılan Seçeneklerle Oluşturun ve Düzenleyin
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Özel Seçeneklerle Oluşturun ve Düzenleyin
Hangi slaytın gösterileceğini, gizli slaytların eklenip eklenmeyeceği gibi seçenekleri belirleyerek düzenlemelerinizi özelleştirebilirsiniz.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Adım 6: Bir E-kitap Belgesi Oluşturma ve Düzenleme
GroupDocs.Editor ayrıca EPUB gibi E-kitap formatlarının düzenlenmesine de olanak tanır. İşte bununla nasıl başa çıkabileceğiniz.
### Varsayılan Seçeneklerle Oluşturun ve Düzenleyin
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Özel Seçeneklerle Oluşturun ve Düzenleyin
Sayfalandırmayı ve dil bilgilerini etkinleştirerek veya devre dışı bırakarak E-kitap düzenlemenizi özelleştirin.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Adım 7: E-posta Belgesi Oluşturma ve Düzenleme
Son olarak e-posta belgelerinin nasıl düzenleneceğine bakacağız. Buna EML gibi formatlar da dahildir.
### Varsayılan Seçeneklerle Oluşturun ve Düzenleyin
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Özel Seçeneklerle Oluşturun ve Düzenleyin
Düzenleme işlemini kontrol etmek için posta mesajı çıkış seçeneklerini belirtin.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Adım 8: Sürecin Sonlandırılması
Belgeleri düzenledikten sonra, kaynakları serbest bırakmak için bellek akışının uygun şekilde imha edilmesi çok önemlidir.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Çözüm
GroupDocs.Editor for .NET, çeşitli belge türlerini programlı olarak düzenleme görevini basitleştirebilen çok yönlü ve güçlü bir araçtır. Bu adım adım kılavuzu izleyerek, ister Kelime İşleme dosyaları, elektronik tablolar, sunumlar, e-kitaplar veya e-postalar olsun, belgeleri kolaylıkla oluşturabilir ve düzenleyebilirsiniz. Daha gelişmiş özellikler ve özelleştirme seçenekleri için GroupDocs.Editor belgelerini inceleyin.
## SSS'ler
### GroupDocs.Editor for .NET ile ne tür belgeleri düzenleyebilirim?
Kelime İşleme, elektronik tablolar, sunumlar, e-kitaplar ve e-postalar da dahil olmak üzere çok çeşitli belgeleri düzenleyebilirsiniz.
### Düzenleme seçeneklerini özelleştirmek mümkün mü?
Evet, GroupDocs.Editor for .NET, her belge türüne özel çeşitli düzenleme seçenekleri aracılığıyla kapsamlı özelleştirmeye olanak tanır.
### Düzenlenen belgelerin çıktısını nasıl halledebilirim?
Düzenlenen belge akışını istediğiniz konuma kaydetmek için geri arama işlevini kullanabilirsiniz.
### GroupDocs.Editor for .NET'i kullanmak için lisansa ihtiyacım var mı?
 Evet, adresinden lisans alabilirsiniz.[Burada](https://purchase.groupdocs.com/buy). Ayrıca geçici lisans seçeneği de bulunmaktadır.
### Daha ayrıntılı belgeleri nerede bulabilirim?
 Ayrıntılı belgeler şu adreste mevcuttur:[.NET dokümantasyon sayfası için GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).