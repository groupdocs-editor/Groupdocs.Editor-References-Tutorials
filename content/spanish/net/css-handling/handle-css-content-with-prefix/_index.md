---
date: 2026-09-26
description: Aprenda cómo manejar el prefijo css y extraer contenido css usando GroupDocs.Editor
  para .NET en este tutorial detallado paso a paso.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Manejar contenido CSS con prefijo
og_description: Descubra cómo manejar el prefijo css y extraer contenido css con GroupDocs.Editor
  para .NET. Siga una guía paso a paso para anteponer URLs a los recursos CSS y recuperar
  hojas de estilo.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Cómo manejar el prefijo css en GroupDocs.Editor para .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Cómo manejar el prefijo css en GroupDocs.Editor para .NET
type: docs
url: /es/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Cómo manejar el prefijo CSS en GroupDocs.Editor para .NET

En este tutorial aprenderás **cómo manejar el prefijo CSS** al trabajar con hojas de estilo dentro de un documento usando GroupDocs.Editor para .NET. Ya sea que necesites anteponer una URL a imágenes, fuentes o cualquier recurso externo, los pasos a continuación te muestran exactamente cómo **manejar el prefijo CSS** y también cómo **extraer contenido CSS** para su posterior procesamiento. Al final de la guía podrás reescribir rutas de recursos, recuperar las cadenas CSS sin procesar e integrarlas en tu flujo de trabajo web con confianza.

## Respuestas rápidas
- **¿Qué significa “manejar el prefijo CSS”?** Añadir un prefijo de URL personalizado a los recursos externos referenciados en CSS.  
- **¿Qué método de API devuelve los estilos CSS?** `EditableDocument.GetCssContent(...)`.  
- **¿Necesito una licencia?** Hay una licencia de prueba disponible; se requiere una licencia comercial para producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+ y .NET Core/5/6.  
- **¿Puedo cambiar el prefijo en tiempo de ejecución?** Sí, simplemente pasa una cadena diferente a `GetCssContent`.

## Qué es manejar el prefijo CSS?
El término se refiere a reescribir las URL de imágenes, fuentes o cualquier activo externo dentro de un archivo CSS para que apunten a una ubicación que controles, como un CDN o un servidor seguro. Al anteponer una URL base consistente garantizas que cada recurso se cargue correctamente cuando el documento se renderiza en un navegador o en un visor web.

## ¿Por qué usar GroupDocs.Editor para extraer contenido CSS?
GroupDocs.Editor puede leer el CSS original incrustado en documentos de procesamiento de texto, devolver las cadenas de hojas de estilo sin procesar y permitirte manipularlas antes de renderizar o guardar. Esto elimina el análisis manual, garantiza la fidelidad a la representación interna del documento y soporta **más de 30 formatos de archivo** mientras procesa archivos de hasta **500 MB** sin cargar todo el archivo en memoria.

## Requisitos previos
Antes de comenzar, asegúrate de que tienes los siguientes requisitos:
- Visual Studio: Necesitarás una instalación funcional de Visual Studio.  
- .NET Framework: Asegúrate de que tienes instalado el .NET Framework.  
- GroupDocs.Editor for .NET: Puedes descargarlo desde la [Página de descarga de GroupDocs.Editor para .NET](https://releases.groupdocs.com/editor/net/).  
- Documento de muestra: Ten un documento de muestra listo para editar.

## Importar espacios de nombres
Primero, importemos los espacios de nombres necesarios para asegurar que nuestro código se ejecute sin problemas. Este paso nos brinda acceso a las clases principales de GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Paso 1: Inicializar el Editor
La clase `Editor` es el punto de entrada para trabajar con documentos en GroupDocs.Editor. Gestiona las operaciones de carga, edición y guardado.  
El primer paso implica crear una instancia de `Editor` con tu documento de muestra. Esto configura el entorno de edición.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Paso 2: Editar el documento
El objeto `EditableDocument` representa la versión editable del archivo y expone sus partes internas, como CSS, imágenes y HTML.  
A continuación, obtenemos un objeto `EditableDocument`. Este objeto nos permite trabajar con el CSS interno del documento.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Paso 3: Establecer prefijos externos
Define los prefijos de URL para imágenes y fuentes. Estos prefijos se antepondrán a cada referencia de imagen y fuente encontrada en el CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Paso 4: Extraer contenido CSS con los prefijos
`GetCssContent` devuelve una colección de cadenas de hojas de estilo CSS que ya contienen las URL con prefijo que proporcionaste.  
Llama a `GetCssContent`, pasando los prefijos que acabas de definir. El método devuelve una lista de cadenas de hojas de estilo CSS que ya contienen las URL con prefijo.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Paso 5: Mostrar los resultados
Imprime el número de hojas de estilo encontradas y muestra cada hoja de estilo. Esto te ayuda a verificar que los prefijos se aplicaron correctamente.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Problemas comunes y soluciones
- **No se devolvieron hojas de estilo** – Asegúrate de que el documento fuente realmente contenga CSS (p. ej., un documento Word con tablas con estilo o HTML incrustado).  
- **URL incorrectas** – Verifica que las cadenas de prefijo terminen con el delimitador apropiado (`/` o `=`) para el enrutamiento de tu servidor.  
- **Problemas de rendimiento** – Para documentos muy grandes, considera procesar las hojas de estilo en lotes para evitar un alto uso de memoria.

## Preguntas frecuentes

**Q: ¿Puedo usar GroupDocs.Editor para .NET con otros formatos de documento?**  
A: Sí, GroupDocs.Editor para .NET soporta PDF, Word, Excel, PowerPoint y muchos otros formatos.

**Q: ¿Hay una prueba gratuita disponible para GroupDocs.Editor para .NET?**  
A: ¡Absolutamente! Puedes iniciar tu prueba gratuita en la [página de prueba gratuita de GroupDocs](https://releases.groupdocs.com/).

**Q: ¿Cómo obtengo una licencia temporal para GroupDocs.Editor para .NET?**  
A: Puedes obtener una licencia temporal en la [página de licencia temporal](https://purchase.groupdocs.com/temporary-license/).

**Q: ¿Dónde puedo encontrar documentación detallada para GroupDocs.Editor para .NET?**  
A: La documentación detallada está disponible en el [sitio de documentación de GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: ¿Qué opciones de soporte están disponibles para GroupDocs.Editor para .NET?**  
A: Puedes obtener soporte a través del [foro de soporte de GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Preguntas frecuentes adicionales

**Q: ¿Puedo cambiar el prefijo después de extraer el CSS?**  
A: Sí. Llama a `GetCssContent` nuevamente con una cadena de prefijo diferente; el método siempre usa los valores que pases en tiempo de ejecución.

**Q: ¿Esto funciona con documentos protegidos con contraseña?**  
A: Sí. Proporciona la contraseña en `WordProcessingLoadOptions` al crear la instancia de `Editor`.

**Q: ¿Es posible guardar el CSS modificado de nuevo en el documento?**  
A: GroupDocs.Editor actualmente proporciona acceso de solo lectura al CSS. Para persistir los cambios necesitarías reemplazar la hoja de estilo original usando las API XML subyacentes del documento.

---

**Última actualización:** 2026-09-26  
**Probado con:** GroupDocs.Editor 23.12 para .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Extraer CSS externo de documentos Word usando GroupDocs.Editor .NET: Guía completa](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extraer y prefijar HTML de documentos Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Cómo extraer y modificar contenido HTML en documentos Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)