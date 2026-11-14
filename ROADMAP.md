# Kavro — Technical Roadmap

[Voltar ao README](README.md)

> **Estado (14/11/2026): P4.1p RC1 — desenvolvimento experimental privado.** Este repositório contém documentação. As implementações e medições locais descritas aqui não constituem releases públicas. Não recomendado para produção.

## Estado atual

| Frente | Progresso técnico local | Próxima etapa |
|---|---|---|
| Semântica e VM | Tipagem, diagnósticos, regressões, 13 tipos numéricos | Especificação e paridade completa |
| KIR e codegen | IR tipada, executor experimental, backend Windows x64 | Integração BigInt ao lowering e ABI |
| Otimização | Alocação, redução de instruções, slots wide e formatação | Benchmarks reproduzíveis e otimizações avançadas |
| Studio Aqua | Host WebView2, documentação offline, workspace e workers | LSP, debugger, validação Windows e E2E |
| Distribuição | CLI comum e instalador experimental | CI, assinatura, validação Windows, política de releases |
| Sistemas e ecossistema | Planejamento | Memória, ponteiros, FFI, stdlib, módulos e pacotes |

## Histórico de desenvolvimento local

| Marco | Entrega experimental |
|---|---|
| P0.1–P0.8 | Correções semânticas, matrizes VM, limites, CLI e inspeção PE |
| P0.9–P1.7 | Prévia Win32, abas, salvamento defensivo, cancelamento, diagnósticos e F8 |
| P1.8–P2.0 | Bootstrap Go restrito, emissor PE32+ independente, relocations e ASLR/NX estruturais |
| P3.x | Integrações de CLI, protótipos de runtime/IR e ferramentas; distribuição local |
| P3.8–P3.8b | Studio Aqua, componentes, workspace, documentação offline e autocompletar textual |
| P3.9–P3.9a | Workers, cancelamento e limites de prévia |
| P4.0a–P4.0d | Potência, BigInt de até 4096 bits, inteiros fixos, f32 na VM |
| P4.1a–P4.1b | Catálogo de backends, probe e executor KIR limitado |
| P4.1c–P4.1f | Codegen x64 via KIR, alocação, chamadas, otimização de instruções e recursão limitada |
| P4.1g–P4.1h | Inteiros de 8–64 bits com intervalos e operações unsigned verificadas |
| P4.1i–P4.1l | Aritmética 128 bits, fluxo de controle, ABI interna e integração dos dez inteiros fixos |
| P4.1m–P4.1n | Aritmética SSE2, conversões, resto binário e verificações de ponto flutuante |
| P4.1o | Impressão decimal shortest round-trip de floats, normalização otimizada |
| P4.1p | Núcleo C BigInt de 4096 bits isolado, testes diferenciais; integração KIR pendente |

## Cobertura numérica

- VM: i8/i16/i32/i64/i128, u8/u16/u32/u64/u128, f32/f64 e bigint limitado a 4096 bits.
- KIR nativo: 12/13 tipos com algum suporte em subconjuntos implementados; bigint ainda não compilável por esse caminho. Inteiros e floats podem coexistir, sem implicar paridade completa.
- BigInt: núcleo experimental de operações verificadas, conversões decimais e comparação já testado isoladamente; falta integração com runtime, lowering, orçamento e funções.

## Próximas etapas

- [ ] P4.1q — Integrar BigInt ao KIR e runtime nativo; primeiro subconjunto linear.
- [ ] Consolidar controle de fluxo, ABI, representação e otimização BigInt, além de ampliar a paridade dos backends.
- [ ] P4.2 — LSP, depurador e testes de interface.
- [ ] P4.3 — Memória, ponteiros, interoperabilidade C e Assembly.
- [ ] P4.4 — Biblioteca padrão, módulos e gerenciador de pacotes.
- [ ] P4.5 — CI, distribuição, assinatura, política de releases e testes Windows.
- [ ] Benchmarks competitivos comparáveis com C, C++, Rust e Zig, sem promessas de superioridade geral.
- [ ] Compilação autocontida e self-hosting.

## Independência e validação

O bootstrap Go é distinto do backend KIR; ambos permanecem experimentais. Atualmente o compilador KIR usa Node.js, Clang e LLD durante a compilação; executáveis produzidos para os subconjuntos implementados não exigem Node.js para executar. O compilador não é escrito em Kavro e não é self-hosted.

Testes locais, execução Linux com ABI Microsoft e compilação cruzada são evidências distintas de execução real no Windows. Validação de ABI/ASLR/DEP/unwind, instalador, interação GUI e CI Windows continuam pendentes. Benchmarks isolados não representam desempenho geral. Não há release pública, nem garantia de estabilidade/produtividade. A referência histórica de 33/58 (57%) não é uma auditoria atualizada e não será apresentada como progresso exato.

## Política de atualização

Registrar apenas avanços verificáveis com escopo e limitações; separar documentação pública das implementações privadas. Nenhum código privado, pacote interno, contexto de continuidade ou credencial deve ser incluído. Revisão documental proposta P4.1p (14/11/2026).
