# CREAR NUEVA INSTANCIA
Name-Instance: pacienteDB
# CREAR DOS TABLAS 
- 1.Table: Paciente
- 2.Table: Users
# TABLE PACIENTE
## CODE:
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
# TABLE USERS
## CODE:
```
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    status BOOLEAN DEFAULT TRUE
);
```
# PROBLEMA
##### 1.- REALIZAR UN TIGGER QUE DESPUES DE ISTERTAR UN PACIENTE ESTE DEBE INSERTE EL USERS.

#### 1.1- Creamos la función del TIGGER o DISPARADOR que cumpla lo solicitado:
## CODE:
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
#### 1.2- Ejecutamos el tigger:
## CODE:
```
CREATE TRIGGER after_insert_paciente_trigger
AFTER INSERT ON Paciente
FOR EACH ROW
EXECUTE FUNCTION after_insert_paciente();
```
#### 1.3- Validamos su funcionamiento insertando datos a la tabla "paciente":

#### 1.3.1- Insertamos el paciente "Yuliana" con su respectiva información:

## CODE:
```
INSERT INTO Paciente (fullname, address, phone, blood_type, email)
VALUES ('Yuliana Cardenas', 'Barrio las Peñas', '096-770-8703', 'A+', 'yuli123@hotmail.com');
```
## CAPTURA:

<img src = "Img/Captura de pantalla 2024-07-25 105748.png" width = "500">


#### 1.3.2- Verficamos en la tabla "Users" si creo la paciente "Yuliana":

## CODE:
```
SELECT * FROM "public"."users" LIMIT 100
```
## CAPTURA:

<img src = "Img/Captura de pantalla 2024-07-25 105723.png" width = "500">









