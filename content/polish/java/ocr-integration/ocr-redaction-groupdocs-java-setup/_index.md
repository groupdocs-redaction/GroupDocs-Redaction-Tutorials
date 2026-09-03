---
date: '2026-06-26'
description: Dowiedz się, jak wyodrębnić tekst ze zeskanowanego PDF i maskować wrażliwe
  dane przy użyciu GroupDocs OCR Redaction oraz Azure OCR. Redaguj social security
  number i skutecznie zastępuj poufne informacje w PDF.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Wyodrębnij tekst ze zeskanowanego PDF – Maskuj dane za pomocą GroupDocs OCR
type: docs
url: /pl/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Wyodrębnianie tekstu ze skanowanego PDF – Maskowanie danych przy użyciu GroupDocs OCR

W dzisiejszym świecie napędzanym danymi, **wyodrębnianie tekstu ze skanowanych plików PDF** i maskowanie poufnych informacji jest nieodłącznym krokiem zapewniającym zgodność. Ten samouczek przeprowadzi Cię przez użycie GroupDocs Redaction wraz z Microsoft Azure OCR, aby niezawodnie rozpoznawać ukryty tekst na zeskanowanych stronach i zastępować go bezpiecznym symbolem, takim jak **`[REDACTED]`**. Zobaczysz, dlaczego to połączenie jest szybkie, dokładne i gotowe do produkcyjnych obciążeń.

## Szybkie odpowiedzi
- **Co oznacza „maskowanie wrażliwych danych”?** Zastępuje zidentyfikowany poufny tekst symbolem zastępczym (np. `[REDACTED]`).  
- **Która biblioteka obsługuje OCR?** Microsoft Azure OCR connector, używany przez GroupDocs Redaction.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w celach oceny; stała licencja jest wymagana w produkcji.  
- **Czy mogę redagować zeskanowane PDF-y?** Tak — OCR wyodrębnia ukryty tekst przed zastosowaniem redakcji regex.  
- **Czy to rozwiązanie jest tylko w Javie?** Przykład jest oparty na Javie, ale GroupDocs udostępnia podobne API dla .NET i innych platform.

## Czym jest redakcja oparta na OCR?
Redakcja oparta na OCR najpierw uruchamia OCR na każdej stronie, przekształcając obrazy w tekst przeszukiwalny, a następnie stosuje wzorce regex, aby zastąpić dopasowania maską, taką jak `[REDACTED]`. Ten dwustopniowy proces pozwala niezawodnie ukrywać dane osobowe nawet w zeskanowanych PDF-ach, zapewniając usunięcie wszelkich wrażliwych ciągów przed udostępnieniem lub archiwizacją dokumentu.

## Dlaczego używać GroupDocs Redaction z Azure OCR?
Powinieneś używać GroupDocs Redaction z Azure OCR, ponieważ zapewnia **>98 % dokładności OCR w przypadku tekstu drukowanego**, obsługuje **ponad 50 formatów wejściowych i wyjściowych** oraz może przetwarzać **PDF-y wielokrotnie setstronicowe bez ładowania całego pliku do pamięci**, zapewniając szybką, skalowalną redakcję dla zgodności. Rozwiązanie także **skaluje się, aby przetworzyć 1 000‑stronicowy PDF w mniej niż 2 minuty na serwerze 8‑rdzeniowym**, co czyni zadania wsadowe praktycznymi.

## Wymagania wstępne
- **Java Development Kit (JDK) 8+** zainstalowany.  
- **Maven** (jeśli wolisz zarządzanie zależnościami) lub możliwość ręcznego pobrania plików JAR.  
- **Microsoft Azure OCR credentials** (endpoint i klucz subskrypcji).  
- Podstawowa znajomość Javy oraz wyrażeń regularnych.

## Konfiguracja GroupDocs Redaction dla Javy

### Konfiguracja Maven
Dodaj repozytorium GroupDocs i zależność do swojego `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Bezpośrednie pobranie
Jeśli wolisz ręczne zarządzanie plikami JAR, pobierz najnowszą wersję z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Uzyskiwanie licencji
- **Free Trial** – przetestuj wszystkie funkcje bez kosztów.  
- **Temporary License** – wydłuż czas oceny.  
- **Full License** – odblokuj możliwości gotowe do produkcji.

### Podstawowa inicjalizacja i konfiguracja
Klasa `Redactor` jest głównym silnikiem, który wykonuje wyodrębnianie OCR i stosuje reguły redakcji do dokumentów PDF.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Jak maskować wrażliwe dane przy użyciu OCR Redaction
Maskowanie wrażliwych danych przy użyciu OCR Redaction polega na załadowaniu PDF z ustawieniami Azure OCR, zdefiniowaniu wzorców regex dla danych, które chcesz ukryć, oraz wywołaniu Redactor, aby zastąpił każde dopasowanie symbolem zastępczym, takim jak `[REDACTED]`. Biblioteka obsługuje OCR, dopasowywanie wzorców i przepisywanie PDF w jednym przepływie pracy.

### Krok 1: Załaduj dokument z ustawieniami OCR
`LoadOptions` konfiguruje sposób, w jaki GroupDocs ładuje plik, umożliwiając przekazanie konektorów OCR, takich jak Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – zamień na ścieżkę do swojego PDF.  
- **`settings`** – zawiera konektor Azure OCR, który utworzyłeś wcześniej.

### Krok 2: Zdefiniuj i zastosuj redakcje regex
`ReplacementOptions` określa tekst zastępczy, który będzie podmieniał każde dopasowanie regex podczas redakcji.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- Wzorzec `\b\d{3}-\d{2}-\d{4}\b` dopasowuje amerykańskie numery Social Security.  
- `ReplacementOptions("[REDACTED]")` zamienia każde dopasowanie na maskę, skutecznie **maskując wrażliwe dane**.

## Typowe przypadki użycia maskowania wrażliwych danych
1. **Legal Document Management** – ukryj identyfikatory klientów przed udostępnieniem wersji roboczych.  
2. **Financial Reporting** – zabezpiecz numery kont i identyfikatory transakcji.  
3. **Healthcare Records** – spełnij wymogi HIPAA, redagując identyfikatory pacjentów.  
4. **Government Publications** – usuń dane osobowe z dokumentów publicznych.  
5. **Corporate Contracts** – ukryj własnościowe warunki podczas przeglądów zewnętrznych.

## Wskazówki dotyczące wydajności
- **Optimize regex** – unikaj zbyt szerokich wzorców, które zwiększają czas przetwarzania; dobrze skonstruowane wyrażenia mogą skrócić czas działania nawet o 40 %.  
- **Memory Management** – zamykaj instancję `Redactor` niezwłocznie (try‑with‑resources robi to automatycznie).  
- **Asynchronous Execution** – przy przetwarzaniu wsadowym uruchamiaj zadania redakcji w osobnych wątkach lub używaj kolejki zadań, aby interfejs pozostawał responsywny.

## Rozwiązywanie problemów
- **Azure credentials error** – sprawdź ponownie URL punktu końcowego i klucz subskrypcji w `MicrosoftAzureOcrConnector`.  
- **Document not loading** – zweryfikuj ścieżkę pliku i upewnij się, że PDF nie jest chroniony hasłem (lub podaj hasło poprzez `LoadOptions`).  
- **No redactions applied** – najpierw przetestuj swój regex na prostym ciągu; użyj `Pattern.compile` w teście jednostkowym, aby potwierdzić dopasowania.

## Najczęściej zadawane pytania

**Q: Czym jest redakcja OCR?**  
A: Redakcja OCR wykorzystuje rozpoznawanie znaków optycznych (Optical Character Recognition) do wyodrębniania ukrytego tekstu z obrazów lub zeskanowanych PDF‑ów, a następnie stosuje reguły redakcji, aby zamaskować ten tekst.

**Q: Czy mogę używać GroupDocs Redaction bez Azure OCR?**  
A: Tak, ale OCR znacznie zwiększa dokładność w zeskanowanych dokumentach, w których natywne wyodrębnianie tekstu zawodzi.

**Q: Jak radzić sobie ze złożonymi wzorcami regex?**  
A: Twórz i testuj je stopniowo, używając klasy `Pattern` w Javie w środowisku testowym przed zastosowaniem do dużych dokumentów.

**Q: Jakie są typowe wąskie gardła wydajności?**  
A: Duże PDF‑y, nadmiernie złożone regexy oraz synchroniczne wywołania OCR mogą spowalniać przetwarzanie; rozważ przetwarzanie wsadowe i zoptymalizowane wzorce.

**Q: Czy dostępne jest wsparcie w kwestiach implementacji?**  
A: Oczywiście — skontaktuj się poprzez [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) po pomoc społeczności lub skontaktuj się z wsparciem GroupDocs.

## Dodatkowe zasoby
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

**Ostatnia aktualizacja:** 2026-06-26  
**Testowane z:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  

## Powiązane samouczki

- [Secure PDF Redaction using OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)  
- [How to Redact Text with GroupDocs.Redaction for Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)  
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)