Sigfox_y_google_sheets
======================

Introducción
------------

En este repositorio se muestra como configurar un callback hacia una hoja de calculo en google drive. Cada vez que un dispositivo dentro del Device Type que tiene el callback envie un mensaje, se creará una fila nueva en nuestro archivo 
con la información que nosotros deseemos enviar.

Primero, en nuestra cuenta de google drive nos vamos a Mi unidad -> Más -> Google Apps Script

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo1.png?raw=true)

ahora abrimos una nueva hoja de cálculo, que será donde se estarán enviando los datos

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo2.png?raw=true)

escribimos en el primer renglón de nuestra hoja de calculo las variables que deseemos enviar. En este caso las variables que se enviarán son:

-	timestamp
-	device
-	dato
-	temperatura
-	humedad

entonces, nuestro primer renglón queda de la siguiente manera

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo3.png?raw=true)

regresamos a nuestro script y pegamos lo siguiente

		function doGet(e) 
		{
 			var params = JSON.stringify(e);
 			var parametersObject = JSON.parse(params);
 
 			var timestamp = parametersObject.parameters.timestamp[0];
 			var device = parametersObject.parameters.device[0];
 			var dato = parametersObject.parameters.dato[0];
 			var temperatura = parametersObject.parameters.temperatura[0];
 			var humedad = parametersObject.parameters.humedad[0];
 
 			var ss = SpreadsheetApp.openByUrl('https://docs.google.com/spreadsheets/d/ID_DE_TU_HOJA_DE_CALCULO/edit');
 
 			var lastRow = ss.getLastRow();
 			var lastCellA = 'A'+(lastRow+1);
 			var lastCellB = 'B'+(lastRow+1);
 			var lastCellC = 'C'+(lastRow+1);
 			var lastCellD = 'D'+(lastRow+1);
 			var lastCellE = 'E'+(lastRow+1);
 
 			ss.getRange(lastCellA).setValue(timestamp);
 			ss.getRange(lastCellB).setValue(device);
			ss.getRange(lastCellC).setValue(dato);
 			ss.getRange(lastCellD).setValue(temperatura);
 			ss.getRange(lastCellE).setValue(humedad);
 
 			return HtmlService.createHtmlOutput(ss.getName()+ ' ' + lastRow + ' ' + lastCellA + ' ' + params + ' ' + parametersObject.parameters.humedad[0]);
		}	

tener cuidado de cambiar las variables por las que se desee enviar. Copiamos el ID de nuestra hoja de calculo y lo pegamos en el URL donde dice "ID_DE_TU_HOJA_DE_CALCULO" 

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo4.png?raw=true)

vamos a la pestaña "Publicar -> Implementar como aplicación web"

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo5.png?raw=true)

escribimos un nombre a nuestro proyecto

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo6.png?raw=true)

aceptamos todos los permisos que nos pida

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo7.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo8.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo9.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo10.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo11.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo12.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo13.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo13.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo14.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo15.png?raw=true)

![goo1](https://github.com/NXTIoT/Sigfox_y_google_sheets/blob/master/imagenes/goo16.png?raw=true)

