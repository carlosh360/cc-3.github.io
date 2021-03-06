---
layout: post
title:  "Laboratorio 10"
date:   2017-01-11
category: lab
description: >
    Con este laboratorio empezaremos a trabajar en Logisim y sera como una guia para realizar el último proyecto de este curso.
---

#### Ejercicio 0: Lo Básico

Vamos a comenzar creando un simple circuito solo para conocer como poner las compuertas y los cables.

* Comiencen haciendo click en el botón “AND gate”. Esto va a causar que la sombra del AND gate siga al cursor por todas partes. Hagan una vez click en la ventana del main schematic para poner el AND gate.
* Hagan click al botón “Input Pin”. Ahora, posicionen dos “input pins” en algún lugar a la izquierda del AND gate.
* Hagan click al boton “Output Pin”. Despues posicionen el pin en algún lugar a la derecha del AND gate.

Su main schematic debería verse algo parecido a esto:

![fig1](/assets/img/labs/schematic1.gif)

* Hagan click al botón “Select tool”. Hagan click y arrastren para conectar los input pins de la izquierda del AND gate al AND gate. Despues la salida del AND conectenla al output pin.

Deberia de verse algo como esto:

![fig2](/assets/img/labs/schematic2.gif)

* Finalmente, hagan click a la herramienta “Poke” y traten de hacer click a los input pins en su main schematic. Observen que pasa.

***

#### Ejercicio 1: Sub-Circuits

Así como los programas en C pueden contener funciones en varias partes, los schematic pueden tener sub-circuits. En esta parte del lab, vamos a crear varios subcircuits para demostrar su uso.

1. Creen un nuevo schematic (File->New).
2. Creen un nuevo subcircuit (Project->Add Circuit). Les va a salir que le pongan un nombre a su circuito; llamenlo “NAND”.
3. En la nueva ventana de schematic, creen una simple compuerta NAND que tome dos input pins en el lado izquierdo y un output pin en el lado derecho. Hagan esto sin utilizar la compuerta que ya se llama NAND en la carpeta GATES.
4. Vuelvan a su main schematic, haciendo doble click en main, en la parte donde están los circuitos.
5. Ahora, hagan click en la lista a su NAND. Esto le va a decir a Logisim que quieren añadir su NAND en su main schematic.
6. Traten de poner su NAND en el main schematic. Si lo hicieron bien, van a ver un gate con 2 input pins en la izquierda y un output pin en la derecha. Traten de probarlo para ver si trabaja como esperaban.
7. Repitan estos pasos para crear mas subcircuits: NOR, XOR, MUX de 2 a 1 y de 4 a 1. No utilicen los que ya estan pre-instalados. Sin embargo, cuando construyan sus propios subcircuits, pueden utilizarlos para construir otros.

**HINT: Utilizen tablas de verdad**

***

#### Ejercicio 2: Storing State

Ahora implementemos el circuito del que hemos estado hablando en la clase, que incrementa un valor **ad infinitum**. La diferencia entre este circuito y los circuitos que construyeron hasta al momento en el lab es que este necesita de algunos registros. Lo siguiente les va a enseñar como añadir registros a su circuito.

* Creen un nuevo subcircuit (Project -> Add Circuit). Llamen a este nuevo circuito, AddMachine
* Carguen la libreria aritmética si no esta cargada ya (Ir a Project -> Load Library -> Built in Library y seleccionen "Arithmethic"). Esta libreria contiene elementos que realizan operaciones aritmeticas basicas. Cuando carguen la libreria, en el buscador del circuito actual, a la izquierda tendran un nuevo folder llamado "Arithmethic".

![fig3](/assets/img/labs/arithmetic.gif)

* Seleccionen el adder subcircuit de la libreria "Arithmethic" y ponganlo en su subcircuit AddMachine.
* Carguen la libreria "Memory" (Ir a Project -> Load Library -> Built in Library y seleccionen "Memory"). Esta libreria contiene elementos de memoria para mantener un estado en el circuito. Un nuevo folder llamado "Memory" a la izquierda tiene que estar en el buscador del circuito actual.
* Seleccionen register del folder "Memory" y pongan un registro en su subcircuit. Aqui abajo hay un diagrama de las partes del registro


![fig4](/assets/img/labs/register.gif)

* Conecten un "clock" a su registro. Pueden encontrar uno en el folder "Wiring" en el buscador del circuito actual.
* Conecten el registro y el adder juntamente basado en el diagrama de la clase.
* Conecten una constante de 8-bits a la segunda entrada del adder. Pueden encontrar la "constante" en el folder "Wiring".
* Agreguen dos pins de salida a su circuito para que puedan visualizar que es lo que sale del adder y del registro.

Al final tendran esto:

![fig5](/assets/img/labs/AddMachine.png)

Ahora vamos a ver si construyeron su circuito correctamente

1. Vayan al "main" subcircuit haciendo doble click en "main" del buscador del circuito actual.
2. Hagan click en su circuito "AddMachine" para seleccionarlo.
3. Cambien la direccion de su circuito. Cada circuito tiene esta propiedad para que puedan cablear a su manera.
4. Pongan su subcircuit AddMachine en el main subcircuit.
5. Seleccionen el subcircuit AddMachine que pusieron en main.
6. Conecten los pines de salida al subcircuit AddMachine. Los pines de salida estan ordenados de arriba hacia abajo, de izquierda a derecha. Asi, si siguieron la esquematica de arriba, entonces el pin de arriba a la derecha saca el valor del adder, y el pin de abajo lo del registro.
7. Click derecho en su subcircuit AddMachine, y seleccionen "View AddMachine" Este es el unico methodo que ayuda a preservar el estado. Doble click en el circuito ya que el buscador a la izquierda hace que logisim piense que ustedes quieren editar el circuito en vez de solo checkear que estado tiene el circuito.
8. Inicialicen el valor del registro a 1. Pueden hacer esto primero, haciendo click en el valor del registro con ayuda de la herramienta "poke". Despues introduciendo el valor hexadecimal.
9. Para regresar al circuito "main" y preservar el estado, ir a Simulate -> Go Out To State -> main. Alternativamente, pueden presionar control y la tecla de hacia arriba.
10. Comiencen a correr su circuito iendo a Simulate -> Ticks Enabled. Su circuito deberia estar sacando un contador en una forma binaria.
11. Si ustedes quieren que su circuito vaya mas rapido, pueden cambiar la frecuencia de los ticks iendo a Simulate -> Ticks Frequency y poner una mas alta.

***

#### Ejercicio 3: FSMs to digital logic

Ahora con el conocimiento adquirido podemos empezar a hacer cosar realmente cool. Pasar una maquina de estados finitos (FSM) a un circuito logico digital.

Si ustedes han estado poniendo atencion en clase se habran dado cuenta que el circuito que construyeron en el ejercicio 2 se mira casi igual al diagrama de un circuito FSM. Vamos a modificar el circuito para implementar el siguiente FSM:

_Si dos unos en una fila o dos zeros en una fila ya han sido vistos, siempre sacara zero el circuito. De otra manera sacara uno._

* Noten que el FSM es implementado por el siguiente diagrama

![fig6](/assets/img/labs/FSM.png)

* Observen que a continuación está la tabla de verdad para este diagrama.

| st1 | st0 | input | next st1 | next st0 | output |
|:---:|:---:|:-----:|:--------:|:--------:|:------:|
|  0  |  0  |   0   |     0    |     1    |    1   |
|  0  |  0  |   1   |     1    |     0    |    1   |
|  0  |  1  |   0   |     1    |     1    |    0   |
|  0  |  1  |   1   |     1    |     0    |    1   |
|  1  |  0  |   0   |     0    |     1    |    1   |
|  1  |  0  |   1   |     1    |     1    |    0   |
|  1  |  1  |   0   |     1    |     1    |    0   |
|  1  |  1  |   1   |     1    |     1    |    0   |

* Nosotros les vamos a dar un circuito ya empezado de Logisim

```shell
$ cp
```

* Noten que la parte de arriba del circuito se mira casi igual como nuestro circuito adder anterior, pero ahora hay un bloque FSMLogic en vez de un bloque adder. El FSMLogic es el circuito logico combinacional para el FSM. Nosotros hicimos el bit de output, ya que es el mas dificil de simplificar e implementar. Ustedes tienen que completar el circuito completando (valga la redundancia) StateBitOne y StateBitZero.


Pueden ir directamente de la tabla al circuito, o pueden notar que por cada bit de estado, hay solo dos situaciones posibles en donde es zero. Esto puede hacer la vida mas facil si piensan fuera de lo habitual... ;)
