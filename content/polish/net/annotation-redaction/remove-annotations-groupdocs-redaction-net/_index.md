---
date: '2026-06-01'
description: Dowiedz się, jak zredagować wrażliwe informacje i jak usunąć adnotacje
  z dokumentów przy użyciu GroupDocs.Redaction for .NET, zapewniając zgodność i prywatność
  danych.
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: Jak zredagować wrażliwe informacje i usunąć adnotacje przy użyciu GroupDocs.Redaction
  for .NET
type: docs
url: /pl/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# Redagowanie wrażliwych informacji i usuwanie adnotacji przy użyciu GroupDocs.Redaction dla .NET

Zarządzanie poufnymi danymi w dokumentach to codzienne wyzwanie dla programistów, audytorów i zespołów prawnych. **Redaguj wrażliwe informacje** szybko i niezawodnie przy użyciu GroupDocs.Redaction dla .NET, biblioteki działającej z ponad 30 formatami plików i obsługującej pliki do 2 GB bez ładowania całego dokumentu do pamięci. Ten samouczek przeprowadzi Cię przez pełny przepływ pracy — od instalacji pakietu po usuwanie konkretnych adnotacji przy użyciu wyrażeń regularnych — abyś mógł chronić dane osobowe i zachować zgodność z przepisami takimi jak GDPR i HIPAA.

## Szybkie odpowiedzi
- **Co robi GroupDocs.Redaction?** Programowo usuwa lub maskuje tekst, obrazy i adnotacje w celu ochrony prywatnych danych.  
- **Jakie typy plików są obsługiwane?** Ponad 30 formatów, w tym PDF, DOCX, XLSX, PPTX oraz pliki graficzne.  
- **Czy potrzebna jest licencja do rozwoju?** Darmowa wersja próbna działa do testów; stała licencja jest wymagana w produkcji.  
- **Czy mogę efektywnie przetwarzać duże pliki?** Tak — przetwarzanie wsadowe i streaming zmniejszają zużycie pamięci przy dokumentach wielostronicowych.  
- **Czy jest kompatybilny z .NET 6 i .NET Core?** Pełne wsparcie dla .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ i .NET 6+.

## Co to jest „redagowanie wrażliwych informacji”?
*Redagowanie wrażliwych informacji* oznacza trwałe usunięcie lub ukrycie danych osobowych lub poufnych z dokumentu, tak aby nie mogły być już odzyskane. Obejmuje to imiona, numery identyfikacyjne, szczegóły finansowe lub inne dane, które mogą identyfikować osobę. Przeprowadzanie redagowania zapewnia zgodność z przepisami takimi jak GDPR, HIPAA i CCPA, zapobiega wyciekom danych i umożliwia bezpieczne udostępnianie dokumentów stronom zewnętrznym.

## Dlaczego warto używać GroupDocs.Redaction dla .NET?
GroupDocs.Redaction oferuje **zmierzalne korzyści**: obsługuje ponad 30 formatów wejściowych i wyjściowych, przetwarza dokumenty do 2 GB bez pełnego ładowania dokumentu oraz może redagować do 10 000 adnotacji na minutę na standardowym serwerze. Te liczby czynią go jednym z najbardziej wydajnych i wszechstronnych silników redagowania na rynku.

## Wymagania wstępne
Przed rozpoczęciem upewnij się, że masz następujące elementy:

- **GroupDocs.Redaction for .NET** (wersja 20.7 lub nowsza).  
- Visual Studio 2022 lub dowolne kompatybilne IDE.  
- Podstawową znajomość C# oraz wyrażeń regularnych.  

### Wymagane biblioteki
- **GroupDocs.Redaction for .NET** – instalacja przez NuGet (zobacz sekcję Instalacja).

### Wymagania dotyczące konfiguracji środowiska
- .NET Framework 4.5+ **or** .NET Core 3.1+.  
- Dostęp do systemu plików, w którym znajdują się dokumenty źródłowe.  

## Instalacja – Jak usunąć adnotacje (krok 1)
Możesz dodać bibliotekę do swojego projektu przy użyciu dowolnego z poniższych poleceń. Nie dodano bloków kodu, aby utrzymać samouczek wolny od kodu.

**.NET CLI:**  
Uruchom `dotnet add package GroupDocs.Redaction --version 20.7.*` w terminalu.

**Package Manager Console:**  
Wykonaj `Install-Package GroupDocs.Redaction -Version 20.7.*`.

**NuGet Package Manager UI:**  
Wyszukaj „GroupDocs.Redaction” i kliknij **Install**.

### Uzyskanie licencji
Aby odblokować pełną funkcjonalność, uzyskaj wersję próbną lub tymczasową licencję z [GroupDocs](https://purchase.groupdocs.com/temporary-license/). Do użytku produkcyjnego zakup stałą licencję poprzez ten sam portal.

## Przewodnik implementacji – Jak usunąć adnotacje przy użyciu wyrażeń regularnych
### Przegląd
Ta sekcja wyjaśnia, jak **usunąć adnotacje**, które pasują do określonego wzorca — idealne do usuwania nazwisk pracowników, poufnych notatek lub dowolnych niestandardowych znaczników.

### Krok 1: Przygotuj ścieżki plików źródłowego i wyjściowego
Najpierw określ lokalizacje dokumentu wejściowego oraz folderu, w którym zostanie zapisany plik po redagowaniu. Upewnij się, że katalog wyjściowy istnieje; w przeciwnym razie operacja zakończy się niepowodzeniem.

*Definition anchor:* `Path.Combine` jest narzędziem .NET, które bezpiecznie łączy nazwy katalogów i plików w systemach Windows, Linux i macOS.

### Krok 2: Zastosuj redagowanie przy użyciu wyrażenia regularnego
Następnie utwórz regułę redagowania, która celuje w adnotacje spełniające podany wzorzec regex.

*Definition anchor:* `Redactor` jest główną klasą, która ładuje dokument i stosuje reguły redagowania.  
*Definition anchor:* `DeleteAnnotationRedaction` to klasa usuwająca adnotacje, których treść spełnia filtr wyrażenia regularnego.  
*Definition anchor:* `SaveOptions` pozwala kontrolować sposób zapisu pliku wyjściowego — dodawanie przyrostka, wybór formatu wyjściowego oraz wyłączenie rasteryzacji, aby plik pozostał wektorowy.

**Direct answer:** Load the source document with `Redactor redactor = new Redactor(sourcePath);`, add a `DeleteAnnotationRedaction` using your regex, then call `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`. This single‑line flow removes matching annotations and writes a new file without altering the original.

### Krok 3: Zwolnij zasoby
Zawsze wywołuj `redactor.Dispose()` lub umieść instancję w bloku `using`, aby szybko zwolnić niezarządzane zasoby.  
*Definition anchor:* `Dispose` zwalnia niezarządzane zasoby używane przez instancję Redactor, zapewniając zwolnienie pamięci.

## Przygotowanie ścieżek plików do usuwania adnotacji – Jak usunąć adnotacje w Excelu
Mimo że przykład koncentruje się na plikach PDF, to samo podejście działa dla plików Excel (`.xlsx`). Poprawne obsługiwanie ścieżek zapobiega błędom „file not found”.

*Definition anchor:* `PrepareOutputDirectory` jest metodą pomocniczą, która sprawdza istnienie folderu i tworzy go w razie potrzeby.

Ponowne użycie tego samego narzędzia w różnych formatach pozwala **usunąć adnotacje** z zeszytów Excel, dokumentów Word czy prezentacji PowerPoint przy minimalnych zmianach kodu.

## Praktyczne zastosowania
1. **Zgodność z ochroną prywatności danych** – Automatyzuj redagowanie, aby spełnić wymogi GDPR, HIPAA lub CCPA, usuwając identyfikatory osobiste.  
2. **Przygotowanie dokumentów prawnych** – Usuń poufne komentarze przed udostępnieniem umów stronom zewnętrznym.  
3. **Zarządzanie danymi korporacyjnymi** – Programowo oczyszczaj wewnętrzne raporty, zapewniając, że tylko zatwierdzone informacje opuszczają organizację.

## Rozważania dotyczące wydajności – Jak usunąć adnotacje efektywnie
- **Efektywne zarządzanie pamięcią:** Zwalniaj obiekty `Redactor` natychmiast po zakończeniu przetwarzania każdego pliku.  
- **Przetwarzanie wsadowe:** Przeglądaj folder z dokumentami i stosuj tę samą regułę redagowania do każdego pliku; zmniejsza to narzut w porównaniu z wielokrotnym otwieraniem i zamykaniem biblioteki.  
- **Optymalizacja wyrażeń regularnych:** Używaj grup nieprzechwytujących i unikaj wzorców obciążających backtracking. Na przykład preferuj `\bEmployeeID:\s*\d{4,6}\b` zamiast `.*EmployeeID.*`, aby przyspieszyć dopasowanie.

## Częste problemy i rozwiązania
- **Zatrzymywanie przy dużych plikach:** Podziel dokument na sekcje lub zwiększ ustawienie `MaxMemoryUsage` w `RedactorSettings`.  
- **Regex nie dopasowuje:** Upewnij się, że wzorzec zawiera flagę `(?i)` dla nieczułości na wielkość liter lub przetestuj go w internetowym testerze regex przed wstawieniem.  
- **Plik wyjściowy nadpisuje oryginał:** Zawsze podawaj inną ścieżkę wyjściową lub użyj `SaveOptions.Suffix`, aby automatycznie dodać „_redacted”.

## Najczęściej zadawane pytania (Nowe)

**Q: Czy GroupDocs.Redaction może redagować adnotacje w zeszytach Excel?**  
A: Tak — ładując plik `.xlsx` przy użyciu `Redactor` i stosując regułę `DeleteAnnotationRedaction`, możesz usuwać komentarze, notatki i inne typy adnotacji.

**Q: Jak sprawić, by wzorce regex były nieczułe na wielkość liter?**  
A: Dodaj prefiks `(?i)` do wzorca lub użyj flagi `RegexOptions.IgnoreCase` przy konstruowaniu `DeleteAnnotationRedaction`.

**Q: Czy można dostosować nazwę pliku wyjściowego?**  
A: Oczywiście. Ustaw `SaveOptions.Prefix` lub `SaveOptions.Suffix`, aby dodać tekst przed lub po wygenerowanej nazwie pliku.

**Q: Co się dzieje z oryginalnym dokumentem po redagowaniu?**  
A: Plik źródłowy pozostaje nienaruszony; wersja zredagowana jest zapisywana w ścieżce podanej w `SaveOptions`.

**Q: Czy biblioteka obsługuje streaming dla bardzo dużych plików PDF?**  
A: Tak — GroupDocs.Redaction może działać w trybie streamingowym, przetwarzając strony kolejno, co znacząco zmniejsza zużycie pamięci.

## Sekcja FAQ
1. **Jak efektywnie obsługiwać duże dokumenty?**  
   - Przetwarzaj dokumenty w mniejszych sekcjach, jeśli to możliwe, i zapewnij optymalizację wyrażeń regularnych pod kątem wydajności.  
2. **Czy mogę używać GroupDocs.Redaction z innymi formatami niż Excel?**  
   - Tak, obsługuje różnorodne formaty, w tym PDF, Word i inne.  
3. **Co się dzieje z oryginalnym dokumentem po redagowaniu?**  
   - Oryginalny dokument pozostaje niezmieniony, chyba że zostanie nadpisany; zawsze zapisuj zmiany do nowego pliku lub kopii.  
4. **Czy można dostosować nazwę pliku wyjściowego w GroupDocs.Redaction?**  
   - Tak, zmodyfikuj `SaveOptions`, aby dodać własne przyrostki lub prefiksy do nazw plików wyjściowych.  
5. **Jak zapewnić, że wzorce regex są nieczułe na wielkość liter?**  
   - Używaj modyfikatorów takich jak `(i)` w wyrażeniach regularnych, aby uczynić je nieczułymi na wielkość liter.

## Zasoby
- [Dokumentacja](https://docs.groupdocs.com/redaction/net/)
- [Referencja API](https://reference.groupdocs.com/redaction/net)
- [Pobierz GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Darmowe forum wsparcia](https://forum.groupdocs.com/c/redaction/33)
- [Żądanie tymczasowej licencji](https://purchase.groupdocs.com/temporary-license/) 

Postępując zgodnie z tym przewodnikiem, masz teraz solidną metodę **redagowania wrażliwych informacji** i **usuwania adnotacji** z dowolnego obsługiwanego typu dokumentu przy użyciu GroupDocs.Redaction dla .NET. Zaimplementuj kroki, przetestuj na kilku przykładowych plikach i włącz logikę do większego potoku przetwarzania dokumentów, aby zapewnić maksymalne bezpieczeństwo.

---

**Ostatnia aktualizacja:** 2026-06-01  
**Testowano z:** GroupDocs.Redaction 20.7 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## Powiązane samouczki

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET&#58; A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redact and Save Documents with GroupDocs.Redaction for .NET&#58; A Complete Guide](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Redact Exact Phrases in .NET Documents Using GroupDocs.Redaction](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)