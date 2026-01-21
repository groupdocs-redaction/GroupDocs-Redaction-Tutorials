---
date: '2026-01-21'
description: Μάθετε πώς να διαγράψετε κείμενο σε PDF με OCR και να διαγράψετε σαρωμένα
  έγγραφα χρησιμοποιώντας το GroupDocs.Redaction για Java με ενσωμάτωση Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Απόκρυψη PDF με OCR χρησιμοποιώντας GroupDocs & Azure OCR – Οδηγός Java
type: docs
url: /el/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Απόκρυψη PDF με OCR χρησιμοποιώντας GroupDocs & Azure OCR – Οδηγός Java

Σε αυτό το ολοκληρωμένο σεμινάριο θα ανακαλύ με το Microsoft Azure OCR. Είτε εργάζεστε με εγγενή PDF είτε με σαρωμένες εικόνες, αυτός ο οδηγός σας δείχνει πώς να εντετε με ακρίβεια ευDF καιχει διαγραφής;** GroupDocs.Redaction για Java.  
- **Ποια υπηρεσία OCR χρησιμοποιείται;** Συνδετήρας Microsoft Azure OCR.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να αποκρύψω τόσο εγγενή όσο και σαρωμένα PDF;** Ναι – το OCR επιτρέπει τη σκόπιμη διαγραφή σαρωμένων εγγράφων επίσης.

## Τι είναι η «απόκρυψη PDF με OCR»;
Η απόκρυψη PDF με OCR σημαίνει χρήση οπτικής ανατροπή του σκόπιμης διαγραφής (π.χ., regex) για απόκρυψη των πληροφοριών πριν το αρχείο κοινοποιηθεί ή αποθηκευτεί.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction με Azure OCR;
- **Υψηλή ακρίβεια** στις σαρωμένες σελίδες.  
θητούμενα
- Java Development Kit (JDK) 8 ή νεότερο.  
- Maven (ή η δυνατότητα λήψης του JAR χειροκίνητα).  
- Λογαριασμός Microsoft Azure με διαπιστευτήρια OCR.  
- Βασικές γνώσεις Java και εξοικείωση με κανονικές εκφράσεις.

## Ρύθμιση του GroupDocs.Redaction για Java

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
Αν προτιμάτε να μην χρησιμοποιήσετε Maven, κατεβάστε το πιο πρόσφατο JAR από τη σελίδα επίσημης κυκλοφορίας: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση Άδειας
- **Δωρεάν Δοκιμή** – εξερευνήστε τις βασικές λειτουργίες χωρίς δέσμευση.  
- **Προσωρινή Άδεια** – επεκτείνετε τη δοκιμαστική περίοδο για μεγαλύτερα έργα.  
- **Πλήρης Άδεια** – ξεκλειδώνει απεριόριστη χρήση και premium υποστήριξη.

### Βασική Αρχικοποίηση και Ρύθμιση
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Πώς να αποκρύψετε PDF με OCR σε Java

### Βήμα 1: Φόρτωση του Εγγράφου με Ρυθμίσεις OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Παράμετροι**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – διαδρομή προς το στοχευόμενο PDF.  
  - `new LoadOptions()` – προεπιλεγμένη διαμόρφωση φόρτωσης.  
  - `settings` – περιέχει το Azure OCR connector.

### Βήμα 2: Εφαρμογή Regex Σκόπιμης Διαγραφής (π.χ., Αριθμοί Κοινωνικής Ασφάλισης)
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
- **Εξήγηση Regex** – `\b\d{3}-\d{2}-\d{4}\b` ταιριάζει με μοτίβα όπως `123-45-6789`.  
- **ReplacementOptions** – αντικαθιστά το εντοπισμένο κείμενο με `[REDACTED]`.

### Συνηθισμένα Παράπτωμα & Επίλυση Προβλημάτων
- **Διαπιστευτήρια Azure** – ελέγξτε ξανά το κλειδί συνδρομής και το endpoint.  
- **Διαδρομή αρχείου** – βεβαιωθείτε ότι το PDF υπάρχει και η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής.  
- **Απόδοση** – μεγάλα PDF μπορεί να απαιτούν αυξημένο μέγεθος heap ή ασύγχρονη επεξεργασία.

## Πρακτικές Περιπτώσεις Χρήσης για Σκόπιμη Διαγραφή Σαρωμένων Εγγράφων
1. **Νομικές εταιρείες** – απόκρυψη αναγνωριστικών πελατών πριν την κοινοποίηση αρχείων υποθέσεων.  
2. **Οικονομικά ιδρύματα** – κάλυψη αριθμών λογαριασμών σε σαρωμένες καταστάσεις.  
3. **Πάροχοι υγειονομικής περίθαλψης** – προστασία των PHI των ασθενών σε σαρωμένα ιατρικά αρχεία.  
4. **Κυβερνητικές υπηρεσίες** – αφαίρεση προσωπικών δεδομένων από δημόσια PDF αρχείων.  
5. **Επιχειρήσεις** – εξάλειψη ευαίσθητων στοιχείων από συμβάσεις πριν από ελέγχους τρίτων.

## Συμβουλές Απόδοσης
- Κρατήστε τα regex μοτίβα όσο το δυνατόν πιο συγκεκριμένα για μείωση του χρόνου επεξεργασίας.  
- Απελευθερώστε άμεσα την παρουσία `Redactor` (χρησιμοποιήστε try‑with‑resources όπως φαίνεται).  
- Για επεξεργασία παρτίδων, σκεφτείτε την ουρά εργασιών και την εκτέλεσή τους σε παράλληλα νήματα.

## Συχνές Ερωτήσεις

**Ε: Τι είναι η σκόπιμη διαγραφή OCR;**  
Α: Η σκόπιμη διαγραφή OCR χρησιμοποιεί οπτική αναγνώριση χαρακτήρων για εξαγωγή κειμένου από εικόνες ή σαρωμένα PDF, έπειτα εφαρμόζει κανόνες σκόπιμης διαγραφής για μόνιμη αφαίρεση του κειμένου.

**Ε: Μπορώ να χρησιμοποιήσω το GroupDocs.Redaction χωρίς Azure OCR;**  
Α: Ναι, αλλά το OCR βελτιώνει δραματικά την ακρίβεια για σαρωμένα έγγραφα, επιτρέποντάς σας να **αποκρύψετε σαρωμένα έγγραφα** αποτελεσματικά.

**Ε: Πώς να διαχειριστώ σύνθετα regex μοτίβα;**  
Α: Δοκιμάστε τα μοτίβα με δείγμα δεδομένων, χρησιμοποιήστε όρια λέξεων (`\b`) για αποφυγή μερικών αντιστοιχίσεων, και σκεφτείτε το διαχωρισμό μεγάλων εκφράσεων σε πολλαπλές απλούστερες σκόπιμες διαγραφές.

**Ε: Ποια είναι τα τυπικά εμπόδια στην απόδοση;**  
Α: Βαριές κλήσεις OCR σε μεγάλα αρχεία, υπερβολικά γενικά regex, και ανεπαρκής κατανομή μνήμης. Βελτιστοποιήστε ρυθμίζοντας τα regex και κλιμακώντας τους πόρους.

**Ε: Πού μπορώ να λάβω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Δημοσιεύστε ερωτήσεις στο φόρουμ της κοινότητας GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Πρόσθετοι Πόροι
- **Τεκμηρίωση**: https://docs.groupdocs.com/redaction/java/  
- **Αναφορά API**: https://reference.groupdocs.com/redaction/java  
- **Λήψη**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Δωρεάν Υποστήριξη**: https://forum.groupdocs.com/c/redaction/33  
- **Προσωρινή Άδεια**: https://purchase.groupdocs.com/temporary-license/  

---

**Τελευταία Ενημέρωση:** 2026-01-21  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 24.9 for Java  
**Συγγραφέας:** GroupDocs