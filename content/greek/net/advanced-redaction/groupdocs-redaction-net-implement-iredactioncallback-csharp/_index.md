---
date: '2026-10-06'
description: Μάθετε πώς να αποκρύψετε δεδομένα χρησιμοποιώντας το GroupDocs.Redaction
  .NET με μια υλοποίηση IRedactionCallback σε C#. Ακολουθήστε αυτόν τον οδηγό step‑by‑step,
  τις βέλτιστες πρακτικές και παραδείγματα πραγματικού κόσμου.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Μάθετε πώς να αποκρύψετε δεδομένα χρησιμοποιώντας το GroupDocs.Redaction
  .NET με μια υλοποίηση IRedactionCallback σε C#. Ακολουθήστε έναν οδηγό step‑by‑step
  με βέλτιστες πρακτικές και παραδείγματα πραγματικού κόσμου.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Πώς να αποκρύψετε δεδομένα με το GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Πώς να αποκρύψετε δεδομένα με το GroupDocs.Redaction .NET (C#)
type: docs
url: /el/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Πώς να αφαιρέσετε δεδομένα με το GroupDocs.Redaction .NET (C#)

Σε αυτό το ολοκληρωμένο tutorial θα ανακαλύψετε **πώς να αφαιρέσετε δεδομένα** από PDF, αρχεία Word και άλλα έγγραφα χρησιμοποιώντας το GroupDocs.Redaction για .NET. Είτε χρειάζεται να κρύψετε προσωπικά αναγνωριστικά σε νομικά συμβόλαια είτε να διαγράψετε εμπιστευτικές αριθμητικές πληροφορίες από οικονομικές εκθέσεις, το SDK σας δίνει προγραμματιστικό έλεγχο ώστε κάθε ευαίσθητο στοιχείο να εξαφανίζεται μόνιμα και με δυνατότητα ελέγχου. Θα περάσουμε από την εγκατάσταση της βιβλιοθήκης, τη διαμόρφωση ενός προσαρμοσμένου `IRedactionCallback` και την εφαρμογή αφαίρεσης ακριβών φράσεων με πλήρη καταγραφή.

## Γρήγορες απαντήσεις
- **Τι κάνει το IRedactionCallback;** Σας επιτρέπει να παρεμβείτε σε κάθε γεγονός αφαίρεσης, να καταγράψετε λεπτομέρειες και προαιρετικά να τροποποιήσετε το κείμενο αντικατάστασης σε πραγματικό χρόνο.  
- **Χρειάζομαι άδεια;** Μια δοκιμαστική έκδοση λειτουργεί για ανάπτυξη· μια μόνιμη άδεια αφαιρεί όλους τους περιορισμούς αξιολόγησης.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Core 3.1+, .NET 5/6 και .NET Framework 4.6+.  
- **Μπορώ να επεξεργαστώ πολλαπλά αρχεία;** Ναι—τυλίξτε τη λογική σε βρόχο ή χρησιμοποιήστε επεξεργασία παρτίδας για βέλτιστη απόδοση.  
- **Είναι δυνατή η ασύγχρονη αφαίρεση;** Δεν είναι ενσωματωμένη, αλλά μπορείτε να εκτελέσετε τις κλήσεις API μέσα σε `Task.Run` ή άλλα ασύγχρονα μοτίβα.

## Τι είναι η αφαίρεση ευαίσθητων δεδομένων;
`Redaction` είναι η μόνιμη αφαίρεση ή απόκρυψη πληροφοριών που δεν πρέπει να αποκαλυφθούν. Με το GroupDocs.Redaction ορίζετε ακριβείς φράσεις, μοτίβα κανονικών εκφράσεων ή προσαρμοσμένους κανόνες και τις αντικαθιστάτε με σύμβολα όπως **[REDACTED]** διατηρώντας την αρχική διάταξη και σελιδοποίηση.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction με IRedactionCallback;
`IRedactionCallback` είναι μια διεπαφή που σας ειδοποιεί κάθε φορά που το SDK αφαιρεί ένα κομμάτι περιεχομένου, επιτρέποντάς σας να καταγράψετε δεδομένα ελέγχου ή να προσαρμόσετε την αντικατάσταση δυναμικά. Αυτό παρέχει πλήρη δυνατότητα ελέγχου, εφαρμογή προσαρμοσμένων επιχειρηματικών κανόνων και απρόσκοπτη ενσωμάτωση με συστήματα συμμόρφωσης—χωρίς να θυσιάζεται η απόδοση.

## Προαπαιτούμενα
- **GroupDocs.Redaction** βιβλιοθήκη (συμβατή έκδοση – δείτε την επίσημη [σελίδα τεκμηρίωσης](https://docs.groupdocs.com/redaction/net/)). Για πλήρεις λεπτομέρειες ανατρέξτε στην [επίσημη τεκμηρίωση](https://docs.groupdocs.com/redaction/net/).  
- .NET Core ή .NET Framework εγκατεστημένο στον υπολογιστή ανάπτυξής σας.  
- Visual Studio (η έκδοση Community είναι εντάξει) ή οποιοδήποτε IDE που υποστηρίζει C#.  
- Βασικές γνώσεις C# και εξοικείωση με τη διαχείριση πακέτων NuGet.

## Ρύθμιση του GroupDocs.Redaction για .NET
Πρώτα, προσθέστε τη βιβλιοθήκη στο έργο σας. Επιλέξτε τη μέθοδο που προτιμάτε – τη CLI, το Package Manager Console ή το UI. Οι εντολές παραμένουν ακριβώς όπως στο αρχικό tutorial.

### Επιλογές εγκατάστασης
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Ανοίξτε το έργο σας στο Visual Studio.  
- Μεταβείτε στη **Διαχείριση πακέτων NuGet**.  
- Αναζητήστε το **GroupDocs.Redaction** και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.

### Απόκτηση άδειας
Για να δοκιμάσετε το προϊόν, ζητήστε μια δωρεάν δοκιμή ή μια προσωρινή άδεια από [εδώ](https://purchase.groupdocs.com/temporary-license/). Μπορείτε επίσης να αποκτήσετε προσωρινή άδεια από τη [σελίδα προσωρινής άδειας](https://purchase.groupdocs.com/temporary-license/). Για παραγωγική χρήση, αγοράστε πλήρη άδεια ώστε να ξεκλειδώσετε όλα τα χαρακτηριστικά χωρίς περιορισμούς.

#### Βασική αρχικοποίηση και ρύθμιση
Παρακάτω είναι ο ελάχιστος κώδικας που χρειάζεστε για να ανοίξετε ένα έγγραφο με την κλάση `Redactor`. Διατηρήστε αυτό το απόσπασμα αμετάβλητο – είναι η βάση για όλα τα επόμενα.  
`Redactor` είναι η κύρια κλάση που αντιπροσωπεύει ένα έγγραφο και παρέχει μεθόδους για την εφαρμογή κανόνων αφαίρεσης.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Οδηγός υλοποίησης
Τώρα θα επεκτείνουμε τη βασική ρύθμιση προσθέτοντας ένα προσαρμοσμένο `IRedactionCallback`. Αυτό σας επιτρέπει να καταγράψετε κάθε γεγονός αφαίρεσης, να το γράψετε σε αρχείο καταγραφής ή ακόμη και να τροποποιήσετε το κείμενο αντικατάστασης σε πραγματικό χρόνο.

### Προσάρτηση και χρήση υλοποίησης IRedactionCallback
`IRedactionCallback` είναι μια διεπαφή που λαμβάνει callbacks για κάθε λειτουργία αφαίρεσης, επιτρέποντάς σας να καταγράψετε ή να τροποποιήσετε τη συμπεριφορά προγραμματιστικά.

#### Βήμα 1: προετοιμασία καταλόγου εξόδου και διαδρομής αρχείου πηγής
Ορίστε πού βρίσκεται το πηγαίο έγγραφό σας. Προσαρμόστε τη διαδρομή ώστε να ταιριάζει με το περιβάλλον σας.

`LoadOptions` είναι ένα αντικείμενο διαμόρφωσης που λέει στο SDK πώς να διαβάσει το αρχείο (π.χ., διαχείριση κωδικού).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Βήμα 2: δημιουργία αντικειμένου Redactor με προσαρμοσμένες ρυθμίσεις
Δημιουργούμε ένα `Redactor` με `LoadOptions` και `RedactorSettings`. Το `RedactionDump` μέσα στις ρυθμίσεις θα καταγράφει αυτόματα κάθε αφαίρεση που πραγματοποιείται.

`RedactorSettings` σας επιτρέπει να ρυθμίσετε λεπτομερώς τη διαδικασία αφαίρεσης· η παροχή ενός `RedactionDump` ενεργοποιεί ένα λεπτομερές αρχείο ελέγχου.  
`RedactionDump` είναι μια βοηθητική κλάση που γράφει κάθε γεγονός αφαίρεσης σε αρχείο dump μορφής JSON για αναφορές συμμόρφωσης.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Βήμα 3: εφαρμογή ακριβούς φράσης αφαίρεσης
Εδώ αντικαθιστούμε τη φράση **John Doe** με το σύμβολο **[REDACTED]**. Μπορείτε να ανταλλάξετε οποιαδήποτε φράση ή μοτίβο χρειάζεται να κρύψετε.

`ReplacementOptions` ορίζει ποιο κείμενο θα αντικαταστήσει το ταιριασμένο περιεχόμενο. Υποστηρίζει επίσης προσαρμογή γραμματοσειράς και χρώματος εάν χρειάζεστε οπτική μάσκα.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Επεξήγηση των βασικών αντικειμένων**
- `LoadOptions()` – λέει στο SDK πώς να διαβάσει το έγγραφο (π.χ., διαχείριση κωδικού).  
- `RedactorSettings(new RedactionDump())` – ενεργοποιεί ένα αρχείο dump που καταγράφει κάθε αφαίρεση για σκοπούς ελέγχου.  
- `ReplacementOptions("[REDACTED]")` – ορίζει το κείμενο που θα αντικαταστήσει τη ταιριαστή φράση.

### Γιατί είναι σημαντικό
Ο μηχανισμός callbacks καταγράφει κάθε γεγονός αφαίρεσης, δημιουργεί ένα μηχανικά αναγνώσιμο ίχνος ελέγχου και σας επιτρέπει να τροποποιείτε δυναμικά τα σύμβολα, βοηθώντας στην τήρηση των απαιτήσεων συμμόρφωσης και μειώνοντας το χειροκίνητο έργο μετά την επεξεργασία. Ενσωματώνοντας αυτά τα δεδομένα στα συστήματα παρακολούθησής σας, μπορείτε να δημιουργείτε αναφορές, να ενεργοποιείτε ειδοποιήσεις και να διασφαλίζετε ότι καμία ευαίσθητη πληροφορία δεν διαφεύγει από τη διαδικασία αφαίρεσης.

Η χρήση του `IRedactionCallback` προσφέρει τρία συγκεκριμένα πλεονεκτήματα:  
1. **Καταγραφές έτοιμες για συμμόρφωση** – κάθε αφαίρεση καταγράφεται σε μηχανικά αναγνώσιμο dump, ικανοποιώντας απαιτήσεις ελέγχου για πάνω από 30 ρυθμιστικά πλαίσια.  
2. **Δυναμική αντικατάσταση** – μπορείτε να αλλάξετε το σύμβολο ανάλογα με τον τύπο δεδομένων, μειώνοντας το χειροκίνητο έργο κατά έως 40 %.  
3. **Κλιμακώσιμη απόδοση** – το callback προσθέτει αμελητέο κόστος (<2 ms ανά αφαίρεση) ενώ σας επιτρέπει να επεξεργάζεστε χιλιάδες αρχεία παράλληλα.

### Συμβουλές αντιμετώπισης προβλημάτων
- **File not found:** Ελέγξτε ξανά τη διαδρομή `sourceFile` και βεβαιωθείτε ότι το αρχείο είναι προσβάσιμο στη διαδικασία εκτέλεσης.  
- **Callback not firing:** Βεβαιωθείτε ότι η κλάση σας υλοποιεί **όλα** τα μέλη του `IRedactionCallback` και ότι το αντικείμενο περνιέται σωστά στο `Redactor`.  
- **Performance lag:** Για μεγάλες παρτίδες, επαναχρησιμοποιήστε το ίδιο αντικείμενο `Redactor` όταν είναι δυνατόν και απελευθερώστε το άμεσα.

## Πρακτικές εφαρμογές
Η αφαίρεση ευαίσθητων δεδομένων είναι χρήσιμη σε πολλούς κλάδους:

1. **Επεξεργασία νομικών εγγράφων** – Αυτόματη αφαίρεση ονομάτων πελατών, αριθμών υποθέσεων ή αριθμών κοινωνικής ασφάλισης πριν την κοινοποίηση προσχεδίων.  
2. **Συστήματα διαχείρισης ανθρώπινου δυναμικού** – Αφαίρεση προσωπικών αναγνωριστικών από συμβάσεις υπαλλήλων κατά τη διάρκεια ελέγχων.  
3. **Οικονομική αναφορά** – Απόκρυψη ιδιόκτητων αριθμών ή λογαριασμών όταν δημιουργούνται PDF για επενδυτές.

## Σκέψεις για την απόδοση
Το GroupDocs.Redaction υποστηρίζει **30+ μορφές εισόδου και εξόδου** (PDF, DOCX, PPTX, XLSX, HTML και τύπους εικόνων) και μπορεί να επεξεργαστεί αρχεία εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη. Για να διατηρήσετε την εφαρμογή σας γρήγορη όταν διαχειρίζεστε δεκάδες ή εκατοντάδες αρχεία:

- **Batch processing:** Φορτώστε μια λίστα αρχείων και εκτελέστε τον βρόχο αφαίρεσης μέσα σε `Parallel.ForEach` για αξιοποίηση πολλαπλών πυρήνων.  
- **Memory management:** Τυλίξτε κάθε `Redactor` σε μπλοκ `using` (όπως φαίνεται) για να εγγυηθείτε την απελευθέρωση.  
- **Asynchronous operations:** Παρόλο που το SDK είναι συγχρονισμένο, μπορείτε να μεταφέρετε το έργο σε παρασκήνια νήματα ή `Task.Run` για να αποφύγετε το μπλοκάρισμα των UI νήματος.

## Συχνά προβλήματα και λύσεις
| Πρόβλημα | Λύση |
|----------|------|
| **Σφάλμα “Invalid file format”** | Βεβαιωθείτε ότι ο τύπος εγγράφου υποστηρίζεται (PDF, DOCX, PPTX κ.λπ.). |
| **Callback receives null values** | Ελέγξτε ότι περνάτε μια συγκεκριμένη υλοποίηση του `IRedactionCallback` κατά τη δημιουργία του `RedactorSettings`. |
| **Redaction not applied** | Επαληθεύστε ότι η ακριβής φράση ταιριάζει με το κεφαλαίο/μικρό και το διάστημα του εγγράφου, ή χρησιμοποιήστε `RegexRedaction` για αντιστοίχιση με μοτίβο. |

## Συχνές ερωτήσεις

**Q: Ποιες είναι οι επιλογές αδειοδότησης για το GroupDocs.Redaction;**  
A: Μπορείτε να ξεκινήσετε με δωρεάν δοκιμή ή να ζητήσετε προσωρινή άδεια για να εξερευνήσετε όλες τις λειτουργίες. Για παραγωγική χρήση, αγοράστε μόνιμη ή συνδρομητική άδεια.

**Q: Μπορώ να χρησιμοποιήσω το GroupDocs.Redaction σε πολλαπλούς τύπους αρχείων;**  
A: Ναι, υποστηρίζει PDF, Word, Excel, PowerPoint και πολλές άλλες κοινές μορφές.

**Q: Πώς να διαχειριστώ εξαιρέσεις κατά τη διάρκεια της αφαίρεσης;**  
A: Τυλίξτε τη λογική αφαίρεσης σε μπλοκ `try‑catch` και καταγράψτε τις λεπτομέρειες της εξαίρεσης. Το callback μπορεί επίσης να χρησιμοποιηθεί για άμεση καταγραφή σφαλμάτων.

**Q: Υπάρχει ενσωματωμένη υποστήριξη για ασύγχρονη επεξεργασία;**  
A: Το κύριο API είναι συγχρονισμένο, αλλά μπορείτε να εκτελείτε κλήσεις αφαίρεσης μέσα σε ασύγχρονα tasks ή υπηρεσίες παρασκηνίου.

**Q: Πού μπορώ να βρω πιο προχωρημένα παραδείγματα;**  
A: Η [επίσημη τεκμηρίωση](https://docs.groupdocs.com/redaction/net/) και η αναφορά API παρέχουν εκτενείς δείγματα κώδικα και οδηγούς σεναρίων.

## Πόροι

- [Τεκμηρίωση GroupDocs.Redaction για .NET](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API GroupDocs.Redaction για .NET](https://reference.groupdocs.com/redaction/net/)
- [Λήψη GroupDocs.Redaction για .NET](https://releases.groupdocs.com/redaction/net/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-10-06  
**Δοκιμάστηκε με:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**Συγγραφέας:** GroupDocs

## Σχετικά Μαθήματα

- [Δημιουργία πολιτικής αφαίρεσης με GroupDocs.Redaction .NET – Οδηγός βήμα‑βήμα](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Πώς να αφαιρέσετε έγγραφα με GroupDocs.Redaction .NET – Πλήρης οδηγός](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Αφαίρεση εγγράφων .net χρησιμοποιώντας Streams – Οδηγός GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)