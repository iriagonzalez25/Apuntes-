# *Apuntes SQL - iria gonzález peteiro -*

-iria gonzález peteiro -


# ESTILOS/PARADIGMAS DE LA PROGRAMACIÓN

Existen dos estilos o paradigmas de la programación: el imperativo y el declarativo. A continuación podemos ver las diferencias entre ambos:

**PROGRAMACIÓN IMPERATIVA**: 
- Detalla los pasos (los algoritmos)
- Se centra en el cómo (cómo se hace algo)

**PROGRAMACIÓN DECLARATIVA**
- Declara la intención
- Se centra en el qué (qué quieres hacer)

El siguiente ejemplo es imperativo porque detalla todos los pasos de forma muy exhaustiva:
_var numbers = [1, 2, 3, 4, 5]_
_var filtered = [ ]_
_for (i=0; i<numbers.length; i++)_
_if (numbers [i]>3)_
_filtered.push(numbers[i])_


# SUBLENGUAJES SQL

Actualmente existen seis sublenguajes de SQL, que son los siguientes:
- **DDL (Data Definition Language)** → create, alter (alterar la estructura), drop (borrar tablas – no los datos de la tabla)
- **TML (Data Manipulation Language)** → insert, update, delete (borrar los datos de una tabla)
- **DQL (Data Query Language)** → SELECT
- **TCL (Transaction Control Language)** → commit, rollback
- **DLC (Data Control Language)** → grant, revoke
- **SCL (Session Control Language)** → alter session






# A TENER EN CUENTA

Siempre hay que poner ; al acabar. Si no hay ; no funciona (aunque en sqlzoo y similares funcione, en una base de datos real no) → sin ; la consulta está mal.

Con NULL hay que usar IS o IS NOT, no se puede usar el = o el LIKE. Con = y LIKE van las cadenas y las expresiones regulares.

Diferencia entre LIKE e = → cuando usamos =, lo del otro lado es una cadena (si se usa igual, lo que se pone tiene que ser exactamente); con LIKE lo otro es una expresión regular, es decir, no tiene que ser tal cual.

Ejemplo:
- _teacher.name = ‘S%’_
- _teacher.name LIKE ‘S%’_
_La diferencia es que en el primer caso el profe se tendría que llamar S%, pero en el segundo caso el profe tiene que tener como primera letra una S._

Cuando hay NULLs importa el orden del JOIN (RIGHT JOIN, LEFT JOIN), pero cuando no los hay CREO que no. La parte con = sí que es siempre intercambiable.

Los siguientes ejemplos serían igual; vemos que lo de después de ON se cambia pero lo de RIGHT JOIN no:
- _FROM dept RIGHT JOIN teacher ON dept.id = teacher.dept;_
- _FROM dept RIGHT JOIN teacher ON teacher.id = dept.dept;_

Si se pide un número de letras como MÍNIMO, se usan guiones bajos (tantos como número de letras haya que haber como mínimo) y un signo de porcentaje. Si se pide un número de letras concreto, se usan solamente guiones bajos (tantos como letras se pidan).

OJITO con OR Y AND → cuando se utiliza AND, se tienen que cumplir ambas condiciones; cuando se usa OR, solamente tiene que cumplirse una (o las dos).

Las longitudes (LENGTH) se comparan con LIKE, no con =.

AND NOT algo = algo2 es lo mismo que AND algo <> algo2

Saber el número de tuplas que hay en una consulta.

No dejar espacios entre SUM/COUNT y el paréntesis de después.

Si te pone: “For  each lo que sea”, hay que usar un GROUP BY (en los ejercicios de sqlzoo).

Diferencias WHERE de HAVING à con GROUP BY puede haber WHERE? Creo que no, si quieres ponerle una condición al GROUP BY tienes que ponerle un HAVING, no un WHERE. Suele ser HAVING COUNT(algo) pero creo que no siempre.

Muestra cada continente y el nombre del país que va primero por orden alfabético:
_SELECT name_
_FROM world AS w1_
_WHERE name <=_ _ALL(__SELECT name FROM world AS w2 WHERE w1.continent = w2.continent);_
¿Cómo modificarías esto?
_SELECT name_
_FROM world AS w1_
_WHERE name <=_ _ALL(__SELECT name FROM world AS w2 WHERE w1.continent = w2.continent AND w1.name <> w2.name);_

Cuando hay que seleccionar país de CADA continente es cuando hay que usar el AS w1 y AS w2. Creo que con esto se usa ALL (y se suele poner que la población no sea nula y que el nombre de un mundo no sea igual que el nombre del otro pero sí el continente).

En un WHERE tiene que ir primero algo > (SELECT algo). Por ejemplo, _SELECT W1.name FROM_ _world_ _AS W1 WHERE W1.population_ _> (SELECT W2.population FROM_ _world_ _AS W2 WHERE W2.name = “__Russia__”);_

Es decir, NO puede ir antes el (SELECT...) que el W1.population.

En la siguiente consulta del lenguaje SQL DQL:
_SELECT actor.name_
_FROM casting JOIN_ _loquesea_
_WHERE_ _casting.ord_ _= 1_
_GROUP BY actor.name_
_HAVING COUNT(_casting.movieid_) >= 15;_

El orden de ejecución es el siguiente: FROM, WHERE, GROUP BY, HAVING, SELECT.

COUNT(*) saca una fila y una columna solamente.

Cuando en el SELECT hay un algo normal y un COUNT, hay que usar GROUP BY.

El predicado en sql es una expresión que se evalúa como TRUE, FALSE o UNKNOWN; es una condición. Se usan predicados en las condiciones de búsqueda de las cláusulas WHERE y HAVING, en las condiciones de combinación de las cláusulas FROM y en otras construcciones que requieren un valor booleano, como ON.

* Pregunta del examen: Las instrucciones del lenguaje SQL DQL que permiten ejecutar predicados son HAVING, ON y WHERE (no sé si sólo esas en todo SQL o sólo esas en las opciones que no, pero básicamente lo permiten aquellas en las que después se puedan hacer condiciones).


# CONSULTAS

La sentencia SELECT permite realizar consultas sobre la información que reside en la base de datos.

Esta sentencia puede constar de tres partes: una en la que se indica lo que se quiere seleccionar (SELECT), otra en la que se indica de dónde se quiere obtener la información (FROM) y otra en la que se indican las condiciones que debe cumplir la información recogida (WHERE).


# OPERADORES

**Operadores lógicos**

- AND (y lógico): indica la necesidad de que se cumplan las dos condiciones que une.

- OR (o lógico): indica la necesidad de que se cumpla al menos una de las dos condiciones que une.

- NOT (negación lógica), sirve para negar una condición.

**Otro operadores**
- Menor que: <
-  Mayor que: >
- Distinto de: <>
- Menor o igual: <=
- Mayor o igual: >=
- Igual que: =
- BETWEEN x AND y: se cumple en el caso de que el valor de comparación se encuentre entre x e y.

- LIKE: se utiliza en comparaciones con cadenas de caracteres (en vez del “=”) mediante el uso de “%”, que se puede sustituir por los caracteres que sean necesarios, o mediante “_”, que se puede sustituir solo por un carácter. También se puede utilizar NOT LIKE para excluir algo del resultado.
%: sustituto para 0 o más caracteres
_: sustituto para exactamente un caracter
[lista de caracteres]: Cualquier carácter de la lista
[^lista caracteres]: Cualquier carácter que no esté en la lista
[!lista caracteres]: Cualquier carácter que no esté en la lista

- IN: se utiliza cuando se quiere seleccionar un conjunto de cosas (_WHERE name IN (‘Suecia’, ‘España’)_ _→ nos muestra lo que hayamos pedido para Suecia y España_).


# SELECT

En esta sentencia se puede utilizar *, con lo que se seleccionarían todos los campos contenidos en la tabla o se puede ir especificando uno a uno cada campo y el orden en que se quieren mostrar.

Es posible renombrar un campo a la hora de visualizar la tabla. Esto es posible con AS. Lo que se ponga como AS, si es una palabra sola, no lleva comillas, pero si son dos o más palabras sí. Ejemplo:
_SELECT teacher.name, dept.name_ _→ nos salen ambas columnas como “name”._
_SELECT teacher.name AS profes, dept.name AS depts_ _→ ahora una columna sale como “profes” y la otra como “depts”._
_SELECT dept.name, COUNT(teacher.name) AS 'nº profes'_ _→ como no es una sola palabra, es necesario ponerlo entre ‘’._

También existe el SELECT DISTINCT, que elimina los registros repetidos.


# FROM

Se pueden seleccionar las tablas que se necesiten. En este caso se realiza el product cartesiano de las tablas, y para evitar recibir más información de la deseada es necesario unir las tablas por los campos relacionados. Esto se hará a través de JOIN.


# WHERE

Las condiciones pueden cumplirse o no, simplemente si se cumple se mostrará en el resultado y si no, no. Para poner condiciones a la información a seleccionar son necesarios los operadores de comparación y comparadores lógicos.


# ORDENACIÓN

Con ORDER BY establecemos el orden en que queremos que se muestre el resultado final (por defecto es ASC). Puede ser ASC (orden ascendente) o DESC (orden descendente). Se puede utilizar LIMIT para limitar el número de resultados que queremos que nos aparezca.


# LIMIT

LIMIT indica el límite de cosas que queremos que se muestren.


# CONSULTAS AGRUPADAS

Cuando queremos un resultado que no proviene de un registro individual, sino de la agrupación de información, podemos usar GROUP BY


# DEVOLUCIÓN DE FILAS NULAS/NO NULAS

IS NULL indica si un campo está vacío, mientras que IS NOT NULL: indica si un campo no está vacío.

Ejemplo:
_SELECT idpedido_
_FROM pedidos_
_WHERE direccionEnvio IS NULL_
_En este caso, el resultado mostrará los pedidos que no tienen dirección de envío asociada._


# CONSULTAS POR INTERSECCIONES ENTRE TABLAS

Si queremos realizar una consulta que necesite varias tablas, debemos usar JOIN.


# CONCAT

Esta función concatena dos o más cadenas. Ejemplo: _queremos mostrar las capitales que incluyan el nombre del país. Por ejemplo Mexico City – Mexico:_
_SELECT capital, name_
_FROM world_
_WHERE capital LIKE CONCAT (name, '%')_


# ROUND

Esta función sirve para redondear, siguiendo la siguiente sintaxis: ROUND (algo, número). Algo es lo que queremos redondear y número es el número de decimales que queremos.


# REPLACE

REPLACE se utiliza para reemplazar siguiendo la siguiente sintaxis: REPLACE (algo, valor1, valor) → En “algo” vamos a cambiar el valor1 por el valor2.

Si por ejemplo _tenemos RELACE (‘Hola’, ‘o’, ‘a’), nos mostraría como resultado Hala, ya que se está reemplazando la a por la o en Hola._

Si por ejemplo _tenemos REPLACE (capital, name, ‘e’), nos mostraría la capital cambiando el nombre del país por una e._


# LENGTH

LENGTH nos indica cuál es la longitud de un resultado. Por ejemplo, _si ponemos LENGTH(population) nos muestra la longitud de population, o si ponemos LENGTH(name), nos muestra la longitud del nombre del país._


# LEFT

LEFT sirve para aislar. La sintaxis es la siguiente: LEFT (algo, número), siendo algo lo que queremos seleccionar y número el número de caracteres que queremos mostrar como resultado, empezando por la izquierda.

Por ejemplo: _LEFT(‘hola’, 2), se nos mostraría como resultado ho (es decir, los dos primeros caracteres de hola)._

Otro ejemplo más complejo sería el siguiente:
_SELECT LEFT(name, 5)_
_FROM world_
_En este caso, se mostraría como resultado los 5 primeros caracteres de cada nombre de la tabla world._


# ALL

ALL compara el valor escalar con un conjunto de valores de una sola columna. Se pone entre paréntesis después de ALL la columna con la que se quiere trabajar (se consigue con SELECT).


# SUM y COUNT

COUNT cuenta el número de algo que tiene ese resultado. Por ejemplo, si pones SELECT COUNT name, aparecerá como resultado el número de países que cumplan esa condición (_Por ejemplo FROM world WHERE population > 2000 → aparecerá el número de países que tienen una población mayor que 2000_).

Por otra parte, si pones SELECT SUM population, como resultado aparecerá la suma de población de lo que sea (_Por ejemplo FROM world WHERE continent = ‘Europe’ → saldrá la población total de Europa_).


# DISTINCT

Utilizando DISTINCT (en SELECT) lo que se hará es que no se repita lo que pongas como DISTINCT. Por ejemplo, _si pones SELECT DISTINCT continent, en el resultado no aparecerá dos veces el mismo continente_.


# GROUP BY

Usando GROUP BY, funciones como SUM y COUNT se aplican a grupos de lo que se ponga como GROUP BY: Es decir, si especificas GROUP BY continent, el resultado va a ser únicamente uno por continente. De este modo, _si ponemos SELECT SUM(population) FROM world GROUP BY continent, el resultado que nos saldrá será la población total de cada continente._

IMPORTANTE → se usa GROUP BY cuando quieres un resultados para todos los algo de un tabla. Por ejemplo: _SELECT game.stadium, COUNT(goal.matchid) FROM game JOIN goal ON game.id = goal.matchid GROUP BY game.stadium_ _te saldrá el estadio y los goles marcados en ese estadio para todos los estadios de la tabla._


# HAVING

HAVING es una condición para GROUP BY.


# JOIN o INNER JOIN

Cuando necesitamos datos de dos o más tablas tenemos que utilizar JOIN. Si las dos tablas no están directamente relacionadas, debemos utilizar tantos JOIN como sean necesarios. JOIN (o INNER JOIN cuando hay nulls) selecciona registros que tienen valores coincidentes en dos tablas.

La sintaxis es tabla1 JOIN tabla2 ON tabla.algo = tabla.algo2. Es decir, unes la tabla 1 y la tabla 2 con algún atributo de ellas que permitan una relación posible. En casa de que no hubiese relación posible entre ninguno de los atributos, se utilizaría una tabla más para llegar a esa relación, siendo tabla1 JOIN tabla2 ON tabla1.algo = tabla2.algo2 JOIN tabla3 ON tabla2.algo3 ON tabla3.algo4.


# LEFT JOIN

A diferencia de INNER JOIN, donde buscábamos una intersección respetada por ambas tablas, con LEFT JOIN damos prioridad a la tabla de la izquierda, y buscamos en la de la derecha. En caso de que no exista ninguna coincidencia para alguna de las filas de la tabla de la izquierda, de igual forma todos los resultados de la primera tabla se muestran.


# RIGHT JOIN

La situación es similar que con LEFT JOIN, solo que se le da prioridad a la tabla de la derecha.


# COALESCE

La función COALESCE evalúa todos los argumentos en orden y devuelve el primer valor no nulo de la lista de argumentos definidos. Por ejemplo, _si tenemos SELECT COALESCE (NULL, ‘A’, ‘B’), se nos mostraría como resultado ‘A’._
