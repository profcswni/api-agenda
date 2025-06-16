# API Agenda - Documentación

Bienvenido a la documentación oficial de API Agenda, un sistema de gestión de datos de contacto para la Universidad Martin Lutero.

## 📚 Índice de Documentación

### 🏗️ [Arquitectura del Sistema](architecture.md)
- Descripción general del sistema
- Stack tecnológico
- Componentes principales
- Decisiones técnicas
- Seguridad y escalabilidad

### ⚙️ [Guía de Configuración](setup.md)
- Requisitos previos
- Instalación paso a paso
- Configuración del entorno
- Solución de problemas
- Actualización del sistema

### 🔌 [Referencia de la API](api-reference.md)
- Información general
- Autenticación
- Endpoints de usuarios
- Endpoints de carreras
- Endpoints de grupos
- Endpoints de invitaciones
- Códigos de estado
- Ejemplos de respuestas

### 💾 [Base de Datos](database.md)
- Esquema de la base de datos
- Modelos y relaciones
- Índices y restricciones
- Migraciones
- Consultas comunes
- Mantenimiento

### 👨‍💻 [Guía de Desarrollo](development.md)
- Estándares de código
- Flujo de trabajo Git
- Pruebas
- Seguridad
- Logging
- Despliegue
- Monitoreo
- Optimización
- Mantenimiento

## 🚀 Inicio Rápido

1. Clona el repositorio:
   ```bash
   git clone git@github.com:profcswni/api-agenda.git
   cd api-agenda
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. Configura el entorno:
   ```bash
   cp .env.example .env
   # Edita .env con tus configuraciones
   ```

4. Inicia la base de datos:
   ```bash
   npx prisma migrate dev
   ```

5. Inicia el servidor:
   ```bash
   npm run dev
   ```

## 📋 Requisitos del Sistema

- Node.js v14 o superior
- MySQL v8.0 o superior
- npm o yarn
- Git

## 🔧 Tecnologías Principales

- **Backend**: Node.js, Express
- **Base de Datos**: MySQL
- **ORM**: Prisma
- **Autenticación**: JWT
- **Documentación**: Markdown

## 🤝 Contribuir

1. Haz fork del repositorio
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 📞 Soporte

Para soporte, por favor abre un issue en el repositorio de GitHub o contacta al equipo de desarrollo.

---

<div align="center">
  <sub>Construido con ❤️ por el equipo de la Universidad Martin Lutero</sub>
</div> 