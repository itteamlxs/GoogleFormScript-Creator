# GoogleFormScript-Creator

# Google Forms Generator from Google Sheets

Este script permite generar un formulario de Google Forms automáticamente desde una hoja de cálculo de Google Sheets. Las preguntas se toman desde la columna **C**, comenzando desde la fila 9, y las opciones de respuesta se toman de un rango específico en la columna **K** (K8:K11).

## Descripción

El script lee los datos de un archivo de Google Sheets y crea un formulario de Google Forms. Las preguntas del formulario se toman desde la columna **C**, y las opciones de respuesta para cada pregunta se extraen del rango **K8:K11**.

### Funcionalidades:
- **Generación automática de preguntas**: Las preguntas se obtienen de la columna **C**, comenzando en la celda **C9**.
- **Opciones de respuesta**: Las opciones para cada pregunta se toman del rango **K8:K11**.
- **Creación del formulario**: El formulario es creado automáticamente usando **Google Forms**.
- **URL del formulario**: El enlace al formulario creado se muestra en el registro de Apps Script.

## Requisitos

- **Google Sheets**: El archivo de hojas de cálculo donde están las preguntas y opciones.
- **Google Forms**: Se crea automáticamente desde Google Apps Script.
- **Acceso a Google Apps Script**: Para ejecutar el script desde el editor de Apps Script.

## Instrucciones

### Paso 1: Configuración de Google Sheets

1. Abre tu archivo de **Google Sheets** donde tienes las preguntas y las opciones.
2. Asegúrate de que las preguntas estén en la **columna C**, comenzando desde la fila **9**.
3. Las opciones de las preguntas deben estar en el rango **K8:K11**. Si necesitas más opciones o preguntas, ajusta las referencias en el script.

### Paso 2: Configuración de Google Apps Script

1. Abre el archivo **Google Sheets**.
2. En el menú superior, haz clic en **Extensiones > Apps Script**.
3. En el editor de Apps Script, borra cualquier código y pega el siguiente código:

```javascript
function createForm() {
  // Abre la hoja de cálculo activa y selecciona la hoja correcta
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Hoja1');
  
  // Abre el formulario
  var form = FormApp.create('Nuevo Formulario');
  
  // Obtén las preguntas desde la columna C, comenzando desde la fila 9
  var questionsRange = sheet.getRange('C9:C'); 
  var questions = questionsRange.getValues().filter(String);  // Filtra para evitar valores vacíos
  
  // Obtén las opciones desplegables desde el rango K8:K11
  var optionsRange = sheet.getRange('K8:K11');
  var options = optionsRange.getValues().filter(String).map(function(row) {
    return row[0];  // Devuelve un array de opciones en una sola dimensión
  });

  // Crear preguntas y agregar opciones desplegables
  questions.forEach(function(row, index) {
    var questionText = row[0];  // La pregunta en la fila correspondiente
    
    // Agregar la pregunta con las opciones desplegables
    var item = form.addListItem();
    item.setTitle(questionText)
        .setChoiceValues(options);  // Asigna las opciones desde el rango K8:K11
  });

  // Muestra la URL del formulario creado
  Logger.log('Formulario creado: ' + form.getEditUrl());
}

Paso 3: Ejecutar el Script
Haz clic en el botón de Ejecutar (ícono de play en el editor de Apps Script).
La primera vez que ejecutes el script, se te pedirá que autorices el acceso de Google Apps Script a tu cuenta.
Después de ejecutar el script, se generará un formulario en Google Forms.
La URL del formulario se mostrará en el registro de Apps Script (puedes verla bajo Ver > Registro).
Paso 4: Obtener la URL del Formulario
Una vez ejecutado el script, el enlace del formulario se muestra en el registro de Apps Script. Puedes acceder al formulario usando ese enlace.
Personalización
Preguntas: Puedes modificar el rango de preguntas cambiando la referencia sheet.getRange('C9:C') si tus preguntas están en otro rango.
Opciones de respuesta: Si las opciones de respuesta son diferentes o están en un rango distinto, ajusta la referencia sheet.getRange('K8:K11') a la ubicación correspondiente.
Tipo de Pregunta: El script está configurado para crear preguntas tipo "Lista desplegable". Si prefieres otro tipo de pregunta (por ejemplo, opción múltiple), puedes modificar form.addListItem() por form.addMultipleChoiceItem().
Limitaciones
Este script supone que todas las preguntas tienen las mismas opciones. Si tienes diferentes opciones para cada pregunta, el script necesitaría modificaciones adicionales.
El script no maneja validación de preguntas obligatorias o tipos de pregunta complejos, aunque se pueden agregar funcionalidades personalizadas.
Recursos adicionales
Google Apps Script Documentation
Google Sheets API



### Explicación de la documentación:

- **Introducción**: Explica qué hace el script, cómo genera el formulario y qué datos necesita.
- **Requisitos**: Lista los elementos necesarios para ejecutar el script.
- **Instrucciones**: Guía paso a paso sobre cómo usar el script, incluyendo cómo configurar Google Sheets, configurar Google Apps Script y ejecutar el script.
- **Personalización**: Explica cómo modificar el código si necesitas adaptarlo a tus necesidades.
- **Limitaciones**: Señala algunas de las limitaciones que tiene el script en su forma actual.
- **Recursos adicionales**: Enlaces a la documentación oficial para obtener más detalles sobre **Google Apps Script** y **Google Sheets API**.
