# Kavro

**Linguagem experimental de programação de sistemas e ambiente de desenvolvimento.**

> **Estado:** pesquisa e desenvolvimento. Kavro ainda não é considerado estável nem adequado para uso em produção.
>
> **Disponibilidade:** este repositório publica, por enquanto, documentação introdutória e o planejamento do projeto. O código-fonte completo, os builds e as distribuições de teste ainda não estão disponíveis publicamente aqui.

## Visão

Kavro explora uma linguagem compilada com foco em **semântica previsível, controle explícito, ergonomia e geração de código nativo**. O projeto também inclui o Kavro Studio, um ambiente offline de desenvolvimento com identidade visual própria.

As escolhas de sintaxe, tipos, memória e ferramentas são tratadas como decisões de engenharia: precisam ter justificativa técnica, exemplos e testes. O objetivo não é reproduzir outra linguagem, mas construir um conjunto coerente de características.

## Direções de desenvolvimento

- **Linguagem:** sintaxe enxuta, inferência de tipos com regras explícitas e diagnósticos úteis.
- **Compilador:** pipeline verificável, representação intermediária e backend nativo para x86-64.
- **Execução:** comportamento consistente entre interpretador/VM de testes e executáveis nativos, nos recursos compartilhados.
- **Studio:** editor e ferramentas offline com edição, navegação e feedback confiáveis.
- **Qualidade:** testes de regressão, validação no Windows real, segurança e pacotes reproduzíveis.

O trabalho com emissão nativa, VM e Studio permanece **experimental**. A existência de um protótipo não equivale a suporte completo da linguagem nem a uma release validada.

## Roadmap e acompanhamento

O planejamento detalhado está em **[ROADMAP.md](ROADMAP.md)**.

| Área | Situação |
| --- | --- |
| Semântica e confiabilidade do compilador | Em desenvolvimento |
| Backend nativo e desempenho | Pesquisa e implementação experimental |
| Kavro Studio | Protótipos em desenvolvimento |
| Programação de sistemas e interoperabilidade | Planejado |
| Testes, documentação e distribuição | Em evolução |

Os estados do roadmap indicam direção de trabalho, **não datas garantidas**. Funcionalidades só serão consideradas validadas após testes compatíveis com seu escopo.

## Como acompanhar o projeto

Acompanhe as mudanças na documentação deste repositório. Quando houver distribuição pública de testes, ela deverá identificar a versão e conter instruções, limitações conhecidas e uma pasta `TESTE/` com casos de verificação e formulário de feedback técnico.

Não execute binários experimentais não verificados nem desative proteções do sistema operacional para testá-los.

## Estado do código e licença

Este repositório ainda **não disponibiliza a implementação completa**. Um documento de roadmap não representa uma licença de distribuição nem garante a publicação de funcionalidades.

Não há uma licença de código aberto selecionada neste momento. Na ausência de um arquivo `LICENSE`, aplicam-se os direitos autorais padrão; não há permissão automática para copiar, redistribuir ou reutilizar código futuro.
