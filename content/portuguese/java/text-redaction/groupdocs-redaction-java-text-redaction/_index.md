---
date: '2026-02-26'
description: Aprenda a censurar texto em documentos Java usando o GroupDocs.Redaction,
  incluindo como mascarar informações pessoais e substituir texto sensível.
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
title: Como Redigir Texto com GroupDocs.Redaction para Java
type: docs
url: /pt/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

Now produce final answer with translated content only.

Let's write Portuguese translation.

Check for any special characters: keep non-breaking spaces? Not needed.

Proceed.

# Como Redigir Texto em Documentos Usando GroupDocs.Redaction para Java

Neste guia você descobrirá **como redigir texto** em documentos baseados em Java com a ajuda do GroupDocs.Redaction. Seja para **mascarar informações pessoais** ou **substituir texto sensível** por marcadores de posição, os passos abaixo o conduzirão por uma solução completa, pronta para produção. Ao final do tutorial você será capaz de proteger a privacidade, manter a conformidade e automatizar a redação em diversos formatos de arquivo.

## Respostas Rápidas
- **Qual biblioteca é usada?** GroupDocs.Redaction para Java  
- **Posso mascarar informações pessoais?** Sim – use a redação por frase exata com opções de substituição.  
- **O processamento em lote é suportado?** Absolutamente, você pode percorrer vários arquivos com a mesma instância de Redactor.  
- **Preciso de licença?** Um teste gratuito funciona para avaliação; uma licença comercial é necessária para produção.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.

## O que é “como redigir texto”?
A redação é o processo de remover ou obscurecer permanentemente dados confidenciais de um documento. Com o GroupDocs.Redaction você pode localizar programaticamente strings específicas, substituí‑las por marcadores seguros e salvar o arquivo sanitizado — tudo sem edição manual.

## Por que usar GroupDocs.Redaction para Java?
- **Amplo suporte a formatos:** DOCX, PDF, XLSX, PPTX e muito mais.  
- **Alto desempenho:** Otimizado para arquivos grandes e operações em lote.  
- **Callbacks extensíveis:** Intercepte eventos de redação para registro ou tratamento personalizado.  
- **Pronto para conformidade:** Atende ao GDPR, HIPAA e outras regulamentações de privacidade.

## Pré‑requisitos
- **Java Development Kit (JDK):** Versão 8 ou mais recente.  
- **IDE:** IntelliJ IDEA, Eclipse ou qualquer editor compatível com Java.  
- **Maven:** Para gerenciamento de dependências.  
- **Conhecimento básico de Java:** Familiaridade com classes, métodos e tratamento de exceções.

## Configurando GroupDocs.Redaction para Java
Para começar, adicione a biblioteca ao seu projeto Maven.

### Configuração Maven
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

### Download Direto
Se preferir, obtenha o JAR mais recente em [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de Licença
Você pode iniciar com um **Free Trial**, solicitar uma **Temporary License** para testes estendidos ou adquirir uma **Commercial License** para uso em produção.

## Como Redigir Texto em Documentos com GroupDocs.Redaction
As seções a seguir orientam passo a passo como **mascarar informações pessoais** e **substituir texto sensível**.

### Etapa 1: Inicializar o Redactor
Crie uma instância de `Redactor` apontando para o documento que deseja processar.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Etapa 2: Aplicar Redação por Frase Exata
Use `ExactPhraseRedaction` para localizar uma frase como “John Doe” e substituí‑la por um marcador seguro.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parâmetros:**  
  - `"John Doe"` – o texto exato a ser redigido.  
  - `ReplacementOptions("[personal]")` – a string que substituirá o conteúdo original, efetivamente **mascarando informações pessoais**.

### Etapa 3: Salvar o Documento Redigido
Persista as alterações em um novo arquivo ou sobrescreva o original.

```java
redactor.save();
```

### Etapa 4: Liberar Recursos
Sempre feche o `Redactor` para liberar recursos nativos.

```java
finally {
    redactor.close();
}
```

## Como Mascarar Informações Pessoais com um Callback Personalizado
Às vezes é necessário mais controle sobre o que acontece quando uma redação ocorre (por exemplo, registro, substituição condicional).

### Crie uma Classe de Callback
Implemente `IRedactionCallback` para receber eventos de redação.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use o Callback ao Instanciar o Redactor
Passe o callback via `RedactorSettings`.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Aplicações Práticas
- **Contratos legais:** Ocultar automaticamente nomes de clientes, SSNs ou cláusulas confidenciais.  
- **Registros médicos:** **Mascarar informações pessoais** como identificadores de pacientes antes de compartilhar com terceiros.  
- **Comunicações corporativas:** **Substituir texto sensível** como códigos internos de projetos antes da distribuição externa.

## Considerações de Desempenho
Ao processar arquivos grandes ou numerosos, tenha em mente estas dicas:

- **Processamento em lote:** Percorra uma coleção de arquivos para reduzir a sobrecarga de inicialização.  
- **Gerenciamento de memória:** Libere o `Redactor` após cada arquivo; evite manter muitos documentos na memória simultaneamente.  
- **Profiling:** Use perfis Java (ex.: VisualVM) para identificar gargalos de I/O ou lógica de redação.

## Perguntas Frequentes
**Q: Posso redigir texto de PDFs usando GroupDocs.Redaction?**  
A: Sim, a biblioteca suporta PDF, DOCX, XLSX, PPTX e muitos outros formatos.

**Q: Uma redação é reversível?**  
A: Não. Redações removem permanentemente o conteúdo original, portanto mantenha um backup do arquivo fonte.

**Q: Como lidar eficientemente com documentos muito grandes?**  
A: Processá‑los em blocos, usar modo em lote e monitorar o uso de memória com ferramentas de profiling.

**Q: Quais outros formatos de texto são suportados?**  
A: Além de DOCX e PDF, você pode redigir TXT, RTF, XLSX, PPTX e mais.

**Q: Posso integrar GroupDocs.Redaction em fluxos de trabalho existentes?**  
A: Absolutamente. A API pode ser chamada a partir de serviços web, jobs em background ou pipelines CI/CD.

## Recursos
- **Documentação:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **Referência da API:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **Repositório GitHub:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Fórum de Suporte Gratuito:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Aplicação de Licença Temporária:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-02-26  
**Testado com:** GroupDocs.Redaction 24.9 para Java  
**Autor:** GroupDocs