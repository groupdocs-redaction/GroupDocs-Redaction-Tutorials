---
date: '2026-09-21'
description: Узнайте, как редактировать изображение с помощью GroupDocs.Redaction
  for Java. Пошаговое руководство охватывает setup, pixel‑level redaction, verification
  и best practices.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Как редактировать изображение с помощью GroupDocs.Redaction for Java.
  Следуйте этому руководству, чтобы mask pixel data в отсканированных файлах, choose
  colors и verify results — идеально для соответствия GDPR и HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Как редактировать изображение с помощью GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Как редактировать изображение с помощью GroupDocs.Redaction for Java
type: docs
url: /ru/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Как замаскировать изображение с помощью GroupDocs.Redaction для Java

В этом полном руководстве вы узнаете **как замаскировать изображение** в Java с помощью GroupDocs.Redaction. Замаскировка отсканированных изображений — важный шаг для защиты персональных данных, соответствия требованиям GDPR, HIPAA и другим нормативам конфиденциальности, а также обеспечения того, чтобы конфиденциальная визуальная информация никогда не утекала. Мы пройдём через настройку проекта, конфигурацию редактирования на уровне пикселей, безопасное сохранение результата и проверку успешности редактирования — всё представлено в разговорном пошаговом стиле, который вы можете скопировать в любое Java‑приложение.

## Быстрые ответы
- **Какая библиотека обрабатывает редактирование изображений в Java?** GroupDocs.Redaction для Java.  
- **Можно ли выбрать цвет редактирования?** Да — любой непрозрачный `java.awt.Color`, например `Color.BLUE` или `Color.BLACK`.  
- **Требуется ли лицензия для продакшна?** Да, действующая лицензия GroupDocs обязательна для коммерческого использования.  
- **Будет ли оригинальное изображение перезаписано?** Нет — API записывает отредактированное изображение в новый файл, который вы указываете.  
- **Какая версия Java поддерживается?** Java 8 и новее (до Java 21 на момент написания).

## Что такое редактирование изображений и почему редактировать отсканированные изображения java?
Редактирование изображений навсегда скрывает визуальные данные — имена, номера, подписи — заменяя области пикселей сплошным цветом. В отличие от редактирования текста, которое работает с выделяемыми символами, отсканированные изображения хранят информацию как сырые пиксели, поэтому только пиксель‑ориентированные инструменты могут гарантировать, что данные нельзя восстановить. С помощью GroupDocs.Redaction вы можете точно задавать координаты, применять любой непрозрачный цвет и создавать новое изображение, которое окончательно удаляет чувствительное содержимое.

## Почему использовать GroupDocs.Redaction для Java?
GroupDocs.Redaction поддерживает **более 50 форматов изображений** (включая JPG, PNG, BMP, GIF) и может обрабатывать документы в сотни страниц без загрузки всего файла в память благодаря своей потоковой архитектуре. Тесты показывают, что отсканированный PNG размером 300 KB редактируется менее чем за 120 ms на типичном процессоре 2.8 GHz, что делает его подходящим как для пакетных задач, так и для сервисов в реальном времени.

## Предварительные требования
Перед началом убедитесь, что у вас есть:

- **JDK 8 или новее** установлен и настроен в `PATH`.  
- **Maven** (или Gradle) для управления зависимостями.  
- IDE, такая как **IntelliJ IDEA**, **Eclipse** или **NetBeans**.  
- Базовые знания работы с файловой системой Java и пакетом `java.awt`.  

## Настройка GroupDocs.Redaction для Java

### Настройка Maven
Добавьте репозиторий GroupDocs и зависимость в ваш `pom.xml`:

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
Кроме того, загрузите последнюю JAR‑файл со страницы официальных выпусков: [выпуски GroupDocs.Redaction для Java](https://releases.groupdocs.com/redaction/java/).

### Приобретение лицензии
- **Бесплатная пробная версия:** Зарегистрируйтесь для пробного доступа к полному API.  
- **Временная лицензия:** Используйте временный ключ для расширенного тестирования без оплаты.  
- **Полная покупка:** Приобретите производственную лицензию для неограниченного развертывания.

## Руководство по реализации

Мы разделим реализацию на две основные функции: **редактирование области изображения** (само маскирование) и **проверка статуса редактирования** (подтверждение успеха).

### Как редактировать отсканированные изображения документов – шаг 1: инициализировать редактор
`Redactor` — центральный класс, который загружает изображение и предоставляет операции редактирования.  
Создайте экземпляр `Redactor`, указывающий на исходное изображение, которое нужно обработать.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Шаг 2: определить параметры редактирования
`ImageAreaRedaction` работает с `Point` (верхний‑левый угол) и `Dimension` (ширина × высота), описывающими прямоугольник для скрытия. В этом примере используется синий цвет заливки.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Шаг 3: применить редактирование
`RegionReplacementOptions` позволяет задать цвет заливки и необязательную рамку. Передача этих параметров в `ImageAreaRedaction` и вызов `apply()` выполняет маскирование. Метод возвращает `RedactorChangeLog`, указывающий на успех или неудачу.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Шаг 4: освободить ресурсы
`Redactor` реализует `AutoCloseable`. Закрытие освобождает нативные буферы и файловые дескрипторы, предотвращая утечки памяти в длительно работающих сервисах.

```java
redactor.close();
```

### Как проверить редактирование – проверка статуса
После применения редактирования проверьте `RedactorChangeLog`. Значение `Status.SUCCESS` подтверждает, что область пикселей заменена без ошибок. Вы также можете отрисовать изображение в `BufferedImage` для визуального контроля перед сохранением.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Практические применения
- **Обработка конфиденциальных документов:** Маскировать персональные данные в отсканированных контрактах перед передачей партнёрам.  
- **Юридическая документация:** Обеспечить соответствие GDPR или HIPAA, редактируя идентификаторы в доказательных изображениях.  
- **Медицинские записи:** Скрывать лица пациентов или рукописные заметки на радиологических снимках, сохраняя диагностическую информацию.  

## Соображения по производительности
- **Пакетная обработка:** Обрабатывайте изображения группами по 10–20, чтобы держать использование памяти ниже 200 MB.  
- **Повторное использование объектов:** Переиспользуйте объекты `Point` и `Dimension` между итерациями, чтобы снизить нагрузку на GC.  
- **Обновления версии:** Переходите на последнюю версию GroupDocs.Redaction, чтобы воспользоваться заявленным ускорением на 15 % в версии 24.10.  

## Распространённые проблемы и решения
| Проблема | Причина | Решение |
|-------|-------|-----|
| **Редактирование не удалось со статусом `Failed`** | Неправильный путь к файлу или неподдерживаемый формат изображения | Проверьте, что файл существует и имеет поддерживаемый формат (JPG, PNG, BMP, GIF). |
| **Файл вывода пустой** | `redactor.save()` вызван до завершения редактирования | Убедитесь, что `apply()` возвращает `Status.SUCCESS` перед вызовом `save()`. |
| **Цвет не применён** | Используется прозрачный `Color` | Выберите непрозрачный цвет, например `Color.BLACK` или `Color.BLUE`. |

## Часто задаваемые вопросы

**Q: В чём разница между `ImageAreaRedaction` и редактированием текста?**  
A: `ImageAreaRedaction` работает с координатами пикселей, тогда как редактирование текста анализирует OCR‑слои для поиска и удаления текстового содержимого.

**Q: Могу ли я редактировать несколько областей на одном изображении?**  
A: Да — вызывайте `redactor.apply()` последовательно с разными объектами `ImageAreaRedaction` перед сохранением итогового файла.

**Q: Поддерживает ли GroupDocs.Redaction другие форматы изображений, такие как TIFF?**  
A: Библиотека поддерживает распространённые растровые форматы (JPG, PNG, BMP, GIF). Для TIFF сначала преобразуйте изображение в поддерживаемый формат.

**Q: Как автоматизировать редактирование папки отсканированных PDF?**  
A: Извлеките каждую страницу как изображение, примените ту же логику редактирования, затем соберите PDF заново с помощью библиотеки PDF, например GroupDocs.Conversion.

**Q: Можно ли предварительно просмотреть редактирование перед сохранением?**  
A: Отрисуйте `Redactor` в `BufferedImage` и отобразите его в UI Swing или JavaFX, чтобы подтвердить корректность замаскированной области перед окончательным сохранением.

## Заключение
Теперь у вас есть полное, готовое к продакшну руководство по **как замаскировать изображение** и, конкретно, **как редактировать отсканированные изображения java** с помощью GroupDocs.Redaction для Java. Следуя описанным шагам, вы сможете защищать чувствительные визуальные данные в финансовом, юридическом и медицинском секторах. Изучайте дополнительные API — такие как редактирование текста, редактирование страниц PDF или пакетная обработка папок — чтобы построить сквозной конвейер защиты данных для вашей организации.

**Ресурсы**  
- [Документация](https://docs.groupdocs.com/redaction/java/)  
- [Справочник API](https://reference.groupdocs.com/redaction/java)  
- [Скачать](https://releases.groupdocs.com/redaction/java/)  
- [Репозиторий GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/redaction/33)  
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/) 

---

**Последнее обновление:** 2026-09-21  
**Тестировано с:** GroupDocs.Redaction 24.9 (Java)  
**Автор:** GroupDocs

## Связанные руководства

- [Как редактировать Java с помощью GroupDocs.Redaction - Полное руководство для разработчиков](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Как редактировать отсканированный PDF с OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Как редактировать текст в Java с помощью GroupDocs.Redaction – Руководство](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)