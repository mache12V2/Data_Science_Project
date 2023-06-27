---
jupyter:
  colab:
    collapsed_sections:
    - SaTrYeW-ayG2
    - lMBhwm-jWIf0
    - wIqcowUH1TQ9
    toc_visible: true
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

# **TRABAJO ACADEMICO FINAL**

> Curso: FUNDAMENTOS DE DATA SCIENCE

> Integrantes:

-   Puglisevich Vergara, Eduardo Elias
-   Cano Chocce, Samuel Esteban
-   Miranda Robles, Jerson
-   Guerreo Iparraguirre Marcelo

> Seccion: CC51

# COMPRENSIÓN DE LOS DATOS

1.  **Carga de datos**

``` python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```
``` python
df_buyers = pd.read_csv("bike_buyers.csv")
```
1.  **Inspección de datos**
``` python
df_buyers
```
``` python
#Vizualizamos los primeros 5 datos del dataframe
df_buyers.head()
```

``` python
#Vizualizamos los ultimos 5 datos del dataframe
df_buyers.tail()
```

``` python
#Vizualizamos nuestras columnas
for c in df_buyers.columns:
  print(c)
```

``` python
 #Vizualizamos los tipos de nuestros datos y observamos si hay datos nulos
# int64 -> enteros
# float64 -> reales
# object -> cadenas de texto
df_buyers.info()
```

A partir de este paso, observamos que hay algunas columnas que debemos
modificar su tipo de dato.

Modificaremos las siguientes columnas

-   ID -\> object
-   Children -\> int
-   Cars -\> int
-   Age -\> int
-   Marital Status -\> category
-   Gender -\> category
-   Education -\> category
-   Occupation -\> category
-   Home owner -\> category
-   Region -\> category
-   Purchased Bike -\> category
-   Commute Distance -\> category

``` python
# df_buyers = df_buyers.fillna(0)
df_buyers["ID"] = df_buyers["ID"].astype("object")
df_buyers["Marital Status"] = df_buyers["Marital Status"].astype("category")
df_buyers["Gender"] = df_buyers["Gender"].astype("category")
df_buyers["Education"] = df_buyers["Education"].astype("category")
df_buyers["Occupation"] = df_buyers["Occupation"].astype("category")
df_buyers["Home Owner"] = df_buyers["Home Owner"].astype("category")
df_buyers["Purchased Bike"] = df_buyers["Purchased Bike"].astype("category")
df_buyers["Region"] = df_buyers["Region"].astype("category")
df_buyers["Commute Distance"] = df_buyers["Commute Distance"].astype("category")
```
``` python
#Vizualizamos maximos, minimos, media, entre otros de los tipos de datos float e int
df_buyers.describe()
```

``` python
#Vizualizamos la frecuencia de los datos categóricos
df_buyers.describe(include=["category"])
```

1.  **Visualizacion de datos**
> -   Grafico circular (Genero)
``` python
plt.title("PiePlot Gender")
conteo_genero = df_buyers['Gender'].value_counts()
conteo_genero.plot(kind='pie', autopct='%1.1f%%')
plt.axis('equal')
plt.title('Distribución de Gender')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/6c434d630dda2552758eb4e42401c4ac9996f2b7.png)

> -   Box plot(Sueldos)

``` python
plt.title("BoxPlot Ingresos")
df_buyers["Income"].plot.box()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/469062d97d64a71f72c9c8b3375c74d4c500d938.png)
-   Box plot (Age)
``` python
plt.title("BoxPlot Age")
df_buyers["Age"].plot.box()
```
![](vertopal_2e25d94b85fb4e49986d749d56adee99/a974e53a9e5c70f1e6ddc529047ea65dde943bea.png)
-   Box plot (Cars)
``` python
plt.title("BoxPlot Cars")
df_buyers["Cars"].plot.box()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/a9a9653bbc23e4460b2a751f73999707ffe5996f.png)

-   Box plt (children)
``` python
plt.title("BoxPlot Children")
df_buyers["Children"].plot.box()
```
![](vertopal_2e25d94b85fb4e49986d749d56adee99/8d089d65dac7c348df740a4d2b863d93a31c05d1.png)

-   Histograma de Occupation

``` python
# Generamos el histograma
df_buyers['Occupation'].hist()

# Agregamos etiquetas y título
plt.xlabel('Occupation')
plt.ylabel('Frequency')
plt.title('Histograma de Occupations')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/4fe6da8bead97db5e73db2c91a35c72c9885133d.png)

-   Histograma de Education

``` python
# Generamos el histograma
df_buyers['Education'].hist()

# Agregamos etiquetas y título
plt.xlabel('Education')
plt.ylabel('Frequency')
plt.title('Histograma de Education')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/b9d60f8848c97f155c083f04ee43bfdf06670716.png)
# **PREPARACIÓN DE LOS DATOS**
1.  Limpieza de datos

Primero copiamos los datos en un nuevo df

``` python
df_limpio = df_buyers.copy()
```
**DATOS NULOS**
``` python
df_limpio.isna().any()
```

``` python
df_limpio.isna().sum()
```

Reemplazo de valores en Income

``` python
df_limpio[df_limpio["Income"].isna()]
```

Comprobamos cual es el Income del primer dato faltante, teniendo en
cuenta obvservaciones que tengan otros campos similares

Y guardamos el indice en el dataframe de la variable

-   Income
``` python
listaIDX = df_limpio[df_limpio["Income"].isna()].index.tolist()
def replaceIncome(idx):
  mediaIncome = df_limpio[(df_buyers["Education"]==df_limpio.loc[idx,"Education"]) & (df_limpio["Occupation"]==df_limpio.loc[idx,"Occupation"])]["Income"].mean()
  return mediaIncome
for idx in listaIDX:
  df_limpio.loc[idx,"Income"] = replaceIncome(idx)
```
``` python
df_limpio["Income"].isna().sum()
```

Usaremos un función similar para todas las variables que contengan datos
nulos

-   Empezaremos con Age
``` python
df_limpio[df_limpio["Age"].isna()]
```

``` python
listaIDX = df_limpio[df_limpio["Age"].isna()].index.tolist()
def replaceAge(idx):
  modeAge = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Cars"]>=df_limpio.loc[idx,"Cars"])]["Age"].median()
  return modeAge
for idx in listaIDX:
  df_limpio.loc[idx,"Age"] = replaceAge(idx)
```
``` python
df_limpio["Age"].isna().sum()
```
``` python
df_limpio[df_limpio["Marital Status"].isna()]
```

``` python
listaIDX = df_limpio[df_limpio["Marital Status"].isna()].index.tolist()
def replaceStatus(idx):
  modeStatus = df_limpio[(df_limpio["Children"]==df_limpio.loc[idx,"Children"]) ]["Marital Status"].mode().loc[0]
  return modeStatus
for idx in listaIDX:
  df_limpio.loc[idx,"Marital Status"] = replaceStatus(idx)
```
``` python
df_limpio["Marital Status"].isna().sum()
```

-   Home owner
``` python
df_limpio[df_limpio["Home Owner"].isna()]
```
::: {.cell .code id="jaWZzBEb2VjP"}
``` python
listaIDX = df_limpio[df_limpio["Home Owner"].isna()].index.tolist()
def replaceHome(idx):
  modeHome = df_limpio[(df_limpio["Income"]==df_limpio.loc[idx,"Income"])]["Home Owner"].mode().loc[0]
  return modeHome
for idx in listaIDX:
   df_limpio.loc[idx,"Home Owner"] = replaceHome(idx)
```
``` python
df_limpio["Home Owner"].isna().sum()
```
-   Children
``` python
df_limpio[df_limpio["Children"].isna()]
```

``` python
listaIDX = df_limpio[df_limpio["Children"].isna()].index.tolist()
def replaceChildren(idx):
  medianChildren = df_limpio[(df_limpio["Marital Status"]==df_limpio.loc[idx,"Marital Status"])]["Children"].median()
  return medianChildren
for idx in listaIDX:
   df_limpio.loc[idx,"Children"] = replaceChildren(idx)
```
``` python
df_limpio["Children"].isna().sum()
```

-   Gender
``` python
df_limpio[df_limpio["Gender"].isna()]
```

``` python
listaIDX = df_limpio[df_limpio["Gender"].isna()].index.tolist()
def replaceGender(idx):
  modeGender = df_limpio["Gender"].mode().loc[0]
  return modeGender
for idx in listaIDX:
   df_limpio.loc[idx,"Gender"] = replaceGender(idx)
```
``` python
df_limpio["Gender"].isna().sum()
```
-   Cars
``` python
df_limpio[df_limpio["Cars"].isna()]
```

``` python
listaIDX = df_limpio[df_limpio["Cars"].isna()].index.tolist()
def replaceCars(idx):
  medianCars = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Children"]==df_limpio.loc[idx,"Children"])]["Cars"].median()
  return medianCars
for idx in listaIDX:
  df_limpio.loc[idx,"Cars"] = replaceCars(idx)
```
``` python
df_limpio["Cars"].isna().sum()
```

**Outliers**

``` python
#Income
low = 0.01
high = 0.99
df_limpio["Income"].quantile([low, high])
```

``` python
#income
listaOut = df_buyers[(df_buyers["Income"] > 130200) | (df_buyers["Income"] <10000)]["Income"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Income"] = df_buyers["Income"].mean()

```
``` python
#Age
low = 0.01
high = 0.99
df_limpio["Age"].quantile([low, high])
```

``` python
#Age
listaOut = df_buyers[(df_buyers["Age"] > 71.01) | (df_buyers["Age"] <26.00)]["Age"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Age"] = df_buyers["Age"].median()
```

``` python
#Cars
low = 0.01
high = 0.99
df_limpio["Cars"].quantile([low, high])
```

``` python
#Cars
listaOut = df_buyers[(df_buyers["Cars"] > 4.0) | (df_buyers["Cars"] <0.0)]["Cars"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Cars"] = df_buyers["Cars"].median()
```
**Conversion de datos**

Convertimos las siguientes variables a int

-   Children
-   Cars
-   Age

``` python
df_limpio["Children"] = df_limpio["Children"].astype("int64")
df_limpio["Cars"] = df_limpio["Cars"].astype("int64")
df_limpio["Age"] = df_limpio["Age"].astype("int64")
```
``` python
df_limpio.info()
```

# **Graficos**
Histograma de Occupation (Data limpia)
``` python
# Generamos el histograma
df_limpio['Occupation'].hist()

# Agregamos etiquetas y título
plt.xlabel('Occupation')
plt.ylabel('Frequency')
plt.title('Histograma de Occupations')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/50fd9967db53dc34989b5b2723cbfff115edc438.png)

Histograma de Education (Data limpia)
``` python
# Generamos el histograma
df_limpio['Education'].hist()

# Agregamos etiquetas y título
plt.xlabel('Education')
plt.ylabel('Frequency')
plt.title('Histograma de Education')
plt.show()
```
``` python
# ¿Cuánto es el promedio de ingresos de acuerdo con si la bicicleta fue comprada o no por el cliente?
average_buy = df_limpio[df_limpio['Purchased Bike']=='Yes'].mean()
average_no_buy = df_limpio[df_limpio['Purchased Bike']=='No'].mean()
categories = ['Compro', 'No compro']
average = [average_buy['Income'], average_no_buy['Income']]
print(average)

plt.bar(categories, average)
plt.xlabel('Compra de bicicleta')
plt.ylabel('Promedio de ingresos')
plt.title('Promedio de ingresos / compra de bicicleta')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/e627c29b19d537a2d3429367042a565514c66e14.png)

``` python
# ¿Cuánto es el promedio de ingresos según el estado civil del cliente?
average_married = df_limpio[df_limpio['Marital Status']=='Married'].mean()
average_singled = df_limpio[df_limpio['Marital Status']=='Single'].mean()
categories = ['Casado', 'Soltero']
average = [average_married['Income'], average_singled['Income']]
print(average)

plt.bar(categories, average)
plt.xlabel('Estado civil')
plt.ylabel('Promedio de ingresos')
plt.title('Promedio de ingresos x estado civil')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/d51bc1d8ac3afffdd65e9eab9de721ff28af2d71.png)
``` python
# Crear una nueva variable llamado Con_hijos, dónde Si: Children > 0, No: Children=0, para los clientes que si tienen hijos ¿Cuánto es el promedio de hijos según el nivel educativo del cliente?
df_withChildrens = df_limpio[df_limpio['Children']>0]
average_children = df_withChildrens.groupby('Education')['Children'].mean()
print(average_children)

gf = average_children.plot(kind='line')
plt.xlabel('Nivel educativo')
plt.ylabel('Promedio de hijos')
plt.title('Promedio de hijos x nivel educativo')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/14ffed21af6c9ac910ff61c3c9cd7547be54f81e.png)
``` python
# Crear una nueva variable llamado Con_vehiculo, dónde Si: Cars>0, No: Cars=0, para los clientes que si tienen vehículo ¿Cuánto es el promedio de vehículos según la ocupación del cliente?
df_withCar = df_limpio[df_limpio['Cars']>0]
average_cars = df_withCar.groupby('Occupation')['Cars'].mean()
print(average_cars)

gf = average_cars.plot(kind='line')
plt.xlabel('Ocupación')
plt.ylabel('Promedio de carros')
plt.title('Promedio de carros x ocupación')
plt.show()
```

![](vertopal_2e25d94b85fb4e49986d749d56adee99/6710bbb9c56ca74efccaebac8e144fc206629770.png)
``` python
# ¿Cuánto es el promedio de edad de acuerdo con si el cliente es o no propietario de una vivienda?
average_owner = df_limpio[df_limpio['Home Owner']=="Yes"].mean()
average_noowner = df_limpio[df_limpio['Home Owner']=="No"].mean()
categories = ['Propietario', 'No Propietario']
average = [average_owner['Age'], average_noowner['Age']]
print(average)

plt.fill_between(categories, average)
plt.xlabel('Dueño de vivienda')
plt.ylabel('Promedio de edad')
plt.title('Promedio de edad x dueño de vivienda')
plt.show()
```
![](vertopal_2e25d94b85fb4e49986d749d56adee99/bddb317ab8b5ebf1a1dfe171682b7b03b0b27bb1.png)
``` python
incomeRange = ["10000-40000","50000-90000","100000-150000"]
for i in range(len(df_limpio)):
    if df_limpio.iloc[i]["Income"] <= 40000:
      df_limpio.loc[i,"Income"] = 0
    elif df_limpio.iloc[i]["Income"] <= 90000:
      df_limpio.loc[i,"Income"] = 1
    else:
      df_limpio.loc[i,"Income"] = 2
```

``` python
#Convertimos nuestras variables categoricas a int, creamos listas y eliminamos la ID
Gender = ["Female","Male"]
Bike = ["No","Yes"]
Home = ["No","Yes"]
Marital = ['Married', 'Single']
Education = ['Bachelors', 'Graduate Degree', 'High School', 'Partial College','Partial High School']
Distance = ['0-1 Miles', '1-2 Miles', '2-5 Miles', '5-10 Miles', '10+ Miles']
Occupation = ['Clerical', 'Management', 'Manual', 'Professional', 'Skilled Manual']
Region = ['Europe', 'North America', 'Pacific']

df_limpio['Purchased Bike'] = df_limpio['Purchased Bike'].map({'Yes': 1, 'No': 0})
df_limpio['Gender'] = df_limpio['Gender'].map({'Male': 1, 'Female': 0})
df_limpio['Home Owner'] = df_limpio['Home Owner'].map({'Yes': 1, 'No': 0})
df_limpio['Marital Status'] = df_limpio['Marital Status'].map({'Single': 1, 'Married': 0})
df_limpio['Education'] = df_limpio['Education'].map({'Bachelors':0, 'Graduate Degree':1, 'High School':2, 'Partial College':3,'Partial High School':4})
df_limpio['Commute Distance'] = df_limpio['Commute Distance'].map({'0-1 Miles':0, '1-2 Miles':1, '2-5 Miles':2, '5-10 Miles':3,'10+ Miles':4})
df_limpio['Occupation'] = df_limpio['Occupation'].map({'Clerical':0, 'Management':1, 'Manual':2, 'Professional':3,'Skilled Manual':4})
df_limpio['Region'] = df_limpio['Region'].map({'Europe':0, 'North America':1, 'Pacific':2})
```
# **MODELADO**
Escoger la técnica de modelado: Esta tarea consiste en la selección de
la técnica de Data Mining más apropiada al tipo de problema que se
quiere resolver. Por ejemplo, si el problema es de predicción: análisis
de regresión lineal/regresión logística.

Generar el plan de prueba: Una vez determinado el modelo, se construye y
adicionalmente se debe generar un procedimiento destinado a probar la
calidad y validez de este. Por ejemplo, en una tarea supervisada de Data
Mining como la clasificación, es común usar la razón de error como
medida de la calidad. Entonces, típicamente se separan los datos en dos
conjuntos, uno de entrenamiento y otro de prueba.

Construir el modelo: A continuación, se ejecuta la técnica seleccionada
sobre los datos previamente preparados para generar uno o más modelos.

``` python
#importamos la siguiente clase
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
```
``` python
#Creamos una instancia del LogisticRegression
modeloLogístico = LogisticRegression()
```
``` python
sz=df_limpio.shape[1]
# Dividir el conjunto de datos en entrenamiento y prueba
xtrain, xtest, ytrain, ytest = train_test_split(df_limpio.iloc[:, 1:sz-2], df_limpio.iloc[:, sz-1], test_size=0.2, random_state=67)

# Normalizar los datos de entrenamiento y prueba
scaler = StandardScaler()
xtrain = scaler.fit_transform(xtrain)
xtest = scaler.transform(xtest)

# Crear el modelo de regresión logística
model_logistic = LogisticRegression()

# Entrenar el modelo
model_logistic.fit(xtrain, ytrain)

# Realizar predicciones en el conjunto de prueba
predictions = model_logistic.predict(xtest)

# Calcular la precisión del modelo
accuracy = accuracy_score(ytest, predictions)
print("Precisión del modelo: {:.2f}%".format(accuracy * 100))
```
**Precisión del modelo: 70.00%**

