---
date: '2026-02-08'
description: Узнайте, как маскировать конфиденциальные данные и редактировать PDF‑файлы
  Java с помощью GroupDocs OCR Redaction и Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Маскировка конфиденциальных данных в PDF с помощью GroupDocs OCR Redaction
type: docs
url: /ru/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

 no actual fenced code blocks in the text, only placeholders. So fine.

Now translate.

We'll translate each heading and paragraph.

Be careful with bold formatting **...** keep.

Also keep inline code formatting `...`.

Let's produce.

# Маскировка конфиденциальных данных в PDF с помощью GroupDocs OCR Redaction

В современном цифровом мире защита персональной и конфиденциальной информации является приоритетом. В этом руководстве **вы узнаете, как маскировать конфиденциальные данные** в PDF‑файлах, комбинируя GroupDocs Redaction с Microsoft Azure OCR. Такой подход обеспечивает надёжное распознавание текста на отсканированных страницах и позволяет **редактировать PDF Java** документы с точностью, гарантируя соответствие требованиям конфиденциальности.

## Быстрые ответы
- **Что означает «маскировать конфиденциальные данные»?** Это замена найденного конфиденциального текста на заполнитель (например, `[REDACTED]`).  
- **Какая библиотека отвечает за OCR?** Коннектор Microsoft Azure OCR, используемый через GroupDocs Redaction.  
- **Нужна ли лицензия?** Для оценки достаточно бесплатной пробной версии; для продакшна требуется постоянная лицензия.  
- **Можно ли редактировать отсканированные PDF?** Да — OCR извлекает скрытый текст перед применением регекс‑правил редактирования.  
- **Это решение только для Java?** Пример написан на Java, но GroupDocs предоставляет аналогичные API для .NET и других платформ.

## Что такое OCR‑Based Redaction?
OCR‑based redaction сначала запускает оптическое распознавание символов (OCR) на каждой странице документа, превращая изображения текста в поисковые строки. После того как текст становится доступным для поиска, можно применять правила регулярных выражений (regex) для поиска конфиденциальной информации — например, номеров социального страхования, номеров кредитных карт или персональных идентификаторов — и заменять её маской, такой как **`[REDACTED]`**.

## Почему стоит использовать GroupDocs Redaction с Azure OCR?
- **Высокая точность** на отсканированных PDF и изображениях.  
- **Бесшовная интеграция с Java** через Maven или прямую загрузку JAR‑файла.  
- **Гибкий движок regex** позволяет задавать пользовательские шаблоны для любого типа данных.  
- **Масштабируемость** для больших пакетов документов, с возможностью асинхронной обработки.

## Предварительные требования
- **Java Development Kit (JDK) 8+** установлен.  
- **Maven** (если вы предпочитаете управление зависимостями) или возможность вручную загрузить JAR‑файлы.  
- **Учётные данные Microsoft Azure OCR** (endpoint и ключ подписки).  
- Базовые знания Java и знакомство с регулярными выражениями.

## Настройка GroupDocs Redaction для Java

### Maven Setup
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

### Прямая загрузка
Если вы предпочитаете управлять JAR‑файлами вручную, скачайте последнюю версию с [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Приобретение лицензии
- **Free Trial** – исследуйте все возможности бесплатно.  
- **Temporary License** – продлите период оценки.  
- **Full License** – разблокируйте возможности для продакшна.

### Базовая инициализация и настройка
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Как маскировать конфиденциальные данные с помощью OCR Redaction

### Шаг 1: Загрузка документа с настройками OCR
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
- **`LoadOptions`** – загрузка по умолчанию; при необходимости можно настроить.  
- **`settings`** – содержит коннектор Azure OCR, который вы создали ранее.

### Шаг 2: Определение и применение regex‑редакций
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
- `ReplacementOptions("[REDACTED]")` заменяет каждое совпадение на маску, эффективно **маскируя конфиденциальные данные**.

## Распространённые сценарии использования маскировки конфиденциальных данных
1. **Управление юридическими документами** – скрывать идентификаторы клиентов перед отправкой черновиков.  
2. **Финансовая отчётность** – защищать номера счетов и идентификаторы транзакций.  
3. **Медицинские записи** – соблюдать HIPAA, редактируя идентификаторы пациентов.  
4. **Государственные публикации** – удалять персональные данные из публичных реестров.  
5. **Корпоративные контракты** – скрывать конфиденциальные условия при внешних проверках.

## Советы по производительности
- **Оптимизируйте regex** – избегайте слишком широких шаблонов, которые увеличивают время обработки.  
- **Управление памятью** – своевременно закрывайте экземпляр `Redactor` (try‑with‑resources делает это автоматически).  
- **Асинхронное выполнение** – для пакетной обработки запускайте задачи редактирования в отдельных потоках или используйте очередь задач.  

## Устранение неполадок
- **Ошибка учётных данных Azure** – дважды проверьте URL endpoint и ключ подписки в `MicrosoftAzureOcrConnector`.  
- **Документ не загружается** – проверьте путь к файлу и убедитесь, что PDF не защищён паролем (или передайте пароль через `LoadOptions`).  
- **Редакции не применяются** – сначала протестируйте ваш regex на простой строке; используйте `Pattern.compile` в юнит‑тесте, чтобы убедиться в совпадениях.

## Часто задаваемые вопросы

**В: Что такое OCR‑redaction?**  
О: OCR‑redaction использует оптическое распознавание символов для извлечения скрытого текста из изображений или отсканированных PDF, после чего применяет правила редактирования для маскирования этого текста.

**В: Можно ли использовать GroupDocs Redaction без Azure OCR?**  
О: Да, но OCR значительно повышает точность на отсканированных документах, где обычное извлечение текста не работает.

**В: Как работать со сложными regex‑шаблонами?**  
О: Создавайте и тестируйте их поэтапно, используя класс Java `Pattern` в песочнице перед применением к большим документам.

**В: Какие типичные узкие места в производительности?**  
О: Большие PDF, слишком сложные regex и синхронные вызовы OCR могут замедлять процесс; рассматривайте пакетную обработку и оптимизированные шаблоны.

**В: Есть ли поддержка при возникновении проблем с реализацией?**  
О: Конечно — обращайтесь через [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) для получения помощи от сообщества или свяжитесь со службой поддержки GroupDocs.

## Дополнительные ресурсы
- **Документация**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Последнее обновление:** 2026-02-08  
**Тестировано с:** GroupDocs.Redaction 24.9 (Java)  
**Автор:** GroupDocs  

---