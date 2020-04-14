## Pines de entrada/salida STM32L476

El pin de entrada / salida de uso general del microcontrolador STM32 (GPIO) proporciona muchas formas de interactuar con circuitos externos dentro de un marco de aplicación.



En este documento daremos una breve explicación de su uso y configuración.

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


