---
title: Trabajar con la colección de campos de formulario heredados
linktitle: Trabajar con la colección de campos de formulario heredados
second_title: API GroupDocs.Editor .NET
description: Aprenda a administrar campos de formularios heredados usando GroupDocs.Editor para .NET con nuestra guía detallada. Perfecto para manejar campos de texto, casillas de verificación, fechas y más.
weight: 12
url: /es/net/form-field-management/work-legacy-form-field-collection/
type: docs
---
# Trabajar con la colección de campos de formulario heredados

## Introducción
Bienvenido a esta guía completa sobre cómo trabajar con colecciones de campos de formularios heredados utilizando GroupDocs.Editor para .NET. Ya sea que trabaje con campos de texto, casillas de verificación, campos de fecha o menús desplegables, este tutorial lo guiará en cada paso para administrar estos campos de manera eficiente. Al final de esta guía, tendrá un conocimiento sólido de cómo utilizar GroupDocs.Editor para manejar varios campos de formulario en sus documentos. ¡Vamos a sumergirnos!
## Requisitos previos
Antes de comenzar, asegúrese de tener los siguientes requisitos previos:
- Visual Studio: cualquier versión reciente funcionará.
- .NET Framework: asegúrese de tener .NET Framework instalado.
-  GroupDocs.Editor para .NET: descargue la última versión[aquí](https://releases.groupdocs.com/editor/net/).
- Documento de muestra: un archivo DOCX de muestra con campos de formulario para fines de prueba.
## Importar espacios de nombres
Para empezar, importe los espacios de nombres necesarios en su proyecto. Estos espacios de nombres son esenciales para acceder a las clases y métodos necesarios para manipular los campos del formulario.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Paso 1: obtenga la ruta del archivo de entrada
Primero, debe especificar la ruta a su archivo de entrada. En este ejemplo, usaremos un archivo DOCX de muestra que contiene varios campos de formulario.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Paso 2: cree una secuencia a partir de la ruta del archivo
A continuación, cree una secuencia de archivos para leer el contenido de su documento. Esta secuencia se utilizará para cargar el documento en GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // El código adicional irá aquí
}
```
## Paso 3: crear opciones de carga para el documento
Antes de cargar el documento, cree opciones de carga. Estas opciones ayudarán a manejar diferentes escenarios, como documentos protegidos con contraseña.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Si el documento está protegido con contraseña, especifique la contraseña.
loadOptions.Password = "your_password_here"; // Utilice una contraseña real si es necesario
```
## Paso 4: cargue el documento con la instancia del editor
Ahora, cargue el documento en la instancia del Editor usando la secuencia de archivos y las opciones de carga que creó anteriormente.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // El código adicional irá aquí
}
```
## Paso 5: leer la instancia de FormFieldManager
Para administrar los campos del formulario, acceda a la instancia de FormFieldManager desde el Editor. Esta instancia le permitirá interactuar con los campos del formulario dentro de su documento.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Paso 6: lea la colección FormField
Recupere FormFieldCollection de FormFieldManager. Esta colección contiene todos los campos de formulario presentes en el documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Paso 7: iterar a través de cada campo del formulario
Recorra cada campo de formulario de la colección e identifique su tipo. Dependiendo del tipo, puede extraer y manipular el valor del campo.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Paso 8: Conclusión
Si sigue estos pasos, podrá administrar e interactuar de manera efectiva con los campos de formulario heredados en sus documentos usando GroupDocs.Editor para .NET. Ya sean campos de texto, casillas de verificación, fechas, números o menús desplegables, esta guía proporciona una manera clara y concisa de manejar cada tipo.
## Conclusión
 Trabajar con campos de formulario heredados en documentos puede resultar sencillo si se utilizan las herramientas adecuadas. GroupDocs.Editor para .NET proporciona una solución sólida para administrar estos campos de manera eficiente. Si sigue esta guía paso a paso, ahora debería poder manipular varios campos de formulario en sus documentos con facilidad. No olvides explorar el[documentación](https://tutorials.groupdocs.com/editor/net/)para funciones y opciones más avanzadas.
## Preguntas frecuentes
### 1. ¿Puedo utilizar GroupDocs.Editor para .NET con documentos protegidos con contraseña?
Sí, puede especificar la contraseña en las opciones de carga para manejar documentos protegidos con contraseña.
### 2. ¿Cómo obtengo una prueba gratuita de GroupDocs.Editor para .NET?
 Puede descargar una prueba gratuita desde[aquí](https://releases.groupdocs.com/).
### 3. ¿Hay algún soporte disponible para GroupDocs.Editor para .NET?
 Sí, puedes acceder a soporte[aquí](https://forum.groupdocs.com/c/editor/20).
### 4. ¿Puedo comprar una licencia de GroupDocs.Editor para .NET?
 Sí, puedes comprar una licencia en[aquí](https://purchase.groupdocs.com/buy).
### 5. ¿Dónde puedo encontrar la documentación de GroupDocs.Editor para .NET?
La documentación está disponible.[aquí](https://tutorials.groupdocs.com/editor/net/).