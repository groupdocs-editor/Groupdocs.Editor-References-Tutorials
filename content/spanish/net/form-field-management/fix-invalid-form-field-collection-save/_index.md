---
title: Reparar la colección de campos de formulario no válidos y guardar
linktitle: Reparar la colección de campos de formulario no válidos y guardar
second_title: API GroupDocs.Editor .NET
description: Aprenda cómo corregir campos de formulario no válidos en DOCX usando Groupdocs.Editor para .NET. Siga esta guía para asegurarse de que sus documentos estén libres de errores y guárdelos de forma segura.
weight: 11
url: /es/net/form-field-management/fix-invalid-form-field-collection-save/
type: docs
---
# Reparar la colección de campos de formulario no válidos y guardar

## Introducción
¡Bienvenido! Si trabaja con campos de formulario en documentos y tiene problemas con colecciones de campos de formulario no válidos, está en el lugar correcto. En este tutorial, veremos cómo corregir campos de formulario no válidos y guardar su documento usando Groupdocs.Editor para .NET. Lo guiaremos a través del proceso paso a paso, asegurándonos de que tenga todos los detalles que necesita para que funcione sin problemas. ¡Empecemos!
## Requisitos previos
Antes de pasar al código, hay algunas cosas que debes tener en cuenta:
-  Groupdocs.Editor para .NET: asegúrese de haber instalado la biblioteca Groupdocs.Editor para .NET. Puedes descargarlo[aquí](https://releases.groupdocs.com/editor/net/).
- Entorno de desarrollo: debe tener configurado un entorno de desarrollo .NET, como Visual Studio.
- Conocimientos básicos de C#: este tutorial asume que tienes conocimientos básicos de programación en C#.
## Importar espacios de nombres
Primero, necesita importar los espacios de nombres necesarios en su proyecto C#. Agregue las siguientes líneas al comienzo de su archivo de código:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Paso 1: obtenga la ruta del archivo de entrada
El primer paso es especificar la ruta a su archivo de entrada. Este archivo debe ser un documento DOCX que contenga campos de formulario.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Paso 2: cree una secuencia a partir de la ruta del archivo
A continuación, cree una secuencia de archivos para leer el documento de entrada. Esto le permitirá cargar el documento en el editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Paso 3: crear opciones de carga para el documento
En este paso, debe crear opciones de carga para su documento. Si su documento está protegido con contraseña, puede especificar la contraseña. En este ejemplo, el documento no está protegido, por lo que se ignora la contraseña.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Paso 4: cargue el documento en la instancia del editor
Ahora, cargue el documento con las opciones especificadas en la instancia del Editor. Aquí es donde se realizarán las principales operaciones sobre el documento.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Paso 4.1: leer la instancia de FormFieldManager
 El`FormFieldManager` La instancia es responsable de administrar los campos del formulario en el documento. Deberá leer esta instancia para acceder y manipular los campos del formulario.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Paso 4.2: Lea FormFieldCollection
 El`FormFieldCollection` contiene todos los campos del formulario en el documento. Leerás esta colección para verificar y corregir campos de formulario no válidos.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Paso 4.3: Corrección automática de campos de formulario no válidos
Intente corregir automáticamente cualquier campo de formulario no válido en el documento. Este es un paso preliminar para abordar cuestiones obvias.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Paso 4.4: Verifique si hay campos de formulario no válidos
Compruebe si quedan campos de formulario no válidos después del intento de reparación automática.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Paso 4.4.1: Obtener todos los nombres de campos de formulario no válidos
Recupere los nombres de todos los campos del formulario no válidos. Estos nombres se utilizarán para arreglar los campos.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Paso 4.4.2: Crear nombres únicos para campos no válidos
Para cada campo de formulario no válido, cree un nombre único. Esto garantiza que no haya conflictos con los nombres de campos de formulario existentes.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Paso 4.4.3: corregir campos de formulario no válidos
Corrija los campos del formulario no válidos utilizando los nombres únicos creados en el paso anterior.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Paso 5: crear opciones para guardar el documento
Configure opciones para guardar el documento. Esto incluye especificar el formato y cualquier configuración de guardado adicional.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Paso 5.1: Optimice el uso de la memoria
 Si su documento es grande y puede causar un`OutOfMemoryException`habilite la opción de optimización de memoria.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Paso 5.2: Proteja el documento de la escritura
Para proteger el documento contra modificaciones, excepto los campos del formulario, establezca una contraseña de protección.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Paso 6: guarde el documento
Finalmente, guarde el documento con las opciones de guardado especificadas. Prepare un flujo de memoria para guardar el documento de salida.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusión
 ¡Y ahí lo tienes! Ha corregido con éxito campos de formulario no válidos y ha guardado su documento usando Groupdocs.Editor para .NET. Esta guía paso a paso debería haber dejado el proceso claro y manejable. Si tiene algún problema o tiene preguntas, no dude en consultar el[documentación](https://tutorials.groupdocs.com/editor/net/) o comuníquese con[apoyo](https://forum.groupdocs.com/c/editor/20).
## Preguntas frecuentes
### ¿Qué pasa si mi documento está protegido con contraseña?
 Puede especificar la contraseña en el`WordProcessingLoadOptions` para abrir el documento.
### ¿Cómo sé si hay campos de formulario no válidos?
 Utilizar el`HasInvalidFormFields` método para comprobar si hay campos de formulario no válidos en el documento.
### ¿Puedo arreglar campos de formulario sin cambiar sus nombres?
Se recomienda crear nombres únicos para los campos de formulario no válidos para evitar conflictos.
### ¿En qué formatos puedo guardar el documento?
 Puede guardar el documento en varios formatos como DOCX, PDF y más configurando el formato apropiado`WordProcessingFormats`.
### ¿Cómo puedo optimizar el uso de la memoria mientras guardo documentos grandes?
 Habilitar el`OptimizeMemoryUsage` opción en el`WordProcessingSaveOptions` para manejar documentos grandes de manera eficiente.