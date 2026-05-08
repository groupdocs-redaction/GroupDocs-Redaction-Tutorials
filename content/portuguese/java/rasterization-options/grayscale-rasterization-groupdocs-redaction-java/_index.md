---
date: '2026-02-13'
description: Aprenda a criar PDF em escala de cinza usando o GroupDocs.Redaction para
  Java, converta PDF em escala de cinza com segurança, preservando a qualidade do
  documento.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: Como criar PDF em tons de cinza com GroupDocs.Redaction Java – Proteja e otimize
  seus documentos
type: docs
url: /pt/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java: Guia de Rasterização em Tons de Cinza

## Introdução

Se você precisa **criar pdf em tons de cinza** mantendo seus documentos seguros e com aparência profissional, você está no lugar certo. Neste tutorial vamos percorrer os passos exatos para converter arquivos coloridos DOCX, PDF ou outros arquivos suportados em uma versão limpa, rasterizada em tons de cinza usando o GroupDocs.Redaction para Java. Você aprenderá por que a rasterização adiciona uma camada extra de segurança, como configurar a biblioteca e como gerenciar recursos de forma eficiente — tudo em um estilo conversacional, passo a passo.

## Respostas Rápidas
- **O que a rasterização em tons de cinza faz?** Converte cada página de um documento em uma imagem de alta resolução e, em seguida, aplica um filtro em tons de cinza, removendo todas as informações de cor.  
- **Por que usar o GroupDocs.Redaction para isso?** Ele combina segurança de redação com opções poderosas de rasterização em uma única API.  
- **Quais formatos são suportados?** DOCX, PDF, XLSX, PPTX, RTF e muitos mais.  
- **Preciso de uma licença?** Uma licença válida do GroupDocs.Redaction é necessária para uso em produção; uma versão de avaliação está disponível para testes.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.

## O que é **criar pdf em tons de cinza**?

Criar um PDF em tons de cinza significa converter cada elemento visual do documento original em tons de cinza. O resultado é um arquivo menor, adequado para impressão, que elimina distrações relacionadas à cor e adiciona um benefício sutil de segurança, pois o conteúdo passa a ser baseado em imagem.

## Por que usar rasterização em tons de cinza com GroupDocs.Redaction?

- **Segurança aprimorada** – páginas rasterizadas não podem ser selecionadas, copiadas ou editadas como texto.  
- **Aparência consistente** – as cores são removidas, proporcionando um visual uniforme e profissional.  
- **Amplo suporte a formatos** – a mesma API funciona para DOCX, PDF, PPTX e mais.  
- **Controle fino** – você pode ajustar DPI, formato de saída e opções avançadas como conversão para tons de cinza.

## Pré‑requisitos

- Java Development Kit (JDK) 8 ou mais recente. Verifique com `java -version`.  
- Uma IDE (IntelliJ IDEA, Eclipse ou NetBeans) para facilitar a codificação e depuração.  
- GroupDocs.Redaction para Java adicionado via Maven ou Gradle.  
- Um documento de exemplo (por exemplo, um DOCX multipágina) no qual você possa experimentar com segurança.  
- Espaço em disco suficiente para a saída rasterizada (arquivos raster podem ser maiores que a origem).

## Importar Pacotes

Configurar as importações corretas é como organizar sua caixa de ferramentas antes de um projeto. As importações a seguir dão acesso à classe central Redactor e às opções de rasterização que usaremos.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Etapa 1: Inicializar o Objeto Redactor

Criar uma instância de `Redactor` abre a porta para todas as capacidades de processamento de documentos.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

Substitua `Constants.MULTIPAGE_SAMPLE_DOCX` pelo caminho do arquivo que você deseja converter para um PDF em tons de cinza.

## Etapa 2: Configurar Opções de Salvamento

`SaveOptions` define como o arquivo final será gravado. Adicionar um sufixo ajuda a manter o arquivo original intacto.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

A saída será nomeada `yourfile_scan.docx` (ou o formato que você especificar posteriormente).

## Etapa 3: Habilitar Rasterização

Ativar a rasterização indica ao mecanismo que ele deve renderizar cada página como uma imagem antes de salvar.

```java
so.getRasterization().setEnabled(true);
```

A rasterização é a base para criar um PDF em tons de cinza porque converte o documento em uma representação baseada em imagem.

## Etapa 4: Aplicar Conversão para Tons de Cinza

Agora adicionamos o filtro de tons de cinza ao pipeline de rasterização.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

Esta opção força cada pixel a ser renderizado em tons de cinza, proporcionando o resultado **criar pdf em tons de cinza** que você deseja.

## Etapa 5: Executar a Transformação do Documento

A chamada `save` executa toda a cadeia de processamento.

```java
redactor.save(so);
```

Depois que esta linha for executada, você encontrará um novo arquivo no disco que está totalmente rasterizado, em tons de cinza e salvo com o sufixo `_scan`.

## Etapa 6: Gerenciamento Adequado de Recursos

Limpar recursos evita bloqueios de arquivos e vazamentos de memória.

```java
finally { redactor.close(); }
```

Para Java moderno você também pode usar o padrão try‑with‑resources, que fecha automaticamente o `Redactor`:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Ambas as abordagens são seguras; a última é mais concisa.

## Opções Avançadas de Configuração

### Ajustar DPI para Qualidade ou Tamanho

DPI mais alto gera imagens mais nítidas (bom para impressão), enquanto DPI mais baixo reduz o tamanho do arquivo.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Escolher um Formato de Saída

Você pode forçar o resultado rasterizado a um formato de contêiner específico, como PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Casos de Uso Comuns

- **Arquivamento de documentos legais** – criar PDFs em tons de cinza imutáveis que não podem ser editados.  
- **Relatórios prontos para impressão** – garantir saída preto‑e‑branco consistente para impressão em massa.  
- **Fluxos de trabalho de conformidade** – combinar redação com rasterização em tons de cinza para atender a regulamentos rigorosos de privacidade de dados.

## Problemas Comuns e Soluções

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| Arquivo de saída maior que o esperado | DPI configurado muito alto ou compressão de imagem desativada | Reduza o DPI (ex.: 150) ou habilite compressão em `RasterizationOptions`. |
| Texto aparece borrado | DPI insuficiente para o tamanho da fonte original | Aumente o DPI para 300 ou mais. |
| Processo lança `OutOfMemoryError` em documentos grandes | Documento inteiro carregado na memória | Use APIs de streaming ou processe páginas em lotes, se suportado. |
| Tons de cinza não aplicados | Opção avançada não adicionada corretamente | Verifique se `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` é chamado antes de `save()`. |

## Perguntas Frequentes

**P: Posso converter documentos para tons de cinza sem rasterização?**  
R: No GroupDocs.Redaction, a opção de tons de cinza está vinculada à rasterização, que garante resultados consistentes e adiciona segurança.

**P: Quais formatos de documento suportam rasterização em tons de cinza?**  
R: Todos os principais formatos suportados pelo GroupDocs.Redaction — incluindo DOCX, PDF, XLSX, PPTX, RTF e mais — podem ser rasterizados e convertidos para tons de cinza.

**P: A rasterização afetará o tamanho dos meus documentos?**  
R: Sim. Arquivos com muito texto podem crescer, enquanto arquivos com muitas imagens podem diminuir. As configurações de DPI têm o maior impacto.

**P: É possível reverter o processo de rasterização em tons de cinza?**  
R: Não. A rasterização é unidirecional; mantenha um backup do original caso precise reverter.

**P: Como otimizar a qualidade de documentos rasterizados em tons de cinza?**  
R: Use um DPI mais alto (300 + para qualidade de impressão) e escolha um formato de saída adequado (PDF é comum para arquivamento).

## Conclusão

Agora você tem uma receita completa, pronta para produção, para **criar pdf em tons de cinza** usando o GroupDocs.Redaction para Java. Ao habilitar a rasterização, adicionar a opção avançada de tons de cinza e gerenciar recursos de forma responsável, você pode produzir documentos seguros, adequados para impressão e que atendem aos padrões de conformidade.

---

**Última atualização:** 2026-02-13  
**Testado com:** GroupDocs.Redaction 23.11 para Java  
**Autor:** GroupDocs  

---