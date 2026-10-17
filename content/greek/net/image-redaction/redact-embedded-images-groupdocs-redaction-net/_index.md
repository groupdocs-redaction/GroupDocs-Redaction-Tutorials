---
date: '2026-10-16'
description: Μάθετε πώς να χρησιμοποιήσετε το GroupDocs για να αποκρύψετε ενσωματωμένες
  εικόνες σε έγγραφα Word χρησιμοποιώντας το GroupDocs.Redaction .NET API, διασφαλίζοντας
  την ασφάλεια των ευαίσθητων δεδομένων.
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: Πώς να χρησιμοποιήσετε το GroupDocs για να αποκρύψετε ενσωματωμένες
  εικόνες σε έγγραφα Word με το .NET API. Προστατέψτε τα εμπιστευτικά οπτικά στοιχεία
  γρήγορα και αξιόπιστα.
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: Πώς να χρησιμοποιήσετε το GroupDocs για να αποκρύψετε εικόνες σε Word με
  .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: Πώς να χρησιμοποιήσετε το GroupDocs για να αποκρύψετε εικόνες σε Word με .NET
type: docs
url: /el/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το GroupDocs για να διαγράψετε εικόνες σε Word με .NET

Όταν χρειάζεται να προστατεύσετε εμπιστευτικά οπτικά στοιχεία σε ένα αρχείο Microsoft Word, το **πώς να χρησιμοποιήσετε το GroupDocs** γίνεται το πρώτο ερώτημα. Αυτό το tutorial σας καθοδηγεί βήμα προς βήμα για να εντοπίσετε, να καλύψετε και να αφαιρέσετε μόνιμα τις ενσωματωμένες εικόνες ώστε οι ευαίσθητες πληροφορίες να μην διαρρεύσουν.

## Γρήγορες απαντήσεις
- **Μπορεί το GroupDocs να διαγράψει αυτόματα όλες τις εικόνες;** Ναι, μπορείτε να επαναλάβετε για κάθε εικόνα και να εφαρμόσετε `ImageAreaRedaction`.
- **Ποιες εκδόσεις του .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια δωρεάν δοκιμή λειτουργεί για δοκιμές· απαιτείται μόνιμη άδεια για παραγωγή.
- **Θα διατηρηθεί η αρχική διάταξη;** Το API διατηρεί το κείμενο και τη μορφοποίηση αμετάβλητα ενώ αδειάζει την περιοχή της εικόνας.
- **Πόσο γρήγορη είναι η διαδικασία;** Το GroupDocs.Redaction μπορεί να επεξεργαστεί έγγραφα 200 σελίδων σε λιγότερο από 2 δευτερόλεπτα σε τυπικό διακομιστή.

## Τι είναι το GroupDocs.Redaction;
Το GroupDocs.Redaction είναι μια βιβλιοθήκη .NET που επιτρέπει προγραμματισμένη διαγραφή κειμένου, εικόνων και μεταδεδομένων σε περισσότερα από 20 μορφότυπα εγγράφων. Επεξεργάζεται αρχεία χωρίς να απαιτείται εγκατεστημένο Microsoft Office, καθιστώντας το ιδανικό για αυτοματοποίηση στο διακομιστή. Παρέχει API για διαγραφή κειμένου, εικόνων και μεταδεδομένων, και υποστηρίζει επεξεργασία σε παρτίδες, προσαρμοσμένα πρότυπα διαγραφής και αναφορές συμμόρφωσης.

## Γιατί να χρησιμοποιήσετε το GroupDocs για διαγραφή εικόνων σε Word;
Η βιβλιοθήκη υποστηρίζει **πάνω από 20 μορφές εισόδου και εξόδου** και μπορεί να διαγράψει εικόνες σε έγγραφα έως 500 MB χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Ο ενσωματωμένος αλγόριθμος `ImageAreaRedaction` εγγυάται ότι η διαγραμμένη περιοχή δεν μπορεί να ανακτηθεί, πληρώντας αυστηρά πρότυπα συμμόρφωσης.

## Προαπαιτούμενα
- .NET Framework 4.5+ **ή** .NET Core 3.1+ εγκατεστημένο.
- Βασικές γνώσεις C# και εξοικείωση με τη δομή αρχείων Word.
- Πρόσβαση στο πακέτο NuGet **GroupDocs.Redaction** (δωρεάν δοκιμή ή με άδεια).

## Πώς να ρυθμίσετε το GroupDocs.Redaction για .NET

### Πώς να εγκαταστήσετε το GroupDocs.Redaction μέσω .NET CLI;
Εκτελέστε την παρακάτω εντολή στον φάκελο του έργου σας: `dotnet add package GroupDocs.Redaction`. Αυτό προσθέτει την πιο πρόσφατη σταθερή έκδοση στο αρχείο του έργου σας.

```bash
dotnet add package GroupDocs.Redaction
```

### Πώς να εγκαταστήσετε το GroupDocs.Redaction χρησιμοποιώντας το Package Manager;
Εκτελέστε `Install-Package GroupDocs.Redaction` στην κονσόλα Package Manager.

```powershell
Install-Package GroupDocs.Redaction
```

### Πώς να αποκτήσετε και να εφαρμόσετε προσωρινή άδεια;
Μπορείτε να ζητήσετε μια προσωρινή άδεια από τη σελίδα [Temporary License](https://purchase.groupdocs.com/temporary-license/).  
Μια προσωρινή άδεια σας επιτρέπει να αξιολογήσετε το πλήρες σύνολο λειτουργιών χωρίς υδατογραφήματα. Μετά την αγορά, τοποθετήστε το αρχείο άδειας στο έργο σας και φορτώστε το όπως φαίνεται:

```csharp
using GroupDocs.Redaction;
```

## Πώς να διαγράψετε ενσωματωμένες εικόνες σε έγγραφο Word;
Για να διαγράψετε εικόνες, φορτώνετε το έγγραφο με μια παρουσία Redactor, εντοπίζετε κάθε εικόνα, ορίζετε την περιοχή που θα κρυφτεί και εφαρμόζετε το ImageAreaRedaction. Το API αντικαθιστά τα επιλεγμένα pixel, εξασφαλίζοντας ότι το αρχικό οπτικό περιεχόμενο δεν μπορεί να ανακτηθεί, ενώ διατηρεί τη γύρω διάταξη και το κείμενο.

### Πώς να προετοιμάσετε τις διαδρομές προέλευσης και εξόδου;
Ορίστε τις απόλυτες διαδρομές για το αρχικό έγγραφο και το αποτέλεσμα της διαγραφής πριν δημιουργήσετε οποιαδήποτε αντικείμενα.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### Πώς να δημιουργήσετε και να διαμορφώσετε το αντικείμενο Redactor;
Το Redactor είναι η κεντρική κλάση που φορτώνει ένα έγγραφο και εκτελεί λειτουργίες διαγραφής.  
Δημιουργήστε μια παρουσία του `Redactor` με το έγγραφό σας:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### Πώς να καθορίσετε συντεταγμένες και να εφαρμόσετε διαγραφή περιοχής εικόνας;
Το ImageAreaRedaction είναι μια μέθοδος που καλύπτει μια ορθογώνια περιοχή μιας εικόνας με ένα συμπαγές χρώμα.  
Εντοπίστε το σημείο επάνω‑αριστερά (`samplePoint`) και το μέγεθος (`sampleSize`) της περιοχής που θέλετε να κρύψετε, στη συνέχεια καλέστε το `ImageAreaRedaction`. Αυτή η μέθοδος αντικαθιστά τα επιλεγμένα pixel με ένα συμπαγές χρώμα.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### Πώς να επαληθεύσετε το αποτέλεσμα της διαγραφής και να αποθηκεύσετε το αρχείο;
Μετά την κλήση του `Redactor.Apply()`, ελέγξτε το αντικείμενο `Result`. Εάν το `IsSuccess` είναι true, γράψτε το τροποποιημένο έγγραφο στη διαδρομή εξόδου.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## Συχνά προβλήματα και συμβουλές αντιμετώπισης
- **Σφάλματα συντεταγμένων:** Βεβαιωθείτε ότι οι τιμές X/Y βρίσκονται εντός των ορίων της εικόνας· διαφορετικά το API ρίχνει `ArgumentOutOfRangeException`.
- **Απουσία άδειας:** Μια δοκιμαστική άδεια λήγει μετά από 30 ημέρες· αντικαταστήστε την με μόνιμη για να αποφύγετε σφάλματα χρόνου εκτέλεσης.
- **Μη υποστηριζόμενη μορφή:** Επαληθεύστε ότι η επέκταση αρχείου βρίσκεται μεταξύ των 20+ μορφών που αναφέρονται στην τεκμηρίωση· παλαιότερα αρχεία `.doc` μπορεί να χρειάζονται μετατροπή σε `.docx` πρώτα.

## Πρακτικές εφαρμογές

1. **Εμπιστευτικές αναφορές:** Διαγράψτε λογότυπα ή διαγράμματα πριν από εξωτερική διανομή.
2. **Νομικά σημειώματα:** Κρύψτε φωτογραφίες πελατών ή σαρωμένα αναγνωριστικά που περιέχουν προσωπικά δεδομένα.
3. **Επιχειρηματικές συμβάσεις:** Καλύψτε ιδιόκτητα διαγράμματα που αποκαλύπτουν εμπορικά μυστικά.
4. **Κυβερνητικές κυκλοφορίες:** Αφαιρέστε ευαίσθητες δορυφορικές εικόνες από δημόσια PDF που δημιουργούνται από Word.

## Σκέψεις απόδοσης
- Επεξεργαστείτε τα έγγραφα διαδοχικά όταν διαχειρίζεστε μεγάλες παρτίδες για να διατηρήσετε τη χρήση μνήμης χαμηλή.
- Χρησιμοποιήστε το `RedactorOptions` για να περιορίσετε τον αριθμό των νημάτων εάν τρέχετε σε περιορισμένο διακομιστή.
- Αποδεσμεύστε άμεσα την παρουσία `Redactor` με `using` για να ελευθερώσετε μη διαχειριζόμενους πόρους.

## Συμπέρασμα
Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε το GroupDocs** για να διαγράψετε αξιόπιστα ενσωματωμένες εικόνες σε αρχεία Word χρησιμοποιώντας το .NET API. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να ενσωματώσετε αυτή τη δυνατότητα σε οποιοδήποτε pipeline επεξεργασίας εγγράφων, διασφαλίζοντας ότι τα εμπιστευτικά οπτικά στοιχεία δεν θα φύγουν ποτέ από τον οργανισμό σας.

Για πιο βαθιά εξερεύνηση, πειραματιστείτε με άλλους τύπους διαγραφής (κείμενο, μεταδεδομένα) και ενσωματώστε τη βιβλιοθήκη σε web services, background workers ή Azure Functions.

## Συχνές ερωτήσεις

**Ε: Μπορώ να διαγράψω πολλές εικόνες σε μία εκτέλεση;**  
Α: Ναι, επαναλάβετε για κάθε κόμβο εικόνας και καλέστε `ImageAreaRedaction` για κάθε περιοχή που χρειάζεται να κρύψετε.

**Ε: Υποστηρίζει το GroupDocs.Redaction αρχεία Word προστατευμένα με κωδικό;**  
Α: Απόλυτα. Παρέχετε τον κωδικό όταν δημιουργείτε το αντικείμενο `Redactor`, και η βιβλιοθήκη θα ανοίξει το έγγραφο με ασφάλεια.

**Ε: Ποιες μορφές αρχείων μπορώ να επεξεργαστώ εκτός από DOCX;**  
Α: Το API διαχειρίζεται DOC, DOCX, RTF, HTML, PDF και πάνω από 20 άλλες μορφές, επιτρέποντάς σας να δημιουργήσετε μια καθολική υπηρεσία διαγραφής.

**Ε: Πώς μπορώ να δοκιμάσω τη διαγραφή χωρίς άδεια;**  
Α: Χρησιμοποιήστε μια προσωρινή άδεια από το portal του GroupDocs· παρέχει πλήρη λειτουργικότητα για 30 ημέρες χωρίς υδατογραφήματα.

**Ε: Πού μπορώ να λάβω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Επισκεφθείτε το φόρουμ [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) για βοήθεια από την κοινότητα ή επικοινωνήστε με τις πωλήσεις του GroupDocs για επιχειρηματική υποστήριξη.

## Πρόσθετοι πόροι

- **Τεκμηρίωση:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **Αναφορά API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Λήψη:** [Latest Releases](https://releases.groupdocs.com/redaction/net/)

---

**Last Updated:** 2026-10-16  
**Tested with:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## Σχετικά tutorials

- [Πώς να διαγράψετε έγγραφα με το GroupDocs.Redaction .NET – Ένας πλήρης οδηγός](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Διαγραφή και αποθήκευση εγγράφων Groupdocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Μάθετε τη διαγραφή ακριβούς φράσης με διάκριση πεζών-κεφαλαίων με το GroupDocs.Redaction .NET για την ασφάλεια εγγράφων](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}