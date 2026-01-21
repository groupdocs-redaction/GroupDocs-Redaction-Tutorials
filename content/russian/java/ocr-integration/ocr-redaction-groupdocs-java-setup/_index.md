---
date: '2026-01-21'
description: Узнайте, как редактировать PDF с помощью OCR и редактировать отсканированные
  документы, используя GroupDocs.Redaction для Java с интеграцией Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Редактирование PDF с OCR с использованием GroupDocs и Azure OCR – Руководство
  по Java
type: docs
url: /ru/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Редактировать PDF с OCR с использованием GroupDocs & Azure OCR – Руководство по Java

В этом всестороннем руководстве вы узнаете, как **redact PDF with OCR** на Java, используя GroupDocs.Redaction совместно с Microsoft Azure OCR. Независимо от того, работаете ли вы с нативными PDF или отсканированными изображениями, это руководство покажет, как точно находить и маскировать конфиденциальные данные, помогая вам **redact scanned documents** для соблюдения правил конфиденциальности.

## Быстрые ответы
- **Что делает OCR redaction?** Он извлекает текст из изображений/PDF и автоматически применяет правила редактирования.  
- **Какая библиотека предоставляет движок редактирования?** GroupDocs.Redaction for Java.  
- **Какой сервис OCR используется?** Microsoft Azure OCR connector.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; для продакшн требуется постоянная лицензия.  
- **Можно ли редактировать как нативные, так и отсканированные PDF?** Да — OCR позволяет редактировать отсканированные документы.

## Что такое «redact PDF with OCR»?
Редактирование PDF с OCR означает использование оптического распознавания символов для преобразования визуального текста в поисковые строки, а затем применение шаблонов редактирования (например, regex) для скрытия этой информации до того, как файл будет передан или сохранён.

## Почему использовать GroupDocs.Redaction с Azure OCR?
- **Высокая точность** на отсканированных страницах благодаря облачному OCR‑движку Azure.  
- **Простой Java API**, который интегрируется напрямую в ваш текущий рабочий процесс.  
- **Гибкие правила редактирования** — regex, ключевые слова или пользовательская логика.  
- **Готовый к соблюдению нормативов** вывод, который навсегда удаляет конфиденциальные данные.

## Предварительные требования
- Java Development Kit (JDK) 8 или новее.  
- Maven (или возможность скачать JAR вручную).  
- Учётная запись Microsoft Azure с учётными данными OCR.  
- Базовые знания Java и знакомство с регулярными выражениями.

## Настройка GroupDocs.Redaction для Java

### Настройка Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Если вы предпочитаете не использовать Maven, скачайте последнюю JAR‑файл с официальной страницы релизов: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Приобретение лицензии
- **Free Trial** – изучите основные функции без обязательств.  
- **Temporary License** – продлите пробный период для более крупных проектов.  
- **Full License** – разблокировать неограниченное использование и премиум‑поддержку.

### Базовая инициализация и настройка
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Как редактировать PDF с OCR на Java

### Шаг 1: Загрузка документа с настройками OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Параметры**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – путь к целевому PDF.  
  - `new LoadOptions()` – конфигурация загрузки по умолчанию.  
  - `settings` – содержит коннектор Azure OCR.

### Шаг 2: Применение редактирования с помощью Regex (например, номера социального страхования)
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
- **Объяснение Regex** – `\b\d** – дважды пров точку.  
- **Путь к файлу** – убедитесь, что PDF существует и приложение имеет права чтения/записи.  
- **Производительность** – большие PDF могут требовать увеличения размера кучи или асинхронной обработки.

## Практические примеры использования редактирования отсканированных документов
1. **Юридические фирмы** – скрывать идентификаторы клиентов перед обменом делами.  
2. **Финансовые учреждения** – маскировать номера счетов в отсканированных выписках.  
3. **Медицинские организации** – защищать PHI пациентов в отсканированных медицинских записях.  
4. **Государственные органы** – удалять персональные данные из публичных PDF‑документов.  
5. **Корпорации** – очищать контракты перед аудитами сторонних организаций.

## Советы по производительности
- Делайте regex‑шаблоны как можно более специфичными, чтобы сократить время обработки.  
- Быстро освобождайте экземпляр `Redactor` (используйте try‑with‑resources, как показано).  
- Для пакетной обработки рассматривайте очередь задач и их выполнение в параллельных потоках.

## Часто задаваемые вопросы

**Q: Что такое OCR redaction?**  
A: OCR redaction использует оптическое распознавание символов для извлечения текста из изображений или отсканированных PDF, затем применяет правила редактирования для постоянного удаления этого текста.

**Q: Можно ли использовать GroupDocs.Redaction без Azure OCR?**  
A: Да, но OCR значительно повышает точность для отсканированных документов, позволяя эффективно **redact scanned documents**.

**Q: Как работать со сложными regex‑шаблонами?**  
A: Тестируйте шаблоны на примерах данных, используйте границы слов (`\b`) чтобы избежать частичных совпадений, и рассматривайте разбивку больших выражений на несколько более простых редактирований.

**Q: Какие типичные узкие места в производительности?**  
A: Интенсивные вызовы OCR на больших файлах, слишком широкие regex и недостаточное выделение памяти. Оптимизируйте, настраивая regex и масштабируя ресурсы.

**Q: Где можно получить помощь при возникновении проблем?**  
A: Задавайте вопросы на форуме сообщества GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Дополнительные ресурсы
- **Documentation**: https://docs.groupdocs.com/redaction/java/
- **API Reference**: https://reference.groupdocs.com/redaction/java
- **Download**: https://releases.groupdocs.com/redaction/java/
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
- **Free Support**: https://forum.groupdocs.com/c/redaction/33
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Последнее обновление:** 2026-01-21  
**Тестировано с:** GroupDocs.Redaction 24.9 for Java  
**Автор:** GroupDocs