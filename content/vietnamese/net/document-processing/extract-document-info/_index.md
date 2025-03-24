---
title: Trích xuất thông tin tài liệu
linktitle: Trích xuất thông tin tài liệu
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách trích xuất thông tin tài liệu bằng GroupDocs.Editor cho .NET với hướng dẫn chi tiết từng bước của chúng tôi. Hoàn hảo để quản lý các loại tài liệu khác nhau.
weight: 10
url: /vi/net/document-processing/extract-document-info/
---
## Giới thiệu
Chào mừng bạn đến với hướng dẫn toàn diện về cách trích xuất thông tin tài liệu bằng GroupDocs.Editor cho .NET. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước thực hiện quy trình, đảm bảo bạn hiểu từng phần một cách rõ ràng và chính xác. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, hướng dẫn này sẽ giúp bạn tích hợp liền mạch GroupDocs.Editor vào các dự án .NET của mình để quản lý và thao tác tài liệu hiệu quả.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo bạn có mọi thứ bạn cần:
- Kiến thức cơ bản về C#: Hiểu những điều cơ bản về lập trình C# là điều cần thiết.
- Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio.
-  GroupDocs.Editor cho .NET: Bạn sẽ cần thư viện GroupDocs.Editor cho .NET. Bạn có thể tải nó xuống từ[trang tải xuống](https://releases.groupdocs.com/editor/net/).
## Nhập không gian tên
Để bắt đầu, bạn cần nhập các không gian tên cần thiết. Điều này cho phép bạn truy cập các lớp và phương thức cần thiết để thao tác với tài liệu.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Bước 1: Tải tài liệu của bạn
Trước tiên, bạn cần tải tài liệu mà bạn muốn trích xuất thông tin. Điều này có thể được thực hiện bằng cách cung cấp đường dẫn tệp tới tài liệu.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Bước 2: Truy xuất thông tin tài liệu
 Tiếp theo, bạn sẽ truy xuất thông tin tài liệu bằng cách sử dụng`GetDocumentInfo` phương pháp. Phương pháp này không yêu cầu bất kỳ tùy chọn tải cụ thể nào nếu bạn không chắc chắn về định dạng tài liệu.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Bước 3: Xác định loại tài liệu
Bây giờ, bạn cần kiểm tra loại tài liệu bạn đang xử lý. Điều này rất quan trọng vì nó quyết định cách bạn sẽ xử lý tài liệu.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Bước 4: Trích xuất thông tin chi tiết
Nếu tài liệu là tài liệu Xử lý văn bản, bạn có thể trích xuất thông tin chi tiết như định dạng, phần mở rộng, số trang, kích thước và liệu nó có được mã hóa hay không.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Bước 5: Lặp lại cho các loại tài liệu khác nhau
Lặp lại các bước tương tự cho các loại tài liệu khác như Bảng tính và tài liệu văn bản.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Bước 6: Xử lý tài liệu được bảo vệ bằng mật khẩu
Khi xử lý các tài liệu được bảo vệ bằng mật khẩu, trước tiên bạn nên thử mở chúng mà không cần mật khẩu, sau đó là mật khẩu không chính xác và cuối cùng là mật khẩu chính xác.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Bước 7: Xử lý tài liệu dựa trên văn bản
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Bước 8: Vứt bỏ tài nguyên
Cuối cùng, hãy đảm bảo bạn loại bỏ tất cả tài nguyên để tránh rò rỉ bộ nhớ.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Phần kết luận
Chúc mừng! Bây giờ bạn đã học cách trích xuất thông tin tài liệu bằng GroupDocs.Editor cho .NET. Thư viện mạnh mẽ này giúp đơn giản hóa việc quản lý và thao tác tài liệu, cho phép bạn xử lý nhiều loại tài liệu khác nhau một cách liền mạch. Cho dù bạn đang xử lý các tài liệu Xử lý văn bản, Bảng tính hay Văn bản, GroupDocs.Editor đều cung cấp một giải pháp mạnh mẽ.
## Câu hỏi thường gặp
### GroupDocs.Editor có thể xử lý những loại tài liệu nào?
GroupDocs.Editor có thể xử lý nhiều loại tài liệu khác nhau bao gồm Xử lý văn bản, Bảng tính và tài liệu dựa trên Văn bản.
### GroupDocs.Editor có thể quản lý các tài liệu được bảo vệ bằng mật khẩu không?
Có, GroupDocs.Editor có thể quản lý tài liệu được bảo vệ bằng mật khẩu. Nó có thể xác định và mở các tài liệu này nếu có mật khẩu chính xác.
### Có cần thiết phải loại bỏ các đối tượng Editor không?
Có, điều quan trọng là phải loại bỏ các đối tượng Editor để giải phóng tài nguyên và ngăn chặn rò rỉ bộ nhớ.
### Tôi có thể trích xuất thông tin chi tiết về định dạng và kích thước tài liệu không?
Tuyệt đối! GroupDocs.Editor cho phép bạn trích xuất thông tin chi tiết bao gồm định dạng, tiện ích mở rộng, kích thước, số lượng trang và trạng thái mã hóa.
### Tôi có thể nhận hỗ trợ ở đâu nếu gặp vấn đề?
 Bạn có thể nhận được sự hỗ trợ từ[Diễn đàn hỗ trợ GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).