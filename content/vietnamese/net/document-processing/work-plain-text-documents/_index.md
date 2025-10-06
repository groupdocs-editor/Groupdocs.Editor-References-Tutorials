---
title: Làm việc với tài liệu văn bản thuần túy
linktitle: Làm việc với tài liệu văn bản thuần túy
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách chỉnh sửa tài liệu văn bản thuần túy bằng GroupDocs.Editor dành cho .NET với hướng dẫn từng bước của chúng tôi. Đơn giản hóa quá trình chỉnh sửa tài liệu .NET của bạn.
weight: 15
url: /vi/net/document-processing/work-plain-text-documents/
type: docs
---
# Làm việc với tài liệu văn bản thuần túy

## Giới thiệu
Bạn đang tìm cách hợp lý hóa quy trình chỉnh sửa tài liệu của mình trong .NET? Không cần tìm đâu xa ngoài GroupDocs.Editor dành cho .NET! API mạnh mẽ này cho phép bạn chỉnh sửa nhiều định dạng tài liệu một cách dễ dàng. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình làm việc với các tài liệu văn bản thuần túy bằng GroupDocs.Editor cho .NET. Cuối cùng, bạn sẽ được trang bị để xử lý việc chỉnh sửa tài liệu văn bản như một người chuyên nghiệp. Sẵn sàng để đi sâu vào? Bắt đầu nào!
## Điều kiện tiên quyết
Trước khi chúng ta bắt đầu, có một số thứ bạn cần chuẩn bị sẵn:
- Môi trường phát triển .NET: Đảm bảo bạn đã thiết lập môi trường phát triển .NET đang hoạt động. Visual Studio là một lựa chọn phổ biến.
-  GroupDocs.Editor cho .NET: Tải xuống và cài đặt[GroupDocs.Editor cho .NET](https://releases.groupdocs.com/editor/net/).
- Kiến thức C# cơ bản: Làm quen với ngôn ngữ lập trình C# sẽ giúp bạn theo dõi các ví dụ.
- Trình soạn thảo văn bản: Bất kỳ trình soạn thảo văn bản nào cũng được, mặc dù Visual Studio Code được khuyên dùng vì các tính năng và tính dễ sử dụng của nó.
## Nhập không gian tên
Để bắt đầu sử dụng GroupDocs.Editor cho .NET, bạn cần nhập các vùng tên cần thiết vào dự án của mình. Điều này đảm bảo rằng tất cả các lớp và phương thức cần thiết đều có sẵn để sử dụng.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Hãy chia nhỏ quy trình thành các bước có thể quản lý được. Hãy làm theo khi chúng tôi hướng dẫn bạn qua từng giai đoạn chỉnh sửa tài liệu văn bản thuần túy bằng GroupDocs.Editor cho .NET.
## Bước 1: Nhận đường dẫn đến tệp TXT đầu vào
Trước tiên, bạn cần chỉ định đường dẫn đến tệp TXT đầu vào. Đây có thể là đường dẫn đến tệp cục bộ hoặc luồng chứa nội dung tệp.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Bước 2: Tạo một phiên bản soạn thảo
 Tiếp theo, tạo một thể hiện của`Editor` lớp học. Lớp này chịu trách nhiệm tải và chỉnh sửa tài liệu. Không có tùy chọn tải được yêu cầu ở giai đoạn này.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Bước 3: Tạo tùy chọn chỉnh sửa TXT
Bây giờ, tạo các tùy chọn chỉnh sửa TXT. Các tùy chọn này cho phép bạn chỉ định cách xử lý nội dung văn bản trong quá trình chỉnh sửa.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Bước 4: Tạo một phiên bản EditableDocument
 Với các tùy chọn chỉnh sửa đã được thiết lập, hãy tạo một`EditableDocument` ví dụ. Điều này thể hiện tài liệu ở định dạng có thể chỉnh sửa.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Bước 5: Chỉnh sửa nội dung tài liệu
Truy xuất nội dung văn bản gốc và thực hiện các chỉnh sửa mà bạn mong muốn. Trong ví dụ này, chúng tôi sẽ thay thế từ "văn bản" bằng "văn bản ĐÃ CHỈNH SỬA".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Bước 6: Tạo Tài liệu có thể chỉnh sửa với nội dung được cập nhật
 Sau khi thực hiện các chỉnh sửa cần thiết, hãy tạo một cái mới`EditableDocument` với nội dung cập nhật và các tài nguyên gốc.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Bước 7: Tạo tùy chọn lưu WordProcessing
Chuẩn bị các tùy chọn lưu cho định dạng WordProcessing. Ví dụ này sử dụng định dạng DOCM và chỉ định ngôn ngữ.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Bước 8: Tạo tùy chọn lưu TXT
Tương tự, tạo các tùy chọn lưu cho định dạng TXT. Đảm bảo mã hóa được đặt thành UTF-8 và giữ nguyên bố cục bảng.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Bước 9: Chuẩn bị đường dẫn đầu ra
Chuẩn bị đường dẫn để lưu tệp DOCX và TXT thu được. Sử dụng đường dẫn tệp đầu vào để xác định tên tệp và thư mục đầu ra.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Bước 10: Lưu tài liệu đã chỉnh sửa
Cuối cùng, lưu tài liệu đã chỉnh sửa ở cả định dạng DOCX và TXT bằng các tùy chọn lưu đã chỉ định.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Phần kết luận
 Chúc mừng! Bạn đã chỉnh sửa thành công tài liệu văn bản thuần túy bằng GroupDocs.Editor cho .NET. Công cụ mạnh mẽ này giúp đơn giản hóa việc chỉnh sửa tài liệu, giúp bạn dễ dàng tích hợp vào các ứng dụng .NET của mình. Cho dù bạn đang xử lý các tệp văn bản đơn giản hay các định dạng tài liệu phức tạp, GroupDocs.Editor đều có thể hỗ trợ bạn. Khám phá thêm các tính năng và khả năng bằng cách truy cập[Tài liệu GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Câu hỏi thường gặp
### GroupDocs.Editor cho .NET hỗ trợ những định dạng tệp nào?
 GroupDocs.Editor cho .NET hỗ trợ nhiều định dạng tệp, bao gồm DOCX, TXT, HTML, v.v. Kiểm tra[tài liệu](https://tutorials.groupdocs.com/editor/net/) để có danh sách đầy đủ.
### Làm cách nào tôi có thể dùng thử miễn phí GroupDocs.Editor cho .NET?
 Bạn có thể tải xuống bản dùng thử miễn phí GroupDocs.Editor cho .NET từ[trang phát hành](https://releases.groupdocs.com/).
### Tôi có thể mua giấy phép tạm thời cho GroupDocs.Editor cho .NET không?
Có, bạn có thể xin giấy phép tạm thời từ[Trang mua GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Tôi có thể nhận hỗ trợ cho GroupDocs.Editor cho .NET ở đâu?
 Hỗ trợ có sẵn thông qua[Diễn đàn hỗ trợ GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Có tài liệu chi tiết nào về GroupDocs.Editor cho .NET không?
 Có, tài liệu chi tiết có sẵn trên[Trang tài liệu GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).