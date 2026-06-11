---
date: '2026-06-11'
description: Aprenda cómo extraer metadata de document streams usando GroupDocs.Redaction
  para .NET, cubriendo setup, code examples y practical applications.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Cómo extraer metadata de document streams usando GroupDocs.Redaction .NET
type: docs
url: /es/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Cómo extraer metadatos de flujos de documentos usando GroupDocs.Redaction .NET

¿Está cansado de extraer manualmente la información de los documentos o de lidiar con archivos grandes que ralentizan su flujo de trabajo? **Cómo extraer metadatos** rápidamente es un desafío común, y la biblioteca GroupDocs.Redaction para .NET ofrece una forma rápida y eficiente en memoria de recuperar los detalles del documento directamente desde flujos. En este tutorial, aprenderá cómo configurar la biblioteca, obtener el tipo de archivo, el recuento de páginas y el tamaño a partir de un flujo, y preparar una carpeta de salida para procesamiento adicional.

## Respuestas rápidas
- **¿Qué significa “extraer metadatos”?** Significa leer propiedades como el tipo de archivo, el recuento de páginas y el tamaño sin abrir el documento completo en memoria.  
- **¿Qué biblioteca maneja esto?** GroupDocs.Redaction para .NET proporciona una API nativa para la extracción de metadatos basada en flujos.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo procesar PDFs de más de 1 GB?** Sí – los flujos le permiten manejar archivos de hasta 2 GB sin cargar todo el archivo.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ y .NET 6+.

## Qué es la extracción de metadatos de flujos
La extracción de metadatos de flujos es el proceso de leer las propiedades del documento directamente desde un objeto `Stream`, evitando la carga completa del archivo y, por lo tanto, ahorrando memoria y tiempo de CPU. Esta técnica es ideal para procesamiento por lotes o servicios basados en la nube donde los recursos son limitados.

## Por qué usar GroupDocs.Redaction para la extracción de metadatos
GroupDocs.Redaction admite **más de 30 formatos de archivo** (incluidos PDF, DOCX, XLSX, PPTX y tipos de imagen) y puede procesar documentos de hasta **2 GB** de tamaño mientras mantiene el uso de memoria por debajo de **50 MB**. Su API `Redactor` proporciona una única llamada para recuperar toda la información clave del documento, eliminando la necesidad de múltiples analizadores.

## Requisitos previos

- **GroupDocs.Redaction for .NET** (última versión)  
- **.NET Framework** 4.5+ **or** **.NET Core/5+/6+**  
- Conocimientos básicos de C# y familiaridad con I/O de archivos  
- Visual Studio 2019 o posterior

## ¿Cómo configuro GroupDocs.Redaction para .NET?
Para comenzar a usar GroupDocs.Redaction, primero debe agregar la biblioteca a su proyecto. Esto se puede hacer a través de la .NET CLI, el Administrador de paquetes de Visual Studio o la interfaz de usuario de NuGet. Elija el enfoque que se ajuste a su flujo de trabajo; la CLI es ideal para compilaciones scriptables, mientras que la UI ofrece una forma gráfica de explorar versiones y dependencias.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Abra el Administrador de paquetes NuGet en Visual Studio.  
- Busque **"GroupDocs.Redaction"** e instale la última versión.

### Pasos para adquirir la licencia
1. **Free Trial:** Descargue una licencia de prueba para explorar todas las funciones sin restricciones.  
2. **Temporary License:** Solicite una licencia temporal en [GroupDocs](https://purchase.groupdocs.com/temporary-license/) para pruebas extendidas.  
3. **Purchase:** Cuando esté listo para producción, compre una licencia comercial.  

Para obtener más información, visite el [sitio web de GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Inicialización y configuración básica
La clase `Redactor` es el punto de entrada para todas las operaciones, incluida la extracción de metadatos.

`Redactor` es la clase central que representa una instancia de documento y proporciona métodos para redactar, recuperar información y manipular archivos. Una vez instalada, puede crear un objeto `Redactor` como se muestra a continuación:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Ahora que la biblioteca está lista, profundicemos en los detalles de implementación.

## Cómo extraer metadatos de un flujo de documento
Cargue el documento como un **flujo de solo lectura**, inicialice el `Redactor` y llame a `GetDocumentInfo()` para recuperar los metadatos en un solo paso. Este enfoque evita cargar todo el archivo en memoria, lo cual es crucial para PDFs grandes o documentos de Office de cientos de páginas.

**Respuesta directa:** Abra el archivo con `File.OpenRead()`, pase el flujo a `new Redactor(stream)`, luego llame a `redactor.GetDocumentInfo()` – el método devuelve un objeto que contiene el tipo de archivo, el recuento de páginas y el tamaño en solo tres líneas de código.

### Paso 1: Preparar la ruta del archivo fuente
Primero, asegúrese de que el archivo fuente exista y de que la carpeta de salida esté lista. El método auxiliar a continuación verifica el directorio de salida y lo crea si es necesario.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*¿Por qué?* Esto garantiza una ruta válida para las operaciones de archivo posteriores y evita `DirectoryNotFoundException`.

### Paso 2: Abrir el flujo del documento
Usar `File.OpenRead()` abre el archivo como un **flujo de solo lectura**, lo que mantiene bajo el uso de memoria incluso para archivos de varios gigabytes.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*¿Por qué?* Los flujos permiten el procesamiento en tiempo real, permitiéndole trabajar con porciones del archivo en lugar de todo el documento.

### Paso 3: Inicializar el Redactor con el flujo del documento
`Redactor` es el objeto API principal que le brinda acceso a operaciones a nivel de documento, incluida la extracción de metadatos.

`Redactor` representa un único documento cargado desde un flujo y expone métodos como `GetDocumentInfo()` para la recuperación rápida de propiedades.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*¿Por qué?* Instanciar `Redactor` con un flujo vincula el objeto al archivo subyacente sin cargarlo completamente.

### Paso 4: Recuperar los metadatos del documento
Llamar a `GetDocumentInfo()` devuelve un objeto `DocumentInfo` que contiene el formato del archivo, el recuento de páginas y el tamaño del archivo.

`GetDocumentInfo()` extrae las propiedades principales (formato, recuento de páginas, tamaño) en una única llamada, eliminando la necesidad de analizadores separados.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*¿Por qué?* Este paso consolida todos los metadatos esenciales, facilitando el registro, filtrado o enrutamiento de documentos según sus características.

## Cómo preparar un directorio de salida para archivos procesados
Antes de escribir cualquier archivo procesado, asegúrese de que la carpeta de destino exista y sea escribible. Al verificar programáticamente la ruta y crearla cuando falta, evita excepciones comunes en tiempo de ejecución como `DirectoryNotFoundException` o errores de permisos. Este paso simple también hace que su código sea portátil entre entornos, ya sea ejecutándose localmente, en un servidor o dentro de un contenedor.

**Respuesta directa:** Use `Directory.Exists()` para comprobar la carpeta y `Directory.CreateDirectory()` para crearla si no existe – esta verificación de una sola línea garantiza una ruta válida antes de cualquier operación de escritura.

### Implementar un método auxiliar
El método a continuación encapsula la lógica de comprobar y crear, devolviendo la ruta verificada para su uso posterior.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*¿Por qué?* Centralizar esta lógica reduce la duplicación y facilita el mantenimiento del código.

## Problemas comunes y soluciones
- **Permission errors:** Asegúrese de que la aplicación se ejecute bajo una cuenta con acceso de escritura a la carpeta de destino.  
- **Invalid paths:** Verifique nuevamente los separadores de ruta (`\\` en Windows, `/` en Linux/macOS) para evitar `DirectoryNotFoundException`.  
- **Large file handling:** Libere los flujos rápidamente (`using` statements) para liberar los manejadores del SO y prevenir fugas.

## Aplicaciones prácticas
1. **Automated Document Ingestion:** Extraiga metadatos al cargar, luego guárdelos en una base de datos para búsqueda rápida e informes de cumplimiento.  
2. **Legal & Compliance Audits:** Obtenga recuentos de páginas y tipos de archivo para verificar que los documentos cumplan con los estándares regulatorios antes de archivarlos.  
3. **Enterprise Content Management:** Use los metadatos para autocategorizar archivos en carpetas, mejorando la organización y la velocidad de recuperación.

## Consideraciones de rendimiento
- **Memory Management:** Siempre envuelva los flujos en bloques `using` para que se eliminen automáticamente.  
- **Batch Processing:** Procese documentos en grupos de 10‑20 para equilibrar el rendimiento y el uso de memoria, especialmente en servidores con recursos limitados.  
- **Parallelism:** Aproveche `Parallel.ForEach` para archivos independientes, pero monitoree la CPU y el I/O para evitar contención.

## Conclusión
Ahora tiene una guía completa y lista para producción sobre **cómo extraer metadatos** de flujos de documentos usando GroupDocs.Redaction para .NET. Siguiendo los pasos anteriores, podrá recuperar eficientemente el tipo de archivo, el recuento de páginas y el tamaño mientras mantiene bajo el uso de memoria y maneja archivos grandes de forma elegante.

**Próximos pasos**
- Revise la referencia completa de la API en la [documentación](https://docs.groupdocs.com/redaction/net/).  
- Profundice en la [Documentación de GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) para explorar funciones de redacción, marcas de agua y OCR.  
- Experimente con diferentes formatos de archivo (PDF, DOCX, XLSX) para ver cómo varían los metadatos entre tipos.  
- Integre los metadatos extraídos en su solución existente de gestión de documentos o búsqueda.

## Preguntas frecuentes

**Q: ¿Cuál es el caso de uso principal de la extracción de metadatos de GroupDocs.Redaction?**  
A: Permite la recuperación rápida y eficiente en memoria de las propiedades del documento para indexación, verificaciones de cumplimiento y enrutamiento automatizado sin abrir el archivo completo.

**Q: ¿Puedo extraer metadatos de archivos protegidos con contraseña?**  
A: Sí, proporcione la contraseña al crear el objeto `Redactor`; la API descifrará el flujo internamente.

**Q: ¿La biblioteca admite formatos que no sean PDF, como DOCX o XLSX?**  
A: Absolutamente – GroupDocs.Redaction maneja más de 30 formatos, incluidos PDF, DOCX, XLSX, PPTX y tipos de imagen comunes.

**Q: ¿Qué tamaño de documento puedo procesar con flujos?**  
A: Los flujos permiten procesar archivos de hasta **2 GB** manteniendo el consumo de memoria por debajo de **50 MB**, gracias a la lectura en tiempo real.

**Q: ¿Dónde puedo obtener ayuda si encuentro problemas?**  
A: Visite el [foro de GroupDocs](https://forum.groupdocs.com/c/redaction/33) para soporte de la comunidad, o consulte la documentación oficial para obtener consejos de solución de problemas.

---

**Última actualización:** 2026-06-11  
**Probado con:** GroupDocs.Redaction 23.12 para .NET  
**Autor:** GroupDocs  

**Recursos**  
- **Documentación:** [Documentación de GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/)  
- **Referencia de API:** [Referencia de API de GroupDocs Redaction](https://reference.groupdocs.com/redaction/net)  
- **Descarga:** [Últimas versiones de GroupDocs](https://releases.groupdocs.com/redaction/net)

## Tutoriales relacionados

- [Recuperación maestra de metadatos de documentos con GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [Cómo redactar metadatos de documentos usando GroupDocs.Redaction para .NET - Guía completa](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Redacción segura de documentos en .NET usando flujos: Guía para GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)