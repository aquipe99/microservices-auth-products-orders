# microservices-auth-products-orders

Proyecto backend desarrollado con **Java 17** y **Spring Boot 3**, basado en una arquitectura de microservicios.
El sistema implementa **autenticación con JWT**, **autorización por roles**, **gestión de productos y órdenes**, además de integrar **configuración centralizada**, **descubrimiento de servicios**, **gestión de secretos** y **API Gateway**.

---

## Descripción general

La plataforma está compuesta por varios microservicios independientes que se comunican entre sí mediante APIs REST.
Cada servicio tiene una responsabilidad específica, lo que permite una arquitectura modular, escalable y fácil de mantener.

Este proyecto fue desarrollado como práctica para fortalecer conocimientos en:

* Arquitectura de microservicios
* Seguridad con JWT
* Spring Cloud
* Configuración centralizada
* Gestión de secretos
* API Gateway
* Buenas prácticas de testing y calidad de código

---

## Arquitectura

La solución está compuesta por los siguientes microservicios y componentes de infraestructura:

* **ms-auth** → Autenticación y autorización de usuarios mediante JWT
* **ms-productos** → Gestión de productos
* **ms-ordenes** → Gestión de órdenes de compra
* **api-gateway** → Punto único de entrada para todos los servicios
* **eureka-server** → Registro y descubrimiento de microservicios
* **config-server** → Configuración centralizada de los servicios
* **vault** → Gestión segura de secretos y credenciales

---

## API Gateway

Se incorporó un **API Gateway** para centralizar el acceso a los microservicios.

### Función del Gateway

El Gateway permite:

* exponer un único punto de entrada al sistema
* enrutar peticiones a los microservicios correspondientes
* simplificar el consumo de la API
* preparar la arquitectura para futuros despliegues en la nube

### Punto de entrada

```text
http://localhost:8080
```

### Rutas configuradas

| Servicio  | Ruta                        |
| --------- | --------------------------- |
| Auth      | `/apis/codigo/auth/**`      |
| Productos | `/apis/codigo/productos/**` |
| Órdenes   | `/apis/codigo/ordenes/**`   |

Actualmente, el Gateway enruta a los microservicios mediante URLs locales directas para asegurar estabilidad en entorno local.

---

## Funcionalidades principales

## Autenticación y autorización

El microservicio `ms-auth` se encarga de la seguridad del sistema.

### Funcionalidades

* Registro de usuarios
* Login con generación de JWT
* Validación de credenciales
* Autorización basada en roles
* Protección de endpoints según permisos

### Roles implementados

* **SUPERADMIN**
* **ADMIN**
* **USER**

### Ejemplo de login

**Endpoint**

```http
POST /apis/codigo/auth/login
```

**Ejemplo de request**

```json
{
  "correo": "adminnuevo@gmail.com",
  "password": "adminnuevo123"
}
```

**Ejemplo de respuesta**

```json
{
  "accessToken": "JWT_TOKEN",
  "refreshToken": null
}
```

### Validación de tokens

Los tokens JWT se utilizan para proteger el acceso a los demás microservicios, permitiendo controlar qué operaciones puede realizar cada usuario según su rol.

---

## Gestión de productos

El microservicio `ms-productos` se encarga de la administración del catálogo de productos.

### Operaciones principales

* Crear producto
* Listar productos
* Actualizar producto
* Eliminar producto

### Restricciones

Solo usuarios con rol:

* **ADMIN**
* **SUPERADMIN**

pueden acceder a las operaciones de administración de productos.

### Acceso vía Gateway

```http
GET /apis/codigo/productos
Authorization: Bearer TU_TOKEN
```

---

## Gestión de órdenes

El microservicio `ms-ordenes` se encarga de la creación y consulta de órdenes de compra.

### Operaciones principales

* Crear órdenes
* Consultar órdenes
* Validar productos antes de registrar una orden

### Reglas generales

* Los usuarios pueden crear órdenes
* Los administradores pueden visualizar y gestionar órdenes
* Antes de crear una orden se valida la información de productos

### Acceso vía Gateway

```http
POST /apis/codigo/ordenes
Authorization: Bearer TU_TOKEN
```

---

## Infraestructura y herramientas

Este proyecto utiliza herramientas comunes en arquitecturas modernas de microservicios:

* **Java 17**
* **Spring Boot 3**
* **Spring Security**
* **JWT**
* **Spring Cloud Eureka**
* **Spring Cloud Config Server**
* **Spring Cloud Gateway**
* **HashiCorp Vault**
* **PostgreSQL**
* **Maven**

---

## Testing y calidad de código

El proyecto incluye prácticas de calidad para asegurar mejor mantenimiento y confiabilidad.

### Testing

* Pruebas unitarias con **JUnit**
* Mocking con **Mockito**

### Calidad

* Análisis de cobertura con **Jacoco**
* Inspección continua con **SonarCloud**

---

## Flujo general del sistema

1. El cliente realiza login a través del API Gateway
2. El Gateway redirige la petición al microservicio `ms-auth`
3. `ms-auth` valida las credenciales y genera el token JWT
4. El cliente utiliza ese token para consumir productos y órdenes
5. Todas las peticiones ingresan por el Gateway
6. Los servicios usan Config Server, Eureka y Vault como parte de la infraestructura

---

## Orden de ejecución

Para ejecutar el sistema en entorno local, se recomienda iniciar los servicios en este orden:

1. **Vault**
2. **Config Server**
3. **Eureka Server**
4. **ms-auth**
5. **ms-productos**
6. **ms-ordenes**
7. **api-gateway**

---

## Puertos utilizados

| Servicio      | Puerto |
| ------------- | ------ |
| api-gateway   | 8080   |
| ms-auth       | 8081   |
| ms-productos  | 8082   |
| ms-ordenes    | 8083   |
| config-server | 8888   |
| eureka-server | 8761   |
| vault         | 8200   |

---

## Configuración

La solución utiliza:

* **Config Server** para centralizar propiedades de configuración
* **Vault** para almacenar secretos y credenciales sensibles
* **Eureka** para el registro de servicios
* **API Gateway** para centralizar el acceso a la plataforma

---

## Pruebas manuales

El sistema puede probarse con herramientas como **Postman**, utilizando el Gateway como punto de entrada.

### Ejemplos de pruebas

* Login exitoso
* Consulta de productos
* Creación de órdenes

Todas las pruebas se realizan a través de:

```text
http://localhost:8080
```

---

## Estructura del repositorio

Una posible estructura del proyecto es la siguiente:

```text
microservices-auth-products-orders/
├── api-gateway
├── ms-auth
├── ms-productos
├── ms-ordenes
├── eureka-server
├── config-server
└── README.md
```

---

## Posibles mejoras

* Implementar balanceo completo mediante `lb://` usando Eureka
* Validar JWT directamente en el API Gateway
* Dockerizar todos los servicios
* Desplegar la solución en Azure
* Agregar monitoreo y observabilidad

---

## Objetivo del proyecto

Este proyecto busca demostrar conocimientos prácticos en:

* diseño de microservicios
* seguridad con JWT
* autorización por roles
* integración con Spring Cloud
* configuración centralizada
* gestión segura de secretos
* implementación de API Gateway
* pruebas y calidad de código

---

## Autor

Proyecto desarrollado como práctica profesional para fortalecer habilidades en desarrollo backend y arquitectura de microservicios.
