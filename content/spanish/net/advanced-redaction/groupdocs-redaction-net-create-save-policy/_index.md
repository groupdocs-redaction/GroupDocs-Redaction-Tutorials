---
date: '2026-10-06'
description: Aprenda cómo redactar datos sensibles con GroupDocs.Redaction .NET. Esta
  guía paso a paso le muestra cómo crear, aplicar y guardar una política de redacción
  como XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Aprenda cómo redactar datos sensibles con GroupDocs.Redaction .NET.
  Esta guía paso a paso le muestra cómo crear, aplicar y guardar una política de redacción
  como XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: Cómo redactar datos sensibles usando GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: Cómo redactar datos sensibles usando GroupDocs.Redaction .NET
type: docs
url: /es/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# Cómo redactar datos sensibles usando GroupDocs.Redaction .NET

Proteger la información confidencial dentro de contratos, estados financieros o registros de pacientes es un requisito innegociable para las aplicaciones modernas. En esta guía aprenderá **cómo redactar datos sensibles** con GroupDocs.Redaction para .NET, desde la instalación del SDK hasta la definición de políticas XML reutilizables que pueden aplicarse a cualquier tipo de documento.

## Respuestas rápidas
- **¿Qué significa “create redaction policy”?** Es el proceso de definir reglas (texto, expresiones regulares, imágenes, etc.) que indican a GroupDocs.Redaction cómo ocultar o reemplazar contenido confidencial.  
- **¿Qué biblioteca necesito?** GroupDocs.Redaction para .NET, disponible a través de NuGet.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia permanente para producción.  
- **¿Puedo reutilizar la política?** Sí—una vez guardada como XML puede cargarse más tarde y aplicarse a cualquier documento.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qué es una política de redacción

Una política de redacción es una colección de reglas que especifican *qué* debe eliminarse o reemplazarse y *cómo* debe verse el reemplazo. Al crear una política una sola vez, puede aplicar estándares de seguridad consistentes a cada documento procesado por su aplicación.

## Cómo funciona una política de redacción

Cargue un documento con el motor `Redactor`, adjunte una o más reglas de redacción y luego invoque `Apply`. El motor escanea el documento, enmascara el contenido coincidente y, opcionalmente, genera un nuevo archivo. El mismo conjunto de reglas puede exportarse a XML, lo que le permite reutilizar la política sin recompilar el código.

## Por qué usar GroupDocs.Redaction para crear una política de redacción

GroupDocs.Redaction ofrece un conjunto completo de funcionalidades que simplifican la creación, gestión y ejecución de políticas de redacción, garantizando una protección de datos consistente en diversos tipos de documentos mientras brinda alto rendimiento e integración fácil en aplicaciones .NET existentes para equipos y organizaciones.

- **Amplio soporte de formatos** – el SDK maneja más de 30 tipos de archivos, incluidos PDF, DOCX, XLSX, PPTX y formatos de imagen, y puede procesar archivos de hasta 2 GB sin cargar todo el archivo en memoria.  
- **Precisión programática** – defina frases exactas, expresiones regulares o lógica personalizada para apuntar solo a los datos que necesita ocultar.  
- **Políticas XML reutilizables** – exporte sus reglas una vez y compártalas entre equipos, servicios o micro‑servicios.  
- **Motor optimizado para rendimiento** – la biblioteca procesa documentos de cientos de páginas en menos de un segundo en hardware de servidor típico, lo que la hace adecuada para canalizaciones de alto rendimiento.

## Requisitos previos
- Biblioteca GroupDocs.Redaction compatible con su tiempo de ejecución .NET.  
- Visual Studio, VS Code o cualquier IDE que soporte C#.  
- Familiaridad básica con C# y la estructura de proyectos .NET.

## Configuración de GroupDocs.Redaction para .NET

Primero, agregue la biblioteca a su proyecto.

**Usando .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Usando Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

O busque “GroupDocs.Redaction” en la interfaz del Administrador de paquetes NuGet y instálelo desde allí.

### Adquisición de licencia
- Comience con una **prueba gratuita** para explorar las funcionalidades.  
- Solicite una **licencia temporal** para pruebas extendidas, luego adquiera una licencia completa para uso en producción.

### Inicialización básica
Agregue el espacio de nombres a su archivo fuente:

La clase `Redactor` es el motor central que carga un documento y aplica reglas de redacción.  
```csharp
using GroupDocs.Redaction;
```  

La clase `Redactor` es el motor central de GroupDocs.Redaction que carga un documento y aplica reglas de redacción.

## Cómo crear una política de redacción paso a paso

A continuación se muestra una guía completa que demuestra cómo crear programáticamente una política de redacción, configurar sus reglas, aplicarlas a un documento y, finalmente, guardar la política como un archivo XML para reutilizarla en el futuro, garantizando una redacción consistente en múltiples proyectos y tipos de documentos.

### Paso 1: prepare su directorio de documentos
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Reemplace `"YOUR_DOCUMENT_DIRECTORY"` con la carpeta que contiene los documentos que desea proteger.*

### Paso 2: cargue el documento
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
El objeto `Redactor` abre el archivo y gestiona su ciclo de vida.

### Paso 3: defina las redacciones
ExactPhraseRedaction define una regla que reemplaza una frase específica, mientras que `RegexRedaction` utiliza una expresión regular para coincidir patrones.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Aquí creamos dos reglas:  
1. **ExactPhraseRedaction** – reemplaza una frase conocida con “[REDACTED]”.  
2. **RegexRedaction** – encuentra fechas en formato `YYYY‑MM‑DD` y las reemplaza con “[DATE REDACTED]”.

### Paso 4: aplique las redacciones
```csharp
redactor.Apply(redactions);
```  
Todas las reglas definidas se ejecutan contra el documento abierto en una sola pasada.

### Paso 5: guarde la política como un archivo XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
El archivo XML almacena las definiciones de redacción, lo que le permite reutilizar la misma política sin reescribir código.

## Aplicaciones prácticas

- **Despachos legales** pueden redactar números de caso y nombres de clientes antes de compartir borradores.  
- **Departamentos financieros** ocultan números de cuenta o fechas de transacciones en informes.  
- **Proveedores de salud** garantizan el cumplimiento de HIPAA al eliminar identificadores de pacientes.

## Consejos de rendimiento

- Abra **un documento a la vez** para mantener bajo el uso de memoria.  
- Escriba **expresiones regulares eficientes**; evite patrones demasiado amplios que aumenten el tiempo de procesamiento.  
- Mantenga la biblioteca **actualizada** para beneficiarse de mejoras de rendimiento y nuevos tipos de redacción.

## Problemas comunes y soluciones

| Problema | Por qué ocurre | Cómo solucionarlo |
|----------|----------------|-------------------|
| **Excepción de E/S al preparar el directorio** | Ruta incorrecta o permisos de escritura faltantes | Verifique que la carpeta exista y que la aplicación tenga derechos de lectura/escritura. |
| **Regex no coincide con el texto esperado** | El patrón es demasiado estricto o faltan caracteres de escape | Pruebe la expresión regular con un probador en línea; ajuste los cuantificadores o escape los caracteres especiales. |
| **Archivo de política no creado** | `SavePolicy` llamado antes de aplicar las redacciones o con una ruta inválida | Asegúrese de que el directorio de salida sea escribible y llame a `SavePolicy` después de `Apply`. |

## Preguntas frecuentes

**P: ¿Puedo cargar una política XML existente en lugar de crear una programáticamente?**  
R: Sí—use `redactor.LoadPolicy("policy.xml")` para importar una política guardada previamente.

**P: ¿GroupDocs.Redaction admite PDFs protegidos con contraseña?**  
R: Absolutamente. Pase la contraseña al constructor `Redactor`: `new Redactor(sourceFile, "password")`.

**P: ¿Es posible redactar imágenes o metadatos?**  
R: El SDK proporciona las clases `ImageRedaction` y `MetadataRedaction` para esos escenarios.

**P: ¿Cómo manejo documentos grandes (cientos de MB)?**  
R: Procéselos en fragmentos o use la API de streaming para reducir la huella de memoria; el motor puede manejar archivos de hasta 2 GB sin cargar todo el archivo en RAM.

**P: ¿Qué modelo de licencia se requiere para uso comercial?**  
R: Se requiere una licencia paga para despliegues en producción; una licencia de prueba es suficiente para desarrollo y pruebas.

## Conclusión

Ahora tiene una **política de redacción** completa y reutilizable que puede aplicar a cualquier documento con GroupDocs.Redaction para .NET. Al exportar la política a XML, simplifica futuras actualizaciones y garantiza una protección de datos consistente en toda su organización.

### Próximos pasos
- Experimente con tipos de redacción adicionales como `ImageRedaction` o `MetadataRedaction`.  
- Integre la lógica de carga de políticas en su flujo de trabajo de gestión de documentos para redacción automatizada.  
- Explore la referencia de la API de **GroupDocs.Redaction** para personalizaciones avanzadas.

---

**Última actualización:** 2026-10-06  
**Probado con:** GroupDocs.Redaction 5.8 for .NET  
**Autor:** GroupDocs  

**Recursos**  
- [Documentación](https://docs.groupdocs.com/redaction/net/)  
- [Referencia de API](https://reference.groupdocs.com/redaction/net)  
- [Descarga](https://releases.groupdocs.com/redaction/net/)  
- [Foro de soporte gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Solicitud de licencia temporal](https://purchase.groupdocs.com/temporary-license/)

## Tutoriales relacionados

- [Redactar datos sensibles con GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implementar la redacción de documentos usando GroupDocs.Redaction .NET&#58; Guía paso a paso](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [Cómo redactar documentos con GroupDocs.Redaction .NET – Guía completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)