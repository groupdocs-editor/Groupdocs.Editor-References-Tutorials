---
date: 2026-08-10
description: Aprenda cómo editar archivos de texto sin formato usando GroupDocs.Editor
  for .NET. La guía cubre la carga de un archivo txt, trimming spaces, setting text
  encoding y guardar el resultado.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Trabajar con documentos de texto sin formato
og_description: Aprenda cómo editar archivos de texto sin formato usando GroupDocs.Editor
  for .NET – load txt file, trim trailing spaces, convert leading spaces, set text
  encoding, y save efficiently.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Editar documentos de texto sin formato con GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Editar documentos de texto sin formato con GroupDocs.Editor for .NET
type: docs
url: /es/net/document-processing/work-plain-text-documents/
weight: 15
---

# Editar documentos de texto sin formato con GroupDocs.Editor para .NET

## Introducción
Si necesitas **editar texto sin formato** rápida y confiablemente en una aplicación .NET, GroupDocs.Editor para .NET es la herramienta que hace el trabajo pesado. Esta API admite más de 30 formatos de documento, puede manejar archivos de hasta 500 MB y te permite manipular texto sin cargar todo el archivo en memoria. En este tutorial aprenderás a cargar un archivo txt, recortar los espacios finales, convertir los espacios iniciales, establecer la codificación correcta y, finalmente, guardar el contenido editado de nuevo en disco. ¿Listo para ponerte manos‑en‑la‑obra? ¡Vamos allá!

## Respuestas rápidas
- **¿Cuál es el primer paso para editar un archivo txt?** Carga el archivo con `Editor` usando la ruta o el flujo que tengas.  
- **¿Puedo cambiar la codificación del archivo mientras lo edito?** Sí – el `TxtSaveOptions` te permite especificar UTF‑8, UTF‑16 o cualquier codificación personalizada.  
- **¿Cómo elimino los espacios extra al final de cada línea?** Obtén el texto, llama a `TrimEnd()` en cada línea y escríbelo de nuevo.  
- **¿GroupDocs.Editor es gratuito para probar?** Hay una prueba totalmente funcional de 30 días disponible en la página de lanzamientos.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.6+, .NET Core 3.1+ y .NET 5/6/7.

## ¿Qué es editar texto sin formato?
**Editar texto sin formato** significa cambiar programáticamente los caracteres dentro de un archivo `.txt` simple—añadiendo, eliminando o reformateando texto—mientras se preserva la codificación original del archivo y el estilo de salto de línea. Puede involucrar tareas como recortar espacios en blanco, normalizar finales de línea, actualizar valores de configuración o insertar contenido generado. La operación debe mantener el archivo legible por cualquier editor de texto estándar y conservar cualquier metadato existente, como los marcadores BOM.

## ¿Por qué usar GroupDocs.Editor para la edición de texto sin formato?
GroupDocs.Editor procesa los archivos de forma streaming, lo que significa que puede editar un archivo de registro de 300 MB usando menos de 50 MB de RAM. La biblioteca admite **más de 50 formatos de entrada y salida**, detecta automáticamente los estilos de fin de línea (CR, LF, CRLF) y ofrece opciones integradas para **recortar espacios finales** y **convertir espacios iniciales** sin necesidad de escribir analizadores personalizados.

## Requisitos previos
- **Entorno de desarrollo .NET** – Visual Studio 2022 o VS Code con la extensión C#.  
- **GroupDocs.Editor para .NET** – descárgalo desde la página de lanzamientos de [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- **Conocimientos básicos de C#** – deberías sentirte cómodo con I/O de archivos y manipulación de cadenas.  
- **Editor de texto (opcional)** – para inspeccionar los archivos fuente; se recomienda VS Code.  
- Para un uso detallado, consulta la [documentación](https://tutorials.groupdocs.com/editor/net/).  
- También puedes explorar la [página de lanzamientos](https://releases.groupdocs.com/) general.

## Cómo editar texto sin formato paso a paso
Carga el archivo, edita su contenido y guárdalo de nuevo — todo en menos de diez líneas de código. Las siguientes secciones te guían a través de cada etapa con explicaciones claras.

### Paso 1: Obtén una ruta al archivo TXT de entrada
Primero, decide si trabajarás con una ruta de archivo física o con un flujo de memoria. Usar una ruta es el enfoque más sencillo para el desarrollo local.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Paso 2: Crea una instancia de Editor
`Editor` es la clase principal que carga un documento y proporciona capacidades de edición.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Paso 3: Crea opciones de edición TXT
`TxtEditOptions` configura cómo se analizan y editan los archivos de texto sin formato, permitiéndote establecer la codificación y las reglas de manejo de espacios.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Paso 4: Crea una instancia de EditableDocument
`EditableDocument` representa la versión en memoria del documento cargado, incluyendo su texto y cualquier recurso asociado.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Paso 5: Edita el contenido del documento
Obtén el texto original, aplica cualquier operación de cadena que necesites (p.ej., reemplazar, recortar, cambiar mayúsculas/minúsculas) y almacena el resultado de nuevo en el `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Paso 6: Crea un EditableDocument con contenido actualizado
Después de haber transformado el texto, instancia un nuevo `EditableDocument` que contiene la cadena editada y la colección de recursos original.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Paso 7: Crea opciones de guardado WordProcessing
`WordProcessingSaveOptions` define la configuración para guardar el documento en un formato compatible con Word, como DOCX o DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Paso 8: Crea opciones de guardado TXT
`TxtSaveOptions` especifica cómo debe escribirse el archivo de texto sin formato editado, incluyendo la codificación, la preservación de los finales de línea y el manejo del diseño de tablas.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Paso 9: Prepara las rutas de salida
Deriva el directorio de salida a partir de la ruta del archivo de entrada, luego construye los nombres de archivo completos para los resultados DOCX y TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Paso 10: Guarda el documento editado
Finalmente, llama a `editor.Save` dos veces—una vez con las opciones de WordProcessing y otra con las opciones de TXT—para generar ambos formatos en una sola operación.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Problemas comunes y soluciones
- **Los espacios finales permanecen después de la edición** – asegúrate de que `TxtEditOptions.TrimTrailingSpaces` esté configurado en `true` antes de cargar el documento.  
- **Codificación incorrecta en el archivo guardado** – verifica que `TxtSaveOptions.Encoding` coincida con la página de códigos deseada (p.ej., `Encoding.UTF8`).  
- **Los archivos grandes provocan OutOfMemoryException** – usa la API de streaming (`Editor.Load(Stream)`) en lugar de cargar desde una ruta de archivo para mantener bajo el uso de memoria.  

## Preguntas frecuentes
**Q: What file formats does GroupDocs.Editor for .NET support?**  
**A:** La biblioteca admite más de 50 formatos, incluidos DOCX, TXT, HTML, PDF y markdown, lo que te permite editar y convertir entre ellos sin problemas.

**Q: How can I get a free trial of GroupDocs.Editor for .NET?**  
**A:** Descarga la prueba desde la [releases page](https://releases.groupdocs.com/).

**Q: Can I purchase a temporary license for testing?**  
**A:** Sí, las licencias temporales están disponibles a través de la [GroupDocs purchase page](https://purchase.groupdocs.com/temporary-license/).

**Q: Where can I find support if I run into issues?**  
**A:** El foro oficial de soporte es el mejor lugar – visita el [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).

**Q: Is there detailed documentation for advanced scenarios?**  
**A:** Absolutamente. La referencia completa está en la [GroupDocs.Editor documentation page](https://tutorials.groupdocs.com/editor/net/).

## Conclusión
Ahora dominas cómo **editar texto sin formato** usando GroupDocs.Editor para .NET—cargar un archivo txt, recortar espacios, convertir espacios iniciales, establecer la codificación adecuada y guardar el resultado en formatos TXT y DOCX. Esta capacidad te permite automatizar la limpieza de archivos de registro, generar archivos de configuración al vuelo o crear pipelines personalizados de procesamiento de texto sin reinventar la rueda. Explora características adicionales como el procesamiento por lotes y la conversión de documentos visitando la documentación oficial.

---

**Última actualización:** 2026-08-10  
**Probado con:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs  

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Tutoriales relacionados

- [Tutoriales de carga de documentos con GroupDocs.Editor para .NET](/editor/net/document-loading/)
- [Tutoriales de guardado y exportación de documentos para GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Tutoriales de edición de documentos de texto sin formato y DSV para GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)