# DocMonitor2.0
Documento técnico

# Proyecto .NET Core

Este proyecto es una aplicación de escritorio en **.NET Core/WinForms** con integración de servicios web y librerías externas.  
El archivo `*.csproj` cumple el mismo rol que el `pom.xml` en proyectos Maven/Spring Boot: define dependencias, configuración de compilación y recursos.

---

## 📌 Características principales

- **Tipo de proyecto:** Aplicación de escritorio (WinForms) con capacidades de red y servicios.  
- **Framework:** .NET Core (versión especificada en `<TargetFramework>` dentro del `.csproj`).  
- **Recursos incluidos:**
  - Archivos de configuración (`.txt`, `.json`) en carpetas `Config` y `FW`.
  - Íconos (`.ico`) y recursos embebidos (`.resx`, `Settings.settings`).
  - Configuraciones específicas por cliente (`Config\Clients\...`).
- **Dependencias externas:**
  - **AWS SDK (S3)** → integración con almacenamiento en la nube.
  - **CsvHelper** → manejo de archivos CSV.
  - **GMap.NET (Core/WinForms)** → mapas y visualización.
  - **Microsoft.AspNetCore.Cors** → soporte para CORS.
  - **Microsoft.Web.WebView2** → navegador embebido basado en Edge.
  - **Newtonsoft.Json** → serialización JSON.
  - **Npgsql / SqlClient / SQLite** → acceso a bases de datos PostgreSQL, SQL Server y SQLite.
  - **NPOI** → manejo de archivos Excel.
  - **SlackAPI / Twilio** → integración con servicios de mensajería.
  - **System.ServiceModel (WCF)** → comunicación distribuida (HTTP, TCP, NamedPipe, seguridad).
- **Referencias directas:**
  - `ConnectionModules.dll` → librería externa utilizada por el proyecto.

---

## 📂 Estructura de carpetas

- `Config\Pemex Codes\` → códigos de configuración específicos.  
- `Config\Internal\` → configuraciones internas (ej. buckets S3).  
- `Config\Clients\` → configuraciones por cliente (ej. PEMEX, SAPI, SHACMAN, MBZ, COPPEL, SEDENA, UNNE, TRAXION).  
- `FW\` → archivos de firmware en formato `.json`.  
- `Properties\` → recursos (`Resources.resx`) y configuraciones (`Settings.settings`).  

---

## 🚀 Objetivo del proyecto

- Proveer una aplicación de escritorio con soporte para:
  - Configuración dinámica por cliente.
  - Integración con servicios en la nube (AWS S3).
  - Conexión a múltiples bases de datos.
  - Visualización de mapas y datos.
  - Comunicación con APIs externas (Slack, Twilio).
  - Uso de WCF para servicios distribuidos.

---

## 🔧 Cómo identificar el tipo de proyecto

El tipo exacto de proyecto se define en la primera línea del `.csproj`:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">


# Clase Resources.Designer.cs

Este archivo corresponde a la clase **`Resources`** ubicada en:

```xml
C:\Users\Numaris Traffilog\source\repos\Monitor2.0\Properties\Resources.Designer.csproj


---

## 📌 Descripción

- La clase **`Resources`** es **auto-generada** por Visual Studio mediante la herramienta **StronglyTypedResourceBuilder**.  
- Su propósito es proveer acceso **fuertemente tipado** a recursos embebidos en el proyecto, como:
  - Cadenas localizadas (strings).
  - Archivos `.resx` (recursos de internacionalización).
  - Íconos, imágenes y otros recursos asociados.  
- **No debe editarse manualmente**, ya que cualquier cambio se perderá al regenerar el archivo.

---

## 🛠️ Funcionalidad principal

- **`ResourceManager`**  
  - Devuelve una instancia en caché de `System.Resources.ResourceManager`.  
  - Se utiliza para buscar y cargar recursos embebidos en el ensamblado.  

- **`Culture`**  
  - Permite sobrescribir la cultura (`CultureInfo`) utilizada en las búsquedas de recursos.  
  - Útil para cambiar dinámicamente el idioma de la aplicación.  

---

## ⚙️ Atributos importantes

- `[GeneratedCode]` → indica que el archivo fue generado automáticamente por una herramienta.  
- `[DebuggerNonUserCode]` → evita que el depurador entre en este código.  
- `[CompilerGenerated]` → señala que el compilador generó parte del código.  
- `[SuppressMessage]` → suprime advertencias específicas de análisis estático.  

---

## 🚀 Uso en el proyecto

1. Los recursos se definen en el archivo **`Resources.resx`** dentro de la carpeta `Properties`.  
2. Al compilar, Visual Studio genera automáticamente esta clase para acceder a dichos recursos.  
3. Ejemplo de uso en código:

```csharp
// Obtener un recurso localizado
string mensaje = Monitor2._0.Properties.Resources.MiCadena;

// Cambiar cultura para internacionalización
Monitor2._0.Properties.Resources.Culture = new System.Globalization.CultureInfo("es-MX");


