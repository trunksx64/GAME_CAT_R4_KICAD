# Game//Cat ::: Revisión R4 :: Versión 4.2.2

![](https://github.com/trunksx64/GAME_CAT_R4_KICAD/blob/master/Images/Front.png)

## Razón e Inspiración

El Game//Cat R4 es la evolución del microcontrolador de 16Bits a 32Bits, mas específicamente del PIC24H al ATSAMD21 como núcleo de control, al igual que su antecesor la idea de esta tarjeta y/ó control de desarrollo es usar dispositivos específicos para el aprendizaje, bricolaje y Hobby para proyectos abiertos o de diseño cerrado, el Hardware el Libre con la posibilidad de adaptarlo, modificarlo, cambiarlo a necesidad, claramente respetando al original. El ATSAMD21 es un microcontrolador Originalmente diseñado por ATMEL que utiliza un Nucleo ARM 0M+ dando la ventaja de ser un microcontrolador fácil de usar con Módulos flexibles y robustos, con documentación abundante tanto por lo Comunidad de ARDUINO y la empresa Microchip en este momento. Se diseñó empleando de forma similar la apariencia del Game//Cat R3, agregando mejoras y eliminando errores del anterior, por lo cual es 100% compatible a nivel de diseño.

El ATSAMD21 es compatible en este momento con Microchip Studio (Atmel Studio) y MPLABX V5.0, tanto con GCC y XC32, para programarlo se puede usar ATMEL ICE, MPLAB SNAP, PICKIT4 y El ICD4, Se planea usar el Bootloader original de ARDUINO Zero en un futuro.

Algunos Elementos "Footprints" y "Symbols" están basados en mis librerías, cuáles encontrarán en este mismo Repositorio.

## Características del Hardware

  * Microcontrolador ATSAMD21.
  * Pantalla LCD PCD8544 (Based Nokia GLCD) - SPI.
  * Joystick Análogo de 2 ejes + Botón Digital.
  * 6 Botones Digitales.
  * Accelerometro - MMA8452Q - I2C. 
  * Sensor de Temperatura (LM61).
  * Sensor de Luz (LDR).
  * Memoria Eeprom 24LCXXX - I2C.
  * Memoria Ram 23KXX - SPI.
  * Memoria Flash SST26VF032B - SPI.
  * Ranura Memoria Micro-SD - SPI.
  * Buzzer por PWM.
  * Conexión USB - Nativa por el ATSAM.
  * Conexión CAN-FD - MCP2518FD.
  * 2 LED´s de Actividad.
  * Salidas Para PWM y UART - Con figurables - 3.3V.
  * Conexión SWD Nativa para Debuger.
  * Cargador de Batería Lipo (MCP73831) con Indicador LED.
  * Regulación 3.3V mediante TPS54231.

## Características Específicas

* Para garantizar el control y tensión correspondiente para el uso de BUS CAN, se utiliza el Transeiver MCP2562FD en conjunto del CI MCP2518FD, haciendo compatible el Control con la última version del protocolo CAN.

* Para Potabilidad he agregado un control para la carga de Baterías de tipo Lipo, este gobernado él con el CI MCP73831, el cual intercambia la alimentación proveniente del conector USB y la Batería según el estado de conexión, se puede usar Baterías de 3,7V en adelante hasta un máximo de 6V, se agregó un interruptor para porder desconectar la Batería en modo portable, para evitar su descarga prologanda.

* Para el Manejo del Joystick, Botones, he empleado el CI-74HC4051, que es un Multiplexor Análogo para leer los Valores por el módulo ADC, el cual puede usarse de 10 o 12Bits en conjunto con un canal DMA si fuere necesario.

* La Comunicación por algunos de los Módulos SERCOM disponibles en los conectores Molex, posee un conversor de tensión de 3.3V a 5V de forma bidireccional con transistores Mosfet, con el fin de proteger y poder comunicar el ATSAMD21 con cualquier tipo de dispositivo.

* La Comunicación USB está dedicada por el mismo ATSAMD21, por lo que es necesario programar el Stack propio, este microcontrolador posee una enorme flexibilidad para configurar impactando de forma mínima los recursos. Es posible utilizar el Bootloader del Arduino Zero con algunas modificaciones, aún está en planes de creación, recomiendo emplear el código Generado por AMTEL START, para simplificar las configuraciones tanto de este Módulo como otros Periféricos.

* La Ranura para la Tarjeta Micro-SD, posee conexión Módulo SPI la cual esta compartida con la Memoria Ram 23Kxxx y Memoria Flash SST26VF032B, Además la pantalla posee también una conexión al segundo Módulo SPI, que puede usarse para "colgar" otros dispositivos si no vamos a usar la Pantalla.

* El control del Buzzer se ha dejado por un Pin que puede ser usado tanto por el Modulo PWM o un pin Común, su uso dependerá del Programa o Aplicación.

* Posee una Memoria I2C en conjunto con un Accelerometro, con comunicación directa.

* Los sensores de Luminosidad y Temperatura están conectados directamente a entradas Analógicas del ATSAMD21, no siendo necesario utilizar le MUX 74HC4051.

* La programación se hace por medio de la conexión ICSP o Bootloader por USB, empleando cualquier programador reciente como el ICD4, PICKIT4, SNAP o ATMEL ICE, igual estas salidas pueden usarse como cualquier puerto, teniendo presente que no poseen ninguna protección a tensiones superiores de 3,3V.

* Ya por Último, he dejado dos visualiza-dores, que usan los pines asignados para la Programación del ATSAMD21, controlados por Mosfets para no interferir con el protocolo SWD, su uso está condicionado fuera del Debug.

## Microcontrolador

  * Microcontrolador ATSAMD21 ARM 0M+ de 32Bits.
  * 256KB of flash and 32KB of SRAM.
  * Up to 48MHz operating frequency.
  * Six serial communication modules (SERCOM) configurable as UART/USART, SPI or I2C, three 16-bit timer/counters, 32-bit Real-Time Clock and calendar, 20 PWM channels, one 14-channel 12-bit ADC, one 10-bit DAC.
  * Full Speed USB Device and embedded Host.
  * 1.62V to 3.63V power supply.
  * Internal and external clock options with 48MH Digital Frequency Locked Loop (DFLL48M) and 48MHto 96MHFractional.
  * Two-pin Serial Wire Debug (SWD) programming, test and debugging interface.
  * 38 GPIO pins.
  * 10-bit, 350ksps Digital-to-Analog Converter (DAC).
  * CRC-32 generator.
  * 32-bit Real Time Counter (RTC) with clock/calendar function.
  * Generation of synchronized pulse width modulation (PWM) pattern across port pins.

## Versiones

* 2021 : 4.0.0 : Primera Versión de Diseño.
* 2021 : 4.0.1 : Mirgración completa a Kicad V6, actualización del Libreias y Logos de Diseño.
* 2021 : 4.1.0 : Cambio de Botones Pasantes a SDM.
* 2021 : 4.1.2 : Conectores Moles de tres pines a cuatro pines para Alimentación externar de dispositivos.
* 2021 : 4.1.3 : Correción y cambio de puerto de Programación SWD RJ11 a Header 2x3, similar al AVR SPI.
* 2021 : 4.1.4 : Cambio de Resistencias del conversor de nivel 5V-3.3V de 1K a 10K.
* 2022 : 4.1.5 : Se agregó Interruptor de Encendio por Batería con control Mosfet.
* 2025 : 4.2.2 : Se Corrige mosfet de los LEDs de Estado y Conexion del BUS I2C.

## Créditos

![](https://github.com/trunksx64/GAME_CAT_R4_KICAD/blob/master/Images/Banner_GameCat_R4.png)

xDNA Electronics & Desing es una Micro-empresa Personal, que se dedica y encarga de elaborar proyectos de Control y Automatización por pedido, su idea es colaborar y ayudar a quines a si lo requieran, el proyecto se hizo principalmente como Hobby el cual gracias a terceros se pudo implementar y hacer su creación, por lo cual se da la libertad de usarlo para experimentar sin hacer uso comercial del mismo.

## Licencia

![](https://github.com/trunksx64/GAME_CAT_R4_KICAD/blob/master/Images/Creative_Commons.png)

Licensed under Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)
