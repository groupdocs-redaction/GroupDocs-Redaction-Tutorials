---
date: 2026-09-21
description: Μάθετε πώς να rasterize redacted pages ενώ mask sensitive data σε Java
  χρησιμοποιώντας GroupDocs.Redaction. Ο οδηγός step‑by‑step καλύπτει installation,
  licensing, rule creation και best practices.
keywords:
- rasterize redacted pages
- hide personal identifiers
- mask credit card numbers
- mask sensitive data java
- redact pdf java
lastmod: 2026-09-21
og_description: Rasterize redacted pages ενώ mask sensitive data σε Java με GroupDocs.Redaction.
  Ανακαλύψτε πώς να κρύψετε προσωπικά αναγνωριστικά, mask credit card numbers, και
  να συμμορφωθείτε με GDPR σε λίγα λεπτά.
og_image_alt: Guide showing Java code that rasterizes redacted pages and masks sensitive
  data using GroupDocs.Redaction
og_title: Rasterize redacted pages και mask sensitive data σε Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  headline: Rasterize redacted pages and mask sensitive data in Java
  type: TechArticle
- description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  name: Rasterize redacted pages and mask sensitive data in Java
  steps:
  - name: add the Maven dependency
    text: Add the following entry to your `pom.xml` (or the equivalent Gradle snippet).
      This gives you access to the `Redactor` class and all rule‑definition helpers.
  - name: initialize the Redactor with your license
    text: '*Definition anchor:* `Redactor` is the main entry point for all redaction
      operations in GroupDocs.Redaction for Java.'
  - name: define redaction rules
    text: You can combine built‑in detectors with custom regular expressions. The
      example below hides Social Security Numbers, masks credit‑card numbers with
      asterisks, and rasterizes any page that contains a match.
  - name: apply the rules and rasterize pages
    text: '*Definition anchor:* `rasterizePages()` converts the visual content of
      selected pages into bitmap images, preventing any hidden text from being recovered.'
  - name: save the redacted document
    text: '*Pro tip:* Store your rule set in a JSON file and load it at runtime so
      you can update patterns without recompiling.'
  type: HowTo
- questions:
  - answer: Yes, rasterizing entire pages hides any embedded images or scanned text,
      making the content unrecoverable.
    question: Can I redact images that contain text?
  - answer: Create a `RedactionRule` with a regular expression that matches your employee‑ID
      format, then add it to the redactor.
    question: How do I redact custom patterns like employee IDs?
  - answer: Use `RedactionResult.getRedactedObjects()` to iterate over each redacted
      element and generate an audit trail.
    question: Is it possible to keep a log of what was redacted?
  - answer: Absolutely—pass the password when loading the document via `redactor.load(inputStream,
      "password")`.
    question: Does the library support password‑protected documents?
  - answer: Yes, inject the redaction service as a Spring bean and call it from your
      REST controller.
    question: Can I integrate this into a Spring Boot microservice?
  type: FAQPage
tags:
- redaction
- GroupDocs.Redaction
- Java document processing
- data privacy
title: Rasterize redacted pages και mask sensitive data σε Java
type: docs
url: /el/java/getting-started/
weight: 1
---

# Rasterize redacted pages and mask sensitive data in Java

Σε αυτό το ολοκληρωμένο tutorial θα μάθετε πώς να **rasterize redacted pages** και να αποκρύψετε ευαίσθητα δεδομένα που αντιμετωπίζουν καθημερινά οι προγραμματιστές Java. Είτε χρειάζεστε να κρύψετε προσωπικά αναγνωριστικά, να αποκρύψετε αριθμούς πιστωτικών καρτών, είτε να συμμορφωθείτε με GDPR και HIPAA, το GroupDocs.Redaction σας παρέχει ένα εύχρηστο API που αυτοματοποιεί ολόκληρη τη ροή εργασίας. Θα δείτε γιατί η rasterization των σελίδων διατηρεί τη διάταξη, πώς να ορίσετε ευέλικτους κανόνες διαγραφής και ποια βήματα απαιτούνται για να έχετε μια λύση έτοιμη για παραγωγή σε Java 8+.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “mask sensitive data Java”;** Σημαίνει τη χρήση κώδικα Java και GroupDocs.Redaction για αυτόματη εντόπιση και απόκρυψη εμπιστευτικών πληροφοριών μέσα σε έγγραφα.  
- **Χρειάζομαι άδεια;** Ναι, απαιτείται έγκυρη άδεια GroupDocs.Redaction για παραγωγική χρήση.  
- **Ποιους τύπους εγγράφων υποστηρίζονται;** PDFs, DOCX, PPTX, XLSX, εικόνες και πολλές άλλες κοινές μορφές.  
- **Μπορώ να επεξεργαστώ έγγραφα μαζικά;** Απόλυτα—οι κανόνες διαγραφής μπορούν να εφαρμοστούν σε μεγάλα batch μέσω ενός απλού βρόχου.  
- **Είναι η βιβλιοθήκη συμβατή με Java 8+;** Ναι, λειτουργεί με Java 8 και νεότερες εκδόσεις.  

## Τι είναι η “mask sensitive data Java”;
Η απόκρυψη ευαίσθητων δεδομένων σε Java σημαίνει προγραμματιστική εντόπιση προσωπικών ή εμπιστευτικών πληροφοριών μέσα σε έγγραφα και απόκρυψή τους. Χρησιμοποιώντας το GroupDocs.Redaction, οι προγραμματιστές μπορούν να ορίσουν μοτίβα ή ανιχνευτές που αντικαθιστούν αυτόματα τα δεδομένα με αστερίσκους, μαύρα κουτιά ή rasterized εικόνες, διασφαλίζοντας ότι η αρχική διάταξη παραμένει αμετάβλητη ενώ προστατεύεται η ιδιωτικότητα. Η κλάση `Redactor` φορτώνει ένα έγγραφο, εφαρμόζει τους κανόνες διαγραφής και γράφει το διαγραμμένο αποτέλεσμα.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για απόκρυψη;
Το GroupDocs.Redaction προσφέρει ενσωματωμένους ανιχνευτές με 99,7 % ακρίβεια για SSN, αριθμούς πιστωτικών καρτών και email, και μπορεί να rasterize σελίδες ώστε το κρυφό περιεχόμενο να μην μπορεί να ανακτηθεί. Υποστηρίζει πάνω από 50 μορφές, λειτουργεί σε Java 8+, και επεξεργάζεται μεγάλα αρχεία αποδοτικά, βοηθώντας σας να τηρήσετε τις απαιτήσεις GDPR, HIPAA και PCI‑DSS.

## Προαπαιτούμενα
- Java 8 ή νεότερη έκδοση εγκατεστημένη στη μηχανή ανάπτυξής σας.  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  
- Αρχείο άδειας GroupDocs.Redaction (προσωρινή άδεια διαθέσιμη για αξιολόγηση).  

## Πώς να αποκρύψετε ευαίσθητα δεδομένα σε Java
Για να αποκρύψετε ευαίσθητα δεδομένα σε Java, δημιουργήστε μια παρουσία `Redactor`, προσθέστε τους απαιτούμενους κανόνες διαγραφής, ενεργοποιήστε τη rasterization για τις σελίδες που περιέχουν αντιστοιχίες και αποθηκεύστε το έγγραφο. Αυτή η ροή εργασίας μονής διέλευσης απλοποιεί την υλοποίηση και διασφαλίζει ότι τόσο η διαγραφή όσο και η οπτική προστασία εφαρμόζονται σταθερά.

### Βήμα 1: προσθέστε την εξάρτηση Maven
Προσθέστε την παρακάτω καταχώρηση στο `pom.xml` σας (ή το αντίστοιχο απόσπασμα Gradle). Αυτό σας δίνει πρόσβαση στην κλάση `Redactor` και σε όλα τα βοηθητικά εργαλεία ορισμού κανόνων.

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-redaction</artifactId>
    <version>3.0</version>
</dependency>
```

### Βήμα 2: αρχικοποιήστε το Redactor με την άδειά σας
```java
Redactor redactor = new Redactor();
redactor.setLicense("path/to/license.lic");
```
*Definition anchor:* `Redactor` είναι το κύριο σημείο εισόδου για όλες τις λειτουργίες διαγραφής στο GroupDocs.Redaction για Java.

### Βήμα 3: ορίστε κανόνες διαγραφής
Μπορείτε να συνδυάσετε ενσωματωμένους ανιχνευτές με προσαρμοσμένες κανονικές εκφράσεις. Το παρακάτω παράδειγμα κρύβει Αριθμούς Κοινωνικής Ασφάλισης, αποκρύπτει αριθμούς πιστωτικών καρτών με αστερίσκους και rasterizes οποιαδήποτε σελίδα περιέχει αντιστοιχία.

```java
redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.SSN())
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withPattern("\\b\\d{4}[- ]?\\d{4}[- ]?\\d{4}[- ]?\\d{4}\\b")
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.PATTERN("\\bCONFIDENTIAL\\b"))
    .withRedactionType(RedactionType.RASTERIZE));
```

### Βήμα 4: εφαρμόστε τους κανόνες και rasterize τις σελίδες
```java
redactor.load("input.pdf");
redactor.applyRules();               // runs all defined rules
redactor.rasterizePages();           // converts matched pages to images
```
*Definition anchor:* `rasterizePages()` μετατρέπει το οπτικό περιεχόμενο των επιλεγμένων σελίδων σε bitmap εικόνες, εμποδίζοντας την ανάκτηση κρυφού κειμένου.

### Βήμα 5: αποθηκεύστε το διαγραμμένο έγγραφο
```java
redactor.save("output.pdf");
redactor.close();    // releases all resources
```
*Pro tip:* Αποθηκεύστε το σύνολο κανόνων σας σε αρχείο JSON και φορτώστε το κατά το runtime ώστε να μπορείτε να ενημερώνετε τα μοτίβα χωρίς επαναμεταγλώττιση.

## Κοινά προβλήματα & αντιμετώπιση σφαλμάτων

- **Rule not triggering** – Επαληθεύστε ότι η κανονική έκφρασή σας είναι σωστή και ότι η ευαισθησία πεζών‑κεφαλαίων του ανιχνευτή ταιριάζει με τα δεδομένα προέλευσης.  
- **Performance lag on large PDFs** – Ενεργοποιήστε τη λειτουργία streaming με `redactor.setUseMemoryStream(false)` για να διατηρήσετε τη χρήση μνήμης χαμηλή.  
- **Output file corrupted** – Πάντα κλείνετε την παρουσία `Redactor` ή χρησιμοποιήστε μπλοκ try‑with‑resources για να διασφαλίσετε ότι τα streams αδειάζονται.  

## Συχνές ερωτήσεις

**Q: Μπορώ να διαγράψω εικόνες που περιέχουν κείμενο;**  
A: Ναι, η rasterization ολόκληρων σελίδων κρύβει οποιεσδήποτε ενσωματωμένες εικόνες ή σαρωμένο κείμενο, καθιστώντας το περιεχόμενο μη ανακτήσιμο.

**Q: Πώς διαγράφω προσαρμοσμένα μοτίβα όπως τα IDs υπαλλήλων;**  
A: Δημιουργήστε ένα `RedactionRule` με κανονική έκφραση που ταιριάζει στη μορφή του employee‑ID σας, και προσθέστε το στον redactor.

**Q: Είναι δυνατόν να διατηρήσω αρχείο καταγραφής του τι διαγράφηκε;**  
A: Χρησιμοποιήστε `RedactionResult.getRedactedObjects()` για να διατρέξετε κάθε διαγραμμένο στοιχείο και να δημιουργήσετε ένα audit trail.

**Q: Υποστηρίζει η βιβλιοθήκη έγγραφα προστατευμένα με κωδικό;**  
A: Απόλυτα—περάστε τον κωδικό όταν φορτώνετε το έγγραφο μέσω `redactor.load(inputStream, "password")`.

**Q: Μπορώ να ενσωματώσω αυτό σε microservice Spring Boot;**  
A: Ναι, ενσωματώστε την υπηρεσία διαγραφής ως Spring bean και καλέστε την από τον REST controller σας.

## Πρόσθετοι πόροι

- [Τεκμηρίωση GroupDocs.Redaction για Java](https://docs.groupdocs.com/redaction/java/)
- [Αναφορά API GroupDocs.Redaction για Java](https://reference.groupdocs.com/redaction/java/)
- [Λήψη GroupDocs.Redaction για Java](https://releases.groupdocs.com/redaction/java/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

## Διαθέσιμα μαθήματα

### [Υλοποίηση Διαγραφής Java με GroupDocs.Redaction: Ένας Πλήρης Οδηγός για Προγραμματιστές](./implement-java-redaction-groupdocs-redaction-guide/)
Μάθετε πώς να εφαρμόσετε αποτελεσματική διαγραφή σε Java χρησιμοποιώντας το GroupDocs.Redaction. Προστατέψτε ευαίσθητες πληροφορίες απρόσκοπτα διατηρώντας την ακεραιότητα του εγγράφου.

### [Οδηγός Διαγραφής Java: Αποτελεσματική Διαχείριση Εγγράφων με GroupDocs.Redaction](./java-redaction-groupdocs-efficient-document-setup/)
Μάθετε πώς να ρυθμίσετε και να διαχειριστείτε αποδοτικά τις διαγραφές εγγράφων σε Java με το GroupDocs.Redaction. Ιδανικό για την προστασία ευαίσθητων πληροφοριών.

### [Μάθημα Διαγραφής Java: Χρήση του API GroupDocs.Redaction για Ασφάλεια Εγγράφων](./java-groupdocs-redaction-tutorial/)
Μάθετε πώς να χρησιμοποιήσετε τη βιβλιοθήκη GroupDocs.Redaction για Java ώστε να διαγράψετε ευαίσθητες πληροφορίες από έγγραφα. Αυτός ο ολοκληρωμένος οδηγός καλύπτει εγκατάσταση, υλοποίηση και βέλτιστες πρακτικές.

### [Αποκτήστε τον Έλεγχο της Διαγραφής Εγγράφων σε Java με GroupDocs.Redaction: Οδηγός Βήμα‑Βήμα](./master-document-redaction-java-groupdocs/)
Μάθετε να διαγράφετε ευαίσθητα δεδομένα από PDFs και αρχεία Word χρησιμοποιώντας το GroupDocs.Redaction για Java. Εφαρμόστε ακριβείς διαγραφές φράσεων, rasterize έγγραφα για ιδιωτικότητα και εξασφαλίστε συμμόρφωση χωρίς κόπο.

---

**Τελευταία Ενημέρωση:** 2026-09-21  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 3.0 (Java)  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να Rasterize PDF με GroupDocs.Redaction Java – Μαθήματα](/redaction/java/rasterization-options/)
- [Πώς να rasterize PDF σε αποχρώσεις του γκρι με GroupDocs.Redaction Java – Ασφαλή και Βελτιστοποιημένα Έγγραφα](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Groupdocs Redaction Java Text Redaction Rasterize Pdf](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/)