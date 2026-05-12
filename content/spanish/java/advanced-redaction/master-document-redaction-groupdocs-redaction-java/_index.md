---
date: '2026-02-16'
description: Aprende cómo usar la dependencia GroupDocs Maven para agregar un sufijo
  a los nombres de archivo mientras redactas documentos en Java. Incluye carga desde
  stream, eliminación de anotaciones y opciones de guardado.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: dependencia de maven de groupdocs – Añadir sufijo al nombre de archivo en Java
type: docs
url: /es/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Cómo agregar un sufijo al nombre de archivo al redactar documentos en Java con GroupDocs.Redaction

Redactar datos confidenciales es solo la mitad de la batalla—también necesitas asegurarte de que el archivo guardado indique claramente que ha sido procesado. **Usar la dependencia groupdocs maven hace esto sencillo**, permitiéndote agregar un sufijo al nombre del archivo de salida en solo unas pocas líneas de código. En esta guía aprenderás cómo agregar un sufijo al nombre de archivo al guardar un documento redactado, junto con cargar, anotar y guardar usando GroupDocs.Redaction para Java. Ya sea que estés protegiendo contratos legales, registros médicos o informes financieros, estos pasos mantendrán tu flujo de trabajo seguro y auditable.

## Respuestas rápidas
- **¿Qué hace “add suffix to filename”?**  
  Añade un sufijo personalizado (p. ej., “_redacted”) al nombre del archivo de salida para que puedas identificar instantáneamente los archivos procesados.  
- **¿Puedo cargar un documento desde un stream?**  
  Sí—GroupDocs.Redaction admite cargar desde cualquier `InputStream`, perfecto para almacenamiento en la nube o procesamiento en memoria.  
- **¿Necesito una licencia para esta función?**  
  Una prueba gratuita funciona para la redacción básica; una licencia temporal o completa desbloquea todas las opciones avanzadas, incluido el manejo de sufijos.  
- **¿Qué formatos son compatibles?**  
  La biblioteca maneja DOCX, PDF, PPTX, XLSX y muchos más.  
- **¿Es necesaria la rasterización para la salida PDF?**  
  La rasterización es opcional; actívala cuando necesites aplanar el documento para mayor seguridad.

## ¿Qué es agregar un sufijo al nombre de archivo?
Agregar un sufijo es una convención de nomenclatura simple que indica que un archivo ha sido redactado. Previene la compartición accidental de versiones originales sin redactar y ayuda a las canalizaciones automatizadas a rastrear el estado del procesamiento.

## ¿Por qué usar GroupDocs.Redaction para esta tarea?
GroupDocs.Redaction ofrece una API fluida de Java que te permite combinar acciones de redacción con opciones de manejo de archivos—como **agregar un sufijo al nombre de archivo**—en solo unas pocas líneas de código. Esto ahorra tiempo de desarrollo y reduce el riesgo de errores manuales.

## Requisitos previos
- **Java Development Kit (JDK):** Versión 8 o superior.  
- **GroupDocs.Redaction Library:** Biblioteca central para tareas de redacción.  
- **IDE:** IntelliJ IDEA, Eclipse o cualquier editor compatible con Java.  
- **Maven:** Para la gestión de dependencias.  

### Conocimientos previos
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
1. **Free Trial:** Accede a la funcionalidad básica sin restricciones.  
2. **Temporary License:** Obtén una licencia temporal para explorar funciones avanzadas.  
3. **Purchase:** Para uso a largo plazo, considera comprar una licencia completa.

#### Inicialización y configuración básicas
Inicializa tu proyecto añadiendo las importaciones necesarias:

```java
import com.groupdocs.redaction.Redactor;
```

Con esta configuración, estás listo para implementar funcionalidades de redacción de documentos.

## Guía de implementación

### Función 1: Cargar documento desde stream
**Visión general:** Aprende cómo cargar documentos en un `InputStream` para su procesamiento.

#### Implementación paso a paso
##### Paso 1.1: Crear InputStream

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

- **Por qué:** Usar `InputStream` te permite manejar documentos almacenados en varios formatos de forma fluida, lo cual es esencial cuando necesitas **load document from stream** en escenarios de nube o micro‑servicios.

### Función 2: Aplicar redacción de eliminación de anotaciones
**Visión general:** Elimina anotaciones de tu documento usando `DeleteAnnotationRedaction`.

#### Implementación paso a paso
##### Paso 2.1: Aplicar DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Por qué:** Este paso garantiza que cualquier anotación sensible sea eliminada, mejorando la privacidad del documento.

### Función 3: Guardar documento con opciones
**Visión general:** Aprende cómo guardar tu documento procesado con opciones específicas como rasterización y **agregar un sufijo al nombre de archivo**.

#### Implementación paso a paso
##### Paso 3.1: Configurar SaveOptions

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

- **Por qué:** Personalizar las opciones de guardado permite formatos de salida flexibles y convenciones de nomenclatura. Habilitar `setAddSuffix(true)` **adds suffix to filename**, dejando claro que el archivo ha sido redactado.

## Visión general de la dependencia groupdocs maven
La **groupdocs maven dependency** incorpora todo el SDK de Redaction a tu proyecto con una única entrada `<dependency>`. Gestiona dependencias transitivas, mantiene las bibliotecas actualizadas y simplifica la automatización de compilaciones. Al declarar la dependencia en `pom.xml`, evitas la gestión manual de JARs y aseguras la compatibilidad con los últimos parches de seguridad.

## Por qué agregar un sufijo es importante
- **Auditabilidad:** Los equipos pueden identificar instantáneamente qué archivos son seguros para distribuir.  
- **Automatización:** Los scripts pueden filtrar archivos por sufijo, evitando el procesamiento accidental de documentos originales.  
- **Cumplimiento:** Muchas regulaciones exigen un etiquetado claro de los documentos sanitizados.  

## Aplicaciones prácticas
Explora estos casos de uso del mundo real:
1. **Legal Document Redaction:** Asegura los contratos antes de compartirlos con el cliente.  
2. **Medical Record Handling:** Protege los identificadores de pacientes.  
3. **Financial Reporting:** Mantén confidenciales los números sensibles.  
4. **CRM Integration:** Redacta automáticamente los datos de clientes antes de exportar.  
5. **Collaboration Tools:** Asegura que los borradores compartidos nunca expongan comentarios ocultos.

## Consideraciones de rendimiento
### Optimización del rendimiento
- Usa streaming (`load document from stream`) para evitar cargar archivos completos en memoria.  
- Cierra las instancias de `Redactor` rápidamente para liberar recursos.

### Directrices de uso de recursos
- Monitorea CPU y memoria durante ejecuciones por lotes.  
- Prefiere `ByteArrayOutputStream` para guardados en memoria cuando trabajas con tamaños de archivo modestos.

### Mejores prácticas para la gestión de memoria en Java
- Reutiliza objetos `Redactor` al procesar varios archivos del mismo tipo.  
- Invoca `close()` en un bloque `try‑with‑resources` para prevenir fugas.

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| **El sufijo no aparece** | `setAddSuffix(false)` o llamada faltante | Asegúrate de que `options.setAddSuffix(true)` esté configurado antes de `save()`. |
| **OutOfMemoryError en DOCX grande** | Cargar todo el archivo en memoria | Cambia a carga mediante `InputStream` (ver Función 1). |
| **Las anotaciones siguen visibles** | Redacción no aplicada antes de guardar | Llama a `redactor.apply(new DeleteAnnotationRedaction())` antes de `save()`. |
| **Rasterización PDF no aplicada** | `setRasterizeToPDF(false)` o omitido | Configura `options.setRasterizeToPDF(true)` cuando necesites un PDF aplanado. |

## Preguntas frecuentes

**Q: ¿Puedo redactar documentos PDF usando GroupDocs.Redaction?**  
A: Sí, la biblioteca soporta PDFs, DOCX, PPTX, XLSX y muchos otros formatos.

**Q: ¿Cuál es la mejor manera de manejar archivos grandes con GroupDocs.Redaction?**  
A: Usa streaming (`load document from stream`) y cierra los recursos rápidamente para mantener bajo el uso de memoria.

**Q: ¿Es posible personalizar el texto del sufijo?**  
A: La API agrega automáticamente un sufijo predeterminado (p. ej., “_redacted”). Para sufijos personalizados, puedes renombrar el archivo de salida después de guardarlo.

**Q: ¿Cómo obtengo una licencia temporal para GroupDocs.Redaction?**  
A: Visita la [Temporary License page](https://purchase.groupdocs.com/temporary-license/) y sigue las instrucciones.

**Q: ¿Dónde puedo obtener ayuda si encuentro problemas?**  
A: Únete al [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) para asistencia de expertos.

## Recursos
- **Documentation:** Explora guías detalladas en [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Accede a detalles completos de la API en [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Obtén la última versión desde [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Contribuye o explora el código fuente en [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs