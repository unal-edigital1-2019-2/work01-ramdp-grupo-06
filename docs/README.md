# GRUPO DE TRABAJO 06
## INTEGRANTES DEL GRUPO
#### Juan Pablo Fiagá Rodríguez   1002461990


## Objetivos
* Analizar la máxima memoria RAM que se puede alojar en la FPGA.
* Plantear el método de adquisición de los datos de la cámara.
* Simular e implementar los diseños hechos.

## Pregunta 1:

¿Cuál es el tamaño máximo de buffer de memoria que puede crear?, se recomienda leer las especificaciones de la FPGA que está usando cada grupo. La respuesta se debe dar en bytes.



## Pregunta 2:

¿Cuál formato y tamaño de imagen de la cámara OV7670 que se ajusta mejor al tamaño de memoria calculado en la pregunta 1?. Para ello revisar la hoja de datos de la cámara OV7670. Revisar el datasheet que se encuentra aquí

## Pregunta 3:

¿Cuáles son los registros de configuración de la cámara OV7670 que permiten tener la configuración dada en la pregunta 2? Revisen los registros dados de la página 11 a la 26 del datasheet e indiquen la configuración para:

    Restablecer todos los registros
    Habilitar el escalado
    Configurar el formato y el tamaño del pixel
    Habilitar el test de barra de colores

Simulación (TestBench):

Una vez resultas las anteriores preguntas se debe descargar el paquete de trabajo 01 de este link WP01. Una vez aceptado el repositorio debe descargarlo en su computador, para ello debe clonar el mismo. Si no sabe cómo hacerlo revise la metodología de trabajo, donde se explica el proceso

Una vez clone el repositorio, realice lo siguiente:

    Comprenda cada línea del código HDL del archivo buffer_ram_dp.v que se encuentra en la carpera src. Si cree necesario realice los respectivos comentarios en el mismo archivo.
    Configure los parámetros del ancho de palabra DW y tamaño de dirección AW, según los resultados dados en la pregunta 1 y 2.
    Cree el proyecto HDL donde el top sea buffer_ram_dp.v. Puede usar ise o construir el makefile.
    Modifique el archivo image.men, para que contenga todos los pixeles de un solo color y que corresponda a la memoria calculada.
    Modifique el archivo TB_ram, con el fin de adicionar las estímulos necesarios para simular la lectura y escritura de la memoria ram. Genera la simulación
    Revise que el sistema funciona como usted lo esperaba. Realice lo comentarios necesarios en el archivo README.md.
    Realice la respectiva publicación del repositorio antes de la fecha dada.


![Caja Negra](./figs/cajanegra.png)
![color](./figs/color.png)
![Matriz](./figs/Matriz.png)
![RGB565](./figs/RGB565.png)
![calculos](./figs/calculos.png)
![320x240sample](./figs/320x240sample.png)


