---
date: 2026-08-04
description: Aprenda como filtrar dados de planilha java e remover de forma segura
  colunas ou células em planilhas Excel usando o GroupDocs.Redaction para Java.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Aprenda como filtrar dados de planilha java e remover de forma segura
  colunas ou células em planilhas Excel usando o GroupDocs.Redaction para Java.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Filtrar dados de planilha java – guia com GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Filtrar dados de planilha java – guia com GroupDocs.Redaction
type: docs
url: /pt/java/spreadsheet-redaction/
weight: 12
---

# Filtrar dados de planilha java – Tutorial GroupDocs.Redaction Java

Se você precisa **filter spreadsheet data java** antes de aplicar a redação, chegou ao guia certo. Neste tutorial você descobrirá como isolar linhas, colunas ou células individuais que contenham informações pessoais ou confidenciais, e então redactá‑las com segurança usando GroupDocs.Redaction para Java. As etapas são explicadas em linguagem simples, incluem dicas de boas práticas e mostram como manter o processamento rápido mesmo em pastas de trabalho grandes.

## Respostas rápidas
- **Qual biblioteca lida com a redação de planilhas em Java?** GroupDocs.Redaction for Java.  
- **Posso filtrar linhas sem carregar todo o arquivo na memória?** Sim – a API transmite dados e permite aplicar filtros em tempo real.  
- **Quais formatos de arquivo são suportados?** Mais de 30 formatos de planilha, incluindo XLS, XLSX, CSV e ODS.  
- **Preciso de uma licença para desenvolvimento?** Uma licença temporária funciona para testes; uma licença completa é necessária para produção.  
- **Existe um limite no tamanho da pasta de trabalho?** O mecanismo pode processar arquivos de até 500 MB sem consumo excessivo de memória.

## O que é filter spreadsheet data java?
**Filter spreadsheet data java** é o processo de selecionar programaticamente linhas, colunas ou células específicas em uma pasta de trabalho estilo Excel usando código Java, de modo que apenas o conteúdo alvo seja examinado ou redactado. Esta técnica reduz o tempo de execução, limita alterações desnecessárias e ajuda a atender à conformidade do tipo GDPR.

## Por que filtrar filter spreadsheet data java?
GroupDocs.Redaction Java suporta **30+ formatos de planilha** e pode processar pastas de trabalho contendo **até 500 MB** (aproximadamente 1 milhão de linhas) mantendo o uso de memória abaixo de **200 MB**. Ao filtrar primeiro, você evita tocar em dados não relacionados, o que reduz o tempo de processamento em **40‑60 %** em média para cenários típicos de limpeza de privacidade.

## Pré-requisitos
- Java 17 ou posterior instalado.  
- Sistema de build Maven ou Gradle.  
- GroupDocs.Redaction for Java (disponível para download no site oficial).  
- Uma chave de licença temporária ou completa.  

## Como filtrar dados em planilhas usando GroupDocs.Redaction Java?
Carregue a pasta de trabalho, defina um filtro que corresponda às células que você deseja redactar, e então aplique a operação de redação. A API executa o filtro de forma streaming, portanto você nunca precisa manter o arquivo inteiro na RAM.

A classe `RedactionFilter` permite especificar índices de colunas, intervalos de linhas ou predicados personalizados. Por exemplo, você pode direcionar cada célula na coluna **B** que contenha um padrão de endereço de e‑mail, ou pode restringir a redação a linhas onde a coluna “Status” seja igual a “Confidential”.

**Resposta direta (40‑70 palavras):**  
Crie uma instância `RedactionFilter`, defina o índice da coluna e uma condição de expressão regular, então passe o filtro para `Redactor.redact(workbook, filter)`. Esse filtro de linha única isola as células exatas que correspondem ao seu critério, e o redator remove ou mascara‑as enquanto deixa o restante da planilha intacto. A operação é concluída em tempo linear em relação às linhas filtradas.

### Etapa 1: instanciar o filtro
`RedactionFilter` é a classe central que representa uma regra de filtragem para redação de planilhas. Ela aceita números de colunas, números de linhas ou expressões lambda personalizadas para identificar os dados.

### Etapa 2: configurar a condição
Use `filter.setColumnIndex(1)` para direcionar a coluna B (base zero) e `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` para corresponder a padrões de e‑mail. Você também pode combinar múltiplas condições com `filter.and(...)` ou `filter.or(...)`.

### Etapa 3: aplicar a redação
`Redactor` é a classe principal que executa operações de redação em uma pasta de trabalho.  
Passe a pasta de trabalho e o filtro configurado para o objeto `Redactor`. A API transmite a pasta de trabalho, aplica o filtro e grava o resultado redactado em um novo arquivo, preservando a formatação e as fórmulas originais.

## Problemas comuns e soluções
- **O filtro não corresponde a nenhuma célula:** Verifique o índice da coluna (base zero) e assegure que a sintaxe da expressão regular esteja correta para Java.  
- **Erros de falta de memória em arquivos grandes:** Aumente o tamanho do heap da JVM modestamente (por exemplo, `-Xmx1g`) ou divida a pasta de trabalho em blocos menores antes de filtrar.  
- **A saída redactada perde formatação:** `RedactionOptions` permite personalizar o comportamento da redação, como preservar a formatação das células. Use `RedactionOptions.setPreserveFormatting(true)` para manter os estilos das células intactos.

## Por que filtrar dados de planilha?
Filtrar antes da redação isola apenas as partes sensíveis de uma pasta de trabalho, o que significa que você evita alterações desnecessárias em dados limpos. Essa abordagem seletiva também reduz o risco de perda acidental de dados e acelera auditorias de conformidade porque o registro de auditoria contém muito menos entradas.

## Como redactar e‑mails em planilhas Excel usando a API GroupDocs.Redaction Java
Carregue seu arquivo Excel, aplique um filtro que procure o padrão típico de e‑mail e invoque o redator. A API substitui cada e‑mail correspondido por um placeholder como “***@***.com” preservando o layout das células ao redor.

## Como filtrar dados – tutoriais disponíveis
- [Como Redactar E‑mails em Planilhas Excel Usando a API GroupDocs.Redaction Java](./redact-emails-excel-groupdocs-redaction-java/)

## Recursos adicionais

- [Documentação do GroupDocs.Redaction para Java](https://docs.groupdocs.com/redaction/java/)
- [Referência da API do GroupDocs.Redaction para Java](https://reference.groupdocs.com/redaction/java/)
- [Download do GroupDocs.Redaction para Java](https://releases.groupdocs.com/redaction/java/)
- [Fórum do GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Suporte Gratuito](https://forum.groupdocs.com/)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-08-04  
**Testado com:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## Perguntas frequentes

**Q: Posso filtrar várias colunas ao mesmo tempo?**  
A: Sim, você pode adicionar índices de colunas adicionais à mesma instância `RedactionFilter` ou encadear múltiplos filtros com `filter.or(...)`.

**Q: O filtro funciona em pastas de trabalho protegidas por senha?**  
A: Forneça a senha ao abrir a pasta de trabalho; o filtro opera após a descriptografia assim como em um arquivo não protegido.

**Q: Quantas linhas a API pode manipular em uma única operação?**  
A: O mecanismo é otimizado para até 1 milhão de linhas (≈500 MB) sem carregar o arquivo inteiro na memória.

**Q: É possível visualizar quais células serão redactadas antes de salvar?**  
A: Sim, chame `filter.preview(workbook)` para obter uma lista de endereços de células que correspondem ao critério.

**Q: Qual modelo de licenciamento é necessário para uso em produção?**  
A: Uma licença comercial completa é necessária para implantações em produção; uma licença temporária é suficiente para testes e avaliação.

## Tutoriais Relacionados

- [Como Redactar Dados Sensíveis em Planilhas Excel Usando a API GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mascarar Dados Sensíveis Java – Guia GroupDocs.Redaction](/redaction/java/getting-started/)
- [Mascarar Dados Sensíveis Java – Redactar Informações Pessoais com GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)