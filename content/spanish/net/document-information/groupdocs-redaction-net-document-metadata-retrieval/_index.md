---
date: '2026-06-06'
description: Aprenda cómo recuperar metadatos y extraer metadatos de documentos usando
  GroupDocs.Redaction .NET, lo que permite una gestión de documentos robusta y cumplimiento.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Cómo recuperar metadatos con GroupDocs.Redaction .NET API
type: docs
url: /es/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Cómo recuperar metadatos con GroupDocs.Redaction .NET

En la era digital actual, **cómo recuperar metadatos** de un archivo es un paso fundamental para cualquier aplicación centrada en documentos. Ya sea que necesite leer los metadatos del archivo para auditorías de cumplimiento, extraer propiedades del documento para indexación, o simplemente mostrar el tamaño del documento en una interfaz de usuario, GroupDocs.Redaction .NET le brinda una API concisa para hacerlo en solo unas pocas líneas de C#. Este tutorial lo guía a través de todo el proceso, desde la configuración del entorno hasta la visualización de la información recuperada, para que pueda comenzar a extraer metadatos de documentos de inmediato.

## Respuestas rápidas
- **¿Cuál es el método principal para obtener metadatos?** Llamar a `Redactor.GetDocumentInfo()` en una instancia de `Redactor`.  
- **¿Qué formatos son compatibles?** Más de 50 formatos de entrada y salida, incluidos PDF, DOCX, XLSX, PPTX y tipos de imagen.  
- **¿Necesito una licencia para desarrollo?** Una licencia de prueba gratuita funciona para pruebas; se requiere una licencia completa para producción.  
- **¿Puedo procesar archivos grandes?** Sí—GroupDocs.Redaction maneja documentos de cientos de páginas sin cargar todo el archivo en memoria.  
- **¿Está disponible el soporte async?** La API puede envolver en patrones async para mantener los hilos de UI responsivos.

## Qué es la recuperación de metadatos en GroupDocs.Redaction?
La recuperación de metadatos es el proceso de acceder a las propiedades integradas de un documento —como el tipo de archivo, el número de páginas y el tamaño— a través de la API de la biblioteca. Al extraer estas propiedades, los desarrolladores pueden evaluar programáticamente las características del documento, soportar la indexación, aplicar reglas de cumplimiento y tomar decisiones informadas sobre pasos de procesamiento posteriores.

## Cómo recuperar metadatos del documento?
The `Redactor` class is the primary interface for loading and inspecting documents in GroupDocs.Redaction.  
`GetDocumentInfo()` is a method that returns a `DocumentInfo` object containing the document’s metadata.  

Load your file with `new Redactor("path/to/file")` and invoke `GetDocumentInfo()`—the call returns a `DocumentInfo` object containing type, page count, size, and other properties. This two‑step approach works for any supported format and requires no additional configuration. You can then read fields like `FileType`, `PageCount`, and `FileSize` to display or log the information.

## Requisitos previos

- **GroupDocs.Redaction .NET** versión 21.6 o posterior.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, o .NET 5/6+.  
- Conocimientos básicos de C# y un IDE de desarrollo (Visual Studio, Rider, etc.).

## Configuración de GroupDocs.Redaction para .NET

Comenzar con GroupDocs.Redaction es sencillo. Instale el paquete usando uno de los siguientes métodos:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Or, use the **NuGet Package Manager UI**: Simply search for “GroupDocs.Redaction” and click **Install**.

### Obtención de licencia

Para probar GroupDocs.Redaction, puede obtener una licencia de prueba gratuita. Para desarrollo continuo o uso en producción, compre una licencia completa o solicite una licencia temporal desde el sitio oficial.

Una vez instalado, inicialice la biblioteca de la siguiente manera:

```csharp
using GroupDocs.Redaction;
```

## Guía de implementación

### Funcionalidad de obtener información del documento

Esta funcionalidad se centra en extraer metadatos esenciales de documentos usando GroupDocs.Redaction .NET. Siga estos pasos:

#### Paso 1: Prepare la ruta de su documento

Defina la ruta absoluta o relativa al archivo objetivo:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Reemplace `YOUR_DOCUMENT_DIRECTORY` con la carpeta que contiene su documento.

#### Paso 2: Inicializar la instancia Redactor

Cree un objeto `Redactor` que proporcione acceso a los métodos de metadatos:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Paso 3: Recuperar información del documento

Llame a `GetDocumentInfo()` en la instancia `Redactor` para obtener todas las propiedades disponibles:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

El objeto devuelto incluye el tipo de archivo, el número de páginas y el tamaño del archivo.

#### Paso 4: Mostrar los detalles del documento

Muestre la información en la consola o en la UI. El código de ejemplo (comentado para ejecuciones independientes) demuestra cómo imprimir cada propiedad:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### ¿Por qué usar GroupDocs.Redaction para la extracción de metadatos?

GroupDocs.Redaction soporta **más de 50 formatos de archivo** y puede procesar documentos de hasta **2 GB** de tamaño mientras mantiene el consumo de memoria por debajo de **100 MB** para cargas de trabajo típicas. La biblioteca extrae metadatos sin cargar completamente el documento, ofreciendo respuestas rápidas—a menudo menos de **200 ms** para un PDF de 100 páginas en hardware de servidor estándar.

### Problemas comunes y soluciones

- **Ruta de archivo incorrecta** – Verifique la cadena de ruta y asegúrese de que el archivo sea accesible para el proceso en ejecución.  
- **Formato no compatible** – Revise la lista de formatos; si falta un formato, considere convertirlo primero.  
- **Cuellos de botella de rendimiento** – Para archivos muy grandes, habilite opciones de streaming o procese páginas en lotes para limitar el uso de memoria.

## Aplicaciones prácticas

Comprender los metadatos de un documento permite varios escenarios del mundo real:

1. **Sistemas de gestión de documentos (DMS)** – Automatice la categorización e indexación basándose en el tipo, tamaño o número de páginas.  
2. **Auditoría de cumplimiento** – Verifique que los archivos confidenciales contengan los metadatos requeridos antes de archivarlos.  
3. **Migración de datos** – Agrupe archivos por propiedades para agilizar tareas de migración masiva.  

## Consideraciones de rendimiento

- **Uso eficiente de recursos** – Use la instancia `Redactor` dentro de un bloque `using` para garantizar la eliminación adecuada.  
- **Patrones asíncronos** – Envuelva las llamadas de metadatos en `Task.Run` o implemente envoltorios async para mantener los hilos de UI responsivos en aplicaciones de escritorio o web.

## Preguntas frecuentes

**Q:** ¿Qué formatos de documento puedo extraer metadatos?  
**A:** GroupDocs.Redaction lee metadatos de más de 50 formatos, incluidos PDF, DOCX, XLSX, PPTX, HTML y tipos de imagen comunes.

**Q:** ¿Cómo manejo archivos protegidos con contraseña?  
**A:** Pase la contraseña al constructor `Redactor`; la API descifrará el archivo antes de extraer los metadatos.

**Q:** ¿Existe un límite al tamaño de los archivos que puedo procesar?  
**A:** Aunque no hay un límite estricto, los archivos mayores de 2 GB pueden requerir ajustes adicionales de memoria; el rendimiento sigue siendo lineal con el tamaño del archivo.

**Q:** ¿Puedo recuperar metadatos en una operación por lotes?  
**A:** Sí—itere sobre una colección de rutas de archivo y llame a `GetDocumentInfo()` para cada una; la biblioteca es segura para hilos en ejecuciones paralelas.

**Q:** ¿Necesito una licencia para compilaciones de desarrollo?  
**A:** Una licencia de prueba gratuita es suficiente para desarrollo y pruebas; se requiere una licencia comercial para despliegues en producción.

## Recursos

- [Documentación](https://docs.groupdocs.com/redaction/net/)  
- [Referencia de API](https://reference.groupdocs.com/redaction/net)  
- [Descarga](https://releases.groupdocs.com/redaction/net/)  
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Información de licencia temporal](https://purchase.groupdocs.com/temporary-license/)

## Conclusión

Ahora tiene una guía completa, paso a paso, sobre **cómo recuperar metadatos** usando GroupDocs.Redaction .NET. Al aprovechar el método `Redactor.GetDocumentInfo()`, puede leer rápidamente los metadatos del archivo, apoyar flujos de trabajo de cumplimiento y mejorar cualquier canal de procesamiento de documentos. Explore características adicionales de Redaction—como la redacción de contenido, marcas de agua y conversión de documentos—para crear una solución de gestión de documentos totalmente funcional.

---

**Last Updated:** 2026-06-06  
**Probado con:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Autor:** GroupDocs  

## Tutoriales relacionados

- [Cómo extraer metadatos de documentos desde streams usando GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Cómo redactar metadatos de documentos usando GroupDocs.Redaction para .NET - Guía completa](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Tutoriales de carga de documentos con GroupDocs.Redaction para .NET](/redaction/net/document-loading/)