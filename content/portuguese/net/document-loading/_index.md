---
date: 2026-06-11
description: Aprenda a carregar documentos, inclusive a partir de streams e arquivos
  protegidos por senha, usando o GroupDocs.Redaction para .NET.
keywords:
- how to load document
- redact password protected pdf
- load password protected file
- load document from stream
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  headline: How to Load Document with GroupDocs.Redaction for .NET
  type: TechArticle
- questions:
  - answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
    question: Can I load DOCX files the same way I load PDFs?
  - answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
    question: Does the library support loading files from Azure Blob Storage?
  - answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
    question: What happens if I provide the wrong password?
  - answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
    question: Is it possible to load multiple documents simultaneously?
  - answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
    question: Do I need to dispose of the RedactionEngine manually?
  type: FAQPage
title: Como Carregar Documento com GroupDocs.Redaction para .NET
type: docs
url: /pt/net/document-loading/
weight: 2
---

# Como Carregar Documento com GroupDocs.Redaction para .NET

Neste guia, você descobrirá **como carregar documentos** no GroupDocs.Redaction para .NET a partir de uma variedade de fontes — disco local, streams de memória e até arquivos protegidos por senha. Seja construindo um serviço de redação, um pipeline de conformidade automatizado ou um utilitário de desktop simples, dominar essas técnicas de carregamento permite que você prepare qualquer documento para redação segura de forma rápida e confiável.

## Respostas Rápidas
- **Qual é o primeiro passo?** Instale o pacote NuGet GroupDocs.Redaction e adicione o namespace `using GroupDocs.Redaction;`.
- **Posso carregar um PDF a partir de um stream?** Sim — passe um `MemoryStream` contendo os bytes do PDF para o construtor `RedactionEngine`.
- **Como abrir um arquivo protegido por senha?** Forneça a senha como segundo argumento ao criar o `RedactionEngine`.
- **Existe um limite de tamanho de arquivo?** O GroupDocs.Redaction processa arquivos de até 2 GB sem carregar o arquivo inteiro na memória.
- **Preciso de uma licença para desenvolvimento?** Uma licença temporária funciona para testes; uma licença completa é necessária para implantações em produção.

## Como Carregar Documento?
`RedactionEngine` é a classe central que carrega e prepara documentos para redação. Carregue um documento criando uma instância de `RedactionEngine` com o caminho do arquivo (ou stream) e, se necessário, a senha. Essa chamada de uma única linha lê o arquivo, valida o formato e constrói o modelo interno do documento pronto para redação. Por exemplo, carregar um PDF do disco é tão simples quanto `new RedactionEngine("sample.pdf")`. Quando uma senha for necessária, use `new RedactionEngine("secret.pdf", "MyPassword")`. Carregar a partir de um stream segue o mesmo padrão com um argumento `MemoryStream`.

## O que é GroupDocs.Redaction?
GroupDocs.Redaction é uma biblioteca .NET que permite aos desenvolvedores localizar e remover permanentemente conteúdo sensível de PDF, DOCX, PPTX e mais de 30 outros formatos de arquivo. Ela oferece redação pixel‑perfeita, suporte a OCR e processamento em lote, tornando-a ideal para aplicações orientadas por conformidade que exigem proteção de dados confiável e segura em diversos tipos de documentos.

## Por que Usar GroupDocs.Redaction para Carregamento de Documentos?
GroupDocs.Redaction fornece um mecanismo de streaming de alto desempenho e baixo consumo de memória que pode lidar com arquivos grandes de até 2 GB, além de suportar documentos protegidos por senha prontamente. Essa combinação de velocidade, flexibilidade e segurança a torna a escolha preferida para desenvolvedores que precisam carregar documentos de forma rápida e segura antes de aplicar regras de redação.

- **Amplo suporte a formatos:** Lida com **30+** tipos de documentos, incluindo PDF, Word, Excel, PowerPoint e arquivos de imagem.
- **Streaming de alto desempenho:** Processa arquivos de até **2 GB** usando um mecanismo de streaming de baixa memória, eliminando a necessidade de carregar o arquivo completo.
- **Manipulação de senha:** Abre perfeitamente **PDFs e arquivos Office protegidos por senha** com uma única sobrecarga de método, reduzindo a complexidade do código.
- **API thread‑safe:** Permite o carregamento simultâneo de múltiplos documentos em serviços multithread sem condições de corrida.

## Pré-requisitos
- .NET 6.0 ou posterior (a biblioteca também suporta .NET Core 3.1 e .NET Framework 4.6.1+).
- Uma licença válida do GroupDocs.Redaction (licença temporária para testes).
- Acesso aos arquivos de documento que você pretende redigir (caminho local, array de bytes ou stream).

## Carregando Documentos de Diferentes Fontes

### Carregar do Disco Local
Forneça o caminho absoluto ou relativo ao arquivo ao construir o engine. A biblioteca detecta automaticamente o formato e o prepara para redação.

### Carregar de um Stream de Memória
Leia o arquivo em um `byte[]`, envolva‑o em um `MemoryStream` e passe o stream para o construtor. Essa abordagem é perfeita para APIs web que recebem arquivos como uploads.

### Carregar Arquivos Protegidos por Senha
Quando um documento está criptografado, forneça a senha como segundo argumento. O engine descriptografa o arquivo em tempo real e disponibiliza o conteúdo para redação sem etapas adicionais.

## Problemas Comuns e Soluções
- **Erro: “Formato de arquivo não suportado.”**  
  Verifique se a extensão do arquivo corresponde a um formato suportado e se o arquivo não está corrompido. O GroupDocs.Redaction suporta mais de 30 formatos; consulte a referência da API para a lista completa.
- **Exceção relacionada à senha.**  
  Certifique‑se de que a string da senha está correta e de que o arquivo realmente requer senha. Passar uma string vazia para um arquivo protegido acionará um erro de autenticação.
- **Falta de memória para arquivos muito grandes.**  
  Use a sobrecarga de streaming (`RedactionEngine(Stream)`) em vez de carregar o arquivo pelo caminho. Isso mantém o uso de memória baixo mesmo para PDFs com centenas de páginas.

## Perguntas Frequentes

**Q: Posso carregar arquivos DOCX da mesma forma que carrego PDFs?**  
A: Sim — o GroupDocs.Redaction detecta automaticamente o formato DOCX quando você fornece o caminho do arquivo ou stream, portanto nenhum código extra é necessário.

**Q: A biblioteca suporta carregamento de arquivos do Azure Blob Storage?**  
A: Absolutamente. Recupere o blob como um array de bytes ou stream e alimente‑o ao construtor `RedactionEngine`.

**Q: O que acontece se eu fornecer a senha errada?**  
A: O construtor lança uma `PasswordIncorrectException`. Capture essa exceção para solicitar ao usuário a senha correta.

**Q: É possível carregar múltiplos documentos simultaneamente?**  
A: Sim — cada instância de `RedactionEngine` é independente e thread‑safe, permitindo processamento paralelo em serviços de background.

**Q: Preciso descartar o RedactionEngine manualmente?**  
A: O engine implementa `IDisposable`. Chame `Dispose()` ou envolva‑o em um bloco `using` para liberar os manipuladores de arquivo prontamente.

## Recursos Adicionais
- [Como Carregar e Redigir Documentos Usando GroupDocs.Redaction .NET: Um Guia Completo](./groupdocs-redaction-net-load-redact-documents/)
- [Como Redigir com Segurança Documentos Protegidos por Senha Usando GroupDocs.Redaction em .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [Documentação do GroupDocs.Redaction para .NET](https://docs.groupdocs.com/redaction/net/)
- [Referência da API do GroupDocs.Redaction para .NET](https://reference.groupdocs.com/redaction/net/)
- [Download do GroupDocs.Redaction para .NET](https://releases.groupdocs.com/redaction/net/)
- [Fórum do GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [Suporte Gratuito](https://forum.groupdocs.com/)
- [Licença Temporária](https://purchase.groupdocs.com/temporary-license/)

---

**Última Atualização:** 2026-06-11  
**Testado com:** GroupDocs.Redaction 5.5 for .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados
- [Como Carregar e Redigir Documentos Usando GroupDocs.Redaction .NET: Um Guia Completo](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redigir e Salvar Documentos com GroupDocs.Redaction para .NET: Um Guia Completo](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)