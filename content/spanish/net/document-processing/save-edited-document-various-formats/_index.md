---
title: Guardar documento editado en varios formatos
linktitle: Guardar documento editado en varios formatos
second_title: API GroupDocs.Editor .NET
description: Aprenda a guardar documentos editados en varios formatos utilizando GroupDocs.Editor para .NET en esta guía completa paso a paso.
weight: 11
url: /es/net/document-processing/save-edited-document-various-formats/
---

# Guardar documento editado en varios formatos

## Introducción
¿Está buscando guardar documentos editados en varios formatos usando GroupDocs.Editor para .NET? ¡Has venido al lugar correcto! Esta guía completa lo guiará a través de todo el proceso, desde configurar su entorno hasta guardar su documento editado en múltiples formatos. ¡Vamos a sumergirnos y hacer que editar y guardar documentos sea muy sencillo!
## Requisitos previos
Antes de comenzar, asegúrese de tener lo siguiente:
1.  GroupDocs.Editor para .NET: descargue la última versión desde[aquí](https://releases.groupdocs.com/editor/net/).
2. Entorno de desarrollo: Visual Studio o cualquier otro IDE compatible con .NET.
3. .NET Framework: asegúrese de tener instalado .NET Framework 4.6.1 o superior.
4. Documento de muestra: un documento de WordProcessing de muestra con el que trabajar.
5. Conocimientos básicos de C#: se requiere familiaridad con la programación de C#.
## Importar espacios de nombres
Para comenzar, asegúrese de importar los espacios de nombres necesarios a su proyecto C#. Esto es crucial para acceder a la funcionalidad GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Dividamos el proceso en pasos manejables. Siga atentamente para asegurarse de comprender cada parte.
## Paso 1: obtenga una ruta al archivo de entrada
Primero, debe especificar la ruta a su archivo de WordProcessing de entrada. Este archivo será cargado y editado.
```csharp
string inputFilePath = "Your Sample Document";
```
## Paso 2: crear opciones de carga para el documento
A continuación, cree opciones de carga específicas para documentos de WordProcessing. Estas opciones ayudarán a personalizar cómo se carga el documento.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Paso 3: cargue el documento con opciones
 Ahora, cargue el documento en un`Editor` instancia utilizando las opciones de carga especificadas.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Paso 4: crear opciones de edición
Prepare las opciones de edición del documento. Estas opciones determinarán cómo se abre el documento para editarlo.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Paso 5: abrir el documento para editarlo
 Abra el documento para editarlo creando un`EditableDocument`instancia. Esta instancia le permitirá realizar cambios en el documento.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Paso 6: edite el contenido del documento
Ahora es el momento de editar el contenido del documento. Primero, obtenga el documento como una única cadena codificada en base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Por ejemplo, modifiquemos el subtítulo en el documento.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Paso 7: cree un nuevo documento editable a partir del contenido editado
 Crear un nuevo`EditableDocument` instancia del contenido y recursos editados.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Paso 8: guarde el documento en varios formatos
Finalmente, repita todos los formatos de WordProcessing compatibles y guarde el documento editado en cada formato.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Preparar opciones de guardado
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Preparar ruta de guardado
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // guardar el documento
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Mensaje de finalización
Para finalizar, podrás imprimir un mensaje indicando que el proceso ha finalizado exitosamente.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusión
¡Felicidades! Ha aprendido con éxito cómo guardar documentos editados en varios formatos usando GroupDocs.Editor para .NET. Esta poderosa herramienta facilita la manipulación y el almacenamiento de documentos en múltiples formatos con solo unas pocas líneas de código. Recuerde, los pasos clave implican cargar el documento, editar el contenido y guardarlo en los formatos deseados.
## Preguntas frecuentes
### ¿Qué es GroupDocs.Editor para .NET?
GroupDocs.Editor para .NET es una potente API que le permite editar documentos en varios formatos utilizando aplicaciones .NET.
### ¿Puedo utilizar GroupDocs.Editor gratis?
 Sí, puedes usarlo con una prueba gratuita. Descargalo[aquí](https://releases.groupdocs.com/).
### ¿Qué formatos admite GroupDocs.Editor?
GroupDocs.Editor admite una amplia gama de formatos, incluidos DOCX, PDF, HTML y muchos más.
### ¿Cómo obtengo una licencia temporal para GroupDocs.Editor?
 Puedes obtener una licencia temporal[aquí](https://purchase.groupdocs.com/temporary-license/).
### ¿Dónde puedo encontrar más documentación y soporte?
 La documentación detallada está disponible.[aquí](https://tutorials.groupdocs.com/editor/net/) y puedes obtener soporte[aquí](https://forum.groupdocs.com/c/editor/20).