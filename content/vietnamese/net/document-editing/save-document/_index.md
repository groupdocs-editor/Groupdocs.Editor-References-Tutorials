---
title: Lưu tài liệu
linktitle: Lưu tài liệu
second_title: API GroupDocs.Editor .NET
description: Chỉnh sửa và lưu tài liệu dễ dàng bằng GroupDocs.Editor cho .NET. Hướng dẫn từng bước này giúp đơn giản hóa quy trình cho các nhà phát triển.
type: docs
weight: 14
url: /vi/net/document-editing/save-document/
---
## Giới thiệu
Bạn đang muốn chỉnh sửa và lưu tài liệu một cách dễ dàng bằng GroupDocs.Editor cho .NET? Bạn đang ở đúng nơi! Hướng dẫn này sẽ hướng dẫn bạn thực hiện quy trình theo từng bước, đảm bảo bạn có thể dễ dàng quản lý tài liệu của mình. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay người mới bắt đầu, hướng dẫn của chúng tôi sẽ cung cấp cho bạn tất cả thông tin bạn cần để bắt đầu.
## Điều kiện tiên quyết
Trước khi đi sâu vào hướng dẫn, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:
- Môi trường phát triển: Visual Studio được cài đặt trên máy của bạn.
- .NET Framework: Đảm bảo bạn có .NET Framework 4.6.1 trở lên.
-  GroupDocs.Editor for .NET: Tải phiên bản mới nhất[đây](https://releases.groupdocs.com/editor/net/).
- Kiến thức C# cơ bản: Cần phải làm quen với lập trình C#.
## Nhập không gian tên
Để sử dụng GroupDocs.Editor trong dự án .NET của bạn, bạn cần nhập các vùng tên cần thiết. Đây là cách bạn làm điều đó:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Bây giờ chúng ta đã thiết lập môi trường và nhập các không gian tên cần thiết, hãy đi sâu vào các bước cần thiết để tải, chỉnh sửa và lưu tài liệu bằng GroupDocs.Editor cho .NET.
## Bước 1: Tải tài liệu
Đầu tiên, chúng ta cần tải tài liệu mà chúng ta muốn chỉnh sửa. GroupDocs.Editor làm cho quá trình này trở nên đơn giản. Đây là cách bạn có thể làm điều đó:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Trong bước này, chúng tôi chỉ định đường dẫn đến tài liệu mà chúng tôi muốn chỉnh sửa và tạo một phiên bản của`Editor` lớp học. Các`Edit` phương thức sau đó được gọi để tải tài liệu vào một`EditableDocument` sự vật.
## Bước 2: Sửa đổi tài liệu
Khi tài liệu đã được tải, đã đến lúc thực hiện một số sửa đổi. Vì chúng tôi không đính kèm trình soạn thảo WYSIWYG nên chúng tôi sẽ mô phỏng quá trình chỉnh sửa bằng mã.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Ở đây, chúng tôi truy xuất nội dung HTML được nhúng của tài liệu, thực hiện thay thế văn bản đơn giản và tạo một văn bản mới`EditableDocument`ví dụ từ HTML đã sửa đổi.
## Bước 3: Lưu tài liệu
Sau khi chỉnh sửa tài liệu, bước cuối cùng là lưu nó. GroupDocs.Editor cung cấp nhiều tùy chọn để lưu tài liệu ở các định dạng khác nhau.
## Lưu dưới dạng RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Lưu dưới dạng DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Lưu dưới dạng văn bản thuần túy
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Bước 4: Dọn dẹp
 Cuối cùng, điều quan trọng là phải loại bỏ`EditableDocument` Và`Editor` trường hợp để giải phóng tài nguyên.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Bằng cách làm theo các bước này, bạn có thể tải, chỉnh sửa và lưu tài liệu một cách hiệu quả bằng GroupDocs.Editor cho .NET. Công cụ mạnh mẽ này mang đến sự linh hoạt và dễ sử dụng, giúp việc quản lý tài liệu trở nên dễ dàng.
## Phần kết luận
Chỉnh sửa và lưu tài liệu theo chương trình chưa bao giờ dễ dàng hơn thế với GroupDocs.Editor cho .NET. Hướng dẫn này sẽ hướng dẫn bạn toàn bộ quá trình, từ tải tài liệu đến lưu tài liệu ở nhiều định dạng khác nhau. Với GroupDocs.Editor, bạn có một giải pháp linh hoạt và mạnh mẽ trong tầm tay, đơn giản hóa quá trình chỉnh sửa tài liệu.
## Câu hỏi thường gặp
### GroupDocs.Editor hỗ trợ những định dạng tệp nào?
GroupDocs.Editor hỗ trợ nhiều định dạng tệp khác nhau, bao gồm DOCX, RTF, TXT, v.v. Để có danh sách đầy đủ, hãy xem[tài liệu](https://reference.groupdocs.com/editor/net/).
### Tôi có thể dùng thử GroupDocs.Editor trước khi mua không?
 Vâng, bạn có thể nhận được một[dùng thử miễn phí](https://releases.groupdocs.com/) để kiểm tra các tính năng của GroupDocs.Editor.
### Có sự hỗ trợ nào nếu tôi gặp vấn đề không?
 Tuyệt đối! Bạn có thể ghé thăm[diễn đàn hỗ trợ](https://forum.groupdocs.com/c/editor/20) để được hỗ trợ về mọi vấn đề bạn gặp phải.
### Làm cách nào để có được giấy phép tạm thời?
 Bạn có thể yêu cầu một[giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/) cho mục đích đánh giá.
### Tôi có thể mua phiên bản đầy đủ của GroupDocs.Editor ở đâu?
 Bạn có thể mua phiên bản đầy đủ[đây](https://purchase.groupdocs.com/buy).