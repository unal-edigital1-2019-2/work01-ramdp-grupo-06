# GRUPO DE TRABAJO 06
## INTEGRANTES DEL GRUPO
#### Juan Pablo Fiagá Rodríguez   1002461990


## Objetivos
* Analizar la máxima memoria RAM que se puede alojar en la FPGA (no mayor al 75%).
* Plantear el método de adquisición de los datos de la cámara.
* Simular e implementar los diseños hechos.

## Pregunta 1:

¿Cuál es el tamaño máximo de buffer de memoria que puede crear?, se recomienda leer las especificaciones de la FPGA que está usando cada grupo. La respuesta se debe dar en bytes.

El tamaño calculado para la matriz fue hecho de la siguiente forma:

![calculos](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/calculos.png)

Teniendo en cuenta que el tamaño en bits del block RAM de la Nexys 4: FPGA Artix-7 es de 4860 Kb se verifica que **Tamaño de datos < Tamaño de Matriz < Tamaño RAM FPGA**.

Dando un porcentaje usado menor al 50%.
![porcentaje](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/porcentaje.png)

Finalmente **AW=17** y **DW=16**.

![Matriz](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/Matriz.png)

## Pregunta 2:

¿Cuál formato y tamaño de imagen de la cámara OV7670 se ajusta mejor al tamaño de memoria calculado en la pregunta 1?. Para ello revisar la hoja de datos de la cámara OV7670. Revisar el datasheet que se encuentra aquí

![320x240sample](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/320x240sample.png)


![RGB565](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/RGB565.png)


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

![color](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/color.png)

## Diagrama de Caja Negra
![Caja Negra](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/cajanegra.png)






