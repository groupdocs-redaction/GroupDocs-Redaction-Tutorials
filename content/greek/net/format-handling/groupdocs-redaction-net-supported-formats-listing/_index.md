---
date: '2026-07-20'
description: Μάθετε πώς να list formats χρησιμοποιώντας GroupDocs.Redaction .NET,
  ενσωματώστε τη δυνατότητα στο document workflow σας και βελτιώστε την performance.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Ανακαλύψτε πώς να list formats χρησιμοποιώντας GroupDocs.Redaction
  .NET, δείτε ένα step‑by‑step guide και λάβετε συμβουλές για optimal performance
  στις .NET εφαρμογές σας.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Πώς να list formats με GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Πώς να list formats με GroupDocs.Redaction .NET
type: docs
url: /el/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Πώς να καταγράψετε μορφές με το GroupDocs.Redaction .NET

Η διαχείριση μιας ευρείας ποικιλίας τύπων εγγράφων είναι καθημερινή πραγματικότητα για τους προγραμματιστές που δημιουργούν εφαρμογές με κέντρο το έγγραφο. Σε αυτό το tutorial θα μάθετε **πώς να καταγράψετε μορφές** που μπορεί να χειριστεί το GroupDocs.Redaction .NET, ώστε να μπορείτε να επικυρώνετε τα αρχεία πριν την επεξεργασία, να παρουσιάζετε στους χρήστες ακριβείς επιλογές και να διατηρείτε την ροή εργασίας σας αποδοτική.

## Εισαγωγή

Η αποδοτική διαχείριση εγγράφων ξεκινά με το να γνωρίζετε ακριβώς ποιους τύπους αρχείων υποστηρίζει η βιβλιοθήκη σας. Το GroupDocs.Redaction παρέχει μια ενσωματωμένη μέθοδο για την ανάκτηση αυτής της πληροφορίας, επιτρέποντάς σας να δημιουργείτε δυναμικά στοιχεία UI, να επιβάλλετε κανόνες επικύρωσης και να αποφεύγετε σφάλματα χρόνου εκτέλεσης. Παρακάτω θα βρείτε όλα όσα χρειάζεστε για να ξεκινήσετε, από την εγκατάσταση μέχρι πρακτικά αποσπάσματα κώδικα και συμβουλές απόδοσης.

### Γρήγορες Απαντήσεις
- **Τι σημαίνει “πώς να καταγράψετε μορφές”;** Αναφέρεται στην ανάκτηση της συλλογής των επεκτάσεων αρχείων που μπορεί να επεξεργαστεί το GroupDocs.Redaction.  
- **Χρειάζομαι άδεια;** Ναι, απαιτείται έγκυρη άδεια GroupDocs.Redaction για χρήση σε παραγωγή.  
- **Ποιες εκδόσεις .NET υποστηρίζονται;** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Πόσες μορφές είναι διαθέσιμες;** Υπέρ των 30 μορφών εισόδου και εξόδου υποστηρίζονται έτοιμες για χρήση.  
- **Απαιτείται κάποια ειδική διαμόρφωση;** Δεν απαιτείται επιπλέον διαμόρφωση πέρα από την τυπική αρχικοποίηση της βιβλιοθήκης.

## Τι είναι το “πώς να καταγράψετε μορφές”;
Αφορά την κλήση του API FileType της βιβλιοθήκης για την απόκτηση μιας συλλογής όπου κάθε στοιχείο περιέχει την επέκταση αρχείου και ένα ανθρώπινα αναγνώσιμο όνομα. Οι προγραμματιστές μπορούν στη συνέχεια να διατρέξουν αυτή τη συλλογή για να δημιουργήσουν κανόνες επικύρωσης, να γεμίσουν λίστες επιλογών UI ή να καταγράψουν τους υποστηριζόμενους τύπους, διασφαλίζοντας ότι μόνο συμβατά έγγραφα θα υποβληθούν σε επεξεργασία.

## Γιατί να καταγράψετε μορφές με το GroupDocs.Redaction;
Το GroupDocs.Redaction υποστηρίζει **30+** διαφορετικούς τύπους αρχείων — συμπεριλαμβανομένων PDF, DOCX, PPTX και μορφών εικόνας — επιτρέποντάς σας να διαχειριστείτε τα περισσότερα επιχειρησιακά έγγραφα χωρίς τρίτους μετατροπείς. Με τον προγραμματιστικό κατάλογο αυτών των μορφών εξαλείφετε τις εικασίες, μειώνετε τα αιτήματα υποστήριξης και διασφαλίζετε ότι μόνο συμβατά αρχεία εισέρχονται στη διαδικασία επεξεργασίας.

## Προαπαιτούμενα

- **GroupDocs.Redaction for .NET** – κατεβάστε το τελευταίο πακέτο από την επίσημη ιστοσελίδα.  
- **.NET Framework ή .NET Core** – συμβατό με το περιβάλλον ανάπτυξής σας.  
- **Visual Studio** (ή οποιοδήποτε IDE συμβατό με C#).  
- Βασική εξοικείωση με τη σύνταξη C#.

## Ρύθμιση του GroupDocs.Redaction για .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### UI Διαχειριστή Πακέτων NuGet
- Αναζητήστε **“GroupDocs.Redaction”** και εγκαταστήστε την τελευταία έκδοση.

### Απόκτηση Άδειας
Η GroupDocs προσφέρει δωρεάν δοκιμή, προσωρινή άδεια για αξιολόγηση ή πλήρεις επιλογές αγοράς. Επισκεφθείτε την ιστοσελίδα της GroupDocs για να αποκτήσετε το κατάλληλο αρχείο άδειας.

### Βασική Αρχικοποίηση και Ρύθμιση
Μετά την προσθήκη του πακέτου, αναφέρετε το namespace και δημιουργήστε μια παρουσία `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Οδηγός Υλοποίησης

### Πώς μπορώ να καταγράψω μορφές με το GroupDocs.Redaction .NET;
Φορτώστε τη βιβλιοθήκη, καλέστε τον στατικό βοηθό και ταξινομήστε τα αποτελέσματα — αυτό σας δίνει μια έτοιμη προς χρήση συλλογή σε μόλις δύο γραμμές κώδικα. Χρησιμοποιήστε `FileType.GetSupportedFileFormats()` για να λάβετε ένα `IEnumerable<FileType>` που περιλαμβάνει την επέκταση και το όνομα εμφάνισης κάθε μορφής, στη συνέχεια ταξινομήστε κατά επέκταση για μια καθαρή λίστα UI.

### Ανάκτηση Υποστηριζόμενων Μορφών Αρχείων

#### Επισκόπηση
Ο στόχος είναι η λήψη λίστας τύπων αρχείων που μπορεί να χειριστεί το GroupDocs.Redaction, διευκολύνοντας την ενσωμάτωση σε λογική επικύρωσης, λίστες επιλογών UI ή μηχανισμούς καταγραφής.

#### Υλοποίηση Βήμα‑Βήμα

**1. Ανάκτηση Υποστηριζόμενων Τύπων Αρχείων**  
`FileType.GetSupportedFileFormats()` επιστρέφει κάθε μορφή που αναγνωρίζει η βιβλιοθήκη. Η μέθοδος είναι μέρος της κλάσης `GroupDocs.Redaction.FileType`, η οποία περιλαμβάνει μεταδεδομένα όπως η επέκταση αρχείου και το φιλικό όνομα.

**2. Εμφάνιση Υποστηριζόμενων Τύπων Αρχείων**  
Διατρέξτε τη συλλογή και εκτυπώστε την επέκταση και την περιγραφή κάθε μορφής. Παράδειγμα ενσωματωμένου κώδικα:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Το απόσπασμα εκτυπώνει μια καλοταξινομημένη λίστα όπως “.pdf – Portable Document Format”, καθιστώντας το ιδανικό για γέμισμα στοιχείων UI.

### Συμβουλές Επίλυσης Προβλημάτων
- **Λείπει το Πακέτο** – Επαληθεύστε την αναφορά του πακέτου NuGet και επαναφέρετε τα πακέτα αν χρειάζεται.  
- **Λανθασμένη Διαδρομή Άδειας** – Βεβαιωθείτε ότι το αρχείο άδειας έχει αντιγραφεί στον φάκελο εξόδου ή δώστε απόλυτη διαδρομή.  
- **Μη Υποστηριζόμενη Επέκταση** – Αν μια μορφή δεν εμφανίζεται, βεβαιωθείτε ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση της βιβλιοθήκης· οι νεότερες εκδόσεις προσθέτουν επιπλέον μορφές.

## Πρακτικές Εφαρμογές
Η κατανόηση των υποστηριζόμενων μορφών αρχείων ανοίγει πολλές πραγματικές περιπτώσεις:

1. **Συστήματα Διαχείρισης Εγγράφων** – Επικυρώστε τις μεταφορτώσεις έναντι της λίστας υποστήριξης για να αποτρέψετε αποτυχίες επεξεργασίας.  
2. **Ασφάλεια Περιεχομένου** – Εφαρμόστε κανόνες σβησίματος μόνο σε τύπους αρχείων που η μηχανή μπορεί να τροποποιήσει με ασφάλεια.  
3. **Διαδικασίες Μαζικής Επεξεργασίας** – Φιλτράρετε μεγάλες παρτίδες αρχείων πριν καλέσετε το redaction, εξοικονομώντας CPU και μνήμη.

## Σκέψεις Απόδοσης
- **Αποτύπωση Μνήμης** – Η καταγραφή μορφών είναι μια ελαφριά λειτουργία· δεν φορτώνει κανένα έγγραφο στη μνήμη.  
- **Διαδικασίες Μαζικής Επεξεργασίας** – Όταν επεξεργάζεστε εκατοντάδες αρχεία, λάβετε τη λίστα μορφών μία φορά και επαναχρησιμοποιήστε την για να αποφύγετε επαναλαμβανόμενες κλήσεις.  
- **Ασφάλεια Νήματος** – `FileType.GetSupportedFileFormats()` είναι thread‑safe και μπορεί να κληθεί από παράλληλες εργασίες χωρίς συγχρονισμό.

## Συμπέρασμα
Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή προσέγγιση για **πώς να καταγράψετε μορφές** χρησιμοποιώντας το GroupDocs.Redaction .NET. Ενσωματώνοντας αυτή τη δυνατότητα, μπορείτε να ενισχύσετε την επικύρωση, να βελτιώσετε την εμπειρία χρήστη και να διατηρήσετε τις διαδικασίες εγγράφων σας ανθεκτικές.

### Επόμενα Βήματα
- Εξερευνήστε το API `Redactor` για την εφαρμογή κανόνων σβησίματος βάσει τύπου αρχείου.  
- Συνδυάστε τη λίστα μορφών με ένα dropdown στο front‑end για απρόσκοπτη επιλογή αρχείου.  
- Ανασκοπήστε τον οδηγό απόδοσης για βελτιστοποίηση μεγάλων εργασιών batch.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να λάβω τη λίστα μορφών χωρίς να αρχικοποιήσω μια παρουσία Redactor;**  
Α: Ναι, η μέθοδος `FileType.GetSupportedFileFormats()` είναι στατική και δεν απαιτεί αντικείμενο `Redactor`.

**Ε: Η λίστα περιλαμβάνει τόσο μορφές εισόδου όσο και εξόδου;**  
Α: Η μέθοδος επιστρέφει όλες τις μορφές που η βιβλιοθήκη μπορεί να διαβάσει και να γράψει· κάθε `FileType` περιλαμβάνει σημαίες `CanRead` και `CanWrite`.

**Ε: Πόσο συχνά ενημερώνεται η λίστα υποστηριζόμενων μορφών;**  
Α: Η GroupDocs κυκλοφορεί ενημερώσεις μορφών με κάθε έκδοση της βιβλιοθήκης· ο έλεγχος της λίστας σε χρόνο εκτέλεσης εξασφαλίζει ότι έχετε πάντα το πιο πρόσφατο σύνολο.

**Ε: Υπάρχει τρόπος να φιλτράρω μόνο μορφές συμβατές με PDF;**  
Α: Ναι, φιλτράρετε τη συλλογή όπου `format.Extension == ".pdf"` ή όπου `format.Name.Contains("PDF")`.

**Ε: Θα λειτουργήσει αυτή η προσέγγιση σε .NET Core 2.1;**  
Α: Η μέθοδος απαιτεί .NET Core 3.1 ή νεότερη· οι παλαιότερες εκδόσεις δεν υποστηρίζονται.

## Ενότητα Συχνών Ερωτήσεων
1. **Πώς εγκαθιστώ το GroupDocs.Redaction για .NET;**  
   Χρησιμοποιήστε την εντολή CLI `dotnet add package GroupDocs.Redaction` ή εγκαταστήστε μέσω του UI Διαχειριστή Πακέτων NuGet.  
2. **Ποια είναι τα κοινά προβλήματα κατά την ανάκτηση των υποστηριζόμενων μορφών;**  
   Βεβαιωθείτε ότι όλες οι εξαρτήσεις έχουν επαναφερθεί και ότι αναφέρετε το σωστό namespace (`GroupDocs.Redaction`).  
3. **Μπορώ να χρησιμοποιήσω αυτή τη δυνατότητα με μη‑.NET εφαρμογές;**  
   Αυτό το tutorial εστιάζει στο .NET, αλλά η GroupDocs παρέχει παρόμοια API για Java, Python και άλλες πλατφόρμες.  
4. **Πώς μπορώ να βελτιστοποιήσω την απόδοση όταν χρησιμοποιώ το GroupDocs.Redaction;**  
   Επαναχρησιμοποιήστε τη λίστα μορφών, αποφύγετε τη φόρτωση πλήρων εγγράφων όταν ελέγχετε μόνο τη συμβατότητα, και παρακολουθείτε τη χρήση μνήμης κατά τις εργασίες batch.  
5. **Ποιους τύπους αρχείων υποστηρίζει το GroupDocs.Redaction;**  
   Η βιβλιοθήκη υποστηρίζει 30+ μορφές, συμπεριλαμβανομένων PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG και πολλές άλλες. Χρησιμοποιήστε `FileType.GetSupportedFileFormats()` για να δείτε τη πλήρη λίστα.

## Πόροι
- [Τεκμηρίωση](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API](https://reference.groupdocs.com/redaction/net)
- [Λήψη GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Δωρεάν Φόρουμ Υποστήριξης](https://forum.groupdocs.com/c/redaction/33)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

**Τελευταία Ενημέρωση:** 2026-07-20  
**Δοκιμάστηκε Με:** GroupDocs.Redaction 4.2.0 for .NET  
**Συγγραφέας:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Σχετικά Μαθήματα

- [Μαθήματα Διαχείρισης Μορφών για το GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Μαθήματα Φόρτωσης Εγγράφων με το GroupDocs.Redaction για .NET](/redaction/net/document-loading/)
- [Μαθήματα Αποθήκευσης Εγγράφων για το GroupDocs.Redaction .NET](/redaction/net/document-saving/)