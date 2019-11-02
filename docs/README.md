# GRUPO DE TRABAJO 06
## INTEGRANTES DEL GRUPO
#### Juan Pablo Fiagá Rodríguez   1002461990
#### Iván leonardo Tamayo Pérez   1052394290
#### Juan Alonso Rubiano Portela    80759456

## Objetivos
* Analizar la máxima memoria RAM que se puede alojar en la FPGA (no mayor al 75%).
* Plantear el método de adquisición de los datos de la cámara.
* Simular e implementar los diseños hechos.

## Pregunta 1:

¿Cuál es el tamaño máximo de buffer de memoria que puede crear?, se recomienda leer las especificaciones de la FPGA que está usando cada grupo. La respuesta se debe dar en bytes.

El tamaño calculado para la matriz fue hecho pensando en un tamaño de imágen de 320px x 240px = 76800 pixels de la siguiente forma:

![calculos](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/calculos.png)

Teniendo en cuenta que el tamaño en bits del block RAM de la Nexys 4: FPGA Artix-7 es de 4860 Kb se verifica que **Tamaño de datos < Tamaño de Matriz < Tamaño RAM FPGA**.

Dando un porcentaje usado menor al 50%.


![porcentaje](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/porcentaje.png)


Finalmente **AW=17** y **DW=16**.

![Matriz](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/Matriz.png)

## Pregunta 2:

¿Cuál formato y tamaño de imagen de la cámara OV7670 se ajusta mejor al tamaño de memoria calculado en la pregunta 1?. Para ello revisar la hoja de datos de la cámara OV7670. Revisar el datasheet que se encuentra aquí

Teniendo en cuenta las respuestas dadas en la pregunta 1 el tamaño de la imágen será de 320 pixels horizontales x 240 pixels verticales, es decir 1/2 de la resolución original.

![320x240sample](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/320x240sample.png)

Donde el formato será RGB565, el cuál está estructurado de la siguiente manera para cada pixel:

![RGB565](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/RGB565.png)

*Podría haberse usado el formato YUV 4:2:2, el cuál al ser de 8 bits por cada pixel, permitiría ahorrar memoria al coste de bajar un poco la calidad del color, pero sin embargo, no se utilizó dada la incertidumbre con respecto al monitor que se iba a usar, en el cual se iba a mostrar la imágen el cuál para este formato debería ser VGA*

## Pregunta 3:

¿Cuáles son los registros de configuración de la cámara OV7670 que permiten tener la configuración dada en la pregunta 2? Revisen los registros dados de la página 11 a la 26 del datasheet e indiquen la configuración para:

* Restablecer todos los registros

- Dirección 12, COM7 Bit[7] (SCCB Register Reset, 0: No change, 1: Resets all registers to default values)

Página 13 en Datasheet
    
* Habilitar el escalado

Dirección 0D | Common control 4 (Average option, same value as COM17)
------------ | -------------
  4 Bit [5:4] | 00:Full window

. |01:1/2 window

. |10:1/4 window

. |11:1/4 window


Dirección 42 | Common control 17
------------ | -------------
Bit [7:6] | 00:Normal

' |01:1/2

. |10:1/4

' |11:1/4

Página 12 en Datasheet

* Configurar el formato y el tamaño del pixel


- Dirección 40, COM15 Bit[5:4]=01.

- Dirección 12, COM7 Bit[2] (Output Format - RGB selection)

Bit[1] (Color Bar)

Bit[0] (Output form - Raw RGB).

Página 18 en datasheet


* Habilitar el test de barra de colores

- Dirección 70, SCALING_XSC Bit[7] y

Bit[6:0] (Horizontal scale factor)

- Dirección 71, SCALING_YSC Bit[7] y 

Bit[6:0] (Vertical scale factor)

(XBit[7], YBit[7]) (00: No test output, 01: Shifting "1", 10: 8-bar color bar, 11: Fade to gray color bar)

## Diagrama de Caja Negra
Finalmente luego de haber planteado todas las *especificaciones* de la memoria RAM se realizó el diagrama de caja negra

![Caja Negra](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/cajanegra.png)


## Simulación (TestBench):

Una vez resultas las anteriores preguntas se debe descargar el paquete de trabajo 01 de este link WP01. Una vez aceptado el repositorio debe descargarlo en su computador, para ello debe clonar el mismo. Si no sabe cómo hacerlo revise la metodología de trabajo, donde se explica el proceso

Una vez clone el repositorio, realice lo siguiente:

    Comprenda cada línea del código HDL del archivo buffer_ram_dp.v que se encuentra en la carpera src. Si cree necesario realice los respectivos comentarios en el mismo archivo.
    Configure los parámetros del ancho de palabra DW y tamaño de dirección AW, según los resultados dados en la pregunta 1 y 2.
    Cree el proyecto HDL donde el top sea buffer_ram_dp.v. Puede usar ise o construir el makefile.
    Modifique el archivo image.men, para que contenga todos los pixeles de un solo color y que corresponda a la memoria calculada.
    Modifique el archivo TB_ram, con el fin de adicionar las estímulos necesarios para simular la lectura y escritura de la memoria ram. Genera la simulación
    Revise que el sistema funciona como usted lo esperaba. Realice lo comentarios necesarios en el archivo README.md.
    Realice la respectiva publicación del repositorio antes de la fecha dada.

Para el testbench se eligó el siguiente formato de color de esta manera, visto también en otros formatos, se rellenó el archivo image.men de 76800 datos con este valor y se hizo la respectiva simulación.

![color](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/color.png)

El valor 1849 es la forma decimal del color dado, realizando la prueba de lectura de datos de entrada a la memoria:

![captura](https://github.com/unal-edigital1-2019-2/work01-ramdp-grupo-06/blob/master/docs/figs/captura.png)



