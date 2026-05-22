---
date: '2026-05-22'
description: Μάθετε πώς να προσθέσετε suffix filename java χρησιμοποιώντας την GroupDocs
  Maven dependency ενώ redacting documents. Περιλαμβάνει streaming load, annotation
  deletion, και save options.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
title: Προσθήκη suffix filename java με GroupDocs Maven
type: docs
url: /el/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Προσθήκη καταλήξεως στο όνομα αρχείου java με GroupDocs Maven

Η διαγραφή εμπιστευτικών δεδομένων είναι μόνο το ήμισυ του αγώνα—πρέπει επίσης να διασφαλίσετε ότι το αποθηκευμένο αρχείο υποδεικνύει σαφώς ότι έχει υποστεί επεξεργασία. **Η χρήση της εξάρτησης GroupDocs Maven καθιστά αυτό απλό**, επιτρέποντάς σας να προσθέσετε μια καταλήξη στο όνομα του αρχείου εξόδου με λίγες μόνο γραμμές κώδικα. Η μέθοδος **add suffix filename java** είναι μια ρύθμιση μίας γραμμής που επισημαίνει αμέσως τα διαγραμμένα αρχεία σας, βοηθώντας σας να παραμείνετε συμμορφωμένοι και έτοιμοι για έλεγχο.

## Γρήγορες Απαντήσεις
- **Τι κάνει η “προσθήκη καταλήξεως στο όνομα αρχείου”;**  
  Προσθέτει μια προσαρμοσμένη καταλήξη (π.χ., “_redacted”) στο όνομα του αρχείου εξόδου ώστε να μπορείτε άμεσα να αναγνωρίζετε τα επεξεργασμένα αρχεία.  
- **Μπορώ να φορτώσω ένα έγγραφο από ροή;**  
  Ναι—το GroupDocs.Redaction υποστηρίζει φόρτωση από οποιοδήποτε `InputStream`, ιδανικό για αποθήκευση στο cloud ή επεξεργασία στη μνήμη.  
- **Χρειάζομαι άδεια για αυτή τη λειτουργία;**  
  Μια δωρεάν δοκιμή λειτουργεί για βασική διαγραφή· μια προσωρινή ή πλήρης άδεια ξεκλειδώνει όλες τις προχωρημένες επιλογές, συμπεριλαμβανομένης της διαχείρισης καταλήξεων.  
- **Ποιες μορφές υποστηρίζονται;**  
  Η βιβλιοθήκη διαχειρίζεται DOCX, PDF, PPTX, XLSX και πολλές άλλες.  
- **Απαιτείται rasterization για έξοδο PDF;**  
  Η rasterization είναι προαιρετική· ενεργοποιήστε την όταν χρειάζεται να επίπεδοποιήσετε το έγγραφο για επιπλέον ασφάλεια.

## Τι είναι η προσθήκη καταλήξεως στο όνομα αρχείου java;
Η τεχνική **add suffix filename java** προσθέτει μια προ‑ορισμένη συμβολοσειρά στο όνομα του αρχείου κατά τη λειτουργία αποθήκευσης, επισημαίνοντας σαφώς το έγγραφο ως διαγραμμένο. Αυτή η απλή σύμβαση αποτρέπει την τυχαία διανομή των αρχικών, αδιάγραπτων αρχείων και ενσωματώνεται ομαλά σε αυτοματοποιημένες γραμμές παραγωγής.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για αυτήν την εργασία;
Το GroupDocs.Redaction παρέχει ένα ευέλικτο Java API που σας επιτρέπει να συνδυάσετε ενέργειες διαγραφής με επιλογές διαχείρισης αρχείων—όπως **add suffix filename java**—σε λίγες μόνο γραμμές κώδικα. Το SDK υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί έγγραφα εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, προσφέροντας ταχύτητα και μικρό αποτύπωμα μνήμης.

## Προαπαιτούμενα
- **Java Development Kit (JDK):** Έκδοση 8 ή νεότερη.  
- **GroupDocs.Redaction Library:** Βασική βιβλιοθήκη για εργασίες διαγραφής.  
- **IDE:** IntelliJ IDEA, Eclipse ή οποιοσδήποτε επεξεργαστής συμβατός με Java.  
- **Maven:** Για διαχείριση εξαρτήσεων.  

### Προαπαιτούμενες Γνώσεις
Η εξοικείωση με το Java I/O και τις βασικές έννοιες αντικειμενοστραφούς προγραμματισμού θα κάνει τα παραδείγματα πιο εύκολα στην παρακολούθηση.

## Ρύθμιση του GroupDocs.Redaction για Java
### Ρύθμιση Maven
Συμπεριλάβετε την παρακάτω διαμόρφωση στο αρχείο `pom.xml` για πρόσβαση στις βιβλιοθήκες GroupDocs μέσω Maven:

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
Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση Άδειας
1. **Free Trial:** Πρόσβαση στη βασική λειτουργικότητα χωρίς περιορισμούς.  
2. **Temporary License:** Απόκτηση προσωρινής άδειας για εξερεύνηση προχωρημένων λειτουργιών.  
3. **Purchase:** Για μακροπρόθεσμη χρήση, σκεφτείτε την αγορά πλήρους άδειας.

#### Βασική Αρχικοποίηση και Ρύθμιση
Αρχικοποιήστε το έργο σας προσθέτοντας τις απαραίτητες εισαγωγές:

```java
import com.groupdocs.redaction.Redactor;
```

Με αυτή τη ρύθμιση, είστε έτοιμοι να υλοποιήσετε λειτουργίες διαγραφής εγγράφων.

## Οδηγός Υλοποίησης

### Χαρακτηριστικό 1: Φόρτωση Εγγράφου από Ροή
**Επισκόπηση:** Μάθετε πώς να φορτώνετε έγγραφα σε ένα `InputStream` για επεξεργασία.

#### Υλοποίηση Βήμα-Βήμα
##### Βήμα 1.1: Δημιουργία InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Γιατί:** Η χρήση του `InputStream` σας επιτρέπει να διαχειρίζεστε έγγραφα αποθηκευμένα σε διάφορες τοποθεσίες—cloud buckets, βάσεις δεδομένων ή buffers στη μνήμη—χωρίς να τα γράφετε πρώτα στο δίσκο. Αυτή η προσέγγιση είναι απαραίτητη όταν χρειάζεται να **load document from stream** σε αρχιτεκτονικές μικρο‑υπηρεσιών.

### Χαρακτηριστικό 2: Εφαρμογή Διαγραφής Σχόλιας (Annotation Deletion Redaction)
**Επισκόπηση:** Αφαιρέστε τις σημειώσεις (annotations) από το έγγραφό σας χρησιμοποιώντας το `DeleteAnnotationRedaction`.

#### Υλοποίηση Βήμα-Βήμα
##### Βήμα 2.1: Εφαρμογή DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Γιατί:** Αυτό το βήμα εξασφαλίζει ότι οποιεσδήποτε ευαίσθητες σημειώσεις (σχόλια, επισημάνσεις ή κρυφές σημειώσεις) αφαιρούνται από το έγγραφο, ενισχύοντας την ιδιωτικότητα και τη συμμόρφωση.

### Χαρακτηριστικό 3: Αποθήκευση Εγγράφου με Επιλογές
**Επισκόπηση:** Μάθετε πώς να αποθηκεύετε το επεξεργασμένο έγγραφό σας με συγκεκριμένες επιλογές όπως rasterization και **add suffix filename java**.

#### Υλοποίηση Βήμα-Βήμα
##### Βήμα 3.1: Διαμόρφωση SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Γιατί:** Η προσαρμογή των επιλογών αποθήκευσης επιτρέπει ευέλικτες μορφές εξόδου και συμβάσεις ονοματοδοσίας. Η ενεργοποίηση του `setAddSuffix(true)` **προσθέτει καταλήξη στο όνομα αρχείου**, καθιστώντας σαφές ότι το αρχείο έχει διαγραφεί.

## Πώς να προσθέσετε καταλήξη στο όνομα αρχείου java κατά την αποθήκευση ενός εγγράφου;
`Redactor` είναι η κύρια κλάση στο GroupDocs.Redaction που φορτώνει ένα έγγραφο και εφαρμόζει λειτουργίες διαγραφής.  
`setAddSuffix` είναι μια μέθοδος του `SaveOptions` που ενεργοποιεί την αυτόματη προσθήκη καταλήξεως στο όνομα του αρχείου εξόδου.  

Φορτώστε την παρουσία σας `Redactor`, εφαρμόστε τις επιθυμητές διαγραφές, στη συνέχεια καλέστε `save()` με `SaveOptions` όπου το `setAddSuffix(true)` είναι ενεργοποιημένο. Αυτή η μοναδική ρύθμιση προσθέτει αυτόματα “_redacted” (ή την προεπιλεγμένη καταλήξη) στο όνομα του αρχείου, εξαλείφοντας την χειροκίνητη μετονομασία και μειώνοντας το ανθρώπινο σφάλμα. Η λειτουργία ολοκληρώνεται σε χρόνο O(n) σε σχέση με το μέγεθος του εγγράφου και λειτουργεί για όλες τις υποστηριζόμενες μορφές.

## Επισκόπηση Εξάρτησης groupdocs Maven
Η **groupdocs maven dependency** φέρνει ολόκληρο το Redaction SDK στο έργο σας με μία μόνο καταχώρηση `<dependency>`. Διαχειρίζεται τις διαμεταβιβάσιμες εξαρτήσεις, διατηρεί τις βιβλιοθήκες ενημερωμένες και απλοποιεί την αυτοματοποίηση της κατασκευής. Με τη δήλωση της εξάρτησης στο `pom.xml`, αποφεύγετε τη χειροκίνητη διαχείριση JAR και εξασφαλίζετε συμβατότητα με τις πιο πρόσφατες ενημερώσεις ασφαλείας.

## Γιατί η Προσθήκη Καταλήξεως Είναι Σημαντική
Η προσθήκη καταλήξεως παρέχει άμεση οπτική επιβεβαίωση ότι ένα έγγραφο έχει υποστεί επεξεργασία, κάτι που είναι απαραίτητο για τα ίχνη ελέγχου, τις αυτοματοποιημένες ροές εργασίας και τη συμμόρφωση με κανονισμούς σε διάφορους κλάδους.

- **Αξιοπιστία Ελέγχου:** Οι ομάδες μπορούν άμεσα να εντοπίζουν ποια αρχεία είναι ασφαλή για διανομή.  
- **Αυτοματοποίηση:** Τα σενάρια μπορούν να φιλτράρουν αρχεία με βάση την καταλήξη, αποτρέποντας τυχαία επεξεργασία των αρχικών εγγράφων.  
- **Συμμόρφωση:** Πολλοί κανονισμοί απαιτούν σαφή σήμανση των εξαγορασμένων εγγράφων.

## Πρακτικές Εφαρμογές
Εξερευνήστε αυτές τις πραγματικές περιπτώσεις χρήσης:

1. **Διαγραφή Νομικών Εγγράφων:** Ασφαλίστε συμβάσεις πριν τη διανομή σε πελάτες.  
2. **Διαχείριση Ιατρικών Αρχείων:** Προστατέψτε τα αναγνωριστικά των ασθενών διατηρώντας τα κλινικά δεδομένα.  
3. **Οικονομική Αναφορά:** Κρατήστε ευαίσθητους αριθμούς εμπιστευτικούς κατά τις εξωτερικές ελέγχους.  
4. **Ενσωμάτωση CRM:** Αυτόματη διαγραφή δεδομένων πελατών πριν την εξαγωγή σε εργαλεία τρίτων.  
5. **Εργαλεία Συνεργασίας:** Διασφαλίστε ότι τα κοινόχρηστα προσχέδια δεν εκθέτουν κρυφά σχόλια ή μεταδεδομένα.

## Σκέψεις Απόδοσης
### Βελτιστοποίηση Απόδοσης
- Χρησιμοποιήστε streaming (`load document from stream`) για να αποφύγετε τη φόρτωση ολόκληρων αρχείων στη μνήμη.  
- Κλείστε γρήγορα τις παρουσίες `Redactor` για να ελευθερώσετε πόρους.

### Οδηγίες Χρήσης Πόρων
- Παρακολουθήστε την CPU και τη μνήμη κατά τις παρτίδες εκτέλεσης.  
- Προτιμήστε `ByteArrayOutputStream` για αποθηκεύσεις στη μνήμη όταν εργάζεστε με μικρά αρχεία.

### Καλές Πρακτικές για Διαχείριση Μνήμης Java
- Επαναχρησιμοποιήστε αντικείμενα `Redactor` όταν επεξεργάζεστε πολλά αρχεία του ίδιου τύπου.  
- Καλείτε `close()` σε ένα μπλοκ `try‑with‑resources` για να αποτρέψετε διαρροές.

## Συνηθισμένα Προβλήματα και Λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Η καταλήξη δεν εμφανίζεται** | `setAddSuffix(false)` ή έλλειψη κλήσης | Βεβαιωθείτε ότι το `options.setAddSuffix(true)` είναι ορισμένο πριν το `save()`. |
| **OutOfMemoryError σε μεγάλο DOCX** | Φόρτωση ολόκληρου του αρχείου στη μνήμη | Μετάβαση σε φόρτωση με `InputStream` (δείτε Χαρακτηριστικό 1). |
| **Οι σημειώσεις εξακολουθούν να είναι ορατές** | Η διαγραφή δεν έχει εφαρμοστεί πριν την αποθήκευση | Καλέστε `redactor.apply(new DeleteAnnotationRedaction())` πριν το `save()`. |
| **Η rasterization PDF δεν εφαρμόστηκε** | `setRasterizeToPDF(false)` ή παραλείπεται | Ορίστε `options.setRasterizeToPDF(true)` όταν χρειάζεστε ένα επίπεδο PDF. |

## Συχνές Ερωτήσεις
**Ε: Μπορώ να διαγράψω έγγραφα PDF χρησιμοποιώντας το GroupDocs.Redaction;**  
Α: Ναι, η βιβλιοθήκη υποστηρίζει PDFs, DOCX, PPTX, XLSX και πολλές άλλες μορφές.

**Ε: Ποιος είναι ο καλύτερος τρόπος διαχείρισης μεγάλων αρχείων με το GroupDocs.Redaction;**  
Α: Χρησιμοποιήστε streaming (`load document from stream`) και κλείστε γρήγορα τους πόρους για να διατηρήσετε τη χρήση μνήμης χαμηλή.

**Ε: Είναι δυνατόν να προσαρμόσω το κείμενο της καταλήξεως;**  
Α: Το API προσθέτει αυτόματα μια προεπιλεγμένη καταλήξη (π.χ., “_redacted”). Για προσαρμοσμένες καταλήξεις, μετονομάστε το αρχείο εξόδου μετά την αποθήκευση.

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το GroupDocs.Redaction;**  
Α: Επισκεφθείτε τη [σελίδα Temporary License](https://purchase.groupdocs.com/temporary-license/) και ακολουθήστε τις οδηγίες.

**Ε: Πού μπορώ να λάβω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Συμμετέχετε στο [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) για εξειδικευμένη βοήθεια.

## Πόροι
- **Τεκμηρίωση:** Εξερευνήστε λεπτομερείς οδηγούς στο [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Αναφορά API:** Πρόσβαση σε ολοκληρωμένες λεπτομέρειες API στο [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Λήψη:** Λάβετε την πιο πρόσφατη έκδοση από το [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Αποθετήριο GitHub:** Συμβάλετε ή εξερευνήστε τον κώδικα στο [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---
**Τελευταία Ενημέρωση:** 2026-05-22  
**Δοκιμασμένο Με:** GroupDocs.Redaction 24.9 for Java  
**Συγγραφέας:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Σχετικές Εκπαιδεύσεις
- [Μετατροπή Word σε PDF και Αποθήκευση Διαγραμμένων Εγγράφων με GroupDocs.Redaction Java](/redaction/java/document-saving/)  
- [Προεπισκόπηση Σελίδων Εγγράφου Java Φόρτωση με GroupDocs.Redaction](/redaction/java/document-loading/)  
- [Προχωρημένες Τεχνικές Διαγραφής για GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)