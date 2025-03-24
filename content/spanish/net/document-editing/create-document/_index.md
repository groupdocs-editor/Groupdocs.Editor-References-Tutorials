---
title: Crear documento
linktitle: Crear documento
second_title: API GroupDocs.Editor .NET
description: Aprenda a editar documentos de Word, Excel, PowerPoint, libros electrónicos y correo electrónico utilizando GroupDocs.Editor para .NET con este completo tutorial paso a paso.
weight: 10
url: /es/net/document-editing/create-document/
---
## Introducción
¿Está cansado de la molestia que conlleva editar diferentes tipos de documentos mediante programación? GroupDocs.Editor para .NET está aquí para simplificar el proceso. Esta poderosa herramienta permite a los desarrolladores editar varios formatos de documentos como Word, Excel, PowerPoint, libros electrónicos y correos electrónicos con facilidad. En este tutorial, profundizaremos en cómo usar GroupDocs.Editor para .NET para crear y editar documentos. Dividiremos el proceso en pasos fáciles de seguir, haciéndolo accesible incluso si eres nuevo en esto.
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
- Visual Studio instalado en su máquina.
- .NET Framework (4.0 o superior).
-  GroupDocs.Editor para la biblioteca .NET. Puedes descargarlo desde[aquí](https://releases.groupdocs.com/editor/net/).
- Conocimientos básicos de programación en C#.
## Importar espacios de nombres
Primero, importemos los espacios de nombres necesarios. Esto hará que las clases y métodos requeridos sean accesibles en nuestra aplicación.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Paso 1: configurar la transmisión
Para empezar, necesitamos configurar un flujo de memoria que actuará como nuestro marcador de posición para el contenido del documento.
```csharp
Stream memoryStream = Stream.Null;
```
## Paso 2: función de devolución de llamada para guardar el documento
A continuación, defina una función de devolución de llamada que guardará el nuevo flujo de documentos. Esta función es esencial para manejar el resultado del proceso de edición del documento.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Paso 3: crear y editar un documento de procesamiento de Word
 Ahora, creemos y editemos un documento de Word. Empezaremos creando un nuevo`Editor` instancia para documentos de WordProcessing y edítelo con las opciones predeterminadas.
### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Crear y editar con opciones personalizadas
Para tener más control, podemos especificar opciones como deshabilitar la paginación y extraer fuentes incrustadas.
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
## Paso 4: crear y editar un documento de hoja de cálculo
Del mismo modo, podemos crear y editar un documento de Excel. Así es como se hace.
### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Crear y editar con opciones personalizadas
 Para apuntar a hojas de trabajo específicas o excluir las ocultas, utilizamos`SpreadsheetEditOptions`.
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
## Paso 5: crear y editar un documento de presentación
También se admiten presentaciones de PowerPoint. Veamos cómo manejarlos.
### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Crear y editar con opciones personalizadas
Puede personalizar sus ediciones especificando opciones como qué diapositiva mostrar y si incluir diapositivas ocultas.
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
## Paso 6: creación y edición de un documento de libro electrónico
GroupDocs.Editor también permite editar formatos de libros electrónicos como EPUB. Así es como puedes manejarlo.
### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Crear y editar con opciones personalizadas
Personalice la edición de su libro electrónico habilitando o deshabilitando la información de paginación e idioma.
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
## Paso 7: crear y editar un documento de correo electrónico
Finalmente, veremos cómo editar documentos de correo electrónico. Esto incluye formatos como EML.
### Crear y editar con opciones predeterminadas
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Crear y editar con opciones personalizadas
Especifique las opciones de salida de mensajes de correo para controlar el proceso de edición.
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
Después de editar los documentos, es fundamental deshacerse del flujo de memoria correctamente para liberar recursos.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusión
GroupDocs.Editor para .NET es una herramienta versátil y poderosa que puede simplificar la tarea de editar varios tipos de documentos mediante programación. Si sigue esta guía paso a paso, podrá crear y editar documentos con facilidad, ya sean archivos de WordProcessing, hojas de cálculo, presentaciones, libros electrónicos o correos electrónicos. Sumérgete en la documentación de GroupDocs.Editor para conocer funciones más avanzadas y opciones de personalización.
## Preguntas frecuentes
### ¿Qué tipos de documentos puedo editar con GroupDocs.Editor para .NET?
Puede editar una amplia gama de documentos, incluidos WordProcessing, hojas de cálculo, presentaciones, libros electrónicos y correos electrónicos.
### ¿Es posible personalizar las opciones de edición?
Sí, GroupDocs.Editor para .NET permite una amplia personalización a través de varias opciones de edición específicas para cada tipo de documento.
### ¿Cómo manejo la salida de los documentos editados?
Puede utilizar una función de devolución de llamada para guardar el flujo de documentos editados en la ubicación deseada.
### ¿Necesito una licencia para utilizar GroupDocs.Editor para .NET?
 Sí, puede obtener una licencia de[aquí](https://purchase.groupdocs.com/buy). También existe la opción de una licencia temporal.
### ¿Dónde puedo encontrar documentación más detallada?
 La documentación detallada está disponible en el[Página de documentación de GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).