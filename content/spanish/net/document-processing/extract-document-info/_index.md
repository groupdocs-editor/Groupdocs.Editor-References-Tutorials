---
title: Extraer información del documento
linktitle: Extraer información del documento
second_title: API GroupDocs.Editor .NET
description: Aprenda a extraer información de documentos utilizando GroupDocs.Editor para .NET con nuestro tutorial detallado paso a paso. Perfecto para gestionar varios tipos de documentos.
weight: 10
url: /es/net/document-processing/extract-document-info/
---
## Introducción
Bienvenido a este tutorial completo sobre cómo extraer información de documentos usando GroupDocs.Editor para .NET. En esta guía, lo guiaremos a través del proceso paso a paso, asegurándonos de que comprenda cada parte de manera clara y concisa. Si es un desarrollador experimentado o recién está comenzando, este tutorial lo ayudará a integrar sin problemas GroupDocs.Editor en sus proyectos .NET para administrar y manipular documentos de manera eficiente.
## Requisitos previos
Antes de profundizar en el código, asegurémonos de tener todo lo que necesita:
- Conocimientos básicos de C#: comprender los conceptos básicos de la programación en C# es esencial.
- Visual Studio: asegúrese de tener Visual Studio instalado.
-  GroupDocs.Editor para .NET: necesitará la biblioteca GroupDocs.Editor para .NET. Puedes descargarlo desde el[pagina de descarga](https://releases.groupdocs.com/editor/net/).
## Importar espacios de nombres
Para comenzar, deberá importar los espacios de nombres necesarios. Esto le permite acceder a las clases y métodos necesarios para manipular documentos.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Paso 1: cargue su documento
Primero, debe cargar el documento del que desea extraer información. Esto se puede hacer proporcionando la ruta del archivo al documento.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Paso 2: recuperar la información del documento
 A continuación, recuperará la información del documento utilizando el`GetDocumentInfo` método. Este método no requiere ninguna opción de carga específica si no está seguro del formato del documento.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Paso 3: determinar el tipo de documento
Ahora debes comprobar el tipo de documento que estás tratando. Esto es crucial ya que dicta cómo manejará el documento.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Paso 4: extraiga información detallada
Si el documento es un documento de procesamiento de textos, puede extraer información detallada como el formato, la extensión, el número de páginas, el tamaño y si está cifrado.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Paso 5: repita para diferentes tipos de documentos
Repita los mismos pasos para otros tipos de documentos como hojas de cálculo y documentos de texto.
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
## Paso 6: Manejar documentos protegidos con contraseña
Cuando trabaje con documentos protegidos con contraseña, primero debe intentar abrirlos sin contraseña, luego con una contraseña incorrecta y finalmente con la contraseña correcta.
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
## Paso 7: Manejar documentos basados en texto
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
## Paso 8: disponer de los recursos
Finalmente, asegúrese de deshacerse de todos los recursos para evitar pérdidas de memoria.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusión
¡Felicidades! Ahora ha aprendido cómo extraer información de documentos usando GroupDocs.Editor para .NET. Esta potente biblioteca simplifica la gestión y manipulación de documentos, permitiéndole manejar varios tipos de documentos sin problemas. Ya sea que esté tratando con procesamiento de textos, hojas de cálculo o documentos basados en texto, GroupDocs.Editor proporciona una solución sólida.
## Preguntas frecuentes
### ¿Qué tipos de documentos puede manejar GroupDocs.Editor?
GroupDocs.Editor puede manejar varios tipos de documentos, incluidos procesamiento de textos, hojas de cálculo y documentos basados en texto.
### ¿Puede GroupDocs.Editor administrar documentos protegidos con contraseña?
Sí, GroupDocs.Editor puede administrar documentos protegidos con contraseña. Puede identificar y abrir estos documentos con la contraseña correcta.
### ¿Es necesario deshacerse de los objetos del Editor?
Sí, es fundamental deshacerse de los objetos del Editor para liberar recursos y evitar pérdidas de memoria.
### ¿Puedo extraer información detallada sobre el formato y tamaño del documento?
¡Absolutamente! GroupDocs.Editor le permite extraer información detallada, incluido el formato, la extensión, el tamaño, el recuento de páginas y el estado de cifrado.
### ¿Dónde puedo obtener asistencia si tengo problemas?
 Puede obtener apoyo del[Foro de soporte de GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).