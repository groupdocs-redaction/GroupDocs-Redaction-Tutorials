---
date: '2026-07-20'
description: Μάθετε πώς να αποκρύψετε έγγραφα, να κρύψετε ευαίσθητες πληροφορίες και
  να αποθηκεύσετε τα επεξεργασμένα αρχεία σε memory stream χρησιμοποιώντας το GroupDocs.Redaction
  for .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Πώς να αποκρύψετε έγγραφα με το GroupDocs.Redaction for .NET. Ακολουθήστε
  αυτόν τον step‑by‑step οδηγό για να κρύψετε ευαίσθητες πληροφορίες και να αποθηκεύσετε
  το επεξεργασμένο αρχείο σε memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Πώς να αποκρύψετε έγγραφα με το GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Πώς να αποκρύψετε έγγραφα με το GroupDocs.Redaction for .NET – Ένας πλήρης
  οδηγός
type: docs
url: /el/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Πώς να διαγράψετε έγγραφα με το GroupDocs.Redaction για .NET

Σε σύγχρονα επιχειρηματικά περιβάλλοντα, **πώς να διαγράψετε έγγραφα** είναι μια κρίσιμη δεξιότητα για την προστασία προσωπικών δεδομένων, εμπορικών μυστικών και πληροφοριών σχετικών με τη συμμόρφωση. Αυτός ο οδηγός σας καθοδηγεί στη διαγραφή ευαίσθητων πληροφοριών από αρχεία Word, PDF ή εικόνας και στη συνέχεια στην αποθήκευση του επεξεργασμένου αποτελέσματος απευθείας σε ροή μνήμης — όλα με το GroupDocs.Redaction για .NET.

## Γρήγορες Απαντήσεις
- **Τι κάνει η διαγραφή;** Αντικαθιστά μόνιμα το επιλεγμένο περιεχόμενο με έναν δείκτη ή το αφαιρεί, διασφαλίζοντας ότι τα δεδομένα δεν μπορούν ποτέ να ανακτηθούν.  
- **Ποιοι τύποι αρχείων υποστηρίζονται;** Πάνω από 30 τύπους αρχείων, συμπεριλαμβανομένων PDF, DOCX, PPTX και κοινών μορφών εικόνας.  
- **Μπορώ να διαγράψω χωρίς να γράψω στο δίσκο;** Ναι — αποθηκεύστε το αποτέλεσμα σε `MemoryStream` για επεξεργασία στη μνήμη.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται πλήρης άδεια για χρήση σε παραγωγή· διατίθεται δωρεάν δοκιμή για αξιολόγηση.  
- **Είναι συμβατό με .NET Core;** Απόλυτα — το GroupDocs.Redaction λειτουργεί με .NET Framework 4.6+, .NET Core 3.1+ και .NET 5/6/7.

## Τι είναι η Διαγραφή Εγγράφων;
Η διαγραφή εγγράφων αφαιρεί μόνιμα ή καλύπτει εμπιστευτικό κείμενο, εικόνες και μεταδεδομένα από ένα αρχείο, διασφαλίζοντας ότι το κρυφό περιεχόμενο δεν μπορεί να ανακτηθεί, να προβληθεί ή να εξαχθεί αργότερα. Αντικαθιστά τα ευαίσθητα στοιχεία με έναν δείκτη όπως ένα μαύρο ορθογώνιο ή προσαρμοσμένο κείμενο, και ενημερώνει τη δομή του εγγράφου ώστε τα διαγραμμένα δεδομένα να είναι ακατάσβεστα.

## Γιατί να Χρησιμοποιήσετε το GroupDocs.Redaction για τη Διαγραφή Εγγράφων;
Το GroupDocs.Redaction υποστηρίζει **πάνω από 30 μορφές αρχείων** και μπορεί να επεξεργαστεί αρχεία έως **2 GB** χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη, προσφέροντας **30 % ταχύτερο χρόνο επεξεργασίας** σε σύγκριση με πολλούς ανταγωνιστές. Το API του σας επιτρέπει να εφαρμόζετε διαγραφές ακριβούς φράσης, κανονικής έκφρασης ή βασισμένες σε εικόνα με μία κλήση μεθόδου, καθιστώντας το την πιο αποδοτική επιλογή για προγραμματιστές .NET.

## Προαπαιτούμενα
- **GroupDocs.Redaction** πακέτο NuGet (τελευταία έκδοση).  
- .NET Framework 4.6+ **ή** .NET Core 3.1+ εγκατεστημένο.  
- Ένα IDE συμβατό με C# όπως το Visual Studio 2022.  
- Βασικές γνώσεις C# και εξοικείωση με file I/O.

### Απαιτούμενες Βιβλιοθήκες και Εκδόσεις
- **GroupDocs.Redaction** – χρησιμοποιείτε πάντα την πιο πρόσφατη έκδοση για πρόσβαση στους τελευταίους αλγόριθμους διαγραφής και ενημερώσεις ασφαλείας.  
- **System.IO** – για διαχείριση ροών (ενσωματωμένο στο .NET).

### Βήματα Απόκτησης Άδειας
- **Δωρεάν Δοκιμή:** Εγγραφείτε στην ιστοσελίδα του GroupDocs για δοκιμή 30 ημερών.  
- **Προσωρινή Άδεια:** Ζητήστε ένα προσωρινό κλειδί για δοκιμές ανάπτυξης.  
- **Πλήρης Άδεια:** Αγοράστε άδεια παραγωγής για απεριόριστη χρήση.

## Βασική Αρχικοποίηση και Ρύθμιση
Η κλάση `Redactor` είναι το σημείο εισόδου για όλες τις λειτουργίες διαγραφής στο GroupDocs.Redaction. Αφού εγκαταστήσετε το πακέτο NuGet, δημιουργείτε ένα αντικείμενο `Redactor` με τη διαδρομή του πηγαίου εγγράφου.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Πώς να Διαγράψετε Συγκεκριμένο Κείμενο σε Ένα Έγγραφο;
Για να διαγράψετε συγκεκριμένο κείμενο, φορτώστε το πηγαίο αρχείο με μια παρουσία `Redactor`, στη συνέχεια εφαρμόστε ένα `ExactPhraseRedaction` που στοχεύει στη συγκεκριμένη συμβολοσειρά που θέλετε να κρύψετε. Το API σαρώει το έγγραφο, αντικαθιστά κάθε αντιστοιχία με την επιλεγμένη επικάλυψη και καταγράφει τις αλλαγές σε ένα αρχείο καταγραφής αλλαγών, επιτρέποντάς σας να επαληθεύσετε τη διαγραφή πριν την αποθήκευση.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

Η κλάση `ExactPhraseRedaction` αντικαθιστά κάθε εμφάνιση της ακριβούς φράσης με ένα μαύρο ορθογώνιο (ή οποιονδήποτε προσαρμοσμένο δείκτη έχετε ρυθμίσει).  

**Βήμα‑Βήμα:**
1. **Φόρτωση** – Δημιουργήστε μια παρουσία `Redactor` που δείχνει στο αρχείο σας.  
2. **Εφαρμογή** – Καλέστε `Apply` με ένα `ExactPhraseRedaction` (ή άλλο τύπο διαγραφής).  
3. **Έλεγχος** – Εξετάστε το `RedactorChangeLog` για να επιβεβαιώσετε πόσες αντιστοιχίες βρέθηκαν και αντικαταστάθηκαν.  

## Πώς να Αποθηκεύσετε ένα Διαγραμμένο Έγγραφο σε Μνήμη (Memory Stream);
`MemoryStream` είναι μια ροή .NET που αποθηκεύει δεδομένα στη μνήμη, επιτρέποντας γρήγορη ανάγνωση/εγγραφή χωρίς I/O δίσκου. Χρησιμοποιώντας τη μέθοδο `Save`, μπορείτε να κατευθύνετε το διαγραμμένο αποτέλεσμα σε ένα `MemoryStream`, το οποίο μπορεί στη συνέχεια να σταλεί μέσω δικτύου, να αποθηκευτεί σε βάση δεδομένων ή να επιστραφεί απευθείας από ένα API endpoint χωρίς δημιουργία προσωρινών αρχείων.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Βασικά Σημεία:**
- Η μέθοδος `Save` γράφει το διαγραμμένο αποτέλεσμα σε οποιαδήποτε υλοποίηση `Stream`, συμπεριλαμβανομένου του `MemoryStream`.  
- Δεν δημιουργούνται προσωρινά αρχεία, κάτι που βελτιώνει την ασφάλεια και την απόδοση.  
- Μπορείτε να το συνδυάσετε με το `FileStreamResult` του ASP.NET Core για να επιστρέψετε το αρχείο απευθείας σε έναν φυλλομετρητή.

## Συνηθισμένα Προβλήματα και Λύσεις
| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| **Η διαγραφή δεν εφαρμόστηκε** | Η περίπτωση (κεφαλαία/μικρά) της φράσης διαφέρει από την πηγή. | Χρησιμοποιήστε `ExactPhraseRedaction("John Doe", caseSensitive: false)` ή μια διαγραφή με κανονική έκφραση για ευέλικτο ταίριασμα. |
| **Μεγάλα αρχεία προκαλούν OutOfMemory** | Προσπάθεια φόρτωσης ολόκληρου του αρχείου στη μνήμη. | Το GroupDocs.Redaction μεταδίδει δεδομένα εσωτερικά· βεβαιωθείτε ότι χρησιμοποιείτε την πιο πρόσφατη έκδοση που επεξεργάζεται τα αρχεία σε τμήματα. |
| **Το αποθηκευμένο αρχείο είναι κατεστραμμένο** | Η ροή δεν επαναφέρθηκε πριν την αποστολή. | Μετά το `redactor.Save(stream)`, ορίστε `stream.Position = 0` πριν το διαβάσετε ή το επιστρέψετε. |

## Συχνές Ερωτήσεις

**Ε: Μπορώ να διαγράψω αρχεία PDF χρησιμοποιώντας το ίδιο API;**  
Α: Ναι — το GroupDocs.Redaction αντιμετωπίζει PDF, DOCX, PPTX και πολλές μορφές εικόνας ομοιόμορφα· απλώς δείξτε το `Redactor` σε ένα αρχείο PDF.

**Ε: Η διαγραφή παραμένει μετά τη μετατροπή του εγγράφου σε άλλη μορφή;**  
Α: Απόλυτα — μόλις διαγραφεί, το περιεχόμενο αφαιρείται μόνιμα, ανεξάρτητα από τις επόμενες μετατροπές.

**Ε: Πώς μπορώ να προσαρμόσω την εμφάνιση της διαγραφής;**  
Α: Χρησιμοποιήστε `RedactionOptions` για να ορίσετε το χρώμα της επικάλυψης, τη διαφάνεια ή να αντικαταστήσετε το κείμενο με μια προσαρμοσμένη συμβολοσειρά.

**Ε: Είναι δυνατόν να διαγράψετε χρησιμοποιώντας κανονικές εκφράσεις;**  
Α: Ναι — το `RegexRedaction` σας επιτρέπει να ορίσετε μοτίβα όπως αριθμούς πιστωτικών καρτών ή διευθύνσεις email.

**Ε: Ποιες εκδόσεις .NET υποστηρίζονται επίσημα;**  
Α: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 και .NET 7.

---

**Τελευταία Ενημέρωση:** 2026-07-20  
**Δοκιμή Με:** GroupDocs.Redaction 23.12 for .NET  
**Συγγραφέας:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Σχετικά Μαθήματα

- [Πώς να Φορτώσετε και να Διαγράψετε Έγγραφα Χρησιμοποιώντας το GroupDocs.Redaction .NET: Ένας Πλήρης Οδηγός](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Αποθήκευση Διαγραμμένων Εγγράφων στην Αρχική Μορφή Χρησιμοποιώντας το GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Ασφαλής Διαγραφή Εγγράφων σε .NET Χρησιμοποιώντας Ροές: Ένας Οδηγός για το GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)