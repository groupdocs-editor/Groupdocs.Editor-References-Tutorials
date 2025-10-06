---
title: Uso avanzado de documentos editables
linktitle: Uso avanzado de documentos editables
second_title: API GroupDocs.Editor .NET
description: Aprenda el uso avanzado de GroupDocs.Editor para .NET creando, editando y extrayendo recursos de documentos mediante programación.
weight: 11
url: /es/net/document-editing/advanced-usage-of-editable-documents/
type: docs
---
# Uso avanzado de documentos editables

## Introducción
Si es un desarrollador de .NET y busca mejorar sus capacidades de edición de documentos, GroupDocs.Editor para .NET ofrece un potente conjunto de herramientas. Esta guía completa lo guiará a través del uso avanzado de documentos editables usando GroupDocs.Editor, desglosando cada paso en detalle para garantizar que pueda aprovechar todo su potencial.
## Requisitos previos
Antes de sumergirse en las funcionalidades avanzadas, asegúrese de tener lo siguiente:
- Visual Studio instalado en su máquina de desarrollo.
- .NET Framework compatible con GroupDocs.Editor.
-  GroupDocs.Editor para la biblioteca .NET. Puede[descarguelo aqui](https://releases.groupdocs.com/editor/net/).
-  Una licencia válida de GroupDocs.Editor. Puedes conseguir un[prueba gratis](https://releases.groupdocs.com/) o comprar un[licencia temporal](https://purchase.groupdocs.com/temporary-license/).
## Importar espacios de nombres
Para comenzar, asegúrese de importar los espacios de nombres necesarios en su proyecto .NET:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Paso 1: crear una instancia de EditableDocument
 Primero, necesitas crear una instancia de`EditableDocument` cargando y editando un documento de entrada de un formato compatible.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
En este paso, cargamos el documento de entrada y lo preparamos para editarlo.
## Paso 2: extraer recursos del documento
 El`EditableDocument` Contiene varios recursos que se pueden extraer y manipular. Analicemos estos:
### Paso 2.1: extraiga el documento completo como HTML
Puedes generar una única cadena que contenga el documento completo con todos sus recursos incrustados como HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Esta cadena será bastante grande ya que incluye hojas de estilo, imágenes y fuentes codificadas en base64.
### Paso 2.2: extraer todas las imágenes
Extraiga todas las imágenes del documento.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Paso 2.3: extrae todas las fuentes
Extraiga todas las fuentes utilizadas en el documento.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Paso 2.4: extraiga todas las hojas de estilo
Extraiga todas las hojas de estilo en formato textual.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Paso 2.5: Reúna todos los recursos
Reúna todos los recursos en una sola llamada.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Esto incluye imágenes, fuentes y hojas de estilo.
### Paso 2.6: Obtener el marcado HTML
Obtenga el marcado HTML del documento sin recursos incrustados.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Paso 3: ajustar los enlaces externos
A veces, es necesario ajustar los enlaces externos para que apunten a un controlador de recursos personalizado. He aquí cómo hacerlo:
### Paso 3.1: preparar prefijos personalizados
Prepare prefijos que antepondrán enlaces externos originales.
```csharp
string customImagesRequesthandlerUri = "http://ejemplo.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://ejemplo.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://ejemplo.com/FontsHandler/id=";
```
### Paso 3.2: Generar marcado HTML con prefijo
Genere marcado HTML con enlaces ajustados.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Paso 3.3: Obtener contenido HTML solo para el cuerpo
Algunos editores WYSIWYG sólo manejan marcado HTML puro sin encabezados.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Paso 3.4: Contenido prefijado solo para el cuerpo
Genere contenido solo para el cuerpo con prefijos de imagen personalizados.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Paso 3.5: extraer hojas de estilo
Extraer hojas de estilo utilizadas en el documento.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Paso 3.6: Hojas de estilo prefijadas
Extraiga hojas de estilo con prefijos personalizados.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Paso 4: guarde el documento como HTML
Guarde el documento editado como un archivo HTML, incluidos sus recursos.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Este método crea un directorio separado para recursos como hojas de estilo, imágenes y fuentes.
## Paso 5: Eliminación del documento editable
 Implementos EditableDocument`IDisposable` y proporciona la capacidad de comprobar si la instancia está eliminada.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Paso 5.1 Manejo del evento de eliminación
También puedes suscribirte al evento de eliminación.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Paso 6: Crear documento editable a partir de HTML
Cree una instancia de EditableDocument a partir de un documento HTML.
### Paso 6.1: desde el archivo HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Paso 6.2: Desde el marcado HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Estas instancias (afterEditFromFile y afterEditFromMarkup) son idénticas al original (antes de Editar).
## Paso 7: Eliminación manual
Deseche manualmente sus instancias de EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Esto asegura una limpieza adecuada de los recursos.
## Conclusión
GroupDocs.Editor para .NET proporciona herramientas sólidas para editar documentos mediante programación. Si sigue esta guía paso a paso, podrá administrar de manera eficiente el contenido, los recursos y los formatos de salida de los documentos. Ya sea que esté incrustando recursos, ajustando enlaces externos o convirtiendo documentos a HTML, GroupDocs.Editor le brinda la funcionalidad necesaria para la manipulación avanzada de documentos.
## Preguntas frecuentes
### ¿Qué formatos admite GroupDocs.Editor?
GroupDocs.Editor admite varios formatos, incluidos DOCX, XLSX, PPTX y más.
### ¿Puedo utilizar GroupDocs.Editor sin licencia?
 Sí, puedes usarlo con un[prueba gratis](https://releases.groupdocs.com/) o un[licencia temporal](https://purchase.groupdocs.com/temporary-license/).
### ¿Cómo extraigo recursos específicos de un documento?
 Puede extraer imágenes, fuentes y hojas de estilo utilizando los métodos proporcionados como`Images`, `Fonts` , y`Css`.
### ¿Es posible ajustar enlaces en la salida HTML?
Sí, puedes ajustar los enlaces externos especificando prefijos personalizados para imágenes, CSS y fuentes.
### ¿Cómo guardo un documento editado como un archivo HTML?
 Utilizar el`Save` método de la`EditableDocument`clase para guardar el documento como un archivo HTML, incluidos sus recursos.