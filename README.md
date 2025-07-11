# 🚀 Proyecto CRUD Completo: Gestión de Personas y Países

Este proyecto implementa una aplicación CRUD (Crear, Leer, Actualizar, Eliminar) completa y robusta para la gestión de personas y países. Utiliza un stack moderno con Angular para el frontend, Spring Boot para el backend (API RESTful) y PostgreSQL como base de datos persistente. Toda la infraestructura está diseñada para ser fácilmente desplegada y gestionada mediante Docker Compose.

---

## 🛠️ Tecnologías y Herramientas Utilizadas

### Frontend:

* **Angular 20**: Framework para la construcción de interfaces de usuario.
* **Angular Material**: Componentes UI de alta calidad.
* **TypeScript**: Lenguaje de programación.
* **Node.js**: Entorno de ejecución.
* **npm**: Gestor de paquetes.
* **VSCode**: Editor de código.

### Backend:

* **Spring Boot 3**: Framework Java para APIs RESTful.
* **Java 17+**: Lenguaje de programación.
* **Spring Data JPA**: Persistencia de datos.
* **Lombok**: Reducción de boilerplate.
* **Maven**: Gestor de dependencias.
* **IntelliJ IDEA**: IDE.

### Base de Datos:

* **PostgreSQL 16**: Sistema de bases de datos relacional.

### Contenedores y Orquestación:

* **Docker**: Contenedorización.
* **Docker Compose**: Orquestador de múltiples contenedores.

---

## 🏩 Diseño y Entidades del Modelo de Datos

### Persona

* `id (Long)`
* `nombre (String)`
* `edad (Integer)`
* `pais (Pais)` → Relación Many-to-One

### Pais

* `id (Long)`
* `nombre (String)`

---

## 🧹 Estructura del Proyecto

```
.
├── backend/
│   ├── src/main/java/.../controller
│   ├── src/main/java/.../entity
│   ├── src/main/java/.../repository
│   ├── src/main/java/.../service
│   ├── src/main/resources/application.properties
│   └── pom.xml
├── frontend/
│   ├── src/app/
│   │   ├── services/
│   │   ├── components/
│   │   └── ...
│   └── angular.json
├── assets/
├── docker-compose.yml
└── README.md
```

---

## 🚀 Cómo Ejecutar el Proyecto (con Docker Compose)

### Clonar el Repositorio:

```bash
git clone https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20.git
cd CRUD-Fullstack-SpringBoot-3-Angular-20
```

### Verificar Configuraciones:

#### `backend/src/main/resources/application.properties`

```properties
spring.datasource.url=jdbc:postgresql://db:5432/mydb
spring.datasource.username=admin
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

#### `frontend/src/app/services/*.service.ts`

```typescript
private apiUrl = 'http://localhost:8080/api/v1';
```

### CORS en Backend:

Asegúrate de tener en los controladores:

```java
@CrossOrigin(origins = "http://localhost:4200", maxAge = 3600)
```

### Construir y Levantar los Contenedores:

```bash
docker-compose up -d --build
```

* `up`: Crea y levanta servicios.
* `-d`: Modo background.
* `--build`: Reconstruye las imágenes.

### Verificar Contenedores:

```bash
docker ps
```

---

## 🌐 Acceder a la Aplicación

Abre el navegador en:

```
http://localhost:4200
```

---

## 📊 Desarrollo y Solución de Problemas Clave

### 1. Docker Compose

Todo orquestado en `docker-compose.yml`. Entorno reproducible.

### 2. Problemas de CORS

Resuelto con la anotación `@CrossOrigin` en controladores REST.

### 3. Sincronización de Estructura JSON

#### Problema

El frontend enviaba `{ paisId: X }` pero el backend esperaba `{ pais: { id: X } }`.

#### Solución

* En `persona.ts`: Usar `pais?: Pais;`, eliminar `paisId?: number;`
* En `pais.ts`: Usar `{ id: number; nombre: string; }`
* En el formulario, usar:

```html
formGroupName="pais" formControlName="id"
```

* En `persona-form.ts`: Eliminar transformación. Enviar el objeto como está.

Esto garantizó compatibilidad entre frontend y backend para operaciones CRUD.

---
## 📦 Ejemplo de Respuesta JSON - GET /api/v1/personas

Este es un ejemplo de la respuesta JSON al consumir el endpoint de obtención de personas:

```json
[
  {
    "id": 1,
    "nombre": "Juan Perez",
    "edad": 30,
    "pais": {
      "id": 1,
      "nombre": "Chile"
    }
  },
  {
    "id": 2,
    "nombre": "Maria Lopez",
    "edad": 25,
    "pais": {
      "id": 1,
      "nombre": "Chile"
    }
  },
  {
    "id": 3,
    "nombre": "Carlos Garcia",
    "edad": 40,
    "pais": {
      "id": 2,
      "nombre": "Argentina"
    }
  },
  {
    "id": 4,
    "nombre": "Ana Diaz",
    "edad": 35,
    "pais": {
      "id": 3,
      "nombre": "Peru"
    }
  }
]

```
## 📸 Demostración del CRUD

A continuación, se muestran capturas de pantalla del flujo de la aplicación.

### 🏠 Dashboard Inicial
La pantalla de bienvenida al sistema, desde donde puedes navegar para gestionar personas o ver países.

![Dashboard Inicial](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-Dashboard.png)

---

### 👥 Vista de Personas
Listado de todas las personas registradas, con opciones para buscar, crear, editar y eliminar.

![Vista Personas](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-CrearPersona-Resultado-png.png)

---

### ➕ Crear Persona (Formulario)
Formulario para añadir una nueva persona al sistema, ingresando nombre, edad y seleccionando un país.

![Crear Persona Formulario](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-CrearPersona-png.png)

---

### ✅ Crear Persona (Resultado)
La tabla de personas después de añadir un nuevo registro.

![Crear Persona Resultado](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-CrearPersona-Resultado-png.png)

---

### ✏️ Editar Persona (Formulario)
Formulario para modificar los datos de una persona existente.

![Editar Persona Formulario](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-Actualizar-.png)

---

### 📝 Editar Persona (Resultado)
La tabla de personas después de actualizar un registro.

![Editar Persona Resultado](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-Actualizar-Resultado.png)

---

### 🗑️ Confirmación de Eliminación
Cuadro de diálogo de confirmación antes de eliminar un registro de persona.

_(Puedes agregar una captura aquí si la tienes)_

---

### ❌ Eliminar Persona (Resultado)
La tabla de personas después de eliminar un registro.

![Eliminar Persona Resultado](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-Eliminar-Resultado-.png)

---

### 🌍 Vista de Países
Listado de todos los países disponibles en el sistema.

![Vista Países](https://github.com/Gleisk78/CRUD-Fullstack-SpringBoot-3-Angular-20/blob/master/Assets/CRUD-Fullstack-paises-.png)

---

### 📜 Logs de Docker Desktop
Muestra el estado de los contenedores y los logs del backend durante la ejecución.

_(Agrega aquí si tienes una captura específica de los logs)_

---

### 📁 Estructura de Paquetes del Backend
Vista de la organización de las carpetas del código Java en el backend.

_(Puedes agregar una imagen de la estructura desde tu IDE si lo deseas)_

---

## 📞 Contacto

Si tienes alguna pregunta o encuentras algún problema, no dudes en contactarme.
