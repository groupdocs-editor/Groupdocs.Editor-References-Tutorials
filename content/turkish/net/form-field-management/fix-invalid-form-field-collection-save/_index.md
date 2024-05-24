---
title: Geçersiz Form Alanı Koleksiyonunu Düzelt ve Kaydet
linktitle: Geçersiz Form Alanı Koleksiyonunu Düzelt ve Kaydet
second_title: GroupDocs.Editor .NET API'si
description: Groupdocs.Editor for .NET'i kullanarak DOCX'teki geçersiz form alanlarını nasıl düzelteceğinizi öğrenin. Belgelerinizin hatasız olduğundan emin olmak ve bunları güvenli bir şekilde kaydetmek için bu kılavuzu izleyin.
type: docs
weight: 11
url: /tr/net/form-field-management/fix-invalid-form-field-collection-save/
---
## giriiş
Hoş geldin! Belgelerdeki form alanlarıyla çalışıyorsanız ve geçersiz form alanı koleksiyonlarıyla ilgili sorunlarla karşılaşıyorsanız doğru yerdesiniz. Bu öğreticide geçersiz form alanlarını nasıl düzelteceğinizi ve Groupdocs.Editor for .NET'i kullanarak belgenizi nasıl kaydedeceğinizi anlatacağız. Süreç boyunca size adım adım rehberlik edeceğiz ve sürecin sorunsuz çalışması için ihtiyacınız olan tüm ayrıntılara sahip olmanızı sağlayacağız. Başlayalım!
## Önkoşullar
Koda geçmeden önce, yerine getirmeniz gereken birkaç şey var:
-  .NET için Groupdocs.Editor: .NET için Groupdocs.Editor kitaplığını yüklediğinizden emin olun. İndirebilirsin[Burada](https://releases.groupdocs.com/editor/net/).
- Geliştirme Ortamı: Visual Studio gibi bir .NET geliştirme ortamına sahip olmanız gerekir.
- Temel C# Bilgisi: Bu eğitimde, C# programlama konusunda temel bir anlayışa sahip olduğunuz varsayılmaktadır.
## Ad Alanlarını İçe Aktar
Öncelikle C# projenize gerekli ad alanlarını içe aktarmanız gerekir. Kod dosyanızın başına aşağıdaki satırları ekleyin:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Adım 1: Giriş Dosyası Yolunu Alın
İlk adım, giriş dosyanızın yolunu belirtmektir. Bu dosya form alanlarını içeren bir DOCX belgesi olmalıdır.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## 2. Adım: Dosya Yolundan Akış Oluşturun
Ardından, giriş belgesini okumak için bir dosya akışı oluşturun. Bu, belgeyi düzenleyiciye yüklemenize olanak tanır.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## 3. Adım: Belge için Yükleme Seçenekleri Oluşturun
Bu adımda belgeniz için yükleme seçenekleri oluşturmanız gerekir. Belgeniz şifre korumalı ise şifreyi belirleyebilirsiniz. Bu örnekte belge korunmadığından parola dikkate alınmaz.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## 4. Adım: Belgeyi Düzenleyici Örneğine Yükleyin
Şimdi, belirtilen seçeneklere sahip belgeyi Editor örneğine yükleyin. Belge üzerindeki ana işlemlerin gerçekleştirileceği yer burasıdır.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Adım 4.1: FormFieldManager Örneğini Okuyun
`FormFieldManager` örnek, belgedeki form alanlarının yönetilmesinden sorumludur. Form alanlarına erişmek ve bunları değiştirmek için bu örneği okumanız gerekir.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Adım 4.2: FormFieldCollection'ı okuyun
`FormFieldCollection` belgedeki tüm form alanlarını içerir. Geçersiz form alanlarını kontrol etmek ve düzeltmek için bu koleksiyonu okuyacaksınız.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Adım 4.3: Geçersiz Form Alanlarını Otomatik Düzelt
Belgedeki geçersiz form alanlarını otomatik olarak düzeltmeye çalışın. Bu, bariz sorunları çözmeye yönelik bir ön adımdır.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Adım 4.4: Geçersiz Form Alanlarını Kontrol Edin
Otomatik düzeltme denemesinden sonra geçersiz form alanı kalıp kalmadığını kontrol edin.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Adım 4.4.1: Tüm Geçersiz Form Alanı Adlarını Alın
Tüm geçersiz form alanlarının adlarını alın. Bu adlar alanları düzeltmek için kullanılacaktır.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Adım 4.4.2: Geçersiz Alanlar için Benzersiz Adlar Oluşturun
Her geçersiz form alanı için benzersiz bir ad oluşturun. Bu, mevcut form alanı adlarıyla çakışma olmamasını sağlar.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Adım 4.4.3: Geçersiz Form Alanlarını Düzeltin
Önceki adımda oluşturulan benzersiz adları kullanarak geçersiz form alanlarını düzeltin.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Adım 5: Belge Kaydetme Seçenekleri Oluşturun
Belgeyi kaydetme seçeneklerini ayarlayın. Buna formatın belirtilmesi ve ek kaydetme ayarları da dahildir.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Adım 5.1: Bellek Kullanımını Optimize Edin
 Belgeniz büyükse ve sorun yaratabiliyorsa`OutOfMemoryException`bellek optimizasyonu seçeneğini etkinleştirin.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Adım 5.2: Belgeyi Yazmaya Karşı Koruyun
Belgeyi form alanları dışında değiştirilmeye karşı korumak için bir koruma parolası ayarlayın.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Adım 6: Belgeyi Kaydedin
Son olarak belgeyi belirtilen kaydetme seçenekleriyle kaydedin. Çıktı belgesini kaydetmek için bir bellek akışı hazırlayın.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Çözüm
 İşte buyur! Geçersiz form alanlarını başarıyla düzelttiniz ve belgenizi Groupdocs.Editor for .NET'i kullanarak kaydettiniz. Bu adım adım kılavuzun süreci açık ve yönetilebilir hale getirmesi gerekirdi. Herhangi bir sorunla karşılaşırsanız veya sorularınız varsa, kontrol etmekten çekinmeyin.[dokümantasyon](https://reference.groupdocs.com/editor/net/) veya iletişime geçin[Destek](https://forum.groupdocs.com/c/editor/20).
## SSS'ler
### Belgem parola korumalıysa ne olur?
 Şifreyi şurada belirtebilirsiniz`WordProcessingLoadOptions` Belgeyi açmak için.
### Geçersiz form alanları olup olmadığını nasıl anlarım?
 Kullan`HasInvalidFormFields` Belgedeki geçersiz form alanlarını kontrol etme yöntemi.
### Form alanlarını adlarını değiştirmeden düzeltebilir miyim?
Çakışmaları önlemek amacıyla geçersiz form alanlarına benzersiz adlar oluşturmanız önerilir.
### Belgeyi hangi formatlarda kaydedebilirim?
 Uygun formatı ayarlayarak belgeyi DOCX, PDF ve daha fazlası gibi çeşitli formatlarda kaydedebilirsiniz.`WordProcessingFormats`.
### Büyük belgeleri kaydederken bellek kullanımını nasıl optimize edebilirim?
 Etkinleştir`OptimizeMemoryUsage` seçeneğindeki`WordProcessingSaveOptions` Büyük belgeleri verimli bir şekilde işlemek için.