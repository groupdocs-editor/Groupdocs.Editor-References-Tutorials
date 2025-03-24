---
title: Làm việc với Bộ sưu tập trường biểu mẫu kế thừa
linktitle: Làm việc với Bộ sưu tập trường biểu mẫu kế thừa
second_title: API GroupDocs.Editor .NET
description: Tìm hiểu cách quản lý các trường biểu mẫu cũ bằng GroupDocs.Editor dành cho .NET với hướng dẫn chi tiết của chúng tôi. Hoàn hảo để xử lý các trường văn bản, hộp kiểm, ngày tháng, v.v.
weight: 12
url: /vi/net/form-field-management/work-legacy-form-field-collection/
---
## Giới thiệu
Chào mừng bạn đến với hướng dẫn toàn diện này về cách làm việc với các bộ sưu tập trường biểu mẫu cũ bằng GroupDocs.Editor cho .NET. Cho dù bạn đang xử lý các trường văn bản, hộp kiểm, trường ngày hay menu thả xuống, hướng dẫn này sẽ hướng dẫn bạn từng bước để quản lý các trường này một cách hiệu quả. Đến cuối hướng dẫn này, bạn sẽ hiểu rõ về cách sử dụng GroupDocs.Editor để xử lý các trường biểu mẫu khác nhau trong tài liệu của mình. Hãy đi sâu vào!
## Điều kiện tiên quyết
Trước khi chúng tôi bắt đầu, hãy đảm bảo bạn có các điều kiện tiên quyết sau:
- Visual Studio: Mọi phiên bản gần đây đều hoạt động.
- .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework.
-  GroupDocs.Editor for .NET: Tải phiên bản mới nhất[đây](https://releases.groupdocs.com/editor/net/).
- Tài liệu mẫu: Tệp DOCX mẫu có các trường biểu mẫu dành cho mục đích thử nghiệm.
## Nhập không gian tên
Để bắt đầu, hãy nhập các không gian tên cần thiết trong dự án của bạn. Các không gian tên này rất cần thiết để truy cập các lớp và phương thức cần thiết để thao tác các trường biểu mẫu.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Bước 1: Lấy đường dẫn tệp đầu vào
Trước tiên, bạn cần chỉ định đường dẫn đến tệp đầu vào của mình. Trong ví dụ này, chúng tôi sẽ sử dụng tệp DOCX mẫu chứa nhiều trường biểu mẫu khác nhau.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Bước 2: Tạo luồng từ đường dẫn tệp
Tiếp theo, tạo luồng tệp để đọc nội dung tài liệu của bạn. Luồng này sẽ được sử dụng để tải tài liệu vào GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Mã bổ sung sẽ ở đây
}
```
## Bước 3: Tạo tùy chọn tải cho tài liệu
Trước khi tải tài liệu, hãy tạo các tùy chọn tải. Các tùy chọn này sẽ giúp xử lý các tình huống khác nhau, chẳng hạn như tài liệu được bảo vệ bằng mật khẩu.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Nếu tài liệu được bảo vệ bằng mật khẩu, hãy chỉ định mật khẩu
loadOptions.Password = "your_password_here"; // Sử dụng mật khẩu thực tế nếu cần thiết
```
## Bước 4: Tải tài liệu bằng phiên bản soạn thảo
Bây giờ, hãy tải tài liệu vào phiên bản Trình soạn thảo bằng cách sử dụng luồng tệp và các tùy chọn tải mà bạn đã tạo trước đó.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Mã bổ sung sẽ ở đây
}
```
## Bước 5: Đọc phiên bản FormFieldManager
Để quản lý các trường biểu mẫu, hãy truy cập phiên bản FormFieldManager từ Trình chỉnh sửa. Phiên bản này sẽ cho phép bạn tương tác với các trường biểu mẫu trong tài liệu của bạn.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Bước 6: Đọc FormFieldCollection
Truy xuất FormFieldCollection từ FormFieldManager. Bộ sưu tập này chứa tất cả các trường biểu mẫu có trong tài liệu.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Bước 7: Lặp lại qua từng trường biểu mẫu
Lặp lại từng trường biểu mẫu trong bộ sưu tập và xác định loại của nó. Tùy thuộc vào loại, bạn có thể trích xuất và thao tác giá trị của trường.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Bước 8: Kết luận
Bằng cách làm theo các bước này, bạn có thể quản lý và tương tác một cách hiệu quả với các trường biểu mẫu cũ trong tài liệu của mình bằng GroupDocs.Editor cho .NET. Cho dù đó là trường văn bản, hộp kiểm, ngày tháng, số hay danh sách thả xuống, hướng dẫn này đều cung cấp cách rõ ràng và ngắn gọn để xử lý từng loại.
## Phần kết luận
 Làm việc với các trường biểu mẫu cũ trong tài liệu có thể đơn giản khi sử dụng đúng công cụ. GroupDocs.Editor cho .NET cung cấp giải pháp mạnh mẽ để quản lý các trường này một cách hiệu quả. Bằng cách làm theo hướng dẫn từng bước này, giờ đây bạn có thể thao tác các trường biểu mẫu khác nhau trong tài liệu của mình một cách dễ dàng. Đừng quên khám phá[tài liệu](https://tutorials.groupdocs.com/editor/net/)để biết thêm các tính năng và tùy chọn nâng cao.
## Câu hỏi thường gặp
### 1. Tôi có thể sử dụng GroupDocs.Editor cho .NET với các tài liệu được bảo vệ bằng mật khẩu không?
Có, bạn có thể chỉ định mật khẩu trong tùy chọn tải để xử lý các tài liệu được bảo vệ bằng mật khẩu.
### 2. Làm cách nào để tôi có thể dùng thử miễn phí GroupDocs.Editor cho .NET?
 Bạn có thể tải xuống bản dùng thử miễn phí từ[đây](https://releases.groupdocs.com/).
### 3. Có hỗ trợ nào dành cho GroupDocs.Editor dành cho .NET không?
 Có, bạn có thể truy cập hỗ trợ[đây](https://forum.groupdocs.com/c/editor/20).
### 4. Tôi có thể mua giấy phép GroupDocs.Editor cho .NET không?
 Có, bạn có thể mua giấy phép từ[đây](https://purchase.groupdocs.com/buy).
### 5. Tôi có thể tìm tài liệu về GroupDocs.Editor cho .NET ở đâu?
Tài liệu có sẵn[đây](https://tutorials.groupdocs.com/editor/net/).