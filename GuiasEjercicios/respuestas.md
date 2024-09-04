# _Respuestas Guía 1.2_
**0.1 Debugger** 

_¿Cuál es la diferencia entre las acciones Into, Over y Through (en el menú del debugger)?_

	
Into: 
El debugger se va a meter dentro del mensaje, por ejemplo si en la implementación actual se le envía el mensaje m1 a o1, va a entrar a la implementación de m1 y vas a seguir debuggeando desde ahí.

Over:
Por el contrario en over el debugger no se va a meter dentro del mensaje, va a "pasarlo por arriba" ejecutandolo pero no mostrandote lo que pasa dentro de el.


_¿Qué sucede al hacer clic en Restart?_

Al hacer click en restart el debugger va a volver al principio del contexto en el que se encuentre, es decir, volvería a ejecutar el mensaje que se este viendo.

_Recorrer el código con Into hasta la última línea del método m2. Luego hacer Restart. ¿Dónde queda ubicado el debugger? ¿Cuál es el valor de aVar?_

El debugger va a quedar ubicado en la primera línea del mensaje. Aunque el debugger vuelva a esa línea, el valor del colaborador aVar se vió modificado, es decir, aunque vuelvas a la primera línea del mensaje el valor del colaborador se mantiene, no se resetea.

**1.1 Colecciones**

**Array**: tienen tamaño fijo.
```
anArray := #(3 5 6 5).
anArray at:1  put:42. 
anArray #(42 5 6 5) .

anArray at:4 put:10.
anArray #(42 5 6 10) .

anArray at:5 put:10. Da error, los arrays son fijos.
```
**Ordered Collections**: su tamaño puede cambiar y los elementos se pueden repetir.

```
orderedCollection := OrderedCollection with:4 with:3 with:2 with:1.
orderedCollection an OrderedCollection(4 3 2 1).

orderedCollection size 4.

orderedCollection add:2.
orderedCollection size. 5.

orderedCollection an OrderedCollection(4 3 2 1 2) .
```


**Sets**: no hay repetidos y su tamaño puede cambiar.
```
x := Set with:4 with:3 with:2 with:1.
x a Set(4 3 2 1).

x add:2.
x size 4.
x a Set(4 3 2 1).

x add: 5.
x a Set(5 4 3 2 1) .
```
**Diccionarios**
```
x := Dictionary new.
x add: #a->4; add: #b->3; add: #c->1; add: #d->2; yourself.
x a Dictionary(#b->3 #a->4 #d->2 #c->1).

x add:#e->42.
x a Dictionary(#b->3 #a->4 #e->42 #d->2 #c->1 ).
x size 5.
x values #(3 4 42 2 1).

x at: #a 4.

x at: #z ifAbsent:24 24.
```
**1.2 Conversión de colecciones**

Array to orderedCollection, set:
```
array := #(1 2 3).

array asOrderedCollection. an OrderedCollection(1 2 3).

array asSet. a Set(1 2 3) .
```
Set to array:
```
set := #(4 3 2 1).
set #(4 3 2 1) .
set asArray. #(4 3 2 1) .
```
Dictionary to array (devuelve los valores):
```
x := Dictionary new.
x add: #a->4; add: #b->3; add: #c->1; add: #d->2; yourself.
x a Dictionary(#b->3 #a->4 #d->2 #c->1 ).

x asArray #(3 4 2 1).
```
**1.8 Algoritmo para encontrar números impares**:

Original:
```
| elements index odds |

elements:= #(1 2 5 6 9).
odds := OrderedCollection new.
index := 1.

[index <= elements size]
whileTrue: [
((elements at: index) odd) ifTrue: [odds add: (elements at: index)].
index := index +1.
].

^odds
```

Usando **do**:
```
| elements odds |

elements := #(1 2 5 6 9 10 11).
odds:= OrderedCollection new.

elements do: [:elem | elem odd ifTrue:[odds add: elem.]].

^odds. 
```
Usando **select**:
```
| elements odds |

elements := #(1 2 5 6 9 10 11).
odds:= OrderedCollection new.

odds := elements select: [:elem | elem odd].

^odds. 
```

**1.10 Algoritmo que devuelve el doble de cada número:**
	
Usando **while**:
```
| elements double index |

elements := #(1 2 5 6 9 10 11).
double := OrderedCollection new.
index := 1.


[index <= elements size] whileTrue: [
	double add: (elements at: index) * 2.
	index := index + 1.
	].


^double
```
Usando **do**:
```
| elements double |

elements := #(1 2 5 6 9 10 11).
double := OrderedCollection new.

elements do: [:elem | double add: elem * 2 ].

^double
```
Usando un mensaje **específico**:

```
| elements |

elements := (#(1 2 5 6 9 10 11))*2.

^elements. #(2 4 10 12 18 20 22)
```

**1.13 Algoritmo para encontrar el primer número par**:

Con **while**:

```
| elements index |

elements := #(1 3 5 7 9 10 12).
index := 1.

[index <= elements size] whileTrue: [
	(elements at: index) even ifTrue: [
		^elements at: index.
		].
	index := index + 1.
	].
```


Con **do**:

```
| elements |

elements := #(1 3 5 7 9 10 12).
elements do: [:elem | elem even ifTrue: [^elem.]].
```
Con un mensaje **específico**:

```
| elements |

elements := #(1 3 5 7 9 10 12).

elements detect: [:elem | elem even].
```

Cuando usamos estos algoritmos con una colección sin pares se retorna la lista de elementos completa.

Con **error** al no encontrar pares:

```
| elements |

elements := #(1 3 5 7 9).

elements detect: [:elem | elem even] ifNone:[^'No se encontró un número par'.].
```

**1.16 Algoritmo para sumar todos los elementos de una colección**:

Con **while**:

```
| elements index sumaParcial |

elements := #(1 3 5 7 9).
index := 1.
sumaParcial := 0.

[index <= elements size] whileTrue: [
	sumaParcial := sumaParcial + (elements at: index).
	index := index + 1.
	].

^sumaParcial.
```
Con **do**:

```
| elements sumaParcial |

elements := #(1 3 5 7 9).
sumaParcial := 0.

elements do: [:elem | sumaParcial := sumaParcial + elem].

^sumaParcial.
```
Utilzando mensaje para la **suma**:
