---
date: '2026-02-16'
description: Узнайте, как использовать зависимость GroupDocs Maven для добавления
  суффикса к именам файлов при редактировании документов в Java. Включает загрузку
  из потока, удаление аннотаций и параметры сохранения.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: GroupDocs Maven зависимость – Добавить суффикс к имени файла в Java
type: docs
url: /ru/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Как добавить суффикс к имени файла при редактировании документов в Java с помощью GroupDocs.Redaction

Редактирование конфиденциальных данных — это только половина задачи: также необходимо убедиться, что сохранённый файл явно указывает, что он был обработан. **Использование зависимости groupdocs maven делает это простым**, позволяя добавить суффикс к имени выходного файла всего в несколько строк кода. В этом руководстве вы узнаете, как добавить суффикс к имени файла при сохранении отредактированного документа, а также как загружать, аннотировать и сохранять его с помощью GroupDocs.Redaction для Java. Защищая юридические контракты, медицинские записи или финансовые отчёты, эти шаги сделают ваш рабочий процесс безопасным и аудируемым.

## Быстрые ответы
- **Что делает «add suffix to filename»?**  
  Добавляет пользовательский суффикс (например, “_redacted”) к имени выходного файла, чтобы сразу определить обработанные файлы.  
- **Можно ли загрузить документ из потока?**  
  Да — GroupDocs.Redaction поддерживает загрузку из любого `InputStream`, что удобно для облачного хранилища или обработки в памяти.  
- **Нужна ли лицензия для этой функции?**  
  Бесплатная пробная версия работает для базового редактирования; временная или полная лицензия открывает все расширенные опции, включая работу с суффиксом.  
- **Какие форматы поддерживаются?**  
  Библиотека обрабатывает DOCX, PDF, PPTX, XLSX и многие другие.  
- **Требуется ли растеризация для вывода PDF?**  
  Растеризация необязательна; включайте её, когда необходимо «сплющить» документ для дополнительной защиты.

## Что такое добавление суффикса к имени файла?
Добавление суффикса — это простая конвенция именования, сигнализирующая о том, что файл прошёл редактирование. Это предотвращает случайное распространение оригинальных, неотредактированных версий и помогает автоматическим конвейерам отслеживать статус обработки.

## Почему использовать GroupDocs.Redaction для этой задачи?
GroupDocs.Redaction предоставляет удобный Java API, позволяющий сочетать действия редактирования с параметрами работы с файлами — например, **добавлением суффикса к имени файла** — всего в несколько строк кода. Это экономит время разработки и снижает риск ручных ошибок.

## Предварительные требования

- **Java Development Kit (JDK):** версия 8 или выше.  
- **GroupDocs.Redaction Library:** основная библиотека для задач редактирования.  
- **IDE:** IntelliJ IDEA, Eclipse или любой совместимый с Java редактор.  
- **Maven:** для управления зависимостями.  

### Требования к знаниям
Знакомство с Java I/O и базовыми объектно‑ориентированными концепциями упростит понимание примеров.

## Настройка GroupDocs.Redaction для Java
### Maven Setup
Добавьте следующую конфигурацию в ваш файл `pom.xml`, чтобы получить доступ к библиотекам GroupDocs через Maven:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Прямая загрузка
Либо скачайте последнюю версию напрямую с [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Получение лицензии
1. **Free Trial:** Доступ к базовому функционалу без ограничений.  
2. **Temporary License:** Получите временную лицензию для изучения расширенных возможностей.  
3. **Purchase:** Для длительного использования рассмотрите покупку полной лицензии.

#### Базовая инициализация и настройка
Инициализируйте проект, добавив необходимые импорты:

```java
import com.groupdocs.redaction.Redactor;
```

С этой настройкой вы готовы реализовать функции редактирования документов.

## Руководство по реализации

### Функция 1: Загрузка документа из потока
**Обзор:** Узнайте, как загружать документы в `InputStream` для последующей обработки.

#### Пошаговая реализация
##### Шаг 1.1: Создание InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Почему:** Использование `InputStream` позволяет работать с документами, хранящимися в разных форматах, что особенно важно, когда нужно **load document from stream** в облаке или микросервисных сценариях.

### Функция 2: Применение редактирования удаления аннотаций
**Обзор:** Удалите аннотации из документа с помощью `DeleteAnnotationRedaction`.

#### Пошаговая реализация
##### Шаг 2.1: Применить DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Почему:** Этот шаг гарантирует удаление всех чувствительных аннотаций, повышая конфиденциальность документа.

### Функция 3: Сохранение документа с параметрами
**Обзор:** Узнайте, как сохранять обработанный документ с конкретными параметрами, такими как растеризация и **добавление суффикса к имени файла**.

#### Пошаговая реализация
##### Шаг 3.1: Настройка SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Почему:** Настройка параметров сохранения позволяет гибко выбирать форматы вывода и схемы именования. Включение `setAddSuffix(true)` **adds suffix to filename**, делая очевидным, что файл отредактирован.

## Обзор groupdocs maven dependency
**groupdocs maven dependency** добавляет весь Redaction SDK в ваш проект одной записью `<dependency>`. Она обрабатывает транзитивные зависимости, поддерживает актуальность библиотек и упрощает автоматизацию сборки. Объявив зависимость в `pom.xml`, вы избавляетесь от ручного управления JAR‑файлами и гарантируете совместимость с последними патчами безопасности.

## Почему добавление суффикса важно
- **Auditability:** Команды сразу видят, какие файлы безопасно распространять.  
- **Automation:** Скрипты могут фильтровать файлы по суффиксу, предотвращая случайную обработку оригиналов.  
- **Compliance:** Многие нормативы требуют чёткой маркировки очищенных документов.  

## Практические применения
Рассмотрите реальные сценарии:
1. **Legal Document Redaction:** Защита контрактов перед отправкой клиенту.  
2. **Medical Record Handling:** Защита идентификаторов пациентов.  
3. **Financial Reporting:** Сохранение конфиденциальности финансовых цифр.  
4. **CRM Integration:** Автоматическое редактирование данных клиентов перед экспортом.  
5. **Collaboration Tools:** Гарантия, что общие черновики не раскрывают скрытые комментарии.

## Соображения по производительности
### Оптимизация производительности
- Используйте потоковую загрузку (`load document from stream`), чтобы не загружать весь файл в память.  
- Закрывайте экземпляры `Redactor` сразу после использования, освобождая ресурсы.

### Руководство по использованию ресурсов
- Следите за загрузкой CPU и памяти во время пакетных запусков.  
- Предпочитайте `ByteArrayOutputStream` для сохранения в памяти при работе с небольшими файлами.

### Лучшие практики управления памятью в Java
- Переиспользуйте объекты `Redactor` при обработке нескольких файлов одного типа.  
- Вызывайте `close()` в блоке `try‑with‑resources`, чтобы избежать утечек.

## Распространённые проблемы и решения
| Проблема | Причина | Решение |
|----------|----------|----------|
| **Suffix not appearing** | `setAddSuffix(false)` или отсутствие вызова | Убедитесь, что `options.setAddSuffix(true)` установлен перед `save()`. |
| **OutOfMemoryError on large DOCX** | Загрузка всего файла в память | Перейдите на загрузку через `InputStream` (см. Функцию 1). |
| **Annotations still visible** | Редактирование не выполнено до сохранения | Вызовите `redactor.apply(new DeleteAnnotationRedaction())` перед `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` или пропущен | Установите `options.setRasterizeToPDF(true)`, если нужен «плоский» PDF. |

## Часто задаваемые вопросы

**Q: Можно ли редактировать PDF‑документы с помощью GroupDocs.Redaction?**  
A: Да, библиотека поддерживает PDF, DOCX, PPTX, XLSX и многие другие форматы.

**Q: Как лучше всего обрабатывать большие файлы с GroupDocs.Redaction?**  
A: Используйте потоковую загрузку (`load document from stream`) и своевременно закрывайте ресурсы, чтобы снизить потребление памяти.

**Q: Можно ли настроить текст суффикса?**  
A: API автоматически добавляет стандартный суффикс (например, “_redacted”). Для пользовательского суффикса вы можете переименовать выходной файл после сохранения.

**Q: Как получить временную лицензию для GroupDocs.Redaction?**  
A: Перейдите на страницу [Temporary License page](https://purchase.groupdocs.com/temporary-license/) и следуйте инструкциям.

**Q: Где получить помощь при возникновении проблем?**  
A: Присоединяйтесь к [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) для получения экспертной поддержки.

## Ресурсы
- **Documentation:** Подробные руководства доступны на [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Полный справочник API находится на [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Последнюю версию можно скачать с [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Внести вклад или изучить исходный код можно в репозитории [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

---