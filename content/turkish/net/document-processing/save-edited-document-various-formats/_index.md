---
title: Düzenlenen Belgeyi Çeşitli Formatlarda Kaydetme
linktitle: Düzenlenen Belgeyi Çeşitli Formatlarda Kaydetme
second_title: GroupDocs.Editor .NET API'si
description: Bu kapsamlı adım adım kılavuzda, GroupDocs.Editor for .NET'i kullanarak düzenlenen belgeleri çeşitli formatlarda nasıl kaydedeceğinizi öğrenin.
type: docs
weight: 11
url: /tr/net/document-processing/save-edited-document-various-formats/
---
## giriiş
Düzenlenen belgeleri GroupDocs.Editor for .NET'i kullanarak çeşitli formatlarda kaydetmek mi istiyorsunuz? Doğru yere geldiniz! Bu kapsamlı kılavuz, ortamınızı ayarlamaktan, düzenlenen belgenizi birden çok formatta kaydetmeye kadar tüm süreç boyunca size yol gösterecektir. Haydi hemen konuya dalalım ve belge düzenlemeyi ve kaydetmeyi çocuk oyuncağı haline getirelim!
## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1.  GroupDocs.Editor for .NET - En son sürümü şu adresten indirin:[Burada](https://releases.groupdocs.com/editor/net/).
2. Geliştirme Ortamı - Visual Studio veya herhangi bir .NET uyumlu IDE.
3. .NET Framework - .NET Framework 4.6.1 veya üstünün kurulu olduğundan emin olun.
4. Örnek Belge - Üzerinde çalışılacak örnek bir Kelime İşleme belgesi.
5. Temel C# Bilgisi - C# programlamaya aşinalık gereklidir.
## Ad Alanlarını İçe Aktar
Başlamak için gerekli ad alanlarını C# projenize aktardığınızdan emin olun. Bu, GroupDocs.Editor işlevselliğine erişim için çok önemlidir.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Süreci yönetilebilir adımlara ayıralım. Her bir parçayı anladığınızdan emin olmak için dikkatlice takip edin.
## Adım 1: Giriş Dosyasının Yolunu Alın
Öncelikle, giriş WordProcessing dosyanızın yolunu belirtmeniz gerekir. Bu dosya yüklenecek ve düzenlenecektir.
```csharp
string inputFilePath = "Your Sample Document";
```
## Adım 2: Belge için Yükleme Seçenekleri Oluşturun
Daha sonra, Kelime İşleme belgelerine özel yükleme seçenekleri oluşturun. Bu seçenekler belgenin yüklenme biçimini özelleştirmenize yardımcı olacaktır.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## 3. Adım: Belgeyi Seçeneklerle Yükleme
 Şimdi belgeyi bir`Editor` örneğin belirtilen yükleme seçeneklerini kullanarak.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## 4. Adım: Düzenleme Seçenekleri Oluşturun
Belge için düzenleme seçeneklerini hazırlayın. Bu seçenekler belgenin düzenleme için nasıl açılacağını belirleyecektir.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Adım 5: Belgeyi Düzenlemek İçin Açın
 Bir belge oluşturarak belgeyi düzenlemek üzere açın.`EditableDocument`misal. Bu örnek belgede değişiklik yapmanıza olanak tanır.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Adım 6: Belge İçeriğini Düzenleyin
Şimdi belgenin içeriğini düzenleme zamanı. Öncelikle belgeyi base64 kodlu tek bir dize olarak alın.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Örneğin belgedeki altyazıyı değiştirelim.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Adım 7: Düzenlenen İçerikten Yeni Düzenlenebilir Belge Oluşturun
 Yeni bir tane oluştur`EditableDocument` Düzenlenen içerik ve kaynaklardan örnek.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Adım 8: Belgeyi Çeşitli Formatlarda Kaydetme
Son olarak, tüm desteklenebilir Kelime İşleme formatlarını yineleyin ve düzenlenen belgeyi her formatta kaydedin.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Kaydetme seçeneklerini hazırlayın
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Kaydetme yolunu hazırla
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Belgeyi kaydet
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Tamamlanma Mesajı
Sonuç olarak işlemin başarıyla tamamlandığını belirten bir mesaj yazdırabilirsiniz.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Çözüm
Tebrikler! GroupDocs.Editor for .NET'i kullanarak düzenlenen belgeleri çeşitli formatlarda nasıl kaydedeceğinizi başarıyla öğrendiniz. Bu güçlü araç, yalnızca birkaç satır kodla birden çok formattaki belgeleri düzenlemeyi ve kaydetmeyi kolaylaştırır. Önemli adımların belgeyi yüklemeyi, içeriği düzenlemeyi ve istenen formatlarda kaydetmeyi içerdiğini unutmayın.
## SSS'ler
### .NET için GroupDocs.Editor nedir?
GroupDocs.Editor for .NET, .NET uygulamalarını kullanarak çeşitli formatlardaki belgeleri düzenlemenize olanak tanıyan güçlü bir API'dir.
### GroupDocs.Editor'ı ücretsiz kullanabilir miyim?
 Evet, ücretsiz deneme sürümüyle kullanabilirsiniz. İndir[Burada](https://releases.groupdocs.com/).
### GroupDocs.Editor hangi formatları destekliyor?
GroupDocs.Editor, DOCX, PDF, HTML ve çok daha fazlasını içeren çok çeşitli formatları destekler.
### GroupDocs.Editor için nasıl geçici lisans alabilirim?
 Geçici lisans alabilirsiniz[Burada](https://purchase.groupdocs.com/temporary-license/).
### Daha fazla belge ve desteği nerede bulabilirim?
 Detaylı dokümantasyon mevcut[Burada](https://reference.groupdocs.com/editor/net/) ve destek alabilirsiniz[Burada](https://forum.groupdocs.com/c/editor/20).