---
date: '2026-06-06'
description: Узнайте, как получать метаданные и извлекать метаданные документов с
  помощью GroupDocs.Redaction .NET, обеспечивая надёжное управление документами и
  соответствие требованиям.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: Как получить метаданные с помощью GroupDocs.Redaction .NET API
type: docs
url: /ru/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# Как получить метаданные с помощью GroupDocs.Redaction .NET

В современную цифровую эпоху **как получить метаданные** из файла — фундаментальный шаг для любого приложения, ориентированного на документы. Независимо от того, нужно ли вам читать метаданные файлов для аудитов соответствия, извлекать свойства документа для индексации или просто отображать размер документа в пользовательском интерфейсе, GroupDocs.Redaction .NET предоставляет лаконичное API, позволяющее сделать это всего за несколько строк C#. Этот учебник проведёт вас через весь процесс, от настройки окружения до отображения полученной информации, чтобы вы могли сразу начать извлекать метаданные документов.

## Быстрые ответы
- **Каков основной метод получения метаданных?** Вызовите `Redactor.GetDocumentInfo()` у экземпляра `Redactor`.  
- **Какие форматы поддерживаются?** Более 50 форматов ввода и вывода, включая PDF, DOCX, XLSX, PPTX и типы изображений.  
- **Нужна ли лицензия для разработки?** Бесплатная пробная лицензия подходит для тестирования; полная лицензия требуется для продакшн.  
- **Можно ли обрабатывать большие файлы?** Да — GroupDocs.Redaction обрабатывает документы с несколькими сотнями страниц без загрузки всего файла в память.  
- **Доступна ли поддержка async?** API можно обернуть в асинхронные паттерны, чтобы UI‑потоки оставались отзывчивыми.

## Что такое извлечение метаданных в GroupDocs.Redaction?
Извлечение метаданных — это процесс доступа к встроенным свойствам документа, таким как тип файла, количество страниц и размер, через API библиотеки. Извлекая эти свойства, разработчики могут программно оценивать характеристики документа, поддерживать индексацию, применять правила соответствия и принимать обоснованные решения о дальнейших шагах обработки.

## Как получить метаданные документа?
Класс `Redactor` является основным интерфейсом для загрузки и инспекции документов в GroupDocs.Redaction.  
`GetDocumentInfo()` — метод, который возвращает объект `DocumentInfo`, содержащий метаданные документа.  

Загрузите ваш файл с помощью `new Redactor("path/to/file")` и вызовите `GetDocumentInfo()` — вызов возвращает объект `DocumentInfo`, содержащий тип, количество страниц, размер и другие свойства. Такой двухшаговый подход работает для любого поддерживаемого формата и не требует дополнительной конфигурации. Затем вы можете читать поля, такие как `FileType`, `PageCount` и `FileSize`, чтобы отобразить или записать информацию.

## Предварительные требования

- **GroupDocs.Redaction .NET** версии 21.6 или новее.  
- .NET Framework 4.7.2 +, .NET Core 3.1 + или .NET 5/6+.  
- Базовые знания C# и среда разработки (Visual Studio, Rider и т.д.).

## Настройка GroupDocs.Redaction для .NET

Начать работу с GroupDocs.Redaction просто. Установите пакет одним из следующих методов:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Или используйте **NuGet Package Manager UI**: просто найдите “GroupDocs.Redaction” и нажмите **Install**.

### Получение лицензии

Чтобы попробовать GroupDocs.Redaction, вы можете получить бесплатную пробную лицензию. Для постоянной разработки или использования в продакшн приобретите полную лицензию или запросите временную лицензию на официальном сайте.

После установки инициализируйте библиотеку следующим образом:

```csharp
using GroupDocs.Redaction;
```

## Руководство по реализации

### Функция получения информации о документе

Эта функция сосредоточена на извлечении важной метаданных из документов с помощью GroupDocs.Redaction .NET. Следуйте этим шагам:

#### Шаг 1: Подготовьте путь к документу

Определите абсолютный или относительный путь к целевому файлу:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Замените `YOUR_DOCUMENT_DIRECTORY` на папку, содержащую ваш документ.

#### Шаг 2: Инициализировать экземпляр Redactor

Создайте объект `Redactor`, который предоставляет доступ к методам метаданных:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Шаг 3: Получить информацию о документе

Вызовите `GetDocumentInfo()` у экземпляра `Redactor`, чтобы получить все доступные свойства:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

Возвращаемый объект включает тип файла, количество страниц и размер файла.

#### Шаг 4: Отобразить детали документа

Выведите информацию в консоль или UI. Пример кода (закомментирован для самостоятельного запуска) демонстрирует, как вывести каждое свойство:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Почему использовать GroupDocs.Redaction для извлечения метаданных?
GroupDocs.Redaction поддерживает **более 50 форматов файлов** и может обрабатывать документы размером до **2 ГБ**, при этом потребление памяти обычно не превышает **100 МБ** для типовых нагрузок. Библиотека извлекает метаданные без полной загрузки документа, обеспечивая быстрые ответы — часто менее **200 мс** для PDF‑файла в 100 страниц на стандартном серверном оборудовании.

### Распространённые проблемы и решения

- **Неправильный путь к файлу** — проверьте строку пути и убедитесь, что файл доступен процессу.  
- **Неподдерживаемый формат** — проверьте список форматов; если формат отсутствует, рассмотрите возможность предварительного конвертирования.  
- **Узкие места в производительности** — для очень больших файлов включите опции потоковой передачи или обрабатывайте страницы пакетами, чтобы ограничить использование памяти.

## Практические применения

Понимание метаданных документа открывает несколько реальных сценариев:

1. **Системы управления документами (DMS)** — автоматизировать категоризацию и индексацию на основе типа, размера или количества страниц.  
2. **Аудит соответствия** — проверять, что конфиденциальные файлы содержат необходимые метаданные перед архивированием.  
3. **Миграция данных** — группировать файлы по свойствам для упрощения массовых задач миграции.

## Соображения по производительности

- **Эффективное использование ресурсов** — используйте экземпляр `Redactor` внутри блока `using`, чтобы гарантировать корректное освобождение.  
- **Асинхронные паттерны** — оберните вызовы метаданных в `Task.Run` или реализуйте async‑обёртки, чтобы UI‑потоки оставались отзывчивыми в настольных или веб‑приложениях.

## Часто задаваемые вопросы

**В: Какие форматы документов я могу извлекать метаданные?**  
О: GroupDocs.Redaction читает метаданные более чем из 50 форматов, включая PDF, DOCX, XLSX, PPTX, HTML и распространённые типы изображений.

**В: Как работать с файлами, защищёнными паролем?**  
О: Передайте пароль в конструктор `Redactor`; API расшифрует файл перед извлечением метаданных.

**В: Есть ли ограничение на размер файлов, которые я могу обрабатывать?**  
О: Хотя строгого ограничения нет, файлы более 2 ГБ могут потребовать дополнительной настройки памяти; производительность остаётся линейной относительно размера файла.

**В: Можно ли получать метаданные пакетно?**  
О: Да — пройдитесь по коллекции путей к файлам и вызовите `GetDocumentInfo()` для каждого; библиотека потокобезопасна для параллельного выполнения.

**В: Нужна ли лицензия для сборок разработки?**  
О: Бесплатная пробная лицензия достаточна для разработки и тестирования; коммерческая лицензия требуется для продакшн‑развёртываний.

## Ресурсы

- [Документация](https://docs.groupdocs.com/redaction/net/)  
- [Справочник API](https://reference.groupdocs.com/redaction/net)  
- [Скачать](https://releases.groupdocs.com/redaction/net/)  
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/redaction/33)  
- [Информация о временной лицензии](https://purchase.groupdocs.com/temporary-license/)

## Заключение

Теперь у вас есть полное пошаговое руководство по **получению метаданных** с помощью GroupDocs.Redaction .NET. Используя метод `Redactor.GetDocumentInfo()`, вы можете быстро читать метаданные файлов, поддерживать процессы соответствия и улучшать любой конвейер обработки документов. Исследуйте дополнительные функции Redaction — такие как редактирование содержимого, добавление водяных знаков и конвертация документов — чтобы построить полностью функциональное решение для управления документами.

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Redaction .NET 21.6 (последняя на момент написания)  
**Автор:** GroupDocs  

## Связанные руководства

- [Как извлечь метаданные документа из потоков с помощью GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [Как редактировать метаданные документа с помощью GroupDocs.Redaction для .NET — полное руководство](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Учебники по загрузке документов с GroupDocs.Redaction для .NET](/redaction/net/document-loading/)