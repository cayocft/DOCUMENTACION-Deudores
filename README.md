# Documentación del backend de Gestión de Usuarios
# Indice
## 1 Datos del Servidor
## 2 Datos estados deudores
## 3 Autenticación (Iniciar Sesión)
## 4 Usuarios
## 5 Registro de Deuda
-----
## Servicios 

### 1. Datos del Servidor
    Servidor: https://novel-heather-cft-99b6f305.koyeb.app
    PREFIJO: /api

### 2. Datos estados deudores
    0: Le Debo
    1: Me deben

### 3. Autenticación (Iniciar Sesión)
#### Rutas
    Ruta: /login/inicio-sesion
    Metodo: POST

#### 3.1 Datos recibidos
    correo: string
    password: string

#### 3.2 Respuesta del servidor
    (200)
    "inicio_sesion": true,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Miwibm9tYnJlIjoiSnVhbiIsImFwZWxsaWRvIjoiTG9yZW4iLCJ0ZWxlZm9ubyI6Ijk5OTk5OTk5OSIsImNvcnJlbyI6Imp1YW5AZ21haWwuY29tIiwidGlwbyI6MCwiZXN0YWRvIjoxLCJwYXNzd29yZCI6IiQyYiQxMCQzTFpIZUlFZHJVZ2tUcU1RL1BJWHdPM2ZFdmtjL1pndGhubTNrVzYxZEN2Li9vOGtYM1NHTyIsImlhdCI6MTYzODc1MjcwMywiZXhwIjoxNjM4ODM5MTAzfQ.0nnUsfr45JbRC22OkD-DJFYV7D7d1gJu9wPP5WCC1xg",
    "mensaje": "Inicio de sesión correcto"

### 4. Usuarios
#### Rutas
    Ruta: /usuario

#### 4.1 Crear usuario

    Ruta: /crear
    Método: POST

#### Datos Recibidos
    nombre: string
    apellido: string
    telefono: string
    correo: string
    tipo: integer (0: Registrado en sistema; 1: Registrado por un usuario)
    estado: integer (0: Inactivo; 1: Activo)
    password: string

#### Respuesta del Servidor
    (200)
    {
    "usuario": {
        "id": 9,
        "nombre": "nombre usuario",
        "apellido": "apellido usuario",
        "telefono": "999999999",
        "correo": "correo@gmail.com",
        "tipo": "0",
        "estado": "1",
        "password": "$2b$10$f0pBvDmpb.eHuRZn6rExmugQ5MtZ3VGVBoc3HaFnD08S1YEczpTR6"
    },
    "mensaje": "Usuario creado correctamente"
}

#### 4.2 Obtener usuario por correo
    Ruta: /obtener-usuario-correo
    Método: POST

#### Datos recibido

    correo: string

#### Respuesta servidor
    (200)
    {
        "usuario": {
            "id": 3,
            "nombre": "Nombre usuario",
            "apellido": "Apellido usuario",
            "telefono": "999999999",
            "correo": "correo@gmail.com",
            "tipo": 0,
            "estado": 1,
            "password": "$2b$10$j45B0u27PF7rtz88AAs7..GAOJ58U.g5H2Ell6R0nl6cPuvl7hqVu"
        },
        "mensaje": "Existe usuario con este correo"
    }

#### 4.3 Obtener todos los usuarios
    Ruta: /obtener-usuarios
    Método: GET

#### Datos recibido

    "No recibe datos"

#### Respuesta servidor
    (200)
    {
        "usuarios": [
            {
                "id": 1,
                "nombre": "Nombre1",
                "apellido": "apellido1",
                "telefono": "999999999",
                "correo": "correo1@gmail.com",
                "tipo": 0,
                "estado": 1,
                "password": "$2b$10$zv8DB9ziLkzA9k3HMgHkPOCaJG10om.YXig7069UIghIUlSsn6Fb6"
            },
            {
                "id": 2,
                "nombre": "Nombre 2",
                "apellido": "apellido2",
                "telefono": "999999999",
                "correo": "correo2@gmail.com",
                "tipo": 0,
                "estado": 1,
                "password": "$2b$10$3LZHeIEdrUgkTqMQ/PIXwO3fEvkc/Zgthnm3kW61dCv./o8kX3SGO"
            },
        ],
        "mensaje": "Usuarios obtenidos correctamente"
    }

### 5. Registro de Deuda
#### Rutas
    Ruta: /registro_deuda

#### 5.1 Crear Registro de deuda

    Ruta: /crear
    Método: POST

#### Datos recibidos

    tipo: integer (0: Le debo dinero; 1: Me debe dinero)
    comentario: string
    valor: integer
    estado: integer (0: Activo; 1 Finalizado)
    fecha_creacion: datetime
    usuarioId: integer
    involucradoId: integer

#### Respuesta del servidor:
    (200)
    {
        "registro_deuda": {
            "id": 48,
            "tipo": "1",
            "comentario": "Arroz Chauda de los que te gustan",
            "valor": "5500",
            "estado": "0",
            "fecha_creacion": "2021-11-28T00:00:00.000Z",
            "usuarioId": "3",
            "involucradoId": "9"
        },
        "usuario": {
            "id": 3,
            "nombre": "nombre usuario que registro la deuda",
            "apellido": "apellido usuario que registro la deuda",
            "telefono": "999999999",
            "correo": "usuarioinicial@gmail.com",
            "tipo": 0,
            "estado": 1,
            "password": "$2b$10$j45B0u27PF7rtz88AAs7..GAOJ58U.g5H2Ell6R0nl6cPuvl7hqVu"
        },
        "involucrado": {
            "id": 9,
            "nombre": "nombre usuario que registro esta involucrado en la deuda",
            "apellido": "apellido usuario que registro esta involucrado en la deuda",
            "telefono": "999999999",
            "correo": "correoinvolucrado@gmail.com",
            "tipo": 0,
            "estado": 1,
            "password": "$2b$10$f0pBvDmpb.eHuRZn6rExmugQ5MtZ3VGVBoc3HaFnD08S1YEczpTR6"
        },
        "respuesta_correoDeudor": {
            "accepted": [
                "correoinvolucrado@gmail.com"
            ],
            "rejected": [],
            "envelopeTime": 108,
            "messageTime": 686,
            "messageSize": 10725,
            "response": "250 OK id=1mu3W4-0006Ut-7M",
            "envelope": {
                "from": "correo del servidor",
                "to": [
                    "correoinvolucrado@gmail.com"
                ]
            },
            "messageId": "<c0447a20-2d47-76fe-6368-7edce96bf238>"
        },
        "mensaje": "Registro deuda creado correctamente"
    }

#### 5.2 Obtener registro de deuda "Le debo" (tipo 0)

    Ruta: /obtener-registro-deuda-deben/:id_usuario/:tipo
    Método: GET

#### Datos recibidos por URL
    id_usuario: integer
    tipo: integer
#### Ejemplo de datos recibidos por URL
    registro_deuda/obtener-registro-deuda-deben/3/0

#### Respuesta servidor
    (200)
    {
        "registro_deudas": [
            {
                "id": 37,
                "tipo": 0,
                "comentario": "comentario de usuario",
                "valor": 6000,
                "estado": 0,
                "fecha_creacion": "2021-11-28T00:00:00.000Z",
                "fecha_finalizado": null,
                "usuarioId": 3,
                "involucradoId": 4,
                "crea": {
                    "nombre": "Nombre Usuario que crear",
                    "apellido": "Apellido Usuario que crear",
                    "telefono": "999999999",
                    "correo": "correousuario@gmail.com",
                    "tipo": 0,
                    "estado": 1
                },
                "involucrado": {
                    "nombre": "Nombre Usuario involucrado",
                    "apellido": "Apellido Usuario involucrado",
                    "telefono": "999999999",
                    "correo": "correoinvolucrado@gmail.com",
                    "tipo": 0,
                    "estado": 1
                }
            },
            {
                "id": 38,
                "tipo": 0,
                "comentario": "comentario de usuario",
                "valor": 6000,
                "estado": 0,
                "fecha_creacion": "2021-11-28T00:00:00.000Z",
                "fecha_finalizado": null,
                "usuarioId": 3,
                "involucradoId": 4,
                "crea": {
                    "nombre": "Nombre Usuario que crear",
                    "apellido": "Apellido Usuario que crear",
                    "telefono": "999999999",
                    "correo": "correousuario@gmail.com",
                    "tipo": 0,
                    "estado": 1
                },
                "involucrado": {
                    "nombre": "Nombre Usuario involucrado",
                    "apellido": "Apellido Usuario involucrado",
                    "telefono": "999999999",
                    "correo": "correoinvolucrado@gmail.com",
                    "tipo": 0,
                    "estado": 1
                }
            },
        ],
        "mensaje": "Registros obtenidos correctamente"
    }

#### 5.3 Obtener registro de deuda "Me deben" (tipo:1)

    Ruta: /obtener-registro-deuda-pagar/:id_usuario/:tipo
    Método: GET

#### Datos recibidos por URL
    id_usuario: integer
    tipo: integer
#### Ejemplo de datos recibidos por URL
    registro_deuda/obtener-registro-deuda-pagar/3/1

#### Respuesta servidor
    (200)
    {
        "registro_deudas": [
            {
                "id": 37,
                "tipo": 0,
                "comentario": "comentario de usuario",
                "valor": 6000,
                "estado": 0,
                "fecha_creacion": "2021-11-28T00:00:00.000Z",
                "fecha_finalizado": null,
                "usuarioId": 3,
                "involucradoId": 4,
                "crea": {
                    "nombre": "Nombre Usuario que crear",
                    "apellido": "Apellido Usuario que crear",
                    "telefono": "999999999",
                    "correo": "correousuario@gmail.com",
                    "tipo": 0,
                    "estado": 1
                },
                "involucrado": {
                    "nombre": "Nombre Usuario involucrado",
                    "apellido": "Apellido Usuario involucrado",
                    "telefono": "999999999",
                    "correo": "correoinvolucrado@gmail.com",
                    "tipo": 0,
                    "estado": 1
                }
            },
            {
                "id": 38,
                "tipo": 0,
                "comentario": "comentario de usuario",
                "valor": 6000,
                "estado": 0,
                "fecha_creacion": "2021-11-28T00:00:00.000Z",
                "fecha_finalizado": null,
                "usuarioId": 3,
                "involucradoId": 4,
                "crea": {
                    "nombre": "Nombre Usuario que crear",
                    "apellido": "Apellido Usuario que crear",
                    "telefono": "999999999",
                    "correo": "correousuario@gmail.com",
                    "tipo": 0,
                    "estado": 1
                },
                "involucrado": {
                    "nombre": "Nombre Usuario involucrado",
                    "apellido": "Apellido Usuario involucrado",
                    "telefono": "999999999",
                    "correo": "correoinvolucrado@gmail.com",
                    "tipo": 0,
                    "estado": 1
                }
            },
        ],
        "mensaje": "Registros obtenidos correctamente"
    }

#### 5.4 Notificar Deuda 

    Ruta: /notificar-deuda/:id_registroDeuda
    Método: GET

#### Datos recibidos por URL
    id_registroDeuda: integer
#### Ejemplo de datos recibidos por URL
    registro_deuda/notificar-deuda/48
#### Respuesta del servidor
    (200)
    {
        "mensaje": "Notificación enviada"
    }

#### 5.5 Finalizar Deuda
    Ruta: /finalizar-deuda/:id_registroDeuda
    Método: GET
#### Datos recibidos por URL
        id_registroDeuda: integer
#### Datos recibidos por BODY (normal)
        fecha_finalizacion: datetime
#### Ejemplo de datos recibidos por URL
    registro_deuda/finalizar-deuda/48
#### Respuesta del servidor
    (200)
    {
        "respuesta_finalizar_deuda": [
            1
        ],
        "mensaje": "Deuda finalizada y Notificada"
    }

# Documentación Finalizada
## Backend prestado por WALIEX ©
