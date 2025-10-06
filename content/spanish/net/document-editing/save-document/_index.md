---
title: Guardar documento
linktitle: Guardar documento
second_title: API GroupDocs.Editor .NET
description: Edite y guarde documentos sin esfuerzo utilizando GroupDocs.Editor para .NET. Esta guía paso a paso simplifica el proceso para los desarrolladores.
weight: 14
url: /es/net/document-editing/save-document/
type: docs
---
# Guardar documento

## Introducción
¿Está buscando editar y guardar documentos sin esfuerzo usando GroupDocs.Editor para .NET? ¡Estás en el lugar correcto! Este tutorial lo guiará a través del proceso paso a paso, asegurándole que pueda administrar fácilmente sus documentos. Ya sea que sea un desarrollador experimentado o un principiante, nuestra guía le brindará toda la información que necesita para comenzar.
## Requisitos previos
Antes de sumergirse en el tutorial, asegúrese de cumplir con los siguientes requisitos previos:
- Entorno de desarrollo: Visual Studio instalado en su máquina.
- .NET Framework: asegúrese de tener .NET Framework 4.6.1 o posterior.
-  GroupDocs.Editor para .NET: descargue la última versión[aquí](https://releases.groupdocs.com/editor/net/).
- Conocimientos básicos de C#: la familiaridad con la programación en C# es esencial.
## Importar espacios de nombres
Para utilizar GroupDocs.Editor en su proyecto .NET, debe importar los espacios de nombres necesarios. Así es como lo haces:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Ahora que tenemos nuestro entorno configurado y los espacios de nombres necesarios importados, profundicemos en los pasos necesarios para cargar, editar y guardar un documento usando GroupDocs.Editor para .NET.
## Paso 1: cargue el documento
Primero, necesitamos cargar el documento que queremos editar. GroupDocs.Editor simplifica este proceso. Así es como puedes hacerlo:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 En este paso, especificamos la ruta al documento que queremos editar y creamos una instancia del`Editor` clase. El`Edit` Luego se llama al método para cargar el documento en un`EditableDocument` objeto.
## Paso 2: modificar el documento
Con el documento cargado, es momento de hacer algunas modificaciones. Como no tenemos un editor WYSIWYG adjunto, simularemos el proceso de edición en código.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Aquí, recuperamos el contenido HTML incrustado del documento, realizamos un reemplazo de texto simple y creamos un nuevo`EditableDocument`instancia del HTML modificado.
## Paso 3: guarde el documento
Después de editar el documento, el último paso es guardarlo. GroupDocs.Editor proporciona múltiples opciones para guardar el documento en diferentes formatos.
## Guardar como RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Guardar como DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Guardar como texto sin formato
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Paso 4: limpieza
 Finalmente, es crucial deshacerse de los`EditableDocument` y`Editor` instancias para liberar recursos.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Si sigue estos pasos, podrá cargar, editar y guardar documentos de manera eficiente utilizando GroupDocs.Editor para .NET. Esta poderosa herramienta brinda flexibilidad y facilidad de uso, lo que hace que la gestión de documentos sea muy sencilla.
## Conclusión
Editar y guardar documentos mediante programación nunca ha sido tan fácil con GroupDocs.Editor para .NET. Esta guía lo guió a través de todo el proceso, desde cargar un documento hasta guardarlo en varios formatos. Con GroupDocs.Editor, tiene una solución versátil y sólida a su alcance, que simplifica el proceso de edición de documentos.
## Preguntas frecuentes
### ¿Qué formatos de archivo admite GroupDocs.Editor?
GroupDocs.Editor admite varios formatos de archivo, incluidos DOCX, RTF, TXT y muchos más. Para obtener una lista completa, consulte el[documentación](https://tutorials.groupdocs.com/editor/net/).
### ¿Puedo probar GroupDocs.Editor antes de comprarlo?
 Sí, puedes conseguir un[prueba gratis](https://releases.groupdocs.com/) para probar las funciones de GroupDocs.Editor.
### ¿Hay algún soporte disponible si tengo problemas?
 ¡Absolutamente! Puedes visitar el[Foro de soporte](https://forum.groupdocs.com/c/editor/20) para obtener ayuda con cualquier problema que encuentre.
### ¿Cómo obtengo una licencia temporal?
 Puedes solicitar un[licencia temporal](https://purchase.groupdocs.com/temporary-license/) para fines de evaluación.
### ¿Dónde puedo comprar la versión completa de GroupDocs.Editor?
 Puedes comprar la versión completa.[aquí](https://purchase.groupdocs.com/buy).