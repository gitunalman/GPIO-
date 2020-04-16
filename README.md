## Pines de entrada/salida STM32L476

El pin de entrada / salida de uso general del microcontrolador STM32 (GPIO) proporciona muchas formas de interactuar con circuitos externos dentro de un marco de aplicación.

En este documento daremos una breve explicación de su uso y configuración.

#### Estructura basica de un GPIO en un microcontrolador SMT32F4 (Similar al STM32L476)
<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO1.png" />

En la imagen anterior se muestra la estructura interna de un GPIO. En el recuadro Azul se muestran las posibles configuraciones de entrada, en el rojo las posibles configuraciones de salida y el recuadro verde muestra las configuraciones disponibles para las resistencias de Pull.





#### Glosario:
Esta sección define las principales siglas y abreviaturas utilizadas para la configuración de las entradas/salidas GPIO.
* AMR: Puntaje máximo absoluto
* GPIO: Entrada/salida de uso general
* PP: Push Pull
* PU: Pull Up
* PD: Pull Down
* OD: Drenaje abierto 
* AF funciona alternativa
* VIH: El nivel mínimo de voltaje que se interpreta como un 1 lógico por una entrada digital
* VIL: El nivel de voltaje máximo que se interpreta como un 0 lógico por una entrada digital
* VOH: El nivel de voltaje mínimo garantizado que proporciona una salida digital establecida en el valor lógico 1
* VOL: El nivel de voltaje máximo garantizado que proporciona una salida digital establecida en el valor lógico 0
* VDD: fuente de alimentación externa para las I/Os
* VDDIO2: fuente de alimentación externa para las I/Os, independiente de voltaje VDD
* VDDA: fuente de alimentación externa para analógico
* VSS: tierra
* IIH: corriente de entrada cuando la entrada es 1
* ILH: corriente de entrada cuando la entrada es 0
* IOH: corriente de salida cuando la salida es 1 
* IOL: corriente de salida cuando la salida es 0
* IIKG: corriente de fuga
* IINJ: corriente inyectada


#### Abreviación de los registros:

* GPIOx_MODER: 		Registro de modo de puerto GPIO
* GPIOx_OTYPER:		Registro de tipo de salida GPIO
* GPIOx_OSPEEDR:		Registro de velocidad de salida GPIO
* GPIOX_PUPDR:		Registro pull-up/pull-down GPIO
* GPIOx_IDR:			Registro de datos de entrada del puerto GPIO
* GPIOx_ODR:		Registro de datos de salida del puerto GPIO
* GPIOx_BSRR:		Registro Set / Reset GPIO
* GPIOx_LCKR:		Registro de configuración de bloqueo GPIO
* GPIOx_AFRL:		Registro bajo de función alternativa
* GPIOx_AFRH:		Registro alto de función alternativa
* GPIOx_ASCR:		Registro de control de interruptor analógico de puerto GPIO



#### Características Principales de los GPIO 

* Estados de salida: Push-Pull, Open Drain + resistencia de Pull o Down, analógico.
* Estados de entrada: flotante, Pull-Up, Pull-Down, analógica.
* Velocidad de lectura/escritura seleccionable.
* Bloqueo de GPIO.
* Selección de funciones alternativas.
* Tolerantes a 5v.
* Casi todos los GPIO de la serie STM32 pueden ser configurados como fuente de interrupción externa.



#### Configuración de entrada digital
<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO2.png" />

El buffer de salida es deshabilitado cuando el GPIO es configurado como entrada:

* La entrada Schmitt Trigger es activada.
* Las resistencias de Pull-Up o Pull-Down están disponibles para ser activadas.
* El dato presente en el puerto puede ser leído y es muestreado tan rápido como la velocidad del puerto sea configurada.


#### Configuración de salida digital
<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO2.png" />

Cuando el GPIO es configurado como salida:

* El buffer de salida es habilitado.
* Modo Open-Drain:
* Un “0” en el registro de salida activa el N-MOS
* Un “1”En el registro de salida deja el puerto en alta impedancia (el P-MOS nunca se activa).
* Modo Push-Pull:
* Un “0” en el registro de salida activa el N-MOS mientras
* Un “1” en el registro de salida activa el P-MOS
* La entrada Schmitt Trigger es activada.
* Las resistencias de Pull-Up o Pull-Down están disponibles para ser activadas.
* Se puede leer el valor presente en el GPIO.
* Se puede leer el último valor escrito en el GPIO.
* El dato presente en el puerto puede ser leído y es muestreado tan rápido como la velocidad del puerto sea configurada.

#### Configuración de función alternativa
<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO4.png" />

Cuando el GPIO es configurado como una función alternativa:

* El buffer de salida puede ser configurado como Open-Drain o como Push-Pull.
* El buffer de salida es controlado por la señal proveniente del periférico seleccionado.
* La entrada Schmitt Trigger es activada.
* Las resistencias de Pull-Up o Pull-Down están disponibles para ser activadas.
* Se puede leer el valor presente en el GPIO.
* El dato presente en el puerto puede ser leído y es muestreado tan rápido como la velocidad del puerto sea configurada.

#### Configuración analógica
<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO5.png" />

Cuando el GPIO es configurado como analógico:

* El buffer de salida es deshabilitado.
* La entrada Schmitt Trigger es desactivada, y se fuerza un valor de “0” a la salida.
* Las resistencias de Pull-Up o Pull-Down están deshabilitadas.
* Si se intenta leer el registro de entrada siempre se obtendrá un valor de “0”.
* Además de leer valores analógicos algunos GPIO permiten escribir valores analógicos a la salida del pin.
 Nota: En configuración analógica el GPIO no es tolerante a 5v, el máximo voltaje soportado es de 3.3v.








#### Selección de velocidad de un GPIO
La arquitectura interna de los GPIO de los microcontroladores de la serie STM32F4 permite configurar la velocidad de lectura o escritura, con la finalidad de tomar mayor control sobre el ruido eléctrico generado por dicho dispositivo.

Las configuraciones de velocidades se enlistan a continuación:
* Low Speed.
* Medium Speed.
* High Speed.Very High Speed.

Dependiendo de la aplicación de cada dispositivo debe ser seleccionada dicha velocidad.


<img src="https://www.intesc.mx/wp-content/uploads/2017/06/GPIO6.png" />

Como se puede observar en la ilustración anterior, los puertos GPIO pertenecen al bus de datos AHB1, que alcanza una frecuencia superior a 84 Mhz, pero si el puerto está configurado con una función alternativa que se encuentre en el bus APB1, alcanzara una frecuencia de 48 Mhz.

## Pasos para configurar un GPIO:

* Seleccionar el número del pin de un que desea utilizar, este debe ser entre 0 y 15.

* Seleccionar el modo de operación; entrada, salida, análogo, interrupción, etc.

* Seleccionar la activación o desactivación de las resistencias de pull.

* Seleccionar la velocidad a la que trabajara dicho periférico.

* Especificar si el periférico está asociado a una función alternativa.



