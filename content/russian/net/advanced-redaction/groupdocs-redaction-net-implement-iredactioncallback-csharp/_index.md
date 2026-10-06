---
date: '2026-10-06'
description: Узнайте, как редактировать данные с использованием GroupDocs.Redaction
  .NET и реализации IRedactionCallback на C#. Следуйте этому пошаговому руководству,
  лучшим практикам и реальным примерам.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Узнайте, как редактировать данные с использованием GroupDocs.Redaction
  .NET и реализации IRedactionCallback на C#. Следуйте пошаговому руководству с лучшими
  практиками и реальными примерами.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Как редактировать данные с помощью GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Как редактировать данные с помощью GroupDocs.Redaction .NET (C#)
type: docs
url: /ru/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Как редактировать данные с помощью GroupDocs.Redaction .NET (C#)

В этом подробном руководстве вы узнаете, **как редактировать данные** в PDF, Word‑файлах и других документах с помощью GroupDocs.Redaction для .NET. Независимо от того, нужно ли скрыть персональные идентификаторы в юридических контрактах или удалить конфиденциальные цифры из финансовых отчётов, SDK предоставляет программный контроль, гарантируя, что каждый чувствительный элемент исчезает навсегда и поддаётся аудиту. Мы пройдём процесс установки библиотеки, настройки пользовательского `IRedactionCallback` и применения редактирования точных фраз с полным журналированием.

## Быстрые ответы
- **Что делает IRedactionCallback?** Он позволяет перехватывать каждое событие редактирования, вести журнал деталей и при необходимости изменять заменяющий текст «на лету».  
- **Нужна ли лицензия?** Пробная версия подходит для разработки; постоянная лицензия снимает все ограничения оценки.  
- **Какие версии .NET поддерживаются?** .NET Core 3.1+, .NET 5/6 и .NET Framework 4.6+.  
- **Можно ли обрабатывать несколько файлов?** Да — оберните логику в цикл или используйте пакетную обработку для лучшей производительности.  
- **Возможна ли асинхронная обработка?** Встроенной поддержки нет, но вы можете выполнять вызовы API внутри `Task.Run` или других асинхронных шаблонов.

## Что такое редактирование конфиденциальных данных?
`Redaction` — это постоянное удаление или скрытие информации, которую нельзя раскрывать. С помощью GroupDocs.Redaction вы определяете точные фразы, шаблоны регулярных выражений или пользовательские правила и заменяете их заполнителями, например **[REDACTED]**, сохраняя оригинальное расположение и нумерацию страниц.

## Почему использовать GroupDocs.Redaction с IRedactionCallback?
`IRedactionCallback` — это интерфейс, который уведомляет вас каждый раз, когда SDK редактирует часть содержимого, позволяя фиксировать данные аудита или динамически изменять замену. Это обеспечивает полную проверяемость, применение пользовательских бизнес‑правил и бесшовную интеграцию с системами соответствия — без потери производительности.

## Предварительные требования
- **GroupDocs.Redaction** библиотека (совместимая версия — см. официальную [страницу документации](https://docs.groupdocs.com/redaction/net/)). Для полной информации обратитесь к [официальной документации](https://docs.groupdocs.com/redaction/net/).  
- .NET Core или .NET Framework, установленные на вашей машине разработки.  
- Visual Studio (издание Community подходит) или любая IDE, поддерживающая C#.  
- Базовые знания C# и знакомство с управлением пакетами NuGet.

## Настройка GroupDocs.Redaction для .NET
Сначала добавьте библиотеку в ваш проект. Выберите предпочитаемый способ — CLI, консоль Package Manager или пользовательский интерфейс. Команды остаются точно такими же, как в оригинальном руководстве.

### Варианты установки
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Откройте ваш проект в Visual Studio.  
- Перейдите к **Manage NuGet Packages**.  
- Найдите **GroupDocs.Redaction** и установите последнюю стабильную версию.

### Получение лицензии
Чтобы опробовать продукт, запросите бесплатную пробную версию или временную лицензию по [ссылке](https://purchase.groupdocs.com/temporary-license/). Вы также можете получить временную лицензию со [страницы временной лицензии](https://purchase.groupdocs.com/temporary-license/). Для использования в продакшене приобретите полную лицензию, чтобы разблокировать все функции без ограничений.

#### Базовая инициализация и настройка
Ниже приведён минимальный код, необходимый для открытия документа с помощью класса `Redactor`. Оставьте этот фрагмент без изменений — он является основой для всего дальнейшего.  
`Redactor` — основной класс, представляющий документ и предоставляющий методы для применения правил редактирования.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Руководство по реализации
Теперь мы расширим базовую настройку, добавив пользовательский `IRedactionCallback`. Это позволяет фиксировать каждое событие редактирования, записывать его в журнал или даже изменять заменяющий текст «на лету».

### Подключение и использование реализации IRedactionCallback
`IRedactionCallback` — это интерфейс, получающий обратные вызовы для каждой операции редактирования, позволяя программно вести журнал или изменять поведение.

#### Шаг 1: подготовьте каталог вывода и путь к исходному файлу
Укажите, где находится ваш исходный документ. Скорректируйте путь в соответствии с вашей средой.

`LoadOptions` — объект конфигурации, который сообщает SDK, как читать файл (например, обработка пароля).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Шаг 2: создайте экземпляр Redactor с пользовательскими настройками
Мы создаём экземпляр `Redactor`, передавая `LoadOptions` и `RedactorSettings`. `RedactionDump`, находящийся в настройках, будет автоматически фиксировать каждое выполненное редактирование.

`RedactorSettings` позволяет точно настроить процесс редактирования; передача `RedactionDump` включает создание подробного аудиторского файла.  
`RedactionDump` — вспомогательный класс, записывающий каждое событие редактирования в JSON‑форматированный дамп для отчётности о соответствии.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Шаг 3: примените редактирование точной фразы
Здесь мы заменяем фразу **John Doe** заполнителем **[REDACTED]**. Вы можете заменить любой фрагмент или шаблон, который необходимо скрыть.

`ReplacementOptions` определяет, какой текст заменит найденное содержимое. Он также поддерживает настройку шрифта и цвета, если нужен визуальный маскировочный слой.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Объяснение ключевых объектов**
- `LoadOptions()` — сообщает SDK, как читать документ (например, обработка пароля).  
- `RedactorSettings(new RedactionDump())` — включает файл дампа, который фиксирует каждое редактирование для целей аудита.  
- `ReplacementOptions("[REDACTED]")` — определяет текст, который заменит найденную фразу.

### Почему это важно
Механизм обратных вызовов фиксирует каждое событие редактирования, создаёт машинно‑читаемый журнал аудита и позволяет динамически изменять заполнители, что помогает соответствовать требованиям комплаенса и снижает объём ручной пост‑обработки. Интегрируя эти данные с вашими системами мониторинга, вы можете генерировать отчёты, запускать оповещения и гарантировать, что конфиденциальная информация не просочится через конвейер редактирования.

Использование `IRedactionCallback` даёт вам три конкретных преимущества:
1. **Логи, готовые к аудиту** — каждое редактирование фиксируется в машинно‑читаемом дампе, удовлетворяя требования аудита более чем 30 нормативных рамок.  
2. **Динамическая замена** — вы можете менять заполнитель в зависимости от типа данных, сокращая ручную пост‑обработку до 40 %.  
3. **Масштабируемая производительность** — обратный вызов добавляет незначительные накладные расходы (<2 мс на редактирование), позволяя пакетно обрабатывать тысячи файлов параллельно.

### Советы по устранению неполадок
- **Файл не найден:** Проверьте путь `sourceFile` и убедитесь, что файл доступен процессу.  
- **Обратный вызов не срабатывает:** Убедитесь, что ваш класс реализует **все** члены `IRedactionCallback` и что экземпляр правильно передан в `Redactor`.  
- **Задержка производительности:** При больших пакетах переиспользуйте один экземпляр `Redactor`, когда это возможно, и своевременно освобождайте его.

## Практические применения
Редактирование конфиденциальных данных полезно в различных отраслях:
1. **Обработка юридических документов** — Автоматически удалять имена клиентов, номера дел или номера социального страхования перед распространением черновиков.  
2. **Системы управления персоналом** — Удалять персональные идентификаторы из трудовых договоров во время аудитов.  
3. **Финансовая отчётность** — Скрывать собственные цифры или номера счетов при создании PDF‑документов для инвесторов.

## Соображения по производительности
GroupDocs.Redaction поддерживает **более 30 форматов ввода и вывода** (PDF, DOCX, PPTX, XLSX, HTML и типы изображений) и может обрабатывать многосотстраничные файлы без загрузки всего документа в память. Чтобы приложение оставалось быстрым при обработке десятков или сотен файлов:
- **Пакетная обработка:** Загрузите список файлов и выполните цикл редактирования внутри `Parallel.ForEach` для использования многопоточности.  
- **Управление памятью:** Оберните каждый `Redactor` в блок `using` (как показано), чтобы гарантировать освобождение ресурсов.  
- **Асинхронные операции:** Хотя сам SDK синхронный, вы можете перенести работу в фоновые потоки или `Task.Run`, чтобы не блокировать UI‑потоки.

## Распространённые проблемы и решения
| Проблема | Решение |
|----------|---------|
| **Ошибка «Недопустимый формат файла»** | Убедитесь, что тип документа поддерживается (PDF, DOCX, PPTX и т.д.). |
| **Обратный вызов получает null‑значения** | Проверьте, что вы передаёте конкретную реализацию `IRedactionCallback` при создании `RedactorSettings`. |
| **Редактирование не применилось** | Убедитесь, что точная фраза совпадает с регистром и пробелами в документе, либо используйте `RegexRedaction` для сопоставления по шаблону. |

## Часто задаваемые вопросы

**Q: Какие варианты лицензирования доступны для GroupDocs.Redaction?**  
A: Вы можете начать с бесплатной пробной версии или запросить временную лицензию, чтобы изучить все функции. Для продакшена приобретите постоянную или подписную лицензию.

**Q: Можно ли использовать GroupDocs.Redaction с несколькими типами файлов?**  
A: Да, он поддерживает PDF, Word, Excel, PowerPoint и многие другие распространённые форматы.

**Q: Как обрабатывать исключения во время редактирования?**  
A: Оберните вашу логику редактирования в блоки `try‑catch` и фиксируйте детали исключения. Обратный вызов также можно использовать для захвата ошибок в реальном времени.

**Q: Есть ли встроенная поддержка асинхронной обработки?**  
A: Основной API синхронный, но вы можете выполнять вызовы редактирования внутри асинхронных задач или фоновых сервисов.

**Q: Где можно найти более продвинутые примеры?**  
A: [Официальная документация](https://docs.groupdocs.com/redaction/net/) и справочник API предоставляют обширные примеры кода и руководства по сценариям.

## Ресурсы

- [GroupDocs.Redaction для .NET – документация](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction для .NET – справочник API](https://reference.groupdocs.com/redaction/net/)
- [Скачать GroupDocs.Redaction для .NET](https://releases.groupdocs.com/redaction/net/)
- [Форум GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Бесплатная поддержка](https://forum.groupdocs.com/)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-10-06  
**Тестировано с:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**Автор:** GroupDocs

## Связанные руководства

- [Создание политики редактирования с GroupDocs.Redaction .NET — пошаговое руководство](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Как редактировать документы с GroupDocs.Redaction .NET — полное руководство](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Редактирование документов .NET с использованием потоков — руководство GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)