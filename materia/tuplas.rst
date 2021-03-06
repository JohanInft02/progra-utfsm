Tuplas
======
.. index:: tupla

Una **tupla** es una secuencia de valores agrupados.

Una tupla sirve para agrupar, como si fueran un único valor,
varios valores que, por su naturaleza, deben ir juntos.

El tipo de datos que representa a las tuplas se llama ``tuple``.
El tipo ``tuple`` es inmutable: una tupla no puede ser modificada
una vez que ha sido creada.

.. index:: tupla literal

Una tupla puede ser creada
poniendo los valores separados por comas y entre paréntesis.
Por ejemplo,
podemos crear una tupla que tenga el nombre y el apellido de una persona::

    >>> persona = ('Perico', 'Los Palotes')
    >>> persona
    ('Perico', 'Los Palotes')

Desempaquetado de tuplas
------------------------
.. index:: desempaquetado

Los valores individuales de una tupla pueden ser recuperados
asignando la tupla a las variables respectivas.
Esto se llama **desempaquetar la tupla** (en inglés: *unpack*)::

    >>> nombre, apellido = persona
    >>> nombre
    'Perico'

Si se intenta desempaquetar una cantidad incorrecta de valores,
ocurre un error de valor::

    >>> a, b, c = persona
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: need more than 2 values to unpack

Además, también es posible extraer los valores usando su índice,
al igual que con las listas::

    >>> persona[1]
    'Los Palotes'

A diferencia de las listas,
los elementos no se pueden modificar::

    >>> persona[1] = 'Smith'
    Traceback (most recent call last):
      File "<console>", line 1, in <module>
    TypeError: 'tuple' object does not support item assignment

Comparación de tuplas
---------------------
Dos tuplas son iguales
cuando tienen el mismo tamaño
y cada uno de sus elementos correspondientes
tienen el mismo valor::

    >>> (1, 2) == (3 / 2, 1 + 1)
    True
    >>> (6, 1) == (6, 2)
    False
    >>> (6, 1) == (6, 1, 0)
    False

.. index:: orden lexicográfico

Para determinar si una tupla es menor que otra,
se utiliza lo que se denomina **orden lexicográfico**.
Si los elementos en la primera posición de ambas tuplas son distintos,
ellos determinan el ordenamiento de las tuplas::

    >>> (1, 4, 7) < (2, 0, 0, 1)
    True
    >>> (1, 9, 10) < (0, 5)
    False

La primera comparación es ``True`` porque ``1 < 2``.
La segunda comparación es ``False`` porque ``1 > 0``.
No importa el valor que tengan los siguientes valores,
o si una tupla tiene más elementos que la otra.

Si los elementos en la primera posición son iguales,
entonces se usa el valor siguiente para hacer la comparación::

    >>> (6, 1, 8) < (6, 2, 8)
    True
    >>> (6, 1, 8) < (6, 0)
    False

La primera comparación es ``True`` porque ``6 == 6`` y ``1 < 2``.
La segunda comparación es ``False`` porque ``6 == 6`` y ``1 > 0``.

Si los elementos respectivos siguen siendo iguales,
entonces se sigue probando con los siguientes uno por uno,
hasta encontrar dos distintos.
Si a una tupla se le acaban los elementos para comparar
antes que a la otra, entonces es considerada menor que la otra::

    >>> (1, 2) < (1, 2, 4)
    True
    >>> (1, 3) < (1, 2, 4)
    False

La primera compación es ``True`` porque ``1 == 1``, ``2 == 2``,
y ahí se acaban los elementos de la primera tupla.
La segunda comparación es ``False`` porque ``1 == 1`` y ``3 < 2``;
en este caso sí se alcanza a determinar el resultado antes que se acaben los elementos
de la primera tupla.

Este método de comparación es el mismo que se utiliza
para poner palabras en orden alfabético
(por ejemplo, en guías telefónicas y diccionarios)::

    >>> 'auto' < 'auxilio'
    True
    >>> 'auto' < 'autos'
    True
    >>> 'mes' < 'mesa' < 'mesadas' < 'mesas' < 'meses' < 'mi'
    True

Usos típicos de las tuplas
--------------------------
Las tuplas se usan siempre que es necesario agrupar valores.
Generalmente, conceptos del mundo real
son representados como tuplas que agrupan información sobre ellos.
Por ejemplo,
un partido de fútbol se puede representar
como una tupla de los equipos que lo juegan::

    partido1 = ('Milan', 'Bayern')

Para representar puntos en el plano,
se puede usar tuplas de dos elementos ``(x, y)``.
Por ejemplo, podemos crear una función ``distancia``
que recibe dos puntos y entrega la distancia entre ellos::

    def distancia(p1, p2):
        x1, y1 = p1
        x2, y2 = p2
        dx = x2 - x1
        dy = y2 - y1
        return (dx ** 2 + dy ** 2) ** 0.5

Al llamar a la función, se le debe pasar dos tuplas::

    >>> a = (2, 3)
    >>> b = (7, 15)
    >>> distancia(a, b)
    13.0

Las fechas generalmente se representan como tuplas
agrupando el año, el mes y el día.
La ventaja de hacerlo en este orden (el año primero)
es que las operaciones relacionales permiten saber
en qué orden ocurrieron las fechas::

    >>> hoy = (2011, 4, 19)
    >>> ayer = (2011, 4, 18)
    >>> navidad = (2011, 12, 25)
    >>> anno_nuevo = (2012, 1, 1)
    >>> hoy < ayer
    False
    >>> hoy < navidad < anno_nuevo
    True

Una tupla puede contener otras tuplas.
Por ejemplo,
una persona puede ser descrita por su nombre, su rut
y su fecha de nacimiento::

    persona = ('Perico Los Palotes', '12345678-9', (1980, 5, 14))

En este caso,
los datos se pueden desempaquetar así::

    >>> nombre, rut, (a, m, d) = persona
    >>> m
    5

A veces a uno le interesa sólo uno de los valores de la tupla.
Para evitar crear variables innecesarias,
se suele asignar estos valores a la variable ``_``.
Por ejemplo, si sólo nos interesa el mes en que nació la persona,
podemos obtenerlo así::

    >>> _, _, (_, mes, _) = persona
    >>> mes
    5

Una tabla de datos generalmente se representa
como una lista de tuplas.
Por ejemplo,
la información de los alumnos que están tomando un ramo
puede ser representada así::

    alumnos = [
        ('Perico', 'Los Palotes', '201199001-5', 'Civil'),
        ('Fulano', 'De Tal',      '201199002-6', 'Electrica'),
        ('Fulano', 'De Tal',      '201199003-7', 'Mecanica'),
    ]

En este caso, se puede desempaquetar los valores automáticamente
al recorrer la lista en un ciclo ``for``::

    for nombre, apellido, rol, carrera in alumnos:
        print nombre, 'estudia', carrera

O, ya que el apellido y el rol no son usados::

    for nombre, _, _, carrera in alumnos:
        print nombre, 'estudia', carrera

Es posible crear tuplas de largo uno
dejando una coma a continuación del único valor::

    >>> t = (12,)
    >>> len(t)
    1

En otros lenguajes,
las tuplas reciben el nombre de **registros**.
Este nombre es común, por lo que conviene conocerlo.

Iteración sobre tuplas
----------------------
Al igual que las listas, las tuplas son iterables::

    for valor in (6, 1):
        print valor ** 2

Además,
se puede convertir una tupla en una lista
usando la función ``list``,
y una lista en una tupla usando la función ``tuple``::

    >>> a = (1, 2, 3)
    >>> b = [4, 5, 6]
    >>> list(a)
    [1, 2, 3]
    >>> tuple(b)
    (4, 5, 6)


