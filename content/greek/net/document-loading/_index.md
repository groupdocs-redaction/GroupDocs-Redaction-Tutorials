---
date: 2026-06-11
description: Μάθετε πώς να φορτώνετε έγγραφα, συμπεριλαμβανομένων των streams και
  των password‑protected files, χρησιμοποιώντας το GroupDocs.Redaction για .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Πώς να φορτώσετε ένα έγγραφο με GroupDocs.Redaction για .NET
type: docs
url: /el/net/document-loading/
weight: 2
---

# Πώς να φορτώσετε έγγραφο με το GroupDocs.Redaction για .NET

Σε αυτόν τον οδηγό θα ανακαλύψετε **πώς να φορτώσετε έγγραφο** αρχεία στο GroupDocs.Redaction για .NET από διάφορες πηγές—τοπικό δίσκο, ροές μνήμης και ακόμη αρχεία με προστασία κωδικού. Είτε δημιουργείτε μια υπηρεσία διαγραφής, μια αυτοματοποιημένη γραμμή συμμόρφωσης, είτε ένα απλό εργαλείο επιφάνειας εργασίας, η εξοικείωση με αυτές τις τεχνικές φόρτωσης σας επιτρέπει να προετοιμάσετε οποιοδήποτε έγγραφο για ασφαλή διαγραφή γρήγορα και αξιόπιστα.

## Γρήγορες απαντήσεις
- **Ποιο είναι το πρώτο βήμα;** Εγκαταστήστε το πακέτο NuGet GroupDocs.Redaction και προσθέστε το χώρο ονομάτων `using GroupDocs.Redaction;`.  
- **Μπορώ να φορτώσω ένα PDF από ροή (stream);** Ναι—περάστε ένα `MemoryStream` που περιέχει τα byte του PDF στον κατασκευαστή `RedactionEngine`.  
- **Πώς ανοίγω ένα αρχείο με προστασία κωδικού;** Παρέχετε τον κωδικό ως δεύτερο όρισμα κατά τη δημιουργία του `RedactionEngine`.  
- **Υπάρχει όριο στο μέγεθος του αρχείου;** Το GroupDocs.Redaction επεξεργάζεται αρχεία έως 2 GB χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγικές αναπτύξεις.

## Πώς να φορτώσετε έγγραφο;
`RedactionEngine` είναι η κύρια κλάση που φορτώνει και προετοιμάζει έγγραφα για διαγραφή. Φορτώστε ένα έγγραφο δημιουργώντας μια παρουσία `RedactionEngine` με τη διαδρομή του αρχείου (ή τη ροή) και, αν χρειάζεται, τον κωδικό. Αυτή η κλήση μιας γραμμής διαβάζει το αρχείο, επικυρώνει τη μορφή και δημιουργεί το εσωτερικό μοντέλο εγγράφου έτοιμο για διαγραφή. Για παράδειγμα, η φόρτωση ενός PDF από δίσκο είναι τόσο απλή όσο `new RedactionEngine("sample.pdf")`. Όταν απαιτείται κωδικός, χρησιμοποιήστε `new RedactionEngine("secret.pdf", "MyPassword")`. Η φόρτωση από ροή ακολουθεί το ίδιο μοτίβο με όρισμα `MemoryStream`.

## Τι είναι το GroupDocs.Redaction;
GroupDocs.Redaction είναι μια βιβλιοθήκη .NET που επιτρέπει στους προγραμματιστές να εντοπίζουν και να αφαιρούν μόνιμα ευαίσθητο περιεχόμενο από PDF, DOCX, PPTX και πάνω από 30 άλλες μορφές αρχείων. Προσφέρει διαγραφή pixel‑perfect, υποστήριξη OCR και επεξεργασία παρτίδας, καθιστώντας το ιδανικό για εφαρμογές που βασίζονται στη συμμόρφωση και απαιτούν αξιόπιστη και ασφαλή προστασία δεδομένων σε πολλούς τύπους εγγράφων.

## Γιατί να χρησιμοποιήσετε το GroupDocs.Redaction για τη φόρτωση εγγράφων;
GroupDocs.Redaction παρέχει μια υψηλής απόδοσης, χαμηλής μνήμης μηχανή ροής που μπορεί να χειριστεί μεγάλα αρχεία έως 2 GB, ενώ υποστηρίζει και αρχεία με προστασία κωδικού έτοιμα για χρήση. Αυτός ο συνδυασμός ταχύτητας, ευελιξίας και ασφάλειας το καθιστά την προτιμώμενη επιλογή για προγραμματιστές που χρειάζονται γρήγορη και ασφαλή φόρτωση εγγράφων πριν εφαρμόσουν κανόνες διαγραφής.

- **Ευρεία υποστήριξη μορφών:** Διαχειρίζεται **30+** τύπους εγγράφων, συμπεριλαμβανομένων PDF, Word, Excel, PowerPoint και αρχείων εικόνας.  
- **Υψηλής απόδοσης ροή:** Επεξεργάζεται αρχεία έως **2 GB** χρησιμοποιώντας μια μηχανή ροής χαμηλής μνήμης, εξαλείφοντας την ανάγκη πλήρους φόρτωσης του αρχείου.  
- **Διαχείριση κωδικού:** Ανοίγει αβίαστα **PDF και αρχεία Office με προστασία κωδικού** με μια μόνο υπερφόρτωση μεθόδου, μειώνοντας την πολυπλοκότητα του κώδικα.  
- **Thread‑safe API:** Επιτρέπει ταυτόχρονη φόρτωση πολλαπλών εγγράφων σε πολυνηματικές υπηρεσίες χωρίς προβλήματα ανταγωνισμού.

## Προαπαιτούμενα
- .NET 6.0 ή νεότερο (η βιβλιοθήκη υποστηρίζει επίσης .NET Core 3.1 και .NET Framework 4.6.1+).  
- Έγκυρη άδεια GroupDocs.Redaction (προσωρινή άδεια για δοκιμές).  
- Πρόσβαση στα αρχεία εγγράφων που προτίθεστε να διαγράψετε (τοπική διαδρομή, byte array ή ροή).

## Φόρτωση εγγράφων από διαφορετικές πηγές

### Φόρτωση από τοπικό δίσκο
Παρέχετε την απόλυτη ή σχετική διαδρομή του αρχείου κατά τη δημιουργία του κινητήρα. Η βιβλιοθήκη ανιχνεύει αυτόματα τη μορφή και το προετοιμάζει για διαγραφή.

### Φόρτωση από Memory Stream
Διαβάστε το αρχείο σε ένα `byte[]`, τυλίξτε το σε ένα `MemoryStream` και περάστε τη ροή στον κατασκευαστή. Αυτή η προσέγγιση είναι ιδανική για web API που λαμβάνουν αρχεία ως μεταφορτώσεις.

### Φόρτωση αρχείων με προστασία κωδικού
Όταν ένα έγγραφο είναι κρυπτογραφημένο, δώστε τον κωδικό ως δεύτερο όρισμα. Η μηχανή αποκρυπτογραφεί το αρχείο εν κινήσει και κάνει το περιεχόμενο διαθέσιμο για διαγραφή χωρίς επιπλέον βήματα.

## Συχνά προβλήματα και λύσεις

- **Error: “File format not supported.”**  
  Επαληθεύστε ότι η επέκταση του αρχείου ταιριάζει με μια υποστηριζόμενη μορφή και ότι το αρχείο δεν είναι κατεστραμμένο. Το GroupDocs.Redaction υποστηρίζει πάνω από 30 μορφές· συμβουλευτείτε την αναφορά API για την πλήρη λίστα.

- **Password‑related exception.**  
  Βεβαιωθείτε ότι η συμβολοσειρά κωδικού είναι σωστή και ότι το αρχείο πραγματικά απαιτεί κωδικό. Η παροχή κενής συμβολοσειράς σε προστατευμένο αρχείο θα προκαλέσει σφάλμα πιστοποίησης.

- **Out‑of‑memory for very large files.**  
  Χρησιμοποιήστε την υπερφόρτωση ροής (`RedactionEngine(Stream)`) αντί για φόρτωση του αρχείου με διαδρομή. Αυτό διατηρεί τη χρήση μνήμης χαμηλή ακόμη και για PDF με εκατοντάδες σελίδες.

## Συχνές ερωτήσεις

**Q: Μπορώ να φορτώσω αρχεία DOCX με τον ίδιο τρόπο που φορτώνω PDFs;**  
A: Ναι—το GroupDocs.Redaction ανιχνεύει αυτόματα τη μορφή DOCX όταν περάσετε τη διαδρομή του αρχείου ή τη ροή, οπότε δεν απαιτείται επιπλέον κώδικας.

**Q: Η βιβλιοθήκη υποστηρίζει τη φόρτωση αρχείων από Azure Blob Storage;**  
A: Απόλυτα. Ανακτήστε το blob ως byte array ή ροή και δώστε το στον κατασκευαστή `RedactionEngine`.

**Q: Τι συμβαίνει αν δώσω λάθος κωδικό;**  
A: Ο κατασκευαστής ρίχνει μια `PasswordIncorrectException`. Πιάστε αυτήν την εξαίρεση για να ζητήσετε από τον χρήστη τον σωστό κωδικό.

**Q: Είναι δυνατόν να φορτώσω πολλαπλά έγγραφα ταυτόχρονα;**  
A: Ναι—κάθε παρουσία `RedactionEngine` είναι ανεξάρτητη και thread‑safe, επιτρέποντας παράλληλη επεξεργασία σε υπηρεσίες παρασκηνίου.

**Q: Πρέπει να απελευθερώσω το RedactionEngine χειροκίνητα;**  
A: Η μηχανή υλοποιεί το `IDisposable`. Καλέστε `Dispose()` ή τυλίξτε την σε ένα `using` block για να απελευθερώσετε άμεσα τους χειριστές αρχείων.

## Πρόσθετοι πόροι

- [Πώς να φορτώσετε και να διαγράψετε έγγραφα χρησιμοποιώντας το GroupDocs.Redaction .NET: Ένας πλήρης οδηγός](./groupdocs-redaction-net-load-redact-documents/)
- [Πώς να διαγράψετε με ασφάλεια έγγραφα με προστασία κωδικού χρησιμοποιώντας το GroupDocs.Redaction σε .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Τεκμηρίωση GroupDocs.Redaction για .NET](https://docs.groupdocs.com/redaction/net/)
- [Αναφορά API GroupDocs.Redaction για .NET](https://reference.groupdocs.com/redaction/net/)
- [Λήψη GroupDocs.Redaction για .NET](https://releases.groupdocs.com/redaction/net/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή άδεια](https://purchase.groupdocs.com/temporary-license/)

**Τελευταία ενημέρωση:** 2026-06-11  
**Δοκιμή με:** GroupDocs.Redaction 5.5 for .NET  
**Συγγραφέας:** GroupDocs

## Σχετικά μαθήματα

- [Πώς να φορτώσετε και να διαγράψετε έγγραφα χρησιμοποιώντας το GroupDocs.Redaction .NET: Ένας πλήρης οδηγός](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Διαγραφή και αποθήκευση εγγράφων με το GroupDocs.Redaction για .NET: Ένας πλήρης οδηγός](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)