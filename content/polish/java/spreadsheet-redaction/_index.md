---
date: 2026-08-04
description: Dowiedz się, jak filtrować dane arkusza kalkulacyjnego w Java i bezpiecznie
  redagować kolumny lub komórki w arkuszach Excel przy użyciu GroupDocs.Redaction
  dla Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Dowiedz się, jak filtrować dane arkusza kalkulacyjnego w Java i bezpiecznie
  redagować kolumny lub komórki w arkuszach Excel przy użyciu GroupDocs.Redaction
  dla Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrowanie danych arkusza kalkulacyjnego w Java – przewodnik z GroupDocs.Redaction
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
title: Filtrowanie danych arkusza kalkulacyjnego w Java – przewodnik z GroupDocs.Redaction
type: docs
url: /pl/java/spreadsheet-redaction/
weight: 12
---

# Filtrowanie danych arkusza kalkulacyjnego java – Samouczek GroupDocs.Redaction Java

Jeśli potrzebujesz **filter spreadsheet data java** przed zastosowaniem redakcji, trafiłeś na właściwy przewodnik. W tym samouczku dowiesz się, jak izolować wiersze, kolumny lub pojedyncze komórki zawierające dane osobowe lub poufne, a następnie bezpiecznie je zredagować przy użyciu GroupDocs.Redaction for Java. Kroki są wyjaśnione prostym językiem, zawierają wskazówki najlepszych praktyk i pokazują, jak utrzymać szybkie przetwarzanie nawet w dużych skoroszytach.

## Szybkie odpowiedzi
- **Która biblioteka obsługuje redakcję arkuszy kalkulacyjnych w Javie?** GroupDocs.Redaction for Java.  
- **Czy mogę filtrować wiersze bez ładowania całego pliku do pamięci?** Yes – the API streams data and lets you apply filters on the fly.  
- **Jakie formaty plików są obsługiwane?** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **Czy potrzebuję licencji do rozwoju?** A temporary license works for testing; a full license is required for production.  
- **Czy istnieje limit rozmiaru skoroszytu?** The engine can process files up to 500 MB without excessive memory consumption.

## Czym jest filter spreadsheet data java?
**Filter spreadsheet data java** to proces programowego wybierania określonych wierszy, kolumn lub komórek w skoroszycie w stylu Excel przy użyciu kodu Java, tak aby tylko wybrana treść była przeglądana lub redagowana. Ta technika skraca czas wykonania, ogranicza niepotrzebne zmiany i pomaga spełnić wymogi zgodności typu GDPR.

## Dlaczego filtrować dane arkusza kalkulacyjnego java?
GroupDocs.Redaction Java obsługuje **30+ formatów arkuszy kalkulacyjnych** i może przetwarzać skoroszyty zawierające **do 500 MB** (około 1 miliona wierszy), utrzymując zużycie pamięci poniżej **200 MB**. Dzięki wstępnemu filtrowaniu unikasz modyfikacji niepowiązanych danych, co średnio skraca czas przetwarzania o **40‑60 %** w typowych scenariuszach usuwania danych prywatnych.

## Wymagania wstępne
- Zainstalowany Java 17 lub nowszy.  
- System budowania Maven lub Gradle.  
- GroupDocs.Redaction for Java (do pobrania z oficjalnej strony).  
- Tymczasowy lub pełny klucz licencyjny.  

## Jak filtrować dane w arkuszach kalkulacyjnych przy użyciu GroupDocs.Redaction Java?
Załaduj skoroszyt, zdefiniuj filtr pasujący do komórek, które chcesz zredagować, a następnie zastosuj operację redakcji. API wykonuje filtrację w trybie strumieniowym, więc nie musisz trzymać całego pliku w pamięci RAM.

Klasa `RedactionFilter` pozwala określić indeksy kolumn, zakresy wierszy lub własne predykaty. Na przykład możesz wybrać każdą komórkę w kolumnie **B**, która zawiera wzorzec adresu e‑mail, lub ograniczyć redakcję do wierszy, w których kolumna „Status” ma wartość „Confidential”.

**Direct answer (40‑70 words):**  
Utwórz instancję `RedactionFilter`, ustaw indeks kolumny oraz warunek wyrażenia regularnego, a następnie przekaż filtr do `Redactor.redact(workbook, filter)`. Ten jednowierszowy filtr izoluje dokładne komórki spełniające kryteria, a redaktor usuwa lub maskuje je, pozostawiając pozostałą część arkusza nietkniętą. Operacja kończy się w czasie liniowym względem przefiltrowanych wierszy.

### Krok 1: utwórz filtr
`RedactionFilter` jest klasą podstawową reprezentującą regułę filtrowania dla redakcji arkuszy kalkulacyjnych. Akceptuje numery kolumn, numery wierszy lub własne wyrażenia lambda, aby precyzyjnie wskazać dane.

### Krok 2: skonfiguruj warunek
Użyj `filter.setColumnIndex(1)`, aby wybrać kolumnę B (indeks zerowy) oraz `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`, aby dopasować wzorce e‑mail. Możesz także łączyć wiele warunków przy użyciu `filter.and(...)` lub `filter.or(...)`.

### Krok 3: zastosuj redakcję
`Redactor` jest główną klasą wykonującą operacje redakcji na skoroszycie.  
Przekaż skoroszyt i skonfigurowany filtr do obiektu `Redactor`. API strumieniuje skoroszyt, stosuje filtr i zapisuje zredagowany wynik do nowego pliku, zachowując oryginalne formatowanie i formuły.

## Typowe problemy i rozwiązania
- **Filtr nie pasuje do żadnych komórek:** Zweryfikuj indeks kolumny (indeks zerowy) i upewnij się, że składnia wyrażenia regularnego jest prawidłowa dla Javy.  
- **Błędy braku pamięci przy dużych plikach:** Zwiększ rozmiar sterty JVM umiarkowanie (np. `-Xmx1g`) lub podziel skoroszyt na mniejsze części przed filtrowaniem.  
- **Zredagowany wynik traci formatowanie:** `RedactionOptions` umożliwia dostosowanie zachowania redakcji, np. zachowanie formatowania komórek. Użyj `RedactionOptions.setPreserveFormatting(true)`, aby utrzymać style komórek.

## Dlaczego filtrować dane arkusza kalkulacyjnego?
Filtrowanie przed redakcją izoluje jedynie wrażliwe fragmenty skoroszytu, co oznacza, że unikasz niepotrzebnych zmian w czystych danych. Takie selektywne podejście zmniejsza ryzyko przypadkowej utraty danych i przyspiesza audyty zgodności, ponieważ dziennik audytu zawiera znacznie mniej wpisów.

## Jak zredagować e‑maile w arkuszach Excel przy użyciu GroupDocs.Redaction Java API
Załaduj plik Excel, zastosuj filtr wyszukujący typowy wzorzec e‑mail i wywołaj redaktor. API zastępuje każdy dopasowany e‑mail symbolem zastępczym, np. “***@***.com”, zachowując otaczający układ komórek.

## Jak filtrować dane – dostępne samouczki
- [Jak zredagować e‑maile w arkuszach Excel przy użyciu GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Dodatkowe zasoby

- [Dokumentacja GroupDocs.Redaction for Java](https://docs.groupdocs.com/redaction/java/)
- [Referencja API GroupDocs.Redaction for Java](https://reference.groupdocs.com/redaction/java/)
- [Pobierz GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [Forum GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Bezpłatne wsparcie](https://forum.groupdocs.com/)
- [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-08-04  
**Testowano z:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## Najczęściej zadawane pytania

**Q: Czy mogę filtrować wiele kolumn jednocześnie?**  
A: Tak, możesz dodać dodatkowe indeksy kolumn do tej samej instancji `RedactionFilter` lub łączyć wiele filtrów przy użyciu `filter.or(...)`.

**Q: Czy filtr działa na skoroszytach zabezpieczonych hasłem?**  
A: Podaj hasło przy otwieraniu skoroszytu; filtr działa po odszyfrowaniu tak samo jak w przypadku pliku niechronionego.

**Q: Ile wierszy może obsłużyć API w jednej operacji?**  
A: Silnik jest zoptymalizowany pod kątem obsługi do 1 miliona wierszy (≈500 MB) bez ładowania całego pliku do pamięci.

**Q: Czy można podglądnąć, które komórki zostaną zredagowane przed zapisaniem?**  
A: Tak, wywołaj `filter.preview(workbook)`, aby uzyskać listę adresów komórek spełniających kryteria.

**Q: Jaki model licencjonowania jest wymagany do użytku produkcyjnego?**  
A: Wymagana jest pełna licencja komercyjna do wdrożeń produkcyjnych; licencja tymczasowa wystarczy do testów i oceny.

## Powiązane samouczki

- [Jak zredagować wrażliwe dane w arkuszach Excel przy użyciu GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Maskowanie wrażliwych danych Java – przewodnik GroupDocs.Redaction](/redaction/java/getting-started/)
- [Maskowanie wrażliwych danych Java – Redagowanie danych osobowych przy użyciu GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)