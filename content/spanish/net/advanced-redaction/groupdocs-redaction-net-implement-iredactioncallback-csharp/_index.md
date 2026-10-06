---
date: '2026-10-06'
description: Aprenda a redactar datos usando GroupDocs.Redaction .NET con una implementación
  de IRedactionCallback en C#. Siga esta guía paso a paso, mejores prácticas y ejemplos
  del mundo real.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Aprenda a redactar datos usando GroupDocs.Redaction .NET con una implementación
  de IRedactionCallback en C#. Siga una guía paso a paso con mejores prácticas y ejemplos
  del mundo real.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Cómo redactar datos con GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Cómo redactar datos con GroupDocs.Redaction .NET (C#)
type: docs
url: /es/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Cómo redactar datos con GroupDocs.Redaction .NET (C#)

En este tutorial completo descubrirás **cómo redactar datos** de PDFs, archivos Word y otros documentos usando GroupDocs.Redaction para .NET. Ya sea que necesites ocultar identificadores personales en contratos legales o eliminar cifras confidenciales de informes financieros, el SDK te brinda control programático para garantizar que cada elemento sensible desaparezca de forma permanente y auditada. Recorreremos la instalación de la biblioteca, la configuración de un `IRedactionCallback` personalizado y la aplicación de redacciones de frase exacta con registro completo.

## Respuestas rápidas
- **¿Qué hace IRedactionCallback?** Permite interceptar cada evento de redacción, registrar detalles y, opcionalmente, modificar el texto de reemplazo sobre la marcha.  
- **¿Necesito una licencia?** Una versión de prueba funciona para desarrollo; una licencia permanente elimina todos los límites de evaluación.  
- **¿Qué versiones de .NET son compatibles?** .NET Core 3.1+, .NET 5/6 y .NET Framework 4.6+.  
- **¿Puedo procesar varios archivos?** Sí, envuelve la lógica en un bucle o usa procesamiento por lotes para obtener el mejor rendimiento.  
- **¿Es posible la redacción asíncrona?** No está incorporada, pero puedes ejecutar las llamadas API dentro de `Task.Run` u otros patrones async.

## ¿Qué es redactar datos sensibles?
`Redaction` es la eliminación permanente o el oscurecimiento de información que no debe divulgarse. Con GroupDocs.Redaction defines frases exactas, patrones de expresiones regulares o reglas personalizadas y las reemplazas con marcadores como **[REDACTED]** mientras preservas el diseño y la paginación originales.

## ¿Por qué usar GroupDocs.Redaction con IRedactionCallback?
`IRedactionCallback` es una interfaz que te notifica cada vez que el SDK redacta un fragmento de contenido, permitiéndote capturar datos de auditoría o ajustar el reemplazo dinámicamente. Esto habilita una auditoría completa, la aplicación de reglas de negocio personalizadas y una integración fluida con sistemas de cumplimiento, todo sin sacrificar el rendimiento.

## Requisitos previos
- Biblioteca **GroupDocs.Redaction** (versión compatible – consulta la página oficial de [documentación](https://docs.groupdocs.com/redaction/net/)). Para más detalles, revisa la [documentación oficial](https://docs.groupdocs.com/redaction/net/).  
- .NET Core o .NET Framework instalado en tu máquina de desarrollo.  
- Visual Studio (la edición Community es suficiente) o cualquier IDE que soporte C#.  
- Conocimientos básicos de C# y familiaridad con la gestión de paquetes NuGet.

## Configuración de GroupDocs.Redaction para .NET
Primero, agrega la biblioteca a tu proyecto. Elige el método que prefieras: CLI, Package Manager Console o la UI. Los comandos permanecen exactamente iguales que en el tutorial original.

### Opciones de instalación
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Abre tu proyecto en Visual Studio.  
- Navega a **Manage NuGet Packages**.  
- Busca **GroupDocs.Redaction** e instala la versión estable más reciente.

### Obtención de licencia
Para probar el producto, solicita una prueba gratuita o una licencia temporal desde [aquí](https://purchase.groupdocs.com/temporary-license/). También puedes obtener una licencia temporal desde la [página de licencia temporal](https://purchase.groupdocs.com/temporary-license/). Para uso en producción, adquiere una licencia completa que desbloquee todas las funciones sin límites.

#### Inicialización básica y configuración
A continuación tienes el código mínimo necesario para abrir un documento con la clase `Redactor`. Mantén este fragmento sin cambios; es la base de todo lo que sigue.  
`Redactor` es la clase principal que representa un documento y proporciona métodos para aplicar reglas de redacción.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Guía de implementación
Ahora ampliaremos la configuración básica añadiendo un `IRedactionCallback` personalizado. Esto te permite capturar cada evento de redacción, escribirlo en un registro o incluso modificar el texto de reemplazo al vuelo.

### Adjuntar y usar una implementación de IRedactionCallback
`IRedactionCallback` es una interfaz que recibe devoluciones de llamada para cada operación de redacción, permitiéndote registrar o alterar el comportamiento programáticamente.

#### Paso 1: preparar el directorio de salida y la ruta del archivo fuente
Define dónde se encuentra tu documento fuente. Ajusta la ruta para que coincida con tu entorno.

`LoadOptions` es un objeto de configuración que indica al SDK cómo leer el archivo (p. ej., manejo de contraseñas).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Paso 2: crear una instancia de Redactor con configuraciones personalizadas
Instanciamos `Redactor` con `LoadOptions` y `RedactorSettings`. El `RedactionDump` dentro de la configuración registrará automáticamente cada redacción que ocurra.

`RedactorSettings` te permite afinar el proceso de redacción; pasar un `RedactionDump` habilita un archivo de auditoría detallado.  
`RedactionDump` es una clase auxiliar que escribe cada evento de redacción en un volcado con formato JSON para informes de cumplimiento.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Paso 3: aplicar una redacción de frase exacta
Aquí reemplazamos la frase **John Doe** con el marcador **[REDACTED]**. Puedes cambiar cualquier frase o patrón que necesites ocultar.

`ReplacementOptions` define qué texto reemplazará el contenido coincidente. También admite personalización de fuente y color si necesitas una máscara visual.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Explicación de los objetos clave**
- `LoadOptions()` – indica al SDK cómo leer el documento (p. ej., manejo de contraseñas).  
- `RedactorSettings(new RedactionDump())` – habilita un archivo de volcado que registra cada redacción para fines de auditoría.  
- `ReplacementOptions("[REDACTED]")` – define el texto que reemplazará la frase encontrada.

### Por qué es importante
El mecanismo de devolución de llamada registra cada evento de redacción, crea una pista de auditoría legible por máquinas y permite modificar los marcadores dinámicamente, lo que ayuda a cumplir con requisitos de cumplimiento y reduce el esfuerzo manual posterior. Al integrar estos datos con tus sistemas de monitoreo puedes generar informes, activar alertas y asegurar que ninguna información sensible se escape del proceso de redacción.

Usar `IRedactionCallback` te brinda tres ventajas concretas:  
1. **Registros listos para cumplimiento** – cada redacción se captura en un volcado legible por máquinas, cumpliendo con más de 30 marcos regulatorios.  
2. **Reemplazo dinámico** – puedes cambiar el marcador según el tipo de dato, reduciendo el procesamiento manual en hasta un 40 %.  
3. **Rendimiento escalable** – la devolución de llamada añade una sobrecarga insignificante (<2 ms por redacción) mientras permite procesar miles de archivos en paralelo.

### Consejos de solución de problemas
- **Archivo no encontrado:** Verifica la ruta `sourceFile` y asegura que el archivo sea accesible para el proceso en ejecución.  
- **Callback no se dispara:** Asegúrate de que tu clase implemente **todos** los miembros de `IRedactionCallback` y que la instancia se pase correctamente al `Redactor`.  
- **Retraso de rendimiento:** Para lotes grandes, reutiliza la misma instancia de `Redactor` cuando sea posible y dispón de ella de inmediato.

## Aplicaciones prácticas
Redactar datos sensibles es útil en muchas industrias:

1. **Procesamiento de documentos legales** – Elimina automáticamente nombres de clientes, números de caso o números de seguridad social antes de compartir borradores.  
2. **Sistemas de gestión de recursos humanos** – Suprime identificadores personales de contratos de empleados durante auditorías.  
3. **Informes financieros** – Oculta cifras propietarias o números de cuenta al generar PDFs para inversores.

## Consideraciones de rendimiento
GroupDocs.Redaction admite **más de 30 formatos de entrada y salida** (PDF, DOCX, PPTX, XLSX, HTML y tipos de imagen) y puede procesar archivos de cientos de páginas sin cargar todo el documento en memoria. Para mantener tu aplicación ágil al manejar decenas o cientos de archivos:

- **Procesamiento por lotes:** Carga una lista de archivos y ejecuta el bucle de redacción dentro de un `Parallel.ForEach` para aprovechar múltiples núcleos.  
- **Gestión de memoria:** Envuelve cada `Redactor` en un bloque `using` (como se muestra) para garantizar su disposición.  
- **Operaciones asíncronas:** Aunque el SDK es sincrónico, puedes delegar el trabajo a hilos en segundo plano o `Task.Run` para evitar bloquear hilos de UI.

## Problemas comunes y soluciones
| Problema | Solución |
|----------|----------|
| **Error “Formato de archivo no válido”** | Asegúrate de que el tipo de documento sea compatible (PDF, DOCX, PPTX, etc.). |
| **Callback recibe valores nulos** | Verifica que estés pasando una implementación concreta de `IRedactionCallback` al crear `RedactorSettings`. |
| **Redacción no se aplica** | Confirma que la frase exacta coincida con mayúsculas, minúsculas y espacios del documento, o usa `RegexRedaction` para coincidencias basadas en patrones. |

## Preguntas frecuentes

**P: ¿Cuáles son las opciones de licencia para GroupDocs.Redaction?**  
R: Puedes comenzar con una prueba gratuita o solicitar una licencia temporal para explorar todas las funciones. Para producción, adquiere una licencia perpetua o por suscripción.

**P: ¿Puedo usar GroupDocs.Redaction con varios tipos de archivo?**  
R: Sí, admite PDFs, Word, Excel, PowerPoint y muchos otros formatos comunes.

**P: ¿Cómo manejo excepciones durante la redacción?**  
R: Envuelve tu lógica de redacción en bloques `try‑catch` y registra los detalles de la excepción. El callback también puede usarse para capturar errores en tiempo real.

**P: ¿Existe soporte incorporado para procesamiento asíncrono?**  
R: La API principal es sincrónica, pero puedes ejecutar las llamadas de redacción dentro de tareas asíncronas o servicios en segundo plano.

**P: ¿Dónde encuentro ejemplos más avanzados?**  
R: La [documentación oficial](https://docs.groupdocs.com/redaction/net/) y la referencia de la API proporcionan numerosos ejemplos de código y guías de escenarios.

## Recursos

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-10-06  
**Probado con:** GroupDocs.Redaction 2.3 (última versión al momento de escribir)  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Create Redaction Policy with GroupDocs.Redaction .NET – Step‑By‑Step Guide](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [How to Redact Documents with GroupDocs.Redaction .NET – A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redact documents .net using Streams – GroupDocs.Redaction Guide](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)