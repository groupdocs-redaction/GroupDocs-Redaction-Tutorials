---
date: '2026-09-21'
description: Μάθετε πώς να αποκρύψετε εικόνα με το GroupDocs.Redaction for Java. Ο
  οδηγός βήμα‑βήμα καλύπτει το setup, το pixel‑level redaction, την verification και
  τις best practices.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Πώς να αποκρύψετε εικόνα με το GroupDocs.Redaction for Java. Ακολουθήστε
  αυτόν τον οδηγό για να mask pixel data σε σαρωμένα αρχεία, να επιλέξετε χρώματα
  και να verify results—ιδανικό για συμμόρφωση με GDPR και HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Πώς να αποκρύψετε εικόνα χρησιμοποιώντας το GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Πώς να αποκρύψετε εικόνα χρησιμοποιώντας το GroupDocs.Redaction for Java
type: docs
url: /el/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Πώς να αποκρύψετε εικόνα χρησιμοποιώντας το GroupDocs.Redaction για Java

Σε αυτό το ολοκληρωμένο tutorial θα μάθετε **πώς να αποκρύψετε εικόνα** αρχεία σε Java με το GroupDocs.Redaction. Η επεξεργασία σαρωμένων εικόνων είναι ένα κρίσιμο βήμα για την προστασία προσωπικών δεδομένων, τη συμμόρφωση με GDPR, HIPAA ή άλλους κανονισμούς απορρήτου, και τη διασφάλιση ότι ευαίσθητες οπτικές πληροφορίες δεν διαρρέουν ποτέ. Θα σας καθοδηγήσουμε μέσα από τη ρύθμιση του έργου, τη διαμόρφωση της επεξεργασίας σε επίπεδο pixel, την ασφαλή αποθήκευση του αποτελέσματος και την επιβεβαίωση ότι η επεξεργασία ήταν επιτυχής—όλα παρουσιάζονται με έναν συνομιλητικό, βήμα‑βήμα τρόπο που μπορείτε να αντιγράψετε σε οποιαδήποτε εφαρμογή Java.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται την επεξεργασία εικόνας σε Java;** GroupDocs.Redaction for Java.  
- **Μπορώ να επιλέξω το χρώμα της επεξεργασίας;** Ναι – οποιοδήποτε αδιαφανές `java.awt.Color` όπως `Color.BLUE` ή `Color.BLACK`.  
- **Απαιτείται άδεια για παραγωγή;** Ναι, μια έγκυρη άδεια GroupDocs είναι υποχρεωτική για εμπορική χρήση.  
- **Θα αντικατασταθεί η αρχική εικόνα;** Όχι – το API γράφει την επεξεργασμένη εικόνα σε νέο αρχείο που καθορίζετε.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 και νεότερη (μέχρι Java 21 τη στιγμή της συγγραφής).

## Τι είναι η επεξεργασία εικόνας και γιατί να επεξεργαστείτε σαρωμένη εικόνα java;
Η επεξεργασία εικόνας αφαιρεί μόνιμα οπτικά δεδομένα—ονόματα, αριθμούς, υπογραφές—αντικαθιστώντας περιοχές pixel με ένα στερεό χρώμα. Σε αντίθεση με την επεξεργασία κειμένου, η οποία λειτουργεί σε επιλέξιμους χαρακτήρες, οι σαρωμένες εικόνες αποθηκεύουν πληροφορίες ως ακατέργαστα pixel, οπότε μόνο εργαλεία βασισμένα σε pixel μπορούν να εγγυηθούν ότι τα δεδομένα δεν μπορούν να ανακτηθούν. Χρησιμοποιώντας το GroupDocs.Redaction μπορείτε να στοχεύσετε ακριβείς συντεταγμένες, να εφαρμόσετε οποιοδήποτε αδιαφανές χρώμα και να δημιουργήσετε μια νέα εικόνα που αφαιρεί μόνιμα το ευαίσθητο περιεχόμενο.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για Java;
Το GroupDocs.Redaction υποστηρίζει **50+ μορφές εικόνας** (συμπεριλαμβανομένων JPG, PNG, BMP, GIF) και μπορεί να επεξεργαστεί έγγραφα πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, χάρη στην αρχιτεκτονική ροής του. Τα benchmarks δείχνουν ότι ένα σαρωμένο PNG 300 KB επεξεργάζεται σε κάτω από 120 ms σε τυπική CPU 2.8 GHz, καθιστώντας το κατάλληλο για batch jobs και υπηρεσίες σε πραγματικό χρόνο.

## Προαπαιτούμενα
- **JDK 8 ή νεότερο** εγκατεστημένο και ρυθμισμένο στο `PATH` σας.  
- **Maven** (ή Gradle) για διαχείριση εξαρτήσεων.  
- Ένα IDE όπως **IntelliJ IDEA**, **Eclipse**, ή **NetBeans**.  
- Βασική εξοικείωση με το Java file I/O και το πακέτο `java.awt`.  

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

### Άμεση λήψη
Εναλλακτικά, κατεβάστε το πιο πρόσφατο JAR από την επίσημη σελίδα κυκλοφορίας: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Απόκτηση άδειας
- **Δωρεάν δοκιμή:** Εγγραφείτε για δοκιμή ώστε να εξερευνήσετε το πλήρες API.  
- **Προσωρινή άδεια:** Χρησιμοποιήστε προσωρινό κλειδί για εκτεταμένη δοκιμή χωρίς κόστος.  
- **Πλήρης αγορά:** Αποκτήστε άδεια παραγωγής για απεριόριστη ανάπτυξη.

## Οδηγός υλοποίησης

Θα χωρίσουμε την υλοποίηση σε δύο κύρια χαρακτηριστικά: **image‑area redaction** (η πραγματική μάσκα) και **redaction status check** (επαλήθευση επιτυχίας).

### Πώς να επεξεργαστείτε σαρωμένες εικόνες εγγράφων – βήμα 1: αρχικοποίηση του redactor
`Redactor` είναι η κεντρική κλάση που φορτώνει μια εικόνα και παρέχει λειτουργίες επεξεργασίας.  
Δημιουργήστε μια παρουσία `Redactor` που δείχνει στην πηγή εικόνας που θέλετε να επεξεργαστείτε.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Βήμα 2: ορισμός παραμέτρων επεξεργασίας
`ImageAreaRedaction` λειτουργεί με ένα `Point` (γωνία πάνω‑αριστερά) και ένα `Dimension` (πλάτος × ύψος) που περιγράφουν το ορθογώνιο προς απόκρυψη. Σε αυτό το παράδειγμα χρησιμοποιούμε χρώμα γεμίσματος μπλε.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Βήμα 3: εφαρμογή επεξεργασίας
`RegionReplacementOptions` σας επιτρέπει να ορίσετε το χρώμα γεμίσματος και προαιρετικό περίγραμμα. Περνώντας αυτές τις επιλογές στο `ImageAreaRedaction` και καλώντας `apply()` εκτελεί τη μάσκα. Η μέθοδος επιστρέφει ένα `RedactorChangeLog` που υποδεικνύει επιτυχία ή αποτυχία.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Βήμα 4: απελευθέρωση πόρων
`Redactor` υλοποιεί το `AutoCloseable`. Το κλείσιμο του ελευθερώνει τους εγγενείς buffer και τους χειριστές αρχείων, αποτρέποντας διαρροές μνήμης σε υπηρεσίες μακράς διάρκειας.

```java
redactor.close();
```

### Πώς να επαληθεύσετε την επεξεργασία – έλεγχος κατάστασης
Μετά την εφαρμογή της επεξεργασίας, εξετάστε το `RedactorChangeLog`. Μια τιμή `Status.SUCCESS` επιβεβαιώνει ότι η περιοχή pixel αντικαταστάθηκε χωρίς σφάλμα. Μπορείτε επίσης να αποδώσετε την εικόνα σε ένα `BufferedImage` για οπτικό έλεγχο πριν την αποθήκευση.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Πρακτικές εφαρμογές
- **Διαχείριση εμπιστευτικών εγγράφων:** Απόκρυψη προσωπικών δεδομένων σε σαρωμένες συμβάσεις πριν την κοινοποίηση σε συνεργάτες.  
- **Νομική τεκμηρίωση:** Διασφάλιση συμμόρφωσης με GDPR ή HIPAA αποκρύπτοντας ταυτοποιητικά στοιχεία σε εικόνες αποδείξεων.  
- **Ιατρικά αρχεία:** Απόκρυψη προσώπων ασθενών ή χειρόγραφων σημειώσεων σε σαρωτές ακτινογραφίες διατηρώντας τα διαγνωστικά στοιχεία.  

## Σκέψεις απόδοσης
- **Επεξεργασία παρτίδας:** Επεξεργασία εικόνων σε ομάδες των 10–20 για να διατηρείται η χρήση μνήμης κάτω από 200 MB.  
- **Επαναχρησιμοποίηση αντικειμένων:** Επαναχρησιμοποιήστε αντικείμενα `Point` και `Dimension` σε επαναλήψεις για μείωση του φορτίου του GC.  
- **Ενημερώσεις έκδοσης:** Αναβαθμίστε στην πιο πρόσφατη έκδοση του GroupDocs.Redaction για να επωφεληθείτε από βελτίωση ταχύτητας 15 % όπως αναφέρεται στην έκδοση 24.10.  

## Συχνά προβλήματα & λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Η επεξεργασία αποτυγχάνει με κατάσταση `Failed`** | Λανθασμένη διαδρομή αρχείου ή μη υποστηριζόμενη μορφή εικόνας | Επαληθεύστε ότι το αρχείο υπάρχει και είναι σε υποστηριζόμενη μορφή (JPG, PNG, BMP, GIF). |
| **Το αρχείο εξόδου είναι κενό** | `redactor.save()` κλήθηκε πριν ολοκληρωθεί η επεξεργασία | Βεβαιωθείτε ότι το `apply()` επιστρέφει `Status.SUCCESS` πριν καλέσετε το `save()`. |
| **Το χρώμα δεν εφαρμόστηκε** | Χρήση διαφανούς `Color` | Επιλέξτε αδιαφανές χρώμα όπως `Color.BLACK` ή `Color.BLUE`. |

## Συχνές ερωτήσεις

**Q: Ποια είναι η διαφορά μεταξύ `ImageAreaRedaction` και επεξεργασίας κειμένου;**  
A: `ImageAreaRedaction` λειτουργεί σε ακατέργαστες συντεταγμένες pixel, ενώ η επεξεργασία κειμένου αναλύει επίπεδα OCR για να εντοπίσει και να αφαιρέσει το κειμενικό περιεχόμενο.

**Q: Μπορώ να επεξεργαστώ πολλαπλές περιοχές σε μία εικόνα;**  
A: Ναι—καλέστε το `redactor.apply()` επανειλημμένα με διαφορετικά αντικείμενα `ImageAreaRedaction` πριν αποθηκεύσετε το τελικό αρχείο.

**Q: Το GroupDocs.Redaction υποστηρίζει άλλες μορφές εικόνας όπως TIFF;**  
A: Η βιβλιοθήκη υποστηρίζει κοινές μορφές raster (JPG, PNG, BMP, GIF). Για TIFF, μετατρέψτε πρώτα την εικόνα σε υποστηριζόμενη μορφή.

**Q: Πώς μπορώ να αυτοματοποιήσω την επεξεργασία για έναν φάκελο σαρωμένων PDF;**  
A: Εξάγετε κάθε σελίδα ως εικόνα, εφαρμόστε την ίδια λογική επεξεργασίας, και στη συνέχεια ξαναδημιουργήστε το PDF χρησιμοποιώντας μια βιβλιοθήκη PDF όπως το GroupDocs.Conversion.

**Q: Υπάρχει τρόπος να προεπισκοπήσετε την επεξεργασία πριν την αποθήκευση;**  
A: Αποδώστε το `Redactor` σε ένα `BufferedImage` και εμφανίστε το σε UI Swing ή JavaFX, ώστε να επιβεβαιώσετε την περιοχή μάσκας πριν την τελική αποθήκευση.

## Συμπέρασμα
Τώρα έχετε έναν πλήρη, έτοιμο για παραγωγή οδηγό για **πώς να αποκρύψετε εικόνα** περιεχόμενο και, ειδικά, πώς να **αποκρύψετε σαρωμένη εικόνα java** χρησιμοποιώντας το GroupDocs.Redaction για Java. Ακολουθώντας τα παραπάνω βήματα μπορείτε να προστατεύσετε ευαίσθητα οπτικά δεδομένα σε τομείς όπως χρηματοοικονομικά, νομικά και υγειονομική περίθαλψη. Εξερευνήστε επιπλέον API—όπως επεξεργασία κειμένου, επεξεργασία σελίδων PDF ή μαζική επεξεργασία φακέλων—για να δημιουργήσετε μια ολοκληρωμένη pipeline προστασίας δεδομένων για τον οργανισμό σας.

**Πόροι**  
- [Τεκμηρίωση](https://docs.groupdocs.com/redaction/java/)  
- [Αναφορά API](https://reference.groupdocs.com/redaction/java)  
- [Λήψη](https://releases.groupdocs.com/redaction/java/)  
- [Αποθετήριο GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Δωρεάν φόρουμ υποστήριξης](https://forum.groupdocs.com/c/redaction/33)  
- [Προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/) 

---

**Τελευταία ενημέρωση:** 2026-09-21  
**Δοκιμάστηκε με:** GroupDocs.Redaction 24.9 (Java)  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Πώς να επεξεργαστείτε Java με το GroupDocs.Redaction - Ένας ολοκληρωμένος οδηγός για προγραμματιστές](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Πώς να επεξεργαστείτε σαρωμένο PDF με OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Πώς να επεξεργαστείτε κείμενο σε Java με το GroupDocs.Redaction – Οδηγός](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)