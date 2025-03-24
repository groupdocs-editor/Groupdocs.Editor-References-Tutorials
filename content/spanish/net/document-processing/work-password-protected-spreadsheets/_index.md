---
title: Trabajar con hojas de cálculo protegidas con contraseña
linktitle: Trabajar con hojas de cálculo protegidas con contraseña
second_title: API GroupDocs.Editor .NET
description: Aprenda a manejar hojas de cálculo protegidas con contraseña utilizando GroupDocs.Editor para .NET. Esta guía detallada lo guiará desde cómo abrir hasta cómo guardar archivos seguros de Excel.
weight: 18
url: /es/net/document-processing/work-password-protected-spreadsheets/
---

# Trabajar con hojas de cálculo protegidas con contraseña

## Introducción
¿Tiene dificultades para administrar hojas de cálculo protegidas con contraseña en sus aplicaciones .NET? Si es así, ¡estás en el lugar correcto! En esta guía completa, lo guiaremos a través del proceso de uso de GroupDocs.Editor para .NET para manejar hojas de cálculo protegidas con contraseña de manera eficiente. Al final de este tutorial, estará bien equipado para abrir, editar y guardar archivos de Excel cifrados con facilidad.
## Requisitos previos
Antes de profundizar en el código, asegurémonos de tener todo lo que necesita para seguirlo:
- Conocimientos básicos de C#: este tutorial asume que está familiarizado con la programación en C#.
- .NET Framework: asegúrese de tener .NET Framework instalado en su máquina de desarrollo.
-  GroupDocs.Editor para .NET: descargue e instale GroupDocs.Editor para .NET desde[aquí](https://releases.groupdocs.com/editor/net/).
## Importar espacios de nombres
Para comenzar, deberá importar los espacios de nombres necesarios en su proyecto C#. Estos espacios de nombres brindan acceso a las funcionalidades de GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Paso 1: obtenga una ruta al archivo de entrada
Primero, necesitará una ruta al archivo de entrada. Para este ejemplo, usaremos un archivo Excel de muestra (`Your Sample Document`) que esté protegido por contraseña.
```csharp
string inputFilePath = "Your Sample Document";
```
## Paso 2: intente abrir el documento sin contraseña
Veamos qué pasa si intentamos abrir el documento sin proporcionar una contraseña.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Paso 3: intente especificar una contraseña incorrecta
Ahora, especificaremos una contraseña incorrecta para demostrar cómo responde el editor.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Paso 4: abra el archivo con la contraseña correcta
Proporcionemos la contraseña correcta y abramos el archivo correctamente.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Paso 5: crear y ajustar las opciones de edición
Para editar la hoja de cálculo, necesitamos crear y ajustar las opciones de edición.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Paso 6: cree un documento editable intermedio
 A continuación, creamos un intermedio.`EditableDocument` que nos permite realizar cambios en la hoja de cálculo.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Paso 7: crear opciones para guardar
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Paso 7.1: Establecer una nueva contraseña de apertura
    saveOptions.Password = "new password";
    // Paso 7.2: configurar la protección contra escritura
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Paso 8: guarde el documento sin modificaciones
    //Paso 8.1: preparar el nombre del archivo de salida y la ruta
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Paso 8.2: Crear flujo de salida
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Paso 8.3: Guardar
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Paso 9: Deseche la instancia del editor
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Conclusión
¡Felicidades! Ha aprendido con éxito cómo manejar hojas de cálculo protegidas con contraseña utilizando GroupDocs.Editor para .NET. Desde intentar abrir el documento sin contraseña hasta guardarlo con nuevas configuraciones de protección, ha cubierto todos los pasos esenciales. Sin duda, este conocimiento mejorará su capacidad para administrar documentos seguros dentro de sus aplicaciones .NET.
## Preguntas frecuentes
### ¿Qué es GroupDocs.Editor para .NET?
GroupDocs.Editor para .NET es una potente API de edición de documentos que permite a los desarrolladores cargar, editar y guardar una variedad de formatos de documentos dentro de aplicaciones .NET.
### ¿Cómo puedo obtener una licencia temporal para GroupDocs.Editor?
 Puede obtener una licencia temporal de[aquí](https://purchase.groupdocs.com/temporary-license/) para evaluar las características del producto.
### ¿Es posible optimizar el uso de la memoria al editar documentos grandes?
 Sí, puede habilitar la optimización de la memoria configurando el`OptimizeMemoryUsage` propiedad a`true`en las opciones de carga.
### ¿Puedo establecer contraseñas diferentes para abrir y escribir en una hoja de cálculo?
¡Absolutamente! Puede establecer contraseñas separadas para abrir el documento y para protección contra escritura usando las opciones de guardar.
### ¿Dónde puedo encontrar documentación más detallada?
 Puede acceder a la documentación completa de GroupDocs.Editor para .NET[aquí](https://tutorials.groupdocs.com/editor/net/).