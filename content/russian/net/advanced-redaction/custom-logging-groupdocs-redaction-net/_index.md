---
date: '2026-10-01'
description: Узнайте, как реализовать custom logger c# в GroupDocs.Redaction для .NET,
  обеспечивая детализированный custom logging .NET и упрощённую отчётность по compliance.
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: Реализуйте custom logger c# в GroupDocs.Redaction для .NET, чтобы
  capture detailed logs, сохранять отредактированные документы без rasterization и
  соответствовать требованиям compliance.
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: Реализация custom logger c# в GroupDocs.Redaction для .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: Реализация custom logger c# в GroupDocs.Redaction для .NET
type: docs
url: /ru/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Реализовать пользовательский логгер c# в GroupDocs.Redaction для .NET

Эффективное управление редактированием документов имеет решающее значение, особенно при работе с конфиденциальной информацией. В этом руководстве вы узнаете **how to implement a custom logger c#** с GroupDocs.Redaction для .NET, получив полный контроль над журналированием, обработкой ошибок и аудиторскими следами. К концу урока вы сможете фиксировать предупреждения, ошибки и информационные сообщения, интегрировать логгер с существующими .NET‑фреймворками журналирования и сохранять отредактированный документ без растеризации.

## Быстрые ответы
- **Что делает пользовательский логгер c#?** Он фиксирует ошибки, предупреждения и информационные сообщения во время редактирования, предоставляя вам поисковый аудиторский след.  
- **Какая библиотека предоставляет интерфейс ILogger?** GroupDocs.Redaction for .NET supplies the `ILogger` interface.  
- **Могу ли я сохранить отредактированный документ без растеризации?** Yes – call `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Нужна ли лицензия для использования в продакшене?** A full license is required for production; a trial license is available for evaluation.  
- **Совместим ли этот подход с .NET Core / .NET 6+?** Absolutely – the same API works across .NET Framework, .NET Core, .NET 5, and .NET 6.

## Что такое пользовательский логгер c#?

**custom logger c#** — это класс, реализующий интерфейс `ILogger`, предоставляемый GroupDocs.Redaction. Он позволяет направлять сообщения журнала туда, где вам нужно — консоль, файл, база данных или внешние системы мониторинга — предоставляя вам полное представление о процессе редактирования.

## Зачем использовать пользовательское журналирование .net с GroupDocs.Redaction?

Оснастите процесс редактирования подробными, поисковыми журналами, которые удовлетворяют регулятивным аудитам и ускоряют устранение неполадок. GroupDocs.Redaction поддерживает **70+ input and output formats** и может обрабатывать документы до 500 страниц без загрузки всего файла в память, поэтому хорошо спроектированный логгер добавляет незначительные накладные расходы, обеспечивая бесценную видимость.

## Требования
- GroupDocs.Redaction for .NET установлен (см. раздел **Installation** ниже).  
- Среда разработки .NET (Visual Studio, VS Code или .NET CLI).  
- Базовые знания C# и знакомство с файловыми потоками.  

## Установка

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Найдите **"GroupDocs.Redaction"** и установите последнюю версию.

## Получение лицензии
- **Free trial:** Test the API with a temporary license.  
- **Temporary license:** Получите полный доступ к функциям на ограниченный период.  
- **Purchase:** Приобретите бессрочную лицензию для продакшн‑развертываний.

## Пошаговое руководство

### Как реализовать пользовательский логгер в .NET Core?

Загрузите класс `CustomLogger` в ваш проект .NET Core и подключите его к `RedactorSettings`. Логгер работает одинаково в .NET Framework, .NET 5 и .NET 6, поэтому вы можете использовать один и тот же код на всех платформах.

### Шаг 1: Определить пользовательский класс логгера (log warnings c#)

Класс `CustomLogger` реализует `ILogger`.  
CustomLogger — это пользовательский класс, реализующий интерфейс `ILogger` для захвата событий редактирования.  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**Definition anchor:** `CustomLogger` — пользовательская реализация интерфейса `ILogger`, записывающая события редактирования.  
**Explanation:** Флаг `HasErrors` помогает решить, продолжать ли обработку. Три метода соответствуют трем уровням журналирования, которые потребуются в большинстве сценариев редактирования.

### Шаг 2: Подготовить пути к файлам и открыть исходный документ

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**Definition anchor:** `Redactor` — основной класс в GroupDocs.Redaction, выполняющий операции редактирования PDF‑документа.  
**Why this matters:** Использование вспомогательных методов сохраняет чистоту кода и гарантирует, что папка вывода существует до попытки **save redacted document**.

### Шаг 3: Применять редактирование с использованием пользовательского логгера

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**Direct answer:** Рабочий процесс редактирования начинается с создания экземпляра `Redactor` с `RedactorSettings(logger)`, затем применения объектов редактирования, проверки `logger.HasErrors` и, наконец, вызова `redactor.Save` с отключённой растеризацией. Этот шаблон гарантирует, что каждый шаг журналируется и сохраняется чистый документ только при отсутствии ошибок.  

**Explanation:**  
1. `Redactor` создаётся с `RedactorSettings(logger)`, связывая ваш `CustomLogger`.  
2. После применения редактирования код проверяет `logger.HasErrors`. Если ошибок нет, документ сохраняется — демонстрируя логику **save redacted document** без растеризации.

## Распространённые подводные камни и устранение неполадок
- **Missing log output:** Убедитесь, что каждый метод `Log*` правильно переопределён.  
- **File access exceptions:** Убедитесь, что приложение имеет права чтения/записи для исходных и целевых путей.  
- **Logger not wired:** Параметр `RedactorSettings(logger)` обязателен; его отсутствие отключает пользовательское журналирование.

## Практические применения
1. **Compliance reporting:** Экспортировать записи журнала в CSV или базу данных для аудиторских следов.  
2. **Error tracking:** Быстро находить проблемные файлы, просматривая вывод `LogError`.  
3. **Workflow automation:** Запускать последующие процессы (например, уведомление сотрудника по соответствию), когда вызывается `LogWarning`.

## Соображения по производительности
- **Dispose streams promptly** освобождать память, особенно при обработке больших пакетов.  
- **Monitor CPU & memory** следить за процессором и памятью во время массового редактирования; рассмотреть параллельную обработку документов с осторожной синхронизацией логгера.  
- **Stay updated:** Новые версии GroupDocs.Redaction часто включают оптимизации производительности и дополнительные точки журналирования.

## Заключение

Реализуя **custom logger c#**, вы получаете детальное представление о каждом этапе конвейера редактирования, что упрощает соблюдение нормативных требований и отладку проблем. Представленный подход без проблем работает с GroupDocs.Redaction для .NET и может быть расширен для интеграции с любой .NET‑системой журналирования, которую вы уже используете.

---

## Часто задаваемые вопросы

**Q: Какова цель пользовательского журналирования с GroupDocs.Redaction?**  
A: Пользовательское журналирование фиксирует детальные события редактирования, удовлетворяет требованиям аудита и упрощает устранение неполадок, предоставляя ошибки и предупреждения в реальном времени.

**Q: Как обрабатывать ошибки с помощью пользовательского логгера?**  
A: Реализуйте `LogError` в вашем классе `CustomLogger`; флаг `HasErrors` позволяет прервать обработку при обнаружении критической проблемы.

**Q: Можно ли интегрировать пользовательское журналирование с другими системами?**  
A: Да — вы можете перенаправлять сообщения журнала в CRM, ERP или централизованные инструменты мониторинга, расширяя методы логгера.

**Q: Какие распространённые подводные камни при реализации пользовательского журналирования?**  
A: Отсутствие переопределения методов, забывание передать `RedactorSettings(logger)` и недостаточные права доступа к файлам — самые частые проблемы.

**Q: Как пользовательское журналирование улучшает рабочие процессы редактирования документов?**  
A: Детальные журналы обеспечивают видимость в реальном времени, упрощают отладку и создают аудиторские следы, требуемые регуляциями, такими как GDPR и HIPAA.

## Ресурсы
- **Документация:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Справочник API:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Скачать:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Последнее обновление:** 2026-10-01  
**Тестировано с:** GroupDocs.Redaction 23.11 for .NET  
**Автор:** GroupDocs  

---

## Связанные руководства
- [Как загрузить документ с GroupDocs.Redaction для .NET](/redaction/net/document-loading/)
- [Как экспортировать отредактированные документы с GroupDocs.Redaction .NET](/redaction/net/document-saving/)
- [Реализация редактирования документов с использованием GroupDocs.Redaction .NET: пошаговое руководство](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)