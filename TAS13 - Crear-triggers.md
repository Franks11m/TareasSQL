# Trabajo de la semana 13

## Actividad

### Crear triggers

### DB Invoice

1.- Crear una función y un trigger para validar que el numero de cedula del cliente tenga 10 números (no letras) en la tabla cliente:

 1.1.- Crear la función para validar el número de cédula:
```
CREATE OR REPLACE FUNCTION validate_nui() RETURNS TRIGGER AS $$
BEGIN
    IF NEW.nui !~ '^\d{10}$' THEN
        RAISE EXCEPTION 'El número de cédula debe tener 10 números';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

```
1.2- Crear el trigger que utilice la función de validación:

```
CREATE TRIGGER validate_nui_trigger
BEFORE INSERT OR UPDATE ON public.client
FOR EACH ROW EXECUTE FUNCTION validate_nui();

```
#### Comprobar tigger:
```
CREATE TRIGGER validate_nui_trigger
BEFORE INSERT OR UPDATE ON public.client
FOR EACH ROW EXECUTE FUNCTION validate_nui();

```
<img src = "carpetas/triggers/Captura 3.png" width = "500">

1.3- Probar tigger al momento de Insertar datos.
#### Intento de inserción con un número de cédula inválido:
```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('12345', 'Gabriel Gonzalez', 'Ricaute', 'Gabod@hotmail.com');

```
<img src = "carpetas/triggers/Captura 3.png" width = "500">

#### Intento de inserción con un número de cédula válido:

```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('0734567890', 'Franks Gonzalez', 'Sinincay', 'Franks@hotmail.com');

```
<img src = "carpetas/triggers/Captura 3.png" width = "500">

2.- Crear un función y un trigger para que cada vez que se inserte un nuevo registro en la tabla item se disminuya el stock de la tabla product.

Función para actualizar el stock:

```
CREATE OR REPLACE FUNCTION update_stock_on_item_insert()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE productos
  SET cantidad_en_stock = cantidad_en_stock - NEW.quantity
  WHERE id = NEW.product_id;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
<img src = "carpetas/triggers/Captura 4.png" width = "500">

Trigger para actualizar el stock después de INSERT en la tabla item:

```
CREATE TRIGGER update_stock_after_item_insert
AFTER INSERT ON item
FOR EACH ROW
EXECUTE PROCEDURE update_stock_on_item_insert();
```
<img src = "carpetas/triggers/Captura 5.png" width = "500">

verificar si el trigger ya existe en la base de datos ejecutando la siguiente consulta:

```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'update_stock_after_item_insert'
  AND event_object_table = 'item';
```
<img src = "carpetas/triggers/Captura  6.png" width = "500">

3.- Crear un función y un trigger para la tabla invoice donde valide que el campo create_at sea del año actual (fecha sistema).

Función para validar la fecha:

```
CREATE OR REPLACE FUNCTION validate_invoice_create_date()
RETURNS TRIGGER AS $$
BEGIN
  IF EXTRACT(YEAR FROM NEW.create_at) <> EXTRACT(YEAR FROM CURRENT_DATE) THEN
    RAISE EXCEPTION 'La fecha de creación debe ser del año actual.';
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
<img src = "carpetas/triggers/Captura  7.png" width = "500">

Creación del Trigger


```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'validate_invoice_create_date_before_insert'
  AND event_object_table = 'invoice';
```
<img src = "carpetas/triggers/Captura 8.png" width = "500">

4.- Crear un función y un trigger para la tabla client y validar que el correo tenga un @.

Función para validar el correo:

```
CREATE OR REPLACE FUNCTION validate_email_format()
RETURNS TRIGGER AS $$
BEGIN
  IF NEW.email !~ '@' THEN
    RAISE EXCEPTION 'El correo electrónico debe contener "@".';
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
<img src = "carpetas/triggers/Captura 9.png" width = "500">

Verificar la existencia del trigger consultando la vista information_schema.triggers de la siguiente manera:

```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'validate_email_format_before_insert'
  AND event_object_table = 'clientes';
```
<img src = "carpetas/triggers/Captura 10.png" width = "500">
