---
title: Làm việc với Bảng tính được bảo vệ bằng mật khẩu
linktitle: Làm việc với Bảng tính được bảo vệ bằng mật khẩu
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách xử lý bảng tính được bảo vệ bằng mật khẩu bằng GroupDocs.Editor cho .NET. Hướng dẫn chi tiết này hướng dẫn bạn cách mở để lưu tệp Excel an toàn.
weight: 18
url: /vi/net/document-processing/work-password-protected-spreadsheets/
---
## Giới thiệu
Bạn đang gặp khó khăn trong việc quản lý các bảng tính được bảo vệ bằng mật khẩu trong các ứng dụng .NET của mình? Nếu vậy, bạn đang ở đúng nơi! Trong hướng dẫn toàn diện này, chúng tôi sẽ hướng dẫn bạn quy trình sử dụng GroupDocs.Editor cho .NET để xử lý các bảng tính được bảo vệ bằng mật khẩu một cách hiệu quả. Đến cuối hướng dẫn này, bạn sẽ được trang bị đầy đủ để mở, chỉnh sửa và lưu các tệp Excel được mã hóa một cách dễ dàng.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo bạn có mọi thứ bạn cần để làm theo:
- Kiến thức cơ bản về C#: Hướng dẫn này giả sử bạn đã quen thuộc với lập trình C#.
- .NET Framework: Đảm bảo bạn đã cài đặt .NET framework trên máy phát triển của mình.
-  GroupDocs.Editor cho .NET: Tải xuống và cài đặt GroupDocs.Editor cho .NET từ[đây](https://releases.groupdocs.com/editor/net/).
## Nhập không gian tên
Để bắt đầu, bạn cần nhập các vùng tên cần thiết vào dự án C# của mình. Các không gian tên này cung cấp quyền truy cập vào các chức năng của GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Bước 1: Nhận đường dẫn đến tệp đầu vào
Trước tiên, bạn sẽ cần một đường dẫn đến tệp đầu vào. Trong ví dụ này, chúng tôi sẽ sử dụng tệp Excel mẫu (`Your Sample Document`) được bảo vệ bằng mật khẩu.
```csharp
string inputFilePath = "Your Sample Document";
```
## Bước 2: Cố gắng mở tài liệu mà không cần mật khẩu
Hãy xem điều gì sẽ xảy ra nếu chúng ta cố mở tài liệu mà không cung cấp mật khẩu.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Bước 3: Thử chỉ định mật khẩu sai
Bây giờ, chúng tôi sẽ chỉ định một mật khẩu không chính xác để minh họa cách người soạn thảo phản hồi.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Bước 4: Mở file bằng mật khẩu đúng
Hãy cung cấp mật khẩu chính xác và mở tệp thành công.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Bước 5: Tạo và điều chỉnh các tùy chọn chỉnh sửa
Để chỉnh sửa bảng tính chúng ta cần tạo và điều chỉnh các tùy chọn chỉnh sửa.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Bước 6: Tạo Tài liệu có thể chỉnh sửa trung gian
 Tiếp theo, chúng tôi tạo một trung gian`EditableDocument` cho phép chúng tôi thực hiện các thay đổi đối với bảng tính.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Bước 7: Tạo tùy chọn lưu
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Bước 7.1: Đặt mật khẩu mở mới
    saveOptions.Password = "new password";
    // Bước 7.2: Đặt bảo vệ ghi
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Bước 8: Lưu tài liệu mà không sửa đổi
    //Bước 8.1: Chuẩn bị tên tệp đầu ra và đường dẫn
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Bước 8.2: Tạo luồng đầu ra
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Bước 8.3: Lưu
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Bước 9: Loại bỏ phiên bản soạn thảo
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Phần kết luận
Chúc mừng! Bạn đã học thành công cách xử lý bảng tính được bảo vệ bằng mật khẩu bằng GroupDocs.Editor cho .NET. Từ việc cố gắng mở tài liệu mà không cần mật khẩu đến lưu tài liệu bằng cài đặt bảo vệ mới, bạn đã thực hiện tất cả các bước cần thiết. Kiến thức này chắc chắn sẽ nâng cao khả năng quản lý tài liệu an toàn trong các ứng dụng .NET của bạn.
## Câu hỏi thường gặp
### GroupDocs.Editor dành cho .NET là gì?
GroupDocs.Editor cho .NET là API chỉnh sửa tài liệu mạnh mẽ cho phép các nhà phát triển tải, chỉnh sửa và lưu nhiều định dạng tài liệu khác nhau trong các ứng dụng .NET.
### Làm cách nào tôi có thể nhận được giấy phép tạm thời cho GroupDocs.Editor?
 Bạn có thể xin giấy phép tạm thời từ[đây](https://purchase.groupdocs.com/temporary-license/) để đánh giá đặc tính của sản phẩm.
### Có thể tối ưu hóa việc sử dụng bộ nhớ trong khi chỉnh sửa các tài liệu lớn không?
 Có, bạn có thể bật tính năng tối ưu hóa bộ nhớ bằng cách đặt`OptimizeMemoryUsage` tài sản để`true`trong các tùy chọn tải.
### Tôi có thể đặt các mật khẩu khác nhau để mở và ghi vào bảng tính không?
Tuyệt đối! Bạn có thể đặt mật khẩu riêng để mở tài liệu và bảo vệ ghi bằng các tùy chọn lưu.
### Tôi có thể tìm tài liệu chi tiết hơn ở đâu?
 Bạn có thể truy cập tài liệu toàn diện về GroupDocs.Editor for .NET[đây](https://tutorials.groupdocs.com/editor/net/).