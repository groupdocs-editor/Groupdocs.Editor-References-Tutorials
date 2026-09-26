---
date: 2026-09-26
description: Tìm hiểu cách xử lý tiền tố CSS và trích xuất nội dung CSS bằng GroupDocs.Editor
  cho .NET trong tutorial chi tiết step‑by‑step.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Xử lý Nội dung CSS với Tiền tố
og_description: Khám phá cách xử lý tiền tố CSS và trích xuất nội dung CSS với GroupDocs.Editor
  cho .NET. Thực hiện hướng dẫn step‑by‑step để prepend URLs tới tài nguyên CSS và
  retrieve stylesheets.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Cách xử lý tiền tố CSS trong GroupDocs.Editor cho .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Cách xử lý tiền tố CSS trong GroupDocs.Editor cho .NET
type: docs
url: /vi/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Cách xử lý tiền tố CSS trong GroupDocs.Editor cho .NET

Trong hướng dẫn này, bạn sẽ học **cách xử lý tiền tố CSS** khi làm việc với các stylesheet bên trong tài liệu bằng GroupDocs.Editor cho .NET. Cho dù bạn cần thêm một URL vào trước các hình ảnh, phông chữ hoặc bất kỳ tài nguyên bên ngoài nào, các bước dưới đây sẽ chỉ cho bạn cách **xử lý tiền tố CSS** và cũng cách **trích xuất nội dung CSS** để xử lý tiếp theo. Khi kết thúc hướng dẫn, bạn sẽ có thể viết lại các đường dẫn tài nguyên, lấy các chuỗi CSS thô, và tích hợp chúng vào quy trình web của mình một cách tự tin.

## Câu trả lời nhanh
- **“handle css prefix” có nghĩa là gì?** Thêm một tiền tố URL tùy chỉnh vào các tài nguyên bên ngoài được tham chiếu trong CSS.  
- **Phương thức API nào trả về các kiểu CSS?** `EditableDocument.GetCssContent(...)`.  
- **Tôi có cần giấy phép không?** Có giấy phép dùng thử; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.5+ và .NET Core/5/6.  
- **Tôi có thể thay đổi tiền tố tại thời gian chạy không?** Có – chỉ cần truyền một chuỗi khác vào `GetCssContent`.

## Tiền tố CSS là gì?
Thuật ngữ này đề cập đến việc viết lại các URL của hình ảnh, phông chữ hoặc bất kỳ tài sản bên ngoài nào trong tệp CSS sao cho chúng trỏ tới một vị trí bạn kiểm soát, chẳng hạn như CDN hoặc máy chủ bảo mật. Bằng cách thêm một URL cơ sở nhất quán vào trước, bạn đảm bảo rằng mọi tài nguyên đều tải đúng khi tài liệu được hiển thị trong trình duyệt hoặc trình xem dựa trên web.

## Tại sao nên sử dụng GroupDocs.Editor để trích xuất nội dung CSS?
GroupDocs.Editor có thể đọc CSS gốc được nhúng trong tài liệu WordProcessing, trả về các chuỗi stylesheet thô và cho phép bạn thao tác chúng trước khi hiển thị hoặc lưu. Điều này loại bỏ việc phân tích thủ công, đảm bảo độ trung thực với biểu diễn nội bộ của tài liệu, và hỗ trợ **hơn 30 định dạng tệp** trong khi xử lý các tệp lên tới **500 MB** mà không cần tải toàn bộ tệp vào bộ nhớ.

## Yêu cầu trước
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã chuẩn bị các yêu cầu sau:
- Visual Studio: Bạn sẽ cần một cài đặt Visual Studio hoạt động.  
- .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework.  
- GroupDocs.Editor for .NET: Bạn có thể tải xuống từ [trang tải GroupDocs.Editor cho .NET](https://releases.groupdocs.com/editor/net/).  
- Sample Document: Có một tài liệu mẫu sẵn sàng để chỉnh sửa.

## Nhập không gian tên
Đầu tiên, hãy nhập các không gian tên cần thiết để đảm bảo mã của chúng ta chạy mượt mà. Bước này cho phép chúng ta truy cập vào các lớp cốt lõi của GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Bước 1: Khởi tạo Editor
`Lớp `Editor` là điểm khởi đầu để làm việc với tài liệu trong GroupDocs.Editor. Nó quản lý các thao tác tải, chỉnh sửa và lưu.  
Bước đầu tiên là tạo một thể hiện `Editor` với tài liệu mẫu của bạn. Điều này thiết lập môi trường chỉnh sửa.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Bước 2: Chỉnh sửa tài liệu
Đối tượng `EditableDocument` đại diện cho phiên bản có thể chỉnh sửa của tệp và hiển thị các phần nội bộ của nó, chẳng hạn như CSS, hình ảnh và HTML.  
Tiếp theo, chúng ta lấy một đối tượng `EditableDocument`. Đối tượng này cho phép chúng ta làm việc với CSS nội bộ của tài liệu.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Bước 3: Đặt tiền tố cho tài nguyên bên ngoài
Xác định các tiền tố URL cho hình ảnh và phông chữ. Các tiền tố này sẽ được thêm vào trước mỗi tham chiếu hình ảnh và phông chữ trong CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Bước 4: Trích xuất nội dung CSS với các tiền tố
`GetCssContent` trả về một tập hợp các chuỗi stylesheet CSS đã chứa các URL đã được tiền tố mà bạn cung cấp.  
Gọi `GetCssContent`, truyền vào các tiền tố bạn vừa định nghĩa. Phương thức này trả về một danh sách các chuỗi stylesheet CSS đã chứa các URL đã được tiền tố.

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
- **Không có stylesheet nào được trả về** – Đảm bảo tài liệu nguồn thực sự chứa CSS (ví dụ, tài liệu Word có bảng được định dạng hoặc HTML nhúng).  
- **URL không đúng** – Kiểm tra lại rằng các chuỗi tiền tố kết thúc bằng dấu phân cách thích hợp (`/` hoặc `=`) cho định tuyến máy chủ của bạn.  
- **Mối quan ngại về hiệu suất** – Đối với tài liệu rất lớn, hãy xem xét xử lý các stylesheet theo lô để tránh việc sử dụng bộ nhớ cao.

## Câu hỏi thường gặp

**Q: Tôi có thể sử dụng GroupDocs.Editor cho .NET với các định dạng tài liệu khác không?**  
A: Có, GroupDocs.Editor cho .NET hỗ trợ PDF, Word, Excel, PowerPoint và nhiều định dạng khác.

**Q: Có bản dùng thử miễn phí cho GroupDocs.Editor cho .NET không?**  
A: Chắc chắn! Bạn có thể bắt đầu dùng thử miễn phí trên [trang dùng thử miễn phí của GroupDocs](https://releases.groupdocs.com/).

**Q: Làm thế nào để tôi có được giấy phép tạm thời cho GroupDocs.Editor cho .NET?**  
A: Bạn có thể lấy giấy phép tạm thời từ [trang giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/).

**Q: Tôi có thể tìm tài liệu chi tiết cho GroupDocs.Editor cho .NET ở đâu?**  
A: Tài liệu chi tiết có sẵn trên [trang tài liệu GroupDocs.Editor cho .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Các tùy chọn hỗ trợ nào có sẵn cho GroupDocs.Editor cho .NET?**  
A: Bạn có thể nhận hỗ trợ qua [diễn đàn hỗ trợ GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Các câu hỏi thường gặp bổ sung

**Q: Tôi có thể thay đổi tiền tố sau khi đã trích xuất CSS không?**  
A: Có. Gọi lại `GetCssContent` với một chuỗi tiền tố khác; phương thức luôn sử dụng các giá trị bạn truyền tại thời gian chạy.

**Q: Điều này có hoạt động với tài liệu được bảo vệ bằng mật khẩu không?**  
A: Có. Cung cấp mật khẩu trong `WordProcessingLoadOptions` khi tạo thể hiện `Editor`.

**Q: Có thể lưu CSS đã chỉnh sửa trở lại tài liệu không?**  
A: Hiện tại GroupDocs.Editor chỉ cung cấp quyền truy cập chỉ đọc vào CSS. Để lưu các thay đổi, bạn cần thay thế stylesheet gốc bằng các API XML nền tảng của tài liệu.

---

**Cập nhật lần cuối:** 2026-09-26  
**Đã kiểm tra với:** GroupDocs.Editor 23.12 for .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Trích xuất CSS bên ngoài từ tài liệu Word bằng GroupDocs.Editor .NET: Hướng dẫn toàn diện](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Trích xuất & Thêm tiền tố HTML từ tài liệu Word bằng GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Cách trích xuất và chỉnh sửa nội dung HTML trong tài liệu Word bằng GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)