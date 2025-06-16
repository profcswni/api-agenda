# API Agenda - Universidad Martin Lutero

Sistema de gestión de datos de contacto de estudiantes y docentes.

## Tecnologías

- Node.js
- Express
- MySQL
- Prisma ORM

---

## Instalación

1. **Clona el repositorio**
   ```bash
   git clone git@github.com:profcswni/api-agenda.git
   cd api-agenda
   ```

2. **Instala las dependencias**
   ```bash
   npm install
   ```

3. **Configura las variables de entorno**

   Crea un archivo `.env` en la raíz con el siguiente contenido:
   ```
   DATABASE_URL="mysql://usuario:contraseña@localhost:3306/nombre_base_datos"
   ```

4. **Inicializa Prisma y la base de datos**
   ```bash
   npx prisma migrate dev --name init
   npx prisma generate
   ```

---

## Levantar el servidor

```bash
npx nodemon index.js
```
o
```bash
node index.js
```

---

## Endpoints

### Usuarios (`usuarios`)
- `GET /usuarios` — Listar todos los usuarios
- `GET /usuarios/:id` — Obtener usuario por ID
- `POST /usuarios` — Crear usuario
- `PUT /usuarios/:id` — Actualizar usuario
- `DELETE /usuarios/:id` — Eliminar usuario

#### Filtros y búsquedas:
- `GET /usuarios?rol=estudiante` — Filtrar por rol
- `GET /usuarios?carrera_id=1` — Filtrar por carrera

---

### Carreras (`carreras`)
- `GET /carreras` — Listar todas las carreras
- `GET /carreras/:id` — Obtener carrera por ID
- `POST /carreras` — Crear carrera
- `PUT /carreras/:id` — Actualizar carrera
- `DELETE /carreras/:id` — Eliminar carrera

---

### Grupos (`grupos`)
- `GET /grupos` — Listar todos los grupos
- `GET /grupos/:id` — Obtener grupo por ID
- `POST /grupos` — Crear grupo
- `PUT /grupos/:id` — Actualizar grupo
- `DELETE /grupos/:id` — Eliminar grupo

#### Miembros de grupo:
- `GET /grupos/:id/miembros` — Listar miembros de un grupo
- `POST /grupos/:id/miembros` — Agregar miembro a grupo
- `DELETE /grupos/:id/miembros/:usuario_id` — Eliminar miembro de grupo

---

### Miembros (`miembros`)
- `GET /miembros` — Listar todos los miembros
- `GET /miembros/:id` — Obtener miembro por ID
- `POST /miembros` — Crear miembro (asociar usuario a grupo)
- `DELETE /miembros/:id` — Eliminar miembro

---

### Invitaciones (`invitaciones`)
- `GET /invitaciones` — Listar todas las invitaciones
- `GET /invitaciones/:id` — Obtener invitación por ID
- `POST /invitaciones` — Crear invitación
- `PUT /invitaciones/:id` — Actualizar estado de invitación (aceptar/rechazar)
- `DELETE /invitaciones/:id` — Eliminar invitación

#### Invitaciones por usuario:
- `GET /usuarios/:id/invitaciones` — Invitaciones recibidas/enviadas por usuario

---

## Notas

- Todos los endpoints aceptan y devuelven datos en formato JSON.
- Se recomienda usar herramientas como Postman para probar la API.
- El sistema soporta roles: `admin`, `profesor`, `estudiante`, `oficina`.

---
