# Trabajo en clase de la semana 11

## Uso de "VIEW" en SQL
#### Las vistas son una herramienta poderosa en SQL para simplificar el acceso a los datos, mejorar la seguridad y mantener la consistencia de las consultas. Se utilizan para crear tablas virtuales que representan los resultados de consultas SQL.

# Actividad
## Mostrar Vista cliente-invoice
### 1. Verificamos nuestra tabla invoice y client funcionen
- CODE:
 ```
SELECT i.id, i.code, i.create_at,i.total,c.full_name
FROM invoice i JOIN client c
  ON c.id=i.client_id;
 ```
- Captura:
<img src="Captura/Captura de pantalla 2024-06-11 222853.png" alt="drawing" width="500"/>

### 2. Crear la tabla adicional "VIEW"
- CODE:
 ```
CREATE VIEW invoice_view AS
SELECT i.id, i.code, i.create_at,i.total,c.full_name
FROM invoice i JOIN client c
  ON c.id=i.client_id;
 ```
### 3. Mostrar la tabla nueva 

- CODE:
 ```
SELECT * FROM invoice_view;
 ```
- Captura:
<img src="Captura/Captura de pantalla 2024-06-11 222853.png" alt="drawing" width="500"/>

## Mostrar Vista detail-product
### 1. Verificamos nuestra tabla detail y product funcionen
- CODE:
 ```
SELECT d.id, d.quantity, p.description,d.price,d.price*d.quantity AS subtotal
FROM detail d JOIN product p
  ON p.id=d.productid;
 ```
- Captura:
<img src="Captura/Captura de pantalla 2024-06-11 222853.png" alt="drawing" width="500"/>

### 2. Crear la tabla adicional "VIEW"
- CODE:
 ```
CREATE VIEW detail_view AS
SELECT d.id, d.quantity, p.description,d.price,d.price*d.quantity AS subtotal
FROM detail d JOIN product p
  ON p.id=d.productid;

 ```
### 3. Mostrar la tabla nueva 

- CODE:
 ```
SELECT * FROM detail_view;
 ```
- Captura:
<img src="Captura/Captura de pantalla 2024-06-11 222853.png" alt="drawing" width="500"/>







  
