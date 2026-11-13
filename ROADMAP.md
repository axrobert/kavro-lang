# Kavro — Roadmap técnico

[Voltar ao README](README.md)

> **Status:** linguagem e ferramentas experimentais, não adequadas para produção. Este repositório publica documentação; os protótipos e os resultados locais abaixo **não estão disponíveis aqui como releases públicas**.

## Como interpretar o progresso

- `[x]` **Concluído no escopo descrito:** há implementação e testes locais identificados. Não implica suporte completo, publicação ou validação em Windows.
- `[ ]` **Pendente:** implementação, integração, validação ou publicação ainda não demonstrada.
- **Experimental:** um protótipo pode funcionar apenas com recursos limitados ou depender de Node.js.

## Visão geral

| Prioridade | Frente | Situação | Próximo bloqueio |
| --- | --- | --- | --- |
| P0 | Semântica, tipos e regressões | Correções locais; integração pendente | Consolidar com o compilador mais recente |
| P1 | Backend Windows x86-64 | Bootstrap P2.0 emite PE32+, código x86-64 e relocations DIR64 para ASLR (subconjunto) + backend histórico | Execução Windows real/ABI, unwind, mais controle de fluxo e paridade |
| P2 | Kavro Studio | Prévia Win32 local P1.7; diagnósticos JSON, F8 e proteção contra edição externa (testes locais) | Integração com o Studio D2.1 e validação de interface no Windows |
| P3 | Memória, ponteiros e FFI | Planejado | Especificação e testes de integração |
| P4 | CLI, testes e distribuição | CLI JS + CLI bootstrap independente e infraestrutura de testes | Consolidação, CI e política de releases |

## Entregas técnicas locais — evidência limitada ao protótipo

As tarefas seguintes foram verificadas em uma linha histórica do compilador (`v0.31.x`), não integradas nem validadas integralmente no Studio Win32 mais recente.

- [x] Casos de regressão para retornos de tipo desconhecido, uso inválido de `void`, limites de `any` e comparação de arrays (P0.1–P0.4; testes automatizados locais).
- [x] Limites de entrada em bytes UTF-8 e validação de orçamentos cooperativos da VM (P0.7C; regressões locais).
- [x] Matriz determinística com 96 programas para comparar comportamento da VM (P0.6; não executa binários Windows).
- [x] Verificação estrutural de sete programas PE32+ com resultados esperados da VM (P0.7B; **não** equivale a execução nativa).
- [x] Pasta `TESTE/` e manifesto SHA-256 em distribuições privadas de avaliação (P4; não configura uma release pública).
- [x] Entrada de terminal `kavro.cmd`/`kavro.sh`, comandos `check`, `run`, `build -o`, `compile`, `doctor`, `--version` e 26 testes de CLI (P0.8; **Node.js 20+ ainda obrigatório**).

- [x] Protótipo Win32 independente com RichEdit, abas, abertura/salvamento e integração local com a CLI (P0.9; build PE32+ GUI verificado, **sem teste de interação Windows e sem integração com D2.1**).
- [x] Prévia Win32 estabilizada com **um controle RichEdit por aba**, estado de edição próprio e verificação de modificações externas antes de salvar (P1.0; compilação cruzada, testes de lógica Go e inspeção estática local; **sem teste visual ou execução Windows**).
- [x] Preservação de formato de arquivos no editor experimental (BOM UTF-8 e LF/CRLF/CR), limite de leitura e escrita em 1 MiB e salvamento sem regravação de arquivo inalterado (P1.1; testes Go, auditoria Node.js e build cruzado; **sem validação interativa Windows**).
- [x] Proteção defensiva de salvamento na prévia Win32: arquivo temporário com sincronização, criação exclusiva em **Salvar como**, preservação básica de permissões, comparação SHA-256 e identidade do arquivo antes de substituir, com segunda verificação após preparar os bytes (P1.2; testes Go, Node.js e compilação cruzada; **sem validação de interface no Windows e sem garantia de bloqueio entre processos**).

- [x] Controle de operações da CLI na prévia Win32: cancelamento explícito (botão e atalho), saída limitada, status distinguindo sucesso, erro, timeout e cancelamento (P1.3; **oito testes funcionais do runner Go em Linux**, dez verificações estruturais e compilação cruzada para Windows x64; **interface real ainda não validada**).

- [x] Protocolo versionado de diagnósticos da CLI `check-json`, com fase, linha e coluna, consumido pela prévia Win32 (P1.4; **18 testes Node locais**, testes do renderizador Go e cross-compilation PE32+; **sem execução Windows e sem integração com D2.1**).

- [x] Navegação F8 ao primeiro erro do compilador na prévia Win32, com vínculo ao arquivo e hash do conteúdo para rejeitar diagnósticos desatualizados (P1.5; testes Go locais e regressões Node, cross-build GUI x64; **sem validação de GUI no Windows e sem integração com D2.1**).

- [x] Coordenadas de diagnóstico coerentes para `LF`, `CRLF` e `CR`, inclusive comentários `//`; validação de posição UTF-16 e seleção de caractere em F8 na prévia independente (P1.6; **14 testes Node, testes Go e compilação cruzada**, ainda sem GUI Windows real ou integração D2.1).

- [x] Vinculação de diagnósticos à origem salva: verificação SHA-256 do arquivo no início do comando, no retorno da CLI e antes de F8, rejeitando mudanças externas ou arquivo removido (P1.7; **testes Go e Node.js locais, sem validação interativa no Windows e sem integração D2.1**).

- [x] **P1.8 — Bootstrap nativo independente da instalação de Node.js:** executável de CLI produzido com Go para Windows x64, com `check`, `build` e `verify-pe`; aceita somente `fn main`, `print`, `let` imutável e expressões inteiras constantes. Gera PE32+ a partir de modelo binário embutido e verificado, com saída estática limitada a 2048 bytes. Testes Go, comparação local com VM e validação estrutural de PE **não equivalem a execução Windows ou cobertura do compilador completo**. O compilador não está escrito em Kavro e **não é self-hosted**.

- [x] **P1.9 — Emissor PE32+ independente de template estático:** o compilador bootstrap Go agora emite instruções x86-64 para operações inteiras, variáveis `let` em pilha e `print` numérico convertido em tempo de execução; constrói cabeçalhos, seções `.text` e `.idata`, IAT e imports WinAPI. Testes Go/Node no Linux, análise estrutural e cross-build Windows x64; **não houve execução nativa no Windows**, paridade completa ou integração D2.1. O resultado está restrito ao subconjunto bootstrap.

- [x] **P2.0 — Relocations/ASLR no bootstrap experimental:** o gerador PE32+ agora cria `.reloc`, entradas `DIR64` de endereços absolutos usados em chamadas à IAT e flags `DYNAMIC_BASE`, `HIGH_ENTROPY_VA` e `NX_COMPAT`. Verificação estrutural, simulação de mudança de base e testes automatizados Linux; **sem execução do carregador Windows**, sem unwind metadata, sem assinatura digital ou validação funcional de ASLR no sistema-alvo. O subconjunto da linguagem não foi ampliado e a IDE D2.1 permanece separada.

## Independência de Node.js e self-hosting — plano incremental

A remoção da dependência do usuário é distinta da implementação do compilador na própria linguagem. A CLI bootstrap já gera código de máquina para um subconjunto restrito; o compilador e o Studio completos ainda dependem de Node.js.

- [x] **Etapa A — Bootstrap nativo mínimo:** comandos `check`, `build` e `verify-pe`, sem subprocessos Node.js ou linker externo durante o uso, apenas para o subconjunto documentado (P1.8; testes locais Linux, sem execução Windows).
- [x] **Etapa B1 — Primeiro emissor real restrito (P1.9):** cabeçalhos PE32+, seções, imports e instruções x86-64 de aritmética e variáveis em runtime gerados programaticamente; testes estruturais locais sem execução Windows.
- [x] **Etapa B1.5 — Primeiro suporte a relocação para ASLR (P2.0):** blocos de relocação DIR64 ligados a endereços IAT absolutos, flags ASLR/NX no PE e testes locais de simulação de rebase; **não validado no carregador Windows real**.
- [ ] **Etapa B2 — Generalização do codegen:** implementar controle de fluxo, variáveis mutáveis, entradas dinâmicas, funções e ampliar a IR; validação funcional em Windows continua pendente.
- [ ] **Etapa C — Paridade funcional e integração:** portar as regras semânticas da linha principal, validar equivalência e usar uma CLI comum com o Studio.
- [ ] **Etapa D — Compilação autocontida validada:** comprovar build, execução e ABI no Windows real sem instalar Node.js, Go ou toolchains adicionais para o usuário.
- [ ] **Etapa E — Self-hosting:** implementar o compilador em Kavro e reproduzir seu próprio build com testes determinísticos de bootstrap.

**Nota:** compiladores nativos podem ser escritos em Go, C ou outras linguagens sem criar dependência de runtime dessas linguagens para o usuário. O objetivo posterior de self-hosting exige código-fonte do compilador escrito em Kavro; não está implementado.

## P0 — Confiabilidade semântica

- [ ] Integrar as correções semânticas à versão mais recente sem regressões de backend ou editor.
- [ ] Publicar especificação verificável de tipos, inferência, mutabilidade, conversões, escopos e erros.
- [ ] Executar regressões positivas/negativas e testes diferenciais após cada integração.
- [ ] Documentar divergências entre VM, codegen nativo e limites de segurança.

**Aceitação:** mesma versão do compilador com regras documentadas e testes reproduzíveis, sem divergências conhecidas não declaradas nos recursos suportados.

## P1 — Backend e compilação nativa

- [ ] Validar execução de executáveis Windows x86-64 em sistema real.
- [ ] Verificar chamadas, stack alignment, retornos e convenções ABI Windows.
- [ ] Validar ASLR/DEP e desenrolamento de pilha em Windows real, com `.pdata/.xdata` quando aplicável.
- [ ] Evoluir lowering IR/SSA, alocação de registradores e operações suportadas.
- [ ] Comparar benchmarks somente com programas equivalentes e dados reprodutíveis.
- [ ] Evoluir o bootstrap limitado para compilador autocontido com cobertura completa; a CLI e o Studio principais **ainda exigem Node.js**.

**Aceitação:** binários testados no Windows e métricas publicáveis com ambiente e metodologia documentados.

## P2 — Kavro Studio

- [ ] Unificar a interface Win32 experimental e o compilador/CLI revisados em uma distribuição.
- [ ] Validar abrir, salvar, abas, Unicode, IME, caret, seleção, undo/redo e scroll no Windows real.
- [ ] Implementar diagnósticos, Explorer e autocompletar com integração semântica.
- [ ] Executar testes end-to-end e de desempenho/fluidez de interface.

**Aceitação:** fluxos de edição e compilação reproduzíveis na distribuição unificada, com limites conhecidos registrados.

## P3 — Programação de sistemas

- [ ] Definir modelo de memória, ponteiros, alocação, tempo de vida e riscos.
- [ ] Definir FFI e interoperabilidade C com convenções de chamada explícitas.
- [ ] Investigar Assembly inline, depuração e inspeção de binários com testes representativos.

**Aceitação:** semântica implementada e validada para cada recurso anunciado.

## P4 — Ferramentas e distribuição

- [ ] Consolidar um único pacote versionado: compilador, IDE, CLI e pasta `TESTE/`.
- [ ] Implementar testes de CI, incluindo execução Windows em ambiente verificável.
- [ ] Fornecer instalador/CLI autocontida se o projeto justificar essa mudança arquitetural.
- [ ] Escolher licença, política de contribuições, compatibilidade e critérios de release.

**Aceitação:** pacote consistente com documentação, hashes, testes apropriados e política pública de distribuição.

## Política de atualização

Cada item concluído deverá indicar escopo, versão e tipo de evidência. **Cross-compilation, validação de PE32+ e execução real no Windows são coisas diferentes.** Um protótipo privado não equivale a uma funcionalidade baixável deste repositório. Nenhuma informação pessoal, credencial ou documentação de continuidade deve ser incluída no GitHub.

**Revisão P2.0 — 13/11/2026:** registrado o primeiro suporte experimental a `.reloc`, entradas DIR64 e sinalização ASLR/NX. Evidência limitada a compilação cruzada, inspeção PE e simulação de realocação. Ainda sem execução Windows, validação de ABI/unwind ou integração da IDE D2.1. As entregas locais não estão publicadas como binários neste repositório.
