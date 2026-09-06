---
date: '2026-09-06'
description: Aprende cómo obtener la extensión de archivo en Java, recuperar el tamaño
  del documento, el número de páginas y los metadatos PDF con GroupDocs.Redaction
  para Java. Mejora el manejo de documentos de tu aplicación Java hoy mismo.
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: Descubre cómo obtener la extensión de archivo en Java, el tamaño del
  documento, el número de páginas y los metadatos PDF con GroupDocs.Redaction para
  Java. Código simple, resultados rápidos.
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: Cómo obtener la extensión de archivo en Java usando GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: Cómo obtener la extensión de archivo en Java usando GroupDocs.Redaction
type: docs
url: /es/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# Cómo obtener la extensión de archivo en Java usando GroupDocs.Redaction

En aplicaciones Java modernas que procesan archivos subidos por el usuario, conocer el tipo exacto de archivo temprano—**java get file extension**—es esencial para el enrutamiento, la seguridad y la planificación de recursos. Este tutorial le muestra cómo java get file extension, obtener el tamaño del documento, el recuento de páginas e incluso recuperar los metadatos PDF usando la biblioteca GroupDocs.Redaction. Al final, tendrá una única llamada de bajo consumo de memoria que devuelve todas las propiedades clave que necesita.

## Respuestas rápidas
- **¿Qué método devuelve el tipo de archivo?** `IDocumentInfo.getFileType()`
- **¿Cómo puedo obtener el recuento de páginas?** `IDocumentInfo.getPageCount()`
- **¿Qué llamada devuelve el tamaño del documento en bytes?** `IDocumentInfo.getSize()`
- **¿Necesito una licencia para ejecutar el ejemplo?** A trial or temporary license works for evaluation.
- **¿Qué versión de Java se requiere?** Java 8 or higher.

## Qué es “java get file extension”?
**java get file extension** significa extraer programáticamente el formato de archivo (p. ej., DOCX, PDF) de un documento en Java. GroupDocs.Redaction expone esta información a través de la interfaz `IDocumentInfo`, de modo que una única llamada al método devuelve la cadena de extensión.

## Por qué usar GroupDocs.Redaction para la extracción de metadatos?
GroupDocs.Redaction puede leer metadatos de **más de 50** formatos de entrada—incluidos PDF, DOCX, XLSX, PPTX y tipos de imagen—sin cargar el archivo completo en memoria. Procesa un PDF de 300 páginas en menos de 200 ms en un servidor típico, manteniendo el uso de RAM por debajo de 20 MB. Este enfoque optimizado para el rendimiento le permite escalar trabajos por lotes mientras mantiene resultados consistentes en todos los formatos compatibles.

## Requisitos previos
- Java 8 o superior instalado.
- IDE compatible con Maven (IntelliJ IDEA, Eclipse, etc.).
- Acceso a una licencia de GroupDocs.Redaction (prueba gratuita o licencia temporal).

## Configuración de GroupDocs.Redaction para Java

### Instalación con Maven
Agregue el repositorio y la dependencia a su archivo `pom.xml`:

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
Alternativamente, descargue la última versión desde [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Obtención de licencia
- **Prueba gratuita:** Comience con una prueba gratuita para evaluar la biblioteca.  
- **Licencia temporal:** Obtenga una licencia temporal para una evaluación prolongada.  
- **Compra:** Considere comprarla si se adapta a sus necesidades.

## Por qué java get file extension es importante en proyectos del mundo real
Conocer el tipo de un documento en el momento de la carga le permite dirigir los archivos al flujo de procesamiento correcto—PDF a redacción, archivos Word a conversión, imágenes a OCR. También permite verificaciones de seguridad (bloqueo de archivos ejecutables) y iconos de UI precisos en los sistemas de gestión documental.

## Cómo java get file extension, obtener el tamaño del documento java y obtener el recuento de páginas java
Puede recuperar el tipo de archivo, el tamaño y el recuento de páginas con una única llamada a `IDocumentInfo`. Esta llamada lee solo el encabezado del documento, por lo que incluso los archivos grandes se procesan rápidamente y con un consumo mínimo de memoria. Este enfoque ligero es ideal para el procesamiento por lotes donde solo se requiere información resumida antes de decidir acciones posteriores. La interfaz `IDocumentInfo` proporciona metadatos como tipo de archivo, recuento de páginas y tamaño sin cargar el documento completo.

### Paso 1: importar clases necesarias
Agregue las importaciones requeridas al inicio de su archivo Java:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### Paso 2: inicializar el redactor
La clase `Redactor` es el motor central que abre un documento y proporciona acceso a sus metadatos.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### Paso 3: recuperar y mostrar la información del documento
`IDocumentInfo` proporciona los metadatos que necesita. Llame a `getDocumentInfo()` una vez y luego consulte las tres propiedades.

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

Las tres sentencias `System.out.println` imprimen el tipo de archivo, el recuento de páginas y el tamaño en bytes—exactamente los datos que necesita para el procesamiento posterior.

## Cómo recuperar metadatos PDF java
Cargue el PDF con `Redactor` y llame a `getDocumentInfo()`. El mismo método devuelve campos específicos de PDF como la versión y el estado de cifrado, por lo que no se requiere código adicional. El objeto `IDocumentInfo` devuelto también contiene campos específicos de PDF como el número de versión, la bandera de cifrado y los metadatos estándar (autor, título, fecha de creación). Puede acceder a estas propiedades directamente con métodos getter, lo que le permite mostrar o registrar los detalles del PDF sin análisis adicional.

## Casos de uso comunes
1. **Sistemas de gestión documental:** Auto‑categorizar archivos por tipo o tamaño antes de almacenarlos.  
2. **Canales de procesamiento de contenido:** Elegir diferentes estrategias de procesamiento según el recuento de páginas (p. ej., redactar por lotes PDFs grandes vs. documentos Word pequeños).  
3. **Bibliotecas de activos digitales:** Mostrar a los usuarios vistas rápidas de las propiedades del documento sin abrir el archivo.

## Problemas comunes y soluciones
- **Archivo no encontrado:** Verifique la ruta absoluta o relativa que pasa a `Redactor`.  
- **Formato no compatible:** Asegúrese de que la extensión de su documento esté entre los más de 50 formatos compatibles con GroupDocs.Redaction.  
- **Errores de licencia:** Use una prueba válida o una licencia permanente; de lo contrario la API lanza una excepción de licencia.

## Consejos de solución de problemas (read document metadata java)
- Envuélvalas llamadas a metadatos en un bloque `try‑catch` para manejar archivos corruptos de forma elegante.  
- Utilice `redactor.isEncrypted()` (si está disponible) para detectar PDFs cifrados antes de leer los metadatos.  
- Al procesar muchos archivos, reutilice un pool de hilos y cierre cada instancia de `Redactor` rápidamente para evitar fugas de manejadores de archivo.

## Consideraciones de rendimiento
Al manejar lotes grandes:
- Abra cada documento en un bloque `try‑with‑resources` para garantizar la liberación oportuna de los manejadores de archivo.  
- Cache solo los metadatos que necesita; evite cargar el contenido completo del documento a menos que sea necesario.  

## Preguntas frecuentes
**P: ¿Qué es GroupDocs.Redaction?**  
R: GroupDocs.Redaction es una biblioteca Java que permite la redacción, extracción de metadatos y procesamiento de documentos independiente del formato en más de 50 tipos de archivo.

**P: ¿Puedo recuperar metadatos de archivos PDF?**  
R: Sí, `IDocumentInfo` devuelve la versión del PDF, el estado de cifrado y los metadatos básicos sin código adicional.

**P: ¿Cómo manejo excepciones al recuperar la información del documento?**  
R: Envuélvase la llamada `getDocumentInfo()` en un bloque `try‑catch` y maneje `RedactionException` para gestionar archivos corruptos o no compatibles.

**P: ¿Qué tipo de información puedo obtener sobre un documento?**  
R: Tipo de archivo, número de páginas, tamaño en bytes, versión del PDF, bandera de cifrado y metadatos básicos de autor/creación.

**P: ¿Existe soporte para procesar por lotes muchos documentos de manera eficiente?**  
R: Sí, instancie un `Redactor` separado para cada archivo dentro de un pool de hilos y reutilice la misma JVM para lograr un alto rendimiento.

## Conclusión
Ahora sabe cómo **java get file extension**, **get document size java**, **get page count java** y **retrieve pdf metadata java** usando GroupDocs.Redaction. Integre estos fragmentos en sus aplicaciones Java para tomar decisiones más inteligentes sobre el manejo de documentos, mejorar el rendimiento y ofrecer experiencias de usuario más ricas.

---

**Última actualización:** 2026-09-06  
**Probado con:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

**Recursos**  
- **Documentación:** [Documentación de GroupDocs Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **Referencia API:** [Referencia API de GroupDocs](https://reference.groupdocs.com/redaction/java)  
- **Descarga:** [Descargas de GroupDocs.Redaction para Java](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [Repositorio GitHub de GroupDocs](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Soporte gratuito:** [Foro de GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **Licencia temporal:** [Obtener una licencia temporal](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Tutoriales relacionados

- [java leer metadatos de archivo – tipo de archivo con GroupDocs.Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Generar vista previa y recuento de páginas de documento – GroupDocs Java](/redaction/java/document-information/)
- [Cómo previsualizar una página con GroupDocs.Redaction para Java – Guía completa](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)