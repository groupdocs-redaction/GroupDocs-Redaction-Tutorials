---
date: '2026-05-17'
description: Узнайте, как rasterize PDF в grayscale с помощью GroupDocs.Redaction
  для Java, применить фильтр grayscale и обеспечить безопасность и высокое качество
  ваших документов.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Как rasterize PDF в grayscale с GroupDocs.Redaction Java – Обеспечьте безопасность
  и оптимизируйте свои документы
type: docs
url: /ru/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Как растеризовать PDF в градациях серого с помощью GroupDocs.Redaction Java

Если вам нужно **растеризовать PDF** в градациях серого, сохранив при этом безопасность ваших документов, их профессиональный вид и простоту архивирования, вы попали по адресу. В этом руководстве мы подробно пройдем все шаги по преобразованию цветных DOCX, PDF или других поддерживаемых файлов в чистую, растеризованную версию в градациях серого с помощью GroupDocs.Redaction для Java. Вы поймете, почему растеризация добавляет уровень защиты, как настроить библиотеку и как эффективно управлять ресурсами — всё представлено в дружелюбном пошаговом стиле.

## Быстрые ответы
- **Что делает растеризация в градациях серого?** Она преобразует каждую страницу в изображение высокого разрешения, а затем применяет фильтр градаций серого, удаляя всю цветовую информацию.  
- **Зачем использовать GroupDocs.Redaction для этого?** Он объединяет безопасность редактирования с опциями растеризации в едином, простом в использовании API.  
- **Какие форматы поддерживаются?** DOCX, PDF, XLSX, PPTX, RTF и более 100 других форматов.  
- **Нужна ли лицензия?** Для продакшн‑использования требуется действующая лицензия GroupDocs.Redaction; бесплатная пробная версия доступна для тестирования.  
- **Какая версия Java требуется?** JDK 8 или выше.

## Как растеризовать PDF в градациях серого?

Загрузите исходный документ с помощью `new Redactor("path/to/file")`, включите растеризацию через `RasterizationOptions`, добавьте расширенную опцию градаций серого и вызовите `save()` — вся конверсия происходит в нескольких лаконичных строках. Такой подход гарантирует, что каждая страница превратится в PDF на основе изображений, черно‑белый, что предотвращает выделение текста и обеспечивает единообразный вид, готовый к печати.

## Что такое **create grayscale pdf**?

Создание PDF в градациях серого означает преобразование каждого визуального элемента оригинального документа в оттенки серого. В результате получается более небольшой, удобный для печати файл, который устраняет отвлекающие цветовые элементы и добавляет небольшой уровень защиты, поскольку содержимое теперь представлено в виде изображений.

## Зачем использовать растеризацию в градациях серого с GroupDocs.Redaction?

Растеризация превращает каждую страницу в изображение, что означает невозможность копировать или редактировать текст, а визуальный вывод остаётся одинаковым на разных принтерах и в просмотрщиках. GroupDocs.Redaction поддерживает **более 100 входных и выходных форматов** — включая DOCX, XLSX, PPTX, HTML и типы изображений — поэтому вы можете применять один и тот же рабочий процесс практически к любому документу.

## Предварительные требования

- Java Development Kit (JDK) 8 или новее. Проверьте с помощью `java -version`.  
- IDE (IntelliJ IDEA, Eclipse или NetBeans) для более удобного написания кода и отладки.  
- GroupDocs.Redaction для Java, добавленный через Maven или Gradle.  
- Пример документа (например, многостраничный DOCX), с которым можно безопасно экспериментировать.  
- Достаточно места на диске для растеризованного вывода (растровые файлы могут быть больше исходных).

## Импорт пакетов

Следующие импорты подключают основные классы Redactor и растеризации, необходимые для примера.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Шаг 1: Инициализация объекта Redactor

Класс `Redactor` является точкой входа для всех операций обработки документов в GroupDocs.Redaction. Создание экземпляра открывает возможность загрузки, редактирования и сохранения документов.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Замените `Constants.MULTIPAGE_SAMPLE_DOCX` на путь к файлу, который вы хотите преобразовать в PDF в градациях серого.

## Шаг 2: Настройка параметров сохранения

Класс `SaveOptions` определяет, как обработанный документ будет записан на диск, включая формат и имя файла.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Выходной файл будет назван `yourfile_scan.pdf` (или в формате, который вы укажете позже).

## Шаг 3: Включение растеризации

Объект `RasterizationOptions` включает рендеринг каждой страницы в виде изображения перед сохранением.

```java
so.getRasterization().setEnabled(true);
```

## Шаг 4: Применение преобразования в градации серого

`AdvancedRasterizationOptions.Grayscale` — это флаг, который заставляет растеризованное изображение использовать только оттенки серого.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Шаг 5: Выполнение трансформации документа

Вызов `save()` запускает полный конвейер обработки и записывает выходной файл.

```java
redactor.save(so);
```

После выполнения этой строки вы найдете новый файл на диске, полностью растеризованный, в градациях серого и сохранённый с суффиксом `_scan`.

## Шаг 6: Правильное управление ресурсами

Метод `close()` освобождает нативные ресурсы и удаляет временные файлы.

```java
finally { redactor.close(); }
```

Для современных версий Java вы также можете использовать шаблон try‑with‑resources, который автоматически закрывает `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Оба подхода безопасны; второй более лаконичен.

## Расширенные параметры конфигурации

### Регулировка DPI для качества или размера

Более высокий DPI дает более чёткие изображения (хорошо для печати), а более низкий DPI уменьшает размер файла. Обычный компромисс — 150 DPI для просмотра на экране и 300 DPI для PDF, готовых к печати.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Выбор формата вывода

Вы можете принудительно сохранить растеризованный результат в определённый контейнерный формат, например PDF, TIFF или PNG. PDF — самый распространённый формат архивирования.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Распространённые сценарии использования

- **Архивирование юридических документов** — создание неизменяемых PDF в градациях серого, которые нельзя редактировать.  
- **Отчёты, готовые к печати** — обеспечение одинакового черно‑белого вывода при массовой печати.  
- **Процессы соответствия** — комбинирование редактирования с растеризацией в градациях серого для соблюдения строгих правил защиты данных.

## Распространённые проблемы и решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Размер выходного файла больше ожидаемого | DPI установлен слишком высоким или отключено сжатие изображений | Уменьшите DPI (например, 150) или включите сжатие в `RasterizationOptions`. |
| Текст выглядит размытым | Недостаточный DPI для оригинального размера шрифта | Увеличьте DPI до 300 или выше. |
| Процесс бросает `OutOfMemoryError` при больших документах | Весь документ загружается в память | Используйте потоковые API или обрабатывайте страницы пакетами, если поддерживается. |
| Градации серого не применены | Расширенная опция не добавлена корректно | Убедитесь, что `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` вызывается перед `save()`. |

## Часто задаваемые вопросы

**Q: Могу ли я конвертировать документы в градации серого без растеризации?**  
A: В GroupDocs.Redaction опция градаций серого связана с растеризацией, что обеспечивает согласованные результаты и добавляет уровень защиты.

**Q: Какие форматы документов поддерживают растеризацию в градациях серого?**  
A: Все основные форматы, поддерживаемые GroupDocs.Redaction — включая DOCX, PDF, XLSX, PPTX, RTF и более 100 других — могут быть растеризованы и преобразованы в градации серого.

**Q: Влияет ли растеризация на размер файлов моих документов?**  
A: Да. Файлы, содержащие много текста, могут увеличиться, а файлы с большим количеством изображений — уменьшиться. Настройки DPI оказывают наибольшее влияние.

**Q: Можно ли отменить процесс растеризации в градациях серого?**  
A: Нет. Растеризация односторонняя; сохраняйте резервную копию оригинала, если понадобится откат.

**Q: Как оптимизировать качество растеризованных документов в градациях серого?**  
A: Используйте более высокий DPI (300 + для печатного качества) и выбирайте PDF в качестве формата вывода для наилучших архивных результатов.

## Заключение

Теперь у вас есть полный, готовый к продакшн рецепт для **растеризации PDF в градациях серого** с помощью GroupDocs.Redaction для Java. Включив растеризацию, добавив расширенную опцию градаций серого и ответственно управляя ресурсами, вы можете создавать безопасные, удобные для печати документы, соответствующие требованиям соответствия и одинаково выглядящие в любом просмотрщике.

---

**Последнее обновление:** 2026-05-17  
**Тестировано с:** GroupDocs.Redaction 23.11 for Java  
**Автор:** GroupDocs  

## ЦЕЛЕВЫЕ КЛЮЧЕВЫЕ СЛОВА:

**Основное ключевое слово (ВЫСШИЙ ПРИОРИТЕТ):**  
how to rasterize pdf

**Вторичные ключевые слова (ПОДДЕРЖИВАЮЩИЕ):**  
java pdf to image, apply grayscale filter pdf

## Связанные руководства

- [Руководства по параметрам растеризации для GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Как использовать groupdocs redaction для Java: Предварительная растеризация в Word‑документах](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Пользовательская шумовая растеризация в Java: Защита конфиденциальной информации с помощью GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)