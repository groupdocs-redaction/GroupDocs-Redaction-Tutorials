---
date: '2026-06-26'
description: Узнайте, как извлекать текст из отсканированного PDF и маскировать чувствительные
  данные с помощью GroupDocs OCR Redaction и Azure OCR. Маскируйте social security
  number и заменяйте confidential info в PDF эффективно.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Извлечение текста из отсканированного PDF – Маскирование данных с помощью GroupDocs
  OCR
type: docs
url: /ru/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Извлечение текста из отсканированного PDF – Маскирование данных с помощью GroupDocs OCR

В современном мире, ориентированном на данные, **извлечение текста из отсканированных PDF** файлов и маскирование конфиденциальной информации является обязательным шагом соответствия. Этот учебник покажет, как использовать GroupDocs Redaction совместно с Microsoft Azure OCR для надёжного распознавания скрытого текста на отсканированных страницах и замены его безопасным заполнителем, например **`[REDACTED]`**. Вы увидите, почему эта комбинация быстра, точна и готова к нагрузкам производственного уровня.

## Быстрые ответы
- **Что означает «маскировать конфиденциальные данные»?** Это заменяет обнаруженный конфиденциальный текст заполнителем (например, `[REDACTED]`).  
- **Какая библиотека обрабатывает OCR?** Коннектор Microsoft Azure OCR, используемый через GroupDocs Redaction.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для оценки; для производства требуется постоянная лицензия.  
- **Могу ли я редактировать отсканированные PDF?** Да — OCR извлекает скрытый текст перед применением регекс‑редакций.  
- **Это решение только для Java?** Пример основан на Java, но GroupDocs предоставляет аналогичные API для .NET и других платформ.

## Что такое OCR‑Based Redaction?
OCR‑Based Redaction сначала запускает OCR на каждой странице, преобразуя изображения в индексируемый текст, затем применяет регекс‑шаблоны для замены совпадений маской, такой как `[REDACTED]`. Этот двухшаговый процесс позволяет надёжно скрывать персональные данные даже в отсканированных PDF, гарантируя, что любые конфиденциальные строки удаляются до того, как документ будет передан или архивирован.

## Почему использовать GroupDocs Redaction с Azure OCR?
Вам следует использовать GroupDocs Redaction с Azure OCR, потому что он обеспечивает **более 98 % точности OCR для печатного текста**, поддерживает **более 50 форматов ввода и вывода** и может обрабатывать **PDF‑файлы со сотнями страниц без загрузки всего файла в память**, обеспечивая быструю и масштабируемую редактировку для соответствия требованиям. Решение также **масштабируется для обработки PDF‑файла в 1 000 страниц менее чем за 2 минуты на 8‑ядерном сервере**, делая пакетные задания практичными.

## Предварительные требования
- **Java Development Kit (JDK) 8+** установлен.  
- **Maven** (если вы предпочитаете управление зависимостями) или возможность скачивать JAR‑файлы вручную.  
- **Учётные данные Microsoft Azure OCR** (конечная точка и ключ подписки).  
- Базовые знания Java и знакомство с регулярными выражениями.

## Настройка GroupDocs Redaction для Java

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
If you prefer manual JAR management, grab the latest release from [GroupDocs.Redaction для Java релизов](https://releases.groupdocs.com/redaction/java/).

### Приобретение лицензии
- **Free Trial** – изучите все функции бесплатно.  
- **Temporary License** – продлите время оценки.  
- **Full License** – разблокировать возможности, готовые к производству.

### Базовая инициализация и настройка
Класс `Redactor` является ядром, которое выполняет извлечение OCR и применяет правила редактирования к PDF‑документам.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Как маскировать конфиденциальные данные с помощью OCR Redaction
Маскирование конфиденциальных данных с помощью OCR Redaction включает загрузку PDF с настройками Azure OCR, определение регекс‑шаблонов для данных, которые нужно скрыть, и вызов Redactor для замены каждого совпадения заполнителем, например `[REDACTED]`. Библиотека обрабатывает OCR, сопоставление шаблонов и перезапись PDF в едином рабочем процессе.

### Шаг 1: Загрузка документа с настройками OCR
`LoadOptions` настраивает, как GroupDocs загружает файл, позволяя передавать OCR‑коннекторы, такие как Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – замените на путь к вашему PDF.  
- **`settings`** – содержит Azure OCR коннектор, созданный ранее.

### Шаг 2: Определение и применение регекс‑редакций
`ReplacementOptions` указывает текст замены, который будет подставлен вместо каждого совпадения регекса во время редактирования.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Шаблон `\b\d{3}-\d{2}-\d{4}\b` соответствует номерам социального страхования США.  
- `ReplacementOptions("[REDACTED]")` заменяет каждое совпадение маской, эффективно **маскируя конфиденциальные данные**.

## Распространённые сценарии использования маскирования конфиденциальных данных
1. **Управление юридическими документами** – скрывать идентификаторы клиентов перед обменом черновиками.  
2. **Финансовая отчётность** – защищать номера счетов и идентификаторы транзакций.  
3. **Медицинские записи** – соответствовать HIPAA, редактируя идентификаторы пациентов.  
4. **Государственные публикации** – удалять персональные данные из публичных записей.  
5. **Корпоративные контракты** – скрывать собственные условия во время внешних проверок.

## Советы по производительности
- **Оптимизировать регекс** – избегать слишком общих шаблонов, которые увеличивают время обработки; хорошо построенные выражения могут сократить время выполнения до 40 %.  
- **Управление памятью** – своевременно закрывайте экземпляр `Redactor` (try‑with‑resources делает это автоматически).  
- **Асинхронное выполнение** – для массовой обработки запускайте задачи редактирования в отдельных потоках или используйте очередь задач, чтобы UI оставался отзывчивым.

## Устранение неполадок
- **Ошибка учётных данных Azure** – дважды проверьте URL конечной точки и ключ подписки в `MicrosoftAzureOcrConnector`.  
- **Документ не загружается** – проверьте путь к файлу и убедитесь, что PDF не защищён паролем (или передайте пароль через `LoadOptions`).  
- **Редакции не применились** – сначала протестируйте ваш регекс на простой строке; используйте `Pattern.compile` в юнит‑тесте, чтобы подтвердить совпадения.

## Часто задаваемые вопросы

**Q: Что такое OCR‑редактирование?**  
A: OCR‑редактирование использует оптическое распознавание символов (Optical Character Recognition) для извлечения скрытого текста из изображений или отсканированных PDF, затем применяет правила редактирования для маскирования этого текста.

**Q: Могу ли я использовать GroupDocs Redaction без Azure OCR?**  
A: Да, но OCR значительно повышает точность в отсканированных документах, где нативное извлечение текста не работает.

**Q: Как работать со сложными регекс‑шаблонами?**  
A: Создавайте и тестируйте их поэтапно, используя класс Java `Pattern` в песочнице перед применением к большим документам.

**Q: Какие типичные узкие места в производительности?**  
A: Большие PDF, слишком сложные регекс и синхронные вызовы OCR могут замедлять обработку; рассмотрите пакетную обработку и оптимизированные шаблоны.

**Q: Доступна ли поддержка по вопросам реализации?**  
A: Абсолютно — обратитесь через [форум GroupDocs](https://forum.groupdocs.com/c/redaction/33) за помощью сообщества или свяжитесь со службой поддержки GroupDocs.

## Дополнительные ресурсы
- **Документация**: https://docs.groupdocs.com/redaction/java/  
- **Справочник API**: https://reference.groupdocs.com/redaction/java  
- **Скачать**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Бесплатная поддержка**: https://forum.groupdocs.com/c/redaction/33  
- **Временная лицензия**: https://purchase.groupdocs.com/temporary-license/

---

**Последнее обновление:** 2026-06-26  
**Тестировано с:** GroupDocs.Redaction 24.9 (Java)  
**Автор:** GroupDocs  

## Связанные учебники

- [Безопасное редактирование PDF с использованием OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Как редактировать текст с помощью GroupDocs.Redaction для Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Маскирование конфиденциальных данных Java – редактирование личной информации с помощью GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)