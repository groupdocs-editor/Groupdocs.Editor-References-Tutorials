---
title: Làm việc với các giá trị được phân tách bằng dấu phân cách (DSV)
linktitle: Làm việc với các giá trị được phân tách bằng dấu phân cách (DSV)
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách chỉnh sửa tệp CSV và TSV bằng GroupDocs.Editor dành cho .NET với hướng dẫn từng bước này. Cải thiện các dự án .NET của bạn một cách dễ dàng.
weight: 12
url: /vi/net/document-processing/work-dsv/
type: docs
---
# Làm việc với các giá trị được phân tách bằng dấu phân cách (DSV)

## Giới thiệu
Nếu bạn là nhà phát triển làm việc với các giá trị được phân tách bằng dấu phân cách (DSV) như tệp CSV hoặc TSV thì bạn biết rằng việc chỉnh sửa các tệp này theo chương trình có thể là một nhiệm vụ khó khăn. Tuy nhiên, với GroupDocs.Editor cho .NET, tác vụ này trở nên đơn giản và hiệu quả hơn đáng kể. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn cách sử dụng GroupDocs.Editor cho .NET để đọc, chỉnh sửa và lưu tệp DSV. Chúng tôi sẽ chia quy trình thành các bước dễ thực hiện, giúp bạn dễ dàng triển khai trong các dự án của mình.
## Điều kiện tiên quyết
Trước khi chúng ta đi sâu vào hướng dẫn, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
- Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình.
-  GroupDocs.Editor cho .NET: Bạn sẽ cần tải xuống và tham khảo thư viện GroupDocs.Editor cho .NET. Bạn có thể tải nó xuống[đây](https://releases.groupdocs.com/editor/net/).
- Hiểu biết cơ bản về C#: Hướng dẫn này giả sử bạn có hiểu biết cơ bản về phát triển C# và .NET.
## Nhập không gian tên
Trước tiên, bạn cần nhập các không gian tên cần thiết trong dự án của mình. Các không gian tên này cung cấp các lớp và phương thức cần thiết để hoạt động với GroupDocs.Editor cho .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Bước 1: Nhận đường dẫn đến tệp DSV đầu vào
Trước tiên, bạn cần chỉ định đường dẫn đến tệp DSV đầu vào. Trong ví dụ này, chúng tôi giả định đó là tệp CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Bước 2: Tạo một phiên bản soạn thảo
 Tạo một thể hiện của`Editor` lớp học. Phiên bản này sẽ được sử dụng để tải và thao tác với tệp DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Bước 3: Tạo tùy chọn chỉnh sửa DSV
 Tiếp theo, tạo một thể hiện của`DelimitedTextEditOptions` và chỉ định dấu phân cách cho tệp DSV. Ở đây, chúng tôi sử dụng dấu phẩy làm dấu phân cách.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Bước 4: Tạo một phiên bản EditableDocument
 Tạo ra một`EditableDocument` ví dụ bằng cách sử dụng`Editor.Edit` phương pháp. Điều này chuẩn bị tài liệu để chỉnh sửa.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Bước 5: Chỉnh sửa nội dung tài liệu
Truy xuất nội dung văn bản gốc và thực hiện các sửa đổi cần thiết. Với mục đích trình diễn, hãy thay thế một số văn bản.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Bước 6: Tạo Tài liệu có thể chỉnh sửa với nội dung được cập nhật
 Tạo một cái mới`EditableDocument` với nội dung được cập nhật.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Bước 7: Tạo tùy chọn lưu CSV
Chỉ định các tùy chọn lưu cho định dạng CSV, bao gồm dấu phân cách và mã hóa.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Bước 8: Tạo tùy chọn lưu TSV
Tương tự, chỉ định các tùy chọn lưu cho định dạng TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Bước 9: Tạo tùy chọn lưu bảng tính
Nếu bạn cần lưu tài liệu dưới dạng bảng tính, hãy tạo các tùy chọn lưu tương ứng.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Bước 10: Chuẩn bị đường dẫn lưu
Xác định đường dẫn nơi các tập tin đã chỉnh sửa sẽ được lưu.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Bước 11: Lưu tài liệu đã chỉnh sửa
Lưu tài liệu đã chỉnh sửa vào các đường dẫn được chỉ định ở các định dạng khác nhau.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Bước 12: Loại bỏ các phiên bản Tài liệu có thể chỉnh sửa
 Cuối cùng, hãy đảm bảo vứt bỏ`EditableDocument` trường hợp để giải phóng tài nguyên.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Phần kết luận
Chỉnh sửa tệp DSV bằng GroupDocs.Editor cho .NET là một quá trình đơn giản bao gồm việc tạo phiên bản trình soạn thảo, đặt tùy chọn chỉnh sửa, sửa đổi nội dung và lưu các thay đổi. Hướng dẫn từng bước này sẽ giúp bạn tích hợp chức năng này vào các ứng dụng .NET của mình một cách dễ dàng. Cho dù bạn đang làm việc với các định dạng CSV, TSV hay DSV khác, GroupDocs.Editor dành cho .NET đều cung cấp giải pháp mạnh mẽ và linh hoạt.
## Câu hỏi thường gặp
### Tôi có thể sử dụng GroupDocs.Editor cho .NET để chỉnh sửa các tệp CSV lớn không?
Có, GroupDocs.Editor cho .NET có khả năng xử lý các tệp CSV lớn một cách hiệu quả.
### GroupDocs.Editor cho .NET có hỗ trợ các định dạng DSV khác ngoài CSV và TSV không?
Có, nó hỗ trợ nhiều định dạng DSV khác nhau miễn là bạn chỉ định dấu phân cách thích hợp.
### Có thể tùy chỉnh mã hóa khi lưu tệp DSV không?
Tuyệt đối, bạn có thể chỉ định mã hóa mong muốn trong tùy chọn lưu.
### Tôi có thể chuyển đổi tệp CSV thành bảng tính Excel bằng GroupDocs.Editor cho .NET không?
Có, bạn có thể lưu tệp CSV dưới dạng bảng tính Excel bằng cách sử dụng các tùy chọn lưu thích hợp.
### Tôi có thể tìm thêm tài liệu về GroupDocs.Editor cho .NET ở đâu?
 Bạn có thể tìm tài liệu chi tiết[đây](https://tutorials.groupdocs.com/editor/net/)