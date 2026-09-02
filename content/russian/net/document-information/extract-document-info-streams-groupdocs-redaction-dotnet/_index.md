---
date: '2026-06-11'
description: Узнайте, как извлекать метаданные из потоков документов с помощью GroupDocs.Redaction
  для .NET, охватывая настройку, примеры кода и практические применения.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Как извлечь метаданные из потоков документов с помощью GroupDocs.Redaction
  .NET
type: docs
url: /ru/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Как извлечь метаданные из потоков документов с помощью GroupDocs.Redaction .NET

Вы устали вручную извлекать информацию из документов или иметь дело с большими файлами, замедляющими ваш рабочий процесс? **Как быстро извлечь метаданные** — распространённая задача, и библиотека GroupDocs.Redaction для .NET предлагает быстрый, экономичный по памяти способ получения деталей документа напрямую из потоков. В этом руководстве вы узнаете, как настроить библиотеку, получить тип файла, количество страниц и размер из потока, а также подготовить папку вывода для дальнейшей обработки.

## Быстрые ответы
- **Что означает “extract metadata”?** Это чтение свойств, таких как тип файла, количество страниц и размер, без открытия полного документа в памяти.  
- **Какая библиотека это делает?** GroupDocs.Redaction for .NET предоставляет нативный API для извлечения метаданных из потоков.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; для продакшна требуется коммерческая лицензия.  
- **Можно ли обрабатывать PDF размером более 1 ГБ?** Да — потоки позволяют работать с файлами до 2 ГБ без загрузки всего файла.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ и .NET 6+.

## Что такое извлечение метаданных из потоков?
Извлечение метаданных из потоков — это процесс чтения свойств документа напрямую из объекта `Stream`, избегая полной загрузки файла и тем самым экономя память и процессорное время. Эта техника идеальна для пакетной обработки или облачных сервисов, где ресурсы ограничены.

## Почему использовать GroupDocs.Redaction для извлечения метаданных?
GroupDocs.Redaction поддерживает **30+ форматов файлов** (включая PDF, DOCX, XLSX, PPTX и типы изображений) и может обрабатывать документы размером до **2 GB**, удерживая использование памяти ниже **50 MB**. Его API `Redactor` предоставляет один вызов для получения всей ключевой информации о документе, устраняя необходимость в нескольких парсерах.

## Предварительные требования

- **GroupDocs.Redaction for .NET** (latest version)  
- **.NET Framework** 4.5+ **or** **.NET Core/5+/6+**  
- Базовые знания C# и знакомство с вводом‑выводом файлов  
- Visual Studio 2019 или новее

## Как настроить GroupDocs.Redaction для .NET?
Чтобы начать использовать GroupDocs.Redaction, сначала нужно добавить библиотеку в ваш проект. Это можно сделать через .NET CLI, менеджер пакетов Visual Studio или UI NuGet. Выберите подходящий способ: CLI удобен для скриптовых сборок, а UI предоставляет графический способ просмотра версий и зависимостей.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Откройте NuGet Package Manager в Visual Studio.  
- Найдите **"GroupDocs.Redaction"** и установите последнюю версию.

### Шаги получения лицензии
1. **Free Trial:** Скачайте пробную лицензию, чтобы исследовать все функции без ограничений.  
2. **Temporary License:** Запросите временную лицензию на сайте [GroupDocs](https://purchase.groupdocs.com/temporary-license/) для расширенного тестирования.  
3. **Purchase:** Когда будете готовы к продакшну, приобретите коммерческую лицензию.  

Для получения дополнительной информации посетите [веб‑сайт GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Базовая инициализация и настройка
Класс `Redactor` является точкой входа для всех операций, включая извлечение метаданных.

`Redactor` — это основной класс, представляющий экземпляр документа и предоставляющий методы для редактирования, получения информации и работы с файлами. После установки вы можете создать объект `Redactor`, как показано ниже:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Теперь, когда библиотека готова, давайте перейдём к деталям реализации.

## Как извлечь метаданные из потока документа?
Загрузите документ как **read‑only stream**, инициализируйте `Redactor` и вызовите `GetDocumentInfo()`, чтобы получить метаданные одним шагом. Такой подход избегает загрузки всего файла в память, что критично для больших PDF или многосотстраничных офисных документов.

**Direct answer:** Откройте файл с помощью `File.OpenRead()`, передайте поток в `new Redactor(stream)`, затем вызовите `redactor.GetDocumentInfo()` — метод возвращает объект, содержащий тип файла, количество страниц и размер всего в три строки кода.

### Шаг 1: Подготовьте путь к исходному файлу
Сначала убедитесь, что исходный файл существует и папка вывода готова. Нижеуказанный вспомогательный метод проверяет каталог вывода и создаёт его при необходимости.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Почему?* Это гарантирует корректный путь для последующих операций с файлами и предотвращает `DirectoryNotFoundException`.

### Шаг 2: Откройте поток документа
Использование `File.OpenRead()` открывает файл как **read‑only stream**, что сохраняет низкое потребление памяти даже для гигабайтных файлов.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Почему?* Потоки позволяют обрабатывать данные «на лету», работая с частями файла, а не с целым документом.

### Шаг 3: Инициализируйте Redactor с потоком документа
`Redactor` — основной объект API, предоставляющий доступ к операциям уровня документа, включая извлечение метаданных.

`Redactor` представляет один документ, загруженный из потока, и раскрывает методы, такие как `GetDocumentInfo()`, для быстрого получения свойств.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Почему?* Создание `Redactor` с потоком связывает объект с файлом без полной его загрузки.

### Шаг 4: Получите метаданные документа
Вызов `GetDocumentInfo()` возвращает объект `DocumentInfo`, содержащий формат файла, количество страниц и размер файла.

`GetDocumentInfo()` извлекает основные свойства (формат, количество страниц, размер) одним вызовом, устраняя необходимость в отдельных парсерах.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Почему?* Этот шаг консолидирует все важные метаданные, упрощая их логирование, фильтрацию или маршрутизацию документов по характеристикам.

## Как подготовить каталог вывода для обработанных файлов?
Перед записью любых обработанных файлов убедитесь, что целевая папка существует и доступна для записи. Программно проверяя путь и создавая его при отсутствии, вы избегаете распространённых исключений времени выполнения, таких как `DirectoryNotFoundException` или ошибки прав доступа. Этот простой шаг также делает ваш код переносимым между различными средами, будь то локальная машина, сервер или контейнер.

**Direct answer:** Используйте `Directory.Exists()` для проверки наличия папки и `Directory.CreateDirectory()` для её создания, если она не существует — эта однострочная проверка гарантирует корректный путь перед любой операцией записи.

### Реализуйте вспомогательный метод
Метод ниже инкапсулирует логику проверки и создания, возвращая проверенный путь для дальнейшего использования.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Почему?* Централизация этой логики уменьшает дублирование и упрощает поддержку кода.

## Распространённые проблемы и решения
- **Permission errors:** Убедитесь, что приложение работает под учётной записью с правом записи в целевую папку.  
- **Invalid paths:** Проверьте разделители путей (`\\` в Windows, `/` в Linux/macOS), чтобы избежать `DirectoryNotFoundException`.  
- **Large file handling:** Своевременно освобождайте потоки (`using`), чтобы освободить дескрипторы ОС и предотвратить утечки.

## Практические применения
1. **Automated Document Ingestion:** Извлекайте метаданные при загрузке, затем сохраняйте их в базе данных для быстрого поиска и отчётности по соответствию.  
2. **Legal & Compliance Audits:** Получайте количество страниц и типы файлов, чтобы убедиться, что документы соответствуют нормативным требованиям перед архивированием.  
3. **Enterprise Content Management:** Используйте метаданные для автоматической категоризации файлов по папкам, улучшая организацию и скорость поиска.

## Соображения по производительности
- **Memory Management:** Всегда оборачивайте потоки в блоки `using`, чтобы они автоматически освобождались.  
- **Batch Processing:** Обрабатывайте документы партиями по 10‑20, чтобы сбалансировать пропускную способность и использование памяти, особенно на серверах с ограниченными ресурсами.  
- **Parallelism:** Используйте `Parallel.ForEach` для независимых файлов, но следите за нагрузкой CPU и I/O, чтобы избежать конкуренции.

## Заключение
Теперь у вас есть полное, готовое к продакшну руководство по **как извлечь метаданные** из потоков документов с помощью GroupDocs.Redaction для .NET. Следуя описанным шагам, вы сможете эффективно получать тип файла, количество страниц и размер, удерживая использование памяти на низком уровне и корректно обрабатывая большие файлы.

**Next Steps**
- Ознакомьтесь с полной ссылкой API в [documentation](https://docs.groupdocs.com/redaction/net/).  
- Углубитесь в [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/), чтобы изучить функции редактирования, водяных знаков и OCR.  
- Поэкспериментируйте с различными форматами файлов (PDF, DOCX, XLSX), чтобы увидеть, как меняются метаданные.  
- Интегрируйте извлечённые метаданные в существующую систему управления документами или поисковое решение.

## Часто задаваемые вопросы

**Q: Какой основной сценарий использования извлечения метаданных GroupDocs.Redaction?**  
A: Он обеспечивает быстрое, экономичное по памяти получение свойств документа для индексации, проверок соответствия и автоматической маршрутизации без открытия полного файла.

**Q: Можно ли извлечь метаданные из файлов, защищённых паролем?**  
A: Да, укажите пароль при создании объекта `Redactor`; API расшифрует поток внутренне.

**Q: Поддерживает ли библиотека форматы, отличные от PDF, такие как DOCX или XLSX?**  
A: Безусловно — GroupDocs.Redaction работает с более чем 30 форматами, включая PDF, DOCX, XLSX, PPTX и распространённые типы изображений.

**Q: Какой максимальный размер документа можно обработать с помощью потоков?**  
A: Потоки позволяют обрабатывать файлы до **2 GB**, удерживая потребление памяти ниже **50 MB**, благодаря чтению «на лету».

**Q: Где получить помощь в случае проблем?**  
A: Посетите [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) для поддержки сообщества или обратитесь к официальной документации для советов по устранению неполадок.

---

**Последнее обновление:** 2026-06-11  
**Тестировано с:** GroupDocs.Redaction 23.12 for .NET  
**Автор:** GroupDocs  

**Ресурсы**  
- **Documentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Связанные руководства

- [Мастерское извлечение метаданных документов с помощью GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [Как редактировать метаданные документов с помощью GroupDocs.Redaction для .NET — Полное руководство](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Безопасное редактирование документов в .NET с использованием потоков: Руководство по GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)