---
title: HTML Kaynaklarını Klasöre Kaydet
linktitle: HTML Kaynaklarını Klasöre Kaydet
second_title: GroupDocs.Editor .NET API'si
description: Groupdocs.Editor for .NET'i kullanarak belgelerden HTML kaynaklarını nasıl çıkaracağınızı öğrenin. Bu kapsamlı eğitim, geliştiricilere adım adım rehberlik sağlar.
weight: 13
url: /tr/net/document-editing/save-html-resources-to-folder/
---
## giriiş
Groupdocs.Editor for .NET, geliştiricilerin .NET uygulamaları içindeki belgeleri sorunsuz bir şekilde değiştirmelerine ve dönüştürmelerine olanak tanıyan güçlü bir araçtır. İster bir belgeden HTML kaynaklarını ayıklamanız, ister gelişmiş düzenleme görevleri gerçekleştirmeniz gerekiyorsa, Groupdocs.Editor, sezgisel API'si ve kapsamlı belgeleriyle süreci basitleştirir.
## Önkoşullar
Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:
1. Temel C# ve .NET Bilgisi: C# programlama dili ve .NET çerçevesine aşinalık, örneklerle birlikte takip edilmesi önemlidir.
2.  Groupdocs.Editor for .NET Kitaplığı: Groupdocs.Editor for .NET kitaplığını indirip yükleyin.[İnternet sitesi](https://releases.groupdocs.com/editor/net/).
3. Geliştirme Ortamı: Visual Studio veya diğer uyumlu IDE gibi tercih ettiğiniz geliştirme ortamını kurun.

## Ad Alanlarını İçe Aktar
Başlamak için C# projenize gerekli ad alanlarını içe aktarın:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Şimdi, Groupdocs.Editor for .NET kullanarak HTML kaynaklarını bir klasöre kaydetme işlemini birden çok adıma ayıralım:
## 1. Adım: Groupdocs.Editor'ü başlatın
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 İlk olarak, başlat`Editor`örnek belgenizin yolunu sağlayarak nesneyi oluşturun. Bu örnekte bir Word belgesi kullanıyoruz, dolayısıyla şunu belirtiyoruz:`WordProcessingLoadOptions` belge türü olarak
## Adım 2: Belgeyi Düzenleyin
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Ardından, bir`EditableDocument` çağırarak nesneyi`Edit` yöntemi`Editor` nesne. Bu, belge üzerinde düzenleme işlemleri gerçekleştirmenize olanak tanır.
## 3. Adım: Kaynakları Çıkarın
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Görüntüler, yazı tipleri ve stil sayfaları gibi kaynakları belgeden çıkarın ve bunları ilgili listelerde saklayın.
## Adım 4: Çıktı Klasörünü Belirleyin
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Çıkarılan kaynakların kaydedileceği çıktı klasörünü tanımlayın. Klasör yolunu ihtiyacınıza göre özelleştirebilirsiniz.
## Adım 5: Kaynakları Kaydedin
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Her görüntü kaynağında dolaşın, çıktı klasörüne kaydedin ve dosya adı, tür ve boyutlar gibi ilgili bilgileri görüntüleyin.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Benzer şekilde, her yazı tipi kaynağını çıktı klasörüne kaydedin.
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Son olarak, her stil sayfasını çıktı klasörüne kaydedin ve düzenleme işlemini tamamlayın.

## Çözüm
Sonuç olarak, Groupdocs.Editor for .NET, .NET uygulamaları içindeki belgeleri programlı bir şekilde yönetmek ve değiştirmek için uygun bir çözüm sağlar. Bu öğreticiyi takip ederek HTML kaynaklarını belgelerden kolayca çıkarabilir ve süreci özel gereksinimlerinize göre özelleştirebilirsiniz.
## SSS'ler
### Groupdocs.Editor, Word'ün yanı sıra diğer belge formatlarıyla da uyumlu mu?
Evet, Groupdocs.Editor Excel, PowerPoint, PDF ve daha fazlasını içeren çok çeşitli belge formatlarını destekler.
### Groupdocs.Editor'ı web uygulamama entegre edebilir miyim?
Kesinlikle Groupdocs.Editor, .NET çerçevesinde geliştirilen web uygulamalarıyla kusursuz entegrasyon sunar.
### Groupdocs.Editor bulut depolama hizmetleri için destek sağlıyor mu?
Evet, Groupdocs.Editor, Google Drive, Dropbox ve Microsoft OneDrive gibi popüler bulut depolama hizmetleriyle entegrasyonu destekler.
### Groupdocs.Editor'un ücretsiz deneme sürümü mevcut mu?
Evet, web sitesinden Groupdocs.Editor'ün ücretsiz denemesinden yararlanabilirsiniz.
### Groupdocs.Editor için nasıl teknik destek alabilirim?
Teknik yardım ve topluluk desteği için Groupdocs.Editor forumunu ziyaret edebilirsiniz.