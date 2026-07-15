---
date: '2026-05-17'
description: Aprenda a rasterizar PDF em escala de cinza usando GroupDocs.Redaction
  para Java, aplicar um filtro de escala de cinza e manter seus documentos seguros
  e de alta qualidade.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: Como rasterizar PDF em escala de cinza com GroupDocs.Redaction Java – Proteja
  e otimize seus documentos
type: docs
url: /pt/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# Como rasterizar PDF em escala de cinza com GroupDocs.Redaction Java

Se você precisa **rasterizar um PDF** em escala de cinza enquanto mantém seus documentos seguros, com aparência profissional e fáceis de arquivar, você está no lugar certo. Neste tutorial, percorreremos os passos exatos para converter arquivos coloridos DOCX, PDF ou outros suportados em uma versão limpa, rasterizada em escala de cinza usando GroupDocs.Redaction para Java. Você entenderá por que a rasterização adiciona uma camada de segurança, como configurar a biblioteca e como gerenciar recursos de forma eficiente — tudo apresentado em um estilo amigável, passo a passo.

## Respostas Rápidas
- **O que a rasterização em escala de cinza faz?** Ela converte cada página em uma imagem de alta resolução e então aplica um filtro em escala de cinza, removendo todas as informações de cor.  
- **Por que usar o GroupDocs.Redaction para isso?** Ele combina a segurança de redaction com opções de rasterização em uma única API fácil de usar.  
- **Quais formatos são suportados?** DOCX, PDF, XLSX, PPTX, RTF e mais de 100 outros formatos.  
- **Preciso de uma licença?** Uma licença válida do GroupDocs.Redaction é necessária para produção; um teste gratuito está disponível para experimentação.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.

## Como rasterizar PDF em escala de cinza?

Carregue seu documento de origem com `new Redactor("path/to/file")`, habilite a rasterização via `RasterizationOptions`, adicione a opção avançada de escala de cinza e chame `save()` — toda a conversão ocorre em poucas linhas concisas. Essa abordagem garante que cada página se torne um PDF baseado em imagem, preto e branco, impedindo a seleção de texto e assegurando uma aparência uniforme pronta para impressão.

## O que é **create grayscale pdf**?

Criar um PDF em escala de cinza significa converter cada elemento visual do documento original em tons de cinza. O resultado é um arquivo menor, adequado para impressão, que elimina distrações relacionadas à cor e adiciona um benefício sutil de segurança, pois o conteúdo agora está baseado em imagem.

## Por que usar rasterização em escala de cinza com GroupDocs.Redaction?

A rasterização transforma cada página em uma imagem, o que significa que o texto não pode ser copiado ou editado, e a saída visual permanece consistente em impressoras e visualizadores. O GroupDocs.Redaction suporta **mais de 100 formatos de entrada e saída** — incluindo DOCX, XLSX, PPTX, HTML e tipos de imagem — para que você possa aplicar o mesmo fluxo de trabalho a praticamente qualquer documento que manipule.

## Pré-requisitos

- Java Development Kit (JDK) 8 ou mais recente. Verifique com `java -version`.  
- Uma IDE (IntelliJ IDEA, Eclipse ou NetBeans) para facilitar a codificação e depuração.  
- GroupDocs.Redaction para Java adicionado via Maven ou Gradle.  
- Um documento de exemplo (por exemplo, um DOCX de várias páginas) que você pode experimentar com segurança.  
- Espaço em disco suficiente para a saída rasterizada (arquivos raster podem ser maiores que a origem).

## Importar Pacotes

As importações a seguir trazem as classes principais Redactor e de rasterização necessárias para o exemplo.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Etapa 1: Inicializar o Objeto Redactor

A classe `Redactor` é o ponto de entrada para todas as operações de processamento de documentos no GroupDocs.Redaction. Criar uma instância abre a porta para carregar, editar e salvar documentos.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Substitua `Constants.MULTIPAGE_SAMPLE_DOCX` pelo caminho do arquivo que você deseja converter para um PDF em escala de cinza.

## Etapa 2: Configurar Opções de Salvamento

A classe `SaveOptions` define como o documento processado será gravado no disco, incluindo formato e nome do arquivo.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

A saída será nomeada `yourfile_scan.pdf` (ou o formato que você especificar posteriormente).

## Etapa 3: Habilitar Rasterização

O objeto `RasterizationOptions` habilita a renderização baseada em imagem de cada página antes de salvar.

```java
so.getRasterization().setEnabled(true);
```

## Etapa 4: Aplicar Conversão em Escala de Cinza

`AdvancedRasterizationOptions.Grayscale` é uma flag que força a imagem rasterizada a usar apenas tons de cinza.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Etapa 5: Executar a Transformação do Documento

Chamar `save()` executa todo o pipeline de processamento e grava o arquivo de saída.

```java
redactor.save(so);
```

Depois que esta linha for executada, você encontrará um novo arquivo no disco que está totalmente rasterizado, em escala de cinza, e salvo com o sufixo `_scan`.

## Etapa 6: Gerenciamento Adequado de Recursos

O método `close()` libera recursos nativos e exclui arquivos temporários.

```java
finally { redactor.close(); }
```

Para Java moderno, você também pode usar o padrão try‑with‑resources, que fecha automaticamente o `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Ambas as abordagens são seguras; a última é mais concisa.

## Opções Avançadas de Configuração

### Ajustar DPI para Qualidade ou Tamanho

Um DPI mais alto produz imagens mais nítidas (bom para impressão), enquanto um DPI mais baixo reduz o tamanho do arquivo. Um equilíbrio comum é 150 DPI para visualização na tela e 300 DPI para PDFs prontos para impressão.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Escolher um Formato de Saída

Você pode forçar o resultado rasterizado a um formato de contêiner específico, como PDF, TIFF ou PNG. PDF é o formato de arquivamento mais amplamente usado.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Casos de Uso Comuns

- **Arquivamento de documentos legais** – criar PDFs em escala de cinza imutáveis que não podem ser editados.  
- **Relatórios prontos para impressão** – garantir saída preto e branco consistente para impressão em massa.  
- **Fluxos de trabalho de conformidade** – combinar redaction com rasterização em escala de cinza para atender a regulamentos rigorosos de privacidade de dados.

## Problemas Comuns e Soluções

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| O arquivo de saída é maior que o esperado | DPI configurado muito alto ou compressão de imagem desativada | Reduza o DPI (ex.: 150) ou habilite a compressão em `RasterizationOptions`. |
| O texto aparece borrado | DPI insuficiente para o tamanho da fonte original | Aumente o DPI para 300 ou mais. |
| Processo lança `OutOfMemoryError` em documentos grandes | Todo o documento carregado na memória | Use APIs de streaming ou processe páginas em lotes, se suportado. |
| Escala de cinza não aplicada | Opção avançada não adicionada corretamente | Verifique se `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` é chamado antes de `save()`. |

## Perguntas Frequentes

**Q: Posso converter documentos para escala de cinza sem rasterização?**  
A: No GroupDocs.Redaction, a opção de escala de cinza está vinculada à rasterização, que garante resultados consistentes e adiciona uma camada de segurança.

**Q: Quais formatos de documento suportam rasterização em escala de cinza?**  
A: Todos os principais formatos suportados pelo GroupDocs.Redaction — incluindo DOCX, PDF, XLSX, PPTX, RTF e mais de 100 outros — podem ser rasterizados e convertidos para escala de cinza.

**Q: A rasterização afetará o tamanho dos meus documentos?**  
A: Sim. Arquivos com muito texto podem crescer, enquanto arquivos com muitas imagens podem diminuir. As configurações de DPI têm o maior impacto.

**Q: É possível reverter o processo de rasterização em escala de cinza?**  
A: Não. A rasterização é unidirecional; mantenha um backup do original se precisar reverter.

**Q: Como posso otimizar a qualidade de documentos rasterizados em escala de cinza?**  
A: Use um DPI mais alto (300 + para qualidade de impressão) e escolha PDF como formato de saída para os melhores resultados de arquivamento.

## Conclusão

Agora você tem uma receita completa e pronta para produção para **rasterizar PDF em escala de cinza** usando GroupDocs.Redaction para Java. Ao habilitar a rasterização, adicionar a opção avançada de escala de cinza e gerenciar recursos de forma responsável, você pode produzir documentos seguros e adequados para impressão que atendem aos padrões de conformidade e apresentam consistência em qualquer visualizador.

---

**Última atualização:** 2026-05-17  
**Testado com:** GroupDocs.Redaction 23.11 for Java  
**Autor:** GroupDocs  

## PALAVRAS‑CHAVE‑ALVO:

**Palavra‑chave principal (MAIOR PRIORIDADE):**  
how to rasterize pdf

**Palavras‑chave secundárias (SUPORTE):**  
java pdf to image, apply grayscale filter pdf

## Tutoriais Relacionados

- [Tutoriais de Opções de Rasterização para GroupDocs.Redaction Java](/redaction/java/rasterization-options/)
- [Como usar groupdocs redaction para Java: Pré‑Rasterização em Documentos Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Rasterização de Ruído Personalizada em Java&#58; Proteger Informações Sensíveis com GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)