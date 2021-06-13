# Web scraping de portales de empleo

Este es un proyecto útil para la captura y almacenamiento de datos de cuatro portales de empleo en el Ecuador, que requieren la elaboración de un método específico para cada uno. 
Por lo que, se lo incluye en un fichero con su nombre a continuación:

- [SocioEmpleo](SocioEmpleo.ipynb)
- [AccionTrabajo](AccionTrabajo.ipynb)
- [TuPortalEmpleo](TuPortalEmpleo.ipynb)
- [Mipleo](Mipleo.ipynb)

## Requisitos

Las herramientas de software instaladas y los requerimientos para su ejecución en un equipo local son:

- Anaconda3 2020.02 (Python 3.7.6) - [sitio oficial](https://www.anaconda.com/products/individual)
  
  Desde Anaconda Navigator crear un entorno virtual para este proyecto y seleccionarlo.
  
  Instalar la versión disponible de Jupyter Notebook.
  
- NoSqlBooster for MongoDB 5.2.12 - [sitio oficial](https://nosqlbooster.com/downloads)
  
  Crear una base de datos de nombre _alldata_ con una colección para cada portal: socioempleo, aciontrabajo, tuportalempleo y mipleo.

- Webdriver for Chrome stable release - [sitio oficial](https://chromedriver.chromium.org/)
  
  Descargar la herramienta, descomprimirla y guardarla en una ubicación de su preferencia para un posterior uso.

## Librerías

La interfaz de Anaconda Navigator facilita la instalación de las librerías necesarias para el web scraping en el entorno virtual, que son:

- Time
- Pandas
- Selenium
- PyMongo

## Procedimiento

Cumplir con los requisitos e instalar las librerías permite ejecutar el código generado a través de la Jupyter Notebook de Anaconda Navigator.
Se realiza un procedimiento individual en cada fichero de acuerdo a su portal de empleo, no obstante comparten la siguiente estructura:

1. Importar librerías instaladas
```
  import time
  import pandas as pd
  from selenium import webdriver
  from pymongo import MongoClient
```
2. Asignar la url del portal de empleo
```
  url = "http://www.portaldeempleo.com"
```
3. Conectar con MongoDb
```
  Client = MongoClient('localhost',27017)
```
4. Listar las bases de datos de MongoDb
```
  Client.list_database_names()
```
5. Seleccionar la base de datos alldata
```
  db = Client.alldata
```
6. Listar las colecciones de la base de datos
```
  colecciones = db.list_collection_names()
  colecciones
```
7. Seleccionar la coleccion creada para el portal de empleo
```
  collection = db["portalempleo"]
```
8. Crear el método

   El método realizado en cada portal de empleo depende de la estructura y componentes de su página, es por ello que se realiza uno diferente en cada sitio.
   Además es muy importante tener en cuenta que si el sitio web es modificado, el método puede requerir cambios o quedar obsoleto.
   
   El código elaborado en cada método permite extraer los datos del anuncio para almacenarlo en la base de datos y colección de mongodb.

9. Invocar al web driver desde su ubicacion en el equipo
```
  driver = webdriver.Chrome(executable_path='C:/../chromedriver.exe')
```
10. Acceder a la url
```
  driver.get(url)
```
11. Ejecutar el método 
```
  obtener_empleos(driver)
```
