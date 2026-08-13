---
date: 2026-06-06
description: Tìm hiểu cách liệt kê các định dạng tài liệu được hỗ trợ và xác định
  phần mở rộng định dạng tệp bằng GroupDocs.Editor cho .NET. Hướng dẫn từng bước với
  các đoạn mã, câu trả lời nhanh và câu hỏi thường gặp.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Liệt kê các định dạng tài liệu được hỗ trợ
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Liệt kê các định dạng tài liệu được hỗ trợ với GroupDocs.Editor .NET
type: docs
url: /vi/net/document-processing/work-document-formats/
weight: 13
---

# Liệt kê các định dạng tài liệu được hỗ trợ

Welcome to our comprehensive tutorial on **cách liệt kê các định dạng tài liệu được hỗ trợ** with GroupDocs.Editor for .NET. Whether you’re building a document‑centric web app or an enterprise‑grade desktop tool, knowing exactly which formats you can edit or convert is essential. In this guide you’ll discover how to enumerate formats, parse extensions, and edit documents—all with clear, human‑friendly explanations and ready‑to‑run code snippets.

## Câu trả lời nhanh
- **Làm thế nào để liệt kê tất cả các định dạng được hỗ trợ?** Use `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (or the Presentation/Spreadsheet equivalents) and iterate the collection.  
- **Tôi có thể xác định định dạng từ phần mở rộng tệp không?** Yes—call `DocumentFormatInfo.FromExtension(".docx")`.  
- **Các loại tệp nào mà GroupDocs.Editor hỗ trợ?** Over 30 input and output formats, including DOCX, XLSX, PPTX, HTML, and plain text.  
- **Tôi có cần giấy phép để liệt kê các định dạng không?** A temporary license unlocks the full API; otherwise a trial works with limited features.  
- **Phiên bản .NET nào tương thích?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## “Liệt kê các định dạng tài liệu được hỗ trợ” là gì
The phrase refers to programmatically retrieving the collection of file types that GroupDocs.Editor can open, edit, and save. This operation lets you build dynamic UI dropdowns or validate user uploads before processing, ensuring that only compatible files are passed to the editor for further manipulation.

## Tại sao cần liệt kê các định dạng tài liệu được hỗ trợ
GroupDocs.Editor **hỗ trợ hơn 30 định dạng đầu vào và đầu ra** và có thể xử lý các tệp lên tới **2 GB** mà không cần tải toàn bộ tài liệu vào bộ nhớ. Biết danh sách chính xác giúp ngăn ngừa lỗi thời gian chạy, cải thiện trải nghiệm người dùng và cho phép bạn thực thi các quy tắc kinh doanh như “chỉ cho phép các tài liệu Office có thể chỉnh sửa”. Nó cũng giúp bạn chỉ hiển thị cho người dùng những định dạng mà ứng dụng thực sự hỗ trợ.

## Yêu cầu trước
1. **.NET development environment** – Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ .NET 6+.  
2. **GroupDocs.Editor for .NET library** – download from the [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
3. **Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/) for unrestricted access.  
4. **Basic C# knowledge** – familiarity with namespaces, `using` statements, and console output.

## Cách liệt kê các định dạng tài liệu được hỗ trợ?
Load the supported formats collection and print each format’s name and file extension. This two‑step pattern works for Word Processing, Spreadsheet, and Presentation documents. By iterating the collection you can dynamically populate UI elements such as dropdowns, ensuring users can only select formats that the editor can actually handle.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Liệt kê các định dạng Word Processing
`Formats.WordProcessingFormats` là một enumeration mô tả mọi loại tệp Word‑processing mà trình chỉnh sửa nhận dạng. Thuộc tính `All` trả về một collection các đối tượng định dạng này.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Giải thích:**  
1. **Loop Through Formats:** Chúng tôi lặp qua tất cả các định dạng Word‑processing có sẵn.  
2. **Output Format Details:** Đối với mỗi định dạng, chúng tôi in ra tên thân thiện và phần mở rộng mặc định.

### Liệt kê các định dạng Presentation
`Formats.PresentationFormats` hoạt động tương tự cho các tệp slide‑deck, hiển thị mỗi loại presentation được hỗ trợ thông qua collection `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Giải thích:**  
1. **Loop Through Formats:** Logic lặp tương tự áp dụng cho các presentation.  
2. **Output Format Details:** Tên và phần mở rộng được hiển thị cho mỗi định dạng.

## Cách xác định phần mở rộng định dạng tệp?
Đôi khi bạn chỉ có tên tệp và cần suy ra `DocumentFormat` tương ứng. GroupDocs.Editor cung cấp một helper tĩnh đơn giản để ánh xạ phần mở rộng tệp tới đại diện định dạng nội bộ, cho phép bạn xác thực hoặc chuyển đổi tệp trước khi tải chúng vào trình chỉnh sửa.

### Phân tích các định dạng Spreadsheet
`Formats.SpreadsheetFormats.FromExtension` chuyển một chuỗi phần mở rộng tệp thành giá trị enum định dạng spreadsheet tương ứng.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Giải thích:**  
1. **Parse Format:** `FromExtension` chuyển phần mở rộng `.xlsm` thành enum `SpreadsheetFormat` nội bộ.  
2. **Output Format:** Tên của định dạng đã phân tích được in ra, xác nhận việc ánh xạ.

### Phân tích các định dạng Textual
Tương tự, `Formats.TextualFormats.FromExtension` giải quyết các phần mở rộng tệp văn bản như HTML hoặc TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Giải thích:**  
1. **Parse Format:** Phương thức `FromExtension` giải quyết phần mở rộng `html` thành một `TextFormat`.  
2. **Output Format:** Tên của định dạng văn bản được hiển thị, hữu ích cho các trình chỉnh sửa dựa trên web.

## Cách chỉnh sửa tài liệu sau khi xác định định dạng?
Khi đã biết định dạng, việc tải và chỉnh sửa tài liệu tuân theo một mẫu nhất quán. Đầu tiên bạn tạo một thể hiện `Editor` với đường dẫn tới tệp nguồn, sau đó gọi `Edit()` để lấy một `EditableDocument`. Từ đó bạn có thể đọc, sửa đổi và cuối cùng lưu nội dung bằng `SaveOptions` phù hợp.

### Tải tài liệu
`Editor` là lớp cốt lõi bao gồm tất cả các thao tác chỉnh sửa cho một tệp nhất định.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Giải thích:**  
1. **Initialize Editor:** Tạo một thể hiện `Editor`, truyền đường dẫn đầy đủ của tệp mục tiêu.  
2. **Dispose Pattern:** Câu lệnh `using` đảm bảo tất cả tài nguyên không quản lý được giải phóng kịp thời.

### Trích xuất nội dung
`EditableDocument.GetContent()` trả về văn bản thô của tài liệu (hoặc HTML cho các trình chỉnh sửa dựa trên web), bạn có thể hiển thị hoặc thao tác.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Giải thích:**  
1. **Edit Method:** `Edit()` trả về một đối tượng `EditableDocument`.  
2. **Get Content:** `GetContent()` trích xuất văn bản thô của tài liệu (hoặc HTML cho các trình chỉnh sửa dựa trên web).  
3. **Output Content:** Nội dung được ghi ra console để xác minh.

### Lưu thay đổi
`SaveOptions` cho trình chỉnh sửa biết cách và định dạng nào để ghi tài liệu đã chỉnh sửa trở lại bộ nhớ lưu trữ.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Giải thích:**  
1. **Edit Method:** Lấy lại `EditableDocument` sau khi đã sửa đổi.  
2. **Modify Content:** Áp dụng các thay đổi của bạn vào chuỗi (không được hiển thị ở đây).  
3. **Save Options:** Cấu hình `SaveOptions` với định dạng đầu ra mong muốn.  
4. **Save Document:** Lưu tệp đã chỉnh sửa trở lại đĩa.

## Cách làm việc với các loại tài liệu khác nhau?
GroupDocs.Editor trừu tượng hoá việc xử lý Word, Spreadsheet và Presentation phía sau cùng một API, giúp dễ dàng chuyển đổi ngữ cảnh mà không cần học một bộ lớp mới cho mỗi họ tài liệu.

### Chỉnh sửa tài liệu Spreadsheet
`SpreadsheetSaveOptions` xác định cách một spreadsheet được ghi, bao gồm định dạng và các cài đặt nén tùy chọn.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xxlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Giải thích:**  
1. **Initialize Editor:** Truyền đường dẫn tệp spreadsheet vào hàm tạo `Editor`.  
2. **Edit Method:** Lấy một `EditableDocument`.  
3. **Get Content:** In ra biểu diễn CSV của spreadsheet (hoặc HTML).  
4. **Modify Content:** Áp dụng bất kỳ thay đổi nào ở mức ô mà bạn cần.  
5. **Save Options:** Chọn `SpreadsheetSaveOptions` phù hợp.  
6. **Save Document:** Ghi spreadsheet đã cập nhật trở lại bộ nhớ lưu trữ.

### Chỉnh sửa tài liệu Presentation
`PresentationSaveOptions` kiểm soát định dạng đầu ra cho các slide deck, cho phép bạn giữ nguyên hoặc thay đổi loại tệp gốc.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Giải thích:**  
1. **Initialize Editor:** Tải tệp PowerPoint bằng `Editor`.  
2. **Edit Method:** Lấy một `EditableDocument`.  
3. **Get Content:** Trích xuất HTML slide hoặc văn bản thuần.  
4. **Modify Content:** Cập nhật tiêu đề, các điểm bullet hoặc hình ảnh.  
5. **Save Options:** Sử dụng `PresentationSaveOptions` để xác định định dạng đầu ra.  
6. **Save Document:** Lưu bản trình chiếu đã chỉnh sửa.

## Các vấn đề thường gặp và giải pháp
- **“Format not supported” error:** Kiểm tra bạn đang sử dụng phiên bản GroupDocs.Editor mới nhất; nó thường xuyên thêm hỗ trợ cho các định dạng Office mới.  
- **Large file memory consumption:** Bật chế độ streaming bằng cách đặt `EditorSettings.EnableStreaming = true` trước khi tải tài liệu.  
- **License not applied:** Đảm bảo tệp giấy phép tạm thời được đặt trong thư mục gốc của ứng dụng hoặc được tải qua `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Câu hỏi thường gặp
**Q: Sự khác biệt giữa `DocumentFormatInfo` và `SaveOptions` là gì?**  
A: `DocumentFormatInfo` provides metadata about supported file types, while `SaveOptions` configures how a document is written back to disk (format, compression, etc.).

**Q: Tôi có thể liệt kê các định dạng cho một phần mở rộng tệp tùy chỉnh không?**  
A: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension isn’t recognized, the method returns `null`.

**Q: GroupDocs.Editor có hỗ trợ các tệp được bảo vệ bằng mật khẩu không?**  
A: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings` to open encrypted documents.

**Q: GroupDocs.Editor thực sự hỗ trợ bao nhiêu định dạng?**  
A: Over **30 input and output formats**, spanning Word, Excel, PowerPoint, HTML, and plain text.

**Q: Có cách nào để giới hạn danh sách chỉ còn các định dạng có thể chỉnh sửa không?**  
A: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation equivalents) to retrieve formats that allow full edit capabilities.

## Tài nguyên bổ sung
- Tải thư viện từ [GroupDocs releases page](https://releases.groupdocs.com/editor/net/).  
- Nhận một [temporary license](https://purchase.groupdocs.com/temporary-license/) để truy cập đầy đủ tính năng.  
- Dùng thử sản phẩm với một [free trial](https://releases.groupdocs.com/).  
- Khám phá các ví dụ sử dụng chi tiết trong [GroupDocs.Editor documentation](https://tutorials.groupdocs.com/editor/net/).  
- Nhận trợ giúp từ cộng đồng trên [support forum](https://forum.groupdocs.com/c/editor/20).

## Kết luận
Bằng cách làm theo hướng dẫn này, bạn đã biết cách **liệt kê các định dạng tài liệu được hỗ trợ**, **xác định định dạng tệp từ phần mở rộng của nó**, và **chỉnh sửa tài liệu** trên các loại Word, Spreadsheet và Presentation bằng GroupDocs.Editor cho .NET. Hãy tích hợp các đoạn mã này vào dự án của bạn để xây dựng các ứng dụng mạnh mẽ, nhận biết định dạng, mang lại trải nghiệm tốt cho người dùng cuối và giảm lỗi thời gian chạy.

---

**Cập nhật lần cuối:** 2026-06-06  
**Kiểm tra với:** GroupDocs.Editor 23.9 for .NET  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Làm chủ việc tải tài liệu trong .NET với GroupDocs.Editor: Hướng dẫn toàn diện](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Làm chủ việc chỉnh sửa tài liệu trong .NET với GroupDocs.Editor: Hướng dẫn toàn diện](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Chuyển đổi Word sang HTML bằng GroupDocs.Editor .NET: Hướng dẫn từng bước](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)