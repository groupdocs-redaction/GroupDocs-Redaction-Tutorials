---
date: 2026-08-04
description: Μάθετε πώς να φιλτράρετε δεδομένα λογιστικού φύλλου java και να διαγράψετε
  με ασφάλεια στήλες ή κελιά σε λογιστικά φύλλα Excel χρησιμοποιώντας το GroupDocs.Redaction
  για Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Μάθετε πώς να φιλτράρετε δεδομένα λογιστικού φύλλου java και να διαγράψετε
  με ασφάλεια στήλες ή κελιά σε λογιστικά φύλλα Excel χρησιμοποιώντας το GroupDocs.Redaction
  για Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Φιλτράρισμα δεδομένων λογιστικού φύλλου java – οδηγός με GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Φιλτράρισμα δεδομένων λογιστικού φύλλου java – οδηγός με GroupDocs.Redaction
type: docs
url: /el/java/spreadsheet-redaction/
weight: 12
---

# Φιλτράρισμα δεδομένων λογιστικού φύλλου java – Οδηγός GroupDocs.Redaction Java

Αν χρειάζεστε **filter spreadsheet data java** πριν εφαρμόσετε τη διαγραφή, έχετε βρεθεί στον σωστό οδηγό. Σε αυτόν τον οδηγό θα ανακαλύψετε πώς να απομονώσετε γραμμές, στήλες ή μεμονωμένα κελιά που περιέχουν προσωπικές ή εμπιστευτικές πληροφορίες, και στη συνέχεια να τα διαγράψετε με ασφάλεια χρησιμοποιώντας το GroupDocs.Redaction for Java. Τα βήματα εξηγούνται με απλή γλώσσα, περιλαμβάνουν συμβουλές βέλτιστων πρακτικών και δείχνουν πώς να διατηρείτε την επεξεργασία γρήγορη ακόμη και σε μεγάλα βιβλία εργασίας.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται τη διαγραφή λογιστικών φύλλων σε Java;** GroupDocs.Redaction for Java.  
- **Μπορώ να φιλτράρω γραμμές χωρίς να φορτώσω ολόκληρο το αρχείο στη μνήμη;** Ναι – το API μεταδίδει δεδομένα σε ροή και σας επιτρέπει να εφαρμόζετε φίλτρα άμεσα.  
- **Ποια μορφές αρχείων υποστηρίζονται;** Πάνω από 30 μορφές λογιστικών φύλλων, συμπεριλαμβανομένων των XLS, XLSX, CSV και ODS.  
- **Χρειάζομαι άδεια για ανάπτυξη;** Μια προσωρινή άδεια λειτουργεί για δοκιμές· απαιτείται πλήρης άδεια για παραγωγή.  
- **Υπάρχει όριο στο μέγεθος του βιβλίου εργασίας;** Η μηχανή μπορεί να επεξεργαστεί αρχεία έως 500 MB χωρίς υπερβολική κατανάλωση μνήμης.

## Τι είναι το filter spreadsheet data java;
**Filter spreadsheet data java** είναι η διαδικασία προγραμματιστικής επιλογής συγκεκριμένων γραμμών, στηλών ή κελιών σε ένα βιβλίο εργασίας τύπου Excel χρησιμοποιώντας κώδικα Java, ώστε μόνο το στοχευμένο περιεχόμενο να εξετάζεται ή να διαγράφεται. Αυτή η τεχνική μειώνει το χρόνο εκτέλεσης, περιορίζει τις περιττές αλλαγές και βοηθά στην τήρηση συμμόρφωσης τύπου GDPR.

## Γιατί να φιλτράρετε δεδομένα λογιστικού φύλλου java;
GroupDocs.Redaction Java υποστηρίζει **30+ μορφές λογιστικών φύλλων** και μπορεί να επεξεργαστεί βιβλία εργασίας που περιέχουν **έως 500 MB** (περίπου 1 εκατομμύριο γραμμές) διατηρώντας τη χρήση μνήμης κάτω από **200 MB**. Φιλτράροντας πρώτα, αποφεύγετε την επεξεργασία άσχετων δεδομένων, κάτι που μειώνει τον χρόνο επεξεργασίας κατά **40‑60 %** κατά μέσο όρο για τυπικά σενάρια καθαρισμού ιδιωτικότητας.

## Προαπαιτούμενα
- Εγκατεστημένο Java 17 ή νεότερο.  
- Σύστημα κατασκευής Maven ή Gradle.  
- GroupDocs.Redaction for Java (διαθέσιμο για λήψη από την επίσημη ιστοσελίδα).  
- Ένα προσωρινό ή πλήρες κλειδί άδειας.

## Πώς να φιλτράρετε δεδομένα σε λογιστικά φύλλα χρησιμοποιώντας το GroupDocs.Redaction Java;
Φορτώστε το βιβλίο εργασίας, ορίστε ένα φίλτρο που ταιριάζει στα κελιά που θέλετε να διαγράψετε, και στη συνέχεια εφαρμόστε τη λειτουργία διαγραφής. Το API εκτελεί το φίλτρο με μορφή ροής, έτσι δεν χρειάζεται ποτέ να κρατάτε ολόκληρο το αρχείο στη μνήμη RAM.

Η κλάση `RedactionFilter` σας επιτρέπει να καθορίσετε δείκτες στηλών, περιοχές γραμμών ή προσαρμοσμένα λογικά κριτήρια. Για παράδειγμα, μπορείτε να στοχεύσετε κάθε κελί στη στήλη **B** που περιέχει μοτίβο διεύθυνσης email, ή μπορείτε να περιορίσετε τη διαγραφή σε γραμμές όπου η στήλη “Status” ισούται με “Confidential”.

**Άμεση απάντηση (40‑70 λέξεις):**  
Δημιουργήστε ένα αντικείμενο `RedactionFilter`, ορίστε τον δείκτη στήλης και μια συνθήκη κανονικής έκφρασης, και στη συνέχεια περάστε το φίλτρο στο `Redactor.redact(workbook, filter)`. Αυτό το φίλτρο μίας γραμμής απομονώνει τα ακριβή κελιά που ταιριάζουν στα κριτήριά σας, και ο redactor τα αφαιρεί ή τα καλύπτει ενώ αφήνει το υπόλοιπο φύλλο αμετάβλητο. Η λειτουργία ολοκληρώνεται σε γραμμικό χρόνο σε σχέση με τις φιλτραρισμένες γραμμές.

### Βήμα 1: δημιουργία του φίλτρου
`RedactionFilter` είναι η βασική κλάση που αντιπροσωπεύει έναν κανόνα φιλτραρίσματος για τη διαγραφή λογιστικών φύλλων. Δέχεται αριθμούς στηλών, αριθμούς γραμμών ή προσαρμοσμένες εκφράσεις lambda για τον εντοπισμό των δεδομένων.

### Βήμα 2: διαμόρφωση της συνθήκης
Χρησιμοποιήστε `filter.setColumnIndex(1)` για να στοχεύσετε τη στήλη B (μηδενική βάση) και `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` για να ταιριάξετε μοτίβα email. Μπορείτε επίσης να συνδυάσετε πολλαπλές συνθήκες με `filter.and(...)` ή `filter.or(...)`.

### Βήμα 3: εφαρμογή της διαγραφής
`Redactor` είναι η κύρια κλάση που εκτελεί λειτουργίες διαγραφής σε ένα βιβλίο εργασίας.  
Περάστε το βιβλίο εργασίας και το διαμορφωμένο φίλτρο στο αντικείμενο `Redactor`. Το API μεταδίδει το βιβλίο εργασίας σε ροή, εφαρμόζει το φίλτρο και γράφει το αποτέλεσμα της διαγραφής σε νέο αρχείο, διατηρώντας την αρχική μορφοποίηση και τους τύπους.

## Συχνά προβλήματα και λύσεις
- **Το φίλτρο δεν ταιριάζει με κανένα κελί:** Επαληθεύστε τον δείκτη στήλης (μηδενική βάση) και βεβαιωθείτε ότι η σύνταξη της κανονικής έκφρασης είναι σωστή για Java.  
- **Σφάλματα έλλειψης μνήμης σε μεγάλα αρχεία:** Αυξήστε το μέγεθος της στοίβας JVM με μέτρο (π.χ., `-Xmx1g`) ή χωρίστε το βιβλίο εργασίας σε μικρότερα τμήματα πριν το φιλτράρισμα.  
- **Η διαγραμμένη έξοδος χάνει μορφοποίηση:** `RedactionOptions` σας επιτρέπει να προσαρμόσετε τη συμπεριφορά της διαγραφής, όπως η διατήρηση της μορφοποίησης των κελιών. Χρησιμοποιήστε `RedactionOptions.setPreserveFormatting(true)` για να διατηρήσετε τα στυλ των κελιών αμετάβλητα.

## Γιατί να φιλτράρετε δεδομένα λογιστικού φύλλου;
Το φιλτράρισμα πριν από τη διαγραφή απομονώνει μόνο τα ευαίσθητα τμήματα ενός βιβλίου εργασίας, πράγμα που σημαίνει ότι αποφεύγετε περιττές αλλαγές σε καθαρά δεδομένα. Αυτή η επιλεκτική προσέγγιση μειώνει επίσης τον κίνδυνο τυχαίας απώλειας δεδομένων και επιταχύνει τους ελέγχους συμμόρφωσης, επειδή το αρχείο ελέγχου περιέχει πολύ λιγότερες καταχωρήσεις.

## Πώς να διαγράψετε email σε λογιστικά φύλλα Excel χρησιμοποιώντας το GroupDocs.Redaction Java API
Φορτώστε το αρχείο Excel, εφαρμόστε ένα φίλτρο που αναζητά το τυπικό μοτίβο email και καλέστε τον redactor. Το API αντικαθιστά κάθε ταιριαστό email με έναν δείκτη όπως “***@***.com” διατηρώντας τη διάταξη των γύρω κελιών.

## Πώς να φιλτράρετε δεδομένα – διαθέσιμοι οδηγοί
- [Πώς να διαγράψετε email σε λογιστικά φύλλα Excel χρησιμοποιώντας το GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Πρόσθετοι πόροι

- [Τεκμηρίωση GroupDocs.Redaction for Java](https://docs.groupdocs.com/redaction/java/)
- [Αναφορά API GroupDocs.Redaction for Java](https://reference.groupdocs.com/redaction/java/)
- [Λήψη GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [Φόρουμ GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Δωρεάν Υποστήριξη](https://forum.groupdocs.com/)
- [Προσωρινή Άδεια](https://purchase.groupdocs.com/temporary-license/)

---

**Τελευταία ενημέρωση:** 2026-08-04  
**Δοκιμή με:** GroupDocs.Redaction 23.11 for Java  
**Συγγραφέας:** GroupDocs  

## Συχνές ερωτήσεις

**Q: Μπορώ να φιλτράρω πολλές στήλες ταυτόχρονα;**  
A: Ναι, μπορείτε να προσθέσετε επιπλέον δείκτες στηλών στην ίδια παρουσία `RedactionFilter` ή να συνδέσετε πολλαπλά φίλτρα με `filter.or(...)`.

**Q: Λειτουργεί το φίλτρο σε βιβλία εργασίας με προστασία κωδικού;**  
A: Παρέχετε τον κωδικό κατά το άνοιγμα του βιβλίου εργασίας· το φίλτρο λειτουργεί μετά την αποκρυπτογράφηση όπως σε ένα μη προστατευμένο αρχείο.

**Q: Πόσες γραμμές μπορεί να διαχειριστεί το API σε μία ενέργεια;**  
A: Η μηχανή είναι βελτιστοποιημένη για έως 1 εκατομμύριο γραμμές (≈500 MB) χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη.

**Q: Είναι δυνατόν να προεπισκοπήσετε ποια κελιά θα διαγραφούν πριν την αποθήκευση;**  
A: Ναι, καλέστε `filter.preview(workbook)` για να λάβετε μια λίστα με τις διευθύνσεις κελιών που ταιριάζουν στα κριτήρια.

**Q: Ποιο μοντέλο αδειοδότησης απαιτείται για παραγωγική χρήση;**  
A: Απαιτείται πλήρης εμπορική άδεια για παραγωγικές εγκαταστάσεις· μια προσωρινή άδεια αρκεί για δοκιμές και αξιολόγηση.

## Σχετικοί οδηγοί

- [Πώς να διαγράψετε ευαίσθητα δεδομένα σε λογιστικά φύλλα Excel χρησιμοποιώντας το GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Απόκρυψη ευαίσθητων δεδομένων Java – Οδηγός GroupDocs.Redaction](/redaction/java/getting-started/)
- [Απόκρυψη ευαίσθητων δεδομένων Java – Διαγραφή προσωπικών πληροφοριών με το GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)