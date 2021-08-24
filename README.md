# autofirma-gecos

Paquete para instalar AutoFirma en GECOS/Guadalinex/Ubuntu

El [paquete oficial de AutoFirma](https://github.com/ctt-gob-es/clienteafirma) utiliza un programa en Java para realizar la instalación. 

Este [instalador Java](https://github.com/ctt-gob-es/clienteafirma/tree/master/afirma-ui-simple-configurator/src/main/java/es/gob/afirma/standalone/configurator) es poco transparente y dificulta la tarea del mantenedor de paquetes: crea unos scripts al vuelo, lleva incrustado un binario (certutil), no cumple las normas de Debian...

Para los despliegues masivos necesitamos un instalador silencioso, que no muestre diálogos al usuario y que podamos revisar y mantener fácilmente.

Así nace este repositorio.

En el directorio sources está lo necesario para generar un paquete binario Debian de AutoFirma. 

Si cambia la versión de AutoFirma, sólo hay que:

* Cambiar el fichero AutoFirma de sources/usr/bin/
* Cambiar el número de versión en sources/DEBIAN/control
* Generar un nuevo paquete con el comando:
 
 ```
   sudo dpkg -b sources  autofirma_X-gecosY.deb
 ```  
   (Donde X es la versión de AutoFirma e Y la versión del paquete)
   
## Cambios respecto al paquete oficial

* Utiliza un procedimiento de instalación mas transparente y ligero, que no requiere Java
* Agrega al menú una opción para que un usuario pueda reinstalarse fácilmente el certificado de AutoFirma 
* Agrega al administrador de archivos (Nemo) una opción para firmar documentos con el botón derecho
* Desinstalación mejorada, sin dejar rastros de configuración
* Corrige el script de lanzamiento de la aplicación Java para mejorar el parseo de parámetros (gracias #vokimon!)
