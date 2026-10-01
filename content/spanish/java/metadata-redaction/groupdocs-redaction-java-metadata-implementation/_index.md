---
date: '2026-10-01'
description: Aprende cómo eliminar los metadatos de autor y guardar archivos de documentos
  redactados en Java usando GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Aprende cómo eliminar los metadatos de autor y guardar archivos de
  documentos redactados en Java usando GroupDocs Redaction. Sigue la guía paso a paso.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Cómo eliminar los metadatos de autor en Java con GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Cómo eliminar los metadatos de autor en Java con GroupDocs
type: docs
url: /es/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Cómo eliminar los metadatos del autor en Java con GroupDocs

En el panorama digital actual, proteger la información sensible oculta dentro de los documentos es una práctica indispensable. **Eliminar los metadatos del autor** evita la divulgación accidental de identificadores personales o corporativos. Este tutorial le muestra, paso a paso, cómo usar `EraseMetadataRedaction` de GroupDocs.Redaction para Java para eliminar campos como *Author* y *Manager* de archivos Word, y luego **guardar copias del documento redactado** de forma segura para compartir o archivar.

## Respuestas rápidas
- **¿Qué hace EraseMetadataRedaction?** Elimina los campos de metadatos seleccionados de un documento.  
- **¿Qué biblioteca proporciona esta función?** GroupDocs.Redaction para Java.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para pruebas; se requiere una licencia permanente para producción.  
- **¿Puedo apuntar a varios campos a la vez?** Sí, combine filtros con un OR lógico.  
- **¿El proceso es thread‑safe?** Las instancias de Redactor no se comparten entre hilos; cree una nueva instancia por operación.

## Qué es EraseMetadataRedaction?
`EraseMetadataRedaction` es una clase de redacción incorporada que le permite especificar qué entradas de metadatos deben ser borradas. Funciona con una amplia gama de formatos de documento compatibles con GroupDocs.Redaction, garantizando que la información de autoría oculta nunca se filtre. Puede apuntar a propiedades estándar como Author, Manager, y también a campos de metadatos personalizados, proporcionando una protección de privacidad integral.

## Por qué usar EraseMetadataRedaction con GroupDocs?
GroupDocs.Redaction soporta **más de 100 formatos de entrada y salida** y puede procesar documentos de hasta 500 páginas sin cargar todo el archivo en memoria. Usar esta clase le brinda una API única y de alto rendimiento para cumplir con los requisitos de GDPR, HIPAA o cumplimiento interno, mientras mantiene su base de código simple.

## Requisitos previos
- Java 8 o superior instalado.  
- Maven (o la capacidad de agregar JARs manualmente).  
- GroupDocs.Redaction para Java (versión 24.9 o posterior).  
- Una licencia válida de prueba o permanente de GroupDocs.

## Configuración de GroupDocs.Redaction para Java

### Instalación con Maven
Add the GroupDocs repository and dependency to your **pom.xml**:

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
Alternativamente, descargue el último JAR desde [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Obtención de licencia
Obtenga una prueba gratuita o compre una licencia temporal desde el portal de GroupDocs. El archivo de licencia debe colocarse donde su aplicación pueda cargarlo (p. ej., raíz del classpath).

### Inicialización y configuración básica
Below is a minimal example that creates a `Redactor` instance for a DOCX file:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Cómo usar EraseMetadataRedaction en Java
Las siguientes secciones desglosan la implementación en pasos claros y accionables.

### Función: limpiar elementos de metadatos específicos

#### Visión general
Eliminaremos los campos de metadatos **Author** y **Manager** usando `EraseMetadataRedaction`. Este es un requisito común al compartir informes internos con socios externos.

#### Implementación paso a paso

##### 1️⃣ Inicializar el objeto Redactor
`Redactor` is the core class that loads a document, applies redaction objects, and writes the result. Create a new instance for each file you process:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Aplicar EraseMetadataRedaction
`MetadataFilters` provides predefined filters for common metadata keys such as Author and Manager.  
`EraseMetadataRedaction` removes metadata entries that match the supplied `MetadataFilters`. The bitwise OR (`|`) combines the `Author` and `Manager` filters so both fields are removed in one call:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configurar opciones de guardado
`SaveOptions` lets you specify the output file name, format, and other saving parameters.  
`SaveOptions` lets you control the output file name, format, and whether the document should be rasterized to PDF. Adding a suffix keeps the original file untouched:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Casos de uso comunes
1. **Documentos legales** – Redactar la información del autor antes de enviar contratos a la parte contraria.  
2. **Informes corporativos** – Eliminar los nombres de los gerentes al publicar resultados trimestrales a los accionistas.  
3. **Archivos de proyecto** – Limpiar la documentación interna del proyecto antes de archivarla o subirla a un repositorio público.

## Consejos de solución de problemas
- **Archivo no encontrado** – Verifique que la ruta en `inputFilePath` apunte a un archivo existente y que la aplicación tenga permisos de lectura.  
- **Campos de metadatos faltantes** – No todos los tipos de documento almacenan las mismas claves de metadatos; verifique primero las propiedades del documento en Office.  
- **Errores de licencia** – Asegúrese de que el archivo de licencia se cargue correctamente antes de crear la instancia `Redactor`.

## Consideraciones de rendimiento
- Cierre el objeto `Redactor` rápidamente (como se muestra en el bloque `finally`) para liberar recursos nativos.  
- Evite rasterizar documentos grandes a menos que necesite una vista previa en PDF; la rasterización puede aumentar el uso de CPU y memoria hasta 3× para archivos de 300 páginas.

## Preguntas frecuentes

**Q1: ¿Qué es la redacción de metadatos?**  
A1: La redacción de metadatos implica eliminar propiedades ocultas del documento (como autor, gerente o etiquetas personalizadas) para evitar la divulgación accidental de información sensible.

**Q2: ¿Puedo usar GroupDocs.Redaction para otros tipos de archivo?**  
A2: Sí, la biblioteca soporta PDF, DOCX, PPTX, XLSX y muchos más formatos—más de 100 en total.

**Q3: ¿Cómo manejo los errores durante la redacción?**  
A3: Envuelva la llamada `apply` en un bloque try‑catch y siempre cierre el `Redactor` en una cláusula finally para asegurar que los recursos se liberen.

**Q4: ¿Es posible redactar campos de metadatos personalizados?**  
A5: Absolutamente. Use `MetadataFilters.Custom("YourFieldName")` para apuntar a cualquier propiedad personalizada almacenada en el documento.

**Q5: ¿Cuáles son las mejores prácticas para usar GroupDocs.Redaction?**  
A5:  
- Cargue la licencia al inicio de su aplicación.  
- Cierre los objetos `Redactor` rápidamente.  
- Use `SaveOptions` para añadir un sufijo, manteniendo los archivos originales sin tocar.  
- Pruebe la redacción en una copia del documento antes de procesar lotes.

**Q6: ¿EraseMetadataRedaction admite operaciones por lotes?**  
A6: Puede iterar sobre una colección de rutas de archivo, creando un nuevo `Redactor` para cada archivo y aplicando la misma lógica de redacción.

**Q7: ¿Puedo combinar EraseMetadataRedaction con otros tipos de redacción?**  
A7: Sí, puede encadenar múltiples objetos de redacción (p. ej., redacción de texto seguida de redacción de metadatos) antes de guardar.

## Recursos

- **Documentación**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referencia de API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Descarga**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Soporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Licencia temporal**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última actualización:** 2026-10-01  
**Probado con:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Extracción de metadatos de documentos Java con GroupDocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Cómo eliminar metadatos en Java usando GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Recuperar información del documento usando GroupDocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)