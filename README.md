# Gestión de Incidentes de Ciberseguridad

Aplicación web en **C# / ASP.NET Core MVC** para registrar y gestionar incidentes de ciberseguridad (phishing, ransomware) sobre los activos de una organización.

Obligatorio de **Programación 2** — Analista en Tecnologías de la Información, Universidad ORT Uruguay (2025). Desarrollado en equipo de 2.

## Funcionalidades

- **Login con manejo de sesión** y dos roles: administrador y operador.
- **Personas**: alta y listado de administradores y operadores.
- **Activos**: alta, listado, asociación a cuentas y detección de activos sin backup.
- **Cuentas**: alta y consulta de los activos de cada cuenta.
- **Incidentes**: registro de incidentes de tipo *phishing* y *ransomware*, con estado, impacto y probabilidad. La **severidad** (0–100) se calcula a partir del impacto y la probabilidad, y los ransomware la ajustan con reglas propias.

## Arquitectura

La solución está separada en capas:

| Proyecto | Responsabilidad |
|---|---|
| `Dominio` | Modelo de negocio y reglas: entidades, validaciones y la clase `Sistema`, que centraliza la lógica. |
| `Web` | ASP.NET Core MVC: controllers, vistas Razor y Bootstrap. |
| `GestionIncidentes` | Aplicación de consola para probar el dominio. |

El dominio usa **POO**: `Incidente` es una clase abstracta de la que heredan `Phishing` y `Ransomware`. `Ransomware` sobrescribe el cálculo de severidad (polimorfismo), y los incidentes implementan `IComparable` para ordenarse de mayor a menor severidad.

Los datos se guardan **en memoria** y se precargan al iniciar, con usuarios y activos de ejemplo.

## Tecnologías

C# · .NET 10 · ASP.NET Core MVC · Razor · Bootstrap · Session

## Cómo ejecutarlo

Requiere el [SDK de .NET 10](https://dotnet.microsoft.com/download).

```bash
git clone https://github.com/fiorenzo-dev/gestion-incidentes.git
cd gestion-incidentes
dotnet run --project Web
```

Después abrí la URL que muestra la consola. Hay usuarios de prueba en la precarga de `Dominio/Sistema.cs`, por ejemplo `juan.perez@gmail.com` / `Juan123` (administrador).
