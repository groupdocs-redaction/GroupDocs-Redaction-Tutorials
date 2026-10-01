---
date: '2026-10-01'
description: Aprenda a remover metadados de autor e salvar arquivos de documentos
  redigidos em Java usando o GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Aprenda a remover metadados de autor e salvar arquivos de documentos
  redigidos em Java usando o GroupDocs Redaction. Siga o guia passo a passo.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Como remover metadados de autor em Java com GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Como remover metadados de autor em Java com GroupDocs
type: docs
url: /pt/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Como remover metadados de autor em Java com GroupDocs

No cenário digital atual, proteger informações sensíveis ocultas dentro de documentos é uma prática indispensável. **Remover metadados de autor** impede a divulgação acidental de identificadores pessoais ou corporativos. Este tutorial mostra, passo a passo, como usar `EraseMetadataRedaction` do GroupDocs.Redaction para Java para remover campos como *Author* e *Manager* de arquivos Word e, em seguida, **salvar cópias do documento redigido** com segurança para compartilhamento ou arquivamento.

## Respostas rápidas
- **O que o EraseMetadataRedaction faz?** Ele remove campos de metadados selecionados de um documento.  
- **Qual biblioteca fornece esse recurso?** GroupDocs.Redaction para Java.  
- **Preciso de uma licença?** Um teste gratuito funciona para testes; uma licença permanente é necessária para produção.  
- **Posso direcionar vários campos ao mesmo tempo?** Sim, combine filtros com um OR lógico.  
- **O processo é thread‑safe?** Instâncias de Redactor não são compartilhadas entre threads; crie uma nova instância por operação.

## O que é EraseMetadataRedaction?
`EraseMetadataRedaction` é uma classe de redação embutida que permite especificar quais entradas de metadados devem ser apagadas. Ela funciona em uma ampla variedade de formatos de documento suportados pelo GroupDocs.Redaction, garantindo que informações de autoria ocultas nunca vazem. Você pode direcionar propriedades padrão como Author, Manager e também campos de metadados personalizados, oferecendo proteção de privacidade abrangente.

## Por que usar EraseMetadataRedaction com GroupDocs?
GroupDocs.Redaction suporta **mais de 100 formatos de entrada e saída** e pode processar documentos de até 500 páginas sem carregar o arquivo inteiro na memória. Usar esta classe fornece uma única API de alto desempenho para atender aos requisitos de GDPR, HIPAA ou conformidade interna, mantendo sua base de código simples.

## Pré-requisitos
- Java 8 ou superior instalado.  
- Maven (ou a capacidade de adicionar JARs manualmente).  
- GroupDocs.Redaction para Java (versão 24.9 ou posterior).  
- Uma licença válida de teste ou permanente do GroupDocs.

## Configurando GroupDocs.Redaction para Java

### Instalação via Maven
Adicione o repositório GroupDocs e a dependência ao seu **pom.xml**:

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
Alternativamente, faça o download do JAR mais recente em [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de licença
Obtenha um teste gratuito ou adquira uma licença temporária no portal GroupDocs. O arquivo de licença deve ser colocado onde sua aplicação possa carregá‑lo (por exemplo, na raiz do classpath).

### Inicialização e configuração básicas
Abaixo está um exemplo mínimo que cria uma instância `Redactor` para um arquivo DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Como usar EraseMetadataRedaction em Java
As seções a seguir dividem a implementação em etapas claras e acionáveis.

### Recurso: limpar itens de metadados específicos

#### Visão geral
Vamos apagar os campos de metadados **Author** e **Manager** usando `EraseMetadataRedaction`. Esta é uma necessidade comum ao compartilhar relatórios internos com parceiros externos.

#### Implementação passo a passo

##### 1️⃣ Inicializar o objeto Redactor
`Redactor` é a classe central que carrega um documento, aplica objetos de redação e grava o resultado. Crie uma nova instância para cada arquivo que você processar:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Aplicar EraseMetadataRedaction
`MetadataFilters` fornece filtros predefinidos para chaves de metadados comuns, como Author e Manager.  
`EraseMetadataRedaction` remove entradas de metadados que correspondem aos `MetadataFilters` fornecidos. O OR bit a bit (`|`) combina os filtros `Author` e `Manager` para que ambos os campos sejam removidos em uma única chamada:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configurar opções de salvamento
`SaveOptions` permite especificar o nome do arquivo de saída, o formato e outros parâmetros de salvamento.  
`SaveOptions` permite controlar o nome do arquivo de saída, o formato e se o documento deve ser rasterizado para PDF. Adicionar um sufixo mantém o arquivo original intocado:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Casos de uso comuns
1. **Documentos legais** – Redigir informações de autor antes de enviar contratos ao advogado da parte contrária.  
2. **Relatórios corporativos** – Remover nomes de gerentes ao publicar resultados trimestrais para acionistas.  
3. **Arquivos de projeto** – Limpar a documentação interna do projeto antes de arquivar ou fazer upload para um repositório público.

## Dicas de solução de problemas
- **Arquivo não encontrado** – Verifique se o caminho em `inputFilePath` aponta para um arquivo existente e se a aplicação tem permissões de leitura.  
- **Campos de metadados ausentes** – Nem todos os tipos de documento armazenam as mesmas chaves de metadados; verifique primeiro as propriedades do documento no Office.  
- **Erros de licença** – Certifique‑se de que o arquivo de licença foi carregado corretamente antes de criar a instância `Redactor`.

## Considerações de desempenho
- Feche o objeto `Redactor` prontamente (conforme mostrado no bloco `finally`) para liberar recursos nativos.  
- Evite rasterizar documentos grandes a menos que precise de uma visualização em PDF; a rasterização pode aumentar o uso de CPU e memória em até 3× para arquivos de 300 páginas.

## Perguntas frequentes

**Q1: O que é redação de metadados?**  
A1: A redação de metadados envolve remover propriedades ocultas do documento (como autor, gerente ou tags personalizadas) para impedir a divulgação acidental de informações sensíveis.

**Q2: Posso usar o GroupDocs.Redaction para outros tipos de arquivo?**  
A2: Sim, a biblioteca suporta PDF, DOCX, PPTX, XLSX e muitos outros formatos — mais de 100 no total.

**Q3: Como lidar com erros durante a redação?**  
A3: Envolva a chamada `apply` em um bloco try‑catch e sempre feche o `Redactor` em uma cláusula finally para garantir que os recursos sejam liberados.

**Q4: É possível redigir campos de metadados personalizados?**  
A5: Absolutamente. Use `MetadataFilters.Custom("YourFieldName")` para direcionar qualquer propriedade personalizada armazenada no documento.

**Q5: Quais são as melhores práticas para usar o GroupDocs.Redaction?**  
A5:  
- Carregue a licença logo no início da sua aplicação.  
- Feche os objetos `Redactor` prontamente.  
- Use `SaveOptions` para adicionar um sufixo, mantendo os arquivos originais intocados.  
- Teste a redação em uma cópia do documento antes de processar lotes.

**Q6: O EraseMetadataRedaction suporta operações em lote?**  
A6: Você pode percorrer uma coleção de caminhos de arquivos, criando um novo `Redactor` para cada arquivo e aplicando a mesma lógica de redação.

**Q7: Posso combinar EraseMetadataRedaction com outros tipos de redação?**  
A7: Sim, você pode encadear múltiplos objetos de redação (por exemplo, redação de texto seguida de redação de metadados) antes de salvar.

## Recursos

- **Documentação**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referência da API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Suporte gratuito**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Licença temporária**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Última atualização:** 2026-10-01  
**Testado com:** GroupDocs.Redaction 24.9 for Java  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Extração de Metadados de Documento Java com Groupdocs Redaction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Como Remover Metadados Java Usando GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Recuperar Informações do Documento Usando Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)