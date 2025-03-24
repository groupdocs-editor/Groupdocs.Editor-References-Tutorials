---
title: Xóa bộ sưu tập trường biểu mẫu
linktitle: Xóa bộ sưu tập trường biểu mẫu
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách xóa trường biểu mẫu khỏi tài liệu Word bằng GroupDocs.Editor dành cho .NET với hướng dẫn từng bước này. Lý tưởng cho các nhà phát triển.
weight: 13
url: /vi/net/form-field-management/remove-form-field-collection/
---

# Xóa bộ sưu tập trường biểu mẫu

## Giới thiệu
Bạn đang tìm cách quản lý các trường biểu mẫu trong tài liệu của mình theo chương trình? GroupDocs.Editor cho .NET cung cấp một giải pháp mạnh mẽ để xử lý và thao tác các trường biểu mẫu ở nhiều định dạng tài liệu khác nhau. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn các bước để xóa bộ sưu tập trường biểu mẫu khỏi tài liệu Word bằng thư viện mạnh mẽ này. 
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo bạn đã thiết lập mọi thứ để có trải nghiệm mượt mà:
1. GroupDocs.Editor cho .NET: Đảm bảo bạn đã tải xuống và cài đặt GroupDocs.Editor cho .NET. Nếu không, bạn có thể tải xuống[đây](https://releases.groupdocs.com/editor/net/).
2. Môi trường phát triển: Bạn sẽ cần một môi trường phát triển như Visual Studio.
3. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework trên máy của mình.
4.  Tài liệu mẫu: Có tài liệu Word mẫu (ví dụ:`SampleLegacyFormFields.docx`) với các trường biểu mẫu mà bạn muốn thao tác.

## Nhập không gian tên
Để bắt đầu, bạn cần nhập các vùng tên cần thiết vào dự án .NET của mình. Điều này sẽ cho phép bạn truy cập các chức năng của GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Bước 1: Tải tài liệu
Trước tiên, bạn cần tải tài liệu bạn muốn chỉnh sửa. Hãy chia nhỏ nó ra:
### Bước 1.1: Lấy đường dẫn đến tệp đầu vào
 Bạn cần chỉ định đường dẫn đến tệp đầu vào của mình. Trong ví dụ này, chúng tôi sẽ sử dụng một tệp mẫu có tên`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Bước 1.2: Tạo FileStream từ đường dẫn
 Tiếp theo, tạo một`FileStream` để đọc tài liệu.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Tiếp tục thực hiện các bước tiếp theo trong khối sử dụng này.
}
```
## Bước 2: Đặt tùy chọn tải
Khi tải tài liệu, bạn có thể cần chỉ định các tùy chọn tải, đặc biệt nếu tài liệu của bạn được bảo vệ bằng mật khẩu.
### Bước 2.1: Tạo tùy chọn tải
 Tạo một thể hiện của`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Bước 2.2: Chỉ định mật khẩu (Nếu cần)
Nếu tài liệu của bạn được bảo vệ bằng mật khẩu, bạn có thể chỉ định mật khẩu.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Bước 3: Tải tài liệu vào trình chỉnh sửa
 Bây giờ hãy tải tài liệu vào`Editor` ví dụ bằng cách sử dụng`FileStream` Và`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Tiếp tục thực hiện các bước tiếp theo trong khối sử dụng này.
}
```
## Bước 4: Truy cập và quản lý các trường biểu mẫu
Khi tài liệu đã được tải, giờ đây bạn có thể truy cập và thao tác với các trường của biểu mẫu.
### Bước 4.1: Đọc FormFieldManager
 Truy xuất`FormFieldManager` từ`Editor` ví dụ.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Bước 4.2: Truy cập FormFieldCollection
 Nhận được`FormFieldCollection` chứa tất cả các trường biểu mẫu trong tài liệu.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Bước 4.3: Xóa trường biểu mẫu văn bản cụ thể
Để xóa một trường biểu mẫu văn bản cụ thể, hãy định vị trường đó theo tên của trường đó rồi xóa trường đó.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Bước 4.4: Xóa nhiều trường biểu mẫu
Bạn cũng có thể xóa nhiều trường biểu mẫu cùng một lúc bằng cách chỉ định tên của chúng.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Bước 5: Lưu tài liệu đã sửa đổi
Sau khi sửa đổi các trường của biểu mẫu, bạn cần lưu tài liệu.
### Bước 5.1: Tạo tùy chọn lưu
Chỉ định định dạng và các tùy chọn lưu cho tài liệu đầu ra.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Bước 5.2: Tối ưu hóa việc sử dụng bộ nhớ
Nếu xử lý các tài liệu lớn, bạn có thể muốn tối ưu hóa việc sử dụng bộ nhớ.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Bước 5.3: Đặt bảo vệ (Nếu cần)
Bạn có thể bảo vệ tài liệu khỏi chỉnh sửa thêm bằng cách đặt mật khẩu ghi.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Bước 5.4: Lưu tài liệu
 Cuối cùng, lưu tài liệu bằng cách sử dụng`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Phần kết luận
Chúc mừng! Bạn đã xóa thành công các trường biểu mẫu khỏi tài liệu Word bằng GroupDocs.Editor cho .NET. Thư viện mạnh mẽ này giúp bạn dễ dàng thao tác nội dung tài liệu theo chương trình, giúp bạn tiết kiệm thời gian và công sức.
## Câu hỏi thường gặp
### Tôi có thể sử dụng GroupDocs.Editor cho .NET với các định dạng tài liệu khác không?
Có, GroupDocs.Editor cho .NET hỗ trợ nhiều định dạng tài liệu khác nhau, bao gồm PDF, HTML, v.v.
### Có thể thêm trường biểu mẫu bằng GroupDocs.Editor cho .NET không?
Có, bạn có thể thêm, sửa đổi và xóa các trường biểu mẫu theo chương trình.
### Nếu tài liệu của tôi rất lớn thì sao?
Bạn có thể kích hoạt tính năng tối ưu hóa bộ nhớ trong các tùy chọn lưu để xử lý các tài liệu lớn một cách hiệu quả.
### Tôi có thể sử dụng GroupDocs.Editor cho .NET trong ứng dụng web không?
Tuyệt đối! GroupDocs.Editor cho .NET có thể được tích hợp vào các ứng dụng web để xử lý tài liệu phía máy chủ.
### Tôi có thể nhận hỗ trợ ở đâu nếu gặp vấn đề?
 Bạn có thể ghé thăm[diễn đàn hỗ trợ](https://forum.groupdocs.com/c/editor/20) để được hỗ trợ về mọi vấn đề.