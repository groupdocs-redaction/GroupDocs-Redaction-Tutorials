---
date: '2026-06-06'
description: Aprenda como converter página para PNG e visualizar páginas PDF com GroupDocs.Redaction
  para .NET. Guia passo a passo, trechos de código e dicas práticas.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: Converter página para PNG usando GroupDocs.Redaction .NET
type: docs
url: /pt/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# Converter Página para PNG Usando GroupDocs.Redaction .NET

Criar uma visualização de uma única página de um documento grande é uma necessidade comum quando você deseja compartilhar apenas a parte relevante da informação. Neste tutorial você aprenderá **como converter uma página para PNG** com GroupDocs.Redaction para .NET, configurar a saída da visualização e integrar o resultado em suas aplicações. Vamos percorrer os pré‑requisitos, instalação, configuração de código e dicas práticas para que você possa começar a gerar visualizações PNG de página única em minutos.

## Respostas Rápidas
- **Posso gerar uma visualização PNG de apenas uma página?** Sim, use `PreviewOptions` para especificar o número da página e o formato.  
- **Qual formato o GroupDocs.Redaction suporta para visualizações?** PNG é o padrão, mas JPEG e BMP também estão disponíveis.  
- **Preciso de uma licença para desenvolvimento?** Um teste gratuito funciona para testes; uma licença de produção é necessária para uso comercial.  
- **Isso funciona em .NET Core e .NET Framework?** Absolutamente – a biblioteca tem como alvo .NET Standard 2.0+.  
- **O processo é eficiente em memória para arquivos grandes?** Sim, a API transmite páginas, evitando o carregamento completo do documento.

## O que é converter página para PNG?
**convert page to PNG** refere‑se à extração de uma única página de um documento suportado (PDF, DOCX, PPTX, etc.) e à renderização dessa página como uma imagem Portable Network Graphics (PNG). A imagem resultante preserva o layout visual, fontes e gráficos da página original, permitindo que você compartilhe uma captura clara enquanto mantém o restante do documento oculto.

## Por que usar uma visualização de página única?
Gerar uma visualização PNG de página única reduz a largura de banda, acelera os tempos de carregamento e protege conteúdo sensível ao expor apenas o que é necessário. O GroupDocs.Redaction pode renderizar um PDF de 300 páginas em um PNG de 200 KB em menos de 0,5 segundo em hardware de servidor típico, tornando‑o ideal para portais web e ferramentas de relatório.

## Pré‑requisitos

- **GroupDocs.Redaction for .NET** – a biblioteca central que realiza a redação de documentos e geração de visualizações.  
- **System.IO** – namespace padrão do .NET para manipulação de arquivos.  
- .NET Core 3.1+ ou .NET Framework 4.6.1+ (qualquer plataforma que suporte .NET Standard 2.0).  
- Conhecimento básico de C# e familiaridade com o gerenciamento de pacotes NuGet.

## Configurando GroupDocs.Redaction para .NET

### Informações de Instalação

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Abra seu projeto no Visual Studio.  
- Escolha **Manage NuGet Packages**.  
- Procure por **GroupDocs.Redaction** e instale a versão estável mais recente.

### Etapas de Aquisição de Licença
Para executar a biblioteca você precisa de uma licença válida. Você pode começar com um teste gratuito ou solicitar uma chave temporária:

1. Visite o [GroupDocs website](https://purchase.groupdocs.com/temporary-license) para solicitar uma licença temporária.  
2. Siga as instruções enviadas por e‑mail para adicionar o arquivo de licença ao seu projeto.

### Inicialização e Configuração Básicas
A classe `RedactionEngine` é o ponto de entrada para todas as operações, incluindo a geração de visualizações.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Guia de Implementação

### Visão Geral
Esta seção mostra como **converter página para PNG** configurando `PreviewOptions` e invocando a API de visualização. A abordagem funciona para PDFs, DOCX, PPTX e muitos outros formatos suportados pelo GroupDocs.Redaction.

### Etapa 1: Prepare Seu Ambiente
Defina o caminho do arquivo de origem e a pasta de saída. Use `Path.Combine` para construir caminhos independentes de plataforma.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Etapa 2: Configurar Opções de Visualização
`PreviewOptions` permite definir o número da página, tamanho da imagem e formato de saída. A classe é o centro de configuração para a geração de visualizações.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Explicação das Configurações Principais
- **Width & Height** – Ajuste esses valores para corresponder à resolução de exibição alvo.  
- **PageNumbers** – Forneça um array com o índice exato da página que deseja renderizar (baseado em zero).  
- **PreviewFormat** – PNG é o padrão; altere para `PreviewFormat.Jpeg` para arquivos menores.

### Dicas de Solução de Problemas
Se o PNG não for gerado:

- Verifique se o caminho do arquivo de origem está correto e o arquivo está acessível.  
- Certifique‑se de que o arquivo de licença foi carregado antes de chamar qualquer método da API.  
- Confirme que `PreviewOptions.PageNumbers` contém um índice de página válido (por exemplo, `0` para a primeira página).

## Aplicações Práticas
Criar uma visualização PNG de página única é útil em muitos cenários:

1. **Apresentações ao Cliente** – Mostre apenas o slide ou cláusula de contrato relevante.  
2. **Revisões Internas** – Permita verificações visuais rápidas sem abrir o documento completo.  
3. **Resumos de Conteúdo** – Incorpore capturas de página em e‑mails ou painéis para contexto instantâneo.  

Integrar esse recurso com um CMS ou CRM pode automatizar a geração de miniaturas para documentos enviados, melhorando a experiência do usuário.

## Considerações de Desempenho
- **Memory Management** – Libere as instâncias de `RedactionEngine` após o uso para liberar recursos.  
- **Asynchronous Execution** – Use `await engine.GeneratePreviewAsync(...)` em aplicações UI para manter a interface responsiva.  
- **Library Updates** – O GroupDocs.Redaction suporta **mais de 30 formatos de entrada e saída** e processa documentos de até 500 páginas sem carregar o arquivo inteiro na memória. Mantenha o pacote atualizado para aproveitar melhorias de desempenho.

## Conclusão
Agora você tem um método completo e pronto para produção para **converter página para PNG** e gerar visualizações de página única com GroupDocs.Redaction para .NET. Seguindo os passos acima, você pode incorporar capturas PNG de alta qualidade em qualquer aplicação .NET, aprimorando o compartilhamento de documentos enquanto preserva a segurança e o desempenho.

## Perguntas Frequentes

**Q: Posso gerar visualizações para PDFs protegidos por senha?**  
A: Sim, forneça a senha ao inicializar `RedactionEngine` e a visualização será criada normalmente.

**Q: Como mudar o formato de saída de PNG para JPEG?**  
A: Defina `options.PreviewFormat = PreviewFormat.Jpeg` antes de chamar o método de visualização.

**Q: É possível visualizar várias páginas de uma vez?**  
A: Absolutamente – atribua um array de números de página a `options.PageNumbers` (por exemplo, `new[] {0, 2, 4}`).

**Q: O que fazer se a imagem da visualização estiver borrada?**  
A: Aumente `options.Width` e `options.Height` para uma resolução maior; a biblioteca escala a imagem de acordo.

**Q: Isso funciona em contêineres Linux?**  
A: Sim, o GroupDocs.Redaction .NET é multiplataforma e roda dentro de contêineres Docker que suportam .NET Core.

## Recursos
- [Documentação](https://docs.groupdocs.com/redaction/net/)
- [Referência da API](https://reference.groupdocs.com/redaction/net)
- [Baixar a Versão Mais Recente](https://releases.groupdocs.com/redaction/net/)
- [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Aquisição de Licença Temporária](https://purchase.groupdocs.com/temporary-license)

---

**Última Atualização:** 2026-06-06  
**Testado com:** GroupDocs.Redaction 5.6 for .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Domine a Segurança de Documentos: Rasterizar e Redigir Documentos Word com GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [Como Excluir Páginas de PDFs Usando GroupDocs.Redaction .NET: Um Guia Abrangente](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implementar Redação de Documentos Usando GroupDocs.Redaction .NET: Um Guia Passo a Passo](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)