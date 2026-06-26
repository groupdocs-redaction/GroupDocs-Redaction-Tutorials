---
date: '2026-06-26'
description: Μάθετε πώς να εξάγετε κείμενο από σκαναρισμένο PDF και να αποκρύπτετε
  ευαίσθητα δεδομένα χρησιμοποιώντας το GroupDocs OCR Redaction με Azure OCR. Αποκρύψτε
  τον social security number και αντικαταστήστε αποτελεσματικά τις εμπιστευτικές πληροφορίες
  PDF.
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
title: Εξαγωγή κειμένου από σκαναρισμένο PDF – Απόκρυψη δεδομένων με GroupDocs OCR
type: docs
url: /el/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Απόσπασμα Κειμένου από Σαρωμένο PDF – Απόκρυψη Δεδομένων με GroupDocs OCR

Στον σημερινό κόσμο που βασίζεται στα δεδομένα, η **εξαγωγή κειμένου από σαρωμένα PDF** αρχεία και η απόκρυψη εμπιστευτικών πληροφοριών είναι ένα αδιαπραγμάτευτο βήμα συμμόρφωσης. Αυτό το εκπαιδευτικό υλικό σας καθοδηγεί στη χρήση του GroupDocs Redaction μαζί με το Microsoft Azure OCR για αξιόπιστη αναγνώριση κρυφού κειμένου σε σαρωμένες σελίδες και την αντικατάστασή του με έναν ασφαλή υπόδειγμα όπως **`[REDACTED]`**. Θα δείτε γιατί αυτός ο συνδυασμός είναι γρήγορος, ακριβής και έτοιμος για εργασίες παραγωγικού επιπέδου.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “απόκρυψη ευαίσθητων δεδομένων”;** Αντικαθιστά το αναγνωρισμένο εμπιστευτικό κείμενο με έναν υπόδειγμα (π.χ., `[REDACTED]`).  
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR;** Ο σύνδεσμος Microsoft Azure OCR, που χρησιμοποιείται μέσω του GroupDocs Redaction.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να επεξεργαστώ σαρωμένα PDF;** Ναι—το OCR εξάγει το κρυφό κείμενο πριν εφαρμόσει τις επεμβάσεις regex.  
- **Είναι αυτή η λύση μόνο για Java;** Το παράδειγμα είναι βασισμένο σε Java, αλλά το GroupDocs παρέχει παρόμοια API για .NET και άλλες πλατφόρμες.

## Τι είναι η Επιδιόρθωση Βασισμένη σε OCR;
Η Επιδιόρθωση Βασισμένη σε OCR πρώτα εκτελεί OCR σε κάθε σελίδα, μετατρέποντας τις εικόνες σε αναζητήσιμο κείμενο, και στη συνέχεια εφαρμόζει πρότυπα regex για να αντικαταστήσει τα ταιριάσματα με μια μάσκα όπως `[REDACTED]`. Αυτή η διαδικασία δύο βημάτων σας επιτρέπει να κρύψετε αξιόπιστα προσωπικά δεδομένα ακόμη και σε σαρωμένα PDF, διασφαλίζοντας ότι οποιεσδήποτε ευαίσθητες αλφαριθμητικές ακολουθίες αφαιρούνται πριν το έγγραφο μοιραστεί ή αρχειοθετηθεί.

## Γιατί να Χρησιμοποιήσετε το GroupDocs Redaction με Azure OCR;
Θα πρέπει να χρησιμοποιήσετε το GroupDocs Redaction με Azure OCR επειδή παρέχει **>98 % ακρίβεια OCR σε τυπωμένο κείμενο**, υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου**, και μπορεί να επεξεργαστεί **PDF πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη**, εξασφαλίζοντας γρήγορη, κλιμακώσιμη επεξεργασία για συμμόρφωση. Η λύση επίσης **κλιμακώνεται ώστε να επεξεργάζεται ένα PDF 1.000 σελίδων σε λιγότερο από 2 λεπτά σε διακομιστή 8 πυρήνων**, καθιστώντας πρακτικές τις εργασίες παρτίδας.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+** εγκατεστημένο.  
- **Maven** (αν προτιμάτε διαχείριση εξαρτήσεων) ή η δυνατότητα λήψης των JAR χειροκίνητα.  
- **Διαπιστευτήρια Microsoft Azure OCR** (endpoint και κλειδί συνδρομής).  
- Βασικές γνώσεις Java και εξοικείωση με κανονικές εκφράσεις.

## Ρύθμιση του GroupDocs Redaction για Java

### Ρύθμιση Maven
Προσθέστε το αποθετήριο GroupDocs και την εξάρτηση στο `pom.xml` σας:

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

### Άμεση Λήψη
Αν προτιμάτε χειροκίνητη διαχείριση JAR, κατεβάστε την πιο πρόσφατη έκδοση από [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση Άδειας
- **Δωρεάν Δοκιμή** – εξερευνήστε όλες τις λειτουργίες χωρίς κόστος.  
- **Προσωρινή Άδεια** – επεκτείνετε το χρόνο αξιολόγησης.  
- **Πλήρης Άδεια** – ξεκλειδώστε δυνατότητες έτοιμες για παραγωγή.

### Βασική Αρχικοποίηση και Ρύθμιση
Η κλάση `Redactor` είναι η κύρια μηχανή που εκτελεί εξαγωγή OCR και εφαρμόζει κανόνες επεξαίρεσης σε έγγραφα PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Πώς να Αποκρύψετε Ευαίσθητα Δεδομένα με OCR Redaction
Η απόκρυψη ευαίσθητων δεδομένων με OCR Redaction περιλαμβάνει τη φόρτωση του PDF με ρυθμίσεις Azure OCR, τον ορισμό προτύπων regex για τα δεδομένα που θέλετε να κρύψετε, και την κλήση του Redactor για να αντικαταστήσει κάθε αντιστοιχία με έναν υπόδειγμα όπως `[REDACTED]`. Η βιβλιοθήκη διαχειρίζεται το OCR, την αντιστοίχιση προτύπων και την επανεγγραφή PDF σε μια ενιαία ροή εργασίας.

### Βήμα 1: Φόρτωση του Εγγράφου με Ρυθμίσεις OCR
`LoadOptions` ρυθμίζει πώς το GroupDocs φορτώνει ένα αρχείο, επιτρέποντάς σας να περάσετε συνδέσμους OCR όπως το Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – αντικαταστήστε με τη διαδρομή του PDF σας.  
- **`settings`** – περιέχει τον σύνδεσμο Azure OCR που δημιουργήσατε προηγουμένως.

### Βήμα 2: Ορισμός και Εφαρμογή Regex Επεξεργασιών
`ReplacementOptions` καθορίζει το κείμενο αντικατάστασης που θα αντικαταστήσει κάθε αντιστοιχία regex κατά την επεξαίρεση.  
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
- Το πρότυπο `\b\d{3}-\d{2}-\d{4}\b` ταιριάζει με Αριθμούς Κοινωνικής Ασφάλισης των ΗΠΑ.  
- `ReplacementOptions("[REDACTED]")` αντικαθιστά κάθε αντιστοιχία με τη μάσκα, αποτελεσματικά **αποκρύπτοντας ευαίσθητα δεδομένα**.

## Συνηθισμένες Περιπτώσεις Χρήσης για Απόκρυψη Ευαίσθητων Δεδομένων
1. **Διαχείριση Νομικών Εγγράφων** – απόκρυψη αναγνωριστικών πελατών πριν από την κοινοποίηση προτύπων.  
2. **Οικονομική Αναφορά** – προστασία αριθμών λογαριασμών και ταυτοτήτων συναλλαγών.  
3. **Ιατρικά Αρχεία** – συμμόρφωση με το HIPAA μέσω επεξαίρεσης αναγνωριστικών ασθενών.  
4. **Κυβερνητικές Εκδόσεις** – αφαίρεση προσωπικών δεδομένων από δημόσια αρχεία.  
5. **Εταιρικές Συμβάσεις** – απόκρυψη ιδιόκτητων όρων κατά τις εξωτερικές αξιολογήσεις.

## Συμβουλές Απόδοσης
- **Βελτιστοποίηση regex** – αποφύγετε υπερβολικά γενικά πρότυπα που αυξάνουν τον χρόνο επεξεργασίας· καλά σχεδιασμένες εκφράσεις μπορούν να μειώσουν το χρόνο εκτέλεσης έως και 40 %.  
- **Διαχείριση μνήμης** – κλείστε άμεσα την παρουσία `Redactor` (το try‑with‑resources το κάνει αυτό αυτόματα).  
- **Ασύγχρονη Εκτέλεση** – για μαζική επεξεργασία, εκτελέστε εργασίες επεξαίρεσης σε ξεχωριστά νήματα ή χρησιμοποιήστε ουρά εργασιών για να διατηρήσετε το UI ανταποκρινόμενο.

## Επίλυση Προβλημάτων
- **Σφάλμα διαπιστευτηρίων Azure** – ελέγξτε ξανά το URL του endpoint και το κλειδί συνδρομής στο `MicrosoftAzureOcrConnector`.  
- **Το έγγραφο δεν φορτώνει** – επαληθεύστε τη διαδρομή του αρχείου και βεβαιωθείτε ότι το PDF δεν είναι προστατευμένο με κωδικό (ή παρέχετε τον κωδικό μέσω `LoadOptions`).  
- **Δεν εφαρμόστηκαν επεξεργασίες** – δοκιμάστε το regex σας με μια απλή συμβολοσειρά πρώτα· χρησιμοποιήστε `Pattern.compile` σε μονάδα ελέγχου για να επιβεβαιώσετε τις αντιστοιχίες.

## Συχνές Ερωτήσεις

**Q: Τι είναι η επεξαίρεση OCR;**  
A: Η επεξαίρεση OCR χρησιμοποιεί την Οπτική Αναγνώριση Χαρακτήρων (OCR) για την εξαγωγή κρυφού κειμένου από εικόνες ή σαρωμένα PDF, και στη συνέχεια εφαρμόζει κανόνες επεξαίρεσης για να καλύψει αυτό το κείμενο.

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs Redaction χωρίς Azure OCR;**  
A: Ναι, αλλά το OCR βελτιώνει δραματικά την ακρίβεια σε σαρωμένα έγγραφα όπου η εγγενής εξαγωγή κειμένου αποτυγχάνει.

**Q: Πώς να διαχειριστώ πολύπλοκα πρότυπα regex;**  
A: Κατασκευάστε και δοκιμάστε τα σταδιακά, χρησιμοποιώντας την κλάση `Pattern` της Java σε περιβάλλον sandbox πριν τα εφαρμόσετε σε μεγάλα έγγραφα.

**Q: Ποια είναι τα τυπικά σημεία συμφόρησης στην απόδοση;**  
A: Μεγάλα PDF, υπερβολικά πολύπλοκα regex και συγχρονικές κλήσεις OCR μπορούν να επιβραδύνουν την επεξεργασία· σκεφτείτε την επεξεργασία παρτίδας και βελτιστοποιημένα πρότυπα.

**Q: Διατίθεται υποστήριξη για ζητήματα υλοποίησης;**  
A: Απόλυτα—επικοινωνήστε μέσω του [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) για βοήθεια από την κοινότητα ή επικοινωνήστε με την υποστήριξη του GroupDocs.

## Πρόσθετοι Πόροι
- **Τεκμηρίωση**: https://docs.groupdocs.com/redaction/java/  
- **Αναφορά API**: https://reference.groupdocs.com/redaction/java  
- **Λήψη**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Δωρεάν Υποστήριξη**: https://forum.groupdocs.com/c/redaction/33  
- **Προσωρινή Άδεια**: https://purchase.groupdocs.com/temporary-license/

---

**Τελευταία Ενημέρωση:** 2026-06-26  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 24.9 (Java)  
**Συγγραφέας:** GroupDocs  

---

## Σχετικές Οδηγίες

- [Ασφαλής Επεξαίρεση PDF με OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Πώς να Επεξεργαστείτε Κείμενο με το GroupDocs.Redaction για Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Απόκρυψη Ευαίσθητων Δεδομένων Java – Επεξαίρεση Προσωπικών Πληροφοριών με το GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)