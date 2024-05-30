# Tarea en clase de la semana 8
# Escribir una sentencia Listar Productos sin pais de origen 
# Tarea TAS7 - Events
## 1. Listar los asistentes mayores a 30 anos al evento
  - Sentencia:
  ```
SELECT COUNT(*) - COUNT (country_of_origin) AS "productos-sin pais"
FROM product;
  ```
  - Captura:

<img src="./Captura/Captura de pantalla 2024-05-30 154858.png" alt="drawing" width="500"/>

## 2. Numero de cliente por ciudad
Utilizar la palabra "DISTINCT"
  - Sentencia:
  ```
  SELECT city
FROM client;
  ```
  - Captura:

<img src="./capturas/sentence01.png" alt="drawing" width="500"/>
