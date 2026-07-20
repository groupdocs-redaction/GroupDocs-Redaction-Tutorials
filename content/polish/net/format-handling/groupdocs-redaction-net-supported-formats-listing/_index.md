---
date: '2026-07-20'
description: Dowiedz się, jak wyświetlać formaty przy użyciu GroupDocs.Redaction .NET,
  zintegrować tę funkcję z przepływem pracy dokumentów i poprawić wydajność.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Odkryj, jak wyświetlać formaty przy użyciu GroupDocs.Redaction .NET,
  zobacz przewodnik krok po kroku i uzyskaj wskazówki dotyczące optymalnej wydajności
  w aplikacjach .NET.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Jak wyświetlić formaty w GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: Jak wyświetlić formaty w GroupDocs.Redaction .NET
type: docs
url: /pl/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Jak wyświetlić listę formatów w GroupDocs.Redaction .NET

Zarządzanie szeroką gamą typów dokumentów jest codzienną rzeczywistością dla programistów tworzących aplikacje skoncentrowane na dokumentach. W tym samouczku dowiesz się **jak wyświetlić listę formatów**, które GroupDocs.Redaction .NET może obsłużyć, aby móc weryfikować pliki przed przetwarzaniem, prezentować użytkownikom dokładne opcje i utrzymać efektywność przepływu pracy.

## Wprowadzenie

Efektywne zarządzanie dokumentami zaczyna się od dokładnej znajomości typów plików obsługiwanych przez Twoją bibliotekę. GroupDocs.Redaction udostępnia wbudowaną metodę umożliwiającą pobranie tych informacji, co pozwala tworzyć dynamiczne elementy interfejsu użytkownika, egzekwować reguły walidacji i unikać błędów w czasie wykonywania. Poniżej znajdziesz wszystko, co potrzebne, aby rozpocząć, od instalacji po praktyczne fragmenty kodu i wskazówki dotyczące wydajności.

### Szybkie odpowiedzi
- **Co oznacza „how to list formats”?** Odnosi się do pobierania kolekcji rozszerzeń plików, które GroupDocs.Redaction może przetwarzać.  
- **Czy potrzebuję licencji?** Tak, ważna licencja GroupDocs.Redaction jest wymagana do użytku produkcyjnego.  
- **Które wersje .NET są obsługiwane?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Ile formatów jest dostępnych?** Ponad 30 formatów wejściowych i wyjściowych jest obsługiwanych od razu.  
- **Czy wymagana jest jakaś specjalna konfiguracja?** Nie, nie jest wymagana dodatkowa konfiguracja poza standardową inicjalizacją biblioteki.

## Co to jest „how to list formats”?

Polega na wywołaniu API FileType biblioteki w celu uzyskania kolekcji, w której każdy element zawiera rozszerzenie pliku oraz czytelną nazwę. Programiści mogą następnie iterować tę kolekcję, aby tworzyć reguły walidacji, wypełniać listy rozwijane w interfejsie użytkownika lub rejestrować obsługiwane typy, zapewniając, że przetwarzane są tylko kompatybilne dokumenty.

## Dlaczego wyświetlać listę formatów w GroupDocs.Redaction?

GroupDocs.Redaction obsługuje **30+** różnych typów plików — w tym PDF, DOCX, PPTX oraz formaty obrazów — co pozwala radzić sobie z większością dokumentów korporacyjnych bez użycia konwerterów firm trzecich. Programowe wyświetlanie tych formatów eliminuje zgadywanie, zmniejsza liczbę zgłoszeń wsparcia i zapewnia, że do Twojego potoku przetwarzania trafiają wyłącznie kompatybilne pliki.

## Wymagania wstępne

- **GroupDocs.Redaction for .NET** – pobierz najnowszy pakiet ze strony oficjalnej.  
- **.NET Framework or .NET Core** – kompatybilne z Twoim środowiskiem programistycznym.  
- **Visual Studio** (lub dowolne IDE kompatybilne z C#).  
- Podstawowa znajomość składni C#.

## Konfiguracja GroupDocs.Redaction dla .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### Interfejs UI Menedżera Pakietów NuGet
- Wyszukaj **„GroupDocs.Redaction”** i zainstaluj najnowszą wersję.

### Uzyskanie licencji
GroupDocs oferuje darmową wersję próbną, tymczasową licencję do oceny lub pełne opcje zakupu. Odwiedź stronę GroupDocs, aby uzyskać odpowiedni plik licencji.

### Podstawowa inicjalizacja i konfiguracja
Po dodaniu pakietu odwołaj się do przestrzeni nazw i utwórz instancję `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Przewodnik implementacji

### Jak wyświetlić listę formatów w GroupDocs.Redaction .NET?
Załaduj bibliotekę, wywołaj statyczny pomocnik i posortuj wyniki — to zapewnia gotową do użycia kolekcję w zaledwie dwóch linijkach kodu. Użyj `FileType.GetSupportedFileFormats()`, aby pobrać `IEnumerable<FileType>` zawierające rozszerzenie i nazwę wyświetlaną każdego formatu, a następnie posortuj według rozszerzenia, aby uzyskać przejrzystą listę w UI.

### Pobieranie obsługiwanych formatów plików

#### Przegląd
Celem jest uzyskanie listy typów plików, które GroupDocs.Redaction może obsłużyć, ułatwiając integrację z logiką walidacji, listami rozwijanymi w UI lub mechanizmami logowania.

#### Implementacja krok po kroku

**1. Pobierz obsługiwane typy plików**  
`FileType.GetSupportedFileFormats()` zwraca każdy format rozpoznawany przez bibliotekę. Metoda jest częścią klasy `GroupDocs.Redaction.FileType`, która kapsułkuje metadane takie jak rozszerzenie pliku i przyjazna nazwa.

**2. Wyświetl obsługiwane typy plików**  
Iteruj po kolekcji i wypisz każde rozszerzenie oraz opis formatu. Przykład kodu w linii:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

Fragment kodu wypisuje starannie uporządkowaną listę, np. „.pdf – Portable Document Format”, co jest idealne do wypełniania elementów UI.

### Wskazówki rozwiązywania problemów
- **Missing Package** – Zweryfikuj odwołanie do pakietu NuGet i przywróć pakiety w razie potrzeby.  
- **Incorrect License Path** – Upewnij się, że plik licencji został skopiowany do katalogu wyjściowego lub podaj ścieżkę bezwzględną.  
- **Unsupported Extension** – Jeśli format nie jest wymieniony, sprawdź, czy używasz najnowszej wersji biblioteki; nowsze wydania dodają dodatkowe formaty.

## Praktyczne zastosowania
Zrozumienie obsługiwanych formatów plików otwiera kilka rzeczywistych scenariuszy:

1. **Systemy zarządzania dokumentami** – Waliduj przesyłane pliki względem listy obsługiwanych, aby zapobiec awariom przetwarzania.  
2. **Bezpieczeństwo treści** – Stosuj reguły redakcji tylko do typów plików, które silnik może bezpiecznie modyfikować.  
3. **Potoki przetwarzania wsadowego** – Filtruj duże partie plików przed wywołaniem redakcji, oszczędzając CPU i pamięć.

## Uwagi dotyczące wydajności
- **Ślad pamięci** – Wyświetlanie listy formatów to lekka operacja; nie ładuje żadnego dokumentu do pamięci.  
- **Operacje wsadowe** – Przy przetwarzaniu setek plików pobierz listę formatów raz i używaj jej ponownie, aby uniknąć zbędnych wywołań.  
- **Bezpieczeństwo wątków** – `FileType.GetSupportedFileFormats()` jest bezpieczne wątkowo i może być wywoływane z równoległych zadań bez synchronizacji.

## Podsumowanie
Masz teraz kompletną, gotową do produkcji metodę **jak wyświetlić listę formatów** przy użyciu GroupDocs.Redaction .NET. Dzięki integracji tej funkcji możesz ulepszyć walidację, poprawić doświadczenia użytkowników i utrzymać solidność swoich potoków dokumentów.

### Kolejne kroki
- Zbadaj API `Redactor`, aby stosować reguły redakcji w zależności od typu pliku.  
- Połącz listę formatów z listą rozwijaną w interfejsie front‑end, aby uzyskać płynny wybór plików.  
- Przejrzyj przewodnik po wydajności, aby zoptymalizować przetwarzanie dużych partii.

## Najczęściej zadawane pytania

**Q: Czy mogę pobrać listę formatów bez inicjalizacji instancji Redactor?**  
A: Tak, `FileType.GetSupportedFileFormats()` jest metodą statyczną i nie wymaga obiektu `Redactor`.

**Q: Czy lista zawiera zarówno formaty wejściowe, jak i wyjściowe?**  
A: Metoda zwraca wszystkie formaty, które biblioteka może zarówno odczytywać, jak i zapisywać; każdy `FileType` zawiera flagi `CanRead` i `CanWrite`.

**Q: Jak często aktualizowana jest lista obsługiwanych formatów?**  
A: GroupDocs wydaje aktualizacje formatów wraz z każdą wersją biblioteki; sprawdzanie listy w czasie działania zapewnia, że zawsze masz najnowszy zestaw.

**Q: Czy istnieje sposób, aby filtrować tylko formaty kompatybilne z PDF?**  
A: Tak, przefiltruj kolekcję, gdzie `format.Extension == ".pdf"` lub gdzie `format.Name.Contains("PDF")`.

**Q: Czy to podejście zadziała na .NET Core 2.1?**  
A: Metoda wymaga .NET Core 3.1 lub nowszego; wcześniejsze środowiska nie są obsługiwane.

## Sekcja FAQ
1. **Jak zainstalować GroupDocs.Redaction dla .NET?**  
   Użyj polecenia CLI `dotnet add package GroupDocs.Redaction` lub zainstaluj poprzez interfejs UI Menedżera Pakietów NuGet.  
2. **Jakie są typowe problemy przy pobieraniu obsługiwanych formatów?**  
   Upewnij się, że wszystkie zależności zostały przywrócone i że odwołujesz się do właściwej przestrzeni nazw (`GroupDocs.Redaction`).  
3. **Czy mogę używać tej funkcji w aplikacjach nie‑.NET?**  
   Ten samouczek koncentruje się na .NET, ale GroupDocs udostępnia podobne API dla Javy, Pythona i innych platform.  
4. **Jak mogę zoptymalizować wydajność przy użyciu GroupDocs.Redaction?**  
   Ponownie używaj listy formatów, unikaj ładowania pełnych dokumentów, gdy sprawdzasz jedynie kompatybilność, oraz monitoruj zużycie pamięci podczas zadań wsadowych.  
5. **Jakie typy plików obsługuje GroupDocs.Redaction?**  
   Biblioteka obsługuje ponad 30 formatów, w tym PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG i wiele innych. Użyj `FileType.GetSupportedFileFormats()`, aby zobaczyć pełną listę.

## Zasoby
- [Dokumentacja](https://docs.groupdocs.com/redaction/net/)
- [Referencja API](https://reference.groupdocs.com/redaction/net)
- [Pobierz GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Darmowe forum wsparcia](https://forum.groupdocs.com/c/redaction/33)
- [Licencja tymczasowa](https://purchase.groupdocs.com/temporary-license/)

---

**Ostatnia aktualizacja:** 2026-07-20  
**Testowano z:** GroupDocs.Redaction 4.2.0 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## Powiązane samouczki

- [Samouczki obsługi formatów dla GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Samouczki ładowania dokumentów z GroupDocs.Redaction dla .NET](/redaction/net/document-loading/)
- [Samouczki zapisywania dokumentów dla GroupDocs.Redaction .NET](/redaction/net/document-saving/)