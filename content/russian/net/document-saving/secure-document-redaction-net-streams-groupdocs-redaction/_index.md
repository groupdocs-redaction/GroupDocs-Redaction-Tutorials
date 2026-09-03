---
date: '2026-07-06'
description: Узнайте, как редактировать документы .net с помощью streams с использованием
  GroupDocs.Redaction. Этот учебник охватывает setup, load document from stream, applying
  redactions и saving securely.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: Редактировать документы .net с помощью streams – Руководство GroupDocs.Redaction
type: docs
url: /ru/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Редактирование документов .net с помощью потоков – Полное руководство

Добро пожаловать! В этом руководстве вы узнаете, как безопасно **redact documents .net** с помощью потоков и GroupDocs.Redaction. Мы пройдем всё, что вам нужно — от установки библиотеки, загрузки документа из потока, применения точных редактирований, до сохранения результата без создания временных файлов на диске.

## Быстрые ответы
- **Какая библиотека обрабатывает редактирование в .NET?** GroupDocs.Redaction for .NET.  
- **Можно ли загрузить файл напрямую из потока?** Да — используйте `FileStream` с конструктором Redactor.  
- **Какие форматы поддерживаются?** Более 70 входных и выходных форматов, включая PDF, DOCX, XLSX, PPTX.  
- **Нужна ли лицензия для продакшн?** Требуется действующая лицензия GroupDocs.Redaction для использования не в пробном режиме.  
- **Безопасно ли это для больших файлов?** Обработка на основе потоков избегает загрузки всего файла в память, позволяя работать с многогигабайтными документами.

## Что такое “redact documents .net”?
**“Redact documents .net”** относится к процессу постоянного удаления или маскирования конфиденциального содержимого из файлов с использованием .NET библиотек, таких как GroupDocs.Redaction. Это гарантирует, что конфиденциальные данные никогда не покидают вашу систему в открытом виде. Обычно используется в юридическом, финансовом и медицинском секторах для соблюдения нормативов конфиденциальности, таких как GDPR и HIPAA, обеспечивая невозможность восстановления чувствительных данных после обработки.

## Почему использовать потоки для редактирования?
GroupDocs.Redaction поддерживает **более 70 форматов файлов** и может обрабатывать файлы размером до **2 ГБ** без полной загрузки их в память. Потоковая обработка снижает нагрузку ввода‑вывода, повышает производительность и соответствует лучшим практикам безопасности, удерживая данные в памяти только на короткое время, необходимое для преобразования.

## Предварительные требования
- **GroupDocs.Redaction for .NET** – установить через NuGet (см. ниже).  
- **.NET 6+** (или .NET Framework 4.6.1+).  
- Visual Studio 2022 или любой совместимый IDE.  
- Базовые знания C# и знакомство с .NET потоками.

## Установка GroupDocs.Redaction
Вы можете добавить пакет с помощью любой из этих команд:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Или найдите “GroupDocs.Redaction” в UI NuGet Package Manager и нажмите **Install**.

### Шаги получения лицензии
1. **Free Trial** – скачайте пробную версию с [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – запросите краткосрочный ключ для оценки.  
3. **Full Purchase** – получите постоянную лицензию для производственных нагрузок.

После установки инициализируйте библиотеку в вашем коде:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Как загрузить документ из потока?
`FileStream` предоставляет поток для чтения и записи файла на диске. Класс `Redactor` обрабатывает документ и применяет правила редактирования. Загрузите исходный файл в `FileStream`, затем передайте поток конструктору `Redactor`. Такой подход избегает записи оригинального файла во временное место и держит данные в памяти только на время обработки. Этот метод работает для любого поддерживаемого формата, включая PDF и офисные документы.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Как инициализировать Redactor с потоком?
Класс `Redactor` — это основной движок, который манипулирует содержимым документа. Предоставив входной поток, вы включаете редактирование в памяти без промежуточных файлов. После создания экземпляра вы можете цепочкой применять правила редактирования, предварительно просматривать изменения и настраивать параметры, такие как растеризация или шифрование, перед сохранением окончательного документа.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Определение якоря:** `GroupDocs.Redaction.Redactor` — основной класс, предоставляющий методы для применения, предварительного просмотра и фиксации операций редактирования над документом, загруженным из потока.

## Как применить редактирования?
Вы можете добавить несколько действий редактирования; пример ниже удаляет все аннотации, что часто требуется для удаления скрытых комментариев или заметок рецензентов. Дополнительные типы редактирования, такие как `DeleteTextRedaction` или `ReplaceTextRedaction`, можно комбинировать для удаления или маскирования конкретных строк, дат или шаблонов по всему документу.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Определение якоря:** `DeleteAnnotationRedaction` — встроенное правило редактирования, которое навсегда стирает объекты аннотаций, такие как комментарии, выделения и штампы из документа.

## Как сохранить отредактированный документ?
Сохранение напрямую в `FileStream` гарантирует, что вывод записывается за один проход, устраняя необходимость во временных файлах. Вы также можете указать формат вывода, уровень сжатия и опциональную защиту паролем через объект `SaveOptions`, чтобы соответствовать требованиям безопасности. В конце закройте выходной поток, чтобы освободить дескрипторы файлов и убедиться, что файл полностью записан на диск.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Определение якоря:** `SaveOptions` позволяет управлять способом сохранения документа, включая растеризацию, шифрование и выбор формата.

## Общие сценарии использования
- **Обработка юридических документов:** Удалять конфиденциальные аннотации перед отправкой черновиков клиентам.  
- **Соответствие GDPR:** Удалять персональные идентификаторы из контрактов или записей сотрудников.  
- **Внутренние аудиторские отчёты:** Скрывать заметки рецензентов, сохраняя основное содержание для распространения.

## Советы по производительности для больших файлов
1. **Своевременно освобождать потоки** – операторы `using` автоматически закрывают потоки, освобождая память.  
2. **Пакетная обработка** – перебирайте коллекцию файлов и переиспользуйте один экземпляр `Redactor`, когда формат позволяет, уменьшая накладные расходы на выделение.

## Устранение неполадок
1. **Отказ в доступе к файлу** – Убедитесь, что учётная запись приложения имеет права чтения/записи в целевых папках.  
2. **Редактирование не применено** – Убедитесь, что выбранный тип редактирования совместим с форматом документа (например, `DeleteAnnotationRedaction` работает для PDF и DOCX).

## Часто задаваемые вопросы

**Q: Какие форматы файлов можно обрабатывать с помощью потоков?**  
A: GroupDocs.Redaction поддерживает более 70 форматов — включая PDF, DOCX, XLSX, PPTX и HTML — при использовании API на основе потоков.

**Q: Можно ли предварительно просмотреть редактирования перед сохранением?**  
A: Да, вызовите `redactor.GetRedactedDocument()`, чтобы получить представление в памяти, которое можно отобразить или программно проанализировать.

**Q: Как библиотека обрабатывает файлы, защищённые паролем?**  
A: Укажите пароль при открытии потока через перегрузки `Redactor`, принимающие `LoadOptions` с паролем.

**Q: Есть ли ограничение по размеру документа?**  
A: Движок может обрабатывать файлы до 2 ГБ; более крупные файлы следует разбивать или обрабатывать частями, чтобы оставаться в пределах памяти.

**Q: Нужна ли отдельная лицензия для каждой среды развертывания?**  
A: Один лицензионный ключ может использоваться в нескольких средах, при условии соблюдения условий лицензионного соглашения.

## Заключение
Теперь у вас есть полное пошаговое решение для **redact documents .net** с использованием потоков и GroupDocs.Redaction. Загружая файлы напрямую из потоков, применяя целевые редактирования и сохраняя без промежуточных артефактов, вы достигаете как безопасности, так и производительности. Изучите дополнительные типы редактирования — такие как замена текста или удаление метаданных — чтобы адаптировать процесс к вашим конкретным требованиям соответствия.

---

**Последнее обновление:** 2026-07-06  
**Тестировано с:** GroupDocs.Redaction 5.0 for .NET  
**Автор:** GroupDocs  

## Ресурсы
- [Документация](https://docs.groupdocs.com/redaction/net/)
- [Справочник API](https://reference.groupdocs.com/redaction/net)
- [Скачать](https://releases.groupdocs.com/redaction/net/)
- [Форум бесплатной поддержки](https://forum.groupdocs.com/c/redaction/33)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## Связанные руководства

- [Как загрузить и отредактировать документы с помощью GroupDocs.Redaction .NET&#58; Полное руководство](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Редактировать и сохранять документы с GroupDocs.Redaction для .NET&#58; Полное руководство](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Как извлечь метаданные документа из потоков с помощью GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)