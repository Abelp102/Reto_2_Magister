import pandas as pd 
from pandas import DataFrame

df_titanic = pd.read_csv('train.csv')

# 1. ¿Cuántas personas iban en el titanic?
contador = df_titanic.count()
print('El número total de pasajeros en el titanic es:',contador.PassengerId)


- Lo primero que hice fue definir la variable contador, en la que nombro el dataframe importado previamente en la linea 4 y utilizo la función count() para contar, en este caso, la columna PassengerId (en MySQL este sería nuestro primary key)


# 2. ¿Cuántos hombres y mujeres sobrevivieron?
vivos = df_titanic.loc[df_titanic['Survived'] == 1] 
hombres_vivos = vivos.loc[vivos['Sex'] == 'male'].index.size
mujeres_vivas = vivos.loc[vivos['Sex'] == 'female'].index.size

print('El número de hombres que sobrevivieron es: {superv_h}, y de mujeres: {superv_m}'.format(superv_h = hombres_vivos, superv_m = mujeres_vivas))

- Aquí en primer lugar filtré el DataFrame con la condición de que los valores de la columna 'Survived' sea igual a 1 (1 sobreviven, 0 no sobreviven), luego con el dataframe modificado según mi condición de que me muestre solo los supervivientes, la función '.loc' localiza los valores de un dataframe según la condición que le demos, en este caso que 'Survived' sea igual a 1. Luego con este DataFrame filtrado en el que todos son supervivientes, buscamos los hombres con .loc también, pero en este caso cambiamos la columna por 'Sex' y ponemos 'male' para los hombres y 'female' para las mujeres. Con la función 'index.size' nos devuelve el número de hombres vivos y mujeres, en este caso.

# 3. ¿Cuál fue el top 10 de edad que más sobrevieron y el top 10 de edad que no lo lograron?
top10_suv = df_titanic.loc[df_titanic['Survived'] == 1].groupby(['Age']).size().reset_index(name='count').sort_values(by=['count'], ascending=False)
print(top10_suv.head(10))

top10_no_suv = df_titanic.loc[df_titanic['Survived'] == 0].groupby(['Age']).size().reset_index(name='count').sort_values(by=['count'], ascending=False)
print(top10_no_suv.head(10))

- 

# 4. ¿Cuántos cargos o títulos iban en el barco? Ejemplo: Capitanes, Mrs. Miss, etc. (pista: usa expresiones regulares)
def extraer_tratamiento(name):
  m = re.search(r"\w*\.", name)
  if not m:
      return ""
  return m[0][:-1]

pd.unique(df_titanic.Name.apply(extraer_tratamiento))


# 5. ¿Cuánto es la sumatoria del valor de los tickets en EUR? (pista: los tickets se vendieron en libras esterlinas)
Sumatorio_libras = df_titanic['Fare'].sum()

Sumatorio_Euros = Sumatorio_libras * 1.175
print('La sumatoria del valor de los tickets en euros es: ',Sumatorio_Euros)
