---
date: '2026-06-11'
description: Μάθετε πώς να εξάγετε μεταδεδομένα από ροές εγγράφων χρησιμοποιώντας
  GroupDocs.Redaction για .NET, καλύπτοντας τη ρύθμιση, παραδείγματα κώδικα και πρακτικές
  εφαρμογές.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: Πώς να εξάγετε μεταδεδομένα από ροές εγγράφων χρησιμοποιώντας GroupDocs.Redaction
  .NET
type: docs
url: /el/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# Πώς να εξάγετε μεταδεδομένα από ροές εγγράφων χρησιμοποιώντας το GroupDocs.Redaction .NET

Κουραστήκατε από την χειροκίνητη εξαγωγή πληροφοριών εγγράφων ή την αντιμετώπιση μεγάλων αρχείων που επιβραδύνουν τη ροή εργασίας σας; Η γρήγορη **εξαγωγή μεταδεδομένων** είναι μια συχνή πρόκληση, και η βιβλιοθήκη GroupDocs.Redaction για .NET προσφέρει έναν γρήγορο, αποδοτικό σε μνήμη τρόπο για την ανάκτηση λεπτομερειών εγγράφου απευθείας από ροές. Σε αυτό το tutorial, θα μάθετε πώς να ρυθμίσετε τη βιβλιοθήκη, να αντλήσετε τον τύπο αρχείου, τον αριθμό σελίδων και το μέγεθος από μια ροή, και να προετοιμάσετε έναν φάκελο εξόδου για περαιτέρω επεξεργασία.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “εξαγωγή μεταδεδομένων”;** Σημαίνει ανάγνωση ιδιοτήτων όπως ο τύπος αρχείου, ο αριθμός σελίδων και το μέγεθος χωρίς το άνοιγμα ολόκληρου του εγγράφου στη μνήμη.  
- **Ποια βιβλιοθήκη το διαχειρίζεται;** Η GroupDocs.Redaction για .NET παρέχει ένα εγγενές API για εξαγωγή μεταδεδομένων βάσει ροής.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να επεξεργαστώ PDF μεγαλύτερα από 1 GB;** Ναι – οι ροές σας επιτρέπουν να διαχειριστείτε αρχεία έως 2 GB χωρίς να φορτώσετε ολόκληρο το αρχείο.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ και .NET 6+.

## Τι είναι η εξαγωγή μεταδεδομένων από ροές;
Η εξαγωγή μεταδεδομένων από ροές είναι η διαδικασία ανάγνωσης ιδιοτήτων εγγράφου απευθείας από ένα αντικείμενο `Stream`, αποφεύγοντας τη φόρτωση ολόκληρου του αρχείου και εξοικονομώντας έτσι μνήμη και χρόνο CPU. Αυτή η τεχνική είναι ιδανική για επεξεργασία παρτίδων ή υπηρεσίες βασισμένες στο cloud όπου οι πόροι είναι περιορισμένοι.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για εξαγωγή μεταδεδομένων;
Το GroupDocs.Redaction υποστηρίζει **πάνω από 30 μορφές αρχείων** (συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και τύπων εικόνων) και μπορεί να επεξεργαστεί έγγραφα έως **2 GB** σε μέγεθος διατηρώντας τη χρήση μνήμης κάτω από **50 MB**. Το API `Redactor` του παρέχει μία κλήση για την ανάκτηση όλων των βασικών πληροφοριών εγγράφου, εξαλείφοντας την ανάγκη για πολλαπλούς αναλυτές.

## Προαπαιτούμενα
- **GroupDocs.Redaction for .NET** (τελευταία έκδοση)  
- **.NET Framework** 4.5+ **ή** **.NET Core/5+/6+**  
- Βασικές γνώσεις C# και εξοικείωση με file I/O  
- Visual Studio 2019 ή νεότερο

## Πώς να ρυθμίσετε το GroupDocs.Redaction για .NET;
Για να αρχίσετε να χρησιμοποιείτε το GroupDocs.Redaction, πρέπει πρώτα να προσθέσετε τη βιβλιοθήκη στο έργο σας. Αυτό μπορεί να γίνει μέσω του .NET CLI, του Visual Studio Package Manager ή του UI του NuGet. Επιλέξτε την προσέγγιση που ταιριάζει στη ροή εργασίας σας· το CLI είναι ιδανικό για αυτοματοποιημένες κατασκευές, ενώ το UI προσφέρει γραφικό τρόπο περιήγησης στις εκδόσεις και τις εξαρτήσεις.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Ανοίξτε το NuGet Package Manager στο Visual Studio.  
- Αναζητήστε το **"GroupDocs.Redaction"** και εγκαταστήστε την τελευταία έκδοση.

### Βήματα Απόκτησης Άδειας
1. **Free Trial:** Κατεβάστε μια δοκιμαστική άδεια για να εξερευνήσετε όλες τις λειτουργίες χωρίς περιορισμούς.  
2. **Temporary License:** Ζητήστε μια προσωρινή άδεια από [GroupDocs](https://purchase.groupdocs.com/temporary-license/) για εκτεταμένη δοκιμή.  
3. **Purchase:** Όταν είστε έτοιμοι για παραγωγή, αγοράστε εμπορική άδεια.

Για περισσότερες πληροφορίες, επισκεφθείτε την [ιστοσελίδα του GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Βασική Αρχικοποίηση και Ρύθμιση
Η κλάση `Redactor` είναι το σημείο εισόδου για όλες τις λειτουργίες, συμπεριλαμβανομένης της εξαγωγής μεταδεδομένων.

`Redactor` είναι η βασική κλάση που αντιπροσωπεύει μια παρουσία εγγράφου και παρέχει μεθόδους για διαγραφή, ανάκτηση πληροφοριών και διαχείριση αρχείων. Μόλις εγκατασταθεί, μπορείτε να δημιουργήσετε ένα αντικείμενο `Redactor` όπως φαίνεται παρακάτω:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας εμβαθύνουμε στις λεπτομέρειες υλοποίησης.

## Πώς να εξάγετε μεταδεδομένα από ροή εγγράφου;
Φορτώστε το έγγραφο ως **ροή μόνο για ανάγνωση**, αρχικοποιήστε το `Redactor` και καλέστε το `GetDocumentInfo()` για να ανακτήσετε τα μεταδεδομένα σε ένα μόνο βήμα. Αυτή η προσέγγιση αποφεύγει τη φόρτωση ολόκληρου του αρχείου στη μνήμη, κάτι που είναι κρίσιμο για μεγάλα PDF ή έγγραφα Office με εκατοντάδες σελίδες.

**Άμεση απάντηση:** Ανοίξτε το αρχείο με `File.OpenRead()`, περάστε τη ροή στο `new Redactor(stream)`, έπειτα καλέστε `redactor.GetDocumentInfo()` – η μέθοδος επιστρέφει ένα αντικείμενο που περιέχει τον τύπο αρχείου, τον αριθμό σελίδων και το μέγεθος σε μόλις τρεις γραμμές κώδικα.

### Βήμα 1: Προετοιμάστε τη διαδρομή του αρχικού αρχείου
Πρώτα, βεβαιωθείτε ότι το αρχικό αρχείο υπάρχει και ότι ο φάκελος εξόδου είναι έτοιμος. Η παρακάτω βοηθητική μέθοδος ελέγχει τον φάκελο εξόδου και τον δημιουργεί εάν χρειάζεται.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Γιατί;* Αυτό εγγυάται μια έγκυρη διαδρομή για τις επόμενες λειτουργίες αρχείων και αποτρέπει το `DirectoryNotFoundException`.

### Βήμα 2: Ανοίξτε τη ροή του εγγράφου
Η χρήση του `File.OpenRead()` ανοίγει το αρχείο ως **ροή μόνο για ανάγνωση**, η οποία διατηρεί τη χρήση μνήμης χαμηλή ακόμη και για αρχεία μεγέθους gigabyte.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Γιατί;* Οι ροές επιτρέπουν επεξεργασία εν κινήσει, επιτρέποντάς σας να δουλεύετε με τμήματα του αρχείου αντί για ολόκληρο το έγγραφο.

### Βήμα 3: Αρχικοποιήστε το Redactor με τη ροή του εγγράφου
`Redactor` είναι το κύριο αντικείμενο API που σας δίνει πρόσβαση σε λειτουργίες επιπέδου εγγράφου, συμπεριλαμβανομένης της εξαγωγής μεταδεδομένων.

`Redactor` αντιπροσωπεύει ένα μόνο έγγραφο που φορτώνεται από μια ροή και εκθέτει μεθόδους όπως `GetDocumentInfo()` για γρήγορη ανάκτηση ιδιοτήτων.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Γιατί;* Η δημιουργία ενός `Redactor` με ροή συνδέει το αντικείμενο με το υποκείμενο αρχείο χωρίς πλήρη φόρτωση.

### Βήμα 4: Ανακτήστε τα μεταδεδομένα του εγγράφου
Καλώντας το `GetDocumentInfo()` επιστρέφει ένα αντικείμενο `DocumentInfo` που περιέχει τη μορφή αρχείου, τον αριθμό σελίδων και το μέγεθος του αρχείου.

`GetDocumentInfo()` εξάγει τις βασικές ιδιότητες (μορφή, αριθμό σελίδων, μέγεθος) σε μία κλήση, εξαλείφοντας την ανάγκη για ξεχωριστούς αναλυτές.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Γιατί;* Αυτό το βήμα ενοποιεί όλα τα απαραίτητα μεταδεδομένα, καθιστώντας εύκολο το logging, το φιλτράρισμα ή η δρομολόγηση εγγράφων βάσει των χαρακτηριστικών τους.

## Πώς να προετοιμάσετε έναν φάκελο εξόδου για επεξεργασμένα αρχεία;
Πριν γράψετε οποιαδήποτε επεξεργασμένα αρχεία, βεβαιωθείτε ότι ο φάκελος προορισμού υπάρχει και είναι εγγράψιμος. Ελέγχοντας προγραμματιστικά τη διαδρομή και δημιουργώντας την όταν λείπει, αποφεύγετε κοινές εξαιρέσεις χρόνου εκτέλεσης όπως `DirectoryNotFoundException` ή σφάλματα δικαιωμάτων. Αυτό το απλό βήμα κάνει επίσης τον κώδικά σας φορητό μεταξύ περιβαλλόντων, είτε εκτελείται τοπικά, σε διακομιστή ή μέσα σε κοντέινερ.

**Άμεση απάντηση:** Χρησιμοποιήστε το `Directory.Exists()` για να ελέγξετε αν υπάρχει ο φάκελος και το `Directory.CreateDirectory()` για να τον δημιουργήσετε εάν δεν υπάρχει – αυτός ο έλεγχος μίας γραμμής εγγυάται μια έγκυρη διαδρομή πριν από οποιαδήποτε λειτουργία εγγραφής.

### Υλοποιήστε μια βοηθητική μέθοδο
Η παρακάτω μέθοδος ενσωματώνει τη λογική ελέγχου‑και‑δημιουργίας, επιστρέφοντας τη επαληθευμένη διαδρομή για μελλοντική χρήση.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Γιατί;* Η κεντρική τοποθέτηση αυτής της λογικής μειώνει την επανάληψη και καθιστά τη βάση κώδικα πιο εύκολη στη συντήρηση.

## Συνηθισμένα Προβλήματα και Λύσεις
- **Σφάλματα δικαιωμάτων:** Βεβαιωθείτε ότι η εφαρμογή εκτελείται υπό λογαριασμό με δικαιώματα εγγραφής στον προορισμό.  
- **Μη έγκυρες διαδρομές:** Ελέγξτε ξανά τους διαχωριστές διαδρομών (`\\` στα Windows, `/` στα Linux/macOS) για να αποφύγετε το `DirectoryNotFoundException`.  
- **Διαχείριση μεγάλων αρχείων:** Αποδεσμεύστε τις ροές άμεσα (`using` δηλώσεις) για να ελευθερώσετε τους χειριστές του OS και να αποτρέψετε διαρροές.

## Πρακτικές Εφαρμογές
1. **Αυτοματοποιημένη Εισαγωγή Εγγράφων:** Εξάγετε μεταδεδομένα κατά τη μεταφόρτωση, στη συνέχεια αποθηκεύστε τα σε βάση δεδομένων για γρήγορη αναζήτηση και αναφορές συμμόρφωσης.  
2. **Νομικοί & Συμμορφωτικοί Έλεγχοι:** Αντλήστε τον αριθμό σελίδων και τους τύπους αρχείων για να επαληθεύσετε ότι τα έγγραφα πληρούν τα κανονιστικά πρότυπα πριν την αρχειοθέτηση.  
3. **Διαχείριση Περιεχομένου Επιχειρήσεων:** Χρησιμοποιήστε τα μεταδεδομένα για αυτόματη κατηγοριοποίηση αρχείων σε φακέλους, βελτιώνοντας την οργάνωση και την ταχύτητα ανάκτησης.

## Σκέψεις Απόδοσης
- **Διαχείριση Μνήμης:** Πάντα τυλίξτε τις ροές σε μπλοκ `using` ώστε να αποδεσμεύονται αυτόματα.  
- **Επεξεργασία Παρτίδων:** Επεξεργαστείτε έγγραφα σε ομάδες των 10‑20 για να ισορροπήσετε τη ροή εργασίας και τη χρήση μνήμης, ειδικά σε διακομιστές με περιορισμένους πόρους.  
- **Παράλληλη Επεξεργασία:** Εκμεταλλευτείτε το `Parallel.ForEach` για ανεξάρτητα αρχεία, αλλά παρακολουθήστε το CPU και το I/O για να αποφύγετε συγκρούσεις.

## Συμπέρασμα
Τώρα έχετε έναν πλήρη, έτοιμο για παραγωγή οδηγό σχετικά με το **πώς να εξάγετε μεταδεδομένα** από ροές εγγράφων χρησιμοποιώντας το GroupDocs.Redaction για .NET. Ακολουθώντας τα παραπάνω βήματα, μπορείτε να ανακτήσετε αποδοτικά τον τύπο αρχείου, τον αριθμό σελίδων και το μέγεθος, διατηρώντας τη χρήση μνήμης χαμηλή και διαχειριζόμενοι μεγάλα αρχεία με ευκολία.

**Επόμενα Βήματα**
- Εξετάστε την πλήρη αναφορά API στην [τεκμηρίωση](https://docs.groupdocs.com/redaction/net/).  
- Βυθιστείτε περισσότερο στην [Τεκμηρίωση GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) για να εξερευνήσετε τις λειτουργίες διαγραφής, υδατογράφησης και OCR.  
- Πειραματιστείτε με διαφορετικούς τύπους αρχείων (PDF, DOCX, XLSX) για να δείτε πώς τα μεταδεδομένα διαφέρουν ανά τύπο.  
- Ενσωματώστε τα εξαγόμενα μεταδεδομένα στην υπάρχουσα λύση διαχείρισης ή αναζήτησης εγγράφων.

## Συχνές Ερωτήσεις

**Ε: Ποια είναι η κύρια περίπτωση χρήσης της εξαγωγής μεταδεδομένων του GroupDocs.Redaction;**  
Α: Επιτρέπει γρήγορη, αποδοτική σε μνήμη ανάκτηση ιδιοτήτων εγγράφου για ευρετηρίαση, ελέγχους συμμόρφωσης και αυτοματοποιημένη δρομολόγηση χωρίς το άνοιγμα ολόκληρου του αρχείου.

**Ε: Μπορώ να εξάγω μεταδεδομένα από αρχεία προστατευμένα με κωδικό;**  
Α: Ναι, παρέχετε τον κωδικό όταν δημιουργείτε το αντικείμενο `Redactor`; το API θα αποκρυπτογραφήσει τη ροή εσωτερικά.

**Ε: Η βιβλιοθήκη υποστηρίζει μη‑PDF μορφές όπως DOCX ή XLSX;**  
Α: Απόλυτα – το GroupDocs.Redaction διαχειρίζεται πάνω από 30 μορφές, συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX και κοινών τύπων εικόνων.

**Ε: Πόσο μεγάλο έγγραφο μπορώ να επεξεργαστώ με ροές;**  
Α: Οι ροές επιτρέπουν την επεξεργασία αρχείων έως **2 GB** διατηρώντας τη χρήση μνήμης κάτω από **50 MB**, χάρη στην ανάγνωση εν κινήσει.

**Ε: Πού μπορώ να λάβω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Επισκεφθείτε το [φόρουμ GroupDocs](https://forum.groupdocs.com/c/redaction/33) για υποστήριξη της κοινότητας ή συμβουλευτείτε την επίσημη τεκμηρίωση για συμβουλές αντιμετώπισης προβλημάτων.

---

**Τελευταία Ενημέρωση:** 2026-06-11  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 23.12 for .NET  
**Συγγραφέας:** GroupDocs  

**Πόροι**  
- **Τεκμηρίωση:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **Αναφορά API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Λήψη:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Σχετικά Μαθήματα
- [Ανάκτηση Μεταδεδομένων Εγγράφου με το GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [Πώς να Διαγράψετε Μεταδεδομένα Εγγράφου Χρησιμοποιώντας το GroupDocs.Redaction για .NET - Ένας Πλήρης Οδηγός](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Ασφαλής Διαγραφή Εγγράφου σε .NET Χρησιμοποιώντας Ροές: Οδηγός για το GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)