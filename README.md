# NorthwindWeb

Aplicación de gestión comercial basada en la base de datos Northwind. Integra una interfaz ASP.NET Core MVC con una API REST y servicios gRPC para administrar información y consultar productos y pedidos.

## Funcionalidades

- Inicio y cierre de sesión, con almacenamiento del usuario y rol en sesión.
- Gestión de productos, clientes, proveedores, transportistas y usuarios.
- Consulta de productos por categoría o proveedor mediante gRPC.
- Consulta de pedidos por cliente o rango de fechas mediante gRPC.
- Panel de inicio y documentación de la API con Swagger.

## Tecnologías y estructura

C# · .NET 8 · ASP.NET Core MVC · Web API · gRPC · SQL Server · ADO.NET · Razor · Bootstrap · jQuery

| Carpeta | Contenido |
| --- | --- |
| `NorthwindWebMvc/` | Interfaz web y consumo de los servicios. |
| `NorthwindWebApi/` | API REST y acceso a datos. |
| `NorthwindgRPC/` | Servicios de consulta y contratos Protocol Buffers. |
| `BD/` | Scripts de la base de datos y procedimientos almacenados. |

## Instalación y configuración

Requiere **SDK de .NET 8** y **SQL Server**. La configuración incluida utiliza autenticación de Windows y una instancia local (`Server=.`).

```bash
git clone https://github.com/thoonidev/NorthwindWeb.git
cd NorthwindWeb
dotnet restore NorthwindWeb.sln
dotnet dev-certs https --trust
```

1. Ejecuta en SQL Server `BD/northwind.sql` y luego `BD/northwind_sp.sql`. **El primer script elimina la base `Northwind` si ya existe y la vuelve a crear.**
2. Ajusta `ConnectionStrings:sql` en `NorthwindWebApi/appsettings.json` a tu instancia.
3. Ajusta también la cadena `cadena` en `NorthwindgRPC/Services/ProductoService.cs` y `OrderService.cs`; actualmente está definida directamente en ambos archivos.
4. Mantén `ApiSettings:BaseUrl` en `NorthwindWebMvc/appsettings.json` con el valor `https://localhost:7226/`. Los controladores MVC también contienen direcciones fijas de la API y de gRPC; si cambias los puertos, actualízalas.

## Ejecución

Desde la raíz del repositorio, inicia cada componente en una terminal diferente:

```bash
dotnet run --project NorthwindWebApi --launch-profile https
```

```bash
dotnet run --project NorthwindgRPC --launch-profile https
```

```bash
dotnet run --project NorthwindWebMvc --launch-profile https
```

| Servicio | Dirección |
| --- | --- |
| Aplicación web | `https://localhost:7017` |
| Swagger de la API | `https://localhost:7226/swagger` |
| Servicio gRPC | `https://localhost:7075` |

Inicia sesión con uno de los usuarios de ejemplo definidos al final de `BD/northwind.sql`. Cambia sus credenciales antes de utilizar el proyecto fuera de un entorno de práctica.

Para compilar toda la solución:

```bash
dotnet build NorthwindWeb.sln
```
