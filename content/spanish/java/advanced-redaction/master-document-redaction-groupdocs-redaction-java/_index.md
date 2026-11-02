---
date: '2026-11-02'
description: Aprenda cómo agregar un sufijo al nombre de archivo en un tutorial de
  GroupDocs redaction Java usando Maven, streaming load, annotation deletion y save
  options.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Aprenda cómo agregar un sufijo al nombre de archivo en un tutorial
  de GroupDocs redaction Java. Siga la configuración paso a paso de Maven, streaming
  load y save options.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Cómo agregar un sufijo al nombre de archivo en GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Cómo agregar un sufijo al nombre de archivo en GroupDocs redaction Java
type: docs
url: /es/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cómo agregar un sufijo al nombre de archivo en GroupDocs redaction Java

En este **groupdocs redaction java tutorial** aprenderás cómo agregar automáticamente un sufijo al nombre del archivo de salida al redactar documentos con GroupDocs.Redaction. Añadir un sufijo elimina la renombración manual, reduce el riesgo de filtrar archivos no redactados y encaja perfectamente en pipelines CI/CD que dependen de convenciones de nombres. La guía te lleva a través de la configuración de Maven, la carga de documentos mediante streaming, la eliminación de anotaciones y la configuración de opciones de guardado, todo con código conciso y listo para producción.

## Respuestas rápidas
- **¿Qué hace “add suffix to filename”?**  
  Cuando habilitas la opción de sufijo, el SDK agrega automáticamente una cadena predefinida (por defecto “_redacted”) al nombre base del archivo de salida antes de la extensión. Esto permite identificar de inmediato qué archivos han sido procesados, ayuda a prevenir la distribución accidental del contenido original y simplifica la automatización posterior que depende de patrones de nombres.  
- **¿Puedo cargar un documento desde un stream?**  
  Sí—GroupDocs.Redaction admite la carga desde cualquier `InputStream`, ideal para almacenamiento en la nube o procesamiento en memoria.  
- **¿Necesito una licencia para esta función?**  
  Una prueba gratuita funciona para redacción básica; una licencia temporal o completa desbloquea todas las opciones avanzadas, incluido el manejo de sufijos.  
- **¿Qué formatos son compatibles?**  
  La biblioteca maneja DOCX, PDF, PPTX, XLSX y muchos más.  
- **¿Es necesaria la rasterización para la salida PDF?**  
  La rasterización es opcional; habilítala cuando necesites aplanar el documento para mayor seguridad.

## Qué hace “add suffix to filename”

Cuando habilitas la opción de sufijo, el SDK agrega automáticamente una cadena predefinida (por defecto “_redacted”) al nombre base del archivo de salida antes de la extensión. Esto permite identificar de inmediato qué archivos han sido procesados, ayuda a prevenir la distribución accidental del contenido original y simplifica la automatización posterior que depende de patrones de nombres.

## Por qué usar GroupDocs.Redaction para esta tarea

GroupDocs.Redaction ofrece una API Java de alto rendimiento que combina acciones de redacción con opciones flexibles de manejo de archivos, como la adición automática de sufijos, soporte de streaming y procesamiento por lotes. Soporta más de 50 formatos de entrada y salida y puede procesar documentos de cientos de páginas sin cargar todo el archivo en memoria, garantizando bajo consumo de memoria y ejecución rápida.

## Requisitos previos

- **Java Development Kit (JDK):** Versión 8 o superior.  
- **GroupDocs.Redaction Library:** Biblioteca central para tareas de redacción.  
- **IDE:** IntelliJ IDEA, Eclipse o cualquier editor compatible con Java.  
- **Maven:** Para la gestión de dependencias.  

### Prerrequisitos de conocimiento
Familiaridad con Java I/O y conceptos básicos de programación orientada a objetos facilitará el seguimiento de los ejemplos.

## Configuración de GroupDocs.Redaction para Java

### Configuración de Maven
Incluye la siguiente configuración en tu archivo `pom.xml` para acceder a las bibliotecas de GroupDocs mediante Maven:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Descarga directa
Alternativamente, descarga la última versión directamente desde [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Obtención de licencia
1. **Free trial:** Accede a la funcionalidad básica sin restricciones.  
2. **Temporary license:** Obtén una licencia temporal para explorar características avanzadas.  
3. **Purchase:** Para uso a largo plazo, considera adquirir una licencia completa.

#### Inicialización y configuración básicas
Inicializa tu proyecto añadiendo las importaciones necesarias:

```java
import com.groupdocs.redaction.Redactor;
```

Con esta configuración, estás listo para implementar funcionalidades de redacción de documentos.

## Guía de implementación

### Función 1: cargar documento desde stream
**Visión general:** Aprende cómo cargar documentos en un `InputStream` para procesarlos.

`InputStream` es una clase de Java I/O que representa un flujo de bytes, permitiéndote leer datos de archivos, conexiones de red u otras fuentes sin cargar todo el contenido en memoria.

#### Paso 1.1: crear inputstream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Why:** Usar `InputStream` te permite manejar documentos almacenados en diversas ubicaciones—buckets en la nube, bases de datos o buffers en memoria—sin escribirlos primero en disco. Este enfoque es esencial cuando necesitas **load document from stream** en arquitecturas de micro‑servicios.

### Función 2: aplicar redacción de eliminación de anotaciones
**Visión general:** Elimina anotaciones de tu documento usando `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` es una operación de redacción que elimina todas las anotaciones—como comentarios, resaltados y notas—del documento.

#### Paso 2.1: aplicar deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Why:** Este paso garantiza que cualquier anotación sensible (comentarios, resaltados o notas ocultas) se elimine del documento, mejorando la privacidad y el cumplimiento.

### Función 3: guardar documento con opciones
**Visión general:** Aprende cómo guardar tu documento procesado con opciones específicas como rasterización y **add suffix filename java**.

`SaveOptions` encapsula la configuración que controla cómo se escribe el documento redactado, incluyendo formato, rasterización y convenciones de nombres.

#### Paso 3.1: configurar saveoptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Why:** Personalizar las opciones de guardado permite formatos de salida flexibles y convenciones de nombres. Habilitar `setAddSuffix(true)` **adds suffix to filename**, dejando claro que el archivo ha sido redactado.

## Cómo agregar sufijo al nombre de archivo java al guardar un documento?

La clase `Redactor` es el componente central que carga un documento y aplica operaciones de redacción. `SaveOptions` define cómo se guarda el documento redactado, incluyendo formato, rasterización y convenciones de nombres. Crea una instancia de `Redactor`, aplica las redacciones necesarias y luego configura un objeto `SaveOptions` con `setAddSuffix(true)`. Llama a `redactor.save(outputPath, options)`. El SDK agrega automáticamente “_redacted” (o el sufijo configurado) al nombre del archivo, por lo que nunca tendrás que renombrarlo manualmente.

## Visión general de la dependencia Maven de GroupDocs

La **groupdocs maven dependency** incorpora todo el SDK de Redaction en tu proyecto con una única entrada `<dependency>`. Gestiona dependencias transitivas, mantiene las bibliotecas actualizadas y simplifica la automatización de compilaciones. Al declarar la dependencia en `pom.xml`, evitas la gestión manual de JARs y garantizas compatibilidad con los últimos parches de seguridad.

## Por qué es importante agregar un sufijo

Agregar un sufijo brinda una confirmación visual inmediata de que un archivo ha sido procesado, lo cual es crítico para auditorías, flujos de trabajo automatizados y cumplimiento regulatorio. Permite que los scripts filtren archivos redactados, previene la distribución accidental del contenido original y satisface muchos estándares de la industria que exigen un etiquetado claro de documentos sanitizados.

## Aplicaciones prácticas

1. **Redacción de documentos legales:** Asegura contratos antes de compartirlos con el cliente.  
2. **Manejo de registros médicos:** Protege identificadores de pacientes mientras se conserva la información clínica.  
3. **Informes financieros:** Mantén números sensibles confidenciales durante auditorías externas.  
4. **Integración CRM:** Redacta automáticamente datos de clientes antes de exportarlos a herramientas de terceros.  
5. **Herramientas de colaboración:** Garantiza que los borradores compartidos nunca expongan comentarios ocultos o metadatos.

## Consideraciones de rendimiento

### Optimización del rendimiento
- Usa streaming (`load document from stream`) para evitar cargar archivos completos en memoria.  
- Cierra las instancias de `Redactor` rápidamente para liberar recursos.  

### Directrices de uso de recursos
- Monitorea CPU y memoria durante ejecuciones por lotes.  
- Prefiere `ByteArrayOutputStream` para guardados en memoria cuando trabajes con archivos de tamaño moderado.

### Mejores prácticas para la gestión de memoria en Java
- Reutiliza objetos `Redactor` al procesar varios archivos del mismo tipo.  
- Invoca `close()` dentro de un bloque `try‑with‑resources` para prevenir fugas.

## Problemas comunes y soluciones
| Issue | Cause | Fix |
|-------|-------|-----|
| **El sufijo no aparece** | `setAddSuffix(false)` o llamada faltante | Asegúrate de que `options.setAddSuffix(true)` esté configurado antes de `save()`. |
| **OutOfMemoryError en DOCX grande** | Cargar todo el archivo en memoria | Cambia a carga mediante `InputStream` (ver Función 1). |
| **Las anotaciones siguen visibles** | Redacción no aplicada antes de guardar | Llama a `redactor.apply(new DeleteAnnotationRedaction())` antes de `save()`. |
| **Rasterización PDF no aplicada** | `setRasterizeToPDF(false)` u omitido | Configura `options.setRasterizeToPDF(true)` cuando necesites un PDF aplanado. |

## Preguntas frecuentes

**Q: ¿Puedo redactar documentos PDF usando GroupDocs.Redaction?**  
A: Sí, la biblioteca soporta PDFs, DOCX, PPTX, XLSX y muchos otros formatos.

**Q: ¿Cuál es la mejor manera de manejar archivos grandes con GroupDocs.Redaction?**  
A: Usa streaming (`load document from stream`) y cierra los recursos rápidamente para mantener bajo el uso de memoria.

**Q: ¿Es posible personalizar el texto del sufijo?**  
A: La API agrega automáticamente un sufijo predeterminado (p. ej., “_redacted”). Para sufijos personalizados, renombra el archivo de salida después de guardarlo.

**Q: ¿Cómo obtengo una licencia temporal para GroupDocs.Redaction?**  
A: Visita la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) y sigue las instrucciones.

**Q: ¿Dónde puedo obtener ayuda si encuentro problemas?**  
A: Únete al [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) para recibir asistencia de expertos.

## Recursos
- **Documentation:** Explora guías detalladas en [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API reference:** Accede a detalles completos de la API en [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Obtén la última versión desde [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repository:** Contribuye o explora el código fuente en [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Última actualización:** 2026-11-02  
**Probado con:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

## Tutoriales relacionados

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)