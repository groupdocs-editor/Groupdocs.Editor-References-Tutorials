---
date: 2026-06-01
description: Tìm hiểu cách lấy số trang và trích xuất siêu dữ liệu tài liệu bằng GroupDocs.Editor
  cho .NET trong một hướng dẫn chi tiết từng bước.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Lấy số trang và Trích xuất thông tin tài liệu
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Lấy số trang và Trích xuất thông tin tài liệu với GroupDocs.Editor
type: docs
url: /vi/net/document-processing/extract-document-info/
weight: 10
---

# Lấy Số Trang & Trích Xuất Thông Tin Tài Liệu với GroupDocs.Editor

## Giới thiệu
Trong hướng dẫn toàn diện này, bạn sẽ học cách **lấy số trang** và trích xuất thông tin chi tiết của tài liệu — bao gồm định dạng, kích thước và trạng thái mã hoá — bằng cách sử dụng GroupDocs.Editor cho .NET. Dù bạn đang xây dựng hệ thống quản lý tài liệu, công cụ báo cáo, hay quy trình chuyển đổi tự động, việc hiểu siêu dữ liệu của tệp là bước đầu tiên để xử lý đáng tin cậy. Hãy cùng đi qua toàn bộ quy trình, từ việc tải tệp đến việc giải phóng tài nguyên một cách an toàn.

## Câu trả lời nhanh
- **Làm thế nào để tôi lấy số trang của một tài liệu?**  
  Gọi `editor.GetDocumentInfo().PageCount` sau khi tải tệp bằng `Editor`.
- **Các định dạng tệp nào được hỗ trợ để trích xuất siêu dữ liệu?**  
  Hơn 50 định dạng, bao gồm DOCX, XLSX, PPTX, PDF, TXT và HTML.
- **Tôi có thể trích xuất siêu dữ liệu từ các tệp được bảo vệ bằng mật khẩu không?**  
  Có — cung cấp mật khẩu khi khởi tạo đối tượng `Editor`.
- **Tôi có cần giải phóng tài nguyên một cách thủ công không?**  
  Chắc chắn; luôn gọi `editor.Dispose()` hoặc bọc editor trong khối `using`.
- **Phiên bản GroupDocs.Editor nào được yêu cầu?**  
  Bản phát hành ổn định mới nhất (v23.12+ tại thời điểm viết) hỗ trợ tất cả các tính năng được trình bày.

## “Lấy số trang” trong GroupDocs.Editor là gì?
`GetDocumentInfo()` là một phương thức trả về đối tượng `DocumentInfo` chứa số trang, định dạng, kích thước và các siêu dữ liệu khác của tài liệu. Lệnh gọi duy nhất này cung cấp cho bạn thông tin ngay lập tức mà không cần phải phân tích tệp thủ công. Bằng cách sử dụng phương thức này, bạn tránh việc tải toàn bộ tài liệu vào bộ nhớ, giúp cải thiện hiệu năng đặc biệt với các tệp lớn và giảm tiêu thụ tài nguyên máy chủ.

## Tại sao phải trích xuất siêu dữ liệu tài liệu với GroupDocs.Editor?
GroupDocs.Editor có thể xử lý **hơn 50 định dạng đầu vào và đầu ra** và truy xuất siêu dữ liệu cho các tệp lên tới **2 GB** mà không cần tải toàn bộ tài liệu vào bộ nhớ. Hiệu suất này giảm tải máy chủ lên tới **70 %** so với việc phân tích toàn bộ tài liệu, rất phù hợp cho các ứng dụng có lưu lượng cao.

## Yêu cầu trước
- **C# development basics** – bạn nên quen thuộc với Visual Studio và cấu trúc dự án .NET.
- **Visual Studio 2022** (hoặc bất kỳ phiên bản mới nào) đã được cài đặt trên máy của bạn.
- **GroupDocs.Editor for .NET** – tải gói mới nhất từ [download page](https://releases.groupdocs.com/editor/net/).

## Cách tải tài liệu của bạn?
`Editor` là lớp chính đại diện cho một tài liệu và cung cấp các phương thức để tải và thao tác với nó. Tải tệp mục tiêu bằng cách tạo một thể hiện `Editor` và truyền đường dẫn tệp. Trình biên tập tự động phát hiện định dạng, vì vậy bạn không cần chỉ định tùy chọn tải. Cách tiếp cận này hoạt động với bất kỳ loại tệp được hỗ trợ nào và đơn giản hoá việc thiết lập ban đầu.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## Cách lấy thông tin tài liệu?
`GetDocumentInfo()` trả về một đối tượng `DocumentInfo` chứa siêu dữ liệu như số trang, định dạng, kích thước và trạng thái mã hoá. Sau khi tải, gọi phương thức này để lấy đối tượng. `DocumentInfo` trả về cho bạn một bức tranh ngắn gọn về đặc điểm của tệp, cho phép bạn đưa ra quyết định mà không cần xử lý thêm.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## Cách xác định loại tài liệu?
`DocumentType` là một enum cho biết tài liệu là WordProcessing, Spreadsheet, hay Text. Biết được loại tài liệu (Word, bảng tính hay văn bản thuần) ảnh hưởng đến cách bạn xử lý sau này. Sử dụng thuộc tính `DocumentType` của đối tượng `DocumentInfo` để đưa ra quyết định và phân nhánh logic tương ứng.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## Cách trích xuất thông tin chi tiết cho các tệp xử lý văn bản?
`WordProcessing` đề cập đến các tài liệu như DOCX, ODT và RTF được xử lý như tệp xử lý văn bản. Nếu loại tài liệu là `WordProcessing`, bạn có thể đọc các thuộc tính bổ sung như **format**, **extension**, **page count**, **size**, và **encryption flag** trực tiếp từ đối tượng `DocumentInfo`. Những chi tiết này giúp bạn tùy chỉnh các bước xử lý, chẳng hạn áp dụng các chuyển đổi hoặc kiểm tra bảo mật cụ thể.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## Cách xử lý tài liệu bảng tính và tài liệu văn bản?
`Spreadsheet` chỉ các tệp bảng tính như XLSX, trong khi `Text` đại diện cho các tài liệu văn bản thuần. Đối với bảng tính (`Spreadsheet`) và tệp văn bản (`Text`), đối tượng `DocumentInfo` vẫn cung cấp siêu dữ liệu cốt lõi (extension, size, page count). Một số định dạng có thể không cung cấp số trang, trong trường hợp này giá trị sẽ là `0`. Bạn vẫn có thể dựa vào các siêu dữ liệu khác cho logic downstream.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## Cách làm việc với tài liệu được bảo vệ bằng mật khẩu?
`Password` là một chuỗi được truyền vào hàm khởi tạo `Editor` để mở các tệp được mã hoá. Khi tài liệu được mã hoá, trước tiên cố gắng mở mà không có mật khẩu. Nếu thất bại, bắt ngoại lệ, sau đó thử lại với mật khẩu đúng. Hàm khởi tạo `Editor` chấp nhận tham số `Password` cho mục đích này, cho phép xử lý liền mạch các tệp được bảo vệ.

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

## Cách xử lý tài liệu dựa trên văn bản?
`DocumentInfo` cung cấp siêu dữ liệu cơ bản như kích thước, phần mở rộng và mã hoá cho các tệp văn bản. Các tệp văn bản (ví dụ: `.txt`, `.md`) được xử lý như các luồng đơn giản. Bạn vẫn có thể lấy thông tin kích thước và mã hoá từ `DocumentInfo`, hữu ích cho việc xác thực tính toàn vẹn của tệp hoặc xác định quy trình xử lý phù hợp.

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

## Cách giải phóng tài nguyên đúng cách?
`Editor` là lớp chính giữ các tài nguyên không quản lý và phải được giải phóng sau khi sử dụng. Để tránh rò rỉ bộ nhớ, luôn giải phóng thể hiện `Editor` sau khi bạn hoàn thành việc trích xuất thông tin. Câu lệnh `using` là mẫu an toàn nhất vì nó đảm bảo giải phóng ngay cả khi có ngoại lệ, giúp quản lý tài nguyên sạch sẽ.

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

## Các vấn đề thường gặp và giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| **PageCount returns 0** | Định dạng không hỗ trợ phân trang (ví dụ: văn bản thuần). | Kiểm tra `DocumentInfo.DocumentType` trước khi dựa vào `PageCount`. |
| **Unsupported file format** | Phần mở rộng tệp không được nhận dạng. | Xác minh tệp thuộc một trong hơn 50 định dạng được hỗ trợ; cập nhật GroupDocs.Editor lên phiên bản mới nhất. |
| **Password exception** | Mật khẩu cung cấp không đúng. | Bắt `PasswordProtectedException` và yêu cầu người dùng nhập lại mật khẩu. |
| **Memory spike on large files** | Tải các PDF rất lớn mà không sử dụng streaming. | Sử dụng `LoadOptions` với `LoadOptions.LoadMode = LoadMode.Stream` (có sẵn trong các phiên bản mới hơn). |

## Câu hỏi thường gặp

**Q: Tôi có thể trích xuất siêu dữ liệu từ những loại tài liệu nào?**  
A: GroupDocs.Editor hỗ trợ các tệp xử lý văn bản, bảng tính, trình chiếu, PDF và văn bản thuần—hơn 50 định dạng tổng cộng.

**Q: Làm thế nào để tôi lấy phần mở rộng của tệp?**  
A: Truy cập `DocumentInfo.Extension` sau khi gọi `GetDocumentInfo()`; nó trả về phần mở rộng mà không có dấu chấm đầu.

**Q: Tôi có thể lấy kích thước của tài liệu tính bằng megabyte không?**  
A: Có — `DocumentInfo.Size` trả về kích thước tính bằng byte; chia cho 1,048,576 để chuyển sang megabyte.

**Q: Có an toàn khi xử lý các tệp được bảo vệ bằng mật khẩu trên máy chủ không?**  
A: Chắc chắn — GroupDocs.Editor không bao giờ ghi mật khẩu ra đĩa và giải phóng mọi đối tượng mật mã sau khi sử dụng.

**Q: Tôi có thể tìm trợ giúp bổ sung ở đâu nếu gặp vấn đề?**  
A: Bạn có thể nhận hỗ trợ từ [diễn đàn hỗ trợ GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Cập nhật lần cuối:** 2026-06-01  
**Đã kiểm tra với:** GroupDocs.Editor 23.12 for .NET  
**Tác giả:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Hướng dẫn liên quan

- [Hướng dẫn toàn diện về Trích xuất Siêu dữ liệu trong .NET với GroupDocs.Editor: Một Hướng dẫn Chi tiết](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Hướng dẫn tải tài liệu với GroupDocs.Editor cho .NET](/editor/net/document-loading/)
- [Chỉnh sửa tài liệu hiệu quả với GroupDocs.Editor .NET: Chuyển đổi HTML thành tài liệu có thể chỉnh sửa](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)