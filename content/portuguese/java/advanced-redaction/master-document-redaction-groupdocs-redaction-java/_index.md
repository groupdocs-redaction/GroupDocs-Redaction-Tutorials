---
date: '2026-02-16'
description: Aprenda a usar a dependência GroupDocs Maven para adicionar um sufixo
  aos nomes de arquivos ao redigir documentos em Java. Inclui carregamento a partir
  de stream, exclusão de anotações e opções de salvamento.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Dependência groupdocs maven – Adicionar sufixo ao nome do arquivo em Java
type: docs
url: /pt/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

All good.

Now produce final translated content.# Como Adicionar Sufixo ao Nome do Arquivo ao Redigir Documentos em Java com GroupDocs.Redaction

Redigir dados confidenciais é apenas metade da batalha — você também precisa garantir que o arquivo salvo indique claramente que foi processado. **Usar a dependência groupdocs maven torna isso simples**, permitindo que você adicione um sufixo ao nome do arquivo de saída em apenas algumas linhas de código. Neste guia você aprenderá como adicionar sufixo ao nome do arquivo ao salvar um documento redigido, além de carregar, anotar e salvar usando GroupDocs.Redaction para Java. Seja protegendo contratos legais, registros médicos ou relatórios financeiros, estas etapas manterão seu fluxo de trabalho seguro e auditável.

## Respostas Rápidas
- **O que “adicionar sufixo ao nome do arquivo” faz?**  
  Ele adiciona um sufixo personalizado (por exemplo, “_redacted”) ao nome do arquivo de saída para que você possa identificar instantaneamente os arquivos processados.  
- **Posso carregar um documento a partir de stream?**  
  Sim — GroupDocs.Redaction suporta carregamento a partir de qualquer `InputStream`, perfeito para armazenamento em nuvem ou processamento em memória.  
- **Preciso de licença para este recurso?**  
  Um teste gratuito funciona para redigência básica; uma licença temporária ou completa desbloqueia todas as opções avançadas, incluindo o tratamento de sufixos.  
- **Quais formatos são suportados?**  
  A biblioteca lida com DOCX, PDF, PPTX, XLSX e muitos outros.  
- **A rasterização é necessária para saída PDF?**  
  A rasterização é opcional; habilite-a quando precisar achatar o documento para maior segurança.

## O Que É Adicionar um Sufixo ao Nome de um Arquivo?

Adicionar um sufixo é uma convenção de nomenclatura simples que indica que um arquivo passou por redigência. Isso impede o compartilhamento acidental de versões originais não redigidas e ajuda pipelines automatizados a rastrear o status de processamento.

## Por Que Usar GroupDocs.Redaction para Esta Tarefa?

GroupDocs.Redaction fornece uma API Java fluente que permite combinar ações de redigência com opções de manipulação de arquivos — como **adicionar um sufixo ao nome do arquivo** — em apenas algumas linhas de código. Isso economiza tempo de desenvolvimento e reduz o risco de erros manuais.

## Pré-requisitos
- **Java Development Kit (JDK):** Versão 8 ou superior.  
- **GroupDocs.Redaction Library:** Biblioteca central para tarefas de redigência.  
- **IDE:** IntelliJ IDEA, Eclipse ou qualquer editor compatível com Java.  
- **Maven:** Para gerenciamento de dependências.  

### Pré-requisitos de Conhecimento
Familiaridade com Java I/O e conceitos básicos de programação orientada a objetos facilitará o acompanhamento dos exemplos.

## Configurando GroupDocs.Redaction para Java
### Configuração Maven
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

### Download Direto
Alternativamente, baixe a versão mais recente diretamente de [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de Licença
1. **Teste Gratuito:** Acesse funcionalidades básicas sem restrições.  
2. **Licença Temporária:** Obtenha uma licença temporária para explorar recursos avançados.  
3. **Compra:** Para uso a longo prazo, considere adquirir uma licença completa.

#### Inicialização e Configuração Básicas
Inicialize seu projeto adicionando os imports necessários:

```java
import com.groupdocs.redaction.Redactor;
```

Com esta configuração, você está pronto para implementar funcionalidades de redigência de documentos.

## Guia de Implementação

### Recurso 1: Carregar Documento a partir de Stream
**Visão geral:** Aprenda como carregar documentos em um `InputStream` para processamento.

#### Implementação Passo a Passo
##### Etapa 1.1: Criar InputStream

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

- **Por quê:** Usar `InputStream` permite manipular documentos armazenados em vários formatos de forma contínua, o que é essencial quando você precisa **carregar documento a partir de stream** em cenários de nuvem ou microsserviços.

### Recurso 2: Aplicar Redigência de Exclusão de Anotação
**Visão geral:** Remova anotações do seu documento usando o `DeleteAnnotationRedaction`.

#### Implementação Passo a Passo
##### Etapa 2.1: Aplicar DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Por quê:** Esta etapa garante que quaisquer anotações sensíveis sejam removidas, aprimorando a privacidade do documento.

### Recurso 3: Salvar Documento com Opções
**Visão geral:** Aprenda como salvar seu documento processado com opções específicas como rasterização e **adicionar um sufixo ao nome do arquivo**.

#### Implementação Passo a Passo
##### Etapa 3.1: Configurar SaveOptions

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

- **Por quê:** Personalizar as opções de salvamento permite formatos de saída flexíveis e convenções de nomenclatura. Habilitar `setAddSuffix(true)` **adiciona sufixo ao nome do arquivo**, deixando claro que o arquivo foi redigido.

## Visão Geral da dependência groupdocs maven
A **dependência groupdocs maven** traz todo o SDK Redaction para o seu projeto com uma única entrada `<dependency>`. Ela gerencia dependências transitivas, mantém as bibliotecas atualizadas e simplifica a automação de builds. Ao declarar a dependência no `pom.xml`, você evita o gerenciamento manual de JARs e garante compatibilidade com os patches de segurança mais recentes.

## Por Que Adicionar um Sufixo É Importante
- **Auditabilidade:** As equipes podem identificar instantaneamente quais arquivos são seguros para distribuição.  
- **Automação:** Scripts podem filtrar arquivos por sufixo, evitando o processamento acidental de documentos originais.  
- **Conformidade:** Muitas regulamentações exigem rotulagem clara de documentos sanitizados.  

## Aplicações Práticas
Explore estes casos de uso reais:
1. **Redigência de Documentos Legais:** Proteja contratos antes de compartilhá‑los com o cliente.  
2. **Manipulação de Registros Médicos:** Proteja identificadores de pacientes.  
3. **Relatórios Financeiros:** Mantenha números sensíveis confidenciais.  
4. **Integração com CRM:** Redija automaticamente dados de clientes antes da exportação.  
5. **Ferramentas de Colaboração:** Garanta que rascunhos compartilhados nunca exponham comentários ocultos.

## Considerações de Desempenho
### Otimizando o Desempenho
- Use streaming (`load document from stream`) para evitar carregar arquivos inteiros na memória.  
- Feche as instâncias de `Redactor` prontamente para liberar recursos.

### Diretrizes de Uso de Recursos
- Monitore CPU e memória durante execuções em lote.  
- Prefira `ByteArrayOutputStream` para salvamentos em memória ao trabalhar com arquivos de tamanho moderado.

### Melhores Práticas para Gerenciamento de Memória Java
- Reutilize objetos `Redactor` ao processar múltiplos arquivos do mesmo tipo.  
- Invocar `close()` em um bloco `try‑with‑resources` para prevenir vazamentos.

## Problemas Comuns e Soluções
| Problema | Causa | Solução |
|----------|-------|---------|
| **Sufixo não aparece** | `setAddSuffix(false)` ou chamada ausente | Garanta que `options.setAddSuffix(true)` esteja definido antes de `save()`. |
| **OutOfMemoryError em DOCX grande** | Carregamento de todo o arquivo na memória | Troque para carregamento via `InputStream` (veja Recurso 1). |
| **Anotações ainda visíveis** | Redigência não aplicada antes de salvar | Chame `redactor.apply(new DeleteAnnotationRedaction())` antes de `save()`. |
| **Rasterização de PDF não aplicada** | `setRasterizeToPDF(false)` ou omitido | Defina `options.setRasterizeToPDF(true)` quando precisar de um PDF achatado. |

## Perguntas Frequentes

**P: Posso redigir documentos PDF usando GroupDocs.Redaction?**  
R: Sim, a biblioteca suporta PDFs, DOCX, PPTX, XLSX e muitos outros formatos.

**P: Qual a melhor maneira de lidar com arquivos grandes usando GroupDocs.Redaction?**  
R: Use streaming (`load document from stream`) e feche os recursos prontamente para manter o uso de memória baixo.

**P: É possível personalizar o texto do sufixo?**  
R: A API adiciona automaticamente um sufixo padrão (por exemplo, “_redacted”). Para sufixos personalizados, você pode renomear o arquivo de saída após a gravação.

**P: Como obtenho uma licença temporária para GroupDocs.Redaction?**  
R: Visite a [página de Licença Temporária](https://purchase.groupdocs.com/temporary-license/) e siga as instruções.

**P: Onde posso obter ajuda se encontrar problemas?**  
R: Participe do [Fórum de Suporte GroupDocs](https://forum.groupdocs.com/c/redaction/33) para assistência especializada.

## Recursos
- **Documentação:** Explore guias detalhados em [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **Referência da API:** Acesse detalhes abrangentes da API em [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Obtenha a versão mais recente em [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **Repositório GitHub:** Contribua ou explore o código-fonte em [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Última Atualização:** 2026-02-16  
**Testado com:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

---