---
date: '2026-02-08'
description: Dowiedz się, jak maskować wrażliwe dane i cenzurować pliki PDF Java przy
  użyciu GroupDocs OCR Redaction z Microsoft Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Maskuj wrażliwe dane w PDF przy użyciu redakcji OCR GroupDocs
type: docs
url: /pl/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Maskowanie wrażliwych danych w PDF przy użyciu GroupDocs OCR Redaction

W dzisiejszym cyfrowym krajobrazie ochrona danych osobowych i poufnych informacji jest priorytetem. W tym samouczku **dowiesz się, jak maskować wrażliwe dane** w plikach PDF, łącząc GroupDocs Redaction z Microsoft Azure OCR. To podejście zapewnia niezawodne rozpoznawanie tekstu na zeskanowanych stronach i pozwala **redagować dokumenty PDF w Javie** z precyzją, zapewniając zgodność z przepisami o ochronie prywatności.

## Szybkie odpowiedzi
- **Co oznacza „maskowanie wrażliwych danych”?** Zastępuje zidentyfikowany poufny tekst symbolem zastępczym (np. `[REDACTED]`).  
- **Która biblioteka obsługuje OCR?** Microsoft Azure OCR connector, używany przez GroupDocs Redaction.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna wystarczy do oceny; stała licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę redagować zeskanowane PDF‑y?** Tak — OCR wyodrębnia ukryty tekst przed zastosowaniem reguł regex.  
- **Czy to rozwiązanie jest wyłącznie dla Javy?** Przykład jest oparty na Javie, ale GroupDocs udostępnia podobne API dla .NET i innych platform.

## Czym jest redakcja oparta na OCR?
Redakcja oparta na OCR najpierw uruchamia rozpoznawanie optyczne znaków (Optical Character Recognition) na każdej stronie dokumentu, zamieniając obrazy tekstu w przeszukiwalne ciągi znaków. Gdy tekst jest przeszukiwalny, możesz zastosować reguły wyrażeń regularnych (regex), aby zlokalizować wrażliwe informacje — takie jak numery ubezpieczenia społecznego, numery kart kredytowych czy identyfikatory osobiste — i zastąpić je maską, np. **`[REDACTED]`**.

## Dlaczego warto używać GroupDocs Redaction z Azure OCR?
- **Wysoka dokładność** przy przetwarzaniu zeskanowanych PDF‑ów i obrazów.  
- **Bezproblemowa integracja z Javą** poprzez Maven lub bezpośrednie pobranie JAR‑a.  
- **Elastyczny silnik regex** umożliwia definiowanie własnych wzorców dla dowolnego typu danych.  
- **Skalowalność** przy przetwarzaniu dużych partii dokumentów, z opcjami przetwarzania asynchronicznego.

## Wymagania wstępne
- **Java Development Kit (JDK) 8+** zainstalowany.  
- **Maven** (jeśli preferujesz zarządzanie zależnościami) lub możliwość ręcznego pobrania JAR‑ów.  
- **Poświadczenia Microsoft Azure OCR** (adres endpointu i klucz subskrypcji).  
- Podstawowa znajomość Javy oraz wyrażeń regularnych.

## Konfiguracja GroupDocs Redaction dla Javy

### Konfiguracja Maven
Dodaj repozytorium GroupDocs oraz zależność do pliku `pom.xml`:

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

### Pobieranie bezpośrednie
Jeśli wolisz ręczne zarządzanie JAR‑ami, pobierz najnowsze wydanie z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Uzyskanie licencji
- **Free Trial** – przetestuj wszystkie funkcje bez kosztów.  
- **Temporary License** – wydłuż czas oceny.  
- **Full License** – odblokuj możliwości gotowe do produkcji.

### Podstawowa inicjalizacja i konfiguracja
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Jak maskować wrażliwe dane przy użyciu OCR Redaction

### Krok 1: Załaduj dokument z ustawieniami OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – zamień na ścieżkę do swojego pliku PDF.  
- **`LoadOptions`** – domyślne ładowanie; możesz dostosować w razie potrzeby.  
- **`settings`** – zawiera connector Azure OCR utworzony wcześniej.

### Krok 2: Zdefiniuj i zastosuj redakcje regex
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
1. **Zarządzanie dokumentami prawnymi** – ukrywanie identyfikatorów klientów przed udostępnieniem wersji roboczych.  
2. **Raportowanie finansowe** – ochrona numerów kont i identyfikatorów transakcji.  
3. **Rekordy medyczne** – spełnianie wymogów HIPAA poprzez redakcję danych pacjentów.  
4. **Publikacje rządowe** – usuwanie danych osobowych z dokumentów publicznych.  
5. **Umowy korporacyjne** – ukrywanie poufnych warunków podczas przeglądów zewnętrznych.

## Wskazówki dotyczące wydajności
- **Optymalizuj regex** – unikaj zbyt ogólnych wzorców, które wydłużają czas przetwarzania.  
- **Zarządzanie pamięcią** – zamykaj instancję `Redactor` niezwłocznie (try‑with‑resources robi to automatycznie).  
- **Wykonanie asynchroniczne** – przy przetwarzaniu wsadowym uruchamiaj zadania redakcji w osobnych wątkach lub używaj kolejki zadań.  

## Rozwiązywanie problemów
- **Błąd poświadczeń Azure** – sprawdź dokładnie adres endpointu i klucz subskrypcji w `MicrosoftAzureOcrConnector`.  
- **Problem z ładowaniem dokumentu** – zweryfikuj ścieżkę pliku i upewnij się, że PDF nie jest zabezpieczony hasłem (lub podaj hasło w `LoadOptions`).  
- **Brak zastosowanych redakcji** – najpierw przetestuj wyrażenie regularne na prostym ciągu; użyj `Pattern.compile` w teście jednostkowym, aby potwierdzić dopasowania.

## Najczęściej zadawane pytania

**Q: Czym jest redakcja OCR?**  
A: Redakcja OCR wykorzystuje rozpoznawanie optyczne znaków do wyodrębnienia ukrytego tekstu z obrazów lub zeskanowanych PDF‑ów, a następnie stosuje reguły redakcji, aby zamaskować ten tekst.

**Q: Czy mogę używać GroupDocs Redaction bez Azure OCR?**  
A: Tak, ale OCR znacząco zwiększa dokładność przy dokumentach skanowanych, gdzie natywne wyodrębnianie tekstu zawodzi.

**Q: Jak radzić sobie ze złożonymi wzorcami regex?**  
A: Buduj i testuj je stopniowo, używając klasy `Pattern` w Javie w środowisku testowym przed zastosowaniem ich do dużych dokumentów.

**Q: Jakie są typowe wąskie gardła wydajności?**  
A: Duże pliki PDF, nadmiernie skomplikowane wyrażenia regularne oraz synchroniczne wywołania OCR mogą spowalniać przetwarzanie; rozważ przetwarzanie wsadowe i zoptymalizowane wzorce.

**Q: Czy dostępne jest wsparcie przy problemach implementacyjnych?**  
A: Oczywiście — skontaktuj się poprzez [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) po pomoc społeczności lub bezpośrednio z zespołem wsparcia GroupDocs.

## Dodatkowe zasoby
- **Dokumentacja**: https://docs.groupdocs.com/redaction/java/  
- **Referencja API**: https://reference.groupdocs.com/redaction/java  
- **Pobieranie**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Bezpłatne wsparcie**: https://forum.groupdocs.com/c/redaction/33  
- **Licencja tymczasowa**: https://purchase.groupdocs.com/temporary-license/

---

**Ostatnia aktualizacja:** 2026-02-08  
**Testowano z:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs