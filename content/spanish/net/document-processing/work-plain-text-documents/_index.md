---
title: Trabajar con documentos de texto sin formato
linktitle: Trabajar con documentos de texto sin formato
second_title: API GroupDocs.Editor .NET
description: Aprenda a editar documentos de texto sin formato usando GroupDocs.Editor para .NET con nuestra guía paso a paso. Simplifique su proceso de edición de documentos .NET.
weight: 15
url: /es/net/document-processing/work-plain-text-documents/
---
## Introducción
¿Está buscando optimizar su proceso de edición de documentos en .NET? ¡No busque más, GroupDocs.Editor para .NET! Esta poderosa API le permite editar una amplia variedad de formatos de documentos con facilidad. En este tutorial, lo guiaremos a través del proceso de trabajar con documentos de texto sin formato usando GroupDocs.Editor para .NET. Al final, estará equipado para manejar la edición de documentos de texto como un profesional. ¿Listo para sumergirte? ¡Empecemos!
## Requisitos previos
Antes de comenzar, hay algunas cosas que deberá implementar:
- Entorno de desarrollo .NET: asegúrese de tener configurado un entorno de desarrollo .NET que funcione. Visual Studio es una opción popular.
-  GroupDocs.Editor para .NET: descargue e instale el[GroupDocs.Editor para .NET](https://releases.groupdocs.com/editor/net/).
- Conocimientos básicos de C#: la familiaridad con el lenguaje de programación C# le ayudará a seguir los ejemplos.
- Editor de texto: cualquier editor de texto servirá, aunque se recomienda Visual Studio Code por sus características y facilidad de uso.
## Importar espacios de nombres
Para comenzar a usar GroupDocs.Editor para .NET, debe importar los espacios de nombres necesarios a su proyecto. Esto garantiza que todas las clases y métodos necesarios estén disponibles para su uso.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Dividamos el proceso en pasos manejables. Continúe mientras lo guiamos a través de cada etapa de la edición de documentos de texto sin formato usando GroupDocs.Editor para .NET.
## Paso 1: obtenga una ruta al archivo TXT de entrada
Primero, debe especificar la ruta al archivo TXT de entrada. Puede ser una ruta a un archivo local o una secuencia que contenga el contenido del archivo.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Paso 2: crear una instancia de editor
 A continuación, cree una instancia del`Editor` clase. Esta clase es responsable de cargar y editar documentos. No se requieren opciones de carga en esta etapa.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Paso 3: crear opciones de edición de TXT
Ahora, crea las opciones de edición de TXT. Estas opciones le permiten especificar cómo se debe procesar el contenido del texto durante la edición.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Paso 4: crear una instancia de EditableDocument
 Con las opciones de edición configuradas, cree un`EditableDocument` instancia. Esto representa el documento en un formato editable.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Paso 5: edite el contenido del documento
Recupere el contenido del texto original y realice las ediciones que desee. Para este ejemplo, reemplazaremos la palabra "texto" por "texto EDITADO".
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Paso 6: cree un documento editable con contenido actualizado
 Después de realizar las ediciones necesarias, cree un nuevo`EditableDocument` con el contenido actualizado y los recursos originales.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Paso 7: cree opciones de guardado de procesamiento de textos
Prepare las opciones de guardado para el formato WordProcessing. Este ejemplo utiliza el formato DOCM y especifica la configuración regional.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Paso 8: cree opciones para guardar TXT
De manera similar, cree las opciones de guardado para el formato TXT. Asegúrese de que la codificación esté configurada en UTF-8 y conserve el diseño de la tabla.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Paso 9: preparar las rutas de salida
Prepare las rutas para guardar los archivos DOCX y TXT resultantes. Utilice la ruta del archivo de entrada para determinar el directorio de salida y los nombres de los archivos.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Paso 10: guarde el documento editado
Finalmente, guarde el documento editado en formato DOCX y TXT utilizando las opciones de guardado especificadas.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusión
 ¡Felicidades! Ha editado con éxito un documento de texto sin formato utilizando GroupDocs.Editor para .NET. Esta poderosa herramienta simplifica la edición de documentos, facilitando su integración en sus aplicaciones .NET. Ya sea que maneje archivos de texto simples o formatos de documentos complejos, GroupDocs.Editor lo tiene cubierto. Explore más características y capacidades visitando el[Documentación de GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Preguntas frecuentes
### ¿Qué formatos de archivo admite GroupDocs.Editor para .NET?
 GroupDocs.Editor para .NET admite una amplia gama de formatos de archivo, incluidos DOCX, TXT, HTML y más. Comprobar el[documentación](https://tutorials.groupdocs.com/editor/net/) para obtener una lista completa.
### ¿Cómo puedo obtener una prueba gratuita de GroupDocs.Editor para .NET?
 Puede descargar una versión de prueba gratuita de GroupDocs.Editor para .NET desde[página de lanzamientos](https://releases.groupdocs.com/).
### ¿Puedo comprar una licencia temporal de GroupDocs.Editor para .NET?
Sí, puede obtener una licencia temporal de la[Página de compra de GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### ¿Dónde puedo obtener soporte para GroupDocs.Editor para .NET?
 El soporte está disponible a través del[Foro de soporte de GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### ¿Existe documentación detallada disponible para GroupDocs.Editor para .NET?
 Sí, la documentación detallada está disponible en el[Página de documentación de GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).