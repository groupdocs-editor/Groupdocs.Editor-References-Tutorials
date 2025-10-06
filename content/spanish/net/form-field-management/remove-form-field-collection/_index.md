---
title: Eliminar colección de campos de formulario
linktitle: Eliminar colección de campos de formulario
second_title: API GroupDocs.Editor .NET
description: Aprenda cómo eliminar campos de formulario de documentos de Word usando GroupDocs.Editor para .NET con esta guía paso a paso. Ideal para desarrolladores.
weight: 13
url: /es/net/form-field-management/remove-form-field-collection/
type: docs
---
# Eliminar colección de campos de formulario

## Introducción
¿Está buscando administrar campos de formulario en sus documentos mediante programación? GroupDocs.Editor para .NET ofrece una poderosa solución para manejar y manipular campos de formulario en varios formatos de documentos. En este tutorial, lo guiaremos a través de los pasos para eliminar colecciones de campos de formulario de un documento de Word utilizando esta sólida biblioteca. 
## Requisitos previos
Antes de profundizar en el código, asegurémonos de tener todo configurado para una experiencia fluida:
1. GroupDocs.Editor para .NET: asegúrese de haber descargado e instalado GroupDocs.Editor para .NET. Si no, puedes descargarlo.[aquí](https://releases.groupdocs.com/editor/net/).
2. Entorno de desarrollo: necesitará un entorno de desarrollo como Visual Studio.
3. .NET Framework: asegúrese de tener .NET Framework instalado en su máquina.
4.  Documento de muestra: tenga un documento de Word de muestra (p. ej.,`SampleLegacyFormFields.docx`) con campos de formulario que desea manipular.

## Importar espacios de nombres
Para comenzar, necesita importar los espacios de nombres necesarios en su proyecto .NET. Esto le permitirá acceder a las funcionalidades de GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Paso 1: cargue el documento
Primero, deberá cargar el documento que desea editar. Vamos a desglosarlo:
### Paso 1.1: Obtenga la ruta al archivo de entrada
 Debe especificar la ruta a su archivo de entrada. Para este ejemplo, usaremos un archivo de muestra llamado`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Paso 1.2: cree un FileStream a partir de la ruta
 A continuación, cree un`FileStream` para leer el documento.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Continúe con los siguientes pasos dentro de este bloque de uso.
}
```
## Paso 2: configurar las opciones de carga
Al cargar el documento, es posible que necesite especificar opciones de carga, especialmente si su documento está protegido con contraseña.
### Paso 2.1: crear opciones de carga
 Crear una instancia de`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Paso 2.2: Especifique la contraseña (si es necesario)
Si su documento está protegido con contraseña, puede especificar la contraseña.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Paso 3: cargue el documento en el editor
 Ahora, cargue el documento en el`Editor` instancia utilizando el`FileStream` y`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Continúe con los siguientes pasos dentro de este bloque de uso.
}
```
## Paso 4: acceder y administrar los campos del formulario
Con el documento cargado, ahora puede acceder y manipular los campos del formulario.
### Paso 4.1: leer el FormFieldManager
 recuperar el`FormFieldManager` desde el`Editor` instancia.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Paso 4.2: Acceda a FormFieldCollection
 Consigue el`FormFieldCollection` que contiene todos los campos del formulario en el documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Paso 4.3: eliminar un campo de formulario de texto específico
Para eliminar un campo de formulario de texto específico, ubíquelo por su nombre y luego elimínelo.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Paso 4.4: eliminar varios campos del formulario
También puede eliminar varios campos de formulario a la vez especificando sus nombres.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Paso 5: guarde el documento modificado
Después de modificar los campos del formulario, debe guardar el documento.
### Paso 5.1: crear opciones para guardar
Especifique el formato y guarde las opciones para el documento de salida.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Paso 5.2: Optimice el uso de la memoria
Si se trata de documentos grandes, es posible que desee optimizar el uso de la memoria.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Paso 5.3: Establecer protección (si es necesario)
Puede proteger el documento para que no se pueda editar más estableciendo una contraseña de escritura.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Paso 5.4: guarde el documento
 Finalmente, guarde el documento usando un`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Conclusión
¡Felicidades! Ha eliminado con éxito campos de formulario de un documento de Word utilizando GroupDocs.Editor para .NET. Esta poderosa biblioteca facilita la manipulación del contenido del documento mediante programación, lo que le ahorra tiempo y esfuerzo.
## Preguntas frecuentes
### ¿Puedo utilizar GroupDocs.Editor para .NET con otros formatos de documentos?
Sí, GroupDocs.Editor para .NET admite varios formatos de documentos, incluidos PDF, HTML y más.
### ¿Es posible agregar campos de formulario usando GroupDocs.Editor para .NET?
Sí, puede agregar, modificar y eliminar campos de formulario mediante programación.
### ¿Qué pasa si mi documento es muy grande?
Puede habilitar la optimización de la memoria en las opciones de guardar para manejar documentos grandes de manera eficiente.
### ¿Puedo utilizar GroupDocs.Editor para .NET en una aplicación web?
¡Absolutamente! GroupDocs.Editor para .NET se puede integrar en aplicaciones web para el procesamiento de documentos del lado del servidor.
### ¿Dónde puedo obtener asistencia si tengo problemas?
 Puedes visitar el[Foro de soporte](https://forum.groupdocs.com/c/editor/20) para obtener ayuda con cualquier problema.