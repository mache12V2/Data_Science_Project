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

``` python
from google.colab import drive
drive.mount('/content/drive')
```
1.  **Inspección de datos**
``` python
df_buyers
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 0      | 12496              | Married    | Female     | 40000.0      | 1.0           | Bachelors       | Skilled Manual | Yes      | 0.0                  | 0-1 Miles  | Europe        | 42.0               | No  |
| 1      | 24107              | Married    | Male       | 30000.0      | 3.0           | Partial College | Clerical       | Yes      | 1.0                  | 0-1 Miles  | Europe        | 43.0               | No  |
| 2      | 14177              | Married    | Male       | 80000.0      | 5.0           | Partial College | Professional   | No       | 2.0                  | 2-5 Miles  | Europe        | 60.0               | No  |
| 3      | 24381              | Single     | NaN        | 70000.0      | 0.0           | Bachelors       | Professional   | Yes      | 1.0                  | 5-10 Miles | Pacific       | 41.0               | Yes |
| 4      | 25597              | Single     | Male       | 30000.0      | 0.0           | Bachelors       | Clerical       | No       | 0.0                  | 0-1 Miles  | Europe        | 36.0               | Yes |
| ...    | ...                | ...        | ...        | ...          | ...           | ...             | ...            | ...      | ...                  | ...        | ...           | ...                | ... |
| 995    | 23731              | Married    | Male       | 60000.0      | 2.0           | High School     | Professional   | Yes      | 2.0                  | 2-5 Miles  | North America | 54.0               | Yes |
| 996    | 28672              | Single     | Male       | 70000.0      | 4.0           | Graduate Degree | Professional   | Yes      | 0.0                  | 2-5 Miles  | North America | 35.0               | Yes |
| 997    | 11809              | Married    | NaN        | 60000.0      | 2.0           | Bachelors       | Skilled Manual | Yes      | 0.0                  | 0-1 Miles  | North America | 38.0               | Yes |
| 998    | 19664              | Single     | Male       | 100000.0     | 3.0           | Bachelors       | Management     | No       | 3.0                  | 1-2 Miles  | North America | 38.0               | No  |
| 999    | 12121              | Single     | Male       | 60000.0      | 3.0           | High School     | Professional   | Yes      | 2.0                  | 10+ Miles  | North America | 53.0               | Yes |

``` python
#Vizualizamos los primeros 5 datos del dataframe
df_buyers.head()
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age** | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------|--------------------|
| 0      | 12496              | Married    | Female     | 40000.0      | 1.0           | Bachelors       | Skilled Manual | Yes      | 0.0                  | 0-1 Miles  | Europe  | 42.0               | No  |
| 1      | 24107              | Married    | Male       | 30000.0      | 3.0           | Partial College | Clerical       | Yes      | 1.0                  | 0-1 Miles  | Europe  | 43.0               | No  |
| 2      | 14177              | Married    | Male       | 80000.0      | 5.0           | Partial College | Professional   | No       | 2.0                  | 2-5 Miles  | Europe  | 60.0               | No  |
| 3      | 24381              | Single     | NaN        | 70000.0      | 0.0           | Bachelors       | Professional   | Yes      | 1.0                  | 5-10 Miles | Pacific | 41.0               | Yes |
| 4      | 25597              | Single     | Male       | 30000.0      | 0.0           | Bachelors       | Clerical       | No       | 0.0                  | 0-1 Miles  | Europe  | 36.0               | Yes |

``` python
#Vizualizamos los ultimos 5 datos del dataframe
df_buyers.tail()
```

| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 995    | 23731              | Married    | Male       | 60000.0      | 2.0           | High School     | Professional   | Yes      | 2.0                  | 2-5 Miles  | North America | 54.0               | Yes |
| 996    | 28672              | Single     | Male       | 70000.0      | 4.0           | Graduate Degree | Professional   | Yes      | 0.0                  | 2-5 Miles  | North America | 35.0               | Yes |
| 997    | 11809              | Married    | NaN        | 60000.0      | 2.0           | Bachelors       | Skilled Manual | Yes      | 0.0                  | 0-1 Miles  | North America | 38.0               | Yes |
| 998    | 19664              | Single     | Male       | 100000.0     | 3.0           | Bachelors       | Management     | No       | 3.0                  | 1-2 Miles  | North America | 38.0               | No  |
| 999    | 12121              | Single     | Male       | 60000.0      | 3.0           | High School     | Professional   | Yes      | 2.0                  | 10+ Miles  | North America | 53.0               | Yes |

``` python
#Vizualizamos nuestras columnas
for c in df_buyers.columns:
  print(c)
```
    ID
    Marital Status
    Gender
    Income
    Children
    Education
    Occupation
    Home Owner
    Cars
    Commute Distance
    Region
    Age
    Purchased Bike

``` python
 #Vizualizamos los tipos de nuestros datos y observamos si hay datos nulos
# int64 -> enteros
# float64 -> reales
# object -> cadenas de texto
df_buyers.info()
```
    RangeIndex: 1000 entries, 0 to 999
    Data columns (total 13 columns):
     #   Column            Non-Null Count  Dtype  
    ---  ------            --------------  -----  
     0   ID                1000 non-null   int64  
     1   Marital Status    993 non-null    object 
     2   Gender            989 non-null    object 
     3   Income            994 non-null    float64
     4   Children          992 non-null    float64
     5   Education         1000 non-null   object 
     6   Occupation        1000 non-null   object 
     7   Home Owner        996 non-null    object 
     8   Cars              991 non-null    float64
     9   Commute Distance  1000 non-null   object 
     10  Region            1000 non-null   object 
     11  Age               992 non-null    float64
     12  Purchased Bike    1000 non-null   object 
    dtypes: float64(4), int64(1), object(8)
    memory usage: 101.7+ KB

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
Desafortunadamente, no podemos modificar los tipos de datos de children,
cars y age, ya que cuentan con valores nulos; por ende, modificaremos
estos tipos posteriormente

``` python
#Vizualizamos maximos, minimos, media, entre otros de los tipos de datos float e int
df_buyers.describe()
```
| **Income** | **Children**  | **Cars**   | **Age**    |
|------------|---------------|------------|------------|
| count      | 994.000000    | 992.000000 | 991.000000 | 992.000000 |
| mean       | 56267.605634  | 1.910282   | 1.455096   | 44.181452  |
| std        | 31067.817462  | 1.626910   | 1.121755   | 11.362007  |
| min        | 10000.000000  | 0.000000   | 0.000000   | 25.000000  |
| 25%        | 30000.000000  | 0.000000   | 1.000000   | 35.000000  |
| 50%        | 60000.000000  | 2.000000   | 1.000000   | 43.000000  |
| 75%        | 70000.000000  | 3.000000   | 2.000000   | 52.000000  |
| max        | 170000.000000 | 5.000000   | 4.000000   | 89.000000  |

``` python
#Vizualizamos la frecuencia de los datos categóricos
df_buyers.describe(include=["category"])
```
| **Marital Status** | **Gender** | **Education** | **Occupation** | **Home Owner** | **Commute Distance** | **Region** | **Purchased Bike** |
|--------------------|------------|---------------|----------------|----------------|----------------------|------------|--------------------|
| count              | 993        | 989           | 1000           | 1000           | 996                  | 1000       | 1000               | 1000 |
| unique             | 2          | 2             | 5              | 5              | 2                    | 5          | 3                  | 2    |
| top                | Married    | Male          | Bachelors      | Professional   | Yes                  | 0-1 Miles  | North America      | No   |
| freq               | 535        | 500           | 306            | 276            | 682                  | 366        | 508                | 519  |


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
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/6c434d630dda2552758eb4e42401c4ac9996f2b7.png)

> -   Box plot(Sueldos)

``` python
plt.title("BoxPlot Ingresos")
df_buyers["Income"].plot.box()
```
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/469062d97d64a71f72c9c8b3375c74d4c500d938.png)

-   Box plot (Age)

``` python
plt.title("BoxPlot Age")
df_buyers["Age"].plot.box()
```
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/a974e53a9e5c70f1e6ddc529047ea65dde943bea.png)

-   Box plot (Cars)

``` python
plt.title("BoxPlot Cars")
df_buyers["Cars"].plot.box()
```
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/a9a9653bbc23e4460b2a751f73999707ffe5996f.png)

-   Box plt (children)

``` python
plt.title("BoxPlot Children")
df_buyers["Children"].plot.box()
```
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/8d089d65dac7c348df740a4d2b863d93a31c05d1.png)

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
![](vertopal_20a8e0f0b2354747b198496fac6a12b0/4fe6da8bead97db5e73db2c91a35c72c9885133d.png)

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

![](vertopal_20a8e0f0b2354747b198496fac6a12b0/b9d60f8848c97f155c083f04ee43bfdf06670716.png)

# **PREPARACIÓN DE LOS DATOS**

1.  Limpieza de datos

Primero copiamos los datos en un nuevo dataframe al que le haremos la
limpieza

``` python
#Creamos una copia del dataset independiente del detaset original
df_limpio = df_buyers.copy()
```

**DATOS NULOS**

Verificamos si existen datos nulos o NA

``` python
df_limpio.isna().any()
```

Verificamos cuántos datos nulos hay

``` python
df_limpio.isna().sum()
```

Vemos que los campos que tiene valores nulos son `Marital Status`,
`Gender`, `Income`, `Children`, `Home Owner` y `Cars`. Procedemos
entonces a encontrar una técnica de limpieza para cada uno de ellos

-   Valores NA en `Income`


``` python
#Visualizamos los valores NA de income

df_limpio[df_limpio["Income"].isna()]
```

| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 9      | 19280              | Married    | Male       | NaN          | 2.0           | Partial College | Manual         | Yes      | 1.0                  | 0-1 Miles  | Europe        | NaN                | Yes |
| 110    | 21006              | Single     | Female     | NaN          | 1.0           | Partial College | Manual         | No       | 0.0                  | 0-1 Miles  | Europe        | 46.0               | Yes |
| 191    | 26944              | Single     | Male       | NaN          | 2.0           | High School     | Manual         | Yes      | 0.0                  | 0-1 Miles  | Europe        | 36.0               | Yes |
| 301    | 17926              | NaN        | Female     | NaN          | 0.0           | Bachelors       | Clerical       | No       | 0.0                  | 0-1 Miles  | Pacific       | 28.0               | Yes |
| 441    | 11061              | Married    | Male       | NaN          | 2.0           | Partial College | Skilled Manual | Yes      | 2.0                  | 5-10 Miles | Pacific       | 52.0               | Yes |
| 509    | 24357              | Married    | Male       | NaN          | 3.0           | Bachelors       | Professional   | Yes      | 1.0                  | 2-5 Miles  | North America | 48.0               | Yes |

Vemos que el campo `Income` corresponde a valores de dinero, y al ser
una cantidad pequeña de valores NA, hemos considerado que la mejor
técnica de limpieza para este campo es cambiar los valores NA por la
media de otras filas con campos similares. Estamos considerando que 2
personas con la misma educación y la misma ocupación tendrán un ingreso
similiar o promedio. Por ello, la función de reemplazo de los valores NA
de `Income` se calculará apartir de las filas `Education` y `Occupation`
que sean similares.

``` python
#Guardamos los índices de los valores NA del dataset
listaIDX = df_limpio[df_limpio["Income"].isna()].index.tolist()

#Creamos una función para calcular el promedio en función de los campos similares
def replaceIncome(idx):
  mediaIncome = df_limpio[(df_buyers["Education"]==df_limpio.loc[idx,"Education"]) & (df_limpio["Occupation"]==df_limpio.loc[idx,"Occupation"])]["Income"].mean()
  return mediaIncome

for idx in listaIDX:
  df_limpio.loc[idx,"Income"] = replaceIncome(idx)
```

Comprobamos que se ya no hayan datos NA en Income

``` python
df_limpio["Income"].isna().sum()
```
    0

Usaremos un función similar para todas las variables que contengan datos
nulos

-   Valores NA en `Age`

Vemos los valores NA que presenta `Age`

``` python
df_limpio[df_limpio["Age"].isna()]
```

| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 9      | 19280              | Married    | Male       | 13823.529412 | 2.0           | Partial College | Manual         | Yes      | 1.0                  | 0-1 Miles  | Europe        | NaN                | Yes |
| 98     | 19441              | NaN        | Male       | 40000.000000 | 0.0           | Graduate Degree | Clerical       | Yes      | 0.0                  | 0-1 Miles  | Europe        | NaN                | Yes |
| 225    | 14135              | Married    | Male       | 20000.000000 | 1.0           | Partial College | Manual         | Yes      | 0.0                  | 1-2 Miles  | Europe        | NaN                | No  |
| 371    | 22918              | Single     | Male       | 80000.000000 | 5.0           | Graduate Degree | Management     | Yes      | 3.0                  | 0-1 Miles  | Pacific       | NaN                | No  |
| 554    | 18580              | Married    | Female     | 60000.000000 | 2.0           | Graduate Degree | Professional   | Yes      | 0.0                  | 2-5 Miles  | North America | NaN                | Yes |
| 688    | 11699              | Single     | NaN        | 60000.000000 | NaN           | Bachelors       | Skilled Manual | No       | 2.0                  | 0-1 Miles  | North America | NaN                | No  |
| 770    | 17699              | Married    | Male       | 60000.000000 | 1.0           | Graduate Degree | Skilled Manual | No       | 0.0                  | 0-1 Miles  | North America | NaN                | No  |
| 986    | 23704              | Single     | Male       | 40000.000000 | 5.0           | High School     | Professional   | Yes      | 4.0                  | 10+ Miles  | North America | NaN                | Yes |


Por ser datos numéricos y tener una relación con los campos `Home Owner`
y `Cars`, utilizaremos la misma técnica como la anterior. Pues es muy
probable que dos personas que son responsables del hogar y que tiene el
mismo valor del campo Cars tengan la misma edad.

``` python
listaIDX = df_limpio[df_limpio["Age"].isna()].index.tolist()
def replaceAge(idx):
  modeAge = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Cars"]>=df_limpio.loc[idx,"Cars"])]["Age"].median()
  return modeAge
for idx in listaIDX:
  df_limpio.loc[idx,"Age"] = replaceAge(idx)
```
Comprobamos que ya no hayan datos faltantes
``` python
df_limpio["Age"].isna().sum()
```
    0
-   Valores NA en `Marital Status`

Verificamos los valores NA que presenta `Marital Status`

``` python
df_limpio[df_limpio["Marital Status"].isna()]
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**      | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age** | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|---------------------|----------------|----------|----------------------|------------|---------|--------------------|
| 8      | 22155              | NaN        | Male       | 20000.0      | 2.0           | Partial High School | Clerical       | Yes      | 2.0                  | 5-10 Miles | Pacific | 58.0               | No  |
| 27     | 18283              | NaN        | Female     | 100000.0     | 0.0           | Bachelors           | Professional   | No       | 1.0                  | 5-10 Miles | Pacific | 40.0               | No  |
| 49     | 14939              | NaN        | Male       | 40000.0      | 0.0           | Bachelors           | Clerical       | Yes      | 0.0                  | 0-1 Miles  | Europe  | 39.0               | Yes |
| 98     | 19441              | NaN        | Male       | 40000.0      | 0.0           | Graduate Degree     | Clerical       | Yes      | 0.0                  | 0-1 Miles  | Europe  | 43.0               | Yes |
| 150    | 26154              | NaN        | Male       | 60000.0      | 1.0           | Partial College     | Skilled Manual | Yes      | 1.0                  | 5-10 Miles | Pacific | 43.0               | Yes |
| 234    | 24611              | NaN        | Male       | 90000.0      | 0.0           | Bachelors           | Professional   | No       | 4.0                  | 10+ Miles  | Pacific | 35.0               | Yes |
| 301    | 17926              | NaN        | Female     | 29375.0      | 0.0           | Bachelors           | Clerical       | No       | 0.0                  | 0-1 Miles  | Pacific | 28.0               | Yes |

Los valores NA pueden relacionarse también con los valores de los campos
`Children`, pues es muy probable que 2 personas con la misma cantidad de
niños tengan una edad promedio. Por ello, se asume completar los valores
NA con el promedio de las personas que tengan una cantidad de niños
igual.

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
 0
-   Valores NA en `Home`

``` python
df_limpio[df_limpio["Home Owner"].isna()]
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 6      | 27974              | Single     | Male       | 160000.0     | 2.0           | High School     | Management     | NaN      | 4.0                  | 0-1 Miles  | Pacific       | 33.0               | Yes |
| 365    | 22636              | Single     | Female     | 40000.0      | 0.0           | Bachelors       | Clerical       | NaN      | 0.0                  | 0-1 Miles  | Europe        | 38.0               | Yes |
| 646    | 16247              | Single     | Female     | 60000.0      | 4.0           | Graduate Degree | Skilled Manual | NaN      | 0.0                  | 1-2 Miles  | North America | 47.0               | No  |
| 943    | 24322              | Married    | Female     | 60000.0      | 4.0           | Bachelors       | Skilled Manual | NaN      | 2.0                  | 0-1 Miles  | North America | 42.0               | No  |


Los valores NA de `Home Owner`pueden relacionarse con `Income`, pues es
muy probable que dos personas con el mismo ingreso sean también
responsables del hogar.

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
    0

-   Valores NA en `Children`

``` python
df_limpio[df_limpio["Children"].isna()]
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**      | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|---------------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 117    | 24065              | Single     | Female     | 20000.0      | NaN           | High School         | Manual         | Yes      | 0.0                  | 0-1 Miles  | Europe        | 40.0               | Yes |
| 217    | 13673              | Single     | Female     | 20000.0      | NaN           | Partial High School | Manual         | No       | 2.0                  | 0-1 Miles  | Europe        | 25.0               | No  |
| 386    | 28957              | Single     | Female     | 120000.0     | NaN           | Partial High School | Professional   | Yes      | 4.0                  | 10+ Miles  | Pacific       | 34.0               | Yes |
| 549    | 13453              | Married    | Female     | 130000.0     | NaN           | Bachelors           | Management     | Yes      | 3.0                  | 0-1 Miles  | North America | 45.0               | Yes |
| 638    | 18949              | Single     | Male       | 70000.0      | NaN           | Graduate Degree     | Management     | Yes      | 2.0                  | 5-10 Miles | North America | 74.0               | Yes |
| 688    | 11699              | Single     | NaN        | 60000.0      | NaN           | Bachelors           | Skilled Manual | No       | 2.0                  | 0-1 Miles  | North America | 46.5               | No  |
| 805    | 26778              | Single     | Female     | 40000.0      | NaN           | High School         | Skilled Manual | Yes      | 2.0                  | 5-10 Miles | North America | 31.0               | No  |
| 960    | 23491              | Single     | Male       | 100000.0     | NaN           | Partial College     | Professional   | No       | 4.0                  | 1-2 Miles  | North America | 45.0               | No  |

Podemos relacionar el valor de `Children` con el promedio de las otras
filas que contengan el mismo valor para `Marital Status`.

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
    0

-   Valores NA en `Gender`

``` python
df_limpio[df_limpio["Gender"].isna()]
```
| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**  | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|-----------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 3      | 24381              | Single     | NaN        | 70000.0      | 0.0           | Bachelors       | Professional   | Yes      | 1.0                  | 5-10 Miles | Pacific       | 41.0               | Yes |
| 154    | 23426              | Single     | NaN        | 80000.0      | 5.0           | Graduate Degree | Management     | Yes      | 3.0                  | 0-1 Miles  | Pacific       | 40.0               | No  |
| 335    | 24369              | Married    | NaN        | 80000.0      | 5.0           | Graduate Degree | Management     | No       | 2.0                  | 0-1 Miles  | Pacific       | 39.0               | No  |
| 601    | 29231              | Single     | NaN        | 80000.0      | 4.0           | Partial College | Professional   | No       | 2.0                  | 0-1 Miles  | North America | 43.0               | No  |
| 688    | 11699              | Single     | NaN        | 60000.0      | 2.0           | Bachelors       | Skilled Manual | No       | 2.0                  | 0-1 Miles  | North America | 46.5               | No  |
| 695    | 18390              | Married    | NaN        | 80000.0      | 5.0           | Partial College | Professional   | Yes      | 2.0                  | 0-1 Miles  | North America | 44.0               | No  |
| 867    | 26693              | Married    | NaN        | 70000.0      | 3.0           | Partial College | Professional   | Yes      | 1.0                  | 5-10 Miles | North America | 49.0               | No  |
| 908    | 23195              | Single     | NaN        | 50000.0      | 3.0           | Bachelors       | Skilled Manual | Yes      | 2.0                  | 2-5 Miles  | North America | 41.0               | Yes |
| 951    | 22296              | Married    | NaN        | 70000.0      | 0.0           | Bachelors       | Professional   | No       | 1.0                  | 0-1 Miles  | North America | 38.0               | No  |
| 973    | 11734              | Married    | NaN        | 60000.0      | 1.0           | Partial College | Skilled Manual | No       | 1.0                  | 0-1 Miles  | North America | 47.0               | No  |
| 997    | 11809              | Married    | NaN        | 60000.0      | 2.0           | Bachelors       | Skilled Manual | Yes      | 0.0                  | 0-1 Miles  | North America | 38.0               | Yes |


Para el caso del campo `Gender`, podemos simplemente reemplazar los
valores NA por la moda. Debido a que son pocos valores, este reemplazo
no significaría un cambio radical para la predicción.

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

    0

-   Valores NA en `Cars`


``` python
df_limpio[df_limpio["Cars"].isna()]
```

| **ID** | **Marital Status** | **Gender** | **Income** | **Children** | **Education** | **Occupation**      | **Home Owner** | **Cars** | **Commute Distance** | **Region** | **Age**       | **Purchased Bike** |
|--------|--------------------|------------|------------|--------------|---------------|---------------------|----------------|----------|----------------------|------------|---------------|--------------------|
| 12     | 11434              | Married    | Male       | 170000.0     | 5.0           | Partial College     | Professional   | Yes      | NaN                  | 0-1 Miles  | Europe        | 55.0               | No  |
| 196    | 16209              | Single     | Female     | 50000.0      | 0.0           | Graduate Degree     | Skilled Manual | Yes      | NaN                  | 1-2 Miles  | Europe        | 36.0               | No  |
| 202    | 18626              | Single     | Male       | 40000.0      | 2.0           | Partial College     | Clerical       | Yes      | NaN                  | 1-2 Miles  | Europe        | 33.0               | Yes |
| 351    | 13572              | Single     | Male       | 10000.0      | 3.0           | High School         | Manual         | Yes      | NaN                  | 0-1 Miles  | Europe        | 37.0               | Yes |
| 448    | 11383              | Married    | Female     | 30000.0      | 3.0           | Graduate Degree     | Clerical       | Yes      | NaN                  | 0-1 Miles  | Europe        | 46.0               | No  |
| 511    | 12207              | Single     | Male       | 80000.0      | 4.0           | Bachelors           | Management     | Yes      | NaN                  | 5-10 Miles | North America | 66.0               | Yes |
| 561    | 27218              | Married    | Female     | 20000.0      | 2.0           | Partial High School | Clerical       | No       | NaN                  | 0-1 Miles  | North America | 48.0               | No  |
| 615    | 11538              | Single     | Female     | 60000.0      | 4.0           | Graduate Degree     | Skilled Manual | No       | NaN                  | 0-1 Miles  | North America | 47.0               | Yes |
| 933    | 11941              | Single     | Male       | 60000.0      | 0.0           | Partial College     | Skilled Manual | Yes      | NaN                  | 5-10 Miles | North America | 29.0               | No  |

Podemos relacionar el campo `Cars` con los campos `Home Owner` y
`Children`, puesto que sería lógico que si 2 personas son responsables
del hogar y tienen la misma cantidad de hijos, entonces es probable que
tengan la misma cantidad de autos.

``` python
listaIDX = df_limpio[df_limpio["Cars"].isna()].index.tolist()
def replaceCars(idx):
  medianCars = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Children"]==df_limpio.loc[idx,"Children"])]["Cars"].median()
  return medianCars
for idx in listaIDX:
  df_limpio.loc[idx,"Cars"] = replaceCars(idx)
```
:::


``` python
df_limpio["Cars"].isna().sum()
```

    0


1.  Outliers

Los **Outliers** son valores atípicos que a veces pueden ser reales o
incorrectos. En cualquier caso, interfieren en la etapa del desarrollo
del modelo de la predicción, por lo que siempre se busca reducir los
outliers lo mejor posible.

Verificamos los máximos y mínimos de `Income`

``` python
#Income
low = 0.01
high = 0.99
df_limpio["Income"].quantile([low, high])
```

``` python
#income
listaOut = df_limpio[(df_limpio["Income"] > 130000) | (df_limpio["Income"] <10000)]["Income"].index.tolist()
for id in listaOut:
  df_limpio.loc[id,"Income"] = df_limpio["Income"].mean()

```

``` python
#Age
low = 0.01
high = 0.99
df_limpio["Age"].quantile([low, high])
```

``` python
#Age
listaOut = df_limpio[(df_limpio["Age"] > 71.01) | (df_limpio["Age"] <26.00)]["Age"].index.tolist()
for id in listaOut:
  df_limpio.loc[id,"Age"] = df_limpio["Age"].median()
```

``` python
#Cars
low = 0.01
high = 0.99
df_limpio["Cars"].quantile([low, high])
```

``` python
#Cars
listaOut = df_limpio[(df_limpio["Cars"] > 4.0) | (df_limpio["Cars"] <0.0)]["Cars"].index.tolist()
for id in listaOut:
  df_limpio.loc[id,"Cars"] = df_limpio["Cars"].median()
```

1.  **Conversion de datos**

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
#Eliminamos la columna de ID, pues no es necesaria para el modelado y las graficas
del df_limpio['ID']
```

``` python
df_limpio.info()
```

    RangeIndex: 1000 entries, 0 to 999
    Data columns (total 12 columns):
     #   Column            Non-Null Count  Dtype   
    ---  ------            --------------  -----   
     0   Marital Status    1000 non-null   category
     1   Gender            1000 non-null   category
     2   Income            1000 non-null   float64 
     3   Children          1000 non-null   int64   
     4   Education         1000 non-null   category
     5   Occupation        1000 non-null   category
     6   Home Owner        1000 non-null   category
     7   Cars              1000 non-null   int64   
     8   Commute Distance  1000 non-null   category
     9   Region            1000 non-null   category
     10  Age               1000 non-null   int64   
     11  Purchased Bike    1000 non-null   category
    dtypes: category(8), float64(1), int64(3)
    memory usage: 40.4 KB

LLegado a este punto, hemos tratado la data para que sea de la mejor
calidad posible, ello emplica que no tenga valores nulos ni outliers,
así como que el formato del dato sea el adecuado con el campo que
representa. Procedemos a guardar el nuevo data set limpio en un archivo
csv llamodo `bike_buyers_clean`, como se muestra a continuación.


``` python
df_buyers.to_csv('bike_buyers_clean.csv', index=False)
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

![](vertopal_20a8e0f0b2354747b198496fac6a12b0/4fe6da8bead97db5e73db2c91a35c72c9885133d.png)

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
average_buy = df_limpio[df_limpio['Purchased Bike']=="Yes"]

average_buy=average_buy['Income'].mean()
average_no_buy = df_limpio[df_limpio['Purchased Bike']=="No"]
average_no_buy=average_no_buy['Income'].mean()

categories = ['Compro', 'No compro']
average = [average_buy, average_no_buy]
print(average)

plt.bar(categories, average)
plt.xlabel('Compra de bicicleta')
plt.ylabel('Promedio de ingresos')
plt.title('Promedio de ingresos / compra de bicicleta')
plt.show()
```

``` python
# ¿Cuánto es el promedio de ingresos según el estado civil del cliente?
average_married = df_limpio[df_limpio['Marital Status']=='Married'].mean(numeric_only=True)
average_singled = df_limpio[df_limpio['Marital Status']=='Single'].mean(numeric_only=True)
categories = ['Casado', 'Soltero']
average = [average_married['Income'], average_singled['Income']]
print(average)

plt.bar(categories, average)
plt.xlabel('Estado civil')
plt.ylabel('Promedio de ingresos')
plt.title('Promedio de ingresos x estado civil')
plt.show()
```

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

``` python
# ¿Cuánto es el promedio de edad de acuerdo con si el cliente es o no propietario de una vivienda?
average_owner = df_limpio[df_limpio['Home Owner']=="Yes"].mean(numeric_only=True)
average_noowner = df_limpio[df_limpio['Home Owner']=="No"].mean(numeric_only=True)
categories = ['Propietario', 'No Propietario']
average = [average_owner['Age'], average_noowner['Age']]
print(average)

plt.bar(categories, average)
plt.xlabel('Dueño de vivienda')
plt.ylabel('Promedio de edad')
plt.title('Promedio de edad x dueño de vivienda')
plt.show()
```
# **MODELADO**

Vamos a hacer unos cambios a los datos para que estén correctamente
categorizados de tal forma que el modelo p ueda entenderlos. Ello
implica solo tener variables numéricas en el caso de campos que
contengan valores categóricos

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
