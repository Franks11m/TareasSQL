# Trabajo Autonomo "Semana 9"
### Funciones de agregacion
## 1. Obtener la edad promedio de los miembros
  - Sentencia:
  ```
SELECT AVG(EXTRACT(YEAR FROM AGE(birth_date))) AS avg_age
FROM members;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-11 221048.png" alt="drawing" width="500"/>

## 2. Obtener la edad mínima de los miembros
  - Sentencia:
  ```
SELECT MIN(EXTRACT(YEAR FROM AGE(birth_date))) AS min_age
FROM members;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-05-30 162429.png" alt="drawing" width="500"/>
