---
date: '2026-03-28'
description: Aprenda a implementar um logger personalizado em C# no GroupDocs.Redaction
  para .NET, permitindo registro detalhado personalizado no .NET e facilitando a geração
  de relatórios de conformidade.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: Implementar logger personalizado em C# no GroupDocs.Redaction para .NET
type: docs
url: /pt/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# Implementar logger personalizado c# no GroupDocs.Redaction para .NET

Gerenciar redações de documentos de forma eficiente é crítico, especialmente ao lidar com informações sensíveis. Neste guia você aprenderá **como implementar um logger personalizado c#** com GroupDocs.Redaction para .NET, dando controle total sobre registro, tratamento de erros e trilhas de auditoria.

## Respostas rápidas
- **O que faz um logger personalizado c#?** Ele captura erros, avisos e mensagens informativas durante a redação.  
- **Qual biblioteca fornece a interface ILogger?** GroupDocs.Redaction para .NET.  
- **Posso salvar o documento redigido sem rasterização?** Sim – use `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **Preciso de uma licença para uso em produção?** Uma licença completa é necessária para produção; uma avaliação está disponível para avaliação.  
- **Esta abordagem é compatível com .NET Core / .NET 6+?** Absolutamente – a mesma API funciona em .NET Framework e .NET Core/5/6.

## O que é um logger personalizado c#?
Um **custom logger c#** é uma classe que implementa a interface `ILogger` fornecida pelo GroupDocs.Redaction. Ela permite direcionar mensagens de log onde você precisar — console, arquivo, banco de dados ou sistemas de monitoramento externos — proporcionando uma visão clara do fluxo de trabalho de redação.

## Por que usar logging personalizado .net com GroupDocs.Redaction?
- **Conformidade & Auditoria:** Logs detalhados atendem aos requisitos regulatórios.  
- **Visibilidade de Erros:** `LogError` e `LogWarning` fornecem feedback imediato sobre problemas.  
- **Flexibilidade de Integração:** Encaminhe logs para frameworks de logging .NET existentes (Serilog, NLog, etc.).  

## Pré-requisitos
- **GroupDocs.Redaction para .NET** instalado (veja a instalação abaixo).  
- Um ambiente de desenvolvimento .NET (Visual Studio, VS Code ou CLI).  
- Conhecimento básico de C# e familiaridade com streams de arquivos.  

## Instalação

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
Pesquise por **"GroupDocs.Redaction"** e instale a versão mais recente.

## Aquisição de Licença
- **Teste Gratuito:** Teste a API com uma licença temporária.  
- **Licença Temporária:** Obtenha acesso total aos recursos por um período limitado.  
- **Compra:** Obtenha uma licença perpétua para implantações de produção.

## Guia passo a passo

### Etapa 1: Definir uma classe de logger personalizada (log warnings c#)

Crie uma classe que implemente `ILogger`. Esta classe capturará erros, avisos e mensagens informativas.

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

**Explicação:** O sinalizador `HasErrors` ajuda a decidir se deve continuar o processamento. Os três métodos correspondem aos três níveis de log que você precisará na maioria dos cenários de redação.

### Etapa 2: Preparar caminhos de arquivos e abrir o documento fonte

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Por que isso importa:** Usar métodos utilitários mantém seu código limpo e garante que a pasta de saída exista antes de tentar **salvar o documento redigido**.

### Etapa 3: Aplicar redações usando o logger personalizado

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

**Explicação:**  
1. O `Redactor` é instanciado com `RedactorSettings(logger)`, vinculando seu `CustomLogger`.  
2. Após aplicar uma redação, o código verifica `logger.HasErrors`. Se não houver erros, o documento é salvo — demonstrando a lógica de **salvar documento redigido** sem rasterização.

### Armadilhas comuns & Solução de problemas
- **Saída de log ausente:** Verifique se cada método `Log*` está corretamente sobrescrito.  
- **Exceções de acesso a arquivos:** Garanta que a aplicação tenha permissões de leitura/escrita para os caminhos de origem e saída.  
- **Logger não conectado:** O parâmetro `RedactorSettings(logger)` é essencial; omiti-lo desativa o logging personalizado.

## Aplicações práticas

1. **Relatórios de Conformidade:** Exporte entradas de log para CSV ou banco de dados para trilhas de auditoria.  
2. **Rastreamento de Erros:** Localize rapidamente arquivos problemáticos escaneando a saída de `LogError`.  
3. **Automação de Fluxo de Trabalho:** Dispare processos subsequentes (ex.: notificar um oficial de conformidade) quando `LogWarning` for invocado.

## Considerações de desempenho

- **Descartar streams prontamente** para liberar memória, especialmente ao processar grandes lotes.  
- **Monitorar CPU & memória** durante redações em massa; considere processar documentos em paralelo com sincronização cuidadosa do logger.  
- **Mantenha-se atualizado:** Versões mais recentes do GroupDocs.Redaction frequentemente incluem otimizações de desempenho e ganchos de logging adicionais.

## Conclusão

Ao implementar um **custom logger c#**, você obtém insight granular em cada etapa do pipeline de redação, facilitando o cumprimento de padrões de conformidade e a depuração de problemas. A abordagem mostrada aqui funciona perfeitamente com GroupDocs.Redaction para .NET e pode ser estendida para integrar-se a qualquer framework de logging .NET que você já use.

---

## Perguntas Frequentes

**Q: Qual é o objetivo do logging personalizado com GroupDocs.Redaction?**  
A: O logging personalizado ajuda a rastrear e gerenciar redações para conformidade, rastreamento de erros e otimização de fluxo de trabalho.

**Q: Como lidar com erros usando um logger personalizado?**  
A: Implemente `LogError` na sua classe `CustomLogger`; o sinalizador `HasErrors` permite interromper o processamento se necessário.

**Q: O logging personalizado pode ser integrado a outros sistemas?**  
A: Sim, você pode encaminhar mensagens de log para CRM, ERP ou ferramentas de monitoramento centralizadas estendendo os métodos do logger.

**Q: Quais são algumas armadilhas comuns ao implementar logging personalizado?**  
A: Implementações incorretas de métodos, ausência de `RedactorSettings(logger)` e problemas de permissão de arquivos são as mais frequentes.

**Q: Como o logging personalizado melhora os fluxos de trabalho de redação de documentos?**  
A: Logs detalhados fornecem visibilidade em tempo real, simplificam a solução de problemas e atendem aos requisitos de auditoria.

## Recursos

- **Documentation:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **API Reference:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)
- **Download:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**Last Updated:** 2026-03-28  
**Tested With:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---