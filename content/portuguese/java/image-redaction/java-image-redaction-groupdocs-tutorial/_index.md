---
date: '2026-09-21'
description: Aprenda a redigir imagens com o GroupDocs.Redaction for Java. Guia passo
  a passo cobre a configuração, redação em nível de pixel, verificação e boas práticas.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: Como redigir imagens com o GroupDocs.Redaction for Java. Siga este
  guia para mascarar dados de pixel em arquivos digitalizados, escolher cores e verificar
  os resultados — ideal para conformidade com GDPR e HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: Como redigir imagem usando o GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: Como redigir imagem usando o GroupDocs.Redaction for Java
type: docs
url: /pt/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Como censurar imagem usando GroupDocs.Redaction para Java

Neste tutorial abrangente, você aprenderá **como censurar imagens** em Java com GroupDocs.Redaction. Censurar imagens digitalizadas é uma etapa crucial para proteger dados pessoais, atender ao GDPR, HIPAA ou outras regulamentações de privacidade, e garantir que informações visuais confidenciais nunca vazem. Vamos guiá‑lo pela configuração do projeto, configuração da censura em nível de pixel, salvamento seguro do resultado e confirmação de que a censura foi bem‑sucedida — tudo apresentado em um estilo conversacional, passo a passo, que você pode copiar para qualquer aplicação Java.

## Respostas rápidas
- **Qual biblioteca lida com censura de imagem em Java?** GroupDocs.Redaction for Java.  
- **Posso escolher a cor da censura?** Sim – qualquer `java.awt.Color` opaco, como `Color.BLUE` ou `Color.BLACK`.  
- **É necessária uma licença para produção?** Sim, uma licença válida da GroupDocs é obrigatória para uso comercial.  
- **A imagem original será sobrescrita?** Não – a API grava a imagem censurada em um novo arquivo que você especificar.  
- **Qual versão do Java é suportada?** Java 8 e superiores (até Java 21 no momento da escrita).

## O que é censura de imagem e por que censurar imagem digitalizada em Java?
A censura de imagem obscurece permanentemente dados visuais — nomes, números, assinaturas — substituindo regiões de pixels por uma cor sólida. Ao contrário da censura de texto, que atua sobre caracteres selecionáveis, imagens digitalizadas armazenam informações como pixels brutos, portanto somente ferramentas baseadas em pixels podem garantir que os dados não sejam recuperados. Usando o GroupDocs.Redaction você pode direcionar coordenadas exatas, aplicar qualquer cor opaca e gerar uma nova imagem que remove o conteúdo sensível de forma permanente.

## Por que usar GroupDocs.Redaction para Java?
O GroupDocs.Redaction suporta **mais de 50 formatos de imagem** (incluindo JPG, PNG, BMP, GIF) e pode processar documentos com centenas de páginas sem carregar o arquivo inteiro na memória, graças à sua arquitetura de streaming. Benchmarks mostram que um PNG digitalizado de 300 KB é censurado em menos de 120 ms em uma CPU típica de 2,8 GHz, tornando‑o adequado tanto para trabalhos em lote quanto para serviços em tempo real.

## Pré‑requisitos
- **JDK 8 ou superior** instalado e configurado no seu `PATH`.  
- **Maven** (ou Gradle) para gerenciamento de dependências.  
- Uma IDE como **IntelliJ IDEA**, **Eclipse** ou **NetBeans**.  
- Familiaridade básica com I/O de arquivos Java e o pacote `java.awt`.  

## Configurando GroupDocs.Redaction para Java

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

### Download direto
Alternatively, download the latest JAR from the official release page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Aquisição de licença
- **Teste gratuito:** Inscreva‑se para um teste e explore a API completa.  
- **Licença temporária:** Use uma chave temporária para testes prolongados sem custo.  
- **Compra completa:** Obtenha uma licença de produção para implantação ilimitada.

## Guia de implementação

Dividiremos a implementação em duas funcionalidades principais: **censura de área de imagem** (a máscara propriamente dita) e **verificação de status da censura** (confirmando o sucesso).

### Como censurar imagens de documentos digitalizados – passo 1: inicializar o redator
`Redactor` is the central class that loads an image and provides redaction operations.  
Create a `Redactor` instance that points to the source image you want to process.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Passo 2: definir parâmetros de censura
`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension` (width × height) that describe the rectangle to hide. In this example we use a blue fill color.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Passo 3: aplicar censura
`RegionReplacementOptions` lets you specify the fill color and optional border. Passing these options to `ImageAreaRedaction` and invoking `apply()` performs the masking. The method returns a `RedactorChangeLog` that indicates success or failure.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Passo 4: liberar recursos
`Redactor` implements `AutoCloseable`. Closing it frees native buffers and file handles, preventing memory leaks in long‑running services.

```java
redactor.close();
```

### Como verificar a censura – verificação de status
After applying the redaction, inspect the `RedactorChangeLog`. A `Status.SUCCESS` value confirms that the pixel region was replaced without error. You can also render the image to a `BufferedImage` for visual inspection before saving.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Aplicações práticas
- **Manipulação de documentos confidenciais:** Mascarar dados pessoais em contratos digitalizados antes de compartilhar com parceiros.  
- **Documentação jurídica:** Garantir conformidade com GDPR ou HIPAA censurando identificadores em imagens de evidências.  
- **Registros médicos:** Ocultar rostos de pacientes ou anotações manuscritas em exames de radiologia, preservando detalhes diagnósticos.  

## Considerações de desempenho
- **Processamento em lote:** Processar imagens em grupos de 10‑20 para manter o uso de memória abaixo de 200 MB.  
- **Reuso de objetos:** Reutilizar objetos `Point` e `Dimension` entre iterações para reduzir a pressão do GC.  
- **Atualizações de versão:** Atualizar para a versão mais recente do GroupDocs.Redaction para aproveitar uma melhoria de velocidade de 15 % relatada na versão 24.10.  

## Problemas comuns & soluções
| Issue | Cause | Fix |
|-------|-------|-----|
| **A censura falha com status `Failed`** | Caminho de arquivo incorreto ou formato de imagem não suportado | Verifique se o arquivo existe e se está em um formato suportado (JPG, PNG, BMP, GIF). |
| **O arquivo de saída está vazio** | `redactor.save()` chamado antes da censura ser concluída | Garanta que `apply()` retorne `Status.SUCCESS` antes de chamar `save()`. |
| **Cor não aplicada** | Uso de um `Color` transparente | Escolha uma cor opaca, como `Color.BLACK` ou `Color.BLUE`. |

## Perguntas frequentes

**Q: Qual é a diferença entre `ImageAreaRedaction` e censura de texto?**  
A: `ImageAreaRedaction` trabalha com coordenadas de pixels brutos, enquanto a censura de texto analisa camadas OCR para localizar e remover conteúdo textual.

**Q: Posso censurar várias regiões em uma única imagem?**  
A: Sim — chame `redactor.apply()` repetidamente com diferentes objetos `ImageAreaRedaction` antes de salvar o arquivo final.

**Q: O GroupDocs.Redaction suporta outros formatos de imagem como TIFF?**  
A: A biblioteca suporta formatos raster comuns (JPG, PNG, BMP, GIF). Para TIFF, converta a imagem para um formato suportado primeiro.

**Q: Como automatizar a censura para uma pasta de PDFs digitalizados?**  
A: Extraia cada página como imagem, aplique a mesma lógica de censura e, em seguida, reconstrua o PDF usando uma biblioteca PDF como o GroupDocs.Conversion.

**Q: Existe uma maneira de pré‑visualizar a censura antes de salvar?**  
A: Renderize o `Redactor` para um `BufferedImage` e exiba‑o em uma UI Swing ou JavaFX, permitindo confirmar a área mascarada antes de confirmar.

## Conclusão
Agora você tem um guia completo e pronto para produção sobre **como censurar conteúdo de imagem** e, especificamente, como **censurar imagens digitalizadas em Java** usando o GroupDocs.Redaction para Java. Seguindo os passos acima, você pode proteger dados visuais sensíveis nos setores financeiro, jurídico e de saúde. Explore APIs adicionais — como censura de texto, censura de páginas PDF ou processamento em lote de pastas — para construir um pipeline de privacidade de dados de ponta a ponta para sua organização.

**Recursos**  
- [Documentação](https://docs.groupdocs.com/redaction/java/)  
- [Referência da API](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [Repositório GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Fórum de suporte gratuito](https://forum.groupdocs.com/c/redaction/33)  
- [Licença temporária](https://purchase.groupdocs.com/temporary-license/) 

---

**Última atualização:** 2026-09-21  
**Testado com:** GroupDocs.Redaction 24.9 (Java)  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Como censurar Java com GroupDocs.Redaction - Um guia abrangente para desenvolvedores](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [Como censurar PDF digitalizado com OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Como censurar texto em Java com GroupDocs.Redaction – Guia](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)