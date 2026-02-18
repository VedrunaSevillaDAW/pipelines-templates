# Pipelines automatizadas

Repositorio de plantillas de automatización para crear proyectos base desde GitHub Actions.

## Qué es este repo

Este repositorio no contiene una aplicación final.  
Contiene **workflows reutilizables/manuales** para que un alumno pueda generar un repositorio nuevo ya inicializado:

- Proyecto **Astro**
- Proyecto **Spring Boot** (con opciones de BBDD y componentes)

## Que incluye

- `.github/workflows/create-astro-project.yml`
- `.github/workflows/create-spring-project.yml`

Cada workflow:
- Crea un repo nuevo en `VedrunaSevillaDAW/<nombre-proyecto>`
- Genera el esqueleto del proyecto
- Añade `Dockerfile` y `.dockerignore`
- Hace commit y push inicial en `main`

## Requisitos previos

Antes de ejecutarlo, necesitas:

- Permiso para ejecutar Actions en este repositorio
- `Environment` llamado `tst`
- Secret `PAT_CREATE_REPO_1` dentro de `tst` con permisos para crear repositorios (scope `repo`)

Si falta ese secret, el pipeline fallará al inicio.

## Cómo usarlo (paso a paso)

1. Entra en la pestaña **Actions** de este repositorio.
2. Elige el workflow que quieras lanzar:
   - `Astro Project Initializer`
   - `Spring Boot Project Initializer`
3. Pulsa **Run workflow**.
4. Rellena los parámetros.
5. Espera a que termine la ejecución.
6. Ve al repo nuevo creado en la organización `VedrunaSevillaDAW`.

## Parámetros de cada workflow

### Astro Project Initializer

- `project`: nombre del repositorio/proyecto a crear.

### Spring Boot Project Initializer

- `project`: nombre del repositorio/proyecto.
- `bbdd`: `MySQL | PostgreSQL | MongoDB | Cassandra | NA`
- `redis`: incluir Redis (`true/false`)
- `elastic`: incluir Elasticsearch (`true/false`)
- `kafka`: incluir Kafka (`true/false`)
- `rabbit`: incluir RabbitMQ (`true/false`)
- `security`: incluir Spring Security (`true/false`)
- `servertype`: `Authorization | Resource | NA`

## Qué genera exactamente

### Para Astro

- Proyecto Astro base
- README inicial del proyecto
- Imagen Docker válida para servir el build estático con Nginx

### Para Spring Boot

- Proyecto generado desde Spring Initializr
- `application.yaml` con configuración según opciones elegidas
- Estructura de carpetas estilo arquitectura hexagonal
- Imagen Docker multi-stage para empaquetar y ejecutar la app

## Errores comunes

- `GH_TOKEN esta vacío`: revisa que `PAT_CREATE_REPO_1` existe en el environment `tst`.
- Error al crear repo: verifica que el token tenga permisos `repo` y que el nombre no exista ya.
- Fallo en build Docker: revisa logs del job para ver en qué paso falla la generación del proyecto.
