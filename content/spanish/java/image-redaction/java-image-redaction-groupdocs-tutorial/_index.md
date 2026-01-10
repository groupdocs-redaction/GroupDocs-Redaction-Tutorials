---
date: '2025-12-29'
description: Aprende a redactar imágenes de documentos escaneados usando GroupDocs.Redaction
  para Java. Guía paso a paso que cubre la configuración, la redacción de áreas de
  la imagen y la verificación.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: Cómo redactar imágenes de documentos escaneados con GroupDocs en Java
type: docs
url: /es/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Cómo redactar imágenes de documentos escaneados con GroupDocs en Java

En el panorama digital actual, **redactar documentos escaneados** es esencial para proteger la privacidad y cumplir con los requisitos de cumplimiento. Ya sea que necesites ocultar datos personales en un contrato escaneado o difuminar detalles de pacientes en una imagen médica, este tutorial te muestra **cómo redactar contenido de imágenes** de forma rápida y fiable usando **GroupDocs.Redaction for Java**. Recorreremos todo, desde la configuración del proyecto hasta la verificación de que la redacción se haya realizado correctamente, para que puedas integrar la solución en cualquier aplicación Java con confianza.

## Respuestas rápidas
- **¿Qué biblioteca maneja la redacción de imágenes en Java?** GroupDocs.Redaction for Java  
- **¿Puedo elegir el color de la redacción?** Sí – cualquier `java.awt.Color` (p.ej., `Color.BLUE`)  
- **¿Se requiere una licencia para producción?** Sí, se necesita una licencia válida de GroupDocs  
- **¿Se sobrescribirá la imagen original?** No – guardas el resultado en un nuevo archivo  
- **¿Qué versión de Java es compatible?** Java 8+ (compatible con JDKs modernos)

## Qué es la redacción de imágenes y por qué redactar imágenes de documentos escaneados?
La redacción de imágenes significa ocultar permanentemente información visual sensible —como nombres, números o firmas— de modo que no pueda recuperarse. Cuando trabajas con documentos escaneados, los datos están incrustados como píxeles, lo que hace que las herramientas tradicionales de redacción de texto sean ineficaces. Usar GroupDocs.Redaction te permite apuntar a regiones exactas de píxeles y reemplazarlas con un color sólido, garantizando que la información se elimine realmente.

## Requisitos previos
Antes de comenzar, asegúrate de contar con:

- **JDK 8 o superior** instalado  
- **Maven** (u otra herramienta de compilación) para la gestión de dependencias  
- Un IDE como **IntelliJ IDEA**, **Eclipse** o **NetBeans**  
- Conocimientos básicos de Java y familiaridad con la E/S de archivos  

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
- **Prueba gratuita:** Regístrate para una prueba y explorar la API.  
- **Licencia temporal:** Usa una clave temporal para pruebas extendidas.  
- **Compra completa:** Obtén una licencia de producción para uso ilimitado.

## Guía de implementación

Dividiremos la implementación en dos características principales: **Image Area Redaction** (el enmascarado real) y **Redaction Status Check** (verificación del éxito).

### Cómo redactar imágenes de documentos escaneados – Paso 1: Inicializar el Redactor
Primero, crea una instancia de `Redactor` que apunte a la imagen que deseas procesar.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Paso 2: Definir los parámetros de redacción
Especifica la esquina superior izquierda (`Point`) y el tamaño (`Dimension`) del rectángulo que deseas ocultar. En este ejemplo usamos un relleno azul.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Paso 3: Aplicar la redacción
Crea un objeto `ImageAreaRedaction` con `RegionReplacementOptions` y ejecútalo. El método devuelve un `RedactorChangeLog` que indica si la operación tuvo éxito.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Paso 4: Liberar recursos
Siempre cierra el `Redactor` cuando termines para liberar los recursos nativos.

```java
redactor.close();
```

### Cómo verificar la redacción – Verificación de estado
Después de aplicar la redacción, puedes inspeccionar el `RedactorChangeLog` para confirmar que la operación no falló.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Aplicaciones prácticas
- **Manejo de documentos confidenciales:** Enmascara automáticamente datos personales en contratos escaneados antes de compartirlos con partes externas.  
- **Documentación legal:** Garantiza el cumplimiento de GDPR o HIPAA redactando identificadores en imágenes de evidencia.  
- **Registros médicos:** Protege la privacidad del paciente ocultando caras o notas manuscritas en imágenes de radiología.

## Consideraciones de rendimiento
- **Procesamiento por lotes:** Carga y redacta imágenes en pequeños lotes para mantener bajo el uso de memoria.  
- **Estructuras de datos eficientes:** Reutiliza objetos `Point` y `Dimension` al procesar muchas imágenes.  
- **Mantente actualizado:** Actualiza regularmente a la última versión de GroupDocs.Redaction para mejoras de rendimiento y corrección de errores.

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| **La redacción falla con estado `Failed`** | Ruta de archivo incorrecta o formato de imagen no compatible | Verifica que la imagen exista y sea un formato compatible (JPG, PNG, BMP). |
| **El archivo de salida está vacío** | `redactor.save()` llamado antes de que la redacción se complete | Asegúrate de que `apply()` devuelva un estado exitoso antes de guardar. |
| **El color no se aplica** | Uso de un color transparente | Elige un `Color` opaco (p.ej., `Color.BLACK` o `Color.BLUE`). |

## Preguntas frecuentes

**P: ¿Cuál es la diferencia entre `ImageAreaRedaction` y la redacción de texto?**  
R: `ImageAreaRedaction` funciona con coordenadas de píxeles, mientras que la redacción de texto analiza capas OCR para localizar y eliminar contenido textual.

**P: ¿Puedo redactar múltiples regiones en una sola imagen?**  
R: Sí—llama a `redactor.apply()` repetidamente con diferentes objetos `ImageAreaRedaction` antes de guardar.

**P: ¿GroupDocs.Redaction admite otros formatos de imagen como TIFF?**  
R: La biblioteca admite formatos raster comunes (JPG, PNG, BMP, GIF). Para TIFF, conviértelo primero a un formato compatible.

**P: ¿Cómo automatizo la redacción para una carpeta de PDFs escaneados?**  
R: Itera sobre cada imagen de página extraída del PDF, aplica la misma lógica de redacción y luego reconstruye el PDF usando una biblioteca PDF.

**P: ¿Hay una forma de previsualizar la redacción antes de guardar?**  
R: Puedes renderizar el `Redactor` a un `BufferedImage` y mostrarlo en una interfaz Swing o JavaFX antes de confirmar los cambios.

## Conclusión
Ahora tienes una guía completa y lista para producción sobre **cómo redactar contenido de imágenes** y, específicamente, cómo **redactar imágenes de documentos escaneados** usando GroupDocs.Redaction para Java. Siguiendo los pasos anteriores, puedes proteger datos visuales sensibles en una amplia gama de industrias. Explora las APIs adicionales —como la redacción de texto o la redacción de páginas PDF— para construir una solución integral de privacidad de datos para tu organización.

**Recursos**  
- [Documentación](https://docs.groupdocs.com/redaction/java/)  
- [Referencia API](https://reference.groupdocs.com/redaction/java)  
- [Descarga](https://releases.groupdocs.com/redaction/java/)  
- [Repositorio GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2025-12-29  
**Probado con:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  
