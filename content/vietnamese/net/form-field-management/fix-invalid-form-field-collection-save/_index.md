---
title: Sửa lỗi Thu thập và lưu trường biểu mẫu không hợp lệ
linktitle: Sửa lỗi Thu thập và lưu trường biểu mẫu không hợp lệ
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách sửa các trường biểu mẫu không hợp lệ trong DOCX bằng Groupdocs.Editor cho .NET. Hãy làm theo hướng dẫn này để đảm bảo tài liệu của bạn không có lỗi và lưu chúng một cách an toàn.
weight: 11
url: /vi/net/form-field-management/fix-invalid-form-field-collection-save/
---

# Sửa lỗi Thu thập và lưu trường biểu mẫu không hợp lệ

## Giới thiệu
Chào mừng! Nếu bạn đang làm việc với các trường biểu mẫu trong tài liệu và gặp phải vấn đề với bộ sưu tập trường biểu mẫu không hợp lệ thì bạn đã đến đúng nơi. Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách sửa các trường biểu mẫu không hợp lệ và lưu tài liệu của bạn bằng Groupdocs.Editor cho .NET. Chúng tôi sẽ hướng dẫn bạn thực hiện quy trình này theo từng bước, đảm bảo bạn có tất cả thông tin chi tiết cần thiết để quy trình này hoạt động trơn tru. Bắt đầu nào!
## Điều kiện tiên quyết
Trước khi chúng ta bắt đầu viết mã, có một số điều bạn cần phải chuẩn bị sẵn:
-  Groupdocs.Editor cho .NET: Đảm bảo bạn đã cài đặt thư viện Groupdocs.Editor cho .NET. Bạn có thể tải nó xuống[đây](https://releases.groupdocs.com/editor/net/).
- Môi trường phát triển: Bạn nên thiết lập môi trường phát triển .NET, chẳng hạn như Visual Studio.
- Kiến thức cơ bản về C#: Hướng dẫn này giả sử bạn có hiểu biết cơ bản về lập trình C#.
## Nhập không gian tên
Trước tiên, bạn cần nhập các vùng tên cần thiết trong dự án C# của mình. Thêm các dòng sau vào đầu tệp mã của bạn:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Bước 1: Lấy đường dẫn tệp đầu vào
Bước đầu tiên là chỉ định đường dẫn đến tệp đầu vào của bạn. Tệp này phải là tài liệu DOCX chứa các trường biểu mẫu.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Bước 2: Tạo luồng từ đường dẫn tệp
Tiếp theo, tạo luồng tệp để đọc tài liệu đầu vào. Điều này sẽ cho phép bạn tải tài liệu vào trình chỉnh sửa.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Bước 3: Tạo tùy chọn tải cho tài liệu
Ở bước này, bạn cần tạo các tùy chọn tải cho tài liệu của mình. Nếu tài liệu của bạn được bảo vệ bằng mật khẩu, bạn có thể chỉ định mật khẩu. Trong ví dụ này, tài liệu không được bảo vệ nên mật khẩu sẽ bị bỏ qua.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Bước 4: Tải tài liệu vào phiên bản soạn thảo
Bây giờ, hãy tải tài liệu có các tùy chọn đã chỉ định vào phiên bản Trình soạn thảo. Đây là nơi sẽ diễn ra các thao tác chính trên tài liệu.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Bước 4.1: Đọc phiên bản FormFieldManager
 Các`FormFieldManager` instance chịu trách nhiệm quản lý các trường biểu mẫu trong tài liệu. Bạn sẽ cần đọc phiên bản này để truy cập và thao tác với các trường biểu mẫu.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Bước 4.2: Đọc FormFieldCollection
 Các`FormFieldCollection` chứa tất cả các trường biểu mẫu trong tài liệu. Bạn sẽ đọc bộ sưu tập này để kiểm tra và sửa các trường biểu mẫu không hợp lệ.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Bước 4.3: Tự động sửa các trường biểu mẫu không hợp lệ
Cố gắng tự động sửa mọi trường biểu mẫu không hợp lệ trong tài liệu. Đây là bước sơ bộ để giải quyết các vấn đề rõ ràng.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Bước 4.4: Kiểm tra các trường biểu mẫu không hợp lệ
Kiểm tra xem có bất kỳ trường biểu mẫu không hợp lệ nào còn lại sau lần thử tự động sửa hay không.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Bước 4.4.1: Nhận tất cả tên trường biểu mẫu không hợp lệ
Truy xuất tên của tất cả các trường biểu mẫu không hợp lệ. Những tên này sẽ được sử dụng để sửa các trường.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Bước 4.4.2: Tạo tên duy nhất cho các trường không hợp lệ
Đối với mỗi trường biểu mẫu không hợp lệ, hãy tạo một tên duy nhất. Điều này đảm bảo rằng không có xung đột với tên trường biểu mẫu hiện có.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Bước 4.4.3: Sửa các trường biểu mẫu không hợp lệ
Sửa các trường biểu mẫu không hợp lệ bằng cách sử dụng tên duy nhất được tạo ở bước trước.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Bước 5: Tạo tùy chọn lưu tài liệu
Thiết lập các tùy chọn để lưu tài liệu. Điều này bao gồm việc chỉ định định dạng và mọi cài đặt lưu bổ sung.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Bước 5.1: Tối ưu hóa việc sử dụng bộ nhớ
 Nếu tài liệu của bạn lớn và có thể gây ra lỗi`OutOfMemoryException`hãy bật tùy chọn tối ưu hóa bộ nhớ.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Bước 5.2: Bảo vệ tài liệu khỏi bị ghi
Để bảo vệ tài liệu khỏi bị sửa đổi, ngoại trừ các trường của biểu mẫu, hãy đặt mật khẩu bảo vệ.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Bước 6: Lưu tài liệu
Cuối cùng, lưu tài liệu với các tùy chọn lưu được chỉ định. Chuẩn bị luồng bộ nhớ để lưu tài liệu đầu ra.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Phần kết luận
 Và bạn có nó rồi đấy! Bạn đã sửa thành công các trường biểu mẫu không hợp lệ và lưu tài liệu của mình bằng Groupdocs.Editor cho .NET. Hướng dẫn từng bước này lẽ ra phải làm cho quy trình trở nên rõ ràng và dễ quản lý. Nếu bạn gặp phải bất kỳ vấn đề hoặc có thắc mắc nào, vui lòng kiểm tra[tài liệu](https://tutorials.groupdocs.com/editor/net/) hoặc tiếp cận với[ủng hộ](https://forum.groupdocs.com/c/editor/20).
## Câu hỏi thường gặp
### Nếu tài liệu của tôi được bảo vệ bằng mật khẩu thì sao?
 Bạn có thể chỉ định mật khẩu trong`WordProcessingLoadOptions` để mở tài liệu.
### Làm cách nào để biết liệu có trường biểu mẫu không hợp lệ hay không?
 Sử dụng`HasInvalidFormFields` phương pháp để kiểm tra bất kỳ trường biểu mẫu không hợp lệ nào trong tài liệu.
### Tôi có thể sửa các trường biểu mẫu mà không thay đổi tên của chúng không?
Bạn nên tạo tên duy nhất cho các trường biểu mẫu không hợp lệ để tránh xung đột.
### Tôi có thể lưu tài liệu ở định dạng nào?
 Bạn có thể lưu tài liệu ở nhiều định dạng khác nhau như DOCX, PDF, v.v. bằng cách đặt cài đặt thích hợp`WordProcessingFormats`.
### Làm cách nào tôi có thể tối ưu hóa việc sử dụng bộ nhớ trong khi lưu các tài liệu lớn?
 Kích hoạt`OptimizeMemoryUsage` tùy chọn trong`WordProcessingSaveOptions` để xử lý các tài liệu lớn một cách hiệu quả.