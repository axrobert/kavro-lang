![Kavro — Programming Language](assets/kavro-banner.jpg)

# Kavro

**Linguagem experimental de programação de sistemas, com foco em código nativo, controle explícito e comportamento previsível.**

[Visão técnica](#visão-técnica) · [Estado do projeto](#estado-do-projeto) · **[Roadmap completo](ROADMAP.md)**

> **Em pesquisa e desenvolvimento.** Kavro não é uma linguagem estável, não está pronta para produção e ainda não possui uma distribuição pública completa neste repositório.

## Visão

Kavro investiga uma linguagem compilada voltada à programação de sistemas, combinando **simplicidade de expressão**, **semântica bem definida** e **proximidade com o código de máquina**. O Kavro Studio é o ambiente de desenvolvimento associado ao projeto, com foco em ferramentas offline e uma interface própria.

A identidade do Kavro não depende de copiar a sintaxe de uma linguagem existente. Propostas de sintaxe, tipos, memória e ferramentas precisam demonstrar utilidade, custo de implementação, compatibilidade e testes.

## Inspirações e identidade técnica

As referências do projeto são **HolyC, C e Assembly x86-64** — cada uma por razões diferentes:

| Referência | Inspiração ou direção técnica |
| --- | --- |
| **HolyC** | Experiência de desenvolvimento integrada e abordagem prática à programação de baixo nível. |
| **C** | Simplicidade estrutural, controle e interoperabilidade de sistemas como direções de projeto. |
| **Assembly x86-64** | Compreensão explícita da arquitetura e emissão experimental de instruções nativas para x86-64. |

Essas referências **não indicam compatibilidade, equivalência de desempenho ou suporte completo a seus recursos**. Em especial, geração de código x86-64 não significa que Assembly inline já esteja disponível.

## Visão técnica

O pipeline experimental considera estas etapas:

```text
Fonte .kvr
    │
    ▼
Análise léxica e sintática
    │
    ▼
Verificação de tipos e semântica
    │
    ▼
Representação intermediária (KIR)
    ├──► VM de testes
    └──► Backend nativo x86-64 (PE32+ / Windows)
```

A geração nativa ainda cobre apenas um subconjunto experimental da linguagem. A equivalência entre VM e backend nos recursos compartilhados é um objetivo de validação, não uma garantia atual.

## Estado do projeto

| Frente | Estado resumido |
| --- | --- |
| Sintaxe, inferência e sistema de tipos | Desenvolvimento e consolidação semântica |
| VM e testes de linguagem | Protótipos experimentais; testes de conformidade em evolução |
| Geração de executáveis x86-64 | Backend experimental, com validação nativa pendente |
| Kavro Studio | Interface e edição em evolução; validação Windows pendente |
| Memória, FFI e Assembly inline | Pesquisa e planejamento |

**Disponibilidade pública:** neste momento, este repositório disponibiliza documentação e planejamento. Os protótipos e builds mencionados não estão publicados aqui como releases estáveis nem devem ser presumidos disponíveis para download.

## Roadmap

O planejamento técnico detalhado, as dependências e os critérios de aceitação estão em **[ROADMAP.md](ROADMAP.md)**.

- **P0 — Confiabilidade:** semântica, tipos, diagnósticos e testes de regressão.
- **P1 — Compilação nativa:** backend x86-64, ABI, IR e benchmarks reproduzíveis.
- **P2 — Kavro Studio:** editor, usabilidade e validação no Windows real.
- **P3 — Programação de sistemas:** memória, ponteiros, interoperabilidade e Assembly inline.
- **P4 — Distribuição:** documentação, automação, empacotamento e critérios de release.

## Como acompanhar e testar

Acompanhe alterações pelo histórico do repositório e pelo [roadmap](ROADMAP.md). Quando houver builds públicos para avaliação, cada pacote deverá identificar sua versão e incluir uma pasta `TESTE/`, instruções de execução, casos de verificação e um modelo de relatório técnico.

**Segurança:** nunca execute binários de origem desconhecida nem desative proteções do sistema para testar versões experimentais.

## Licença

Ainda não foi selecionada uma licença de código aberto. A ausência de `LICENSE` não concede automaticamente permissão de copiar, modificar ou redistribuir código.
