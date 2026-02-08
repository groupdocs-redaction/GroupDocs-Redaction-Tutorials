---
date: '2026-02-08'
description: Μάθετε πώς να αποκρύπτετε ευαίσθητα δεδομένα και να διαγράφετε αρχεία
  PDF Java χρησιμοποιώντας το GroupDocs OCR Redaction με το Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Απόκρυψη ευαίσθητων δεδομένων σε PDF με το GroupDocs OCR Redaction
type: docs
url: /el/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

 final answer.# Απόκρυψη Ευαίσθητων Δεδομένων σε PDFs με GroupDocs OCR Redaction

Στο σημερινό ψηφιακό τοπίο, η προστασία των προσωπικών και εμπιστευτικών πληροφοριών είναι κορυφαία προτεραιότητα. Σε αυτό το σεμινάριο, **θα μάθετε πώς να αποκρύπτετε ευαίσθητα δεδομένα** σε αρχεία PDF συνδυάζοντας το GroupDocs Redaction με το Microsoft Azure OCR. Αυτή η προσέγγιση σας παρέχει αξιόπιστη αναγνώριση κειμένου σε σαρωμένες σελίδες και σας επιτρέπει να **αποκρύψετε έγγραφα PDF Java** με ακρίβεια, εξασφαλίζοντας τη συμμόρφωση με τους κανονισμούς απορρήτου.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “mask sensitive data”;** Αντικαθιστά το αναγνωρισμένο εμπιστευτικό κείμενο με έναν υπόδειγμα (π.χ., `[REDACTED]`).  
- **Ποια βιβλιοθήκη διαχειρίζεται το OCR;** Ο συνδετήρας Microsoft Azure OCR, που χρησιμοποιείται μέσω του GroupDocs Redaction.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να αποκρύψω σαρωμένα PDFs;** Ναι—το OCR εξάγει το κρυφό κείμενο πριν εφαρμόσει τις redactions με regex.  
- **Είναι αυτή η λύση μόνο για Java;** Το παράδειγμα βασίζεται σε Java, αλλά το GroupDocs παρέχει παρόμοια APIs για .NET και άλλες πλατφόρμες.

## Τι είναι η Redaction Βασισμένη σε OCR;
Η redaction βασισμένη σε OCR εκτελεί πρώτα Optical Character Recognition σε κάθε σελίδα ενός εγγράφου, μετατρέποντας τις εικόνες κειμένου σε αναζητήσιμες συμβολοσειρές. Μόλις το κείμενο είναι αναζητήσιμο, μπορείτε να εφαρμόσετε κανόνες regular‑expression (regex) για να εντοπίσετε ευαίσθητες πληροφορίες—όπως αριθμούς Social Security, αριθμούς πιστωτικών καρτών ή προσωπικά αναγνωριστικά—και να το αντικαταστήσετε με μια μάσκα όπως **`[REDACTED]`**.

## Γιατί να Χρησιμοποιήσετε το GroupDocs Redaction με Azure OCR;
- **Υψηλή ακρίβεια** σε σαρωμένα PDFs και εικόνες.  
- **Απρόσκοπτη ενσωμάτωση Java** μέσω Maven ή άμεσης λήψης JAR.  
- **Ευέλικτη μηχανή regex** που σας επιτρέπει να ορίσετε προσαρμοσμένα μοτίβα για οποιονδήποτε τύπο δεδομένων.  
- **Κλιμακούμενη** για μεγάλες παρτίδες εγγράφων, με επιλογές για ασύγχρονη επεξεργασία.

## Προαπαιτούμενα
- **Java Development Kit (JDK) 8+** εγκατεστημένο.  
- **Maven** (αν προτιμάτε διαχείριση εξαρτήσεων) ή τη δυνατότητα λήψης JARs χειροκίνητα.  
- **Διαπιστευτήρια Microsoft Azure OCR** (endpoint και κλειδί συνδρομής).  
- Βασικές γνώσεις Java και εξοικείωση με regular expressions.

## Ρύθμιση του GroupDocs Redaction για Java

### Ρύθμιση Maven
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

### Άμεση Λήψη
Αν προτιμάτε χειροκίνητη διαχείριση JAR, κατεβάστε την τελευταία έκδοση από [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση Άδειας
- **Free Trial** – εξερευνήστε όλες τις δυνατότητες χωρίς κόστος.  
- **Temporary License** – επεκτείνετε το χρόνο αξιολόγησης.  
- **Full License** – ξεκλειδώστε δυνατότητες έτοιμες για παραγωγή.

### Βασική Αρχικοποίηση και Ρύθμιση
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Πώς να Αποκρύψετε Ευαίσθητα Δεδομένα με OCR Redaction

### Βήμα 1: Φόρτωση του Εγγράφου με Ρυθμίσεις OCR
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
- **`LoadOptions`** – προεπιλεγμένη φόρτωση· μπορείτε να προσαρμόσετε αν χρειάζεται.  
- **`settings`** – περιέχει τον Azure OCR connector που δημιουργήσατε νωρίτερα.

### Βήμα 2: Ορισμός και Εφαρμογή Regex Redactions
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
- Το μοτίβο `\b\d{3}-\d{2}-\d{4}\b` ταιριάζει με Αριθμούς Κοινωνικής Ασφάλισης των Η.Π.Α.  
- `ReplacementOptions("[REDACTED]")` αντικαθιστά κάθε αντιστοιχία με τη μάσκα, αποτελεσματικά **αποκρύπτοντας ευαίσθητα δεδομένα**.

## Συνηθισμένες Περιπτώσεις Χρήσης για Αποκάλυψη Ευαίσθητων Δεδομένων
1. **Legal Document Management** – απόκρυψη αναγνωριστικών πελατών πριν από την κοινοποίηση προσχεδίων.  
2. **Financial Reporting** – προστασία αριθμών λογαριασμών και ID συναλλαγών.  
3. **Healthcare Records** – συμμόρφωση με το HIPAA αποκρύπτοντας τα αναγνωριστικά των ασθενών.  
4. **Government Publications** – αφαίρεση προσωπικών δεδομένων από δημόσια αρχεία.  
5. **Corporate Contracts** – απόκρυψη ιδιόκτητων όρων κατά τις εξωτερικές αξιολογήσεις.

## Συμβουλές Απόδοσης
- **Βελτιστοποίηση regex** – αποφύγετε υπερβολικά γενικά μοτίβα που αυξάνουν το χρόνο επεξεργασίας.  
- **Διαχείριση μνήμης** – κλείστε άμεσα την παρουσία `Redactor` (το try‑with‑resources το κάνει αυτό αυτόματα).  
- **Ασύγχρονη Εκτέλεση** – για μαζική επεξεργασία, εκτελέστε εργασίες redaction σε ξεχωριστά νήματα ή χρησιμοποιήστε ουρά εργασιών.  

## Επίλυση Προβλημάτων
- **Σφάλμα διαπιστευτηρίων Azure** – ελέγξτε ξανά το endpoint URL και το κλειδί συνδρομής στο `MicrosoftAzureOcrConnector`.  
- **Το έγγραφο δεν φορτώνει** – επαληθεύστε τη διαδρομή του αρχείου και βεβαιωθείτε ότι το PDF δεν είναι προστατευμένο με κωδικό (ή δώστε τον κωδικό μέσω `LoadOptions`).  
- **Δεν εφαρμόζονται redactions** – δοκιμάστε το regex σας με μια απλή συμβολοσειρά πρώτα· χρησιμοποιήστε `Pattern.compile` σε μια μονάδα δοκιμής για να επιβεβαιώσετε τις αντιστοιχίες.

## Συχνές Ερωτήσεις

**Q: Τι είναι η OCR redaction;**  
A: Η OCR redaction χρησιμοποιεί Optical Character Recognition για την εξαγωγή κρυφού κειμένου από εικόνες ή σαρωμένα PDFs, στη συνέχεια εφαρμόζει κανόνες redaction για να καλύψει αυτό το κείμενο.

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs Redaction χωρίς Azure OCR;**  
A: Ναι, αλλά το OCR βελτιώνει δραματικά την ακρίβεια σε σαρωμένα έγγραφα όπου η εγγενής εξαγωγή κειμένου αποτυγχάνει.

**Q: Πώς να διαχειριστώ σύνθετα regex μοτίβα;**  
A: Κατασκευάστε και δοκιμάστε τα σταδιακά, χρησιμοποιώντας την κλάση `Pattern` της Java σε sandbox πριν τα εφαρμόσετε σε μεγάλα έγγραφα.

**Q: Ποια είναι τα τυπικά bottlenecks απόδοσης;**  
A: Μεγάλα PDFs, υπερβολικά σύνθετα regex και συγχρονικές κλήσεις OCR μπορούν να επιβραδύνουν την επεξεργασία· σκεφτείτε επεξεργασία σε παρτίδες και βελτιστοποιημένα μοτίβα.

**Q: Υπάρχει υποστήριξη για ζητήματα υλοποίησης;**  
A: Απόλυτα—επικοινωνήστε μέσω του [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) για βοήθεια από την κοινότητα ή επικοινωνήστε με την υποστήριξη του GroupDocs.

## Πρόσθετοι Πόροι
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Τελευταία Ενημέρωση:** 2026-02-08  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 24.9 (Java)  
**Συγγραφέας:** GroupDocs