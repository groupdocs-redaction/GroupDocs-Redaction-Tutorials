---
date: '2026-07-20'
description: Aprenda a enumerar formatos usando GroupDocs.Redaction .NET, integre
  la función en su flujo de trabajo de documentos y mejore el rendimiento.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Descubra cómo enumerar formatos usando GroupDocs.Redaction .NET, vea
  una guía paso a paso y obtenga consejos para un rendimiento óptimo en sus aplicaciones
  .NET.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Cómo enumerar formatos con GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Cómo enumerar formatos con GroupDocs.Redaction .NET
type: docs
url: /es/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Cómo enumerar formatos con GroupDocs.Redaction .NET

Gestionar una amplia variedad de tipos de documentos es una realidad diaria para los desarrolladores que crean aplicaciones centradas en documentos. En este tutorial aprenderás **cómo enumerar formatos** que GroupDocs.Redaction .NET puede manejar, para que puedas validar archivos antes de procesarlos, presentar a los usuarios opciones precisas y mantener tu flujo de trabajo eficiente.

## Introducción

El manejo eficiente de documentos comienza con saber exactamente qué tipos de archivo admite tu biblioteca. GroupDocs.Redaction proporciona un método incorporado para obtener esta información, lo que te permite crear elementos de UI dinámicos, aplicar reglas de validación y evitar errores en tiempo de ejecución. A continuación encontrarás todo lo que necesitas para comenzar, desde la instalación hasta fragmentos de código prácticos y consejos de rendimiento.

### Respuestas rápidas
- **¿Qué significa “cómo enumerar formatos”?** Se refiere a obtener la colección de extensiones de archivo que GroupDocs.Redaction puede procesar.  
- **¿Necesito una licencia?** Sí, se requiere una licencia válida de GroupDocs.Redaction para uso en producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **¿Cuántos formatos están disponibles?** Se admiten más de 30 formatos de entrada y salida de forma predeterminada.  
- **¿Se necesita alguna configuración especial?** No se requiere configuración adicional más allá de la inicialización estándar de la biblioteca.

## Qué es “cómo enumerar formatos”

Implica llamar a la API FileType de la biblioteca para obtener una colección donde cada entrada contiene la extensión del archivo y un nombre legible por humanos. Los desarrolladores pueden iterar esta colección para crear reglas de validación, rellenar listas desplegables de UI o registrar los tipos compatibles, asegurando que solo se procesen documentos compatibles.

## Por qué enumerar formatos con GroupDocs.Redaction?

GroupDocs.Redaction admite **30+** tipos de archivo distintos —incluidos PDF, DOCX, PPTX y formatos de imagen—, lo que te permite manejar la mayoría de los documentos empresariales sin conversores de terceros. Al enumerar programáticamente estos formatos eliminas la conjetura, reduces los tickets de soporte y garantizas que solo los archivos compatibles ingresen a tu canal de procesamiento.

## Requisitos previos

- **GroupDocs.Redaction for .NET** – descarga el paquete más reciente desde el sitio oficial.  
- **.NET Framework o .NET Core** – compatible con tu entorno de desarrollo.  
- **Visual Studio** (o cualquier IDE compatible con C#).  
- Familiaridad básica con la sintaxis de C#.

## Configuración de GroupDocs.Redaction para .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Administrador de paquetes
`Install-Package GroupDocs.Redaction`

### Interfaz de usuario del Administrador de paquetes NuGet
- Busca **“GroupDocs.Redaction”** e instala la versión más reciente.

### Obtención de licencia
GroupDocs ofrece una prueba gratuita, una licencia temporal para evaluación o opciones de compra completa. Visita el sitio web de GroupDocs para obtener el archivo de licencia adecuado.

### Inicialización y configuración básica
Después de agregar el paquete, referencia el espacio de nombres y crea una instancia de `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Guía de implementación

### ¿Cómo enumerar formatos con GroupDocs.Redaction .NET?
Carga la biblioteca, llama al asistente estático y ordena los resultados —esto te brinda una colección lista para usar en solo dos líneas de código. Usa `FileType.GetSupportedFileFormats()` para obtener un `IEnumerable<FileType>` que incluye la extensión y el nombre visible de cada formato, luego ordénalo por extensión para obtener una lista UI limpia.

### Recuperación de formatos de archivo compatibles

#### Visión general
El objetivo es obtener una lista de tipos de archivo que GroupDocs.Redaction puede manejar, facilitando la integración en lógica de validación, listas desplegables de UI o mecanismos de registro.

#### Implementación paso a paso

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` devuelve todos los formatos que la biblioteca reconoce. El método forma parte de la clase `GroupDocs.Redaction.FileType`, que encapsula metadatos como la extensión del archivo y el nombre amigable.

**2. Display Supported File Types**  
Itera sobre la colección y muestra la extensión y descripción de cada formato. Ejemplo de código en línea:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

El fragmento imprime una lista ordenada como “.pdf – Portable Document Format”, lo que lo hace perfecto para rellenar elementos de UI.

### Consejos de solución de problemas
- **Missing Package** – Verifica la referencia del paquete NuGet y restaura los paquetes si es necesario.  
- **Incorrect License Path** – Asegúrate de que el archivo de licencia se copie al directorio de salida o proporciona una ruta absoluta.  
- **Unsupported Extension** – Si un formato no aparece en la lista, confirma que estás usando la versión más reciente de la biblioteca; las versiones más nuevas añaden formatos adicionales.

## Aplicaciones prácticas
Comprender los formatos de archivo compatibles abre varios escenarios del mundo real:

1. **Sistemas de gestión documental** – Valida las cargas contra la lista compatible para evitar fallos de procesamiento.  
2. **Seguridad de contenido** – Aplica reglas de redacción solo a los tipos de archivo que el motor puede modificar de forma segura.  
3. **Canales de procesamiento por lotes** – Filtra grandes lotes de archivos antes de invocar la redacción, ahorrando CPU y memoria.

## Consideraciones de rendimiento
- **Memory Footprint** – Enumerar formatos es una operación ligera; no carga ningún documento en memoria.  
- **Batch Operations** – Al procesar cientos de archivos, recupera la lista de formatos una sola vez y reutilízala para evitar llamadas redundantes.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` es seguro para subprocesos y puede llamarse desde tareas paralelas sin sincronización.

## Conclusión
Ahora dispones de un enfoque completo y listo para producción para **cómo enumerar formatos** usando GroupDocs.Redaction .NET. Al integrar esta funcionalidad, puedes mejorar la validación, optimizar la experiencia del usuario y mantener tus canales de documentos robustos.

### Próximos pasos
- Explora la API `Redactor` para aplicar reglas de redacción según el tipo de archivo.  
- Combina la lista de formatos con un menú desplegable en el front‑end para una selección de archivos sin fricciones.  
- Revisa la guía de rendimiento para optimizar trabajos por lotes a gran escala.

## Preguntas frecuentes

**Q: ¿Puedo obtener la lista de formatos sin inicializar una instancia de Redactor?**  
A: Sí, `FileType.GetSupportedFileFormats()` es estático y no requiere un objeto `Redactor`.

**Q: ¿La lista incluye tanto formatos de entrada como de salida?**  
A: El método devuelve todos los formatos que la biblioteca puede leer y escribir; cada `FileType` incluye una bandera `CanRead` y `CanWrite`.

**Q: ¿Con qué frecuencia se actualiza la lista de formatos compatibles?**  
A: GroupDocs publica actualizaciones de formatos con cada versión de la biblioteca; consultar la lista en tiempo de ejecución garantiza que siempre tengas el conjunto más reciente.

**Q: ¿Existe una forma de filtrar solo los formatos compatibles con PDF?**  
A: Sí, filtra la colección donde `format.Extension == ".pdf"` o donde `format.Name.Contains("PDF")`.

**Q: ¿Este enfoque funciona en .NET Core 2.1?**  
A: El método requiere .NET Core 3.1 o posterior; los entornos anteriores no son compatibles.

## Sección de preguntas frecuentes

1. **¿Cómo instalo GroupDocs.Redaction para .NET?**  
   Usa el comando CLI `dotnet add package GroupDocs.Redaction` o instala a través de la interfaz del Administrador de paquetes NuGet.  

2. **¿Cuáles son algunos problemas comunes al recuperar los formatos compatibles?**  
   Asegúrate de que todas las dependencias se restauren y de que estés referenciando el espacio de nombres correcto (`GroupDocs.Redaction`).  

3. **¿Puedo usar esta función con aplicaciones que no sean .NET?**  
   Este tutorial se centra en .NET, pero GroupDocs ofrece APIs similares para Java, Python y otras plataformas.  

4. **¿Cómo puedo optimizar el rendimiento al usar GroupDocs.Redaction?**  
   Reutiliza la lista de formatos, evita cargar documentos completos cuando solo verificas compatibilidad y monitoriza el uso de memoria durante los trabajos por lotes.  

5. **¿Qué tipos de archivo admite GroupDocs.Redaction?**  
   La biblioteca admite más de 30 formatos, incluidos PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG y muchos más. Usa `FileType.GetSupportedFileFormats()` para ver la lista completa.

## Recursos
- [Documentación](https://docs.groupdocs.com/redaction/net/)
- [Referencia de API](https://reference.groupdocs.com/redaction/net)
- [Descargar GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-07-20  
**Probado con:** GroupDocs.Redaction 4.2.0 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Tutoriales relacionados

- [Tutoriales de manejo de formatos para GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Tutoriales de carga de documentos con GroupDocs.Redaction para .NET](/redaction/net/document-loading/)
- [Tutoriales de guardado de documentos para GroupDocs.Redaction .NET](/redaction/net/document-saving/)