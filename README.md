Biblioteca
/
README_ServiceTrack_Publico.md


# ServiceTrack

Plataforma full stack para gestionar solicitudes de soporte y servicios técnicos.

ServiceTrack está orientada a pequeñas empresas que necesitan registrar solicitudes, asignar responsables, controlar estados, mantener trazabilidad y consultar métricas operativas.

## Objetivo

Este proyecto forma parte de mi portafolio profesional y busca demostrar experiencia práctica en:

- desarrollo backend con ASP.NET Core;
- desarrollo frontend con Angular;
- arquitectura por capas;
- autenticación y autorización;
- reglas de negocio;
- persistencia con PostgreSQL;
- pruebas automatizadas;
- Docker y Docker Compose;
- integración y despliegue continuo;
- publicación en una VPS con HTTPS;
- monitoreo de disponibilidad.

## Funcionalidades principales

### Administrador

- Gestionar usuarios.
- Gestionar clientes.
- Gestionar categorías.
- Consultar todas las solicitudes.
- Asignar técnicos.
- Cambiar prioridades.
- Consultar métricas operativas.

### Técnico

- Consultar solicitudes asignadas.
- Cambiar el estado de una solicitud.
- Agregar comentarios.
- Registrar tiempo trabajado.
- Adjuntar evidencias.

### Cliente

- Crear solicitudes.
- Consultar sus solicitudes.
- Agregar comentarios.
- Adjuntar archivos.
- Evaluar el servicio recibido.

## Flujo de atención

```text
Nueva
  ↓
Asignada
  ↓
En progreso
  ↓
En espera
  ↓
Resuelta
  ↓
Cerrada
```

Prioridades disponibles:

```text
Baja
Media
Alta
Crítica
```

## Stack tecnológico

### Backend

- .NET 10
- ASP.NET Core Web API
- Entity Framework Core
- PostgreSQL
- FluentValidation
- JWT
- OpenAPI
- xUnit

### Frontend

- Angular
- TypeScript
- Angular Material
- SCSS
- Reactive Forms
- Standalone Components
- Signals

### Infraestructura

- Docker
- Docker Compose
- GitHub Actions
- GitHub Container Registry
- Caddy
- Uptime Kuma
- VPS Linux

## Arquitectura

El backend utiliza una arquitectura por capas.

```text
ServiceTrack.Api
        │
        ├── ServiceTrack.Application
        │
        └── ServiceTrack.Infrastructure
                    │
                    ├── ServiceTrack.Application
                    └── ServiceTrack.Domain

ServiceTrack.Application
        │
        └── ServiceTrack.Domain

ServiceTrack.Domain
        │
        └── Sin dependencias hacia otros proyectos
```

### ServiceTrack.Domain

Contiene entidades, enumeraciones, reglas de negocio, excepciones y objetos de valor.

No depende de la API, la base de datos ni otros detalles de infraestructura.

### ServiceTrack.Application

Contiene casos de uso, contratos, DTO, validaciones, servicios de aplicación e interfaces de repositorio.

Depende de `ServiceTrack.Domain`.

### ServiceTrack.Infrastructure

Contiene Entity Framework Core, PostgreSQL, repositorios, persistencia, almacenamiento de archivos y servicios externos.

Depende de `ServiceTrack.Application` y `ServiceTrack.Domain`.

### ServiceTrack.Api

Contiene endpoints, autenticación, autorización, middleware, OpenAPI y configuración de dependencias.

Depende de `ServiceTrack.Application` y `ServiceTrack.Infrastructure`.

### ServiceTrack.Tests

Contiene pruebas automatizadas para reglas de dominio, validaciones, casos de uso y endpoints principales.

## Estructura del repositorio

```text
servicetrack/
├── .github/
│   └── workflows/
├── backend/
│   ├── ServiceTrack.Api/
│   ├── ServiceTrack.Application/
│   ├── ServiceTrack.Domain/
│   ├── ServiceTrack.Infrastructure/
│   ├── ServiceTrack.Tests/
│   └── ServiceTrack.sln
├── frontend/
│   └── servicetrack-web/
├── deploy/
├── docs/
├── .gitignore
├── LICENSE
└── README.md
```

## Requisitos locales

- .NET SDK 10
- Node.js compatible con la versión de Angular
- npm
- Docker Desktop
- Git

## Ejecución local

### Backend

```powershell
cd .\backend

dotnet restore .\ServiceTrack.sln

dotnet build .\ServiceTrack.sln `
  --configuration Release `
  --no-restore

dotnet run `
  --project .\ServiceTrack.Api\ServiceTrack.Api.csproj
```

### Pruebas del backend

```powershell
cd .\backend

dotnet test .\ServiceTrack.sln `
  --configuration Release
```

### Frontend

```powershell
cd .\frontend\servicetrack-web

npm ci

npm start
```

La aplicación Angular estará disponible normalmente en:

```text
http://localhost:4200
```

### Build del frontend

```powershell
cd .\frontend\servicetrack-web

npm ci

npm run build
```