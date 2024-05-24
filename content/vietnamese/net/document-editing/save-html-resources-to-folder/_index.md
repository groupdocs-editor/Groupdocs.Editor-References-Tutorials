---
title: Lưu tài nguyên HTML vào thư mục
linktitle: Lưu tài nguyên HTML vào thư mục
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách trích xuất tài nguyên HTML từ tài liệu bằng Groupdocs.Editor cho .NET. Hướng dẫn toàn diện này cung cấp hướng dẫn từng bước cho các nhà phát triển.
type: docs
weight: 13
url: /vi/net/document-editing/save-html-resources-to-folder/
---
## Giới thiệu
Groupdocs.Editor cho .NET là một công cụ mạnh mẽ cho phép các nhà phát triển thao tác và chuyển đổi tài liệu trong ứng dụng .NET của họ một cách liền mạch. Cho dù bạn cần trích xuất tài nguyên HTML từ tài liệu hay thực hiện các tác vụ chỉnh sửa nâng cao, Groupdocs.Editor đều đơn giản hóa quy trình bằng API trực quan và tài liệu mở rộng.
## Điều kiện tiên quyết
Trước khi đi sâu vào hướng dẫn, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
1. Kiến thức cơ bản về C# và .NET: Cần phải làm quen với ngôn ngữ lập trình C# và .NET framework để làm theo các ví dụ.
2.  Groupdocs.Editor for .NET Library: Tải xuống và cài đặt thư viện Groupdocs.Editor for .NET từ[trang mạng](https://releases.groupdocs.com/editor/net/).
3. Môi trường phát triển: Thiết lập môi trường phát triển ưa thích của bạn như Visual Studio hoặc bất kỳ IDE tương thích nào khác.

## Nhập không gian tên
Để bắt đầu, hãy nhập các vùng tên cần thiết trong dự án C# của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Bây giờ, hãy chia nhỏ quy trình lưu tài nguyên HTML vào một thư mục bằng Groupdocs.Editor cho .NET thành nhiều bước:
## Bước 1: Khởi tạo Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Đầu tiên, khởi tạo`Editor`đối tượng bằng cách cung cấp đường dẫn đến tài liệu mẫu của bạn. Trong ví dụ này, chúng tôi đang sử dụng tài liệu Word, vì vậy chúng tôi chỉ định`WordProcessingLoadOptions` như loại tài liệu.
## Bước 2: Chỉnh sửa tài liệu
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 Tiếp theo, tạo một`EditableDocument` đối tượng bằng cách gọi`Edit` phương pháp của`Editor` sự vật. Điều này cho phép bạn thực hiện các thao tác chỉnh sửa trên tài liệu.
## Bước 3: Trích xuất tài nguyên
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Trích xuất các tài nguyên như hình ảnh, phông chữ và biểu định kiểu từ tài liệu và lưu trữ chúng trong danh sách tương ứng.
## Bước 4: Chỉ định thư mục đầu ra
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Xác định thư mục đầu ra nơi tài nguyên được trích xuất sẽ được lưu. Bạn có thể tùy chỉnh đường dẫn thư mục theo yêu cầu của mình.
## Bước 5: Lưu tài nguyên
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Lặp lại từng tài nguyên hình ảnh, lưu nó vào thư mục đầu ra và hiển thị thông tin liên quan như tên tệp, loại và kích thước.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Tương tự, lưu từng tài nguyên phông chữ vào thư mục đầu ra.
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
Cuối cùng, lưu từng biểu định kiểu vào thư mục đầu ra và hoàn tất quá trình chỉnh sửa.

## Phần kết luận
Tóm lại, Groupdocs.Editor cho .NET cung cấp một giải pháp thuận tiện để quản lý và thao tác tài liệu theo chương trình trong các ứng dụng .NET. Bằng cách làm theo hướng dẫn này, bạn có thể dễ dàng trích xuất tài nguyên HTML từ tài liệu và tùy chỉnh quy trình theo yêu cầu cụ thể của mình.
## Câu hỏi thường gặp
### Groupdocs.Editor có tương thích với các định dạng tài liệu khác ngoài Word không?
Có, Groupdocs.Editor hỗ trợ nhiều định dạng tài liệu bao gồm Excel, PowerPoint, PDF, v.v.
### Tôi có thể tích hợp Groupdocs.Editor vào ứng dụng web của mình không?
Hoàn toàn có thể, Groupdocs.Editor cung cấp khả năng tích hợp liền mạch với các ứng dụng web được phát triển trên .NET framework.
### Groupdocs.Editor có cung cấp hỗ trợ cho các dịch vụ lưu trữ đám mây không?
Có, Groupdocs.Editor hỗ trợ tích hợp với các dịch vụ lưu trữ đám mây phổ biến như Google Drive, Dropbox và Microsoft OneDrive.
### Có bản dùng thử miễn phí cho Groupdocs.Editor không?
Có, bạn có thể dùng thử miễn phí Groupdocs.Editor từ trang web.
### Làm cách nào tôi có thể nhận được hỗ trợ kỹ thuật cho Groupdocs.Editor?
Để được hỗ trợ kỹ thuật và hỗ trợ cộng đồng, bạn có thể truy cập diễn đàn Groupdocs.Editor.