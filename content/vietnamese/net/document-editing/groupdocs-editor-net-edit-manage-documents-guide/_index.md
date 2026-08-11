---
date: '2026-04-11'
description: Tìm hiểu cách tạo tài liệu có thể chỉnh sửa bằng GroupDocs.Editor cho
  .NET và lưu tài liệu dưới dạng HTML một cách hiệu quả.
keywords:
- create editable document
- extract images from document
- save document as html
title: Tạo tài liệu có thể chỉnh sửa bằng GroupDocs.Editor .NET
type: docs
url: /vi/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# Tạo tài liệu có thể chỉnh sửa với GroupDocs.Editor .NET

Trong thời đại kỹ thuật số ngày nay, **tạo tài liệu có thể chỉnh sửa** là một yêu cầu cốt lõi cho bất kỳ quy trình làm việc hiện đại nào. Cho dù bạn đang xây dựng một trình soạn thảo cộng tác, một hệ thống quản lý nội dung, hoặc một công cụ báo cáo tự động, khả năng chỉnh sửa và lưu các tệp HTML một cách lập trình có thể tiết kiệm vô số giờ. Hướng dẫn này cho bạn biết cách **tạo tài liệu có thể chỉnh sửa** các thể hiện, trích xuất tài nguyên, và **lưu tài liệu dưới dạng HTML** bằng cách sử dụng GroupDocs.Editor cho .NET.

## Câu trả lời nhanh
- **“create editable document” có nghĩa là gì?** Nó có nghĩa là tải một tệp nguồn vào đối tượng `EditableDocument` của GroupDocs.Editor mà bạn có thể chỉnh sửa bằng chương trình.  
- **Các định dạng nào tôi có thể chuyển đổi sang HTML?** Word, Excel, PowerPoint và nhiều định dạng Office khác được hỗ trợ.  
- **Làm thế nào để trích xuất hình ảnh từ tài liệu?** Sử dụng bộ sưu tập `EditableDocument.Images`.  
- **Tôi có thể tạo một chuỗi HTML duy nhất với tất cả tài nguyên được nhúng không?** Có—gọi `GetEmbeddedHtml()`.  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Bản dùng thử hoạt động cho việc đánh giá; giấy phép vĩnh viễn là bắt buộc cho việc sử dụng thương mại.

## “create editable document” là gì?
Tạo một tài liệu có thể chỉnh sửa có nghĩa là tải một tệp nguồn (ví dụ, một tệp .docx) vào GroupDocs.Editor, mà trả về một đối tượng `EditableDocument`. Đối tượng này cung cấp mã HTML của tài liệu, hình ảnh, phông chữ và CSS, cho phép bạn chỉnh sửa nội dung, thay thế tài nguyên, hoặc nhúng toàn bộ vào một trang web.

## Tại sao nên sử dụng GroupDocs.Editor .NET cho nhiệm vụ này?
- **API đầy đủ tính năng** – Xử lý Word, Excel, PowerPoint và hơn nữa.  
- **Trích xuất tài nguyên** – Lấy ra hình ảnh, phông chữ và bảng kiểu với các thuộc tính đơn giản.  
- **Tạo HTML nhúng** – Tạo một chuỗi HTML duy nhất chứa tất cả tài nguyên, hoàn hảo cho email hoặc ứng dụng một trang.  
- **Tập trung vào hiệu năng** – Giải phóng đối tượng kịp thời và sử dụng các mẫu bất đồng bộ khi cần.

## Yêu cầu trước
- **Môi trường .NET**: Thiết lập môi trường phát triển cho các ứng dụng .NET.
- **Thư viện & Phụ thuộc**:
  - Install GroupDocs.Editor using one of these methods:
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI**: Tìm kiếm và cài đặt phiên bản mới nhất.
- **Yêu cầu kiến thức**: Nên có kiến thức về lập trình C# và các khái niệm cơ bản về xử lý tài liệu.

## Cài đặt GroupDocs.Editor cho .NET
### Hướng dẫn cài đặt
To start, set up GroupDocs.Editor in your project:
1. **Cài đặt qua .NET CLI**:
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Sử dụng Package Manager**:
   - Open the Package Manager Console and run:
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI**: 
   - Navigate to NuGet, search for "GroupDocs.Editor", and install.

### Nhận giấy phép
- **Bản dùng thử & Giấy phép tạm thời**:
  Bắt đầu với bản dùng thử miễn phí bằng cách tải xuống từ [GroupDocs releases](https://releases.groupdocs.com/editor/net/). Để thử nghiệm kéo dài, hãy đăng ký giấy phép tạm thời tại [trang mua hàng](https://purchase.groupdocs.com/temporary-license).

### Khởi tạo và Cấu hình Cơ bản
Dưới đây là cách khởi tạo GroupDocs.Editor trong ứng dụng của bạn:
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## Cách tạo tài liệu có thể chỉnh sửa với GroupDocs.Editor .NET
### Tạo một thể hiện EditableDocument
**Tổng quan**: Tải và chỉnh sửa tài liệu bằng cách tạo một thể hiện `EditableDocument`.

#### Tải tài liệu
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## Cách tạo HTML nhúng
### Tạo HTML nhúng từ EditableDocument
**Tổng quan**: Chuyển đổi toàn bộ tài liệu thành một chuỗi HTML nhúng duy nhất có kèm stylesheet và tài nguyên.
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## Cách trích xuất hình ảnh từ tài liệu
### Trích xuất tài nguyên từ EditableDocument
**Tổng quan**: Lấy hình ảnh, phông chữ, CSS và các tài nguyên khác từ tài liệu của bạn.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Cách trích xuất phông chữ từ tài liệu
*Khối mã cùng trên cũng cho thấy cách lấy tài nguyên phông chữ qua `beforeEdit.Fonts`.*

## Cách lấy nội dung HTML thuần
### Lấy nội dung HTML từ EditableDocument
**Tổng quan**: Trích xuất nội dung HTML thuần mà không có tài nguyên nhúng.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Cách điều chỉnh liên kết bên ngoài trong nội dung HTML
### Điều chỉnh liên kết bên ngoài trong nội dung HTML
**Tổng quan**: Sửa đổi các liên kết bên ngoài cho hình ảnh, CSS và phông chữ bằng cách sử dụng tiền tố tùy chỉnh.
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## Cách lưu tài liệu dưới dạng html
### Lưu EditableDocument dưới dạng tệp HTML
**Tổng quan**: Lưu tài liệu đã chỉnh sửa trở lại đĩa ở định dạng HTML.
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## Giải phóng và Xử lý Sự kiện cho EditableDocument
**Tổng quan**: Quản lý việc giải phóng tài nguyên và xử lý các sự kiện liên quan đến vòng đời tài liệu.
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## Cách tạo tài liệu có thể chỉnh sửa từ nội dung HTML
### Tạo EditableDocument từ nội dung HTML
**Tổng quan**: Tái tạo một thể hiện `EditableDocument` từ nội dung HTML hiện có.
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## Ứng dụng thực tiễn
GroupDocs.Editor .NET có thể được tận dụng trong nhiều kịch bản thực tế:
- **Chỉnh sửa cộng tác**: Tạo điều kiện cho việc chỉnh sửa tài liệu liền mạch bởi nhiều người dùng.  
- **Xuất bản web**: Chuyển đổi tài liệu sang định dạng thân thiện với web để xem và tương tác trực tuyến.  
- **Hệ thống quản lý nội dung**: Tích hợp với các nền tảng CMS để cho phép cập nhật nội dung động.  
- **Tự động tạo báo cáo**: Tự động tạo và định dạng báo cáo từ nhiều nguồn dữ liệu khác nhau.

## Các yếu tố về hiệu năng
- Quản lý bộ nhớ hiệu quả bằng cách giải phóng đối tượng kịp thời sau khi sử dụng.  
- Giảm thời gian tải tài nguyên bằng cách tối ưu hóa đường dẫn tệp và URL.  
- Sử dụng xử lý bất đồng bộ khi có thể để cải thiện độ phản hồi của ứng dụng.

## Các vấn đề thường gặp và giải pháp
- **Các tệp lớn gây tiêu thụ bộ nhớ cao** – Giải phóng các đối tượng `EditableDocument` ngay khi bạn hoàn thành việc xử lý chúng.  
- **Liên kết hình ảnh bị hỏng sau khi chuyển đổi** – Đảm bảo bạn sử dụng đúng URI của bộ xử lý tài nguyên khi gọi `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)`.  
- **Phông chữ thiếu trong HTML được tạo** – Kiểm tra xem tài liệu nguồn có nhúng các phông chữ cần thiết hay chúng có sẵn trên máy chủ.

## Câu hỏi thường gặp
**Q: GroupDocs.Editor .NET có tương thích với tất cả các định dạng tài liệu không?**  
A: GroupDocs.Editor hỗ trợ một loạt các định dạng, bao gồm Word, Excel, PowerPoint và nhiều định dạng khác, mang lại sự linh hoạt cho các trường hợp sử dụng khác nhau.

**Q: Làm thế nào để xử lý các tệp lớn một cách hiệu quả bằng GroupDocs.Editor?**  
A: Sử dụng các API bất đồng bộ khi có, xử lý tệp theo từng phần khi có thể, và luôn giải phóng kịp thời các đối tượng `EditableDocument` và `Editor` để giải phóng bộ nhớ.

**Q: Tôi có thể tích hợp GroupDocs.Editor với các giải pháp lưu trữ đám mây không?**  
A: Có, bạn có thể kết nối tới Azure Blob Storage, Amazon S3, Google Cloud Storage, hoặc bất kỳ nhà cung cấp đám mây nào khác bằng cách truyền luồng tệp vào hàm khởi tạo `Editor`.

**Q: Các tùy chọn giấy phép cho GroupDocs.Editor là gì?**  
A: Bạn có thể bắt đầu với bản dùng thử miễn phí hoặc đăng ký giấy phép tạm thời để đánh giá. Việc triển khai trong môi trường sản xuất yêu cầu giấy phép trả phí.

**Q: Tôi có thể nhận hỗ trợ ở đâu nếu gặp vấn đề?**  
A: [Diễn đàn Hỗ trợ GroupDocs](https://forum.groupdocs.com) có sẵn để giúp đỡ, và bạn cũng có thể liên hệ trực tiếp với đội ngũ hỗ trợ của GroupDocs.

---

**Cập nhật lần cuối:** 2026-04-11  
**Được kiểm thử với:** GroupDocs.Editor 23.12 for .NET  
**Tác giả:** GroupDocs