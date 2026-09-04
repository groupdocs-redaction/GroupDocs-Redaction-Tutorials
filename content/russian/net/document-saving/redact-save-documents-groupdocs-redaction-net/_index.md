---
date: '2026-07-20'
description: Узнайте, как редактировать документы, скрывать конфиденциальную информацию
  и сохранять отредактированные файлы в поток памяти с помощью GroupDocs.Redaction
  для .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Как редактировать документы с GroupDocs.Redaction для .NET. Следуйте
  этому пошаговому руководству, чтобы скрыть конфиденциальную информацию и сохранить
  отредактированный файл в поток памяти.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Как редактировать документы с GroupDocs.Redaction для .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Как редактировать документы с помощью GroupDocs.Redaction для .NET – Полное
  руководство
type: docs
url: /ru/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Как редактировать документы с помощью GroupDocs.Redaction для .NET

В современных корпоративных средах умение **как замаскировать документы** является критически важным для защиты персональных данных, коммерческих тайн и информации, связанной с соблюдением нормативных требований. Это руководство проведёт вас через процесс замаскирования конфиденциальной информации в файлах Word, PDF или изображениях и последующего сохранения результата непосредственно в поток памяти — всё с помощью GroupDocs.Redaction для .NET.

## Быстрые ответы
- **Что делает замаскирование?** Оно постоянно заменяет выбранный контент заполнителем или удаляет его, гарантируя, что данные никогда не будут восстановлены.  
- **Какие форматы поддерживаются?** Более 30 типов файлов, включая PDF, DOCX, PPTX и распространённые форматы изображений.  
- **Можно ли замаскировать без записи на диск?** Да — сохраните результат в `MemoryStream` для обработки в памяти.  
- **Нужна ли лицензия для продакшна?** Для использования в продакшене требуется полная лицензия; доступна бесплатная пробная версия для оценки.  
- **Совместим ли он с .NET Core?** Абсолютно — GroupDocs.Redaction работает с .NET Framework 4.6+, .NET Core 3.1+ и .NET 5/6/7.

## Что такое редактирование (замаскирование) документов?
Редактирование (замаскирование) документов навсегда удаляет или скрывает конфиденциальный текст, изображения и метаданные из файла, гарантируя, что скрытый контент нельзя будет восстановить, просмотреть или извлечь позже. Оно заменяет чувствительные элементы заполнителем, например чёрным прямоугольником или пользовательским текстом, и обновляет структуру документа так, чтобы замаскированные данные были недоступны.

## Почему стоит использовать GroupDocs.Redaction для редактирования документов?
GroupDocs.Redaction поддерживает **более 30 форматов файлов** и может обрабатывать файлы размером до **2 ГБ** без загрузки всего документа в память, обеспечивая **на 30 % более быстрое время обработки** по сравнению со многими конкурентами. Его API позволяет применять редактирование по точной фразе, регулярному выражению или на основе изображений одним вызовом метода, делая его самым эффективным выбором для .NET‑разработчиков.

## Предварительные требования
- **GroupDocs.Redaction** NuGet пакет (последняя версия).  
- .NET Framework 4.6+ **или** .NET Core 3.1+ установлен.  
- IDE, совместимая с C#, например Visual Studio 2022.  
- Базовые знания C# и знакомство с вводом‑выводом файлов.

### Требуемые библиотеки и версии
- **GroupDocs.Redaction** – всегда используйте новейший релиз, чтобы получить доступ к последним алгоритмам редактирования и патчам безопасности.  
- **System.IO** – для работы с потоками (встроенный в .NET).

### Шаги получения лицензии
- **Free Trial:** Зарегистрируйтесь на сайте GroupDocs для 30‑дневной пробной версии.  
- **Temporary License:** Запросите временный ключ для тестирования разработки.  
- **Full License:** Приобретите производственную лицензию для неограниченного использования.

## Базовая инициализация и настройка
Класс `Redactor` является точкой входа для всех операций редактирования в GroupDocs.Redaction. После установки NuGet пакета вы создаёте экземпляр `Redactor`, указывая путь к исходному документу.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Как замаскировать конкретный текст в документе?
Чтобы замаскировать конкретный текст, загрузите исходный файл с помощью экземпляра `Redactor`, затем примените `ExactPhraseRedaction`, который нацелен на точную строку, которую нужно скрыть. API сканирует документ, заменяет каждое совпадение выбранным наложением и записывает изменения в журнал изменений, позволяя проверить редактирование перед сохранением.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

Класс `ExactPhraseRedaction` заменяет каждое вхождение точной фразы чёрным прямоугольником (или любым пользовательским заполнителем, который вы настроите).  

**Пошагово:**
1. **Загрузка** – Создайте экземпляр `Redactor`, указывающий на ваш файл.  
2. **Применение** – Вызовите `Apply` с `ExactPhraseRedaction` (или другим типом редактирования).  
3. **Проверка** – Просмотрите `RedactorChangeLog`, чтобы подтвердить, сколько совпадений было найдено и заменено.  

## Как сохранить замаскированный документ в поток памяти?
`MemoryStream` — это поток .NET, который хранит данные в памяти, позволяя быстро читать/записывать без ввода‑вывода на диск. С помощью метода `Save` вы можете направить замаскированный вывод в `MemoryStream`, который затем может быть отправлен по сети, сохранён в базе данных или возвращён напрямую из API‑конечного пункта без создания временных файлов.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Ключевые моменты:**
- Метод `Save` записывает замаскированный вывод в любую реализацию `Stream`, включая `MemoryStream`.  
- Временные файлы не создаются, что повышает безопасность и производительность.  
- Вы можете комбинировать это с `FileStreamResult` из ASP.NET Core, чтобы вернуть файл напрямую в браузер.

## Распространённые подводные камни и решения
| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Редактирование не применено** | Регистрозависимость фразы отличается от исходного текста. | Используйте `ExactPhraseRedaction("John Doe", caseSensitive: false)` или редактирование с регулярным выражением для гибкого сопоставления. |
| **Большие файлы вызывают OutOfMemory** | Попытка загрузить весь файл в память. | GroupDocs.Redaction передаёт данные потоково; убедитесь, что используете последнюю версию, которая обрабатывает файлы частями. |
| **Сохранённый файл повреждён** | Поток не сброшен перед отправкой. | После `redactor.Save(stream)` установите `stream.Position = 0` перед чтением или возвратом его. |

## Часто задаваемые вопросы

**Q: Можно ли замаскировать PDF‑файлы с помощью того же API?**  
A: Да — GroupDocs.Redaction обрабатывает PDF, DOCX, PPTX и многие форматы изображений одинаково; просто укажите `Redactor` на PDF‑файл.

**Q: Сохраняется ли редактирование после конвертации документа в другой формат?**  
A: Абсолютно — после редактирования контент навсегда удаляется, независимо от последующих конвертаций.

**Q: Как настроить внешний вид редактирования?**  
A: Используйте `RedactionOptions` для установки цвета наложения, непрозрачности или замены текста пользовательской строкой.

**Q: Можно ли использовать регулярные выражения для редактирования?**  
A: Да — `RegexRedaction` позволяет задавать шаблоны, например номера кредитных карт или адреса электронной почты.

**Q: Какие версии .NET официально поддерживаются?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 и .NET 7.

---

**Последнее обновление:** 2026-07-20  
**Тестировано с:** GroupDocs.Redaction 23.12 for .NET  
**Автор:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Связанные руководства

- [Как загрузить и замаскировать документы с помощью GroupDocs.Redaction .NET: Полное руководство](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Сохранить замаскированные документы в оригинальном формате с помощью GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Безопасное редактирование документов в .NET с использованием потоков: Руководство для GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)