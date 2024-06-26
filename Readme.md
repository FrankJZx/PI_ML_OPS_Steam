# Proyecto MLOps de Steam de:

![Texto alternativo](img/imagen1.png)

## Introducción
¡Bienvenido a mi proyecto MLOps de Steam!

En este proyecto, asumiremos el rol de un Ingeniero MLOps en Steam. Nuestra tarea es crear un sistema de recomendación de videojuegos utilizando aprendizaje automático. Los datos necesitan ser refinados, y nuestra tarea es llevarlos en un estado utilizable, desarrollar un Producto Mínimo Viable (MVP) y desplegarlo como una API RESTful.

## Información del Juego en Steam
En este proyecto, trabajamos con tres archivos JSON que contienen datos sobre los juegos en la plataforma. 
Cada archivo aporta una base de datos de distintas caracteristicas:

* australian_user_reviews.json: <br>
Este conjunto de datos es de opiniones de usuarios sobre los juegos que han experimentado en Steam. Ofrece detalles sobre si recomendaron o no un juego y estadísticas sobre la utilidad de los comentarios. contiene: el ID del usuario, su URL de perfil y el ID del juego que están comentando.

![Texto alternativo](img/imagen2.png)



* australian_users_items.json:<br>
Aquí, obtenemos una visión panorámica de los juegos que cada usuario ha jugado y cuánto tiempo les han dedicado.

![Texto alternativo](img/imagen3.png)



* output_steam_games.json: <br>
Este conjunto de datos proporciona una ventana a los propios juegos en Steam. Incluye información vital como títulos, desarrolladores, precios, características técnicas y etiquetas.

![Texto alternativo](img/imagen4.png)

## Flujo de Trabajo Propuesto

### Ingeniería de Datos

- **Limpieza y Transformación de Datos:** Enfoque inicial en leer el conjunto de datos en el formato correcto. Eliminar columnas innecesarias para optimizar el rendimiento de la API y el entrenamiento del modelo. En este proyecto el etl se divide entre los tres conjuntos de datos que fueron proporcionados y ofrecen informacion acerca de las distintas caracteristicas y opiniones de los juegos presentes en la plataforma.
["Etl_games"](jupyter_nooteboks/01_Etl_games.ipynb)
["Etl_items"](jupyter_nooteboks/01_Etl_items.ipynb)
["Etl_reviews"](jupyter_nooteboks/01_Etl_review.ipynb)

- **Análisis de Sentimiento:** Crear una nueva columna, 'sentiment_analysis', aplicando análisis de sentimiento mediante Procesamiento de Lenguaje Natural (NLP) a las reseñas de usuarios. La escala que se utilizo fue: '0' para comentarios negativos, '1' para neutrales y '2' para positivos.

### Análisis Exploratorio de Datos (EDA)

- **Procesos:** Se realizo un EDA manual de todos los archivos después del ETL para investigar las relaciones entre variables, identificar valores atípicos y descubrir patrones interesantes dentro del conjunto de datos, para esta tarea se utilizan diferentes librerias y medidas estadisticas. ["Eda"](jupyter_nooteboks/02_Eda_all.ipynb)

### Explicacion detallada

- **Creación de DataFrames:** Antes de desarrollar las funciones de la API, se crearon DataFrames con el fin de optimizar el espacio y mejorar el rendimiento de las funciones. Estos DataFrames se utilizaron para almacenar datos específicos necesarios para las consultas de la API. ["data"](data)


### Desarrollo de la API

- **Framework:** Utilizar el framework FastAPI para exponer los datos de la empresa a través de endpoints RESTful.
- **Endpoints:**
  - `developer( desarrollador : str )`: Cantidad de items y porcentaje de contenido Free 
  - `userdata( User_id : str )`: Debe devolver cantidad de dinero gastado por el usuario, el porcentaje de recomendación y cantidad de items.
  - `best_developer_year( año : int )`: Devuelve el top 3 de desarrolladores con juegos MÁS recomendados por usuarios 
  - `PlayTimeGenre(genero: str)`: Devuelve el año de lanzamiento con más horas jugadas para el género especificado.
  - `UserForGenre_parte_1(genero: str)`: Devuelve el usuario con más horas jugadas para el género dado y una lista de acumulación de horas jugadas por año.
  - `UserForGenre_parte_2(genero: str)`: Devuelve el total de horas jugadas para cada genero.
  - `UsersRecommend(año: int)`: Devuelve el top 3 de juegos más recomendados por usuarios para el año especificado.
  - `UsersWorstDeveloper(año: int)`: Devuelve el top 3 de desarrolladoras con juegos menos recomendados por usuarios para el año especificado.
  - `sentiment_analysis(empresa_desarrolladora: str)`: Devuelve un diccionario con el recuento de análisis de sentimiento para reseñas asociadas con el desarrollador de juegos especificado.


### Modelo de Aprendizaje Automático

- **Sistema de Recomendación:** Se implementa un sistema de recomendación de filtrado colaborativo item-item. En este caso el sistema de recomendacion funciona tomando un item y encontrando cinco similares a este. Para poder lograr deployar el modelo con espacio de memoria limitado se utiliza una parte del total de los datos, esto significa que se usa solo una muestra de los datos para realizar la recomendacion aunque esto puede conllevar a predicciones no tan acertadas.

### Implementación en la Nube
Para poner en funcionamiento la API que hemos desarrollado, optamos por la plataforma Render.Una vez que hemos completado y probado nuestra API localmente, Render nos brinda la capacidad de llevarla a la web de manera sencilla y automatizada. Esto simplifica significativamente el proceso de poner nuestra aplicación en línea y asegura una implementación rápida y confiable.
Se deja a continuacion el link para ingresar a ["Render"](https://p1-mlops-deploy.onrender.com)

## Conclusión

Este proyecto integral de MLOps tiene como objetivo transformar datos de juegos en bruto en un sistema funcional de recomendación desplegado como una API RESTful. La optimización del espacio mediante DataFrames es una estrategia clave para mejorar el rendimiento de las funciones al igual que utilizar el muestreo en el modelo de recomendacion. Al abordar el proyecto se busca proporcionar información valiosa y recomendaciones a los usuarios de Steam acerca de los juegos presentes en la plataforma.

## Tecnologías Utilizadas

* Python: Utilizamos el lenguaje de programación Python para la implementación de la lógica del proyecto.

* Pandas y NumPy: Estas bibliotecas de Python fueron esenciales para la manipulación eficiente y el análisis de datos.

* Data Wrangler (Preview): una extencion de Vsc(Visual studio code) la cual permite realizar un analisis rapido y completo de los df.

* FastAPI: Para exponer nuestros datos al mundo, optamos por FastAPI, un marco moderno y rápido para la construcción de APIs en Python.

* Cosine Similarity (Scikit-learn): Implementamos la similitud del coseno utilizando Scikit-learn para construir un sistema de recomendación basado en ítems.

* Render: Para la implementación en la nube y el despliegue automático desde GitHub, seleccionamos Render como plataforma de elección.

* Análisis de Sentimientos con NLP: Aplicamos técnicas de Procesamiento del Lenguaje Natural (NLP) para realizar análisis de sentimientos en las reseñas de usuarios y asignar etiquetas correspondientes.


## Etapas del proyecto

1) Descarga de archivos y revisión:
Comencé descargando los archivos relevantes y los examiné para entender su estructura y contenido.
2) Planificación y dirección:
Después de revisar los archivos, identifiqué la dirección a seguir y planifiqué los siguientes pasos.
3) ETL (Extracción, Transformación y Carga):
Realicé el proceso de ETL para limpiar y transformar los datos contenidos en los archivos.
4) Guardado de archivos limpios:
Conservé una copia de los archivos procesados y limpios, incluyendo todas las transformaciones realizadas.
5) Análisis exploratorio de datos (EDA):
Realicé un análisis exploratorio para comprender qué datos eran relevantes y cuáles podrían descartarse.
6) Feature Engineering (ingeniería de características):
Generé nuevas características a partir de los datos existentes y creé archivos específicos (dataframes) para reducir la carga durante el despliegue.
7) Modelo de sistemas de recomendación:
Implementé un modelo de recomendación basado en la similitud del coseno. Este modelo se utilizó para recomendaciones item-item, específicamente para juegos similares.
8) Pruebas de funciones:
Realicé pruebas exhaustivas de las funciones que se mostrarán en el despliegue para asegurarme de que todo funcione correctamente.
9) Preparación para el despliegue:
Redacté el archivo principal (que se utilizará para las funciones) y un Dockerfile (que contiene los requisitos de instalación). Es importante tener en cuenta que sin el archivo Dockerfile, no se puede realizar el despliegue.
10) Optimización y copia de archivos esenciales:
Al finalizar el proyecto, creé una copia que incluye solo los archivos indispensables para agilizar el proceso y reducir el tiempo necesario para agilizar el despliegue.

A continuacion se deja un video explicativo del proyecto [Enlace_del_video](https://drive.google.com/drive/folders/1Ql37e-klQp05BZ4eNy_tKHf0MkETuJHy?usp=drive_link)

Enlace a la Api [API](https://pl-ml-ops-deploy.onrender.com/)


## Puntos a mejorar 

#### punto 1
Como punto a mejora creo que tendria que realizar un eda mas completo y mas organizado

#### punto 2
el archivo [feature_eng](jupyter_nooteboks/01_feature_eng.ipynb) se volveria a realizar, buscando en todo momento de mantener el orden y las buenas practicas.

#### punto 3
el deploy se podria buscar realizar por otros medios el cual no tenga las limitaciones como render, tratando de buscar vias accecibles para su deployage.

#### punto 4
Otro punto a tener en cuenta hubiera sido la realizacion de las funciones en otro archivo e importarlas al main, esto supondria una mejora en la legibilidad de los archivos y una mejor base para editar en futuras etapas el proyecto.

#### punto 5
Un proceso de EDA y extraccion/transformacion mas limpio y ordenado, hubiera resultado en mejores de legibilidad de codigo asi tambien como entendimiento del mismo.


## Como realizar un deploy por Render

lo primero y principal es acceder a la pagina de render, [RENDER](https://dashboard.render.com/).

Una vez en la pagina 
![pagina_principal](img/imagen5.png)

se va a la pesataña de dashboard y ahi se selecciona service webs
una vez dentro de la misma enlazamos nuestra cuenta de github la cual tenga el repositorio a deployar

![logeado](img/imagen6.png)

una vez seleccionado el repositorio (el boton conectar) nos aparecera una pagina antes de poder deployar, seleccionas el boton cotinuar y despues seleccionas deploy.

siguiendo estos pasos deberias poder deployar tu api en render(aclaracion: utilizando fastapi en tu main) sin ningun problema.

una vez deployada se veria asi:
![deploy](img/imgane7.png)

<br><br><br><br><br>

### Muchas gracias por su tiempo, estoy abierto a opiniones o mejoras que sean propuestas para el proyecto