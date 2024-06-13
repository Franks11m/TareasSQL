# Trabajo Autonomo "Semana 8"
### Sentencias Where multicriterio
## Creacion de dos tablas:
 ```
Tabla client
CREATE TABLE IF NOT EXISTS client (
    id SERIAL PRIMARY KEY, 
    nui VARCHAR(50) NOT NULL,
    full_name VARCHAR(100) NOT NULL,
    phone VARCHAR(15),
    type_of_client VARCHAR(50),
    city VARCHAR(50),
    credit_limit NUMERIC(10, 2)
);

);

Tabla product
CREATE TABLE IF NOT EXISTS product (
    id SERIAL PRIMARY KEY, 
    description VARCHAR(255) NOT NULL,
    price NUMERIC(10, 2) NOT NULL,
    category VARCHAR(100),
    country_of_origin VARCHAR(50),
    year_of_production INT
);
 ```
## Proporcionar informacion o datos a cada tabla:
 ```
Tabla client
INSERT INTO client (nui, full_name, phone, type_of_client, city, credit_limit) VALUES
('1234567890', 'John Doe', '555-1234', 'Regular', 'New York', 5000.00),
('0987654321', 'Jane Smith', '555-5678', 'Premium', 'Los Angeles', 10000.00),
('1122334455', 'Jack Johnson', '555-8765', 'Regular', 'Chicago', 7500.00),
('6677889900', 'Jill Taylor', '555-4321', 'Premium', 'Houston', 15000.00),
('2233445566', 'Jerry Wilson', '555-7890', 'Regular', 'Phoenix', 3000.00);

Tabla product
INSERT INTO product (description, price, category, country_of_origin, year_of_production) VALUES
('Laptop', 1200.00, 'Electronics', 'USA', 2022),
('Smartphone', 800.00, 'Electronics', 'China', 2023),
('Tablet', 300.00, 'Electronics', 'USA', 2022),
('Headphones', 150.00, 'Accessories', 'Germany', 2021),
('Smartwatch', 200.00, 'Accessories', 'China', 2023);
 ```

## 1. Contar el número de productos de una categoría específica.
  - Sentencia:
  ```
SELECT COUNT(*) AS product_count
FROM product
WHERE category = 'Electronics';

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 180920.png" alt="drawing" width="500"/>

## 2. Contar el número de clientes en una ciudad específica.
  - Sentencia:
  ```
SELECT COUNT(*) AS client_count
FROM client
WHERE city = 'New York';

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 180937.png" alt="drawing" width="500"/>

## 3. Contar el número de productos cuyo precio está dentro de un rango específico 
  - Sentencia:
  ```
SELECT COUNT(*) AS product_count
FROM product
WHERE price BETWEEN 100 AND 500;

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 180958.png" alt="drawing" width="500"/>

## 4. Seleccionar clientes que viven en una ciudad específica y tienen un tipo de cliente específico

  - Sentencia:
  ```
SELECT *
FROM client
WHERE city = 'Los Angeles' AND type_of_client = 'Premium';

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 181014.png" alt="drawing" width="500"/>

## 5. Seleccionar productos que pertenecen a una categoría específica y cuyo precio está por encima de un valor específico

  - Sentencia:
  ```
SELECT *
FROM product
WHERE category = 'Electronics' AND price > 500;


  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 181033.png" alt="drawing" width="500"/>

## 6. Seleccionar productos que fueron producidos en un año específico y en un país de origen específico
  - Sentencia:
  ```
SELECT *
FROM product
WHERE year_of_production = 2022 AND country_of_origin = 'USA';

  ```
  - Captura:

<img src="Captura/Captura de pantalla 2024-06-12 181049.png" alt="drawing" width="500"/>

## 7. Seleccionar clientes cuyo nombre completo comience con 'J'.
  - Sentencia:
  ```
SELECT *
FROM client
WHERE full_name LIKE 'J%';

  ```
  - Captura:
<img src="Captura/Captura de pantalla 2024-06-12 181108.png" alt="drawing" width="500"/>

## 8. Seleccionar clientes cuya ciudad contenga la letra 'a'
  - Sentencia:
  ```
SELECT *
FROM client
WHERE city LIKE '%a%';

  ```
  - Captura:
<img src="Captura/Captura de pantalla 2024-06-12 181126.png" alt="drawing" width="500"/>
