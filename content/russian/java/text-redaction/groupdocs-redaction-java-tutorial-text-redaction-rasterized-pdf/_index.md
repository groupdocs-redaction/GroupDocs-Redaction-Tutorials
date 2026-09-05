---
date: '2026-08-20'
description: Узнайте, как замаскировать текст с помощью GroupDocs.Redaction Java,
  сохранить как растровый PDF, заменить точные фразы и применить пользовательские
  настройки PDF.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Как замаскировать текст с помощью GroupDocs.Redaction Java. Это руководство
  покажет вам замену точных фраз, создание растрового PDF и соответствие стандарту
  PDF/A‑1a за несколько шагов.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Как замаскировать текст с библиотекой GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Как замаскировать текст с помощью GroupDocs.Redaction Java
type: docs
url: /ru/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Как редактировать текст с помощью GroupDocs.Redaction Java

В современных приложениях **как редактировать текст** в документе, сохраняя быстрый и соответствующий требованиям рабочий процесс, является частой задачей для разработчиков, аудиторов и специалистов по соблюдению нормативов. Этот учебник покажет, как использовать GroupDocs.Redaction для Java, чтобы находить точные фразы, заменять их безопасными наложениями и в конце экспортировать результат как растровый документ PDF/A‑1a — идеально подходящий для архивного или юридического распространения.

## Быстрые ответы
- **Какой основной класс для редактирования?** `Redactor`  
- **Могу ли я заменить фразу цветным наложением?** Yes, using `ExactPhraseRedaction` and `ReplacementOptions`.  
- **Как создать растровый PDF?** Enable rasterization via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Какой уровень соответствия PDF используется в примере?** `PdfComplianceLevel.PdfA1a`.  
- **Нужна ли лицензия для использования в продакшене?** A valid GroupDocs.Redaction license is required for production deployments.

## Что такое «как редактировать текст» в Java?
`Redaction` — это постоянное удаление или скрытие конфиденциального содержимого из файла, так чтобы его нельзя было восстановить или прочитать позже. С помощью GroupDocs.Redaction вы программно ищете точную фразу — например, номер социального страхования или конфиденциальный код проекта — и заменяете её красным наложением, чёрным блоком или любым пользовательским визуальным элементом, гарантируя, что исходные данные невозможно восстановить.

## Почему использовать GroupDocs.Redaction для Java?
GroupDocs.Redaction поддерживает **более 30 форматов ввода и вывода** (PDF, DOCX, PPTX, XLSX, HTML и типы изображений) и может обрабатывать документы из сотен страниц без загрузки всего файла в память. Его алгоритм точного совпадения фраз снижает количество ложных срабатываний более чем на 95 % по сравнению с обычным поиском по ключевым словам, а встроенный движок растеризации позволяет создавать файлы PDF/A‑1a, полностью основанные на изображениях, для долгосрочного хранения.

## Требования
Before you start, ensure you have:

- **GroupDocs.Redaction for Java** (v24.9 or newer).  
- **Java Development Kit (JDK) 8+**.  
- IDE, например IntelliJ IDEA, Eclipse или NetBeans.  
- Maven для управления зависимостями.  

### Требуемые библиотеки и зависимости
- GroupDocs.Redaction for Java – добавьте репозиторий и зависимость в ваш `pom.xml` (см. раздел настройки Maven).  
- Опционально: любой предпочитаемый вами фреймворк логирования (SLF4J, Log4j и т.д.).

### Требования к знаниям
- Базовый синтаксис Java и работа с файловым вводом/выводом.  
- Знакомство со структурой `pom.xml` Maven.

## Настройка GroupDocs.Redaction для Java
### Настройка Maven
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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

### Прямое скачивание
В качестве альтернативы вы можете скачать последнюю версию напрямую с [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Приобретение лицензии
- **Free trial** – исследуйте API без лицензионного ключа.  
- **Temporary license** – используйте для расширенной оценки.  
- **Full license** – требуется для производственных сред.

### Базовая инициализация и настройка
Класс `Redactor` является точкой входа для всех операций редактирования. Он загружает документ, применяет правила редактирования и сохраняет результат.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Как редактировать текст — пример точной фразы
Redactor — основной класс, который загружает документ и применяет правила редактирования. ExactPhraseRedaction определяет правило, которое сопоставляет конкретную строку. Этот пример демонстрирует загрузку файла, создание правила ExactPhraseRedaction и выполнение редактирования в один шаг, предоставляя разработчикам лаконичный рабочий процесс, при этом гарантируя постоянное скрытие оригинального содержимого.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Как сохранить как растровый PDF
SaveOptions — объект конфигурации, который управляет способом сохранения документа. Включив его функцию растеризации и выбрав соответствие PDF/A‑1a, вы можете создать PDF, состоящий только из изображений, где каждая страница рендерится как bitmap, соответствующий архивным стандартам и предотвращающий извлечение текста.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Практические применения
1. **Редактирование конфиденциальных данных** – автоматически скрывать персональные идентификаторы перед обменом контрактами.  
2. **Архивирование документов** – преобразовать окончательные отчёты в растровый PDF/A для долгосрочного соответствия.  
3. **Массовое обновление содержимого** – заменить устаревшую терминологию в сотнях файлов с помощью единого скрипта.

## Соображения по производительности
- **Close the `Redactor`** после каждой операции, чтобы освободить файловые дескрипторы и память.  
- **Batch processing** – загрузите список файлов и пройдитесь по нему в цикле, при возможности переиспользуя один экземпляр `Redactor`.  
- **Monitor resources** – используйте инструменты профилирования Java для наблюдения за загрузкой CPU и использованием кучи при масштабных редактированиях.

## Часто задаваемые вопросы

**Q: Как установить GroupDocs.Redaction в Maven‑проекте?**  
A: Добавьте репозиторий GroupDocs и зависимость `groupdocs-redaction` в ваш `pom.xml`, как показано в разделе настройки Maven.

**Q: Могу ли я редактировать текст в PDF‑файлах с помощью этой библиотеки?**  
A: Да, GroupDocs.Redaction поддерживает PDF, DOCX, PPTX и многие другие форматы.

**Q: Что происходит, если точная фраза не найдена?**  
A: `RedactorChangeLog` вернёт статус `Failed`. Проверьте написание фразы и чувствительность к регистру.

**Q: Как эффективно обрабатывать очень большие документы?**  
A: Обрабатывайте их небольшими диапазонами страниц, включайте растеризацию только при необходимости и всегда закрывайте `Redactor`, чтобы освободить ресурсы.

**Q: Можно ли сохранить растровые PDF с определёнными диапазонами страниц?**  
A: Конечно. Используйте `options.getRasterization().setPageIndex()` и `setPageCount()`, чтобы указать точные страницы для растеризации.

## Заключение
Теперь у вас есть полное пошаговое руководство по **how to redact text** с GroupDocs.Redaction Java и **save as rasterized PDF**. Следуя этим шагам, вы сможете защищать конфиденциальную информацию, соответствовать строгим стандартам соответствия и поддерживать производительность ваших Java‑сервисов в масштабе.

**Следующие шаги**  
- Углубитесь в API, изучив [официальную документацию](https://docs.groupdocs.com/redaction/java/).  
- Экспериментируйте с другими типами редактирования, такими как `RegexRedaction` и `ImageRedaction`.  
- Присоединяйтесь к сообществу на [форуме поддержки GroupDocs](https://forum.groupdocs.com/c/redaction/33) для советов и лучших практик.

---

**Последнее обновление:** 2026-08-20  
**Тестировано с:** GroupDocs.Redaction Java 24.9  
**Автор:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Связанные учебники

- [Как редактировать текст с помощью GroupDocs.Redaction для Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Учебник по редактированию текста Java: руководство с GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)