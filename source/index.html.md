---
title: ConSis API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json--server: Game Server
  - json--user: User

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introducción

Profe culiao aquí está la documentación para la API de mi proyecto.

Para la API, existen 3 tipos de usuarios:

  * Administrator de sistema: Tiene el poder para gestionar las cuentas asociadas a los condominios, ya sean cuentas de administradores y cuentas de copropietarios.
  * Administrador de condominio: Podrá acceder a la información de los copropietarios de su condominio e interactuar con ellos.
  * Copropietario: Podrá realizar cambios asociados a su cuenta e interactuar con el administrador del condominio y podrá ver mensajes, notificaciones y avisos personalizados para él.

# Condominios

## Obtener todos los condominios y sus atributos

```json--server
[
  {
    "id": 1,
    "name": "Los valles",
    "address": "Las Azucenas 123",
  },
  ...
]
```

Este endpoint retorna una lista de todos los condominios y sus datos.

### HTTP Request

`GET http://localhost:3000/condominios`

## Crear un condominio.

```json--server
  {
    "id": 1,
    "name": "Los valles",
    "address": "Las Azucenas 123",
  },
```

Crear un nuevo condominio y lo retorna.

### HTTP Request

`POST http://localhost:3000/condominios`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
name  | string | true | | Nombre condominio.
address | string | true | | Dirección del condominio.

## Obtener los atributos de un condominio en específico.

```json--server
{
  "id": 1,
  "name": "Los valles",
  "address": "Las Azucenas 123",
}
```

Este endpoint entrega los datos de un condominio en específico.
### HTTP Request

`GET http://localhost:3000/condominios/:id`

## Actualizar atributos de un condominio en específico.


```json--server
{
  "id": 1,
  "name": "Los montes",
  "address": "Las Azucenas 123",
}
```

Este endpoint te permite actualizar atributos de un condominio.
### HTTP Request

`PATCH http://localhost:3000/condominios/:id`


Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
name  | string | false | | El nuevo valor del atributo.
address | string | false | | El nuevo valor del atributo.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente

## Eliminar un condominio.

```json--server
{
  "id": 2,
  "name": "Los corcolones",
  "address": "Francisco bilbao 123",
}
```
Este endpoint te permite eliminar un condominio en específico.
### HTTP Request

`DELETE http://localhost:3000/condominios/:id`

# Datos transferencia
## Listar datos de transferencia para un condominio.
```json--server
{
  "bank": "Banco de Chile",
  "account_number": "12312312321",
  "rut": "71411224-1",
  "account_type": "Cuenta corriente",
  "name": "Condominio Los Aromos"
  "id_condominio": "1",
}
```

Permite listar los datos de transferencia para un condominio.
### HTTP Request

`GET http://localhost:3000/condominios/:id/info`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente

## Editar datos de transferencia para un condominio.
```json--server
{
  "bank": "Banco Santander",
  "account_number": "12312312322",
  "rut": "71444224-1",
  "account_type": "Cuenta corriente",
  "name": "Condominio Los Aromos"
  "id_condominio": "1",
}
```
Permite editar los datos de transferencia para un condominio.
### HTTP Request

`PATCH http://localhost:3000/condominios/:id/info`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente


# Apartamento
## Obtener lista apartamentos por condominio
```json--server
[
  {
    "id": "1",
    "address": "Francisco Bilbao 142",
    "label": "A41",
    "description": "blabla",
    "condominio_id" : "1",
  }
  ...
]
```
Permite listar apartamentos por condominio.
### HTTP Request

`GET http://localhost:3000/condominios/:id/apartamentos`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente

## Crear apartamento
```json--server
  {
    "id": "1",
    "address": "Francisco Bilbao 142",
    "label": "A41",
    "description": "blabla",
    "condominio_id" : "1",
  }
```

Permite crear apartamento por condominio

### HTTP Request

`POST http://localhost:3000/condominios/:id/apartamentos`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
address  | string | true | | Dirección de apartamento.
label | string | true | | Número y torre de apartamento.
description | string | false | | Descripción breve de apartamento.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente

## Editar apartamento
```json--server
  {
    "id": "1",
    "address": "Francisco Bilbao 142",
    "label": "A41",
    "description": "blablablablabla",
    "condominio_id" : "1",
  }
```
Permite editar datos de apartamento.
### HTTP Request

`POST http://localhost:3000/condominios/:id/apartamentos/:id`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
description | string | false | | Nuevo valor para la descripción.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente
unknown_apartamento  | 404 | Apartamento no existente




# Usuarios

## Obtener lista con usuarios.
```json--server
[
  {
    "id": "1",
    "name": "Rodrigo Torres",
    "rut": "19289131-0",
    "email": "rodrigo@gmail.com",
    "username": "rodrigotorrese",
    "password": "1234",
    "user_type": "administradorSistema"
  }
  ...
]
```
Listar todos los usuarios del sistema.
### HTTP Request

`GET http://localhost:3000/users`

## Obtener atríbutos de un usuario específico
```json--server
{
  "id": "1",
  "name": "Rodrigo Torres",
  "rut": "19289131-0",
  "email": "rodrigo@gmail.com",
  "username": "rodrigotorrese",
  "password": "1234",
  "user_type": "administradorSistema",
}
```
Permite obtener atríbutos de un usuario en específico.
### HTTP Request

`GET http://localhost:3000/users/:id`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user  | 404 | No se encuentra a usuario.
not_authorized | 403 | No se cuenta con el permiso suficiente.


## Crear usuario.
```json--server
{
  "id": "2",
  "name": "Felipe Morales",
  "rut": "9421706-7",
  "email": "felipe@gmail.com",
  "username": "felipemoralesm",
  "password": "1234",
  "user_type": "copropietario",
}
```
Crea un nuevo usuario y lo retorna.
### HTTP Request

`POST http://localhost:3000/users`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
name  | string | true | | Nombre completo usuario.
rut | string | true | | | Rut usuario.
email | string | true | | Correo electrónico usuario.
username | string | true | | Nombre cuenta de usuario.
password | string | true | | Contraseña de cuenta de usuario.
user_type | string | true | | Nivel de usuario.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
not_authorized | 403 | No se cuenta con el permiso suficiente.

## Editar usuario.

```json--server
{
  "id": "2",
  "name": "Felipe Morales",
  "rut": "9421706-7",
  "email": "felipe_morales@gmail.com",
  "username": "felipemoralesm",
  "password": "1234",
  "user_type": "copropietario",
}
```
Permite editar atributos de un usuario.
### HTTP Request

`POST http://localhost:3000/users/:id`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
email | string | true | Correo electrónico usuario.
username | string | true | Nombre cuenta de usuario.
password | string | true | Contraseña de cuenta de usuario.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user  | 404 | No se encuentra a usuario.
not_authorized | 403 | No se cuenta con el permiso suficiente.


## Eliminar usuario.

```json--server
{
  "id": "2",
  "name": "Felipe Morales",
  "rut": "9421706-7",
  "email": "felipe_morales@gmail.com",
  "username": "felipemoralesm",
  "password": "1234",
  "user_type": "copropietario",
}
```
Permite eliminar usuario especificado.
### HTTP Request

`DELETE http://localhost:3000/users/:id`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user  | 404 | No se encuentra a usuario.
not_authorized | 403 | No se cuenta con el permiso suficiente.

# Noticias
## Listar noticias

```json--server
{
  "id": "1",
  "title": "Empiezan trabajos.",
  "msge": "Desde el día martes 5 de septiembre, se empiezan los trabajos dentro del condominio con el fin de mejorar las calles para el correcto tránsito de los vehículos.",
  "condominio_id": "1",
}
```

Permite listar todas las noticias de un condominio en específico.
### HTTP Request

`GET http://localhost:3000/condominios/:id/noticias`

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente.

## Crear noticia
```json--server
{
  "id": "2",
  "title": "Cierre plaza 1",
  "msge": "Debido a trabajos, la plaza 1 será cerrada.",
  "condominio_id": "1",
}
``` 

Permite crear noticias para un condominio.
### HTTP Request

`POST http://localhost:3000/condominios/:id/noticias`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
title | string | true | Título noticia.
msge | string | true | Cuerpo noticia.
condominio_id | int | true | Id de condominio que irá noticia.

### Errors
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente.

## Eliminar noticia
```json--server
{
  "id": "2",
  "title": "Cierre plaza 1",
  "msge": "Debido a trabajos, la plaza 1 será cerrada.",
  "condominio_id": "1",
}
```

Permite eliminar noticia en específico y la retorna.
### HTTP Request

`Delete http://localhost:3000/condominios/:id/noticias/:id`

### Errores
String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_condominio  | 404 | Condominio no existente.
unknown_noticia | 404 | Noticia no existente.

# Notificaciones
## Listar notificaciones
```json--server
{
  "id": "1",
  "title": "Deuda",
  "msge": "Recuerda tu pago para este mes con fecha de vencimiento el 8/09/2017 por un monto de $135.000",
  "id_usuario": "1",
}
```

Permite listar notificaciones de un usuario.

### HTTP Request

`GET http://localhost:3000/users/:id/notificaciones`

### Errores

String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user | 404 | Usuario no existente.

## Crear notificación
```json--server
{
  "id": "2",
  "title": "Problema resuelto",
  "msge": "Señor Felipe, su problema ha sido resuelto, por favor acercarse a administración",
  "id_usuario": "2",
}
```

Permite crear una notificación para un usuario.

### HTTP Request

`POST http://localhost:3000/users/:id/notificaciones`

Parámetro | Tipo | Requerido | Defecto | Descripción
--------- | ---- | -------- | ------- | -----------
title | string | true | Título notificación.
msge | string | true | Cuerpo notificación.
id_usuario | int | true | Id de usuario a cual llegará notificación.

### Errores

String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user | 404 | Usuario no existente.

## Eliminar notificación
```json--server
{
  "id": "2",
  "title": "Problema resuelto",
  "msge": "Señor Felipe, su problema ha sido resuelto, por favor acercarse a administración",
  "id_usuario": "2",
}
```

Permite eliminar una notificación y luego retornarla.

### HTTP Request

`DELETE http://localhost:3000/users/:id/notificaciones/:id`

### Errores

String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_notificacion | 404 | Notificación no existente.
unknown_user | 404 | Usuario no existente.

# Documentos

## Listar documentos para un usuario.
```json--server
{
  "id": "1",
  "title": "Factura mes septiembre",
  "fecha_subida": "01/09/2017",
}
```
Permite listar documentos asociados a un usuario.

### HTTP Request

`GET http://localhost:3000/users/:id/documentos`

### Errores

String code | Associated Code | Meaning
----------- | --------------- | -------
unknown_user | 404 | Usuario no existente.

## Subir documento a un usuario.

### HTTP Request

## Eliminar documento a un usuario.

### HTTP Request
