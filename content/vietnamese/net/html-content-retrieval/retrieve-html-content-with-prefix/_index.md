---
title: Truy xuất nội dung HTML bằng tiền tố
linktitle: Truy xuất nội dung HTML bằng tiền tố
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách truy xuất nội dung HTML từ tài liệu bằng GroupDocs.Editor cho .NET với tiền tố tùy chỉnh cho hình ảnh và biểu định kiểu. Hướng dẫn từng bước bao gồm.
weight: 11
url: /vi/net/html-content-retrieval/retrieve-html-content-with-prefix/
type: docs
---
# Truy xuất nội dung HTML bằng tiền tố

## Giới thiệu
Chào mừng bạn đến với hướng dẫn từng bước của chúng tôi về cách truy xuất nội dung HTML từ tài liệu bằng GroupDocs.Editor cho .NET. Cho dù bạn là nhà phát triển dày dạn hay chỉ mới bắt đầu, hướng dẫn này sẽ hướng dẫn bạn thực hiện quy trình một cách dễ thực hiện. Chúng tôi sẽ đề cập đến mọi thứ bạn cần biết, từ thiết lập môi trường cho đến thực thi mã thành công. Hãy đi sâu vào!
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có sẵn các điều kiện tiên quyết sau:
1.  GroupDocs.Editor cho .NET: Tải xuống phiên bản mới nhất từ[trang tải xuống](https://releases.groupdocs.com/editor/net/).
2. Môi trường phát triển: Visual Studio hoặc bất kỳ môi trường phát triển .NET ưa thích nào khác.
3. Kiến thức cơ bản về C#: Làm quen với lập trình C# sẽ giúp bạn theo dõi các ví dụ.
4. Tài liệu cần chỉnh sửa: Chuẩn bị sẵn tài liệu mẫu để thử nghiệm, chẳng hạn như tài liệu Word.
5. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework trên máy của mình.
Bây giờ bạn đã sẵn sàng mọi thứ, hãy bắt đầu!
## Nhập không gian tên
Trước tiên, bạn cần nhập các vùng tên cần thiết trong dự án C# của mình. Các không gian tên này cung cấp các lớp và phương thức cần thiết để hoạt động với GroupDocs.Editor cho .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Với các không gian tên đã được nhập, chúng ta có thể chuyển sang thiết lập trình chỉnh sửa.
## Bước 1: Khởi tạo Trình chỉnh sửa
 Để bắt đầu, bạn cần khởi tạo`Editor`lớp với tài liệu của bạn. Bước này liên quan đến việc chỉ định tài liệu bạn muốn chỉnh sửa và cung cấp các tùy chọn tải cần thiết.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Các bước tiếp theo sẽ được thêm vào đây
}
```
 Trong ví dụ này, chúng tôi đang tải một tài liệu Word. Bạn có thể thay thế`"Your Sample Document"` với đường dẫn đến tài liệu của bạn.
## Bước 2: Chỉnh sửa tài liệu
 Tiếp theo, chúng ta cần mở tài liệu để chỉnh sửa. Việc này được thực hiện bằng cách sử dụng`Edit` phương pháp của`Editor` lớp, đòi hỏi`WordProcessingEditOptions` như một lý lẽ.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Các bước tiếp theo sẽ được thêm vào đây
}
```
 Các`EditableDocument` instance đại diện cho tài liệu ở định dạng có thể chỉnh sửa. Bây giờ chúng ta đã sẵn sàng để lấy nội dung HTML.
## Bước 3: Xác định tiền tố tùy chỉnh
Để thêm tiền tố tùy chỉnh cho hình ảnh và CSS, chúng ta cần xác định tiền tố dưới dạng chuỗi. Bước này đảm bảo rằng nội dung HTML sẽ có tiền tố được chỉ định cho các tài nguyên bên ngoài.
```csharp
string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
string externalCssPrefix = "http://www.mywebsite.com/css/id=";
```
Bạn có thể thay thế các URL bằng tiền tố mong muốn của mình. Những tiền tố này sẽ được sử dụng trong bước tiếp theo để tùy chỉnh đầu ra HTML.
## Bước 4: Truy xuất nội dung HTML
Bây giờ chúng ta đã đặt tiền tố, chúng ta có thể truy xuất nội dung HTML từ tài liệu. Các`GetContent` phương pháp của`EditableDocument` class cho phép chúng ta chỉ định tiền tố hình ảnh và CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Đoạn mã này tìm nạp nội dung HTML với các tiền tố tùy chỉnh và in nó ra bảng điều khiển. Bạn có thể xử lý thêm hoặc lưu nội dung HTML này nếu cần.
## Phần kết luận
Và bạn có nó rồi đấy! Bằng cách làm theo các bước này, bạn có thể dễ dàng truy xuất nội dung HTML từ tài liệu bằng GroupDocs.Editor cho .NET, hoàn chỉnh với các tiền tố tùy chỉnh cho hình ảnh và biểu định kiểu. Công cụ mạnh mẽ này đơn giản hóa thao tác tài liệu, cho phép bạn tập trung vào việc tích hợp chỉnh sửa tài liệu vào các ứng dụng .NET của mình một cách liền mạch.
 Để biết thêm thông tin chi tiết, hãy xem[GroupDocs.Editor cho tài liệu .NET](https://tutorials.groupdocs.com/editor/net/) . Nếu bạn có bất kỳ câu hỏi nào hoặc cần hỗ trợ thêm, vui lòng liên hệ theo số[diễn đàn hỗ trợ](https://forum.groupdocs.com/c/editor/20).
## Câu hỏi thường gặp
### Tôi có thể chỉnh sửa những loại tài liệu nào bằng GroupDocs.Editor cho .NET?
GroupDocs.Editor hỗ trợ nhiều định dạng tài liệu khác nhau bao gồm Word, Excel, PowerPoint, PDF, v.v.
### Làm cách nào để tôi có thể dùng thử miễn phí GroupDocs.Editor cho .NET?
 Bạn có thể dùng thử miễn phí từ[Trang web GroupDocs](https://releases.groupdocs.com/).
### Tôi có thể tùy chỉnh thêm nội dung HTML không?
Có, bạn có thể sửa đổi nội dung HTML được truy xuất nếu cần trước khi hiển thị hoặc lưu nó.
### Có thể sử dụng GroupDocs.Editor cho .NET với các ngôn ngữ .NET khác không?
Có, bạn có thể sử dụng nó với bất kỳ ngôn ngữ tương thích .NET nào như VB.NET hoặc F#.
### Làm cách nào để có được giấy phép tạm thời cho GroupDocs.Editor cho .NET?
 Bạn có thể nhận được giấy phép tạm thời từ[trang mua hàng](https://purchase.groupdocs.com/temporary-license/).