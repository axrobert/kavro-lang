# Kavro — Roadmap técnico

[← Voltar ao README](README.md)

Este documento organiza **prioridades, dependências, entregas verificáveis e critérios de conclusão**. Não contém datas prometidas nem representa um anúncio de versão estável.

> **Estado público:** este repositório contém documentação e planejamento. Recursos descritos como protótipos experimentais não são releases públicas nem garantem disponibilidade ou funcionamento no ambiente do leitor.

## Visão geral

| Prioridade | Frente | Estado | Próxima evidência necessária |
| --- | --- | --- | --- |
| **P0** | Semântica e confiabilidade | Em desenvolvimento | Regressões e conformidade da linguagem |
| **P1** | Backend nativo x86-64 | Pesquisa e implementação experimental | Execução e ABI verificadas no Windows |
| **P2** | Kavro Studio | Protótipos em desenvolvimento | Testes de edição e compilação no Windows |
| **P3** | Programação de sistemas | Planejado | Modelo de memória e interoperabilidade especificados |
| **P4** | Testes, documentação e distribuição | Em evolução | Pipeline reproduzível de pacotes e validação |

**Como interpretar:** **Em desenvolvimento** significa trabalho ativo, não conclusão; **Pesquisa** significa alternativas em avaliação; **Planejado** não indica implementação disponível; **Validado** exige evidência reproduzível. Uma tarefa permanece desmarcada até que seus critérios estejam demonstrados na versão pertinente.

## P0 — Semântica e confiabilidade

**Objetivo:** tornar as garantias da linguagem explícitas e impedir que o compilador aceite programas que violem seu próprio sistema de tipos.

- [ ] Publicar a especificação de tipos primitivos, inferência, mutabilidade, escopo e retornos.
- [ ] Definir as regras de `any` e de retorno sem anotação, eliminando aceitação indevida de tipos incompatíveis.
- [ ] Formalizar conversões, overflow, comparação, valores booleanos e tratamento de erros.
- [ ] Criar testes positivos e negativos com diagnósticos verificáveis (arquivo, linha e causa).
- [ ] Executar testes de conformidade entre VM e binários nativos **somente** para recursos suportados pelos dois.
- [ ] Ampliar a cobertura de regressão e estabelecer fuzzing instrumentado quando a infraestrutura estiver pronta.

**Critério de aceitação:** regras documentadas; regressões reproduzíveis; testes automatizados aprovados no escopo declarado; divergências conhecidas registradas e não anunciadas como resolvidas.

**Dependência:** é a base para estabilizar P1 e para diagnósticos corretos em P2.

## P1 — Compilador nativo e desempenho

**Objetivo:** produzir e verificar executáveis x86-64 sem confundir geração estrutural de PE32+ com execução funcional comprovada.

- [ ] Executar programas representativos no Windows x64 e validar saída, código de retorno e comportamento de falhas.
- [ ] Verificar calling convention, alinhamento de pilha, passagem de parâmetros e ABI.
- [ ] Consolidar a representação intermediária executável e seu lowering para instruções nativas.
- [ ] Implementar e testar estratégia de alocação de registradores, incluindo casos de pressão de registradores.
- [ ] Expandir o subconjunto de linguagem suportado, preservando regras semânticas de P0.
- [ ] Investigar compilação autocontida e redução da dependência de Node.js no processo de build.
- [ ] Publicar benchmarks equivalentes e reproduzíveis, com ambiente, versões, comandos e resultados brutos.

**Critério de aceitação:** executáveis realmente testados no sistema-alvo, ABI validada, regressões automatizadas e resultados de benchmark sem extrapolações.

**Dependência:** P0 define o comportamento que o backend deve preservar; P4 fornece automação de distribuição e testes.

## P2 — Kavro Studio

**Objetivo:** oferecer uma experiência offline de edição e compilação confiável, sem sacrificar desempenho nem acessibilidade.

- [ ] Testar a interface nativa no Windows: abertura, múltiplas abas, edição, salvar, fechar e confirmação de mudanças.
- [ ] Validar Unicode, IME, seleção, teclado, caret, histórico de undo/redo e scroll.
- [ ] Organizar Explorer, diagnósticos e navegação de símbolos; avaliar conclusão de código com base na semântica real.
- [ ] Medir redimensionamento, consumo de recursos e comportamento com arquivos maiores.
- [ ] Revisar contraste, foco, espaçamento, atalhos e consistência das animações Aqua.
- [ ] Criar testes de integração e cenários end-to-end em Windows real.

**Critério de aceitação:** fluxos principais executados e documentados no Windows, com bugs conhecidos e roteiro de reprodução; testes unitários e cross-compilation isolados não são suficientes.

**Dependência:** pode evoluir em paralelo a P1, mas diagnósticos semânticos e integração de compilação exigem interfaces estáveis com P0.

## P3 — Recursos de programação de sistemas

**Objetivo:** ampliar o controle de baixo nível sem deixar regras de segurança ou tempo de vida implícitas.

- [ ] Especificar representação e manipulação de memória, ponteiros, alocação e tempo de vida.
- [ ] Definir interfaces de chamada e interoperabilidade com bibliotecas C/FFI.
- [ ] Avaliar Assembly inline e seus contratos de registradores, memória e efeitos colaterais.
- [ ] Planejar inspeção de binários, depuração e diagnósticos para recursos nativos.
- [ ] Testar casos adversariais e comportamento nos limites definidos pela especificação.

**Critério de aceitação:** especificação implementável, testes representativos de integração e documentação explícita dos recursos ainda não suportados.

**Dependência:** ABI e semântica de P0/P1.

## P4 — Testes, documentação e distribuição

**Objetivo:** garantir que cada artefato publicado corresponda exatamente ao que foi construído, testado e documentado.

- [ ] Automatizar builds, verificações de integridade e relatórios de versão reproduzíveis.
- [ ] Padronizar pacotes de avaliação com uma pasta `TESTE/`, instruções, casos de teste e formulário de feedback técnico.
- [ ] Separar pacote público de testes, código-fonte distribuível e documentação de continuidade restrita.
- [ ] Documentar suporte por sistema, matriz de compatibilidade e limitações por versão.
- [ ] Configurar CI para testes estáticos e validação no Windows, sem confundir CI com avaliação manual no alvo.
- [ ] Definir licença, política de contribuição, versionamento e requisitos de release antes da divulgação de código.

**Critério de aceitação:** pacote auditado e íntegro, testes identificados, limitações publicadas, arquivos públicos revisados e procedimento de reprodução claro.

**Dependência:** acompanha todas as fases; nenhuma entrega pública deve depender de documentação interna.

## Ordem prática de execução

1. **Primeiro:** fechar as garantias semânticas e as regressões prioritárias de P0.
2. **Em paralelo:** validar o editor Windows (P2) e consolidar o empacotamento de testes (P4).
3. **Depois:** avançar P1 com execução real e confirmação de ABI, usando a semântica estabilizada.
4. **A seguir:** definir e implementar P3 por incrementos pequenos, cada um com teste de integração.
5. **Continuamente:** atualizar documentação, riscos e estado de validação, sem transformar planos em funcionalidades prontas.

## Política de atualização do roadmap

- Uma caixa `[x]` exige evidência reproduzível ligada a uma versão identificada; não basta um protótipo ou compilação cruzada bem-sucedida.
- **Teste local**, **CI**, **execução nativa** e **revisão visual** são evidências diferentes e devem ser descritas separadamente.
- Mudanças significativas de sintaxe ou arquitetura devem apresentar alternativas, motivos, impactos e compatibilidade.
- Nenhum detalhe pessoal, credencial, log sensível ou documento restrito faz parte da documentação pública.

[← Voltar ao README](README.md)
