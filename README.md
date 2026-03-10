# Spring Boot Microservices Platform

Proyecto backend desarrollado con **Java 17 y Spring Boot 3**, basado en una arquitectura de **microservicios**.  
El sistema implementa autenticación con **JWT**, autorización por roles y gestión de productos y órdenes, integrando servicios de configuración centralizada, descubrimiento de servicios y seguridad.

## Arquitectura

La plataforma está compuesta por varios microservicios independientes que se comunican entre sí mediante APIs REST.

Microservicios incluidos:

- **ms-auth** → Autenticación y autorización de usuarios mediante JWT
- **ms-productos** → Gestión de productos
- **ms-ordenes** → Gestión de órdenes de compra
- **eureka-server** → Registro y descubrimiento de microservicios
- **config-server** → Configuración centralizada de los servicios

## Funcionalidades principales

### Autenticación y Autorización

- Registro de usuarios
- Login con generación de **JWT**
- Autorización basada en roles:
  - SUPERADMIN
  - ADMIN
  - USER
- Validación de tokens entre microservicios

### Gestión de Productos

Operaciones CRUD para productos:

- Crear producto
- Listar productos
- Actualizar producto
- Eliminar producto

Solo usuarios con rol **ADMIN o SUPERADMIN** pueden acceder.

### Gestión de Órdenes

- Creación de órdenes por usuarios
- Visualización de órdenes por administradores
- Validación de productos antes de crear órdenes

## Infraestructura y herramientas

Este proyecto utiliza varias herramientas comunes en arquitecturas de microservicios:

- **Spring Boot 3**
- **Spring Security**
- **JWT**
- **Spring Cloud Eureka**
- **Spring Cloud Config Server**
- **HashiCorp Vault**
- **Maven**
- **JUnit**
- **Mockito**
- **Jacoco**
- **SonarCloud**

## Testing

El proyecto incluye:

- Pruebas unitarias con **JUnit**
- Mocking con **Mockito**
- Análisis de cobertura con **Jacoco**

## Estructura del repositorio
