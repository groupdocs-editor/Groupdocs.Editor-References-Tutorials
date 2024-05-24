---
title: Sınırlandırılmış Ayrılmış Değerlerle Çalışma (DSV)
linktitle: Sınırlandırılmış Ayrılmış Değerlerle Çalışma (DSV)
second_title: GroupDocs.Editor .NET API'si
description: Bu adım adım kılavuzla GroupDocs.Editor for .NET'i kullanarak CSV ve TSV dosyalarını nasıl düzenleyeceğinizi öğrenin. .NET projelerinizi zahmetsizce geliştirin.
type: docs
weight: 12
url: /tr/net/document-processing/work-dsv/
---
## giriiş
CSV veya TSV dosyaları gibi sınırlandırılmış ayrılmış değerlerle (DSV) çalışan bir geliştiriciyseniz, bu dosyaları programlı olarak düzenlemenin göz korkutucu bir görev olabileceğini biliyorsunuzdur. Ancak GroupDocs.Editor for .NET ile bu görev önemli ölçüde daha basit ve daha verimli hale gelir. Bu eğitimde, DSV dosyalarını okumak, düzenlemek ve kaydetmek için GroupDocs.Editor for .NET'in nasıl kullanılacağı konusunda size yol göstereceğiz. Süreci takip edilmesi kolay adımlara ayırarak projelerinizde uygulamanızı kolaylaştıracağız.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
- Visual Studio: Makinenizde Visual Studio'nun kurulu olduğundan emin olun.
-  GroupDocs.Editor for .NET: GroupDocs.Editor for .NET kitaplığını indirip başvurmanız gerekecektir. İndirebilirsin[Burada](https://releases.groupdocs.com/editor/net/).
- Temel C# Anlayışı: Bu eğitimde, C# ve .NET geliştirme konusunda temel bir anlayışa sahip olduğunuz varsayılmaktadır.
## Ad Alanlarını İçe Aktar
Öncelikle projenize gerekli ad alanlarını içe aktarmanız gerekir. Bu ad alanları, GroupDocs.Editor for .NET ile çalışmak için gereken sınıfları ve yöntemleri sağlar.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Adım 1: Giriş DSV Dosyasının Yolunu Alın
Öncelikle giriş DSV dosyasının yolunu belirtmeniz gerekir. Bu örnekte bunun bir CSV dosyası olduğunu varsayacağız.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Adım: Düzenleyici Örneği Oluşturun
 Bir örneğini oluşturun`Editor` sınıf. Bu örnek, DSV dosyasını yüklemek ve işlemek için kullanılacaktır.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## 3. Adım: DSV Düzenleme Seçeneklerini Oluşturun
 Ardından, bir örneğini oluşturun`DelimitedTextEditOptions` ve DSV dosyası için sınırlayıcıyı belirtin. Burada sınırlayıcı olarak virgül kullanıyoruz.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## 4. Adım: DüzenlenebilirDocument Örneği Oluşturun
 Oluşturduğunuz bir`EditableDocument` örneğini kullanarak`Editor.Edit` yöntem. Bu, belgeyi düzenlemeye hazırlar.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Adım 5: Belge İçeriğini Düzenleyin
Orijinal metin içeriğini alın ve gerekli değişiklikleri yapın. Gösterim amacıyla bazı metinleri değiştirelim.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. Adım: Güncellenmiş İçerikle Düzenlenebilir Bir Belge Oluşturun
 Yeni bir tane oluştur`EditableDocument` güncellenen içerikle.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## 7. Adım: CSV Kaydetme Seçeneklerini Oluşturun
Sınırlayıcı ve kodlama da dahil olmak üzere CSV formatı için kaydetme seçeneklerini belirtin.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## 8. Adım: TSV Kaydetme Seçeneklerini Oluşturun
Benzer şekilde TSV formatı için kaydetme seçeneklerini belirtin.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Adım 9: Elektronik Tablo Kaydetme Seçenekleri Oluşturun
Belgeyi elektronik tablo olarak kaydetmeniz gerekiyorsa ilgili kaydetme seçeneklerini oluşturun.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Adım 10: Kaydetme Yollarını Hazırlayın
Düzenlenen dosyaların kaydedileceği yolları tanımlayın.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Adım 11: Düzenlenen Belgeyi Kaydedin
Düzenlenen belgeyi belirtilen yollara farklı formatlarda kaydedin.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Adım 12: Düzenlenebilir Belge Örneklerini Elden Çıkarın
 Son olarak, çöpe attığınızdan emin olun.`EditableDocument` Kaynakları boşaltmak için örnekler.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Çözüm
DSV dosyalarını GroupDocs.Editor for .NET kullanarak düzenlemek, bir düzenleyici örneği oluşturmayı, düzenleme seçeneklerini ayarlamayı, içeriği değiştirmeyi ve değişiklikleri kaydetmeyi içeren basit bir işlemdir. Bu adım adım kılavuz, bu işlevselliği .NET uygulamalarınıza kolaylıkla entegre etmenize yardımcı olacaktır. İster CSV, TSV, ister diğer DSV formatlarıyla çalışıyor olun, GroupDocs.Editor for .NET sağlam ve esnek bir çözüm sunar.
## SSS'ler
### Büyük CSV dosyalarını düzenlemek için GroupDocs.Editor for .NET'i kullanabilir miyim?
Evet, GroupDocs.Editor for .NET büyük CSV dosyalarını verimli bir şekilde işleme kapasitesine sahiptir.
### GroupDocs.Editor for .NET, CSV ve TSV'nin yanı sıra diğer DSV formatlarını da destekliyor mu?
Evet, uygun sınırlayıcıyı belirttiğiniz sürece çeşitli DSV formatlarını destekler.
### DSV dosyalarını kaydederken kodlamayı özelleştirmek mümkün mü?
Kesinlikle kaydetme seçeneklerinde istediğiniz kodlamayı belirleyebilirsiniz.
### GroupDocs.Editor for .NET'i kullanarak bir CSV dosyasını Excel elektronik tablosuna dönüştürebilir miyim?
Evet, uygun kaydetme seçeneklerini kullanarak bir CSV dosyasını Excel elektronik tablosu olarak kaydedebilirsiniz.
### GroupDocs.Editor for .NET hakkında daha fazla belgeyi nerede bulabilirim?
 Ayrıntılı belgeleri bulabilirsiniz[Burada](https://reference.groupdocs.com/editor/net/)