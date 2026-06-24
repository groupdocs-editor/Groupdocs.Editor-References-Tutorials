---
date: 2026-05-12
description: Aprenda cómo extraer fuentes y otros recursos HTML de documentos usando
  GroupDocs.Editor for .NET. Guía paso a paso para desarrolladores .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Guardar recursos HTML en una carpeta
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Cómo extraer fuentes y guardar recursos HTML en una carpeta
type: docs
url: /es/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Cómo extraer fuentes y guardar recursos HTML en una carpeta

## Introducción
GroupDocs.Editor for .NET le permite **extraer fuentes** y otros recursos de un documento mientras lo convierte a HTML. En unas pocas líneas de C# puede extraer imágenes, hojas de estilo y archivos de fuentes, y luego almacenarlos en una carpeta de su elección. Este tutorial lo guía a través de todo el flujo de trabajo, desde la inicialización del editor hasta el guardado de cada recurso en disco.

## Respuestas rápidas
- **¿Qué significa “cómo extraer fuentes”?** Es el proceso de recuperar los archivos de fuentes incrustados en un documento fuente durante la conversión a HTML.  
- **¿Qué biblioteca maneja esto?** GroupDocs.Editor for .NET proporciona una API dedicada para extraer fuentes, imágenes y hojas de estilo.  
- **¿Necesito una licencia?** Hay una prueba gratuita disponible; se requiere una licencia comercial para uso en producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **¿Puedo especificar una carpeta personalizada?** Sí, puede indicar cualquier ruta con permisos de escritura al guardar los recursos extraídos.

## Qué significa “cómo extraer fuentes”
**Cómo extraer fuentes** se refiere a recuperar los archivos de fuentes originales incrustados en un documento fuente (p. ej., DOCX, PPTX) para que puedan ser referenciados por el HTML generado. Esto garantiza que el texto se renderice exactamente como se pretende en los navegadores sin depender de fuentes del sistema.

## ¿Por qué usar GroupDocs.Editor para la extracción de recursos HTML?
GroupDocs.Editor admite **más de 50 formatos de entrada y salida** —incluidos DOCX, PPTX, PDF y HTML— y puede procesar documentos con **hasta 300 páginas** sin cargar todo el archivo en memoria. Su API extrae fuentes, imágenes y CSS en una sola pasada, reduciendo el tiempo de desarrollo hasta en **un 70 %** en comparación con el análisis manual.

## Requisitos previos
Antes de sumergirse en el tutorial, asegúrese de contar con los siguientes requisitos:
1. **Conocimientos básicos de C# y .NET** – Familiaridad con el lenguaje de programación C# y el framework .NET es esencial para seguir los ejemplos.  
2. **Biblioteca GroupDocs.Editor for .NET** – Descargue e instale la biblioteca GroupDocs.Editor for .NET desde el [sitio web](https://releases.groupdocs.com/editor/net/).  
3. **Entorno de desarrollo** – Configure su entorno de desarrollo preferido, como Visual Studio u otro IDE compatible.

## Importar espacios de nombres
Para comenzar, importe los espacios de nombres necesarios en su proyecto C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```

## ¿Cómo extraer fuentes y guardar recursos HTML en una carpeta?
Cargue su documento fuente con `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` y luego llame a `editor.Save("output.html", SaveOptions.Html);`. Después de la operación de guardado, la colección `Resources` contiene todos los recursos extraídos —incluidas las fuentes— que puede iterar y escribir en disco. Este enfoque de un solo paso maneja automáticamente tanto la conversión como la extracción de recursos.

## Paso 1: Inicializar GroupDocs.Editor
`Editor` es la clase central que orquesta la carga, conversión y extracción de recursos del documento. Representa una única sesión de documento en memoria.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Primero, inicialice el objeto `Editor` proporcionando la ruta a su documento de ejemplo. En este caso, estamos usando un documento Word, por lo que especificamos `WordProcessingLoadOptions` como el tipo de documento.

## Paso 2: Editar documento
`EditableDocument` es la representación editable devuelta por el método `Edit`, que le permite manipular el documento antes de guardarlo.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
A continuación, cree un objeto `EditableDocument` llamando al método `Edit` del objeto `Editor`. Esto le permite realizar operaciones de edición en el documento.

## Paso 3: Extraer recursos
`Resources` es una colección que agrupa los recursos extraídos —imágenes, fuentes y hojas de estilo— en listas separadas para facilitar su manejo.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraiga recursos como imágenes, fuentes y hojas de estilo del documento y guárdelos en las listas correspondientes.

## Paso 4: Especificar carpeta de salida
`outputFolder` es una cadena que define dónde se escribirán los archivos extraídos. Puede apuntarlo a cualquier directorio con permisos de escritura en el servidor o en la máquina **local**.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Defina la carpeta de salida donde se guardarán los recursos extraídos. **Puede personalizar la ruta de la carpeta según sus requisitos**.

## Paso 5: Guardar recursos
`SaveResource` es una rutina auxiliar que escribe un único recurso binario (imagen, fuente o hoja de estilo) en el sistema de archivos.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Recorra cada recurso de imagen, guárdelo en la carpeta de salida y muestre información relevante como el nombre de archivo, el tipo y las dimensiones.

```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
De manera similar, guarde cada recurso de fuente en la carpeta de salida.

```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Finalmente, guarde cada hoja de estilo en la carpeta de salida y complete el proceso de edición.

## Problemas comunes y soluciones
- **Fuentes faltantes después de la conversión** – Asegúrese de que el documento fuente realmente incruste las fuentes; de lo contrario, GroupDocs.Editor solo podrá referenciar fuentes del sistema.  
- **Errores de acceso denegado** – Verifique que el proceso de la aplicación tenga permisos de escritura en la carpeta de salida objetivo.  
- **Los documentos grandes provocan un alto uso de memoria** – Utilice `LoadOptions` con `LoadMode = LoadMode.Stream` para transmitir archivos grandes en lugar de cargarlos completamente en memoria.

## Preguntas frecuentes

**Q: ¿Es compatible GroupDocs.Editor con otros formatos de documento además de Word?**  
A: Sí, admite Excel, PowerPoint, PDF, HTML y más de 50 formatos adicionales tanto para la edición como para la extracción de recursos.

**Q: ¿Puedo integrar GroupDocs.Editor en una aplicación web?**  
A: Por supuesto. La API funciona sin problemas con proyectos ASP.NET Core, MVC y Web API, lo que le permite procesar documentos del lado del servidor.

**Q: ¿GroupDocs.Editor ofrece integración con almacenamiento en la nube?**  
A: Sí, incluye conectores integrados para Google Drive, Dropbox, OneDrive y Amazon S3, lo que permite cargar y guardar documentos directamente en la nube.

**Q: ¿Hay una prueba gratuita disponible para GroupDocs.Editor?**  
A: Se puede descargar una prueba totalmente funcional de 30 días desde el sitio web de GroupDocs sin necesidad de tarjeta de crédito.

**Q: ¿Cómo puedo obtener soporte técnico para problemas de extracción?**  
A: Puede contactar al equipo de soporte de GroupDocs a través del foro oficial, enviar un ticket mediante el portal de clientes o consultar la documentación detallada de la API.

**Última actualización:** 2026-05-12  
**Probado con:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Edición eficiente de documentos con GroupDocs.Editor .NET&#58; Transformar HTML en documentos editables](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Extracción y guardado eficiente de recursos DOCX usando GroupDocs.Editor .NET - Guía completa](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Dominar la edición y conversión de documentos con GroupDocs.Editor .NET&#58; Guía completa](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)