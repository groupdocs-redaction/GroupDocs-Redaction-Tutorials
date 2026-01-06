---
date: '2026-01-06'
description: Μάθετε πώς να αποκτήσετε τον τύπο αρχείου Java, να διαβάσετε τις ιδιότητες
  του εγγράφου και να ανακτήσετε τον αριθμό σελίδων Java με το GroupDocs.Redaction
  για Java. Οδηγός βήμα‑βήμα με κώδικα.
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: Λάβετε τύπο αρχείου java χρησιμοποιώντας το GroupDocs.Redaction – Εξαγωγή μεταδεδομένων
type: docs
url: /el/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# Αποκτήστε τον τύπο αρχείου java και εξάγετε τα μεταδεδομένα εγγράφου με το GroupDocs.Redaction σε Java

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να λάβω τον τύπο αρχείου ενός εγγράφου σε Java;** Χρησιμοποιήστε `redactor.getDocumentInfo().getFileType()`.
- **Ποια βιβλιοθήκη διαχειρίζεται την εξαγωγή μεταδεδομένων και την επεξεργασία redaction μαζί;** GroupDocs.Redaction για Java.
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται μόνιμη άδεια για παραγωγή.
- **Μπορώ επίσης να ανακτήσω τον αριθμό σελίδων;** Ναι, καλέστε `getPageCount()` στο αντικείμενο `IDocumentInfo`.
- **Είναι αυτή η προσέγγιση συμβατή με Java 8+;** Απόλυτα· το GroupDocs.Redaction υποστηρίζει Java 8 και νεότερες εκδόσεις.

## Τι είναι το “get file type java” και γιατί είναι σημαντικό;
Όταν καλείτε `getFileType()` σε ένα έγγραφο, η βιβλιοθήκη εξετάζει την κεφαλίδα του αρχείου και επιστρέφει ένα φιλικό enum (π.χ. **DOCX**, **PDF**, **XLSX**). Η γνώση του ακριβούς τύπου σας επιτρέπει να κατευθύνετε το αρχείο στη σωστή διαδικασία επεξεργασίας, να εφαρμόζετε πολιτικές ασφαλείας ή απλώς να εμφανίζετε ακριβείς πληροφορίες στους τελικούς χρήστες.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για java read document properties;
- **All‑in‑one solution:** Redaction, εξαγωγή μεταδεδομένων και μετατροπή μορφών βρίσκονται κάτω από ένα ενιαίο API.
- **Stream‑friendly:** Λειτουργεί απευθείας με `InputStream`, ώστε να μπορείτε να επεξεργάζεστε αρχεία από δίσκο, δίκτυο ή αποθήκευση cloud χωρίς προσωρινά αρχεία.
- **Performance‑tuned:** Ελάχιστο αποτύπωμα μνήμης και αυτόματος καθαρισμός πόρων όταν κλείνετε το αντικείμενο `Redactor`.

## Προαπαιτούμενα
1. **GroupDocs.Redaction για Java** (έκδοση 24.9 ή νεότερη).  
2. JDK 8 ή νεότερο.  
3. Βασικές γνώσεις Java και εξοικείωση με ροές I/O αρχείων.

## Ρύθμιση του GroupDocs.Redaction για Java

### Maven Installation
Προσθέστε το αποθετήριο και την εξάρτηση στο `pom.xml` σας:

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

### Direct Download
Εναλλακτικά, κατεβάστε την πιο πρόσφατη έκδοση απευθείας από [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
- **Free Trial:** Ιδανική για αξιολόγηση του API.  
- **Temporary License:** Διαθέσιμη στον επίσημο ιστότοπο για βραχυπρόθεσμη δοκιμή.  
- **Full License:** Αγοράστε όταν είστε έτοιμοι για χρήση σε παραγωγή.

## Basic Initialization (Java)

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## Πώς να λάβετε τον τύπο αρχείου java με το GroupDocs.Redaction

### Step 1: Open a File Stream
Ξεκινήστε δημιουργώντας ένα `InputStream` για το στοχευόμενο έγγραφο:

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### Step 2: Initialize the Redactor
Δημιουργήστε ένα αντικείμενο `Redactor` χρησιμοποιώντας τη ροή. Αυτό το αντικείμενο σας δίνει πρόσβαση στα μεταδεδομένα του εγγράφου.

```java
final Redactor redactor = new Redactor(stream);
```

### Step 3: Retrieve Document Information
Καλέστε `getDocumentInfo()` για να λάβετε ένα αντικείμενο `IDocumentInfo`. Εδώ είναι όπου **get file type java**, διαβάζετε άλλες ιδιότητες και ακόμη **retrieve page count java**.

```java
try {
    IDocumentInfo info = redactor.getDocumentInfo();
    
    // Display document information (uncomment as needed)
    System.out.println("\
File type: " + info.getFileType() +
           "\
Number of pages: " + info.getPageCount() + 
           "\
Document size: " + info.getSize() + " bytes");
} finally {
    redactor.close();
    stream.close();
}
```

> **Pro tip:** Αποσχολιάστε τις γραμμές `System.out.println` μόνο όταν χρειάζεστε έξοδο στην κονσόλα· διατηρώντας τις σχολιασμένες στην παραγωγή μειώνετε το φορτίο I/O.

### Step 4: Close Resources
Πάντα κλείστε το `Redactor` και τη ροή σε ένα μπλοκ `finally` (όπως φαίνεται) για να αποφύγετε διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλά έγγραφα παράλληλα.

## Practical Applications (java read document properties)

1. **Document Management Systems:** Αυτόματη κατηγοριοποίηση αρχείων κατά τύπο, αριθμό σελίδων και μέγεθος.  
2. **Data‑Analytics Pipelines:** Παροχή μεταδεδομένων σε πίνακες ελέγχου για αναφορές.  
3. **Content‑Creation Platforms:** Εμφάνιση λεπτομερειών αρχείου στους τελικούς χρήστες πριν από τη λήψη ή την προεπισκόπηση.

## Performance Considerations
- Χρησιμοποιήστε **buffered streams** (`BufferedInputStream`) για μεγάλα αρχεία ώστε να βελτιώσετε την ταχύτητα I/O.  
- Απελευθερώστε τους πόρους άμεσα (`close()` τόσο στο `Redactor` όσο και στη ροή).  
- Όταν επεξεργάζεστε παρτίδες, σκεφτείτε την επαναχρησιμοποίηση ενός μόνο αντικειμένου `Redactor` ανά νήμα για να μειώσετε το κόστος δημιουργίας αντικειμένων.

## Common Issues & Solutions
| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|---------|--------------|----------|
| `FileNotFoundException` | Λάθος διαδρομή ή έλλειψη αρχείου | Επαληθεύστε τη απόλυτη/σχετική διαδρομή και τα δικαιώματα του αρχείου. |
| `LicenseException` | Δεν φορτώθηκε έγκυρη άδεια | Φορτώστε δοκιμαστική ή αγορασμένη άδεια πριν δημιουργήσετε το `Redactor`. |
| `OutOfMemoryError` on large PDFs | Ανεμπλοκή ροής ή επεξεργασία πολλών αρχείων ταυτόχρονα | Μεταβείτε σε `BufferedInputStream` και περιορίστε τα ταυτόχρονα νήματα. |

## Frequently Asked Questions

**Q: What is GroupDocs.Redaction used for?**  
A: Primarily for redacting sensitive content, it also provides robust APIs to **java read document properties** such as file type and page count.

**Q: Can I use GroupDocs.Redaction with other Java frameworks?**  
A: Yes, the library works seamlessly with Spring, Jakarta EE, and even plain Java SE projects.

**Q: How do I handle very large documents efficiently?**  
A: Wrap the file stream in a `BufferedInputStream`, close resources promptly, and consider processing files in a streaming fashion rather than loading the whole document into memory.

**Q: Does the library support non‑English documents?**  
A: Absolutely—GroupDocs.Redaction handles multiple languages and character sets out of the box.

**Q: What are typical pitfalls when extracting metadata?**  
A: Missing licenses, incorrect file paths, and forgetting to close streams are the most common. Always follow the resource‑cleanup pattern shown above.

## Conclusion
Now you have a complete, production‑ready recipe for **getting file type java**, reading other document properties, and **retrieving page count java** using GroupDocs.Redaction. Integrate these snippets into your existing services, and you’ll gain instant visibility into every document that flows through your system.

**Next Steps**  
- Δοκιμάστε άλλα πεδία μεταδεδομένων που εκτίθενται από το `IDocumentInfo`.  
- Συνδυάστε την εξαγωγή μεταδεδομένων με τις ροές redaction για ολοκληρωμένη ασφάλεια εγγράφων.  
- Εξερευνήστε μοτίβα επεξεργασίας παρτίδων για περιβάλλοντα υψηλού όγκου.

---  
**Last Updated:** 2026-01-06  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)