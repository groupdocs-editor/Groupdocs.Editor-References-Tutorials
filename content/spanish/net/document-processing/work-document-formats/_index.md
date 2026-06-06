---
date: 2026-06-06
description: Aprenda cómo listar los formatos de documento compatibles y determinar
  la extensión del formato de archivo usando GroupDocs.Editor para .NET. Guía paso
  a paso con fragmentos de código, respuestas rápidas y preguntas frecuentes.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Listar formatos de documento compatibles
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Listar formatos de documento compatibles con GroupDocs.Editor .NET
type: docs
url: /es/net/document-processing/work-document-formats/
weight: 13
---

# Enumerar formatos de documento compatibles

Bienvenido a nuestro tutorial completo sobre **cómo enumerar los formatos de documento compatibles** con GroupDocs.Editor para .NET. Ya sea que estés construyendo una aplicación web centrada en documentos o una herramienta de escritorio de nivel empresarial, conocer exactamente qué formatos puedes editar o convertir es esencial. En esta guía descubrirás cómo enumerar formatos, analizar extensiones y editar documentos, todo con explicaciones claras y amigables y fragmentos de código listos para ejecutar.

## Respuestas rápidas
- **¿Cómo enumero todos los formatos compatibles?** Usa `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (o los equivalentes para Presentation/Spreadsheet) e itera la colección.  
- **¿Puedo determinar un formato a partir de una extensión de archivo?** Sí—llama a `DocumentFormatInfo.FromExtension(".docx")`.  
- **¿Qué tipos de archivo admite GroupDocs.Editor?** Más de 30 formatos de entrada y salida, incluidos DOCX, XLSX, PPTX, HTML y texto plano.  
- **¿Necesito una licencia para enumerar formatos?** Una licencia temporal desbloquea la API completa; de lo contrario, una versión de prueba funciona con funciones limitadas.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## ¿Qué es “enumerar formatos de documento compatibles”?
La frase se refiere a obtener programáticamente la colección de tipos de archivo que GroupDocs.Editor puede abrir, editar y guardar. Esta operación te permite crear menús desplegables dinámicos en la UI o validar las cargas de usuarios antes del procesamiento, garantizando que solo se pasen archivos compatibles al editor para su manipulación posterior.

## ¿Por qué enumerar formatos de documento compatibles?
GroupDocs.Editor **admite más de 30 formatos de entrada y salida** y puede manejar archivos de hasta **2 GB** sin cargar todo el documento en memoria. Conocer la lista exacta evita errores en tiempo de ejecución, mejora la experiencia del usuario y te permite aplicar reglas de negocio como “solo permitir documentos de Office editables”. También ayuda a presentar a los usuarios únicamente los formatos que tu aplicación realmente soporta.

## Requisitos previos
Antes de comenzar, asegúrate de tener:

1. **Entorno de desarrollo .NET** – Visual Studio 2022 o cualquier IDE que soporte .NET 6+.  
2. **Biblioteca GroupDocs.Editor para .NET** – descárgala desde la [página de lanzamientos de GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Licencia temporal** – obtén una [licencia temporal](https://purchase.groupdocs.com/temporary-license/) para acceso sin restricciones.  
4. **Conocimientos básicos de C#** – familiaridad con espacios de nombres, sentencias `using` y salida a consola.

## ¿Cómo enumerar formatos de documento compatibles?
Carga la colección de formatos compatibles e imprime el nombre y la extensión de cada formato. Este patrón de dos pasos funciona para documentos de procesamiento de texto, hoja de cálculo y presentación. Al iterar la colección puedes poblar dinámicamente elementos de UI como menús desplegables, garantizando que los usuarios solo seleccionen formatos que el editor realmente puede manejar.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Enumerar formatos de procesamiento de texto
`Formats.WordProcessingFormats` es una enumeración que describe cada tipo de archivo de procesamiento de texto reconocido por el editor. La propiedad `All` devuelve una colección de estos objetos de formato.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explicación:**  
1. **Recorrer formatos:** Iteramos todos los formatos de procesamiento de texto disponibles.  
2. **Mostrar detalles del formato:** Para cada formato imprimimos su nombre amigable y su extensión de archivo predeterminada.

### Enumerar formatos de presentación
`Formats.PresentationFormats` funciona de la misma manera para archivos de diapositivas, exponiendo cada tipo de presentación soportado a través de la colección `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explicación:**  
1. **Recorrer formatos:** La misma lógica de iteración se aplica a presentaciones.  
2. **Mostrar detalles del formato:** Se muestra el nombre y la extensión de cada formato.

## ¿Cómo determinar la extensión del formato de archivo?
A veces solo dispones del nombre de un archivo y necesitas inferir el `DocumentFormat` correspondiente. GroupDocs.Editor ofrece un asistente estático sencillo que asigna una extensión de archivo a su representación interna de formato, permitiéndote validar o convertir archivos antes de cargarlos en el editor.

### Analizando formatos de hoja de cálculo
`Formats.SpreadsheetFormats.FromExtension` convierte una cadena de extensión de archivo en el valor de enumeración de formato de hoja de cálculo correspondiente.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explicación:**  
1. **Analizar formato:** `FromExtension` convierte la extensión `.xlsm` en su enumeración interna `SpreadsheetFormat`.  
2. **Mostrar formato:** Se imprime el nombre del formato analizado, confirmando la asignación.

### Analizando formatos textuales
De manera similar, `Formats.TextualFormats.FromExtension` resuelve extensiones de archivo textuales como HTML o TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explicación:**  
1. **Analizar formato:** El método `FromExtension` resuelve la extensión `html` a un `TextFormat`.  
2. **Mostrar formato:** Se muestra el nombre del formato textual, útil para editores basados en web.

## ¿Cómo editar documentos después de identificar los formatos?
Una vez que conoces el formato, cargar y editar un documento sigue un patrón consistente. Primero creas una instancia de `Editor` con la ruta al archivo fuente, luego llamas a `Edit()` para obtener un `EditableDocument`. Desde allí puedes leer, modificar y, finalmente, guardar el contenido usando los `SaveOptions` apropiados.

### Cargando un documento
`Editor` es la clase central que encapsula todas las operaciones de edición para un archivo dado.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explicación:**  
1. **Inicializar Editor:** Crea una instancia de `Editor`, pasando la ruta completa del archivo objetivo.  
2. **Patrón Dispose:** La instrucción `using` garantiza que todos los recursos no administrados se liberen de inmediato.

### Extrayendo contenido
`EditableDocument.GetContent()` devuelve el texto bruto del documento (o HTML para editores basados en web), que puedes mostrar o manipular.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explicación:**  
1. **Método Edit:** `Edit()` devuelve un objeto `EditableDocument`.  
2. **Obtener contenido:** `GetContent()` extrae el texto bruto del documento (o HTML para editores web).  
3. **Mostrar contenido:** El contenido se escribe en la consola para verificación.

### Guardando cambios
`SaveOptions` indica al editor cómo y en qué formato escribir el documento editado de vuelta al almacenamiento.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explicación:**  
1. **Método Edit:** Vuelve a obtener el `EditableDocument` después de las modificaciones.  
2. **Modificar contenido:** Aplica tus cambios a la cadena (no mostrado aquí).  
3. **Opciones de guardado:** Configura `SaveOptions` con el formato de salida deseado.  
4. **Guardar documento:** Persiste el archivo editado en disco.

## ¿Cómo trabajar con diferentes tipos de documento?
GroupDocs.Editor abstrae el manejo de Word, Spreadsheet y Presentation detrás de la misma superficie API, facilitando el cambio de contexto sin aprender un nuevo conjunto de clases para cada familia de documentos.

### Editando documentos de hoja de cálculo
`SpreadsheetSaveOptions` define cómo se escribe una hoja de cálculo, incluyendo el formato y configuraciones opcionales de compresión.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explicación:**  
1. **Inicializar Editor:** Pasa la ruta de un archivo de hoja de cálculo al constructor de `Editor`.  
2. **Método Edit:** Obtén un `EditableDocument`.  
3. **Obtener contenido:** Imprime la representación CSV (o HTML) de la hoja de cálculo.  
4. **Modificar contenido:** Aplica los cambios a nivel de celda que necesites.  
5. **Opciones de guardado:** Elige el `SpreadsheetSaveOptions` adecuado.  
6. **Guardar documento:** Escribe la hoja de cálculo actualizada en el almacenamiento.

### Editando documentos de presentación
`PresentationSaveOptions` controla el formato de salida para los paquetes de diapositivas, permitiéndote preservar o cambiar el tipo de archivo original.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explicación:**  
1. **Inicializar Editor:** Carga un archivo PowerPoint mediante `Editor`.  
2. **Método Edit:** Obtén un `EditableDocument`.  
3. **Obtener contenido:** Extrae el HTML de las diapositivas o texto plano.  
4. **Modificar contenido:** Actualiza títulos, viñetas o imágenes.  
5. **Opciones de guardado:** Usa `PresentationSaveOptions` para definir el formato de salida.  
6. **Guardar documento:** Persiste la presentación editada.

## Problemas comunes y soluciones
- **Error “Formato no soportado”:** Verifica que estés usando la última versión de GroupDocs.Editor; agrega soporte para nuevos formatos de Office de forma regular.  
- **Alto consumo de memoria con archivos grandes:** Habilita el modo de transmisión estableciendo `EditorSettings.EnableStreaming = true` antes de cargar el documento.  
- **Licencia no aplicada:** Asegúrate de que el archivo de licencia temporal esté en la raíz de la aplicación o cárgalo mediante `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Preguntas frecuentes

**P: ¿Cuál es la diferencia entre `DocumentFormatInfo` y `SaveOptions`?**  
R: `DocumentFormatInfo` proporciona metadatos sobre los tipos de archivo soportados, mientras que `SaveOptions` configura cómo se escribe un documento de vuelta al disco (formato, compresión, etc.).

**P: ¿Puedo enumerar formatos para una extensión de archivo personalizada?**  
R: Sí—usa `DocumentFormatInfo.FromExtension("yourExt")`; si la extensión no se reconoce, el método devuelve `null`.

**P: ¿GroupDocs.Editor admite archivos protegidos con contraseña?**  
R: Absolutamente. Pasa la contraseña al constructor de `Editor` mediante `EditorSettings` para abrir documentos cifrados.

**P: ¿Cuántos formatos admite realmente GroupDocs.Editor?**  
R: Más de **30 formatos de entrada y salida**, abarcando Word, Excel, PowerPoint, HTML y texto plano.

**P: ¿Existe una forma de limitar la lista solo a formatos editables?**  
R: Usa `GetEditableWordProcessingFormats()` (o los equivalentes para Spreadsheet/Presentation) para obtener los formatos que permiten capacidades completas de edición.

## Recursos adicionales
- Descarga la biblioteca desde la [página de lanzamientos de GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Obtén una [licencia temporal](https://purchase.groupdocs.com/temporary-license/) para acceso completo a todas las funciones.  
- Prueba el producto con una [prueba gratuita](https://releases.groupdocs.com/).  
- Explora ejemplos de uso detallados en la [documentación de GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Obtén ayuda de la comunidad en el [foro de soporte](https://forum.groupdocs.com/c/editor/20).

## Conclusión
Al seguir esta guía ahora sabes cómo **enumerar los formatos de documento compatibles**, **determinar un formato de archivo a partir de su extensión** y **editar documentos** en los tipos Word, Spreadsheet y Presentation usando GroupDocs.Editor para .NET. Incorpora estos fragmentos en tus propios proyectos para crear aplicaciones robustas, conscientes de los formatos, que deleiten a los usuarios finales y reduzcan errores en tiempo de ejecución.

---

**Última actualización:** 2026-06-06  
**Probado con:** GroupDocs.Editor 23.9 para .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Mastering Document Loading in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Master Document Editing in .NET with GroupDocs.Editor: A Comprehensive Guide](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Convert Word to HTML Using GroupDocs.Editor .NET: A Step‑By‑Step Guide](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)