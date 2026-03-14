---
date: 2026-03-14
description: Tìm hiểu cách trích xuất hình ảnh từ DOCX, chuyển DOCX sang HTML và lưu
  tài liệu dưới dạng HTML bằng GroupDocs.Editor cho .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Trích xuất hình ảnh từ DOCX – Sử dụng tài liệu có thể chỉnh sửa nâng cao
type: docs
url: /vi/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

 With:** GroupDocs.Editor for .NET (latest release)" -> "**Kiểm tra với:** GroupDocs.Editor cho .NET (phiên bản mới nhất)". "**Author:** GroupDocs" -> "**Tác giả:** GroupDocs".

Make sure to keep markdown formatting.

Now produce final content.# Trích xuất hình ảnh từ DOCX – Sử dụng tài liệu có thể chỉnh sửa nâng cao

Nếu bạn là một nhà phát triển .NET muốn **trích xuất hình ảnh từ DOCX** và nâng cao khả năng chỉnh sửa tài liệu, GroupDocs.Editor cho .NET cung cấp một bộ công cụ mạnh mẽ. Hướng dẫn toàn diện này sẽ hướng dẫn bạn cách sử dụng nâng cao các tài liệu có thể chỉnh sửa bằng GroupDocs.Editor, phân tích chi tiết từng bước để bạn có thể khai thác tối đa tiềm năng của nó.

## Câu trả lời nhanh
- **Làm thế nào để tôi có thể trích xuất hình ảnh từ tệp DOCX?** Sử dụng `EditableDocument.Images` sau khi tải tài liệu bằng `Editor`.
- **Tôi có thể chuyển DOCX sang HTML với các tài nguyên nhúng không?** Có—gọi `EditableDocument.GetEmbeddedHtml()` hoặc `GetContent()` để lấy mã HTML.
- **Phương thức nào lưu tài liệu đã chỉnh sửa dưới dạng HTML?** `EditableDocument.Save(htmlFilePath)` tạo một tệp HTML kèm thư mục tài nguyên.
- **Có thể trích xuất phông chữ từ tài liệu Word không?** Sử dụng `EditableDocument.Fonts` để lấy tất cả các tài nguyên phông chữ.
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần một giấy phép GroupDocs.Editor hợp lệ; có sẵn bản dùng thử miễn phí.

## **extract images from docx** là gì?
Việc trích xuất hình ảnh từ tệp DOCX có nghĩa là lấy ra từng ảnh được nhúng trong tài liệu Word một cách lập trình để bạn có thể tái sử dụng, chỉnh sửa hoặc lưu trữ chúng riêng biệt. GroupDocs.Editor cung cấp bộ sưu tập `Images` trên một đối tượng `EditableDocument`, giúp công việc này trở nên đơn giản.

## Tại sao nên sử dụng GroupDocs.Editor cho quy trình này?
- **Kiểm soát toàn diện** các tài nguyên của tài liệu (hình ảnh, phông chữ, CSS) mà không cần xử lý ZIP thủ công.  
- **Chuyển đổi liền mạch** từ DOCX sang HTML đồng thời giữ nguyên bố cục và kiểu dáng.  
- **Dễ dàng trích xuất tài nguyên** cho việc xử lý hình ảnh tùy chỉnh, nhúng phông chữ hoặc phân phối qua CDN.  
- **Mẫu giải phóng tài nguyên mạnh mẽ** đảm bảo không có rò rỉ bộ nhớ trong các dịch vụ chạy lâu dài.

## Yêu cầu trước
- Visual Studio đã được cài đặt trên máy phát triển của bạn.  
- .NET Framework tương thích với GroupDocs.Editor.  
- Thư viện GroupDocs.Editor cho .NET. Bạn có thể [tải xuống tại đây](https://releases.groupdocs.com/editor/net/).  
- Giấy phép GroupDocs.Editor hợp lệ. Bạn có thể nhận [bản dùng thử miễn phí](https://releases.groupdocs.com/) hoặc mua [giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).

## Nhập các Namespace
Để bắt đầu, hãy chắc chắn rằng bạn đã nhập các namespace cần thiết trong dự án .NET của mình:

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

## Bước 1: Tạo một thể hiện EditableDocument
Đầu tiên, bạn cần tạo một thể hiện của `EditableDocument` bằng cách tải và chỉnh sửa một tài liệu đầu vào có định dạng được hỗ trợ.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

Trong bước này, chúng ta tải tài liệu đầu vào và chuẩn bị nó để chỉnh sửa.

## Cách **trích xuất hình ảnh từ DOCX**?
Dưới đây chúng ta sẽ khám phá khả năng trích xuất tài nguyên, bắt đầu với nhu cầu phổ biến nhất—lấy tất cả hình ảnh ra khỏi tệp Word.

## Bước 2: Trích xuất tài nguyên tài liệu
Đối tượng `EditableDocument` chứa nhiều tài nguyên có thể được trích xuất và thao tác. Hãy phân tích chúng:

### Bước 2.1: Trích xuất toàn bộ tài liệu dưới dạng HTML
Bạn có thể tạo một chuỗi duy nhất chứa toàn bộ tài liệu cùng với tất cả tài nguyên được nhúng dưới dạng HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

Chuỗi này sẽ khá lớn vì nó bao gồm các stylesheet, hình ảnh và phông chữ được mã hoá dưới dạng base64.

### Bước 2.2: Trích xuất tất cả hình ảnh *(từ khóa chính trong hành động)*
Trích xuất tất cả hình ảnh từ tài liệu—đây là cốt lõi của **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Bước 2.3: Trích xuất tất cả phông chữ *(từ khóa phụ)*
Nếu bạn cũng cần **trích xuất phông chữ từ word**, hãy sử dụng lệnh sau:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Bước 2.4: Trích xuất tất cả stylesheet
Trích xuất tất cả stylesheet ở dạng văn bản.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Bước 2.5: Thu thập tất cả tài nguyên
Thu thập tất cả tài nguyên trong một lần gọi.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Điều này bao gồm hình ảnh, phông chữ và stylesheet.

### Bước 2.6: Lấy mã HTML
Lấy mã HTML của tài liệu mà không có các tài nguyên được nhúng.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Cách **chuyển đổi docx sang html** với xử lý tùy chỉnh?
Đôi khi bạn cần điều chỉnh các liên kết bên ngoài để chúng trỏ tới trình xử lý tài nguyên của riêng bạn.

## Bước 3: Điều chỉnh liên kết bên ngoài
### Bước 3.1: Chuẩn bị tiền tố tùy chỉnh
Chuẩn bị các tiền tố sẽ được thêm vào trước các liên kết bên ngoài gốc.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Bước 3.2: Tạo mã HTML có tiền tố
Tạo mã HTML với các liên kết đã được điều chỉnh.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Bước 3.3: Lấy nội dung HTML chỉ phần body
Một số trình soạn thảo WYSIWYG chỉ xử lý mã HTML thuần mà không có phần header.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Bước 3.4: Nội dung chỉ body có tiền tố
Tạo nội dung chỉ phần body với các tiền tố hình ảnh tùy chỉnh.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Bước 3.5: Trích xuất stylesheet
Trích xuất stylesheet được sử dụng trong tài liệu.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Bước 3.6: Stylesheet có tiền tố
Trích xuất stylesheet với các tiền tố tùy chỉnh.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Cách **lưu tài liệu dưới dạng html** một cách chính xác?
## Bước 4: Lưu tài liệu dưới dạng HTML
Lưu tài liệu đã chỉnh sửa dưới dạng tệp HTML, kèm theo các tài nguyên của nó.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Phương thức này tạo một thư mục riêng cho các tài nguyên như stylesheet, hình ảnh và phông chữ.

## Bước 5: Giải phóng EditableDocument
`EditableDocument` triển khai `IDisposable` và cung cấp khả năng kiểm tra xem thể hiện đã được giải phóng hay chưa.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Bước 5.1 Xử lý sự kiện Dispose
Bạn cũng có thể đăng ký sự kiện disposing.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Bước 6: Tạo EditableDocument từ HTML
Tạo một thể hiện của `EditableDocument` từ một tài liệu HTML.

### Bước 6.1: Từ tệp HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Bước 6.2: Từ mã HTML

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Các thể hiện này (`afterEditFromFile` và `afterEditFromMarkup`) giống hệt với thể hiện gốc (`beforeEdit`).

## Bước 7: Giải phóng thủ công
Giải phóng thủ công các thể hiện `EditableDocument` của bạn.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Điều này đảm bảo việc dọn dẹp tài nguyên đúng cách.

## Các vấn đề thường gặp và giải pháp
- **Hình ảnh không hiển thị sau khi trích xuất:** Kiểm tra xem tài liệu có thực sự chứa hình ảnh nhúng không và bạn đang truy cập `beforeEdit.Images` sau khi gọi `Edit`.  
- **Phông chữ thiếu trong đầu ra HTML:** Đảm bảo bạn gọi `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` để nhúng đúng URL phông chữ.  
- **Chuỗi HTML lớn gây áp lực bộ nhớ:** Sử dụng `GetContent()` để lấy markup mà không có tài nguyên nhúng và phục vụ hình ảnh/CSS từ các tệp riêng.

## Câu hỏi thường gặp

**H: GroupDocs.Editor hỗ trợ những định dạng nào?**  
Đ: GroupDocs.Editor hỗ trợ DOCX, XLSX, PPTX và nhiều định dạng văn phòng phổ biến khác.

**H: Tôi có thể sử dụng GroupDocs.Editor mà không có giấy phép không?**  
Đ: Có, bạn có thể sử dụng nó với [bản dùng thử miễn phí](https://releases.groupdocs.com/) hoặc [giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).

**H: Làm sao tôi có thể trích xuất các tài nguyên cụ thể từ tài liệu?**  
Đ: Sử dụng các bộ sưu tập `Images`, `Fonts` và `Css` trên thể hiện `EditableDocument`.

**H: Có thể điều chỉnh các liên kết trong đầu ra HTML không?**  
Đ: Có, truyền các tiền tố URI tùy chỉnh vào `GetContent` hoặc `GetBodyContent` để viết lại các liên kết hình ảnh, CSS và phông chữ.

**H: Làm sao tôi lưu tài liệu đã chỉnh sửa dưới dạng tệp HTML?**  
Đ: Gọi phương thức `Save` trên thể hiện `EditableDocument`, cung cấp đường dẫn tệp kết thúc bằng `.html`.

---

**Cập nhật lần cuối:** 2026-03-14  
**Kiểm tra với:** GroupDocs.Editor cho .NET (phiên bản mới nhất)  
**Tác giả:** GroupDocs