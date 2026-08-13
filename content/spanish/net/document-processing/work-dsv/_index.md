---
date: 2026-06-06
description: Aprenda cómo **crear documentos editables** a partir de archivos CSV
  y TSV usando GroupDocs.Editor para .NET. Esta guía también muestra cómo **leer texto
  delimitado C#** y **editar CSV .NET** de manera eficiente en Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Trabajar con valores separados delimitados (DSV) – crear documento editable
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Trabajar con valores separados delimitados (DSV) – crear documento editable
type: docs
url: /es/net/document-processing/work-dsv/
weight: 12
---

# Trabajar con valores separados delimitados (DSV) – crear documento editable

Si eres un desarrollador .NET que necesita **create editable document** objetos a partir de valores separados delimitados (DSV) como CSV o TSV, has llegado al lugar correcto. En las primeras 100 palabras explicaremos por qué GroupDocs.Editor para .NET es la forma más fiable de **read delimited text C#**, editarlo y luego guardarlo sin perder el formato. Saldrás con un flujo de trabajo completo, listo para copiar‑y‑pegar, que encaja de forma natural en cualquier solución de Visual Studio.

## Respuestas rápidas
- **¿Qué biblioteca maneja la edición de CSV mejor en .NET?** GroupDocs.Editor for .NET.
- **¿Puedo editar archivos CSV grandes en Visual Studio?** Sí – la API transmite datos y evita cargar todo el archivo en memoria.
- **¿Necesito una licencia para uso en producción?** Se requiere una licencia comercial; hay una prueba gratuita disponible.
- **¿Qué formatos puedo exportar después de la edición?** CSV, TSV y formatos de hoja de cálculo compatibles con Excel.
- **¿Es la API compatible con .NET 6+?** Absolutamente – soporta .NET Framework 4.5+, .NET Core 3.1+, .NET 5 y .NET 6.

## Qué es “create editable document” en el contexto de GroupDocs.Editor?
**Create editable document** significa generar una instancia `EditableDocument` que representa una versión mutable de un archivo fuente (CSV, TSV, etc.) en memoria. Este objeto te permite leer, modificar y volver a guardar el contenido usando la misma API. Proporciona métodos para obtener el texto del documento, aplicar cambios y guardarlo en varios formatos, asegurando que la alineación de columnas y las comillas se conserven.

## Por qué usar GroupDocs.Editor para el manejo de DSV?
GroupDocs.Editor procesa **more than 50 input and output formats**, incluyendo CSV, TSV y hojas de cálculo compatibles con Excel, mientras mantiene el uso de memoria por debajo de 10 MB para archivos de hasta 500 MB. También preserva la alineación de columnas, las reglas de comillas y las codificaciones personalizadas automáticamente, lo que elimina la necesidad de lógica de análisis manual.

## Requisitos previos
Antes de profundizar, asegúrate de tener lo siguiente instalado:

- **Visual Studio** (cualquier edición reciente) – desarrollarás y depurarás directamente dentro del IDE.
- **GroupDocs.Editor for .NET** – descarga el paquete más reciente **[aquí](https://releases.groupdocs.com/editor/net/)**.
- **Basic C# knowledge** – el tutorial asume que puedes crear un proyecto de consola o ASP.NET y agregar paquetes NuGet.

## Importar espacios de nombres
Las clases `Editor`, `EditableDocument` y de opciones se encuentran en el espacio de nombres `GroupDocs.Editor`.

La clase `DelimitedTextEditOptions` es el punto de entrada para definir el delimitador (coma, tabulación, etc.) y otras reglas de análisis.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Cómo crear un documento editable a partir de un archivo CSV?
Carga el CSV fuente con `Editor` y llama al método `Edit`, pasando una instancia de `DelimitedTextEditOptions` que especifica un delimitador de coma. El método devuelve un `EditableDocument` que puedes manipular en memoria. Este patrón de dos pasos—cargar → editar—cubre escenarios de **read delimited text C#** y garantiza que se conserve la estructura original del archivo.

## Paso 1: Obtener una ruta al archivo DSV de entrada
Primero, debes especificar la ruta absoluta o relativa al archivo DSV fuente. Para la demostración usaremos un CSV sencillo ubicado en la carpeta `Data` del proyecto.

```csharp
string inputFilePath = "Your Sample Document";
```

## Paso 2: Crear una instancia de Editor
`Editor` es la clase central que orquesta la carga, edición y guardado. Instanciarla con un objeto `FileInfo` te brinda control total sobre el ciclo de vida del archivo.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Paso 3: Crear opciones de edición DSV
`DelimitedTextEditOptions` indica al editor cómo interpretar el archivo. Puedes establecer el delimitador, si la primera fila contiene encabezados y la codificación de caracteres.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Paso 4: Crear una instancia de EditableDocument
`EditableDocument` representa una versión mutable en memoria del archivo fuente. Llamar a `Editor.Edit` con las opciones devuelve un `EditableDocument`. Este objeto contiene el texto del archivo en una cadena mutable, listo para cualquier operación **parse delimited values C#** que necesites.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Paso 5: Editar el contenido del documento
`GetDocumentText()` devuelve el texto actual del documento editable como una cadena. Recupera el texto original mediante `EditableDocument.GetDocumentText()`, realiza tus modificaciones (p.ej., reemplazar el valor de una columna) y guarda el resultado en una nueva cadena. Aquí es donde **edit CSV .NET** sin tocar flujos de archivo de bajo nivel.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Paso 6: Crear un EditableDocument con contenido actualizado
Envuelve la cadena modificada nuevamente en un `EditableDocument`. Este paso finaliza los cambios y prepara el objeto para guardarlo en cualquier formato compatible.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Paso 7: Crear opciones de guardado CSV
`DelimitedTextSaveOptions` especifica cómo escribir el contenido editado de vuelta a un archivo CSV. Cuando estés listo para persistir los cambios, configura `DelimitedTextSaveOptions`. Puedes especificar el mismo delimitador, uno diferente o incluso cambiar el estilo de terminación de línea.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Paso 8: Crear opciones de guardado TSV
Si necesitas una versión separada por tabulaciones, simplemente cambia el delimitador a `\t`. El mismo `EditableDocument` puede guardarse múltiples veces con diferentes opciones.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Paso 9: Crear opciones de guardado de hoja de cálculo
`SpreadsheetSaveOptions` configura la exportación del documento a formatos compatibles con Excel como .xlsx. GroupDocs.Editor también te permite exportar los datos editados a un formato compatible con Excel (`.xlsx`). La clase `SpreadsheetSaveOptions` maneja automáticamente los tipos de columna, fórmulas y estilo de celdas.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Paso 10: Preparar rutas de guardado
Define rutas de salida distintas para cada formato. Usar convenciones de nombres claras (p.ej., `output.csv`, `output.tsv`, `output.xlsx`) ayuda a mantener tu proyecto organizado.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Paso 11: Guardar el documento editado
`Save()` escribe el documento en disco usando las opciones de guardado proporcionadas. Invoca `EditableDocument.Save` con las opciones apropiadas para cada formato de destino. La API escribe el archivo directamente en disco, preservando la codificación original a menos que la sobrescribas.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Paso 12: Liberar instancias de EditableDocument
Tanto `Editor` como `EditableDocument` implementan `IDisposable`. Liberarlos libera los manejadores de archivo y recursos no administrados, lo cual es crucial al procesar muchos archivos en un trabajo por lotes.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Problemas comunes y soluciones
| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Unexpected extra quotes** | El analizador CSV predeterminado puede tratar comas incrustadas como delimitadores. | Establece `EscapeMode = EscapeMode.DoubleQuote` en `DelimitedTextEditOptions`. |
| **Large file memory spike** | Cargar un archivo de 500 MB sin transmisión. | Usa `Editor.Load` con `LoadOptions` que habiliten la carga diferida. |
| **Encoding mismatch** | El archivo fuente usa UTF‑16 pero las opciones por defecto son UTF‑8. | Establece explícitamente `Encoding = Encoding.Unicode` en las opciones de guardado. |

## Preguntas frecuentes

**Q: ¿Puedo usar GroupDocs.Editor para .NET para editar archivos CSV grandes?**  
A: Sí, la API transmite datos y puede manejar archivos de más de 1 GB sin cargar todo el documento en memoria.

**Q: ¿GroupDocs.Editor para .NET admite otros formatos DSV además de CSV y TSV?**  
A: Absolutamente – cualquier delimitador de un solo carácter (p.ej., barra vertical `|`, punto y coma `;`) es compatible siempre que lo especifiques en `DelimitedTextEditOptions`.

**Q: ¿Es posible personalizar la codificación al guardar archivos DSV?**  
A: Sí, puedes establecer la propiedad `Encoding` en `DelimitedTextSaveOptions` a UTF‑8, UTF‑16, ISO‑8859‑1, o cualquier `Encoding` de .NET que necesites.

**Q: ¿Puedo convertir un archivo CSV a una hoja de cálculo Excel usando GroupDocs.Editor para .NET?**  
A: Sí – después de editar, simplemente usa `SpreadsheetSaveOptions` para exportar el contenido como un libro de trabajo `.xlsx`.

**Q: ¿Dónde puedo encontrar más documentación sobre GroupDocs.Editor para .NET?**  
A: Referencias detalladas de la API y ejemplos de código están disponibles **[aquí](https://tutorials.groupdocs.com/editor/net/)**.

---

**Última actualización:** 2026-06-06  
**Probado con:** GroupDocs.Editor 23.10 for .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Tutoriales de edición de documentos de texto plano y DSV para GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Domina GroupDocs.Editor .NET para la edición y conversión eficiente de documentos CSV](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Dominar la carga de documentos en .NET con GroupDocs.Editor: Guía completa](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)