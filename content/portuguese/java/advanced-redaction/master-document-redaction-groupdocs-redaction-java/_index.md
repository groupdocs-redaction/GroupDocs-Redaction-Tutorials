---
date: '2026-11-02'
description: Aprenda como adicionar sufixo ao nome de arquivo em um tutorial de GroupDocs
  redaction Java usando Maven, carregamento em streaming, exclusão de anotações e
  opções de salvamento.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: Aprenda como adicionar sufixo ao nome de arquivo em um tutorial de
  GroupDocs redaction Java. Siga a configuração passo a passo do Maven, o carregamento
  em streaming e as opções de salvamento.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: Como adicionar sufixo ao nome de arquivo no GroupDocs redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: Como adicionar sufixo ao nome de arquivo no GroupDocs redaction Java
type: docs
url: /pt/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Como adicionar sufixo ao nome de arquivo no GroupDocs Redaction Java

Neste **groupdocs redaction java tutorial** você aprenderá como anexar automaticamente um sufixo ao nome do arquivo de saída ao redigir documentos com GroupDocs.Redaction. Adicionar um sufixo elimina a renomeação manual, reduz o risco de vazamento de arquivos não redigidos e se encaixa perfeitamente em pipelines CI/CD que dependem de convenções de nomenclatura. O guia orienta você através da configuração do Maven, carregamento de documentos por streaming, remoção de anotações e configuração das opções de salvamento — tudo com código conciso e pronto para produção.

## Respostas rápidas
- **O que faz “add suffix to filename”?**  
  Quando você habilita a opção de sufixo, o SDK anexa automaticamente uma string predefinida (por padrão “_redacted”) ao nome base do arquivo de saída antes da extensão. Isso deixa imediatamente claro quais arquivos foram processados, ajuda a prevenir a distribuição acidental de conteúdo original e simplifica a automação downstream que depende de padrões de nomenclatura.  
- **Posso carregar um documento a partir de stream?**  
  Sim—GroupDocs.Redaction suporta carregamento a partir de qualquer `InputStream`, perfeito para armazenamento em nuvem ou processamento em memória.  
- **Preciso de licença para este recurso?**  
  Um teste gratuito funciona para redação básica; uma licença temporária ou completa desbloqueia todas as opções avançadas, incluindo o tratamento de sufixo.  
- **Quais formatos são suportados?**  
  A biblioteca lida com DOCX, PDF, PPTX, XLSX e muitos mais.  
- **A rasterização é necessária para saída PDF?**  
  A rasterização é opcional; habilite-a quando precisar achatar o documento para segurança extra.

## O que faz “add suffix to filename”?

Quando você habilita a opção de sufixo, o SDK anexa automaticamente uma string predefinida (por padrão “_redacted”) ao nome base do arquivo de saída antes da extensão. Isso deixa imediatamente claro quais arquivos foram processados, ajuda a prevenir a distribuição acidental de conteúdo original e simplifica a automação downstream que depende de padrões de nomenclatura.

## Por que usar GroupDocs.Redaction para esta tarefa?

GroupDocs.Redaction oferece uma API Java de alto desempenho que combina ações de redação com opções flexíveis de manipulação de arquivos, como adição automática de sufixo, suporte a streaming e processamento em lote. Suporta mais de 50 formatos de entrada e saída e pode processar documentos com centenas de páginas sem carregar o arquivo inteiro na memória, garantindo baixo uso de memória e execução rápida.

## Pré-requisitos

- **Java Development Kit (JDK):** Versão 8 ou superior.  
- **GroupDocs.Redaction Library:** Biblioteca principal para tarefas de redação.  
- **IDE:** IntelliJ IDEA, Eclipse ou qualquer editor compatível com Java.  
- **Maven:** Para gerenciamento de dependências.  

### Pré-requisitos de conhecimento
Familiaridade com Java I/O e conceitos básicos de orientação a objetos facilitará o acompanhamento dos exemplos.

## Configurando GroupDocs.Redaction para Java

### Configuração do Maven
Inclua a seguinte configuração no seu arquivo `pom.xml` para acessar as bibliotecas GroupDocs via Maven:

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
Alternativamente, faça o download da versão mais recente diretamente em [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de licença
1. **Teste gratuito:** Acesse funcionalidades básicas sem restrições.  
2. **Licença temporária:** Obtenha uma licença temporária para explorar recursos avançados.  
3. **Compra:** Para uso a longo prazo, considere adquirir uma licença completa.

#### Inicialização e configuração básicas
Inicialize seu projeto adicionando as importações necessárias:

```java
import com.groupdocs.redaction.Redactor;
```

Com esta configuração, você está pronto para implementar funcionalidades de redação de documentos.

## Guia de implementação

### Recurso 1: carregar documento a partir de stream
**Visão geral:** Aprenda como carregar documentos em um `InputStream` para processamento.

`InputStream` é uma classe Java I/O que representa um fluxo de bytes, permitindo ler dados de arquivos, conexões de rede ou outras fontes sem carregar todo o conteúdo na memória.

#### Etapa 1.1: criar inputstream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Por quê:** Usar `InputStream` permite lidar com documentos armazenados em vários locais — buckets de nuvem, bancos de dados ou buffers em memória — sem precisar gravá‑los primeiro em disco. Essa abordagem é essencial quando você precisa **load document from stream** em arquiteturas de microsserviços.

### Recurso 2: aplicar remoção de anotação de redação
**Visão geral:** Remova anotações do seu documento usando o `DeleteAnnotationRedaction`.

`DeleteAnnotationRedaction` é uma operação de redação que remove todas as anotações — como comentários, realces e notas — do documento.

#### Etapa 2.1: aplicar deleteannotationredaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Por quê:** Esta etapa garante que quaisquer anotações sensíveis (comentários, realces ou notas ocultas) sejam removidas do documento, aprimorando a privacidade e a conformidade.

### Recurso 3: salvar documento com opções
**Visão geral:** Aprenda como salvar seu documento processado com opções específicas como rasterização e **add suffix filename java**.

`SaveOptions` encapsula configurações que controlam como o documento redigido é gravado, incluindo formato, rasterização e convenções de nomenclatura.

#### Etapa 3.1: configurar saveoptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Por quê:** Personalizar as opções de salvamento permite formatos de saída flexíveis e convenções de nomenclatura. Habilitar `setAddSuffix(true)` **adds suffix to filename**, tornando claro que o arquivo foi redigido.

## Como adicionar sufixo ao nome de arquivo java ao salvar um documento?

A classe `Redactor` é o componente central que carrega um documento e aplica operações de redação. `SaveOptions` define como o documento redigido é salvo, incluindo formato, rasterização e convenções de nomenclatura. Crie uma instância de `Redactor`, aplique as redações necessárias e, em seguida, configure um objeto `SaveOptions` com `setAddSuffix(true)`. Chame `redactor.save(outputPath, options)`. O SDK anexa automaticamente “_redacted” (ou o sufixo configurado) ao nome do arquivo, de modo que você nunca precise renomear o arquivo manualmente.

## Visão geral da dependência Maven do GroupDocs

A **groupdocs maven dependency** traz todo o SDK Redaction para o seu projeto com uma única entrada `<dependency>`. Ela lida com dependências transitivas, mantém as bibliotecas atualizadas e simplifica a automação de builds. Ao declarar a dependência em `pom.xml`, você evita o gerenciamento manual de JARs e garante compatibilidade com os patches de segurança mais recentes.

## Por que adicionar um sufixo é importante

Anexar um sufixo fornece confirmação visual imediata de que um arquivo foi processado, o que é crítico para trilhas de auditoria, fluxos de trabalho automatizados e conformidade regulatória. Ele permite que scripts filtrem arquivos redigidos, impede a distribuição acidental de conteúdo original e satisfaz muitos padrões da indústria que exigem rotulagem clara de documentos sanitizados.

## Aplicações práticas

1. **Redação de documentos legais:** Proteger contratos antes de compartilhamento com clientes.  
2. **Manipulação de registros médicos:** Proteger identificadores de pacientes enquanto preserva dados clínicos.  
3. **Relatórios financeiros:** Manter números sensíveis confidenciais durante auditorias externas.  
4. **Integração CRM:** Redigir automaticamente dados de clientes antes da exportação para ferramentas de terceiros.  
5. **Ferramentas de colaboração:** Garantir que rascunhos compartilhados nunca exponham comentários ocultos ou metadados.

## Considerações de desempenho

### Otimizando desempenho
- Use streaming (`load document from stream`) para evitar carregar arquivos inteiros na memória.  
- Feche as instâncias de `Redactor` prontamente para liberar recursos.  

### Diretrizes de uso de recursos
- Monitore CPU e memória durante execuções em lote.  
- Prefira `ByteArrayOutputStream` para salvamentos em memória ao trabalhar com arquivos de tamanho moderado.

### Melhores práticas para gerenciamento de memória Java
- Reutilize objetos `Redactor` ao processar múltiplos arquivos do mesmo tipo.  
- Invocar `close()` em um bloco `try‑with‑resources` para prevenir vazamentos.

## Problemas comuns e soluções
| Problema | Causa | Correção |
|----------|-------|----------|
| **Sufixo não aparecendo** | `setAddSuffix(false)` ou chamada ausente | Certifique‑se de que `options.setAddSuffix(true)` esteja definido antes de `save()`. |
| **OutOfMemoryError em DOCX grande** | Carregando o arquivo inteiro na memória | Mude para carregamento via `InputStream` (veja Recurso 1). |
| **Anotações ainda visíveis** | Redação não aplicada antes de salvar | Chame `redactor.apply(new DeleteAnnotationRedaction())` antes de `save()`. |
| **Rasterização PDF não aplicada** | `setRasterizeToPDF(false)` ou omitido | Defina `options.setRasterizeToPDF(true)` quando precisar de um PDF achatado. |

## Perguntas frequentes

**Q: Posso redigir documentos PDF usando GroupDocs.Redaction?**  
A: Sim, a biblioteca suporta PDFs, DOCX, PPTX, XLSX e muitos outros formatos.

**Q: Qual a melhor forma de lidar com arquivos grandes usando GroupDocs.Redaction?**  
A: Use streaming (`load document from stream`) e feche recursos prontamente para manter o uso de memória baixo.

**Q: É possível personalizar o texto do sufixo?**  
A: A API adiciona automaticamente um sufixo padrão (ex.: “_redacted”). Para sufixos personalizados, renomeie o arquivo de saída após a gravação.

**Q: Como obtenho uma licença temporária para GroupDocs.Redaction?**  
A: Visite a [Temporary License page](https://purchase.groupdocs.com/temporary-license/) e siga as instruções.

**Q: Onde posso obter ajuda se encontrar problemas?**  
A: Junte‑se ao [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) para assistência especializada.

## Recursos
- **Documentação:** Explore guias detalhados em [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Referência da API:** Acesse detalhes abrangentes da API em [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Obtenha a versão mais recente em [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Repositório GitHub:** Contribua ou explore o código‑fonte em [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Última atualização:** 2026-11-02  
**Testado com:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

## Tutoriais relacionados

- [Converter Word para PDF e salvar documentos redigidos com GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Visualizar páginas de documento Java carregamento com GroupDocs.Redaction](/redaction/java/document-loading/)
- [Técnicas avançadas de redação para GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)