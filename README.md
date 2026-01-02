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

<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">


# Clase Resources.Designer.cs

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

# Clase Settings.Designer.cs


---

## 📌 Descripción

- La clase **`Settings`** es **auto-generada** por Visual Studio mediante el **Settings Designer**.  
- Su propósito es proveer acceso **fuertemente tipado** a configuraciones de la aplicación y del usuario.  
- Se basa en el archivo **`Settings.settings`** dentro de la carpeta `Properties`.  
- **No debe editarse manualmente**, ya que cualquier cambio se perderá al regenerar el archivo.

---

## 🛠️ Funcionalidad principal

- **`Default`**  
  - Devuelve una instancia única (`singleton`) de la clase `Settings`.  
  - Se utiliza para acceder a las configuraciones definidas.  

- **Configuraciones definidas:**
  - `UserName` → Nombre de usuario (configuración de usuario).  
  - `CommandTimeout` → Tiempo de espera para comandos (valor por defecto: `10`).  
  - `CommandTimeoutBulk` → Tiempo de espera para operaciones masivas (valor por defecto: `250`).  
  - `S3AccessKey`, `S3Secret`, `S3BucketName`, `S3ClientName` → Credenciales y configuración de acceso a Amazon S3.  
  - `UnitTimeout1` → Tiempo de espera de unidad (valor por defecto: `4`).  
  - `APIToken` y `APITokenDate` → Token de autenticación y fecha de emisión.  
  - `DB` → Cadena de conexión a base de datos PostgreSQL (valor por defecto incluye host, usuario y contraseña).  
  - `Server1` → Servidor principal (valor por defecto: `units-admin.mx.questarauto.com`).  
  - `UnitTimeout2` → Tiempo de espera adicional de unidad (valor por defecto: `5`).  
  - `DisconnectedTime` → Tiempo máximo de desconexión permitido (valor por defecto: `120`).  

---

## ⚙️ Atributos importantes

- `[CompilerGenerated]` → indica que el código fue generado por el compilador.  
- `[GeneratedCode]` → señala que el archivo fue generado automáticamente por Visual Studio.  
- `[UserScopedSetting]` → configuración específica de cada usuario.  
- `[ApplicationScopedSetting]` → configuración compartida por toda la aplicación.  
- `[DefaultSettingValue]` → valor por defecto de cada propiedad.  
- `[DebuggerNonUserCode]` → evita que el depurador entre en este código.  

---

## 🚀 Uso en el proyecto

Ejemplo de cómo acceder y modificar configuraciones:

```csharp
// Obtener valores
string usuario = Monitor2._0.Properties.Settings.Default.UserName;
string conexionDB = Monitor2._0.Properties.Settings.Default.DB;

// Modificar valores de usuario
Monitor2._0.Properties.Settings.Default.UserName = "admin";
Monitor2._0.Properties.Settings.Default.S3AccessKey = "mi-access-key";
Monitor2._0.Properties.Settings.Default.Save(); // Guardar cambios


# Archivo ClickOnceProfile.pubxml

---

## 📌 Descripción

- Define la configuración de publicación del proyecto mediante **ClickOnce**, una tecnología de despliegue para aplicaciones de escritorio en .NET.  
- Permite especificar:
  - Versión de la aplicación.
  - Directorio y protocolo de publicación.
  - Archivos incluidos en el paquete.
  - Dependencias necesarias en el cliente (bootstrapper packages).
- Se utiliza cuando se publica la aplicación desde Visual Studio con la opción **Publish**.

---

## 🛠️ Configuración principal

- **ApplicationRevision:** `21` → número de revisión de la aplicación.  
- **ApplicationVersion:** `1.0.0.*` → versión de la aplicación, con incremento automático en la revisión.  
- **Configuration:** `Release` → se publica en modo Release.  
- **Platform:** `x64` → compilación para arquitectura de 64 bits.  
- **PublishDir:** `bin\Release\net8.0-windows\app.publish\` → carpeta donde se generan los archivos publicados.  
- **PublishUrl / InstallUrl:** `\\DESKTOP-QGQAB74\Monitor2.0\` → ruta UNC donde se distribuye la aplicación.  
- **PublishProtocol:** `ClickOnce` → protocolo de publicación.  
- **TargetFramework:** `net8.0-windows` → framework objetivo.  
- **CreateDesktopShortcut:** `True` → se crea acceso directo en el escritorio.  
- **UpdateEnabled:** `True` → habilita actualizaciones automáticas.  
- **UpdateMode:** `Foreground` → las actualizaciones se aplican al iniciar la aplicación.  

---

## 📂 Archivos incluidos en la publicación

El perfil asegura que ciertos archivos de configuración y recursos se incluyan en el paquete:

- `Config\CENTRO.txt`  
- `Config\GASP.txt`  
- `Config\GOLFO.txt`  
- `Config\NORTE.txt`  
- `Config\PACIFICO.txt`  
- `Config\Params Codes.txt`  
- `monkey_39003.ico`  

Cada archivo se marca con:
- **PublishState:** `Include` → se incluye en la publicación.  
- **IncludeHash:** `true` → se valida integridad mediante hash.  
- **FileType:** `File` → tipo de recurso.

---

## 📦 Paquetes bootstrapper

El perfil también define los paquetes que deben instalarse en el cliente antes de ejecutar la aplicación:

- **Microsoft.EdgeRuntime** → instala el runtime de **Edge WebView**.  
- **Microsoft.NetCore.DesktopRuntime.8.0.x64** → instala el runtime de **.NET Desktop 8.0.4 (x64)**.  

---

## 🚀 Objetivo del perfil

- Facilitar la distribución de la aplicación **Monitor2.0** mediante **ClickOnce**.  
- Garantizar que los usuarios finales tengan instaladas las dependencias necesarias.  
- Incluir archivos de configuración críticos y recursos visuales en el paquete de despliegue.  
- Permitir actualizaciones automáticas sin necesidad de reinstalación manual.

---
