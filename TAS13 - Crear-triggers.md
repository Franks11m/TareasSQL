# Trabajo de la semana 13

## Actividad

### Crear triggers

### DB Invoice

1.- Crear una función y un trigger para validar que el numero de cedula del cliente tenga 10 números (no letras) en la tabla cliente:

 1.1.- Creo la función para validar el número de cédula:
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
1.2- Creo el trigger que utilice la función de validación:

```
CREATE TRIGGER validate_nui_trigger
BEFORE INSERT OR UPDATE ON public.client
FOR EACH ROW EXECUTE FUNCTION validate_nui();

```
#### Compruebo  tigger:
```
CREATE TRIGGER validate_nui_trigger
BEFORE INSERT OR UPDATE ON public.client
FOR EACH ROW EXECUTE FUNCTION validate_nui();

```
<img src = "Img/Captura de pantalla 2024-07-15 010238.png" width = "500">

1.3- Probar tigger al momento de Insertar datos.
#### Intento con número de cédula inválido:
```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('12345', 'Gabriel Gonzalez', 'Ricaute', 'Gabod@hotmail.com');

```
<img src = "Img/Captura de pantalla 2024-07-15 010343.png" width = "500">

#### Intento con un número de cédula válido:

```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('0734567890', 'Franks Gonzalez', 'Sinincay', 'Franks@hotmail.com');

```
<img src = "Img/Captura de pantalla 2024-07-15 010459.png" width = "500">

2.- Crear un función y un trigger para que cada vez que se inserte un nuevo registro en la tabla item se disminuya el stock de la tabla product.

2.1- Creo la función para disminuir el stock:

```
CREATE OR REPLACE FUNCTION decrease_stock() RETURNS TRIGGER AS $$
BEGIN
    UPDATE public.product
    SET stock = stock - NEW.quantity
    WHERE id = NEW.productid;
    
    IF (SELECT stock FROM public.product WHERE id = NEW.productid) < 0 THEN
        RAISE EXCEPTION 'No hay suficiente stock para el producto';
    END IF;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

```
2.2- Creo el trigger que utilice la función de disminuir el stock:

```
CREATE TRIGGER decrease_stock_trigger
AFTER INSERT ON public.detail
FOR EACH ROW EXECUTE PROCEDURE decrease_stock();

```
#### Compruebo tigger:
```
SELECT tgname, tgrelid::regclass, tgfoid::regprocedure
FROM pg_trigger
WHERE tgrelid = 'public.detail'::regclass
  AND tgname = 'decrease_stock_trigger';

```
<img src = "Img/Captura de pantalla 2024-07-15 011249.png" width = "500">

2.3- Probar tigger al momento de Insertar datos.

#### Verifico el stock del producto:
```
SELECT stock FROM public.product WHERE id = 1;
```

#### Agrego un nuevo detalle:
```
INSERT INTO public.detail (quantity, price, invoice_id, productid)
VALUES (2, 0.12e3, 1, 1);
```
#### Verifico el stock del producto después del nuevo detalle
```
SELECT stock FROM public.product WHERE id = 1;
```

<img src = "Img/Captura de pantalla 2024-07-15 011654.png" width = "500">

3.- Crear un función y un trigger para la tabla invoice donde valide que el campo create_at sea del año actual (fecha sistema).

3.1- Creo la función para validar el campo create_at:

```
CREATE OR REPLACE FUNCTION validate_create_at() RETURNS TRIGGER AS $$
BEGIN
    IF EXTRACT(YEAR FROM NEW.create_at) != EXTRACT(YEAR FROM CURRENT_DATE) THEN
        RAISE EXCEPTION 'La fecha debe ser del año actual';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

```
3.2- Creo el trigger que utilice la función de validación

```
CREATE TRIGGER validate_create_at_trigger
BEFORE INSERT OR UPDATE ON public.invoice
FOR EACH ROW EXECUTE PROCEDURE validate_create_at();

```
#### Compruebo tigger
```
SELECT tgname, tgrelid::regclass, tgfoid::regprocedure
FROM pg_trigger
WHERE tgrelid = 'public.invoice'::regclass
  AND tgname = 'validate_create_at_trigger';

```
<img src = "Img/Captura de pantalla 2024-07-15 015002.png" width = "500">

3.3- Probar tigger al momento de Insertar datos.

#### Intento con fecha fuera del año actual:
```
INSERT INTO public.invoice (code, create_at, total, client_id)
VALUES ('INV999', '2023-05-01', 100, 1);

```
<img src = "Img/Captura de pantalla 2024-07-15 015049.png" width = "500">

#### Intento con fecha del año actual:
```
INSERT INTO public.invoice (code, create_at, total, client_id)
VALUES ('INV1000', '2024-07-15', 100, 1);

```
<img src = "Img/Captura de pantalla 2024-07-15 015133.png" width = "500">

4.- Crea una función y un trigger para la tabla client y validar que el correo tenga un @.

4.1- Creo la función para validar el correo:

```
CREATE OR REPLACE FUNCTION validate_email() RETURNS TRIGGER AS $$
BEGIN
    IF NEW.email !~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z]{2,}$' THEN
        RAISE EXCEPTION 'El correo debe contener un @ y ser válido';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

```

4.2- Creo el trigger que utilice la función de valida:

```
CREATE TRIGGER validate_email_trigger
BEFORE INSERT OR UPDATE ON public.client
FOR EACH ROW EXECUTE PROCEDURE validate_email();
```
#### Compruebo tigger
```
SELECT tgname, tgrelid::regclass, tgfoid::regprocedure
FROM pg_trigger
WHERE tgrelid = 'public.invoice'::regclass
  AND tgname = 'validate_create_at_trigger';

```
<img src = "Img/Captura de pantalla 2024-07-15 015918.png" width = "500">

4.3- Probar tigger al momento de Insertar datos.

####  Intento con correo inválido:
```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('1234567890', 'Carlos Guillas', 'Baños', ' Carloshotmail.com');

```
<img src = "Img/Captura de pantalla 2024-07-15 020144.png" width = "500">

#### Intento con correo válido:
```
INSERT INTO public.client (nui, full_name, address, email)
VALUES ('0987654321', 'Luis Martinez', 'Uncovia', 'Martinez@hotmail.com');

```
<img src = "Img/Captura de pantalla 2024-07-15 020319.png" width = "500">



