---
date: 2026-06-11
description: Aprenda cómo exportar archivos redactados, configurar carpetas de salida,
  crear PDFs rasterizados y guardar en flujos utilizando GroupDocs.Redaction for .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Cómo exportar documentos redactados con GroupDocs.Redaction .NET
type: docs
url: /es/net/document-saving/
weight: 3
---

# Cómo exportar documentos redactados con GroupDocs.Redaction .NET

En esta guía completa descubrirás **cómo exportar contenido redactado** de forma segura y eficiente usando GroupDocs.Redaction para .NET. Ya sea que necesites mantener el tipo de archivo original, bloquear el documento como un PDF rasterizado, o transmitir el resultado directamente en memoria, te guiaremos a través de cada opción con explicaciones claras y conversacionales y consejos del mundo real. Al final de este tutorial podrás elegir la estrategia de exportación adecuada para cualquier escenario impulsado por cumplimiento.

## Respuestas rápidas
- **¿Qué formatos puedo exportar?** Cualquiera de los más de 30 formatos nativos compatibles con GroupDocs.Redaction, más PDF rasterizado para máxima seguridad.  
- **¿Necesito una licencia para streaming?** Sí, se requiere una licencia válida de GroupDocs.Redaction para streaming en producción.  
- **¿Puedo establecer una carpeta de salida personalizada?** Absolutamente – usa la propiedad `OutputPath` o `SaveOptions` para configurarla.  
- **¿Es segura la rasterización para archivos grandes?** Maneja documentos de hasta 500 páginas sin cargar todo el archivo en memoria.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## ¿Qué es GroupDocs.Redaction?
GroupDocs.Redaction es una biblioteca .NET que elimina o enmascara programáticamente información sensible de PDFs, Word, Excel, PowerPoint, imágenes y muchos otros formatos. Ofrece una API de alto nivel para definir regiones de redacción, aplicar políticas y, finalmente, exportar el documento limpiado. Esto facilita la integración de capacidades de redacción en cualquier aplicación .NET.

## ¿Por qué exportar documentos redactados como PDFs rasterizados?
Los PDFs rasterizados convierten cada página en una imagen plana, eliminando capas de texto ocultas que podrían extraerse posteriormente. Este formato garantiza que el contenido redactado no pueda recuperarse, cumpliendo con estrictas normas regulatorias como GDPR y HIPAA. GroupDocs.Redaction puede generar PDFs rasterizados de hasta 300 dpi, preservando la fidelidad visual mientras asegura la seguridad.

## ¿Cómo exportar documentos redactados?
Carga el archivo fuente, aplica tus reglas de redacción y luego llama al método de guardado apropiado—ya sea `Save` para el formato original, `SaveAsRasterizedPdf` para PDFs solo de imagen, o `SaveToStream` para manejo en memoria. A continuación se muestra el flujo de trabajo paso a paso. Cada método garantiza que el contenido redactado se elimine permanentemente mientras se preserva el formato de salida deseado.

### Paso 1: Instalar el paquete NuGet
Add the latest GroupDocs.Redaction package to your project:

```bash
dotnet add package GroupDocs.Redaction
```

### Paso 2: Cargar el documento y definir redacciones
Create a `Redactor` instance, load the file, and specify the regions you want to hide. The `Redactor` class provides the core functionality for loading documents and applying redaction rules.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Paso 3: Elegir el método de exportación
#### Exportar en formato original
```csharp
redactor.Save("RedactedReport.docx");
```

#### Exportar como PDF rasterizado
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Exportar a un Memory Stream (ideal para APIs web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

El método `Save` escribe el documento redactado en un archivo en su formato original. `SaveAsRasterizedPdf` crea un PDF donde cada página se renderiza como una imagen, eliminando cualquier texto oculto. `SaveToStream` devuelve el archivo redactado como un memory stream, adecuado para respuestas web.

## ¿Cómo configurar una carpeta de salida?
Establece la propiedad `OutputPath` en el `Redactor` o pasa un objeto `SaveOptions` personalizado que incluya el directorio deseado. `OutputPath` es una propiedad del `Redactor` que especifica el directorio donde se escriben los archivos de salida. `SaveOptions` te permite personalizar varios parámetros de guardado, incluida la carpeta de salida. Esto garantiza que todos los archivos exportados se guarden en una ubicación predecible, simplificando las canalizaciones de procesamiento por lotes. También puedes especificar subcarpetas por tipo de documento para mantener tu espacio de trabajo organizado.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Problemas comunes y soluciones
- **Redacción no aplicada:** Verifica que el patrón de búsqueda coincida exactamente con el texto del documento; usa `RegexOptions.IgnoreCase` si es necesario. `RegexOptions` es una enumeración que controla el comportamiento de coincidencia de expresiones regulares, como la sensibilidad a mayúsculas.  
- **Los archivos grandes generan presión de memoria:** Habilita el modo de streaming usando `SaveToStream` y evita llamar a `Save` en todo el documento.  
- **El PDF rasterizado se ve borroso:** Incrementa el DPI en `RasterizationOptions` (p. ej., 300–600) para mejorar la calidad de la imagen. `RasterizationOptions` permite establecer parámetros como DPI y formato de imagen para la salida de PDF rasterizado.

## Preguntas frecuentes

**P: ¿Puedo exportar a un formato que no estaba soportado originalmente?**  
R: Sí, GroupDocs.Redaction puede convertir la mayoría de los tipos de entrada a PDF, DOCX, XLSX, PPTX o PDF rasterizado, cubriendo más de 30 formatos.

**P: ¿Cómo protege la rasterización los datos redactados?**  
R: Al renderizar cada página como una imagen plana, se eliminan todas las capas de texto ocultas, lo que hace imposible extraer el contenido original.

**P: ¿Es posible encadenar múltiples reglas de redacción?**  
R: Absolutamente – puedes llamar a `Apply` repetidamente o pasar una colección de `RedactionOptions` para procesar muchos patrones en una sola pasada. `RedactionOptions` define la configuración para una única operación de redacción, como la región y el tipo de reemplazo.

**P: ¿Necesito cerrar el objeto Redactor?**  
R: El `Redactor` implementa `IDisposable`; envuélvelo en un bloque `using` o llama a `Dispose()` para liberar los manejadores de archivo rápidamente. `IDisposable` es una interfaz que proporciona un mecanismo para liberar recursos no administrados.

**P: ¿Qué entornos de ejecución .NET se prueban oficialmente?**  
R: GroupDocs.Redaction está validado en .NET Framework 4.6+, .NET Core 3.1+ y .NET 5/6/7.

## Recursos adicionales

### Tutoriales disponibles
- [Cómo guardar documentos como PDFs rasterizados usando GroupDocs.Redaction para .NET&#58; Guía completa](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementar directorio de salida en .NET con GroupDocs.Redaction&#58; Guía completa](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redactar y guardar documentos con GroupDocs.Redaction para .NET&#58; Guía completa](./redact-save-documents-groupdocs-redaction-net/)
- [Guardar documentos redactados en formato original usando GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redacción segura de documentos en .NET usando Streams&#58; Guía para GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Enlaces útiles
- [Documentación de GroupDocs.Redaction para .NET](https://docs.groupdocs.com/redaction/net/)
- [Referencia API de GroupDocs.Redaction para .NET](https://reference.groupdocs.com/redaction/net/)
- [Descargar GroupDocs.Redaction para .NET](https://releases.groupdocs.com/redaction/net/)
- [Foro de GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Soporte gratuito](https://forum.groupdocs.com/)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-06-11  
**Probado con:** GroupDocs.Redaction 23.11 for .NET  
**Autor:** GroupDocs  

## Tutoriales relacionados
- [Guardar documentos redactados en formato original usando GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Cómo guardar documentos como PDFs rasterizados usando GroupDocs.Redaction para .NET: Guía completa](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Redacción segura de documentos en .NET usando Streams: Guía para GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)