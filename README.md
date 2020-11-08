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
1. Ir a [Azure Portal](portal.azure.com)
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

### 4. Escribir Consulta (Query) para obtener fecha de caducidad, productos comprados, cantidad y fecha de compra.
5.

## Demo

[link de la aplicación]
