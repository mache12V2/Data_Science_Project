import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
df_buyers = pd.read_csv("bike_buyers.csv")
df_buyers
#Vizualizamos los primeros 5 datos del dataframe
df_buyers.head()
#Vizualizamos los ultimos 5 datos del dataframe
df_buyers.tail()
#Vizualizamos nuestras columnas
for c in df_buyers.columns:
  print(c)
   #Vizualizamos los tipos de nuestros datos y observamos si hay datos nulos
# int64 -> enteros
# float64 -> reales
# object -> cadenas de texto
df_buyers.info()
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
#Vizualizamos maximos, minimos, media, entre otros de los tipos de datos float e int
df_buyers.describe()
#Vizualizamos maximos, minimos, media, entre otros de los tipos de datos float e int
df_buyers.describe()
#Vizualizamos la frecuencia de los datos categóricos
df_buyers.describe(include=["category"])
plt.title("PiePlot Gender")
conteo_genero = df_buyers['Gender'].value_counts()
conteo_genero.plot(kind='pie', autopct='%1.1f%%')
plt.axis('equal')
plt.title('Distribución de Gender')
plt.show()
plt.title("BoxPlot Ingresos")
df_buyers["Income"].plot.box()
plt.title("BoxPlot Age")
df_buyers["Age"].plot.box()
plt.title("BoxPlot Cars")
df_buyers["Cars"].plot.box()
plt.title("BoxPlot Children")
df_buyers["Children"].plot.box()
# Generamos el histograma
df_buyers['Occupation'].hist()

# Agregamos etiquetas y título
plt.xlabel('Occupation')
plt.ylabel('Frequency')
plt.title('Histograma de Occupations')
plt.show()
# Generamos el histograma
df_buyers['Education'].hist()

# Agregamos etiquetas y título
plt.xlabel('Education')
plt.ylabel('Frequency')
plt.title('Histograma de Education')
plt.show()

df_limpio = df_buyers.copy()
df_limpio.isna().any()
df_limpio.isna().sum()
df_limpio[df_limpio["Income"].isna()]
listaIDX = df_limpio[df_limpio["Income"].isna()].index.tolist()
def replaceIncome(idx):
  mediaIncome = df_limpio[(df_buyers["Education"]==df_limpio.loc[idx,"Education"]) & (df_limpio["Occupation"]==df_limpio.loc[idx,"Occupation"])]["Income"].mean()
  return mediaIncome
for idx in listaIDX:
  df_limpio.loc[idx,"Income"] = replaceIncome(idx)

df_limpio["Income"].isna().sum()
df_limpio[df_limpio["Age"].isna()]
listaIDX = df_limpio[df_limpio["Age"].isna()].index.tolist()
def replaceAge(idx):
  modeAge = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Cars"]>=df_limpio.loc[idx,"Cars"])]["Age"].median()
  return modeAge
for idx in listaIDX:
  df_limpio.loc[idx,"Age"] = replaceAge(idx)

df_limpio["Age"].isna().sum()
df_limpio[df_limpio["Marital Status"].isna()]

listaIDX = df_limpio[df_limpio["Marital Status"].isna()].index.tolist()
def replaceStatus(idx):
  modeStatus = df_limpio[(df_limpio["Children"]==df_limpio.loc[idx,"Children"]) ]["Marital Status"].mode().loc[0]
  return modeStatus
for idx in listaIDX:
  df_limpio.loc[idx,"Marital Status"] = replaceStatus(idx)

df_limpio["Marital Status"].isna().sum()
df_limpio[df_limpio["Home Owner"].isna()]
listaIDX = df_limpio[df_limpio["Home Owner"].isna()].index.tolist()
def replaceHome(idx):
  modeHome = df_limpio[(df_limpio["Income"]==df_limpio.loc[idx,"Income"])]["Home Owner"].mode().loc[0]
  return modeHome
for idx in listaIDX:
   df_limpio.loc[idx,"Home Owner"] = replaceHome(idx)
  
df_limpio["Home Owner"].isna().sum()
df_limpio[df_limpio["Children"].isna()]

  listaIDX = df_limpio[df_limpio["Children"].isna()].index.tolist()
def replaceChildren(idx):
  medianChildren = df_limpio[(df_limpio["Marital Status"]==df_limpio.loc[idx,"Marital Status"])]["Children"].median()
  return medianChildren
for idx in listaIDX:
   df_limpio.loc[idx,"Children"] = replaceChildren(idx)

   df_limpio["Children"].isna().sum()
   df_limpio[df_limpio["Gender"].isna()]

  listaIDX = df_limpio[df_limpio["Gender"].isna()].index.tolist()
def replaceGender(idx):
  modeGender = df_limpio["Gender"].mode().loc[0]
  return modeGender
for idx in listaIDX:
   df_limpio.loc[idx,"Gender"] = replaceGender(idx)


   df_limpio["Gender"].isna().sum()
   df_limpio[df_limpio["Cars"].isna()]

   listaIDX = df_limpio[df_limpio["Cars"].isna()].index.tolist()
def replaceCars(idx):
  medianCars = df_limpio[(df_limpio["Home Owner"]==df_limpio.loc[idx,"Home Owner"]) & (df_limpio["Children"]==df_limpio.loc[idx,"Children"])]["Cars"].median()
  return medianCars
for idx in listaIDX:
  df_limpio.loc[idx,"Cars"] = replaceCars(idx)

  df_limpio["Cars"].isna().sum()

#Income
low = 0.01
high = 0.99
df_limpio["Income"].quantile([low, high])
#income
listaOut = df_buyers[(df_buyers["Income"] > 130200) | (df_buyers["Income"] <10000)]["Income"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Income"] = df_buyers["Income"].mean()
  #Age
low = 0.01
high = 0.99
df_limpio["Age"].quantile([low, high])
#Age
listaOut = df_buyers[(df_buyers["Age"] > 71.01) | (df_buyers["Age"] <26.00)]["Age"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Age"] = df_buyers["Age"].median()
  #Cars
low = 0.01
high = 0.99
df_limpio["Cars"].quantile([low, high])
#Cars
listaOut = df_buyers[(df_buyers["Cars"] > 4.0) | (df_buyers["Cars"] <0.0)]["Cars"].index.tolist()
for id in listaOut:
  df_buyers.loc[id,"Cars"] = df_buyers["Cars"].median()
  df_limpio["Children"] = df_limpio["Children"].astype("int64")
df_limpio["Cars"] = df_limpio["Cars"].astype("int64")
df_limpio["Age"] = df_limpio["Age"].astype("int64")
df_limpio.info()
# Generamos el histograma
df_limpio['Occupation'].hist()

# Agregamos etiquetas y título
plt.xlabel('Occupation')
plt.ylabel('Frequency')
plt.title('Histograma de Occupations')
plt.show()
# Generamos el histograma
df_limpio['Education'].hist()

# Agregamos etiquetas y título
plt.xlabel('Education')
plt.ylabel('Frequency')
plt.title('Histograma de Education')
plt.show()
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
# Crear una nueva variable llamado Con_hijos, dónde Si: Children > 0, No: Children=0, para los clientes que si tienen hijos ¿Cuánto es el promedio de hijos según el nivel educativo del cliente?
df_withChildrens = df_limpio[df_limpio['Children']>0]
average_children = df_withChildrens.groupby('Education')['Children'].mean()
print(average_children)

gf = average_children.plot(kind='line')
plt.xlabel('Nivel educativo')
plt.ylabel('Promedio de hijos')
plt.title('Promedio de hijos x nivel educativo')
plt.show()
# Crear una nueva variable llamado Con_vehiculo, dónde Si: Cars>0, No: Cars=0, para los clientes que si tienen vehículo ¿Cuánto es el promedio de vehículos según la ocupación del cliente?
df_withCar = df_limpio[df_limpio['Cars']>0]
average_cars = df_withCar.groupby('Occupation')['Cars'].mean()
print(average_cars)

gf = average_cars.plot(kind='line')
plt.xlabel('Ocupación')
plt.ylabel('Promedio de carros')
plt.title('Promedio de carros x ocupación')
plt.show()
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
incomeRange = ["10000-40000","50000-90000","100000-150000"]
for i in range(len(df_limpio)):
    if df_limpio.iloc[i]["Income"] <= 40000:
      df_limpio.loc[i,"Income"] = 0
    elif df_limpio.iloc[i]["Income"] <= 90000:
      df_limpio.loc[i,"Income"] = 1
    else:
      df_limpio.loc[i,"Income"] = 2

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

#importamos la siguiente clase
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

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

