# Docker Manual Vídeos
** Joel Helguera Menéndez**

## 01-02-03
**Introdución**
Docker es un proyecto de código abierto formado por contenedores software para el aprendizaje de creación y administración de bases de datos.

Estos vídeos traen unos links con las soluciones y los comandos para ir siguiendo las clases.

## 04-05-06
**Conceptos**
¿Ques es una base de datos?
 Es un sistema informático, utilizado para organizar y almacenar datos para que puedan ser útiles en un momento superior.

Un sistema de gestión de bases de datos relacionales o RDBMS te las herramientas necesarias para construir una base de datos.
-RDBMS le ayudará a encontrar las columnas que componen cada mesa.
-RDBMS le ayudará a almacenar y organizar sus datos.
-RDBMS tambien protege sus datos estructura, almacena y protege sus datos.

Que RDBMS elegir según tus necesidades 
######· Para un proyecto personal o una pequeña empresa:
Un RDBMS de escritorio 
Microsoft Access
FileMaker
Open Office Base
######· Para empresas grandes y clientes empresariales 
Microsoft SQL Server
Oracle
Postgre SQL
######· Si quieres almacenar en la nube para que sea acesible para todo el mundo
Azure SQL Database 
Amazobn RDS

## 07
Todos los RDBMS operan de un modelo cliente-servidor
Tiene 2 partes 
El servidor que es el que realizar todo el trabajo de gestión de bases de datos relacionales.
El segundo es el cliente es la interfaz que permite a los usuarios permite controlara su funcionamento.
Puede ser por línea de comandos o gráfica.

## 08 
Los contenedores RDBMS son entornos ligeros de tiempo de ejecución que proporcionan a las aplicaciones los archivos, las variables .. que necesitan.

##  09 
**Como Instalar docker**
Ir a docker.com> ir al extremo derecho que pone Get Started y elegir la versión adecuada para ti.
Una vez instaldo buscar instalador en el propio pc y ejecutarlo valores predeterminados reiniciar despues de instalar comprobar funcionamiento.
*Todos los comandos en docker comienzan con la palabra docker delante*
Abre powershell 
`Docker version` Muestra la version instalada
`Docker` lista los comandos de docker

## 10
Comandos en el archivo Docker_Container.txt

######· Microsoft SQL
`docker run --name SQLServer2019 -e "ACCEPT_EULA=Y" -E"SA_PASSWORD=Adam123456" -p 1404:1433 -d mcr.microsoft.com/mssql/server:2019 -latest`

######· Postgre SQL
`docker run --name postgresql -p 5401:5432 -e postgres_PASSWORD=Adam123456 -d postgres:latest`

## 11
**Iniciar sesión en un contenedor MicrosoftSQL**
`docker exec -it sqlserver2019 bash`
*Ahora estas entro del contenedor*
`/opt/mssql-tools/bin/sqlcmd -U sa -P Adam123456`
*Comando iniciar sesión*
Podemos crear una base de datos así:
`CREATE DATABASE mytestdb`
`GO`
`EXIT` para salir
**En Postgresql para iniciar sesion**
`docker exec -it  postgresql bash`
`psql -U postgres`

## 12-13
Objetivo Crear Un Contenedor
**SOLUCIÓN**
Create a new container on a Windows PC:
docker run --name MySecondSQLServer -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Adam123456" -p 1420:1433 -d mcr.microsoft.com/mssql/server:2019-latest

** View all runing containers**
`docker ps`

**Stop a container**
`docker stop MySecondSQLServer`

**View all containers**
`docker ps -a`

** Start a container**
`docker start MySecondSQLServer`

** Remove a container**
`docker rm MySecondSQLServer`

## 14
Explora la distintas interfaces gráficas que hay para docker como  Kilematic, Azure, DockStation...


## 15
Vamos a instalar Azure Data Studio:
Iremos a la página y le daremos a descargar en la opción mas adecuado para tu equipo, una vez instalado vas a tu pc a la carpeta descargas y ejecutar el .exe y seguirás hasta instalarlo.
Nada mas instalado se ejecutará.

## 16-17
Configuración de Azure x Docker
Para usar la terminal con el  **Ctrl + '** 
Presiona el boton azul, empezaremos con MicrosoftSQL , rellena la barra lateral emergente como ditcta en el vídeo.
Para PostgreSQL es el mismo proceso.
Se pueden hacer grupos con las opción Add server group.

## 18
Haz click en la tuerca y vete a settings, en la barra de búsqueda busca **tab color** y ponlo en fill para cambiar los colores de los comandos según el tipo.
Usa **Select From** y ect para consultar en la terminal la información de la tabla que hay intregrada en la base de datos.

## 19-20
Objetivo crear base de datos para una empresa llamada KinetEco y administarla con Azure.
**SOLUCIÓN**
**Create the server container**
Windows PC:
docker run --name kineteco -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Adam123456" -p 1411:1433 -d mcr.microsoft.com/mssql/server:2019-latest

MacOS & Linux:
docker run --name kineteco -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Adam123456' -p 1411:1433 -d mcr.microsoft.com/mssql/server:2019-latest


**Connect in Azure Data Studio with the following settings**
Connection type: Microsoft SQL Server
Server name: localhost
User name: SA
Password: Adam123456
Remember passowrd: checked
Server group: SQL Server
Name: KinetEco
Advanced - Port: 1411


**Create the database in a new query window**
CREATE DATABASE KinetEco;

## 21
Los comandos se pueden desglosar en 2 grupos diferentes:
DDL (Data Definition Language) > se utilizan para diseñar y construir los componentes de su base de datos.
DML (Data Manupulation Language) > se utilizan para trabajra con el almacenamiento de datos.

## 22
La manera de ilustrar los datos para que sea visual y sencillo puede ser mediante el uso de **Tablas**, **Esquemas** ...

Dentro de **SQL Server 2019 > Databases > Two Trees** , dentro de Two Trees haz click derecho y haz una new query.
*Asegurate de que ponga arriba TwoTrees*
Crea un esquema con los productos de Two Trees:
`CREATE SCHEMA products;`
`DROP SCHEMA products;` para borrar esquema.

Mismo proceso en PostgreSQL.

## 23
Para comenzar con la creación de la tabla tienes que tener en cuenta diversos factores como: 
Fecha, el creador , el objetivo ...

## 24
Abre el archivo de la tabla del video con **EXCEL **o **CALC**
Y mediante el terminal procederemos a crear un tabla con los siguientes comandos especificando todo al detalle:
`CREATE TABLE products.products (
 SKU CHAR(7) NOR NULL PRIMARY KEY,
 ProductName CHAR(50) NOT NULL,
 CategoryID  INT,
 Size INT,
 Price DECIMAL(5,2) NOT NULL
);`
*En POSTGRESQL es exactamente igual*

## 25
Crea una tabla según indica el video con el siguiente comando:

`CREATE TABLE products.categories (
CategoryID INt PRIMARY KEY,
CategoryDescription CHAR(50)
)`

Comando agregar columnas una vez creada la tabla:
`ALTER TABLE products.categories
ADD Productline CHAR(25);`

## 26
Identificador " "
Se usa para nombrar nombres de columnas, tablas...

## 27-28
Objetivo:
Continuar la base de datos KinetEco añadiendo un esquema llamado HumanResources, añade la table for Employees, incluye columnas.
**SOLUCIÓN**
**Create a schema and table for the KinetEco database**

CREATE SCHEMA HumanResources;

`CREATE TABLE HumanResources.Employees (
    EmployeeID INT        NOT NULL   PRIMARY KEY,
    FirstName  CHAR(50)   NOT NULL,
    LastName   CHAR(50)   NOT NULL,
    Department CHAR(20)   NOT NULL,
    HireDate   DATE       NOT NULL
);`

## 29
Las columnas componene atributos de los datos las filas representan elementos individuales.

## 30
Crea una  una nueva consulta dentro de Databases, y lo que vamos hacer va a ser insertarle una fila:
**Agregue datos a una tabla completando todas las columnas en orden**

`INSERT INTO products.products`
`VALUES`
   ` ('FCP008', 'First Cold Press', 1, 8, 8.99);`




INSERT INTO products.products
VALUES
  `  ('BI008', 'Basil-Infused EVO',  2,  8, 10.99),`
 `   ('GI016', 'Garlic-Infused EVO', 2, 16, 15.99);`


Add rows by specifying columns

`INSERT INTO products.products`
  `  (SKU, ProductName, Price)`
`VALUES`
`    ('OGEC004', 'Olive Glow Eye Cream', 18.99);`

## 31
Comandos que usaremos para actualizar y borrar columnas:

**Cambiar los valores en una fila específica**

`UPDATE products.products`
`SET`
    `CategoryID = 3,`
    `Size       = 4`
`WHERE SKU = 'OGEC004';`


**Eliminar una fila específica de la base de datos**

`DELETE FROM products.products`
`WHERE SKU = 'OGEC004';`

## 32
Para guardar nuestra línea de comandos harás click en la X de salir y saldrás dandole a SAVE  y guarda la línea de comandos en un sitio facíl para ti.
Para abrir de nuevo la línea de comando solo tienes que ir a FILE  y OPEN FILE abriendo el archivo previamente guardado para seguir trabajando.

## 33-34
Añadir a la bases de datos KinetEco a la Employees table, añadir la data table, añadir fecha,día y mes.
**SOLUCIÓN**
**Agregar 3 nuevos empleados**
`INSERT INTO HumanResources.Employees`
    `(EmployeeID, FirstName, LastName, Department, HireDate)`
`VALUES`
    `(101, 'Robert', 'Boyle', 'Chemistry', '20200325'),`
    `(102, 'Marie',  'Curie', 'Chemistry', '20200825'),`
    `(103, 'Niels',  'Bohr',  'Physics',   '20200923');`


**Modificar el departamento de un empleado**
`UPDATE HumanResources.Employees`
`SET Department = 'Physics'`
`WHERE EmployeeID = 102;`

**Eliminar el registro de un empleado**
`DELETE FROM HumanResources.Employees`
`WHERE EmployeeID = 101;`

## 35
Para hacer consultas básicas a nuestra bases usaremos lenguaje SQL y utilizaremos comandos básicos como SELECT, FROM Y WHERE.

## 36
**Eliminar todas las filas de la tabla de productos**
DELETE FROM products.products;

**Agregar todos los datos de productos nuevos**
INSERT INTO products.products
    (SKU, ProductName, CategoryID, Size, Price)
Usa los comandos que dicta el vídeo y que estan en los bloq de notas de ayuda.

## 37-38-39-40
En estos videos filtraremos usando lenguaje SQL  server.
Aprenderemos desde consultas fáciles a otro nivel más complejo.
Las consultas están en los bloq de notas de ayuda.
Mostraré aquí las mas sencillas:
__________________________________________________________________________________________________________
-- View related data in two tables
SELECT * FROM products.products
WHERE SKU = 'ALB008';

SELECT * FROM products.categories
WHERE CategoryID = 1;

-- Join columns together in a single query
SELECT products.ProductName,
    products.CategoryID,
    products.SKU,
    products.Price,
    categories.ProductLine
FROM products.products
    JOIN products.categories
        ON products.CategoryID = categories.CategoryID
WHERE SKU = 'ALB008';

_______________________________________________
-- Retrieving only a specific number of rows
-- SQL Server uses the TOP keyword
SELECT TOP 5 *
FROM products.products
ORDER BY Price DESC;


-- PostgreSQL uses the LIMIT clause
SELECT *
FROM products.products
ORDER BY Price DESC
LIMIT 5;
_______________________

## 41-42-43-44-45
Seguimos filtrando usando en las consultas lenguaje SQL, en estos videos se explicará como el having, group by ...
Recuerda que las consultas usadas en este vídeo las pone en el bloq de notas de ayuda.

· La cláusula GROUP BY es un comando SQL que se usa para agrupar filas que tienen los mismos valores . La cláusula GROUP BY se utiliza en la instrucción SELECT. Opcionalmente se usa junto con funciones agregadas para producir informes resumidos de la base de datos.
· Así como la cláusula "where" permite seleccionar (o rechazar) registros individuales; la cláusula "having" permite seleccionar (o rechazar) un grupo de registros. ... Se utiliza "having", seguido de la condición de búsqueda, para seleccionar ciertas filas retornadas por la cláusula "group by"

## 46-47
Objetivo: Consultar una base de datos.
Responde preguntas como:
¿Cuáles son los tamaños en militros?, 
¿cuáles SKUS de productos diferentes hay disponibles en cada tamaño?, 
¿cuál es el producto de mayor precio en la línea de productos cosméticos?
**SOLUCIÓN**
__________
-- Q1: convert size from oz to ml
SELECT SKU, ProductName,
    Size AS "Size (Ounces)",
    Size * 29.57353 AS "Size (Milliliters)"
FROM products.products;

-- Q2: how many products are in each size
SELECT
    Size AS "Size (Ounces)",
    COUNT(SKU) AS "Number of Products"
FROM products.products
GROUP BY Size;

-- Q3: Highest priced product in cosmetic product line
SELECT MAX(Price)
FROM products.products
WHERE CategoryID = 3

SELECT SKU, ProductName, CategoryID, Size, Price
FROM products.products
WHERE PRICE =
    (SELECT MAX(Price)
     FROM products.products
     WHERE CategoryID = 3)
    AND CategoryID = 3
____________________________________________________
## 48
Felicidades has termiando el Curso de SQL.
