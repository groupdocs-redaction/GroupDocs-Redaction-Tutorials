---
date: '2026-08-20'
description: Aprenda como redigir texto com GroupDocs.Redaction Java, salvar como
  PDF rasterizado, substituir frases exatas e aplicar configurações personalizadas
  de PDF.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: Como redigir texto com GroupDocs.Redaction Java. Este guia mostra
  a substituição de frases exatas, a criação de PDF rasterizado e a conformidade com
  PDF/A‑1a em poucos passos.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: Como redigir texto com a biblioteca GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: Como redigir texto com GroupDocs.Redaction Java
type: docs
url: /pt/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# Como redigir texto com GroupDocs.Redaction Java

Em aplicações modernas, **como redigir texto** em um documento mantendo o fluxo de trabalho rápido e em conformidade é um desafio frequente para desenvolvedores, auditores e oficiais de conformidade. Este tutorial orienta você a usar o GroupDocs.Redaction para Java para localizar frases exatas, substituí‑las por sobreposições seguras e, finalmente, exportar o resultado como um documento PDF/A‑1a rasterizado — perfeito para arquivamento ou distribuição legal.

## Respostas rápidas
- **Qual é a classe principal para redaction?** `Redactor`  
- **Posso substituir uma frase por uma sobreposição colorida?** Sim, usando `ExactPhraseRedaction` e `ReplacementOptions`.  
- **Como gero um PDF rasterizado?** Ative a rasterização via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Qual nível de conformidade PDF é usado no exemplo?** `PdfComplianceLevel.PdfA1a`.  
- **Preciso de uma licença para uso em produção?** Uma licença válida do GroupDocs.Redaction é necessária para implantações em produção.

## O que é “como redigir texto” em Java?
`Redaction` é a remoção permanente ou ocultação de conteúdo sensível de um arquivo de modo que não possa ser recuperado ou lido posteriormente. Com o GroupDocs.Redaction você pode programaticamente buscar uma frase exata — como um número de segurança social ou um código de projeto confidencial — e substituí‑la por uma sobreposição vermelha, caixa preta ou qualquer elemento visual personalizado, garantindo que os dados originais sejam irrecuperáveis.

## Por que usar GroupDocs.Redaction para Java?
GroupDocs.Redaction suporta **mais de 30 formatos de entrada e saída** (PDF, DOCX, PPTX, XLSX, HTML e tipos de imagem) e pode processar documentos com centenas de páginas sem carregar todo o arquivo na memória. Seu algoritmo de correspondência de frase exata reduz falsos positivos em > 95 % comparado a buscas genéricas por palavras‑chave, e o mecanismo de rasterização integrado permite produzir arquivos PDF/A‑1a que são totalmente baseados em imagens para preservação a longo prazo.

## Pré‑requisitos
Antes de começar, assegure‑se de que você tem:

- **GroupDocs.Redaction for Java** (v24.9 ou mais recente).  
- **Java Development Kit (JDK) 8+**.  
- Uma IDE como IntelliJ IDEA, Eclipse ou NetBeans.  
- Maven para gerenciamento de dependências.  

### Bibliotecas e dependências necessárias
- GroupDocs.Redaction for Java – adicione o repositório e a dependência ao seu `pom.xml` (veja a seção de configuração Maven).  
- Opcional: qualquer framework de logging que preferir (SLF4J, Log4j, etc.).

### Pré‑requisitos de conhecimento
- Sintaxe básica de Java e I/O de arquivos.  
- Familiaridade com a estrutura `pom.xml` do Maven.

## Configurando GroupDocs.Redaction para Java
### Configuração Maven
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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

### Download direto
Alternatively, you can download the latest version directly from [lançamentos do GroupDocs.Redaction para Java](https://releases.groupdocs.com/redaction/java/).

### Aquisição de licença
- **Teste gratuito** – explore a API sem chave de licença.  
- **Licença temporária** – use para avaliação prolongada.  
- **Licença completa** – necessária para ambientes de produção.

### Inicialização e configuração básicas
A classe `Redactor` é o ponto de entrada para todas as operações de redaction. Ela carrega um documento, aplica regras de redaction e salva o resultado.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Como redigir texto – exemplo de frase exata
Redactor is the primary class that loads a document and applies redaction rules. ExactPhraseRedaction defines a rule that matches a specific string. This example demonstrates loading a file, creating an ExactPhraseRedaction rule, and executing the redaction in a single step, providing a concise workflow for developers while ensuring the original content is permanently obscured.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## Como salvar como PDF rasterizado
SaveOptions is the configuration object that controls how a document is saved. By enabling its rasterization feature and selecting PDF/A‑1a compliance, you can produce an image‑only PDF where each page is rendered as a bitmap, meeting archival standards and preventing text extraction.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Aplicações práticas
1. **Redaction de dados sensíveis** – ocultar automaticamente identificadores pessoais antes de compartilhar contratos.  
2. **Arquivamento de documentos** – converter relatórios finalizados para PDF/A rasterizado para conformidade a longo prazo.  
3. **Atualização em massa de conteúdo** – substituir terminologia desatualizada em centenas de arquivos com um único script.

## Considerações de desempenho
- **Feche o `Redactor`** após cada operação para liberar manipuladores de arquivos e memória.  
- **Processamento em lote** – carregue uma lista de arquivos e itere sobre eles, reutilizando uma única instância de `Redactor` quando possível.  
- **Monitore recursos** – use ferramentas de profiling Java para observar o uso de CPU e heap durante redactions em grande escala.

## Perguntas frequentes

**Q: Como instalo o GroupDocs.Redaction em um projeto Maven?**  
A: Adicione o repositório GroupDocs e a dependência `groupdocs-redaction` ao seu `pom.xml` conforme mostrado na seção de Configuração Maven.

**Q: Posso redigir texto de arquivos PDF usando esta biblioteca?**  
A: Sim, o GroupDocs.Redaction suporta PDF, DOCX, PPTX e muitos outros formatos.

**Q: O que acontece se a frase exata não for encontrada?**  
A: O `RedactorChangeLog` retornará um status de `Failed`. Verifique a ortografia da frase e a sensibilidade a maiúsculas/minúsculas.

**Q: Como posso lidar com documentos muito grandes de forma eficiente?**  
A: Processá‑los em intervalos de páginas menores, habilitar a rasterização apenas onde necessário e sempre fechar o `Redactor` para liberar recursos.

**Q: É possível salvar PDFs rasterizados com intervalos de páginas específicos?**  
A: Absolutamente. Use `options.getRasterization().setPageIndex()` e `setPageCount()` para direcionar as páginas exatas que você deseja rasterizar.

## Conclusão
Você agora tem um guia completo, de ponta a ponta, sobre **como redigir texto** com GroupDocs.Redaction Java e **salvar como PDF rasterizado**. Seguindo estas etapas, você pode proteger informações sensíveis, atender a rigorosos padrões de conformidade e manter seus serviços Java performáticos em escala.

**Próximos passos**  
- Mergulhe mais fundo na API explorando a [documentação oficial](https://docs.groupdocs.com/redaction/java/).  
- Experimente outros tipos de redaction como `RegexRedaction` e `ImageRedaction`.  
- Participe da comunidade no [Fórum de Suporte GroupDocs](https://forum.groupdocs.com/c/redaction/33) para dicas e boas práticas.

---

**Última atualização:** 2026-08-20  
**Testado com:** GroupDocs.Redaction Java 24.9  
**Autor:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Tutoriais Relacionados

- [Como Redigir Texto com GroupDocs.Redaction para Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Tutorial de Redaction de Texto Java: Guia com GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)