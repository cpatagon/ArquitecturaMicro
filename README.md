# Preguntas orientadoras

Describa brevemente los diferentes perfiles de familias de microprocesadores/microcontroladores de ARM. Explique alguna de sus diferenciascaracterísticas.

# Cortex M
## 1. Describa brevemente las diferencias entre las familias de procesadores Cortex M0, M3 y M4

Los procesadores ARM Cortex-M0, Cortex-M3 y Cortex-M4 pertenecen a la familia de procesadores ARM Cortex-M diseñados para sistemas embebidos y dispositivos de baja energía. Aunque comparten muchas características, hay diferencias notables entre ellos:

### Cortex-M0:

a. **Eficiencia Energética**: Está diseñado para ser extremadamente eficiente en consumo de energía y tamaño, ideal para dispositivos de bajo costo y bajo consumo de energía.

b. **Conjunto de Instrucciones**: Tiene un conjunto de instrucciones reducido en comparación con otros núcleos Cortex-M.

c. **Arquitectura**: Basado en una arquitectura von Neumann de 32 bits.
 
d. **Rendimiento**: Menor rendimiento comparado con los otros modelos, pero suficiente para tareas simples.

e. **Sin Unidad de Punto Flotante (FPU)**: No tiene capacidad de realizar cálculos de punto flotante de hardware. 

f. **Sin instrucciones SIMD**: Sin Soporte para Instrucciones SIMD (Single Instruction, Multiple Data).

### Cortex-M3:

a. **Equilibrio**: Ofrece un buen equilibrio entre rendimiento y eficiencia energética. 

b. **Conjunto de Instrucciones**: Tiene un conjunto de instrucciones más extenso que el Cortex-M0, lo que permite una mayor flexibilidad. 

c. **Arquitectura**: También basado en una arquitectura von Neumann de 32 bits. 

d. **Rendimiento**: Mayor rendimiento que el Cortex-M0 debido a características como pipeline de 3 etapas. 

e. **Sin Unidad de Punto Flotante (FPU)**: Al igual que el M0, no tiene FPU. 

f. **Sin instrucciones SIMD**: Sin Soporte para Instrucciones SIMD.

### Cortex-M4:

a. **Rendimiento**: Está diseñado para aplicaciones que requieren cálculos matemáticos complejos y control digital de señales (DSP). 

b. **Conjunto de Instrucciones**: Aún más extenso, incluye instrucciones SIMD y otras optimizaciones. 

c. **Arquitectura**: También de 32 bits y basado en la arquitectura von Neumann. 

d. **Unidad de Punto Flotante (FPU)**: Opcionalmente, puede incluir una FPU para realizar cálculos de punto flotante de manera más eficiente. 

e. **Instrucciones SIMD**: Soporte para instrucciones SIMD para mejorar el rendimiento en operaciones paralelas.

---
## 2. ¿Por qué se dice que el set de instrucciones Thumb permite mayor densidad de código? Explique

El conjunto de instrucciones Thumb en la arquitectura ARM se diseñó con el objetivo de mejorar la densidad del código. Esto significa permitir que el código compilado ocupe menos espacio de memoria sin sacrificar demasiado rendimiento. A continuación se detallan algunas de las razones por las cuales Thumb logra una mayor densidad de código:

#### Instrucciones de 16 bits
Una de las características más notables del conjunto de instrucciones Thumb es que la mayoría de sus instrucciones son de 16 bits, en lugar de 32 bits como en el conjunto de instrucciones ARM tradicional. Esto significa que se puede almacenar más código en la misma cantidad de espacio de memoria.

#### Optimización para Operaciones Comunes
El conjunto de instrucciones Thumb está optimizado para las operaciones más comunes que se realizan en aplicaciones embebidas y sistemas de baja potencia. Al proporcionar instrucciones más cortas para operaciones frecuentes, se mejora la densidad del código.

#### Compatibilidad
Thumb es compatible con el conjunto de instrucciones ARM más grande, lo que permite a los programadores cambiar entre modos ARM y Thumb en tiempo de ejecución. Esto significa que los desarrolladores pueden usar instrucciones ARM de 32 bits para tareas computacionalmente intensivas y luego cambiar a Thumb para las partes del código donde la densidad y la eficiencia son más críticas.

#### Menor Ancho de Banda de Memoria
Debido a que las instrucciones son más pequeñas, se requiere menos ancho de banda de memoria para cargarlas, lo que a su vez puede llevar a un sistema más eficiente en términos de energía.

---
## 3. ¿Qué entiende por arquitectura load-store? ¿Qué tipo de instrucciones no posee este tipo de arquitectura?

 La arquitectura Load-Store es un tipo de diseño de conjunto de instrucciones (ISA, por sus siglas en inglés) en la que las instrucciones que realizan operaciones aritméticas o lógicas operan exclusivamente en registros del procesador, en lugar de directamente en la memoria. En esta arquitectura, las operaciones de carga (load) y almacenamiento (store) son las únicas que interactúan con la memoria. Este enfoque tiene varios beneficios, como facilitar la optimización del rendimiento y simplificar el diseño del procesador.

#### Instrucciones que no posee este tipo de arquitectura

La arquitectura Load-Store generalmente no posee instrucciones que combinan operaciones aritméticas o lógicas con operaciones de acceso a memoria en una sola instrucción. Por ejemplo, no tendrían instrucciones como las siguientes:

1. **Operaciones de Aritmética de Memoria**: Instrucciones que realizan una operación aritmética y almacenan el resultado directamente en la memoria.
2. **Instrucciones de Lógica de Memoria**: Instrucciones que toman un valor de la memoria, realizan una operación lógica y almacenan el resultado de nuevo en la memoria.
3. **Instrucciones de Manipulación de Memoria**: Instrucciones que mueven datos entre registros y memoria mientras también realizan alguna forma de procesamiento en los datos.

Estas instrucciones estarían presentes en arquitecturas más complejas que permiten operaciones entre registros y memoria en una única instrucción, pero en una arquitectura Load-Store, estas tareas se descompondrían en múltiples instrucciones: una para cargar datos de la memoria a un registro, una para realizar la operación en registros y una tercera para almacenar el resultado de nuevo en la memoria.


---
## 4. ¿Cómo es el mapa de memoria de la familia?

### Mapa de Memoria de la Familia ARM Cortex-M

La familia de procesadores ARM Cortex-M posee un mapa de memoria uniforme y bien definido, lo que facilita la portabilidad del código y la consistencia en el diseño de sistemas embebidos. Esta es de 4G, que comienza en la direccion comienza en la dirección `0x00000000` y termina en la dirección `0xFFFFFFFF`, Aunque puede haber variaciones específicas según el microcontrolador en particular, el mapa de memoria generalmente se divide en varias regiones:

![Drag Racing](fig/mapaCortexM.png)

a) **Area de Código** Longitud de 512 MB, y sus direcciones van desde  `0x00000000` a `0xFFFFFFFF`. Esta area tiene 6 subbloques. 2 son reservados y los otrs cuatro son funcionales.

   i. **Primer subbloque** la primera subseccion es especial porque nos permite acceder a otros sub bloques, por ejempl al bloque de la Flash, al bolque de la memoria del sistema y al bloque de la RAM y eso depende de la configuracion que tenga el boot. El boot a nivel de HardWard esta compuesto por dos pines externos, al cual tendremos acceso y podemos darle diferente niveles de voltaje. Por ejemplo un valor logico alto o bajo. Dependiendo los valores logicos que le demos tendremos acceso a la Flash a la memoria del sistema o a la SRAM y ese acceso se va a dar en forma inmediata cualdo el microcontrolado se reinicia

   ii. **Memoria Flash**: Esta es donde generalmente se almacena el código del programa. Usualmente comienza en la dirección `0x08000000` o `0x00000000` dependiendo de la configuración de arranque del sistema. Termina de manera indeterminada ya que le da flexibilidad hasta donde llegara al fabricante. 
   
   iii. **Memoria de Sistema**: Espacio reservado para funciones específicas del sistema, como la tabla de vectores de interrupción, que generalmente se ubica cerca del inicio del mapa de memoria. Contiene el bootloader que permite escribir y leer en la Flash sin necesidad de un programador. Es decir, sin una piesa de hardware que actua como interfas que actua como interprete. Para programarlo  se pueden ocupar los puertos UART, CAN y USB.  Comienza en la dirección `0x01FFFX000`
   
   iiii. **Option bytes**: permiten configurar ciertas características del hardware que son leídas durante el arranque del microcontrolador o en tiempo de ejecución. Algunas de las configuraciones son Protección de Lectura y Escritura, Configuración de Arranque, Opciones de Hardware, Configuración de Periféricos, Niveles de Interrupción, Modo de Depuración, etc. Aqui hay opciones de poder bloquear la lectura de la flash para que evitar que copien nuestro programa.

	

![Mapa de Memoria](fig/mapMemori_primer.png)
  
B). **Memoria RAM**: Utilizada para datos y almacenamiento temporal durante la ejecución del programa, es decir se almacenan las variables. Comúnmente comienza en direcciones como `0x20000000`. Tiene una longitud de 0,5GB (máxima). 
  
C). **Registros de Periféricos**: Estos son mapeados en el espacio de direcciones para permitir la interacción con periféricos del microcontrolador como GPIO, UART, ADC, etc. Su posición en el mapa de memoria varía según el microcontrolador específico.
  
D). **Memoria Externa**: Algunos microcontroladores pueden soportar memoria externa, que también tendría su propio rango en el mapa de memoria. Se puede (1GB)

E). **Perifericos Externos**: Como memoria Flash  (1GB)
  
B). **Regiones No Asignadas**: Estas son áreas del mapa de memoria que no están asignadas ni reservadas, y acceder a ellas generalmente resultará en un comportamiento indefinido. Registros propios del microcontrolador. Como perifericos propios del microcontrolador.

Es fundamental comprender este mapa de memoria al diseñar software para microcontroladores basados en la arquitectura ARM Cortex-M, especialmente cuando se realizan operaciones a bajo nivel que requieren acceso directo a direcciones de memoria específicas.



---
## 5. ¿Qué ventajas presenta el uso de los “shadowed pointers” del PSP y el MSP?

### Ventajas del Uso de "Shadowed Pointers" para PSP y MSP en Microcontroladores ARM Cortex-M

Los punteros sombreados ("shadowed pointers") para el PSP (Puntero de Pila de Proceso) y el MSP (Puntero de Pila Principal) ofrecen varias ventajas que contribuyen a la eficiencia y la reactividad del sistema. A continuación se detallan algunas de estas ventajas:

#### Cambio Rápido de Contexto
- Una ventaja clave es la capacidad de cambiar rápidamente entre diferentes contextos. Esto permite que el procesador cambie automáticamente del PSP al MSP cuando ocurre una interrupción, mejorando la eficiencia en el manejo de interrupciones.

#### Separación de Privilegios
- El uso de diferentes punteros de pila para los modos Thread y Handler facilita una separación clara de privilegios entre el código de la aplicación y el código de manejo de interrupciones. Esto es especialmente útil en sistemas con requisitos estrictos de seguridad o fiabilidad.

#### Simplificación de la Gestión de Tareas
- En sistemas que utilizan múltiples tareas o hilos, el PSP puede manejar el contexto de cada tarea de forma individual, mientras que el MSP se usa para funciones del sistema operativo y el manejo de interrupciones. Esto simplifica la lógica necesaria para el cambio de contexto en sistemas operativos en tiempo real (RTOS).

#### Optimización de Desempeño
- El hardware en estos microcontroladores puede estar optimizado para hacer cambios rápidos entre los punteros de pila, resultando en mejor rendimiento comparado con una implementación que maneje múltiples pilas puramente en software.

#### Mayor Flexibilidad
- Tener diferentes punteros de pila ofrece más flexibilidad para asignar y gestionar la memoria. Por ejemplo, se podría asignar una pila muy pequeña para ciertas interrupciones de alta prioridad para asegurar una respuesta rápida.

En resumen, el uso de "shadowed pointers" para el PSP y MSP en la arquitectura ARM Cortex-M permite una gestión más eficaz y segura de múltiples tareas e interrupciones, mejorando la eficiencia general del sistema.


---
## 6. Describa los diferentes modos de privilegio y operación del Cortex M, sus relaciones y como se conmuta de uno al otro. Describa un ejemplo en el que se pasa del modo privilegiado a no priviligiado y nuevamente a privilegiado.


Los microcontroladores ARM Cortex-M ofrecen diferentes modos de operación y niveles de privilegio que permiten un control granular sobre la ejecución del programa y la gestión de recursos. Estos modos y niveles son especialmente útiles para aplicaciones embebidas y sistemas operativos en tiempo real (RTOS).

### Modos de Operación
1. **Thread Mode**: Este es el modo inicial después del arranque y generalmente es donde se ejecuta el código de aplicación.
2. **Handler Mode**: Este modo se activa automáticamente cuando se produce una excepción o interrupción. Se utiliza para manejar interrupciones y excepciones.

### Niveles de Privilegio
1. **Privilegiado**: Permite acceso completo a todas las instrucciones y recursos del sistema.
2. **No Privilegiado**: Restringe el acceso a ciertos recursos e instrucciones, como las instrucciones que manipulan el modo de operación y nivel de privilegio.

### Relaciones entre los Modos y Niveles de Privilegio
- **Thread Mode**: Puede operar tanto en nivel privilegiado como en no privilegiado. 
- **Handler Mode**: Siempre opera en nivel privilegiado.

### Conmutación entre Modos y Niveles de Privilegio
1. **De Thread a Handler Mode**: La transición ocurre automáticamente cuando se produce una excepción o interrupción. El procesador guarda el contexto actual y cambia al Handler Mode.
2. **De Handler a Thread Mode**: Al finalizar la ejecución del controlador de interrupción, se restaura el contexto y se regresa al Thread Mode.
3. **De Privilegiado a No Privilegiado**: Esto generalmente se realiza mediante instrucciones específicas que modifican el estado del procesador.
4. **De No Privilegiado a Privilegiado**: Esto usualmente se hace a través de una excepción controlada, como una llamada al sistema operativo, que conmuta al Handler Mode (que es siempre privilegiado).


### Ejemplo de Transición entre Modos Privilegiado y No Privilegiado en ARM Cortex-M

Imaginemos un sistema embebido con un sistema operativo en tiempo real (RTOS) que maneja dos tareas: una tarea de sensor y una tarea de usuario. La tarea de sensor es crítica para el sistema, mientras que la tarea de usuario es menos crítica. En este escenario, es probable que se desee que la tarea de sensor opere en un modo privilegiado para acceder directamente a recursos del sistema, mientras que la tarea de usuario debería operar en un modo no privilegiado para limitar su acceso a recursos críticos del sistema.

### Paso a No Privilegiado desde Privilegiado
1. **Inicio en Modo Privilegiado**: Suponga que el sistema arranca y el RTOS se inicializa en el Thread Mode con nivel de privilegio.
2. **Llamada a la Tarea de Usuario**: El RTOS decide que es momento de ejecutar la tarea de usuario.
3. **Cambio a No Privilegiado**: Antes de pasar el control a la tarea de usuario, el RTOS utiliza instrucciones específicas para cambiar al modo no privilegiado.
4. **Ejecución de la Tarea de Usuario**: Ahora, la tarea de usuario se ejecuta con un nivel no privilegiado, limitando su capacidad para acceder o modificar recursos críticos del sistema.

### Regreso a Modo Privilegiado
1. **Interrupción o Excepción**: Suponga que el sensor produce una interrupción que necesita ser manejada de inmediato.
2. **Handler Mode**: El procesador cambia automáticamente al Handler Mode (que siempre es privilegiado) para manejar esta interrupción.
3. **Ejecución de la Tarea de Sensor**: La tarea de sensor se ejecuta para manejar los datos del sensor.
4. **Regreso a Thread Mode**: Una vez que se ha manejado la interrupción, el sistema vuelve al Thread Mode y regresa al RTOS, que podría optar por seguir ejecutando la tarea de usuario o conmutar a otra tarea.

### Notas Adicionales
- En la transición de Handler Mode a Thread Mode, el RTOS podría decidir restaurar el estado de privilegio según la tarea a la que pasará el control.

Este ejemplo ilustra cómo un sistema operativo en tiempo real podría gestionar tareas con diferentes niveles de privilegio y cómo se puede conmutar entre los modos privilegiado y no privilegiado para mantener tanto la seguridad como la eficiencia del sistema.


En resumen, los microcontroladores ARM Cortex-M ofrecen modos de operación y niveles de privilegio flexibles que permiten una gestión eficaz de las tareas y los recursos del sistema, así como una transición eficiente y segura entre diferentes contextos y niveles de acceso.


---
## 7. ¿Qué se entiende por modelo de registros ortogonal? Dé un ejemplo

### Modelo de Registros Ortogonal

El concepto de "modelo de registros ortogonal" se refiere a un diseño de arquitectura de conjunto de instrucciones (ISA) en el que cada instrucción puede utilizar cualquier registro del conjunto de registros disponibles de manera indistinta. En otras palabras, las instrucciones no están limitadas a usar un subconjunto específico de registros, y cualquier instrucción que opere en registros puede utilizar cualquiera de los registros disponibles.

#### Ventajas

- **Simplicidad**: Hace que el conjunto de instrucciones sea más fácil de entender y usar.
- **Flexibilidad**: Permite más libertad al compilador o al programador para optimizar el uso de registros.
- **Eficiencia**: Puede reducir la cantidad de instrucciones necesarias para mover datos entre registros específicos, mejorando así la eficiencia del código.

#### Ejemplo en un Modelo de Registros No Ortogonal

La arquitectura de los microcontroladores ARM Cortex-M de STMicroelectronics generalmente sigue un modelo más ortogonal en comparación con algunas otras arquitecturas, pero no es completamente ortogonal en el sentido más estricto del término.

En ARM Cortex-M, la mayoría de las instrucciones de operaciones aritméticas y lógicas pueden operar con varios registros del conjunto de registros del núcleo. Sin embargo, hay algunas restricciones en instrucciones específicas o en ciertas formas de direccionamiento. Por ejemplo, ciertas instrucciones pueden requerir que uno de los operandos esté en un registro de bajo orden (R0-R7).

#### Ejemplo en ARM Cortex-M

Un ejemplo de instrucción en ARM Cortex-M podría ser:

```assembly
// Suma R1 y R2, y almacena el resultado en R0
ADD R0, R1, R2  

```
En este caso, podemos utilizar cualquier registro general (R0 a R12) para almacenar y manipular datos, lo cual es bastante flexible y se acerca al concepto de un modelo de registros ortogonal.




---
## 8. ¿Qué ventajas presenta el uso de intrucciones de ejecución condicional (IT)? Dé un ejemplo

### Ventajas del Uso de Instrucciones de Ejecución Condicional (IT) en ARM Cortex-M

Las instrucciones de ejecución condicional (`IT` y sus variantes) en ARM Cortex-M ofrecen una forma eficiente de ejecutar instrucciones basadas en ciertas condiciones sin tener que usar las instrucciones de salto condicional. Esto puede tener varias ventajas:

#### Ventajas

1. **Optimización del Flujo de Control**: Reduce la necesidad de instrucciones de salto, lo que puede hacer que el código sea más eficiente en términos de rendimiento y uso de memoria.
   
2. **Mejora del Rendimiento del Pipeline**: Al eliminar algunos saltos condicionales, se pueden reducir los peligros de control en el pipeline, mejorando así el rendimiento del CPU.
  
3. **Código más Compacto**: Pueden resultar en un código más pequeño, lo que es beneficioso para sistemas con memoria limitada.

4. **Mayor Claridad**: En ciertos casos, el uso de instrucciones condicionales puede hacer que el código sea más fácil de entender y mantener.

#### Ejemplo

A continuación se muestra un ejemplo simple que utiliza la instrucción `IT` para ejecutar instrucciones condicionalmente. Este ejemplo compara dos registros (`R0` y `R1`) y, dependiendo de si son iguales, incrementa el valor en `R2`.

```assembly
    CMP  R0, R1        ; Compara R0 y R1
    ITE  EQ            ; If-Then-Else Equal
    ADDEQ R2, R2, #1   ; Si son iguales (condición EQ), suma 1 a R2
    ADDNE R2, R2, #0   ; Si son diferentes (condición NE), no cambia R2
```

En este ejemplo, si R0 y R1 son iguales (EQ), entonces la instrucción ADDEQ se ejecutará, sumando 1 a R2. De lo contrario, la instrucción ADDNE se ejecutará, pero no cambiará el valor de R2.

Este tipo de instrucciones condicionales permite una optimización tanto en tamaño de código como en velocidad de ejecución.
  
 
---
## 9. Describa brevemente las excepciones más prioritarias (reset, NMI, Hardfault).

### Excepciones Más Prioritarias en ARM Cortex-M

Los microcontroladores basados en la arquitectura ARM Cortex-M manejan diferentes tipos de excepciones, y algunas de estas tienen alta prioridad para asegurar la funcionalidad y la seguridad del sistema. Las más prioritarias son: Reset, NMI (Non-Maskable Interrupt) y HardFault.

#### Reset

- **Prioridad**: Más alta (nivel de prioridad fijado por el hardware)
- **Descripción**: Esta excepción se genera cuando el sistema se reinicia, ya sea en el arranque inicial o debido a un reinicio inducido por software o hardware.
- **Uso**: Inicializar todos los registros y el estado del sistema a valores conocidos.

#### NMI (Non-Maskable Interrupt)

- **Prioridad**: Segunda más alta (también fijada por el hardware)
- **Descripción**: NMI es una interrupción que no se puede enmascarar o deshabilitar, asegurando que siempre se atienda.
- **Uso**: Generalmente se usa para manejar eventos críticos del sistema que requieren una atención inmediata, como errores de hardware.

#### HardFault

- **Prioridad**: Tercera más alta (por debajo de Reset y NMI)
- **Descripción**: Este tipo de excepción se genera en casos de errores graves como acceso a una dirección de memoria inválida.
- **Uso**: Usualmente se utiliza para capturar errores en tiempo de ejecución que no pueden recuperarse, como fallos en el bus o errores de precisión de punto flotante en modelos que soportan FPU.

Estas excepciones de alta prioridad garantizan que el sistema pueda responder a eventos críticos de manera adecuada, incluso si otras interrupciones están siendo procesadas o enmascaradas.


---
## 10. Describa las funciones principales de la pila. ¿Cómo resuelve la arquitectura el llamado a funciones y su retorno?

### Funciones Principales de la Pila en la Arquitectura de Computadoras

La pila (stack) es una estructura de datos que sigue el principio LIFO (Last In, First Out) y desempeña varias funciones críticas en la arquitectura de computadoras, especialmente en el llamado y retorno de funciones.

#### Funciones Principales

1. **Almacenamiento Temporal**: Guarda variables locales y datos temporales.
  
2. **Control del Flujo de Ejecución**: Guarda las direcciones de retorno cuando se llama a funciones, permitiendo regresar al punto correcto del programa después de que se ha completado la ejecución de la función.

3. **Passing Arguments**: Permite pasar argumentos a funciones, especialmente cuando el número de argumentos es variable o desconocido.

4. **Manejo de Excepciones e Interrupciones**: Guarda el estado del programa antes de pasar a un controlador de excepción o interrupción.

#### Resolución del Llamado a Funciones y su Retorno en ARM Cortex-M

1. **Llamado a Funciones (`BL` o `BLX` en ensamblador)**
   - Antes de saltar a la dirección de la función, la dirección de retorno (la dirección de la instrucción después del `BL`) se guarda en el registro de enlace (link register, `LR`).
   - Los argumentos para la función son generalmente pasados a través de registros (`R0-R3`) o se colocan en la pila si hay más argumentos.
   - Se cambia el puntero de la pila (`SP`) para hacer espacio para variables locales y guardar registros si es necesario.

2. **Ejecución de la Función**
   - Las variables locales y los registros que deben ser preservados se almacenan en la pila.
   - La función realiza su tarea.

3. **Retorno de la Función (`BX LR` en ensamblador)**
   - Si se han almacenado variables locales o registros en la pila, estos son recuperados.
   - La dirección de retorno se toma del registro de enlace (`LR`) y se coloca en el contador de programa (`PC`), haciendo que la ejecución regrese al punto donde se hizo el llamado original a la función.

4. **Recuperación del Estado**
   - Si se almacenaron argumentos o registros en la pila, estos son eliminados o restaurados según corresponda.
  
Este flujo asegura que tanto el llamado a funciones como el retorno de estas se realicen de manera ordenada y predecible.

---
## 11. Describa la secuencia de reset del microprocesador.


### Secuencia de Reset en Microprocesadores ARM Cortex-M

El proceso de reset es fundamental para inicializar un microprocesador y prepararlo para la ejecución de programas. En los microprocesadores ARM Cortex-M, la secuencia de reset sigue un conjunto específico de pasos para asegurarse de que el hardware y el software estén en un estado conocido.

#### Secuencia de Pasos

1. **Activación del Reset**: Se activa la señal de reset, ya sea mediante un evento externo, un fallo de alimentación o una solicitud de reset por software.

2. **Inicialización de Hardware**: Todas las unidades funcionales, registros y periféricos se inicializan a sus valores por defecto. Esto incluye poner todos los pines GPIO en su estado de reset, inicializar los registros de control y estado, y más.

3. **Configuración del Vector Table Offset Register (VTOR)**: En muchos casos, la dirección de inicio de la tabla de vectores se carga en el registro VTOR. Por defecto, esta tabla se encuentra en el inicio de la memoria flash, pero puede ser reubicada.

4. **Carga del Stack Pointer**: El valor inicial del puntero de pila (Stack Pointer, `SP`) se carga desde la primera entrada de la tabla de vectores. Este valor apunta a la parte superior de la pila principal (Main Stack).

5. **Carga del Program Counter**: La segunda entrada de la tabla de vectores contiene la dirección de inicio del programa (Reset Handler). Este valor se coloca en el Program Counter (`PC`).

6. **Ingreso al Modo Privilegiado**: El procesador entra en el modo privilegiado (Thread Mode con privilegios), deshabilitando algunas de las funciones de seguridad hasta que el software del sistema las habilite explícitamente.

7. **Inicio del Programa**: El procesador comienza la ejecución del programa a partir de la dirección almacenada en el `PC`. Generalmente, esto llevará al código que realiza más inicializaciones específicas del sistema y finalmente entra en el bucle principal del programa o en el sistema operativo.

#### Notas Adicionales

- Durante el proceso de reset, las interrupciones están generalmente deshabilitadas para evitar que cualquier actividad externa interfiera con la secuencia de inicialización.

Estos pasos aseguran que el microprocesador se inicialice en un estado limpio y predecible, listo para la ejecución de programas.

---
## 12. ¿Qué entiende por “core peripherals”? ¿Qué diferencia existe entre estos y el resto de los periféricos?

### ¿Qué son los "Core Peripherals" en la Arquitectura de Microprocesadores ARM Cortex-M?

Los "Core Peripherals" o periféricos del núcleo son componentes hardware estrechamente acoplados al núcleo del procesador (CPU core) y son esenciales para su funcionamiento básico y el control del microprocesador. Estos periféricos están diseñados para ser accedidos de manera rápida y eficiente por el núcleo del procesador.

#### Core Peripherals Típicos en ARM Cortex-M

1. **System Control Block (SCB)**: Controla diversas configuraciones del sistema como la configuración del vector de interrupciones, la velocidad del reloj y las excepciones del sistema.
  
2. **Nested Vectored Interrupt Controller (NVIC)**: Administra las interrupciones y excepciones, incluido el enmascaramiento, la prioridad y el enrutamiento de interrupciones.
  
3. **Debug Access Port (DAP)**: Proporciona funcionalidades para la depuración en tiempo real.

4. **SysTick Timer**: Un contador de tiempo simple pero efectivo que puede ser útil para generar interrupciones periódicas.

#### Diferencia entre Core Peripherals y Otros Periféricos

1. **Acceso Directo vs Indirecto**: Los core peripherals están directamente conectados al núcleo del procesador para permitir un acceso rápido y eficiente, mientras que otros periféricos podrían estar conectados a través de buses como el AHB, APB, etc.

2. **Funciones Críticas vs Funciones Extendidas**: Los core peripherals están diseñados para funciones críticas y básicas del sistema como el manejo de interrupciones, el control del sistema y la depuración. Otros periféricos, como GPIO, UART, SPI, etc., proporcionan funciones extendidas y no son críticos para el funcionamiento básico del procesador.

3. **Universalidad vs Especificidad**: Los core peripherals suelen ser comunes en toda una familia de procesadores, mientras que otros periféricos pueden variar significativamente entre diferentes chips o familias de procesadores.

4. **Configuración Inicial**: Los core peripherals son generalmente configurados durante la inicialización del sistema y raramente se cambian durante la operación del sistema. Otros periféricos pueden ser configurados y reconfigurados múltiples veces durante la ejecución del programa.

En resumen, los core peripherals son fundamentales para el funcionamiento básico del microprocesador y están diseñados para una interacción estrecha con el núcleo del procesador.

---
## 13. ¿Cómo se implementan las prioridades de las interrupciones? Dé un ejemplo

### Implementación de Prioridades de Interrupciones en ARM Cortex-M

La implementación de prioridades de interrupciones en la arquitectura ARM Cortex-M es una tarea manejada principalmente por el ***Nested Vectored Interrupt Controller (NVIC)***. El NVIC permite asignar diferentes niveles de prioridad a cada interrupción, permitiendo que algunas interrupciones tengan precedencia sobre otras.

#### Cómo Funciona

1. **Registros de Prioridad**: Cada interrupción tiene un registro de prioridad asociado en el NVIC. Estos registros permiten asignar un valor numérico que indica la prioridad de la interrupción.

2. **Mecanismo de Anidamiento**: El NVIC permite la anidación de interrupciones. Una interrupción de alta prioridad puede interrumpir la ejecución de una de menor prioridad pero no viceversa.

3. **Configuración de Grupos y Subprioridades**: Algunas implementaciones permiten la división de las prioridades en grupos y subprioridades, ofreciendo aún más flexibilidad.

#### Ejemplo en Código C

Supongamos que tenemos dos interrupciones: una para un botón (con una prioridad más baja) y otra para un sensor de temperatura crítico (con una prioridad más alta).

```c
// Configuración de prioridades usando CMSIS para ARM Cortex-M
NVIC_SetPriority(Button_IRQn, 5);  // Prioridad más baja
NVIC_SetPriority(TempSensor_IRQn, 1);  // Prioridad más alta

// Habilitar las interrupciones
NVIC_EnableIRQ(Button_IRQn);
NVIC_EnableIRQ(TempSensor_IRQn);
```

En este ejemplo, la interrupción del sensor de temperatura tiene una prioridad más alta (1) que la del botón (5). Si ambas interrupciones se disparan al mismo tiempo, el NVIC asegurará que primero se atienda la interrupción del sensor de temperatura.


---
## 14. ¿Qué es el CMSIS? ¿Qué función cumple? ¿Quién lo provee? ¿Qué ventajas aporta?

### ¿Qué es el CMSIS?

CMSIS significa Cortex Microcontroller Software Interface Standard. Es un conjunto estandarizado de interfaces de software, bibliotecas y definiciones de macros diseñadas para simplificar y acelerar el desarrollo de aplicaciones en microcontroladores basados en la arquitectura ARM Cortex-M.

#### ¿Qué función cumple?

1. **Abstracción de Hardware**: Provee una capa de abstracción de hardware que facilita la portabilidad de código entre diferentes microcontroladores Cortex-M.

2. **Bibliotecas de Soporte**: Incluye una amplia variedad de bibliotecas de soporte para tareas comunes como el manejo de periféricos, matemáticas y operaciones en tiempo real.

3. **Depuración y Diagnóstico**: Ofrece funcionalidades para depuración, trazabilidad y diagnóstico del sistema.

4. **Manejo de Interrupciones**: Simplifica la configuración y el manejo de interrupciones a través del NVIC.

#### ¿Quién lo provee?

CMSIS es provisto y mantenido por ARM Ltd. (ahora parte de NVIDIA).

#### ¿Qué ventajas aporta?

1. **Portabilidad**: Facilita la portabilidad de código entre diferentes plataformas basadas en Cortex-M.

2. **Rapidez de Desarrollo**: Las bibliotecas y abstracciones predefinidas aceleran el proceso de desarrollo.

3. **Uniformidad**: Al usar un estándar común, los desarrolladores pueden compartir y colaborar más fácilmente en proyectos.

4. **Optimización**: Las bibliotecas incluidas están optimizadas para un rendimiento eficiente en microcontroladores Cortex-M.

5. **Soporte y Mantenimiento**: Al ser un estándar mantenido por ARM, se beneficia de actualizaciones y soporte regulares.

En resumen, CMSIS busca simplificar y estandarizar el desarrollo de software para microcontroladores basados en la arquitectura ARM Cortex-M, facilitando así el desarrollo de aplicaciones robustas y eficientes.



---
## 15. Cuando ocurre una interrupción, asumiendo que está habilitada ¿Cómo opera el microprocesador para atender a la subrutina correspondiente? Explique con un ejemplo

### Procedimiento de Manejo de Interrupciones en Microprocesadores ARM Cortex-M

Cuando ocurre una interrupción y está habilitada, el microprocesador ARM Cortex-M sigue una serie de pasos para atender a la subrutina correspondiente. Este procedimiento se conoce como "context switching" o cambio de contexto.

#### Secuencia de Operación

1. **Detener la Ejecución Actual**: El microprocesador detiene la ejecución del código actual.

2. **Guardar el Contexto Actual**: Guarda el contexto actual del CPU, que incluye varios registros y el Program Counter, en la pila (stack).

3. **Consultar Vector de Interrupciones**: Se consulta la tabla de vectores de interrupciones para encontrar la dirección de la subrutina de manejo de interrupción (Interrupt Service Routine, ISR) correspondiente.

4. **Saltar a la ISR**: El Program Counter se actualiza para saltar a la dirección de inicio de la ISR.

5. **Ejecutar ISR**: Se ejecuta el código dentro de la ISR.

6. **Restaurar Contexto y Retornar**: Una vez finalizada la ISR, se restaura el contexto original desde la pila y se retoma la ejecución del código donde fue interrumpido.

#### Ejemplo en Código C

Supongamos que tenemos una interrupción de un botón que cambia el estado de un LED.

```c
// ISR para la interrupción del botón
void Button_IRQHandler(void) {
    // Código para cambiar el estado del LED
    toggleLED();
    
    // Limpiar la señal de interrupción
    clearButtonInterruptFlag();
}

// Configuración inicial
void setup() {
    // Configurar y habilitar la interrupción del botón
    configureButtonInterrupt();
    NVIC_EnableIRQ(Button_IRQn);
}

// Bucle principal
void loop() {
    // Código de la aplicación principal
}
```

En este ejemplo, cuando se presiona el botón, se genera una interrupción que es atendida por la función Button_IRQHandler. Dentro de esta ISR, se cambia el estado del LED y se limpia la señal de interrupción para prepararse para futuras interrupciones.


---
## 16. ¿Cómo cambia la operación de stacking al utilizar la unidad de punto flotante?

### Cambio en la Operación de Stacking con Unidad de Punto Flotante en ARM Cortex-M

En los microprocesadores ARM Cortex-M que incorporan una Unidad de Punto Flotante (FPU), el mecanismo de "stacking" o apilado durante una interrupción varía ligeramente en comparación con aquellos que no tienen FPU. 

#### Operación de Stacking sin FPU

En un microcontrolador sin FPU, el stacking implica guardar registros de propósito general (como R0 a R3), el Program Counter (PC), el Program Status Register (xPSR), etc., en la pila (stack) antes de saltar a la rutina de servicio de interrupción (ISR).

#### Operación de Stacking con FPU

Cuando se utiliza un microcontrolador con FPU, el hardware adicionalmente guarda y restaura los registros de punto flotante en la pila durante un cambio de contexto. Esto es especialmente relevante si la ISR utiliza operaciones de punto flotante.

1. **Registros de Punto Flotante**: Registros como S0-S15 y otros registros relacionados con la FPU son guardados en la pila, además de los registros de propósito general y de estado.

2. **Tamaño de la Pila**: Debido a la adición de registros de punto flotante, el tamaño del área de stacking se incrementa.

3. **Tiempo de Ejecución**: El tiempo requerido para entrar y salir de la ISR podría ser ligeramente mayor debido al tiempo extra requerido para guardar y restaurar más registros.

4. **CONTROL.FPCA**: Este bit en el registro CONTROL determina si los registros de punto flotante serán apilados o no. Si está habilitado, se realizará el stacking completo incluyendo los registros de la FPU.

#### Ejemplo

```c
// ISR que utiliza operaciones de punto flotante
void My_IRQHandler(void) {
    float a = 10.5;
    float b = 20.5;
    float result = a + b;  // Operación de punto flotante
    // Código adicional
}
```
En este ejemplo, debido a la operación de punto flotante dentro de la ISR, si el bit CONTROL.FPCA está habilitado, los registros de punto flotante involucrados en la operación serán guardados y restaurados durante el stacking y unstacking respectivamente.



---
## 17. Explique las características avanzadas de atención a interrupciones: tail chaining y late arrival.

### Características Avanzadas de Atención a Interrupciones: Tail Chaining y Late Arrival

Los microcontroladores ARM Cortex-M ofrecen algunas características avanzadas para el manejo eficiente de interrupciones, que incluyen "Tail Chaining" y "Late Arrival". Estas optimizaciones están diseñadas para reducir el tiempo y el costo en ciclos de CPU asociados con el servicio de interrupciones.

### Tail Chaining

La técnica de "Tail Chaining" permite a múltiples interrupciones ser manejadas más eficientemente al evitar el "unstacking" y "stacking" redundantes entre interrupciones consecutivas.

#### Cómo Funciona:

1. **Primera Interrupción**: El microcontrolador entra en la ISR (Rutina de Servicio de Interrupción) y apila el contexto actual.
2. **Segunda Interrupción**: Si una segunda interrupción llega antes de que la primera ISR termine, el microcontrolador evita el proceso de "unstacking" del contexto de la primera ISR.
3. **Transición Directa**: En lugar de restaurar el contexto y luego volver a apilarlo para la segunda ISR, el microcontrolador transita directamente de la primera a la segunda ISR.

#### Ventajas:

- Menor tiempo en el servicio de interrupciones consecutivas.
- Ahorro de ciclos de CPU.

### Late Arrival

"Late Arrival" es otra técnica avanzada que permite a una interrupción con una prioridad más alta "interrumpir" una interrupción de menor prioridad durante el proceso de "stacking".

#### Cómo Funciona:

1. **Interrupción de Menor Prioridad**: Se activa una interrupción y el microcontrolador comienza a apilar el contexto.
2. **Interrupción de Mayor Prioridad**: Si llega una interrupción de mayor prioridad durante el apilado del contexto de la interrupción de menor prioridad, el proceso de apilado se completa rápidamente.
3. **Atender la Mayor Prioridad**: El microcontrolador inmediatamente comienza a atender la interrupción de mayor prioridad.

#### Ventajas:

- Capacidad para responder rápidamente a interrupciones de alta prioridad.
- Mejora el rendimiento del sistema al asegurar que las interrupciones críticas se manejen lo más rápido posible.

En resumen, tanto "Tail Chaining" como "Late Arrival" son características avanzadas que optimizan el manejo de interrupciones, reduciendo el tiempo y los ciclos de CPU necesarios para el servicio de múltiples interrupciones.





---
## 18. ¿Qué es el systick? ¿Por qué puede afirmarse que su implementación favorece la portabilidad de los sistemas operativos embebidos?

### SysTick: Reloj del Sistema y Portabilidad en Sistemas Operativos Embebidos

#### ¿Qué es el SysTick?

SysTick (System Tick Timer) es un temporizador de cuenta regresiva presente en los microcontroladores ARM Cortex-M. Es un periférico del núcleo (core peripheral) que proporciona una fuente de interrupción con una frecuencia regular y bien conocida. SysTick se utiliza comúnmente para implementar funciones de tiempo de retraso (delay), medir el tiempo transcurrido, y más importante aún, para el "scheduling" o planificación de tareas en sistemas operativos en tiempo real (RTOS).

#### Características Principales

- **Facilidad de Uso**: Configurar SysTick es sencillo, lo que facilita su uso en aplicaciones diversas.
- **Base de Tiempo**: Proporciona una fuente de tiempo consistente y predecible.
- **Interrupciones**: Puede generar interrupciones en intervalos de tiempo regulares, lo cual es útil para la planificación de tareas.

#### Ventajas para la Portabilidad de Sistemas Operativos Embebidos

1. **Estándar en Cortex-M**: Dado que SysTick es un componente estándar en la arquitectura Cortex-M, los sistemas operativos que lo utilizan son más fáciles de portar entre diferentes microcontroladores basados en esta arquitectura.

2. **Abstracción de Hardware**: SysTick ofrece una capa de abstracción para el temporizador, lo que significa que el código del sistema operativo no necesita conocer los detalles específicos del hardware para implementar la funcionalidad de temporización.

3. **Facilita el Multitasking**: Al proporcionar una fuente de interrupción regular, SysTick facilita la implementación de algoritmos de planificación, haciendo más sencillo el soporte de multitarea.

4. **Independencia de Proveedor**: Al utilizar el periférico estándar SysTick, los sistemas operativos embebidos no están atados a una implementación específica de un proveedor, lo que mejora la portabilidad.

5. **Configuración Simplificada**: Al estar bien documentado y ser consistente en toda la familia Cortex-M, SysTick simplifica la configuración de temporizadores, reduciendo la curva de aprendizaje cuando se pasa a un nuevo microcontrolador.


En resumen, SysTick es un periférico de núcleo en la arquitectura ARM Cortex-M que no solo facilita la programación de temporizadores, sino que también aumenta significativamente la portabilidad de los sistemas operativos embebidos entre diferentes microcontroladores basados en Cortex-M.




---
## 19. ¿Qué funciones cumple la unidad de protección de memoria (MPU)?

### Funciones de la Unidad de Protección de Memoria (MPU)

La Unidad de Protección de Memoria (MPU, por sus siglas en inglés Memory Protection Unit) es un componente opcional en algunos microcontroladores ARM Cortex-M. Su objetivo principal es mejorar la seguridad y la robustez del sistema al proporcionar un mecanismo de control de acceso a regiones de memoria.

### Funciones Principales

1. **Control de Acceso**: La MPU permite configurar políticas de acceso para diferentes regiones de memoria. Esto puede incluir quién puede leer, escribir o ejecutar código en ciertas áreas de memoria.

2. **Aislamiento de Tareas**: En un entorno multitarea, la MPU puede ser usada para aislar las áreas de memoria utilizadas por diferentes tareas, asegurando que una tarea no pueda acceder o modificar la memoria utilizada por otra.

3. **Protección contra Fallos**: Al restringir el acceso a ciertas regiones de memoria, la MPU ayuda a evitar que errores de software, como desbordamientos de búfer, afecten a áreas críticas del sistema.

4. **Seguridad**: Puede añadir una capa adicional de seguridad al evitar el acceso no autorizado a áreas de memoria que contienen datos o código sensible.

5. **Modos de Operación**: Facilita la implementación de diferentes modos de operación (por ejemplo, modos privilegiados y no privilegiados) en el sistema, permitiendo diferentes niveles de acceso a la memoria en función del modo actual.

### Ejemplos de Uso

- **RTOS**: En un Sistema Operativo en Tiempo Real, la MPU puede ser utilizada para asegurar que las tareas individuales no puedan interferir entre sí, mejorando así la estabilidad y fiabilidad del sistema.

- **Aplicaciones Críticas**: En sistemas que manejan información sensible o que controlan maquinaria, la MPU puede evitar accesos no deseados o errores que podrían ser catastróficos.

En resumen, la Unidad de Protección de Memoria en microcontroladores ARM Cortex-M proporciona un conjunto de funcionalidades esenciales para aumentar la seguridad, la robustez y la integridad del sistema, siendo especialmente útil en aplicaciones complejas y sistemas en tiempo real.



---
## 20. ¿Cuántas regiones pueden configurarse como máximo? ¿Qué ocurre en caso de haber solapamientos de las regiones? ¿Qué ocurre con las zonas de memoria no cubiertas por las regiones definidas?

### Configuración de Regiones en la MPU y Manejo de Solapamientos

#### Cantidad Máxima de Regiones

El número de regiones que pueden ser configuradas en la Unidad de Protección de Memoria (MPU) varía según la implementación específica del microcontrolador ARM Cortex-M. Algunos pueden soportar tan pocas como 8 regiones, mientras que otros pueden soportar más. Es importante consultar la documentación específica del microcontrolador para obtener detalles precisos.

#### Solapamientos de Regiones

Si hay regiones que se solapan, la MPU normalmente aplica la política de la región con el número más alto. En otras palabras, si las regiones 2 y 3 se solapan, las políticas configuradas para la región 3 tendrían prioridad sobre las de la región 2.

#### Zonas de Memoria No Cubiertas

Las áreas de memoria que no están cubiertas por ninguna región configurada en la MPU generalmente tendrán el acceso definido por los ajustes por defecto del sistema o del modo de operación actual (por ejemplo, privilegiado o no privilegiado). Estas áreas serán accesibles según los permisos predeterminados, lo cual podría representar un riesgo si no se maneja cuidadosamente.

#### Resumen

- **Máximo de Regiones**: Depende de la implementación específica del microcontrolador.
- **Solapamientos**: La región con el número más alto tiene prioridad.
- **Áreas No Cubiertas**: Acceso según los ajustes por defecto del sistema o modo de operación.

Al comprender estos aspectos, se puede configurar la MPU de manera efectiva para proteger las áreas críticas de la memoria y permitir un acceso adecuado para diferentes tareas o modos de operación.




---
## 21. ¿Para qué se suele utilizar la excepción PendSV? ¿Cómo se relaciona su uso con el resto de las excepciones? Dé un ejemplo

### Uso de la Excepción PendSV y su Relación con Otras Excepciones

#### ¿Para qué se suele utilizar la Excepción PendSV?

La excepción PendSV (Pendable Service Call) se utiliza comúnmente en microcontroladores ARM Cortex-M para realizar cambios de contexto en Sistemas Operativos en Tiempo Real (RTOS). Esta excepción es especialmente útil para manipular el cambio de una tarea a otra de manera eficiente.

#### Relación con Otras Excepciones

La excepción PendSV suele tener la menor prioridad entre todas las excepciones e interrupciones, lo que la hace útil para realizar cambios de contexto sólo cuando no hay otras excepciones o interrupciones más críticas que requieran ser atendidas. Esta baja prioridad asegura que las tareas más urgentes se ejecuten primero y que el cambio de contexto se realice sólo en momentos apropiados.

#### Ejemplo

Supongamos que estamos usando un RTOS y tenemos dos tareas: `Tarea_A` y `Tarea_B`. `Tarea_A` es una tarea de alta prioridad que maneja la entrada/salida de un sensor, y `Tarea_B` es una tarea de baja prioridad que actualiza la interfaz de usuario.

1. `Tarea_A` se activa debido a una nueva lectura del sensor y preemte a `Tarea_B`.
2. Al finalizar su ejecución, `Tarea_A` libera su recurso y el RTOS decide que es momento de volver a `Tarea_B`.
3. En lugar de realizar el cambio de contexto inmediatamente, el RTOS pone la excepción PendSV pendiente.
4. Como PendSV tiene la menor prioridad, se ejecutará solo después de que todas las otras excepciones e interrupciones hayan sido atendidas.
5. Cuando finalmente se ejecuta PendSV, se realiza el cambio de contexto y `Tarea_B` retoma su ejecución.


De esta manera, el uso de PendSV permite una gestión eficiente del cambio de contexto, asegurando que las tareas y excepciones de mayor prioridad sean atendidas primero.




---
## 22. ¿Para qué se suele utilizar la excepción SVC? Explíquelo dentro de un marco de un sistema operativo embebido.


### Uso de la Excepción SVC en un Sistema Operativo Embebido

#### ¿Qué es la Excepción SVC?

La excepción SVC (SuperVisor Call) es una excepción de software en la familia de microcontroladores ARM Cortex-M. Se activa mediante la instrucción `SVC`, y se usa principalmente para cambiar el nivel de privilegio del código, desde un modo no privilegiado a un modo privilegiado.

#### Uso en un Sistema Operativo Embebido

En un Sistema Operativo en Tiempo Real (RTOS) embebido, la excepción SVC se utiliza comúnmente para implementar llamadas al sistema (system calls). Estas son funciones del núcleo del sistema operativo que proporcionan servicios seguros y controlados a las tareas o procesos en ejecución.

##### Ejemplo de Uso

1. **Modo No Privilegiado**: Una tarea en modo no privilegiado necesita acceder a un recurso de hardware.
  
2. **Llamada al Sistema**: La tarea no puede acceder directamente al recurso por razones de seguridad y, en su lugar, hace una llamada al sistema.

3. **Instrucción SVC**: La llamada al sistema usa la instrucción `SVC` para invocar la excepción SVC.

4. **Cambio a Modo Privilegiado**: Cuando se activa la excepción SVC, el sistema cambia a modo privilegiado.

5. **Ejecución Segura**: Ahora, en modo privilegiado, el núcleo del RTOS puede acceder al recurso de hardware de forma segura y realizar la operación solicitada por la tarea.

6. **Regreso al Modo No Privilegiado**: Una vez completada la operación, el sistema regresa al modo no privilegiado y retoma la ejecución de la tarea.

De esta manera, la excepción SVC facilita un mecanismo para gestionar el acceso seguro a recursos y funcionalidades que de otro modo estarían restringidas para el código en modo no privilegiado. Esto es crucial para mantener la integridad y la seguridad en sistemas operativos embebidos.






# ISA
1. ¿Qué son los sufijos y para qué se los utiliza? Dé un ejemplo

2. ¿Para qué se utiliza el sufijo ‘s’? Dé un ejemplo

3. ¿Qué utilidad tiene la implementación de instrucciones de aritmética saturada? Dé un ejemplo con operaciones con datos de 8 bits.

4. Describa brevemente la interfaz entre assembler y C ¿Cómo se reciben los argumentos de las funciones? ¿Cómo se devuelve el resultado? ¿Qué registros deben guardarse en la pila antes de ser modificados?

5. ¿Qué es una instrucción SIMD? ¿En qué se aplican y que ventajas reporta su uso? Dé un ejemplo.
