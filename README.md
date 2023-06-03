<div align="center">
  <h1>EDA para la elaboración de un Modelo predictivo de clasificación del riesgo de sufrir depresión en usuarios de redes sociales </h1>
  <h2>Manipulación y Análisis de datos con Pandas y Python</h2>
</div>

<div align="center"> 
  <img src="readme_img/python-pandas.png" width="">
</div>

## Introducción al documento

El contenido de este documento son **apuntes teoricos y prácticos** y un proyecto de **ANÁLISIS EXPLORATORIO DE DATOS** para **USUARIO DE REDES SOCIALES** del Curso de **Python para el Análisis de datos** (Realizado en **Google Colab**) y busca ser una guía para futuros trabajos personales. El mismo está dictado por Edwin Escobedo, Data Scientist del team [Data Science Research Perú](https://www.datascience.pe/).

Pandas es la librería de software libre para manipulación de datos con Python más usada. Manipula grandes sets de datos numéricos, tablas y series de tiempo. Trabaja con múltiples formatos de archivos de datos como csv o xls.

## Objetivos del documento

- Ejecutar operaciones básicas de Pandas.
- Comprender el significado y uso de los DataFrames en Análisis de Datos e Ciencia de Datos.
- Usar Computational Tools de Pandas para realizar cálculos básicos.
- Trabajar con Statisticals tools.
- Hacer preprocesamiento de datos para crea un modelo predictivo por desarrollar podría detectar de manera oportuna si una persona es depresiva, tomando en consideración el sentimiento de soledad, estrés, falta de concentración, fatiga, además del uso de redes sociales. 
- Extraer información del Data Set realizada a usuarios de redes sociales durante catorce días para fines prácticos.
- Abrir camino a que la persona encuestada pueda optar por ayuda profesional, e incluso realizar más estudios sobre el nivel de depresión que se encuentra para una pronta ayuda idónea.


## Tabla de contenido
- [Resumen](#Resumen)
- [I. Introducción](#Introducción)
- [II. Definición del problema](#Definición-del-problema)
  - [A. Usuarios de redes sociales](#Usuarios-de-redes-sociales)
  - [B. Transtornos depresivos](#Transtornos-depresivos)
- [III. Trabajos relacionados](#Trabajos-relacionados)
  - [A. Social Media and Depression Symptoms: A Network Perspective](#Social-Media-and-Depression-Symptoms-A-Network-Perspective)
  - [B. Metodología de Análisis de Emociones para Identificar Riesgo de Cometer Suicidio Generado por el COVID-19](#Metodología-de-Análisis-de-Emociones-para-Identificar-Riesgo-de-Cometer-Suicidio-Generado-por-el-COVID-19)
  - [C. Monitoreo de las tendencias de depresión en Twiter durante la pandemia de COVID-19: Estudio observacional](#Monitoreo-de-las-tendencias-de-depresión-en-Twiter-durante-la-pandemia-de-COVID-19-Estudio-observacional)
- [IV. Propuesta de Data Product](#Propuesta-de-Data-Product)
  - [A. Set de datos](#Set-de-datos)
  - [B. Modelamiento y/o análisis](#Modelamiento-y-análisis)
- [V. Beneficios](#Beneficios)
- [VI. Plan de proyecto](#Plan-de-proyecto)
- [VII. Análisis de datos](#Análisis-de-datos)
  - [A. Limpieza de datos](#Limpieza-de-datos)
  - [B. Análisis univariante](#Análisis-univariante)
    - [Categórico](#Categórico)
    - [Numérico](#Numérico)
  - [C. Análisis multivariante](#Análisis-multivariante)
  - [D. Eliminación de Outliers](#Eliminación-de-Outliers)
  - [E. Matriz de Correlación](#Matriz-de-Correlación)
    - [Categórica](#Categórica)
    - [Numérica](#Numérica)
  - [F. Codificación de variables](#Codificación-de-variables)
  - [G. Escalamiento de variables](#Escalamiento-de-variables)
  - [H. Experimentación](#Experimentación)
    - [Sin balanceo](#Sin-balanceo)
    - [Con balanceo](#Con-balanceo)

## Resumen

Este documento presenta el análisis exploratorio de un dataset resultante de encuesta realizada a usuarios de redes sociales durante catorce días, con la intención de identificar hallazgos importantes en relación al riesgo de sufrir depresión, luego de limpiar y clasificar la data en mención.

**Palabras claves—Modelo predictivo, procesamiento de datos, depresión, redes sociales, salud mental**

## Introducción

Las redes sociales han llegado a ser parte de la vida de las personas, ya que con ellas se ha obtenido una herramienta para fomentar la cercanía entre ellas, ya sea por intereses en común o para expresar opiniones.
Hasta enero de 2022 se sabe que entre las redes sociales con mayor interacción están Facebook con 2 900 millones de usuarios, e Instagram con 1 478 millones de usuarios, asimismo se prevé un crecimiento de usuarios de Twiter hasta el 2025, siendo estas redes sociales donde se publican diversos comentarios.
 Entre los usuarios de estas redes sociales se encuentran quienes sufren de depresión, lo cual, como se muestra en la “Fig. 1”, se estima que afecta aproximadamente al 3,8% de la población, de los cuales el 5,7% son los mayores de 20 años, y el 5,7% son mayores de 60 años.

<div align="center"> 
  <img src="readme_img/fig_1.png" width="">
  <p><i>Fig. 1.	Resultados del estudio Global Burden of Disease (GBD) de 2019 referente a la depresión.</i></p>
</div>

Se tomará un conjunto de datos basado en las respuestas dadas por usuarios de redes sociales, durante catorce días, en donde cuantificaba su estado de ánimo de 0 a 100, con la determinación de realizar hallazgos sobre los sentimientos que resultan predictores a un posible riesgo de sufrir depresión.

## Definición del problema

### Usuarios de redes sociales

Si bien hay diversos conjuntos de datos disponibles para analizar a los usuarios con tendencia a depresión, se les ha estado generalizando sin considerar a fondo las características de cada uno.
Una evaluación recurrente es la del procesamiento del lenguaje natural (NLP) y el aprendizaje automático, para lo cual se transforma los datos de texto no estructurado, como comentarios de usuarios en redes sociales, en datos numéricos estructurados.
Sin embargo, extraer información de personas con el fin de rastrear la depresión es una desventaja evaluarlo de la manera descrita, puesto a que se trata a todos los involucrados como si tuvieran el mismo perfil.
Ante ello se opta por encuesta realizada a cada individuo, en el cual se cuantifica del 0 al 100 los sentimientos de este, y así, en base al análisis de estos determinar si tiene tendencia a la depresión.

### Transtornos depresivos

Frente a un episodio depresivo la persona presenta dificultades en diversos ámbitos de su vida incluyendo su entorno social, y puede expresarlo a través de las redes sociales, ya sea con algún comentario no tan comprometedor, o realizando publicaciones recurrentes que den a notar su sentir depresivo.
Los tipos de episodios depresivos pueden ser leves, moderados o graves, en función de los síntomas que tenga la persona.
Entre los trastornos del estado de ánimo se encuentran los que se dan una sola vez, los recurrentes y los bipolares que tienen episodios eufóricos e irritables. Tomando en consideración los diversos estados de ánimo que puede tener una persona, se busca a través de la encuesta medirlos para llegar a una conclusión más acertada.

## Trabajos relacionados

### Social Media and Depression Symptoms *A Network Perspective*

Destaca su enfoque en el uso pasivo de las redes sociales, como lo es desplazarse por las noticias en las redes sociales, y cómo esto se relaciona con los síntomas de depresión.

### Metodología de Análisis de Emociones para Identificar Riesgo de Cometer Suicidio Generado por el COVID-19

Su objetivo es proponer y evaluar una nueva metodología tomando como fundamento el análisis de emociones para calcular masivamente la presencia de indicios de suicidio en usuarios de Twiter, haciendo uso del modelo supervisado y no supervisado.

### Monitoreo de las tendencias de depresión en Twiter durante la pandemia de COVID-19 *Estudio observacional*

Basado en un método de búsqueda de expresiones regulares de usuarios identificados con depresión, creando un clasificado de texto psicológico consiguiendo, como se visualiza en “Fig. 2”, perfiles lingüísticos de los Tweets de usuarios depresivos y no depresivos.

<div align="center"> 
  <img src="readme_img/fig_ 2.png" width="">
  <p><i>Fig. 2.	Perfiles lingüísticos de los Tweets depresivos y no depresivos.</i></p>
</div>

## Propuesta de Data Product

Se utilizará como insumo principal un set de datos listado en un archivo .csv en el repositorio de GitHub con la intención de utilizarla académicamente.

### Set de datos

Los datos elegidos para realizar el análisis son las respuestas a una encuesta de tres preguntas basadas en el uso de las redes sociales ya sea pasiva o activamente, así como las consultas a noticias de carácter político o de interés público realizada por usuarios de redes sociales durante catorce días contestando siete veces al día.


Las variables de estudio a considerar son:

1. Variables relacionadas al uso de redes sociales:
 - [x] Uso activo de redes sociales – ASMU
 - [x] Uso pasivo de redes sociales – PSMU
 - [x] Consulta de noticias - News
2. Variables relacionadas a la depresión:
 - [x]	Grado de estrés – Stress
 - [x] Sentimiento de desesperanza – Hopeless
 - [x] Sentimiento de inferioridad – Inferior
 - [x] Pérdida de interés – LossOflnt
 - [x]	Falta de concentración – Concentrat
 - [x]	Sentimiento de soledad – Loneliness
 - [x]	Sensación de fatiga – Fatigue
 - [x]	Bajo estado de ánimo - LowMood

### Modelamiento y análisis

Teniendo en consideración las variables (numéricas) de estudio anteriormente mencionadas, se elabora un tipo de algoritmo supervisado, usando un modelo de clasificación, puesto a que finalmente se trabaja con una variable categórica.

Para la variable categórica se realiza el uso de la siguiente fórmula:
```python
DeprRate = -0,025 + 0,31 Loneliness + 0,25 Inferior + 0,19 Concentrat + 0,15 Stress + 0,06 Fatigue
```
En donde involucra cinco de las variables numéricas, con el fin de calcular el índice de depresión (variable categórica).
Para la realización de la clasificación de la variable categórica, se considera como base la escala de Hamilton [5], en donde considera la puntuación de 0 a 52, clasificando de la siguiente manera:

- [x] No deprimido: 0-7
- [x] Depresión ligera/menor: 8-13
- [x] Depresión moderada: 14-18
- [x] Depresión severa: 19-22
- [x] Depresión muy severa: >23

En base a esa escala se hace la clasificación de deprimido y no deprimido en una primera instancia. También se realiza la correlación de esta variable categórica con las variables numéricas: Loneliness, stress, y news.

## Beneficios

El modelo predictivo por desarrollar podría detectar de manera oportuna si una persona es depresiva, tomando en consideración el sentimiento de soledad, estrés, falta de concentración, fatiga, además del uso de redes sociales. Por otro lado, abre camino a que la persona encuestada pueda optar por ayuda profesional, e incluso realizar más estudios sobre el nivel de depresión que se encuentra para una pronta ayuda idónea.

## Plan de proyecto

El plan del proyecto se realizará con la metodología CRISP-DM, del cual se adaptará para que se pueda centrar más en los datos que en el “negocio”. 

En la *primera fase* se realiza el análisis del contexto, enfocándose en el propósito de realizar un modelo para predecir depresión en usuarios de redes sociales.
Para esta primera fase, en el presente documento ya se plantea la problemática y el plan preliminar para alcanzar dicho propósito.
Se consideran dos días para avanzar con esta primera fase, teniendo en consideración la recopilación de la data que se procesa.
En la *segunda fase* se realiza el entendimiento de los datos, detectando que la data se tiene clasificar y limpiar antes de realizar el procesamiento para el entrenamiento del modelo predictivo.

Esta segunda fase puede llevar 1 semanas aproximadamente, considerando diferentes fuentes de datos de distintas redes sociales. 
Una de las herramientas que ya se puede ir usando desde esta fase es Python, Colab, que ayuda mucho en la limpieza de datos y su procesamiento.

En la *tercera fase* se realiza la preparación de los datos, en donde se incluye actividades como selección de atributos, así como la transformación y limpieza de los datos para el posterior modelado.
En esta tercera fase, puede tomar 1 semana debido a la cantidad de datos a procesar y atributos de clasificación que se ha de considerar.

En la *cuarta fase* se procede con el modelamiento, el cual puede llegar a ser varios modelados si se tiende a separar la data según red social de origen. Normalmente cuando se realiza este modelado puede que se tenga que volver a la fase de preparación de datos con el fin de volverlo lo más robusto posible.
Llegada a esta fase puede extenderse a 4 semanas mientras se va mejorando el modelado.

En la *quinta fase* se continúa con la evaluación, en donde ya se tiene construido el modelo que se estimada que ha alcanzado la calidad necesaria para el análisis de los datos puestos a evaluación.
Esta penúltima fase se puede en una semana, teniendo en cuenta que ya hay un modelo definido para la evaluación de los datos.

Y en la *sexta fase* se finaliza con el despliegue, que se tomará como la presentación del modelo para que pueda ser usado en la evaluación de nuevos datos con atributos similares de los que se ha basado para realizarlo.

Respecto a los recursos y perfiles, para este proyecto se necesitará los siguientes:

- [x] Data Scientist, quien será el encargado de analizar los datos precisos para el análisis predictivo según el propósito definido.
- [x]	Data Engineer, quien se encargará de la extracción, transformación y carga de los datos a evaluar con el modelado que se desarrolle.
- [x]	Especialista en salud mental, quien dará los conocimientos de las variables a considerar en la evaluación de una persona depresiva enfocada en el contexto de usuario de redes sociales.

## Análisis de datos

```python
### IMPORTACION DE LIBRERIAS NECESARIAS PARA REALIZAR EL PROYECTO ####
from google.colab import drive
drive.mount('/content/drive')
```
> *IMPORTANTE: Antes de ejecutar o luego de la ejecución del código de conexión entre Google Colab y el Drive personal, se tiene que importar dentro del Drive personal el archivo **"OSF_socialmedia_data.csv"** con el que se va trabajar, ubicado en la raíz de este respositorio.*

```python
import numpy as np
import pandas as pd
import datetime as dt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')
```

```python
### IMPORTACION DE LA DATA ####
redes = pd.read_csv("/content/drive/MyDrive/PYTHON-ANALISIS DE DATOS-DSRP/OSF_socialmedia_data.csv", index_col = 0)
redes= redes.reset_index(drop = True)
redes
```

```python
# Conteo de la data
print(f"Hay {redes.shape[0]:,} filas.")
print(f"Hay {redes.shape[1]:,} variables.")
print(f"Hay {redes['Participant'].unique().size} participantes.")
```

```python
# Información de la data
redes.info()
```

```python
# Convertir la columna Date a formato dato
redes['Date']= pd.to_datetime(redes['Date'])
redes.head()
```

```python
# Agregación de la columna DrepRate y IndDep
redes = redes.rename(columns={'Active':'ASMU'}) # USO ACTIVO DE LAS REDES SOCIALES
redes = redes.rename(columns={'DeprMood':'LowMood'}) # ESTADO DE ÁNIMO BAJO
redes['Participant'] = redes['Participant'].astype('object')

var_totales = list(redes.select_dtypes(include=['object','datetime','float64','int64']).columns)
var_totales.append('DrepRate')
var_totales
df = np.array((-0.025+0.31*redes['Loneliness']+0.25*redes['Inferior']+0.19*redes['Concentrat']+0.15*redes['Stress']+0.06*redes['Fatigue'])).round(2)
rate = pd.DataFrame(df,columns=['DrepRate'])
prueba= redes.copy()
prueba = pd.concat([prueba, rate], axis = 1,ignore_index = True)
prueba.columns=var_totales
prueba.reset_index(drop = True)
prueba
condition = np.where(prueba['DrepRate']>11.58, 'Deprimido', 'No Deprimido')
condition_1 = pd.DataFrame(condition,columns=['IndDep'])
prueba_1= prueba.copy()
prueba_1 = pd.concat([prueba_1, condition_1], axis = 1,ignore_index = True)
var_totales.append('IndDep')
prueba_1.columns=var_totales
prueba_1.reset_index(drop = True)
prueba_1
```
> *Aquí se habla de las encuestas que fueron respondidas (1) y de las que no (0). Se está ubicando las que si fueron respondidas para luego poder eliminar las que no fueron respondidas.*

```python
# La variable Responded nos indica con 1 si fue respondido y 0 que no fueron respondidos
prueba_1['Responded'].unique()
```

```python
# Eliminamos las filas con 0 ya que no fueron respondidas y no podremos analizar los valores de lás demás variables
responde = prueba_1['Responded']==0
filtro = prueba_1.loc[responde].index
redes_df = prueba_1.drop(filtro)
# Formularios respondidos
redes_df
```

```python
### ELIMINAR COLUMNAS INNECESARIAS ###
redes_df1 = redes_df.copy()
redes_df1.drop(columns = ['Date','Time','Instr_DQs','Session.Name','Notification.No','LifePak.Download.No','Responded','Completed.Session','Session.Instance','Session.Instance.Response.Lapse','Reminders.Delivered','AutoPSMU','DrepRate'], axis=1, inplace=True)
```

```python
### SEPARAR COLUMNAS POR TIPO DE VARIABLE ###

# Variables categóricas
var_categoricas = list(redes_df1.select_dtypes(include=['object']).columns)
var_categoricas.pop(2)
var_categoricas

# Variables numéricas
var_numericas = list(redes_df1.drop('LowMood', axis = 1).select_dtypes(exclude=['object','datetime']).columns)
var_numericas

# Target u objetivo a alcanzar
target = "IndDep"
target
```

### Limpieza de datos

```python
#@title Función de visualización de los valores faltantes
import matplotlib.pyplot as plt
import seaborn as sns
import missingno
def report_missings(data, opt = 0):
  """
  data = dataframe
  opt = opcion de graficar {0: todo, >0 solo faltantes}
        default= 0
  """
  data_rep = round(data.isna().sum().sort_values(ascending=False)/len(data)*100, 3)
  data_rep2 = data.isna().sum().sort_values(ascending=False)
  df = pd.concat([data_rep2, data_rep], axis=1).reset_index()
  df.columns = ["Variable", "Cant. Nulos", "% Nulos"]
  df["Cant. No Nulos"] = len(data) - df["Cant. Nulos"]
  df = df.reindex(columns=["Variable","Cant. No Nulos","Cant. Nulos","% Nulos"])
    
  print("*"*100)
  print("*"*20, "Reporte General", "*"*20)
  print("*"*100)
  print(df)
  
  if opt:
    data_rep = data_rep[data_rep > 0] # opcional
  miss = data_rep.to_frame()
  miss.columns = ['Cantidad (%)']
  miss.index.names = ['Variable']
  miss['Variable'] = miss.index

  fig = plt.figure(figsize=(15,15))
  #plot the missing value count
  #plt.figure(figsize=(10,6))
  ax1 = fig.add_subplot(3,2,1)
  print("*"*70, "Graficas de datos faltantes", "*"*70)
  print("*"*180)
  missingno.bar(data, figsize=(10,5), fontsize=12, ax=ax1, color="dodgerblue");
  plt.title("Conteo de muestras para cada variable (porcentaje y cantidad)")

  ax3 = fig.add_subplot(3,2,3)
  sns.heatmap(data.isna().transpose(),
            cmap="YlGnBu",
            cbar_kws={'label': 'Valores perdidos'})
  plt.title("Distribución de valores perdidos")
  plt.tight_layout()


  ax2 = fig.add_subplot(3,2,2)
  #sns.set(style="whitegrid", color_codes=True)
  sns.barplot(x = 'Variable', y = 'Cantidad (%)', data=miss, ax=ax2)
  plt.title("Porcentaje de datos faltantes por variable")
  plt.xticks(rotation = 90)
  #plt.savefig("missing1.png", dpi=100)
  
  

  ax4 = fig.add_subplot(3,2,4)
  missingno.heatmap(data, cmap="RdYlGn", figsize=(10,5), fontsize=12, ax=ax4)
  plt.title("Correlación de nulidad entre variables")
  ax5 = fig.add_subplot(3,2,5)
  missingno.dendrogram(data, figsize=(10,5), fontsize=12,ax=ax5)
  plt.title("Dendograma basado en la correlación de valores faltantes")
  plt.tight_layout()

```

```python
# Se hace llamado a la función
report_missings(redes_df1)
```
> *Al hacer el llamado, genera la siguiente imagen:*

<div align="center">
<img id ="foto" src="readme_img/fig_ 3.png" width="800px" height="800px"/>
</div>

```python
# Se observa la distribución de los datos para "LowMood"
sns.displot(redes_df1['LowMood'], kind="kde")
```

<div align="center">
<img id ="foto" src="readme_img/fig_ 20.png" width="800px" height="800px"/>
</div>

```python
# Nuestro método de imputación será la eliminación de las filas que tengan los valores NaN, ya que en la mayoría de las variables forman parte del 0.5 % aprox.
redes_df2 = redes_df1.copy()
redes_df3 = redes_df2.dropna()
redes_df3
```

```python
# Notamos que la cantidad de datos nulos en cero.
data_rep = round(redes_df3.isna().sum().sort_values(ascending=False)/len(redes_df3)*100, 2)
data_rep
```
> *Se vuelve a hacer el llamado a la función de visualización para poder ver que ya no existen valores nulos*

```python
report_missings(redes_df3)
```

<div align="center">
<img id ="foto2" src="readme_img/fig_ 4.png" width="800px" height="800px" />
</div>

> *Se empieza a buscar duplicados para eliminarlos, ya que van a perjudicar a nuestro modelo*

```python
# Buscamos si hay duplicados dentro de las filas
redes_unica = redes_df3.duplicated(keep='first')
redes_df3[~redes_unica]
```

```python
# Eliminamos las filas repetidas y la cantidad se reduce de 8631 a 8460.
redes_df4 = redes_df3.drop_duplicates(keep='first').reset_index(drop=True)
redes_df4
```

### Análisis univariante

#### Categórico

```python
# Se agrega la variable "IndDep" a las variables categóricas existentes
var_total = var_categoricas.copy()
var_total.append('IndDep')
var_total
```

```python
# Generar gráfica
for var in var_total:
  sns.set_style('whitegrid')
  total = float(len(redes_df4[var_categoricas]))
  plt.figure(figsize=(30,5))
  ax = sns.countplot(x=var, data=redes_df4)
  plt.xticks(size = 12)
  if var == 'Day':
    plt.xlabel('Días de la semana', fontsize=20)
  elif var == target:
    plt.xlabel('Indice de depresión', fontsize=20)
  else:
    plt.xlabel('Participantes', fontsize=20)
    ax.set_xticklabels(ax.get_xticklabels(),rotation = 90)

  for p in ax.patches:
      percentage="{:.1f}%                   ".format(100 * p.get_height()/total)
      x = p.get_x() + p.get_width()
      y = p.get_height()
      ax.annotate(percentage, (x, y),ha="right")
  plt.show()
```


<div align="center"> 
  <img src="readme_img/fig_5.png" width="800px" height="300px">
</div>

#### Numérico

```python
# Generar gráfica
redes_df4.hist(figsize=(10,15))
```

<div align="center">
<img id ="foto" src="readme_img/fig_6.png" width="800px" height="800px"/>
</div>

```python
# Generar gráfica
boxplot = redes_df4.boxplot(figsize=(20,5))
```
>*OJO: Ejecutar este código genera la primera gráfica de la Fig 3*

```python
#@title Variables propias de los participantes - indice de depresion
dias=pd.concat([redes_df4['IndDep']],axis=1)
fig,(ax)=plt.subplots(ncols=1,figsize=(40,5))
pd.crosstab(redes_df4['Participant'],redes_df4['IndDep']).plot(kind='bar',linestyle='dashed',ax=ax, ylim=[0,20])
```
>*OJO: Ejecutar este código genera la segunda gráfica de la Fig 3*

<div align="center">
<img id ="foto" src="readme_img/fig_7.png" width="800px" height="300px"/>
<p><i>Fig. 3</i></p>
</div>

```python
# Tablas extras para entender mejor la data
data = pd.crosstab(redes_df4['Participant'],redes_df4['Day'])
data
```

```python
data = pd.crosstab(redes_df4['Participant'],redes_df4['IndDep'])
data
```
### Análisis multivariante
```python
#@title Respecto a la variable objetivo
f, axes = plt.subplots(nrows=4, ncols=3, figsize=(25,15))

sns.boxplot(x="IndDep", y="Fatigue", data=redes_df4, ax=axes[0,0])
sns.boxplot(x="IndDep", y="Loneliness", data=redes_df4, ax=axes[0,1])
sns.boxplot(x="IndDep", y="Concentrat", data=redes_df4, ax=axes[0,2])
sns.boxplot(x="IndDep", y="LossOfInt", data=redes_df4, ax=axes[1,0])
sns.boxplot(x="IndDep", y="Inferior", data=redes_df4, ax=axes[1,1])
sns.boxplot(x="IndDep", y="Hopeless", data=redes_df4, ax=axes[1,2])
sns.boxplot(x="IndDep", y="Stress", data=redes_df4, ax=axes[2,0])
sns.boxplot(x="IndDep", y="PSMU", data=redes_df4, ax=axes[2,1])
sns.boxplot(x="IndDep", y="News", data=redes_df4, ax=axes[2,2])
sns.boxplot(x="IndDep", y="ASMU", data=redes_df4, ax=axes[3,0])
sns.boxplot(x="IndDep", y="LowMood", data=redes_df4, ax=axes[3,1])

df_frequency=pd.concat([redes_df4['Stress'],redes_df4['News'],redes_df4['Loneliness'],redes_df4['LowMood'],redes_df4['IndDep']],axis=1)
fig,ax=plt.subplots(ncols=3,figsize=(20,5))
sns.scatterplot(data=df_frequency,y="Loneliness",x="Stress",hue="IndDep",ax=ax[0])
sns.scatterplot(data=df_frequency,y="Loneliness",x="News",hue="IndDep",ax=ax[1])
sns.scatterplot(data=df_frequency,y="Loneliness",x="LowMood",hue="IndDep",ax=ax[2])
```

<div align="center">
<img id ="foto" src="readme_img/fig_8.png" width="800" height="400px"/>
</div>
<div align="center">
<img id ="foto" src="readme_img/fig_9.png" width="800px" height="200px"/>
</div>

### Eliminación de Outliers

```python
# Generar gráfica para visualizar los outliers
boxplot = redes_df4.boxplot(figsize=(20,5))
```
>*OJO: Ejecutar este código genera la primera gráfica de la Fig 4*

```python
# Hallando el RIC para todo las variables

for var in redes_df4.drop(columns=var_total).columns.values:
  Q1 = np.percentile(redes_df4[var],25,interpolation = "midpoint")
  Q3 = np.percentile(redes_df4[var],75,interpolation = "midpoint")

  RIC = Q3-Q1

  superior = np.where(redes_df4[var]>= (Q3+1.5*RIC))
  inferior = np.where(redes_df4[var]<= (Q1-1.5*RIC))

  redes_df5 = redes_df4.drop(superior[0])
  redes_df5 = redes_df5.drop(inferior[0])
```

```python
# Generar gráfica para visualizar que se eliminaron los outliers
boxplot = redes_df5.boxplot(figsize=(20,5))
```
>*OJO: Ejecutar este código genera la segunda gráfica de la Fig 4*

<div align="center"> 
  <img src="readme_img/fig_10.png" width="800px" height="300px">
  <p><i>Fig. 4</i></p>
</div>

### Matriz de Correlación

```python
# Correlación de variables numéricas
matriz_crr = redes_df5[var_numericas + ["IndDep"]].copy()
matriz_crr = pd.get_dummies(matriz_crr, columns=["IndDep"], drop_first=False)
matriz_crr.head()
```

#### Categórica

```python
# Correlación de variables categoricas
matriz_cat = redes_df5[var_categoricas + ["IndDep"]].copy()
matriz_cat.head()
```

```python
#@title funciones categoricas
from sklearn import preprocessing
from scipy.stats import chi2_contingency
def cramers_V(var1,var2):
  crosstab = np.array(pd.crosstab(var1,var2, rownames=None, colnames=None)) 
  chi2 = chi2_contingency(crosstab)[0]
  n = np.sum(crosstab)
  phi2 = chi2 / n
  r, k = crosstab.shape
  phi2corr = max(0, phi2 - ((k-1)*(r-1))/(n-1))
  rcorr = r - ((r-1)**2)/(n-1) 
  kcorr = k - ((k-1)**2)/(n-1)
  return np.sqrt(phi2corr / min((kcorr-1), (rcorr-1)))
rows = []
for var1 in matriz_cat.columns:
  col = []
  for var2 in matriz_cat.columns:
    cramer = cramers_V(matriz_cat[var1], matriz_cat[var2])
    col.append(round(cramer, 2))
  rows.append(col)

plt.figure(figsize=(6,6))
rows = np.array(rows)
matr_corr = pd.DataFrame(rows, columns = matriz_cat.columns, index = matriz_cat.columns)
mask = np.triu(np.ones_like(matr_corr, dtype = np.bool))
sns.heatmap(matr_corr, mask = mask, cmap = "BrBG", annot = True, vmin = -1, vmax = 1)
plt.show()
```

<div align="center"> 
  <img src="readme_img/fig_11.png" width="800px" height="600px">
</div>

#### Numérica

```python
Correlación de variables numéricass
plt.figure(figsize=(16,6))
mask = np.triu(np.ones_like(matriz_crr.corr(), dtype = np.bool))
sns.heatmap(round(matriz_crr.corr(), 2), mask = mask, cmap = "Spectral", annot = True, vmin = -1, vmax =1 )
plt.show()
```

<div align="center"> 
  <img src="readme_img/fig_12.png" width="800px" height="400px">
</div>

### Codificación de variables

```python
redes_df5

redes_df6=redes_df5.copy()
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split
encoder = LabelEncoder()
# Encode labels in column
for i in var_categoricas: 
  redes_df6[i]= encoder.fit_transform(redes_df6[i]) 
redes_df6
# Codificar el target

dic_cat = {
    "No Deprimido":0, 
    "Deprimido":1
    }

redes_df6[target] = redes_df6[target].map(dic_cat)
redes_df6

# redes_df6 = pd.get_dummies(redes_df6, columns=[target], drop_first=False)
# redes_df6
```

<div align="center"> 
  <img src="readme_img/fig_13.png" width="800px" height="300px">
</div>

```python
redes_df6.info()
```

### Escalamiento de variables

```python
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import MinMaxScaler

redes_df7 = redes_df6.copy()
data_sc = redes_df7.drop([target],axis = 1)
data_nsc = redes_df7[target].reset_index(drop=True)
```

```python
#@title seccion de funciones
def scaler_data(data, scaler=0):
  # data: el dataframe a escalar
  # scaler: 0 (default) no aplicar nada
  if scaler==0:
    return data, np.nan    
  if scaler==1:
    sc = StandardScaler()
  else:
    sc = MinMaxScaler()
  data_tr = sc.fit_transform(data)

  return data_tr, sc
```

```python
#@title Seleccionar método de escalamiento { run: "auto" }
aplicar_todo = False #@param {type:"boolean"}
dicc_scaler= {"No aplicar":0, "StandardScaler":1, "MinMaxScaler":2}
method_scaler = "StandardScaler" #@param ["No aplicar", "StandardScaler", "MinMaxScaler"]
```

```python
print(f"Scaler {method_scaler}:")
redes_sc, sc = scaler_data(data_sc, dicc_scaler[method_scaler])
sc
```

```python
redes_sc_df=pd.DataFrame(redes_sc,columns=data_sc.columns.values)
redes_sc_df
```

```python
redes_sc_df = pd.concat([redes_sc_df, data_nsc], axis = 1, ignore_index = True)
redes_sc_df.columns = redes_df6.columns.values
redes_sc_df
```
> *El resultado de ejecutar este último código es la siguiente tabla*

<div align="center"> 
  <img src="readme_img/fig_14.png" width="800px" height="300px">
</div>

### Experimentación

<div align="center"> 
  <img src="readme_img/fig_15.png" width="800px" height="100px">
</div>

#### Sin balanceo

<div align="center">
<img id ="foto" src="readme_img/fig_16.png" width="800px" height="400px"/>
</div>
<div align="center">
<img id ="foto" src="readme_img/fig_17.png" width="800px" height="800px"/>
</div>

#### Con balanceo

<div align="center">
<img id ="foto" src="readme_img/fig_18.png" width="800px" height="400px"/>
</div>
<div align="center">
<img id ="foto" src="readme_img/fig_19.png" width="800px" height="800px"/>
</div>
