---
date: '2026-07-20'
description: Aprenda como redactar documentos, ocultar informações sensíveis e salvar
  arquivos redactados em um memory stream usando GroupDocs.Redaction para .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: Como redactar documentos com GroupDocs.Redaction para .NET. Siga este
  guia passo a passo para ocultar informações sensíveis e salvar o arquivo redactado
  em um memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: Como Redactar Documentos com GroupDocs.Redaction para .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: Como Redactar Documentos com GroupDocs.Redaction para .NET – Um Guia Completo
type: docs
url: /pt/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# Como Redigir Documentos com GroupDocs.Redaction para .NET

Em ambientes empresariais modernos, **como redigir documentos** é uma habilidade crítica para proteger dados pessoais, segredos comerciais e informações relacionadas à conformidade. Este guia orienta você a censurar informações sensíveis de arquivos Word, PDF ou de imagem e, em seguida, salvar a saída censurada diretamente em um memory stream — tudo com GroupDocs.Redaction para .NET.

## Respostas Rápidas
- **O que a censura faz?** Ela substitui permanentemente o conteúdo selecionado por um placeholder ou o remove, garantindo que os dados nunca possam ser recuperados.  
- **Quais formatos são suportados?** Mais de 30 tipos de arquivo, incluindo PDF, DOCX, PPTX e formatos de imagem comuns.  
- **Posso censurar sem gravar no disco?** Sim — salve o resultado em um `MemoryStream` para processamento em memória.  
- **Preciso de licença para produção?** Uma licença completa é necessária para uso em produção; um teste gratuito está disponível para avaliação.  
- **É compatível com .NET Core?** Absolutamente — GroupDocs.Redaction funciona com .NET Framework 4.6+, .NET Core 3.1+ e .NET 5/6/7.

## O que é Redação de Documentos?
A redação de documentos remove ou obscurece permanentemente texto confidencial, imagens e metadados de um arquivo, garantindo que o conteúdo oculto não possa ser recuperado, visualizado ou extraído posteriormente. Ela substitui os elementos sensíveis por um placeholder, como um retângulo preto ou texto personalizado, e atualiza a estrutura do documento para que os dados censurados sejam irrecuperáveis.

## Por que Usar GroupDocs.Redaction para Redigir Documentos?
GroupDocs.Redaction suporta **30+ formatos de arquivo** e pode lidar com arquivos de até **2 GB** sem carregar o documento inteiro na memória, oferecendo um **tempo de processamento 30 % mais rápido** em comparação com muitos concorrentes. Sua API permite aplicar redações por frase exata, expressão regular ou baseadas em imagem com uma única chamada de método, tornando‑a a escolha mais eficiente para desenvolvedores .NET.

## Pré-requisitos
- **GroupDocs.Redaction** pacote NuGet (versão mais recente).  
- .NET Framework 4.6+ **ou** .NET Core 3.1+ instalado.  
- Uma IDE compatível com C#, como Visual Studio 2022.  
- Conhecimento básico de C# e familiaridade com I/O de arquivos.

### Bibliotecas e Versões Necessárias
- **GroupDocs.Redaction** – sempre use a versão mais recente para acessar os últimos algoritmos de redação e patches de segurança.  
- **System.IO** – para manipulação de streams (integrado ao .NET).

### Etapas para Aquisição de Licença
- **Teste Gratuito:** Inscreva‑se no site da GroupDocs para um teste de 30 dias.  
- **Licença Temporária:** Solicite uma chave temporária para testes de desenvolvimento.  
- **Licença Completa:** Compre uma licença de produção para uso ilimitado.

## Inicialização e Configuração Básicas
A classe `Redactor` é o ponto de entrada para todas as operações de redação no GroupDocs.Redaction. Após instalar o pacote NuGet, você instancia `Redactor` com o caminho para o documento de origem.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Como Redigir Texto Específico em um Documento?
Para redigir texto específico, carregue o arquivo de origem com uma instância `Redactor`, então aplique um `ExactPhraseRedaction` que visa a string exata que você deseja ocultar. A API varre o documento, substitui cada correspondência pela sobreposição escolhida e registra as alterações em um log de mudanças, permitindo que você verifique a redação antes de salvar.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

A classe `ExactPhraseRedaction` substitui cada ocorrência da frase exata por um retângulo preto (ou qualquer placeholder personalizado que você configure).  

**Passo a Passo:**
1. **Carregar** – Crie uma instância `Redactor` apontando para seu arquivo.  
2. **Aplicar** – Chame `Apply` com um `ExactPhraseRedaction` (ou outro tipo de redação).  
3. **Inspecionar** – Revise `RedactorChangeLog` para confirmar quantas correspondências foram encontradas e substituídas.  

## Como Salvar um Documento Redigido em um Memory Stream?
`MemoryStream` é um stream .NET que armazena dados na memória, permitindo leitura/escrita rápida sem I/O de disco. Usando o método `Save`, você pode direcionar a saída redigida para um `MemoryStream`, que pode então ser enviado pela rede, armazenado em um banco de dados ou retornado diretamente de um endpoint de API sem criar arquivos temporários.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Pontos Principais:**
- O método `Save` grava a saída redigida em qualquer implementação de `Stream`, incluindo `MemoryStream`.  
- Nenhum arquivo temporário é criado, o que melhora a segurança e o desempenho.  
- Você pode combinar isso com o `FileStreamResult` do ASP.NET Core para retornar o arquivo diretamente ao navegador.

## Armadilhas Comuns e Soluções
| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Redação não aplicada** | O caso da frase difere da origem. | Use `ExactPhraseRedaction("John Doe", caseSensitive: false)` ou uma redação por expressão regular para correspondência flexível. |
| **Arquivos grandes causam OutOfMemory** | Tentativa de carregar o arquivo inteiro na memória. | GroupDocs.Redaction transmite dados internamente; certifique‑se de usar a versão mais recente que processa arquivos em blocos. |
| **Arquivo salvo está corrompido** | Stream não foi redefinido antes de enviar. | Após `redactor.Save(stream)`, defina `stream.Position = 0` antes de ler ou retorná‑lo. |

## Perguntas Frequentes

**Q: Posso redigir arquivos PDF usando a mesma API?**  
A: Sim — GroupDocs.Redaction trata PDF, DOCX, PPTX e muitos formatos de imagem de forma uniforme; basta apontar `Redactor` para um arquivo PDF.

**Q: A redação sobrevive após converter o documento para outro formato?**  
A: Absolutamente — uma vez redigido, o conteúdo é removido permanentemente, independentemente de conversões subsequentes.

**Q: Como personalizar a aparência da redação?**  
A: Use `RedactionOptions` para definir a cor da sobreposição, opacidade ou substituir o texto por uma string personalizada.

**Q: É possível redigir usando expressões regulares?**  
A: Sim — `RegexRedaction` permite definir padrões como números de cartão de crédito ou endereços de e‑mail.

**Q: Quais versões do .NET são oficialmente suportadas?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 e .NET 7.

---

**Última Atualização:** 2026-07-20  
**Testado com:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Tutoriais Relacionados

- [Como Carregar e Redigir Documentos Usando GroupDocs.Redaction .NET&#58; Um Guia Completo](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Salvar Documentos Redigidos no Formato Original Usando GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Redação Segura de Documentos em .NET Usando Streams&#58; Um Guia para GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)