---
title: Tạo tài liệu
linktitle: Tạo tài liệu
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách chỉnh sửa tài liệu Word, Excel, PowerPoint, Ebook và Email bằng GroupDocs.Editor cho .NET với hướng dẫn từng bước toàn diện này.
weight: 10
url: /vi/net/document-editing/create-document/
---
## Giới thiệu
Bạn có mệt mỏi với những rắc rối khi chỉnh sửa các loại tài liệu khác nhau theo chương trình không? GroupDocs.Editor dành cho .NET có mặt để đơn giản hóa quy trình. Công cụ mạnh mẽ này cho phép các nhà phát triển chỉnh sửa các định dạng tài liệu khác nhau như Word, Excel, PowerPoint, Ebooks và Email một cách dễ dàng. Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách sử dụng GroupDocs.Editor cho .NET để tạo và chỉnh sửa tài liệu. Chúng tôi sẽ chia quy trình thành các bước dễ thực hiện, giúp bạn có thể dễ dàng thực hiện quy trình này ngay cả khi bạn chưa quen với quy trình này.
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có những điều sau:
- Visual Studio được cài đặt trên máy của bạn.
- .NET Framework (4.0 trở lên).
-  GroupDocs.Editor cho thư viện .NET. Bạn có thể tải nó xuống từ[đây](https://releases.groupdocs.com/editor/net/).
- Kiến thức cơ bản về lập trình C#.
## Nhập không gian tên
Đầu tiên, hãy nhập các không gian tên cần thiết. Điều này sẽ làm cho các lớp và phương thức cần thiết có thể truy cập được trong ứng dụng của chúng ta.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Bước 1: Thiết lập luồng
Để bắt đầu, chúng ta cần thiết lập một luồng bộ nhớ sẽ đóng vai trò giữ chỗ cho nội dung tài liệu.
```csharp
Stream memoryStream = Stream.Null;
```
## Bước 2: Chức năng gọi lại để lưu tài liệu
Tiếp theo, xác định chức năng gọi lại sẽ lưu luồng tài liệu mới. Chức năng này rất cần thiết để xử lý đầu ra của quá trình chỉnh sửa tài liệu.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Bước 3: Tạo và chỉnh sửa tài liệu WordProcessing
 Bây giờ, hãy tạo và chỉnh sửa tài liệu Word. Chúng ta sẽ bắt đầu bằng cách tạo một cái mới`Editor` ví dụ cho các tài liệu WordProcessing và chỉnh sửa nó với các tùy chọn mặc định.
### Tạo và chỉnh sửa với các tùy chọn mặc định
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Tạo và chỉnh sửa với tùy chọn tùy chỉnh
Để kiểm soát nhiều hơn, chúng tôi có thể chỉ định các tùy chọn như tắt phân trang và trích xuất phông chữ được nhúng.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Bước 4: Tạo và chỉnh sửa tài liệu bảng tính
Tương tự, chúng ta có thể tạo và chỉnh sửa một tài liệu Excel. Đây là cách bạn làm điều đó.
### Tạo và chỉnh sửa với các tùy chọn mặc định
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Tạo và chỉnh sửa với tùy chọn tùy chỉnh
 Để nhắm mục tiêu các bảng tính cụ thể hoặc loại trừ các bảng tính bị ẩn, chúng tôi sử dụng`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Bước 5: Tạo và chỉnh sửa tài liệu thuyết trình
Bản trình bày PowerPoint cũng được hỗ trợ. Hãy xem cách xử lý chúng.
### Tạo và chỉnh sửa với các tùy chọn mặc định
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Tạo và chỉnh sửa với tùy chọn tùy chỉnh
Bạn có thể tùy chỉnh các chỉnh sửa của mình bằng cách chỉ định các tùy chọn như trang chiếu nào sẽ hiển thị và có bao gồm các trang trình bày ẩn hay không.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Bước 6: Tạo và chỉnh sửa tài liệu Ebook
GroupDocs.Editor cũng cho phép chỉnh sửa các định dạng Ebook như EPUB. Đây là cách bạn có thể xử lý nó.
### Tạo và chỉnh sửa với các tùy chọn mặc định
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Tạo và chỉnh sửa với tùy chọn tùy chỉnh
Tùy chỉnh chỉnh sửa Ebook của bạn bằng cách bật hoặc tắt thông tin phân trang và ngôn ngữ.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Bước 7: Tạo và chỉnh sửa tài liệu email
Cuối cùng, chúng ta sẽ xem cách chỉnh sửa tài liệu email. Điều này bao gồm các định dạng như EML.
### Tạo và chỉnh sửa với các tùy chọn mặc định
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Tạo và chỉnh sửa với tùy chọn tùy chỉnh
Chỉ định các tùy chọn đầu ra thư để kiểm soát quá trình chỉnh sửa.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Bước 8: Hoàn thiện quy trình
Sau khi chỉnh sửa tài liệu, điều quan trọng là phải xử lý luồng bộ nhớ đúng cách để giải phóng tài nguyên.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Phần kết luận
GroupDocs.Editor cho .NET là một công cụ linh hoạt và mạnh mẽ có thể đơn giản hóa tác vụ chỉnh sửa các loại tài liệu khác nhau theo chương trình. Bằng cách làm theo hướng dẫn từng bước này, bạn có thể tạo và chỉnh sửa tài liệu một cách dễ dàng, cho dù đó là tệp WordProcessing, bảng tính, bản trình bày, sách điện tử hay email. Đi sâu vào tài liệu GroupDocs.Editor để biết thêm các tính năng nâng cao và tùy chọn tùy chỉnh.
## Câu hỏi thường gặp
### Tôi có thể chỉnh sửa những loại tài liệu nào bằng GroupDocs.Editor cho .NET?
Bạn có thể chỉnh sửa nhiều loại tài liệu, bao gồm WordProcessing, bảng tính, bản trình bày, sách điện tử và email.
### Có thể tùy chỉnh các tùy chọn chỉnh sửa?
Có, GroupDocs.Editor dành cho .NET cho phép tùy chỉnh rộng rãi thông qua nhiều tùy chọn chỉnh sửa khác nhau dành riêng cho từng loại tài liệu.
### Làm cách nào để xử lý đầu ra của tài liệu đã chỉnh sửa?
Bạn có thể sử dụng chức năng gọi lại để lưu luồng tài liệu đã chỉnh sửa vào vị trí mong muốn.
### Tôi có cần giấy phép để sử dụng GroupDocs.Editor cho .NET không?
 Có, bạn có thể lấy giấy phép từ[đây](https://purchase.groupdocs.com/buy). Ngoài ra còn có một tùy chọn cho giấy phép tạm thời.
### Tôi có thể tìm tài liệu chi tiết hơn ở đâu?
 Tài liệu chi tiết có sẵn trên[GroupDocs.Editor cho trang tài liệu .NET](https://tutorials.groupdocs.com/editor/net/).