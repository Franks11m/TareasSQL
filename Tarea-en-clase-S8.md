# Tarea en clase de la semana 8 
## 1. Listar productos que no muestren pais de origen
  - Sentencia:
  ```
SELECT COUNT(*) - COUNT (country_of_origin) AS "productos-sin pais"
FROM product;
  ```
  - Captura:

<img src="./Captura/Captura de pantalla 2024-05-30 154858.png" alt="drawing" width="500"/>

## 2. Numero de cliente por ciudad
### Utilizamos la palabra "DISTINCT"
  - Sentencia:
  ```
SELECT DISTINCT city
FROM client;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-05-30 162429.png" alt="drawing" width="500"/>
