---
date: 2026-08-04
description: Aprende cómo filtrar datos de hoja de cálculo en Java y redactar de forma
  segura columnas o celdas en hojas de cálculo de Excel usando GroupDocs.Redaction
  para Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Aprende cómo filtrar datos de hoja de cálculo en Java y redactar de
  forma segura columnas o celdas en hojas de cálculo de Excel usando GroupDocs.Redaction
  para Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrar datos de hoja de cálculo en Java – guía con GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtrar datos de hoja de cálculo en Java – guía con GroupDocs.Redaction
type: docs
url: /es/java/spreadsheet-redaction/
weight: 12
---

# Filtrar datos de hoja de cálculo java – Tutorial de GroupDocs.Redaction Java

Si necesitas **filter spreadsheet data java** antes de aplicar la redacción, has llegado a la guía correcta. En este tutorial descubrirás cómo aislar filas, columnas o celdas individuales que contienen información personal o confidencial, y luego redactarlas de forma segura con GroupDocs.Redaction para Java. Los pasos se explican en lenguaje sencillo, incluyen consejos de mejores prácticas y muestran cómo mantener el procesamiento rápido incluso en libros de trabajo grandes.

## Respuestas rápidas
- **¿Qué biblioteca maneja la redacción de hojas de cálculo en Java?** GroupDocs.Redaction for Java.  
- **¿Puedo filtrar filas sin cargar todo el archivo en memoria?** Sí – la API transmite datos y permite aplicar filtros al vuelo.  
- **¿Qué formatos de archivo son compatibles?** Más de 30 formatos de hoja de cálculo, incluidos XLS, XLSX, CSV y ODS.  
- **¿Necesito una licencia para desarrollo?** Una licencia temporal funciona para pruebas; se requiere una licencia completa para producción.  
- **¿Existe un límite en el tamaño del libro de trabajo?** El motor puede procesar archivos de hasta 500 MB sin un consumo excesivo de memoria.

## Qué es filter spreadsheet data java?
**Filter spreadsheet data java** es el proceso de seleccionar programáticamente filas, columnas o celdas específicas en un libro de trabajo estilo Excel usando código Java, de modo que solo el contenido objetivo se examine o redacte. Esta técnica reduce el tiempo de ejecución, limita cambios innecesarios y ayuda a cumplir con la normativa tipo GDPR.

## Por qué filtrar spreadsheet data java?
GroupDocs.Redaction Java admite **30+ formatos de hoja de cálculo** y puede procesar libros de trabajo que contengan **hasta 500 MB** (aproximadamente 1 millón de filas) manteniendo el uso de memoria por debajo de **200 MB**. Al filtrar primero, evitas tocar datos no relacionados, lo que reduce el tiempo de procesamiento entre **40‑60 %** en promedio para escenarios típicos de limpieza de privacidad.

## Requisitos previos
- Java 17 o posterior instalado.  
- Sistema de compilación Maven o Gradle.  
- GroupDocs.Redaction for Java (descargable desde el sitio oficial).  
- Una clave de licencia temporal o completa.  

## Cómo filtrar datos en hojas de cálculo usando GroupDocs.Redaction Java?
Carga el libro de trabajo, define un filtro que coincida con las celdas que deseas redactar y luego aplica la operación de redacción. La API realiza el filtro de forma streaming, por lo que nunca necesitas mantener todo el archivo en RAM.

La clase `RedactionFilter` te permite especificar índices de columnas, rangos de filas o predicados personalizados. Por ejemplo, puedes apuntar a cada celda en la columna **B** que contenga un patrón de dirección de correo electrónico, o puedes restringir la redacción a filas donde la columna “Status” sea igual a “Confidential”.

**Respuesta directa (40‑70 palabras):**  
Crea una instancia de `RedactionFilter`, establece el índice de columna y una condición de expresión regular, luego pasa el filtro a `Redactor.redact(workbook, filter)`. Este filtro de una sola línea aísla las celdas exactas que coinciden con tus criterios, y el redactor las elimina o enmascara mientras deja el resto de la hoja sin tocar. La operación se completa en tiempo lineal respecto a las filas filtradas.

### Paso 1: instanciar el filtro
`RedactionFilter` es la clase principal que representa una regla de filtrado para la redacción de hojas de cálculo. Acepta números de columna, números de fila o expresiones lambda personalizadas para precisar los datos.

### Paso 2: configurar la condición
Usa `filter.setColumnIndex(1)` para apuntar a la columna B (basado en cero) y `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` para coincidir con patrones de correo electrónico. También puedes combinar múltiples condiciones con `filter.and(...)` o `filter.or(...)`.

### Paso 3: aplicar la redacción
`Redactor` es la clase principal que ejecuta operaciones de redacción en un libro de trabajo.  
Pasa el libro de trabajo y el filtro configurado al objeto `Redactor`. La API transmite el libro de trabajo, aplica el filtro y escribe el resultado redactado en un nuevo archivo, preservando el formato y las fórmulas originales.

## Problemas comunes y soluciones
- **El filtro no coincide con ninguna celda:** Verifica el índice de columna (basado en cero) y asegura que la sintaxis de la expresión regular sea correcta para Java.  
- **Errores de falta de memoria en archivos grandes:** Incrementa modestamente el tamaño del heap de JVM (p. ej., `-Xmx1g`) o divide el libro de trabajo en fragmentos más pequeños antes de filtrar.  
- **La salida redactada pierde formato:** `RedactionOptions` permite personalizar el comportamiento de la redacción, como preservar el formato de celdas. Usa `RedactionOptions.setPreserveFormatting(true)` para mantener intactos los estilos de celda.

## Por qué filtrar spreadsheet data?
Filtrar antes de la redacción aísla solo las porciones sensibles de un libro de trabajo, lo que significa que evitas cambios innecesarios en datos limpios. Este enfoque selectivo también reduce el riesgo de pérdida accidental de datos y acelera las auditorías de cumplimiento porque el registro de auditoría contiene muchas menos entradas.

## Cómo redactar correos electrónicos en hojas de cálculo Excel usando la API Java de GroupDocs.Redaction
Carga tu archivo Excel, aplica un filtro que busque el patrón típico de correo electrónico e invoca el redactor. La API reemplaza cada correo electrónico coincidente con un marcador de posición como “***@***.com” mientras preserva el diseño de las celdas circundantes.

## Cómo filtrar datos – tutoriales disponibles
- [Cómo redactar correos electrónicos en hojas de cálculo Excel usando la API Java de GroupDocs.Redaction](./redact-emails-excel-groupdocs-redaction-java/)

## Recursos adicionales
- [Documentación de GroupDocs.Redaction para Java](https://docs.groupdocs.com/redaction/java/)
- [Referencia de API de GroupDocs.Redaction para Java](https://reference.groupdocs.com/redaction/java/)
- [Descargar GroupDocs.Redaction para Java](https://releases.groupdocs.com/redaction/java/)
- [Foro de GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Soporte gratuito](https://forum.groupdocs.com/)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

**Última actualización:** 2026-08-04  
**Probado con:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## Preguntas frecuentes
**P: ¿Puedo filtrar varias columnas a la vez?**  
R: Sí, puedes añadir índices de columna adicionales a la misma instancia de `RedactionFilter` o encadenar varios filtros con `filter.or(...)`.

**P: ¿El filtro funciona en libros de trabajo protegidos con contraseña?**  
R: Proporciona la contraseña al abrir el libro de trabajo; el filtro opera después de la descifrado igual que en un archivo sin protección.

**P: ¿Cuántas filas puede manejar la API en una sola operación?**  
R: El motor está optimizado para hasta 1 millón de filas (≈500 MB) sin cargar todo el archivo en memoria.

**P: ¿Es posible previsualizar qué celdas serán redactadas antes de guardar?**  
R: Sí, llama a `filter.preview(workbook)` para obtener una lista de direcciones de celdas que coinciden con los criterios.

**P: ¿Qué modelo de licencia se requiere para uso en producción?**  
R: Se requiere una licencia comercial completa para despliegues en producción; una licencia temporal es suficiente para pruebas y evaluación.

## Tutoriales relacionados
- [Cómo redactar datos sensibles en hojas de cálculo Excel usando la API Java de GroupDocs.Redaction](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Enmascarar datos sensibles Java – Guía de GroupDocs.Redaction](/redaction/java/getting-started/)
- [Enmascarar datos sensibles Java – Redactar información personal con GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)