---
date: 2026-06-06
description: Узнайте, как извлекать метаданные документа, получать количество страниц
  и создавать предварительные просмотры с помощью GroupDocs.Redaction для .NET – пошаговые
  учебники на C#.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Извлечение метаданных документа – учебники GroupDocs.Redaction .NET
type: docs
url: /ru/net/document-information/
weight: 15
---

# Учебные материалы по информации о документах для GroupDocs.Redaction .NET

В этом центре вы узнаете, как **извлекать метаданные документа** из широкого спектра типов файлов, определять количество страниц и создавать изображения предварительного просмотра перед выполнением операций редактирования. Программно получая эту информацию, вы можете решить, какие файлы требуют особой обработки, обеспечить соблюдение правил соответствия и улучшить общую производительность обработки. Все примеры написаны на C# и ориентированы на .NET 6+, так что их можно сразу добавить в существующие проекты.

## Быстрые ответы
- **Как извлечь метаданные?** Используйте `RedactionEngine.GetDocumentInfo()` для получения свойств, таких как автор, дата создания и количество страниц.  
- **Можно ли читать метаданные из потока?** Да — передайте `MemoryStream`, содержащий файл, в тот же метод API.  
- **Какие форматы поддерживаются?** Более 100 форматов, включая PDF, DOCX, PPTX и файлы изображений.  
- **Быстро ли получение количества страниц?** Движок читает только заголовок файла, предоставляя количество страниц менее чем за 50 мс для большинства документов.  
- **Нужна ли лицензия для разработки?** Временная лицензия подходит для тестирования; полная лицензия требуется для продакшн.

## Что такое «извлечение метаданных документа»?
**Извлечение метаданных документа** означает программное получение встроенных свойств — таких как автор, заголовок, дата создания и количество страниц — из файла без его открытия в просмотрщике. Эта легковесная операция позволяет вашему приложению принимать обоснованные решения до начала редактирования.

## Почему извлекать метаданные документа с помощью GroupDocs.Redaction?
GroupDocs.Redaction может читать метаданные более чем **100** форматов файлов, при этом потребление памяти не превышает 10 МБ для документов до 500 страниц. API возвращает полностью типизированный объект `DocumentInfo`, устраняя необходимость в пользовательских парсерах и сокращая время разработки до 70 %.

## Требования
- .NET 6+ (или .NET Core 3.1 / .NET Framework 4.7.2)  
- Установлен пакет NuGet GroupDocs.Redaction for .NET  
- Временный или полный лицензионный ключ (доступен в портале GroupDocs)

## Как извлечь метаданные документа с помощью GroupDocs.Redaction .NET?
`RedactionEngine` — основной компонент, который загружает документы и предоставляет методы извлечения метаданных. `GetDocumentInfo()` возвращает объект `DocumentInfo`, содержащий метаданные, такие как автор, заголовок и количество страниц. Загрузите файл (или поток) с помощью `RedactionEngine`, вызовите `GetDocumentInfo()` и прочитайте возвращённые свойства. Операция завершается одной строкой кода и не требует загрузки всего документа в память.

### Как получить количество страниц из документа?
`DocumentInfo` — типизированный объект, который хранит извлечённые метаданные документа. Свойство `DocumentInfo.PageCount` возвращает общее количество страниц. Это значение вычисляется из заголовка файла, позволяя движку определить количество страниц без полной загрузки документа, поэтому даже PDF‑документ из 300 страниц обрабатывается за несколько миллисекунд.

### Как прочитать метаданные из потока?
`RedactionEngine` загружает документ из пути к файлу или из потока и предоставляет возможности извлечения метаданных. Передайте экземпляр `Stream` (например, `MemoryStream`) в `RedactionEngine` вместо пути к файлу. Движок читает заголовок потока, извлекает метаданные и затем автоматически освобождает поток, обеспечивая минимальное потребление памяти и быструю обработку даже больших файлов.

### Как извлечь метаданные на C#?
Используйте следующий шаблон:
1. Создайте экземпляр `RedactionEngine`, указав путь к файлу или поток.  
2. Вызовите `GetDocumentInfo()`.  
3. Обратитесь к свойствам, таким как `Author`, `Title`, `CreatedDate` и `PageCount`.  

Эти шаги дают вам полную снимок метаданных, готовый к использованию в бизнес‑логике.

## Распространённые проблемы и решения
- **Метаданные пусты** – Убедитесь, что исходный файл действительно содержит встроенные свойства; некоторые сканы удаляют метаданные.  
- **Ошибка неподдерживаемого формата** – Проверьте, что расширение файла указано в таблице поддерживаемых форматов GroupDocs.Redaction (более 100 записей).  
- **Снижение производительности на больших файлах** – Используйте флаг `LoadOptions` `ReadOnly = true`, чтобы избежать ненужного выделения ресурсов.

## Часто задаваемые вопросы

**Q: Могу ли я извлечь метаданные из PDF, защищённых паролем?**  
A: Да. Укажите пароль при создании `RedactionEngine`; API расшифрует заголовок и вернёт метаданные.

**Q: Поддерживает ли API пакетную обработку нескольких файлов?**  
A: Абсолютно. Пройдитесь по коллекции файлов, создайте `RedactionEngine` для каждого и вызовите `GetDocumentInfo()` — движок достаточно лёгок, чтобы обрабатывать тысячи файлов.

**Q: Что происходит, если у документа нет метаданных?**  
A: Соответствующие свойства возвращают `null` или значения по умолчанию; вы можете безопасно проверять их на `null` перед использованием.

**Q: Можно ли изменить метаданные после их извлечения?**  
A: GroupDocs.Redaction ориентирован на редактирование, а не на изменение метаданных. Для сценариев записи используйте GroupDocs.Metadata или другую библиотеку.

**Q: Какие версии .NET официально поддерживаются?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+ и .NET 6+ полностью поддерживаются.

## Заключение
Освоив техники **извлечения метаданных документа**, вы даёте своим приложениям возможность принимать более умные решения по редактированию, обеспечивать соблюдение политик соответствия и повышать общую скорость обработки. Изучите ссылки на учебные материалы ниже, чтобы увидеть конкретные реализации для предварительного просмотра одностраничных документов, извлечения из потоков и полного получения метаданных.

## Доступные учебные материалы

### [Создать предварительный просмотр одностраничного документа с помощью GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Узнайте, как создавать предварительные просмотры одностраничных документов с помощью GroupDocs.Redaction для .NET. Это руководство предлагает пошаговые инструкции, советы по настройке и практические примеры.

### [Как извлечь метаданные документа из потоков с помощью GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Узнайте, как эффективно извлекать метаданные документа с помощью GroupDocs.Redaction для .NET. Руководство охватывает настройку, примеры кода и практические применения.

### [Освоить получение метаданных документа с помощью GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
Узнайте, как эффективно получать метаданные документа с помощью GroupDocs.Redaction .NET. Улучшите управление документами и процессы соответствия.

## Дополнительные ресурсы

- [Документация GroupDocs.Redaction для .NET](https://docs.groupdocs.com/redaction/net/)
- [Справочник API GroupDocs.Redaction для .NET](https://reference.groupdocs.com/redaction/net/)
- [Скачать GroupDocs.Redaction для .NET](https://releases.groupdocs.com/redaction/net/)
- [Форум GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Бесплатная поддержка](https://forum.groupdocs.com/)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-06-06  
**Тестировано с:** GroupDocs.Redaction 4.0 for .NET  
**Автор:** GroupDocs

## Связанные учебные материалы

- [Учебные материалы по загрузке документов с GroupDocs.Redaction для .NET](/redaction/net/document-loading/)
- [Как редактировать метаданные документа с помощью GroupDocs.Redaction для .NET — Полное руководство](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Создать предварительный просмотр одностраничного документа с помощью GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)