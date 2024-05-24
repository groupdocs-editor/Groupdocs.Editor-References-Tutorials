---
title: Guardar recursos HTML en una carpeta
linktitle: Guardar recursos HTML en una carpeta
second_title: API GroupDocs.Editor .NET
description: Aprenda a extraer recursos HTML de documentos usando Groupdocs.Editor para .NET. Este completo tutorial proporciona orientación paso a paso para los desarrolladores.
type: docs
weight: 13
url: /es/net/document-editing/save-html-resources-to-folder/
---
## Introducción
Groupdocs.Editor para .NET es una poderosa herramienta que permite a los desarrolladores manipular y convertir documentos dentro de sus aplicaciones .NET sin problemas. Ya sea que necesite extraer recursos HTML de un documento o realizar tareas de edición avanzadas, Groupdocs.Editor simplifica el proceso con su API intuitiva y su extensa documentación.
## Requisitos previos
Antes de sumergirse en el tutorial, asegúrese de tener los siguientes requisitos previos:
1. Conocimientos básicos de C# y .NET: la familiaridad con el lenguaje de programación C# y el marco .NET es esencial para seguir los ejemplos.
2.  Groupdocs.Editor para la biblioteca .NET: descargue e instale Groupdocs.Editor para la biblioteca .NET desde[sitio web](https://releases.groupdocs.com/editor/net/).
3. Entorno de desarrollo: configure su entorno de desarrollo preferido, como Visual Studio o cualquier otro IDE compatible.

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
##Ahora, dividamos el proceso de guardar recursos HTML en una carpeta usando Groupdocs.Editor para .NET en varios pasos:
## Paso 1: Inicializar Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Primero, inicialice el`Editor`objeto proporcionando la ruta a su documento de muestra. En este ejemplo, usamos un documento de Word, por lo que especificamos`WordProcessingLoadOptions` como tipo de documento.
## Paso 2: Editar documento
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 A continuación, cree un`EditableDocument` objeto llamando al`Edit` método de la`Editor` objeto. Esto le permite realizar operaciones de edición en el documento.
## Paso 3: extraer recursos
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraiga recursos como imágenes, fuentes y hojas de estilo del documento y guárdelos en las listas respectivas.
## Paso 4: especificar la carpeta de salida
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Defina la carpeta de salida donde se guardarán los recursos extraídos. Puede personalizar la ruta de la carpeta según sus necesidades.
## Paso 5: Ahorre recursos
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Recorra cada recurso de imagen, guárdelo en la carpeta de salida y muestre información relevante como el nombre del archivo, el tipo y las dimensiones.
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

## Conclusión
En conclusión, Groupdocs.Editor para .NET proporciona una solución conveniente para administrar y manipular documentos mediante programación dentro de aplicaciones .NET. Siguiendo este tutorial, podrá extraer fácilmente recursos HTML de documentos y personalizar el proceso según sus requisitos específicos.
## Preguntas frecuentes
### ¿Groupdocs.Editor es compatible con otros formatos de documentos además de Word?
Sí, Groupdocs.Editor admite una amplia gama de formatos de documentos, incluidos Excel, PowerPoint, PDF y más.
### ¿Puedo integrar Groupdocs.Editor en mi aplicación web?
Por supuesto, Groupdocs.Editor ofrece una integración perfecta con aplicaciones web desarrolladas en el marco .NET.
### ¿Groupdocs.Editor brinda soporte para servicios de almacenamiento en la nube?
Sí, Groupdocs.Editor admite la integración con servicios populares de almacenamiento en la nube como Google Drive, Dropbox y Microsoft OneDrive.
### ¿Existe una prueba gratuita disponible para Groupdocs.Editor?
Sí, puede aprovechar una prueba gratuita de Groupdocs.Editor desde el sitio web.
### ¿Cómo puedo obtener soporte técnico para Groupdocs.Editor?
Para obtener asistencia técnica y soporte de la comunidad, puede visitar el foro Groupdocs.Editor.