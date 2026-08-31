---
date: '2026-03-28'
description: Dowiedz się, jak zaimplementować własny logger C# w GroupDocs.Redaction
  dla .NET, umożliwiając szczegółowe niestandardowe logowanie w .NET i ułatwiając
  raportowanie zgodności.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implementacja własnego loggera C# w GroupDocs.Redaction dla .NET
type: docs
url: /pl/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Implementacja własnego loggera c# w GroupDocs.Redaction dla .NET

Efektywne zarządzanie redakcjami dokumentów jest kluczowe, szczególnie przy obsłudze wrażliwych informacji. W tym przewodniku dowiesz się **jak zaimplementować własny logger c#** z GroupDocs.Redaction dla .NET, co daje pełną kontrolę nad logowaniem, obsługą błędów i ścieżkami audytu.

## Szybkie odpowiedzi
- **Co robi własny logger c#?** Rejestruje błędy, ostrzeżenia i komunikaty informacyjne podczas redakcji.  
- **Która biblioteka udostępnia interfejs ILogger?** GroupDocs.Redaction dla .NET.  
- **Czy mogę zapisać zredagowany dokument bez rasteryzacji?** Tak – użyj `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Czy potrzebna jest licencja do użytku produkcyjnego?** Wymagana jest pełna licencja do produkcji; dostępna jest wersja próbna do oceny.  
- **Czy to podejście jest kompatybilne z .NET Core / .NET 6+?** Absolutnie – to samo API działa zarówno w .NET Framework, jak i .NET Core/5/6.

## Czym jest własny logger c#?
**Własny logger c#** to klasa implementująca interfejs `ILogger` dostarczany przez GroupDocs.Redaction. Pozwala kierować komunikaty logów tam, gdzie potrzebujesz — konsola, plik, baza danych lub zewnętrzne systemy monitorujące — zapewniając przejrzysty podgląd procesu redakcji.

## Dlaczego warto używać własnego logowania .net z GroupDocs.Redaction?
- **Zgodność i audyt:** Szczegółowe logi spełniają wymogi regulacyjne.  
- **Widoczność błędów:** `LogError` i `LogWarning` zapewniają natychmiastową informację o problemach.  
- **Elastyczność integracji:** Przekazuj logi do istniejących frameworków logowania .NET (Serilog, NLog, itp.).  

## Wymagania wstępne
- **GroupDocs.Redaction for .NET** zainstalowany (zobacz instalację poniżej).  
- Środowisko programistyczne .NET (Visual Studio, VS Code lub CLI).  
- Podstawowa znajomość C# oraz obsługi strumieni plików.  

## Instalacja

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Wyszukaj **"GroupDocs.Redaction"** i zainstaluj najnowszą wersję.

## Uzyskanie licencji
- **Darmowa wersja próbna:** Przetestuj API z tymczasową licencją.  
- **Licencja tymczasowa:** Uzyskaj pełny dostęp do funkcji na ograniczony czas.  
- **Zakup:** Uzyskaj licencję wieczystą do wdrożeń produkcyjnych.

## Przewodnik krok po kroku

### Krok 1: Zdefiniuj własną klasę loggera (log warnings c#)

Utwórz klasę implementującą `ILogger`. Klasa ta będzie przechwytywać błędy, ostrzeżenia i komunikaty informacyjne.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**Wyjaśnienie:** Flaga `HasErrors` pomaga zdecydować, czy kontynuować przetwarzanie. Trzy metody odpowiadają trzem poziomom logowania, które będą potrzebne w większości scenariuszy redakcji.

### Krok 2: Przygotuj ścieżki plików i otwórz dokument źródłowy

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Dlaczego to ważne:** Korzystanie z metod pomocniczych utrzymuje kod czystym i zapewnia, że folder wyjściowy istnieje przed próbą **zapisania zredagowanego dokumentu**.

### Krok 3: Zastosuj redakcje używając własnego loggera

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**Wyjaśnienie:**  
1. `Redactor` jest tworzony z `RedactorSettings(logger)`, łącząc Twój `CustomLogger`.  
2. Po zastosowaniu redakcji kod sprawdza `logger.HasErrors`. Jeśli nie wystąpiły błędy, dokument jest zapisywany — co demonstruje logikę **zapisania zredagowanego dokumentu** bez rasteryzacji.

### Typowe pułapki i rozwiązywanie problemów
- **Brak wyjścia logu:** Zweryfikuj, że każda metoda `Log*` jest prawidłowo nadpisana.  
- **Wyjątki dostępu do pliku:** Upewnij się, że aplikacja ma uprawnienia odczytu/zapisu zarówno do ścieżek źródłowych, jak i wyjściowych.  
- **Logger nie podłączony:** Parametr `RedactorSettings(logger)` jest niezbędny; pominięcie go wyłącza własne logowanie.

## Praktyczne zastosowania
1. **Raportowanie zgodności:** Eksportuj wpisy logów do CSV lub bazy danych w celu tworzenia ścieżek audytu.  
2. **Śledzenie błędów:** Szybko zlokalizuj problematyczne pliki, przeszukując wyjście `LogError`.  
3. **Automatyzacja przepływu pracy:** Uruchom procesy zależne (np. powiadomienie pracownika ds. zgodności) gdy wywołany zostanie `LogWarning`.

## Uwagi dotyczące wydajności
- **Niezwłocznie zwalniaj strumienie** aby zwolnić pamięć, szczególnie przy przetwarzaniu dużych partii.  
- **Monitoruj CPU i pamięć** podczas masowych redakcji; rozważ przetwarzanie dokumentów równolegle przy zachowaniu ostrożnej synchronizacji loggera.  
- **Bądź na bieżąco:** Nowsze wersje GroupDocs.Redaction często zawierają optymalizacje wydajności i dodatkowe haki logowania.

## Zakończenie

Implementując **własny logger c#**, uzyskasz szczegółowy wgląd w każdy krok potoku redakcji, co ułatwia spełnianie standardów zgodności i debugowanie problemów. Podejście przedstawione tutaj działa płynnie z GroupDocs.Redaction dla .NET i może być rozszerzone o integrację z dowolnym frameworkiem logowania .NET, którego już używasz.

---

## Najczęściej zadawane pytania

**Q: Jaki jest cel własnego logowania z GroupDocs.Redaction?**  
A: Własne logowanie pomaga śledzić i zarządzać redakcjami pod kątem zgodności, śledzenia błędów i optymalizacji przepływu pracy.

**Q: Jak obsługiwać błędy przy użyciu własnego loggera?**  
A: Zaimplementuj `LogError` w swojej klasie `CustomLogger`; flaga `HasErrors` pozwala w razie potrzeby zatrzymać przetwarzanie.

**Q: Czy własne logowanie może być zintegrowane z innymi systemami?**  
A: Tak, możesz przekazywać komunikaty logów do systemów CRM, ERP lub scentralizowanych narzędzi monitorujących, rozszerzając metody loggera.

**Q: Jakie są typowe pułapki przy implementacji własnego logowania?**  
A: Nieprawidłowe implementacje metod, brak `RedactorSettings(logger)` oraz problemy z uprawnieniami do plików są najczęstsze.

**Q: Jak własne logowanie usprawnia przepływy pracy redakcji dokumentów?**  
A: Szczegółowe logi zapewniają widoczność w czasie rzeczywistym, upraszczają rozwiązywanie problemów i spełniają wymogi audytu.

## Zasoby

- **Documentation:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **API Reference:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)
- **Download:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Ostatnia aktualizacja:** 2026-03-28  
**Testowano z:** GroupDocs.Redaction 23.11 for .NET  
**Autor:** GroupDocs