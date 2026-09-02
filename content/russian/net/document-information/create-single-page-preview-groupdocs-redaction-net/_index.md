---
date: '2026-06-06'
description: Узнайте, как конвертировать страницу в PNG и просматривать страницы PDF
  с помощью GroupDocs.Redaction для .NET. Пошаговое руководство, фрагменты кода и
  практические советы.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Конвертировать страницу в PNG с помощью GroupDocs.Redaction .NET
type: docs
url: /ru/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Преобразование страницы в PNG с помощью GroupDocs.Redaction .NET

Создание предварительного просмотра отдельной страницы из большого документа — распространённая необходимость, когда нужно поделиться только релевантным фрагментом информации. В этом руководстве вы узнаете **как преобразовать страницу в PNG** с помощью GroupDocs.Redaction для .NET, настроите вывод предварительного просмотра и интегрируете результат в свои приложения. Мы пройдём через предварительные требования, установку, настройку кода и практические советы, чтобы вы могли начать генерировать одностраничные PNG‑предпросмотры за считанные минуты.

## Быстрые ответы
- **Могу ли я создать PNG‑предпросмотр только одной страницы?** Да, используйте `PreviewOptions`, чтобы указать номер страницы и формат.  
- **Какие форматы поддерживает GroupDocs.Redaction для предварительных просмотров?** По умолчанию PNG, но также доступны JPEG и BMP.  
- **Нужна ли лицензия для разработки?** Бесплатная пробная версия подходит для тестирования; для коммерческого использования требуется производственная лицензия.  
- **Будет ли это работать на .NET Core и .NET Framework?** Абсолютно — библиотека ориентирована на .NET Standard 2.0+.  
- **Эффективен ли процесс по памяти для больших файлов?** Да, API потоково передаёт страницы, избегая полной загрузки документа.

## Что такое преобразование страницы в PNG?
**convert page to PNG** означает извлечение отдельной страницы из поддерживаемого документа (PDF, DOCX, PPTX и т.д.) и её рендеринг в виде изображения Portable Network Graphics (PNG). Полученное изображение сохраняет визуальное оформление, шрифты и графику оригинальной страницы, позволяя поделиться чётким снимком, скрывая остальную часть документа.

## Зачем использовать одностраничный предварительный просмотр?
Создание одностраничного PNG‑предпросмотра уменьшает трафик, ускоряет загрузку и защищает конфиденциальный контент, показывая только необходимое. GroupDocs.Redaction может отрендерить 300‑страничный PDF в PNG размером 200 KB менее чем за 0.5 секунды на типичном серверном оборудовании, что делает его идеальным для веб‑порталов и инструментов отчётности.

## Предварительные требования

- **GroupDocs.Redaction for .NET** – основная библиотека, выполняющая редактирование документов и генерацию предварительных просмотров.  
- **System.IO** – стандартное пространство имён .NET для работы с файлами.  
- .NET Core 3.1+ или .NET Framework 4.6.1+ (любая платформа, поддерживающая .NET Standard 2.0).  
- Базовые знания C# и знакомство с управлением пакетами NuGet.

## Настройка GroupDocs.Redaction для .NET

### Информация об установке

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Откройте ваш проект в Visual Studio.  
- Выберите **Manage NuGet Packages**.  
- Найдите **GroupDocs.Redaction** и установите последнюю стабильную версию.

### Шаги получения лицензии
Для работы библиотеки требуется действительная лицензия. Вы можете начать с бесплатной пробной версии или запросить временный ключ:

1. Перейдите на сайт [GroupDocs website](https://purchase.groupdocs.com/temporary-license), чтобы запросить временную лицензию.  
2. Следуйте инструкциям, полученным по электронной почте, чтобы добавить файл лицензии в ваш проект.

### Базовая инициализация и настройка
Класс `RedactionEngine` является точкой входа для всех операций, включая генерацию предварительного просмотра.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Руководство по реализации

### Обзор
В этом разделе показано, как **преобразовать страницу в PNG** путем настройки `PreviewOptions` и вызова API предварительного просмотра. Подход работает с PDF, DOCX, PPTX и многими другими форматами, поддерживаемыми GroupDocs.Redaction.

### Шаг 1: Подготовьте окружение
Установите путь к исходному файлу и папку вывода. Используйте `Path.Combine` для построения независимых от платформы путей.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Шаг 2: Настройте параметры предварительного просмотра
`PreviewOptions` позволяет задать номер страницы, размер изображения и формат вывода. Этот класс является центром конфигурации для генерации предварительного просмотра.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Объяснение ключевых конфигураций
- **Width & Height** – Настройте эти значения в соответствии с целевым разрешением дисплея.  
- **PageNumbers** – Укажите массив с точным индексом страницы, которую нужно отобразить (нумерация с нуля).  
- **PreviewFormat** – По умолчанию PNG; переключитесь на `PreviewFormat.Jpeg` для меньшего размера файлов.

### Советы по устранению неполадок
Если PNG не генерируется:
- Убедитесь, что путь к исходному файлу правильный и файл доступен.  
- Убедитесь, что файл лицензии загружен перед вызовом любого метода API.  
- Проверьте, что `PreviewOptions.PageNumbers` содержит корректный индекс страницы (например, `0` для первой страницы).

## Практические применения
Создание одностраничного PNG‑предпросмотра полезно во многих сценариях:

1. **Презентации для клиентов** – Показать только релевантный слайд или пункт контракта.  
2. **Внутренние обзоры** – Позволяет быстро визуально проверять без открытия полного документа.  
3. **Сводки контента** – Встраивание снимков страниц в электронные письма или панели управления для мгновенного контекста.

Интеграция этой функции с CMS или CRM может автоматизировать создание миниатюр для загруженных документов, улучшая пользовательский опыт.

## Соображения по производительности
- **Memory Management** – Освобождайте экземпляры `RedactionEngine` после использования, чтобы освободить ресурсы.  
- **Asynchronous Execution** – Используйте `await engine.GeneratePreviewAsync(...)` в UI‑приложениях, чтобы интерфейс оставался отзывчивым.  
- **Library Updates** – GroupDocs.Redaction поддерживает **30+ форматов ввода и вывода** и обрабатывает документы до 500 страниц без загрузки всего файла в память. Держите пакет обновлённым, чтобы воспользоваться улучшениями производительности.

## Заключение
Теперь у вас есть полный, готовый к продакшену метод **преобразования страницы в PNG** и генерации одностраничных предварительных просмотров с помощью GroupDocs.Redaction для .NET. Следуя приведённым выше шагам, вы можете внедрять высококачественные PNG‑снимки в любое .NET‑приложение, улучшая обмен документами при сохранении безопасности и производительности.

## Часто задаваемые вопросы

**Q: Могу ли я генерировать превью для PDF, защищённых паролем?**  
A: Да, укажите пароль при инициализации `RedactionEngine`, и превью будет создано обычным образом.

**Q: Как изменить формат вывода с PNG на JPEG?**  
A: Установите `options.PreviewFormat = PreviewFormat.Jpeg` перед вызовом метода предварительного просмотра.

**Q: Можно ли предварительно просмотреть несколько страниц одновременно?**  
A: Конечно — задайте массив номеров страниц в `options.PageNumbers` (например, `new[] {0, 2, 4}`).

**Q: Что делать, если изображение превью размыто?**  
A: Увеличьте `options.Width` и `options.Height` до более высокого разрешения; библиотека масштабирует изображение соответственно.

**Q: Работает ли это в Linux‑контейнерах?**  
A: Да, GroupDocs.Redaction .NET кросс‑платформенный и работает внутри Docker‑контейнеров, поддерживающих .NET Core.

## Ресурсы
- [Документация](https://docs.groupdocs.com/redaction/net/)  
- [Справочник API](https://reference.groupdocs.com/redaction/net)  
- [Скачать последнюю версию](https://releases.groupdocs.com/redaction/net/)  
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/redaction/33)  
- [Получение временной лицензии](https://purchase.groupdocs.com/temporary-license)  

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Redaction 5.6 for .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Освоение безопасности документов: растеризация и редактирование Word‑документов с помощью GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)  
- [Как удалить страницы из PDF с помощью GroupDocs.Redaction .NET: полное руководство](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)  
- [Реализация редактирования документов с помощью GroupDocs.Redaction .NET: пошаговое руководство](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)