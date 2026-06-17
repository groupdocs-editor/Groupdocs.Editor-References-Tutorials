---
date: 2026-03-06
description: Tìm hiểu cách xử lý nội dung CSS với tiền tố và trích xuất nội dung CSS
  bằng GroupDocs.Editor cho .NET trong hướng dẫn chi tiết từng bước này.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Xử lý nội dung CSS với tiền tố
type: docs
url: /vi/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Xử lý nội dung CSS với tiền tố

Trong hướng dẫn này, bạn sẽ khám phá **cách xử lý tiền tố css** khi làm việc với các stylesheet trong tài liệu bằng cách sử dụng GroupDocs.Editor cho .NET. Cho dù bạn cần thêm một URL vào trước các hình ảnh, phông chữ, hoặc bất kỳ tài nguyên bên ngoài nào, các bước dưới đây sẽ cho bạn thấy chính xác cách **xử lý tiền tố css** và cũng cách **trích xuất nội dung css** để xử lý tiếp.

## Câu trả lời nhanh
- **“handle css prefix” có nghĩa là gì?** Thêm một tiền tố URL tùy chỉnh vào các tài nguyên bên ngoài được tham chiếu trong CSS.
- **Phương thức API nào trả về các kiểu CSS?** `EditableDocument.GetCssContent(...)`.
- **Tôi có cần giấy phép không?** Có giấy phép dùng thử; giấy phép thương mại được yêu cầu cho môi trường sản xuất.
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.5+ và .NET Core/5/6.
- **Tôi có thể thay đổi tiền tố ở thời gian chạy không?** Có – chỉ cần truyền một chuỗi khác vào `GetCssContent`.

## **handle css prefix** là gì?
Áp dụng một tiền tố cho các tài nguyên CSS sẽ ghi lại lại các đường dẫn của hình ảnh, phông chữ hoặc các tài sản khác sao cho chúng trỏ tới một vị trí bạn kiểm soát (ví dụ: CDN hoặc máy chủ bảo mật). Điều này đặc biệt hữu ích khi bạn xuất một tài liệu và cần tất cả các tham chiếu bên ngoài có thể truy cập được từ một ứng dụng web.

## Tại sao nên sử dụng GroupDocs.Editor để **trích xuất nội dung css**?
GroupDocs.Editor có thể đọc CSS gốc được nhúng trong tài liệu WordProcessing, cung cấp cho bạn các chuỗi stylesheet thô, và cho phép bạn thao tác chúng trước khi render hoặc lưu. Điều này loại bỏ nhu cầu phân tích thủ công và đảm bảo rằng CSS được trích xuất khớp với biểu diễn nội bộ của tài liệu.

## Yêu cầu trước
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có các yêu cầu sau:
- Visual Studio: Bạn sẽ cần một cài đặt Visual Studio hoạt động.
- .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework.
- GroupDocs.Editor cho .NET: Bạn có thể tải xuống tại [here](https://releases.groupdocs.com/editor/net/).
- Sample Document: Có một tài liệu mẫu sẵn sàng để chỉnh sửa.

## Nhập các Namespace
Đầu tiên, hãy nhập các namespace cần thiết để đảm bảo mã của chúng ta chạy trơn tru. Bước này cho phép chúng ta truy cập vào các lớp cốt lõi của GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Bước 1: Khởi tạo Editor
Bước đầu tiên liên quan đến việc tạo một thể hiện `Editor` với tài liệu mẫu của bạn. Điều này thiết lập môi trường chỉnh sửa.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Bước 2: Chỉnh sửa tài liệu
Tiếp theo, chúng ta lấy một đối tượng `EditableDocument`. Đối tượng này đại diện cho phiên bản có thể chỉnh sửa của tệp và cho phép chúng ta làm việc với các phần nội bộ của nó.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Bước 3: Đặt tiền tố cho tài nguyên bên ngoài
Xác định các tiền tố URL cho hình ảnh và phông chữ. Các tiền tố này sẽ được thêm vào trước mỗi tham chiếu hình ảnh và phông chữ được tìm thấy trong CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Bước 4: **Trích xuất nội dung CSS** với các tiền tố
Gọi `GetCssContent`, truyền vào các tiền tố bạn vừa định nghĩa. Phương thức này trả về một danh sách các chuỗi stylesheet CSS đã chứa các URL có tiền tố.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Bước 5: Xuất kết quả
In số lượng stylesheet được tìm thấy và hiển thị mỗi stylesheet. Điều này giúp bạn xác nhận rằng các tiền tố đã được áp dụng đúng.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Các vấn đề thường gặp và giải pháp
- **Không có stylesheet nào được trả về** – Đảm bảo tài liệu nguồn thực sự chứa CSS (ví dụ: tài liệu Word có bảng được định dạng hoặc HTML nhúng).
- **URL không đúng** – Kiểm tra lại rằng các chuỗi tiền tố kết thúc bằng dấu phân cách phù hợp (`/` hoặc `=`) cho định tuyến máy chủ của bạn.
- **Mối quan ngại về hiệu suất** – Đối với tài liệu rất lớn, hãy cân nhắc xử lý các stylesheet theo lô để tránh việc sử dụng bộ nhớ cao.

## Kết luận
Xử lý nội dung CSS với tiền tố bằng cách sử dụng GroupDocs.Editor cho .NET là đơn giản và mạnh mẽ. Bằng cách thực hiện các bước này, bạn có thể **xử lý tiền tố css**, lấy CSS thô thông qua **trích xuất nội dung css**, và tích hợp liền mạch các tài nguyên bên ngoài vào quy trình web của mình. Khám phá các tính năng khác của GroupDocs.Editor như chuyển đổi HTML, trích xuất hình ảnh và hợp nhất tài liệu để nhận được giá trị cao hơn từ API.

## Câu hỏi thường gặp
### Tôi có thể sử dụng GroupDocs.Editor cho .NET với các định dạng tài liệu khác không?
Có, GroupDocs.Editor cho .NET hỗ trợ nhiều định dạng tài liệu khác nhau bao gồm PDF, Word, Excel và hơn nữa.

### Có bản dùng thử miễn phí cho GroupDocs.Editor cho .NET không?
Chắc chắn! Bạn có thể bắt đầu bản dùng thử miễn phí [here](https://releases.groupdocs.com/).

### Làm thế nào để tôi nhận được giấy phép tạm thời cho GroupDocs.Editor cho .NET?
Bạn có thể nhận giấy phép tạm thời [here](https://purchase.groupdocs.com/temporary-license/).

### Tôi có thể tìm tài liệu chi tiết cho GroupDocs.Editor cho .NET ở đâu?
Tài liệu chi tiết có sẵn [here](https://tutorials.groupdocs.com/editor/net/).

### Các tùy chọn hỗ trợ nào có sẵn cho GroupDocs.Editor cho .NET?
Bạn có thể nhận hỗ trợ [here](https://forum.groupdocs.com/c/editor/20).

## Các câu hỏi thường gặp bổ sung

**Q: Tôi có thể thay đổi tiền tố sau khi đã trích xuất CSS không?**  
A: Có. Gọi lại `GetCssContent` với một chuỗi tiền tố khác; phương thức luôn sử dụng các giá trị bạn truyền vào thời gian chạy.

**Q: Điều này có hoạt động với tài liệu được bảo vệ bằng mật khẩu không?**  
A: Có. Cung cấp mật khẩu trong `WordProcessingLoadOptions` khi tạo thể hiện `Editor`.

**Q: Có thể lưu CSS đã chỉnh sửa trở lại tài liệu không?**  
A: Hiện tại GroupDocs.Editor chỉ cung cấp quyền truy cập chỉ đọc vào CSS. Để lưu các thay đổi, bạn cần thay thế stylesheet gốc bằng cách sử dụng các API XML nền tảng của tài liệu.

---

**Cập nhật lần cuối:** 2026-03-06  
**Kiểm tra với:** GroupDocs.Editor 23.12 cho .NET  
**Tác giả:** GroupDocs