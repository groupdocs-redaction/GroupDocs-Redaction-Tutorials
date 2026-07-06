---
date: '2026-07-06'
description: Μάθετε πώς να αποκρύπτετε έγγραφα .net χρησιμοποιώντας streams με το
  GroupDocs.Redaction. Αυτό το σεμινάριο καλύπτει τη ρύθμιση, τη φόρτωση εγγράφου
  από stream, την εφαρμογή redactions, και την ασφαλή αποθήκευση.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: Απόκρυψη εγγράφων .net χρησιμοποιώντας Streams – GroupDocs.Redaction Οδηγός
type: docs
url: /el/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# Απόκρυψη εγγράφων .net χρησιμοποιώντας Ροές – Ένας Πλήρης Οδηγός

Καλώς ήρθατε! Σε αυτό το σεμινάριο θα ανακαλύψετε πώς να **redact documents .net** με ασφάλεια χρησιμοποιώντας ροές με το GroupDocs.Redaction. Θα περάσουμε από όλα όσα χρειάζεστε—από την εγκατάσταση της βιβλιοθήκης, τη φόρτωση ενός εγγράφου από ροή, την εφαρμογή ακριβών αποκρύψεων, έως την αποθήκευση του αποτελέσματος χωρίς να αφήνουμε προσωρινά αρχεία στο δίσκο.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται την απόκρυψη σε .NET;** GroupDocs.Redaction for .NET.  
- **Μπορώ να φορτώσω ένα αρχείο απευθείας από ροή;** Yes—use `FileStream` with the Redactor constructor.  
- **Ποιοι μορφότυποι υποστηρίζονται;** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **Χρειάζομαι άδεια για παραγωγή;** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **Είναι ασφαλές για μεγάλα αρχεία;** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## Τι είναι το “redact documents .net”;
**“Redact documents .net”** αναφέρεται στη διαδικασία της μόνιμης αφαίρεσης ή κάλυψης ευαίσθητου περιεχομένου από αρχεία χρησιμοποιώντας .NET βιβλιοθήκες όπως το GroupDocs.Redaction. Αυτό εξασφαλίζει ότι τα εμπιστευτικά δεδομένα δεν αφήνουν ποτέ το σύστημά σας σε απλό κείμενο. Χρησιμοποιείται συνήθως στους νομικούς, οικονομικούς και τομείς υγειονομικής περίθαλψης για συμμόρφωση με κανονισμούς προστασίας προσωπικών δεδομένων όπως GDPR και HIPAA, διασφαλίζοντας ότι τα ευαίσθητα δεδομένα δεν μπορούν να ανακτηθούν μετά την επεξεργασία.

## Γιατί να χρησιμοποιήσετε ροές για την απόκρυψη;
Το GroupDocs.Redaction υποστηρίζει **70+ μορφότυπους αρχείων** και μπορεί να επεξεργαστεί αρχεία έως **2 GB** χωρίς να τα φορτώνει πλήρως στη μνήμη. Η ροή μειώνει το φορτίο I/O, βελτιώνει την απόδοση και ευθυγραμμίζεται με τις βέλτιστες πρακτικές ασφαλείας διατηρώντας τα δεδομένα στη μνήμη μόνο για το σύντομο χρονικό διάστημα που απαιτείται για τη μετατροπή.

## Προαπαιτούμενα
- **GroupDocs.Redaction for .NET** – install via NuGet (see below).  
- **.NET 6+** (or .NET Framework 4.6.1+).  
- Visual Studio 2022 ή οποιοδήποτε συμβατό IDE.  
- Βασικές γνώσεις C# και εξοικείωση με .NET streams.

## Εγκατάσταση του GroupDocs.Redaction
Μπορείτε να προσθέσετε το πακέτο με οποιαδήποτε από αυτές τις εντολές:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

Ή εντοπίστε το “GroupDocs.Redaction” στο UI του NuGet Package Manager και κάντε κλικ στο **Install**.

### Βήματα Απόκτησης Άδειας
1. **Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – request a short‑term key for evaluation.  
3. **Full Purchase** – obtain a permanent license for production workloads.

Μόλις εγκατασταθεί, αρχικοποιήστε τη βιβλιοθήκη στον κώδικά σας:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## Πώς να φορτώσετε ένα έγγραφο από ροή;
Ένα `FileStream` παρέχει μια ροή για ανάγνωση και εγγραφή σε αρχείο στο δίσκο. Η κλάση `Redactor` επεξεργάζεται το έγγραφο και εφαρμόζει κανόνες απόκρυψης. Φορτώστε το αρχικό αρχείο σας σε ένα `FileStream`, στη συνέχεια περάστε τη ροή στον κατασκευαστή του `Redactor`. Αυτή η προσέγγιση αποφεύγει τη δημιουργία του αρχικού αρχείου σε προσωρινή τοποθεσία και διατηρεί τα δεδομένα στη μνήμη μόνο για τη διάρκεια της επεξεργασίας. Αυτή η μέθοδος λειτουργεί για οποιονδήποτε υποστηριζόμενο μορφότυπο, συμπεριλαμβανομένων των PDF και εγγράφων Office.

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## Πώς να αρχικοποιήσετε το Redactor με τη ροή;
Η κλάση `Redactor` είναι η κύρια μηχανή που χειρίζεται το περιεχόμενο του εγγράφου. Παρέχοντας τη ροή εισόδου, ενεργοποιείτε την απόκρυψη στη μνήμη χωρίς ενδιάμεσα αρχεία. Μετά τη δημιουργία του αντικειμένου, μπορείτε να συνδυάσετε κανόνες απόκρυψης, να προεπισκοπήσετε τις αλλαγές και να διαμορφώσετε επιλογές όπως rasterization ή κρυπτογράφηση πριν υποβάλετε το τελικό έγγραφο.

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Αγκύρωση ορισμού:** `GroupDocs.Redaction.Redactor` is the primary class that provides methods to apply, preview, and commit redaction operations on a document loaded from a stream.

## Πώς να εφαρμόσετε αποκρύψεις;
Μπορείτε να προσθέσετε πολλαπλές ενέργειες απόκρυψης· το παρακάτω παράδειγμα διαγράφει όλες τις σημειώσεις, κάτι που είναι κοινή απαίτηση για την αφαίρεση κρυφών σχολίων ή σημειώσεων ελεγκτή. Πρόσθετοι τύποι απόκρυψης όπως `DeleteTextRedaction` ή `ReplaceTextRedaction` μπορούν να συνδυαστούν για την αφαίρεση ή κάλυψη συγκεκριμένων συμβολοσειρών, ημερομηνιών ή προτύπων σε όλο το έγγραφο.

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Αγκύρωση ορισμού:** `DeleteAnnotationRedaction` is a built‑in redaction rule that permanently erases annotation objects such as comments, highlights, and stamps from the document.

## Πώς να αποθηκεύσετε το έγγραφο με απόκρυψη;
Η αποθήκευση απευθείας σε ένα `FileStream` εξασφαλίζει ότι το αποτέλεσμα γράφεται σε μία μόνο διέλευση, εξαλείφοντας περιττά προσωρινά αρχεία. Μπορείτε επίσης να καθορίσετε μορφότυπο εξόδου, επίπεδο συμπίεσης και προαιρετική προστασία με κωδικό μέσω του αντικειμένου `SaveOptions` για να πληρούν τις απαιτήσεις ασφαλείας. Τέλος, κλείστε τη ροή εξόδου για να απελευθερώσετε τους χειριστές αρχείων και να διασφαλίσετε ότι το αρχείο έχει γραφτεί πλήρως στο δίσκο.

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Αγκύρωση ορισμού:** `SaveOptions` lets you control how the document is persisted, including rasterization, encryption, and format selection.

## Συνηθισμένες Περιπτώσεις Χρήσης
- **Διαχείριση νομικών εγγράφων:** Αφαίρεση εμπιστευτικών σημειώσεων πριν από την κοινοποίηση των προσχεδίων στους πελάτες.  
- **Συμμόρφωση με GDPR:** Αφαίρεση προσωπικών αναγνωριστικών από συμβάσεις ή αρχεία υπαλλήλων.  
- **Εσωτερικές εκθέσεις ελέγχου:** Απόκρυψη σημειώσεων ελεγκτή ενώ διατηρείται το βασικό περιεχόμενο για διανομή.

## Συμβουλές Απόδοσης για Μεγάλα Αρχεία
1. **Αποδεσμεύστε τις ροές άμεσα** – οι δηλώσεις `using` κλείνουν αυτόματα τις ροές, ελευθερώνοντας μνήμη.  
2. **Επεξεργασία σε παρτίδες** – Επανάληψη σε μια συλλογή αρχείων και επαναχρησιμοποίηση ενός μοναδικού αντικειμένου `Redactor` όταν το μορφότυπο το επιτρέπει, μειώνοντας το κόστος κατανομής.  

## Επίλυση Προβλημάτων
1. **Απαγορευμένη πρόσβαση σε αρχείο** – Επαληθεύστε ότι ο λογαριασμός της εφαρμογής έχει δικαιώματα ανάγνωσης/εγγραφής στους προορισμένους φακέλους.  
2. **Η απόκρυψη δεν εφαρμόστηκε** – Βεβαιωθείτε ότι ο τύπος απόκρυψης που επιλέξατε είναι συμβατός με το μορφότυπο του εγγράφου (π.χ., το `DeleteAnnotationRedaction` λειτουργεί για PDF και DOCX).  

## Συχνές Ερωτήσεις
**Q: Ποιοι μορφότυποι αρχείων μπορούν να επεξεργαστούν με ροές;**  
A: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX, PPTX, and HTML—when using stream‑based APIs.

**Q: Μπορώ να προεπισκοπήσω τις αποκρύψεις πριν την αποθήκευση;**  
A: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation that you can render or inspect programmatically.

**Q: Πώς η βιβλιοθήκη διαχειρίζεται αρχεία με προστασία κωδικού;**  
A: Supply the password when opening the stream via `Redactor` overloads that accept `LoadOptions` containing the password.

**Q: Υπάρχει όριο στο μέγεθος του εγγράφου;**  
A: The engine can process files up to 2 GB; larger files should be split or processed in chunks to stay within memory limits.

**Q: Χρειάζομαι ξεχωριστή άδεια για κάθε περιβάλλον ανάπτυξης;**  
A: A single license key can be used across multiple environments as long as the usage complies with the licensing agreement.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, βήμα‑βήμα λύση για **redact documents .net** χρησιμοποιώντας ροές με το GroupDocs.Redaction. Φορτώνοντας αρχεία απευθείας από ροές, εφαρμόζοντας στοχευμένες αποκρύψεις και αποθηκεύοντας χωρίς ενδιάμεσα τεχνουργήματα, επιτυγχάνετε τόσο την ασφάλεια όσο και την απόδοση. Εξερευνήστε πρόσθετους τύπους αποκρύψεων—όπως αντικατάσταση κειμένου ή αφαίρεση μεταδεδομένων—για να προσαρμόσετε τη διαδικασία στις συγκεκριμένες ανάγκες συμμόρφωσης σας.

---

**Τελευταία Ενημέρωση:** 2026-07-06  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 5.0 for .NET  
**Συγγραφέας:** GroupDocs  

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη](https://releases.groupdocs.com/redaction/net/)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/redaction/33)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## Σχετικά Μαθήματα
- [Πώς να φορτώσετε και να αποκρύψετε έγγραφα χρησιμοποιώντας το GroupDocs.Redaction .NET&#58; Ένας πλήρης οδηγός](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Απόκρυψη και αποθήκευση εγγράφων με το GroupDocs.Redaction για .NET&#58; Ένας πλήρης οδηγός](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Πώς να εξάγετε μεταδεδομένα εγγράφου από ροές χρησιμοποιώντας το GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)