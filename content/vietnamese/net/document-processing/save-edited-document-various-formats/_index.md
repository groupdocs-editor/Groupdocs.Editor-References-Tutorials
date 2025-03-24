---
title: Lưu tài liệu đã chỉnh sửa sang các định dạng khác nhau
linktitle: Lưu tài liệu đã chỉnh sửa sang các định dạng khác nhau
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách lưu tài liệu đã chỉnh sửa sang nhiều định dạng khác nhau bằng GroupDocs.Editor cho .NET trong hướng dẫn từng bước toàn diện này.
weight: 11
url: /vi/net/document-processing/save-edited-document-various-formats/
---

# Lưu tài liệu đã chỉnh sửa sang các định dạng khác nhau

## Giới thiệu
Bạn đang muốn lưu tài liệu đã chỉnh sửa sang nhiều định dạng khác nhau bằng GroupDocs.Editor cho .NET? Bạn đã đến đúng nơi! Hướng dẫn toàn diện này sẽ hướng dẫn bạn toàn bộ quá trình, từ thiết lập môi trường đến lưu tài liệu đã chỉnh sửa của bạn ở nhiều định dạng. Hãy cùng bắt tay vào thực hiện việc chỉnh sửa và lưu tài liệu một cách dễ dàng!
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có những điều sau:
1.  GroupDocs.Editor cho .NET - Tải xuống phiên bản mới nhất từ[đây](https://releases.groupdocs.com/editor/net/).
2. Môi trường phát triển - Visual Studio hoặc bất kỳ IDE tương thích .NET nào khác.
3. .NET Framework - Đảm bảo bạn đã cài đặt .NET Framework 4.6.1 trở lên.
4. Tài liệu mẫu - Một tài liệu xử lý Word mẫu để làm việc.
5. Kiến thức C# cơ bản - Yêu cầu làm quen với lập trình C#.
## Nhập không gian tên
Để bắt đầu, hãy đảm bảo bạn nhập các vùng tên cần thiết vào dự án C# của mình. Điều này rất quan trọng để truy cập chức năng GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Hãy chia nhỏ quy trình thành các bước có thể quản lý được. Hãy theo dõi cẩn thận để đảm bảo bạn hiểu rõ từng phần.
## Bước 1: Nhận đường dẫn đến tệp đầu vào
Trước tiên, bạn cần chỉ định đường dẫn đến tệp WordProcessing đầu vào của mình. Tập tin này sẽ được tải và chỉnh sửa.
```csharp
string inputFilePath = "Your Sample Document";
```
## Bước 2: Tạo tùy chọn tải cho tài liệu
Tiếp theo, tạo các tùy chọn tải dành riêng cho tài liệu WordProcessing. Các tùy chọn này sẽ giúp tùy chỉnh cách tải tài liệu.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Bước 3: Tải tài liệu với các tùy chọn
 Bây giờ, tải tài liệu vào một`Editor` instance bằng cách sử dụng các tùy chọn tải được chỉ định.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Bước 4: Tạo tùy chọn chỉnh sửa
Chuẩn bị các tùy chọn chỉnh sửa cho tài liệu. Các tùy chọn này sẽ xác định cách mở tài liệu để chỉnh sửa.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Bước 5: Mở tài liệu để chỉnh sửa
 Mở tài liệu để chỉnh sửa bằng cách tạo một`EditableDocument`ví dụ. Trường hợp này sẽ cho phép bạn thực hiện các thay đổi đối với tài liệu.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Bước 6: Chỉnh sửa nội dung tài liệu
Bây giờ là lúc chỉnh sửa nội dung của tài liệu. Đầu tiên, lấy tài liệu dưới dạng một chuỗi được mã hóa base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Ví dụ: hãy sửa đổi phụ đề trong tài liệu.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Bước 7: Tạo tài liệu có thể chỉnh sửa mới từ nội dung đã chỉnh sửa
 Tạo một cái mới`EditableDocument` ví dụ từ nội dung và tài nguyên đã chỉnh sửa.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Bước 8: Lưu tài liệu sang nhiều định dạng khác nhau
Cuối cùng, lặp lại tất cả các định dạng WordProcessing có thể hỗ trợ và lưu tài liệu đã chỉnh sửa ở từng định dạng.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Chuẩn bị các tùy chọn lưu
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Chuẩn bị đường dẫn lưu
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Lưu tài liệu
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Thông báo hoàn thành
Để kết luận, bạn có thể in một thông báo cho biết quá trình đã kết thúc thành công.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Phần kết luận
Chúc mừng! Bạn đã học thành công cách lưu tài liệu đã chỉnh sửa sang nhiều định dạng khác nhau bằng GroupDocs.Editor cho .NET. Công cụ mạnh mẽ này giúp bạn dễ dàng thao tác và lưu tài liệu ở nhiều định dạng chỉ với một vài dòng mã. Hãy nhớ rằng các bước chính liên quan đến việc tải tài liệu, chỉnh sửa nội dung và lưu nó ở các định dạng mong muốn.
## Câu hỏi thường gặp
### GroupDocs.Editor dành cho .NET là gì?
GroupDocs.Editor cho .NET là một API mạnh mẽ cho phép bạn chỉnh sửa tài liệu ở nhiều định dạng khác nhau bằng ứng dụng .NET.
### Tôi có thể sử dụng GroupDocs.Editor miễn phí không?
 Có, bạn có thể sử dụng nó với bản dùng thử miễn phí. Tải xuống[đây](https://releases.groupdocs.com/).
### GroupDocs.Editor hỗ trợ những định dạng nào?
GroupDocs.Editor hỗ trợ nhiều định dạng, bao gồm DOCX, PDF, HTML, v.v.
### Làm cách nào để có được giấy phép tạm thời cho GroupDocs.Editor?
 Bạn có thể có được giấy phép tạm thời[đây](https://purchase.groupdocs.com/temporary-license/).
### Tôi có thể tìm thêm tài liệu và hỗ trợ ở đâu?
 Tài liệu chi tiết có sẵn[đây](https://tutorials.groupdocs.com/editor/net/) , và bạn có thể nhận được hỗ trợ[đây](https://forum.groupdocs.com/c/editor/20).