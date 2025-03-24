---
title: Eski Form Alanı Koleksiyonuyla Çalışma
linktitle: Eski Form Alanı Koleksiyonuyla Çalışma
second_title: GroupDocs.Editor .NET API'si
description: Ayrıntılı kılavuzumuzla GroupDocs.Editor for .NET'i kullanarak eski form alanlarını nasıl yöneteceğinizi öğrenin. Metin alanlarını, onay kutularını, tarihleri ve daha fazlasını yönetmek için mükemmeldir.
weight: 12
url: /tr/net/form-field-management/work-legacy-form-field-collection/
---
## giriiş
GroupDocs.Editor for .NET kullanılarak eski form alanı koleksiyonlarıyla nasıl çalışılacağına ilişkin bu kapsamlı kılavuza hoş geldiniz. İster metin alanları, onay kutuları, tarih alanları veya açılır menülerle ilgileniyor olun, bu eğitim, bu alanları verimli bir şekilde yönetmek için her adımda size yol gösterecektir. Bu kılavuzun sonunda, belgelerinizdeki çeşitli form alanlarını yönetmek için GroupDocs.Editor'ı nasıl kullanacağınıza dair sağlam bir anlayışa sahip olacaksınız. Hadi dalalım!
## Önkoşullar
Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
- Visual Studio: Herhangi bir güncel sürüm çalışacaktır.
- .NET Framework: .NET Framework'ün yüklü olduğundan emin olun.
-  .NET için GroupDocs.Editor: En son sürümü indirin[Burada](https://releases.groupdocs.com/editor/net/).
- Örnek Belge: Test amaçlı form alanları içeren örnek bir DOCX dosyası.
## Ad Alanlarını İçe Aktar
Başlangıç olarak projenize gerekli ad alanlarını içe aktarın. Bu ad alanları, form alanlarını değiştirmek için gereken sınıflara ve yöntemlere erişim için gereklidir.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Adım 1: Giriş Dosyası Yolunu Alın
Öncelikle giriş dosyanızın yolunu belirtmeniz gerekir. Bu örnekte çeşitli form alanlarını içeren örnek bir DOCX dosyası kullanacağız.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## 2. Adım: Dosya Yolundan Akış Oluşturun
Daha sonra belgenizin içeriğini okumak için bir dosya akışı oluşturun. Bu akış, belgeyi GroupDocs.Editor'a yüklemek için kullanılacaktır.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Ek kod buraya gelecek
}
```
## 3. Adım: Belge için Yükleme Seçenekleri Oluşturun
Belgeyi yüklemeden önce yükleme seçeneklerini oluşturun. Bu seçenekler, parola korumalı belgeler gibi farklı senaryoların ele alınmasına yardımcı olacaktır.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Belge parola korumalıysa parolayı belirtin
loadOptions.Password = "your_password_here"; // Gerekirse gerçek bir şifre kullanın
```
## 4. Adım: Belgeyi Düzenleyici Örneğiyle Yükleme
Şimdi, daha önce oluşturduğunuz dosya akışını ve yükleme seçeneklerini kullanarak belgeyi Editor örneğine yükleyin.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Ek kod buraya gelecek
}
```
## 5. Adım: FormFieldManager Örneğini Okuyun
Form alanlarını yönetmek için Düzenleyici'den FormFieldManager örneğine erişin. Bu örnek, belgenizdeki form alanlarıyla etkileşim kurmanıza olanak tanır.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Adım 6: FormFieldCollection'ı okuyun
FormFieldManager'dan FormFieldCollection'ı alın. Bu koleksiyon, belgede bulunan tüm form alanlarını içerir.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Adım 7: Her Form Alanında Yineleme Yapın
Koleksiyondaki her form alanında dolaşın ve türünü tanımlayın. Türe bağlı olarak alanın değerini çıkarabilir ve değiştirebilirsiniz.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Adım 8: Sonuç
Bu adımları izleyerek, GroupDocs.Editor for .NET'i kullanarak belgelerinizdeki eski form alanlarını etkili bir şekilde yönetebilir ve bunlarla etkileşimde bulunabilirsiniz. Metin alanları, onay kutuları, tarihler, sayılar veya açılır listeler olsun, bu kılavuz her türün ele alınması için açık ve kısa bir yol sağlar.
## Çözüm
 Doğru araçları kullandığınızda belgelerdeki eski form alanlarıyla çalışmak kolay olabilir. GroupDocs.Editor for .NET, bu alanları verimli bir şekilde yönetmek için sağlam bir çözüm sağlar. Bu adım adım kılavuzu izleyerek artık belgelerinizdeki çeşitli form alanlarını kolaylıkla yönetebileceksiniz. Keşfetmeyi unutmayın[dokümantasyon](https://tutorials.groupdocs.com/editor/net/)Daha gelişmiş özellikler ve seçenekler için.
## SSS'ler
### 1. GroupDocs.Editor for .NET'i parola korumalı belgelerle kullanabilir miyim?
Evet, parola korumalı belgeleri işlemek için yükleme seçeneklerinde parolayı belirleyebilirsiniz.
### 2. GroupDocs.Editor for .NET'in ücretsiz deneme sürümünü nasıl edinebilirim?
 Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.groupdocs.com/).
### 3. GroupDocs.Editor for .NET için herhangi bir destek mevcut mu?
 Evet, desteğe erişebilirsiniz[Burada](https://forum.groupdocs.com/c/editor/20).
### 4. GroupDocs.Editor for .NET lisansını satın alabilir miyim?
 Evet, adresinden lisans satın alabilirsiniz.[Burada](https://purchase.groupdocs.com/buy).
### 5. GroupDocs.Editor for .NET belgelerini nerede bulabilirim?
Belgeler mevcut[Burada](https://tutorials.groupdocs.com/editor/net/).