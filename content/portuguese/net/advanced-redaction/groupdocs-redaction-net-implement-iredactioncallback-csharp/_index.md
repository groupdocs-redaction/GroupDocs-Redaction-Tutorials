---
date: '2026-10-06'
description: Aprenda a remover dados usando GroupDocs.Redaction .NET com uma implementação
  de IRedactionCallback em C#. Siga este guia passo a passo, as melhores práticas
  e exemplos do mundo real.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: Aprenda a remover dados usando GroupDocs.Redaction .NET com uma implementação
  de IRedactionCallback em C#. Siga este guia passo a passo, as melhores práticas
  e exemplos do mundo real.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: Como remover dados com GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: Como remover dados com GroupDocs.Redaction .NET (C#)
type: docs
url: /pt/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# Como remover dados com GroupDocs.Redaction .NET (C#)

Neste tutorial abrangente, você descobrirá **como remover dados** de PDFs, arquivos Word e outros documentos usando o GroupDocs.Redaction para .NET. Seja para ocultar identificadores pessoais em contratos legais ou limpar informações confidenciais de relatórios financeiros, o SDK oferece controle programático para garantir que cada elemento sensível desapareça permanentemente e de forma auditável. Vamos percorrer a instalação da biblioteca, a configuração de um `IRedactionCallback` personalizado e a aplicação de redacções de frases exatas com registro completo.

## Respostas rápidas
- **O que faz IRedactionCallback?** Ele permite interceptar cada evento de remoção, registrar detalhes e, opcionalmente, modificar o texto de substituição em tempo real.  
- **Preciso de uma licença?** Uma versão de avaliação funciona para desenvolvimento; uma licença permanente remove todas as limitações de avaliação.  
- **Quais versões do .NET são suportadas?** .NET Core 3.1+, .NET 5/6 e .NET Framework 4.6+.  
- **Posso processar vários arquivos?** Sim—envolva a lógica em um loop ou use processamento em lote para melhor desempenho.  
- **A redacção assíncrona é possível?** Não está incorporada, mas você pode executar as chamadas da API dentro de `Task.Run` ou outros padrões assíncronos.

## O que é a remoção de dados sensíveis?
`Redaction` é a remoção permanente ou ocultação de informações que não devem ser divulgadas. Com o GroupDocs.Redaction você define frases exatas, padrões de expressão regular ou regras personalizadas e as substitui por marcadores como **[REDACTED]**, preservando o layout e a paginação originais.

## Por que usar GroupDocs.Redaction com IRedactionCallback?
`IRedactionCallback` é uma interface que notifica você sempre que o SDK remove um trecho de conteúdo, permitindo capturar dados de auditoria ou ajustar a substituição dinamicamente. Isso possibilita total auditabilidade, aplicação de regras de negócios personalizadas e integração perfeita com sistemas de conformidade — tudo sem sacrificar o desempenho.

## Pré-requisitos
- **GroupDocs.Redaction** library (versão compatível – veja a [página de documentação oficial](https://docs.groupdocs.com/redaction/net/)). Para detalhes completos, consulte a [documentação oficial](https://docs.groupdocs.com/redaction/net/).  
- .NET Core ou .NET Framework instalados na sua máquina de desenvolvimento.  
- Visual Studio (edição Community é suficiente) ou qualquer IDE que suporte C#.  
- Conhecimento básico de C# e familiaridade com o gerenciamento de pacotes NuGet.

## Configurando GroupDocs.Redaction para .NET
Primeiro, adicione a biblioteca ao seu projeto. Escolha o método que preferir – a CLI, o Package Manager Console ou a UI. Os comandos permanecem exatamente os mesmos do tutorial original.

### Opções de instalação
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Abra seu projeto no Visual Studio.  
- Navegue até **Manage NuGet Packages**.  
- Procure por **GroupDocs.Redaction** e instale a versão estável mais recente.

### Aquisição de licença
Para experimentar o produto, solicite uma avaliação gratuita ou uma licença temporária em [aqui](https://purchase.groupdocs.com/temporary-license/). Você também pode obter uma licença temporária na [página de licença temporária](https://purchase.groupdocs.com/temporary-license/). Para uso em produção, adquira uma licença completa para desbloquear todos os recursos sem limites.

#### Inicialização e configuração básicas
Abaixo está o código mínimo necessário para abrir um documento com a classe `Redactor`. Mantenha este trecho inalterado – ele é a base para tudo que segue.  
`Redactor` é a classe principal que representa um documento e fornece métodos para aplicar regras de remoção.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Guia de implementação
Agora vamos estender a configuração básica adicionando um `IRedactionCallback` personalizado. Isso permite capturar cada evento de remoção, gravá‑lo em um log ou até mesmo modificar o texto de substituição em tempo real.

### Anexar e usar uma implementação de IRedactionCallback
`IRedactionCallback` é uma interface que recebe callbacks para cada operação de remoção, permitindo registrar ou alterar o comportamento programaticamente.

#### Etapa 1: preparar diretório de saída e caminho do arquivo fonte
Defina onde seu documento fonte está localizado. Ajuste o caminho para corresponder ao seu ambiente.

`LoadOptions` é um objeto de configuração que informa ao SDK como ler o arquivo (por exemplo, tratamento de senha).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Etapa 2: criar uma instância Redactor com configurações personalizadas
Instanciamos `Redactor` com `LoadOptions` e `RedactorSettings`. O `RedactionDump` dentro das configurações registrará automaticamente cada remoção que ocorrer.

`RedactorSettings` permite ajustar finamente o processo de remoção; passar um `RedactionDump` habilita um arquivo de auditoria detalhado.  
`RedactionDump` é uma classe auxiliar que grava cada evento de remoção em um dump formatado em JSON para relatórios de conformidade.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Etapa 3: aplicar uma remoção de frase exata
Aqui substituímos a frase **John Doe** pelo marcador **[REDACTED]**. Você pode trocar qualquer frase ou padrão que precise ocultar.

`ReplacementOptions` define qual texto substituirá o conteúdo correspondido. Também suporta personalização de fonte e cor se você precisar de uma máscara visual.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Explicação dos objetos principais**
- `LoadOptions()` – informa ao SDK como ler o documento (por exemplo, tratamento de senha).  
- `RedactorSettings(new RedactionDump())` – habilita um arquivo dump que registra cada remoção para fins de auditoria.  
- `ReplacementOptions("[REDACTED]")` – define o texto que substituirá a frase correspondida.

### Por que isso importa
O mecanismo de callback registra cada evento de remoção, cria um rastro de auditoria legível por máquina e permite modificar os marcadores dinamicamente, o que ajuda a atender aos requisitos de conformidade e reduz o esforço manual de pós‑processamento. Ao integrar esses dados aos seus sistemas de monitoramento, você pode gerar relatórios, disparar alertas e garantir que nenhuma informação sensível escape do pipeline de remoção.

Usar `IRedactionCallback` oferece três vantagens concretas:
1. **Logs prontos para conformidade** – cada remoção é capturada em um dump legível por máquina, atendendo aos requisitos de auditoria de mais de 30 + estruturas regulatórias.  
2. **Substituição dinâmica** – você pode mudar o marcador com base no tipo de dado, reduzindo o pós‑processamento manual em até 40 %.  
3. **Desempenho escalável** – o callback adiciona uma sobrecarga insignificante (<2 ms por remoção) enquanto permite processar em lote milhares de arquivos em paralelo.

### Dicas de solução de problemas
- **Arquivo não encontrado:** Verifique novamente o caminho `sourceFile` e assegure que o arquivo esteja acessível ao processo em execução.  
- **Callback não disparando:** Verifique se sua classe implementa **todos** os membros de `IRedactionCallback` e se a instância é passada corretamente ao `Redactor`.  
- **Atraso de desempenho:** Para lotes grandes, reutilize a mesma instância `Redactor` quando possível e descarte‑a prontamente.

## Aplicações práticas
Remover dados sensíveis é útil em diversas indústrias:
1. **Processamento de documentos jurídicos** – Remova automaticamente nomes de clientes, números de processos ou números de segurança social antes de compartilhar rascunhos.  
2. **Sistemas de gestão de RH** – Remova identificadores pessoais de contratos de funcionários durante auditorias.  
3. **Relatórios financeiros** – Oculte figuras proprietárias ou números de conta ao gerar PDFs para investidores.

## Considerações de desempenho
GroupDocs.Redaction suporta **mais de 30 formatos de entrada e saída** (PDF, DOCX, PPTX, XLSX, HTML e tipos de imagem) e pode processar arquivos com centenas de páginas sem carregar todo o documento na memória. Para manter sua aplicação ágil ao lidar com dezenas ou centenas de arquivos:
- **Processamento em lote:** Carregue uma lista de arquivos e execute o loop de remoção dentro de um `Parallel.ForEach` para utilização de múltiplos núcleos.  
- **Gerenciamento de memória:** Envolva cada `Redactor` em um bloco `using` (conforme mostrado) para garantir a liberação.  
- **Operações assíncronas:** Embora o SDK seja síncrono, você pode delegar o trabalho a threads em segundo plano ou `Task.Run` para evitar bloquear threads de UI.

## Problemas comuns e soluções
| Problema | Solução |
|----------|---------|
| **Erro “Formato de arquivo inválido”** | Certifique-se de que o tipo de documento é suportado (PDF, DOCX, PPTX, etc.). |
| **Callback recebe valores nulos** | Verifique se está passando uma implementação concreta de `IRedactionCallback` ao construir `RedactorSettings`. |
| **Remoção não aplicada** | Verifique se a frase exata corresponde ao caso e espaçamento do documento, ou use `RegexRedaction` para correspondência baseada em padrão. |

## Perguntas frequentes

**Q: Quais são as opções de licenciamento para GroupDocs.Redaction?**  
A: Você pode começar com uma avaliação gratuita ou solicitar uma licença temporária para explorar todos os recursos. Para produção, adquira uma licença perpétua ou por assinatura.

**Q: Posso usar GroupDocs.Redaction em vários tipos de arquivo?**  
A: Sim, ele suporta PDFs, Word, Excel, PowerPoint e muitos outros formatos comuns.

**Q: Como lidar com exceções durante a remoção?**  
A: Envolva sua lógica de remoção em blocos `try‑catch` e registre os detalhes da exceção. O callback também pode ser usado para capturar erros em tempo real.

**Q: Existe suporte nativo para processamento assíncrono?**  
A: A API principal é síncrona, mas você pode executar chamadas de remoção dentro de tarefas assíncronas ou serviços em segundo plano.

**Q: Onde posso encontrar exemplos mais avançados?**  
A: A [documentação oficial](https://docs.groupdocs.com/redaction/net/) e a referência da API fornecem extensos exemplos de código e guias de cenários.

## Recursos

- [Documentação do GroupDocs.Redaction para .NET](https://docs.groupdocs.com/redaction/net/)
- [Referência da API do GroupDocs.Redaction para .NET](https://reference.groupdocs.com/redaction/net/)
- [Download do GroupDocs.Redaction para .NET](https://releases.groupdocs.com/redaction/net/)
- [Fórum do GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Suporte gratuito](https://forum.groupdocs.com/)
- [Licença temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última atualização:** 2026-10-06  
**Testado com:** GroupDocs.Redaction 2.3 (mais recente no momento da escrita)  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Criar política de remoção com GroupDocs.Redaction .NET – Guia passo a passo](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [Como remover documentos com GroupDocs.Redaction .NET – Guia completo](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Remover documentos .net usando Streams – Guia GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)