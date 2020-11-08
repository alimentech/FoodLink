# FoodLink
Repositorio con recursos y código para la aplicación Foodlink desarrollada por Alimentech

Foodlink es una aplicación que busca contribuir a la solución del problema de desperdicio de comida.
A través de esta app, los usuarios pueden observar directamente las fechas de caducidad de cada alimento que compraron en el supermercado. La app manda alertas al usuario cuando sus productos están próximos a caducarse para que el usuario los consuma antes de que el alimento se caduque y, consecuentemente, se desperdicie.
El usuario marca en la aplicación cuando ya consumió un alimento antes de que se caduque y, al hacer esto, recibe una recompensa de puntos que se pueden utilizar para hacer compras en el supermercado.
La aplicación también recolecta información sobre las compras del usuario, para poder predecir compras futuras y que el usuario reciba ofertas y recomendaciones personalizadas sobre los productos que más consume.

## Pasos que seguimos para crear Foodlink

### 1. Creación de base de datos de prueba en Access
1. Crear una base de datos nueva en Access y llenarla con datos como en el siguiente archivo:

[Base de datos de Alimentech](https://github.com/alimentech/FoodLink/blob/main/Base%20de%20datos%20AlimenTech.accdb)

### 2. Creación de recursos Azure SQL Server y Azure SQL Database
1. Ir a [Azure Portal](https://portal.azure.com)
2. Crear recurso de SQL Database. Llenamos los datos solicitados de la siguiente manera:
* Suscripción: Azure para estudiantes
* Grupo de recursos: alimentech-rg (nuevo)
* Nombre: AlimentechDB
* Servidor: Crear nuevo:
  * Nombre: alimentechsql
  * (Se agregan credenciales de cuenta de inicio de sesión y contraseña)
  * Ubicación: Centro-Sur de EE.UU.
* Proceso y Almacenamiento: Básico
3. Una vez creado el recurso, ir a este y seleccionar la opción "Establecer el Firewall del Servidor"
4. Al Agregar IP del cliente se agrega automáticamente la dirección IP del usuario. De esta manera, se podrá ingresar a la base de datos creada con las credenciales establecidas al crear el servidor de SQL.

### 3. Migración de base de datos de Access a Azure SQL Server
1. Descargar SQL Migration Assistant for Access, installar y abrir el programa
2. Crear un nuevo proyecto de migración
3. Añadir base de datos creada en el punto 1. Creación de base de datos de prueba en Access.
4. Conectar a SQL Server insertando los datos del nombre del servidor (alimentechsql.database.windows.net) base de datos (AlimentechDB) y credenciales de inicio de sesión y contraseña
5. Seguir instrucciones del asistente para migrar la base de datos
6. Ir a recurso de base de datos (AlimentechDB) en Azure Portal
7. Ir al editor de consultas, iniciar sesión y verificar que todas las tablas y columnas del archivo de Access se hayan migrado exitosamente a la base de datos.

### 4. Escribir Consulta (Query) para obtener fecha de caducidad, productos comprados, cantidad y fecha de compra.
1. Escribir consulta utilizando INNER JOIN:
```
SELECT [Product], [OrderDate], [AlertDaysBeforeExp]
FROM [dbo].[Orders] INNER JOIN [dbo].[Category]
    ON ([dbo].[Orders].[CategoryID] = [dbo].[Category].[CategoryID])
GO
```
2. Ir a recurso de base de datos (AlimentechDB) en Azure Portal
3. Ir al editor de consultas, iniciar sesión e insertar consulta anterior.
4. Ejecutar consulta y verificar en los resultados que estén los datos que solicitamos (producto, fecha de compra, días para expiración)
5. Guardar consulta en archivo .sql

Esta consulta nos servirá para obtener los datos que mostraremos a los usuarios en la aplicación.

### 5. Predicción de compras del cliente con Machine Learning Studio
1. Ir a [Azure Machine Learning Studio](https://studio.azureml.net/) e iniciar sesión
2. En Proyects crear un nuevo proyecto con el nombre "Predicciones de compras Alimentech" y descripción "Proyecto de Machine Learning para predecir los productos que comprarán los clientes en el supermercado".
3. Ir a experiments y crear un experimento nuevo.
4. Abrir el menú de Data Input and Output y arrastrar Import Data al área de trabajo. Llenar el menú de la izquierda con las siguientes opciones:
* Data Source: Azure SQL Database
* Database Server name: alimentechsql.database.windows.net
* Database name: AlimentechDB
* (Llenar username y password con las credenciales de la base de datos)
* Database Query:
```
SELECT Product, ClientID FROM [dbo].[Orders]
```
5. Abrir el menú de Data Transformations, Sample and Split y arrastrar Split Data al área de trabajo.
6. Conectar Input Data con Split Data
7. Abrir el menú de Machine Learning, Initialize Model, Regression y arrastrar Linear Regression al área de trabajo.
8. En el menú de Machine Learning, abrir Train y arrastrar Train Model al área de trabajo.
9. Conectar Split Data y Linear Regression a Train Model.
10. En el menú de Machine Learning, abrir Score y arrastrar Score Model al área de trabajo.
11. Conectar Split Data y Train Model a Score Model.
12. En el menú de Machine Learning, abrir Evaluate y arrastrar Evaluate Model al área de trabajo.
13. Conectar Score Model a Evaluate Model.
14. Correr modelo
15. En Set up web service, seleccionar Predictive Web Service
16. Correr modelo
17. Seleccionar la opción Deploy web service
18. Ir a Web services y seleccionar el modelo de predicción.
19. Hacer click en Test y llenar datos para predecir.
20. Se devuelve un archivo JSON con la evaluación y puntuación de la predicción.
21. Guardar clave API del servicio para usar en aplicación

El URL para utilizar nuestro modelo de predicción de Machine Learning Studio es: [https://ussouthcentral.services.azureml.net/workspaces/693dc0cde7d245cb8e587c26f5163f41/services/61d04666fb3d4f9ca86bcbd23eb1317d/execute?api-version=2.0&details=true](https://ussouthcentral.services.azureml.net/workspaces/693dc0cde7d245cb8e587c26f5163f41/services/61d04666fb3d4f9ca86bcbd23eb1317d/execute?api-version=2.0&details=true)

### 6. Creación de App Móvil con AppHive
1. Ir al sitio web de [AppHive](https://apphive.io/es) e iniciar sesión
2. Crear un nuevo proyecto y una nueva aplicación.
3. Importar base de datos.
4. Añadir pantallas y funciones.

## Demo de App Móvil

[link de la aplicación]
