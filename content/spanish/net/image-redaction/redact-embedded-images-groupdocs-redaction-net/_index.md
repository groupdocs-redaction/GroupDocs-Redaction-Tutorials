---
date: '2026-10-16'
description: Aprenda cómo usar GroupDocs para redactar imágenes incrustadas en documentos
  de Word utilizando la API .NET de GroupDocs.Redaction, manteniendo seguros los datos
  sensibles.
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: Cómo usar GroupDocs para redactar imágenes incrustadas en documentos
  de Word con la API .NET. Proteja visuales confidenciales de forma rápida y fiable.
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: Cómo usar GroupDocs para redactar imágenes en Word con .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: Cómo usar GroupDocs para redactar imágenes en Word con .NET
type: docs
url: /es/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar GroupDocs para redactar imágenes en Word con .NET

Cuando necesitas proteger imágenes confidenciales en un archivo Microsoft Word, **cómo usar GroupDocs** se convierte en la primera pregunta. Este tutorial te guía paso a paso para localizar, enmascarar y eliminar permanentemente las imágenes incrustadas, de modo que la información sensible nunca se filtre.

## Respuestas rápidas
- **¿Puede GroupDocs redactar todas las imágenes automáticamente?** Sí, puedes iterar sobre cada imagen y aplicar `ImageAreaRedaction`.
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para pruebas; se requiere una licencia permanente para producción.
- **¿Se conservará el diseño original?** La API mantiene el texto y el formato intactos mientras enmascara el área de la imagen.
- **¿Qué tan rápido es el proceso?** GroupDocs.Redaction puede manejar documentos de 200 páginas en menos de 2 segundos en un servidor típico.

## Qué es GroupDocs.Redaction?
GroupDocs.Redaction es una biblioteca .NET que permite la redacción programática de texto, imágenes y metadatos en más de 20 formatos de documento. Procesa archivos sin requerir Microsoft Office instalado, lo que la hace ideal para automatización del lado del servidor. Ofrece APIs para redactar texto, imágenes y metadatos, y soporta procesamiento por lotes, patrones de redacción personalizados e informes de cumplimiento.

## ¿Por qué usar GroupDocs para la redacción de imágenes en Word?
La biblioteca soporta **más de 20 formatos de entrada y salida** y puede redactar imágenes en documentos de hasta 500 MB sin cargar todo el archivo en memoria. Su algoritmo incorporado `ImageAreaRedaction` garantiza que la región redactada no pueda recuperarse, cumpliendo con estrictas normas de cumplimiento.

## Requisitos previos
- .NET Framework 4.5+ **or** .NET Core 3.1+ instalado.
- Conocimientos básicos de C# y familiaridad con la estructura de archivos Word.
- Acceso al paquete NuGet **GroupDocs.Redaction** (prueba gratuita o con licencia).

## Cómo configurar GroupDocs.Redaction para .NET

### ¿Cómo instalar GroupDocs.Redaction mediante .NET CLI?
Ejecuta el siguiente comando en la carpeta de tu proyecto: `dotnet add package GroupDocs.Redaction`. Esto agrega la última versión estable a tu archivo de proyecto.

```bash
dotnet add package GroupDocs.Redaction
```

### ¿Cómo instalar GroupDocs.Redaction usando Package Manager?
Ejecuta `Install-Package GroupDocs.Redaction` en la consola del Package Manager.

```powershell
Install-Package GroupDocs.Redaction
```

### ¿Cómo obtener y aplicar una licencia temporal?
Puedes solicitar una licencia temporal desde la página de [Licencia Temporal](https://purchase.groupdocs.com/temporary-license/).  
Una licencia temporal te permite evaluar el conjunto completo de funciones sin marcas de agua. Después de la compra, coloca el archivo de licencia en tu proyecto y cárgalo como se muestra:

```csharp
using GroupDocs.Redaction;
```

## ¿Cómo redactar imágenes incrustadas en un documento Word?

Para redactar imágenes, cargas el documento con una instancia de Redactor, localizas cada picture, defines el área a ocultar y aplicas ImageAreaRedaction. La API sobrescribe los píxeles seleccionados, asegurando que el contenido visual original no pueda recuperarse, mientras preserva el diseño y el texto circundante.

### ¿Cómo preparar las rutas de origen y salida?
Define las rutas absolutas para el documento original y el resultado redactado antes de crear cualquier objeto.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### ¿Cómo crear y configurar el objeto Redactor?
Redactor es la clase central que carga un documento y realiza operaciones de redacción.  
Crea una instancia de `Redactor` con tu documento:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### ¿Cómo especificar coordenadas y aplicar la redacción de área de imagen?
ImageAreaRedaction es un método que enmascara una región rectangular de una imagen con un color sólido.  
Identifica el punto superior‑izquierdo (`samplePoint`) y el tamaño (`sampleSize`) de la región que deseas ocultar, luego llama a `ImageAreaRedaction`. Este método sobrescribe los píxeles seleccionados con un color sólido.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### ¿Cómo verificar el resultado de la redacción y guardar el archivo?
Después de llamar a `Redactor.Apply()`, inspecciona el objeto `Result`. Si `IsSuccess` es verdadero, escribe el documento modificado en la ruta de salida.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## Problemas comunes y consejos de solución
- **Errores de coordenadas:** Asegúrate de que los valores X/Y estén dentro de los límites de la imagen; de lo contrario la API lanza una `ArgumentOutOfRangeException`.
- **Licencia faltante:** Una licencia de prueba expira después de 30 días; reemplázala por una permanente para evitar fallos en tiempo de ejecución.
- **Formato no compatible:** Verifica que la extensión del archivo esté entre los más de 20 formatos listados en la documentación; los archivos `.doc` más antiguos pueden necesitar conversión a `.docx` primero.

## Aplicaciones prácticas

1. **Informes confidenciales:** Redactar logotipos o gráficos antes de la distribución externa.
2. **Memorandos legales:** Ocultar fotografías de clientes o identificaciones escaneadas que contengan datos personales.
3. **Contratos comerciales:** Enmascarar diagramas propietarios que revelen secretos comerciales.
4. **Publicaciones gubernamentales:** Eliminar imágenes satelitales sensibles de PDFs públicos generados a partir de Word.

## Consideraciones de rendimiento
- Procesa los documentos secuencialmente al manejar lotes grandes para mantener bajo el uso de memoria.
- Usa `RedactorOptions` para limitar el número de hilos si ejecutas en un servidor con recursos limitados.
- Libera la instancia de `Redactor` rápidamente con `using` para liberar recursos no administrados.

## Conclusión
Ahora sabes **cómo usar GroupDocs** para redactar de forma fiable imágenes incrustadas en archivos Word usando la API .NET. Siguiendo los pasos anteriores, puedes integrar esta capacidad en cualquier canal de procesamiento de documentos, garantizando que los visuales confidenciales nunca abandonen tu organización.

Para una exploración más profunda, experimenta con otros tipos de redacción (texto, metadatos) e integra la biblioteca en servicios web, workers en segundo plano o Azure Functions.

## Preguntas frecuentes

**P: ¿Puedo redactar varias imágenes en una sola pasada?**  
R: Sí, itera sobre cada nodo picture y llama a `ImageAreaRedaction` para cada región que necesites ocultar.

**P: ¿GroupDocs.Redaction soporta archivos Word protegidos con contraseña?**  
R: Absolutamente. Proporciona la contraseña al construir el objeto `Redactor`, y la biblioteca abrirá el documento de forma segura.

**P: ¿Qué formatos de archivo puedo procesar además de DOCX?**  
R: La API maneja DOC, DOCX, RTF, HTML, PDF y más de 20 formatos adicionales, lo que te permite crear un servicio universal de redacción.

**P: ¿Cómo probar la redacción sin una licencia?**  
R: Usa una licencia temporal del portal de GroupDocs; habilita la funcionalidad completa durante 30 días sin marcas de agua.

**P: ¿Dónde puedo obtener ayuda si tengo problemas?**  
R: Visita el foro de [Soporte gratuito de GroupDocs](https://forum.groupdocs.com/c/redaction/33) para asistencia de la comunidad o contacta al equipo de ventas de GroupDocs para soporte empresarial.

## Recursos adicionales

- **Documentación:** [Documentación de GroupDocs Redaction](https://docs.groupdocs.com/redaction/net/)
- **Referencia de API:** [Referencia de API de GroupDocs](https://reference.groupdocs.com/redaction/net)
- **Descarga:** [Últimas versiones](https://releases.groupdocs.com/redaction/net/)

---

**Last Updated:** 2026-10-16  
**Tested with:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## Tutoriales relacionados

- [Cómo redactar documentos con GroupDocs.Redaction .NET – Guía completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redactar y guardar documentos GroupDocs Redaction .NET](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Dominar la redacción de frases exactas sensible a mayúsculas con GroupDocs.Redaction .NET para seguridad de documentos](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}