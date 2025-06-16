# Documentación de la Base de Datos

## Esquema de la Base de Datos

### Modelo de Datos

```prisma
// Esquema Prisma

model Usuario {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  password  String
  nombre    String
  apellido  String
  rol       Rol      @default(estudiante)
  carrera   Carrera? @relation(fields: [carrera_id], references: [id])
  carrera_id Int?
  grupos    Miembro[]
  invitaciones_enviadas Invitacion[] @relation("Invitador")
  invitaciones_recibidas Invitacion[] @relation("Invitado")
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt
}

model Carrera {
  id        Int      @id @default(autoincrement())
  nombre    String
  codigo    String   @unique
  usuarios  Usuario[]
  grupos    Grupo[]
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt
}

model Grupo {
  id          Int      @id @default(autoincrement())
  nombre      String
  descripcion String?
  carrera     Carrera  @relation(fields: [carrera_id], references: [id])
  carrera_id  Int
  miembros    Miembro[]
  invitaciones Invitacion[]
  created_at  DateTime @default(now())
  updated_at  DateTime @updatedAt
}

model Miembro {
  id         Int      @id @default(autoincrement())
  usuario    Usuario  @relation(fields: [usuario_id], references: [id])
  usuario_id Int
  grupo      Grupo    @relation(fields: [grupo_id], references: [id])
  grupo_id   Int
  created_at DateTime @default(now())
  updated_at DateTime @updatedAt

  @@unique([usuario_id, grupo_id])
}

model Invitacion {
  id          Int      @id @default(autoincrement())
  grupo       Grupo    @relation(fields: [grupo_id], references: [id])
  grupo_id    Int
  invitador   Usuario  @relation("Invitador", fields: [invitador_id], references: [id])
  invitador_id Int
  invitado    Usuario  @relation("Invitado", fields: [invitado_id], references: [id])
  invitado_id Int
  mensaje     String?
  estado      EstadoInvitacion @default(pending)
  created_at  DateTime @default(now())
  updated_at  DateTime @updatedAt

  @@unique([grupo_id, invitado_id])
}

enum Rol {
  admin
  profesor
  estudiante
  oficina
}

enum EstadoInvitacion {
  pending
  accepted
  rejected
}
```

## Relaciones

### Usuario
- Pertenece a una Carrera (opcional)
- Puede ser miembro de múltiples Grupos
- Puede enviar y recibir Invitaciones

### Carrera
- Tiene múltiples Usuarios
- Tiene múltiples Grupos

### Grupo
- Pertenece a una Carrera
- Tiene múltiples Miembros
- Tiene múltiples Invitaciones

### Miembro
- Conecta Usuarios con Grupos
- Relación muchos a muchos

### Invitacion
- Conecta Usuarios con Grupos
- Tiene un estado (pending, accepted, rejected)
- Tiene un invitador y un invitado

## Índices y Restricciones

### Índices
- `Usuario.email`: Único
- `Carrera.codigo`: Único
- `Miembro(usuario_id, grupo_id)`: Único
- `Invitacion(grupo_id, invitado_id)`: Único

### Restricciones
- `Usuario.carrera_id`: Clave foránea a `Carrera.id`
- `Grupo.carrera_id`: Clave foránea a `Carrera.id`
- `Miembro.usuario_id`: Clave foránea a `Usuario.id`
- `Miembro.grupo_id`: Clave foránea a `Grupo.id`
- `Invitacion.grupo_id`: Clave foránea a `Grupo.id`
- `Invitacion.invitador_id`: Clave foránea a `Usuario.id`
- `Invitacion.invitado_id`: Clave foránea a `Usuario.id`

## Tipos de Datos

### Enumeraciones
- `Rol`: admin, profesor, estudiante, oficina
- `EstadoInvitacion`: pending, accepted, rejected

### Campos Comunes
- `id`: Int (autoincrement)
- `created_at`: DateTime
- `updated_at`: DateTime

## Migraciones

### Crear Migración Inicial
```bash
npx prisma migrate dev --name init
```

### Aplicar Migraciones
```bash
npx prisma migrate deploy
```

### Resetear Base de Datos
```bash
npx prisma migrate reset
```

## Consultas Comunes

### Obtener Usuarios por Carrera
```sql
SELECT * FROM Usuario WHERE carrera_id = ?;
```

### Obtener Miembros de un Grupo
```sql
SELECT u.* FROM Usuario u
JOIN Miembro m ON u.id = m.usuario_id
WHERE m.grupo_id = ?;
```

### Obtener Invitaciones Pendientes
```sql
SELECT i.*, g.nombre as grupo_nombre, u.nombre as invitador_nombre
FROM Invitacion i
JOIN Grupo g ON i.grupo_id = g.id
JOIN Usuario u ON i.invitador_id = u.id
WHERE i.invitado_id = ? AND i.estado = 'pending';
```

## Mantenimiento

### Backup
```bash
mysqldump -u usuario -p nombre_base_datos > backup.sql
```

### Restaurar
```bash
mysql -u usuario -p nombre_base_datos < backup.sql
```

### Optimización
```sql
-- Analizar tablas
ANALYZE TABLE Usuario, Carrera, Grupo, Miembro, Invitacion;

-- Optimizar tablas
OPTIMIZE TABLE Usuario, Carrera, Grupo, Miembro, Invitacion;
``` 