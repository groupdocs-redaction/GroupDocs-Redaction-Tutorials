---
date: '2025-12-17'
description: Aprenda como adicionar sufixo ao nome do arquivo e remover informações
  sensíveis de documentos usando o GroupDocs.Redaction para Java. Melhore a segurança
  e a privacidade dos documentos de forma eficaz.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Como adicionar sufixo ao nome do arquivo ao redigir documentos em Java com
  GroupDocs.Redaction
type: docs
url: /pt/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Como Adicionar Sufixo ao Nome do Arquivo ao Redigir Documentos em Java com GroupDocs.Redaction

Redigir dados confidenciais é apenas metade da batalha — você também precisa garantir que o arquivo salvo indique claramente que foi processado. Neste guia você aprenderá **como adicionar sufixo ao nome do arquivo** ao salvar um documento redigido, além de carregar, anotar e salvar usando GroupDocs.Redaction para Java. Seja protegendo contratos legais, registros ou relatórios financeiros, estas etapas manterão seu fluxo de trabalho seguro e auditável.

## Respostas Rápidas
- **O que faz “add suffix to filename”?**  
  Ele adiciona um sufixo personalizado (ex.: “_redacted”) ao nome do arquivo de saída, permitindo identificar instantaneamente os arquivos processados.  
- **Posso carregar um documento a partir de stream?**  
  Sim — GroupDocs.Redaction suporta carregamento a partir de qualquer `InputStream`, ideal para armazenamento em nuvem ou processamento em memória.  
- **Preciso de licença para este recurso?**  
  Um teste gratuito funciona para redigimento básico; uma licença temporária ou completa desbloqueia todas as opções avançadas, incluindo o tratamento de sufixo.  
- **Quais formatos são suportados?**  
  A biblioteca lida com DOCX, PDF, PPTX, XLSX e muitos outros.  
- **A rasterização é necessária para saída PDF?**  
  A rasterização é opcional; habilite-a quando precisar achatar o documento para maior segurança.

## O Que É Adicionar um Sufixo ao Nome de Arquivo?
Adicionar um sufixo é uma convenção de nomenclatura simples que indica que um arquivo passou por redigimento. Isso impede o compartilhamento acidental de versões originais não redigidas e ajuda pipelines automatizados a rastrear o status de processamento.

## Por Que Usar GroupDocs.Redaction para Esta Tarefa?
GroupDocs.Redaction fornece uma API Java fluente que permite combinar ações de redigimento com opções de manipulação de arquivos — como **adicionar um sufixo ao nome do arquivo** — em apenas algumas linhas de código. Isso economiza tempo de desenvolvimento e reduz o risco de erros manuais.

## Pré-requisitos
- **Java Development Kit (JDK):** Versão 8 ou superior.  
- **GroupDocs.Redaction Library:** Biblioteca central para tarefas de redigimento.  
- **IDE:** IntelliJ IDEA, Eclipse ou qualquer editor compatível com Java.  
- **Maven:** Para gerenciamento de dependências.  

### Pré-requisitos de Conhecimento
Familiaridade com Java I/O e conceitos básicos de orientação a objetos facilitará o acompanhamento dos exemplos.

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
Alternativamente, faça o download da versão mais recente diretamente de [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de Licença
1. **Free Trial:** Acesse funcionalidades básicas sem restrições.  
2. **Temporary License:** Obtenha uma licença temporária para explorar recursos avançados.  
3. **Purchase:** Para uso a longo prazo, considere adquirir uma licença completa.

#### Inicialização e Configuração Básicas
Inicialize seu projeto adicionando as importações necessárias:

```java
import com.groupdocs.redaction.Redactor;
```

Com esta configuração, você está pronto para implementar funcionalidades de redigimento de documentos.

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

- **Por quê:** Usar `InputStream` permite lidar com documentos armazenados em vários formatos de forma contínua, o que é essencial quando você precisa **carregar documento a partir de stream** em cenários de nuvem ou microsserviços.

### Recurso 2: Aplicar Redigimento de Exclusão de Anotação
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
##### Etapa3.1: Configurar SaveOptions

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

## Por Que Adicionar um Suffix é Importante
- **Auditabilidade:** As equipes podem identificar instantaneamente quais arquivos são seguros para distribuição.  
- **Automação:** Scripts podem filtrar arquivos por sufixo, evitando o processamento acidental de documentos originais.  
- **Conformidade:** Muitas regulamentações exigem rotulagem clara de documentos sanitizados.

## Aplicações Práticas
Explore estes casos de uso reais:

1. **Redigimento de Documentos Legais:** Proteja contratos antes de compartilhá-los com clientes.  
2. **Manipulação de Registros Médicos:** Proteja identificadores de pacientes.  
3. **Relatórios Financeiros:** Mantenha números sensíveis confidenciais.  
4. **Integração CRM:** Redija automaticamente dados de clientes antes da exportação.  
5. **Ferramentas de Colaboração:** Garanta que rascunhos compartilhados nunca exponham comentários ocultos.

## Considerações de Desempenho
### Otimizando o Desempenho
- Use streaming (`load document from stream`) para evitar carregar arquivos inteiros na memória.  
- Feche as instâncias de `Redactor` prontamente para liberar recursos.

### Diretrizes de Uso de Recursos
- Monitore CPU e memória durante execuções em lote.  
- Prefira `ByteArrayOutputStream` para salvamentos em memória ao trabalhar com arquivos de tamanho moderado.

### Melhores Práticas para Gerenciamento de Memória Java
- Reutilize objetos `Redactor` ao processar vários arquivos do mesmo tipo.  
- Chame `close()` em um bloco `finally` ou try‑with‑resources para evitar vazamentos.

## Problemas Comuns e Soluções
| Problema | Causa | Correção |
|----------|-------|----------|
| **Sufixo não aparecendo** | `setAddSuffix(false)` ou chamada ausente | Garanta que `options.setAddSuffix(true)` esteja definido antes de `save()`. |
| **OutOfMemoryError em DOCX grande** | Carregamento de todo o arquivo na memória | Mude para carregamento via `InputStream` (veja Recurso 1). |
| **Anotações ainda visíveis** | Redigimento não aplicado antes de salvar | Chame `redactor.apply(new DeleteAnnotationRedaction())` antes de `save()`. |
| **Rasterização de PDF não aplicada** | `setRasterizeToPDF(false)` ou omitido | Defina `options.setRasterizeToPDF(true)` quando precisar de um PDF achatado. |

## Perguntas Frequentes

**Q: Posso redigir documentos PDF usando GroupDocs.Redaction?**  
A: Sim, a biblioteca suporta PDFs, DOCX, PPTX, XLSX e muitos outros formatos.

**Q: Qual a melhor maneira de lidar com arquivos grandes usando GroupDocs.Redaction?**  
A: Use streaming (`load document from stream`) e feche os recursos prontamente para manter o uso de memória baixo.

**Q: É possível personalizar o texto do sufixo?**  
A: A API adiciona automaticamente um sufixo padrão (ex.: “_redacted”). Para sufixos personalizados, você pode renomear o arquivo de saída após a gravação.

**Q: Como obtenho uma licença temporária para GroupDocs.Redaction?**  
A: Visite a [Temporary License page](https://purchase.groupdocs.com/temporary-license/) e siga as instruções.

**Q: Onde posso obter ajuda se encontrar problemas?**  
A: Participe do [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) para assistência especializada.

## Recursos
- **Documentation:** Explore guias detalhados em [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/).  
- **API Reference:** Acesse detalhes abrangentes da API em [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java).  
- **Download:** Obtenha a versão mais recente em [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/).  
- **GitHub Repository:** Contribua ou explore o código-fonte em [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

---

**Última atualização:** 2025-12-17  
**Testado com:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs  

---