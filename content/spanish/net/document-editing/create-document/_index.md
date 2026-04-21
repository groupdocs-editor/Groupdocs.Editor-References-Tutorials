---
date: 2026-03-14
description: Aprenda a editar presentaciones de PowerPoint y otros tipos de documentos
  usando GroupDocs.Editor para .NET. La guía también cubre cómo guardar el documento
  editado y editar documentos Word en .NET.
linktitle: Create Document
second_title: GroupDocs.Editor .NET API
title: Editar presentación de PowerPoint con GroupDocs.Editor para .NET
type: docs
url: /es/net/document-editing/create-document/
weight: 10
---

# Editar presentación de PowerPoint con GroupDocs.Editor para .NET

## Introducción
Si buscas una manera confiable de **editar presentación de PowerPoint** de forma programática, GroupDocs.Editor para .NET es la respuesta. Esta biblioteca te permite trabajar con formatos Word, Excel, PowerPoint, Ebook y Email, todo desde una única API fácil de usar. En este tutorial recorreremos la creación y edición de cada tipo de documento compatible, te mostraremos cómo **guardar documento editado** en streams y te daremos consejos prácticos que puedes aplicar en proyectos reales.

## Respuestas rápidas
- **¿Qué biblioteca me permite editar archivos PowerPoint en .NET?** GroupDocs.Editor para .NET.  
- **¿Puedo editar archivos Word, Excel y Epub con la misma API?** Sí, la misma clase `Editor` admite todos esos formatos.  
- **¿Cómo capturo el archivo editado?** Proporciona una función de devolución de llamada (por ejemplo, `SaveNewDocument`) que recibe el stream resultante.  
- **¿Necesito una licencia para uso en producción?** Sí, compra una licencia o utiliza una licencia de prueba temporal.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.0+, .NET Core y .NET 5/6.

## ¿Qué es “editar presentación de PowerPoint” con GroupDocs.Editor?
Editar una presentación de PowerPoint significa cargar un archivo `.pptx`, aplicar cambios (como modificar diapositivas, texto o elementos ocultos) y luego obtener el archivo actualizado, todo sin necesidad de tener Microsoft Office instalado.

## ¿Por qué usar GroupDocs.Editor para .NET?
- **API única para muchos formatos** – No es necesario manejar bibliotecas distintas para Word, Excel o Epub.  
- **Sin dependencia de Office** – Funciona en servidores, contenedores y pipelines CI.  
- **Control granular** – Personaliza la paginación, la información de idioma, la extracción de fuentes y más.  
- **Procesamiento basado en streams** – Ideal para servicios en la nube donde trabajas con streams de memoria en lugar de archivos físicos.

## Requisitos previos
- Visual Studio (cualquier edición reciente).  
- .NET Framework 4.0 o superior (o .NET Core/.NET 5+).  
- Biblioteca GroupDocs.Editor para .NET – descárgala desde [aquí](https://releases.groupdocs.com/editor/net/).  
- Conocimientos básicos de C#.

## Importar espacios de nombres
Primero, importa los espacios de nombres que contienen las clases principales que utilizaremos.

```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```

## Paso 1: Configurar el stream
Usaremos un memory stream como marcador de posición para el contenido del documento.

```csharp
Stream memoryStream = Stream.Null;
```

## Paso 2: Función de devolución de llamada para **guardar documento editado**
Define una devolución de llamada que reciba el stream editado y lo almacene en `memoryStream`.

```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```

## Paso 3: Crear y editar un documento WordProcessing  
(Aquí **editamos documento Word .net**.)

### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```

### Crear y editar con opciones personalizadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```

## Paso 4: Crear y editar un documento Spreadsheet  
(Usa esto para **editar archivo Excel .net**.)

### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```

### Crear y editar con opciones personalizadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```

## Paso 5: **Editar presentación de PowerPoint** – Creación y edición de un documento de presentación
Este es el núcleo de nuestro enfoque principal de palabras clave.

### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```

### Crear y editar con opciones personalizadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```

## Paso 6: Crear y editar un documento Ebook  
(Aquí **editamos archivo epub**.)

### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```

### Crear y editar con opciones personalizadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```

## Paso 7: Crear y editar un documento Email
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```

### Crear y editar con opciones personalizadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```

## Paso 8: Finalizar el proceso
Dispón del stream para liberar recursos una vez que hayas terminado.

```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```

## Problemas comunes y consejos
- **Nunca olvides disponer del stream** – dejarlo abierto puede provocar fugas de memoria en servicios de larga ejecución.  
- **Al editar PowerPoint, asegúrate de establecer `SlideNumber` correctamente**; de lo contrario la primera diapositiva podría duplicarse.  
- **Si necesitas conservar el nombre original del archivo**, guárdalo antes de la devolución de llamada y renombra el stream de salida después de la edición.  
- **Para documentos grandes**, considera procesarlos en fragmentos o usar `Editor` con un archivo temporal para evitar un alto consumo de memoria.

## Preguntas frecuentes

**P: ¿Qué tipos de documentos puedo editar con GroupDocs.Editor para .NET?**  
R: Puedes editar WordProcessing, hojas de cálculo, presentaciones, ebooks y correos electrónicos, incluidos los archivos PowerPoint para el caso de uso de **editar presentación de PowerPoint**.

**P: ¿Es posible personalizar las opciones de edición?**  
R: Sí, cada formato tiene su propia clase de opciones (por ejemplo, `WordProcessingEditOptions`, `SpreadsheetEditOptions`, `PresentationEditOptions`) que permite afinar la paginación, diapositivas ocultas, selección de hoja, etc.

**P: ¿Cómo manejo la salida de los documentos editados?**  
R: Utiliza la función de devolución de llamada (`SaveNewDocument`) para capturar el stream editado; luego puedes escribirlo en disco, en una base de datos o devolverlo desde una API web.

**P: ¿Necesito una licencia para usar GroupDocs.Editor para .NET?**  
R: Sí, se requiere una licencia para producción. Puedes obtener una desde [aquí](https://purchase.groupdocs.com/buy). También está disponible una licencia de prueba temporal.

**P: ¿Dónde puedo encontrar documentación más detallada?**  
R: La documentación detallada está disponible en la [página de documentación de GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).

## Conclusión
GroupDocs.Editor para .NET facilita **editar presentación de PowerPoint** y una amplia gama de otros tipos de documentos. Siguiendo los pasos anteriores puedes crear, modificar y **guardar documento editado** en streams totalmente mediante código, sin depender de instalaciones de Office. Explora las opciones avanzadas de la biblioteca para adaptar la experiencia de edición a las necesidades específicas de tu negocio.

---

**Última actualización:** 2026-03-14  
**Probado con:** GroupDocs.Editor para .NET (última versión)  
**Autor:** GroupDocs