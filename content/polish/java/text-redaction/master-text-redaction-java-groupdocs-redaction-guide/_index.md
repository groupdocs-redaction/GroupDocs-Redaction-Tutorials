---
date: '2026-08-20'
description: Odkryj, jak redagować tekst przy użyciu regex w Java z GroupDocs.Redaction.
  Ten krok po kroku poradnik pokazuje, jak zastosować regex, skonfigurować opcje zapisu
  i chronić wrażliwe dane.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Dowiedz się, jak redagować tekst w Java przy użyciu GroupDocs.Redaction.
  Ten przewodnik wyjaśnia redakcję przy użyciu regex, konfigurację opcji zapisu oraz
  wskazówki dotyczące wydajności w ochronie wrażliwych danych.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Jak redagować tekst w Java z GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Jak redagować tekst w Java przy użyciu GroupDocs.Redaction: Kompletny przewodnik'
type: docs
url: /pl/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Jak redagować tekst w Javie przy użyciu GroupDocs.Redaction: Kompletny przewodnik

W dzisiejszym szybko zmieniającym się świecie cyfrowym, **jak redagować tekst** w dokumentach jest pytaniem, z którym spotyka się wielu programistów. Niezależnie od tego, czy chronisz dane osobowe, spełniasz wymogi regulacyjne, czy po prostu porządkujesz wersje robocze, ten przewodnik pokaże Ci, jak używać GroupDocs.Redaction dla Javy do **szybkiego i bezpiecznego stosowania redakcji opartej na wyrażeniach regularnych**. Dowiesz się, dlaczego redakcja jest ważna, jak skonfigurować bibliotekę oraz poznasz wskazówki najlepszych praktyk dla wysokowydajnego przetwarzania.

## Szybkie odpowiedzi
- **Jaki jest podstawowy cel GroupDocs.Redaction?** Zapewnia niezawodne API do lokalizowania i maskowania wrażliwego tekstu w ponad 50 formatach dokumentów.  
- **Jak zastosować regex do redakcji?** Utwórz obiekt `RegexRedaction` z własnym wzorcem i przekaż go do metody `Redactor.apply()`.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; płatna licencja odblokowuje pełne funkcje w produkcji.  
- **Czy mogę redagować pliki PDF oraz DOCX?** Tak — GroupDocs.Redaction obsługuje PDF, DOCX, PPTX i wiele innych formatów.  
- **Jaki jest najlepszy sposób na poprawę wydajności?** Szybko zamykaj instancje `Redactor`, utrzymuj wzorce regex proste i przetwarzaj pliki w partiach.

## Czym jest redakcja tekstu i dlaczego jest ważna?
Redakcja tekstu trwale usuwa lub zaciemnia wrażliwe informacje w dokumencie, zapewniając, że poufne dane — takie jak numery ubezpieczenia społecznego, dane kart kredytowych czy rekordy medyczne — nie mogą zostać odzyskane ani wyświetlone przez nieuprawnione osoby. Działa poprzez nadpisanie oryginalnych znaków lub zastąpienie ich maską, tak aby ukryta treść nie mogła być wyodrębniona przy kopiowaniu‑wklejaniu ani przez narzędzia OCR. Zapewnia to zgodność z przepisami o ochronie prywatności i chroni osoby przed kradzieżą tożsamości lub wyciekami danych.

## Dlaczego używać regex do redakcji tekstu?
Wyrażenia regularne pozwalają definiować elastyczne wzorce, które pasują do szerokiego zakresu formatów danych (np. numery telefonów, numery kart kredytowych). Użycie regex z GroupDocs.Redaction daje precyzyjną kontrolę nad tym, co zostaje ukryte, przy jednoczesnym zachowaniu zwięzłości i łatwości utrzymania implementacji.

## Wymagania wstępne
Zanim zaczniemy, upewnij się, że masz:

- **Java Development Kit (JDK)** zainstalowany (Java 8 lub nowsza).  
- Podstawową znajomość składni Javy i wyrażeń regularnych.  
- IDE, takie jak **IntelliJ IDEA** lub **Eclipse**, aby uruchamiać i debugować kod.  

## Konfiguracja GroupDocs.Redaction dla Javy
Najpierw dodaj bibliotekę do swojego projektu.

### Konfiguracja Maven
Jeśli używasz Maven, wstaw poniższy fragment do swojego `pom.xml`:

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
Alternatywnie, pobierz najnowszy plik JAR z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Podstawowa inicjalizacja
`Redactor` jest klasą rdzeniową, która otwiera dokument, stosuje reguły redakcji i zapisuje wynik.

Gdy biblioteka jest dostępna, możesz rozpocząć redagowanie dokumentów:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Jak redagować tekst przy użyciu regex w Javie?
Proces polega na załadowaniu pliku źródłowego do instancji `Redactor`, utworzeniu reguły `RegexRedaction` definiującej wzorzec do dopasowania, zastosowaniu reguły za pomocą `redactor.apply()` oraz zapisaniu zmodyfikowanego dokumentu przy użyciu `SaveOptions`. Postępując zgodnie z tymi krokami, możesz niezawodnie lokalizować i maskować dowolne wrażliwe ciągi w obsługiwanych formatach.

Klasa `Redactor` jest centralnym komponentem, który otwiera dokument, stosuje reguły redakcji i zapisuje plik wyjściowy. Zarządza zasobami wewnętrznie, więc po przetworzeniu musisz ją zamknąć, aby zwolnić pamięć.

### Krok 1: import wymaganych klas
Poniższe importy dają dostęp do API redakcji:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Krok 2: zainicjalizuj redactor i zastosuj wzorzec regex
`RegexRedaction` reprezentuje regułę redakcji opartą na wyrażeniu regularnym. Wzorzec, który podasz, określa, które fragmenty tekstu zostaną zastąpione.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Wyjaśnienie regex**: Wzorzec `\b\d{3}-\d{2}-\d{4}\b` dopasowuje amerykańskie numery Social Security (trzy cyfry, myślnik, dwie cyfry, myślnik, cztery cyfry). `ReplacementOptions` pozwala wybrać jednolitą czarną nakładkę lub własną maskę tekstową.

### Krok 3: skonfiguruj opcje zapisu
`SaveOptions` kontroluje sposób zapisu pliku po redakcji. Dodanie przyrostka ułatwia rozpoznanie, które pliki zostały przetworzone, a zachowanie oryginalnego formatu zapobiega niechcianej konwersji.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Opcje zapisu**: `setAddSuffix(true)` automatycznie dodaje „_redacted” do nazwy pliku wyjściowego, zapobiegając przypadkowym nadpisaniom.

### Krok 4: dostosuj dodatkowe ustawienia zapisu
Możesz dalej dopasować wynik — np. zachowując metadane lub spłaszczając adnotacje — poprzez modyfikację obiektu `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Kluczowa konfiguracja**: Ustawienie `setPreserveMetadata(true)` zachowuje oryginalne właściwości dokumentu, co często jest wymagane podczas audytów zgodności.

## Praktyczne zastosowania
Scenariusze z życia wzięte, w których **jak redagować tekst** jest niezbędne:

1. **Dokumenty prawne** – Ukrywanie identyfikatorów klientów przed udostępnieniem wersji roboczych zewnętrznym prawnikom.  
2. **Rekordy medyczne** – Maskowanie imion pacjentów, ich ID lub numerów ubezpieczenia, aby spełnić wymogi HIPAA.  
3. **Raporty finansowe** – Usuwanie poufnych numerów kont przy dystrybucji kwartalnych podsumowań.  

## Uwagi dotyczące wydajności
- **Zarządzanie pamięcią**: Zawsze wywołuj `redactor.close()`, aby zwolnić uchwyty plików i zasoby natywne.  
- **Efektywny regex**: Prostsze wzorce działają szybciej; unikaj nadmiernego back‑trackingu, stosując grupy atomowe, gdy to możliwe.  
- **Przetwarzanie wsadowe**: Dla dużych zestawów dokumentów przetwarzaj pliki w partiach po 20–50, aby utrzymać przewidywalne zużycie sterty.

## Typowe problemy i rozwiązania
| Problem | Rozwiązanie |
|-------|----------|
| **Regex dopasowuje zbyt wiele** | Przetestuj swój wzorzec w internetowym testerze regex i zawęź klasy znaków. |
| **Konflikt nazw plików wyjściowych** | Użyj `setAddSuffix(true)` lub podaj własną ścieżkę wyjściową za pomocą `saveOptions.setOutputPath()`. |
| **Wycieki pamięci przy dużych PDF** | Przetwarzaj PDF strona po stronie lub zwiększ rozmiar sterty JVM (`-Xmx2g`). |

## Najczęściej zadawane pytania

**Q: Jaki jest cel `setAddSuffix(true)` w SaveOptions?**  
A: Automatycznie dodaje przyrostek (np. `_redacted`) do nazwy pliku wyjściowego, co jasno wskazuje, które pliki zostały przetworzone.

**Q: Czy mogę używać wzorców regex innych niż liczby do redakcji tekstu?**  
A: Oczywiście. Każde prawidłowe wyrażenie regularne Javy może zostać przekazane do `RegexRedaction`, aby celować w e‑maile, numery telefonów, własne identyfikatory itp.

**Q: Jak powinienem obsługiwać błędy podczas redakcji?**  
A: Umieść logikę redakcji w bloku try‑catch, zaloguj wyjątek i zawsze zamykaj `Redactor` w bloku finally, aby zwolnić zasoby.

**Q: Czy redakcja PDF jest obsługiwana?**  
A: Tak. GroupDocs.Redaction działa z PDF, DOCX, PPTX i wieloma innymi formatami.

**Q: Jakie są najlepsze praktyki dla dużych projektów redakcyjnych?**  
A: Stosuj przetwarzanie wsadowe, utrzymuj wzorce regex proste i monitoruj zużycie pamięci przy pomocy narzędzi profilujących.

## Dodatkowe zasoby
- **Dokumentacja**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **Referencja API**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Ostatnia aktualizacja:** 2026-08-20  
**Testowano z:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs

## Powiązane samouczki

- [Maskowanie wrażliwych danych Java – Przewodnik GroupDocs.Redaction](/redaction/java/getting-started/)
- [Maskowanie wrażliwych danych Java – Redagowanie danych osobowych przy użyciu GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Jak redagować PDF przy użyciu Aspose OCR i Javy – Implementacja wzorców regex z GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)