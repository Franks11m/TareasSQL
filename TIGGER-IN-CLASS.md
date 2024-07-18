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
1.- REALIZAR UN TIGGER DESPUES DE ISTERTAR UN PACIENTE INSERTE EL USERS
1.1- 
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





