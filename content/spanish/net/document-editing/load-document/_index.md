---
title: Cargar documento
linktitle: Cargar documento
second_title: API GroupDocs.Editor .NET
description: Aprenda a editar documentos mediante programación con GroupDocs.Editor para .NET. Guía paso a paso para cargar documentos, manejar archivos protegidos con contraseña y más.
type: docs
weight: 13
url: /es/net/document-editing/load-document/
---
## Introducción
Editar documentos mediante programación puede ser una tarea desalentadora, especialmente si se trata de diferentes formatos de archivos y estructuras complejas. Afortunadamente, GroupDocs.Editor para .NET facilita esta tarea al proporcionar una API sólida y fácil de usar para editar una amplia gama de tipos de documentos. En este tutorial, lo guiaremos a través de todo lo que necesita para comenzar con GroupDocs.Editor para .NET, incluidos los requisitos previos, cómo importar espacios de nombres y una guía detallada paso a paso para cargar documentos usando varios métodos.
## Requisitos previos
Antes de sumergirnos, asegúrese de tener configurados los siguientes requisitos previos:
- Visual Studio: asegúrese de tener Visual Studio instalado en su máquina.
- .NET Framework: GroupDocs.Editor para .NET admite .NET Framework 2.0 o posterior. Asegúrese de que su proyecto esté dirigido a un marco compatible.
-  GroupDocs.Editor para .NET: descargue la última versión desde[pagina de descarga](https://releases.groupdocs.com/editor/net/).
- Conocimientos básicos de C#: Es necesario estar familiarizado con la programación en C# y .NET para seguir este tutorial.
## Importar espacios de nombres
Para comenzar a usar GroupDocs.Editor para .NET, debe importar los espacios de nombres necesarios a su proyecto. Agregue las siguientes directivas de uso en la parte superior de su archivo C#:
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
Estos espacios de nombres proporcionarán acceso a las clases y métodos necesarios para las tareas de edición de documentos.
## Paso 1: cargar el documento desde una ruta de archivo
Cargar un documento desde una ruta de archivo es sencillo. Este método es ideal para documentos almacenados localmente en su máquina.

```csharp
string inputPath = "Your Sample Document";
// Cargue el documento como archivo a través de la ruta y sin opciones de carga
Editor editor1 = new Editor(inputPath);
// Disponer de recursos
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Paso 2: cargar el documento con opciones de carga
A veces, es posible que necesites cargar documentos que requieren un manejo especial, como archivos protegidos con contraseña. En tales casos, puede utilizar las opciones de carga.

```csharp
string inputPath = "Your Sample Document";
//Crear opciones de carga para documentos de Word
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Cargue el documento como archivo a través de la ruta y con opciones de carga
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Disponer de recursos
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Paso 3: cargar el documento desde un flujo de bytes
Cargar un documento desde un flujo de bytes es útil cuando necesita procesar documentos que no están almacenados como archivos, como los recuperados de una base de datos o un servicio web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Cargue el documento como contenido desde el flujo de bytes y sin opciones de carga
Editor editor3 = new Editor(delegate { return inputStream; });
// Disponer de recursos
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Paso 4: cargar el documento con opciones de carga desde un flujo de bytes
Para documentos que requieren un manejo especial cuando se cargan desde un flujo de bytes, puede combinar la carga del flujo de bytes con opciones de carga.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Crear opciones de carga para hojas de cálculo
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Cargue el documento como contenido desde el flujo de bytes y con opciones de carga
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Disponer de recursos
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Conclusión
¡Felicidades! Ha aprendido con éxito cómo cargar documentos usando GroupDocs.Editor para .NET de varias maneras. Ya sea que trabaje con archivos locales, documentos protegidos con contraseña o flujos de bytes, GroupDocs.Editor proporciona una solución flexible y potente para sus necesidades de edición de documentos. Recuerde disponer siempre de los recursos para garantizar un rendimiento óptimo y una gestión de recursos en sus aplicaciones.
## Preguntas frecuentes
### ¿Qué formatos de archivo son compatibles con GroupDocs.Editor para .NET?
 GroupDocs.Editor admite una amplia gama de formatos de archivo, incluidos DOCX, XLSX, PPTX, HTML y muchos más. Para obtener una lista completa, consulte la[documentación](https://reference.groupdocs.com/editor/net/).
### ¿Cómo manejo documentos protegidos con contraseña?
 Puede utilizar opciones de carga como`WordProcessingLoadOptions` para especificar la contraseña al cargar documentos protegidos con contraseña.
### ¿Puedo utilizar GroupDocs.Editor en una aplicación web?
Sí, GroupDocs.Editor se puede utilizar en aplicaciones web. Asegúrese de manejar adecuadamente los flujos de archivos y la eliminación de recursos para evitar pérdidas de memoria.
### ¿Dónde puedo obtener una licencia temporal para GroupDocs.Editor?
 Puede obtener una licencia temporal del[página de licencia temporal](https://purchase.groupdocs.com/temporary-license/).
### ¿Hay soporte disponible si tengo problemas?
 Sí, GroupDocs brinda soporte a través de su[Foro de soporte](https://forum.groupdocs.com/c/editor/20).