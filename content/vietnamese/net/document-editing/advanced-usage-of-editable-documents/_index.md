---
title: Cách sử dụng nâng cao các tài liệu có thể chỉnh sửa
linktitle: Cách sử dụng nâng cao các tài liệu có thể chỉnh sửa
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách sử dụng nâng cao của GroupDocs.Editor để tạo, chỉnh sửa và trích xuất tài nguyên từ tài liệu theo chương trình.
type: docs
weight: 11
url: /vi/net/document-editing/advanced-usage-of-editable-documents/
---
## Giới thiệu
Nếu bạn là nhà phát triển .NET đang tìm cách nâng cao khả năng chỉnh sửa tài liệu của mình thì GroupDocs.Editor dành cho .NET cung cấp một bộ công cụ mạnh mẽ. Hướng dẫn toàn diện này sẽ hướng dẫn bạn cách sử dụng nâng cao các tài liệu có thể chỉnh sửa bằng GroupDocs.Editor, chia nhỏ từng bước một cách chi tiết để đảm bảo bạn có thể khai thác hết tiềm năng của nó.
## Điều kiện tiên quyết
Trước khi đi sâu vào các chức năng nâng cao, hãy đảm bảo bạn có những điều sau:
- Visual Studio được cài đặt trên máy phát triển của bạn.
- .NET Framework tương thích với GroupDocs.Editor.
-  GroupDocs.Editor cho thư viện .NET. Bạn có thể[tải về tại đây](https://releases.groupdocs.com/editor/net/).
-  Giấy phép GroupDocs.Editor hợp lệ. Bạn có thể nhận được một[dùng thử miễn phí](https://releases.groupdocs.com/) hoặc mua một[giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).
## Nhập không gian tên
Để bắt đầu, hãy đảm bảo bạn nhập các vùng tên cần thiết trong dự án .NET của mình:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Bước 1: Tạo một phiên bản EditableDocument
 Đầu tiên, bạn cần tạo một thể hiện của`EditableDocument` bằng cách tải và chỉnh sửa tài liệu đầu vào có định dạng được hỗ trợ.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Ở bước này, chúng ta tải tài liệu đầu vào và chuẩn bị chỉnh sửa.
## Bước 2: Trích xuất tài nguyên tài liệu
 Các`EditableDocument` chứa nhiều tài nguyên khác nhau có thể được trích xuất và thao tác. Hãy chia nhỏ những điều này:
### Bước 2.1: Trích xuất toàn bộ tài liệu dưới dạng HTML
Bạn có thể tạo một chuỗi chứa toàn bộ tài liệu với tất cả tài nguyên được nhúng dưới dạng HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Chuỗi này sẽ khá lớn vì nó bao gồm các bảng định kiểu, hình ảnh và phông chữ được mã hóa trong base64.
### Bước 2.2: Trích xuất tất cả hình ảnh
Trích xuất tất cả hình ảnh từ tài liệu.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Bước 2.3: Trích xuất tất cả phông chữ
Trích xuất tất cả các phông chữ được sử dụng trong tài liệu.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Bước 2.4: Trích xuất tất cả các bảng định kiểu
Trích xuất tất cả các bảng định kiểu ở định dạng văn bản.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Bước 2.5: Thu thập tất cả tài nguyên
Tập hợp tất cả các tài nguyên trong một cuộc gọi.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Điều này bao gồm hình ảnh, phông chữ và bảng định kiểu.
### Bước 2.6: Lấy đánh dấu HTML
Nhận đánh dấu HTML của tài liệu mà không cần tài nguyên được nhúng.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Bước 3: Điều chỉnh liên kết ngoài
Đôi khi, bạn cần điều chỉnh các liên kết bên ngoài để trỏ đến trình xử lý tài nguyên tùy chỉnh. Đây là cách thực hiện:
### Bước 3.1: Chuẩn bị tiền tố tùy chỉnh
Chuẩn bị các tiền tố sẽ thêm vào các liên kết bên ngoài ban đầu.
```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```
### Bước 3.2: Tạo đánh dấu HTML có tiền tố
Tạo đánh dấu HTML với các liên kết được điều chỉnh.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Bước 3.3: Lấy nội dung HTML chỉ có nội dung
Một số trình soạn thảo WYSIWYG chỉ xử lý đánh dấu HTML thuần túy không có tiêu đề.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Bước 3.4: Nội dung chỉ có nội dung có tiền tố
Tạo nội dung chỉ có nội dung với tiền tố hình ảnh tùy chỉnh.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Bước 3.5: Trích xuất bảng định kiểu
Trích xuất các bảng định kiểu được sử dụng trong tài liệu.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Bước 3.6: Bảng định kiểu có tiền tố
Trích xuất các bảng định kiểu với tiền tố tùy chỉnh.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Bước 4: Lưu tài liệu dưới dạng HTML
Lưu tài liệu đã chỉnh sửa dưới dạng tệp HTML, bao gồm cả tài nguyên của nó.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Phương pháp này tạo một thư mục riêng cho các tài nguyên như biểu định kiểu, hình ảnh và phông chữ.
## Bước 5: Loại bỏ tài liệu có thể chỉnh sửa
 Công cụ EditableDocument`IDisposable` và cung cấp khả năng kiểm tra xem phiên bản đó có được xử lý hay không.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Bước 5.1 Xử lý sự kiện vứt bỏ
Bạn cũng có thể đăng ký sự kiện xử lý.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Bước 6: Tạo tài liệu có thể chỉnh sửa từ HTML
Tạo một phiên bản EditableDocument từ một tài liệu HTML.
### Bước 6.1: Từ tệp HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Bước 6.2: Từ đánh dấu HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Các phiên bản này (afterEditFromFile và afterEditFromMarkup) giống hệt với phiên bản gốc (trướcEdit).
## Bước 7: Xử lý thủ công
Loại bỏ thủ công các phiên bản EditableDocument của bạn.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Điều này đảm bảo làm sạch tài nguyên thích hợp.
## Phần kết luận
GroupDocs.Editor cho .NET cung cấp các công cụ mạnh mẽ để chỉnh sửa tài liệu theo chương trình. Bằng cách làm theo hướng dẫn từng bước này, bạn có thể quản lý nội dung tài liệu, tài nguyên và định dạng đầu ra một cách hiệu quả. Cho dù bạn đang nhúng tài nguyên, điều chỉnh liên kết bên ngoài hay chuyển đổi tài liệu sang HTML, GroupDocs.Editor đều trang bị cho bạn chức năng cần thiết để thao tác tài liệu nâng cao.
## Câu hỏi thường gặp
### GroupDocs.Editor hỗ trợ những định dạng nào?
GroupDocs.Editor hỗ trợ nhiều định dạng khác nhau bao gồm DOCX, XLSX, PPTX, v.v.
### Tôi có thể sử dụng GroupDocs.Editor mà không cần giấy phép không?
 Có, bạn có thể sử dụng nó với[dùng thử miễn phí](https://releases.groupdocs.com/) hoặc một[giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).
### Làm cách nào để trích xuất các tài nguyên cụ thể từ một tài liệu?
 Bạn có thể trích xuất hình ảnh, phông chữ và biểu định kiểu bằng các phương pháp được cung cấp như`Images`, `Fonts` , Và`Css`.
### Có thể điều chỉnh các liên kết trong đầu ra HTML không?
Có, bạn có thể điều chỉnh các liên kết bên ngoài bằng cách chỉ định tiền tố tùy chỉnh cho hình ảnh, CSS và phông chữ.
### Làm cách nào để lưu tài liệu đã chỉnh sửa dưới dạng tệp HTML?
 Sử dụng`Save` phương pháp của`EditableDocument`class để lưu tài liệu dưới dạng tệp HTML, bao gồm cả tài nguyên của nó.