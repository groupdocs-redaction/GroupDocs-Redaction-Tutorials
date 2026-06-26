---
date: '2026-06-26'
description: Aprenda cómo extraer texto de PDF escaneado y enmascarar datos sensibles
  usando GroupDocs OCR Redaction con Azure OCR. Redacte el número de seguro social
  y reemplace la información confidencial del PDF de manera eficiente.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Extraer texto de PDF escaneado – Enmascarar datos con GroupDocs OCR
type: docs
url: /es/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Extraer texto de PDF escaneado – Enmascarar datos con GroupDocs OCR

En el mundo actual impulsado por los datos, **extraer texto de PDF escaneados** y enmascarar información confidencial es un paso de cumplimiento innegociable. Este tutorial le guía a través del uso de GroupDocs Redaction junto con Microsoft Azure OCR para reconocer de manera fiable el texto oculto en páginas escaneadas y reemplazarlo con un marcador seguro como **`[REDACTED]`**. Verá por qué esta combinación es rápida, precisa y está lista para cargas de trabajo de nivel de producción.

## Respuestas rápidas
- **¿Qué significa “enmascarar datos sensibles”?** Reemplaza el texto confidencial identificado con un marcador (p. ej., `[REDACTED]`).  
- **¿Qué biblioteca maneja OCR?** Conector Microsoft Azure OCR, usado a través de GroupDocs Redaction.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para evaluación; se requiere una licencia permanente para producción.  
- **¿Puedo redactar PDFs escaneados?** Sí—OCR extrae el texto oculto antes de aplicar redactados con expresiones regulares.  
- **¿Esta solución es solo Java?** El ejemplo está basado en Java, pero GroupDocs ofrece APIs similares para .NET y otras plataformas.

## ¿Qué es la redacción basada en OCR?
La redacción basada en OCR primero ejecuta OCR en cada página, convirtiendo imágenes en texto buscable, y luego aplica patrones regex para reemplazar coincidencias con una máscara como `[REDACTED]`. Este proceso de dos pasos le permite ocultar de manera fiable datos personales incluso en PDFs escaneados, asegurando que cualquier cadena sensible se elimine antes de que el documento se comparta o archive.

## ¿Por qué usar GroupDocs Redaction con Azure OCR?
Debe usar GroupDocs Redaction con Azure OCR porque ofrece **>98 % de precisión OCR en texto impreso**, soporta **más de 50 formatos de entrada y salida**, y puede procesar **PDFs de varios cientos de páginas sin cargar todo el archivo en memoria**, garantizando una redacción rápida y escalable para el cumplimiento. La solución también **escalable para procesar un PDF de 1 000 páginas en menos de 2 minutos en un servidor de 8 núcleos**, haciendo prácticos los trabajos por lotes.

## Requisitos previos
- **Java Development Kit (JDK) 8+** instalado.  
- **Maven** (si prefiere la gestión de dependencias) o la capacidad de descargar JARs manualmente.  
- **Credenciales de Microsoft Azure OCR** (punto final y clave de suscripción).  
- Conocimientos básicos de Java y familiaridad con expresiones regulares.

## Configuración de GroupDocs Redaction para Java

### Configuración de Maven
Agregue el repositorio y la dependencia de GroupDocs a su `pom.xml`:

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
Si prefiere la gestión manual de JARs, obtenga la última versión de [GroupDocs.Redaction para Java releases](https://releases.groupdocs.com/redaction/java/).

### Obtención de licencia
- **Prueba gratuita** – explore todas las funciones sin costo.  
- **Licencia temporal** – extienda el tiempo de evaluación.  
- **Licencia completa** – desbloquee capacidades listas para producción.

### Inicialización y configuración básicas
La clase `Redactor` es el motor central que realiza la extracción OCR y aplica reglas de redacción a documentos PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Cómo enmascarar datos sensibles con redacción OCR
Enmascarar datos sensibles con redacción OCR implica cargar el PDF con la configuración de Azure OCR, definir patrones regex para los datos que desea ocultar y invocar al Redactor para reemplazar cada coincidencia con un marcador como `[REDACTED]`. La biblioteca maneja OCR, coincidencia de patrones y reescritura de PDF en un único flujo de trabajo.

### Paso 1: Cargar el documento con la configuración OCR
`LoadOptions` configura cómo GroupDocs carga un archivo, permitiéndole pasar conectores OCR como Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – reemplace con la ruta a su PDF.  
- **`settings`** – contiene el conector Azure OCR que creó anteriormente.

### Paso 2: Definir y aplicar redactados regex
`ReplacementOptions` especifica el texto de reemplazo que sustituirá cada coincidencia regex durante la redacción.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- El patrón `\b\d{3}-\d{2}-\d{4}\b` coincide con los números de Seguro Social de EE. UU.  
- `ReplacementOptions("[REDACTED]")` intercambia cada coincidencia con la máscara, enmascarando efectivamente **datos sensibles**.

## Casos de uso comunes para enmascarar datos sensibles
1. **Gestión de documentos legales** – ocultar identificadores de clientes antes de compartir borradores.  
2. **Informes financieros** – proteger números de cuenta e IDs de transacciones.  
3. **Registros de salud** – cumplir con HIPAA redactando identificadores de pacientes.  
4. **Publicaciones gubernamentales** – eliminar datos personales de registros públicos.  
5. **Contratos corporativos** – ocultar términos propietarios durante revisiones externas.

## Consejos de rendimiento
- **Optimizar regex** – evite patrones demasiado amplios que aumenten el tiempo de procesamiento; expresiones bien diseñadas pueden reducir el tiempo de ejecución hasta en un 40 %.  
- **Gestión de memoria** – cierre la instancia `Redactor` rápidamente (try‑with‑resources lo hace automáticamente).  
- **Ejecución asíncrona** – para procesamiento masivo, ejecute trabajos de redacción en hilos separados o use una cola de tareas para mantener la UI receptiva.

## Solución de problemas
- **Error de credenciales de Azure** – verifique nuevamente la URL del punto final y la clave de suscripción en `MicrosoftAzureOcrConnector`.  
- **El documento no se carga** – verifique la ruta del archivo y asegúrese de que el PDF no esté protegido con contraseña (o proporcione la contraseña mediante `LoadOptions`).  
- **No se aplicaron redactados** – pruebe su regex con una cadena simple primero; use `Pattern.compile` en una prueba unitaria para confirmar coincidencias.

## Preguntas frecuentes

**Q: ¿Qué es la redacción OCR?**  
A: La redacción OCR utiliza reconocimiento óptico de caracteres para extraer texto oculto de imágenes o PDFs escaneados, y luego aplica reglas de redacción para enmascarar ese texto.

**Q: ¿Puedo usar GroupDocs Redaction sin Azure OCR?**  
A: Sí, pero OCR mejora drásticamente la precisión en documentos escaneados donde la extracción de texto nativa falla.

**Q: ¿Cómo manejo patrones regex complejos?**  
A: Constrúyalos y pruébelos de forma incremental, usando la clase `Pattern` de Java en un entorno aislado antes de aplicarlos a documentos grandes.

**Q: ¿Cuáles son los cuellos de botella de rendimiento típicos?**  
A: PDFs grandes, regex demasiado complejas y llamadas OCR síncronas pueden ralentizar el procesamiento; considere el procesamiento por lotes y patrones optimizados.

**Q: ¿Está disponible soporte para problemas de implementación?**  
A: Absolutamente—contacte a través del [foro de GroupDocs](https://forum.groupdocs.com/c/redaction/33) para ayuda de la comunidad o contacte al soporte de GroupDocs.

## Recursos adicionales
- **Documentación**: https://docs.groupdocs.com/redaction/java/  
- **Referencia API**: https://reference.groupdocs.com/redaction/java  
- **Descarga**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Soporte gratuito**: https://forum.groupdocs.com/c/redaction/33  
- **Licencia temporal**: https://purchase.groupdocs.com/temporary-license/

---

**Última actualización:** 2026-06-26  
**Probado con:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  

## Tutoriales relacionados

- [Redacción segura de PDF usando OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Cómo redactar texto con GroupDocs.Redaction para Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Enmascarar datos sensibles Java – Redactar información personal con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)