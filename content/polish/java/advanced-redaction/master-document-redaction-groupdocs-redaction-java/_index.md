---
date: '2025-12-17'
description: Dowiedz się, jak dodać sufiks do nazwy pliku i usunąć wrażliwe informacje
  z dokumentów przy użyciu GroupDocs.Redaction dla Javy. Skutecznie zwiększ bezpieczeństwo
  i prywatność dokumentów.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Jak dodać przyrostek do nazwy pliku podczas redagowania dokumentów w Javie
  z użyciem GroupDocs.Redaction
type: docs
url: /pl/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Jak dodać przyrostek do nazwy pliku podczas redagowania dokumentów w Javie przy użyciu GroupDocs.Redaction

Redagowanie poufnych danych to dopiero połowa walki — musisz także upewnić się, że zapisany plik wyraźnie wskazuje, że został przetworzony. W tym przewodniku dowiesz się **jak dodać przyrostek do nazwy pliku** podczas zapisywania zredagowanego dokumentu, a także jak ładować, anotować i zapisywać przy użyciu GroupDocs.Redaction dla Javy. Niezależnie od tego, czy chronisz umowy prawne, rekordy medyczne czy raporty finansowe, te kroki zapewnią, że Twój przepływ pracy będzie zarówno bezpieczny, jak i audytowalny.

## Szybkie odpowiedzi
- **Co robi „add suffix to filename”?**  
  Dodaje niestandardowy przyrostek (np. “_redacted”) do nazwy pliku wyjściowego, abyś mógł od razu zidentyfikować przetworzone pliki.
- **Czy mogę wczytać dokument ze strumienia?**  
  Tak — GroupDocs.Redaction obsługuje ładowanie z dowolnego `InputStream`, co jest idealne dla przechowywania w chmurze lub przetwarzania w pamięci.
- **Czy potrzebuję licencji na tę funkcję?**  
  Darmowa wersja próbna działa dla podstawowego redagowania; tymczasowa lub pełna licencja odblokowuje wszystkie zaawansowane opcje, w tym obsługę przyrostka.
- **Jakie formaty są obsługiwane?**  
  Biblioteka obsługuje DOCX, PDF, PPTX, XLSX i wiele innych.
- **Czy rasteryzacja jest wymagana przy wyjściu PDF?**  
  Rasteryzacja jest opcjonalna; włącz ją, gdy potrzebujesz spłaszczyć dokument dla dodatkowego bezpieczeństwa.

## Co to jest dodawanie przyrostka do nazwy pliku?
Dodanie przyrostka to prosta konwencja nazewnictwa, która sygnalizuje, że plik został poddany redagowaniu. Zapobiega przypadkowemu udostępnianiu oryginalnych, niezredagowanych wersji i pomaga zautomatyzowanym potokom śledzić status przetwarzania.

## Dlaczego używać GroupDocs.Redaction do tego zadania?
GroupDocs.Redaction udostępnia płynne API Java, które pozwala łączyć akcje redagowania z opcjami obsługi plików — takimi jak **dodawanie przyrostka do nazwy pliku** — w zaledwie kilku linijkach kodu. To oszczędza czas programisty i zmniejsza ryzyko błędów ręcznych.

## Prerequisites
- **Java Development Kit (JDK):** wersja 8 lub wyższa.
- **GroupDocs.Redaction Library:** podstawowa biblioteka do zadań redagowania.
- **IDE:** IntelliJ IDEA, Eclipse lub dowolny edytor kompatybilny z Javą.
- **Maven:** do zarządzania zależnościami.

### Wymagania wstępne wiedzy
Znajomość Java I/O oraz podstawowych koncepcji obiektowych ułatwi zrozumienie przykładów.

## Konfiguracja GroupDocs.Redaction dla Javy
### Maven Setup
Umieść następującą konfigurację w pliku `pom.xml`, aby uzyskać dostęp do bibliotek GroupDocs za pośrednictwem Maven:

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
Alternatywnie, pobierz najnowszą wersję bezpośrednio z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
1. **Free Trial:** Dostęp do podstawowej funkcjonalności bez ograniczeń.  
2. **Temporary License:** Uzyskaj tymczasową licencję, aby wypróbować zaawansowane funkcje.  
3. **Purchase:** W przypadku długoterminowego użycia rozważ zakup pełnej licencji.

#### Basic Initialization and Setup
Zainicjalizuj projekt, dodając niezbędne importy:

```java
import com.groupdocs.redaction.Redactor;
```

Po tej konfiguracji jesteś gotowy do implementacji funkcji redagowania dokumentów.

## Implementation Guide

### Funkcja 1: Ładowanie dokumentu ze strumienia
**Przegląd:** Dowiedz się, jak ładować dokumenty do `InputStream` w celu przetwarzania.

#### Step-by-Step Implementation
##### Step 1.1: Create InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Dlaczego:** Użycie `InputStream` pozwala na płynne obsługiwanie dokumentów przechowywanych w różnych formatach, co jest niezbędne, gdy musisz **load document from stream** w scenariuszach chmurowych lub mikro‑serwisowych.

### Funkcja 2: Zastosowanie redagowania usuwania adnotacji
**Przegląd:** Usuń adnotacje z dokumentu przy użyciu `DeleteAnnotationRedaction`.

#### Step-by-Step Implementation
##### Step 2.1: Apply DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Dlaczego:** Ten krok zapewnia usunięcie wszelkich wrażliwych adnotacji, zwiększając prywatność dokumentu.

### Funkcja 3: Zapis dokumentu z opcjami
**Przegląd:** Dowiedz się, jak zapisać przetworzony dokument z określonymi opcjami, takimi jak rasteryzacja i **dodawanie przyrostka do nazwy pliku**.

#### Step-by-Step Implementation
##### Step 3.1: Configure SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Dlaczego:** Dostosowanie opcji zapisu umożliwia elastyczne formaty wyjściowe i konwencje nazewnictwa. Włączenie `setAddSuffix(true)` **adds suffix to filename**, co jasno wskazuje, że plik został zredagowany.

## Dlaczego dodawanie przyrostka ma znaczenie
- **Auditability:** Zespoły mogą od razu zauważyć, które pliki są bezpieczne do dystrybucji.
- **Automation:** Skrypty mogą filtrować pliki po przyrostku, zapobiegając przypadkowemu przetwarzaniu oryginalnych dokumentów.
- **Compliance:** Wiele regulacji wymaga wyraźnego oznaczenia oczyszczonych dokumentów.

## Praktyczne zastosowania
1. **Legal Document Redaction:** Zabezpiecz umowy przed udostępnieniem klientowi.  
2. **Medical Record Handling:** Chroń identyfikatory pacjentów.  
3. **Financial Reporting:** Zachowaj poufność wrażliwych liczb.  
4. **CRM Integration:** Automatycznie redaguj dane klientów przed eksportem.  
5. **Collaboration Tools:** Zapewnij, że udostępnione wersje robocze nie ujawniają ukrytych komentarzy.

## Rozważania dotyczące wydajności
### Optimizing Performance
- Używaj strumieniowania (`load document from stream`), aby uniknąć ładowania całych plików do pamięci.  
- Szybko zamykaj instancje `Redactor`, aby zwolnić zasoby.

### Resource Usage Guidelines
- Monitoruj CPU i pamięć podczas uruchamiania wsadowego.  
- Preferuj `ByteArrayOutputStream` przy zapisywaniu w pamięci przy pracy z umiarkowanymi rozmiarami plików.

### Best Practices for Java Memory Management
- Ponownie używaj obiektów `Redactor` przy przetwarzaniu wielu plików tego samego typu.  
- Wywołuj `close()` w bloku `finally` lub używaj try‑with‑resources, aby zapobiec wyciekom.

## Common Issues and Solutions
| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| **Suffix nie pojawia się** | `setAddSuffix(false)` lub brak wywołania | Upewnij się, że `options.setAddSuffix(true)` jest ustawione przed wywołaniem `save()`. |
| **OutOfMemoryError przy dużym DOCX** | Ładowanie całego pliku do pamięci | Przejdź na ładowanie przy użyciu `InputStream` (zobacz Funkcję 1). |
| **Adnotacje nadal widoczne** | Redagowanie nie zostało zastosowane przed zapisem | Wywołaj `redactor.apply(new DeleteAnnotationRedaction())` przed `save()`. |
| **Rasteryzacja PDF nie zastosowana** | `setRasterizeToPDF(false)` lub pominięte | Ustaw `options.setRasterizeToPDF(true)`, gdy potrzebny jest spłaszczony PDF. |

## Najczęściej zadawane pytania

**Q: Czy mogę redagować dokumenty PDF przy użyciu GroupDocs.Redaction?**  
A: Tak, biblioteka obsługuje PDF, DOCX, PPTX, XLSX i wiele innych formatów.

**Q: Jaki jest najlepszy sposób obsługi dużych plików przy użyciu GroupDocs.Redaction?**  
A: Używaj strumieniowania (`load document from stream`) i szybko zamykaj zasoby, aby utrzymać niskie zużycie pamięci.

**Q: Czy można dostosować tekst przyrostka?**  
A: API automatycznie dodaje domyślny przyrostek (np. “_redacted”). Aby użyć własnego przyrostka, możesz zmienić nazwę pliku wyjściowego po zapisaniu.

**Q: Jak uzyskać tymczasową licencję dla GroupDocs.Redaction?**  
A: Odwiedź [Temporary License page](https://purchase.groupdocs.com/temporary-license/) i postępuj zgodnie z instrukcjami.

**Q: Gdzie mogę uzyskać pomoc w razie problemów?**  
A: Dołącz do [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33), aby uzyskać pomoc ekspertów.

## Resources
- **Documentation:** Przeglądaj szczegółowe przewodniki na [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Uzyskaj dostęp do szczegółowych informacji API na [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Pobierz najnowszą wersję z [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Współpracuj lub przeglądaj kod źródłowy na [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Ostatnia aktualizacja:** 2025-12-17  
**Testowane z:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

---