---
date: '2026-08-14'
description: Como remover texto em documentos Java usando GroupDocs.Redaction – mascare
  informações pessoais e substitua texto sensível de forma eficiente.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: Como remover texto com GroupDocs.Redaction para Java permite que você
  mascare permanentemente dados pessoais e substitua cadeias sensíveis em PDFs, DOCX
  e outros, garantindo conformidade com GDPR e HIPAA.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: Como remover texto com GroupDocs.Redaction para Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: Como remover texto com GroupDocs.Redaction para Java
type: docs
url: /pt/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Como redigir texto com GroupDocs.Redaction para Java

Neste tutorial, você aprenderá **como redigir texto** em documentos baseados em Java usando o GroupDocs.Redaction. Você verá como mascarar informações pessoais, substituir strings sensíveis por placeholders seguros e processar vários arquivos de forma amigável a lotes. Ao final, você terá uma solução pronta para produção que protege a privacidade, atende aos requisitos GDPR/HIPAA e integra-se perfeitamente a aplicações Java existentes.

## Respostas rápidas
- **Qual biblioteca é usada?** GroupDocs.Redaction for Java.  
- **Posso mascarar informações pessoais?** Sim – use a redação de frase exata com opções de substituição.  
- **O processamento em lote é suportado?** Absolutamente, você pode percorrer vários arquivos com a mesma instância de Redactor.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença comercial é necessária para produção.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.

## O que é “como redigir texto”?

A redação remove ou obscurece permanentemente dados confidenciais de um documento. Com o GroupDocs.Redaction, você pode localizar strings específicas, substituí‑las por placeholders seguros e salvar o arquivo sanitizado — tudo sem edição manual.

## Por que usar GroupDocs.Redaction para Java?

GroupDocs.Redaction para Java suporta **mais de 50 formatos de entrada e saída** (incluindo PDF, DOCX, XLSX, PPTX, TXT, RTF) e pode processar arquivos com centenas de páginas sem carregar o documento inteiro na memória, oferecendo operações em lote de alta taxa de transferência em hardware de servidor padrão.

## Pré-requisitos
- **Java Development Kit (JDK):** Versão 8 ou mais recente.  
- **IDE:** IntelliJ IDEA, Eclipse ou qualquer editor compatível com Java.  
- **Maven:** Para gerenciamento de dependências.  
- **Conhecimento básico de Java:** Familiaridade com classes, métodos e tratamento de exceções.

## Configurando GroupDocs.Redaction para Java
Para começar, adicione a biblioteca ao seu projeto Maven.

### Configuração do Maven
Adicione o repositório e a dependência ao seu arquivo `pom.xml`:

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
Se preferir, obtenha o JAR mais recente em [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de licença
Você pode começar com um **Teste Gratuito**, solicitar uma **Licença Temporária** para testes estendidos ou adquirir uma **Licença Comercial** para uso em produção.

## Como redigir texto em documentos com GroupDocs.Redaction

As seções a seguir orientam você pelos passos exatos necessários para **mascarar informações pessoais** e **substituir texto sensível**.

### Etapa 1: inicializar o redator
`Redactor` é a classe principal que carrega um documento, aplica regras de redação e grava a saída.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Etapa 2: aplicar redação de frase exata
`ExactPhraseRedaction` procura por uma correspondência exata de string, enquanto `ReplacementOptions` define como o texto correspondido deve ser substituído.  

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parâmetros:**  
  - `"John Doe"` – o texto exato a ser redigido.  
  - `ReplacementOptions("[personal]")` – a string que substituirá o conteúdo original, efetivamente **mascarando informações pessoais**.

### Etapa 3: salvar o documento redigido
`Redactor.save` grava o documento modificado em um novo arquivo ou sobrescreve o original, preservando o formato original.  

```java
redactor.save();
```

### Etapa 4: limpar recursos
Sempre chame `Redactor.close()` para liberar recursos nativos e evitar vazamentos de memória.  

```java
finally {
    redactor.close();
}
```

## Como mascarar informações pessoais com um callback personalizado

Um callback personalizado permite reagir a cada evento de redação — útil para registro, substituições condicionais ou trilhas de auditoria.

### Crie uma classe de callback
`IRedactionCallback` define métodos que são invocados antes e depois de cada operação de redação.  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use o callback ao instanciar o Redactor
Passe sua implementação de callback via `RedactorSettings` para que o motor saiba invocá‑la durante o processamento.  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Aplicações práticas
- **Contratos legais:** Ocultar automaticamente nomes de clientes, SSNs ou cláusulas confidenciais antes de compartilhar rascunhos.  
- **Registros médicos:** **Mascarar informações pessoais** como identificadores de pacientes ao exportar registros para parceiros de pesquisa.  
- **Comunicações corporativas:** **Substituir texto sensível** como códigos de projetos internos antes da distribuição externa, garantindo que não haja vazamentos acidentais.

## Considerações de desempenho
Ao processar arquivos grandes ou numerosos, tenha estas dicas em mente:

- **Processamento em lote:** Percorra uma coleção de arquivos para reduzir a sobrecarga de inicialização.  
- **Gerenciamento de memória:** Libere o `Redactor` após cada arquivo; evite manter muitos documentos na memória simultaneamente.  
- **Perfilamento:** Use perfis de Java (por exemplo, VisualVM) para identificar gargalos em I/O ou na lógica de redação.

## Perguntas frequentes
**Q: Posso redigir texto de PDFs usando o GroupDocs.Redaction?**  
A: Sim, a biblioteca suporta PDF, DOCX, XLSX, PPTX e muitos outros formatos.

**Q: A redação é reversível?**  
A: Não. As redações removem permanentemente o conteúdo original, portanto mantenha um backup do arquivo fonte.

**Q: Como lidar com documentos muito grandes de forma eficiente?**  
A: Processá‑los em partes, usar modo em lote e monitorar o uso de memória com ferramentas de perfilamento.

**Q: Quais outros formatos de texto são suportados?**  
A: Além de DOCX e PDF, você pode redigir TXT, RTF, XLSX, PPTX e mais.

**Q: Posso integrar o GroupDocs.Redaction em fluxos de trabalho existentes?**  
A: Absolutamente. A API pode ser chamada a partir de serviços web, jobs em background ou pipelines CI/CD.

## Recursos
- **Documentação:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referência da API:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **Repositório GitHub:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Fórum de suporte gratuito:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Aplicação de licença temporária:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-08-14  
**Testado com:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Mascarar Dados Sensíveis Java – Guia GroupDocs.Redaction](/redaction/java/getting-started/)  
- [Mascarar Dados Sensíveis Java – Redigir Informações Pessoais com GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)  
- [Editar Docs Protegidos por Senha Java - Redigir Documentos Usando GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)