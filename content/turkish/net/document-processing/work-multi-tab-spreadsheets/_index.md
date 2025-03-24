---
title: Çok Sekmeli Elektronik Tablolarla Çalışma
linktitle: Çok Sekmeli Elektronik Tablolarla Çalışma
second_title: GroupDocs.Editor .NET API'si
description: GroupDocs.Editor'ı kullanarak .NET'te çok sekmeli elektronik tablolarla nasıl çalışılacağını öğrenin. Adım adım kılavuz, kod örnekleri ve en iyi uygulamalar dahildir.
weight: 17
url: /tr/net/document-processing/work-multi-tab-spreadsheets/
---
## giriiş
Çok sekmeli elektronik tabloları yönetmek, özellikle aynı belge içindeki farklı sayfalardaki verileri değiştirmeniz veya çıkarmanız gerektiğinde oldukça zor bir iş olabilir. .NET ile çalışıyorsanız ve sağlam bir çözüm arıyorsanız, GroupDocs.Editor for .NET mükemmel bir seçimdir. Bu öğreticide, GroupDocs.Editor for .NET'i kullanarak çok sekmeli elektronik tablolarla çalışma sürecinde size yol göstereceğiz. Ortamınızı ayarlamaktan her sekmeyi ayrı bir dosya olarak kaydetmeye kadar her şeyi ele alacağız.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:
1. Visual Studio: Makinenizde Visual Studio'nun kurulu olduğundan emin olun.
2. .NET Framework: .NET için GroupDocs.Editor, .NET Framework 4.0 veya üstünü destekler.
3. GroupDocs.Editor for .NET: GroupDocs.Editor for .NET kitaplığını indirip yükleyin. Şu adresten alabilirsiniz:[indirme sayfası](https://releases.groupdocs.com/editor/net/).
4.  Lisans: Bir lisansı kullanabilirsiniz.[geçici lisans](https://purchase.groupdocs.com/temporary-license/) Kitaplığı denemek için üretimde kullanıma yönelik tam lisans satın almanız önerilir.
## Ad Alanlarını İçe Aktar
Kodlamaya başlamadan önce gerekli ad alanlarını içe aktarmanız gerekir. Aşağıdaki kullanma yönergelerini .cs dosyanızın en üstüne ekleyin:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Giriş Dosyasının Yolunu Alın
Öncelikle giriş e-tablosu dosyanızın yolunu belirtmeniz gerekir. Bu dosya birden fazla sekmeli bir XLSX (OOXML) olmalıdır.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Elektronik Tabloyu Düzenleyici Örneğine Yükleyin
 Daha sonra e-tabloyu bir`Editor` misal. Bu, bir dosya akışı kullanılarak ve bir elektronik tablo için uygun yükleme seçeneklerinin belirtilmesiyle yapılır.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Daha ileri adımlar buraya gelecek
    }
}
```
## 3. İlk Sekmeden Düzenlenebilir Bir Belge Oluşturun
 Belirli bir sekmeyi düzenlemek veya değiştirmek için bir`EditableDocument` bu sekme için örnek. Sekme, 0 tabanlı bir dizin kullanılarak belirtilir.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // İlk sekme
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. İkinci Sekmeden Düzenlenebilir Bir Belge Oluşturun
 Benzer şekilde, bir`EditableDocument` ikinci sekme için.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // İkinci sekme
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. İlk Sekmeyi Ayrı Bir Belgeye Kaydedin
Şimdi ilk sekmeyi ayrı bir belge olarak kaydedin. Kaydetme biçimini ve çıktı yolunu belirtin.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. İkinci Sekmeyi Ayrı Bir Belgeye Kaydedin
İkinci sekme için işlemi tekrarlayın ancak bu sefer farklı bir formatta kaydedin.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. EditableDocument Örneklerini İmha Edin
 Son olarak, cihazı uygun şekilde imha ettiğinizden emin olun.`EditableDocument` Kaynakları boşaltmak için örnekler.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Çözüm
Bu adımları izleyerek GroupDocs.Editor'ı kullanarak .NET'teki çok sekmeli elektronik tablolarla kolayca çalışabilirsiniz. Bu güçlü kitaplık, bir elektronik tablodaki farklı sayfaları düzenleme ve kaydetme sürecini basitleştirerek geliştirme görevlerinizi daha yönetilebilir hale getirir. İster karmaşık veri işlemeyle ister basit düzenlemelerle uğraşıyor olun, GroupDocs.Editor for .NET, işi verimli bir şekilde halletmeniz için ihtiyaç duyduğunuz araçları sağlar.
## SSS'ler
### .NET için GroupDocs.Editor nedir?
GroupDocs.Editor for .NET, geliştiricilerin .NET uygulamaları içindeki çeşitli formatlardaki belgeleri yüklemesine, düzenlemesine ve kaydetmesine olanak tanıyan güçlü bir belge düzenleme API'sidir.
### Satın almadan önce GroupDocs.Editor for .NET'i deneyebilir miyim?
 Evet, kullanabilirsiniz[ücretsiz deneme](https://releases.groupdocs.com/) veya bir istekte bulunun[geçici lisans](https://purchase.groupdocs.com/temporary-license/) Ürünü değerlendirmek için.
### GroupDocs.Editor for .NET hangi dosya formatlarını destekliyor?
GroupDocs.Editor, DOCX, XLSX, PPTX, PDF ve çok daha fazlasını içeren çok çeşitli formatları destekler.
### .NET için GroupDocs.Editor desteğini nasıl alabilirim?
 adresini ziyaret ederek destek alabilirsiniz.[destek Forumu](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET'in tam lisansını nereden satın alabilirim?
 Tam lisansı şuradan satın alabilirsiniz:[satın alma sayfası](https://purchase.groupdocs.com/buy).