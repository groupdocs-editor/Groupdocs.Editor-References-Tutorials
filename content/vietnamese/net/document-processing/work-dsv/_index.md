---
date: 2026-06-06
description: Tìm hiểu cách **tạo tài liệu có thể chỉnh sửa** từ các tệp CSV và TSV
  bằng GroupDocs.Editor for .NET. Hướng dẫn này cũng chỉ ra cách **đọc văn bản phân
  tách C#** và **chỉnh sửa CSV .NET** một cách hiệu quả trong Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Làm việc với Delimited Separated Values (DSV) – tạo tài liệu có thể chỉnh
  sửa
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Làm việc với Delimited Separated Values (DSV) – tạo tài liệu có thể chỉnh sửa
type: docs
url: /vi/net/document-processing/work-dsv/
weight: 12
---

# Làm việc với Dữ liệu phân tách bằng dấu phân cách (DSV) – tạo tài liệu có thể chỉnh sửa

Nếu bạn là một nhà phát triển .NET cần **tạo tài liệu có thể chỉnh sửa** từ các giá trị phân tách (DSV) như CSV hoặc TSV, bạn đã đến đúng nơi. Trong 100 từ đầu tiên, chúng tôi sẽ giải thích lý do tại sao GroupDocs.Editor cho .NET là cách đáng tin cậy nhất để **đọc văn bản phân tách C#**, chỉnh sửa nó và sau đó lưu lại mà không mất định dạng. Bạn sẽ có một quy trình hoàn chỉnh, sẵn sàng sao chép‑dán, phù hợp tự nhiên với bất kỳ giải pháp Visual Studio nào.

## Câu trả lời nhanh
- **Thư viện nào xử lý chỉnh sửa CSV tốt nhất trong .NET?** GroupDocs.Editor for .NET.
- **Tôi có thể chỉnh sửa các tệp CSV lớn trong Visual Studio không?** Có – API streaming dữ liệu và tránh tải toàn bộ tệp vào bộ nhớ.
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần giấy phép thương mại; bản dùng thử miễn phí có sẵn.
- **Các định dạng nào tôi có thể xuất sau khi chỉnh sửa?** CSV, TSV và các định dạng bảng tính tương thích Excel.
- **API có tương thích với .NET 6+ không?** Chắc chắn – nó hỗ trợ .NET Framework 4.5+, .NET Core 3.1+, .NET 5 và .NET 6.

## “create editable document” là gì trong ngữ cảnh của GroupDocs.Editor?
**Create editable document** có nghĩa là tạo một thể hiện `EditableDocument` đại diện cho phiên bản có thể thay đổi của tệp nguồn (CSV, TSV, v.v.) trong bộ nhớ. Đối tượng này cho phép bạn đọc, sửa đổi và lưu lại nội dung bằng cùng một API. Nó cung cấp các phương thức để lấy văn bản tài liệu, áp dụng thay đổi và lưu lại ở các định dạng khác nhau, đảm bảo rằng việc căn cột và trích dẫn được giữ nguyên.

## Tại sao nên sử dụng GroupDocs.Editor cho việc xử lý DSV?
GroupDocs.Editor xử lý **hơn 50 định dạng đầu vào và đầu ra**, bao gồm CSV, TSV và các bảng tính tương thích Excel, đồng thời giữ mức sử dụng bộ nhớ dưới 10 MB cho các tệp lên tới 500 MB. Nó cũng tự động giữ nguyên việc căn cột, quy tắc trích dẫn và mã hoá tùy chỉnh, loại bỏ nhu cầu viết logic phân tích thủ công.

## Yêu cầu trước
Trước khi chúng ta bắt đầu, hãy chắc chắn rằng bạn đã cài đặt các thành phần sau:

- **Visual Studio** (bất kỳ phiên bản gần đây nào) – bạn sẽ phát triển và gỡ lỗi trực tiếp trong IDE.
- **GroupDocs.Editor for .NET** – tải gói mới nhất **[here](https://releases.groupdocs.com/editor/net/)**.
- **Kiến thức cơ bản về C#** – hướng dẫn giả định bạn có thể tạo một dự án console hoặc ASP.NET và thêm các gói NuGet.

## Nhập không gian tên
`Editor`, `EditableDocument`, và các lớp tùy chọn nằm trong không gian tên `GroupDocs.Editor`.  
Lớp `DelimitedTextEditOptions` là điểm vào để định nghĩa dấu phân cách (dấu phẩy, tab, v.v.) và các quy tắc phân tích khác.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Cách tạo tài liệu có thể chỉnh sửa từ tệp CSV?
Tải tệp CSV nguồn bằng `Editor` và gọi phương thức `Edit`, truyền vào một thể hiện `DelimitedTextEditOptions` chỉ định dấu phân cách là dấu phẩy. Phương thức này trả về một `EditableDocument` mà bạn có thể thao tác trong bộ nhớ. Mô hình hai bước này—load → edit—đáp ứng các kịch bản **read delimited text C#** và đảm bảo cấu trúc tệp gốc được giữ nguyên.

## Bước 1: Lấy Đường dẫn tới Tệp DSV Đầu vào
Đầu tiên, bạn cần chỉ định đường dẫn tuyệt đối hoặc tương đối tới tệp DSV nguồn. Để minh họa, chúng ta sẽ sử dụng một tệp CSV đơn giản nằm trong thư mục `Data` của dự án.

```csharp
string inputFilePath = "Your Sample Document";
```

## Bước 2: Tạo một Thể hiện Editor
`Editor` là lớp cốt lõi điều phối việc tải, chỉnh sửa và lưu. Tạo một thể hiện của nó bằng một đối tượng `FileInfo` sẽ cho bạn kiểm soát đầy đủ vòng đời của tệp.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Bước 3: Tạo Tùy chọn Chỉnh sửa DSV
`DelimitedTextEditOptions` cho biết trình chỉnh sửa cách diễn giải tệp. Bạn có thể đặt dấu phân cách, liệu hàng đầu tiên có chứa tiêu đề hay không, và mã hoá ký tự.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Bước 4: Tạo Thể hiện EditableDocument
`EditableDocument` đại diện cho một phiên bản có thể thay đổi trong bộ nhớ của tệp nguồn. Gọi `Editor.Edit` với các tùy chọn sẽ trả về một `EditableDocument`. Đối tượng này chứa văn bản của tệp trong một chuỗi có thể thay đổi, sẵn sàng cho bất kỳ thao tác **parse delimited values C#** nào bạn cần.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Bước 5: Chỉnh sửa Nội dung Tài liệu
`GetDocumentText()` trả về văn bản hiện tại của tài liệu có thể chỉnh sửa dưới dạng chuỗi. Lấy văn bản gốc bằng `EditableDocument.GetDocumentText()`, thực hiện các sửa đổi của bạn (ví dụ: thay thế giá trị cột), và lưu kết quả vào một chuỗi mới. Đây là nơi bạn **edit CSV .NET** mà không cần chạm tới các luồng tệp cấp thấp.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Bước 6: Tạo EditableDocument với Nội dung Đã Cập nhật
Đóng gói chuỗi đã sửa đổi lại thành một `EditableDocument`. Bước này hoàn thiện các thay đổi và chuẩn bị đối tượng để lưu dưới bất kỳ định dạng nào được hỗ trợ.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Bước 7: Tạo Tùy chọn Lưu CSV
`DelimitedTextSaveOptions` chỉ định cách ghi nội dung đã chỉnh sửa trở lại tệp CSV. Khi bạn sẵn sàng lưu các thay đổi, cấu hình `DelimitedTextSaveOptions`. Bạn có thể chỉ định cùng dấu phân cách, một dấu khác, hoặc thậm chí thay đổi kiểu kết thúc dòng.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Bước 8: Tạo Tùy chọn Lưu TSV
Nếu bạn cần một phiên bản tách bằng tab, chỉ cần chuyển dấu phân cách thành `\t`. Cùng một `EditableDocument` có thể được lưu nhiều lần với các tùy chọn khác nhau.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Bước 9: Tạo Tùy chọn Lưu Bảng tính
`SpreadsheetSaveOptions` cấu hình xuất tài liệu sang các định dạng tương thích Excel như .xlsx. GroupDocs.Editor cũng cho phép bạn xuất dữ liệu đã chỉnh sửa sang định dạng tương thích Excel (`.xlsx`). Lớp `SpreadsheetSaveOptions` tự động xử lý các loại cột, công thức và kiểu dáng ô.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Bước 10: Chuẩn bị Đường dẫn Lưu
Xác định các đường dẫn đầu ra riêng biệt cho mỗi định dạng. Sử dụng quy tắc đặt tên rõ ràng (ví dụ: `output.csv`, `output.tsv`, `output.xlsx`) giúp dự án của bạn được tổ chức tốt.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Bước 11: Lưu Tài liệu Đã Chỉnh sửa
`Save()` ghi tài liệu ra đĩa bằng các tùy chọn lưu đã cung cấp. Gọi `EditableDocument.Save` với các tùy chọn phù hợp cho mỗi định dạng đích. API ghi tệp trực tiếp ra đĩa, giữ nguyên mã hoá gốc trừ khi bạn ghi đè.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Bước 12: Giải phóng Các Thể hiện EditableDocument
Cả `Editor` và `EditableDocument` đều triển khai `IDisposable`. Giải phóng chúng sẽ giải phóng các handle tệp và tài nguyên không quản lý, điều này rất quan trọng khi xử lý nhiều tệp trong một công việc batch.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Các vấn đề thường gặp và giải pháp
| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|----------------|-----|
| **Dấu ngoặc kép thừa không mong muốn** | Trình phân tích CSV mặc định có thể coi dấu phẩy nhúng là dấu phân cách. | Đặt `EscapeMode = EscapeMode.DoubleQuote` trong `DelimitedTextEditOptions`. |
| **Tăng đột biến bộ nhớ khi xử lý tệp lớn** | Tải tệp 500 MB mà không sử dụng streaming. | Sử dụng `Editor.Load` với `LoadOptions` cho phép tải lười (lazy loading). |
| **Không khớp mã hoá** | Tệp nguồn sử dụng UTF‑16 nhưng các tùy chọn mặc định là UTF‑8. | Đặt rõ ràng `Encoding = Encoding.Unicode` trong các tùy chọn lưu. |

## Câu hỏi thường gặp

**Q: Tôi có thể sử dụng GroupDocs.Editor cho .NET để chỉnh sửa các tệp CSV lớn không?**  
A: Có, API streaming dữ liệu và có thể xử lý các tệp lớn hơn 1 GB mà không tải toàn bộ tài liệu vào bộ nhớ.

**Q: GroupDocs.Editor cho .NET có hỗ trợ các định dạng DSV khác ngoài CSV và TSV không?**  
A: Chắc chắn – bất kỳ dấu phân cách một ký tự nào (ví dụ: pipe `|`, dấu chấm phẩy `;`) đều được hỗ trợ miễn là bạn chỉ định nó trong `DelimitedTextEditOptions`.

**Q: Có thể tùy chỉnh mã hoá khi lưu các tệp DSV không?**  
A: Có, bạn có thể đặt thuộc tính `Encoding` trong `DelimitedTextSaveOptions` thành UTF‑8, UTF‑16, ISO‑8859‑1, hoặc bất kỳ .NET `Encoding` nào bạn cần.

**Q: Tôi có thể chuyển đổi tệp CSV sang bảng tính Excel bằng GroupDocs.Editor cho .NET không?**  
A: Có – sau khi chỉnh sửa, chỉ cần sử dụng `SpreadsheetSaveOptions` để xuất nội dung dưới dạng workbook `.xlsx`.

**Q: Tôi có thể tìm tài liệu chi tiết hơn về GroupDocs.Editor cho .NET ở đâu?**  
A: Các tham chiếu API chi tiết và mẫu mã có sẵn **[here](https://tutorials.groupdocs.com/editor/net/)**.

---

**Cập nhật lần cuối:** 2026-06-06  
**Kiểm tra với:** GroupDocs.Editor 23.10 for .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Hướng dẫn chỉnh sửa tài liệu Văn bản thuần và DSV cho GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Thành thạo GroupDocs.Editor .NET để chỉnh sửa và chuyển đổi tài liệu CSV hiệu quả](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Thành thạo việc tải tài liệu trong .NET với GroupDocs.Editor: Hướng dẫn toàn diện](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)