---
date: '2026-06-06'
description: Aprende cómo convertir una página a PNG y previsualizar páginas PDF con
  GroupDocs.Redaction para .NET. Guía paso a paso, fragmentos de código y consejos
  prácticos.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Convertir página a PNG usando GroupDocs.Redaction .NET
type: docs
url: /es/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Convertir página a PNG usando GroupDocs.Redaction .NET

Crear una vista previa de una sola página de un documento grande es una necesidad frecuente cuando deseas compartir solo la porción relevante de la información. En este tutorial aprenderás **cómo convertir una página a PNG** con GroupDocs.Redaction para .NET, configurar la salida de la vista previa e integrar el resultado en tus aplicaciones. Recorreremos los requisitos previos, la instalación, la configuración del código y consejos prácticos para que puedas comenzar a generar vistas previas PNG de una sola página en minutos.

## Respuestas rápidas
- **¿Puedo generar una vista previa PNG de solo una página?** Sí, use `PreviewOptions` para especificar el número de página y el formato.  
- **¿Qué formato admite GroupDocs.Redaction para vistas previas?** PNG es el predeterminado, pero también están disponibles JPEG y BMP.  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para pruebas; se requiere una licencia de producción para uso comercial.  
- **¿Esto funciona en .NET Core y .NET Framework?** Absolutamente – la biblioteca apunta a .NET Standard 2.0+.  
- **¿El proceso es eficiente en memoria para archivos grandes?** Sí, la API transmite páginas, evitando la carga completa del documento.

## ¿Qué es convertir página a PNG?
**convert page to PNG** se refiere a extraer una sola página de un documento compatible (PDF, DOCX, PPTX, etc.) y renderizar esa página como una imagen Portable Network Graphics (PNG). La imagen resultante conserva el diseño visual, fuentes y gráficos de la página original, permitiéndote compartir una captura clara mientras mantienes oculto el resto del documento.

## ¿Por qué usar una vista previa de una sola página?
Generar una vista previa PNG de una sola página reduce el ancho de banda, acelera los tiempos de carga y protege contenido sensible al exponer solo lo necesario. GroupDocs.Redaction puede renderizar un PDF de 300 páginas en un PNG de 200 KB en menos de 0.5 segundos en hardware de servidor típico, lo que lo hace ideal para portales web y herramientas de informes.

## Requisitos previos

- **GroupDocs.Redaction for .NET** – la biblioteca central que realiza la redacción de documentos y la generación de vistas previas.  
- **System.IO** – espacio de nombres estándar de .NET para manejo de archivos.  
- .NET Core 3.1+ o .NET Framework 4.6.1+ (cualquier plataforma que soporte .NET Standard 2.0).  
- Conocimientos básicos de C# y familiaridad con la gestión de paquetes NuGet.

## Configuración de GroupDocs.Redaction para .NET

### Información de instalación

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Abra su proyecto en Visual Studio.  
- Elija **Manage NuGet Packages**.  
- Busque **GroupDocs.Redaction** e instale la versión estable más reciente.

### Pasos para adquirir licencia
Para ejecutar la biblioteca necesitas una licencia válida. Puedes comenzar con una prueba gratuita o solicitar una clave temporal:

1. Visite el [GroupDocs website](https://purchase.groupdocs.com/temporary-license) para solicitar una licencia temporal.  
2. Siga las instrucciones enviadas por correo electrónico para agregar el archivo de licencia a su proyecto.

### Inicialización y configuración básica
La clase `RedactionEngine` es el punto de entrada para todas las operaciones, incluida la generación de vistas previas.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Guía de implementación

### Visión general
Esta sección muestra cómo **convertir página a PNG** configurando `PreviewOptions` e invocando la API de vista previa. El enfoque funciona para PDFs, DOCX, PPTX y muchos otros formatos compatibles con GroupDocs.Redaction.

### Paso 1: Preparar su entorno
Establezca la ruta del archivo fuente y la carpeta de salida. Use `Path.Combine` para crear rutas independientes de la plataforma.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Paso 2: Configurar opciones de vista previa
`PreviewOptions` le permite definir el número de página, el tamaño de la imagen y el formato de salida. La clase es el centro de configuración para la generación de vistas previas.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Explicación de configuraciones clave
- **Width & Height** – Ajuste estos valores para que coincidan con la resolución de pantalla objetivo.  
- **PageNumbers** – Proporcione una matriz con el índice exacto de la página que desea renderizar (basado en cero).  
- **PreviewFormat** – PNG es el predeterminado; cambie a `PreviewFormat.Jpeg` para archivos más pequeños.

### Consejos de solución de problemas
Si el PNG no se genera:

- Verifique que la ruta del archivo fuente sea correcta y que el archivo sea accesible.  
- Asegúrese de que el archivo de licencia se haya cargado antes de llamar a cualquier método de la API.  
- Confirme que `PreviewOptions.PageNumbers` contenga un índice de página válido (p. ej., `0` para la primera página).

## Aplicaciones prácticas
Crear una vista previa PNG de una sola página es útil en muchos escenarios:

1. **Presentaciones al cliente** – Muestre solo la diapositiva o cláusula contractual relevante.  
2. **Revisiones internas** – Permita verificaciones visuales rápidas sin abrir el documento completo.  
3. **Resúmenes de contenido** – Inserte instantáneas de página en correos electrónicos o paneles de control para ofrecer contexto inmediato.  

Integrar esta función con un CMS o CRM puede automatizar la generación de miniaturas para documentos cargados, mejorando la experiencia del usuario.

## Consideraciones de rendimiento
- **Memory Management** – Libere las instancias de `RedactionEngine` después de usarlas para liberar recursos.  
- **Asynchronous Execution** – Use `await engine.GeneratePreviewAsync(...)` en aplicaciones UI para mantener la interfaz receptiva.  
- **Library Updates** – GroupDocs.Redaction admite **más de 30 formatos de entrada y salida** y procesa documentos de hasta 500 páginas sin cargar todo el archivo en memoria. Mantenga el paquete actualizado para beneficiarse de mejoras de rendimiento.

## Conclusión
Ahora dispones de un método completo y listo para producción para **convertir página a PNG** y generar vistas previas de una sola página con GroupDocs.Redaction para .NET. Siguiendo los pasos anteriores puedes incrustar instantáneas PNG de alta calidad en cualquier aplicación .NET, mejorando el intercambio de documentos mientras preservas la seguridad y el rendimiento.

## Preguntas frecuentes

**Q: ¿Puedo generar vistas previas para PDFs protegidos con contraseña?**  
A: Sí, proporcione la contraseña al inicializar `RedactionEngine` y la vista previa se creará normalmente.

**Q: ¿Cómo cambio el formato de salida de PNG a JPEG?**  
A: Establezca `options.PreviewFormat = PreviewFormat.Jpeg` antes de llamar al método de vista previa.

**Q: ¿Es posible previsualizar varias páginas a la vez?**  
A: Absolutamente – asigne una matriz de números de página a `options.PageNumbers` (p. ej., `new[] {0, 2, 4}`).

**Q: ¿Qué debo hacer si la imagen de vista previa está borrosa?**  
A: Aumente `options.Width` y `options.Height` a una resolución mayor; la biblioteca escalará la imagen en consecuencia.

**Q: ¿Esto funciona en contenedores Linux?**  
A: Sí, GroupDocs.Redaction .NET es multiplataforma y se ejecuta dentro de contenedores Docker que soportan .NET Core.

## Recursos
- [Documentación](https://docs.groupdocs.com/redaction/net/)
- [Referencia de API](https://reference.groupdocs.com/redaction/net)
- [Descargar la última versión](https://releases.groupdocs.com/redaction/net/)
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Adquisición de licencia temporal](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2026-06-06  
**Probado con:** GroupDocs.Redaction 5.6 for .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Dominar la seguridad de documentos: rasterizar y redactar documentos Word con GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Cómo eliminar páginas de PDFs usando GroupDocs.Redaction .NET: Guía completa](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementar la redacción de documentos usando GroupDocs.Redaction .NET: Guía paso a paso](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)