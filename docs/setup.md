# Guía de Configuración

## Requisitos Previos

### Software Necesario
- Node.js (v14 o superior)
- MySQL (v8.0 o superior)
- Git
- npm o yarn

### Cuentas y Accesos
- Acceso a GitHub para clonar el repositorio
- Credenciales de base de datos MySQL

## Instalación Paso a Paso

### 1. Clonar el Repositorio
```bash
git clone git@github.com:profcswni/api-agenda.git
cd api-agenda
```

### 2. Instalar Dependencias
```bash
npm install
```

### 3. Configuración del Entorno

#### Crear archivo .env
Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:
```env
# Base de datos
DATABASE_URL="mysql://usuario:contraseña@localhost:3306/nombre_base_datos"

# Configuración del servidor
PORT=3000
NODE_ENV=development

# JWT (para autenticación)
JWT_SECRET=tu_secreto_jwt
JWT_EXPIRES_IN=24h
```

#### Variables de Entorno Requeridas
- `DATABASE_URL`: URL de conexión a la base de datos MySQL
- `PORT`: Puerto donde correrá el servidor (default: 3000)
- `NODE_ENV`: Entorno de ejecución (development/production)
- `JWT_SECRET`: Secreto para firmar tokens JWT
- `JWT_EXPIRES_IN`: Tiempo de expiración de tokens JWT

### 4. Configuración de la Base de Datos

#### Crear Base de Datos
```sql
CREATE DATABASE nombre_base_datos;
```

#### Ejecutar Migraciones
```bash
# Crear y aplicar migraciones
npx prisma migrate dev --name init

# Generar cliente Prisma
npx prisma generate
```

### 5. Verificar la Instalación

#### Probar la Conexión
```bash
# Verificar conexión a la base de datos
npx prisma db pull

# Verificar que el servidor inicia correctamente
npm run dev
```

## Comandos Útiles

### Desarrollo
```bash
# Iniciar servidor en modo desarrollo
npm run dev

# Iniciar servidor en modo producción
npm start

# Ejecutar tests
npm test
```

### Base de Datos
```bash
# Ver estado de migraciones
npx prisma migrate status

# Resetear base de datos
npx prisma migrate reset

# Abrir Prisma Studio
npx prisma studio
```

## Solución de Problemas

### Problemas Comunes

1. **Error de conexión a la base de datos**
   - Verificar que MySQL está corriendo
   - Confirmar credenciales en DATABASE_URL
   - Asegurar que la base de datos existe

2. **Errores en migraciones**
   - Ejecutar `npx prisma migrate reset`
   - Verificar logs de migración
   - Asegurar que no hay conflictos en el esquema

3. **Dependencias faltantes**
   - Eliminar node_modules y package-lock.json
   - Ejecutar `npm install` nuevamente

### Logs y Depuración
- Revisar logs en `logs/` (si está configurado)
- Usar `console.log` en desarrollo
- Configurar nivel de log en `.env`

## Actualización del Sistema

### Actualizar Dependencias
```bash
# Verificar actualizaciones disponibles
npm outdated

# Actualizar dependencias
npm update

# Actualizar Prisma
npx prisma update
```

### Actualizar Base de Datos
```bash
# Crear nueva migración
npx prisma migrate dev --name nombre_migracion

# Aplicar migraciones pendientes
npx prisma migrate deploy
``` 