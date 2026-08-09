---
date: '2026-08-09'
description: Μάθετε πώς να δημιουργήσετε non editable PDF αρχεία με redacting κειμένου
  και rasterizing PDFs χρησιμοποιώντας GroupDocs.Redaction for Java.
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: Δημιουργήστε non editable PDF αρχεία με redacting κειμένου και rasterizing
  PDFs χρησιμοποιώντας GroupDocs.Redaction for Java. Ακολουθήστε έναν step‑by‑step
  οδηγό με tips, pitfalls, και FAQs.
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: Δημιουργήστε non editable PDF με GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: Πώς να δημιουργήσετε non editable PDF με GroupDocs.Redaction Java
type: docs
url: /el/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# Πώς να δημιουργήσετε μη επεξεργάσιμο PDF με το GroupDocs.Redaction Java

Σε πολλές ρυθμιζόμενες βιομηχανίες πρέπει να παραδίδετε έγγραφα που δεν μπορούν να τροποποιηθούν ή να αντιγραφούν. Ο πιο αξιόπιστος τρόπος για να το διασφαλίσετε είναι να **δημιουργήσετε μη επεξεργάσιμο PDF** αρχεία, διαγράφοντας πρώτα το ευαίσθητο κείμενο και στη συνέχεια ραστεριάζοντας ολόκληρο το έγγραφο. Το GroupDocs.Redaction για Java σας παρέχει ένα API μιας γραμμής για την εκτέλεση και των δύο βημάτων, ώστε να μπορείτε να πληροίτε τις απαιτήσεις συμμόρφωσης χωρίς να χτίζετε μια προσαρμοσμένη μηχανή PDF.

## Γρήγορες απαντήσεις
- **Τι σημαίνει “διαγραφή κειμένου”;** Αφαιρεί μόνιμα ή καλύπτει ευαίσθητες αλφαριθμητικές ακολουθίες ώστε να μην μπορούν να διαβαστούν ή να ανακτηθούν.  
- **Ποια βιβλιοθήκη εκτελεί τη δουλειά;** Το GroupDocs.Redaction για Java παρέχει ενσωματωμένες δυνατότητες διαγραφής και ραστερισμού.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται μόνιμη άδεια για παραγωγή.  
- **Μπορώ να μετατρέψω DOCX σε ραστεριζόμενο PDF σε ένα βήμα;** Ναι – εφαρμόστε πρώτα τη διαγραφή, έπειτα χρησιμοποιήστε το `SaveOptions` με ενεργοποιημένο ραστερισμό.  
- **Το αποτέλεσμα είναι πραγματικά μη επεξεργάσιμο;** Τα ραστεριζόμενα PDF αποδίδονται ως εικόνες, εμποδίζοντας την εξαγωγή ή τροποποίηση κειμένου.

## Τι είναι η διαγραφή κειμένου;
Η διαγραφή κειμένου αφαιρεί μόνιμα ή θολώνει εμπιστευτικές πληροφορίες—όπως προσωπικά αναγνωριστικά, οικονομικά δεδομένα ή νομικές ρήτρες—από ένα έγγραφο. Σε αντίθεση με μια απλή εύρεση‑αντικατάσταση, η διαγραφή εγγυάται ότι το κρυμμένο περιεχόμενο δεν μπορεί να ανακτηθεί από κανένα εργαλείο. Διαγράφοντας τους αρχικούς χαρακτήρες και προαιρετικά αντικαθιστώντας τους με ένα placeholder, η διαγραφή εξασφαλίζει ότι τα ευαίσθητα δεδομένα είναι ακατάσβεστα και το έγγραφο παραμένει αναγνώσιμο για εξουσιοδοτημένους χρήστες.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για Java;
Το GroupDocs.Redaction για Java προσφέρει ένα ολοκληρωμένο σύνολο λειτουργιών που απλοποιούν την ασφαλή επεξεργασία εγγράφων. Υποστηρίζει ευρύ φάσμα μορφών αρχείων, παρέχει πολλαπλούς τύπους διαγραφής και περιλαμβάνει ραστερισμό με ένα κλικ για κλείδωμα των PDF. Η βιβλιοθήκη είναι βελτιστοποιημένη για απόδοση, λειτουργεί σε Windows και Linux, και ενσωματώνεται εύκολα σε υπάρχουσες εφαρμογές Java, καθιστώντας την αξιόπιστη επιλογή για επιχειρήσεις που χρειάζονται προστασία ευαίσθητων πληροφοριών σε κλίμακα.

## Προαπαιτούμενα
- Java Development Kit (JDK 11 ή νεότερο) και ένα IDE όπως IntelliJ IDEA ή Eclipse.  
- Βιβλιοθήκη GroupDocs.Redaction (έκδοση 24.9 ή νεότερη).  
- Βασικές γνώσεις Java—θα γράψετε μόνο μερικά σύντομα αποσπάσματα.

## Ρύθμιση του GroupDocs.Redaction για Java

### Εγκατάσταση μέσω Maven
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
Αν το Maven δεν είναι η επιλογή σας, μπορείτε να κατεβάσετε το JAR από τη σελίδα κυκλοφορίας: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Απόκτηση άδειας
- **Δωρεάν δοκιμή** – εξερευνήστε το API χωρίς κόστος.  
- **Προσωρινή άδεια** – ιδανική για εκτεταμένες δοκιμές.  
- **Πλήρης άδεια** – απαιτείται για παραγωγικές εγκαταστάσεις.

## Βασική αρχικοποίηση
`Redactor` είναι η κεντρική κλάση του GroupDocs.Redaction που φορτώνει και τροποποιεί ένα έγγραφο στη μνήμη. Αφού εισάγετε το namespace, δημιουργήστε ένα αντικείμενο `Redactor` με τη διαδρομή του αρχικού αρχείου, και είστε έτοιμοι να εφαρμόσετε κανόνες διαγραφής.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Οδηγός υλοποίησης

## Πώς να δημιουργήσετε μη επεξεργάσιμο PDF σε Java;
Φορτώστε το πηγαίο έγγραφο, εφαρμόστε τους επιθυμητούς κανόνες διαγραφής και, στη συνέχεια, αποθηκεύστε το αποτέλεσμα με ενεργοποιημένο ραστερισμό. Αυτή η τριπλή ροή—φόρτωση, διαγραφή, ραστερισμός—παράγει ένα PDF που δεν μπορεί να επεξεργαστεί, αντιγραφεί ή αναζητηθεί, ικανοποιώντας τα πιο αυστηρά πρότυπα συμμόρφωσης. Με τη μετατροπή κάθε σελίδας σε εικόνα, το τελικό αρχείο εξαλείφει τυχόν κρυφά επίπεδα κειμένου που θα μπορούσαν να εξαχθούν αργότερα.

## Πώς να διαγράψετε κείμενο σε Java
Παρακάτω παρουσιάζουμε τη διαγραφή ακριβούς φράσης, ιδανική για την αφαίρεση γνωστών αναγνωριστικών όπως το όνομα ενός ατόμου. Η διαδικασία περιλαμβάνει την εισαγωγή των απαραίτητων κλάσεων, τον ορισμό ενός κανόνα διαγραφής και την εφαρμογή του στο έγγραφο πριν την αποθήκευση.

### Βήμα 1: Εισαγωγή των απαιτούμενων κλάσεων
`ExactPhraseRedaction` είναι ένας κανόνας διαγραφής που στοχεύει σε μια κυριολεκτική συμβολοσειρά. `ReplacementOptions` καθορίζει τι placeholder θα εισαχθεί αντί του αρχικού κειμένου.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Βήμα 2: Εφαρμογή διαγραφής ακριβούς φράσης
Το παρακάτω απόσπασμα αντικαθιστά κάθε εμφάνιση του **“John Doe”** με το placeholder **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**Γιατί λειτουργεί αυτό:**  
- Το `ExactPhraseRedaction` στοχεύει στη κυριολεκτική συμβολοσειρά “John Doe”.  
- Το `ReplacementOptions` λέει στη μηχανή τι να εισάγει αντί του αρχικού κειμένου.

**Συμβουλές & κοινά λάθη**  
- Ελέγξτε τη διαδρομή του εγγράφου· μια λανθασμένη διαδρομή προκαλεί `FileNotFoundException`.  
- Βεβαιωθείτε ότι η διαδικασία Java έχει δικαίωμα εγγραφής στον φάκελο εξόδου.

## Πώς να αποθηκεύσετε ως rasterized PDF
Μετά τη διαγραφή, πιθανότατα θέλετε ένα μη επεξεργάσιμο PDF. Ο ραστερισμός μετατρέπει κάθε σελίδα σε εικόνα, αφαιρώντας τη δυνατότητα επιλογής ή επεξεργασίας κειμένου. Αυτό το βήμα εξασφαλίζει ότι το τελικό PDF συμπεριφέρεται όπως ένα σαρωμένο έγγραφο, καθιστώντας το ανθεκτικό σε εργαλεία εξαγωγής κειμένου και τυχαίες τροποποιήσεις.

### Βήμα 1: Εισαγωγή του `SaveOptions`
Το `SaveOptions` διαμορφώνει τον τρόπο αποθήκευσης του εγγράφου, συμπεριλαμβανομένων των επιλογών ραστερισμού και ονοματοδοσίας αρχείων.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### Βήμα 2: Διαμόρφωση και αποθήκευση του rasterized PDF
Το παρακάτω απόσπασμα απενεργοποιεί το αυτόματο επίθημα “_redacted”, ενεργοποιεί τον ραστερισμό και γράφει το αρχείο εξόδου.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Επεξήγηση:**  
- `setAddSuffix(false)` διατηρεί το αρχικό όνομα αρχείου (μπορείτε να το ενεργοποιήσετε για να προσθέσετε “_redacted”).  
- `setRasterizeToPDF(true)` λέει στο GroupDocs να αποδώσει κάθε σελίδα ως εικόνα μέσα σε PDF, εγγυώμενο ότι το έγγραφο είναι **μη επεξεργάσιμο**.

**Αντιμετώπιση προβλημάτων**  
- Εάν ο ραστερισμός αποτύχει, ελέγξτε ότι το runtime Java περιλαμβάνει τις εξαρτήσεις απόδοσης PDF (είναι ενσωματωμένες στη βιβλιοθήκη).

## Πρακτικές εφαρμογές
1. **Επεξεργασία νομικών εγγράφων** – διαγράψτε ονόματα πελατών πριν τα μοιραστείτε με αντίθετο δικηγόρο.  
2. **Διαχείριση αρχείων HR** – κρύψτε αριθμούς υπαλλήλων σε εσωτερικές αναφορές.  
3. **Οικονομική αναφορά** – προστατεύστε αριθμούς λογαριασμών κατά τη διανομή περιλήψεων ελέγχου.  

Μπορείτε να συνδυάσετε αυτά τα βήματα σε αυτοματοποιημένη ροή εργασίας, συνδέοντας το GroupDocs.Redaction με σύστημα διαχείρισης εγγράφων ή αποθήκη cloud.

## Σκέψεις για την απόδοση
- **Επεξεργασία δέσμης:** Επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο `Redactor` όταν επεξεργάζεστε πολλά αρχεία για μείωση του κόστους κατά έως 40 %.  
- **Διαχείριση μνήμης:** Για μεγάλα έγγραφα, καλέστε `System.gc()` μετά από κάθε `redactor.close()` ή εκτελέστε τη διαδικασία σε ξεχωριστό JVM.  
- **Διατηρήστε τις εξαρτήσεις ενημερωμένες:** Οι νέες εκδόσεις περιέχουν βελτιώσεις απόδοσης για ραστερισμό PDF, συμπεριλαμβανομένης μιας αύξησης ταχύτητας κατά 20 % για πολυπύρηνα συστήματα.

## Συχνά προβλήματα και λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| *File not found* | Επαληθεύστε την απόλυτη διαδρομή και βεβαιωθείτε ότι το αρχείο υπάρχει στον διακομιστή. |
| *Permission denied* | Εκτελέστε το JVM με επαρκή δικαιώματα λειτουργικού συστήματος ή αλλάξτε τα ACL του φακέλου εξόδου. |
| *Rasterization produces blank pages* | Επιβεβαιώστε ότι το πηγαίο έγγραφο δεν είναι ήδη ραστερισμένη εικόνα· χρησιμοποιήστε την πιο πρόσφατη έκδοση της βιβλιοθήκης. |
| *Redaction leaves hidden text* | Χρησιμοποιήστε `ExactPhraseRedaction` με `ReplacementOptions`; αποφύγετε τις απλές μεθόδους find‑replace. |

## Συχνές ερωτήσεις

**Ε: Τι είναι η διαγραφή ακριβούς φράσης;**  
Α: Αντικαθιστά μια συγκεκριμένη συμβολοσειρά (π.χ. ένα όνομα) με ένα placeholder, εξασφαλίζοντας ότι το αρχικό κείμενο δεν μπορεί να ανακτηθεί.

**Ε: Πώς ο ραστερισμός PDF βελτιώνει την ασφάλεια;**  
Α: Τα ραστεριζόμενα PDF αποδίδουν κάθε σελίδα ως εικόνα, εμποδίζοντας την επιλογή, αντιγραφή ή επεξεργασία κειμένου.

**Ε: Μπορώ να επεξεργαστώ πολλαπλά αρχεία σε μία εκτέλεση;**  
Α: Ναι—επανάληψη πάνω σε λίστα διαδρομών αρχείων, επαναχρησιμοποιώντας την ίδια διαμόρφωση `Redactor` για κάθε έγγραφο.

**Ε: Είναι δυνατή η ενσωμάτωση με το cloud;**  
Α: Απόλυτα. Μπορείτε να διαβάζετε/γράφετε ροές από AWS S3, Azure Blob ή Google Cloud Storage και να τις τροφοδοτείτε απευθείας στο API.

**Ε: Ποια είναι τα τυπικά λάθη για αρχάριους;**  
Α: Η παράλειψη κλεισίματος του `Redactor` (που κλειδώνει τα αρχεία) και η χρήση παλιάς έκδοσης βιβλιοθήκης που δεν υποστηρίζει ραστερισμό.

## Πόροι
- **Τεκμηρίωση:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Αναφορά API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Λήψη:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Δωρεάν υποστήριξη:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Προσωρινή άδεια:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

**Τελευταία ενημέρωση:** 2026-08-09  
**Δοκιμή με:** GroupDocs.Redaction 24.9 for Java  
**Συγγραφέας:** GroupDocs  

## Σχετικά Μαθήματα

- [How to create grayscale pdf with GroupDocs.Redaction Java – Secure and Optimize Your Documents](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Mastering Document Security in Java: Exact Phrase Redaction and Advanced Rasterization with GroupDocs.Redaction](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [How to Convert DOCX to Image & Redact Word Documents Using GroupDocs Redaction Java](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)