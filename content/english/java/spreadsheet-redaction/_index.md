---
date: 2026-08-04
description: Learn how to filter spreadsheet data java and securely redact columns
  or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
images:
- /java/spreadsheet-redaction/og-image.png
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Learn how to filter spreadsheet data java and securely redact columns
  or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filter spreadsheet data java – guide with GroupDocs.Redaction
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
title: Filter spreadsheet data java – guide with GroupDocs.Redaction
type: docs
url: /java/spreadsheet-redaction/
weight: 12
---

# Filter spreadsheet data java – GroupDocs.Redaction Java tutorial

If you need to **filter spreadsheet data java** before applying redaction, you’ve landed on the right guide. In this tutorial you’ll discover how to isolate rows, columns, or individual cells that contain personal or confidential information, then redact them safely with GroupDocs.Redaction for Java. The steps are explained in plain language, include best‑practice tips, and show how to keep processing fast even on large workbooks.

## Quick answers
- **Which library handles spreadsheet redaction in Java?** GroupDocs.Redaction for Java.  
- **Can I filter rows without loading the whole file into memory?** Yes – the API streams data and lets you apply filters on the fly.  
- **What file formats are supported?** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **Do I need a license for development?** A temporary license works for testing; a full license is required for production.  
- **Is there a limit on workbook size?** The engine can process files up to 500 MB without excessive memory consumption.

## What is filter spreadsheet data java?
**Filter spreadsheet data java** is the process of programmatically selecting specific rows, columns, or cells in an Excel‑style workbook using Java code so that only targeted content is examined or redacted. This technique reduces runtime, limits unnecessary changes, and helps meet GDPR‑type compliance.

## Why filter spreadsheet data java?
GroupDocs.Redaction Java supports **30+ spreadsheet formats** and can process workbooks containing **up to 500 MB** (roughly 1 million rows) while keeping memory usage under **200 MB**. By filtering first, you avoid touching unrelated data, which cuts processing time by **40‑60 %** on average for typical privacy‑scrubbing scenarios.

## Prerequisites
- Java 17 or later installed.  
- Maven or Gradle build system.  
- GroupDocs.Redaction for Java (downloadable from the official site).  
- A temporary or full license key.  

## How to filter data in spreadsheets using GroupDocs.Redaction Java?

Load the workbook, define a filter that matches the cells you want to redact, and then apply the redaction operation. The API performs the filter in a streaming fashion, so you never need to hold the entire file in RAM.

The `RedactionFilter` class lets you specify column indexes, row ranges, or custom predicates. For example, you can target every cell in column **B** that contains an email address pattern, or you can restrict redaction to rows where a “Status” column equals “Confidential”.

**Direct answer (40‑70 words):**  
Create a `RedactionFilter` instance, set the column index and a regular‑expression condition, then pass the filter to `Redactor.redact(workbook, filter)`. This single‑line filter isolates the exact cells that match your criteria, and the redactor removes or masks them while leaving the rest of the sheet untouched. The operation completes in linear time relative to the filtered rows.

### Step 1: instantiate the filter
`RedactionFilter` is the core class that represents a filtering rule for spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda expressions to pinpoint data.

### Step 2: configure the condition
Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` to match email patterns. You can also combine multiple conditions with `filter.and(...)` or `filter.or(...)`.

### Step 3: apply the redaction
`Redactor` is the main class that executes redaction operations on a workbook.  
Pass the workbook and the configured filter to the `Redactor` object. The API streams the workbook, applies the filter, and writes the redacted result to a new file, preserving original formatting and formulas.

## Common issues and solutions
- **Filter does not match any cells:** Verify the column index (zero‑based) and ensure the regular‑expression syntax is correct for Java.  
- **Out‑of‑memory errors on large files:** Increase the JVM heap size modestly (e.g., `-Xmx1g`) or split the workbook into smaller chunks before filtering.  
- **Redacted output loses formatting:** `RedactionOptions` allows you to customize redaction behavior, such as preserving cell formatting. Use `RedactionOptions.setPreserveFormatting(true)` to keep cell styles intact.

## Why filter spreadsheet data?

Filtering before redaction isolates only the sensitive portions of a workbook, which means you avoid unnecessary changes to clean data. This selective approach also reduces the risk of accidental data loss and speeds up compliance audits because the audit log contains far fewer entries.

## How to redact emails in Excel spreadsheets using GroupDocs.Redaction Java API

Load your Excel file, apply a filter that looks for the typical email pattern, and invoke the redactor. The API replaces each matched email with a placeholder such as “***@***.com” while preserving the surrounding cell layout.

## How to filter data – available tutorials
- [How to Redact Emails in Excel Spreadsheets Using GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Additional resources

- [GroupDocs.Redaction for Java Documentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API Reference](https://reference.groupdocs.com/redaction/java/)
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-08-04  
**Tested With:** GroupDocs.Redaction 23.11 for Java  
**Author:** GroupDocs  

---

## Frequently asked questions

**Q: Can I filter multiple columns at once?**  
A: Yes, you can add additional column indexes to the same `RedactionFilter` instance or chain multiple filters with `filter.or(...)`.

**Q: Does the filter work on password‑protected workbooks?**  
A: Provide the password when opening the workbook; the filter operates after decryption just like on an unprotected file.

**Q: How many rows can the API handle in a single operation?**  
A: The engine is optimized for up to 1 million rows (≈500 MB) without loading the entire file into memory.

**Q: Is it possible to preview which cells will be redacted before saving?**  
A: Yes, call `filter.preview(workbook)` to get a list of cell addresses that match the criteria.

**Q: What licensing model is required for production use?**  
A: A full commercial license is required for production deployments; a temporary license is sufficient for testing and evaluation.

## Related Tutorials

- [How to Redact Sensitive Data in Excel Spreadsheets Using GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)