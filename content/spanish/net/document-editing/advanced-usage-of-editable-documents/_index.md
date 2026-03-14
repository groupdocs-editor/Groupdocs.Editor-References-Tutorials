---
date: 2026-03-14
description: Aprenda cómo extraer imágenes de DOCX, convertir DOCX a HTML y guardar
  el documento como HTML usando GroupDocs.Editor para .NET.
linktitle: Extract Images from DOCX – Advanced Editable Document Usage
second_title: GroupDocs.Editor .NET API
title: Extraer imágenes de DOCX – Uso avanzado de documentos editables
type: docs
url: /es/net/document-editing/advanced-usage-of-editable-documents/
weight: 11
---

# Extraer imágenes de DOCX – Uso avanzado de documentos editables

Si eres un desarrollador .NET que busca **extraer imágenes de DOCX** y mejorar tus capacidades de edición de documentos, GroupDocs.Editor para .NET ofrece un conjunto potente de herramientas. Esta guía completa te acompañará paso a paso en el uso avanzado de documentos editables con GroupDocs.Editor, desglosando cada paso en detalle para que puedas aprovechar todo su potencial.

## Respuestas rápidas
- **¿Cómo puedo extraer imágenes de un archivo DOCX?** Usa `EditableDocument.Images` después de cargar el documento con `Editor`.
- **¿Puedo convertir DOCX a HTML con recursos incrustados?** Sí—llama a `EditableDocument.GetEmbeddedHtml()` o `GetContent()` para obtener el marcado HTML.
- **¿Qué método guarda el documento editado como HTML?** `EditableDocument.Save(htmlFilePath)` crea un archivo HTML con una carpeta de recursos.
- **¿Es posible extraer fuentes de un documento Word?** Usa `EditableDocument.Fonts` para obtener todos los recursos de fuentes.
- **¿Necesito una licencia para uso en producción?** Se requiere una licencia válida de GroupDocs.Editor; hay una prueba gratuita disponible.

## Qué es **extract images from docx**?
Extraer imágenes de un archivo DOCX significa recuperar programáticamente cada imagen incrustada en el documento Word para que puedas reutilizarla, modificarla o almacenarla por separado. GroupDocs.Editor expone la colección `Images` en una instancia de `EditableDocument`, lo que hace que esta tarea sea sencilla.

## ¿Por qué usar GroupDocs.Editor para este flujo de trabajo?
- **Control total** sobre los recursos del documento (imágenes, fuentes, CSS) sin necesidad de manejar ZIP manualmente.  
- **Conversión sin problemas** de DOCX a HTML manteniendo el diseño y el estilo.  
- **Extracción fácil de recursos** para manejo personalizado de imágenes, incrustación de fuentes o entrega mediante CDN.  
- **Patrón de eliminación robusto** que garantiza que no haya fugas de memoria en servicios de larga duración.

## Requisitos previos
- Visual Studio instalado en tu máquina de desarrollo.  
- .NET Framework compatible con GroupDocs.Editor.  
- Biblioteca GroupDocs.Editor para .NET. Puedes [descargarla aquí](https://releases.groupdocs.com/editor/net/).  
- Una licencia válida de GroupDocs.Editor. Puedes obtener una [prueba gratuita](https://releases.groupdocs.com/) o comprar una [licencia temporal](https://purchase.groupdocs.com/temporary-license/).

## Importar espacios de nombres
Para comenzar, asegúrate de importar los espacios de nombres necesarios en tu proyecto .NET:

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

## Paso 1: Crear una instancia de EditableDocument
Primero, necesitas crear una instancia de `EditableDocument` cargando y editando un documento de entrada en un formato compatible.

```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## Cómo **extract images from DOCX**?
A continuación profundizamos en las capacidades de extracción de recursos, comenzando con la necesidad más común: obtener todas las imágenes de un archivo Word.

## Paso 2: Extraer recursos del documento
El `EditableDocument` contiene varios recursos que pueden extraerse y manipularse. Vamos a desglosarlos:

### Paso 2.1: Extraer documento completo como HTML
Puedes generar una única cadena que contenga todo el documento con todos sus recursos incrustados como HTML.

```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

### Paso 2.2: Extraer todas las imágenes *(palabra clave principal en acción)*
Extrae todas las imágenes del documento—este es el núcleo de **extract images from docx**.

```csharp
List<IImageResource> allImages = beforeEdit.Images;
```

### Paso 2.3: Extraer todas las fuentes *(palabra clave secundaria)*
Si también necesitas **extract fonts from word**, usa la siguiente llamada:

```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```

### Paso 2.4: Extraer todas las hojas de estilo
Extrae todas las hojas de estilo en formato textual.

```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```

### Paso 2.5: Reunir todos los recursos
Reúne todos los recursos en una sola llamada.

```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

Esto incluye imágenes, fuentes y hojas de estilo.

### Paso 2.6: Obtener el marcado HTML
Obtén el marcado HTML del documento sin recursos incrustados.

```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## Cómo **convert docx to html** con manejo personalizado?
A veces necesitas ajustar los enlaces externos para que apunten a tus propios manejadores de recursos.

## Paso 3: Ajustar enlaces externos
### Paso 3.1: Preparar prefijos personalizados
Prepara prefijos que se antepondrán a los enlaces externos originales.

```csharp
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://example.com/FontsHandler/id=";
```

### Paso 3.2: Generar marcado HTML con prefijos
Genera el marcado HTML con los enlaces ajustados.

```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

### Paso 3.3: Obtener contenido HTML solo del cuerpo
Algunos editores WYSIWYG solo manejan marcado HTML puro sin encabezados.

```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```

### Paso 3.4: Contenido solo del cuerpo con prefijos
Genera contenido solo del cuerpo con prefijos de imagen personalizados.

```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```

### Paso 3.5: Extraer hojas de estilo
Extrae las hojas de estilo usadas en el documento.

```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```

### Paso 3.6: Hojas de estilo con prefijos
Extrae las hojas de estilo con prefijos personalizados.

```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```

## Cómo **save document as html** correctamente?
## Paso 4: Guardar documento como HTML
Guarda el documento editado como un archivo HTML, incluyendo sus recursos.

```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```

Este método crea un directorio separado para recursos como hojas de estilo, imágenes y fuentes.

## Paso 5: Eliminar EditableDocument
`EditableDocument` implementa `IDisposable` y permite comprobar si la instancia está eliminada.

```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```

### Paso 5.1 Manejo del evento Dispose
También puedes suscribirte al evento de eliminación.

```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```

## Paso 6: Crear EditableDocument a partir de HTML
Crea una instancia de `EditableDocument` a partir de un documento HTML.

### Paso 6.1: Desde archivo HTML

```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```

### Paso 6.2: Desde marcado HTML

```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```

Estas instancias (`afterEditFromFile` y `afterEditFromMarkup`) son idénticas a la original (`beforeEdit`).

## Paso 7: Eliminación manual
Elimina manualmente tus instancias de `EditableDocument`.

```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

Esto garantiza una limpieza adecuada de los recursos.

## Problemas comunes y soluciones
- **Las imágenes no aparecen después de la extracción:** Verifica que el documento realmente contenga imágenes incrustadas y que estés accediendo a `beforeEdit.Images` después de llamar a `Edit`.  
- **Faltan fuentes en la salida HTML:** Asegúrate de llamar a `GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri)` para incrustar correctamente las URLs de fuentes.  
- **Cadenas HTML grandes que causan presión de memoria:** Usa `GetContent()` para obtener el marcado sin recursos incrustados y sirve imágenes/CSS desde archivos separados.

## Preguntas frecuentes

**P: ¿Qué formatos admite GroupDocs.Editor?**  
R: GroupDocs.Editor admite DOCX, XLSX, PPTX y muchos otros formatos de oficina populares.

**P: ¿Puedo usar GroupDocs.Editor sin una licencia?**  
R: Sí, puedes usarlo con una [prueba gratuita](https://releases.groupdocs.com/) o una [licencia temporal](https://purchase.groupdocs.com/temporary-license/).

**P: ¿Cómo extraigo recursos específicos de un documento?**  
R: Usa las colecciones `Images`, `Fonts` y `Css` en la instancia de `EditableDocument`.

**P: ¿Es posible ajustar los enlaces en la salida HTML?**  
R: Sí, pasa prefijos URI personalizados a `GetContent` o `GetBodyContent` para reescribir los enlaces de imágenes, CSS y fuentes.

**P: ¿Cómo guardo un documento editado como archivo HTML?**  
R: Llama al método `Save` en la instancia de `EditableDocument`, proporcionando una ruta de archivo que termine con `.html`.

---

**Última actualización:** 2026-03-14  
**Probado con:** GroupDocs.Editor para .NET (última versión)  
**Autor:** GroupDocs