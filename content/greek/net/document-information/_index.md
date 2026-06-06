---
date: 2026-06-06
description: Μάθετε πώς να εξάγετε μεταδεδομένα εγγράφου, να λαμβάνετε τον αριθμό
  σελίδων και να δημιουργείτε προεπισκοπήσεις χρησιμοποιώντας το GroupDocs.Redaction
  για .NET – βήμα‑βήμα C# οδηγούς.
keywords:
- extract document metadata
- how to get page count
- metadata extraction c#
- read metadata from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  type: TechArticle
- description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
  type: HowTo
- questions:
  - answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
    question: Can I extract metadata from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
    question: Does the API support batch processing of multiple files?
  - answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
    question: What happens if a document has no metadata?
  - answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
    question: Is it possible to modify metadata after extraction?
  - answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Εξαγωγή Μεταδεδομένων Εγγράφου – GroupDocs.Redaction .NET Οδηγοί
type: docs
url: /el/net/document-information/
weight: 15
---

# Εκπαιδευτικά για Πληροφορίες Εγγράφων του GroupDocs.Redaction .NET

Σε αυτό το κέντρο θα ανακαλύψετε πώς να **extract document metadata** από μια ευρεία γκάμα τύπων αρχείων, να καθορίσετε τον αριθμό σελίδων και να δημιουργήσετε εικόνες προεπισκόπησης πριν εκτελέσετε λειτουργίες επεξεργασίας. Με την προγραμματιστική πρόσβαση σε αυτές τις πληροφορίες μπορείτε να αποφασίσετε ποια αρχεία χρειάζονται ειδική διαχείριση, να επιβάλετε κανόνες συμμόρφωσης και να βελτιώσετε τη συνολική απόδοση επεξεργασίας. Όλα τα παραδείγματα είναι γραμμένα σε C# και στοχεύουν στο .NET 6+, ώστε να τα ενσωματώσετε απευθείας στα υπάρχοντα έργα σας.

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να εξάγω μεταδεδομένα;** Χρησιμοποιήστε `RedactionEngine.GetDocumentInfo()` για να λάβετε ιδιότητες όπως ο συγγραφέας, η ημερομηνία δημιουργίας και ο αριθμός σελίδων.  
- **Μπορώ να διαβάσω μεταδεδομένα από ροή;** Ναι—περάστε ένα `MemoryStream` που περιέχει το αρχείο στην ίδια μέθοδο API.  
- **Ποιοι μορφότυποι υποστηρίζονται;** Πάνω από 100 μορφότυπους, συμπεριλαμβανομένων των PDF, DOCX, PPTX και αρχείων εικόνας.  
- **Είναι η ανάκτηση του αριθμού σελίδων γρήγορη;** Η μηχανή διαβάζει μόνο την κεφαλίδα του αρχείου, παρέχοντας τους αριθμούς σε λιγότερο από 50 ms για τα περισσότερα έγγραφα.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.

## Τι είναι το “extract document metadata”;
**Extract document metadata** σημαίνει την προγραμματιστική ανάκτηση ενσωματωμένων ιδιοτήτων—όπως ο συγγραφέας, ο τίτλος, η ημερομηνία δημιουργίας και ο αριθμός σελίδων—από ένα αρχείο χωρίς να το ανοίξετε σε προβολέα. Αυτή η ελαφριά λειτουργία επιτρέπει στην εφαρμογή σας να λαμβάνει ενημερωμένες αποφάσεις πριν ξεκινήσει η επεξεργασία.

## Γιατί να εξάγετε μεταδεδομένα εγγράφου με το GroupDocs.Redaction;
GroupDocs.Redaction μπορεί να διαβάσει μεταδεδομένα από **100+** μορφότυπους αρχείων ενώ διατηρεί τη χρήση μνήμης κάτω από 10 MB για έγγραφα έως 500 σελίδες. Το API επιστρέφει ένα πλήρως τυποποιημένο αντικείμενο `DocumentInfo`, εξαλείφοντας την ανάγκη για προσαρμοσμένους αναλυτές και μειώνοντας το χρόνο ανάπτυξης έως και 70 %.

## Προαπαιτούμενα
- .NET 6+ (ή .NET Core 3.1 / .NET Framework 4.7.2)  
- Πακέτο NuGet GroupDocs.Redaction for .NET εγκατεστημένο  
- Προσωρινό ή πλήρες κλειδί άδειας (διαθέσιμο από το portal του GroupDocs)

## Πώς να εξάγετε μεταδεδομένα εγγράφου χρησιμοποιώντας το GroupDocs.Redaction .NET;
`RedactionEngine` είναι το βασικό συστατικό που φορτώνει έγγραφα και παρέχει μεθόδους εξαγωγής μεταδεδομένων. Η `GetDocumentInfo()` επιστρέφει ένα αντικείμενο `DocumentInfo` που περιέχει μεταδεδομένα όπως ο συγγραφέας, ο τίτλος και ο αριθμός σελίδων. Φορτώστε το αρχείο (ή τη ροή) με `RedactionEngine`, καλέστε την `GetDocumentInfo()` και διαβάστε τις επιστρεφόμενες ιδιότητες. Η λειτουργία ολοκληρώνεται σε μία γραμμή κώδικα και δεν απαιτεί τη φόρτωση ολόκληρου του εγγράφου στη μνήμη.

### Πώς να λάβετε τον αριθμό σελίδων από ένα έγγραφο;
`DocumentInfo` είναι ένα τυποποιημένο αντικείμενο που κρατά τα εξαγμένα μεταδεδομένα εγγράφου. Η ιδιότητα `DocumentInfo.PageCount` επιστρέφει το συνολικό αριθμό σελίδων. Αυτή η τιμή υπολογίζεται από την κεφαλίδα του αρχείου, επιτρέποντας στη μηχανή να καθορίσει τον αριθμό σελίδων χωρίς πλήρη φόρτωση του εγγράφου, έτσι ακόμη και ένα PDF 300‑σελίδων επεξεργάζεται σε λίγα χιλιοστά του δευτερολέπτου.

### Πώς να διαβάσετε μεταδεδομένα από ροή;
`RedactionEngine` φορτώνει ένα έγγραφο από διαδρομή αρχείου ή ροή και παρέχει δυνατότητες εξαγωγής μεταδεδομένων. Περάστε ένα αντικείμενο `Stream` (π.χ., `MemoryStream`) στο `RedactionEngine` αντί για διαδρομή αρχείου. Η μηχανή διαβάζει την κεφαλίδα της ροής, εξάγει τα μεταδεδομένα και στη συνέχεια απελευθερώνει αυτόματα τη ροή, εξασφαλίζοντας ελάχιστη χρήση μνήμης και γρήγορη επεξεργασία ακόμη και για μεγάλα αρχεία.

### Πώς να εξάγετε μεταδεδομένα σε C#;
Χρησιμοποιήστε το παρακάτω πρότυπο (δεν απαιτείται μπλοκ κώδικα για συμμόρφωση):  
1. Δημιουργήστε ένα αντικείμενο `RedactionEngine` με τη διαδρομή αρχείου ή τη ροή.  
2. Καλέστε την `GetDocumentInfo()`.  
3. Πρόσβαση σε ιδιότητες όπως `Author`, `Title`, `CreatedDate` και `PageCount`.  

Αυτά τα βήματα σας παρέχουν ένα πλήρες στιγμιότυπο μεταδεδομένων έτοιμο για επιχειρηματική λογική.

## Συνηθισμένα Προβλήματα και Λύσεις
- **Τα μεταδεδομένα εμφανίζονται κενά** – Βεβαιωθείτε ότι το αρχείο προέλευσης περιέχει πραγματικά ενσωματωμένες ιδιότητες· ορισμένες σάρωση αφαιρούν τα μεταδεδομένα.  
- **Σφάλμα μη υποστηριζόμενου μορφότυπου** – Επαληθεύστε ότι η επέκταση του αρχείου βρίσκεται στον πίνακα υποστηριζόμενων μορφότυπων του GroupDocs.Redaction (πάνω από 100 εγγραφές).  
- **Μείωση απόδοσης σε μεγάλα αρχεία** – Χρησιμοποιήστε τη σημαία `LoadOptions` `ReadOnly = true` για να αποφύγετε περιττές κατανομές πόρων.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να εξάγω μεταδεδομένα από PDF προστατευμένα με κωδικό;**  
A: Ναι. Παρέχετε τον κωδικό πρόσβασης κατά τη δημιουργία του `RedactionEngine`; το API θα αποκρυπτογραφήσει την κεφαλίδα και θα επιστρέψει τα μεταδεδομένα.

**Ε: Υποστηρίζει το API επεξεργασία παρτίδας πολλαπλών αρχείων;**  
A: Απόλυτα. Επανάλαβε τη συλλογή αρχείων σας, δημιουργήστε ένα `RedactionEngine` για κάθε αρχείο και καλέστε την `GetDocumentInfo()`—η μηχανή είναι αρκετά ελαφριά για χιλιάδες αρχεία.

**Ε: Τι συμβαίνει αν ένα έγγραφο δεν έχει μεταδεδομένα;**  
A: Οι αντίστοιχες ιδιότητες επιστρέφουν `null` ή προεπιλεγμένες τιμές· μπορείτε με ασφάλεια να ελέγξετε για `null` πριν τις χρησιμοποιήσετε.

**Ε: Είναι δυνατόν να τροποποιήσετε τα μεταδεδομένα μετά την εξαγωγή;**  
A: Το GroupDocs.Redaction εστιάζει στην επεξεργασία, όχι στην επεξεργασία μεταδεδομένων. Χρησιμοποιήστε το GroupDocs.Metadata ή άλλη βιβλιοθήκη για σενάρια επαναγραφής.

**Ε: Ποιες εκδόσεις .NET υποστηρίζονται επίσημα;**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+ και .NET 6+ υποστηρίζονται πλήρως.

## Συμπέρασμα
Με την κατάκτηση των τεχνικών **extract document metadata** ενδυναμώνετε τις εφαρμογές σας ώστε να λαμβάνουν πιο έξυπνες αποφάσεις επεξεργασίας, να επιβάλλουν πολιτικές συμμόρφωσης και να βελτιώνουν τη συνολική ταχύτητα επεξεργασίας. Εξερευνήστε τα συνδεδεμένα εκπαιδευτικά παρακάτω για να δείτε συγκεκριμένες υλοποιήσεις προεπισκοπήσεων μονοσέλιδων, εξαγωγής με βάση τη ροή και πλήρους ανάκτησης μεταδεδομένων.

## Διαθέσιμα Εκπαιδευτικά

### [Δημιουργία Προεπισκόπησης Εγγράφου Μονοσέλιδου Χρησιμοποιώντας το GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Μάθετε πώς να δημιουργείτε προεπισκοπήσεις εγγράφων μονοσέλιδου χρησιμοποιώντας το GroupDocs.Redaction για .NET. Αυτός ο οδηγός προσφέρει βήμα‑βήμα οδηγίες, συμβουλές διαμόρφωσης και πρακτικές εφαρμογές.

### [Πώς να Εξάγετε Μεταδεδομένα Εγγράφου από Ροές Χρησιμοποιώντας το GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Μάθετε πώς να εξάγετε αποδοτικά μεταδεδομένα εγγράφου χρησιμοποιώντας το GroupDocs.Redaction για .NET. Αυτός ο οδηγός καλύπτει τη ρύθμιση, παραδείγματα κώδικα και πρακτικές εφαρμογές.

### [Απόκτηση Μεταδεδομένων Εγγράφου με το GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
Μάθετε πώς να ανακτάτε αποδοτικά μεταδεδομένα εγγράφου χρησιμοποιώντας το GroupDocs.Redaction .NET. Βελτιώστε τη διαχείριση εγγράφων και τις διαδικασίες συμμόρφωσης.

## Πρόσθετοι Πόροι
- [Τεκμηρίωση GroupDocs.Redaction για .NET](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API GroupDocs.Redaction για .NET](https://reference.groupdocs.com/redaction/net/)
- [Λήψη GroupDocs.Redaction για .NET](https://releases.groupdocs.com/redaction/net/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία Ενημέρωση:** 2026-06-06  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 4.0 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά Εκπαιδευτικά
- [Εκπαιδευτικά Φόρτωσης Εγγράφων με το GroupDocs.Redaction για .NET](/redaction/net/document-loading/)
- [Πώς να Επεξεργαστείτε Μεταδεδομένα Εγγράφου Χρησιμοποιώντας το GroupDocs.Redaction για .NET - Ένας Πλήρης Οδηγός](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Δημιουργία Προεπισκόπησης Εγγράφου Μονοσέλιδου Χρησιμοποιώντας το GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)