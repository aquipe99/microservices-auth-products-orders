# 🚀 Microservices Auth Products Orders

Plataforma de microservicios desarrollada con **Java 17**, **Spring Boot 3** y **Spring Cloud**, implementando autenticación mediante **JWT**, autorización basada en roles, configuración centralizada, descubrimiento de servicios, gestión segura de secretos y un **API Gateway** como punto único de entrada.

---

# 📌 Objetivo

El objetivo de este proyecto es demostrar la implementación de una arquitectura de microservicios utilizando el ecosistema **Spring Cloud**, aplicando buenas prácticas de seguridad, separación de responsabilidades y administración centralizada de la infraestructura.

---

# ✨ Características

- Arquitectura basada en Microservicios
- API Gateway
- Service Discovery con Eureka Server
- Configuración centralizada mediante Config Server
- Gestión segura de secretos utilizando HashiCorp Vault
- Autenticación con JWT
- Autorización basada en roles
- CRUD de Productos
- Gestión de Órdenes
- Integración con PostgreSQL
- Testing con JUnit y Mockito
- Calidad de código con JaCoCo y SonarCloud

---

# 🛠 Tecnologías

## Backend

- Java 17
- Spring Boot 3

## Seguridad

- Spring Security
- JWT

## Spring Cloud

- Eureka Server
- Config Server
- Spring Cloud Gateway

## Base de Datos

- PostgreSQL

## Gestión de Secretos

- HashiCorp Vault

## Testing

- JUnit 5
- Mockito

## Calidad de Código

- JaCoCo
- SonarCloud

## Build Tool

- Maven

---

# 🏛 Arquitectura

La solución está compuesta por múltiples microservicios independientes, cada uno responsable de una parte específica del negocio.

```
                   Cliente
                      │
                      ▼
               API Gateway
                      │
      ┌───────────────┼───────────────┐
      ▼               ▼               ▼
  ms-auth      ms-productos      ms-ordenes
      │               │               │
      └───────────────┼───────────────┘
                      ▼
                 PostgreSQL


Infraestructura

• Eureka Server
• Config Server
• HashiCorp Vault
```

Cada servicio puede evolucionar de forma independiente manteniendo una arquitectura modular y escalable.

---

# 📦 Microservicios

## API Gateway

Punto único de entrada para todas las solicitudes del sistema.

Responsabilidades:

- Enrutamiento de peticiones
- Centralización del acceso
- Simplificación del consumo de la API

Puerto:

```
8080
```

---

## ms-auth

Responsable de la autenticación y autorización.

Funcionalidades:

- Registro de usuarios
- Login
- Generación de JWT
- Validación de credenciales
- Protección de endpoints

Roles implementados:

- SUPERADMIN
- ADMIN
- USER

---

## ms-productos

Responsable de la administración del catálogo de productos.

Operaciones principales:

- Crear productos
- Actualizar productos
- Consultar productos
- Eliminar productos

Acceso permitido para:

- ADMIN
- SUPERADMIN

---

## ms-ordenes

Responsable de la gestión de órdenes.

Operaciones:

- Registrar órdenes
- Consultar órdenes
- Validar productos antes del registro

---

# 🔄 Flujo del sistema

1. El cliente realiza login mediante el API Gateway.
2. El Gateway redirige la petición al microservicio de autenticación.
3. El microservicio genera un JWT válido.
4. El cliente utiliza ese JWT para consumir los demás servicios.
5. Todas las solicitudes ingresan por el Gateway.
6. Los microservicios obtienen su configuración desde Config Server.
7. Las credenciales sensibles son administradas mediante Vault.
8. Eureka mantiene registrado el estado de todos los servicios.

---

# 🔗 Endpoints principales

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| POST | /apis/codigo/auth/login | Iniciar sesión |
| POST | /apis/codigo/auth/register | Registrar usuario |
| GET | /apis/codigo/productos | Obtener productos |
| POST | /apis/codigo/productos | Crear producto |
| GET | /apis/codigo/ordenes | Consultar órdenes |
| POST | /apis/codigo/ordenes | Registrar orden |

---

# ▶️ Ejecución del proyecto

Se recomienda iniciar los servicios en el siguiente orden:

1. HashiCorp Vault
2. Config Server
3. Eureka Server
4. ms-auth
5. ms-productos
6. ms-ordenes
7. API Gateway

---

# 🌐 Puertos utilizados

| Servicio | Puerto |
|----------|--------|
| API Gateway | 8080 |
| ms-auth | 8081 |
| ms-productos | 8082 |
| ms-ordenes | 8083 |
| Config Server | 8888 |
| Eureka Server | 8761 |
| HashiCorp Vault | 8200 |

---

# 🧪 Testing

El proyecto incorpora pruebas unitarias utilizando:

- JUnit 5
- Mockito

Además se utiliza:

- JaCoCo para cobertura de código
- SonarCloud para análisis de calidad

---

# 📚 Conceptos aplicados

Durante el desarrollo de este proyecto se implementaron conocimientos relacionados con:

- Arquitectura de Microservicios
- Spring Cloud
- Spring Security
- JWT
- API Gateway
- Eureka Server
- Config Server
- HashiCorp Vault
- Arquitectura desacoplada
- APIs REST
- Seguridad basada en roles

---

# 🚀 Próximas mejoras

- Contenerización completa mediante Docker
- Docker Compose para toda la plataforma
- Balanceo de carga utilizando Eureka (`lb://`)
- Despliegue en Kubernetes
- Observabilidad con Prometheus y Grafana
- Integración de Apache Kafka para comunicación asíncrona

---

# 📊 Estado del proyecto

✅ Proyecto funcional.

Desarrollado como práctica para fortalecer conocimientos en arquitecturas de microservicios utilizando Spring Cloud y Spring Security.

---

# 👨‍💻 Autor

**Alex Choque**

Java Backend Developer

Tecnologías principales:

- Java
- Spring Boot
- Spring Cloud
- Spring Security
- JWT
- PostgreSQL
- Docker
- Kubernetes

GitHub:

https://github.com/aquipe99
