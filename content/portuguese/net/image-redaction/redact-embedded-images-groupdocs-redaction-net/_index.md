---
date: '2026-10-16'
description: Aprenda a usar o GroupDocs para ocultar imagens incorporadas em documentos
  do Word usando a API GroupDocs.Redaction .NET, mantendo os dados sensíveis seguros.
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: Como usar o GroupDocs para ocultar imagens incorporadas em documentos
  do Word com a API .NET. Proteja visualizações confidenciais de forma rápida e confiável.
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: Como usar o GroupDocs para ocultar imagens no Word com .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: Como usar o GroupDocs para ocultar imagens no Word com .NET
type: docs
url: /pt/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar o GroupDocs para redigir imagens no Word com .NET

Quando você precisa proteger imagens confidenciais em um arquivo Microsoft Word, **como usar o GroupDocs** se torna a primeira pergunta. Este tutorial orienta você em cada passo necessário para localizar, mascarar e remover permanentemente imagens incorporadas, garantindo que informações sensíveis nunca vazem.

## Respostas rápidas
- **O GroupDocs pode redigir todas as imagens automaticamente?** Sim, você pode iterar por cada imagem e aplicar `ImageAreaRedaction`.
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Preciso de uma licença para desenvolvimento?** Um teste gratuito funciona para testes; uma licença permanente é necessária para produção.
- **O layout original será preservado?** A API mantém o texto e a formatação intactos enquanto oculta a área da imagem.
- **Quão rápido é o processo?** O GroupDocs.Redaction pode processar documentos de 200 páginas em menos de 2 segundos em um servidor típico.

## O que é o GroupDocs.Redaction?
GroupDocs.Redaction é uma biblioteca .NET que permite a redação programática de texto, imagens e metadados em mais de 20 formatos de documento. Ela processa arquivos sem a necessidade de ter o Microsoft Office instalado, tornando‑a ideal para automação no lado do servidor. Oferece APIs para redigir texto, imagens e metadados, e suporta processamento em lote, padrões de redação personalizados e relatórios de conformidade.

## Por que usar o GroupDocs para redação de imagens no Word?
A biblioteca suporta **mais de 20 formatos de entrada e saída** e pode redigir imagens em documentos de até 500 MB sem carregar o arquivo inteiro na memória. Seu algoritmo interno `ImageAreaRedaction` garante que a região redigida não possa ser recuperada, atendendo a rigorosos padrões de conformidade.

## Pré‑requisitos
- .NET Framework 4.5+ **ou** .NET Core 3.1+ instalado.
- Conhecimento básico de C# e familiaridade com a estrutura de arquivos do Word.
- Acesso ao pacote NuGet **GroupDocs.Redaction** (teste gratuito ou licenciado).

## Como configurar o GroupDocs.Redaction para .NET

### Como instalar o GroupDocs.Redaction via .NET CLI?
Execute o seguinte comando na pasta do seu projeto: `dotnet add package GroupDocs.Redaction`. Isso adiciona a versão estável mais recente ao seu arquivo de projeto.

```bash
dotnet add package GroupDocs.Redaction
```

### Como instalar o GroupDocs.Redaction usando o Package Manager?
Execute `Install-Package GroupDocs.Redaction` no Console do Package Manager.

```powershell
Install-Package GroupDocs.Redaction
```

### Como obter e aplicar uma licença temporária?
Você pode solicitar uma licença temporária na página [Licença Temporária](https://purchase.groupdocs.com/temporary-license/).  
Uma licença temporária permite avaliar o conjunto completo de recursos sem marcas d'água. Após a compra, coloque o arquivo de licença no seu projeto e carregue‑o conforme mostrado:

```csharp
using GroupDocs.Redaction;
```

## Como redigir imagens incorporadas em um documento Word?
Para redigir imagens, você carrega o documento com uma instância de Redactor, localiza cada imagem, define a área a ser ocultada e aplica ImageAreaRedaction. A API sobrescreve os pixels selecionados, garantindo que o conteúdo visual original não possa ser recuperado, ao mesmo tempo preservando o layout e o texto ao redor.

### Como preparar os caminhos de origem e destino?
Defina os caminhos absolutos para o documento original e o resultado redigido antes de criar quaisquer objetos.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### Como criar e configurar o objeto Redactor?
Redactor é a classe central que carrega um documento e executa operações de redação.  
Crie uma instância de `Redactor` com seu documento:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### Como especificar coordenadas e aplicar a redação de área de imagem?
ImageAreaRedaction é um método que mascara uma região retangular de uma imagem com uma cor sólida.  
Identifique o ponto superior esquerdo (`samplePoint`) e o tamanho (`sampleSize`) da região que deseja ocultar, então chame `ImageAreaRedaction`. Este método sobrescreve os pixels selecionados com uma cor sólida.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### Como verificar o resultado da redação e salvar o arquivo?
Após chamar `Redactor.Apply()`, inspecione o objeto `Result`. Se `IsSuccess` for verdadeiro, escreva o documento modificado no caminho de saída.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## Problemas comuns e dicas de solução
- **Erros de coordenadas:** Certifique-se de que os valores X/Y estejam dentro dos limites da imagem; caso contrário, a API lança uma `ArgumentOutOfRangeException`.
- **Licença ausente:** Uma licença de teste expira após 30 dias; substitua‑a por uma permanente para evitar falhas em tempo de execução.
- **Formato não suportado:** Verifique se a extensão do arquivo está entre os mais de 20 formatos listados na documentação; arquivos `.doc` mais antigos podem precisar ser convertidos para `.docx` primeiro.

## Aplicações práticas

1. **Relatórios confidenciais:** Redija logotipos ou gráficos antes da distribuição externa.
2. **Memorandos jurídicos:** Oculte fotografias de clientes ou IDs escaneados que contenham dados pessoais.
3. **Contratos comerciais:** Mascarar diagramas proprietários que revelam segredos comerciais.
4. **Publicações governamentais:** Remover imagens de satélite sensíveis de PDFs públicos gerados a partir do Word.

## Considerações de desempenho
- Processar documentos sequencialmente ao lidar com grandes lotes para manter o uso de memória baixo.
- Use o `RedactorOptions` para limitar o número de threads se você estiver executando em um servidor com recursos limitados.
- Libere a instância `Redactor` prontamente com `using` para liberar recursos não gerenciados.

## Conclusão
Agora você sabe **como usar o GroupDocs** para redigir de forma confiável imagens incorporadas em arquivos Word usando a API .NET. Seguindo os passos acima, você pode incorporar essa capacidade em qualquer pipeline de processamento de documentos, garantindo que imagens confidenciais nunca deixem sua organização.

Para uma exploração mais aprofundada, experimente outros tipos de redação (texto, metadados) e integre a biblioteca em serviços web, workers em segundo plano ou Azure Functions.

## Perguntas frequentes

**Q: Posso redigir várias imagens em uma única passagem?**  
A: Sim, itere sobre cada nó de imagem e chame `ImageAreaRedaction` para cada região que precisar ocultar.

**Q: O GroupDocs.Redaction suporta arquivos Word protegidos por senha?**  
A: Absolutamente. Forneça a senha ao construir o objeto `Redactor`, e a biblioteca abrirá o documento de forma segura.

**Q: Quais formatos de arquivo posso processar além de DOCX?**  
A: A API manipula DOC, DOCX, RTF, HTML, PDF e mais de 20 outros formatos, permitindo que você construa um serviço universal de redação.

**Q: Como testar a redação sem uma licença?**  
A: Use uma licença temporária do portal GroupDocs; ela habilita a funcionalidade completa por 30 dias sem marcas d'água.

**Q: Onde posso obter ajuda se encontrar problemas?**  
A: Visite o fórum [Suporte Gratuito GroupDocs](https://forum.groupdocs.com/c/redaction/33) para assistência da comunidade ou entre em contato com as vendas da GroupDocs para suporte empresarial.

## Recursos adicionais

- **Documentação:** [Documentação do GroupDocs Redaction](https://docs.groupdocs.com/redaction/net/)
- **Referência da API:** [Referência da API GroupDocs](https://reference.groupdocs.com/redaction/net)
- **Download:** [Últimas versões](https://releases.groupdocs.com/redaction/net/)

---

**Última atualização:** 2026-10-16  
**Testado com:** GroupDocs.Redaction 23.12 for .NET  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Como Redigir Documentos com GroupDocs.Redaction .NET – Um Guia Completo](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redigir e Salvar Documentos Groupdocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Domine a Redação de Frases Exatas Sensível a Maiúsculas com GroupDocs.Redaction .NET para Segurança de Documentos](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}