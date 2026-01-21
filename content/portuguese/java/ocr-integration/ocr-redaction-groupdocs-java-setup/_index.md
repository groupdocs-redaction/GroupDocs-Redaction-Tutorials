---
date: '2026-01-21'
description: Aprenda a censurar PDFs com OCR e a censurar documentos digitalizados
  usando o GroupDocs.Redaction para Java com integração ao Azure OCR.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: Redigir PDF com OCR usando GroupDocs e Azure OCR – Guia Java
type: docs
url: /pt/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Redigir PDF com OCR usando GroupDocs & Azure OCR – Guia Java

Neste tutorial abrangente, você descobrirá como **redigir PDF com OCR** em Java, aproveitando o GroupDocs.Redaction juntamente com o Microsoft Azure OCR. Seja lidando com PDFs nativos ou imagens escaneadas, este guia mostra como localizar e mascarar dados sensíveis com precisão, ajudando você a **redigir documentos escaneados** para atender às regulamentações de privacidade.

## Respostas Rápidas
- **O que a redação com OCR faz?** Ela extrai texto de imagens/PDFs e aplica regras de redação automaticamente.  
- **Qual biblioteca fornece o mecanismo de redação?** GroupDocs.Redaction para Java.  
- **Qual serviço de OCR é usado?** Conector Microsoft Azure OCR.  
- **Preciso de uma licença?** Um teste gratuito funciona para experimentação; uma licença permanente é necessária para produção.  
- **Posso redigir PDFs nativos e escaneados?** Sim – o OCR permite a redação de documentos esc é “redigir PDF com OCR”?
Redigir PDF com OCR significa usar reconhecimento óptico de caracteres para transformar texto visual em cadeias pesquisáveis e, em seguida, aplicar padrões de redação (por exemplo, regex) para ocultar essas informações antes que o arquivo seja compartilhado ou armazenado.

## Por que usar GroupDocs.Redaction com Azure OCR?
- **Alta precisão** em páginas escaneadas graças ao mecanismo de OCR baseado na nuvem da Azure.  
- **API Java simples** que se integra diretamente ao seu lógica personalizada.  
- **Saída pronta para conformidade** que remove permanentemente os dados sens.Red
Adicione o repositório GroupDocs e a dependência ao seu `pom.xml`:

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
Se preferir não usar Maven, baixe o JAR mais recente na página oficial de lançamentos: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de Licença
- **Teste Gratuito** – explore os recursos principais sem compromisso** – estenda o período de teste para projetos maiores.  
- **Licença Completa** – desbloqueie uso ilimitado e suporte premium.

### Inicialização e Configuração Básicas
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Como redigir PDF com OCR em Java

### Etapa 1: Carregar o Documento com Configurações de OCR
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parâmetros**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – caminho para o PDF alvo.  
  - `new LoadOptions()` – configuração padrão de carregamento.  
  - `settings` – contém o conector Azure OCR.

### Etapa 2: Aplicar Redações Regex (por exemplo, Números de Seguro Social)
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- **Explicação da Regex** – `\b\d{3}-\d{2}-\d{4}\b` corresponde a padrões como `123-45-6789`.  
- **ReplacementOptions** – substitui o texto detectado por `[REDACTED]`.

### Armadilhas Comuns & Solução de Problemas
- **Credenciais Azure** – verifique novamente a chave de assinatura e o endpoint.  
- **Caminho do arquivo** – assegure que o PDF exista e que a aplicação tenha permissões de leitura/escrita.  
- **Desempenho** – PDFs grandes podem exigir aumento do tamanho de heap ou processamento assíncrono.

## Casos de Uso Práticos para Redigir Documentos Escaneados
1. **Escritórios de advocacia** – ocultar identificadores de clientes antes de compartilhar processos.  
2. **Instituições financeiras** – mascarar números de conta em extratos escaneados.  
3. **Provedores de saúde** – proteger PHI de pacientes em registros médicos escaneados.  
4. **Agências governamentais** – remover dados pessoais de PDFs de registros públicos.  
5. **Empresas** – sanitizar contratos antes de auditorias de terceiros.

## Dicas de Desempenho
- Mantenha os padrões regex o mais específico possível para reduzir o tempo de processamento.  
- Libere a instância `Redactor` prontamente (use try‑with‑resources como mostrado).  
- Para processamento em lote, considere enfileirar trabalhos.

## Perguntas Frequentes

 de imagens ou PDFs escaneados e, em seguida, aplica regras de redação palavra (`\b`) para evitar correspondências parciais e considere dividir expressões grandes em várias redações mais simples.

**Q: Quais são os gargalos de desempenho típicos?**  
A: Chamadas intensivas de OCR em arquivos grandes, regex muito amplas e alocação insuficiente de memória. Otimize ajustando regex e escalando recursos.

**Q: Onde posso obter ajuda se encontrar problemas?**  
A: Publique perguntas no fórum da comunidade GroupDocs: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Recursos Adicionais
- **Documentação**: https://docs.groupdocs.com/redaction/java/
- **Referência da API**: https://reference.groupdocs.com/redaction/java
- **Download**: https://releases.groupdocs.com/redaction/java/
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
- **Suporte Gratuito**: https://forum.groupdocs.com/c/redaction/33
- **Licença Temporária**: https://purchase.groupdocs.com/temporary-license/

---

**Última atualização:** 2026-01-21  
**Testado com:** GroupDocs.Redaction 24.9 para Java  
**Autor:** GroupDocs