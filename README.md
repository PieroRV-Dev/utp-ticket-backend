#UTP TICKET BACKEND

Backend de `UTP-TICKET`, la plataforma que vamos a construir para gestionar eventos, venta de entradas, control de accesos, promotores, colaboradores y operaciones internas desde una sola API.

La idea de este proyecto es consolidar en un único servicio todo lo necesario para operar la experiencia completa de un evento: desde la publicación y consulta de eventos, hasta el checkout, la emisión de tickets, la validación por QR, la gestión de perfiles, permisos, wallet y reportes operativos.

## Objetivo del proyecto

Este proyecto se crea para dejar una base sólida y escalable sobre la que podamos seguir creciendo `UTP-TICKET`.

La API quedará orientada a cubrir estos frentes:

- autenticación de usuarios con credenciales y Google
- gestión de perfiles y datos personales
- administración de eventos
- configuración y emisión de tickets
- checkout y creación de órdenes
- integración de pagos con Mercado Pago y Yape
- validación de entradas por QR y control de acceso
- administración de colaboradores, roles y permisos
- gestión de promotores y atribuciones de venta
- wallet y movimientos transaccionales
- envío de correos y notificaciones base
- documentación OpenAPI para integraciones y pruebas

## Stack definido

El proyecto queda montado con la siguiente base tecnológica:

- `Java 17`
- `Spring Boot 3.3.6`
- `Spring Web`
- `Spring Security`
- `Spring OAuth2 Resource Server`
- `Spring Data JDBC`
- `MySQL`
- `Spring Mail`
- `Thymeleaf`
- `springdoc-openapi` para Swagger
- `Caffeine` para caché
- `ZXing` para generación/lectura de QR
- `Apache POI` para manejo de archivos Excel
- `Thumbnailator` para procesamiento de imágenes
- `JWT` para autenticación basada en tokens

## Alcance funcional esperado

La API queda organizada para soportar módulos como los siguientes:

- `auth`: login, refresh token, registro y autenticación social
- `users/profile/personal`: datos de usuario, perfil público e imagen
- `events`: administración de eventos y consulta pública
- `tickets`: tipos de tickets, emisión, lectura y validación
- `checkout` y `orders`: flujo de compra, órdenes y respuesta de pago
- `payment`: integración con procesadores de pago
- `access`: admisión, escaneo QR y control de ingreso
- `collaborators` y `roles`: permisos por evento y operación interna
- `promoters`: registro, atribución y seguimiento comercial
- `wallet`: solicitudes y movimientos financieros internos
- `sales`: reportes y vistas de ventas
- `ubications`: departamentos, provincias y distritos
- `notifications/email`: plantillas y envío de correo

## Estructura base del proyecto

```text
src/
  main/
    java/com/pe/utp-ticket/api/
      core/                 # configuración, seguridad, AOP y utilidades
      gateway/              # controladores HTTP por contexto
      transactions/         # lógica de negocio y acceso a datos
    resources/
      application.properties
      application-dev.properties
      application-int.properties
      templates/email/
      sql-scripts/
      excel/
  test/
```

## Convención de capas

La implementación se apoya en una separación clara de responsabilidades:

- `gateway`: expone endpoints REST
- `transactions/.../business`: contiene los casos de uso y reglas del dominio
- `transactions/.../repository`: acceso a datos y entidades
- `core`: configuración transversal, seguridad, utilidades, manejo de errores y aspectos

## Perfiles de ejecución

El proyecto queda preparado para trabajar con perfiles:

- `dev`: desarrollo local
- `int`: integración
- `prod`: producción

Actualmente la aplicación parte desde el contexto:

```text
/api-ticket/v1
```

## Variables y configuración esperada

Para dejar el proyecto listo para trabajar de forma segura, la configuración sensible debe venir por variables de entorno o por archivos de propiedades fuera del repositorio.

La API necesita, como mínimo, configurar:

- conexión a `MySQL`
- secreto JWT
- credenciales SMTP
- credenciales OAuth de Google
- credenciales de Mercado Pago
- dominio y políticas de cookies
- rutas de almacenamiento para imágenes y vouchers
- URL del frontend
- orígenes permitidos por CORS

## Puesta en marcha local

### 1. Requisitos

- `JDK 17`
- `Maven` o uso del wrapper `mvnw`
- `MySQL` disponible localmente

### 2. Configurar base de datos

Crear una base, por ejemplo:

```sql
CREATE DATABASE ticketdbv2;
```

Luego completar las propiedades del perfil `dev` con las credenciales correctas y cargar los scripts necesarios si aplica.

## 3. Ejecutar el proyecto

Con el wrapper de Maven:

```bash
./mvnw spring-boot:run
```

En Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Para forzar un perfil:

```powershell
.\mvnw.cmd spring-boot:run "-Dspring-boot.run.profiles=dev"
```

## 4. Documentación de endpoints

Con la aplicación levantada, la documentación quedará disponible en:

- `http://localhost:8080/api-ticket/v1/swagger-ui.html`
- `http://localhost:8080/api-ticket/v1/api-docs`

## Flujo funcional que buscamos dejar cubierto

La plataforma quedará preparada para soportar este recorrido:

1. un organizador crea y configura un evento
2. se definen tipos de ticket, cupos, reglas y condiciones
3. un usuario consulta eventos públicos
4. el usuario inicia checkout y genera una orden
5. la API procesa el pago con el proveedor configurado
6. se emiten tickets con su identificación correspondiente
7. se genera o consulta el QR del acceso
8. el personal autorizado valida el ingreso en puerta
9. el equipo administrativo revisa ventas, promotores, wallet y movimientos

## Seguridad y operación

La base del proyecto contempla:

- autenticación con JWT
- refresh token por cookie
- integración con Google Sign-In
- validación de permisos por roles y alcances
- configuración CORS por entorno
- manejo centralizado de excepciones
- trazabilidad vía logs y aspectos

## Estado esperado del proyecto

Al cerrar esta primera etapa, la API debe quedar como el backend principal de UTP Ticket, lista para servir como núcleo operativo de la plataforma web y de futuras integraciones administrativas, móviles o de validación en campo.

## Próximos pasos naturales

- completar documentación funcional por módulo
- externalizar completamente secretos y configuraciones sensibles
- incorporar migraciones versionadas de base de datos
- ampliar cobertura de pruebas
- agregar pipeline de build y despliegue
- documentar contratos de integración con frontend y webhooks

## Nombre del artefacto

- `groupId`: `com.pe.utp-ticket`
- `artifactId`: `limonApi`
- `version`: `0.0.1-BETA`
