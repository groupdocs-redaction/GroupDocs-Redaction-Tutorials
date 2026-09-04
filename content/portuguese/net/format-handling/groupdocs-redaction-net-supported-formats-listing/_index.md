---
date: '2026-07-20'
description: Aprenda a listar formatos usando GroupDocs.Redaction .NET, integre o
  recurso ao seu fluxo de trabalho de documentos e melhore o desempenho.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Descubra como listar formatos usando GroupDocs.Redaction .NET, veja
  um guia passo a passo e obtenha dicas para desempenho ideal em suas aplicações .NET.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: Como listar formatos com GroupDocs.Redaction .NET
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
title: Como listar formatos com GroupDocs.Redaction .NET
type: docs
url: /pt/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# Como Listar Formatos com GroupDocs.Redaction .NET

Gerenciar uma ampla variedade de tipos de documentos é uma realidade diária para desenvolvedores que criam aplicações centradas em documentos. Neste tutorial você aprenderá **como listar formatos** que o GroupDocs.Redaction .NET pode manipular, para que possa validar arquivos antes do processamento, apresentar aos usuários opções precisas e manter seu fluxo de trabalho eficiente.

## Introdução

O manuseio eficiente de documentos começa com saber exatamente quais tipos de arquivo sua biblioteca suporta. O GroupDocs.Redaction fornece um método embutido para recuperar essas informações, permitindo que você construa elementos de UI dinâmicos, aplique regras de validação e evite erros em tempo de execução. Abaixo você encontrará tudo o que precisa para começar, desde a instalação até trechos de código práticos e dicas de desempenho.

### Respostas Rápidas
- **O que significa “como listar formatos”?** Refere‑se a recuperar a coleção de extensões de arquivo que o GroupDocs.Redaction pode processar.  
- **Preciso de licença?** Sim, uma licença válida do GroupDocs.Redaction é necessária para uso em produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **Quantos formatos estão disponíveis?** Mais de 30 formatos de entrada e saída são suportados prontamente.  
- **É necessária alguma configuração especial?** Nenhuma configuração extra é necessária além da inicialização padrão da biblioteca.

## O que é “como listar formatos”?

Envolve chamar a API FileType da biblioteca para obter uma coleção onde cada entrada contém a extensão do arquivo e um nome legível. Os desenvolvedores podem então iterar essa coleção para criar regras de validação, preencher menus suspensos da UI ou registrar tipos suportados, garantindo que apenas documentos compatíveis sejam processados.

## Por que listar formatos com GroupDocs.Redaction?

O GroupDocs.Redaction suporta **30+** tipos de arquivo distintos — incluindo PDF, DOCX, PPTX e formatos de imagem — permitindo que você manipule a maioria dos documentos corporativos sem conversores de terceiros. Ao listar programaticamente esses formatos, você elimina suposições, reduz tickets de suporte e garante que apenas arquivos compatíveis entrem no seu pipeline de processamento.

## Pré-requisitos

- **GroupDocs.Redaction for .NET** – baixe o pacote mais recente no site oficial.  
- **.NET Framework ou .NET Core** – compatível com seu ambiente de desenvolvimento.  
- **Visual Studio** (ou qualquer IDE compatível com C#).  
- Familiaridade básica com a sintaxe C#.

## Configurando GroupDocs.Redaction para .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Gerenciador de Pacotes
`Install-Package GroupDocs.Redaction`

### UI do Gerenciador de Pacotes NuGet
- Procure por **“GroupDocs.Redaction”** e instale a versão mais recente.

### Aquisição de Licença
O GroupDocs oferece um teste gratuito, uma licença temporária para avaliação ou opções de compra completa. Visite o site do GroupDocs para obter o arquivo de licença apropriado.

### Inicialização e Configuração Básicas
Depois de adicionar o pacote, referencie o namespace e crie uma instância `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Guia de Implementação

### Como listar formatos com GroupDocs.Redaction .NET?
Carregue a biblioteca, chame o helper estático e ordene os resultados — isso fornece uma coleção pronta para uso em apenas duas linhas de código. Use `FileType.GetSupportedFileFormats()` para recuperar um `IEnumerable<FileType>` que inclui a extensão e o nome de exibição de cada formato, então ordene por extensão para obter uma lista de UI limpa.

### Recuperando Formatos de Arquivo Compatíveis

#### Visão Geral
O objetivo é obter uma lista de tipos de arquivo que o GroupDocs.Redaction pode manipular, facilitando a integração em lógica de validação, menus suspensos da UI ou mecanismos de registro.

#### Implementação Passo a Passo

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` retorna todos os formatos que a biblioteca reconhece. O método faz parte da classe `GroupDocs.Redaction.FileType`, que encapsula metadados como extensão de arquivo e nome amigável.

**2. Display Supported File Types**  
Itere sobre a coleção e exiba a extensão e a descrição de cada formato. Exemplo de código inline:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

O snippet imprime uma lista ordenada como “.pdf – Portable Document Format”, tornando‑a perfeita para preencher elementos de UI.

### Dicas de Solução de Problemas
- **Missing Package** – Verifique a referência do pacote NuGet e restaure os pacotes se necessário.  
- **Incorrect License Path** – Garanta que o arquivo de licença seja copiado para o diretório de saída ou forneça um caminho absoluto.  
- **Unsupported Extension** – Se um formato não aparecer na lista, confirme que está usando a versão mais recente da biblioteca; versões mais novas adicionam formatos adicionais.

## Aplicações Práticas
Entender os formatos de arquivo suportados desbloqueia vários cenários reais:

1. **Sistemas de Gerenciamento de Documentos** – Valide uploads contra a lista suportada para evitar falhas de processamento.  
2. **Segurança de Conteúdo** – Aplique regras de redação apenas a tipos de arquivo que o motor pode modificar com segurança.  
3. **Pipelines de Processamento em Lote** – Filtre grandes lotes de arquivos antes de invocar a redação, economizando CPU e memória.

## Considerações de Desempenho
- **Memory Footprint** – Listar formatos é uma operação leve; não carrega nenhum documento na memória.  
- **Batch Operations** – Ao processar centenas de arquivos, recupere a lista de formatos uma única vez e reutilize‑a para evitar chamadas redundantes.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` é thread‑safe e pode ser chamada de tarefas paralelas sem sincronização.

## Conclusão
Agora você tem uma abordagem completa e pronta para produção para **como listar formatos** usando GroupDocs.Redaction .NET. Ao integrar esse recurso, você pode aprimorar a validação, melhorar a experiência do usuário e manter seus pipelines de documentos robustos.

### Próximos Passos
- Explore a API `Redactor` para aplicar regras de redação com base no tipo de arquivo.  
- Combine a lista de formatos com um menu suspenso front‑end para seleção de arquivos sem atritos.  
- Revise o guia de desempenho para otimizar trabalhos em lote de grande escala.

## Perguntas Frequentes

**Q: Posso recuperar a lista de formatos sem inicializar uma instância Redactor?**  
A: Sim, `FileType.GetSupportedFileFormats()` é estático e não requer um objeto `Redactor`.

**Q: A lista inclui formatos de entrada e saída?**  
A: O método retorna todos os formatos que a biblioteca pode ler e escrever; cada `FileType` inclui um sinalizador `CanRead` e `CanWrite`.

**Q: Com que frequência a lista de formatos suportados é atualizada?**  
A: O GroupDocs lança atualizações de formatos a cada nova versão da biblioteca; verificar a lista em tempo de execução garante que você sempre tenha o conjunto mais recente.

**Q: Existe uma forma de filtrar apenas formatos compatíveis com PDF?**  
A: Sim, filtre a coleção onde `format.Extension == ".pdf"` ou onde `format.Name.Contains("PDF")`.

**Q: Essa abordagem funciona no .NET Core 2.1?**  
A: O método requer .NET Core 3.1 ou posterior; runtimes mais antigos não são suportados.

## Seção de FAQ
1. **Como instalo o GroupDocs.Redaction para .NET?**  
   Use o comando CLI `dotnet add package GroupDocs.Redaction` ou instale via UI do Gerenciador de Pacotes NuGet.  
2. **Quais são os problemas comuns ao recuperar formatos suportados?**  
   Certifique‑se de que todas as dependências foram restauradas e que você está referenciando o namespace correto (`GroupDocs.Redaction`).  
3. **Posso usar esse recurso em aplicações que não sejam .NET?**  
   Este tutorial foca em .NET, mas o GroupDocs fornece APIs semelhantes para Java, Python e outras plataformas.  
4. **Como otimizar o desempenho ao usar o GroupDocs.Redaction?**  
   Reutilize a lista de formatos, evite carregar documentos completos quando apenas verificar compatibilidade e monitore o uso de memória durante trabalhos em lote.  
5. **Quais tipos de arquivo o GroupDocs.Redaction suporta?**  
   A biblioteca suporta mais de 30 formatos, incluindo PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG e muitos outros. Use `FileType.GetSupportedFileFormats()` para ver a lista completa.

## Recursos
- [Documentação](https://docs.groupdocs.com/redaction/net/)
- [Referência da API](https://reference.groupdocs.com/redaction/net)
- [Baixar GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Fórum de Suporte Gratuito](https://forum.groupdocs.com/c/redaction/33)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última Atualização:** 2026-07-20  
**Testado com:** GroupDocs.Redaction 4.2.0 for .NET  
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

## Tutoriais Relacionados

- [Tutoriais de Manipulação de Formatos para GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Tutoriais de Carregamento de Documentos com GroupDocs.Redaction para .NET](/redaction/net/document-loading/)
- [Tutoriais de Salvamento de Documentos para GroupDocs.Redaction .NET](/redaction/net/document-saving/)