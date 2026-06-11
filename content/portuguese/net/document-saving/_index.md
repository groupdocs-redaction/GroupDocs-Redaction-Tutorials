---
date: 2026-06-11
description: Aprenda a exportar arquivos redigidos, configurar pastas de saída, criar
  PDFs rasterizados e salvar em streams usando GroupDocs.Redaction para .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: Como Exportar Documentos Redigidos com GroupDocs.Redaction .NET
type: docs
url: /pt/net/document-saving/
weight: 3
---

# Como Exportar Documentos Redigidos com GroupDocs.Redaction .NET

Neste guia abrangente, você descobrirá **como exportar conteúdo redigido** de forma segura e eficiente usando o GroupDocs.Redaction para .NET. Seja para manter o tipo de arquivo original, bloquear o documento como um PDF rasterizado ou transmitir o resultado diretamente na memória, guiamos você por todas as opções com explicações claras e conversacionais e dicas práticas. Ao final deste tutorial, você será capaz de escolher a estratégia de exportação correta para qualquer cenário orientado por conformidade.

## Respostas Rápidas
- **Quais formatos posso exportar?** Qualquer um dos mais de 30 formatos nativos suportados pelo GroupDocs.Redaction, além de PDF rasterizado para máxima segurança.  
- **Preciso de licença para streaming?** Sim, uma licença válida do GroupDocs.Redaction é necessária para streaming em produção.  
- **Posso definir uma pasta de saída personalizada?** Absolutamente – use a propriedade `OutputPath` ou `SaveOptions` para configurá‑la.  
- **A rasterização é segura para arquivos grandes?** Ela manipula documentos de até 500 páginas sem carregar o arquivo inteiro na memória.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## O que é GroupDocs.Redaction?
GroupDocs.Redaction é uma biblioteca .NET que remove ou mascara programaticamente informações sensíveis de PDFs, Word, Excel, PowerPoint, imagens e muitos outros formatos. Ela oferece uma API de alto nível para definir regiões de redação, aplicar políticas e, finalmente, exportar o documento limpo. Isso facilita a integração de recursos de redação em qualquer aplicação .NET.

## Por que Exportar Documentos Redigidos como PDFs Rasterizados?
PDFs rasterizados convertem cada página em uma imagem plana, eliminando camadas de texto ocultas que poderiam ser extraídas posteriormente. Este formato garante que o conteúdo redigido não possa ser recuperado, atendendo a rigorosos padrões regulatórios como GDPR e HIPAA. O GroupDocs.Redaction pode produzir PDFs rasterizados de até 300 dpi, preservando a fidelidade visual enquanto assegura a segurança.

## Como Exportar Documentos Redigidos?
Carregue o arquivo de origem, aplique suas regras de redação e, em seguida, chame o método de salvamento apropriado — seja `Save` para o formato original, `SaveAsRasterizedPdf` para PDFs apenas de imagem ou `SaveToStream` para manipulação em memória. Abaixo está o fluxo de trabalho passo a passo. Cada método garante que o conteúdo redigido seja removido permanentemente, preservando o formato de saída desejado.

### Etapa 1: Instalar o Pacote NuGet
Adicione o pacote mais recente do GroupDocs.Redaction ao seu projeto:

```bash
dotnet add package GroupDocs.Redaction
```

### Etapa 2: Carregar o Documento e Definir Redações
Crie uma instância `Redactor`, carregue o arquivo e especifique as regiões que deseja ocultar. A classe `Redactor` fornece a funcionalidade central para carregar documentos e aplicar regras de redação.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Etapa 3: Escolher o Método de Exportação
#### Exportar no Formato Original
```csharp
redactor.Save("RedactedReport.docx");
```

#### Exportar como PDF Rasterizado
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Exportar para um Memory Stream (ideal para APIs web)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

O método `Save` grava o documento redigido em um arquivo no seu formato original. `SaveAsRasterizedPdf` cria um PDF onde cada página é renderizada como uma imagem, removendo qualquer texto oculto. `SaveToStream` devolve o arquivo redigido como um memory stream, adequado para respostas web.

## Como Configurar uma Pasta de Saída?
Defina a propriedade `OutputPath` no `Redactor` ou passe um objeto `SaveOptions` personalizado que inclua o diretório desejado. `OutputPath` é uma propriedade do `Redactor` que especifica o diretório onde os arquivos de saída são gravados. `SaveOptions` permite personalizar vários parâmetros de salvamento, incluindo a pasta de saída. Isso garante que todos os arquivos exportados sejam gravados em um local previsível, simplificando pipelines de processamento em lote. Você também pode especificar subpastas por tipo de documento para manter seu espaço de trabalho organizado.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Problemas Comuns e Soluções
- **Redação não aplicada:** Verifique se o padrão de busca corresponde exatamente ao texto do documento; use `RegexOptions.IgnoreCase` se necessário. `RegexOptions` é uma enumeração que controla o comportamento de correspondência de expressões regulares, como sensibilidade a maiúsculas/minúsculas.  
- **Arquivos grandes causam pressão de memória:** Ative o modo de streaming usando `SaveToStream` e evite chamar `Save` no documento inteiro.  
- **PDF rasterizado parece borrado:** Aumente o DPI em `RasterizationOptions` (por exemplo, 300–600) para melhorar a qualidade da imagem. `RasterizationOptions` permite definir parâmetros como DPI e formato de imagem para a saída de PDF rasterizado.

## Perguntas Frequentes

**Q: Posso exportar para um formato que não era originalmente suportado?**  
A: Sim, o GroupDocs.Redaction pode converter a maioria dos tipos de entrada para PDF, DOCX, XLSX, PPTX ou PDF rasterizado, abrangendo mais de 30 formatos.

**Q: Como a rasterização protege os dados redigidos?**  
A: Ao renderizar cada página como uma imagem plana, quaisquer camadas de texto ocultas são removidas, tornando impossível extrair o conteúdo original.

**Q: É possível encadear múltiplas regras de redação?**  
A: Absolutamente – você pode chamar `Apply` repetidamente ou passar uma coleção de `RedactionOptions` para processar vários padrões em uma única passagem. `RedactionOptions` define as configurações para uma única operação de redação, como região e tipo de substituição.

**Q: Preciso fechar o objeto Redactor?**  
A: O `Redactor` implementa `IDisposable`; envolva‑o em um bloco `using` ou chame `Dispose()` para liberar os manipuladores de arquivo rapidamente. `IDisposable` é uma interface que fornece um mecanismo para liberar recursos não gerenciados.

**Q: Quais runtimes .NET são oficialmente testados?**  
A: O GroupDocs.Redaction é validado em .NET Framework 4.6+, .NET Core 3.1+ e .NET 5/6/7.

## Recursos Adicionais

### Tutoriais Disponíveis

- [Como Salvar Documentos como PDFs Rasterizados Usando GroupDocs.Redaction para .NET: Um Guia Completo](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementando Diretório de Saída em .NET com GroupDocs.Redaction: Um Guia Abrangente](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redigir e Salvar Documentos com GroupDocs.Redaction para .NET: Um Guia Completo](./redact-save-documents-groupdocs-redaction-net/)
- [Salvar Documentos Redigidos no Formato Original Usando GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redação Segura de Documentos em .NET Usando Streams: Um Guia para GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Links Úteis

- [Documentação do GroupDocs.Redaction para .NET](https://docs.groupdocs.com/redaction/net/)
- [Referência da API do GroupDocs.Redaction para .NET](https://reference.groupdocs.com/redaction/net/)
- [Download do GroupDocs.Redaction para .NET](https://releases.groupdocs.com/redaction/net/)
- [Fórum do GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Suporte Gratuito](https://forum.groupdocs.com/)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última Atualização:** 2026-06-11  
**Testado com:** GroupDocs.Redaction 23.11 for .NET  
**Autor:** GroupDocs  

## Tutoriais Relacionados

- [Salvar Documentos Redigidos no Formato Original Usando GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Como Salvar Documentos como PDFs Rasterizados Usando GroupDocs.Redaction para .NET: Um Guia Completo](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Redação Segura de Documentos em .NET Usando Streams: Um Guia para GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)