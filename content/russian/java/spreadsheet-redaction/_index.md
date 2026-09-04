---
date: 2026-08-04
description: Узнайте, как фильтровать данные электронных таблиц Java и безопасно redact
  столбцы или ячейки в Excel‑таблицах с помощью GroupDocs.Redaction для Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Узнайте, как фильтровать данные электронных таблиц Java и безопасно
  redact столбцы или ячейки в Excel‑таблицах с помощью GroupDocs.Redaction для Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Фильтрация данных электронных таблиц Java – руководство с GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Фильтрация данных электронных таблиц Java – руководство с GroupDocs.Redaction
type: docs
url: /ru/java/spreadsheet-redaction/
weight: 12
---

# Фильтрация данных таблицы java – Руководство по GroupDocs.Redaction Java

Если вам нужно **filter spreadsheet data java** перед применением редактирования, вы попали в нужное руководство. В этом уроке вы узнаете, как изолировать строки, столбцы или отдельные ячейки, содержащие личную или конфиденциальную информацию, а затем безопасно их отредактировать с помощью GroupDocs.Redaction для Java. Шаги объяснены простым языком, включают рекомендации лучших практик и показывают, как сохранять высокую скорость обработки даже для больших книг.

## Быстрые ответы
- **Какая библиотека обрабатывает редактирование таблиц в Java?** GroupDocs.Redaction for Java.  
- **Могу ли я фильтровать строки без загрузки всего файла в память?** Да — API передаёт данные потоково и позволяет применять фильтры на лету.  
- **Какие форматы файлов поддерживаются?** Более 30 форматов таблиц, включая XLS, XLSX, CSV и ODS.  
- **Нужна ли лицензия для разработки?** Временная лицензия подходит для тестирования; полная лицензия требуется для продакшн.  
- **Есть ли ограничение на размер книги?** Движок может обрабатывать файлы до 500 МБ без чрезмерного потребления памяти.

## Что такое filter spreadsheet data java?
**Filter spreadsheet data java** — это процесс программного выбора определённых строк, столбцов или ячеек в рабочей книге в стиле Excel с использованием кода Java, чтобы проверять или редактировать только целевой контент. Эта техника сокращает время выполнения, ограничивает ненужные изменения и помогает соответствовать требованиям типа GDPR.

## Почему filter spreadsheet data java?
GroupDocs.Redaction Java поддерживает **30+ форматов таблиц** и может обрабатывать книги, содержащие **до 500 МБ** (примерно 1 миллион строк), при этом потребление памяти остаётся ниже **200 МБ**. Фильтруя данные заранее, вы избегаете работы с нерелевантными данными, что в среднем сокращает время обработки на **40‑60 %** для типичных сценариев очистки конфиденциальных данных.

## Требования
- Java 17 или новее, установленный.  
- Система сборки Maven или Gradle.  
- GroupDocs.Redaction for Java (доступен для скачивания с официального сайта).  
- Временный или полный лицензионный ключ.  

## Как фильтровать данные в таблицах с помощью GroupDocs.Redaction Java?
Загрузите рабочую книгу, определите фильтр, соответствующий ячейкам, которые нужно отредактировать, и затем выполните операцию редактирования. API выполняет фильтрацию потоково, поэтому вам не нужно держать весь файл в ОЗУ.

Класс `RedactionFilter` позволяет задавать индексы столбцов, диапазоны строк или пользовательские предикаты. Например, вы можете выбрать каждую ячейку в столбце **B**, содержащую шаблон email‑адреса, или ограничить редактирование строками, где столбец «Status» равен «Confidential».

**Direct answer (40‑70 words):**  
Создайте экземпляр `RedactionFilter`, задайте индекс столбца и условие регулярного выражения, затем передайте фильтр в `Redactor.redact(workbook, filter)`. Этот однострочный фильтр изолирует точные ячейки, соответствующие вашим критериям, а редактор удаляет или маскирует их, оставляя остальную часть листа нетронутой. Операция завершается за линейное время относительно отфильтрованных строк.

### Шаг 1: создать экземпляр фильтра
`RedactionFilter` — основной класс, представляющий правило фильтрации для редактирования таблиц. Он принимает номера столбцов, номера строк или пользовательские лямбда‑выражения для точного определения данных.

### Шаг 2: настроить условие
Используйте `filter.setColumnIndex(1)`, чтобы выбрать столбец B (нумерация с нуля), и `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` для сопоставления шаблона email‑адресов. Вы также можете комбинировать несколько условий с помощью `filter.and(...)` или `filter.or(...)`.

### Шаг 3: применить редактирование
`Redactor` — основной класс, выполняющий операции редактирования над рабочей книгой.  
Передайте рабочую книгу и настроенный фильтр объекту `Redactor`. API передаёт книгу потоково, применяет фильтр и записывает отредактированный результат в новый файл, сохраняя исходное форматирование и формулы.

## Распространённые проблемы и решения
- **Фильтр не находит ячейки:** Проверьте индекс столбца (нумерация с нуля) и убедитесь, что синтаксис регулярного выражения корректен для Java.  
- **Ошибки нехватки памяти при работе с большими файлами:** Увеличьте размер кучи JVM умеренно (например, `-Xmx1g`) или разбейте книгу на более мелкие части перед фильтрацией.  
- **Отредактированный вывод теряет форматирование:** `RedactionOptions` позволяет настроить поведение редактирования, например, сохранять форматирование ячеек. Используйте `RedactionOptions.setPreserveFormatting(true)`, чтобы сохранить стили ячеек.

## Почему фильтровать данные таблицы?
Фильтрация перед редактированием изолирует только чувствительные части книги, что позволяет избежать ненужных изменений чистых данных. Такой избирательный подход также снижает риск случайной потери данных и ускоряет аудиты соответствия, поскольку журнал аудита содержит гораздо меньше записей.

## Как отредактировать email‑адреса в Excel‑таблицах с помощью GroupDocs.Redaction Java API
Загрузите ваш Excel‑файл, примените фильтр, ищущий типичный шаблон email‑адреса, и вызовите редактор. API заменяет каждый найденный email на заполнитель, например «***@***.com», при этом сохраняет расположение окружающих ячеек.

## Как фильтровать данные – доступные руководства
- [How to Redact Emails in Excel Spreadsheets Using GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Дополнительные ресурсы

- [Документация GroupDocs.Redaction для Java](https://docs.groupdocs.com/redaction/java/)
- [Справочник API GroupDocs.Redaction для Java](https://reference.groupdocs.com/redaction/java/)
- [Скачать GroupDocs.Redaction для Java](https://releases.groupdocs.com/redaction/java/)
- [Форум GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Бесплатная поддержка](https://forum.groupdocs.com/)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-08-04  
**Тестировано с:** GroupDocs.Redaction 23.11 for Java  
**Автор:** GroupDocs  

---

## Часто задаваемые вопросы

**В: Можно ли фильтровать несколько столбцов одновременно?**  
О: Да, вы можете добавить дополнительные индексы столбцов в тот же экземпляр `RedactionFilter` или связать несколько фильтров с помощью `filter.or(...)`.

**В: Работает ли фильтр с паролем защищёнными книгами?**  
О: Укажите пароль при открытии книги; фильтр работает после расшифровки так же, как и с незащищённым файлом.

**В: Сколько строк может обработать API за одну операцию?**  
О: Движок оптимизирован для обработки до 1 миллиона строк (≈500 МБ) без загрузки всего файла в память.

**В: Можно ли предварительно просмотреть, какие ячейки будут отредактированы перед сохранением?**  
О: Да, вызовите `filter.preview(workbook)`, чтобы получить список адресов ячеек, соответствующих критериям.

**В: Какая модель лицензирования требуется для продакшн‑использования?**  
О: Для продакшн‑развёртываний требуется полная коммерческая лицензия; временная лицензия достаточна для тестирования и оценки.

## Связанные руководства

- [Как отредактировать конфиденциальные данные в Excel‑таблицах с помощью GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Маскирование конфиденциальных данных Java – Руководство GroupDocs.Redaction](/redaction/java/getting-started/)
- [Маскирование конфиденциальных данных Java – Редактирование личной информации с помощью GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)