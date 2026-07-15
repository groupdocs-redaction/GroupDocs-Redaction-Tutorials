---
date: '2026-06-26'
description: Aprenda como extrair texto de PDF escaneado e mascarar dados sensíveis
  usando GroupDocs OCR Redaction com Azure OCR. Mascarar número de segurança social
  e substituir informações confidenciais em PDF de forma eficiente.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Extrair Texto de PDF Escaneado – Mascarar Dados com GroupDocs OCR
type: docs
url: /pt/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Extrair Texto de PDF Escaneado – Mascarar Dados com GroupDocs OCR

No mundo orientado a dados de hoje, **extrair texto de PDFs escaneados** e mascarar informações confidenciais é uma etapa de conformidade inegociável. Este tutorial mostra como usar o GroupDocs Redaction junto com o Microsoft Azure OCR para reconhecer de forma confiável o texto oculto em páginas escaneadas e substituí‑lo por um placeholder seguro, como **`[REDACTED]`**. Você verá por que essa combinação é rápida, precisa e pronta para cargas de trabalho de nível de produção.

## Respostas Rápidas
- **O que significa “mascarar dados sensíveis”?** Substitui o texto confidencial identificado por um placeholder (por exemplo, `[REDACTED]`).  
- **Qual biblioteca lida com OCR?** Conector Microsoft Azure OCR, usado através do GroupDocs Redaction.  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença permanente é necessária para produção.  
- **Posso remover informações de PDFs escaneados?** Sim—OCR extrai o texto oculto antes de aplicar as remoções por regex.  
- **Esta solução é apenas Java?** O exemplo é baseado em Java, mas o GroupDocs fornece APIs semelhantes para .NET e outras plataformas.

## O que é Redação Baseada em OCR?
A Redação Baseada em OCR primeiro executa OCR em cada página, transformando imagens em texto pesquisável, e então aplica padrões regex para substituir as correspondências por uma máscara como `[REDACTED]`. Esse processo em duas etapas permite ocultar de forma confiável dados pessoais mesmo em PDFs escaneados, garantindo que quaisquer cadeias sensíveis sejam removidas antes que o documento seja compartilhado ou arquivado.

## Por que Usar GroupDocs Redaction com Azure OCR?
Você deve usar o GroupDocs Redaction com Azure OCR porque ele oferece **>98 % de precisão OCR em texto impresso**, suporta **mais de 50 formatos de entrada e saída**, e pode processar **PDFs com centenas de páginas sem carregar o arquivo inteiro na memória**, garantindo redação rápida e escalável para conformidade. A solução também **escala para processar um PDF de 1.000 páginas em menos de 2 minutos em um servidor de 8 núcleos**, tornando os trabalhos em lote práticos.

## Pré‑requisitos
- **Java Development Kit (JDK) 8+** instalado.  
- **Maven** (se preferir gerenciamento de dependências) ou a capacidade de baixar JARs manualmente.  
- **Credenciais do Microsoft Azure OCR** (endpoint e chave de assinatura).  
- Conhecimento básico de Java e familiaridade com expressões regulares.

## Configurando GroupDocs Redaction para Java

### Configuração Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Se preferir gerenciamento manual de JARs, obtenha a versão mais recente em [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de Licença
- **Teste Gratuito** – explore todos os recursos sem custo.  
- **Licença Temporária** – estenda o tempo de avaliação.  
- **Licença Completa** – desbloqueie recursos prontos para produção.

### Inicialização e Configuração Básicas
The `Redactor` class is the core engine that performs OCR extraction and applies redaction rules to PDF documents.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## Como Mascarar Dados Sensíveis com Redação OCR
Mascarar dados sensíveis com Redação OCR envolve carregar o PDF com as configurações do Azure OCR, definir padrões regex para os dados que você deseja ocultar e invocar o Redactor para substituir cada correspondência por um placeholder como `[REDACTED]`. A biblioteca lida com OCR, correspondência de padrões e reescrita de PDF em um único fluxo de trabalho.

### Etapa 1: Carregar o Documento com Configurações OCR
`LoadOptions` configura como o GroupDocs carrega um arquivo, permitindo que você passe conectores OCR como o Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – substitua pelo caminho do seu PDF.  
- **`settings`** – contém o conector Azure OCR que você criou anteriormente.

### Etapa 2: Definir e Aplicar Redações Regex
`ReplacementOptions` especifica o texto de substituição que substituirá cada correspondência regex durante a redação.  
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
- O padrão `\b\d{3}-\d{2}-\d{4}\b` corresponde a números de Seguro Social dos EUA.  
- `ReplacementOptions("[REDACTED]")` troca cada correspondência pela máscara, efetivamente **mascarando dados sensíveis**.

## Casos de Uso Comuns para Mascarar Dados Sensíveis
1. **Gerenciamento de Documentos Legais** – ocultar identificadores de clientes antes de compartilhar rascunhos.  
2. **Relatórios Financeiros** – proteger números de conta e IDs de transação.  
3. **Registros de Saúde** – cumprir a HIPAA ao remover identificadores de pacientes.  
4. **Publicações Governamentais** – remover dados pessoais de registros públicos.  
5. **Contratos Corporativos** – ocultar termos proprietários durante revisões externas.

## Dicas de Performance
- **Otimizar regex** – evite padrões excessivamente amplos que aumentam o tempo de processamento; expressões bem elaboradas podem reduzir o tempo de execução em até 40 %.  
- **Gerenciamento de Memória** – feche a instância `Redactor` prontamente (try‑with‑resources faz isso automaticamente).  
- **Execução Assíncrona** – para processamento em lote, execute trabalhos de redação em threads separadas ou use uma fila de tarefas para manter a UI responsiva.

## Solução de Problemas
- **Erro nas credenciais do Azure** – verifique novamente o URL do endpoint e a chave de assinatura em `MicrosoftAzureOcrConnector`.  
- **Documento não carregando** – verifique o caminho do arquivo e assegure que o PDF não esteja protegido por senha (ou forneça a senha via `LoadOptions`).  
- **Nenhuma redação aplicada** – teste seu regex com uma string simples primeiro; use `Pattern.compile` em um teste unitário para confirmar as correspondências.

## Perguntas Frequentes

**Q: O que é redação OCR?**  
A: A redação OCR usa Reconhecimento Óptico de Caracteres para extrair texto oculto de imagens ou PDFs escaneados, e então aplica regras de redação para mascarar esse texto.

**Q: Posso usar GroupDocs Redaction sem Azure OCR?**  
A: Sim, mas o OCR melhora drasticamente a precisão em documentos escaneados onde a extração de texto nativa falha.

**Q: Como lidar com padrões regex complexos?**  
A: Construa e teste-os incrementalmente, usando a classe `Pattern` do Java em um sandbox antes de aplicar a documentos grandes.

**Q: Quais são os gargalos de performance típicos?**  
A: PDFs grandes, regex excessivamente complexos e chamadas OCR síncronas podem desacelerar o processamento; considere processamento em lote e padrões otimizados.

**Q: O suporte está disponível para questões de implementação?**  
A: Absolutamente—entre em contato através do [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) para ajuda da comunidade ou contate o suporte da GroupDocs.

## Recursos Adicionais
- **Documentação**: https://docs.groupdocs.com/redaction/java/  
- **Referência da API**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Suporte Gratuito**: https://forum.groupdocs.com/c/redaction/33  
- **Licença Temporária**: https://purchase.groupdocs.com/temporary-license/

---

**Última Atualização:** 2026-06-26  
**Testado com:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs  

## Tutoriais Relacionados

- [Redação Segura de PDF usando OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Como Redigir Texto com GroupDocs.Redaction para Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Mascarar Dados Sensíveis Java – Redigir Informações Pessoais com GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)