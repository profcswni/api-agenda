# Referencia de la API

## Información General

- **Base URL**: `http://localhost:3000/api`
- **Formato**: Todos los endpoints aceptan y devuelven JSON
- **Autenticación**: Bearer Token (JWT)

## Autenticación

### Login
```http
POST /auth/login
Content-Type: application/json

{
    "email": "usuario@ejemplo.com",
    "password": "contraseña"
}
```

### Respuesta
```json
{
    "token": "jwt_token",
    "user": {
        "id": 1,
        "email": "usuario@ejemplo.com",
        "rol": "estudiante"
    }
}
```

## Usuarios

### Listar Usuarios
```http
GET /usuarios
Authorization: Bearer <token>

# Filtros opcionales
?rol=estudiante
?carrera_id=1
?search=nombre
```

### Obtener Usuario
```http
GET /usuarios/:id
Authorization: Bearer <token>
```

### Crear Usuario
```http
POST /usuarios
Authorization: Bearer <token>
Content-Type: application/json

{
    "email": "nuevo@ejemplo.com",
    "password": "contraseña",
    "nombre": "Nombre",
    "apellido": "Apellido",
    "rol": "estudiante",
    "carrera_id": 1
}
```

### Actualizar Usuario
```http
PUT /usuarios/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "nombre": "Nuevo Nombre",
    "apellido": "Nuevo Apellido"
}
```

### Eliminar Usuario
```http
DELETE /usuarios/:id
Authorization: Bearer <token>
```

## Carreras

### Listar Carreras
```http
GET /carreras
Authorization: Bearer <token>
```

### Obtener Carrera
```http
GET /carreras/:id
Authorization: Bearer <token>
```

### Crear Carrera
```http
POST /carreras
Authorization: Bearer <token>
Content-Type: application/json

{
    "nombre": "Ingeniería en Sistemas",
    "codigo": "IS-001"
}
```

### Actualizar Carrera
```http
PUT /carreras/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "nombre": "Nuevo Nombre",
    "codigo": "IS-002"
}
```

### Eliminar Carrera
```http
DELETE /carreras/:id
Authorization: Bearer <token>
```

## Grupos

### Listar Grupos
```http
GET /grupos
Authorization: Bearer <token>

# Filtros opcionales
?carrera_id=1
?usuario_id=1
```

### Obtener Grupo
```http
GET /grupos/:id
Authorization: Bearer <token>
```

### Crear Grupo
```http
POST /grupos
Authorization: Bearer <token>
Content-Type: application/json

{
    "nombre": "Grupo de Estudio",
    "descripcion": "Grupo para estudiar programación",
    "carrera_id": 1
}
```

### Actualizar Grupo
```http
PUT /grupos/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "nombre": "Nuevo Nombre",
    "descripcion": "Nueva descripción"
}
```

### Eliminar Grupo
```http
DELETE /grupos/:id
Authorization: Bearer <token>
```

### Gestión de Miembros

#### Listar Miembros
```http
GET /grupos/:id/miembros
Authorization: Bearer <token>
```

#### Agregar Miembro
```http
POST /grupos/:id/miembros
Authorization: Bearer <token>
Content-Type: application/json

{
    "usuario_id": 1
}
```

#### Eliminar Miembro
```http
DELETE /grupos/:id/miembros/:usuario_id
Authorization: Bearer <token>
```

## Invitaciones

### Listar Invitaciones
```http
GET /invitaciones
Authorization: Bearer <token>

# Filtros opcionales
?estado=pending
?grupo_id=1
?usuario_id=1
```

### Obtener Invitación
```http
GET /invitaciones/:id
Authorization: Bearer <token>
```

### Crear Invitación
```http
POST /invitaciones
Authorization: Bearer <token>
Content-Type: application/json

{
    "grupo_id": 1,
    "usuario_id": 1,
    "mensaje": "Te invito a unirte al grupo"
}
```

### Actualizar Invitación
```http
PUT /invitaciones/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "estado": "accepted" // o "rejected"
}
```

### Eliminar Invitación
```http
DELETE /invitaciones/:id
Authorization: Bearer <token>
```

## Códigos de Estado

- `200 OK`: La solicitud fue exitosa
- `201 Created`: Recurso creado exitosamente
- `400 Bad Request`: Error en la solicitud
- `401 Unauthorized`: No autenticado
- `403 Forbidden`: No autorizado
- `404 Not Found`: Recurso no encontrado
- `500 Internal Server Error`: Error del servidor

## Ejemplos de Respuestas de Error

### Error de Validación
```json
{
    "error": "ValidationError",
    "message": "Datos inválidos",
    "details": {
        "email": "Debe ser un email válido",
        "password": "Debe tener al menos 6 caracteres"
    }
}
```

### Error de Autenticación
```json
{
    "error": "UnauthorizedError",
    "message": "Token inválido o expirado"
}
```

### Error de Recurso No Encontrado
```json
{
    "error": "NotFoundError",
    "message": "Usuario no encontrado"
}
``` 