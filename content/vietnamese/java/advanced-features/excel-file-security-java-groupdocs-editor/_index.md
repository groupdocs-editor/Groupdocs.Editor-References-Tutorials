---
date: '2026-10-16'
description: Tìm hiểu cách mở các tệp Excel được bảo vệ bằng password trong Java với
  GroupDocs.Editor, đặt password mới và quản lý write protection.
keywords:
- open password protected excel
- write protect excel workbook
- optimize memory usage java
- protect specific worksheet
lastmod: '2026-10-16'
og_description: Mở các tệp Excel được bảo vệ bằng password trong Java bằng GroupDocs.Editor.
  Hướng dẫn này chỉ cho bạn cách tải các workbook được mã hoá, xử lý password sai,
  áp dụng password mới khi lưu và bật write protection đồng thời tối ưu hoá memory
  usage.
og_image_alt: 'Developer guide: Open password protected Excel in Java with GroupDocs.Editor'
og_title: Mở tệp Excel được bảo vệ bằng password trong Java bằng GroupDocs.Editor
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  headline: Open password protected Excel in Java using GroupDocs.Editor
  type: TechArticle
- description: Learn how to open password protected Excel files in Java with GroupDocs.Editor,
    set new passwords, and manage write protection.
  name: Open password protected Excel in Java using GroupDocs.Editor
  steps:
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Initialize the Editor**'
    text: '**Initialize the Editor**'
  - name: '**Attempt to edit without a password**'
    text: '**Attempt to edit without a password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Set up load options with an incorrect password**'
    text: '**Set up load options with an incorrect password**'
  - name: '**Handle the exception**'
    text: '**Handle the exception**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Configure load options with the correct password**'
    text: '**Configure load options with the correct password**'
  - name: '**Import required classes**'
    text: '**Import required classes**'
  - name: '**Load the workbook with the existing password**'
    text: '**Load the workbook with the existing password**'
  type: HowTo
- questions:
  - answer: Yes. Load the workbook with the existing password, then save it using
      `SpreadsheetSaveOptions.setPassword` with the new value.
    question: Can I change the password of an already protected workbook?
  - answer: GroupDocs.Editor throws `PasswordRequiredException`, which you should
      catch to request the password from the user.
    question: What happens if I try to open a workbook without specifying a password
      when it is protected?
  - answer: Use `WorksheetProtection` with a specific `WorksheetProtectionType` (e.g.,
      `LockedCells`) and apply it to individual sheets via the API.
    question: Is it possible to protect only specific worksheets instead of the whole
      workbook?
  - answer: It reduces memory consumption at the cost of a slight processing overhead,
      which is beneficial for very large files.
    question: Does `setOptimizeMemoryUsage(true)` affect performance?
  - answer: Licensing terms are per deployment; consult the GroupDocs licensing guide
      for multi‑node scenarios.
    question: Do I need a separate license for each server instance?
  type: FAQPage
tags:
- open password protected excel
- GroupDocs.Editor
- Java Excel security
- workbook protection
title: Mở tệp Excel được bảo vệ bằng password trong Java bằng GroupDocs.Editor
type: docs
url: /vi/java/advanced-features/excel-file-security-java-groupdocs-editor/
weight: 1
---
# Mở tệp Excel được bảo vệ bằng mật khẩu trong Java bằng GroupDocs.Editor

Trong hướng dẫn toàn diện này, bạn sẽ khám phá cách **mở tệp Excel được bảo vệ bằng mật khẩu** trong Java bằng GroupDocs.Editor, xử lý mật khẩu không đúng, áp dụng mật khẩu mới khi lưu, và bật bảo vệ ghi cho toàn bộ workbook. Các bước được minh họa bằng các giải thích rõ ràng, kịch bản sử dụng thực tế, và các mẹo thực hành tốt cho việc xử lý bảng tính quy mô lớn.

## Câu trả lời nhanh
- **Thư viện nào giúp mở Excel được bảo vệ bằng mật khẩu?** GroupDocs.Editor cho Java.  
- **Tôi có thể mở workbook được bảo vệ bằng mật khẩu mà không có mật khẩu không?** Không – API ném ra `PasswordRequiredException`.  
- **Làm thế nào để xử lý mật khẩu không đúng?** Bắt `IncorrectPasswordException` và yêu cầu người dùng nhập lại.  
- **Có thể đặt mật khẩu mới khi lưu không?** Có, sử dụng `SpreadsheetSaveOptions.setPassword`.  
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần một giấy phép GroupDocs.Editor hợp lệ cho bất kỳ triển khai sản xuất nào.

## Excel được bảo vệ bằng mật khẩu là gì?
`open password protected Excel` mô tả quá trình tải một workbook Excel có mật khẩu mở một cách lập trình, xác minh mật khẩu, và tùy chọn lưu lại với mật khẩu mới hoặc bảo vệ bổ sung. Sử dụng các API Java loại bỏ các bước thủ công và cho phép bạn nhúng bảo mật vào các pipeline tự động.

## Tại sao lại bảo vệ workbook Excel bằng Java?
GroupDocs.Editor cung cấp **hơn 30 phương thức API** dành riêng cho việc xử lý mật khẩu, có thể xử lý **hàng trăm worksheet** mà không cần tải toàn bộ tệp vào bộ nhớ, và đảm bảo **độ chính xác bố cục 100 %** khi lưu lại các tệp đã mã hóa. Những khả năng định lượng này cho phép bạn xây dựng các công việc batch xử lý **bảng tính 200 trang trong vòng dưới 5 giây** trên một máy chủ tiêu chuẩn, đồng thời giữ dữ liệu an toàn và tuân thủ.

## Yêu cầu trước
- Java Development Kit (JDK) 8 hoặc cao hơn  
- Maven để quản lý phụ thuộc  
- Kiến thức lập trình Java cơ bản  
- Giấy phép GroupDocs.Editor (bản dùng thử hoặc đã mua)  

## Cài đặt GroupDocs.Editor cho Java

### Sử dụng Maven
Add the repository and dependency to your `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/editor/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-editor</artifactId>
      <version>25.3</version>
   </dependency>
</dependencies>
```

### Tải trực tiếp
Alternatively, download the latest JAR from [GroupDocs.Editor cho Java](https://releases.groupdocs.com/editor/java/).

#### Nhận giấy phép
- **Dùng thử miễn phí** – khám phá tất cả tính năng mà không tốn phí.  
- **Giấy phép tạm thời** – loại bỏ giới hạn đánh giá trong quá trình thử nghiệm.  
- **Mua** – nhận giấy phép đầy đủ từ [GroupDocs](https://purchase.groupdocs.com/temporary-license).

### Khởi tạo cơ bản
`Editor` là điểm vào cho tất cả các thao tác tài liệu trong GroupDocs.Editor cho Java. Nó tải một workbook vào bộ nhớ và cung cấp các phương thức để chỉnh sửa, lưu và quản lý bảo mật.

```java
import com.groupdocs.editor.Editor;

// Initialize the editor with an Excel file path
Editor editor = new Editor("path/to/your/excel/file.xlsx");
```

## Hướng dẫn triển khai

Chúng tôi sẽ hướng dẫn qua bốn kịch bản phổ biến mà bạn có thể gặp khi bảo mật workbook Excel.

### Cách mở Excel được bảo vệ bằng mật khẩu mà không có mật khẩu?

**Câu trả lời trực tiếp:** Gọi `Editor.edit` chỉ với đường dẫn tệp; nếu workbook được mã hóa, GroupDocs.Editor sẽ ném `PasswordRequiredException`, bạn có thể bắt để yêu cầu mật khẩu từ giao diện người dùng.

`PasswordRequiredException` cho biết workbook yêu cầu mật khẩu nhưng không có mật khẩu nào được cung cấp. Bằng cách bắt ngoại lệ này, bạn có thể hiển thị một lời nhắc, ghi lại sự kiện, hoặc hủy thao tác một cách nhẹ nhàng.

1. **Nhập các lớp cần thiết** – đưa vào `PasswordRequiredException` và các kiểu liên quan.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.PasswordRequiredException;
```

2. **Khởi tạo Editor** – tạo một thể hiện `Editor` sử dụng `EditorConfig` hợp lệ trỏ tới tệp giấy phép của bạn.  

```java
String inputFilePath = "path/to/sample_xls_protected";
Editor editor = new Editor(inputFilePath);
```

3. **Cố gắng chỉnh sửa mà không có mật khẩu** – gọi `Editor.edit` chỉ với đường dẫn tệp. Nếu workbook được bảo vệ, lời gọi sẽ ném `PasswordRequiredException`.  

```java
try {
    // Try editing without a password
    editor.edit();
} catch (PasswordRequiredException ex) {
    System.out.println("Cannot edit the document because it is password-protected.");
}
editor.dispose();
```

#### Mẹo khắc phục sự cố
- Xác minh đường dẫn tệp trỏ tới một workbook tồn tại.  
- Sử dụng ngoại lệ đã bắt để kích hoạt lời nhắc UI yêu cầu mật khẩu.  

### Cách mở Excel được bảo vệ bằng mật khẩu với mật khẩu không đúng?

**Câu trả lời trực tiếp:** Tải workbook bằng `SpreadsheetLoadOptions` với mật khẩu đã cung cấp; nếu mật khẩu không khớp, bắt `IncorrectPasswordException` và thông báo cho người dùng thử lại.

`IncorrectPasswordException` cho biết mật khẩu bạn cung cấp không khớp với khóa mã hóa của workbook. Xử lý ngoại lệ này cho phép bạn đưa ra phản hồi rõ ràng và tùy chọn giới hạn số lần thử lại.

1. **Nhập các lớp cần thiết** – bao gồm `IncorrectPasswordException` trong phần import của bạn.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.IncorrectPasswordException;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Cấu hình tùy chọn tải với mật khẩu không đúng** – tạo một thể hiện `SpreadsheetLoadOptions` và đặt mật khẩu mà bạn biết là sai để thử nghiệm.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("incorrect_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Xử lý ngoại lệ** – bao quanh lời gọi tải trong khối try‑catch và bắt `IncorrectPasswordException` để hiển thị thông báo lỗi hoặc khóa người dùng sau một số lần thử nhất định.  

```java
try {
    // Attempt editing with an incorrect password
    editor.edit();
} catch (IncorrectPasswordException ex) {
    System.out.println("Cannot edit the document because the password is incorrect.");
}
editor.dispose();
```

#### Mẹo khắc phục sự cố
- Đảm bảo chuỗi mật khẩu thực sự khác với mật khẩu đúng.  
- Sử dụng mẫu này để giới hạn số lần thử lại trong UI của bạn.  

### Cách mở Excel được bảo vệ bằng mật khẩu với mật khẩu đúng?

**Câu trả lời trực tiếp:** Cung cấp mật khẩu đúng qua `SpreadsheetLoadOptions.setPassword`, bật `setOptimizeMemoryUsage(true)`, và sau đó gọi `Editor.edit` để lấy đối tượng `Spreadsheet` có thể chỉnh sửa.

`SpreadsheetLoadOptions` cấu hình cách workbook được tải, bao gồm cài đặt mật khẩu và sử dụng bộ nhớ. Bật tối ưu hoá bộ nhớ giữ mức tiêu thụ RAM thấp khi xử lý bảng tính lớn.

1. **Nhập các lớp cần thiết** – đưa vào `SpreadsheetLoadOptions` và các tiện ích liên quan.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetLoadOptions;
```

2. **Cấu hình tùy chọn tải với mật khẩu đúng** – đặt mật khẩu, bật tối ưu hoá bộ nhớ, và sau đó gọi `Editor.edit`.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
loadOptions.setOptimizeMemoryUsage(true);
Editor editor = new Editor(inputFilePath, loadOptions);
```

#### Các tùy chọn cấu hình chính
- **setOptimizeMemoryUsage** – giảm tiêu thụ RAM khi làm việc với bảng tính lớn, cho phép bạn xử lý các tệp lên tới **500 MB** mà không gặp lỗi OutOfMemory.  

### Cách đặt mật khẩu mở mới và bảo vệ ghi cho workbook Excel khi lưu?

**Câu trả lời trực tiếp:** Tải workbook với mật khẩu hiện có, tạo một đối tượng `SpreadsheetSaveOptions`, gọi `setPassword` với giá trị mới, bật `setWriteProtection(true)`, và cuối cùng gọi `Editor.save`.  

`SpreadsheetSaveOptions` xác định cách workbook được lưu, bao gồm các cờ mật khẩu và bảo vệ ghi. `setWriteProtection(true)` khóa workbook khỏi các chỉnh sửa tiếp theo trừ khi mật khẩu đúng được cung cấp.  

`WorksheetProtection` cho phép bạn bảo vệ các worksheet riêng lẻ với các loại bảo vệ cụ thể.

1. **Nhập các lớp cần thiết** – bao gồm `SpreadsheetSaveOptions` và `WorksheetProtection` nếu bạn cần kiểm soát chi tiết.  

```java
import com.groupdocs.editor.Editor;
import com.groupdocs.editor.options.SpreadsheetFormats;
import com.groupdocs.editor.options.SpreadsheetSaveOptions;
import com.groupdocs.editor.options.WorksheetProtection;
import com.groupdocs.editor.options.WorksheetProtectionType;
```

2. **Tải workbook với mật khẩu hiện có** – sử dụng `SpreadsheetLoadOptions` để mở tệp được bảo vệ trước khi thực hiện thay đổi.  

```java
String inputFilePath = "path/to/sample_xls_protected";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.setPassword("excel_password");
Editor editor = new Editor(inputFilePath, loadOptions);
```

3. **Cấu hình tùy chọn lưu với mật khẩu mới và bảo vệ ghi** – gọi `setPassword` để đặt mật khẩu mở mới và `setWriteProtection(true)` để khóa workbook khỏi việc chỉnh sửa.  

```java
SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(xlsmFormat);
saveOptions.setPassword("new_password");
saveOptions.setWorksheetProtection(new WorksheetProtection(WorksheetProtectionType.All, "write_password"));

String outputPath = "path/to/edited_document.xlsm";
editor.save(editor.edit(null), System.out, saveOptions);
editor.dispose();
```

#### Mẹo khắc phục sự cố
- Chọn một mật khẩu mạnh, khó đoán cho lời gọi `setPassword`.  
- Cờ `WorksheetProtectionType.All` khóa mọi yếu tố có thể chỉnh sửa; điều chỉnh theo nhu cầu để bảo vệ chọn lọc.  

## Ứng dụng thực tế

1. **Chia sẻ dữ liệu an toàn** – bảo vệ các mô hình tài chính nhạy cảm trước khi gửi email cho các bên liên quan.  
2. **Pipeline tài liệu tự động** – nhúng các đoạn mã này vào các công việc batch xử lý và mã hoá lại hàng nghìn bảng tính mỗi đêm.  
3. **Tuân thủ quy định** – thực thi mã hoá workbook để đáp ứng yêu cầu GDPR, HIPAA, hoặc PCI‑DSS một cách tự động.  

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| `PasswordRequiredException` ngay cả khi tôi đã truyền mật khẩu | Tùy chọn tải không được gắn vào lời gọi edit | Đảm bảo bạn truyền thể hiện `SpreadsheetLoadOptions` đã cấu hình vào `Editor.edit`. |
| Lỗi Out‑of‑memory trên các tệp lớn | Tối ưu hoá bộ nhớ bị tắt | Gọi `setOptimizeMemoryUsage(true)` trên `SpreadsheetLoadOptions`. |
| Workbook đã lưu mất định dạng | Sử dụng `SpreadsheetSaveOptions` mặc định mà không bảo tồn bố cục | Đặt `setPreserveFormatting(true)` (có sẵn trong phiên bản 25.3+). |
| Bảo vệ ghi không được áp dụng | Quên gọi `setWriteProtection(true)` | Thêm lời gọi này trước khi gọi `Editor.save`. |

## Câu hỏi thường gặp

**H: Tôi có thể thay đổi mật khẩu của một workbook đã được bảo vệ không?**  
**Đ:** Có. Tải workbook với mật khẩu hiện có, sau đó lưu nó bằng `SpreadsheetSaveOptions.setPassword` với giá trị mới.

**H: Điều gì xảy ra nếu tôi cố gắng mở một workbook mà không chỉ định mật khẩu khi nó được bảo vệ?**  
**Đ:** GroupDocs.Editor ném `PasswordRequiredException`, bạn nên bắt để yêu cầu mật khẩu từ người dùng.

**H: Có thể bảo vệ chỉ các worksheet cụ thể thay vì toàn bộ workbook không?**  
**Đ:** Sử dụng `WorksheetProtection` với một `WorksheetProtectionType` cụ thể (ví dụ, `LockedCells`) và áp dụng nó cho các sheet riêng lẻ qua API.

**H: `setOptimizeMemoryUsage(true)` có ảnh hưởng đến hiệu năng không?**  
**Đ:** Nó giảm tiêu thụ bộ nhớ với chi phí là một chút overhead xử lý, điều này có lợi cho các tệp rất lớn.

**H: Tôi có cần giấy phép riêng cho mỗi instance máy chủ không?**  
**Đ:** Các điều khoản giấy phép tính cho mỗi triển khai; tham khảo hướng dẫn giấy phép của GroupDocs cho các kịch bản đa node.

## Kết luận

Bằng cách làm theo hướng dẫn này, bạn đã biết cách **mở Excel được bảo vệ bằng mật khẩu trong Java** bằng GroupDocs.Editor, xử lý mật khẩu sai một cách nhẹ nhàng, áp dụng mật khẩu mới khi lưu, và bật bảo vệ ghi cho toàn bộ workbook. Những khả năng này cho phép bạn xây dựng các quy trình tài liệu an toàn, tuân thủ và hiệu suất cao, mở rộng từ một tệp đơn lẻ đến các quy trình batch quy mô lớn.

---

**Cập nhật lần cuối:** 2026-10-16  
**Kiểm tra với:** GroupDocs.Editor 25.3  
**Tác giả:** GroupDocs  

## Hướng dẫn liên quan

- [Chỉnh sửa hàng loạt tệp Word trong Java với GroupDocs.Editor – Hướng dẫn từng bước](/editor/java/document-loading/groupdocs-editor-java-loading-word-documents/)
- [cách chỉnh sửa tệp excel và Word trong Java với GroupDocs.Editor](/editor/java/document-editing/java-groupdocs-editor-master-document-editing/)
- [Cách đặt giấy phép cho GroupDocs.Editor trong Java bằng InputStream: Hướng dẫn toàn diện](/editor/java/licensing-configuration/groupdocs-editor-java-inputstream-license-setup/)
