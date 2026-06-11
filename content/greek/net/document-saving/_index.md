---
date: 2026-06-11
description: Μάθετε πώς να εξάγετε διαγραμμένα αρχεία, να διαμορφώσετε φακέλους εξόδου,
  να δημιουργήσετε rasterized PDFs και να αποθηκεύσετε σε ροές χρησιμοποιώντας το
  GroupDocs.Redaction για .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Πώς να εξάγετε διαγραμμένα έγγραφα με το GroupDocs.Redaction .NET
type: docs
url: /el/net/document-saving/
weight: 3
---

# Πώς να Εξάγετε Επεξεργασμένα Έγγραφα με το GroupDocs.Redaction .NET

Σε αυτόν τον ολοκληρωμένο οδηγό θα ανακαλύψετε **πώς να εξάγετε επεξεργασμένο** περιεχόμενο με ασφάλεια και αποδοτικότητα χρησιμοποιώντας το GroupDocs.Redaction για .NET. Είτε χρειάζεστε να διατηρήσετε τον αρχικό τύπο αρχείου, είτε να κλειδώσετε το έγγραφο ως rasterized PDF, είτε να μεταδώσετε το αποτέλεσμα απευθείας στη μνήμη, σας καθοδηγούμε βήμα-βήμα με σαφείς, συνομιλιακές εξηγήσεις και πρακτικές συμβουλές. Στο τέλος αυτού του σεμιναρίου θα μπορείτε να επιλέξετε τη σωστή στρατηγική εξαγωγής για οποιοδήποτε σενάριο συμμόρφωσης.

## Γρήγορες Απαντήσεις
- **Σε ποιες μορφές μπορώ να εξάγω;** Οποιαδήποτε από τις 30+ εγγενείς μορφές που υποστηρίζει το GroupDocs.Redaction, συν rasterized PDF για μέγιστη ασφάλεια.  
- **Χρειάζομαι άδεια για streaming;** Ναι, απαιτείται έγκυρη άδεια GroupDocs.Redaction για παραγωγικό streaming.  
- **Μπορώ να ορίσω προσαρμοσμένο φάκελο εξόδου;** Απόλυτα – χρησιμοποιήστε την ιδιότητα `OutputPath` ή το `SaveOptions` για να το διαμορφώσετε.  
- **Είναι ασφαλής η rasterization για μεγάλα αρχεία;** Διαχειρίζεται έγγραφα έως 500 σελίδες χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## Τι είναι το GroupDocs.Redaction;
Το GroupDocs.Redaction είναι μια βιβλιοθήκη .NET που αφαιρεί ή καλύπτει προγραμματιστικά ευαίσθητες πληροφορίες από PDFs, Word, Excel, PowerPoint, εικόνες και πολλές άλλες μορφές. Παρέχει ένα υψηλού επιπέδου API για τον ορισμό περιοχών επεξεργασίας, την εφαρμογή πολιτικών και τελικά την εξαγωγή του καθαρισμένου εγγράφου. Αυτό καθιστά εύκολη την ενσωμάτωση δυνατοτήτων επεξεργασίας σε οποιαδήποτε εφαρμογή .NET.

## Γιατί να Εξάγετε Επεξεργασμένα Έγγραφα ως Rasterized PDF;
Τα Rasterized PDF μετατρέπουν κάθε σελίδα σε επίπεδη εικόνα, εξαλείφοντας κρυφά επίπεδα κειμένου που θα μπορούσαν να εξαχθούν αργότερα. Αυτή η μορφή εγγυάται ότι το επεξεργασμένο περιεχόμενο δεν μπορεί να ανακτηθεί, πληρώντας αυστηρά κανονιστικά πρότυπα όπως GDPR και HIPAA. Το GroupDocs.Redaction μπορεί να παράγει rasterized PDF έως 300 dpi, διατηρώντας την οπτική πιστότητα ενώ εξασφαλίζει την ασφάλεια.

## Πώς να Εξάγετε Επεξεργασμένα Έγγραφα;
Φορτώστε το αρχείο προέλευσης, εφαρμόστε τους κανόνες επεξεργασίας, και στη συνέχεια καλέστε τη κατάλληλη μέθοδο αποθήκευσης — είτε `Save` για την αρχική μορφή, `SaveAsRasterizedPdf` για PDF μόνο με εικόνες, είτε `SaveToStream` για επεξεργασία στη μνήμη. Παρακάτω βρίσκεται η βήμα-βήμα ροή εργασίας. Κάθε μέθοδος εξασφαλίζει ότι το επεξεργασμένο περιεχόμενο αφαιρείται μόνιμα ενώ διατηρεί τη ζητούμενη μορφή εξόδου.

### Βήμα 1: Εγκατάσταση του Πακέτου NuGet
Προσθέστε το πιο πρόσφατο πακέτο GroupDocs.Redaction στο έργο σας:

```bash
dotnet add package GroupDocs.Redaction
```

### Βήμα 2: Φόρτωση του Εγγράφου και Ορισμός Επεξεργασιών
Δημιουργήστε μια παρουσία `Redactor`, φορτώστε το αρχείο και καθορίστε τις περιοχές που θέλετε να κρύψετε. Η κλάση `Redactor` παρέχει τη βασική λειτουργικότητα για τη φόρτωση εγγράφων και την εφαρμογή κανόνων επεξεργασίας.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Βήμα 3: Επιλογή της Μεθόδου Εξαγωγής
#### Εξαγωγή στην Αρχική Μορφή
```csharp
redactor.Save("RedactedReport.docx");
```

#### Εξαγωγή ως Rasterized PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Εξαγωγή σε Memory Stream (ιδανικό για web APIs)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

Η μέθοδος `Save` γράφει το επεξεργασμένο έγγραφο σε αρχείο στην αρχική του μορφή. Η `SaveAsRasterizedPdf` δημιουργεί ένα PDF όπου κάθε σελίδα αποδίδεται ως εικόνα, αφαιρώντας τυχόν κρυφό κείμενο. Η `SaveToStream` επιστρέφει το επεξεργασμένο αρχείο ως memory stream, κατάλληλο για απαντήσεις web.

## Πώς να Διαμορφώσετε Φάκελο Εξόδου;
Ορίστε την ιδιότητα `OutputPath` στο `Redactor` ή περάστε ένα προσαρμοσμένο αντικείμενο `SaveOptions` που περιλαμβάνει τον επιθυμητό κατάλογο. Το `OutputPath` είναι μια ιδιότητα του `Redactor` που καθορίζει τον φάκελο όπου γράφονται τα αρχεία εξόδου. Το `SaveOptions` σας επιτρέπει να προσαρμόσετε διάφορες παραμέτρους αποθήκευσης, συμπεριλαμβανομένου του φακέλου εξόδου. Αυτό εξασφαλίζει ότι όλα τα εξαγόμενα αρχεία τοποθετούνται σε προβλέψιμη θέση, απλοποιώντας τις διαδικασίες επεξεργασίας παρτίδας. Μπορείτε επίσης να καθορίσετε υποφακέλους ανά τύπο εγγράφου για να διατηρήσετε τον χώρο εργασίας σας οργανωμένο.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Συχνά Προβλήματα και Λύσεις
- **Η επεξεργασία δεν εφαρμόστηκε:** Επαληθεύστε ότι το πρότυπο αναζήτησης ταιριάζει ακριβώς με το κείμενο του εγγράφου· χρησιμοποιήστε `RegexOptions.IgnoreCase` εάν χρειάζεται. Το `RegexOptions` είναι μια απαρίθμηση που ελέγχει τη συμπεριφορά ταίριαξης κανονικών εκφράσεων, όπως η ευαισθησία σε πεζά/κεφαλαία.
- **Τα μεγάλα αρχεία προκαλούν πίεση μνήμης:** Ενεργοποιήστε τη λειτουργία streaming χρησιμοποιώντας `SaveToStream` και αποφύγετε την κλήση του `Save` σε ολόκληρο το έγγραφο.
- **Το rasterized PDF φαίνεται θολό:** Αυξήστε το DPI στο `RasterizationOptions` (π.χ., 300–600) για να βελτιώσετε την ποιότητα της εικόνας. Το `RasterizationOptions` σας επιτρέπει να ορίσετε παραμέτρους όπως DPI και μορφή εικόνας για την έξοδο rasterized PDF.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να εξάγω σε μορφή που δεν υποστηριζόταν αρχικά;**  
Α: Ναι, το GroupDocs.Redaction μπορεί να μετατρέψει τις περισσότερες εισόδους σε PDF, DOCX, XLSX, PPTX ή rasterized PDF, καλύπτοντας πάνω από 30 μορφές.

**Ε: Πώς η rasterization προστατεύει τα επεξεργασμένα δεδομένα;**  
Α: Με την απόδοση κάθε σελίδας ως επίπεδη εικόνα, αφαιρούνται τυχόν κρυφά επίπεδα κειμένου, καθιστώντας αδύνατη την εξαγωγή του αρχικού περιεχομένου.

**Ε: Είναι δυνατόν να συνδυάσετε πολλαπλούς κανόνες επεξεργασίας;**  
Α: Απόλυτα – μπορείτε να καλέσετε το `Apply` επανειλημμένα ή να περάσετε μια συλλογή από `RedactionOptions` για να επεξεργαστείτε πολλά πρότυπα σε μία διεργασία. Το `RedactionOptions` ορίζει τις ρυθμίσεις για μια ενιαία λειτουργία επεξεργασίας, όπως περιοχή και τύπο αντικατάστασης.

**Ε: Πρέπει να κλείσω το αντικείμενο Redactor;**  
Α: Το `Redactor` υλοποιεί το `IDisposable`; τυλίξτε το σε μπλοκ `using` ή καλέστε `Dispose()` για να απελευθερώσετε άμεσα τους χειριστές αρχείων. Το `IDisposable` είναι μια διεπαφή που παρέχει μηχανισμό απελευθέρωσης μη διαχειριζόμενων πόρων.

**Ε: Ποια .NET runtime έχουν δοκιμαστεί επίσημα;**  
Α: Το GroupDocs.Redaction έχει επικυρωθεί σε .NET Framework 4.6+, .NET Core 3.1+ και .NET 5/6/7.

## Πρόσθετοι Πόροι

### Διαθέσιμα Σεμινάρια
- [Πώς να Αποθηκεύσετε Έγγραφα ως Rasterized PDF Χρησιμοποιώντας το GroupDocs.Redaction για .NET&#58; Ένας Πλήρης Οδηγός](./groupdocs-redaction-net-rasterized-pdfs/)
- [Υλοποίηση Καταλόγου Εξόδου σε .NET με το GroupDocs.Redaction&#58; Ένας Πλήρης Οδηγός](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Επεξεργασία και Αποθήκευση Εγγράφων με το GroupDocs.Redaction για .NET&#58; Ένας Πλήρης Οδηγός](./redact-save-documents-groupdocs-redaction-net/)
- [Αποθήκευση Επεξεργασμένων Εγγράφων στην Αρχική Μορφή Χρησιμοποιώντας το GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Ασφαλής Επεξεργασία Εγγράφων σε .NET Χρησιμοποιώντας Streams&#58; Ένας Οδηγός για το GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Χρήσιμοι Σύνδεσμοι
- [Τεκμηρίωση GroupDocs.Redaction για .NET](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API GroupDocs.Redaction για .NET](https://reference.groupdocs.com/redaction/net/)
- [Λήψη GroupDocs.Redaction για .NET](https://releases.groupdocs.com/redaction/net/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## Σχετικά Σεμινάρια
- [Αποθήκευση Επεξεργασμένων Εγγράφων στην Αρχική Μορφή Χρησιμοποιώντας το GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Πώς να Αποθηκεύσετε Έγγραφα ως Rasterized PDF Χρησιμοποιώντας το GroupDocs.Redaction για .NET: Ένας Πλήρης Οδηγός](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Ασφαλής Επεξεργασία Εγγράφων σε .NET Χρησιμοποιώντας Streams: Ένας Οδηγός για το GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)