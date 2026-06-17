---
date: 2026-06-01
description: Aprende cómo obtener el recuento de páginas y extraer los metadatos del
  documento usando GroupDocs.Editor para .NET en un tutorial detallado paso a paso.
keywords:
- get page count
- extract document metadata
- get document info
- find document extension
- retrieve document size
linktitle: Obtener recuento de páginas y extraer información del documento
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to get page count and extract document metadata using GroupDocs.Editor
    for .NET in a detailed step‑by‑step tutorial.
  headline: Get Page Count & Extract Document Info with GroupDocs.Editor
  type: TechArticle
- questions:
  - answer: GroupDocs.Editor supports Word processing, spreadsheet, presentation,
      PDF, and plain‑text files—over 50 formats in total.
    question: What document types can I extract metadata from?
  - answer: Access `DocumentInfo.Extension` after calling `GetDocumentInfo()`; it
      returns the extension without the leading dot.
    question: How do I retrieve the file extension?
  - answer: Yes—`DocumentInfo.Size` returns the size in bytes; divide by 1,048,576
      to convert to megabytes.
    question: Can I get the size of a document in megabytes?
  - answer: Absolutely—GroupDocs.Editor never writes the password to disk and disposes
      of all cryptographic objects after use.
    question: Is it safe to process password‑protected files on a server?
  - answer: You can get support from the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find additional help if I run into issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Obtener recuento de páginas y extraer información del documento con GroupDocs.Editor
type: docs
url: /es/net/document-processing/extract-document-info/
weight: 10
---

# Obtener recuento de páginas y extraer información del documento con GroupDocs.Editor

## Introducción
En este tutorial completo aprenderá a **obtener el recuento de páginas** y extraer información detallada del documento—incluido el formato, tamaño y estado de cifrado—usando GroupDocs.Editor para .NET. Ya sea que esté construyendo un sistema de gestión de documentos, un motor de informes o una canalización de conversión automatizada, comprender los metadatos de un archivo es el primer paso para un procesamiento fiable. Recorramos todo el flujo de trabajo, desde cargar un archivo hasta liberar los recursos de forma segura.

## Respuestas rápidas
- **¿Cómo obtengo el recuento de páginas de un documento?**  
  Llame a `editor.GetDocumentInfo().PageCount` después de cargar el archivo con `Editor`.
- **¿Qué formatos de archivo son compatibles para la extracción de metadatos?**  
  Más de 50 formatos, incluidos DOCX, XLSX, PPTX, PDF, TXT y HTML.
- **¿Puedo extraer metadatos de archivos protegidos con contraseña?**  
  Sí—proporcione la contraseña al crear la instancia de `Editor`.
- **¿Necesito liberar recursos manualmente?**  
  Absolutamente; siempre llame a `editor.Dispose()` o envuelva el editor en un bloque `using`.
- **¿Qué versión de GroupDocs.Editor se requiere?**  
  La última versión estable (v23.12+ al momento de escribir) admite todas las funciones mostradas.

## ¿Qué es “obtener recuento de páginas” en GroupDocs.Editor?
`GetDocumentInfo()` es un método que devuelve un objeto `DocumentInfo` que contiene el recuento de páginas del documento, formato, tamaño y otros metadatos. Esta única llamada le brinda información inmediata sin analizar el archivo manualmente. Al usar este método evita cargar todo el documento en memoria, lo que mejora el rendimiento especialmente para archivos grandes y reduce el consumo de recursos del servidor.

## ¿Por qué extraer metadatos del documento con GroupDocs.Editor?
GroupDocs.Editor puede procesar **más de 50 formatos de entrada y salida** y recuperar metadatos para archivos de hasta **2 GB** sin cargar todo el documento en memoria. Esta eficiencia reduce la carga del servidor hasta en **un 70 %** comparado con el análisis completo del documento, lo que lo hace ideal para aplicaciones de alto rendimiento.

## Requisitos previos
Antes de comenzar, asegúrese de tener:

- **Conceptos básicos de desarrollo en C#** – debe sentirse cómodo con Visual Studio y la estructura de proyectos .NET.
- **Visual Studio 2022** (o cualquier versión reciente) instalado en su máquina.
- **GroupDocs.Editor para .NET** – descargue el paquete más reciente desde la [página de descarga](https://releases.groupdocs.com/editor/net/).

## ¿Cómo cargar su documento?
`Editor` es la clase principal que representa un documento y proporciona métodos para cargarlo y manipularlo. Cargue el archivo objetivo creando una instancia de `Editor` y pasando la ruta del archivo. El editor detecta automáticamente el formato, por lo que no necesita especificar opciones de carga. Este enfoque funciona para cualquier tipo de archivo compatible y simplifica la configuración inicial.

```csharp
using System;
using GroupDocs.Editor.Metadata;
```

## ¿Cómo obtener la información del documento?
`GetDocumentInfo()` devuelve un objeto `DocumentInfo` que contiene metadatos como recuento de páginas, formato, tamaño y estado de cifrado. Después de cargar, llame a este método para obtener el objeto. El `DocumentInfo` devuelto le brinda una instantánea concisa de las características del archivo, permitiéndole tomar decisiones sin procesamiento adicional.

```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```

## ¿Cómo determinar el tipo de documento?
`DocumentType` es un enum que indica si el documento es WordProcessing, Spreadsheet o Text. Saber si un archivo es un documento de procesamiento de texto, hoja de cálculo o texto plano influye en cómo lo maneja posteriormente. Use la propiedad `DocumentType` del objeto `DocumentInfo` para tomar esta decisión y ramificar su lógica en consecuencia.

```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```

## ¿Cómo extraer información detallada para archivos de procesamiento de texto?
`WordProcessing` se refiere a documentos como DOCX, ODT y RTF manejados como archivos de procesamiento de texto. Si el tipo de documento es `WordProcessing`, puede leer propiedades adicionales como **formato**, **extensión**, **recuento de páginas**, **tamaño** y **bandera de cifrado** directamente del objeto `DocumentInfo`. Estos detalles le ayudan a adaptar los pasos de procesamiento, como aplicar conversiones específicas o verificaciones de seguridad.

```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```

## ¿Cómo manejar documentos de hoja de cálculo y textuales?
`Spreadsheet` denota archivos de hoja de cálculo como XLSX, mientras que `Text` representa documentos de texto plano. Para hojas de cálculo (`Spreadsheet`) y archivos de texto plano (`Text`), el objeto `DocumentInfo` sigue proporcionando metadatos básicos (extensión, tamaño, recuento de páginas). Algunos formatos pueden no exponer un recuento de páginas; en ese caso el valor será `0`. Aún puede confiar en otros metadatos para la lógica posterior.

```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## ¿Cómo trabajar con documentos protegidos con contraseña?
`Password` es una cadena que se pasa al constructor de `Editor` para abrir archivos cifrados. Cuando un documento está cifrado, primero intente abrirlo sin contraseña. Si falla, capture la excepción y vuelva a intentarlo con la contraseña correcta. El constructor de `Editor` acepta un parámetro `Password` para este propósito, lo que permite manejar archivos protegidos de forma fluida.

```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## ¿Cómo procesar documentos basados en texto?
`DocumentInfo` proporciona metadatos básicos como tamaño, extensión y codificación para archivos de texto. Los archivos de texto (p. ej., `.txt`, `.md`) se tratan como flujos simples. Aún puede obtener información de tamaño y codificación desde `DocumentInfo`, lo cual es útil para validar la integridad del archivo o determinar la canalización de procesamiento adecuada.

```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```

## ¿Cómo liberar recursos correctamente?
`Editor` es la clase principal que posee recursos no administrados y debe ser liberada después de su uso. Para evitar fugas de memoria, siempre libere la instancia de `Editor` después de terminar de extraer la información. La instrucción `using` es el patrón más seguro porque garantiza la liberación incluso si ocurre una excepción, asegurando una gestión limpia de los recursos.

```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| **PageCount devuelve 0** | El formato no admite paginación (p. ej., texto plano) | Verifique `DocumentInfo.DocumentType` antes de confiar en `PageCount`. |
| **Formato de archivo no compatible** | Extensión de archivo no reconocida | Verifique que el archivo sea uno de los más de 50 formatos compatibles; actualice GroupDocs.Editor a la última versión. |
| **Excepción de contraseña** | Contraseña incorrecta suministrada | Capture `PasswordProtectedException` y solicite al usuario que vuelva a ingresar la contraseña. |
| **Pico de memoria en archivos grandes** | Cargar PDFs muy grandes sin transmisión | Utilice `LoadOptions` con `LoadOptions.LoadMode = LoadMode.Stream` (disponible en versiones más recientes). |

## Preguntas frecuentes

**P: ¿De qué tipos de documentos puedo extraer metadatos?**  
R: GroupDocs.Editor admite archivos de procesamiento de texto, hoja de cálculo, presentación, PDF y texto plano—más de 50 formatos en total.

**P: ¿Cómo obtengo la extensión del archivo?**  
R: Acceda a `DocumentInfo.Extension` después de llamar a `GetDocumentInfo()`; devuelve la extensión sin el punto inicial.

**P: ¿Puedo obtener el tamaño de un documento en megabytes?**  
R: Sí—`DocumentInfo.Size` devuelve el tamaño en bytes; divida por 1,048,576 para convertir a megabytes.

**P: ¿Es seguro procesar archivos protegidos con contraseña en un servidor?**  
R: Absolutamente—GroupDocs.Editor nunca escribe la contraseña en disco y elimina todos los objetos criptográficos después de su uso.

**P: ¿Dónde puedo encontrar ayuda adicional si tengo problemas?**  
R: Puede obtener soporte en el [foro de soporte de GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

---

**Última actualización:** 2026-06-01  
**Probado con:** GroupDocs.Editor 23.12 para .NET  
**Autor:** GroupDocs

```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```

## Tutoriales relacionados

- [Dominio de la extracción de metadatos en .NET con GroupDocs.Editor: Guía completa](/editor/net/advanced-features/groupdocs-editor-net-metadata-extraction-guide/)
- [Tutoriales de carga de documentos con GroupDocs.Editor para .NET](/editor/net/document-loading/)
- [Edición eficiente de documentos con GroupDocs.Editor .NET: Transformar HTML en documentos editables](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)