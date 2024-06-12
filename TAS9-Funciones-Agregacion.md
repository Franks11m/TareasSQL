# Trabajo Autonomo "Semana 9"
### Funciones de agregacion
## Creacion de tres tablas:
 ```
Tabla members
CREATE TABLE members (
    member_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    birth_date DATE
);

Tabla events
CREATE TABLE events (
    event_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(100),
    event_date DATE
);

Tabla registrations
CREATE TABLE registrations (
    registration_id SERIAL PRIMARY KEY,
    member_id INT REFERENCES members(member_id),
    event_id INT REFERENCES events(event_id)
);
 ```
## Proporcionar informacion o datos a cada tabla:
 ```
Tabla members
INSERT INTO members (name, birth_date) VALUES 
('Alice', '1990-01-15'),
('Bob', '1985-07-23'),
('Charlie', '1992-05-30');

Tabla events
INSERT INTO events (name, city, event_date) VALUES 
('Tech Conference', 'New York', '2023-06-15'),
('Business Summit', 'Chicago', '2023-08-20'),
('Health Expo', 'San Francisco', '2023-09-25');

Tabla registrations
INSERT INTO registrations (member_id, event_id) VALUES 
(1, 1),
(2, 1),
(3, 2),
(1, 3),
(2, 3),
(3, 3);
 ```

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

## 3. obtener el número total de registros asistidos
  - Sentencia:
  ```
SELECT COUNT(*) AS total_registrations
FROM registrations;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-11 221048.png" alt="drawing" width="500"/>

## 4. obtener el número total de asistentes a todas las conferencias

  - Sentencia:
  ```
SELECT COUNT(DISTINCT member_id) AS total_attendees
FROM registrations;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-05-30 162429.png" alt="drawing" width="500"/>
## 5. obtener el número total de eventos por cada ciudad:

  - Sentencia:
  ```
SELECT city, COUNT(*) AS total_events
FROM events
GROUP BY city;

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-11 221048.png" alt="drawing" width="500"/>

## 6. obtener el número de registros por cada miembro:
  - Sentencia:
  ```
SELECT member_id, COUNT(*) AS registrations_count
FROM registrations
GROUP BY member_id;
  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-05-30 162429.png" alt="drawing" width="500"/>

## 7. obtener el número de registros por cada conferencia:
  - Sentencia:
  ```
SELECT event_id, COUNT(*) AS registrations_count
FROM registrations
GROUP BY event_id;
  ```
  - Captura:
<img src="Captura/Captura de pantalla 2024-06-11 221048.png" alt="drawing" width="500"/>


