---
date: '2026-10-01'
description: Μάθετε πώς να υλοποιήσετε έναν προσαρμοσμένο καταγραφέα c# στο GroupDocs.Redaction
  για .NET, επιτρέποντας λεπτομερή προσαρμοσμένη καταγραφή .net και πιο εύκολη αναφορά
  συμμόρφωσης.
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: Υλοποιήστε έναν προσαρμοσμένο καταγραφέα c# στο GroupDocs.Redaction
  για .NET ώστε να καταγράφετε λεπτομερή logs, να αποθηκεύετε τα redacted έγγραφα
  χωρίς rasterization και να πληροίτε τις απαιτήσεις συμμόρφωσης.
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: Υλοποίηση προσαρμοσμένου καταγραφέα c# στο GroupDocs.Redaction για .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: Υλοποίηση προσαρμοσμένου καταγραφέα c# στο GroupDocs.Redaction για .NET
type: docs
url: /el/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Υλοποίηση προσαρμοσμένου καταγραφέα c# στο GroupDocs.Redaction για .NET

Η διαχείριση των διαγραφών εγγράφων αποδοτικά είναι κρίσιμη, ειδικά όταν χειρίζεστε ευαίσθητες πληροφορίες. Σε αυτόν τον οδηγό θα μάθετε **πώς να υλοποιήσετε έναν προσαρμοσμένο καταγραφέα c#** με το GroupDocs.Redaction για .NET, αποκτώντας πλήρη έλεγχο πάνω στην καταγραφή, τη διαχείριση σφαλμάτων και τα αρχεία ελέγχου. Στο τέλος του σεμιναρίου θα μπορείτε να καταγράψετε προειδοποιήσεις, σφάλματα και πληροφοριακά μηνύματα, να ενσωματώσετε τον καταγραφέα με υπάρχοντα .NET πλαίσια καταγραφής και να αποθηκεύσετε το διαγραμμένο έγγραφο χωρίς rasterization.

## Γρήγορες απαντήσεις
- **Τι κάνει ένας προσαρμοσμένος καταγραφέας c#;** Καταγράφει σφάλματα, προειδοποιήσεις και πληροφοριακά μηνύματα κατά τη διάρκεια της διαγραφής, παρέχοντας ένα αναζητήσιμο αρχείο ελέγχου.  
- **Ποια βιβλιοθήκη παρέχει το interface ILogger;** Το GroupDocs.Redaction για .NET παρέχει το interface `ILogger`.  
- **Μπορώ να αποθηκεύσω το διαγραμμένο έγγραφο χωρίς rasterization;** Ναι – καλέστε `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Χρειάζομαι άδεια για παραγωγική χρήση;** Απαιτείται πλήρης άδεια για παραγωγή· διατίθεται δοκιμαστική άδεια για αξιολόγηση.  
- **Είναι αυτή η προσέγγιση συμβατή με .NET Core / .NET 6+;** Απόλυτα – το ίδιο API λειτουργεί σε .NET Framework, .NET Core, .NET 5 και .NET 6.

## Τι είναι ένας προσαρμοσμένος καταγραφέας c#;

Ένας **προσαρμοσμένος καταγραφέας c#** είναι μια κλάση που υλοποιεί το interface `ILogger` που παρέχεται από το GroupDocs.Redaction. Σας επιτρέπει να κατευθύνετε τα μηνύματα καταγραφής όπου χρειάζεστε — κονσόλα, αρχείο, βάση δεδομένων ή εξωτερικά συστήματα παρακολούθησης — παρέχοντας μια σαφή εικόνα της συνολικής ροής εργασίας διαγραφής.

## Γιατί να χρησιμοποιήσετε προσαρμοσμένη καταγραφή .net με το GroupDocs.Redaction;

Φορτώστε τη διαδικασία διαγραφής σας με λεπτομερείς, αναζητήσιμες καταγραφές που ικανοποιούν τις κανονιστικές απαιτήσεις ελέγχου και επιταχύνουν την αντιμετώπιση προβλημάτων. Το GroupDocs.Redaction υποστηρίζει **70+ μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί έγγραφα έως 500 σελίδες χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, έτσι ένας καλά σχεδιασμένος καταγραφέας προσθέτει ελάχιστο κόστος ενώ παρέχει ανεκτίμητη διαφάνεια.

## Προαπαιτούμενα
- GroupDocs.Redaction για .NET εγκατεστημένο (δείτε την ενότητα **Installation** παρακάτω).  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, VS Code ή το .NET CLI).  
- Βασικές γνώσεις C# και εξοικείωση με ροές αρχείων.  

## Εγκατάσταση

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Αναζητήστε το **"GroupDocs.Redaction"** και εγκαταστήστε την πιο πρόσφατη έκδοση.

## Απόκτηση άδειας

- **Δωρεάν δοκιμή:** Δοκιμάστε το API με προσωρινή άδεια.  
- **Προσωρινή άδεια:** Λάβετε πλήρη πρόσβαση σε λειτουργίες για περιορισμένο χρονικό διάστημα.  
- **Αγορά:** Αποκτήστε μια διαρκή άδεια για παραγωγικές εγκαταστάσεις.

## Οδηγός βήμα‑βήμα

### Πώς να υλοποιήσετε προσαρμοσμένο καταγραφέα σε .NET Core;

Φορτώστε την κλάση `CustomLogger` στο έργο .NET Core και συνδέστε την με το `RedactorSettings`. Ο καταγραφέας λειτουργεί με τον ίδιο τρόπο σε .NET Framework, .NET 5 και .NET 6, ώστε να μπορείτε να μοιράζεστε τον ίδιο κώδικα σε όλες τις πλατφόρμες.

### Βήμα 1: Ορισμός προσαρμοσμένης κλάσης καταγραφέα (καταγραφή προειδοποιήσεων c#)

Η κλάση `CustomLogger` υλοποιεί το `ILogger`.  
CustomLogger είναι μια κλάση ορισμένη από τον χρήστη που υλοποιεί το interface `ILogger` για την καταγραφή γεγονότων διαγραφής.  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**Αγκύρωση ορισμού:** `CustomLogger` είναι μια υλοποίηση ορισμένη από τον χρήστη του interface `ILogger` που καταγράφει γεγονότα διαγραφής.  
**Επεξήγηση:** Η σημαία `HasErrors` σας βοηθά να αποφασίσετε αν θα συνεχίσετε την επεξεργασία. Οι τρεις μέθοδοι αντιστοιχούν στα τρία επίπεδα καταγραφής που θα χρειαστείτε στις περισσότερες περιπτώσεις διαγραφής.

### Βήμα 2: Προετοιμασία διαδρομών αρχείων και άνοιγμα του πηγαίου εγγράφου

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**Αγκύρωση ορισμού:** `Redactor` είναι η κύρια κλάση στο GroupDocs.Redaction που εκτελεί λειτουργίες διαγραφής σε έγγραφο PDF.  
**Γιατί είναι σημαντικό:** Η χρήση βοηθητικών μεθόδων διατηρεί τον κώδικά σας καθαρό και εγγυάται ότι ο φάκελος εξόδου υπάρχει πριν προσπαθήσετε να **αποθηκεύσετε το διαγραμμένο έγγραφο**.

### Βήμα 3: Εφαρμογή διαγραφών χρησιμοποιώντας τον προσαρμοσμένο καταγραφέα

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**Άμεση απάντηση:** Η ροή εργασίας διαγραφής ξεκινά με τη δημιουργία ενός αντικειμένου `Redactor` με `RedactorSettings(logger)`, στη συνέχεια εφαρμόζει αντικείμενα διαγραφής, ελέγχει το `logger.HasErrors` και τελικά καλεί το `redactor.Save` με απενεργοποιημένο το rasterization. Αυτό το μοτίβο εξασφαλίζει ότι κάθε βήμα καταγράφεται και ότι αποθηκεύετε ένα καθαρό έγγραφο μόνο όταν δεν προέκυψαν σφάλματα.  

**Επεξήγηση:**  
1. Η `Redactor` δημιουργείται με `RedactorSettings(logger)`, συνδέοντας τον `CustomLogger` σας.  
2. Μετά την εφαρμογή μιας διαγραφής, ο κώδικας ελέγχει το `logger.HasErrors`. Αν δεν προέκυψαν σφάλματα, το έγγραφο αποθηκεύεται—δείχνοντας τη λογική **save redacted document** χωρίς rasterization.

## Συχνά προβλήματα & αντιμετώπιση σφαλμάτων

- **Απουσία εξόδου καταγραφής:** Επαληθεύστε ότι κάθε μέθοδος `Log*` έχει παρακαμφθεί σωστά.  
- **Εξαιρέσεις πρόσβασης σε αρχείο:** Βεβαιωθείτε ότι η εφαρμογή έχει δικαιώματα ανάγνωσης/εγγραφής για τις διαδρομές πηγής και εξόδου.  
- **Ο καταγραφέας δεν είναι συνδεδεμένος:** Η παράμετρος `RedactorSettings(logger)` είναι απαραίτητη· η παράλειψή της απενεργοποιεί την προσαρμοσμένη καταγραφή.

## Πρακτικές εφαρμογές

1. **Αναφορά συμμόρφωσης:** Εξαγωγή καταγραφών σε CSV ή βάση δεδομένων για αρχεία ελέγχου.  
2. **Παρακολούθηση σφαλμάτων:** Εντοπίστε γρήγορα προβληματικά αρχεία σκανάροντας την έξοδο `LogError`.  
3. **Αυτοματοποίηση ροής εργασίας:** Ενεργοποιήστε επόμενες διεργασίες (π.χ., ειδοποίηση υπεύθυνου συμμόρφωσης) όταν κληθεί το `LogWarning`.

## Σκέψεις απόδοσης

- **Απελευθέρωση ροών άμεσα** για ελευθέρωση μνήμης, ειδικά κατά την επεξεργασία μεγάλων παρτίδων.  
- **Παρακολούθηση CPU & μνήμης** κατά τις μαζικές διαγραφές· σκεφτείτε την επεξεργασία εγγράφων παράλληλα με προσεκτικό συγχρονισμό του καταγραφέα.  
- **Παραμείνετε ενημερωμένοι:** Οι νεότερες εκδόσεις του GroupDocs.Redaction συχνά περιλαμβάνουν βελτιστοποιήσεις απόδοσης και πρόσθετα hooks καταγραφής.

## Συμπέρασμα

Με την υλοποίηση ενός **προσαρμοσμένου καταγραφέα c#**, αποκτάτε λεπτομερή εικόνα σε κάθε βήμα της αλυσίδας διαγραφής, διευκολύνοντας την τήρηση προτύπων συμμόρφωσης και την αντιμετώπιση σφαλμάτων. Η προσέγγιση αυτή λειτουργεί αβίαστα με το GroupDocs.Redaction για .NET και μπορεί να επεκταθεί για ενσωμάτωση με οποιοδήποτε .NET πλαίσιο καταγραφής χρησιμοποιείτε ήδη.

---

## Συχνές ερωτήσεις

**Q: Ποιος είναι ο σκοπός της προσαρμοσμένης καταγραφής με το GroupDocs.Redaction;**  
A: Η προσαρμοσμένη καταγραφή καταγράφει λεπτομερή γεγονότα διαγραφής, ικανοποιεί τις απαιτήσεις ελέγχου και απλοποιεί την αντιμετώπιση προβλημάτων εκθέτοντας σφάλματα και προειδοποιήσεις σε πραγματικό χρόνο.

**Q: Πώς διαχειρίζομαι σφάλματα χρησιμοποιώντας έναν προσαρμοσμένο καταγραφέα;**  
A: Υλοποιήστε τη μέθοδο `LogError` στην κλάση `CustomLogger`; η σημαία `HasErrors` σας επιτρέπει να διακόψετε την επεξεργασία εάν εντοπιστεί κρίσιμο πρόβλημα.

**Q: Μπορεί η προσαρμοσμένη καταγραφή να ενσωματωθεί με άλλα συστήματα;**  
A: Ναι—μπορείτε να προωθήσετε τα μηνύματα καταγραφής σε CRM, ERP ή κεντρικά εργαλεία παρακολούθησης επεκτείνοντας τις μεθόδους του καταγραφέα.

**Q: Ποια είναι τα κοινά προβλήματα κατά την υλοποίηση προσαρμοσμένης καταγραφής;**  
A: Η έλλειψη παρακάμψεων μεθόδων, η παράλειψη του `RedactorSettings(logger)` και οι ανεπαρκείς άδειες αρχείων είναι τα πιο συχνά ζητήματα.

**Q: Πώς η προσαρμοσμένη καταγραφή βελτιώνει τις ροές εργασίας διαγραφής εγγράφων;**  
A: Οι λεπτομερείς καταγραφές παρέχουν ορατότητα σε πραγματικό χρόνο, απλοποιούν τον εντοπισμό σφαλμάτων και δημιουργούν τα αρχεία ελέγχου που απαιτούνται από κανονισμούς όπως GDPR και HIPAA.

## Πόροι

- **Τεκμηρίωση:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Αναφορά API:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Λήψη:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

**Τελευταία ενημέρωση:** 2026-10-01  
**Δοκιμή με:** GroupDocs.Redaction 23.11 for .NET  
**Συγγραφέας:** GroupDocs  

## Σχετικά Μαθήματα

- [Πώς να φορτώσετε έγγραφο με το GroupDocs.Redaction για .NET](/redaction/net/document-loading/)
- [Πώς να εξάγετε διαγραμμένα έγγραφα με το GroupDocs.Redaction .NET](/redaction/net/document-saving/)
- [Υλοποίηση διαγραφής εγγράφων χρησιμοποιώντας το GroupDocs.Redaction .NET&#58; Οδηγός βήμα‑βήμα](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)