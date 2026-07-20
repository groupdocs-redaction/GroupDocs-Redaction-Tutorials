---
date: '2026-07-20'
description: Aprenda a redactar documentos, ocultar información sensible y guardar
  archivos redactados en un memory stream usando GroupDocs.Redaction for .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Cómo redactar documentos con GroupDocs.Redaction for .NET. Siga esta
  guía step‑by‑step para ocultar información sensible y guardar el archivo redactado
  en un memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Cómo redactar documentos con GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Cómo redactar documentos con GroupDocs.Redaction for .NET – Guía completa
type: docs
url: /es/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Cómo redactar documentos con GroupDocs.Redaction para .NET

En entornos empresariales modernos, **cómo redactar documentos** es una habilidad crítica para proteger datos personales, secretos comerciales e información relacionada con el cumplimiento. Esta guía le muestra cómo redactar información sensible de archivos Word, PDF o de imagen y luego guardar la salida redactada directamente en un MemoryStream, todo con GroupDocs.Redaction para .NET.

## Respuestas rápidas
- **¿Qué hace la redacción?** Reemplaza permanentemente el contenido seleccionado con un marcador de posición o lo elimina, garantizando que los datos nunca puedan recuperarse.  
- **¿Qué formatos son compatibles?** Más de 30 tipos de archivo, incluidos PDF, DOCX, PPTX y formatos de imagen comunes.  
- **¿Puedo redactar sin escribir en disco?** Sí—guarde el resultado en un `MemoryStream` para procesamiento en memoria.  
- **¿Necesito una licencia para producción?** Se requiere una licencia completa para uso en producción; hay una prueba gratuita disponible para evaluación.  
- **¿Es compatible con .NET Core?** Absolutamente—GroupDocs.Redaction funciona con .NET Framework 4.6+, .NET Core 3.1+, y .NET 5/6/7.

## ¿Qué es la redacción de documentos?
La redacción de documentos elimina o oculta permanentemente texto confidencial, imágenes y metadatos de un archivo, asegurando que el contenido oculto no pueda recuperarse, verse o extraerse más tarde. Reemplaza los elementos sensibles con un marcador de posición, como un rectángulo negro o texto personalizado, y actualiza la estructura del documento para que los datos redactados sean irrecuperables.

## ¿Por qué usar GroupDocs.Redaction para redactar documentos?
GroupDocs.Redaction admite **más de 30 formatos de archivo** y puede manejar archivos de hasta **2 GB** sin cargar todo el documento en memoria, ofreciendo un **30 % más rápido tiempo de procesamiento** en comparación con muchos competidores. Su API le permite aplicar redacciones por frase exacta, expresiones regulares o basadas en imágenes con una sola llamada de método, convirtiéndolo en la opción más eficiente para desarrolladores .NET.

## Requisitos previos
- **GroupDocs.Redaction** paquete NuGet (última versión).  
- .NET Framework 4.6+ **or** .NET Core 3.1+ instalado.  
- Un IDE compatible con C# como Visual Studio 2022.  
- Conocimientos básicos de C# y familiaridad con I/O de archivos.

### Bibliotecas requeridas y versiones
- **GroupDocs.Redaction** – siempre use la versión más reciente para acceder a los últimos algoritmos de redacción y parches de seguridad.  
- **System.IO** – para el manejo de streams (integrado en .NET).

### Pasos para obtener la licencia
- **Prueba gratuita:** Regístrese en el sitio web de GroupDocs para una prueba de 30 días.  
- **Licencia temporal:** Solicite una clave temporal para pruebas de desarrollo.  
- **Licencia completa:** Adquiera una licencia de producción para uso ilimitado.

## Inicialización y configuración básicas
La clase `Redactor` es el punto de entrada para todas las operaciones de redacción en GroupDocs.Redaction. Después de instalar el paquete NuGet, instancie `Redactor` con la ruta al documento fuente.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## ¿Cómo redactar texto específico en un documento?
Para redactar texto específico, cargue el archivo fuente con una instancia de `Redactor`, luego aplique una `ExactPhraseRedaction` que apunte a la cadena exacta que desea ocultar. La API escanea el documento, reemplaza cada coincidencia con la superposición elegida y registra los cambios en un registro de cambios, lo que le permite verificar la redacción antes de guardar.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

La clase `ExactPhraseRedaction` reemplaza cada aparición de la frase exacta con un rectángulo negro (o cualquier marcador de posición personalizado que configure).  

**Paso a paso:**
1. **Load** – Cree una instancia de `Redactor` apuntando a su archivo.  
2. **Apply** – Llame a `Apply` con una `ExactPhraseRedaction` (u otro tipo de redacción).  
3. **Inspect** – Revise `RedactorChangeLog` para confirmar cuántas coincidencias se encontraron y reemplazaron.  

## ¿Cómo guardar un documento redactado en un MemoryStream?
`MemoryStream` es un stream de .NET que almacena datos en memoria, permitiendo lecturas/escrituras rápidas sin I/O de disco. Usando el método `Save`, puede dirigir la salida redactada a un `MemoryStream`, que luego puede enviarse a través de una red, almacenarse en una base de datos o devolverse directamente desde un endpoint API sin crear archivos temporales.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Puntos clave:**
- El método `Save` escribe la salida redactada en cualquier implementación de `Stream`, incluido `MemoryStream`.  
- No se crean archivos temporales, lo que mejora la seguridad y el rendimiento.  
- Puede combinar esto con `FileStreamResult` de ASP.NET Core para devolver el archivo directamente al navegador.

## Problemas comunes y soluciones
| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Redacción no aplicada** | El caso de la frase difiere del origen. | Use `ExactPhraseRedaction("John Doe", caseSensitive: false)` o una redacción por expresión regular para coincidencias flexibles. |
| **Archivos grandes causan OutOfMemory** | Intentar cargar todo el archivo en memoria. | GroupDocs.Redaction procesa datos en fragmentos internamente; asegúrese de usar la última versión que procesa archivos por partes. |
| **Archivo guardado está corrupto** | El stream no se reinicia antes de enviarlo. | Después de `redactor.Save(stream)`, establezca `stream.Position = 0` antes de leer o devolverlo. |

## Preguntas frecuentes

**Q: ¿Puedo redactar archivos PDF usando la misma API?**  
A: Sí—GroupDocs.Redaction trata PDF, DOCX, PPTX y muchos formatos de imagen de manera uniforme; simplemente apunte `Redactor` a un archivo PDF.

**Q: ¿La redacción sobrevive después de convertir el documento a otro formato?**  
A: Absolutamente—una vez redactado, el contenido se elimina permanentemente, sin importar conversiones posteriores.

**Q: ¿Cómo personalizo la apariencia de la redacción?**  
A: Use `RedactionOptions` para establecer el color de superposición, la opacidad o reemplazar texto con una cadena personalizada.

**Q: ¿Es posible redactar usando expresiones regulares?**  
A: Sí—`RegexRedaction` le permite definir patrones como números de tarjeta de crédito o direcciones de correo electrónico.

**Q: ¿Qué versiones de .NET son oficialmente compatibles?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 y .NET 7.

---

**Última actualización:** 2026-07-20  
**Probado con:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Tutoriales relacionados

- [Cómo cargar y redactar documentos usando GroupDocs.Redaction .NET&#58; Guía completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Guardar documentos redactados en formato original usando GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redacción segura de documentos en .NET usando Streams&#58; Guía para GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)