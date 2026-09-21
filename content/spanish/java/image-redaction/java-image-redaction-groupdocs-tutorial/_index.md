---
date: '2026-09-21'
description: Aprenda a redactar una imagen con GroupDocs.Redaction para Java. Guía
  paso a paso que cubre la configuración, la redacción a nivel de píxel, la verificación
  y las mejores prácticas.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Cómo redactar una imagen con GroupDocs.Redaction para Java. Siga esta
  guía para ocultar datos de píxeles en archivos escaneados, elegir colores y verificar
  resultados, ideal para el cumplimiento de GDPR y HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Cómo redactar una imagen usando GroupDocs.Redaction para Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Cómo redactar una imagen usando GroupDocs.Redaction para Java
type: docs
url: /es/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Cómo redactar imágenes usando GroupDocs.Redaction para Java

En este tutorial exhaustivo aprenderás **cómo redactar imágenes** en Java con GroupDocs.Redaction. Redactar imágenes escaneadas es un paso crucial para proteger datos personales, cumplir con GDPR, HIPAA u otras regulaciones de privacidad, y garantizar que la información visual confidencial nunca se filtre. Te guiaremos a través de la configuración del proyecto, la configuración de la redacción a nivel de píxel, el guardado seguro del resultado y la confirmación de que la redacción se realizó con éxito, todo presentado en un estilo conversacional paso a paso que puedes copiar en cualquier aplicación Java.

## Respuestas rápidas
- **¿Qué biblioteca maneja la redacción de imágenes en Java?** GroupDocs.Redaction for Java.  
- **¿Puedo elegir el color de redacción?** Sí – cualquier `java.awt.Color` opaco como `Color.BLUE` o `Color.BLACK`.  
- **¿Se requiere una licencia para producción?** Sí, una licencia válida de GroupDocs es obligatoria para uso comercial.  
- **¿Se sobrescribirá la imagen original?** No – la API escribe la imagen redactada en un nuevo archivo que especifiques.  
- **¿Qué versión de Java es compatible?** Java 8 y posteriores (hasta Java 21 al momento de escribir).

## Qué es la redacción de imágenes y por qué redactar imágenes escaneadas en Java
La redacción de imágenes oculta permanentemente datos visuales—nombres, números, firmas—reemplazando regiones de píxeles con un color sólido. A diferencia de la redacción de texto, que actúa sobre caracteres seleccionables, las imágenes escaneadas almacenan la información como píxeles crudos, por lo que solo las herramientas basadas en píxeles pueden garantizar que los datos no se recuperen. Con GroupDocs.Redaction puedes apuntar a coordenadas exactas, aplicar cualquier color opaco y producir una nueva imagen que elimina el contenido sensible de forma definitiva.

## ¿Por qué usar GroupDocs.Redaction para Java?
GroupDocs.Redaction soporta **más de 50 formatos de imagen** (incluidos JPG, PNG, BMP, GIF) y puede procesar documentos de cientos de páginas sin cargar todo el archivo en memoria, gracias a su arquitectura de streaming. Las pruebas de rendimiento muestran que un PNG escaneado de 300 KB se redacta en menos de 120 ms en una CPU típica de 2.8 GHz, lo que lo hace adecuado tanto para trabajos por lotes como para servicios en tiempo real.

## Requisitos previos
- **JDK 8 o posterior** instalado y configurado en tu `PATH`.  
- **Maven** (o Gradle) para la gestión de dependencias.  
- Un IDE como **IntelliJ IDEA**, **Eclipse** o **NetBeans**.  
- Familiaridad básica con la E/S de archivos Java y el paquete `java.awt`.  

## Configuración de GroupDocs.Redaction para Java

### Configuración de Maven
Agrega el repositorio de GroupDocs y la dependencia a tu `pom.xml`:

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
Alternativamente, descarga el JAR más reciente desde la página oficial de lanzamientos: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Obtención de licencia
- **Prueba gratuita:** Regístrate para una prueba y explorar la API completa.  
- **Licencia temporal:** Usa una clave temporal para pruebas extendidas sin costo.  
- **Compra completa:** Obtén una licencia de producción para despliegue ilimitado.

## Guía de implementación

Dividiremos la implementación en dos características principales: **redacción de áreas de imagen** (el enmascarado real) y **comprobación del estado de la redacción** (verificar el éxito).

### Cómo redactar imágenes de documentos escaneados – paso 1: inicializar el redactor
`Redactor` es la clase central que carga una imagen y proporciona operaciones de redacción.  
Crea una instancia de `Redactor` que apunte a la imagen fuente que deseas procesar.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Paso 2: definir parámetros de redacción
`ImageAreaRedaction` funciona con un `Point` (esquina superior izquierda) y un `Dimension` (ancho × alto) que describen el rectángulo a ocultar. En este ejemplo usamos un color de relleno azul.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Paso 3: aplicar la redacción
`RegionReplacementOptions` te permite especificar el color de relleno y un borde opcional. Pasar estas opciones a `ImageAreaRedaction` e invocar `apply()` realiza el enmascarado. El método devuelve un `RedactorChangeLog` que indica éxito o fracaso.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Paso 4: liberar recursos
`Redactor` implementa `AutoCloseable`. Cerrarlo libera buffers nativos y manejadores de archivos, evitando fugas de memoria en servicios de larga duración.

```java
redactor.close();
```

### Cómo verificar la redacción – comprobación de estado
Después de aplicar la redacción, inspecciona el `RedactorChangeLog`. Un valor `Status.SUCCESS` confirma que la región de píxeles fue reemplazada sin error. También puedes renderizar la imagen a un `BufferedImage` para una inspección visual antes de guardarla.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Aplicaciones prácticas
- **Manejo de documentos confidenciales:** Ocultar datos personales en contratos escaneados antes de compartirlos con socios.  
- **Documentación legal:** Garantizar el cumplimiento de GDPR o HIPAA redactando identificadores en imágenes de evidencia.  
- **Registros médicos:** Ocultar rostros de pacientes o notas manuscritas en escaneos de radiología mientras se preservan los detalles diagnósticos.  

## Consideraciones de rendimiento
- **Procesamiento por lotes:** Procesa imágenes en grupos de 10–20 para mantener el uso de memoria bajo 200 MB.  
- **Reutilización de objetos:** Reutiliza objetos `Point` y `Dimension` en iteraciones para reducir la presión del GC.  
- **Actualizaciones de versión:** Actualiza a la última versión de GroupDocs.Redaction para beneficiarte de una mejora de velocidad del 15 % reportada en la versión 24.10.  

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| **La redacción falla con estado `Failed`** | Ruta de archivo incorrecta o formato de imagen no compatible | Verifica que el archivo exista y sea un formato compatible (JPG, PNG, BMP, GIF). |
| **El archivo de salida está vacío** | `redactor.save()` llamado antes de que la redacción se complete | Asegúrate de que `apply()` devuelva `Status.SUCCESS` antes de invocar `save()`. |
| **El color no se aplica** | Uso de un `Color` transparente | Elige un color opaco como `Color.BLACK` o `Color.BLUE`. |

## Preguntas frecuentes

**P: ¿Cuál es la diferencia entre `ImageAreaRedaction` y la redacción de texto?**  
`ImageAreaRedaction` funciona con coordenadas de píxeles crudos, mientras que la redacción de texto analiza capas OCR para localizar y eliminar contenido textual.

**P: ¿Puedo redactar múltiples regiones en una sola imagen?**  
Sí—llama a `redactor.apply()` repetidamente con diferentes objetos `ImageAreaRedaction` antes de guardar el archivo final.

**P: ¿GroupDocs.Redaction admite otros formatos de imagen como TIFF?**  
La biblioteca admite formatos raster comunes (JPG, PNG, BMP, GIF). Para TIFF, convierte la imagen a un formato compatible primero.

**P: ¿Cómo automatizo la redacción para una carpeta de PDFs escaneados?**  
Extrae cada página como una imagen, aplica la misma lógica de redacción y luego reconstruye el PDF usando una biblioteca PDF como GroupDocs.Conversion.

**P: ¿Hay una forma de previsualizar la redacción antes de guardar?**  
Renderiza el `Redactor` a un `BufferedImage` y muéstralo en una UI Swing o JavaFX, lo que te permite confirmar el área enmascarada antes de confirmar.

## Conclusión
Ahora tienes una guía completa y lista para producción sobre **cómo redactar imágenes** y, específicamente, cómo **redactar imágenes escaneadas en Java** usando GroupDocs.Redaction para Java. Siguiendo los pasos anteriores puedes proteger datos visuales sensibles en los sectores financiero, legal y de salud. Explora APIs adicionales—como redacción de texto, redacción de páginas PDF o procesamiento masivo de carpetas—para construir una canalización de privacidad de datos de extremo a extremo para tu organización.

**Recursos**  
- [Documentación](https://docs.groupdocs.com/redaction/java/)  
- [Referencia de API](https://reference.groupdocs.com/redaction/java)  
- [Descarga](https://releases.groupdocs.com/redaction/java/)  
- [Repositorio de GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/) 

---

**Última actualización:** 2026-09-21  
**Probado con:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Cómo redactar Java con GroupDocs.Redaction - Guía completa para desarrolladores](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Cómo redactar PDF escaneado con OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Cómo redactar texto en Java con GroupDocs.Redaction – Guía](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)