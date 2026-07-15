---
date: 2026-06-11
description: Aprenda cómo cargar document, incluyendo desde streams y password‑protected
  files, usando GroupDocs.Redaction for .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Cómo cargar un Document con GroupDocs.Redaction for .NET
type: docs
url: /es/net/document-loading/
weight: 2
---

# Cómo cargar un documento con GroupDocs.Redaction para .NET

En esta guía descubrirá **cómo cargar documentos** en GroupDocs.Redaction para .NET desde una variedad de fuentes: disco local, flujos de memoria y archivos protegidos con contraseña. Ya sea que esté creando un servicio de redacción, una canalización de cumplimiento automatizada o una utilidad de escritorio sencilla, dominar estas técnicas de carga le permite preparar cualquier documento para una redacción segura de forma rápida y fiable.

## Respuestas rápidas
- **¿Cuál es el primer paso?** Instale el paquete NuGet de GroupDocs.Redaction y agregue el espacio de nombres `using GroupDocs.Redaction;`.  
- **¿Puedo cargar un PDF desde un flujo?** Sí—pase un `MemoryStream` que contenga los bytes del PDF al constructor de `RedactionEngine`.  
- **¿Cómo abro un archivo protegido con contraseña?** Proporcione la contraseña como segundo argumento al crear el `RedactionEngine`.  
- **¿Existe un límite de tamaño de archivo?** GroupDocs.Redaction procesa archivos de hasta 2 GB sin cargar todo el archivo en memoria.  
- **¿Necesito una licencia para desarrollo?** Una licencia temporal funciona para pruebas; se requiere una licencia completa para implementaciones en producción.

## ¿Cómo cargar un documento?
`RedactionEngine` es la clase central que carga y prepara documentos para la redacción. Cargue un documento creando una instancia de `RedactionEngine` con la ruta del archivo (o el flujo) y, si es necesario, la contraseña. Esta llamada de una sola línea lee el archivo, valida el formato y construye el modelo interno del documento listo para la redacción. Por ejemplo, cargar un PDF desde el disco es tan simple como `new RedactionEngine("sample.pdf")`. Cuando se requiere una contraseña, use `new RedactionEngine("secret.pdf", "MyPassword")`. Cargar desde un flujo sigue el mismo patrón con un argumento `MemoryStream`.

## ¿Qué es GroupDocs.Redaction?
GroupDocs.Redaction es una biblioteca .NET que permite a los desarrolladores localizar y eliminar permanentemente contenido sensible de PDF, DOCX, PPTX y más de 30 formatos de archivo adicionales. Ofrece redacción pixel‑perfecta, soporte OCR y procesamiento por lotes, lo que la hace ideal para aplicaciones orientadas al cumplimiento que requieren protección de datos fiable y segura en muchos tipos de documentos.

## ¿Por qué usar GroupDocs.Redaction para cargar documentos?
GroupDocs.Redaction proporciona un motor de streaming de alto rendimiento y bajo consumo de memoria que puede manejar archivos grandes de hasta 2 GB, al mismo tiempo que admite documentos protegidos con contraseña de forma nativa. Esta combinación de velocidad, flexibilidad y seguridad lo convierte en la opción preferida para los desarrolladores que necesitan cargar documentos rápida y seguramente antes de aplicar reglas de redacción.

- **Amplio soporte de formatos:** Maneja **más de 30** tipos de documentos, incluidos PDF, Word, Excel, PowerPoint y archivos de imagen.  
- **Transmisión de alto rendimiento:** Procesa archivos de hasta **2 GB** usando un motor de streaming de bajo consumo de memoria, eliminando la necesidad de cargar el archivo completo.  
- **Manejo de contraseñas:** Abre sin problemas **PDFs y archivos de Office protegidos con contraseña** con una única sobrecarga de método, reduciendo la complejidad del código.  
- **API segura para subprocesos:** Permite la carga concurrente de varios documentos en servicios multihilo sin condiciones de carrera.

## Requisitos previos
- .NET 6.0 o posterior (la biblioteca también admite .NET Core 3.1 y .NET Framework 4.6.1+).  
- Una licencia válida de GroupDocs.Redaction (licencia temporal para pruebas).  
- Acceso a los archivos de documento que desea redactar (ruta local, matriz de bytes o flujo).

## Cargando documentos desde diferentes fuentes

### Cargar desde disco local
Proporcione la ruta absoluta o relativa al archivo al construir el motor. La biblioteca detecta automáticamente el formato y lo prepara para la redacción.

### Cargar desde un flujo de memoria
Lea el archivo en un `byte[]`, envuélvalo en un `MemoryStream` y pase el flujo al constructor. Este enfoque es perfecto para APIs web que reciben archivos como cargas.

### Cargar archivos protegidos con contraseña
Cuando un documento está cifrado, suministre la contraseña como segundo argumento. El motor descifra el archivo al vuelo y pone el contenido a disposición para la redacción sin pasos adicionales.

## Problemas comunes y soluciones

- **Error: “File format not supported.”**  
  Verifique que la extensión del archivo coincida con un formato compatible y que el archivo no esté dañado. GroupDocs.Redaction admite más de 30 formatos; consulte la referencia de la API para obtener la lista completa.

- **Excepción relacionada con la contraseña.**  
  Asegúrese de que la cadena de contraseña sea correcta y de que el archivo realmente requiera una contraseña. Pasar una cadena vacía a un archivo protegido provocará un error de autenticación.

- **Falta de memoria para archivos muy grandes.**  
  Utilice la sobrecarga de streaming (`RedactionEngine(Stream)`) en lugar de cargar el archivo por ruta. Esto mantiene bajo el uso de memoria incluso para PDFs de cientos de páginas.

## Preguntas frecuentes

**Q: ¿Puedo cargar archivos DOCX de la misma manera que cargo PDFs?**  
A: Sí—GroupDocs.Redaction detecta automáticamente el formato DOCX cuando pasa la ruta del archivo o el flujo, por lo que no se necesita código adicional.

**Q: ¿La biblioteca admite cargar archivos desde Azure Blob Storage?**  
A: Absolutamente. Recupere el blob como una matriz de bytes o flujo y páselo al constructor de `RedactionEngine`.

**Q: ¿Qué ocurre si proporciono una contraseña incorrecta?**  
A: El constructor lanza una `PasswordIncorrectException`. Capture esta excepción para solicitar al usuario la contraseña correcta.

**Q: ¿Es posible cargar varios documentos simultáneamente?**  
A: Sí—cada instancia de `RedactionEngine` es independiente y segura para subprocesos, lo que permite el procesamiento paralelo en servicios en segundo plano.

**Q: ¿Necesito disponer manualmente del RedactionEngine?**  
A: El motor implementa `IDisposable`. Llame a `Dispose()` o envuélvalo en un bloque `using` para liberar los manejadores de archivo de inmediato.

## Recursos adicionales

- [Cómo cargar y redactar documentos usando GroupDocs.Redaction .NET&#58; una guía completa](./groupdocs-redaction-net-load-redact-documents/)
- [Cómo redactar de forma segura documentos protegidos con contraseña usando GroupDocs.Redaction en .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Documentación de GroupDocs.Redaction para .NET](https://docs.groupdocs.com/redaction/net/)
- [Referencia de API de GroupDocs.Redaction para .NET](https://reference.groupdocs.com/redaction/net/)
- [Descargar GroupDocs.Redaction para .NET](https://releases.groupdocs.com/redaction/net/)
- [Foro de GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Soporte gratuito](https://forum.groupdocs.com/)
- [Licencia temporal](https://purchase.groupdocs.com/temporary-license/)

---

**Última actualización:** 2026-06-11  
**Probado con:** GroupDocs.Redaction 5.5 for .NET  
**Autor:** GroupDocs

## Tutoriales relacionados

- [Cómo cargar y redactar documentos usando GroupDocs.Redaction .NET: una guía completa](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redactar y guardar documentos con GroupDocs.Redaction para .NET: una guía completa](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)