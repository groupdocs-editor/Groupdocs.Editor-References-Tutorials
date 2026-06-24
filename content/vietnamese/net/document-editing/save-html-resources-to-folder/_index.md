---
date: 2026-05-12
description: Tìm hiểu cách trích xuất phông chữ và các tài nguyên HTML khác từ tài
  liệu bằng GroupDocs.Editor cho .NET. Hướng dẫn chi tiết từng bước cho các nhà phát
  triển .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Lưu Tài Nguyên HTML vào Thư Mục
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Cách Trích Xuất Phông Chữ và Lưu Tài Nguyên HTML vào Thư Mục
type: docs
url: /vi/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Cách Trích Xuất Phông Chữ và Lưu Tài Nguyên HTML vào Thư Mục

## Giới thiệu
GroupDocs.Editor for .NET cho phép bạn **cách trích xuất phông chữ** và các tài nguyên khác từ một tài liệu khi chuyển đổi nó sang HTML. Chỉ trong vài dòng C# bạn có thể lấy ra hình ảnh, stylesheet và các tệp phông chữ, sau đó lưu chúng vào một thư mục bạn chọn. Hướng dẫn này sẽ đưa bạn qua toàn bộ quy trình, từ khởi tạo editor đến việc lưu từng tài nguyên lên đĩa.

## Câu trả lời nhanh
- **“cách trích xuất phông chữ” có nghĩa là gì?** Đó là quá trình lấy các tệp phông chữ được nhúng từ tài liệu nguồn trong quá trình chuyển đổi sang HTML.  
- **Thư viện nào xử lý việc này?** GroupDocs.Editor for .NET cung cấp một API chuyên dụng để trích xuất phông chữ, hình ảnh và stylesheet.  
- **Tôi có cần giấy phép không?** Một bản dùng thử miễn phí có sẵn; giấy phép thương mại cần thiết cho việc sử dụng trong môi trường sản xuất.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Tôi có thể chỉ định thư mục tùy chỉnh không?** Có, bạn chỉ định bất kỳ đường dẫn có thể ghi được nào khi lưu các tài nguyên đã trích xuất.

## “cách trích xuất phông chữ” là gì?
**Cách trích xuất phông chữ** đề cập đến việc lấy các tệp phông chữ gốc được nhúng trong tài liệu nguồn (ví dụ: DOCX, PPTX) để chúng có thể được tham chiếu bởi HTML được tạo ra. Điều này đảm bảo văn bản hiển thị chính xác như mong muốn trong trình duyệt mà không phụ thuộc vào phông chữ hệ thống.

## Tại sao nên sử dụng GroupDocs.Editor để trích xuất tài nguyên HTML?
GroupDocs.Editor hỗ trợ **hơn 50 định dạng đầu vào và đầu ra**—bao gồm DOCX, PPTX, PDF và HTML—và có thể xử lý tài liệu với **tối đa 300 trang** mà không cần tải toàn bộ tệp vào bộ nhớ. API của nó trích xuất phông chữ, hình ảnh và CSS trong một lần, giảm thời gian phát triển lên tới **70 %** so với việc phân tích thủ công.

## Yêu cầu trước
Trước khi bắt đầu hướng dẫn, hãy đảm bảo bạn có các yêu cầu sau:
1. **Kiến thức cơ bản về C# và .NET** – Quen thuộc với ngôn ngữ lập trình C# và framework .NET là cần thiết để theo dõi các ví dụ.  
2. **Thư viện GroupDocs.Editor cho .NET** – Tải xuống và cài đặt thư viện GroupDocs.Editor cho .NET từ [website](https://releases.groupdocs.com/editor/net/).  
3. **Môi trường phát triển** – Thiết lập môi trường phát triển ưa thích của bạn như Visual Studio hoặc bất kỳ IDE tương thích nào khác.

## Nhập các Namespace
Để bắt đầu, nhập các namespace cần thiết vào dự án C# của bạn:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## Cách trích xuất phông chữ và lưu tài nguyên HTML vào thư mục?
Tải tài liệu nguồn của bạn bằng `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` sau đó gọi `editor.Save("output.html", SaveOptions.Html);`. Sau khi lưu, bộ sưu tập `Resources` chứa tất cả các tài nguyên đã trích xuất—bao gồm phông chữ—mà bạn có thể duyệt và ghi ra đĩa. Cách tiếp cận một bước này tự động xử lý cả việc chuyển đổi và trích xuất tài nguyên.

## Bước 1: Khởi tạo GroupDocs.Editor
`Editor` là lớp cốt lõi điều phối việc tải tài liệu, chuyển đổi và trích xuất tài nguyên. Nó đại diện cho một phiên làm việc tài liệu duy nhất trong bộ nhớ.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Đầu tiên, khởi tạo đối tượng `Editor` bằng cách cung cấp đường dẫn tới tài liệu mẫu của bạn. Trong ví dụ này, chúng ta sử dụng tài liệu Word, vì vậy chúng ta chỉ định `WordProcessingLoadOptions` làm loại tài liệu.

## Bước 2: Chỉnh sửa tài liệu
`EditableDocument` là đại diện có thể chỉnh sửa được trả về bởi phương thức `Edit`, cho phép bạn thao tác tài liệu trước khi lưu.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Tiếp theo, tạo một đối tượng `EditableDocument` bằng cách gọi phương thức `Edit` của đối tượng `Editor`. Điều này cho phép bạn thực hiện các thao tác chỉnh sửa trên tài liệu.

## Bước 3: Trích xuất tài nguyên
`Resources` là một bộ sưu tập nhóm các tài nguyên đã trích xuất—hình ảnh, phông chữ và stylesheet—vào các danh sách riêng biệt để dễ xử lý.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Trích xuất các tài nguyên như hình ảnh, phông chữ và stylesheet từ tài liệu và lưu chúng vào các danh sách tương ứng.

## Bước 4: Chỉ định thư mục đầu ra
`outputFolder` là một chuỗi xác định nơi các tệp đã trích xuất sẽ được ghi. Bạn có thể chỉ đến bất kỳ thư mục có thể ghi nào trên máy chủ hoặc máy cục bộ.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Xác định thư mục đầu ra nơi các tài nguyên đã trích xuất sẽ được lưu. Bạn có thể tùy chỉnh đường dẫn thư mục theo yêu cầu của mình.

## Bước 5: Lưu tài nguyên
`SaveResource` là một hàm trợ giúp ghi một tài nguyên nhị phân duy nhất (hình ảnh, phông chữ hoặc stylesheet) vào hệ thống tệp.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Lặp qua mỗi tài nguyên hình ảnh, lưu nó vào thư mục đầu ra và hiển thị thông tin liên quan như tên tệp, loại và kích thước.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Tương tự, lưu mỗi tài nguyên phông chữ vào thư mục đầu ra.

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
Cuối cùng, lưu mỗi stylesheet vào thư mục đầu ra và hoàn thành quá trình chỉnh sửa.

## Các vấn đề thường gặp và giải pháp
- **Thiếu phông chữ sau khi chuyển đổi** – Đảm bảo tài liệu nguồn thực sự nhúng phông chữ; nếu không, GroupDocs.Editor chỉ có thể tham chiếu tới phông chữ hệ thống.  
- **Lỗi từ chối truy cập** – Kiểm tra xem quá trình ứng dụng có quyền ghi vào thư mục đầu ra mục tiêu hay không.  
- **Tài liệu lớn gây sử dụng bộ nhớ cao** – Sử dụng `LoadOptions` với `LoadMode = LoadMode.Stream` để truyền dữ liệu các tệp lớn thay vì tải toàn bộ vào bộ nhớ.

## Câu hỏi thường gặp

**Q: GroupDocs.Editor có tương thích với các định dạng tài liệu khác ngoài Word không?**  
A: Có, nó hỗ trợ Excel, PowerPoint, PDF, HTML và hơn 50 định dạng bổ sung cho cả việc chỉnh sửa và trích xuất tài nguyên.

**Q: Tôi có thể tích hợp GroupDocs.Editor vào ứng dụng web không?**  
A: Chắc chắn. API hoạt động liền mạch với các dự án ASP.NET Core, MVC và Web API, cho phép bạn xử lý tài liệu phía máy chủ.

**Q: GroupDocs.Editor có cung cấp tích hợp lưu trữ đám mây không?**  
A: Có, nó bao gồm các kết nối tích hợp sẵn cho Google Drive, Dropbox, OneDrive và Amazon S3, cho phép tải lên và lưu tài liệu trực tiếp trên đám mây.

**Q: Có bản dùng thử miễn phí cho GroupDocs.Editor không?**  
A: Một bản dùng thử đầy đủ chức năng 30 ngày có thể tải xuống từ trang web GroupDocs mà không cần yêu cầu thẻ tín dụng.

**Q: Làm thế nào tôi có thể nhận hỗ trợ kỹ thuật cho các vấn đề trích xuất?**  
A: Bạn có thể liên hệ với đội hỗ trợ GroupDocs qua diễn đàn chính thức, gửi ticket qua cổng khách hàng, hoặc tham khảo tài liệu API chi tiết.

---

**Cập nhật lần cuối:** 2026-05-12  
**Kiểm thử với:** GroupDocs.Editor 23.11 cho .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Chỉnh sửa tài liệu hiệu quả với GroupDocs.Editor .NET&#58; Chuyển đổi HTML thành tài liệu có thể chỉnh sửa](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Trích xuất và lưu tài nguyên DOCX một cách hiệu quả bằng GroupDocs.Editor .NET - Hướng dẫn đầy đủ](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Thành thạo chỉnh sửa và chuyển đổi tài liệu với GroupDocs.Editor .NET&#58; Hướng dẫn đầy đủ](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)