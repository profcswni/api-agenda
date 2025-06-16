# Arquitectura del Sistema

## Descripción General
API Agenda es un sistema de gestión de contactos diseñado para la Universidad Martin Lutero, enfocado en la gestión de datos de contacto de estudiantes y docentes.

## Stack Tecnológico

### Backend
- **Node.js**: Runtime de JavaScript para el servidor
- **Express**: Framework web para Node.js
- **Prisma ORM**: ORM moderno para la gestión de la base de datos
- **MySQL**: Sistema de gestión de base de datos relacional

### Estructura del Proyecto
```
api-agenda/
├── docs/               # Documentación del proyecto
├── prisma/            # Configuración y modelos de Prisma
├── src/
│   ├── controllers/   # Controladores de la aplicación
│   ├── routes/        # Definición de rutas
│   ├── middleware/    # Middleware personalizado
│   └── utils/         # Utilidades y helpers
├── .env              # Variables de entorno
└── index.js          # Punto de entrada de la aplicación
```

## Componentes Principales

### 1. Gestión de Usuarios
- Sistema de roles (admin, profesor, estudiante, oficina)
- Autenticación y autorización
- Perfiles de usuario con información de contacto

### 2. Gestión de Carreras
- Administración de carreras universitarias
- Asociación de usuarios con carreras
- Gestión de grupos por carrera

### 3. Sistema de Grupos
- Creación y gestión de grupos
- Gestión de miembros
- Sistema de invitaciones

### 4. API RESTful
- Endpoints RESTful para todas las operaciones CRUD
- Respuestas JSON estandarizadas
- Manejo de errores consistente

## Decisiones Técnicas

### Por qué Prisma ORM
- Type safety con TypeScript
- Migraciones automáticas
- Generación de tipos
- Query builder intuitivo

### Por qué Express
- Framework ligero y flexible
- Gran ecosistema de middleware
- Fácil de aprender y mantener
- Excelente rendimiento

### Por qué MySQL
- Base de datos relacional robusta
- Excelente para datos estructurados
- Buena integración con Prisma
- Amplio soporte en la comunidad

## Seguridad
- Validación de datos en todas las entradas
- Sanitización de inputs
- Manejo seguro de contraseñas
- Protección contra ataques comunes (XSS, CSRF, etc.)

## Escalabilidad
- Arquitectura modular
- Separación clara de responsabilidades
- Fácil de extender con nuevas funcionalidades
- Preparado para crecimiento en usuarios y datos 