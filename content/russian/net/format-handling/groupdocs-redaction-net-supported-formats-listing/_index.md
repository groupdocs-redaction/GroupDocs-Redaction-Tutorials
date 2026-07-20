---
date: '2026-07-20'
description: Узнайте, как перечислять форматы с помощью GroupDocs.Redaction .NET,
  интегрировать эту функцию в ваш документооборот и повысить производительность.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Узнайте, как перечислять форматы с помощью GroupDocs.Redaction .NET,
  ознакомьтесь с пошаговым руководством и получите рекомендации по оптимальной производительности
  в ваших .NET‑приложениях.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Как перечислить форматы с помощью GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Как перечислить форматы с помощью GroupDocs.Redaction .NET
type: docs
url: /ru/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Как перечислить форматы с GroupDocs.Redaction .NET

Управление широким спектром типов документов — ежедневная реальность для разработчиков, создающих приложения, ориентированные на работу с документами. В этом руководстве вы узнаете **как перечислить форматы**, которые поддерживает GroupDocs.Redaction .NET, чтобы проверять файлы перед обработкой, предлагать пользователям точные варианты и поддерживать эффективность рабочего процесса.

## Введение

Эффективная работа с документами начинается с точного понимания, какие типы файлов поддерживает ваша библиотека. GroupDocs.Redaction предоставляет встроенный метод для получения этой информации, позволяя создавать динамические элементы UI, применять правила валидации и избегать ошибок выполнения. Ниже вы найдёте всё, что нужно для начала работы, от установки до практических фрагментов кода и советов по производительности.

### Быстрые ответы
- **Что означает “how to list formats”?** Это получение коллекции расширений файлов, которые GroupDocs.Redaction может обрабатывать.  
- **Нужна ли лицензия?** Да, для использования в продакшене требуется действующая лицензия GroupDocs.Redaction.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Сколько форматов доступно?** Более 30 входных и выходных форматов поддерживаются «из коробки».  
- **Требуется ли какая‑либо особая конфигурация?** Дополнительная настройка не требуется, достаточно стандартной инициализации библиотеки.

## Что такое “how to list formats”?

Это вызов API FileType библиотеки для получения коллекции, где каждая запись содержит расширение файла и человекочитаемое название. Разработчики могут перебрать эту коллекцию, чтобы построить правила валидации, заполнить выпадающие списки UI или вести журнал поддерживаемых типов, гарантируя обработку только совместимых документов.

## Почему перечислять форматы с GroupDocs.Redaction?

GroupDocs.Redaction поддерживает **30+** различных типов файлов — включая PDF, DOCX, PPTX и форматы изображений — что позволяет работать с большинством корпоративных документов без сторонних конвертеров. Программно перечисляя эти форматы, вы устраняете догадки, снижаете количество запросов в поддержку и гарантируете, что в ваш конвейер обработки попадут только совместимые файлы.

## Требования

- **GroupDocs.Redaction for .NET** – загрузите последнюю версию пакета с официального сайта.  
- **.NET Framework или .NET Core** – совместимы с вашей средой разработки.  
- **Visual Studio** (или любой IDE, поддерживающий C#).  
- Базовое знакомство с синтаксисом C#.

## Настройка GroupDocs.Redaction для .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### UI менеджер пакетов NuGet
- Найдите **“GroupDocs.Redaction”** и установите последнюю версию.

### Получение лицензии
GroupDocs предлагает бесплатную пробную версию, временную лицензию для оценки или полные варианты покупки. Посетите сайт GroupDocs, чтобы получить соответствующий файл лицензии.

### Базовая инициализация и настройка
После добавления пакета подключите пространство имён и создайте экземпляр `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Руководство по реализации

### Как перечислить форматы с GroupDocs.Redaction .NET?
Загрузите библиотеку, вызовите статический помощник и отсортируйте результаты — это даст готовую к использованию коллекцию всего в две строки кода. Используйте `FileType.GetSupportedFileFormats()` для получения `IEnumerable<FileType>`, включающего расширение и отображаемое имя каждого формата, затем упорядочьте по расширению для чистого списка UI.

### Получение поддерживаемых форматов файлов

#### Обзор
Цель — получить список типов файлов, которые GroupDocs.Redaction может обрабатывать, облегчая интеграцию в логику валидации, выпадающие списки UI или механизмы логирования.

#### Пошаговая реализация

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` возвращает каждый формат, который распознаёт библиотека. Метод является частью класса `GroupDocs.Redaction.FileType`, который инкапсулирует метаданные, такие как расширение файла и дружественное название.

**2. Display Supported File Types**  
Переберите коллекцию и выведите расширение и описание каждого формата. Пример встроенного кода:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Фрагмент выводит аккуратно упорядоченный список, например “.pdf – Portable Document Format”, что идеально подходит для заполнения элементов UI.

### Советы по устранению неполадок
- **Missing Package** – Проверьте ссылку на пакет NuGet и восстановите пакеты при необходимости.  
- **Incorrect License Path** – Убедитесь, что файл лицензии скопирован в каталог вывода или укажите абсолютный путь.  
- **Unsupported Extension** – Если формат не отображается в списке, проверьте, что используете последнюю версию библиотеки; новые релизы добавляют дополнительные форматы.

## Практические применения
Понимание поддерживаемых форматов открывает несколько реальных сценариев:

1. **Системы управления документами** – Проверяйте загрузки по поддерживаемому списку, чтобы предотвратить сбои обработки.  
2. **Безопасность контента** – Применяйте правила редактирования только к типам файлов, которые движок может безопасно модифицировать.  
3. **Конвейеры пакетной обработки** – Фильтруйте большие партии файлов перед вызовом редактирования, экономя CPU и память.

## Соображения по производительности
- **Memory Footprint** – Перечисление форматов — лёгкая операция; она не загружает документы в память.  
- **Batch Operations** – При обработке сотен файлов получайте список форматов один раз и переиспользуйте его, чтобы избежать лишних вызовов.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` потокобезопасен и может вызываться из параллельных задач без синхронизации.

## Заключение
Теперь у вас есть полный, готовый к продакшену подход **как перечислить форматы** с использованием GroupDocs.Redaction .NET. Интегрируя эту возможность, вы улучшаете валидацию, повышаете удобство для пользователей и делаете конвейеры работы с документами надёжнее.

### Следующие шаги
- Исследуйте API `Redactor` для применения правил редактирования в зависимости от типа файла.  
- Скомбинируйте список форматов с выпадающим списком на фронтенде для бесшовного выбора файлов.  
- Ознакомьтесь с руководством по производительности, чтобы оптимизировать крупномасштабные пакетные задания.

## Часто задаваемые вопросы

**Q: Можно ли получить список форматов без инициализации экземпляра Redactor?**  
A: Да, `FileType.GetSupportedFileFormats()` статичен и не требует объекта `Redactor`.

**Q: Включает ли список как входные, так и выходные форматы?**  
A: Метод возвращает все форматы, которые библиотека может как читать, так и записывать; каждый `FileType` содержит флаги `CanRead` и `CanWrite`.

**Q: Как часто обновляется список поддерживаемых форматов?**  
A: GroupDocs выпускает обновления форматов с каждой новой версией библиотеки; проверка списка во время выполнения гарантирует наличие актуального набора.

**Q: Есть ли способ отфильтровать только PDF‑совместимые форматы?**  
A: Да, отфильтруйте коллекцию, где `format.Extension == ".pdf"` или где `format.Name.Contains("PDF")`.

**Q: Будет ли этот подход работать на .NET Core 2.1?**  
A: Метод требует .NET Core 3.1 или новее; более ранние среды не поддерживаются.

## Раздел FAQ
1. **Как установить GroupDocs.Redaction для .NET?**  
   Используйте команду CLI `dotnet add package GroupDocs.Redaction` или установите через UI менеджер пакетов NuGet.  
2. **Какие типичные проблемы возникают при получении поддерживаемых форматов?**  
   Убедитесь, что все зависимости восстановлены и вы подключаете правильное пространство имён (`GroupDocs.Redaction`).  
3. **Можно ли использовать эту функцию в приложениях, не основанных на .NET?**  
   Это руководство ориентировано на .NET, но GroupDocs предоставляет аналогичные API для Java, Python и других платформ.  
4. **Как оптимизировать производительность при работе с GroupDocs.Redaction?**  
   Переиспользуйте список форматов, избегайте загрузки полных документов, если требуется лишь проверка совместимости, и контролируйте использование памяти при пакетных заданиях.  
5. **Какие типы файлов поддерживает GroupDocs.Redaction?**  
   Библиотека поддерживает более 30 форматов, включая PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG и многие другие. Используйте `FileType.GetSupportedFileFormats()` для просмотра полного списка.

## Ресурсы
- [Документация](https://docs.groupdocs.com/redaction/net/)
- [Справочник API](https://reference.groupdocs.com/redaction/net)
- [Скачать GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/redaction/33)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 4.2.0 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Связанные руководства

- [Руководства по работе с форматами для GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Руководства по загрузке документов с GroupDocs.Redaction для .NET](/redaction/net/document-loading/)
- [Руководства по сохранению документов для GroupDocs.Redaction .NET](/redaction/net/document-saving/)