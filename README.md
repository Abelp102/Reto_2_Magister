# 1. ¿Cuántas personas iban en el titanic?
-Lo primero que hice fue definir la variable contador, en la que nombro el dataframe importado previamente en la linea 4 y utilizo la función count() para contar, en este caso, la columna PassengerId (en MySQL este sería nuestro primary key)


# 2. ¿Cuántos hombres y mujeres sobrevivieron?
- Aquí en primer lugar filtré el DataFrame con la condición de que los valores de la columna 'Survived' sea igual a 1 (1 sobreviven, 0 no sobreviven), luego con el dataframe modificado según mi condición de que me muestre solo los supervivientes, la función '.loc' localiza los valores de un dataframe según la condición que le demos, en este caso que 'Survived' sea igual a 1. Luego con este DataFrame filtrado en el que todos son supervivientes, buscamos los hombres con .loc también, pero en este caso cambiamos la columna por 'Sex' y ponemos 'male' para los hombres y 'female' para las mujeres. Con la función 'index.size' nos devuelve el número de hombres vivos y mujeres, en este caso.

# 3. ¿Cuál fue el top 10 de edad que más sobrevieron y el top 10 de edad que no lo lograron?
- Para hallar las 10 edades más frecuentes que sobrevivieron, volvemos a poner la condición de que hayan sobrevivido con la función '.loc()' seleccionando la columna 'Survived' e igualandolo a 1, posteriormente agrupamos por edad con la función '.groupby()', con 'size()' contamos los casos de cada grupo y luego ustilicé '.reset_index(name='count') para que nos devuelva un dataframe y con 'sort_values(by=['count'], ascending=False', hacemos que la frecuencia se ordene de mayor a menor. 

- Para el top 10 de las edades que no lo lograron simplemente cambiamos la condición de 'Survived' igualandolo a 0.

# 4. ¿Cuántos cargos o títulos iban en el barco? Ejemplo: Capitanes, Mrs. Miss, etc. (pista: usa expresiones regulares)
- Aquí creamos una función con el nombre de extraer_tratamientos en el que la expresión regular busca la primera palabra que aparezca terminada por punto. Si no encuentra ninguna, devuelve la cadena vacía. Si la encuentra, devuelve esa palabra menos el punto (por eso el [:-1]). Esto nos devolvería todos los valores repetidos de todos los registros de la columna name, para quedarnos solo con un únco elemento de todos aquellos que se repiten usamos la función 'pd.unique()', el '.apply()' es para aplicar la función a cada uno de los elementos de nuestra columna (Name) del dataframe.

# 5. ¿Cuánto es la sumatoria del valor de los tickets en EUR? (pista: los tickets se vendieron en libras esterlinas)
- En primer lugar creamos la variable de la sumatoria, simplemente nombramos el dataframe y seleccionamos la columna, posteriormente
