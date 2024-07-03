# Trabajo en clase de la semana 12

## Uso de "subconsultas" en SQL
### Son consultas SQL que se incrustan dentro de otra consulta; estas sirven para proporcionar resultados intermedios que se utilizan en la consulta principal y se usan para realizar operaciones más complejas y específicas en una base de datos.

# Actividad
## DB INVOICE
### 1. El numero total de facturas realizadas por cada cliente.
- CODE:
 ```
SELECT 
    COUNT(i.client_id)
FROM 
    invoice i
WHERE 
    i.client_id = 1;
 ```
- Captura:
<img src="Img/Captura de pantalla 2024-07-02 200321.png" alt="drawing" width="500"/>

### 2. Listar nombre y correo de los clientes junto a su compra mas cara realizada.
- CODE:
 ```
SELECT 
    c.full_name, 
    c.email, 
    i.total AS compra_mas_cara
FROM 
    client c
JOIN 
    invoice i ON c.id = i.client_id
WHERE 
    i.total = (
        SELECT MAX(i2.total)
        FROM invoice i2
        WHERE i2.client_id = c.id
    );

 ```
- Captura:
<img src="Img/Captura de pantalla 2024-07-02 200607.png" alt="drawing" width="500"/>

### 3. Listar las facturas donde sus totales sean mayores al promedio de las facturas.

- CODE:
 ```
SELECT i.create_at, i.total
From invoice i
WHERE i.total > (SELECT AVG(total) FROM invoice);
 ```
- Captura:
<img src="Img/Captura de pantalla 2024-07-02 200828.png" alt="drawing" width="500"/>

## DB EVENT
### 1. Subconsulta en SELECT: "Contar conferencias asistidas por miembro"
- CODE:
 ```
SELECT 
    m.id,
    m.fullname,
    m.email,
    m.age,
    (SELECT COUNT(*) 
     FROM register r 
     WHERE r.member_id = m.id AND r.assisted = true) AS total_conferences_attended
FROM 
    member m;

 ```
- Captura:
<img src="Img/Captura de pantalla 2024-07-02 202759.png" alt="drawing" width="500"/>

### 2. Subconsulta en WHERE: "Conferencias con asistentes por encima del promedio"
- CODE:
 ```
SELECT 
    c.id,
    c.title,
    c.speaker,
    c.hour,
    c.day,
    c.total_attendees,
    c.event_id
FROM 
    conference c
WHERE 
    c.total_attendees > (SELECT AVG(total_attendees) FROM conference);

 ```
- Captura:
<img src="Img/Captura de pantalla 2024-07-02 202832.png" width="500"/>







  
