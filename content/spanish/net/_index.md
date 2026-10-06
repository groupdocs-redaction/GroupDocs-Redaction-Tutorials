---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: Aprenda a redactar páginas PDF, eliminar anotaciones PDF y redactar celdas
  de Excel usando GroupDocs.Redaction for .NET – una API segura y multiplataforma
  para la redacción de documentos.
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: Tutoriales de GroupDocs.Redaction for .NET
og_description: Cómo redactar páginas PDF rápidamente con GroupDocs.Redaction for
  .NET. La API elimina anotaciones PDF, redacta celdas de Excel y protege datos sensibles
  en más de 30 formatos.
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: Cómo redactar páginas PDF – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: Cómo redactar páginas PDF con GroupDocs.Redaction for .NET
type: docs
url: /es/net/
weight: 10
---

# Cómo redactar páginas PDF con GroupDocs.Redaction para .NET

Si necesita **redactar páginas PDF** de forma rápida y fiable, GroupDocs.Redaction para .NET le ofrece una API completa y multiplataforma que elimina contenido sensible de más de 30 formatos de archivo. Ya sea que esté creando un flujo de trabajo impulsado por cumplimiento, un portal de gestión documental o una aplicación centrada en la privacidad, esta biblioteca le permite borrar permanentemente datos confidenciales mientras preserva el resto de la estructura del documento.

**GroupDocs.Redaction para .NET es una biblioteca .NET que permite la eliminación permanente de contenido sensible de más de 30 formatos de documento.** Soporta procesamiento de alto volumen, puede manejar archivos de cientos de páginas sin cargar todo el documento en memoria, y ofrece opciones de rasterización que convierten texto en imágenes para mayor seguridad.

{{% alert color="primary" %}}
GroupDocs.Redaction para .NET ofrece un conjunto completo de tutoriales y ejemplos para implementar la redacción segura de documentos en sus aplicaciones .NET. Desde reemplazos básicos de texto hasta la limpieza avanzada de metadatos, estos recursos cubren técnicas esenciales para redactar información sensible de los documentos. Aprenda a eliminar permanentemente datos privados de varios formatos de documento, incluidos PDF, Word, Excel, PowerPoint e imágenes, con control preciso y eliminación completa del contenido confidencial. Nuestras guías paso a paso le ayudan a dominar tanto las capacidades de redacción estándar como las avanzadas para cumplir con los requisitos de cumplimiento y proteger la información sensible de manera eficaz.
{{% /alert %}}

## Respuestas rápidas
- **¿Puede GroupDocs.Redaction redactar páginas PDF completas?** Sí, puede eliminar páginas individuales o rangos de páginas con una sola llamada a la API.  
- **¿Admite la eliminación de anotaciones PDF?** Absolutamente: las anotaciones, comentarios y marcas pueden eliminarse en un solo paso.  
- **¿Puedo redactar celdas de Excel sin convertir a PDF?** Sí, la biblioteca se dirige directamente a las hojas de cálculo de Excel.  
- **¿Se admite cargar un PDF desde un stream?** La API acepta objetos `Stream`, lo que permite el procesamiento en memoria.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qué es la redacción en el contexto de los PDFs?
La redacción es la eliminación permanente o el ocultamiento de contenido sensible de un documento para que no pueda recuperarse ni verse posteriormente. En los archivos PDF, la redacción puede dirigirse a texto, imágenes, anotaciones o páginas completas, y el resultado es un archivo sanitizado que conserva su diseño original.

## Por qué usar GroupDocs.Redaction para .NET?
GroupDocs.Redaction para .NET ofrece una solución robusta y de alto rendimiento que puede manejar documentos grandes mientras garantiza la eliminación completa de datos sensibles, ofreciendo rasterización incorporada, amplio soporte de formatos y registro de auditoría detallado, lo que la hace ideal para aplicaciones impulsadas por cumplimiento y entornos empresariales.

- **30+ formatos compatibles** – incluidos PDF, DOCX, XLSX, PPTX, HTML y tipos de imagen comunes.  
- **Rendimiento escalable** – procesa PDFs de 500 páginas en menos de 5 segundos en un servidor típico, sin cargar todo el archivo en RAM.  
- **Rasterización incorporada** – convierte las páginas redactadas en imágenes, garantizando que no quede texto oculto.  
- **Listo para cumplimiento** – cumple con los requisitos de GDPR, HIPAA y PCI‑DSS con registro de auditoría.

## Requisitos previos
- .NET Framework 4.5+ **o** .NET Core 3.1+ instalado en su máquina de desarrollo.  
- Una licencia válida de GroupDocs.Redaction (prueba disponible para evaluación).  
- Acceso a los archivos PDF, Excel o Word que desea procesar.

## Cómo redactar páginas PDF paso a paso

Redactor es la clase principal en GroupDocs.Redaction que carga, modifica y guarda documentos. RemovePages elimina las páginas especificadas del documento cargado.

Cargue el PDF, defina las páginas que desea eliminar, aplique la redacción y guarde el resultado. La siguiente respuesta directa explica el patrón central:

Cargue el PDF objetivo con `Redactor.Load(streamOrPath)`, llame a `Redactor.RemovePages(pageNumbers)` para eliminar las páginas no deseadas y, finalmente, invoque `Redactor.Save(outputPath)` – este flujo de tres pasos redacta páginas en menos de un segundo para la mayoría de los documentos.

### Paso 1: cargar el PDF
Puede abrir un archivo desde disco, un stream de memoria o una fuente remota. La API acepta tanto una cadena de ruta de archivo como un objeto `Stream`, lo que es ideal para servicios web que reciben cargas.

### Paso 2: definir las páginas a redactar
Pase una lista de índices de página basados en cero o una cadena de rango como `"1-3,5"` al método `RemovePages`. La biblioteca valida el rango y lanza una excepción clara si una página no existe.

### Paso 3: guardar el documento sanitizado
Llame a `Save` con el formato de salida deseado. Puede mantener el PDF original, exportar a un PDF rasterizado o transmitir el resultado directamente a la respuesta del cliente.

## Problemas comunes y soluciones
- **Problema:** La redacción parece funcionar pero el texto original sigue siendo buscable.  
  **Solución:** Habilite la rasterización (`Redactor.Rasterize = true`) antes de guardar; esto convierte la página en una imagen, eliminando capas de texto oculto.  

- **Problema:** Los PDFs grandes provocan excepciones OutOfMemory.  
  **Solución:** Use `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` para procesar el archivo en fragmentos.  

- **Problema:** Las anotaciones no se eliminan.  
  **Solución:** Llame a `Redactor.RemoveAnnotations()` después de cargar el documento; este método elimina comentarios, resaltados y campos de formulario.

## Preguntas frecuentes

**P:** ¿Puedo redactar páginas PDF sin afectar el resto del diseño del documento?  
**R:** Sí, la biblioteca elimina las páginas especificadas mientras preserva la numeración de páginas, marcadores y referencias cruzadas del contenido restante.

**P:** ¿Es posible redactar solo anotaciones PDF?  
**R:** Absolutamente. Use `Redactor.RemoveAnnotations()` para eliminar todos los objetos de anotación en una sola llamada.

**P:** ¿Cómo redacto celdas de Excel directamente?  
**R:** Cargue el libro con `Redactor.LoadExcel(path)`, luego llame a `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` y guarde.

**P:** ¿GroupDocs.Redaction admite cargar PDFs desde un stream?  
**R:** Sí, puede pasar cualquier `System.IO.Stream` al método `Load`, lo cual es ideal para procesar archivos cargados a través de controladores ASP.NET Core.

**P:** ¿Qué modelo de licenciamiento se recomienda para uso de producción de alto volumen?  
**R:** El licenciamiento por consumo le permite pagar por operación de redacción, escalando de manera rentable con picos de uso.

---

**Última actualización:** 2026-10-06  
**Probado con:** GroupDocs.Redaction 23.10 para .NET  
**Autor:** GroupDocs  

---  

### Tutoriales de GroupDocs.Redaction para .NET – cómo redactar páginas PDF

### [Tutoriales de introducción](./getting-started/)

Comience aquí si es nuevo en GroupDocs.Redaction. Este tutorial le guía a través de la instalación, licenciamiento y la creación de su primer proyecto de redacción en .NET. Verá cómo abrir un documento, definir una regla de redacción simple y guardar el archivo sanitizado.

### [Técnicas avanzadas de redacción](./advanced-redaction/)

Profundice con manejadores de redacción personalizados, políticas, callbacks y redacción asistida por IA. Esta guía le muestra cómo construir pipelines flexibles que pueden **redactar páginas PDF**, manejar estructuras de documentos complejas e integrar modelos de aprendizaje automático para una detección de contenido más inteligente.

### [Tutoriales de redacción de anotaciones](./annotation-redaction/)

Las anotaciones a menudo contienen notas confidenciales. Aprenda cómo localizar, modificar o eliminar completamente anotaciones, comentarios y marcas de revisión de PDFs, archivos Word y otros formatos compatibles.

### [Tutoriales de información de documentos](./document-information/)

Entender los metadatos de un documento es el primer paso para una redacción segura. Este tutorial explica cómo recuperar propiedades del documento, enumerar formatos compatibles y generar imágenes de vista previa antes de aplicar cualquier redacción.

### [Tutoriales de carga de documentos](./document-loading/)

Los documentos pueden residir en disco, en streams o detrás de capas de autenticación. Aprenda las mejores prácticas para cargar archivos locales, streams de memoria y documentos protegidos con contraseña de forma segura.

### [Tutoriales de guardado de documentos](./document-saving/)

Después de la redacción necesitará persistir el archivo limpiado. Esta guía cubre el guardado en el formato original, la exportación a PDF rasterizado y la transmisión de resultados directamente a una aplicación del lado del cliente.

### [Tutoriales de manejo de formatos](./format-handling/)

GroupDocs.Redaction admite una amplia gama de formatos. Explore cómo trabajar con diferentes tipos de archivo, crear manejadores de formatos personalizados y ampliar la biblioteca para cubrir estándares de documentos especializados.

### [Tutoriales de redacción de imágenes](./image-redaction/)

Las imágenes pueden ocultar datos visuales sensibles. Aprenda a redactar regiones específicas de la imagen, eliminar imágenes incrustadas y limpiar los metadatos de la imagen para garantizar que no quede información oculta.

### [Tutoriales de licenciamiento y configuración](./licensing-configuration/)

El licenciamiento adecuado es crítico para el uso en producción. Este tutorial le muestra cómo aplicar licencias, configurar ajustes de tiempo de ejecución e implementar licenciamiento por consumo para implementaciones escalables.

### [Tutoriales de redacción de metadatos](./metadata-redaction/)

Los metadatos a menudo filtran detalles confidenciales. Siga esta guía para eliminar propiedades del documento, comentarios ocultos y otros metadatos de archivos PDF, Word, Excel y PowerPoint.

### [Tutoriales de integración OCR](./ocr-integration/)

Al tratar con PDFs escaneados o imágenes, OCR es esencial. Aprenda a integrar motores OCR, extraer texto buscable y luego **redactar páginas PDF** que contengan información sensible.

### [Tutoriales de redacción de páginas](./page-redaction/)

A veces necesita eliminar páginas completas. Este tutorial demuestra cómo eliminar páginas individuales, rangos de páginas y eliminar condicionalmente páginas según el contenido.

### [Tutoriales de redacción específicos de PDF](./pdf-specific-redaction/)

Los PDFs tienen características únicas como capas, anotaciones y campos de formulario. Domine técnicas de redacción exclusivas para PDF, incluyendo filtrado de contenido y preservación de la integridad del documento.

### [Tutoriales de opciones de rasterización](./rasterization-options/)

Los PDFs rasterizados convierten el contenido en imágenes, haciendo imposible la extracción de datos. Aprenda a configurar ruido, inclinación, escala de grises y bordes, y descubra cómo **guardar PDFs rasterizados** para máxima seguridad.

### [Tutoriales de redacción de hojas de cálculo](./spreadsheet-redaction/)

Las hojas de cálculo de Excel a menudo contienen celdas confidenciales. Esta guía le muestra cómo apuntar y **redactar celdas de Excel**, ocultar fórmulas y proteger hojas de cálculo sensibles.

### [Tutoriales de redacción de texto](./text-redaction/)

El texto es el tipo de dato más común de proteger. Siga instrucciones paso a paso para coincidencia de frases exactas, redacción con expresiones regulares y búsquedas sensibles a mayúsculas, incluyendo cómo **redactar texto de Word** de manera eficiente.

## Tutoriales relacionados

- [Cómo eliminar anotaciones – Tutoriales de redacción de anotaciones para GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [Cómo eliminar la última página de un PDF usando GroupDocs.Redaction para .NET](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [Cómo redactar PDF y guardar como PDF rasterizado con GroupDocs.Redaction para .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)