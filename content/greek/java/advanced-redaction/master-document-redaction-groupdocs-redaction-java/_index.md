---
date: '2026-11-02'
description: Μάθετε πώς να προσθέσετε κατάληξη στο όνομα αρχείου σε ένα σεμινάριο
  GroupDocs redaction Java χρησιμοποιώντας Maven, streaming load, annotation deletion
  και save options.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Μάθετε πώς να προσθέσετε κατάληξη στο όνομα αρχείου σε ένα σεμινάριο
  GroupDocs redaction Java. Ακολουθήστε βήμα‑βήμα τη ρύθμιση Maven, το streaming load
  και τις επιλογές αποθήκευσης.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Πώς να προσθέσετε κατάληξη στο όνομα αρχείου στο GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
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
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Πώς να προσθέσετε κατάληξη στο όνομα αρχείου στο GroupDocs redaction Java
type: docs
url: /el/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Πώς να προσθέσετε κατάληξη στο όνομα αρχείου στο GroupDocs redaction Java

Σε αυτό το **groupdocs redaction java tutorial** θα μάθετε πώς να προσθέτετε αυτόματα μια κατάληξη στο όνομα του αρχείου εξόδου κατά την επεξεργασία εγγράφων με το GroupDocs.Redaction. Η προσθήκη κατάληξης εξαλείφει την χειροκίνητη μετονομασία, μειώνει τον κίνδυνο διαρροής μη επεξεργασμένων αρχείων και εντάσσεται άψογα σε CI/CD pipelines που βασίζονται σε κανόνες ονοματοδοσίας. Ο οδηγός σας καθοδηγεί μέσω της ρύθμισης Maven, φόρτωσης εγγράφων μέσω streaming, αφαίρεσης σχολίων και διαμόρφωσης επιλογών αποθήκευσης — όλα με σύντομο, έτοιμο για παραγωγή κώδικα.

## Γρήγορες απαντήσεις
- **Τι κάνει η «προσθήκη κατάληξης στο όνομα αρχείου»;**  
  Όταν ενεργοποιήσετε την επιλογή κατάληξης, το SDK προσθέτει αυτόματα μια προκαθορισμένη συμβολοσειρά (από προεπιλογή «_redacted») στο βασικό όνομα του αρχείου εξόδου πριν την επέκταση. Αυτό καθιστά αμέσως σαφές ποια αρχεία έχουν υποστεί επεξεργασία, βοηθά στην αποτροπή τυχαίας διανομής του αρχικού περιεχομένου και απλοποιεί την αυτοματοποίηση downstream που βασίζεται σε πρότυπα ονοματοδοσίας.  
- **Μπορώ να φορτώσω ένα έγγραφο από ροή;**  
  Ναι—GroupDocs.Redaction υποστηρίζει φόρτωση από οποιοδήποτε `InputStream`, ιδανικό για αποθήκευση στο cloud ή επεξεργασία στη μνήμη.  
- **Χρειάζομαι άδεια για αυτή τη λειτουργία;**  
  Μια δωρεάν δοκιμή λειτουργεί για βασική επεξεργασία· μια προσωρινή ή πλήρης άδεια ξεκλειδώνει όλες τις προχωρημένες επιλογές, συμπεριλαμβανομένης της διαχείρισης κατάληξης.  
- **Ποιοι τύποι αρχείων υποστηρίζονται;**  
  Η βιβλιοθήκη διαχειρίζεται DOCX, PDF, PPTX, XLSX και πολλά άλλα.  
- **Απαιτείται rasterization για έξοδο PDF;**  
  Η rasterization είναι προαιρετική· ενεργοποιήστε την όταν χρειάζεται να επίπεδοποιήσετε το έγγραφο για επιπλέον ασφάλεια.

## Τι κάνει η «προσθήκη κατάληξης στο όνομα αρχείου»;

Όταν ενεργοποιήσετε την επιλογή κατάληξης, το SDK προσθέτει αυτόματα μια προκαθορισμένη συμβολοσειρά (από προεπιλογή «_redacted») στο βασικό όνομα του αρχείου εξόδου πριν την επέκταση. Αυτό καθιστά αμέσως σαφές ποια αρχεία έχουν υποστεί επεξεργασία, βοηθά στην αποτροπή τυχαίας διανομής του αρχικού περιεχομένου και απλοποιεί την αυτοματοποίηση downstream που βασίζεται σε πρότυπα ονοματοδοσίας.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για αυτήν την εργασία;

GroupDocs.Redaction προσφέρει ένα υψηλής απόδοσης Java API που συνδυάζει ενέργειες επεξεργασίας με ευέλικτες επιλογές διαχείρισης αρχείων, όπως αυτόματη προσθήκη κατάληξης, υποστήριξη streaming και επεξεργασία δέσμης. Υποστηρίζει πάνω από 50 μορφές εισόδου και εξόδου και μπορεί να επεξεργαστεί έγγραφα εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, εξασφαλίζοντας χαμηλή χρήση μνήμης και γρήγορη εκτέλεση.

## Προαπαιτούμενα

- **Java Development Kit (JDK):** Έκδοση 8 ή νεότερη.  
- **GroupDocs.Redaction Library:** Κύρια βιβλιοθήκη για εργασίες επεξεργασίας.  
- **IDE:** IntelliJ IDEA, Eclipse ή οποιοσδήποτε επεξεργαστής συμβατός με Java.  
- **Maven:** Για διαχείριση εξαρτήσεων.  

### Προαπαιτούμενες γνώσεις
Η εξοικείωση με Java I/O και βασικές αντικειμενοστραφείς έννοιες θα κάνει τα παραδείγματα πιο εύκολα στην παρακολούθηση.

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

### Άμεση λήψη
Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση άδειας
1. **Free trial:** Πρόσβαση σε βασική λειτουργικότητα χωρίς περιορισμούς.  
2. **Temporary license:** Απόκτηση προσωρινής άδειας για εξερεύνηση προχωρημένων λειτουργιών.  
3. **Purchase:** Για μακροπρόθεσμη χρήση, εξετάστε την αγορά πλήρους άδειας.

#### Βασική αρχικοποίηση και ρύθμιση
Αρχικοποιήστε το έργο σας προσθέτοντας τις απαραίτητες εισαγωγές:

```java
import com.groupdocs.redaction.Redactor;
```

Με αυτήν τη ρύθμιση, είστε έτοιμοι να υλοποιήσετε λειτουργίες επεξεργασίας εγγράφων.

## Οδηγός υλοποίησης

### Χαρακτηριστικό 1: φόρτωση εγγράφου από ροή
**Επισκόπηση:** Μάθετε πώς να φορτώνετε έγγραφα σε ένα `InputStream` για επεξεργασία.

`InputStream` είναι μια κλάση Java I/O που αντιπροσωπεύει μια ροή byte, επιτρέποντάς σας να διαβάζετε δεδομένα από αρχεία, δικτυακές συνδέσεις ή άλλες πηγές χωρίς να φορτώνετε ολόκληρο το περιεχόμενο στη μνήμη.

#### Βήμα 1.1: δημιουργία inputstream

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

- **Γιατί:** Η χρήση του `InputStream` σας επιτρέπει να διαχειρίζεστε έγγραφα αποθηκευμένα σε διάφορες τοποθεσίες — cloud buckets, βάσεις δεδομένων ή buffers στη μνήμη — χωρίς πρώτα να τα γράψετε στον δίσκο. Αυτή η προσέγγιση είναι απαραίτητη όταν χρειάζεται να **load document from stream** σε αρχιτεκτονικές μικρο‑υπηρεσιών.

### Χαρακτηριστικό 2: εφαρμογή διαγραφής σχολίων redaction
**Επισκόπηση:** Αφαιρέστε τα σχόλια από το έγγραφό σας χρησιμοποιώντας το `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` είναι μια λειτουργία επεξεργασίας που αφαιρεί όλα τα σχόλια—όπως σχόλια, επισήμανση και σημειώσεις—από το έγγραφο.

#### Βήμα 2.1: εφαρμογή deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Γιατί:** Αυτό το βήμα εξασφαλίζει ότι τυχόν ευαίσθητα σχόλια (σχόλια, επισήμανση ή κρυφές σημειώσεις) αφαιρούνται από το έγγραφο, ενισχύοντας την ιδιωτικότητα και τη συμμόρφωση.

### Χαρακτηριστικό 3: αποθήκευση εγγράφου με επιλογές
**Επισκόπηση:** Μάθετε πώς να αποθηκεύετε το επεξεργασμένο έγγραφό σας με συγκεκριμένες επιλογές όπως rasterization και **add suffix filename java**.

`SaveOptions` περιλαμβάνει ρυθμίσεις που ελέγχουν πώς γράφεται το επεξεργασμένο έγγραφο, συμπεριλαμβανομένης της μορφής, rasterization και των κανόνων ονοματοδοσίας.

#### Βήμα 3.1: διαμόρφωση saveoptions

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

- **Γιατί:** Η προσαρμογή των επιλογών αποθήκευσης επιτρέπει ευέλικτες μορφές εξόδου και κανόνες ονοματοδοσίας. Η ενεργοποίηση του `setAddSuffix(true)` **adds suffix to filename**, καθιστώντας σαφές ότι το αρχείο έχει επεξεργαστεί.

## Πώς να προσθέσετε κατάληξη στο όνομα αρχείου java κατά την αποθήκευση ενός εγγράφου;

Η κλάση `Redactor` είναι το βασικό στοιχείο που φορτώνει ένα έγγραφο και εφαρμόζει λειτουργίες επεξεργασίας. Το `SaveOptions` ορίζει πώς αποθηκεύεται το επεξεργασμένο έγγραφο, συμπεριλαμβανομένης της μορφής, rasterization και των κανόνων ονοματοδοσίας. Δημιουργήστε μια παρουσία `Redactor`, εφαρμόστε τις απαιτούμενες επεξεργασίες, στη συνέχεια διαμορφώστε ένα αντικείμενο `SaveOptions` με `setAddSuffix(true)`. Καλέστε `redactor.save(outputPath, options)`. Το SDK προσθέτει αυτόματα το «_redacted» (ή την προσαρμοσμένη κατάληξη) στο όνομα του αρχείου, ώστε να μην χρειάζεται ποτέ να μετονομάσετε το αρχείο χειροκίνητα.

## Επισκόπηση εξάρτησης Maven του GroupDocs

Το **groupdocs maven dependency** φέρνει ολόκληρο το Redaction SDK στο έργο σας με μία μόνο καταχώρηση `<dependency>`. Διαχειρίζεται τις διαμεταβιβάσιμες εξαρτήσεις, διατηρεί τις βιβλιοθήκες ενημερωμένες και απλοποιεί την αυτοματοποίηση της κατασκευής. Με τη δήλωση της εξάρτησης στο `pom.xml`, αποφεύγετε τη χειροκίνητη διαχείριση JAR και εξασφαλίζετε συμβατότητα με τις τελευταίες ενημερώσεις ασφαλείας.

## Γιατί η προσθήκη κατάληξης είναι σημαντική

Η προσθήκη κατάληξης παρέχει άμεση οπτική επιβεβαίωση ότι ένα αρχείο έχει υποστεί επεξεργασία, κάτι κρίσιμο για ιχνηλασιμότητα, αυτοματοποιημένες ροές εργασίας και κανονιστική συμμόρφωση. Επιτρέπει στα σενάρια να φιλτράρουν τα επεξεργασμένα αρχεία, αποτρέπει την τυχαία διανομή του αρχικού περιεχομένου και ικανοποιεί πολλά βιομηχανικά πρότυπα που απαιτούν σαφή σήμανση των εξαγορασμένων εγγράφων.

## Πρακτικές εφαρμογές

1. **Legal document redaction:** Ασφαλής συμβάσεις πριν την κοινοποίηση σε πελάτες.  
2. **Medical record handling:** Προστασία ταυτοτήτων ασθενών ενώ διατηρούνται τα κλινικά δεδομένα.  
3. **Financial reporting:** Διατήρηση ευαίσθητων αριθμών εμπιστευτικών κατά τις εξωτερικές ελέγχους.  
4. **CRM integration:** Αυτόματη επεξεργασία δεδομένων πελατών πριν την εξαγωγή σε τρίτα εργαλεία.  
5. **Collaboration tools:** Διασφάλιση ότι τα κοινόχρηστα προσχέδια δεν εκθέτουν κρυφά σχόλια ή μεταδεδομένα.

## Σκέψεις απόδοσης

### Βελτιστοποίηση απόδοσης
- Χρησιμοποιήστε streaming (`load document from stream`) για αποφυγή φόρτωσης ολόκληρων αρχείων στη μνήμη.  
- Κλείστε άμεσα τις παρουσίες `Redactor` για απελευθέρωση πόρων.  

### Οδηγίες χρήσης πόρων
- Παρακολουθήστε CPU και μνήμη κατά τις εκτελέσεις δέσμης.  
- Προτιμήστε `ByteArrayOutputStream` για αποθηκεύσεις στη μνήμη όταν εργάζεστε με μέτρια μεγέθη αρχείων.  

### Καλές πρακτικές για διαχείριση μνήμης Java
- Επαναχρησιμοποιήστε αντικείμενα `Redactor` όταν επεξεργάζεστε πολλαπλά αρχεία του ίδιου τύπου.  
- Καλείτε `close()` σε μπλοκ `try‑with‑resources` για αποφυγή διαρροών.

## Συχνά προβλήματα και λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Suffix not appearing** | `setAddSuffix(false)` ή έλλειψη κλήσης | Βεβαιωθείτε ότι το `options.setAddSuffix(true)` έχει οριστεί πριν το `save()`. |
| **OutOfMemoryError on large DOCX** | Φόρτωση ολόκληρου αρχείου στη μνήμη | Μεταβείτε στη φόρτωση με `InputStream` (δείτε το Χαρακτηριστικό 1). |
| **Annotations still visible** | Η επεξεργασία δεν έχει εφαρμοστεί πριν την αποθήκευση | Καλέστε `redactor.apply(new DeleteAnnotationRedaction())` πριν το `save()`. |
| **PDF rasterization not applied** | `setRasterizeToPDF(false)` ή παραλείπεται | Ορίστε `options.setRasterizeToPDF(true)` όταν χρειάζεστε επίπεδο PDF. |

## Συχνές ερωτήσεις

**Q: Μπορώ να επεξεργαστώ έγγραφα PDF χρησιμοποιώντας το GroupDocs.Redaction;**  
A: Ναι, η βιβλιοθήκη υποστηρίζει PDF, DOCX, PPTX, XLSX και πολλές άλλες μορφές.

**Q: Ποιος είναι ο καλύτερος τρόπος διαχείρισης μεγάλων αρχείων με το GroupDocs.Redaction;**  
A: Χρησιμοποιήστε streaming (`load document from stream`) και κλείστε άμεσα τους πόρους για χαμηλή χρήση μνήμης.

**Q: Είναι δυνατόν να προσαρμόσω το κείμενο της κατάληξης;**  
A: Το API προσθέτει αυτόματα μια προεπιλεγμένη κατάληξη (π.χ., «_redacted»). Για προσαρμοσμένες καταλήξεις, μετονομάστε το αρχείο εξόδου μετά την αποθήκευση.

**Q: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το GroupDocs.Redaction;**  
A: Επισκεφθείτε τη [Temporary License page](https://purchase.groupdocs.com/temporary-license/) και ακολουθήστε τις οδηγίες.

**Q: Πού μπορώ να λάβω βοήθεια αν αντιμετωπίσω προβλήματα;**  
A: Συμμετέχετε στο [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) για εξειδικευμένη υποστήριξη.

## Πόροι
- **Documentation:** Εξερευνήστε λεπτομερείς οδηγούς στο [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API reference:** Πρόσβαση σε ολοκληρωμένες λεπτομέρειες API στο [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Λάβετε την πιο πρόσφατη έκδοση από [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub repository:** Συμβάλετε ή εξερευνήστε τον κώδικα στο [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Last Updated:** 2026-11-02  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## Σχετικά μαθήματα

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)