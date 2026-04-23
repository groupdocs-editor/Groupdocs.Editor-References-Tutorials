---
date: 2026-03-06
description: Aprende cómo manejar contenido CSS con prefijo y extraer contenido CSS
  usando GroupDocs.Editor para .NET en este tutorial detallado paso a paso.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Manejar contenido CSS con prefijo
type: docs
url: /es/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Manejar contenido CSS con prefijo

En este tutorial descubrirás **cómo manejar el prefijo CSS** al trabajar con hojas de estilo dentro de un documento usando GroupDocs.Editor para .NET. Ya sea que necesites anteponer una URL a imágenes, fuentes o cualquier recurso externo, los pasos a continuación te muestran exactamente cómo **manejar el prefijo CSS** y también cómo **extraer contenido CSS** para su procesamiento posterior.

## Respuestas rápidas
- **¿Qué significa “manejar el prefijo CSS”?** Añadir un prefijo de URL personalizado a los recursos externos referenciados en CSS.
- **¿Qué método de la API devuelve los estilos CSS?** `EditableDocument.GetCssContent(...)`.
- **¿Necesito una licencia?** Hay una licencia de prueba disponible; se requiere una licencia comercial para producción.
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+ y .NET Core/5/6.
- **¿Puedo cambiar el prefijo en tiempo de ejecución?** Sí – simplemente pasa una cadena diferente a `GetCssContent`.

## Qué es **manejar el prefijo CSS**?
Aplicar un prefijo a los recursos CSS reescribe las rutas de imágenes, fuentes u otros activos para que apunten a una ubicación que controlas (p. ej., un CDN o un servidor seguro). Esto es especialmente útil cuando exportas un documento y necesitas que todas las referencias externas sean accesibles desde una aplicación web.

## Por qué usar GroupDocs.Editor para **extraer contenido CSS**?
GroupDocs.Editor puede leer el CSS original incrustado en documentos de procesamiento de texto, proporcionarte las cadenas de hojas de estilo sin procesar y permitirte manipularlas antes de renderizar o guardar. Esto elimina la necesidad de análisis manual y garantiza que el CSS extraído coincida con la representación interna del documento.

## Requisitos previos
- Visual Studio: Necesitarás una instalación funcional de Visual Studio.  
- .NET Framework: Asegúrate de que tienes instalado el .NET Framework.  
- GroupDocs.Editor para .NET: Puedes descargarlo [aquí](https://releases.groupdocs.com/editor/net/).  
- Documento de muestra: Ten un documento de muestra listo para editar.

## Importar espacios de nombres
Primero, importemos los espacios de nombres necesarios para garantizar que nuestro código se ejecute sin problemas. Este paso nos brinda acceso a las clases principales de GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Paso 1: Inicializar el Editor
El primer paso consiste en crear una instancia de `Editor` con tu documento de muestra. Esto configura el entorno de edición.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Paso 2: Editar el documento
A continuación, obtenemos un objeto `EditableDocument`. Este objeto representa la versión editable del archivo y nos permite trabajar con sus partes internas.

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

## Paso 4: **Extraer contenido CSS** con los prefijos
Llama a `GetCssContent`, pasando los prefijos que acabas de definir. El método devuelve una lista de cadenas de hojas de estilo CSS que ya contienen las URLs con prefijo.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Paso 5: Mostrar los resultados
Imprime la cantidad de hojas de estilo encontradas y muestra cada hoja de estilo. Esto te ayuda a verificar que los prefijos se aplicaron correctamente.

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
- **No se devolvieron hojas de estilo** – Asegúrate de que el documento fuente realmente contenga CSS (p. ej., un documento Word con tablas con estilo o HTML incrustado).  
- **URLs incorrectas** – Verifica que las cadenas de prefijo terminen con el delimitador apropiado (`/` o `=`) para el enrutamiento de tu servidor.  
- **Problemas de rendimiento** – Para documentos muy grandes, considera procesar las hojas de estilo en lotes para evitar un alto consumo de memoria.

## Conclusión
Manejar contenido CSS con un prefijo usando GroupDocs.Editor para .NET es sencillo y potente. Siguiendo estos pasos puedes **manejar el prefijo CSS**, obtener el CSS sin procesar mediante **extraer contenido CSS**, e integrar sin problemas recursos externos en tu flujo de trabajo web. Explora otras funciones de GroupDocs.Editor como la conversión a HTML, extracción de imágenes y combinación de documentos para obtener aún más valor de la API.

## Preguntas frecuentes
### ¿Puedo usar GroupDocs.Editor para .NET con otros formatos de documento?
Sí, GroupDocs.Editor para .NET admite varios formatos de documento, incluidos PDF, Word, Excel y más.

### ¿Hay una prueba gratuita disponible para GroupDocs.Editor para .NET?
¡Absolutamente! Puedes iniciar tu prueba gratuita [aquí](https://releases.groupdocs.com/).

### ¿Cómo obtengo una licencia temporal para GroupDocs.Editor para .NET?
Puedes obtener una licencia temporal [aquí](https://purchase.groupdocs.com/temporary-license/).

### ¿Dónde puedo encontrar documentación detallada para GroupDocs.Editor para .NET?
La documentación detallada está disponible [aquí](https://tutorials.groupdocs.com/editor/net/).

### ¿Qué opciones de soporte están disponibles para GroupDocs.Editor para .NET?
Puedes obtener soporte [aquí](https://forum.groupdocs.com/c/editor/20).

## Preguntas frecuentes adicionales

**Q: ¿Puedo cambiar el prefijo después de extraer el CSS?**  
A: Sí. Llama a `GetCssContent` nuevamente con una cadena de prefijo diferente; el método siempre usa los valores que pasas en tiempo de ejecución.

**Q: ¿Esto funciona con documentos protegidos con contraseña?**  
A: Sí. Proporciona la contraseña en `WordProcessingLoadOptions` al crear la instancia de `Editor`.

**Q: ¿Es posible guardar el CSS modificado de nuevo en el documento?**  
A: Actualmente GroupDocs.Editor proporciona acceso de solo lectura al CSS. Para persistir los cambios deberías reemplazar la hoja de estilo original usando las API XML subyacentes del documento.

---

**Última actualización:** 2026-03-06  
**Probado con:** GroupDocs.Editor 23.12 para .NET  
**Autor:** GroupDocs