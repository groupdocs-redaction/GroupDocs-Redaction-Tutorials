---
date: '2026-01-21'
description: Dowiedz się, jak redagować pliki PDF przy użyciu OCR oraz redagować zeskanowane
  dokumenty za pomocą GroupDocs.Redaction dla Javy z integracją Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Redagowanie PDF z OCR przy użyciu GroupDocs i Azure OCR – Przewodnik Java
type: docs
url: /pl/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Redagowanie PDF z OCR przy użyciu GroupDocs i Azure OCR – Przewodnik Java

W tym obszernej tutorialu dowiesz się, jak **redagować PDF z OCR** w Javie, wykorzystując GroupDocs.Redaction wraz z Microsoft Azure OCR. Niezależnie od tego, czy pracujesz z natywnymi plakcja OCR?**ów/PDF‑ów i automatycznie stosuje reguły redakcji.  
- **Która biblioteka zapewnia silnik redakcji?** GroupDocs.Redaction dla Java.  
- **Jakiego serwisu OCR użyto?** Microsoft Azure OCR connector.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do testów; do produkcji wymagana jest stała licencja.  
- **Czy mogę redagować zarówno natywne, jak i zeskanowane PDF‑y?** Tak – OCR umożliwia redakcję także dokumentów zeskanowanych.

## Co to jest „redagowanie PDF z OCR”?
Redagowanie PDF z OCR oznacza użycie rozpoznawania znaków optycznych (OCR) do przekształcenia widocznego tekstu w przeszukiwalne ciągi znaków, a następnie zastosowanie wzorców redakcji (np. wyrażeń regularnych), aby ukryć te informacje przed udostępnieniem lub zapisaniem pliku.

## Dlaczego warto używać GroupDocs.Redaction z Azure OCR?
- **Wysoka dokładność** na zeskanowanych stronach dzięki chmurowemu silnikowi OCR Azure.  
- **Proste API Java**, które integruje się bezpośrednio z istniejącym przepływem pracy.  
- **Elastyczne reguły redakcji** – wyrażenia regularne, słowa kluczowe lub własna logika.  
- **Gotowy do zgodności** wynik, który trwale usuwa wrażliwe dane.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub nowszy.  
- Maven (lub możliwość ręcznego pobrania pliku JAR).  
- Konto Microsoft Azure z danymi uwierzytelniającymi OCR.  
- Podstawowa znajomość Javy oraz wyrażeń regularnych.

## Konfiguracja GroupDocs.Redaction dla Java

### Konfiguracja Maven
Dodaj repozytorium GroupDocs i zależność do pliku `pom.xml`:

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
Jeśli nie chcesz używać Maven, pobierz najnowszy plik JAR ze strony wydania: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Uzyskanie licencji
- **Darmowa wersja próbna** – przetestuj podstawowe funkcje bez zobowiązań.  
- **Licencja tymczasowa** – wydłuż okres próbny dla większych projektów.  
- **Pełna licencja** – odblokuj nieograniczone użycie i wsparcie premium.

### Podstawowa inicjalizacja i konfiguracja
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Jak redagować PDF z OCR w Javie

### Krok 1: Załaduj dokument z ustawieniami OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parametry**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – ścieżka do docelowego PDF‑a.  
  - `new LoadOptions()` – domyślna konfiguracja ładowania.  
  - `settings` – zawiera łącznik Azure OCR.

### Krok 2: Zastosuj redakcję przy użyciu wyrażeń regularnych (np. numery ubezpieczenia społecznego)
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
- **Wyjaśnienie regex** – `\b\d{3}-\d{2}-\d{4}\b` dopasowuje wzorce takie jak `123-45-6789`.  
- **ReplacementOptions** – zastępuje wykryty tekst ciągiem `[REDACTED]`.

### Typowe pułapki i rozwiązywanie problemów
- **Poświadczenia Azure** – sprawdź dwukrotnie klucz subskrypcji i punkt końcowy.  
- **Ścieżka pliku** – upewnij się, że PDF istnieje i aplikacja ma uprawnienia odczytu/zapisu.  
- **Wydajność** – duże PDF‑y mogą wymagać zwiększenia rozmiaru sterty lub przetwarzania asynchronicznego.

## Praktyczne zastosowania redagowania zeskanowanych dokumentów
1. **Kancelarie prawne** – ukrywanie identyfikatorów klientów przed udostępnieniem akt spraw.  
2. **Instytucje finansowe** – maskowanie numerów kont w zeskanowanych wyciągach.  
3. **Placówki opieki zdrowotnej** – ochrona danych PHI pacjentów w zeskanowanych rekordach medycznych.  
4. **Agencje rządowe** – usuwanie danych osobowych z publicznie dostępnych PDF‑ów.  
5. **Przedsiębior przed audytami podmiotów trzecich.

## Wskazówki dotyczące wydajności
- Utrzymuj wzorce regex tak specyficzne, jak to możliwe, aby skrócić czas przetwarzania.  
- Szybko zwalniaj instancję `Redakcja OCR?**  
O: Redakcja OCR wykorzystuje rozpoznawnie stosuje reguły redakcji, aby trwale usunąć ten tekst.

**P: Czy mogę używać GroupDocs.Redaction bez Azure OCR?**  
O: Tak, ale OCR znacząco zwiększa dokładność przy dokumentach zeskanowanych, umożliwiając skuteczne **redagowanie zeskanowanych dokumentów**.

**P: Jak radzić sobie ze skomplikowanymi wyrażeniami regularnymi?**  
O: Testuj wzorce na danych przykładowych, używaj granic słów (`\b`), aby uniknąć częściowych dopasowań, i rozważ podzielenie dużych wyrażeń na kilka prostszych redakcji.

**P: Jakie są typowe wąskie gardła wydajności?**  
O: Ciężkie wywołania OCR na dużych plikach, zbyt szerokie regexy oraz niewystarczające przydzielenie pamięci. Optymalizuj regex i skaluj zasoby.

**P: Gdzie mogę uzyskać pomoc w razie problemów?**  
O: Zadaj pytanie na forum społeczności GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Dodatkowe zasoby
- **Dokumentacja**: https://docs.groupdocs.com/redaction/java/
- **Referencja API**: https://reference.groupdocs.com/redaction/java
- **Pobieranie**: https://releases.groupdocs.com/redaction/java/
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
- **Bezpłatne wsparcie**: https://forum.groupdocs.com/c/redaction/33
- **Licencja tymczasowa**: https://purchase.groupdocs.com/temporary-license/

---

**Ostatnia aktualizacja:** 2026-01-21  
**Testowano z:** GroupDocs.Redaction 24.9 dla Java  
**Autor:** GroupDocs