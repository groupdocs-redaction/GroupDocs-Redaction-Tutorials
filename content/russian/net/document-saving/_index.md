---
date: 2026-06-11
description: Узнайте, как экспортировать отредактированные файлы, настроить папки
  вывода, создавать растровые PDF и сохранять в потоки, используя GroupDocs.Redaction
  for .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Как экспортировать отредактированные документы с помощью GroupDocs.Redaction
  .NET
type: docs
url: /ru/net/document-saving/
weight: 3
---

# Как экспортировать редактированные документы с помощью GroupDocs.Redaction .NET

В этом полном руководстве вы узнаете **как экспортировать редактированные** данные безопасно и эффективно, используя GroupDocs.Redaction для .NET. Независимо от того, нужно ли вам сохранить оригинальный тип файла, зафиксировать документ в виде растрового PDF или передать результат напрямую в память, мы подробно рассмотрим каждый вариант с понятными объяснениями и практическими советами. К концу этого урока вы сможете выбрать правильную стратегию экспорта для любой задачи, связанной с соблюдением нормативных требований.

## Быстрые ответы
- **Какие форматы я могу экспортировать?** Любой из более чем 30 нативных форматов, поддерживаемых GroupDocs.Redaction, плюс растровый PDF для максимальной безопасности.  
- **Нужна ли лицензия для потоковой передачи?** Да, для производственной потоковой передачи требуется действующая лицензия GroupDocs.Redaction.  
- **Можно ли задать пользовательскую папку вывода?** Абсолютно — используйте свойство `OutputPath` или `SaveOptions` для её настройки.  
- **Безопасна ли растеризация для больших файлов?** Она обрабатывает документы до 500 страниц без загрузки всего файла в память.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Что такое GroupDocs.Redaction?
GroupDocs.Redaction — это .NET‑библиотека, которая программно удаляет или маскирует конфиденциальную информацию из PDF, Word, Excel, PowerPoint, изображений и многих других форматов. Она предоставляет высокоуровневый API для определения областей редактирования, применения политик и окончательного экспорта очищенного документа. Это упрощает интеграцию возможностей редактирования в любое .NET‑приложение.

## Почему экспортировать редактированные документы в виде растровых PDF?
Растровые PDF преобразуют каждую страницу в плоское изображение, устраняя скрытые текстовые слои, которые могли бы быть извлечены позже. Такой формат гарантирует, что редактированный контент невозможно восстановить, соответствуя строгим нормативным требованиям, таким как GDPR и HIPAA. GroupDocs.Redaction может создавать растровые PDF с разрешением до 300 dpi, сохраняя визуальное качество при обеспечении безопасности.

## Как экспортировать редактированные документы?
Загрузите исходный файл, примените правила редактирования, затем вызовите соответствующий метод сохранения — либо `Save` для оригинального формата, `SaveAsRasterizedPdf` для PDF только с изображениями, либо `SaveToStream` для обработки в памяти. Ниже представлена пошаговая последовательность. Каждый метод гарантирует окончательное удаление редактированного контента при сохранении желаемого формата вывода.

### Шаг 1: Установите пакет NuGet
Добавьте последнюю версию пакета GroupDocs.Redaction в ваш проект:

```bash
dotnet add package GroupDocs.Redaction
```

### Шаг 2: Загрузите документ и определите редактирования
Создайте экземпляр `Redactor`, загрузите файл и укажите области, которые нужно скрыть. Класс `Redactor` предоставляет основную функциональность для загрузки документов и применения правил редактирования.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Шаг 3: Выберите метод экспорта
#### Экспорт в оригинальном формате
```csharp
redactor.Save("RedactedReport.docx");
```

#### Экспорт в виде растрового PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Экспорт в поток памяти (идеально для веб‑API)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Метод `Save` записывает редактированный документ в файл в его оригинальном формате. `SaveAsRasterizedPdf` создаёт PDF, где каждая страница отрисовывается как изображение, удаляя любые скрытые текстовые слои. `SaveToStream` возвращает редактированный файл в виде потока памяти, подходящего для веб‑ответов.

## Как настроить папку вывода?
Установите свойство `OutputPath` у объекта `Redactor` или передайте пользовательский объект `SaveOptions`, включающий требуемый каталог. `OutputPath` — свойство `Redactor`, указывающее директорию, в которую записываются файлы вывода. `SaveOptions` позволяет настроить различные параметры сохранения, включая папку вывода. Это гарантирует, что все экспортированные файлы окажутся в предсказуемом месте, упрощая конвейеры пакетной обработки. Вы также можете задавать подпапки для каждого типа документа, чтобы поддерживать порядок в рабочем пространстве.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Распространённые проблемы и решения
- **Редактирование не применилось:** Убедитесь, что шаблон поиска точно совпадает с текстом документа; при необходимости используйте `RegexOptions.IgnoreCase`. `RegexOptions` — перечисление, контролирующее поведение сопоставления регулярных выражений, например чувствительность к регистру.  
- **Большие файлы вызывают нагрузку на память:** Включите режим потоковой передачи, используя `SaveToStream`, и избегайте вызова `Save` для всего документа.  
- **Растровый PDF выглядит размытым:** Увеличьте DPI в `RasterizationOptions` (например, 300–600), чтобы улучшить качество изображения. `RasterizationOptions` позволяет задавать параметры, такие как DPI и формат изображения, для вывода растрового PDF.

## Часто задаваемые вопросы

**В: Можно ли экспортировать в формат, который изначально не поддерживался?**  
О: Да, GroupDocs.Redaction может конвертировать большинство входных типов в PDF, DOCX, XLSX, PPTX или растровый PDF, охватывая более 30 форматов.

**В: Как растеризация защищает редактированные данные?**  
О: При отрисовке каждой страницы как плоского изображения все скрытые текстовые слои удаляются, делая невозможным извлечение оригинального содержимого.

**В: Можно ли последовательно применять несколько правил редактирования?**  
О: Абсолютно — вы можете вызывать `Apply` многократно или передать коллекцию `RedactionOptions` для обработки множества шаблонов за один проход. `RedactionOptions` определяет настройки для одной операции редактирования, такие как область и тип замены.

**В: Нужно ли закрывать объект Redactor?**  
О: Класс `Redactor` реализует `IDisposable`; оберните его в блок `using` или вызовите `Dispose()`, чтобы своевременно освободить файловые дескрипторы. `IDisposable` — интерфейс, предоставляющий механизм освобождения неуправляемых ресурсов.

**В: Какие среды выполнения .NET официально протестированы?**  
О: GroupDocs.Redaction проверен на .NET Framework 4.6+, .NET Core 3.1+, и .NET 5/6/7.

## Дополнительные ресурсы

### Доступные руководства

- [Как сохранять документы в виде растровых PDF с помощью GroupDocs.Redaction для .NET: Полное руководство](./groupdocs-redaction-net-rasterized-pdfs/)
- [Реализация каталога вывода в .NET с GroupDocs.Redaction: Полное руководство](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Редактирование и сохранение документов с GroupDocs.Redaction для .NET: Полное руководство](./redact-save-documents-groupdocs-redaction-net/)
- [Сохранение редактированных документов в оригинальном формате с использованием GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Безопасное редактирование документов в .NET с использованием потоков: Руководство для GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Полезные ссылки

- [Документация GroupDocs.Redaction для .NET](https://docs.groupdocs.com/redaction/net/)
- [Справочник API GroupDocs.Redaction для .NET](https://reference.groupdocs.com/redaction/net/)
- [Скачать GroupDocs.Redaction для .NET](https://releases.groupdocs.com/redaction/net/)
- [Форум GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Бесплатная поддержка](https://forum.groupdocs.com/)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-06-11  
**Тестировано с:** GroupDocs.Redaction 23.11 for .NET  
**Автор:** GroupDocs  

---

## Связанные руководства

- [Сохранение редактированных документов в оригинальном формате с использованием GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Как сохранять документы в виде растровых PDF с помощью GroupDocs.Redaction для .NET: Полное руководство](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Безопасное редактирование документов в .NET с использованием потоков: Руководство для GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)