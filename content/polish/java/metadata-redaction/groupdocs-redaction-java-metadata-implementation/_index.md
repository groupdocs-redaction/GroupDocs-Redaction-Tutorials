---
date: '2026-10-01'
description: Dowiedz się, jak usunąć author metadata i zapisać redacted document files
  w Java przy użyciu GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Dowiedz się, jak usunąć author metadata i zapisać redacted document
  files w Java przy użyciu GroupDocs Redaction. Postępuj zgodnie z przewodnikiem krok
  po kroku.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Jak usunąć author metadata w Java z GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Jak usunąć author metadata w Java z GroupDocs
type: docs
url: /pl/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Jak usunąć metadane autora w Javie przy użyciu GroupDocs

W dzisiejszym cyfrowym krajobrazie ochrona wrażliwych informacji ukrytych w dokumentach jest niezbędną praktyką. **Usuwanie metadanych autora** zapobiega przypadkowemu ujawnieniu danych osobowych lub firmowych. Ten samouczek pokazuje krok po kroku, jak używać `EraseMetadataRedaction` z GroupDocs.Redaction dla Javy, aby usunąć pola takie jak *Author* i *Manager* z plików Word, a następnie **zapisz bezpiecznie zredagowane kopie dokumentów** do udostępniania lub archiwizacji.

## Szybkie odpowiedzi
- **Co robi EraseMetadataRedaction?** Usuwa wybrane pola metadanych z dokumentu.  
- **Która biblioteka zapewnia tę funkcję?** GroupDocs.Redaction for Java.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa do testów; stała licencja jest wymagana w środowisku produkcyjnym.  
- **Czy mogę celować w wiele pól jednocześnie?** Tak, połącz filtry operatorem logicznym OR.  
- **Czy proces jest bezpieczny wątkowo?** Instancje Redactor nie są współdzielone między wątkami; utwórz nową instancję dla każdej operacji.

## Co to jest EraseMetadataRedaction?
`EraseMetadataRedaction` to wbudowana klasa redakcji, która pozwala określić, które wpisy metadanych mają zostać usunięte. Działa na szerokim zakresie formatów dokumentów obsługiwanych przez GroupDocs.Redaction, zapewniając, że ukryte informacje o autorze nigdy nie wyciekną. Możesz celować w standardowe właściwości, takie jak Author, Manager, a także własne pola metadanych, zapewniając kompleksową ochronę prywatności.

## Dlaczego używać EraseMetadataRedaction z GroupDocs?
GroupDocs.Redaction obsługuje **ponad 100 formatów wejściowych i wyjściowych** i może przetwarzać dokumenty do 500 stron bez ładowania całego pliku do pamięci. Korzystanie z tej klasy zapewnia jedyne, wysokowydajne API spełniające wymagania GDPR, HIPAA lub wewnętrzne wymogi zgodności, jednocześnie utrzymując prostotę kodu.

## Wymagania wstępne
- Zainstalowana Java 8 lub nowsza.  
- Maven (lub możliwość ręcznego dodania plików JAR).  
- GroupDocs.Redaction for Java (wersja 24.9 lub nowsza).  
- Ważna wersja próbna lub stała licencja GroupDocs.

## Konfiguracja GroupDocs.Redaction dla Javy

### Instalacja Maven
Dodaj repozytorium GroupDocs i zależność do swojego **pom.xml**:

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
Alternatywnie, pobierz najnowszy JAR z [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Uzyskanie licencji
Uzyskaj darmową wersję próbną lub zakup tymczasową licencję w portalu GroupDocs. Plik licencji powinien znajdować się w miejscu, które aplikacja może załadować (np. w katalogu root classpath).

### Podstawowa inicjalizacja i konfiguracja
Poniżej znajduje się minimalny przykład tworzący instancję `Redactor` dla pliku DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Jak używać EraseMetadataRedaction w Javie
Poniższe sekcje rozkładają implementację na jasne, praktyczne kroki.

### Funkcja: czyszczenie konkretnych elementów metadanych

#### Przegląd
Usuniemy pola metadanych **Author** i **Manager** przy użyciu `EraseMetadataRedaction`. Jest to częsty wymóg przy udostępnianiu wewnętrznych raportów partnerom zewnętrznym.

#### Implementacja krok po kroku

##### 1️⃣ Inicjalizacja obiektu Redactor
`Redactor` to podstawowa klasa, która ładuje dokument, stosuje obiekty redakcji i zapisuje wynik. Utwórz nową instancję dla każdego przetwarzanego pliku:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Zastosowanie EraseMetadataRedaction
`MetadataFilters` udostępnia predefiniowane filtry dla typowych kluczy metadanych, takich jak Author i Manager.  
`EraseMetadataRedaction` usuwa wpisy metadanych pasujące do podanych `MetadataFilters`. Operator bitowy OR (`|`) łączy filtry `Author` i `Manager`, więc oba pola są usuwane w jednym wywołaniu:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Konfiguracja opcji zapisu
`SaveOptions` pozwala określić nazwę pliku wyjściowego, format oraz inne parametry zapisu.  
`SaveOptions` umożliwia kontrolowanie nazwy pliku wyjściowego, formatu oraz tego, czy dokument ma być rasteryzowany do PDF. Dodanie przyrostka zachowuje oryginalny plik niezmieniony:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Typowe przypadki użycia
1. **Dokumenty prawne** – Zredaguj informacje o autorze przed wysłaniem umów do przeciwnej strony.  
2. **Raporty korporacyjne** – Usuń nazwiska menedżerów przy publikacji wyników kwartalnych dla akcjonariuszy.  
3. **Pliki projektowe** – Oczyść wewnętrzną dokumentację projektową przed archiwizacją lub przesłaniem do publicznego repozytorium.

## Porady dotyczące rozwiązywania problemów
- **File not found** – Sprawdź, czy ścieżka w `inputFilePath` wskazuje istniejący plik i czy aplikacja ma uprawnienia do odczytu.  
- **Missing metadata fields** – Nie wszystkie typy dokumentów przechowują te same klucze metadanych; najpierw sprawdź właściwości dokumentu w Office.  
- **License errors** – Upewnij się, że plik licencji został poprawnie załadowany przed utworzeniem instancji `Redactor`.

## Uwagi dotyczące wydajności
- Zamknij obiekt `Redactor` niezwłocznie (jak pokazano w bloku `finally`), aby zwolnić zasoby natywne.  
- Unikaj rasteryzacji dużych dokumentów, chyba że potrzebny jest podgląd PDF; rasteryzacja może zwiększyć zużycie CPU i pamięci nawet 3‑krotnie dla plików o 300 stronach.

## Najczęściej zadawane pytania

**Q1: Czym jest redakcja metadanych?**  
A1: Redakcja metadanych polega na usuwaniu ukrytych właściwości dokumentu (takich jak autor, menedżer lub własne tagi), aby zapobiec przypadkowemu ujawnieniu wrażliwych informacji.

**Q2: Czy mogę używać GroupDocs.Redaction do innych typów plików?**  
A2: Tak, biblioteka obsługuje PDF, DOCX, PPTX, XLSX i wiele innych formatów — ponad 100 łącznie.

**Q3: Jak obsługiwać błędy podczas redakcji?**  
A3: Umieść wywołanie `apply` w bloku try‑catch i zawsze zamykaj `Redactor` w klauzuli finally, aby zapewnić zwolnienie zasobów.

**Q4: Czy można redagować własne pola metadanych?**  
A5: Absolutnie. Użyj `MetadataFilters.Custom("YourFieldName")`, aby celować w dowolną własną właściwość przechowywaną w dokumencie.

**Q5: Jakie są najlepsze praktyki używania GroupDocs.Redaction?**  
A5:  
- Załaduj licencję wcześnie w aplikacji.  
- Zamykaj obiekty `Redactor` niezwłocznie.  
- Użyj `SaveOptions`, aby dodać przyrostek, zachowując oryginalne pliki niezmienione.  
- Testuj redakcję na kopii dokumentu przed przetwarzaniem partii.

**Q6: Czy EraseMetadataRedaction obsługuje operacje wsadowe?**  
A6: Możesz iterować po kolekcji ścieżek plików, tworząc nowy `Redactor` dla każdego pliku i stosując tę samą logikę redakcji.

**Q7: Czy mogę łączyć EraseMetadataRedaction z innymi typami redakcji?**  
A7: Tak, możesz łączyć wiele obiektów redakcji (np. redakcję tekstu, a następnie redakcję metadanych) przed zapisem.

## Zasoby

- **Documentation**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Ostatnia aktualizacja:** 2026-10-01  
**Testowano z:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs

## Powiązane samouczki

- [Groupdocs Redaction Java - Ekstrakcja metadanych dokumentu](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Jak usunąć metadane w Javie przy użyciu GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Pobieranie informacji o dokumencie przy użyciu Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)