---
date: '2026-01-24'
description: Dowiedz się, jak redagować pliki PDF za pomocą GroupDocs.Redaction dla
  Javy, wybierając konkretne obszary na ostatniej stronie, aby zapewnić prywatność
  i zgodność.
keywords:
- Java PDF Redaction
- GroupDocs.Redaction
- PDF Area Redaction
title: 'Jak redagować PDF w Javie i GroupDocs.Redaction: celowanie w ostatnią stronę
  i konkretne obszary'
type: docs
url: /pl/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# Jak redagować PDF w Javie i GroupDocs.Redaction: Celowanie w ostatnią stronę i określone obszary

W tym samouczku dowiesz się **jak redagować PDF** przy użyciu biblioteki GroupDocs.Redaction dla Javy, koncentrując się na ostatniej stronie i precyzyjnych prostokątnych obszarach. Niezależnie od tego, czy chronisz poufne dane w umowach prawnych, czy oczyszczasz raporty przed dystrybucją, poniższe kroki zapewnią Ci jasną, praktyczną ścieżkę do uzyskania zgodnych z przepisami redakcji.

## Szybkie odpowiedzi
- **Jakiej biblioteki użyto?** GroupDocs.Redaction for Java.  
- **Czy mogę celować tylko w ostatnią stronę?** Tak, używając `PageRangeFilter` z `PageSeekOrigin.End`.  
- **Jak zdefiniować konkretny obszar?** Za pomocą `PageAreaFilter`, który przyjmuje współrzędne i wymiary.  
- **Czy potrzebna jest licencja?** Licencja próbna lub tymczasowa działa w trybie testowym; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Czy kod jest kompatybilny z Java 17?** Absolutnie – biblioteka obsługuje nowoczesne wersje JDK.

## Co to jest redakcja PDF i dlaczego ma znaczenie?

Redakcja trwale usuwa lub maskuje wrażliwe treści z pliku PDF, zapewniając, że ukryte dane nie mogą zostać odzyskane. W przeciwieństwie do prostego nakładania lub ukrywania, redakcja modyfikuje podstawową strukturę dokumentu, co czyni ją kluczowym narzędziem do spełniania wymogów GDPR, HIPAA i innych regulacji dotyczących prywatności.

## Wymagania wstępne

Zanim przejdziesz dalej, upewnij się, że masz:

1. **Biblioteki i zależności**  
   - Biblioteka GroupDocs.Redaction (24.9 lub nowsza)  
   - Zainstalowany Java Development Kit (JDK)  
   - IDE, takie jak IntelliJ IDEA lub Eclipse  

2. **Konfiguracja środowiska**  
   - Maven skonfigurowany do zarządzania zależnościami  

3. **Podstawowa wiedza**  
   - Znajomość składni Javy i obsługi plików  

## Konfiguracja GroupDocs.Redaction dla Javy

Możesz dodać bibliotekę do swojego projektu za pomocą Maven lub pobierając plik JAR bezpośrednio.

### Maven Setup
Dodaj poniższy fragment do pliku `pom.xml`, aby uwzględnić GroupDocs.Redaction jako zależność:

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

### Direct Download
Alternatywnie pobierz najnowszą wersję z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### Kroki uzyskania licencji
- **Bezpłatna wersja próbna:** Testuj API bez klucza licencyjnego.  
- **Licencja tymczasowa:** Użyj klucza ograniczonego czasowo, aby uzyskać pełny dostęp do funkcji podczas rozwoju.  
- **Zakup:** Uzyskaj stałą licencję do wdrożeń produkcyjnych.

### Basic Initialization
Rozpocznij od utworzenia instancji `Redactor`, wskazującej na PDF, który chcesz przetworzyć:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

## Jak redagować PDF – Implementacja redakcji opartej na obszarze na ostatniej stronie

Poniżej znajduje się krok‑po‑kroku przewodnik, który dokładnie pokazuje **jak redagować PDF** na ostatniej stronie, ograniczając operację do określonego prostokąta.

### Funkcja 1: Redagowanie konkretnych obszarów na stronie PDF

**Przegląd:** Ta funkcja pozwala maskować tekst wyłącznie w wybranym regionie ostatniej strony, pozostawiając resztę dokumentu nietkniętą.

#### Krok 1: Wczytaj dokument PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Krok 2: Pobierz informacje o stronach dokumentu
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### Krok 3: Zdefiniuj opcje zamiany dla redakcji
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```

#### Krok 4: Skonfiguruj filtry określające, które obszary poddać redakcji
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```

#### Krok 5: Zastosuj redakcję
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```

#### Krok 6: Sprawdź, czy redakcja zakończyła się sukcesem i zapisz zmiany
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```

#### Krok 7: Zamknij Redactor, aby zwolnić zasoby
```java
redactor.close();
```

### Funkcja 2: Filtrowanie zakresu stron dla redakcji

**Przegląd:** Użyj tej funkcji, gdy musisz ograniczyć redakcję do konkretnych stron, np. ostatniej strony wielostronicowego kontraktu.

#### Krok 1: Wczytaj dokument PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Krok 2: Pobierz informacje o stronach dokumentu
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### Krok 3: Zdefiniuj filtr zakresu stron, aby celować w wybrane strony
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```

### Funkcja 3: Redakcja oparta na obszarze na stronach PDF

**Przegląd:** To podejście daje precyzyjną kontrolę piksel po pikselu, umożliwiając określenie dokładnego prostokąta, który ma zostać ukryty.

#### Krok 1: Wczytaj dokument PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### Krok 2: Pobierz informacje o stronach dokumentu
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### Krok 3: Zdefiniuj filtr obszaru, aby określić, którą część strony poddać redakcji
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```

#### Krok 4: Zamknij Redactor, aby zwolnić zasoby
```java
redactor.close();
```

## Praktyczne zastosowania

- **Sanitizacja dokumentów prawnych:** Usuń imiona klientów lub numery spraw przed udostępnieniem wersji roboczych.  
- **Raporty finansowe:** Zasłoń numery kont lub dane osobowe w kwartalnych sprawozdaniach.  
- **Rekordy medyczne:** Zapewnij ukrycie PHI przy eksportowaniu PDF‑ów do celów badawczych.  
- **Przegląd przed wydaniem:** Ukryj sekcje wciąż w fazie rozwoju, jednocześnie umożliwiając recenzentom wgląd w pozostałą część dokumentu.

## Wskazówki dotyczące wydajności

- **Ponowne użycie instancji Redactor:** Jeśli przetwarzasz wiele PDF‑ów w partii, utrzymuj jedną obiekt `Redactor` i resetuj go pomiędzy plikami.  
- **Szybkie zwalnianie zasobów:** Zawsze wywołuj `close()`, aby zwolnić zasoby natywne.  
- **Walidacja na próbce:** Przetestuj redakcję na małym pliku testowym, aby potwierdzić poprawność geometrii filtrów przed skalowaniem.

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| Nie utworzono pliku wyjściowego | `result.getStatus()` zwrócił `Failed` | Sprawdź konsolę pod kątem szczegółów wyjątku; upewnij się, że tekst zamiany jest prawidłowy, a filtry poprawnie zdefiniowane. |
| Redakcja obejmuje całą stronę | Nieprawidłowe wymiary `PageAreaFilter` | Zweryfikuj wartości `lastPage.getHeight()` i `lastPage.getWidth()`; odpowiednio dostosuj `Point` i `Dimension`. |
| Błąd licencji | Brakujący lub wygasły klucz licencyjny | Zastosuj wersję próbną lub tymczasową przed przejściem do produkcji. |

## Najczęściej zadawane pytania

**Q: Czy mogę redagować obrazy lub grafikę, a nie tylko tekst?**  
A: Tak. Użyj `ExactImageRedaction` lub połącz filtry tekstu i obrazu, aby ukryć elementy wizualne.

**Q: Czy redakcja przetrwa w przeglądarkach PDF obsługujących edycję?**  
A: Absolutnie. Redakcja trwale usuwa podstawową treść, więc nie może zostać odzyskana przez żaden standardowy edytor PDF.

**Q: Jak redagować PDF‑y zabezpieczone hasłem?**  
A: Wczytaj dokument z hasłem, używając konstruktora `Redactor`, który przyjmuje obiekt `LoadOptions` zawierający hasło.

**Q: Czy można łączyć wiele filtrów (np. zakres stron + obszar)?**  
A: Tak. Przekaż tablicę obiektów `RedactionFilter` do `options.setFilters()` tak, jak pokazano w przykładzie.

**Q: Jakie wersje Javy są obsługiwane?**  
A: GroupDocs.Redaction 24.9 obsługuje Java 8 do Java 21, w tym wydania LTS.

## Podsumowanie

Masz teraz kompletny, gotowy do wdrożenia przewodnik **jak redagować PDF** przy użyciu Javy i GroupDocs.Redaction. Dzięki filtrom zakresu stron i obszaru możesz precyzyjnie usuwać wrażliwe dane, zachowując integralność pozostałej części dokumentu. Eksperymentuj z różnymi filtrami, integruj przepływ pracy z istniejącymi pipeline’ami dokumentów i utrzymuj zgodność z regulacjami ochrony danych.

---

**Ostatnia aktualizacja:** 2026-01-24  
**Testowano z:** GroupDocs.Redaction 24.9  
**Autor:** GroupDocs