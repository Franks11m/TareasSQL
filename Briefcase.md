# · DDL
## TEORIA
DDL (Data Definition Language) es un subconjunto de SQL que se utiliza para definir y gestionar la estructura de las bases de datos. Los comandos DDL permiten crear, modificar y eliminar estructuras de datos como bases de datos, tablas, índices y vistas.

### 1. Comandos Principales:
1.1- CREATE: Se utiliza para crear objetos en la base de datos, como tablas, vistas, índices, etc.

1.2- ALTER: Se utiliza para modificar una estructura existente en la base de datos.

1.3- DROP: Se utiliza para eliminar objetos de la base de datos.

1.4- TRUNCATE: Se utiliza para eliminar todos los registros de una tabla sin eliminar la tabla en sí.

1.5- COMMENT: Se utiliza para agregar comentarios a los objetos de la base de datos.

### 2. Tipo de Datos:
 Al definir las columnas de una tabla, es crucial especificar el tipo de datos (VARCHAR, INT, DATE, etc.). Esto asegura que los datos almacenados sean del tipo correcto.
### 3. Restricciones:
##### Son usadas para garantizar la integridad de los datos.
3.1- PRIMARY KEY: Un identificador único para cada fila.

3.2- FOREIGN KEY: Garantiza que el valor de una columna en una tabla exista en una columna de otra tabla.  

3.3- UNIQUE: Garantiza que todos los valores de una columna sean únicos.

3.4- NOT NULL: Asegura que una columna no tenga valores nulos.

3.5- CHECK: Impone una condición sobre los valores en una columna.

## Ejemplo Práctico
+ Creamos tabla "libros":
 ```
CREATE TABLE libros (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    autor VARCHAR(255),
    fecha_publicacion DATE,
    precio DECIMAL(10, 2) CHECK (precio > 0)
);

 ```
+  Añadir una columna a la tabla "libros":
 ```
ALTER TABLE libros
ADD COLUMN genero VARCHAR(100);
 ```
+ Eliminamos tabla "libros":
 ```
DROP TABLE libros;
 ```


# · DML
## TEORIA
DML (Data Manipulation Language) es un subconjunto de SQL que se utiliza para gestionar y manipular los datos almacenados en las estructuras de la base de datos. Los comandos DML permiten insertar, actualizar, eliminar y recuperar datos de las tablas.

## 1. Comandos Principales
1.1- INSERT: Se utiliza para insertar nuevos registros en una tabla.

1.2- UPDATE: Se utiliza para modificar registros existentes en una tabla.

1.3- DELETE: Se utiliza para eliminar registros de una tabla.

1.4- SELECT: Se utiliza para recuperar datos de una o más tablas.

## 2. Conceptos Importantes
2.1- Condiciones (WHERE): filtra datos en una tabla
 ```
SELECT * FROM empleados WHERE puesto = 'Desarrollador';
 ```
2.2- Operadores: '=', '>','<', '>=', '<=', '<>', AND, OR y LIKE
 ```
SELECT * FROM empleados WHERE salario > 40000 AND puesto = 'Desarrollador';
 ```
2.3- Funciones Agregadas: 'COUNT', 'SUM', 'AVG', 'MIN' y 'MAX' se utilizan para realizar cálculos sobre un conjunto de registros.
 ```
SELECT AVG(salario) FROM empleados;
 ```
2.4- Agrupación (GROUP BY): Agrupa los registros que tienen los mismos valores en las columnas especificadas y luego realizar cálculos agregados sobre cada grupo.
 ```
SELECT puesto, AVG(salario) 
FROM empleados 
GROUP BY puesto;
 ```
2.5- Ordenación (ORDER BY): Ordena los resultados de una consulta en orden ascendente o descendente.
 ```
SELECT nombre, salario 
FROM empleados 
ORDER BY salario DESC;
 ```
2.6- Agregación de conjuntos de datos para consulta: JOIN, UNION
##### JOIN:
  ###### Un JOIN en SQL se utiliza para combinar registros de dos o más tablas en una base de datos.
+ INNER JOIN: Combina filas con coincidencias en ambas tablas.
+ LEFT JOIN: Devuelve todas las filas de la tabla izquierda, con coincidencias de la tabla derecha.
+ RIGHT JOIN: Devuelve todas las filas de la tabla derecha, con coincidencias de la tabla izquierda.
+ FULL JOIN: Devuelve todas las filas cuando hay una coincidencia en una de las tablas.
+ CROSS JOIN: Devuelve el producto cartesiano de las dos tablas.
##### UNION:
 ###### Se utiliza para combinar los resultados de dos o más consultas SELECT en un solo conjunto de resultados.
+ UNION combina resultados de múltiples consultas SELECT y elimina duplicados.
+ UNION ALL combina resultados y incluye duplicados.
+ Las consultas combinadas deben tener el mismo número de columnas y tipos de datos compatibles.

## Ejemplo Práctico
+ Creamos tabla "empleados":
```
CREATE TABLE empleados (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    puesto VARCHAR(50),
    salario DECIMAL(10, 2)
);
```
+ Insertamos algunos registros:
```
INSERT INTO empleados (nombre, puesto, salario) VALUES ('Ana López', 'Gerente', 75000);
INSERT INTO empleados (nombre, puesto, salario) VALUES ('Carlos Gómez', 'Desarrollador', 50000);
INSERT INTO empleados (nombre, puesto, salario) VALUES ('Laura Martínez', 'Analista', 60000);
```
+ Actualizamos el salario de un empleado:
```
UPDATE empleados SET salario = 55000 WHERE nombre = 'Carlos Gómez';
```
+ Eliminamos un registro:
```
DELETE FROM empleados WHERE nombre = 'Laura Martínez';
```
+ Seleccionamos los empleados con un salario mayor a 50000:
```
SELECT nombre, puesto, salario FROM empleados WHERE salario > 50000;
```
# · PROGRAMACIÓN DE BASES DE DATOS
## TEORIA
## 1. Subconsultas
Una subconsulta es una consulta anidada dentro de otra consulta; estas permiten ejecutar una consulta dentro de otra para filtrar datos, calcular valores o hacer comparaciones.

1.1- Dentro de la instancia "invoince" se realizan los siguientes consulta:
###### Contar el numero de facturas de un cliente:
##### CODE:
```
SELECT COUNT(*)
FROM invoice 
WHERE client_id= 1
```
##### CAPTURA:
<img src="Img/Captura de pantalla 2024-07-25 123947.png" alt="drawing" width="500"/>

## 2. Vistas
Consultas almacenadas que actúan como tablas virtuales, simplificando consultas y mejorando la seguridad.

1.1- Mostrar Vista en tala "cliente-invoice" de la instancia "invoice"

###### 1. Verificamos nuestra tabla invoice y client funcionen
##### CODE:
 ```
SELECT i.id, i.code, i.create_at,i.total,c.full_name
FROM invoice i JOIN client c
  ON c.id=i.client_id;
 ```
##### CAPTURA:
<img src="Img/Captura de pantalla 2024-06-28 170351.png" alt="drawing" width="500"/>

###### 2. Crear la tabla adicional "VIEW"
##### CODE:
 ```
CREATE VIEW invoice_view AS
SELECT i.id, i.code, i.create_at,i.total,c.full_name
FROM invoice i JOIN client c
  ON c.id=i.client_id;
 ```
###### 3. Mostrar la tabla nueva 
##### CODE:
 ```
SELECT * FROM invoice_view;
 ```
##### CAPTURA:
<img src="Img/Captura de pantalla 2024-06-28 172619.png" alt="drawing" width="500"/>

## 3. Funciones y Procedimientos Almacenados:
Bloques de código que realizan múltiples operaciones y no necesariamente devuelven un valor.
### 3.1 Funciones
Son bloques de código que realizan una tarea específica y devuelven un valor
##### Ejemplo:
 ```
CREATE FUNCTION obtener_salario_promedio() RETURNS DECIMAL AS $$
BEGIN
    RETURN (SELECT AVG(salario) FROM empleados);
END;
$$ LANGUAGE plpgsql;

-- Usar la función
SELECT obtener_salario_promedio();
 ```
### 3.2 Procedimientos almacenados
Son similares a las funciones, pero pueden realizar múltiples operaciones (como insertar, actualizar, eliminar datos) y no necesariamente devuelven un valor.
##### Ejemplo:
 ```
CREATE PROCEDURE actualizar_salario(id_empleado INT, nuevo_salario DECIMAL)
LANGUAGE plpgsql
AS $$
BEGIN
    UPDATE empleados
    SET salario = nuevo_salario
    WHERE id = id_empleado;
END;
$$;

-- Ejecutar el procedimiento
CALL actualizar_salario(1, 52000);
CREATE FUNCTION obtener_salario_promedio() RETURNS DECIMAL AS $$
BEGIN
    RETURN (SELECT AVG(salario) FROM empleados);
END;
$$ LANGUAGE plpgsql;

-- Usar la función
SELECT obtener_salario_promedio();
 ```

## 3. Disparadores (Triggers)
Bloques de código que se ejecutan automáticamente en respuesta a eventos en una tabla para aplicar reglas de negocio o validar datos.
### Ejemplo practico
###### CREAR NUEVA INSTANCIA
Name-Instance: pacienteDB
###### CREAR DOS TABLAS 
- 1.Table: Paciente
- 2.Table: Users
##### TABLE PACIENTE
###### CODE:
```
CREATE TABLE Paciente (
    id SERIAL PRIMARY KEY,
    fullname VARCHAR(255) NOT NULL,
    address VARCHAR(255),
    phone VARCHAR(20),
    blood_type VARCHAR(3),
    email VARCHAR(255) UNIQUE
);
```
##### TABLE USERS
###### CODE:
```
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    status BOOLEAN DEFAULT TRUE
);
```
##### PROBLEMA
##### 1.- REALIZAR UN TIGGER QUE DESPUES DE ISTERTAR UN PACIENTE ESTE DEBE INSERTE EL USERS.

##### 1.1- Creamos la función del TIGGER o DISPARADOR que cumpla lo solicitado:
###### CODE:
```
CREATE OR REPLACE FUNCTION after_insert_paciente()
RETURNS TRIGGER AS $$
BEGIN
    -- Insertar un nuevo usuario en la tabla Users
    INSERT INTO Users (username, password)
    VALUES (NEW.fullname, 'default_password');
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
##### 1.2- Ejecutamos el tigger:
###### CODE:
```
CREATE TRIGGER after_insert_paciente_trigger
AFTER INSERT ON Paciente
FOR EACH ROW
EXECUTE FUNCTION after_insert_paciente();
```
##### 1.3- Validamos su funcionamiento insertando datos a la tabla "paciente":

##### 1.3.1- Insertamos el paciente "Yuliana" con su respectiva información:

###### CODE:
```
INSERT INTO Paciente (fullname, address, phone, blood_type, email)
VALUES ('Yuliana Cardenas', 'Barrio las Peñas', '096-770-8703', 'A+', 'yuli123@hotmail.com');
```
###### CAPTURA:

<img src = "Img/Captura de pantalla 2024-07-25 105748.png" width = "500">


##### 1.3.2- Verficamos en la tabla "Users" si creo la paciente "Yuliana":

###### CODE:
```
SELECT * FROM "public"."users" LIMIT 100
```
###### CAPTURA:

<img src = "Img/Captura de pantalla 2024-07-25 105723.png" width = "500">
