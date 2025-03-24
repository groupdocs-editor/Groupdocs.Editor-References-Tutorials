---
title: Trabajar con valores separados delimitados (DSV)
linktitle: Trabajar con valores separados delimitados (DSV)
second_title: API GroupDocs.Editor .NET
description: Aprenda a editar archivos CSV y TSV usando GroupDocs.Editor para .NET con esta guía paso a paso. Mejore sus proyectos .NET sin esfuerzo.
weight: 12
url: /es/net/document-processing/work-dsv/
---

# Trabajar con valores separados delimitados (DSV)

## Introducción
Si es un desarrollador que trabaja con valores separados delimitados (DSV), como archivos CSV o TSV, sabe que editar estos archivos mediante programación puede ser una tarea desalentadora. Sin embargo, con GroupDocs.Editor para .NET, esta tarea se vuelve significativamente más sencilla y eficiente. En este tutorial, le explicaremos cómo utilizar GroupDocs.Editor para .NET para leer, editar y guardar archivos DSV. Dividiremos el proceso en pasos fáciles de seguir, para que usted pueda implementarlo en sus proyectos.
## Requisitos previos
Antes de sumergirnos en el tutorial, asegúrese de tener los siguientes requisitos previos:
- Visual Studio: asegúrese de tener Visual Studio instalado en su máquina.
-  GroupDocs.Editor para .NET: deberá descargar y consultar la biblioteca GroupDocs.Editor para .NET. Puedes descargarlo[aquí](https://releases.groupdocs.com/editor/net/).
- Comprensión básica de C#: este tutorial asume que tiene conocimientos básicos de desarrollo de C# y .NET.
## Importar espacios de nombres
Primero, necesita importar los espacios de nombres necesarios en su proyecto. Estos espacios de nombres proporcionan las clases y métodos necesarios para trabajar con GroupDocs.Editor para .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Paso 1: obtener una ruta al archivo DSV de entrada
Primero, debe especificar la ruta al archivo DSV de entrada. Para este ejemplo, asumiremos que es un archivo CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Paso 2: crear una instancia de editor
 Crear una instancia del`Editor` clase. Esta instancia se utilizará para cargar y manipular el archivo DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Paso 3: crear opciones de edición de DSV
 A continuación, cree una instancia de`DelimitedTextEditOptions` y especifique el delimitador del archivo DSV. Aquí utilizamos una coma como delimitador.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Paso 4: crear una instancia de EditableDocument
 Crear un`EditableDocument` instancia utilizando el`Editor.Edit` método. Esto prepara el documento para su edición.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Paso 5: edite el contenido del documento
Recuperar el contenido del texto original y realizar las modificaciones necesarias. Para fines de demostración, reemplacemos parte del texto.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Paso 6: cree un documento editable con contenido actualizado
 Crear un nuevo`EditableDocument` con el contenido actualizado.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Paso 7: cree opciones de guardado CSV
Especifique las opciones de guardado para el formato CSV, incluido el delimitador y la codificación.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Paso 8: cree opciones de guardado de TSV
De manera similar, especifique las opciones de guardado para el formato TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Paso 9: crear opciones para guardar la hoja de cálculo
Si necesita guardar el documento como una hoja de cálculo, cree las opciones de guardado correspondientes.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Paso 10: preparar rutas de guardado
Defina las rutas donde se guardarán los archivos editados.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Paso 11: guarde el documento editado
Guarde el documento editado en las rutas especificadas en diferentes formatos.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Paso 12: Eliminar instancias de EditableDocument
 Finalmente, asegúrese de desechar el`EditableDocument` instancias para liberar recursos.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusión
Editar archivos DSV usando GroupDocs.Editor para .NET es un proceso sencillo que implica crear una instancia de editor, configurar opciones de edición, modificar el contenido y guardar los cambios. Esta guía paso a paso debería ayudarle a integrar esta funcionalidad en sus aplicaciones .NET con facilidad. Ya sea que esté trabajando con CSV, TSV u otros formatos DSV, GroupDocs.Editor para .NET proporciona una solución sólida y flexible.
## Preguntas frecuentes
### ¿Puedo usar GroupDocs.Editor para .NET para editar archivos CSV grandes?
Sí, GroupDocs.Editor para .NET es capaz de manejar archivos CSV grandes de manera eficiente.
### ¿GroupDocs.Editor para .NET admite otros formatos DSV además de CSV y TSV?
Sí, admite varios formatos DSV siempre que especifique el delimitador adecuado.
### ¿Es posible personalizar la codificación al guardar archivos DSV?
Por supuesto, puede especificar la codificación deseada en las opciones de guardar.
### ¿Puedo convertir un archivo CSV a una hoja de cálculo de Excel usando GroupDocs.Editor para .NET?
Sí, puede guardar un archivo CSV como una hoja de cálculo de Excel utilizando las opciones de guardado adecuadas.
### ¿Dónde puedo encontrar más documentación sobre GroupDocs.Editor para .NET?
 Puedes encontrar documentación detallada.[aquí](https://tutorials.groupdocs.com/editor/net/)